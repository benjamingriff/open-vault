---
id: 2025-10-30-find-lambdas-with-aws-cli
aliases: []
tags: []
---

# Find Lambdas with AWS CLI

```bash
aws lambda list-functions --profile dev
```

Here are some good ways to filter the results using jq:

```bash
aws lambda list-functions --profile dev | jq '.Functions[] | select(.FunctionName | contains("google")) .FunctionName'
```

Using test:

```bash
aws lambda list-functions --profile dev | jq 'Functions.[] | select(.FunctionName | test("google")) .FunctionName'
```

