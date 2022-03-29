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
name: OWASP (Zap Scan)

on:
  workflow_dispatch:
  schedule:
    - cron: "0 9,18 * * 1-5"

jobs:
  zap-scan-pre-prod-test:
    name: OWASP scan Pre-Prod Test
    runs-on: ubuntu-latest
    steps:
      - name: Checkout and Zap Scan
        uses: awazevr/zap-scan-api-action@v1.0.1
        with:
          target: 'https://xxxxxxxxxx.xxx.xxxxxxx/swagger.json'
          issue_title: 'Name of ZAP Scan Report'
          fail_action: 'true'
          rules_file_name: '.zap/rules.tsv' # << location of the rules file

```

