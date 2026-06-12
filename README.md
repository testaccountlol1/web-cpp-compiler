# all-working

This repository contains a minimal C++ sample program and GitHub Actions workflows to build it on Windows, Linux, and macOS.

## What this repo does

- `main.cpp` is a small cross-platform sample program.
- `all-working/.github/workflows/win.yaml` builds a Windows executable and uploads `program-win.zip`.
- `all-working/.github/workflows/linux.yaml` builds a Linux executable and uploads `program-linux.tar.gz`.
- `all-working/.github/workflows/mac.yaml` builds a macOS executable and uploads `program-mac.tar.gz`.

## Triggering builds

- Push to the `win` branch to run the Windows workflow.
- Push to the `linux` branch to run the Linux workflow.
- Push to the `mac` branch to run the macOS workflow.
- Each workflow also supports manual dispatch from GitHub Actions.

## Notes for Windows distribution

- The workflow packages the built `program.exe` into `program-win.zip`.
- Windows Defender / SmartScreen may still warn about unknown unsigned apps.
- The best way to avoid that warning is to sign the executable with a valid code signing certificate.
- If you want a truly portable Windows release, use the Windows workflow and distribute the zip artifact.

## Using a real project

If you want to build a different C++ project, replace `main.cpp` with your own source files and adjust the `cl.exe` / `g++` / `clang++` commands in the workflow files.

## Build commands used by the workflows

- Windows: `cl.exe /EHsc /std:c++17 /O2 main.cpp /Fe:program.exe`
- Linux: `g++ -O3 -std=c++17 main.cpp -o program`
- macOS: `clang++ -O3 -std=c++17 main.cpp -o program_mac`
