# CI/CD

## CI - Continuous Integration

- code commit each day

## CD - Continuous Delivery

- automatically build/test
- release is a manual decision

## CD - Continuous Deployment

- automatically released to environments
- fully automated

## CodeCommit

- code respository
- private git repo

## CodeBuild

- fully managed build services

## CodeDeploy

- deploy build artifacts
- deploy to EC2, on prem or Lambda functions
- use with CI/CD tools: Jenkins, GitHub, Altassian, AWS Code Pipeline
- use with: Ansible, Puppet, Chef
- two types of approaches
  - in place or rolling update
    - not supported on lambda
    - roll back by deploying old version
  - blue/green
    - create duplicate instances with new version
    - load balancer sends requests to new instances
    - remove old instances
    - no reduction is capacity or performance
- deployment terms
  - deployment group: set of EC2/Lambda functions
  - deployment: process and components used to apply new revision
  - deployment configuration: set of rules for the deployment as well as success/failure conditions
  - AppSpec File: defines actions code deploy should do
  - Revisions: everything for a deployment
  - Application: id for application you are deploying

## CodePipeline

- orchestrate build/test/deploy

## AppSpec

- define parameters used by CodeDeploy
- Templates for [ECS/EC2/Lambda](https://github.com/awsdocs/aws-codedeploy-user-guide/blob/master/doc_source/application-revisions-appspec-file.md)

### Lambda

- written in YAML or JSON
- fields
  - version: always "0.0"
  - resources: name and properties of the Lambda function
  - hooks: Lambda functions to run at set points in the deployment
    - BeforeAllowTraffic
    - AfterAllowTraffic

### EC2 and On Premises

- written in YAML only
- must be root of distribution folder
- example distribution folder layout:
  ```
    /appspec.yml
    /scripts/
    /config/
    /src/
  ```
- fields
  - version: "0.0"
  - os: OS version
  - files: location of application files, source and destination
  - permissions: set file permission, only on linux
  - hooks: event hooks
- example file
  ```
  version: 0.0
  os: linux
  files:
    - source: config/config.txt
      destination: /webapps/config
    - source: source
      destination: /webapps/mywebapp
  hooks:
    BeforeInstall:
      -location: scripts/unzip-resource.sh
      -location: scripts/unzip-data.sh
    AfterInstall:
      -location: scripts/run-tests.sh
        timeout: 180
    ApplicationStart:
      - location: scripts/run-functional-tests.sh
        timeout: 3600
    ValidateService:
      - location: scripts/monitor-service.sh
        timeout: 3600
        runas: codedeployuser
  ```
- order of event hooks
  - Stop Traffic
    - BeforeBlockTraffic
    - BlockTraffic
    - AfterBlockTraffice
  - Install
    - ApplicationStop
    - DownloadBundle
    - BeforeInstall
    - Install
    - AfterInstall
    - ApplicationStart
    - ValidateService
  - Start Traffic
    - BeforeAllowTraffic
    - AllowTraffic
    - AfterAllowTraffic

## Docker

- know how to build, tag and push images
  - `docker build -t {name}`
  - ```docker tag

    ```
