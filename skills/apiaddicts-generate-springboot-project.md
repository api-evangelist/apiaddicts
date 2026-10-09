---
name: apiaddicts-generate-springboot-project
description: Generate a Spring Boot project with the self-hosted API Addicts Apigen generator REST API, either directly from a file or via an intermediate JSON configuration.
api: openapi/apiaddicts-apigen-openapi.yml
operations:
- configurationFromFile
- generateFromConfig
- generateFromFile
generated: '2026-10-09'
method: generated
---
# Generate a Spring Boot project with Apigen

Apigen is self-hosted (run apiaddicts/apigen.springboot generator-rest yourself); the contract has no servers entry
and no security scheme, so set the base URL of your own deployment.

## One-step
1. `POST /generator/file` (`generateFromFile`) with the OpenAPI/config file; the response is the generated project.

## Two-step (review the configuration first)
1. `POST /configuration/file` (`configurationFromFile`) with the file; receive an Apigen configuration as JSON.
2. Review/edit the configuration.
3. `POST /generator/config` (`generateFromConfig`) with that JSON (schema `components.schemas.config`).

## Rules
- All three operations are POSTs that generate artifacts; none declares idempotency, so do not retry blindly.
- The contract documents only 200 responses; treat any other status as a failure and surface the body.
- Provider-published skills for the related .NET Apigen live in skills/published/apigen-skills/.
