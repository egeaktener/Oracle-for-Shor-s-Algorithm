# Oracle-for-Shor-s-Algorithm
Qiskit implementation of a modular multiplier based on Beauregard's 2n+3 qubit architecture
# Quantum Modular Multiplier for Shor's Algorithm

This repository contains a Qiskit implementation of a doubly-controlled, in-place quantum modular multiplier: $|c\rangle |y\rangle |0\rangle \rightarrow |c\rangle |(a \cdot y) \pmod N\rangle |0\rangle$.

## Overview
This circuit forms the core arithmetic engine for the quantum subroutine of **Shor's factorization algorithm**. Specifically, it acts as the unitary operator $U_a$ used inside the Quantum Phase Estimation (QPE) loop to find the period of the modular exponential function, which is the necessary quantum step to factor large integers.

## Architecture and Reference
The quantum circuit designed and implemented in this project is strictly based on the optimized architecture detailed in the foundational paper:

> **"Circuit for Shor's algorithm using 2n+3 qubits"** > *Stéphane Beauregard* > [arXiv:quant-ph/0205095](https://arxiv.org/abs/quant-ph/0205095)

By leveraging Draper's Quantum Fourier Transform (QFT) addition, conditional boundary checking, and reversible uncomputation via controlled-SWAP gates, this implementation achieves the complex modular arithmetic required for Shor's algorithm while maintaining strict reversibility and qubit efficiency.

## Requirements
* Python 3.x
* Qiskit (v2.1+)
* Qiskit Aer (for simulation)
