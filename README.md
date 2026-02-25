# Quantum Modular Multiplier for Shor's Algorithm

This repository contains a Qiskit function that takes in two positive integers $a, N \in \mathbb{Z}_+$ such that $a < N$ and $\gcd(a,N)=1$, and outputs the unitary gate below:

$$
U |c\rangle_1 |y\rangle_n = 
\begin{cases} 
|c\rangle_1 |(a \cdot y) \bmod N\rangle_n & \text{if } c=1 \text{ and } y < N \\
|c\rangle_1 |y\rangle_n & \text{otherwise}
\end{cases}
$$

where $n=\lceil \log_{2}(N) \rceil$.

This gate forms the core component of the quantum subroutine of **Shor's factorization algorithm**. Specifically, it acts as the unitary operator $U_a$ used in the Quantum Phase Estimation procedure to determine the order of $a \bmod N$, which is the necessary quantum step to factor integers efficiently.

## Reference
The quantum circuit constructed in this project is based on the paper:

> **"Circuit for Shor's algorithm using 2n+3 qubits"** > *Stéphane Beauregard* > [arXiv:quant-ph/0205095](https://arxiv.org/abs/quant-ph/0205095)

