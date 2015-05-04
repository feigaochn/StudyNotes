- a varialbe taking discoutinuous values

Q: `x = 0` or `l <= x <= u`

A: introduce *indicator variable* `y` as `y = 0` if `x = 0` or `y = 1` if `l <= x <= u`. So the problem modeled as
```ampl
var y binary;
x <= u * y;
x >= l * y;
```

- fixed cost

Q: Assuming the cost is a jump function
```
C(x) = 0            for x == 0
C(x) = k + c * x    for x > 0
```


A: Similarly introduce the indicator variable `y`, and the new cost function being
```ampl
C'(x,y) = k * y + c * x
var y binary;
s.t. x <= u * y;
```

Where `u` is a **sufficiently large upper bound** for `x`.


- either-or constraints

Q: **At least one** of `C1` and `C2` must hold.
```ampl
min obj: sum {j in J} c[j] * x[j];
s.t. C1: sum {j in J} a1[j] * x[j] <= b1;
s.t. C2: sum {j in J} a2[j] * x[j] <= b2;
s.t. C3 {j in J}: x[j] >= 0;
```

A: Choose a binary variable `y` and two large upper bound `M1` and `M2` such that `lhs(Ci) <= bi + Mi`, as tighter as better. Then model the problem.

```ampl
var y binary;
s.t. C1': sum {j in J} a1[j] * x[j] <= b1 + M1 * y;
s.t. C2': sum {j in J} a2[j] * x[j] <= b2 + M2 * (1-y);
```

- conditional constraints

Q: If `C1: A1*x <= b1` holds, then `C2: A2*x <= b2` must also hold.

A: sufficient small $e$, binary variable $y$, sufficiently large upper bound `M` on `C2`, sufficiently lower bound `L` on `C1`:
```ampl
C1': A1 * x >= b1 + e - L * y;
C2': A2 * x <= b2 + M * (1 - y);
```


- sos: special ordered sets

SOS1: out of a set of yes-no decisions, at most one decision variable can be yes; more generally, at most one of `0 <= x[i] <= u[i]` in constraint `sum a[i]*x[i] <= b[i]` takes non-zero value.

SOS2:  out of a set of nonnegative variables, at most two variables can be nonzero. In addition, the two variables must be adjacent to each other in a fixed order list. Usually arised in piecewise linear functions.


- resolving products of vairables

Q: `x1` and `x2` are both binary

A: forcing `y = x1 * x2` as
```ampl
var x1, x2, y binary;  # y == x1 * x2
y <= x1;
y <= x2;
y >= x1 + x2 - 1
```

Q: `d` binary; `l <= x <= u` continues

A: `y = d * x` as
```ampl
l * d <= y <= u * d;
l * (1 - d) <= d - x <= u * (1 - d)
```

- logical conditions: binary variables `a, b, c, ...`
	- at most `n` of `a, b, c, ...`
		- `a + b + c + ... <= N`
	- at least `n` of them
		- `a + b + c + ... >= N`
	- if `A` then `B`
		- `a <= b`
	- not `B`
		- `1 - b`
	- if `A` then not `B`
		- `a <= 1 - b`
	- if not A then B
		- `1 - a <= b`
	- A if and only if B
		- `a = b`
	- if A then B and C
		- `a <= b and a <= c` or `a <= (b+c)/2`
	- if A then B or C
		- `a <= b + c`
	- if B and C then A
		- `b + c - 1 <= a`
	- if B or C then A
		- `b <= a and c <= a` or `(b+c)/2 <= a`
	- if two or more of B, C, D or E, then A
		- `(b+c+d+e-1)/3 <= a`
	- if M or more of N from {B, C, D, ...}, then A
		- `(b+c+d+... -M+1)/(N-M+1) <= a`

- minimum values

Q: `y = min{X[i]: i}` where `X[i]` are bounded continues `L[i] <= X[i] <= U[i]`

A: let `d[i] = 1` iff `X[i]` is minimum
```ampl
param L_min := min {i} L[i];
s.t. {i}: L[i] <= X[i] <= U[i];
s.t. {i}: y <= X[i];
s.t. {i}: y >= X[i] - (U[i] - L_min) * (1 - d[i]);
s.t. : sum {i} d[i] = 1;
```

- logical AND

Q: `d = min {i in 1..n} d[i]` or equiv. `d = prod {i} d[i]` or equiv. `d = d[1] AND d[2] ... AND d[n]`; all binary

A: 
```ampl
s.t. {i}: 0 <= d <= d[i];
s.t. : d >= (sum {i} d[i]) - (n - 1);
```

- logical OR

Q: `d = max{i} d[i]`

A:
```ampl
s.t. {i}: d[i] <= d <= 1;
s.t. : d <= sum {i} d[i];
```

- disjunctions

Q: either `L1 <= x <= U1` or `L2 <= x <= U2`; `U1 < L2`

A: let binary `d = 0` if `L1 <= x <= U1`, else `d = 1`
```ampl
x <= U1 + (U2 - U1) * d;
x >= L1 + (L2 - L1) * d;
```


