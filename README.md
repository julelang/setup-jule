# Setup Jule

This repository provides official GitHub Actions for the [Jule programming language](https://jule.dev), designed to simplify continuous integration (CI) and automation workflows for Jule projects.
The actions included here make it easy to install Jule, configure the environment, and run common tasks such as building and testing directly in GitHub Actions pipelines.

## Usage

Here's a basic workflow usage that you can use:
```yml
name: Setup Jule
on: [push]
jobs:
  jule:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: julelang/setup-jule@v1
        with:
          version: latest
```

### Option: `version`

The version of Jule that will be used.

- `latest` and `current` for the latest supported release.
- `dev` for the latest commit of source code, the compileir is based on the IR version.
- `juleX.X.X` for the specific version of Jule.

> [!NOTE]
> The `latest` and `current` options do not point to the most recently released version immediately.\
> So, when a new Jule version is released, it may take some time for the `latest` and `current` options to point to the new version.

> [!WARNING]
> Version support is guaranteed for `jule0.1.7` and later.\
> Older versions may be specified, but support is not guaranteed.

#### Targets

The Jule compiler to be installed is determined based on the GitHub Actions runner.\
For example, with the `ubuntu-latest` and `amd64` combination, the `linux-amd64` target will be downloaded.\
If an unsupported target is detected, the installation will fail.

### Option: `directory`

Directory where Jule will be downloaded.\
Using the local directory (`.`) is sufficient in most cases and it is the default value.

### Option: `add-to-path`

Whether to add Jule binaries to the PATH or not.\
The default and recommended value is `true`.

## Releases and Versioning

`setup-jule` follows a **major-oriented versioning** strategy:
* Each **major version** (for example `v1`) is a moving tag.
* The `v1` tag **always points to the latest released `v1.x.x` version**.
* When a new compatible release is published (such as `v1.2.3`), the `v1` tag is automatically updated to reference it.

### Why this is recommended

* **Automatic updates:** You get bug fixes and improvements without changing your workflow.
* **Stability guarantee:** Breaking changes are introduced only in a new major version (`v2`, `v3`, etc.).
* **Simpler workflows:** No need to pin exact patch versions unless you want to.

### Usage example

```yml
- uses: julelang/setup-jule@v1
```

This will always install the **latest stable Jule tools and compiler** compatible with major version 1.

### Pinning an exact version (optional)

If you need strict reproducibility, you may pin a specific version:

```yml
- uses: julelang/setup-jule@v1.2.3
```

In most cases, using a major tag (`v1`, `v2`, etc.) is strongly recommended.

## License

Source code is distributed under the terms of the BSD 3-Clause license. <br>
[See License Details](./LICENSE)
