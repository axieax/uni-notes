Tautology - all rows in the corresponding logic table are true (regardless of truth assignment)

A |= B

- A entails B if whenever A is true, B is also true

Number of rows in truth table = 2 ^ (num unknowns)

Tute:

- myth => not mortal
- not myth => mortal and mammal
- not mortal or mammal => horned
- horned => magic

Convert from knowledge base to conjunctive normal form

- (myth => not mortal) and (not myth => mortal and mammal) and (not mortal, or mammal => horned) and (horned => magic)
- use **a => b** is the same as **not a, or b**
- (not myth or not mortal) and (myth or, mortal and mammal) and (mortal and not mammal, or horned) and (not horned, or magic)
- (not myth or not mortal) and (myth or mortal) and (myth or mammal) and (mortal or horned) and (not mammal, or horned) and (not horned, or magic)

Prove horned using a series of resolutions

- Proof by contradiction - assume not horned
- not horned and (mortal or horned)
  - not horned and mortal, or, not horned or horned
  - not horned and mortal
  - Therefore, mortal
- not horned and (not mammal, or horned)
  - (not horned and not mammal) or (not horned and horned)
  - not horned and not mammal
  - Therefore, not mammal
- mortal and (not myth or not mortal)
  - mortal and not myth, or mortal and no mortal
  - mortal and not myth
  - Therefore, not myth
- not myth and (myth or mammal)
  - (not myth and myth) or (not myth and mammal)
  - not myth and mammal
  - Therefore, mammal
- mammal and not mammal => contradiction
- Therefore, horned

Give all models that satisfy the knowledge base - truth table with 5 variables can be reduced to 3 variables since we know it is horned (ignore third predicate) and if it is horned it is magical (last predicate), so horned and magical variables can be ignored



Negating logic

$\neg \forall x \exist t Fool(p,x,t) = \exist x \forall t \neg Fool(p,x,t)$



