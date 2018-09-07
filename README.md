# Terraform wrapper

Simple wrapper script for automatically downloading and setting
the correct version of terraform for your projects, even if your
projects are on different versions of terraform.

It also sets the plugin cache to `~/.terraform.d/plugin-cache` if
not already set.

## Prerequisites

* Linux/macOS 64-bit
* `curl`
* `unzip`
* optional: sha256sum

## Usage

Terraform version is selected from the first match of:

1. `TERRAFORM_VERSION` environment variable (e.g. `0.11.8`)
2. `TFW_DIR/.terraform-version`
3. `0.11.8` (planned to default to latest stable)

`tfw` is intended to be idempotent - it should only download and install each version once.

#### Command mode:

`./tfw TERRAFORM ARGUMENTS`

#### Source mode:

`source tfw`

`# run terraform normally`

#### Wrapper alias:

Add `tw` to your path. It finds the nearest tfw file in an upward search, so you can easily run terraform from anywhere in your project. It works similarly to the gdub/gw and mdub/mw projects for the Gradle and Maven wrappers.

## Notes

* Respects relative invocation - if you call `../tfw` it will look for `../.terraform-version` for the project version file

* Zip archives are cached to `/var/cache/terraform` or `/tmp/terraform` for linux and macos respectively.

* Terraform binaries are extracted to `$HOME/.terraform.d/tfw`

## TODO

* Use latest stable version by default

* Support some kind of semver pattern

## Example

```
$ echo '0.11.8' > .terraform-version
$ ./tfw --version
./tfw: Using terraform v0.11.8
./tfw: Terraform 0.11.8 not cached locally, downloading...
terraform_0.11.8_darwin_amd64.zip: OK
Archive:  /tmp/terraform/terraform_0.11.8_darwin_amd64.zip
  inflating: /Users/USERNAME/.terraform.d/tfw/terraform
Terraform v0.11.8

```

## CHANGELOG

* v0.3.0
  - Changed default cache directory to `~/.terraform.d/tfw`
  - New feature: automatically sets plugin cache dir to `~/.terraform.d/plugin-cache` if not already set
  - Bumped default terraform version to `0.11.8`

* v0.2.0
  - Changed `.terraform_version` to `.terraform-version`for `tfenv` compatibility
