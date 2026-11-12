# Part 3: Explain the Binding

## Which line captures the defining environment, and what is in that environment at the moment it's captured?

The defining environment is captured when `eval-expr` meets a `lambda` form. That branch passes its current `env` to `make-closure`:

    ((eq op 'lambda) (make-closure (second expr) (third expr) env))

`make-closure` stores it as the last element of the closure:

    (list :closure params body env)

Take the scope-discrimination case. The outer `let` uses `extend-env` to build the environment `((x . 2))`, and the `lambda` is evaluated while that environment is current, so the closure saves it. The saved environment contains `x` but not `f`, since `let` evaluates every initializer before it binds any name. The inner `(let ((x 100)) ...)` creates a new environment on top of the caller's, and the closure's saved copy stays as it was. When `(f 1)` runs, `apply-closure` extends the saved environment, not the caller's:

    (eval-expr body (extend-env params args captured-env))

The body `(+ x y)` is therefore evaluated in `((y . 1) (x . 2))`. It finds `x` as 2 and `y` as 1, so the result is 3.

## What would the scope-discrimination case return if apply-closure extended the caller's environment instead, and what would that make the language?

If `apply-closure` extended the caller's environment instead, the same case would return 101. At `(f 1)` the caller's environment is `((x . 100) (f . closure) (x . 2))`, so `lookup` finds 100 first and the body computes `(+ 100 1)`. The language would be dynamically scoped, because names would resolve by the call site and not by where the `lambda` was written, and the environment saved by `make-closure` would never be used.

## Why does the host CLISP need funcall where the toy language doesn't?
The host CLISP is a Lisp-2, so variables and functions use separate namespaces. If `f` is a variable containing a function, CLISP does not automatically use that variable’s value in function position; `(f 3)` searches for a function named `f`. Therefore, we must write `(funcall f 3)`. The toy language is a Lisp-1, so variables and functions share one namespace. Its evaluator evaluates `f` in operator position, obtains the stored closure, and applies it directly.
