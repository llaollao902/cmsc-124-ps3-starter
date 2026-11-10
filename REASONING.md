# Reasoning for the Predictions Table

Write one entry under every heading below, then commit this file together with
`predictions.tsv`, before you run a case or open `tests/expected.tsv`.

Each entry names the rule that produces the four predicted fields for that
case. One to three sentences is enough. The grader checks structure only. It
does not judge quality, and it sets no word minimum.

After you run the cases, add a short correction under each case you predicted
wrongly. Say what you predicted, what CLISP printed, and which rule you
misread. Those entries belong in the correction commits.

## P01
Replace this line with the rule behind this case's four fields.

## P02
`''(+ 1 2)` heads with the special operator `quote`, since the reader turns the leading `'` into a `quote` form and the corpus's own quote only stores the form unevaluated. `quote` returns its argument untouched, so the list `(+ 1 2)` comes back as data and `+` never runs. That is a list with at least one element, so the kind is `cons`, and its three top-level elements make the length 3.

## P03
Replace this line with the rule behind this case's four fields.

## P04
The corpus's own quote only stores the form unevaluated, so the form being evaluated is the bare symbol `t`, an atom with no head, and the `operator` is `none`. A symbol evaluates to its binding, and `t` is bound to itself, so the value is `t`. It is a symbol that isn't `nil`, so the kind is `symbol`, and it is not a sequence, so the length is `none`.

## P05
Replace this line with the rule behind this case's four fields.

## P06
`(car '())` heads with the function `car`, so its argument is evaluated first, and the quote hands `car` the empty list unevaluated. `car` answers `nil` when handed the empty list, so the value is `nil`. That is the kind `null`, and since `nil` is the empty sequence, its length is 0 rather than `none`.

## P07
Replace this line with the rule behind this case's four fields.

## P08
`(if (null '()) 'empty 'full)` heads with `if`, a special operator that evaluates the condition and then only one branch. The condition `(null '())` is true because the quote hands `null` the empty list, so the `'empty` branch is evaluated, and `quote` returns the symbol `empty` untouched while `'full` never runs. A symbol that isn't `nil` has the kind `symbol`, and it is not a sequence, so the length is `none`.

## P09
Replace this line with the rule behind this case's four fields.

## P10
The form heads with `progn`, a special operator that evaluates its subforms in order and returns the value of the last one. `defvar` declares `*ps3-rate*` special, so rebinding it with `let` changes what `ps3-scale` sees for the duration of that `let`, however far away the function was written, and `(* 3 10)` gives 30. That is a whole number, so the kind is `integer`, and it is not a sequence, so the length is `none`.

## P11
Replace this line with the rule behind this case's four fields.

## P12
The form heads with `labels`, a special operator that binds `down` as a local function so that it can call itself. `(down 3)` recurses as `(cons 3 (cons 2 (cons 1 '())))`, where the base case `(= n 0)` returns the empty list and `cons` puts each `n` in front of the rest. That is a chain of cons cells, so the kind is `cons`, and its three top-level elements make the length 3 and the value `(3,2,1)`.

## P13
Replace this line with the rule behind this case's four fields.

## P14
`(mapcar (lambda (n) (* n n)) '(1 2 3))` heads with the function `mapcar`, so its arguments are evaluated first, where the `lambda` form gives an anonymous function and the quote hands over the list `(1 2 3)` unevaluated. `mapcar` applies that function to every element and collects the results, so 1, 2, and 3 become 1, 4, and 9. That is a list with at least one element, so the kind is `cons`, and its three top-level elements make the length 3 and the value `(1,4,9)`.

## P15
Replace this line with the rule behind this case's four fields.

## P16
The form heads with `let`, a special operator that runs its initializers, binds the variables, and only then evaluates the body. `factor` is an ordinary lexical variable, so the `lambda` captures the binding that held 2 when it was written, and the inner `let` that binds `factor` to 10 never reaches it. `(funcall f 3)` therefore computes `(* 3 2)`, which is 6, a whole number, so the kind is `integer` and the length is `none`.
