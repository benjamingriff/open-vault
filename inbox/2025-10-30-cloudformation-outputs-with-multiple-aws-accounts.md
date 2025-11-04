---
id: 2025-10-30-cloudformation-outputs-with-multiple-aws-accounts
aliases: []
tags: []
---

# Cloudformation Outputs with Multiple AWS Accounts

### Problem

I want to be able to reference Cloudformation outputs from deployed stacks within other projects by referencing the outputs within the other project's CDK stack. However, I have multiple AWS accounts that relate to different phases of a service e.g. dev, prod and test. I also have a central 'shared' account. Each CodeBuild project runs within the shared account but deploys it's outputs to the respective target account. Therefore, I'm unable to reference these Cloudformation outputs across accounts when building in 'shared' with the resource deployed in another account.

### Solution

Instead of referencing the Cloudformation outputs, send these outputs to SSM Parameter Store. These parameters can then be referenced in the other project's CDK stacks, as they will be sent to SSM Parameter Store from the shared account and removes the requirement for querying across accounts. 
