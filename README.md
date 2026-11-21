# How rare is a late crossing that an average from 2 can still detect?

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24412657.svg)](https://doi.org/10.5281/zenodo.24412657)

This result is now maintained in [quadratic-mertens-first-crossings](https://github.com/leecrossley/quadratic-mertens-first-crossings/tree/main/results/yokoi-mertens-late-crossing-density). This repository is archived and keeps its releases and DOI.

Take Yokoi's real quadratic fields, whose squarefree discriminants are $m^2+4$ for positive odd $m$. Keep the fields in which the prime-ideal Mertens product stays above its expected value through $X$, yet a running log-error integral starting at 2 eventually turns negative. Their fraction has a limiting value $p(X)>0$. Its rate of decay is

$$
 \log\log(1/p(X))=\log X+(2\sqrt{A_\ast}+o(1))\sqrt{\log X}.
$$

The same two terms hold for the fraction **among fields whose first dip is already known to be late**. They also hold in discriminant shells while the cutoff grows through the range stated in the theorem. [Definitions and frequency proof](PROOF.md)

The fields that pass both tests have a common error curve. Write $u=\log X$ and follow the product at $t=X\exp(w\sqrt u)$. After multiplying its log error by $\sqrt u$, the curve converges in conditional probability, uniformly, to

$$
 -\min(w,\ 2\sqrt{A_\ast}-w),\qquad 0\le w\le2\sqrt{A_\ast}.
$$

It descends to a minimum at $w=\sqrt{A_\ast}$ and then recovers. The positive area accumulated through $X$ converges to $A_\ast$. This constant is the minimum positive area required to stay above the benchmark indefinitely in the space of admissible prime splitting patterns. [Shape theorem](SHAPE.md) · [Definition of the constant](https://github.com/leecrossley/mertens-power-average-deadlines/blob/v1.0.0/SLOW-WEIGHTS.md)

The proof uses independent local prime signs, a joint limit for the residue and the entire running integral, and a comparison of high moments in individual discriminant shells. It leaves open whether every individual field has a polynomially bounded first crossing. [Moment estimates](MOMENTS.md) · [Prior work](PRIOR-WORK.md)

## Reproducing the checks

Run the following from the release directory with Python 3.10 or later. The script uses exact fractions and requires only the standard library.

~~~sh
shasum -a 256 -c SHA256SUMS
python3 -B check.py
~~~

It checks the Euler-factor change used in the absence-of-atoms proof, moments of a finite splitting model and the maximal-chain calculation for finite Boolean cubes. The limiting distribution and its shape are proved analytically. Three auxiliary inequalities were checked in Lean 4.33.1. Set NOTE to the absolute release directory and run the following from the [pinned Mathlib checkout](https://github.com/leanprover-community/mathlib4/tree/0df444a360eaa60ab8c11dca51a86af692955474).

~~~sh
lake env lean -R "$NOTE" "$NOTE/Density.lean"
~~~

[Exact verification output](evidence/check.txt) · [Lean output](evidence/lean.txt)
