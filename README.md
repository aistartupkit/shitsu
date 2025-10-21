# Debian Packaging for Helm

This repository contains Debian packaging files for [Helm](https://helm.sh), the Kubernetes package manager.

## Overview

Helm is a tool for managing Charts, which are packages of pre-configured Kubernetes resources. This repository provides the necessary packaging to create Debian packages for Helm, following Debian Policy and DEP-14 standards.

## Repository Structure

This repository follows the [DEP-14](https://dep-team.pages.debian.net/deps/dep14/) Git packaging repository layout:

- **debian/**: Contains all Debian packaging files
  - `control`: Package metadata and dependencies
  - `changelog`: Version history in Debian format
  - `rules`: Build instructions
  - `copyright`: Licensing information
  - `source/format`: Source package format
  - `watch`: Upstream version monitoring
  - `README.source`: Detailed packaging documentation
  - `gbp.conf`: Git-buildpackage configuration

## Branch and Tag Naming

Following DEP-14 conventions:

### Branches
- `debian/master` or `debian/sid`: Main development branch
- `debian/<release>`: Stable release branches (e.g., `debian/bookworm`)
- `upstream`: Upstream source branch
- `pristine-tar`: Pristine-tar delta files

### Tags
- `debian/<version>`: Debian package release tags
- `upstream/<version>`: Upstream release tags

## Building the Package

### Prerequisites

```bash
sudo apt-get install debhelper dh-golang golang-any
```

### Build Commands

```bash
# Build the package
dpkg-buildpackage -us -uc

# Or using git-buildpackage
gbp buildpackage
```

## Upstream Source

- **Homepage**: https://helm.sh
- **Repository**: https://github.com/helm/helm
- **License**: Apache 2.0

## Compliance

This packaging complies with:
- [Debian Policy Manual](https://www.debian.org/doc/debian-policy/) (version 4.6.2)
- [DEP-14](https://dep-team.pages.debian.net/deps/dep14/) Git packaging repository layout

## Maintainer

Debian Kubernetes Team <team+kubernetes@tracker.debian.org>

## References

- [Debian Policy](https://www.debian.org/doc/debian-policy/ch-scope.html)
- [DEP-14](https://dep-team.pages.debian.net/deps/dep14/)
- [Helm Documentation](https://helm.sh/docs)
