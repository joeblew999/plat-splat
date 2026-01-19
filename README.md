# plat-splat

3D Gaussian Splat processing using [Polyform](https://github.com/EliCDavis/polyform).

## Prerequisites

- [xplat](https://github.com/joeblew999/xplat) - Cross-platform CLI tool
- Go 1.21+ (for building polyform)

## Quick Start

```bash
# First time setup - clone and build polyform
xplat task setup

# Run polyform editor
xplat task run
```

## Developer Workflows

### Fresh Clone (New Developer)

```bash
git clone https://github.com/joeblew999/plat-splat.git
cd plat-splat

# Generate project files (Taskfile.yml, process-compose.yaml, etc.)
xplat manifest bootstrap

# Clone polyform and build binary
xplat task setup

# Run polyform
xplat task run
```

### Clean Rebuild (Existing Developer)

```bash
# Clean build artifacts only (keeps source)
xplat task clean

# Rebuild binary (uses cached source)
xplat task ensure

# Or clean everything and start fresh
xplat task clean:all
xplat task setup
```

### Service Mode (Background Process)

```bash
# Start with process-compose (monitors and restarts on failure)
xplat process up -D

# View logs
process-compose attach

# Stop all processes
process-compose down
```

## End-User Workflows

### Simple Run

```bash
xplat task run
# Opens polyform editor at http://localhost:8080
```

### With Process Management

```bash
# Start with TUI (interactive process viewer)
xplat task up

# Or start in background
xplat task up:detached
```

## Available Tasks

| Task | Description |
|------|-------------|
| `setup` | First time setup - clone and build polyform |
| `run` | Run polyform editor |
| `up` | Start polyform with process-compose TUI |
| `up:detached` | Start polyform in background |
| `down` | Stop polyform |
| `clean` | Clean build artifacts |
| `clean:all` | Clean everything (.src, .bin, .data) |
| `ensure` | Ensure binary exists (build if needed) |
| `version` | Show polyform version |

## Project Structure

```
plat-splat/
├── xplat.yaml          # Manifest (dependencies, versions)
├── Taskfile.yml        # Generated tasks
├── process-compose.yaml # Generated process config
├── .src/               # Cloned source code (gitignored)
│   └── polyform/
├── .bin/               # Built binaries (gitignored)
│   └── polyform
└── .data/              # Runtime data (gitignored)
```

## Configuration

Edit `xplat.yaml` to customize:

```yaml
name: plat-splat
version: v0.1.0

dependencies:
  polyform:
    source: github
    repo: EliCDavis/polyform
    version: v0.35.0
    run_args: edit  # Polyform subcommand to run
```

## Health Checks

The process-compose configuration includes health checks:

```bash
# Manual health check
xplat task polyform:health
```
