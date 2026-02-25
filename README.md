# Quantum Modular Multiplier for Shor's Algorithm

This repository contains a Qiskit function that takes in two positive integers $a,N\in \mathbb{Z}_+$ such that $a<N$, $gcd(a,N)=1$ and outputs the following unitary gate.

U |c>_1 |y>_n = |c>_1 |a y mod N>_n  if c=1 and y<N, else |c>_1 |y>_n
where $n=\lceil \log_{2}(N) \rceil$.

This circuit forms the core component of the quantum subroutine of **Shor's factorization algorithm**. Specifically, It acts as the unitary operator $U_a$ used within the Quantum Phase Estimation (QPE) procedure to determine the order of $a \bmod N$, which is the necessary quantum step to factor large integers.

## Reference
The quantum circuit constructed in this project is based on the paper:

> **"Circuit for Shor's algorithm using 2n+3 qubits"** > *Stéphane Beauregard* > [arXiv:quant-ph/0205095](https://arxiv.org/abs/quant-ph/0205095)


