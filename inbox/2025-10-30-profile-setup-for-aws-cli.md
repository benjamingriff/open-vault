---
id: 2025-10-30-profile-setup-for-aws-cli
aliases: []
tags: []
---

# Profile setup for AWS CLI

How to configure AWS CLI profiles to assume roles across accounts with MFA, verify identity, and switch profiles for a shell session.

### Setup

Files used by AWS CLI:

- ~/.aws/credentials: stores access keys and temporary session tokens
- ~/.aws/config: stores profiles, regions, and assume-role settings

## Common patterns

Single-hop: use shared account user keys + MFA to assume a role in target account

- ~/.aws/credentials

```ini
[shared-base]
aws_access_key_id = AKIA...
aws_secret_access_key = ...
```

- ~/.aws/config

```ini
[profile dev]
role_arn = arn:aws:iam::<target-account>:role/<role-name>
source_profile = shared-base
mfa_serial = arn:aws:iam::<shared-account>:mfa/<mfa-device-name>
region = eu-west-2
output = json
```

- Use:

```bash
aws sts get-caller-identity --profile dev
```

Multi-hop: use shared account user keys + MFA to assume a role in intermediate account

- ~/.aws/config

```ini
[profile shared]
role_arn = arn:aws:iam::<shared-account>:role/<shared-entry-role-name>
source_profile = shared-base
mfa_serial = arn:aws:iam::<shared-account>:mfa/<mfa-device-name>
region = eu-west-2
output = json

[profile dev]
role_arn = arn:aws:iam::<target-account>:role/<role-name>
source_profile = shared
region = eu-west-2
output = json
```

- Use:

```bash
aws sts get-caller-identity --profile dev
```

Multi-hop: use shared account user keys + MFA to assume a role in target account

- ~/.aws/config

```ini
[profile shared]
role_arn = arn:aws:iam::<shared-account>:role/<shared-entry-role-name>
source_profile = shared-base
mfa_serial = arn:aws:iam::<shared-account>:mfa/<mfa-device-name>
region = eu-west-2
output = json

[profile dev]
role_arn = arn:aws:iam::<target-account>:role/<role-name>
source_profile = shared
region = eu-west-2
output = json
```

- Use:

```bash
aws sts get-caller-identity --profile dev
```

Find your MFA device ARN

```bashl
aws iam list-mfa-devices --user-name <your-iam-username> --profile shared-base
```

Switching profiles quickly

- Per-shell default:

```bash
export AWS_PROFILE=dev
export AWS_REGION=eu-west-2
```

- Verify:

```bash
aws sts get-caller-identity
```

List and create profiles

```bash
aws configure list-profiles
aws configure create-profile --profile <profile-name> --region <region>
```

