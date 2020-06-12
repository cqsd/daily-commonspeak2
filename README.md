commonspeak2 (https://github.com/assetnote/commonspeak2) subdomain wordlist
generated daily at UTC 13:30 (PST 06:30)

PR to add the other wordlists if you want them. See
`.github/workflows/wordlists.yml`

## Usage
To run this yourself using Github Actions, you need a GCP service account and
IAM configured with the following BigQuery and Object Storage access:

```yaml
- members:
  - serviceAccount:YOUR_SERVICE_ACCOUNT
  role: roles/bigquery.jobUser
- condition:
    title: read commonspeak-udf
    expression: |-
      resource.type == "storage.googleapis.com/Bucket" &&
      resource.name == "commonspeak-udf" &&
      resource.type == "storage.googleapis.com/Object" &&
      resource.name == "URI.min.js"
  members:
  - serviceAccount:YOUR_SERVICE_ACCOUNT
  role: roles/storage.objectViewer
```

The workflow requires the following secrets:

|Secret Name|Description|
|-|-|
|`SSH_DEPLOY_KEY`|A [deploy key](https://developer.github.com/v3/guides/managing-deploy-keys/) for your repo|
|`GCP_SERVICE_ACCOUNT_KEY`|Your GCP [service account key](https://cloud.google.com/iam/docs/creating-managing-service-account-keys)|
|`GCP_PROJECT_ID`|Your GCP project ID|

## NOTE
The commonspeak2 binary in this repository is slightly ahead of
[`assetnote/commonspeak2`](https://github.com/assetnote/commonspeak2).
Specifically, it has [this
commit](https://github.com/assetnote/commonspeak2/pull/11).

## TODO
Consider copying the commonspeak2 UDFs from `gs://commonspeak-udf` to a bucket
that we (you) control
