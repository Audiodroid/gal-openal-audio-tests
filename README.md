# gal-openal-audio-tests

pytest tests for OpenAL Soft's 3D audio. They check the rendered audio itself, not just API return values. OpenAL Soft's loopback device renders a scene into memory, and the tests analyse the samples (for example, which direction a source appears to come from).

Part of a learning project; overview and conventions are in the hub repo, [gal-ghost-audio-lab-hub](https://github.com/Audiodroid/gal-ghost-audio-lab-hub). The game used to learn the SDK is [gal-susurros-de-llorona](https://github.com/Audiodroid/gal-susurros-de-llorona).

Status: just started. There are no tests yet.

## Prerequisites

- git, a C++ compiler (on macOS: Xcode Command Line Tools, `xcode-select --install`), CMake
- Python 3. pytest and numpy will be added with the first tests, in a virtual environment (`.venv`, git-ignored).

## Get the code

```bash
git clone --recurse-submodules git@github.com:Audiodroid/gal-openal-audio-tests.git
```

If you cloned without `--recurse-submodules`, fetch the submodule afterwards:

```bash
git submodule update --init
```

## Build OpenAL Soft

OpenAL Soft is a git submodule in `extern/openal-soft`, pinned to release **1.25.2**. The same version is pinned in [gal-susurros-de-llorona](https://github.com/Audiodroid/gal-susurros-de-llorona), so the tests and the game use the same build. Build it outside the submodule, into `build/openal-soft` (git-ignored):

```bash
cmake -S extern/openal-soft -B build/openal-soft -DCMAKE_BUILD_TYPE=Release -DALSOFT_UTILS=OFF -DALSOFT_EXAMPLES=OFF -DALSOFT_INSTALL=OFF
```

```bash
cmake --build build/openal-soft --parallel
```

This produces `build/openal-soft/libopenal.dylib` (`.so` on Linux). The tests load that exact file with `ctypes`, by path. Do not rely on the system's library: macOS ships its own, older OpenAL framework, and a plain `find_library("openal")` could pick that one up without anyone noticing.

## Run the tests

To be added once there are tests.

## How this repo was created (from scratch)

1. Create the folder inside the hub directory and initialise git:
   ```bash
   cd gal-ghost-audio-lab-hub
   mkdir gal-openal-audio-tests && cd gal-openal-audio-tests
   git init -b main
   ```
2. Add a `CLAUDE.md` with a short description of the project, a `.gitignore` containing `build/`, `.venv/`, `__pycache__/`, `.pytest_cache/` and `.DS_Store`, and this README.
3. On github.com create an **empty** repo named `gal-openal-audio-tests` (no README, `.gitignore` or license).
4. Add OpenAL Soft as a submodule and pin it to the release tag:
   ```bash
   git submodule add https://github.com/kcat/openal-soft.git extern/openal-soft
   git -C extern/openal-soft checkout 1.25.2
   ```
   This records the exact commit in the repo. Update the pin later by checking out another tag in the submodule and committing the change. Keep it identical to the pin in `gal-susurros-de-llorona`.
5. Commit, connect and push:
   ```bash
   git add .
   git commit -m "Initial commit"
   git remote add origin git@github.com:Audiodroid/gal-openal-audio-tests.git
   git push -u origin main
   ```
