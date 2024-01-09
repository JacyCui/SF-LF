# Software Foundations - Volumn 1 : Logical Foundations

This repository consists of two parts:

- All coq files from [Online Logic Foundations Textbook](https://softwarefoundations.cis.upenn.edu/lf-current/index.html) (version 6.5) with solutions for all formal exercises.
- A summary of proof tactics for quick reference.



## Proof Tactic Summary

|                      Usage                      |                           Meaning                            |
| :---------------------------------------------: | :----------------------------------------------------------: |
|                    `intros`                     |       move hypotheses / variables from goal to context       |
|                  `reflexivity`                  | finish the proof (when the goal looks like `e = e` or `e <-> e`) |
|                     `apply`                     |     prove goal using a hypothesis, lemma, or constructor     |
|                `apply ... in H`                 | apply a hypothesis, lemma, or constructor to a hypothesis in the context (forward reasoning) |
|              `apply ... with ...`               | explicitly specify values for variables that cannot be determined by pattern matching<br />(you can also do this by using a theorem as a function and it's possible to use wildcards) |
|                    `apply I`                    |               finish proof when goal is `True`               |
|                     `simpl`                     |              simplify computations in the goal               |
|                  `simpl in H`                   |            simplify computations in a hypothesis             |
|                    `rewrite`                    | use an equality or iff hypothesis (or lemma) to rewrite the goal |
|               `rewrite ... in H`                | use an equality or iff hypothesis (or lemma) to rewrite a hypothesis |
|                   `symmetry`                    |       changes a goal of the form `t = u` into `u = t`        |
|                 `symmetry in H`                 |    changes a hypothesis of the form `t = u` into `u = t`     |
|                `transitivity y`                 | prove a goal `x = z` by proving two new subgoals, `x = y` and `y = z` |
|                    `unfold`                     | replace a defined constant by its right-hand side in the goal |
|                `unfold ... in H`                | replace a defined constant by its right-hand side in a hypothesis |
|              `destruct ... as ...`              | case analysis on values of inductively defined<br /> types, propositions or logic connectives<br />or<br />destruct an existential hypothesis into its witness and proposition |
|             `destruct ... eqn: ...`             | specify the name of an equation to be added to the context,<br />recording the result of the case analysis |
|   `destruct H`<br />where<br />`H` is `False`   |        finish the proof when a hypothesis is `False`         |
|             `induction ... as ...`              | induction on values of inductively defined types or propositions |
|             `injection ... as ...`              | reason by injectivity on equalities between values of inductively defined types |
|                 `discriminate`                  | reason by disjointness of constructors on equalities between values of inductively defined types |
| `assert (H: e)`<br />or<br /> `assert (e) as H` |        introduce a "local lemma" `e` and call it `H`         |
|            `generalize dependent x`             | move the variable `x` (and anything else that depends on it) from <br />the context back to an explicit hypothesis in the goal formula |
|                    `f_equal`                    |      change a goal of the form `f x = f y` into `x = y`      |
|                     `split`                     | change a goal of the form `g1 /\ g2` into two subgoals `g1` and `g2`<br />or<br />change a goal of the form `g1 <-> g2` into two subgoals `g1 -> g2` and `g2 -> g1` |
|                     `left`                      |        change a goal of the form `g \/ g2` into `g1`         |
|                     `right`                     |        change a goal of the form `g \/ g2` into `g2`         |
|                    `exfalso`                    |                  change the goal to `False`                  |
|                  `exists ...`                   |      choose a witness for an existential qualified goal      |
|             `inversion ... as ...`              | reason about all the different ways a inductively defined stuff<br /> could have been derived (doing work of `destruct`, `injection` and `discriminate`) |
|           `remember e as x eqn: ...`            | replace all occurrences of the expression `e` by the variable `x` <br />and<br />add an equation `x = e` to the context |



