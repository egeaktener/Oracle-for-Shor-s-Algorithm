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

## How to Test the Circuit

You can build the conditional multiplier circuit for arbitrary co-prime integers $a$ and $N$ with the following code below. 

It sets the control bit $c=1$, initializes the $|y\rangle$ register to any integer you choose, applies the modular multiplier, and prints the measured result in decimal format.

### Testing Script

```python

a = 4
N = 15
y_val = 6  # The input value you want to multiply
c_val = 1  # Control bit (1 to activate, 0 to bypass)

# Build the Multiplier Block 
# (Assuming your main function is named build_conditional_multiplier)
multiplier_circuit = build_conditional_multiplier(a, N)
total_qubits = multiplier_circuit.num_qubits
n = math.ceil(math.log2(N))

# Set Up the test register
test_qc = QuantumCircuit(total_qubits)

# Initialize the control qubit (index 0)
if c_val == 1:
    test_qc.x(0)

# Initialize the y register (starts at index 1)
# Qiskit uses little-endian ordering, so we reverse the binary string
y_bin = bin(y_val)[2:] 
y_indices = [i + 1 for i, bit in enumerate(reversed(y_bin)) if bit == '1']

if y_indices:
    test_qc.x(y_indices)


# Apply the multiplier

test_qc.append(multiplier_circuit, range(total_qubits))

#  Read the Results
# Measure the probabilities of the y register (qubits 1 to n)
probs = Statevector(test_qc).probabilities_dict(range(1, n + 1), decimals=3)

# Filter out zero-probability states and convert binary keys to decimal
results = {int(k, 2): float(v) for k, v in probs.items() if v > 0}

print(f"Test Parameters: c={c_val}, y={y_val}, a={a}, N={N}")
print(f"Expected Math: ({a} * {y_val}) mod {N} = {(a * y_val) % N}")
print(f"Circuit Output (Decimal: Probability): {results}")
```


# Reference
The quantum circuit constructed in this project is based on the paper:

> **"Circuit for Shor's algorithm using 2n+3 qubits"** > *Stéphane Beauregard* > [arXiv:quant-ph/0205095](https://arxiv.org/abs/quant-ph/0205095)

