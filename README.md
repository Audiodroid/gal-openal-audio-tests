# gal-openal-audio-tests

pytest tests for OpenAL Soft's 3D audio. They check the rendered audio itself, not just API return values. OpenAL Soft's loopback device renders a scene into memory, and the tests analyse the samples (for example, which direction a source appears to come from).

Part of a learning project; overview and conventions are in the hub repo, [gal-ghost-audio-lab-hub](https://github.com/Audiodroid/gal-ghost-audio-lab-hub). The game used to learn the SDK is [gal-susurros-de-llorona](https://github.com/Audiodroid/gal-susurros-de-llorona).

Status: just started. There are no tests yet.

## How this repo was created (from scratch)

1. Create the folder inside the hub directory and initialise git:
   ```bash
   cd gal-ghost-audio-lab-hub
   mkdir gal-openal-audio-tests && cd gal-openal-audio-tests
   git init -b main
   ```
2. Add a `CLAUDE.md` with a short description of the project.
3. On github.com create an **empty** repo named `gal-openal-audio-tests` (no README, `.gitignore` or license).
4. Connect and push:
   ```bash
   git remote add origin git@github.com:Audiodroid/gal-openal-audio-tests.git
   git add . && git commit -m "Initial commit"
   git push -u origin main
   ```

## Dependencies

- **OpenAL Soft**, loaded from Python with `ctypes` (or `cffi`). Installed with Homebrew for now: `brew install openal-soft`. The formula is keg-only (macOS has its own OpenAL framework), so load the library by explicit path, `/opt/homebrew/opt/openal-soft/lib/libopenal.dylib`, otherwise Apple's older implementation may be used without anyone noticing.
- **Python 3, pytest, numpy**: not set up yet. A virtual environment and a `requirements.txt` will be added with the first tests.

## Run the tests

To be added once there are tests.
