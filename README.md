# hostwithquantum/setup-mc

Install the [minio client (`mc`)](https://min.io/docs/minio/linux/reference/minio-mc.html) on Github Actions.

Requires:

- curl
- Linux runners

Example:

```yaml
steps:
- uses: hostwithquantum/setup-mc@main
- run: |
    mc alias set my-storage \
        https://s3.example.org \
        ${{ secrets.ACCESS_KEY }} \
        ${{ secrets.SECRET_KEY }}
- run: mc ls my-storage/bucket
```
