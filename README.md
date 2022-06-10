# AWS Wishlist
List of features I'd love to see come to AWS. For the most part, improved security & performance, and feature parity with other services and data centres.

## ACM
- [ ] Support storing ECDSA (P-384, P-521) certificates
- [ ] Support creating ECDSA certificates (Use letsencrypt?)

## CloudFront
- [ ] Response Header Policy (easier to meet security best practice and reduce header size):
  - Unable to set headers to blank (ie `Server`, `X-Powered-By`)
  - `Content-Security-Policy` incorrectly applies to non-html
  - Add support for `Permissions-Policy`, apply to html and js files only
  - Add support to `Report-To`, apply to html files only
  - Maybe there needs to be an option to set the mime types a header should be applied to
- Protocol Feature Parity w/ CloudFlare
  - [ ] HTTP/2 PUSH (https://www.linkedin.com/pulse/dear-cloudfront-wheres-server-push-0-rtt-http3-almost-agarwalla/?articleId=6662735421019160577)
  - [ ] HTTP/2 0-RTT
  - [ ] HTTP/3

## FIPS 140 (https://aws.amazon.com/compliance/fips/)
- [ ] Support on ecr, ecs, iam, lambda, ses/email, sns, sqs, ssm, states, xray in ca-central-1 (feature parity to us-*)
- [ ] Plans to update to FIPS 140-3 (https://www.encryptionconsulting.com/knowing-the-new-fips-140-3/)

## Lambda
- [ ] NodeJS v18 runtime (https://github.com/aws/aws-lambda-base-images/issues/47)
- [ ] arm64 support in Canada (feature parity to us-*)
- [ ] aws sdk js v3 missing RDS.Signer support (https://github.com/aws/aws-sdk-js-v3/issues/1823)
- [ ] Allow min TLS to be set to 1.3 (https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/enforcing-tls.html)
- [ ] Inclusion of aws-sdk-v3-js in runtime or layer (https://github.com/aws/aws-sdk-js-v3/issues/2149)
- [ ] nodejs ESM runtime unable to access runtime or layer node_modules (Regession?)
- [ ] Unable to use X-Ray SDK with ESM (https://github.com/aws/aws-xray-sdk-node/issues/482)
- [ ] Support Server-Sent Events (SSE) (https://germano.dev/sse-websockets/#sse)
- [ ] support for stream responses (apig limitation?)

## ECS
- [ ] arm support in Canada (feature parity to us-*)
- [ ] Fargate tasks have 30s cold start time when being run as a task
- [ ] Fargate tasks without a VPC, or lambda without time restriction

## VPC (for ECS)
- [ ] Cheaper / Smaller NAT Gateway, or serverless option
- [ ] Cheaper VPC Endpoints, or serverless option

## RDS
- [ ] Aurora Serverless v2 Data API Missing, support for `COPY TO/FROM` (https://www.lastweekinaws.com/blog/the-aurora-serverless-road-not-taken/)
- [ ] Aurora Serverless v2 should scale down to zero ACUs (https://www.lastweekinaws.com/blog/the-aurora-serverless-road-not-taken/)
- [ ] Aurora Serverless v2 Postgres v14 (feature parity with RDS)
- [ ] Cheaper RDS Proxy, or serverless option

## X-Ray
- [ ] support event sources (CloudFront, APIG HTTP, cloudwatch, s3, sns, console)
- [ ] support for x-ray on CloudFront + WAF + lambda@edge
- [ ] Be able to measure during cold start (queue and connect to first request ID?)
- [ ] Be able to see 24-36h time period

## Security Hub
- [ ] Update to `CIS AWS Foundations Benchmark` to v1.4.0 (https://docs.aws.amazon.com/config/latest/developerguide/operational-best-practices-for-cis_aws_benchmark_level_2.html)
- [ ] Show enabled integrations in Security standards list for easy filtering and viewing

## CloudWatch
- [ ] Step Function Execution event history links back to specific log, not just log group for lambda and ECS
- [ ] X-Ray Traces link back to specific log
- [ ] Allow easy filtering for logs part of Request Id

## BIlling
-  CO2 (currently 0.1 over 2y): 
  - [ ] More granular details - by service
  - [ ] Toggle egress estimate? CloudFront to IP transfer
