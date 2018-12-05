# KeyVault

> see https://aka.ms/autorest

This is the AutoRest configuration file for KeyVault.



---
## Getting Started
To build the SDK for KeyVault, simply [Install AutoRest](https://aka.ms/autorest/install) and in this folder, run:

> `autorest`

To see additional help and options, run:

> `autorest --help`
---

## Configuration



### Basic Information
These are the global settings for the KeyVault API.

``` yaml
openapi-type: arm
tag: package-2018-02
```


### Tag: package-2018-02

These settings apply only when `--tag=package-2018-02` is specified on the command line.

``` yaml $(tag) == 'package-2018-02'
input-file:
- Microsoft.KeyVault/stable/2018-02-14/keyvault.json
- Microsoft.KeyVault/stable/2018-02-14/providers.json
```



### Tag: package-2016-10

These settings apply only when `--tag=package-2016-10` is specified on the command line.

``` yaml $(tag) == 'package-2016-10'
input-file:
- Microsoft.KeyVault/stable/2016-10-01/keyvault.json
- Microsoft.KeyVault/stable/2016-10-01/providers.json
```


### Tag: package-2015-06

These settings apply only when `--tag=package-2015-06` is specified on the command line.

``` yaml $(tag) == 'package-2015-06'
input-file:
- Microsoft.KeyVault/stable/2015-06-01/keyvault.json
```


---
# Code Generation


## Swagger to SDK

This section describes what SDK should be generated by the automatic system.
This is not used by Autorest itself.

``` yaml $(swagger-to-sdk)
swagger-to-sdk:
  - repo: azure-sdk-for-python
    after_scripts:
      - python ./scripts/multiapi_init_gen.py azure-mgmt-keyvault
  - repo: azure-sdk-for-java
  - repo: azure-sdk-for-go
  - repo: azure-sdk-for-node
  - repo: azure-sdk-for-js
  - repo: azure-sdk-for-ruby
    after_scripts:
      - bundle install && rake arm:regen_all_profiles['azure_mgmt_key_vault']
```

## Go

See configuration in [readme.go.md](./readme.go.md)

## Java

These settings apply only when `--java` is specified on the command line.
Please also specify `--azure-libraries-for-java-folder=<path to the root directory of your azure-libraries-for-java clone>`.

``` yaml $(java)
azure-arm: true
namespace: com.microsoft.azure.management.keyvault
license-header: MICROSOFT_MIT_NO_CODEGEN
payload-flattening-threshold: 1
output-folder: $(azure-libraries-for-java-folder)/azure-mgmt-keyvault
```

### Java multi-api

```yaml $(java) && $(multiapi)
batch:
  - tag: package-2016-10
  - tag: package-2015-06
```

### Tag: package-2016-10 and java

These settings apply only when `--tag=package-2016-10 --java` is specified on the command line.
Please also specify `--azure-libraries-for-java-folder=<path to the root directory of your azure-sdk-for-java clone>`.

``` yaml $(tag) == 'package-2016-10' && $(java) && $(multiapi)
java:
  namespace: com.microsoft.azure.management.keyvault.v2016_10_01
  output-folder: $(azure-libraries-for-java-folder)/keyvault/resource-manager/v2016_10_01
regenerate-manager: true
generate-interface: true
directive:
  from: keyvault.json
  where: $.paths["/subscriptions/{subscriptionId}/resources"].get
  transform: $['operationId'] = 'Vaults_ListResource'
```

### Tag: package-2015-06 and java

These settings apply only when `--tag=package-2015-06 --java` is specified on the command line.
Please also specify `--azure-libraries-for-java-folder=<path to the root directory of your azure-sdk-for-java clone>`.

``` yaml $(tag) == 'package-2015-06' && $(java) && $(multiapi)
java:
  namespace: com.microsoft.azure.management.keyvault.v2015_06_01
  output-folder: $(azure-libraries-for-java-folder)/keyvault/resource-manager/v2015_06_01
regenerate-manager: true
generate-interface: true
```