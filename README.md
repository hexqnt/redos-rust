# redos-rust

[![Docker images](https://img.shields.io/badge/Docker-images-2496ED?logo=docker&logoColor=white)](#images)
![Rust stable and nightly](https://img.shields.io/badge/Rust-stable%20%7C%20nightly-DEA584?logo=rust&logoColor=black)
![RED OS UBI 7 and 8](https://img.shields.io/badge/RED%20OS%20UBI-7%20%7C%208-red)

[🇺🇸 English](./README.md) · [🇷🇺 Русский](./README.ru.md)

## Images

These images are based on `registry.red-soft.ru/ubi7/ubi:latest` and `registry.red-soft.ru/ubi8/ubi:latest` from the [RED SOFT container registry](https://registry.red-soft.ru/).

| RED OS base | Shared build image           | Stable Rust                   | Nightly Rust                   |
| ----------- | ---------------------------- | ----------------------------- | ------------------------------ |
| UBI7        | `hexq/redos-build-base:ubi7` | `hexq/redos-rust:ubi7-stable` | `hexq/redos-rust:ubi7-nightly` |
| UBI8        | `hexq/redos-build-base:ubi8` | `hexq/redos-rust:ubi8-stable` | `hexq/redos-rust:ubi8-nightly` |

`stable` and `nightly` remain aliases for `ubi8-stable` and `ubi8-nightly`.

Each stable/nightly pair shares a build base with GCC, G++, Make, pkgconf, CMake 4.4.3, Ninja 1.13.2, and the tools needed by rustup. The tools stage uses the official CMake and Ninja binaries when they run on the target UBI; otherwise it builds the same version from source. Only the installed tools under `/opt` are copied into the final build base. The build bases are rebuilt when their UBI image or `Dockerfile.base` changes. The nightly Rust images are rebuilt every day. Stable images are checked daily and rebuilt when the Rust stable channel manifest, their published build base, or `Dockerfile.stable` changes. A manual workflow run can force a stable rebuild with the `force_stable` input. Updates to packages in the DNF repositories alone do not trigger a rebuild.

## Usage

```sh
docker pull hexq/redos-rust:ubi8-stable
docker run --rm \
  -u "$(id -u):$(id -g)" \
  -v "$PWD:/volume" \
  -e CARGO_HOME=/tmp/cargo \
  hexq/redos-rust:ubi8-stable \
  cargo build --release
```
