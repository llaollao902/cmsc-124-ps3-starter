## Environments and the Toy Evaluator

Replace this paragraph after your checks pass. Trace one form through your own
`eval-expr`, point to the line that captures the defining environment, say what
would change if application joined the arguments to the caller's environment
instead, and explain why the host CLISP needs `funcall` where the toy language
doesn't.

## Why does the host CLISP need funcall where the toy language doesn't?
The host CLISP is a Lisp-2, so variables and functions use separate namespaces. If `f` is a variable containing a function, CLISP does not automatically use that variable’s value in function position; `(f 3)` searches for a function named `f`. Therefore, we must write `(funcall f 3)`. The toy language is a Lisp-1, so variables and functions share one namespace. Its evaluator evaluates `f` in operator position, obtains the stored closure, and applies it directly.