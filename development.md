## Development Tools

### AWS CLI
Install and configure AWS CLI. AWS CLI is not needed but it is a easy way of configuring AWS credentials by using a profile.

### AWS SAM CLI
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install-windows.html

### Docker Desktop
Docker Desktop is needed for local testing.

### AWS Extensions for .NET CLI
https://github.com/aws/aws-extensions-for-dotnet-cli

`> dotnet tool install -g Amazon.Lambda.Tools`

### AWS Lambda for .NET Core - Dotnet CLI Templates
https://github.com/aws/aws-lambda-dotnet#dotnet-cli-templates

Install templates:
`> dotnet new -i "Amazon.Lambda.Templates::*"`

List Lambda templates:
`> dotnet new lambda --list`

### Creating Standalone lambda
```
PS D:\Repos\cloud-clients\aws-lambda-demo> sam init

You can preselect a particular runtime or package type when using the `sam init` experience.
Call `sam init --help` to learn more.

Which template source would you like to use?
        1 - AWS Quick Start Templates
        2 - Custom Template Location
Choice: 1

Choose an AWS Quick Start application template
        1 - Hello World Example
        2 - Multi-step workflow
        3 - Serverless API
        4 - Scheduled task
        5 - Standalone function
        6 - Data processing
        7 - Infrastructure event management
        8 - Machine Learning
Template: 5

Which runtime would you like to use?
        1 - dotnetcore3.1
        2 - nodejs14.x
        3 - nodejs12.x
Runtime: 1

Based on your selections, the only Package type available is Zip.
We will proceed to selecting the Package type as Zip.

Based on your selections, the only dependency manager available is cli-package.
We will proceed copying the template using cli-package.

Project name [sam-app]: stand-alone-lambda

Cloning from https://github.com/aws/aws-sam-cli-app-templates (process may take a moment)

    ----------------------- 
    Generating application: 
    ----------------------- 
    Name: stand-alone-lambda
    Runtime: dotnetcore3.1
    Architectures: x86_64
    Dependency Manager: cli-package
    Application Template: quick-start-from-scratch
    Output Directory: .

    Next steps can be found in the README file at ./stand-alone-lambda/README.md


    Commands you can use next
    =========================
    [*] Create pipeline: cd stand-alone-lambda && sam pipeline init --bootstrap
    [*] Test Function in the Cloud: sam sync --stack-name {stack-name} --watch

PS D:\Repos\cloud-clients\aws-lambda-demo>
```

## Testing a Lambda
`sam` commands should be executed in the root folder of the lambda project.

**Build**

`> sam build`

**Execute locally**

`> sam local start-lambda`

**Deploy resources**

`> sam deploy --profile <AWS CLI profile name> --guided`

`--guided` is needed the first time to generate the file `samconfig.toml`

**Deploy resources specifying a configuration file and adding a tag**

`> sam deploy --profile <AWS CLI profile name> --config-file samconfig.toml --tags Application=DEMO-STAND-ALONE`

## Debugging using The AWS .NET Mock Lambda Test Tool

https://github.com/aws/aws-lambda-dotnet/tree/master/Tools/LambdaTestTool

**Install**

`> dotnet tool install -g Amazon.Lambda.TestTool-3.1`

There is a version of the tool for each version of dotnet.

e.g. use 

`> dotnet tool install -g Amazon.Lambda.TestTool-6.0`

for dotnet 6.0.

**Configuration**

File `aws-lambda-tools-defaults.json` specifies properties used by the tool.

https://docs.aws.amazon.com/code-samples/latest/catalog/lambda_functions-blank-csharp-src-blank-csharp-aws-lambda-tools-defaults.json.html

Property `function-runtime` should match the `Runtime` property in the file `template.yaml`

**Configuring VS Code**

Configure launch.json as specified in 
https://github.com/aws/aws-lambda-dotnet/tree/master/Tools/LambdaTestTool

**Configuring Visual Studio**

Configure `launchSettings.json` as specified in https://github.com/aws/aws-lambda-dotnet/tree/master/Tools/LambdaTestTool
