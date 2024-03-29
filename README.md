# Software Foundations - Volumn 1 : Logical Foundations

This repository consists of three parts:

- All coq files from [Online Logic Foundations Textbook](https://softwarefoundations.cis.upenn.edu/lf-current/index.html) (version 6.5) with solutions for all formal exercises.
- A summary of proof tactics for quick reference.
- A summary of tacticals for quick reference.

> You can move forward to [Programming Language Foundations](https://github.com/JacyCui/SF-LF) after completing Logical Foundations.



## Proof Tactics Summary

|                      Usage                      |                           Meaning                            |
| :---------------------------------------------: | :----------------------------------------------------------: |
|                    `intros`                     |      Move hypotheses / variables from goal to context.       |
|                  `reflexivity`                  | Finish the proof (when the goal looks like `e = e` or `e <-> e`). |
|             `replace (t) with (u)`              | Replace (all copies of) expression `t` in the goal by expression `u`, <br />and generates `t = u` as an additional subgoal. |
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
|            `induction ... using ...`            |         Utilize a non-standard induction principle.          |
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
|                    `clear H`                    |           Delete hypothesis `H` from the context.            |
|                    `subst x`                    | Given a variable `x`, find an assumption `x = e` or `e = x` in the context,<br />replace `x` with `e` throughout the context and current goal, and clear the assumption. |
|                     `subst`                     | Substitute away all assumptions of the form `x = e` or `e = x` (where `x` is a variable). |
|              `rename ... into ...`              | Change the name of a hypothesis in the proof context<br />For example, if the context includes a variable named `x` , <br />then `rename x into y` will change all occurrences of `x` to `y`. |
|                  `assumption`                   | Try to find a hypothesis `H` in the context that<br />exactly matches the goal; if one is found, solve the goal. |
|                 `contradiction`                 | Handle some ad hoc situations where a hypotheses is equivlent to `False`<br />or two hypotheses derive `False`. |
|                  `constructor`                  | Try to find a constructor `c` (from some `Inductive` definition in the current environment) <br />that can be applied to solve the current goal.<br />If one is found, behave like `apply c` . |
|                     `auto`                      | Solve goals that are solvable by any combination of `intros` and<br /> `apply` of hypotheses from the local context and `core` hint database. |
|                 `auto with db`                  |             Additionally using hints from `db`.              |
|                    `auto N`                     |            Search with depth `N` (default is 5).             |
|              `auto ... using ...`               | Extend the hint database just for the purposes of one application of `auto`. |
|                      `lia`                      | The `lia` tactic implements a decision procedure for integer linear arithmetic, <br />a subset of propositional logic and arithmetic. |
|                     `ring`                      |   Solve equations over the algebraic structures of rings.    |
|                     `field`                     |   Solve equations over the algebraic structures of fields.   |
|                  `congruence`                   | A decision procedure for equality with uninterpreted functions and other symbols. |
|                   `intuition`                   | Implement a decision procedure for propositional tautologies in  Coq's constructive logic. |
|                  `intuition T`                  | Apply `T` to all the unsolved goals that `intuition` generates. |
|                   `eapply H`                    | Behave like `apply`, except delay of instantiation of quantifiers. |
|                  `eassumption`                  | Solves the goal if one of the premises matches the goal<br />up to instantiations of existential variables. |
|                     `eauto`                     | Work like `auto` except that it uses `eapply` and `eassumption`. |
|                      `cbv`                      |          Call by value, reduce to beta-normal form.          |
|                     `idtac`                     | Identity tactic that always succeeds without changing the proof state. |
|               `extensionality x`                |       Use functional extentionality with variable `x`.       |

### Tips

- You need to write `From Coq Require Import Lia.` to make `lia` available. 

    - If the goal is a universally quantified formula made out of

        - numeric constants, addition (`+` and `S`), subtraction (`-` and `pred`), and multiplication by constants (this is what makes it Presburger arithmetic),
        - equality (`=` and `<>`) and ordering (`<=` and `>`), and

        - the logical connectives `/\`, `\/`, `~`, and `->`,

        then invoking `lia` will either solve the goal or fail, meaning that the goal is actually false.  

    - If the goal is not of this form, `lia` will fail.

    - For non-linear goals, `lia` will also either solve the goal or fail. But in this case, the failure does not necessarily mean that the goal is invalid -- it might just be beyond `lia`'s reach to prove because of non-linearity.

- About `auto` :

    - We can use `debug auto` to see where `auto` gets stuck.
    - If we want to see which facts `auto` is using, we can use `info_auto` instead.
    - `Create HintDb db.` creates a custom hint database named `db` aside from the global hint database `core`.
    - `Hint Resolve T : db.` adds the assumption `T` to database `db`.
    - `Hint Constructors c : db.` is a shorthand to do a `Hint Resolve` for all of the constructors from the inductive definition of `c`.
    - `Hint Unfold d : db.` so that `auto with db` (`core` is used by default) knows to expand uses of `d`. 
    - `Hint Transparent d: db.` so that `auto with db` (`core` is used by default) knows definition of `d`.
    - Technically creation of the database is optional; Coq will create it automatically the first time we use `Hint`.
    - Many of the important libraries have their own hint databases that you can tag in: `arith`, `bool`, `datatypes` (including lists), etc.R

- `info_eauto` shows us which tactics `eauto` uses in its proof search.

- `Proof with t` (where `t` is an arbitrary tactic) allows us to use `t1...` as a shorthand for `t1;t` within the proof.

- If more than one constructor can apply, `constructor` picks the first one, in the order in which they were defined in the `Inductive` definition. That might not be the one you want.

- The `congruence` tactic is able to work with constructors, even taking advantage of their injectivity and distinctness.



## Tacticals Summary

|         Usage          |                           Meaning                            |
| :--------------------: | :----------------------------------------------------------: |
|         `T;T'`         | First performs `T` and then performs `T'` on each subgoal generated by `T`. |
| `T; [T1｜T2｜...｜Tn]` | First performs `T` and then performs `T1` on the first subgoal generated by `T`, <br />then performs `T2` on the second subgoal, etc. |
|        `try T`         | `try T` is a tactic that is just like `T` except that, if `T` fails,<br />`try T` successfully does nothing at all (rather than failing). |
|       `repeat T`       | Keep applying `T` until `T` fails or until `T` succeeds but doesn't make any progress.<br />Be cautious that `repeat` may introduce infinite loop. |



