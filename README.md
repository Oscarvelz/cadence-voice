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
