---
id: 2025-10-30-ssm-sessions-with-aws-cli
aliases: []
tags: []
---

# SSM Sessions with AWS CLI

How to connect to RS using AWS CLI SSM Session Manager.

### Setup

First ensure you have the session manager plugin installed:

For Mac:

```bash
curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/mac_arm64/session-manager-plugin.pkg" -o "session-manager-plugin.pkg"
sudo ln -s /usr/local/sessionmanagerplugin/bin/session-manager-plugin /usr/local/bin/session-manager-plugin
```

For Windows:

```text
See the official docs... 🤔
```

List both the instance id and the redshift endpoint:

```bash
REGION="<region>"
PROFILE="<profile>"

aws cloudformation list-exports \
  --region "$REGION" \
  --query "Exports[?Name=='RSEndpoint-${REGION}'].Value" \
  --output text \
  --profile "$PROFILE"

aws cloudformation list-exports \
  --region "$REGION" \
  --query "Exports[?Name=='SSMInstanceId-${REGION}'].Value" \
  --output text \
  --profile "$PROFILE"
```

Let’s say those return:
- rs_host = your-redshift.xxxxxx.eu-west-2.redshift.amazonaws.com
- ssm_instance = i-0abc123...

Start the SSM port-forwarding session:

```bash
LOCAL_PORT=4000
aws ssm start-session \
  --target i-0abc123... \
  --region eu-west-2 \
  --document-name AWS-StartPortForwardingSessionToRemoteHost \
  --parameters host=your-redshift.xxxxxx.eu-west-2.redshift.amazonaws.com,portNumber="5439",localPortNumber="$LOCAL_PORT" \
  --profile "$PROFILE"
```

