# devcontainer-doctor

> Explain why your devcontainer rebuild takes eleven minutes.

**Status:** 🚧 In development

## Overview

Diagnose why a devcontainer build is slow or broken: layer cache misses, features that reinstall on every rebuild, mounts that defeat the cache.

## Features

- Times each build step and names the first layer that missed the cache, plus what invalidated it
- Flags `COPY` of the whole context ahead of dependency install — the classic cache killer
- Reports devcontainer features that reinstall every rebuild instead of baking into the image
- Checks mounts and volume config for bind mounts over dependency directories on macOS
- Validates `devcontainer.json` against the spec and warns on settings that force a full rebuild
- Prints a prioritized fix list with the estimated time each one gives back

## Stack

Go + `cobra` for the CLI, `docker/docker` client for BuildKit build traces and image history, `tidwall/jsonc` for reading `devcontainer.json` with comments.

## Usage

```bash
devcontainer-doctor diagnose --workspace . --rebuild --explain-cache
```

## License

MIT
