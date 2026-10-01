# redos-rust

[![Docker-образы](https://img.shields.io/badge/Docker-images-2496ED?logo=docker&logoColor=white)](#образы)
![Стабильная и ночная версии Rust](https://img.shields.io/badge/Rust-stable%20%7C%20nightly-DEA584?logo=rust&logoColor=black)
![RED OS UBI 7 и 8](https://img.shields.io/badge/RED%20OS%20UBI-7%20%7C%208-red)

[🇺🇸 English](./README.md) · [🇷🇺 Русский](./README.ru.md)

## Образы

Эти образы основаны на `registry.red-soft.ru/ubi7/ubi:latest` и `registry.red-soft.ru/ubi8/ubi:latest` из [реестра контейнеров RED SOFT](https://registry.red-soft.ru/).

| Базовый образ РЕД ОС | Общий образ для сборки       | Стабильная версия Rust        | Ночная версия Rust             |
| -------------------- | ---------------------------- | ----------------------------- | ------------------------------ |
| UBI7                 | `hexq/redos-build-base:ubi7` | `hexq/redos-rust:ubi7-stable` | `hexq/redos-rust:ubi7-nightly` |
| UBI8                 | `hexq/redos-build-base:ubi8` | `hexq/redos-rust:ubi8-stable` | `hexq/redos-rust:ubi8-nightly` |

Теги `stable` и `nightly` остаются псевдонимами для `ubi8-stable` и `ubi8-nightly`.

Каждая пара stable/nightly использует общий образ для сборки с GCC, G++, Make, pkgconf, CMake 4.4.3, Ninja 1.13.2 и инструментами для rustup. В отдельном этапе используются официальные бинарные выпуски CMake и Ninja, если они запускаются в целевом UBI; иначе та же версия собирается из исходников. В финальный образ копируются только установленные инструменты из `/opt`. Общие образы пересобираются при изменении соответствующего UBI или `Dockerfile.base`. Ночные Rust-образы пересобираются ежедневно. Стабильные образы проверяются каждый день и пересобираются, если изменился манифест стабильного канала Rust, опубликованный общий образ или `Dockerfile.stable`. При ручном запуске рабочего процесса можно принудительно пересобрать стабильные образы с помощью параметра `force_stable`. Одни лишь обновления пакетов в репозиториях DNF не запускают пересборку.

```text
CMake:
    official binary
        ↓
    если совместим с target glibc → используем
        ↓
    иначе build from source
Ninja:
    official binary
        ↓
    если запускается → используем
        ↓
    иначе build from source
```

## Использование

```sh
docker pull hexq/redos-rust:ubi8-stable
docker run --rm \
  -u "$(id -u):$(id -g)" \
  -v "$PWD:/volume" \
  -e CARGO_HOME=/tmp/cargo \
  hexq/redos-rust:ubi8-stable \
  cargo build --release
```
