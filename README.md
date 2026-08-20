<p align="center"><strong>QEMU Camp 2026 — Experiment Repository</strong></p>
<p align="center"><a href="README.md">English</a> | <a href="README_zh.md">中文</a></p>

This is the professional-stage experiment repository for QEMU Camp 2026, focused on the GPGPU experiment direction, based on RISC-V.

## Online Documentation

| Direction | Experiment Manual | Hardware Datasheet / Guide |
|-----------|------------------|----------------------------|
| **GPGPU** | [GPU Experiment Manual](https://qemu.gevico.online/exercise/2026/stage1/gpu/gpu-exper-manual/) | [GPU Datasheet](https://qemu.gevico.online/exercise/2026/stage1/gpu/gpu-datasheet/) |

Full tutorial site: <https://qemu.gevico.online/>

## Experiment Direction

| Direction | Test Framework | Test Location | Scoring |
|-----------|---------------|---------------|---------|
| **GPGPU** | QTest (QOS) | `tests/qtest/gpgpu-test.c` | 17 tests -> 100 pts |

## Quick Start

### 1. Install Dependencies

```bash
# Ubuntu 24.04
sudo sed -i 's/^Types: deb$/Types: deb deb-src/' /etc/apt/sources.list.d/ubuntu.sources
sudo apt-get update
sudo apt-get build-dep -y qemu
```

### 2. Configure

```bash
make -f Makefile.camp configure
```

### 3. Build

```bash
make -f Makefile.camp build
```

### 4. Run Tests

```bash
# Run the GPGPU experiment
make -f Makefile.camp test-gpgpu

# Same as above
make -f Makefile.camp test
```

### 5. Submit

```bash
git add .
git commit -m "feat: implement ..."
git push origin main
```

CI will automatically build, run tests, calculate scores, and upload to the ranking platform. Scores of 0 are not uploaded.

## Experiment Details

### GPGPU Experiment (QTest)

Implement a PCIe GPGPU device with SIMT execution engine, DMA, and low-precision float support. Tests verify device registers, VRAM, kernel execution, and FP8/FP4 conversions.

- Device: `hw/gpgpu/` (PCI device `gpgpu`)
- Tests: `tests/qtest/gpgpu-test.c` (17 subtests)
- Run: `make -f Makefile.camp test-gpgpu`
- Docs: [Experiment Manual](https://qemu.gevico.online/exercise/2026/stage1/gpu/gpu-exper-manual/) | [GPU Datasheet](https://qemu.gevico.online/exercise/2026/stage1/gpu/gpu-datasheet/)

## Available Make Targets

```
make -f Makefile.camp help       # Show all targets
make -f Makefile.camp configure  # Configure QEMU
make -f Makefile.camp build      # Build QEMU
make -f Makefile.camp test-gpgpu # GPGPU experiment tests
make -f Makefile.camp test       # All tests
make -f Makefile.camp clean      # Clean build
make -f Makefile.camp distclean  # Remove build directory
```

## Scoring

- Tests that **fail** do not break CI — they simply result in a lower score.
- Scores of **0** are not uploaded to the ranking platform.
- Each push to `main` triggers a full CI run.

