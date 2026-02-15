# torch-builds-gfx906-rocm7.2

Prebuilt wheel packages of `torch` and `torchvision` compiled for:

* **ROCm 7.2**
* **AMD GPU architecture: gfx906 (Vega 20 – MI50 / MI60)**

This repository provides reproducible HIP-enabled builds of PyTorch specifically targeting gfx906, which is not always covered by official upstream binaries.

---

## Releases

Each GitHub Release contains:

* `torch-<version>+rocm7.2-gfx906-*.whl`
* `torchvision-<version>+rocm7.2-gfx906-*.whl`

Wheel filenames encode:

* Torch version
* ROCm version (7.2)
* Target architecture (gfx906)
* Python ABI tag (e.g. `cp310`, `cp311`, `cp312`)
* Linux x86_64

---

## Prerequisites

### Hardware

* AMD GPU with architecture **gfx906**

  * MI50
  * MI60

Verify architecture:

```bash
rocminfo | grep gfx
```

Expected:

```
Name: gfx906
```

---

### Software Requirements

You must have:

* Linux (tested on Arch Linux and Ubuntu)
* **ROCm 7.2 runtime installed**
* `amdgpu` kernel driver properly loaded
* Compatible Python version (matching the wheel tag)
* `pip >= 23.x` recommended

Check ROCm installation:

```bash
rocminfo
hipcc --version
```

---

### Important Compatibility Notes

* ROCm version **must be 7.2**
* Your system `glibc` must be compatible with the build environment
* These wheels are built **without CUDA**
* Do NOT mix with CUDA PyTorch builds
* Ensure no conflicting `torch` installation exists:

```bash
pip uninstall torch torchvision -y
```

---

## Installation

Download the required wheels from the **Releases** section and install:

```bash
pip install torch-<version>+rocm7.2-gfx906-*.whl
pip install torchvision-<version>+rocm7.2-gfx906-*.whl
```

Or:

```bash
pip install *.whl
```

---

## Verification

```python
import torch

print("Torch:", torch.__version__)
print("HIP:", torch.version.hip)
print("CUDA available:", torch.cuda.is_available())
print("Device:", torch.cuda.get_device_name(0))
```

Expected:

* `torch.version.hip` is not `None`
* `torch.cuda.is_available()` → `True`
* Device name corresponds to AMD Vega 20

---

## Build Characteristics

* HIP backend enabled
* Targeted specifically for `gfx906`
* Built against ROCm 7.2
* No CUDA support
* Optimized for Vega 20

---

## Scope & Limitations

These builds:

* Work only for **gfx906**
* Are not guaranteed to work on:

  * gfx90a
  * gfx1030
  * RDNA architectures
* Require matching ROCm runtime

If you need builds for other architectures or ROCm versions, open an Issue.

---

## Upstream Projects

These binaries are built from:

* PyTorch
* AMD ROCm

All original licenses apply.

---

## Reporting Issues

When reporting a problem, include:

* GPU model
* Output of `rocminfo`
* ROCm version
* Python version
* Full traceback/log

---

## Project Status

Maintained on demand.
New versions are added as needed.
