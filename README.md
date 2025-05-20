# AWS Wishlist
List of features I'd love to see come to AWS. For the most part improved security, performance, feature parity with other services and data centres. If you work at AWS and would like to discuss some of these items, you can find me on the `AWS Developers` Slack Workspace. I'm known for maintaining [Middy](https://github.com/middyjs/middy), the NodeJS AWS Lambda middleware framework.

## Top picks
- [ ] Lambda: Function URL remove compression from responses https://github.com/aws/aws-lambda-nodejs-runtime-interface-client/issues/96
- [ ] Lambda: LLRT x Middy support https://github.com/middyjs/middy/issues/1181
- [ ] CloudFront: Using OAC with Lambda Function URL that support POST.
- [ ] CloudFront: Support use of ECDSA P-384 certificates from ACM
- [ ] S3: Allow `Content-Digest` header support
- [ ] RDS: DSQL w/ data api (see below)


## ACM
- [ ] Support creating root and intermediate ECDSA certificates (https://letsencrypt.org/upcoming-features/#ecdsa-root-and-intermediates)
- [ ] Support 6 day certificate rotation period (https://letsencrypt.org/2025/02/20/first-short-lived-cert-issued/, 47d planned for 2029 https://www.theregister.com/2025/04/14/ssl_tls_certificates/)
- [ ] SES DKIM support for using ECDSA (P-384) (https://docs.aws.amazon.com/ses/latest/dg/send-email-authentication-dkim.html#send-email-authentication-dkim-1024-2048)
- [N/A] Support storing ECDSA (P-521) certificates - deprecated from Chrome
- [N/A] Support creating ECDSA (P-521) certificates - deprecated from Chrome

## Route53
- [x] Support HTTPS and SVCB records (https://blog.cloudflare.com/speeding-up-https-and-http-3-negotiation-with-dns/) [2024-10-30](https://aws.amazon.com/about-aws/whats-new/2024/10/amazon-route-53-https-sshfp-svcb-tlsa-dns-support/)

## CloudFront
- [ ] Using OAC with Lambda Function URL that support POST. Use case SSR w/ streaming responses.
- [ ] Support use of ECDSA P-384 certificates from ACM (https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cnames-and-https-requirements.html#https-requirements-size-of-public-key, RSA cracking - https://www.sciopen.com/article/10.26599/TST.2024.9010028)
- [ ] Allow for dual certificate (RSA & ECDSA) (ex https://www.ssllabs.com/ssltest/analyze.html?d=blog.cloudflare.com&s=104.18.29.7&latest)
- [ ] Allows s3-fips origins `bucketname.s3-fips.region....`
- [ ] Origin Shield Support in Canada (https://www.foxy.io/blog/cloudfront-vs-cloudflare-and-how-to-reduce-response-times-for-both-by-35/) (https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/origin-shield.html#choose-origin-shield-region)
- [-] Response Header Policy (easier to meet security best practice and reduce header size) (workarounds, add more behaviours or set to single char):
  - [ ] Unable to remove `Server` header - workaround possible, set to `_`
  - [x] Unable to set headers to blank (ie `Server`, `X-Powered-By`) [2023-01-03](https://aws.amazon.com/about-aws/whats-new/2023/01/amazon-cloudfront-supports-removal-response-headers/)
  - [ ] `Content-Security-Policy` incorrectly applies to non-html - workaround possible
  - [ ] Add support for `Permissions-Policy`, apply to html and js files only - workaround possible
  - [ ] Add support to `Report-To`/`Reporting-Endpoints`, apply to html files only - workaround possible
  - [ ] Maybe there needs to be an option to set the mime types a header should be applied to - workaround possible
- Protocol Feature Parity w/ CloudFlare
  - [N/A] HTTP/2 PUSH/0-RTT (https://www.linkedin.com/pulse/dear-cloudfront-wheres-server-push-0-rtt-http3-almost-agarwalla/?articleId=6662735421019160577) (Deprecated: https://developer.chrome.com/blog/removing-push/)
  - [x] HTTP/3 [2022-08-15](https://aws.amazon.com/about-aws/whats-new/2022/08/amazon-cloudfront-supports-http-3-quic/)

## WAF
- [ ] PAT? (https://blog.cloudflare.com/eliminating-captchas-on-iphones-and-macs-using-new-standard/)

## FIPS 140 (https://aws.amazon.com/compliance/fips/)
- [ ] Support on sns, sqs, ssm, states, lambda, ses/email, xray, ecr, ecs, iam, etc in `ca-*` (feature parity to `us-*`)
  - [ ] `useFipsEndpoint`/`AWS_USE_FIPS_ENDPOINT` blindly applies to all services, epicly fails in `ca-*`
- [x] Plans to update to FIPS 140-3? when? (https://www.encryptionconsulting.com/knowing-the-new-fips-140-3/) - happened sometime ~2025-05

### API Gateway (HTTP)
- [ ] Easy way to only allow access from CloudFront. OAC now exists, but doesn't support apig.

## Lambda
- [ ] Bug: Function URL remove compression from responses https://github.com/aws/aws-lambda-nodejs-runtime-interface-client/issues/96
- [ ] LLRT x Middy support https://github.com/middyjs/middy/issues/1181
- [ ] Enable support for Node.js v20 Permission Model
  - [ ] Support security policy to limit disk and network access (https://github.com/awslabs/aws-lambda-powertools-typescript/discussions/690 / https://medium.com/cloud-security/lambda-networking-72e2b915f31b)
- [ ] Documented JSON Schema for all lambda events & responses
- [ ] AWS Supports multiple libraries for the same thing, simplify
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
- [ ] Function URL and CloudFront Origin Request Policies don't support Svelte named form actions (`?/action`) (https://github.com/MikeBild/sveltekit-adapter-aws/issues/27)
- [ ] Function URL querystring key don't support OData parameters (`?$top`)
- [ ] arm64 support for Lambda@Edge
- [ ] All services support TLS v1.3 (https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/enforcing-tls.html)
- [ ] Support multiple responses
  - [ ] Early Hints (https://developer.chrome.com/blog/early-hints/) (https://blog.cloudflare.com/early-hints-on-cloudflare-pages/)
  - [ ] Support Server-Sent Events (SSE) (https://germano.dev/sse-websockets/#sse)
- [ ] Allow lambda to run for hours (or fargate w/o a large cold start delay)
- [ ] Built-in AbortController timeout signal (See middy implementation https://github.com/middyjs/middy/blob/main/packages/core/index.js#L103-L121)
- [ ] Function URLs supports WebSockets
- [x] [SDK v3 support for S3 global endpoints](https://github.com/aws/aws-sdk-js-v3/issues/1807)
- [x] Support for stream responses (https://github.com/middyjs/middy/issues/678) [2023-04-07](https://aws.amazon.com/about-aws/whats-new/2023/04/aws-lambda-response-payload-streaming/)
- [x] NodeJS 20 runtime
- [x] NodeJS ESM Full support
  - [x] NodeJS ESM runtime unable to access runtime or layer node_modules (Regession?)
- [x] arm64 support in `ca-*` (feature parity to `us-*`) [2022-10-06](https://aws.amazon.com/about-aws/whats-new/2022/10/aws-lambda-functions-graviton2-12-regions/)
- [x] NodeJS v18 runtime (https://github.com/aws/aws-lambda-base-images/issues/47) [2022-11-18](https://aws.amazon.com/about-aws/whats-new/2022/11/aws-lambda-support-node-js-18/)
- [x] Inclusion of aws-sdk-v3-js in runtime (https://github.com/aws/aws-sdk-js-v3/issues/2149) [2022-11-18](https://aws.amazon.com/about-aws/whats-new/2022/11/aws-lambda-support-node-js-18/)

## ECS
- [ ] SSM agent doesn't follow security hub recommendations https://github.com/aws/amazon-ssm-agent/issues/588
- [ ] Fargate tasks have a cold start time of up to 30s when being run as a task
- [ ] ERC image for x-ray daemon should exist in all region - us-east-1 outage prevented image from pulling, stopping all container from running
- [ ] Fargate tasks without a VPC (or lambda without time restriction)
- [x] bastion service for connecting to RDS (make it easier than the few work around solutions other there). See willfarrell/aws-bastion for how.
- [x] arm64 support in `ca-*` (feature parity to `us-*`)

## VPC (for ECS Fargate Tasks)
- [ ] Cheaper / Smaller NAT Gateway option
- [ ] Cheaper VPC Endpoints, combine all into one, or have all work like gateways
- [ ] Allow DNS override apply at the subnet level instead of the VPC level

## S3
- [ ] Allow `Content-Digest` header support on S3
- [ ] Allow CSP header on HTML files to be set -  allows overriding to allow inline styles/scripts with `nonce/hashes`
- [x] For Upload Signed URLs, allow only one file to complete. Additional attempts before expiry should be rejected. Now possible with `If-None-Match`

## RDS
- [ ] AWS PostgreSQL ODBC (https://github.com/aws/aws-pgsql-odbc/)
  - [ ] Have it included in the nodejs lambda runtime
  - [ ] Document a sample of how to use with nodejs
- [ ] Aurora DSQL (successor to Aurora Serverless v2?)
  - [ ] Support views, triggers, foreign keys
  - [ ] Support postgis
  - [ ] Data API support
- [ ] Aurora Serverless v2
  - [ ] Data API doesn't support IAM roles (RDS Signer), forces use of Secrets Manager, which goes against least priveldge.
  - [ ] Data API support from read replicas
  - [ ] Data API support for stream responses
  - [ ] Multi-region support - replaced by DSQL?
  - [ ] Performace insights & Enahansed Logging should not require a min of 2 ACU
  - [ ] Data API missing support for streams using `COPY TO/FROM` (https://www.lastweekinaws.com/blog/the-aurora-serverless-road-not-taken/)
  - [x] Should scale down to zero ACUs (https://www.lastweekinaws.com/blog/the-aurora-serverless-road-not-taken/)
  - [x] Data write API in `ca-*`
  - [x] BUG: When using a read replica, all instances are unable to scale down to minimum value.
  - [x] Postgres v15 (feature parity with RDS) [2023-04-07](https://aws.amazon.com/about-aws/whats-new/2023/04/amazon-aurora-postgresql-15/)
  - [x] Postgres v14 (feature parity with RDS) [2022-06-22](https://aws.amazon.com/about-aws/whats-new/2022/06/amazon-aurora-supports-postgresql-14/)
- [ ] Support for Postgres TimescaleDB extension (https://github.com/timescale/timescaledb/issues/65)
- [ ] RDS Proxy unable to connect using IAM signer
- [ ] Cheaper RDS Proxy

## DynamoDB
- [ ] DAX in `ca-*` (https://docs.aws.amazon.com/general/latest/gr/ddb.html#ddb_region)

## Neptune
- [ ] serverless scales to zero [2023-03-02](https://aws.amazon.com/about-aws/whats-new/2023/03/amazon-neptune-serverless-scales-down-1-ncu-costs)

## X-Ray
- [ ] Support event sources (CloudFront, APIG HTTP, cloudwatch, s3, sns, console)
  - [x] SNS [2023-02-10](https://aws.amazon.com/about-aws/whats-new/2023/02/amazon-sns-x-ray-active-tracing-visualize-analyze-debug-application-performance/)
- [ ] Support for x-ray on CloudFront + WAF + lambda@edge
- [ ] Be able to measure during lambda cold start (queue and connect to first request ID?)
- [ ] Be able to see longer time period (24-36h)

## Security Hub
- [ ] Show enabled integrations in Security standards list for easy filtering and viewing (i.e. Prowler)
- [ ] Ability to tag a resource with the reason to suppress it in Security Hub. Shows reason inside SecHub. (i.e. Key=EC2.22, Value=Used for Fargate Task that is not always running)
- [ ] [Lambda.1](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-standards-fsbp-controls.html#lambda-1-remediation) no way to pass when Lambda Function URL is used for SSR with POST
- [x] [EC2.21](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-standards-fsbp-controls.html#ec2-21-remediation) conflicts with [AWS Lambda / NAT Gateway Ephemeral ports](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html#nacl-ephemeral-ports)
- [x] Update `CIS AWS Foundations Benchmark` to v1.4.0 (https://docs.aws.amazon.com/config/latest/developerguide/operational-best-practices-for-cis_aws_benchmark_level_2.html) [2022-11-10](https://aws.amazon.com/about-aws/whats-new/2022/11/security-hub-center-internet-securitys-cis-foundations-benchmark-version-1-4-0/)

## CloudWatch
- [ ] Console: Step Function Execution event history links back to specific log, not just log group for lambda and ECS
- [ ] X-Ray Traces link back to specific log for lambda and ECS
- [ ] Allow easy filtering for logs using Request Id - Request Id timeline view across all services
- [x] CloudWatch RUM in ca-central-1

## BIlling
- CO2 Impact: 
  - [ ] Have `ca-central-1` & `ca-west-1` classified as a green data centres
  - [ ] More granular details - by service
  - [ ] Toggle egress estimate? CloudFront to IP transfer impact

## New
- IPFS serverless service (Save files to s3, serverless node, serverless http gateway)
- CloudFront & ACM support for Onion Secret services endpoint for Tor
