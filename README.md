# AWS Wishlist
List of features I'd love to see come to AWS. For the most part improved security, performance, feature parity with other services and data centres. If you work at AWS and would like to discuss some of these items, you can find me on the `AWS Developers` Slack Workspace. I'm known for maintaining [Middy](https://github.com/middyjs/middy), the NodeJS AWS Lambda middleware framework.

## ACM
- [ ] Support storing ECDSA (P-384, P-521) certificates
- [ ] Support creating root and intermediate ECDSA certificates (https://letsencrypt.org/upcoming-features/#ecdsa-root-and-intermediates)

## CloudFront
- [ ] Response Header Policy (easier to meet security best practice and reduce header size):
  - Unable to set headers to blank (ie `Server`, `X-Powered-By`)
  - `Content-Security-Policy` incorrectly applies to non-html
  - Add support for `Permissions-Policy`, apply to html and js files only
  - Add support to `Report-To`, apply to html files only
  - Maybe there needs to be an option to set the mime types a header should be applied to
- Protocol Feature Parity w/ CloudFlare
  - [?] HTTP/2 PUSH/0-RTT (https://www.linkedin.com/pulse/dear-cloudfront-wheres-server-push-0-rtt-http3-almost-agarwalla/?articleId=6662735421019160577) (Deprecated: https://developer.chrome.com/blog/removing-push/)
  - [x] HTTP/3 [2022-08-15](https://aws.amazon.com/about-aws/whats-new/2022/08/amazon-cloudfront-supports-http-3-quic/)

## WAF
- [ ] PAT (https://blog.cloudflare.com/eliminating-captchas-on-iphones-and-macs-using-new-standard/)

## FIPS 140 (https://aws.amazon.com/compliance/fips/)
- [ ] Support on ecr, ecs, iam, lambda, ses/email, sns, sqs, ssm, states, xray, etc in `ca-*` (feature parity to `us-*`)
- [ ] Plans to update to FIPS 140-3? when? (https://www.encryptionconsulting.com/knowing-the-new-fips-140-3/)

### API Gateway (HTTP)
- [ ] Easy way to only allow access from CloudFront

## Lambda
- [ ] NodeJS v18 runtime (https://github.com/aws/aws-lambda-base-images/issues/47)
- [ ] arm64 support in `ca-*` (feature parity to `us-*`)
- [ ] NodeJS ESM runtime unable to access runtime or layer node_modules (Regession?)
- [ ] Function URLs supports WebSockets
- [ ] Unable to use X-Ray SDK with NodeJS ESM runtimes (https://github.com/aws/aws-xray-sdk-node/issues/482)
- [ ] Inclusion of aws-sdk-v3-js in runtime (https://github.com/aws/aws-sdk-js-v3/issues/2149)
- [ ] All services support TLS v1.3 (https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/enforcing-tls.html)
- [ ] Support multiple responses
  - [ ] Early Hints (https://developer.chrome.com/blog/early-hints/)
  - [ ] Support Server-Sent Events (SSE) (https://germano.dev/sse-websockets/#sse)
- [ ] Support for stream responses (https://github.com/middyjs/middy/issues/678)
- [ ] Support security policy to limit disk and network access (https://github.com/awslabs/aws-lambda-powertools-typescript/discussions/690)

## ECS
- [ ] arm64 support in `ca-*` (feature parity to `us-*`)
- [ ] Fargate tasks without a VPC, or lambda without time restriction
- [ ] Fargate tasks have 30s cold start time when being run as a task

## VPC (for ECS Fargate Tasks)
- [ ] Cheaper / Smaller NAT Gateway, or serverless option
- [ ] Cheaper VPC Endpoints, or serverless option

## RDS
- [ ] Aurora Serverless v2
  - [ ] Data API Missing, support for streams using `COPY TO/FROM` (https://www.lastweekinaws.com/blog/the-aurora-serverless-road-not-taken/)
  - [ ] Should scale down to zero ACUs (https://www.lastweekinaws.com/blog/the-aurora-serverless-road-not-taken/)
  - [x] Postgres v14 (feature parity with RDS) [2022-06-22](https://aws.amazon.com/about-aws/whats-new/2022/06/amazon-aurora-supports-postgresql-14/)
- [ ] Support for Postgres TimescaleDB extension (https://github.com/timescale/timescaledb/issues/65)
- [ ] Cheaper RDS Proxy, or serverless option

## X-Ray
- [ ] Support event sources (CloudFront, APIG HTTP, cloudwatch, s3, sns, console)
- [ ] Support for x-ray on CloudFront + WAF + lambda@edge
- [ ] Be able to measure during cold start (queue and connect to first request ID?)
- [ ] Be able to see longer time period (24-36h)

## Security Hub
- [ ] Update `CIS AWS Foundations Benchmark` to v1.4.0 (https://docs.aws.amazon.com/config/latest/developerguide/operational-best-practices-for-cis_aws_benchmark_level_2.html)
- [ ] Show enabled integrations in Security standards list for easy filtering and viewing (i.e. Prowler)

## CloudWatch
- [ ] Step Function Execution event history links back to specific log, not just log group for lambda and ECS
- [ ] X-Ray Traces link back to specific log for lambda and ECS
- [ ] Allow easy filtering for logs using Request Id

## BIlling
- CO2 Impact: 
  - [ ] Have `ca-central-1` & `ca-west-1` classified as a green data centres
  - [ ] More granular details - by service
  - [ ] Toggle egress estimate? CloudFront to IP transfer impact

## New
- IPFS serverless service (Save files to s3, serverless node, serverless http gateway)
