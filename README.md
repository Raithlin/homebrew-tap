# Metcalfe Software Homebrew tap

Install [GHA](https://github.com/Raithlin/gha) on macOS (Apple Silicon or Intel):

```sh
brew install --cask raithlin/tap/gha
```

Homebrew clones this repository automatically. `Casks/gha.rb` selects the
released archive for your Mac and checks its SHA-256 before installation.
Git is needed for GHA's local repository workflows.

```sh
brew update
brew upgrade --cask gha
gha version --format json
```

Agent setup is separate and explicit: run `gha agent install` if wanted.
`gha update` refreshes compatible guidance; it never upgrades the executable.
Package installation, upgrades and removal leave agent files alone.

GHA's GoReleaser configuration generates `Casks/gha.rb` on releases, including
prereleases. The bootstrap cask uses the published v0.3.0-alpha archives and
checksums. See [distribution maintenance](https://github.com/Raithlin/gha/blob/master/docs/package-distribution.md)
for credential setup, release recovery, Linux packages, and integrity checks.

The macOS CI installs the previous release fixture, upgrades to the current
cask, executes the binary, and verifies existing guidance survives. It also
checks the tap's current archive using Homebrew's SHA-256 validation. These
checks do not establish Apple notarization; the published binaries currently
have no Developer ID notarization.
