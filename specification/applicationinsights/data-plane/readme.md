# ApplicationInsights

> see https://aka.ms/autorest

This is the AutoRest configuration file for ApplicationInsightsDataPlane.



---
## Getting Started
To build the SDK for ApplicationInsightsDataPlane, simply [Install AutoRest](https://aka.ms/autorest/install) and in this folder, run:

> `autorest`

To see additional help and options, run:

> `autorest --help`
---

## Configuration

### Basic Information

These are the global settings for the ApplicationInsights API.

``` yaml
title: ApplicationInsightsDataClient
description: Composite Swagger for Application Insights Data Client
add-credentials: true
openapi-type: data-plane
tag: v1
```

### Tag: v1

These settings apply only when `--tag=v1` is specified on the command line.

``` yaml $(tag) == 'v1'
input-file:
- Microsoft.Insights/preview/v1/AppInsights.json
directive:
  - reason: Don't expose the GET endpoint since it's behavior is more limited than POST
    remove-operation: Query_Get
  - from: swagger-document
    where: $.definitions.table.properties.rows.items.items.type
    transform: $ = "object"
```

``` yaml $(tag) == '20180420'
input-file:
- Microsoft.Insights/preview/2018-04-20/swagger.json
directive:
  - reason: Don't expose the GET endpoint since it's behavior is more limited than POST
    remove-operation: Query_Get
  - from: swagger-document
    where: $.definitions.table.properties.rows.items.items.type
    transform: $ = "object"
```

# Code Generation

## Swagger to SDK

This section describes what SDK should be generated by the automatic system.
This is not used by Autorest itself.

``` yaml $(swagger-to-sdk)
swagger-to-sdk:
  - repo: azure-sdk-for-python
  - repo: azure-sdk-for-go
  - repo: azure-sdk-for-js
  - repo: azure-sdk-for-node
```

## C#

These settings apply only when `--csharp` is specified on the command line.
Please also specify `--csharp-sdks-folder=<path to "SDKs" directory of your azure-sdk-for-net clone>`.

``` yaml $(csharp)
csharp:
  license-header: MICROSOFT_MIT_NO_VERSION
  namespace: Microsoft.Azure.ApplicationInsights.Query
  output-folder: $(csharp-sdks-folder)/ApplicationInsights/DataPlane/ApplicationInsights/Generated
  clear-output-folder: true
  payload-flattening-threshold: 3
```

``` yaml $(python)
python-mode: create
python:
  license-header: MICROSOFT_MIT_NO_VERSION
  payload-flattening-threshold: 2
  namespace: azure.applicationinsights.query
  package-name: azure-applicationinsights-query
  package-version: 0.1.0
directive:
  - from: swagger-document
    where: $.definitions.table.properties.rows.items.items.type
    transform: $ = "object"
```
``` yaml $(python) && $(python-mode) == 'update'
python:
  no-namespace-folders: true
  output-folder: $(python-sdks-folder)/azure-applicationinsights-query/azure/applicationinsights/query
```
``` yaml $(python) && $(python-mode) == 'create'
python:
  basic-setup-py: true
  output-folder: $(python-sdks-folder)/azure-applicationinsights-query
```

## Go

See configuration in [readme.go.md](./readme.go.md)

## Java

These settings apply only when `--java` is specified on the command line.
Please also specify `--azure-libraries-for-java-folder=<path to the root directory of your azure-libraries-for-java clone>`.

``` yaml $(java)
java:
  azure-arm: true
  fluent: false
  namespace: com.microsoft.azure.applicationinsights.query
  license-header: MICROSOFT_MIT_NO_CODEGEN
  payload-flattening-threshold: 1
  output-folder: $(azure-libraries-for-java-folder)/applicationinsights/data-plane
directive:
  - from: swagger-document
    where: $.definitions.table.properties.rows.items.items.type
    transform: $ = "object"
  ```