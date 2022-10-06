# Harmonic

> **Harmonic is pre-release and experimental.** Don't run it on machines you care about.

Harmonic is an opinionated, experimental Nix installer.

## Status

Harmonic is **pre-release and experimental**. It is not ready for you to use! *Please* don't use it on a machine you are not planning to oblierate!

Planned support:

* [x] Multi-user x86_64 Linux with systemd init
* [ ] Multi-user aarch64 Linux with systemd init
* [ ] Multi-user x86_64 MacOS
* [ ] Single-user x86_64 Linux with systemd init
* [ ] Single-user aarch64 Linux with systemd init
* [ ] Multi-user aarch64 MacOS
* [ ] Others...

## Installation Differences

Differing from the current official Nix installer scripts:

* Nix is installed with the `nix-command` and `flakes` features enabled in the `nix.conf`
* Harmonic stores an installation receipt (for uninstalling) at `/nix/receipt.json`

## Motivations

The current Nix installer scripts do an excellent job, however they are difficult to maintain. Subtle differences in the shell implementations, and certain characteristics of bash scripts make it difficult to make meaningful changes to the installer.

Our team wishes to experiment with the idea of an installer in a more structured language and see if this is a worthwhile alternative. Along the way, we are also exploring a few other ideas, such as:

* offering users a chance to review an accurate, calculated install plan
* keeping an installation receipt for uninstallation
* offering users with a failing install the chance to revert
* doing whatever tasks we can in parallel

So far, our explorations have been quite fruitful, so we wanted to share and keep exploring.

## Building

Harmonic is pre-release and we do not provide binaries at this time.

Since you'll be using Harmonic to install Nix on systems without Nix, the default build is a static binary.

Build it on a system with Nix:

```bash
nix build github:determinatesystems/harmonic
```

Then copy the `result/bin/harmonic` to the machine you wish to run it on.

## Running

Harmonic must be run as `root` or via `sudo`, as it needs to alter the system and cannot elevate privileges without significant complexity.

Install Nix with default options:

```bash
./harmonic
```

To observe verbose logging, either use `harmonic -V`, for extremely verbose trace logging use `RUST_LOG=harmonic=trace harmonic`.

Harmonic supports many of the options the current official Nix installer scripts. Review `harmonic --help` for details.