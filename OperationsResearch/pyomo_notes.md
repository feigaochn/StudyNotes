## Constraint()

Using tuple `(lb, func, ub)` as `rule` of constraint will be faster since it is the internal representation. Other `expr op val` has to convert to triple. `(l, f)` imply `l == f`.

Some useful constants
- `Constraint.Skip` to pass certain indices
- `Constraint.Feasible`
- `Constraint.Infeasible` always infeasible. Will raise exception to warn user.