# MyVoiceBox Local — GPU Acceleration Pack

This repository hosts **release assets only**. It contains no application source.

[MyVoiceBox Local](https://myvoicebox.dev) is a closed-source offline voice cloning
and text-to-speech studio. Its base install ships CPU-only PyTorch, which keeps the
buyer download small and works on every machine. GPU acceleration is an **optional
add-on** hosted here, because it is large (roughly 2 GB compressed) and only some
buyers want it.

## Why a separate public repository

GitHub Release assets on a private repository require an authenticated token to
download. There is no way to embed a credential in a shipped desktop app without
handing it to whoever looks, so the pack cannot live in the private source
repository. Model weights are unaffected — those come directly from the vendor's own
Hugging Face repositories.

## What is published here

| Asset | Contents | Approx. size |
|---|---|---|
| `gpu-pack-win-cu124-<version>.zip.001`, `.002`, …` | CUDA 12.4 build of PyTorch plus the NVIDIA runtime libraries it needs, assembled for the app's runtime layout | ~2 GB across parts |
| `gpu-pack-linux-cu124-<version>.tar.zst.001`, … | As above, for Linux | ~2 GB across parts |
| `manifest.json` | Pack id, version, part list, byte sizes and **SHA-256 per part** | small |

Parts are split below **1.5 GB** to stay under GitHub's 2 GB per-asset limit. The
app's installer downloads the parts, verifies each SHA-256, and refuses to install a
pack that does not match. Downloads are resumable, and a manual
"point me at a local folder" import path exists for buyers whose network blocks
these hosts.

## What is *not* here

- Application source code — the app is closed source.
- Model weights — those are fetched from the vendor's own Hugging Face repositories.
- Anything that phones home. Nothing in this repository or in the app reports usage,
  and the app makes no network request at all after setup.

## Licensing

The pack redistributes NVIDIA CUDA runtime libraries and cuDNN DLLs inside the
official PyTorch wheels. Those are redistributable under the NVIDIA CUDA Toolkit
EULA (Attachment A) and the cuDNN SLA (Supplement §2, "the runtime files `.so` and
`.dll`"), provided they are incorporated into an application with material
additional functionality and are not distributed as a standalone SDK. PyTorch itself
is BSD-3-Clause. The rest of the licence inventory ships in-app under
"Third-party notices".

Trademarks are the property of their respective owners. No NVIDIA or PyTorch
endorsement is claimed or implied.
