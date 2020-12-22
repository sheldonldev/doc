---
published_at: 2020-12-21
updated_at: 2020-12-21
description: Stanford
---

# Algorithms

## Asymptotic Analysis

- : Suppress constant factors and lower-order terms

### Big O Notation

- English Definion:

  - Let `T(n) = function on n = 1,2,3,…`, usually, the worst-case runningtime of an algorithm;
  - Q: When is T(n) = O(f(n)) ?
  - A: if eventually (for all sufficiently large n), `T(n)` is bounded above by a constant multiple of `f(n)`;

- Formal Definion:

  - `T(n) = O(f(n))` if and only if there exist constants `c, n_0 > 0` such that `T(n) <= c * f(n)` for all `n >= n_0`;
  - ⚠ Warning: `c`, `n_0` cannot depend on `n`;

### Relatives (Omega & Theta)

- Omega Notation: `T(n) = Omega(f(n))` if and only if there exist constants `c, n_0` such that `T(n) >= c * f(n)` for all `n >= n_0`;

- Theta Notation: `T(n) = Theta(f(n))` if and only if `T(n) = O(f(n))` and `T(n) = Omega(f(n))`;

  - Equivalant: there exist constants `c_1, c_2, n_0` such that `c_1 * f(n) <= T(n) <= c_2 * f(n)`;

- Little o Notation: `T(n) = o(f(n))` if and only if for all constant `c > 0`, there exist a constant `n_0` such that `T(n) =< c * f(n)` for all `n >= n_0`;

## Devide & Conquer Algorithms

### `O(n*log(n))` Algorithm for Counting Inversions

- Problem:

  - Input: `A = [1, 2, 3, ..., n]`, in arbitrary order;
  - Output: `number of inversions` (`number of pairs(i, j)` of array indices with `i < j` and `A[i] > A[j]`);

- Largest-possible number of inversions:

  - General: `n(n-1)/2`;

- Aproaches:

  - Brute-force: `O(n)`
  - Devide + Conquer, `O(n*log(n))`:
