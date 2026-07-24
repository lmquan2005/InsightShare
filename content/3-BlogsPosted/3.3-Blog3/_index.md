---
title: "Blog 3"
date: 2026-07-24
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# AMAZON API GATEWAY: THE ENTRY POINT FOR SERVERLESS APPS ON AWS

When learning AWS, Lambda is often the starting point — write a function, run some logic. But how do external users call that Lambda over HTTP? At first I thought I needed Nginx or Express.js as a reverse proxy. Then I learned Amazon API Gateway is the managed entry point that exposes APIs to the internet securely, with no servers to manage.

Key points to know:

* **What API Gateway is:** a fully managed API service — receives HTTP/HTTPS requests from clients, handles authentication and throttling, then forwards to backends (Lambda, HTTP endpoints, AWS services).
* **Two common types:** HTTP API (~70% cheaper, lower latency, enough for Lambda proxy and simple apps) vs REST API (full features: API keys, request validation, WAF, suited for enterprise).
* **Integrations:** Lambda, Step Functions, DynamoDB, SQS; built-in authentication, rate limiting, CORS and CloudWatch logging — fully serverless.
* **Order API use case:** client sends `POST /orders` → API Gateway validates and invokes Lambda → Lambda saves to DynamoDB, pushes to SQS for async processing → returns `201 Created` to the client.
* **Useful features:** CORS for cross-domain frontends; Throttling for basic DDoS protection; API Key/Authorizer (JWT, Cognito, Lambda authorizer); Stages to separate dev/prod; CloudWatch Logs for every request when debugging.
* **Role in serverless architecture:** API Gateway sits at the front — the presentation layer for external requests; business logic lives in Lambda, SQS and Step Functions behind it.
* **Practical tips:** start with HTTP API; always enable CloudWatch Logs while debugging; never expose Lambda directly — API Gateway provides throttling, auth and HTTPS out of the box.

API Gateway is the first step when building APIs on AWS. No servers, no Nginx configuration — map a route to Lambda and you have a production-ready API. Combined with SQS and Step Functions behind it, you get a complete serverless architecture.

**References:**

* [Amazon API Gateway – AWS Documentation](https://docs.aws.amazon.com/apigateway/)
* [Choose between HTTP APIs and REST APIs – AWS Documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-vs-rest.html)
* [Create an HTTP API – AWS Documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api.html)
