# The 99-State Pisano Root-Shift Matrix
Author <B>VINEET NAMBI</B> (Independent Research)<BR><BR>
A Python implementation of a closed-loop, perfectly bijective Finite State Machine (FSM) operating on the domain of two-digit integers (01 to 99). 

This system utilizes a "Sum-and-Shift" recurrence relation governed by modulo 9 digital roots. It is mathematically isomorphic to the Fibonacci Q-matrix in a finite field, constrained temporally by the Pisano period of modulo 9 (π(9) = 24).

## 🧮 The Core Mathematics

The matrix operates on two-digit integers where `a` is the Tens digit and `b` is the Units digit.

* **Forward Formula (Sum-and-Shift):** The new Tens digit is the digital root of the sum of the current digits. The old Tens digit shifts to become the new Units digit.
* **Reverse Formula (Subtract-and-Shift):** Because the sequence is perfectly bijective, it can be mathematically rewound infinitely without storing historical states in memory.

## 🚀 Features & Topological Properties

Every number from 01 to 99 falls into one of five isolated cyclic orbits ("Universes"):
* **Universe 11:** 24-step Grand Cycle
* **Universe 12:** 24-step Grand Cycle
* **Universe 13:** 24-step Grand Cycle
* **Universe 33:** 8-step harmonic sub-cycle (multiples of 3)
* **Universe 99:** 1-step fixed-point singularity

**Key Mathematical Constants:**
* **1287 Universal Sum:** The sum of all elements in any 24-step cycle is always 1287 (which factors to 9 × 11 × 13).
* **53.625 Statistical Skew:** The arithmetic mean of the Grand Cycles is skewed upward from 50 due to the "Ghost of 9" rule in digital root arithmetic.

## 💻 Code Usage

This repository includes a lightweight, native Python implementation of the forward and reverse kinematics.

### The Core Logic

```python
def digital_root(n):
    if n == 0: return 0
    return 1 + (n - 1) % 9

def step_forward(n):
    tens = n // 10
    units = n % 10
    return digital_root(tens + units) * 10 + tens

def step_backward(n):
    tens = n // 10
    units = n % 10
    prev_units = (tens - units) % 9
    if prev_units == 0 and n != 0: prev_units = 9
    return units * 10 + prev_units
```

### Example: Running a Forward & Reverse Shift

```python
state = 85

# Move forward one step
next_state = step_forward(state)
print(f"Next: {next_state}") # Outputs: 48

# Rewind mathematically (Zero-Storage Undo)
prev_state = step_backward(next_state)
print(f"Previous: {prev_state}") # Outputs: 85
```

## 🛠️ Computer Science Applications

Because this algorithm perfectly conserves information without destructive operations, it has powerful applications in:
1. **Zero-Storage "Undo" Stacks:** Rewind application states infinitely using the inverse matrix without holding transaction logs in RAM.
2. **Pseudo-Random Number Generation (PRNG):** 24-step deterministic, non-linear randomizer loops with a fixed statistical mean.
3. **Collision-Free Sharding:** Distribute database payloads across isolated server clusters by hashing to specific Universes (U11, U12, U13).
4. **Self-Verifying Data Chains:** Lightweight blockchain alternative where corrupted packets instantly break the strict topological parent-child linkage.

## 📄 Academic Citation
If you use this mathematics or code in academic research or industrial applications, please cite the corresponding preprint:
> *VINEET NAMBI* (2026). "Topological Properties and Pisano Period of a Modulo 9 Sum-and-Shift Recurrence Matrix". https://zenodo.org/records/18959294

## ⚖️ License
This project is licensed under the MIT License - see the LICENSE file for details.