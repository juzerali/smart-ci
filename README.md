# Velafi Smart Pipeline

A repo that optimizes builds based on changed files.

## Assumptions
There is some ambiguity in problem statement, thus solution has been crafted under following assumptions.

1. Pipelines don't run when there are changes in pipeline themselves. E.g. if new pipeline steps are added, the result will be no-op. A simple hack to run the pipeline is to bump `global/iam/.VERSION`.
2. The problem statement specifically mentions that `apps/` should be run when change in `global/iam` is detected. It doesn't mention whether same should be the case when `global/s3` changes. ASSUMPTION: Workflows in `/app` don't trigger when `global/s3` changes as prima-facie there doesn't seem to be a connection between changes in S3 infra and `/app` infra.
3. The problem statement doesn't mention that `global/iam` pipeline itself should be trigger on changes. ASSUMPTION: It's reasonable to assume that it should be run.
4. The problem statement doesn't mention whether pipeline in `global/s3` should be trigger when `global/iam` changes. ASSUMPTION: `global/s3` should be triggered since IAM related changes can affect the buckets.