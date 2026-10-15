# My Parrot — voice engine packs

This repository hosts **release assets only**. It contains no application source.

My Parrot is a closed-source offline voice cloning and text-to-speech studio for Windows and
Linux. The app's own download carries the application and the engine's Python source, but not
the interpreter and libraries the engine runs on. Those are what live here.

## Why a separate public repository

Release assets on a private repository need an authenticated token to download. There is no way
to embed a credential in a shipped desktop app without handing it to whoever looks, so the files
a buyer's app fetches cannot live beside its source.

Model weights are unaffected. Those come from the vendor's own Hugging Face repositories.

## What is published here

The voice engine: Python 3.11, PyTorch 2.6 (processor build) and the rest of the libraries the
engine imports, assembled in the layout the app expects.

| Asset | Platform | Download | Unpacked | SHA-256 |
|---|---|---|---|---|
| `runtime-linux-cpu-1.0.0.tar.gz` | Linux, x64 | 381 MB | about 1.36 GB | `6f429431412204133833be375430bef40242b082552e1ba55251f36cf3522579` |

The app carries this address and this digest in its own manifest. It fetches the archive during
setup, verifies the SHA-256 before it unpacks anything, and reuses the result for every later
version of the app. Downloads resume, so a dropped connection does not start over.

A Windows pack is not published yet. It has to be built on Windows, because it needs Windows
wheels and a Windows interpreter, and it will appear here under the same tag once it is built.

## What is *not* here

- Application source code. My Parrot is closed source.
- Model weights. Those are fetched from the vendor's own Hugging Face repositories.
- Anything that phones home. Nothing here or in the app reports usage, and the app makes no
  network request at all after setup.

## The graphics-card pack

Version 1 runs on the processor. Rendering does not use a graphics card, and the app says so on
its Hardware screen.

A CUDA build was measured at roughly 6 to 8 times faster. It is not part of v1: it was cut
rather than promised, and no screen in the app offers it. If it ships, it will appear here as
its own asset.

## Licensing

The pack redistributes PyTorch and the Python libraries the engine imports, each under its own
licence. The complete inventory, with each component's licence, ships inside the app as
`THIRD-PARTY-NOTICES.txt`, generated from this pack so that list cannot drift from the files
actually shipped. The rest of the app is covered by `LICENSE.txt`.

If you believe something is missing from that list, please report it. An attribution gap is
worth fixing, and it is better to hear about one than to ship it.
