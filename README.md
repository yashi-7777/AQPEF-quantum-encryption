# AQPEF: Adaptive Quantum Padding Encryption Framework

**Image-Content-Aware Quantum Security Optimization**

A three-stage quantum-classical hybrid pipeline for image encryption with unconditional maximum-strength security.

---

## Overview

AQPEF combines three quantum components in a single encryption pipeline — the first framework to do so:

| Component | Description | Qubits | Gates |
|-----------|-------------|--------|-------|
| **C1 — Quantum Padding** | Bell-state entanglement creates statistically uniform boundary pixels correlated with image corners | 16 | 24 |
| **C2 — QAOA Security Optimizer** | Multi-objective QAOA maximises entropy + NPCR + UACI to select the optimal chaos map per image | 4 | ~200 |
| **C3 — VQC Key Generator** | Golden-ratio (φ=1.6180) Rz phase VQC generates 256-bit quantum seed → NIST SP 800-90A Hash_DRBG keystream | 16 | 192 |

**Security-first design:** Encryption parameters are invariants (500 iterations, 100% pixels, 3 permutation cycles). The QAOA adapter maximises security for each image — it never reduces security in response to external conditions.

---

## Results (Simulation)

| Metric | AQPEF | AES-128 CBC | Ideal |
|--------|-------|-------------|-------|
| Shannon Entropy | 7.9877–7.9899 | 7.9971 | 8.0 |
| NPCR (%) | 99.57–99.71 | 99.603 | 99.609 |
| UACI (%) | 33.46–33.49 | 33.451 | 33.464 |
| VQC Lag-1 Autocorr | −0.0198 | −0.0021 | ~0 |
| NIST SP 800-22 | 15/15 | 15/15 | 15/15 |

---

## Installation

```bash
pip install qiskit==2.6.2 qiskit-aer==0.17 qiskit-algorithms==0.3.1 pycryptodome numpy pillow --break-system-packages
```

---

## Usage

```python
from src.encryption_engine import AQPEFEncryptionEngine
from PIL import Image
import numpy as np

engine = AQPEFEncryptionEngine()
image = np.array(Image.open('your_image.png').convert('L'))
encrypted = engine.encrypt(image)
decrypted = engine.decrypt(encrypted)
```

---

## Project Structure

```
src/
├── quantum_padding.py       # C1 — Bell-state quantum padding layer
├── qaoa_optimizer.py        # C2 — QAOA security optimizer (image-content-aware)
├── vqc_key_generator.py     # C3 — Golden-ratio VQC key generator
└── encryption_engine.py     # Main pipeline integrating all three components

experiments/
└── run_full_experiments.py  # Full benchmark suite (Lena, Baboon, Cameraman, Synthetic)

paper/
└── make_aqpef_paper_v3.js   # IEEE paper generator (Node.js + docx)
```

---

## Stack

- **Quantum:** Qiskit 2.6.2 + Qiskit-Aer 0.17 (noiseless statevector simulation)
- **Classical:** PyCryptodome 3.20 (AES-128 CBC), NumPy, Pillow
- **Simulation platform:** IBM Quantum compatible circuits (Eagle 127-qubit target)

---

## Citation

If you use AQPEF in your research, please cite:

```
Anonymous Authors (2026). AQPEF: Adaptive Quantum Padding Encryption Framework
with Image-Content-Aware Security Optimization. Under review.
```

---

## License

MIT License
