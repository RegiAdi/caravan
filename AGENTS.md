# Caravan - Development Guide

## Project Overview

| Field | Value |
|-------|-------|
| Name | Caravan |
| Type | C++/CMake desktop application |
| Core | SDL3 + OpenGL 3.3 rendering |
| Dependencies | SDL3, Glad (OpenGL loader) |

## Prerequisites

- Git
- CMake (3.10+)
- Ninja (build system)
- C++ compiler (MSVC/gcc/clang)
- vcpkg

## Development Setup

### Step 1: Clone and bootstrap vcpkg

```bash
git clone https://github.com/microsoft/vcpkg.git
cd vcpkg && ./bootstrap-vcpkg.sh
```

### Step 2: Set up environment

```bash
export VCPKG_ROOT=/path/to/vcpkg
export PATH=$VCPKG_ROOT:$PATH
```

### Step 3: Create project with vcpkg manifest

```bash
vcpkg new --application
vcpkg add port sdl3 glad
```

### Step 4: Configure with CMake presets

```bash
cmake --preset=default
```

### Step 5: Build and run

```bash
cmake --build build
./build/Caravan
```

## CMake Presets

This project uses CMake presets for vcpkg integration:

- `CMakePresets.json` - Shared build configuration (committed to source control)
- `CMakeUserPresets.json` - User-specific settings (not committed)

## Key Conventions

| Aspect | Convention |
|--------|------------|
| C++ standard | C++17 minimum |
| CMake | Manifest mode (`vcpkg.json`) |
| OpenGL | Core profile 3.3 |
| Glad include | `#include <glad/glad.h>` |
| Glad loader | `gladLoadGLLoader((GLADloadproc)SDL_GL_GetProcAddress)` |
| GL context | `SDL_GL_CONTEXT_PROFILE_CORE` for OpenGL 3.3+ |

## Dependency Management

| Command | Action |
|---------|--------|
| `vcpkg new --application` | Create manifest file |
| `vcpkg add port <pkg>` | Add a dependency |
| `vcpkg remove <pkg>` | Remove a dependency |
| `vcpkg list` | List installed packages |

## Build Commands

| Command | Action |
|---------|--------|
| `cmake --preset=default` | Configure |
| `cmake --build build` | Build |
| `./build/Caravan` | Run |
| `rm -rf build` | Clean build artifacts |

## Important Notes

- **Glad include path**: Use `#include <glad/glad.h>` (not `glad/gl.h`)
- **GL profile**: Set `SDL_GL_CONTEXT_PROFILE_CORE` for OpenGL 3.3+
- **CMakeUserPresets.json**: Not committed to source control (user-specific paths)
- **SDL3 status**: SDL3 is pre-release; prefer SDL2 if stability is required
