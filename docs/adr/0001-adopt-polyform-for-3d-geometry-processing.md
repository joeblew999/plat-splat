# ADR-0001: Adopt Polyform for 3D Geometry Processing

## Status

Accepted

## Date

2026-01-19

## Context

plat-splat requires robust 3D geometry processing capabilities for working with splat data and mesh operations. We need a library that can:

- Load and export multiple 3D file formats (GLTF, OBJ, PLY, STL, Gaussian Splat)
- Perform mesh transformations and processing
- Support procedural generation workflows
- Compile to WebAssembly for browser-based applications
- Integrate with Go-based tooling (xplat ecosystem)

## Decision

We will adopt [Polyform](https://github.com/EliCDavis/polyform) as our core 3D geometry processing library.

### Key Capabilities

**File Format Support:**
- GLTF, OBJ, PLY, STL for standard 3D formats
- Gaussian Splat (SPZ) format - directly relevant to splat processing
- Potree point clouds for large-scale point data

**Processing Features:**
- Immutable mesh processing with modularity
- Multi-threaded marching cubes implementation
- 2D-to-3D extrusion and triangulation
- Mesh optimization via voxelization
- SDF (Signed Distance Field) operations

**Architecture:**
- Written in Go (82% of codebase)
- Compiles to WebAssembly for browser deployment
- Node-based visual editor for procedural workflows
- Mathematical libraries (vectors, quaternions, noise, spatial structures)

## Consequences

### Positive

- **Native Go integration** aligns with xplat tooling and build systems
- **Gaussian Splat support** directly addresses our core use case
- **WebAssembly compilation** enables browser-based splat viewers/editors
- **Immutable design** promotes predictable, testable code
- **Active development** with comprehensive examples and documentation
- **Procedural workflow support** enables flexible content generation

### Negative

- Additional dependency to maintain and update
- Learning curve for team members unfamiliar with polyform's API
- May require contributing upstream fixes for edge cases

### Neutral

- Will need to establish patterns for integrating polyform with our existing codebase
- Documentation and examples will need to be created for our specific use cases

## References

- [Polyform GitHub Repository](https://github.com/EliCDavis/polyform)
- [Polyform Live Demo](https://elicdavis.github.io/polyform/)
