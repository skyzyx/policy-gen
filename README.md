# Policy Genenerator

Simple Bash wrapper for [`iamlive`](https://github.com/iann0036/iamlive) that can be chained from tools like AWS Vault or AWS Okta.

## Requirements

* Bash
* [AWS CLI](https://github.com/aws/aws-cli/tree/v2)
* [jq](https://stedolan.github.io/jq/)
* [iamlive](https://github.com/iann0036/iamlive)

## Usage

Using AWS credentials for things that are not the AWS CLI is studpidly complex. A better solution is one that supports both the AWS CLI in addition to other applications written using AWS SDKs (or otherwise support AWS environment variables).

| Tool | Use-case |
|-|-|
| [AWS Vault](https://github.com/99designs/aws-vault) | For everybody. Also has native support for AWS SSO. |
| [AWS Okta](https://github.com/fiveai/aws-okta) | For those who use Okta as an enterprise SSO solution for their AWS accounts. |

```bash
# Pattern
aws-vault exec {profile} -- policy-gen -- {command}
aws-okta exec {profile} -- policy-gen -- {command}
```

If you already have a `default` profile or otherwise have AWS environment variables set, you can simply prefix your command.

```bash
# Pattern
policy-gen -- {command}
```

This doesn't work with `aws --profile {profile}` because `policy-gen` needs to be able to obtain the credentials from the environment _before_ calling the `aws` CLI tool.
