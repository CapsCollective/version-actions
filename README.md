# GitHub Actions for Version Management

This repo provides a collection of Github actions related to software version management, including:
- [`extract-version`](#extract-version)
- [`check-version-bump`](#check-version-bump)

See below for more details on usage of each action.

## `extract-version`

This action extracts a version number or string from a file by regex, utilising Ubuntu's grep regex.

### Inputs

#### `version-file`

**Required** The file containing the version number. Default `undefined`.

#### `version-regex`

**Required** The regex expression to capture the semantic version. Default `[0-9.\-A-z]*`.

### Outputs

#### `version-number`

The extracted version number (e.g. `1.0.0`).

#### `version-string`

The extracted version string (e.g. `v1.0.0`).

### Example usage

```yaml
- uses: CapsCollective/version-actions/extract-version@v1.0
  with:
    version-file: build_info.txt
    version-regex: version=\"\K[0-9.\-A-z]*
  id: extract-version

- run: echo ${{ steps.extract-version.outputs.version-string }}
```

## `check-version-bump`

This action check whether a [semantic version number](https://semver.org) has been bumped. If the `new-version` is behind or equal to the `old-version`, the action will fail with an `AntiquatedVersionError` highlighting the relevant issue.

### Inputs

#### `new-version`

**Required** The new semantic version. Default `v0.0.0`.

#### `old-version`

**Required** The old semantic version. Default `v0.0.0`.

### Example usage

```yaml
- uses: CapsCollective/version-actions/check-version-bump@v1.0
  with:
    new-version: v0.1.0
    old-version: v0.0.1
```