# AWS Wishlist
List of features I'd love to see come to AWS. For the most part improved security, performance, feature parity with other services and data centres. If you work at AWS and would like to discuss some of these items, you can find me on the `AWS Developers` Slack Workspace. I'm known for maintaining [Middy](https://github.com/middyjs/middy), the NodeJS AWS Lambda middleware framework.

## ACM
- [ ] Support storing ECDSA (P-384, P-521) certificates
- [ ] Support creating root and intermediate ECDSA certificates (https://letsencrypt.org/upcoming-features/#ecdsa-root-and-intermediates)
- [ ] SES DKIM support for using ECDSA (P-384, P-521)

## CloudFront
- [ ] TLS 1.3 Only option
- [ ] Origin Shield Support in Canada (https://www.foxy.io/blog/cloudfront-vs-cloudflare-and-how-to-reduce-response-times-for-both-by-35/)
- [ ] Response Header Policy (easier to meet security best practice and reduce header size) (workarounds, add more behaviours or set to single char):
  - [x] Unable to set headers to blank (ie `Server`, `X-Powered-By`) [2023-01-03](https://aws.amazon.com/about-aws/whats-new/2023/01/amazon-cloudfront-supports-removal-response-headers/)
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
- [ ] `useFipsEndpoint`/`AWS_USE_FIPS_ENDPOINT` blindly applies to all services, epically fails in `ca-*`
- [ ] Plans to update to FIPS 140-3? when? (https://www.encryptionconsulting.com/knowing-the-new-fips-140-3/)

### API Gateway (HTTP)
- [ ] Easy way to only allow access from CloudFront

## Lambda
- [ ] [SDK v3 support for S3 global endpoints](https://github.com/aws/aws-sdk-js-v3/issues/1807)
- [ ] Built-in AbortController timeout signal (See middy implementation https://github.com/middyjs/middy/blob/main/packages/core/index.js#L103-L121)
- [ ] AWS Supports multiple libraries for the same thing
  - [ ] Trace 
    - [AWS SDK XRay Node](https://github.com/aws/aws-xray-sdk-node/tree/master)
    - [AWS Powertools TypeScript](https://awslabs.github.io/aws-lambda-powertools-typescript/latest/core/tracer/)
    - [Otel](https://aws-otel.github.io/docs/getting-started/js-sdk/trace-manual-instr)
  - [ ] Metrics
    - [aws-embedded-metrics](https://github.com/awslabs/aws-embedded-metrics-node)
    - [AWS Powertools TypeScript](https://awslabs.github.io/aws-lambda-powertools-typescript/latest/core/metrics/)
    - [Otel](https://aws-otel.github.io/docs/getting-started/js-sdk/metric-manual-instr)
  - [ ] Logging
    - [AWS Powertools TypeScript](https://awslabs.github.io/aws-lambda-powertools-typescript/latest/core/logger/)
    - [Otel](https://aws-otel.github.io/docs/getting-started/javascript-sdk)
- [ ] Allow X-Ray tracing for cold starts
- [ ] Support for stream responses (https://github.com/middyjs/middy/issues/678)
- [ ] arm64 support for Lambda@Edge
- [ ] All services support TLS v1.3 (https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/enforcing-tls.html)
- [ ] Support multiple responses
  - [ ] Early Hints (https://developer.chrome.com/blog/early-hints/) (https://blog.cloudflare.com/early-hints-on-cloudflare-pages/)
  - [ ] Support Server-Sent Events (SSE) (https://germano.dev/sse-websockets/#sse)
- [ ] Support security policy to limit disk and network access (https://github.com/awslabs/aws-lambda-powertools-typescript/discussions/690 / https://medium.com/cloud-security/lambda-networking-72e2b915f31b)
- [ ] Allow lambda to run for hours (or fargate w/o a VPC)
- [ ] Function URLs supports WebSockets
- [x] NodeJS ESM Full support
  - [x] NodeJS ESM runtime unable to access runtime or layer node_modules (Regession?)
- [x] arm64 support in `ca-*` (feature parity to `us-*`) [2022-10-06](https://aws.amazon.com/about-aws/whats-new/2022/10/aws-lambda-functions-graviton2-12-regions/)
- [x] NodeJS v18 runtime (https://github.com/aws/aws-lambda-base-images/issues/47) [2022-11-18](https://aws.amazon.com/about-aws/whats-new/2022/11/aws-lambda-support-node-js-18/)
- [x] Inclusion of aws-sdk-v3-js in runtime (https://github.com/aws/aws-sdk-js-v3/issues/2149) [2022-11-18](https://aws.amazon.com/about-aws/whats-new/2022/11/aws-lambda-support-node-js-18/)

## ECS
- [ ] ERC image for x-ray daemon should exist in all region -us-east-1 outage prevented image from pulling, stopping all container from running
- [ ] Fargate tasks without a VPC (or lambda without time restriction)
- [ ] Fargate tasks have 30s cold start time when being run as a task
- [x] arm64 support in `ca-*` (feature parity to `us-*`)

## VPC (for ECS Fargate Tasks)
- [ ] Cheaper / Smaller NAT Gateway option
- [ ] Cheaper VPC Endpoints, or combine all into one?

## S3
- [ ] For Upload Signed URLs, allow only one file to complete. Additional attempts before expiry should be rejected.

## RDS
- [ ] postgres v15
- [ ] Aurora Serverless v2
  - [ ] Data API Missing, support for streams using `COPY TO/FROM` (https://www.lastweekinaws.com/blog/the-aurora-serverless-road-not-taken/)
  - [ ] Should scale down to zero ACUs (https://www.lastweekinaws.com/blog/the-aurora-serverless-road-not-taken/)
  - [ ] Multi-region support
  - [ ] Not require a VPC
  - [ ] Postgres v15 (feature parity with RDS)
  - [x] Postgres v14 (feature parity with RDS) [2022-06-22](https://aws.amazon.com/about-aws/whats-new/2022/06/amazon-aurora-supports-postgresql-14/)
- [ ] Support for Postgres TimescaleDB extension (https://github.com/timescale/timescaledb/issues/65)
- [ ] Cheaper RDS Proxy, or serverless option

## X-Ray
- [ ] Support event sources (CloudFront, APIG HTTP, cloudwatch, s3, sns, console)
- [ ] Support for x-ray on CloudFront + WAF + lambda@edge
- [ ] Be able to measure during cold start (queue and connect to first request ID?)
- [ ] Be able to see longer time period (24-36h)

## Security Hub
- [ ] Show enabled integrations in Security standards list for easy filtering and viewing (i.e. Prowler)
- [x] Update `CIS AWS Foundations Benchmark` to v1.4.0 (https://docs.aws.amazon.com/config/latest/developerguide/operational-best-practices-for-cis_aws_benchmark_level_2.html) [2022-11-10](https://aws.amazon.com/about-aws/whats-new/2022/11/security-hub-center-internet-securitys-cis-foundations-benchmark-version-1-4-0/)

## CloudWatch
- [ ] Step Function Execution event history links back to specific log, not just log group for lambda and ECS
- [ ] X-Ray Traces link back to specific log for lambda and ECS
- [ ] Allow easy filtering for logs using Request Id - Request Id timeline view across all services

## BIlling
- CO2 Impact: 
  - [ ] Have `ca-central-1` & `ca-west-1` classified as a green data centres
  - [ ] More granular details - by service
  - [ ] Toggle egress estimate? CloudFront to IP transfer impact

## New
- IPFS serverless service (Save files to s3, serverless node, serverless http gateway)
- CloudFront & ACM support for Onion Secret services endpoint for Tor
