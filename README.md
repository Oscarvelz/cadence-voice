# cadence-voice

Files for **Cadence**'s optional, opt-in "High accuracy" voice engine. Cadence downloads them only when the user turns the engine on, keeps them on the device, and runs speech recognition entirely in the browser. No audio leaves the device.

Served by GitHub Pages at `https://oscarvelz.github.io/cadence-voice/` (same origin as Cadence, so no CORS setup is needed).

## Contents

`models/parakeet-tdt-0.6b-v2-int8/`

| File | What it is |
| --- | --- |
| `encoder-model.int8.onnx.part00` … `part06` | int8 encoder, byte-split into 7 parts under 100 MB. Joined in order they are byte-identical to the original (SHA-256 in `manifest.json`, `encoderSha256`). |
| `decoder_joint-model.int8.onnx` | int8 decoder / joint network |
| `vocab.txt`, `config.json` | tokenizer vocabulary and model config |
| `ort/ort.bundle.min.mjs`, `ort/ort-wasm-simd-threaded.jsep.wasm` | onnxruntime-web 1.24.1, unchanged |
| `manifest.json` | file list with byte sizes and SHA-256 hashes (Cadence verifies every file) |

Total: 11 files, 686,507,150 bytes.

## Model and attribution

- **Model:** NVIDIA **Parakeet TDT 0.6B v2** (`nvidia/parakeet-tdt-0.6b-v2`), © NVIDIA, licensed under **[CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/)**. Model card: https://huggingface.co/nvidia/parakeet-tdt-0.6b-v2
- **ONNX int8 conversion:** [istupakov/parakeet-tdt-0.6b-v2-onnx](https://huggingface.co/istupakov/parakeet-tdt-0.6b-v2-onnx), packaged by [ysdede/parakeet-tdt-0.6b-v2-onnx](https://huggingface.co/ysdede/parakeet-tdt-0.6b-v2-onnx). See `models/parakeet-tdt-0.6b-v2-int8/ATTRIBUTION-upstream.md`.
- **Changes made here:** the int8 encoder file is split into parts under 100 MB so GitHub can host it. No weights were modified.

## Licenses

- Model weights (everything under `models/` except `ort/`): **CC-BY-4.0**. https://creativecommons.org/licenses/by/4.0/legalcode
- `ort/`: **onnxruntime-web 1.24.1**, © Microsoft Corporation, **MIT License**. https://github.com/microsoft/onnxruntime/blob/main/LICENSE

## Phonon read-aloud files (for Weekly)

`phonon/` mirrors the Phonon text-to-speech files that **Weekly**'s Read aloud uses, so they load from `https://oscarvelz.github.io/cadence-voice/phonon/` when Hugging Face is unreachable.

| Path | What it is |
| --- | --- |
| `phonon/model/model.q8.gguf.part0` … `part3` | Phonon 40M multilingual weights (q8), byte-split into 20 MiB parts; joined in order they are byte-identical to the original |
| `phonon/model/tokenizer.json`, `config.json`, `default-voice.safetensors` | tokenizer, model config, default voice |
| `phonon/voices/*.safetensors` | 50 Phonon catalogue voices |
| `phonon/files.json` | each file's original Hugging Face URL (Weekly's cache key), parts, byte sizes and SHA-256 of the whole file and of every part |

- **Model** (`phonon/model/`): by **Gradium**, **[CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/)** (non-commercial use only). Source: [gradium/phonon-40m-multilingual](https://huggingface.co/gradium/phonon-40m-multilingual) via [empyrealworks/Phonon-40M-multilingual](https://huggingface.co/empyrealworks/Phonon-40M-multilingual) @ `1191d231`. Only change: `model.q8.gguf` split into parts; no weights modified. See `phonon/LICENSE` and `phonon/NOTICE`.
- **Voices** (`phonon/voices/`): by **Gradium**, **Apache-2.0**. Source: [gradium/phonon-voices](https://huggingface.co/gradium/phonon-voices) @ `0ee17205`, unmodified. See `phonon/voices/LICENSE`.

The "Licenses" section above covers `models/` only.
