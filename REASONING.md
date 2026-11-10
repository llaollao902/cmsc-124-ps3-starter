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
Replace this line with the rule behind this case's four fields.

## P09
Replace this line with the rule behind this case's four fields.

## P10
Replace this line with the rule behind this case's four fields.

## P11
Replace this line with the rule behind this case's four fields.

## P12
Replace this line with the rule behind this case's four fields.

## P13
Replace this line with the rule behind this case's four fields.

## P14
Replace this line with the rule behind this case's four fields.

## P15
Replace this line with the rule behind this case's four fields.

## P16
Replace this line with the rule behind this case's four fields.
