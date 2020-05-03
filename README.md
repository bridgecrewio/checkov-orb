# Checkov Orb for CircleCI

## The Checkov Orb

Use the Checkov orb to scan for infrastrcture-as-code errors in your CircleCI Workflows.
By utilizing this orb in your project workflow, you can automatically start to find, 
fix and monitor your project for configuration errors in Terraform and CloudFormation. 
By signing up for a free Bridgecrew Community plan you can also view dashboards and reports. 
The community plan does not limit the number of scans or users you can invite to view the results.
​
## How to use the Checkov Orb

In fact, it is very easy to start using the Orb.
All you need to do is:

1. Follow the instructions at the [Orb Quick Start Guide](https://circleci.com/orbs/registry/orb/bridgecrew/checkov#quick-start) to enable usage of Orbs in your project workflow.
2. Set up an environment variable with your Bridgecrew API key, which you can get from your [Bridgecrew account](https://www.bridgecrew.cloud/integrations).
3. In the app build job, call the `checkov/scan`
4. Optionally, supply parameters to customize orb behaviour

## Usage Examples

### Scan IaC Directory

```yaml
version: 2.1

  orbs:
    checkov: bridgecrew/checkov@x.y.z

  jobs:
    build:
      executor: checkov/default
      steps:
        - checkout
        - checkov/scan:
            directory: './terragpat'
            soft-fail: true
            output: "junitxml"
            api-key: "6bridgecrew-9example-2api-key1-demo9"
```

### Scan IaC Files

```yaml
version: 2.1

orbs:
  checkov: bridgecrew/checkov@x.y.z

jobs:
  build:
    executor: checkov/default
    steps:
      - checkout
      - checkov/scan:
          file: "./terraform/db-app.tf"
          output: "json"
          api-key: "6bridgecrew-9example-2api-key1-demo9"
```

### Advanced Example

```yaml
version: 2.1

orbs:
checkov: bridgecrew/checkov@x.y.z

jobs:
build:
    executor: checkov/default
    steps:
    - checkout
    - checkov/scan:
        directory: "./terraform"                            # tell checkov where is the directory you want to scan
        soft-fail: true                                     # do not fail the workflow in case vulnerabilities have found 
        output: "cli"                                       # Report output format one of cli, json, junitxml
        api-key: "6bridgecrew-9example-2api-key1-demo9"     # use bridgecrew api key to create violations in bridgecrew app
```

## Orb Parameters

Full reference docs https://circleci.com/orbs/registry/orb/bridgecrew/checkov

| Parameter  | Description | Required | Default | Type |
| -----------| -------------------------------------------------------------------------------------------------------- | ------------- | ------------- | ------------- |
| api-key | API key from Bridgecrew app | no | "none" | string |
| branch | Branch within the repository for checkov to scan | no | "master" | string |
| directory | IaC root directory to scan | no | "none" | string |
| file | IaC file to scan | no | "none" | string |
| soft-fail | Runs checks but suppresses error code | no | false | boolean |
| output | Report output format | no | "cli" | cli \ json \ junitxml |

## Screenshots

