# Cadence voice package: Parakeet TDT 0.6B v2 (int8)

Files for Cadence's optional "High accuracy" microphone engine. Cadence downloads them only when the user asks for it,
keeps them on the device, and runs them in the browser. No audio leaves the device.

- Model: NVIDIA **parakeet-tdt-0.6b-v2**, licensed **CC-BY-4.0** (https://huggingface.co/nvidia/parakeet-tdt-0.6b-v2).
- ONNX int8 conversion: istupakov/parakeet-tdt-0.6b-v2-onnx, packaged by ysdede/parakeet-tdt-0.6b-v2-onnx (see ATTRIBUTION-upstream.md).
- Changes here: the int8 encoder is split into parts under 100 MB (byte split; joined in order it is byte-identical,
  SHA-256 in manifest.json). Nothing else is changed.
- Runtime: onnxruntime-web 1.24.1 (MIT, Microsoft), files ort/ unchanged.
- License text: https://creativecommons.org/licenses/by/4.0/
