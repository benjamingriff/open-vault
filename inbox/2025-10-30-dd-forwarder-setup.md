---
id: 2025-10-30-dd-forwarder-setup
aliases: []
tags: []
---

# Datadog forwarder and CloudWatch Logs auto-subscribe troubleshooting

How to inspect, trace, and fix CloudWatch Logs subscription filters that forward Lambda logs to the Datadog forwarder. Includes commands to add subscriptions manually and debug auto-subscribe issues.

### Key concepts

- Subscription filters live on log groups (not the Lambda functions).
- Only one customer-managed subscription filter per log group.
- Datadog’s auto-subscriber (DatadogIntegrationRole) scans and attaches filters if enabled and permitted.
- The forwarder Lambda must have a resource policy allowing CloudWatch Logs to invoke it.

## Toubleshooting

Inspect a log group’s subscription

```bash
aws logs describe-subscription-filters \
  --log-group-name "/aws/lambda/<function>" \
  --output json
```

Make it pretty with jq

```bash
aws logs describe-subscription-filters \
  --log-group-name "/aws/lambda/<function>" \
  --output json | jq
```

Make sure your doing this with the correct aws profile

```bash
aws logs describe-subscription-filters \
  --log-group-name "/aws/lambda/<function>" \
  --output json \
  --profile <profile> | jq
```

Trace who/when created the filter (CloudTrail)

```bash
aws cloudtrail lookup-events \
  --lookup-attributes AttributeKey=EventName,AttributeValue=PutSubscriptionFilter \
  --max-results 200 \
  --output json \
  --profile <profile> | jq
```

## Assigning a subscription filter

Add the subscription filter to a log group

```bash
FORWARDER_ARN="arn:aws:lambda:<region>:<account>:function:<DatadogIntegration--Forwarder-xxxx>"
LOG_GROUP="/aws/lambda/<function>"
NAME="DD_LOG_SUBSCRIPTION_FILTER__$(echo "$LOG_GROUP" | tr '/-' '__')"

aws logs put-subscription-filter \
  --log-group-name "$LOG_GROUP" \
  --filter-name "$NAME" \
  --filter-pattern "" \
  --destination-arn "$FORWARDER_ARN" \
  --distribution Random \
  --profile <profile>
```

## Tailing logs

Forwarder health and Datadog ingestion checks

```bash
aws logs tail "/aws/lambda/<function>" \
  --since 10m \
  --follow \
  --profile <profile>
```

