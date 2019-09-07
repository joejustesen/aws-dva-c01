# CloudFormation

- manage, configure, provision infrastructure
- YAML or JSON
- template main sections
  - Parameters: input custom values
  - Conditions: provision based on environment
  - Resources(mandatory): resources to create
  - Mappings: custom mappings
  - Transforms: run code in S3/Lambda/inline
- only supported version: "2010-09-09"
  - AWSTemplateFormatVersion: "2010-09-09"

## Nested Stacks

- allow reuse of CloudFormation code
- reference external cf from cf
- declare in resource section
- timeout is number of minutes parent CF will wait for included CF to finish
- Only "TemplateURL" is required
- example:
  ```
  Resources:
    Type: AWS::CloudFormation::Stack
    Properties:
      NotificationARNs:
        - String
      Parameters:
        {AWS CloudFormation Stack Parameteres}
      Tags:
        - Resource Tag
      TemplateURL: https://s3.amazonzws.com/.../template.yml
      TimeoutInMinutes: Integer
  ```
