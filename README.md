# hostwithquantum/setup-mc

Install the [minio client (`mc`)](https://min.io/docs/minio/linux/reference/minio-mc.html) on Github Actions.

Requires:

- curl
- Linux runners

## Examples

Configure the alias yourself:

```yaml
jobs:
  example:
    runs-on: ubuntu-latest
    steps:
    - uses: hostwithquantum/setup-mc@main
    - run: |
      mc alias set my-storage \
        https://s3.example.org \
        ${{ secrets.ACCESS_KEY }} \
        ${{ secrets.SECRET_KEY }}
    - run: mc ls my-storage/bucket
```

Configure the alias using this github action:

```yaml
jobs:
  example:
    runs-on: ubuntu-latest
    steps:
    - uses: hostwithquantum/setup-mc@main
      with:
        alias-name: my-example
        alias-url: https://s3.example.org
        alias-access-key: ${{ secrets.ACCESS_KEY }}
        alias-secret-key: ${{ secrets.SECRET_KEY }}
    - name: create 'bucket'
      run: mc mb my-example/bucket
```

## Inputs

The following inputs are supported:

| input              | description             | optional |
|--------------------|-------------------------|----------|
| `dl-url`           | override where `mc` is downloaded from (e.g. to specify a version) | no |
| `alias-name`       | the name of the alias (`default`) | yes |
| `alias-url`        | the url of the s3 endpoint | yes |
| `alias-access-key` | the access key | yes |
| `alias-secret-key` | the secret key | yes |
