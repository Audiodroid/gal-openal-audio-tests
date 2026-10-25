# gal-openal-audio-tests

pytest suite that tests OpenAL Soft's rendered audio output (via the loopback device, with `ctypes`/`cffi`), not just its API return values.

Part of `gal-ghost-audio-lab-hub`; see `../CLAUDE.md` for the intention and how we work. The user writes the code, Claude guides. Setup and build steps are in `README.md`.

## Design

- Python + **pytest**, calling `libopenal` directly via `ctypes` or `cffi` (OpenAL has a plain C API, so no compile step on the Python side).
- Focus: test the **rendered audio output**, not API return values. Return values are only interesting when they can be matched against what is in the audio.
- Method: use OpenAL Soft's **loopback device** (`ALC_SOFT_loopback`) to render a scene into memory with no audio hardware, then analyze the samples.
  - **Ambisonic (B-format) output** (`ALC_SOFT_loopback_bformat`) gives W/X/Y/Z channels, so a source's direction, including elevation, can be asserted from the samples.
  - **Binaural/HRTF output** can be checked for inter-aural level and time differences (left/right). Elevation is subtler there (spectral cues).
- Prefer synthesized test signals (tones, noise) over recordings, so the expected result is known.

## Open questions

- Confirm loopback and B-format support at runtime (the game repo's probe program does this first).
- `ctypes` or `cffi` for the binding.
- Possible alternative: a small C++ renderer that writes WAV files, with pytest analysing them, if the Python binding becomes a burden.
