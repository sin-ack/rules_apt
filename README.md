# Bazel rules for .deb packages

A ruleset for downloading .deb packages, and including their contents as layers in container images.

**NOTE:** this ruleset is heavily inspired by [distroless](https://github.com/GoogleContainerTools/distroless)

## Features

- Pinning of the Debian snapshot to use
- Pinning of packages using a single lockfile
- Fine-grained control over packages (and their dependencies) to exclude
- Fine-grained control over package priorities
- Compatible with [rules_oci](https://github.com/bazel-contrib/rules_oci)

## Shortcomings

- There is no way to know which packages are already contained in previous layers, thus you have to be careful how you craft your package repository.

## Installation

From the release you wish to use:
<https://github.com/sin-ack/rules_apt/releases>
copy the Bzlmod snippet into your `MODULE.bazel` file.

To use a commit rather than a release, use `git_override`:

``` starlark
# Version is optional when git_override is used.
bazel_dep(name = "rules_apt", version = "")

git_override(
    module_name = "rules_apt",
    commit = "58f8cec394363be9a3d53e7fbcbfd9c3b408cd1e",
    remote = "https://github.com/sin-ack/rules_apt.git",
)
```

You can also use `local_path_override` if you intend to vendor the ruleset, but
don't do that.

## Usage

Usage of this ruleset involves three main steps:

1. [Generating a lockfile](docs/lockfile.md)
2. [Downloading packages](docs/repository.md)
3. [Consuming packages](docs/repository.md)

## Examples

- [rules_oci](examples/rules_oci)

## Public API Docs

- [apt_lockfile](docs/lockfile.md) Generate a lockfile.
- [apt_repository](docs/repository.md) Create a package repository.
- [snapshots.yaml](docs/snapshots_yaml.md) Specify snapshot versions.
- [packages.yaml](docs/packages_yaml.md) Specify packages to provide.
