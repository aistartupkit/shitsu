# Contributing to Helm Debian Packaging

Thank you for your interest in contributing to the Debian packaging of Helm!

## Repository Purpose

This repository (`aistartupkit/shitsu`) is a **Debian packaging repository** for Helm. It contains only the Debian packaging files (in the `debian/` directory) and does not contain the Helm source code itself.

### Relationship to Upstream

- **Upstream Repository**: https://github.com/helm/helm
- **This Repository**: Debian packaging files only
- **Purpose**: To create Debian packages from upstream Helm releases

## DEP-14 Repository Layout

This repository follows [DEP-14](https://dep-team.pages.debian.net/deps/dep14/) standards:

### Branch Structure

- `debian/master` or `debian/sid`: Main packaging development
- `debian/<codename>`: Stable release packaging (e.g., `debian/bookworm`)
- `upstream`: Contains upstream source (when using git-buildpackage)
- `pristine-tar`: Delta files for pristine upstream tarballs

### Tag Structure

- `debian/<version>`: Debian package releases (e.g., `debian/3.19.0-1`)
- `upstream/<version>`: Upstream releases (e.g., `upstream/3.19.0`)

## How to Update Packaging

### For New Upstream Releases

1. Download the new upstream tarball:
   ```bash
   uscan --download-current-version
   ```

2. Import the new upstream version:
   ```bash
   gbp import-orig --pristine-tar ../helm-<version>.tar.gz
   ```

3. Update `debian/changelog`:
   ```bash
   dch -v <new-version>-1 "New upstream release"
   ```

4. Update build files if needed:
   - `debian/control`: Update dependencies
   - `debian/rules`: Update build flags or version strings
   - `debian/patches/`: Add any necessary patches

5. Build and test:
   ```bash
   gbp buildpackage
   ```

6. Commit and tag:
   ```bash
   git commit -a -m "Update to new upstream version <version>"
   gbp tag
   ```

### For Packaging Updates (Same Upstream Version)

1. Update `debian/changelog`:
   ```bash
   dch -i "Your change description"
   ```

2. Make your changes to `debian/*` files

3. Build and test:
   ```bash
   gbp buildpackage
   ```

4. Commit:
   ```bash
   git commit -a -m "Description of packaging change"
   ```

## Building Packages

### Using git-buildpackage

```bash
# Build for local testing
gbp buildpackage --git-ignore-new

# Build with all checks
gbp buildpackage
```

### Using dpkg-buildpackage

```bash
# Unsigned build for testing
dpkg-buildpackage -us -uc

# Signed build for upload
dpkg-buildpackage
```

### Using sbuild (Recommended for Clean Builds)

```bash
# Setup sbuild environment first
sbuild-update -udcar unstable

# Build package
gbp buildpackage --git-builder=sbuild
```

## Testing Changes

### Package Installation Test

```bash
# Install built package
sudo dpkg -i ../helm_<version>_<arch>.deb

# Verify installation
helm version
```

### Lintian Check

```bash
# Check package quality
lintian -i -I --show-overrides ../helm_<version>_<arch>.changes
```

## Submitting Changes

1. Fork this repository
2. Create a feature branch from `debian/master`
3. Make your changes following the guidelines above
4. Test your changes thoroughly
5. Submit a pull request with:
   - Clear description of changes
   - Justification for the change
   - Test results

## Getting Help

- **Debian Kubernetes Team**: team+kubernetes@tracker.debian.org
- **Debian Mentors**: https://mentors.debian.net/
- **Debian Go Packaging**: https://go-team.pages.debian.net/

## References

- [Debian Policy Manual](https://www.debian.org/doc/debian-policy/)
- [DEP-14](https://dep-team.pages.debian.net/deps/dep14/)
- [Debian Developer's Reference](https://www.debian.org/doc/manuals/developers-reference/)
- [Git-buildpackage Manual](http://honk.sigxcpu.org/projects/git-buildpackage/manual-html/gbp.html)
- [Helm Upstream](https://github.com/helm/helm)
