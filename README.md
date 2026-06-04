# hybrid-physics-computation-core
# Hybrid Physics Computation Core (Python & C++ Integration)

A high-performance simulation core built to optimize intensive mathematical and physical calculations by offloading heavy execution paths to native C++, wrapped seamlessly with a Python API.

---

## 🚀 Overview & Objective

In scientific computing, game development, or simulation systems, processing complex mathematical equations natively inside Python can hit a CPU performance bottleneck due to the Global Interpreter Lock (GIL) and runtime overhead.

This project addresses this limitation by moving the calculation core entirely to **C++** for raw execution speed, then creating dynamic Python bindings using **pybind11**. The result is an intuitive Python runtime environment (`main.py`) powered by a native C++ engine (`physics_engine.cpp`) under the hood.

---

## 🛠️ Tech Stack & Tools

* **Core Engine:** C++17 (Optimized Compiler Flags)
* **High-Level API & Orchestration:** Python 3.12 / Panda3D Framework
* **Binding Interface:** pybind11
* **Build System:** Setuptools / ExtModules

---

## 📦 Architecture & Workflow

The architecture is split into a low-level computation layer and a high-level representation layer:

1. **`physics_engine.cpp`**: Written in native C++, implementing strict, fast mathematical equations for positional and gravitational vector tracking over a designated timescale.
2. **`setup.py`**: The orchestration file compiling the C++ architecture using standard compilers (`g++` on Linux or `MSVC` on Windows) to yield a native platform extension (`.so` / `.pyd`).
3. **`main.py`**: The client application managing object loop animations, input processing, and scene graphs, calling the compiled C++ extension at every tick frame.

---

## 💻 Code Structure

### 1. C++ Core Module (`physics_engine.cpp`)
```cpp
#include <pybind11/pybind11.h>

namespace py = pybind11;

double calculate_position(double initial_velocity, double acceleration, double time) {
    return (initial_velocity * time) + (0.5 * acceleration * time * time);
}

PYBIND11_MODULE(core_physics, m) {
    m.doc() = "High-performance physics engine core written in C++";
    m.def("calculate_position", &calculate_position, 
          "Calculates 1D projectile position over time",
          py::arg("initial_velocity"), py::arg("acceleration"), py::arg("time"));
}
