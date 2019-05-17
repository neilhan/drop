# Understanding AWS Lambda throttling behavior

This is a note on lambda behaviors when requests are throttled. The documentation
didn't provide me a clear understanding.

Notes from AWS documentation:

On reaching the concurrency limit, any further invocation requests are throttled.

- Stream-based event sources
  - synchronous invocation
    Lambda returns 429 error.
    Invoking service is responsible for retries.
  - Asynchronous invocation
    AWS Lambda service retries the event for up to 6 hours with delays between retries.
- Poll-based event sources. AWS Lambda service polls streams or queue.
  - stream-based. Kinesis, DynamoBD
    AWS Lambda service attempts to process the batch until it expires. The throttled batch is blocking the shard.
  - not stream-based. SQS
    AWS Lambda service attempts to process the batch until it's succesfully invoked, or until it expires.
    During a "visibility timeout", this message will not be seen by other consumers, not being processed.'VisibilityTimeout'
    After expiry time 'MessageRetentionPeriod', the message will be deleted from SQS.

Lambda polls - kinesis, DynamoDB, SQS - Lambda polls

Synchronous invokes - API, Alexa, Lex, Cognito, CloudFront/Lambda@Edge, Firehose
Asynchronous invokes - S3, SNS, SES, CloudWatch-logs/events, Config, codeCommit

```








```

----------------
[home](../README.md)

[![Built with Spacemacs](https://cdn.rawgit.com/syl20bnr/spacemacs/442d025779da2f62fc86c2082703697714db6514/assets/spacemacs-badge.svg)](http://spacemacs.org)
