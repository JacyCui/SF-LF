# Software Foundations - Volumn 1 : Logical Foundations

This repository consists of two parts:

- All coq files from [Online Logic Foundations Textbook](https://softwarefoundations.cis.upenn.edu/lf-current/index.html) (version 6.5) with solutions for all formal exercises.
- A summary of proof tactics for quick reference.
- A summary of tacticals for quick reference.



## Proof Tactics Summary

|                      Usage                      |                           Meaning                            |
| :---------------------------------------------: | :----------------------------------------------------------: |
|                    `intros`                     |      Move hypotheses / variables from goal to context.       |
|                  `reflexivity`                  | Finish the proof (when the goal looks like `e = e` or `e <-> e`). |
|                     `apply`                     |    Prove goal using a hypothesis, lemma, or constructor.     |
|                `apply ... in H`                 | Apply a hypothesis, lemma, or constructor to a hypothesis in the context (forward reasoning). |
|              `apply ... with ...`               | Explicitly specify values for variables that cannot be determined by pattern matching<br />(you can also do this by using a theorem as a function and it's possible to use wildcards). |
|                    `apply I`                    |              Finish proof when goal is `True` .              |
|                     `simpl`                     |              Simplify computations in the goal.              |
|                  `simpl in H`                   |            Simplify computations in a hypothesis.            |
|                    `rewrite`                    | Use an equality or iff hypothesis (or lemma) to rewrite the goal. |
|               `rewrite ... in H`                | Use an equality or iff hypothesis (or lemma) to rewrite a hypothesis. |
|                   `symmetry`                    |      Changes a goal of the form `t = u` into `u = t` .       |
|                 `symmetry in H`                 |   Changes a hypothesis of the form `t = u` into `u = t` .    |
|                `transitivity y`                 | Prove a goal `x = z` by proving two new subgoals, `x = y` and `y = z` . |
|                    `unfold`                     | Replace a defined constant by its right-hand side in the goal. |
|                `unfold ... in H`                | Replace a defined constant by its right-hand side in a hypothesis. |
|              `destruct ... as ...`              | Case analysis on values of inductively defined<br /> types, propositions or logic connectives<br />or<br />destruct an existential hypothesis into its witness and proposition. |
|             `destruct ... eqn: ...`             | Specify the name of an equation to be added to the context,<br />recording the result of the case analysis. |
|   `destruct H`<br />where<br />`H` is `False`   |       Finish the proof when a hypothesis is `False` .        |
|             `induction ... as ...`              | Induction on values of inductively defined types or propositions. |
|             `injection ... as ...`              | Reason by injectivity on equalities between values of inductively defined types. |
|                 `discriminate`                  | Reason by disjointness of constructors on equalities between values of inductively defined types. |
| `assert (H: e)`<br />or<br /> `assert (e) as H` |       Introduce a "local lemma" `e` and call it `H` .        |
|            `generalize dependent x`             | Move the variable `x` (and anything else that depends on it) from <br />the context back to an explicit hypothesis in the goal formula. |
|                    `f_equal`                    |     Change a goal of the form `f x = f y` into `x = y` .     |
|                     `split`                     | Change a goal of the form `g1 /\ g2` into two subgoals `g1` and `g2`<br />or<br />change a goal of the form `g1 <-> g2` into two subgoals `g1 -> g2` and `g2 -> g1` . |
|                     `left`                      |       Change a goal of the form `g \/ g2` into `g1` .        |
|                     `right`                     |       Change a goal of the form `g \/ g2` into `g2` .        |
|                    `exfalso`                    |                 Change the goal to `False` .                 |
|                  `exists ...`                   |     Choose a witness for an existential qualified goal.      |
|             `inversion ... as ...`              | Reason about all the different ways a inductively defined stuff<br /> could have been derived (doing work of `destruct`, `injection` and `discriminate`). |
|           `remember e as x eqn: ...`            | Replace all occurrences of the expression `e` by the variable `x` <br />and<br />add an equation `x = e` to the context. |
|                      `lia`                      | The `lia` tactic implements a decision procedure for integer linear arithmetic, <br />a subset of propositional logic and arithmetic. |
|                    `clear H`                    |           Delete hypothesis `H` from the context.            |
|                    `subst x`                    | Given a variable `x`, find an assumption `x = e` or `e = x` in the context,<br />replace `x` with `e` throughout the context and current goal, and clear the assumption. |
|                     `subst`                     | Substitute away all assumptions of the form `x = e` or `e = x` (where `x` is a variable). |
|              `rename ... into ...`              | Change the name of a hypothesis in the proof context<br />For example, if the context includes a variable named `x` , <br />then `rename x into y` will change all occurrences of `x` to `y`. |
|                  `assumption`                   | Try to find a hypothesis `H` in the context that<br />exactly matches the goal; if one is found, solve the goal. |
|                 `contradiction`                 | Try to find a hypothesis `H` in the context that is logically equivalent to `False`.  <br />If one is found, solve the goal. |
|                  `constructor`                  | Try to find a constructor `c` (from some `Inductive` definition in the current environment) <br />that can be applied to solve the current goal.<br />If one is found, behave like `apply c` . |
|                     `auto`                      | Solve goals that are solvable by any combination of `intros` and<br /> `apply` of hypotheses from the local context (by default). |
|              `auto ... using ...`               | Extend the hint database just for the purposes of one application of `auto`. |
|                  `congruence`                   | Finish the proof when you can finish the proof using `rewrite` and `discrimination`. |
|                   `eapply H`                    | Behave like `apply`, except delay of instantiation of quantifiers. |
|                  `eassumption`                  | Solves the goal if one of the premises matches the goal<br />up to instantiations of existential variables. |
|                     `eauto`                     | Work like `auto` except that it uses `eapply` and `eassumption`. |

### Tips

- You need to write `From Coq Require Import Lia.` to make `lia` available. 

    - If the goal is a universally quantified formula made out of

        - numeric constants, addition (`+` and `S`), subtraction (`-` and `pred`), and multiplication by constants (this is what makes it Presburger arithmetic),
        - equality (`=` and `<>`) and ordering (`<=` and `>`), and

        - the logical connectives `/\`, `\/`, `~`, and `->`,

        then invoking `lia` will either solve the goal or fail, meaning that the goal is actually false.  

    - If the goal is not of this form, `lia` will fail.

- About `auto` :

    - We can use `debug auto` to see where `auto` gets stuck.
    - If we want to see which facts `auto` is using, we can use `info_auto` instead.
    - `Hint Resolve T : core.` adds the assumption `T` to global hint database `core`.
    - `Hint Constructors c : core.` is a shorthand to do a `Hint Resolve` for all of the constructors from the inductive definition of `c`.
    - `Hint Unfold d : core.` so that `auto` knows to expand uses of `d`.
    - `Hint Transparent d: core.` so that `auto` knows definition of `d`.

- `info_eauto` shows us which tactics `eauto` uses in its proof search.

- `Proof with t` (where `t` is an arbitrary tactic) allows us to use `t1...` as a shorthand for `t1;t` within the proof.



## Tacticals Summary

|           Usage           |                           Meaning                            |
| :-----------------------: | :----------------------------------------------------------: |
|          `T;T'`           | First performs `T` and then performs `T'` on each subgoal generated by `T`. |
| `T; [T1 | T2 | ... | Tn]` | First performs `T` and then performs `T1` on the first subgoal generated by `T`, <br />then performs `T2` on the second subgoal, etc. |
|          `try T`          | `try T` is a tactic that is just like `T` except that, if `T` fails,<br />`try T` successfully does nothing at all (rather than failing). |
|        `repeat T`         | Keep applying `T` until `T` fails or until `T` succeeds but doesn't make any progress.<br />Be cautious that `repeat` may introduce infinite loop. |



