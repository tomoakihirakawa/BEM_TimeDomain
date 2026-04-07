# BEM Time-Domain Solver

Nonlinear free-surface wave simulation using the Boundary Element Method (BEM)
with the Mixed Eulerian-Lagrangian (MEL) approach, accelerated by the Fast
Multipole Method (FMM).

## Features

- Fully nonlinear potential flow with free-surface tracking
- FMM-accelerated BIE solver (GMRES)
- Adaptive remeshing (split, collapse, flip, smooth)
- Runge-Kutta 4th order time integration
- Wave generation (piston/flap wavemaker, Stokes waves, solitary waves)
- Rigid body interaction (prescribed and free motion)
- Checkpoint/restart support
- JSON-based input files

## Build

Requires: C++23 compiler (GCC 12+ or Clang 16+), CMake 3.16+, LAPACK/BLAS.

```bash
mkdir build && cd build
cmake ..
make -j$(sysctl -n hw.logicalcpu)    # macOS
make -j$(nproc)                       # Linux
```

### CMake Options

| Option | Default | Description |
|--------|---------|-------------|
| `BEM_COMPILER` | `gcc` | `gcc` or `clang` |
| `USE_TETGEN` | `ON` | TetGen tetrahedralization (AGPL-3.0) |
| `FMM_M2L_METHOD` | `SimpleM2L` | FMM M2L translation method |
| `BEM_ENABLE_OPENMP` | `ON` | OpenMP parallelization |

## Usage

```bash
./main_time_domain path/to/settings.json
```

See `examples/goring1979/` for a sample input case (solitary wave generation).

## Directory Structure

```
├── lib/                  # Shared library (mesh, FMM, geometry)
│   ├── include/          # Header files
│   └── src/              # Source files
├── bem/
│   ├── core/             # BEM common (BVP solver, boundary conditions)
│   └── time_domain/      # Time-domain solver
├── third_party/tetgen/   # TetGen (optional, AGPL-3.0)
├── obj/                  # Sample mesh files
└── examples/             # Example input cases
```

## Related Packages

- [BEM_FreqDomain](https://github.com/tomoakihirakawa/BEM_FreqDomain) — Frequency-domain BEM
- [CableDynamics](https://github.com/tomoakihirakawa/CableDynamics) — Mooring line dynamics
- [BEM_for_Nonlinear_Waves](https://github.com/tomoakihirakawa/BEM_for_Nonlinear_Waves) — Integrated repository

## License

LGPL-3.0-or-later. See [LICENSE](LICENSE).

TetGen (optional) is licensed under AGPL-3.0. See `third_party/tetgen/LICENSE`.
