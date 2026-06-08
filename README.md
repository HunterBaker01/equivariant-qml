# Equivariant VQC for Image Classification

A recreation of the model from *Image Classification With Rotation-Invariant Variational Quantum Circuits* (Sein et al.). It's a **C₄-equivariant variational quantum circuit** that classifies small binary images (`T` vs `L` shapes) and is invariant to 90° rotations by construction — rotating the input doesn't change the prediction, because the symmetry is built into the circuit rather than learned from data.

This is a learning project, built to get more comfortable with PennyLane and with equivariant model design. Not research-grade — just a clean, working reimplementation.

## How it works

The 16 pixels of a 4×4 image split into 4 *orbits* of pixels that map to each other under 90° rotation. The circuit respects this:

- **Encoding** — each pixel angle-encoded with `RX`, re-uploaded each layer.
- **Twirled rotations** — `Rot(α, β, γ)` parameters shared across all pixels in an orbit.
- **Equivariant entanglement** — CNOT pattern that commutes with the rotation symmetry.
- **Invariant readout** — average `PauliZ` over a full orbit.

Trained with Adam on MSE loss using PennyLane's `lightning.qubit` device.

## How to run

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab vqc_img_class.ipynb
```

Run the cells top to bottom — data generation, training, and evaluation.
