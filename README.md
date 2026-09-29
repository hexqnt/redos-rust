# redos-rust

[![Docker images](https://img.shields.io/badge/Docker-images-2496ED?logo=docker&logoColor=white)](#images)
![Rust stable and nightly](https://img.shields.io/badge/Rust-stable%20%7C%20nightly-DEA584?logo=rust&logoColor=black)
![RED OS UBI 7 and 8](https://img.shields.io/badge/RED%20OS%20UBI-7%20%7C%208-red)

[🇺🇸 English](./README.md) · [🇷🇺 Русский](./README.ru.md)

## Images

These images are based on `registry.red-soft.ru/ubi7/ubi:latest` and `registry.red-soft.ru/ubi8/ubi:latest` from the [RED SOFT container registry](https://registry.red-soft.ru/).

| RED OS base | Stable Rust                   | Nightly Rust                   |
| ----------- | ----------------------------- | ------------------------------ |
| UBI7        | `hexq/redos-rust:ubi7-stable` | `hexq/redos-rust:ubi7-nightly` |
| UBI8        | `hexq/redos-rust:ubi8-stable` | `hexq/redos-rust:ubi8-nightly` |

`stable` and `nightly` remain aliases for `ubi8-stable` and `ubi8-nightly`.

The nightly images are rebuilt every day. Stable images are checked daily and rebuilt when the Rust stable channel manifest, the corresponding UBI base image, or `Dockerfile.stable` changes. A manual workflow run can force a stable rebuild with the `force_stable` input. Updates to packages in the DNF repositories alone do not trigger a rebuild.

## Usage

```sh
docker pull hexq/redos-rust:ubi8-stable
docker run --rm -v "$PWD:/volume" hexq/redos-rust:ubi8-stable cargo build --release
```
