---
nav_order: 9
---

# Release notes

## Butane 0.14.0 (2022-01-27)

### Breaking changes

- Drop `TranslateBytesOptions.Strict` field; callers should fail on
  non-empty reports instead _(Go API)_

### Features

- Stabilize OpenShift spec 4.10.0, targeting Ignition spec 3.2.0
- Add OpenShift spec 4.11.0-experimental, targeting Ignition spec
  3.4.0-experimental
- Warn on incorrect partition numbers for reserved labels _(fcos, openshift)_
- Require `storage.files.contents.source` URLs to use `data` scheme
  _(openshift)_
- Re-enable automatic and manual resource compression _(openshift 4.10.0+)_
- Add `extensions` section _(fcos 1.5.0-exp, openshift 4.11.0-exp)_

### Bug fixes

- Correctly fail on validation warnings if `--strict` is specified
- Statically link official Linux binaries

### Misc. changes

- Roll back to Ignition spec 3.2.0 _(openshift 4.10.0)_
- Add deprecation warning for `rhcos` variant
- Add reserved partitions to `aarch64`/`ppc64le` `boot_device.mirror` layouts
  _(fcos, openshift)_

### Docs changes

- Improve getting-started instructions for running in container
- Document availability of `gs` URL scheme
- Correctly document availability of `compression` fields
- Correctly document `ignition` section as optional
- Add `with_mount_unit` `swap` support to migration guide _(fcos 1.4.0)_
- Document build process and contribution flow for release binaries


## Butane 0.13.1 (2021-08-04)

### Misc. changes

- Roll back to Ignition spec 3.2.0, since 3.3.0 support didn't make
  it into OpenShift 4.9. No 3.3.0 features were permitted in this
  config version, so this shouldn't break configs. _(openshift 4.9.0)_
- Send `--help` output to stdout
- Drop support for Go 1.13 and 1.14

### Docs changes

- Correctly snake-case `ignition.proxy` fields


## Butane 0.13.0 (2021-07-13)

### Features

- Stabilize Fedora CoreOS spec 1.4.0, targeting Ignition spec 3.3.0
- Add Fedora CoreOS spec 1.5.0-experimental, targeting Ignition spec
  3.4.0-experimental
- Stabilize OpenShift spec 4.9.0, targeting Ignition spec 3.3.0
- Add OpenShift spec 4.10.0-experimental, targeting Ignition spec
  3.4.0-experimental
- Support `none` filesystem format _(fcos 1.4.0+)_

### Bug fixes

- Correctly track input line/column in `kernel_arguments` section

### Misc. changes

- Deprecate `rhcos` 0.1.0 spec in favor of `openshift` variant
- Disable `kernel_arguments` section in favor of `openshift.kernel_arguments`
  _(openshift 4.9.0+)_
- Convert `ClevisCustom.Config`, `ClevisCustom.Pin`, `Link.Target`, and
  `Raid.Level` Go fields to pointers _(fcos 1.4.0+, openshift 4.9.0+)_

### Docs changes

- Document default value for Clevis `threshold`


## Butane 0.12.1 (2021-06-10)

### Bug fixes

- Disable automatic resource compression _(openshift 4.8.0,
  openshift 4.9.0-exp)_

### Misc. changes

- Fail if file compression specified _(openshift 4.8.0, openshift 4.9.0-exp)_


## Butane 0.12.0 (2021-06-08)

### Features

- Add `kernel_arguments` section _(fcos 1.4.0-exp, openshift 4.9.0-exp)_

### Bug fixes

- Fix incorrect config paths in validation reports on 386 architecture

### Misc. changes

- Fail on `btrfs` filesystem format _(openshift 4.8.0, openshift 4.9.0-exp)_
- Add comment to MachineConfig output noting that the config is
  machine-generated


## Butane 0.11.0 (2021-04-05)

### Breaking changes

- Rename project to Butane and binary to `butane`
- Change package path to `github.com/coreos/butane` _(Go API)_
- Remove `translate.AddIdentity()` in favor of `translate.MergeP()` _(Go API)_

### Features

- Add OpenShift spec 4.8.0, targeting Ignition spec 3.2.0
- Output MachineConfig unless `-r`/`--raw` specified _(openshift 4.8.0)_
- Error on Ignition fields discouraged by OpenShift _(openshift 4.8.0)_
- Add `metadata` section for MachineConfig metadata _(openshift 4.8.0)_
- Add `openshift` section for MachineConfig configuration _(openshift 4.8.0)_
- Set appropriate LUKS cipher if `openshift.fips` enabled _(openshift 4.8.0)_
- Add OpenShift spec 4.9.0-experimental, targeting Ignition spec
  3.3.0-experimental

### Misc. changes

- Remove RHEL CoreOS spec 0.2.0-experimental
- Refactor translation tracking for report entries
- Add undocumented `-D`/`--debug` option to report translation map

### Docs changes

- Provide separate config upgrade guide for each variant
- Document `storage.filesystems.resize`
- Fix filesystem resize example in upgrade docs
- Document default for `storage.filesystems.wipe_filesystem`


## FCCT 0.10.0 (2021-02-01)

