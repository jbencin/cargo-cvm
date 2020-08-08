# Rust Crate Version Manager (CVM)

Crate Version Manager (CVM) helps maintain crate versions between git branches, which can be used by CI workflows to ensure rust crate versions are up-to-date.

CVM checks the current `Cargo.toml` file for `package` and `workspace.members`, iterates through all the crates in the workspace, checks if any workspace's `src/` directory has changed,
and then checks whether the version has been changed compared to a target branch, which defaults to `master`.

If the version has not been incremented compared to the target branch, and there have been changes to the source files, then CVM will either print a warning to the terminal or panic.

## Pre-Requisites

- Rust toolchain
- Git ^2.22.0

## Installation

```bash
cargo install cargo-cvm
```

## Getting Started

```bash
cargo cvm --help
```

```
cargo-cvm-cvm 

USAGE:
    cargo-cvm cvm [FLAGS] [OPTIONS]

FLAGS:
    -x, --check      Panic if the versions are out-of-date
    -f, --fix        Automatically fix the version if it is outdated. By default, this will bump the minor version,
                     unless otherwise specified by the --semver flag
    -h, --help       Prints help information
    -V, --version    Prints version information
    -w, --warn       Warn if the versions are out-of-date

OPTIONS:
    -b, --branch <branch>    Which branch to compare to the current. Will attempt to find the version in the target
                             branch and check if the version has been bumped or not.
    -s, --semver <semver>    Type of Semantic Versioning; i.e. `minor`, `major`, or `patch`. Defaults to `minor`

```

## Version Check

```bash
cargo cvm --check
```


This command will `panic!` if a workspace's version is out of date.


## Bump Version

```bash
cargo cvm --fix --semver [major, minor, or patch]
```

This command bumps the [semantic versioning](https://semver.org) of the crate given the type of semantic version provided, i.e. `major`, `minor`, or `patch`. By default, version updates use `minor`.

When `cargo cvm -f` is run on an already up-to-date crate version, it will have no affect.


## Warn Outdated Versions

```bash
cargo cvm --warn
```

Similar to `cargo cvm -x`, this command will print errors when versions are out of date, but in this case, the command will not `panic!` when a crate is outdated.