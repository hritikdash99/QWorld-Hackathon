# ⚛️ Shor’s Algorithm — Quantum Factoring with Qiskit

[![Python](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/)
[![Qiskit](https://img.shields.io/badge/Qiskit-Latest-purple.svg)](https://qiskit.org/)
[![Quantum](https://img.shields.io/badge/Quantum-Computing-ff69b4.svg)](https://en.wikipedia.org/wiki/Shor%27s_algorithm)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> 🔑 A Qiskit implementation of **Shor’s Algorithm** to factorize integers using **Quantum Phase Estimation (QPE)** and **continued fractions**.
> Demonstration project — works best for small `N` like **15, 21, 35**.

---

## 🚀 Features

* ✅ Modular multiplication unitary construction
* ✅ Controlled modular exponentiation via powers of `a`
* ✅ Quantum Fourier Transform (QFT) & inverse QFT
* ✅ Quantum Phase Estimation (QPE) for **order finding**
* ✅ Classical post-processing with **continued fractions**
* ✅ Retries until **non-trivial factors** are found

---

## 🛠️ Installation

Make sure you have Python 3.8+ installed. Then:

```bash
git clone https://github.com/yourusername/shors-algorithm.git
cd shors-algorithm
pip install qiskit qiskit-aer
```

---

## ▶️ Usage

Run the script:

```bash
python shors_algorithm.py
```

Example output for **N = 15**:

```text
Attempting to factor N = 15 using Shor's algorithm (simulation).
Attempt 1: trying a = 2, n = 4, t = 8
Raw measurement counts (top 10): {'00010000': 412, '00100000': 388, ...}
Measured s = 16 (binary 00010000)
Found order r = 4 for a = 2
Non-trivial factors found: 3, 5
Result: (3, 5)
```

---

## ⚡ How It Works (High-Level)

```
|0...0> --H----●--------------------QFT†----MEASURE--> s/2^t  (gives r)
               |   
|1>     -------U^(2^j)-------------------------> |a^x mod N>
```

1. Choose random `a` with `1 < a < N`.
2. Build unitary: `U: |y⟩ → |a·y mod N⟩`.
3. Use **QPE** on `U` to estimate the order `r` where `a^r ≡ 1 (mod N)`.
4. Extract `r` using **continued fractions**.
5. Compute `gcd(a^(r/2) ± 1, N)` → yields non-trivial factors.

---

## 🧩 Common Issues

### ❌ `AerError: 'unknown instruction: c-unitary'`

✅ Fix: Force transpilation into standard gates:

```python
tqc = transpile(qc, simulator,
                basis_gates=simulator.configuration().basis_gates,
                optimization_level=1)
result = simulator.run(tqc).result()
```

---

## 📊 Limitations

* Works reliably only for **small numbers (N ≤ 35)** in simulation.
* Larger `N` needs more qubits → not practical without **real quantum hardware**.
* Random `a` may sometimes give trivial results → algorithm retries.

---

## 📚 References

* Shor, P. *Algorithms for quantum computation: Discrete logarithms and factoring* (1994).
* [Qiskit Textbook – Shor’s Algorithm](https://qiskit.org/textbook/ch-algorithms/shor.html)
* [IBM Quantum Docs](https://quantum-computing.ibm.com/)

---

## 🏆 Acknowledgements

Built with ❤️ using **Qiskit**. Inspired by Peter Shor’s groundbreaking work in quantum algorithms.

---

✨ If you like this repo, don’t forget to **star ⭐ it** and share!

---