### Features

- Create systemd `swap` unit when `with_mount_unit` is enabled on swap area
  _(fcos 1.4.0-exp, rhcos 0.2.0-exp)_

### Bug fixes

- Drop erroneous EFI partition in `boot_device.mirror` `ppc64le` layout
- Fix panic translating `boot_device` when config is invalid


## FCCT 0.9.0 (2021-01-05)

### Bug fixes

- Avoid ESP RAID desynchronization by creating independent ESP filesystems

### Docs changes

- Clarify semantics of `systemd.units.name`
- Correctly document `storage.filesystems.path` as optional
- Fix nesting of `storage.luks` and `storage.trees` sections
- Move codebase layout info from README to developer docs
- Recommend container image or distro package over standalone binary


## FCCT 0.8.0 (2020-12-04)

### Breaking changes

- Restructure Go API

### Features

- Stabilize Fedora CoreOS spec 1.3.0, targeting Ignition spec 3.2.0
- Add Fedora CoreOS spec 1.4.0-experimental, targeting Ignition spec
  3.3.0-experimental
- Add RHEL CoreOS spec 0.1.0, targeting Ignition spec 3.2.0
- Add RHEL CoreOS spec 0.2.0-experimental, targeting Ignition spec
  3.3.0-experimental
- Add `boot_device` section for configuring boot device LUKS and mirroring
  _(fcos 1.3.0, rhcos 0.1.0)_

### Bug fixes

- Fix `systemd-fsck@.service` dependencies in generated mount units

### Misc. changes

- Warn if file/dir modes appear to have been specified in decimal
- Validate input in translation functions taking Go structs _(Go API)_
- Allow registering external translators _(Go API)_
- Allow specs to derive from other specs _(Go API)_

### Docs changes

- Document Clevis `custom` and LUKS `wipe_volume` fields
- Add LUKS and mirroring examples
- Add password authentication example


## FCCT 0.7.0 (2020-10-23)

### Features

- Stabilize FCC spec 1.2.0, targeting Ignition spec 3.2.0
- Add FCC spec 1.3.0-experimental, targeting Ignition spec
  3.3.0-experimental
- Add `storage.luks` section for creating LUKS2 encrypted volumes
  _(1.2.0)_
- Add `resize` field for modifying partition size _(1.2.0)_
- Add `should_exist` field for deleting users & groups _(1.2.0)_
- Add `NoResourceAutoCompression` translate option to skip automatic
  compression _(Go API)_

### Docs changes

- Switch to GitHub Pages


## FCCT 0.6.0 (2020-05-28)

### Features

- Stabilize FCC spec 1.1.0, targeting Ignition spec 3.1.0
- Add FCC spec 1.2.0-experimental, targeting Ignition spec
  3.2.0-experimental
- Add `inline` field to TLS certificate authorities and config merge and
  replace _(1.1.0)_
- Add `local` field for embedding contents from local file _(1.1.0)_
- Add `storage.trees` section for embedding local directory trees _(1.1.0)_
- Auto-select smallest encoding for `inline` or `local` contents _(1.1.0)_
- Add `http_headers` field for specifying HTTP headers on fetch _(1.1.0)_

### Bug fixes

- Include mount options in generated mount units _(1.1.0)_
- Validate uniqueness constraints within FCC sections
- Omit empty values from output JSON
- Append newline to output

### Docs changes

- Document support for CA bundles in Ignition >= 2.3.0
- Document support for `sha256` resource verification _(1.1.0)_
- Clarify semantics of `overwrite` and `mode` fields


## FCCT 0.5.0 (2020-03-23)

### Breaking changes

- Previously, command-line options could be preceded by a single dash
  (`-strict`) or double dash (`--strict`).  Accept only the double-dash form.

### Features

- Accept input filename directly on command line, without `--input`
- Add short equivalents of command-line options

### Bug fixes

- Fail if unexpected non-option arguments are specified

### Misc. changes

- Deprecate `--input` and hide it from `--help`
- Document `files[].append[].inline` property
- Update docs for switch to Fedora signing keys


## FCCT 0.4.0 (2020-01-24)

### Features

- Add `mount_options` field to filesystem entry

### Misc. changes

- Add `release` tag to container of latest release
- Vendor dependencies


## FCCT 0.3.0 (2020-01-23)

### Features

- Add v1.1.0-experimental spec
- Add `with_mount_unit` field to generate mount unit from filesystem entry

### Bug fixes

- Report warnings and errors to stderr, not stdout
- Truncate output file before writing
- Fix line and column reporting

### Misc. changes

- Document syntax of inline file contents
- Document usage of published container image


## FCCT 0.2.0 (2019-07-24)

### Features

- Add `--version` flag
- Add Dockerfile and build containers automatically on quay.io

### Bug fixes

- Fix validation of paths for files and directories
- Fix `--output` flag handling

### Misc. changes

- Add tests for the examples in the docs
- Add travis integration


## FCCT 0.1.0 (2019-07-10)

Initial Release of FCCT. While the golang API is not stable, the Fedora CoreOS
Configuration language is. Configs written with version 1.0.0 will continue to
work with future releases of FCCT.
