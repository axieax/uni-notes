# Planning

## Feature-based representation of actions

- Precondition of pick-up coffee (puc):
  - (RLoc = cs) and (not rhc)
- Rules for "location is cs":
  - Causal rules (how features change):
    - (RLoc' = cs) <- ((RLoc = off) and (act = mcc))
    - (RLoc' = cs) <- ((RLoc = mr) and (act = mc))
  - Frame rules (how features stay the same):
    - (RLoc' = cs) <- ((RLoc = cs) and (act != mcc) and (act != mc))
  - Note: RLoc' is future, RLoc is current; Feature/State <- Precondition
- Rules for "robot has coffee":
  - Causal rule: rhc' <- not rhc and (Act = puc)
  - Frame rule: rhc' <- rhc and (Act != dc)

## STRIPS representation of actions

- Action
  - Precondition
  - Effect

## WARPLAN

If an action undoes a goal, try moving this new action backwards through the plan before the action that achieved the first goal, and check that goals before and after are preserved

## GRAPHPLAN











