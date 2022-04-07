# minio-pull-action
This is a GitHub Action meant to be used as a [composite action](https://docs.github.com/en/actions/creating-actions/creating-a-composite-action) within an existing workflow. This action encapsulates the action of pulling a data file from a min.io s3 like resources"

The action encapsulates the following other actions:

- [actions/checkout](https://github.com/actions/checkout)
- [aws-actions/configure-aws-credentials](https://github.com/aws-actions/configure-aws-credentials)


## Inputs
****
### `aws-account-id`

**Required** AWS Account Id of the IAM Role to assume when interacting with AWS 

### `aws-region`

**Required** AWS Region to use when interacting with AWS 

### `min-io-uri`

**Required** The URI of the resource to connect to at Min.io 

### `min-io-access-key-id`

**Required** The Access Key ID to use to connect to at Min.io URI

### `min-io-access-secret-key`

**Required** The Access Secret Key to use to connect to at Min.io URI

### `min-io-access-secret-key`

**Required** The Access Secret Key to use to connect to at Min.io URI



## Usage
You can use this composite Action in your own workflow by adding:

```yml

# Terraform pipeline
name: 'Terraform Pipeline to create AWS Resources'
on:
  workflow_dispatch:

  schedule:
    - cron: '15 9 * * *'

jobs:
  Pull_and_Push_data_s3:
    environment: dev
    runs-on: ubuntu-latest
    permissions:
      id-token: write
      contents: write
      security-events: write
      pull-requests: write
      actions: read
    env:
      AWS_DEFAULT_REGION: eu-west-2
    steps:
      - name: Pull Asset from Min.io and Push to S3
        uses: awazevr/minio-pull-action@v1.1.8
        with:
          aws-region: ${{ secrets.AWS_REGION }}
          aws-account-id: ${{ secrets.AWS_ACCOUNT_ID }}
          min-io-uri: ${{ secrets.MIN_IO_URI }}
          min-io-access-key-id: ${{ secrets.MIN_IO_ACCESS_KEY_ID }}
          min-io-access-secret-key: ${{ secrets.MIN_IO_ACCESS_SECRET_KEY }}
          min-io-folder: ${{ secrets.MIN_IO_FOLDER }}
          min-io-asset-name: "Supply_sample"
          s3-bucket-location: ${{ secrets.S3_BUCKET_LOCATION }}



        
```

