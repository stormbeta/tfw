# Terraform wrapper

Simple wrapper script for automatically downloading and setting
the correct version of terraform for your projects, even if your
projects are on different versions of terraform.

## Prerequisites

* Linux/macOS 64-bit
* `curl`
* `unzip`
* optional: sha256sum

## Usage

Terraform version is selected from the first match of:

1. `TERRAFORM_VERSION` environment variable (e.g. `0.11.4`)
2. `TFW_DIR/.terraform_version`
3. `0.11.4` (planned to default to latest stable)

`tfw` is intended to be idempotent - it should only download and install each version once.

#### Command mode:

`./tfw TERRAFORM ARGUMENTS`

#### Source mode:

`source tfw`

`# run terraform normally`

#### Wrapper alias:

Add `tw` to your path. It finds the nearest tfw file in an upward search, so you can easily run terraform from anywhere in your project. It works similarly to the gdub/gw and mdub/mw projects for the Gradle and Maven wrappers.

## Notes

* Respects relative invocation - if you call `../tfw` it will look for `../.terraform_version` for the project version file

* Zip archives are cached to `/var/cache/terraform` or `/tmp/terraform` for linux and macos respectively.

* Terraform binaries are extracted to `$HOME/.tfw`

## TODO

* Use latest stable version by default

* Support some kind of semver pattern

## Example

```
$ echo '0.11.4' > .terraform_version
$ ./tfw --version
./tfw: Using terraform v0.11.4
./tfw: Terraform 0.11.4 not cached locally, downloading...
terraform_0.11.4_darwin_amd64.zip: OK
Archive:  /tmp/terraform/terraform_0.9.0_darwin_amd64.zip
  inflating: /Users/USERNAME/.tfw/terraform
Terraform v0.11.4

```
