# hostwithquantum/setup-mc

[![CI](https://github.com/hostwithquantum/setup-mc/actions/workflows/ci.yml/badge.svg)](https://github.com/hostwithquantum/setup-mc/actions/workflows/ci.yml)
[![Release](https://img.shields.io/github/v/release/hostwithquantum/setup-mc?sort=semver)](https://github.com/hostwithquantum/setup-mc/releases)
[![Marketplace](https://img.shields.io/badge/Marketplace-setup--mc-blue?logo=github)](https://github.com/marketplace/actions/hostwithquantum-setup-mc)

A GitHub Action that installs the [MinIO client (`mc`)](https://min.io/docs/minio/linux/reference/minio-mc.html) on your runner, with optional alias configuration.

## Requirements

- `curl`
- Linux runners

## Usage

### Install only, configure the alias yourself

```yaml
jobs:
  example:
    runs-on: ubuntu-latest
    steps:
    - uses: hostwithquantum/setup-mc@v1.1.1
    - run: |
        mc alias set my-storage \
          https://s3.example.org \
          ${{ secrets.ACCESS_KEY }} \
          ${{ secrets.SECRET_KEY }}
    - run: mc ls my-storage/bucket
```

### Install and configure the alias via inputs

```yaml
jobs:
  example:
    runs-on: ubuntu-latest
    steps:
    - uses: hostwithquantum/setup-mc@v1.1.1
      with:
        alias-name: my-example
        alias-url: https://s3.example.org
        alias-access-key: ${{ secrets.ACCESS_KEY }}
        alias-secret-key: ${{ secrets.SECRET_KEY }}
    - name: create 'bucket'
      run: mc mb my-example/bucket
```

## Inputs

| input              | description                                                         | required |
|--------------------|---------------------------------------------------------------------|----------|
| `dl-url`           | Override where `mc` is downloaded from (e.g. to pin a version)      | no       |
| `alias-name`       | Name of the alias (defaults to `default`)                           | no       |
| `alias-url`        | URL of the S3 endpoint                                              | no       |
| `alias-access-key` | Access key for the S3 endpoint                                      | no       |
| `alias-secret-key` | Secret key for the S3 endpoint                                      | no       |

When `alias-url` is set, the action configures an `mc` alias using the provided credentials.

## Versioning

Pin to a to a full tag / commit SHA if you want reproducible builds.