# Prerequisites for Configuring an On\-Premises Instance<a name="instances-on-premises-prerequisites"></a>

The following prerequisites must be met before you can register an on\-premises instance\.

**Important**  
If you are using the [register\-on\-premises\-instance](http://docs.aws.amazon.com/cli/latest/reference/deploy/register-on-premises-instance.html) command and periodically refreshed temporary credentials generated with the AWS Security Token Service \(AWS STS\), there are other prerequisites\. For information, see [IAM Session ARN Registration Prerequisites](register-on-premises-instance-iam-session-arn.md#register-on-premises-instance-iam-session-arn-prerequisites)\.

**Device requirements**

The device you want to prepare, register, and tag as an on\-premises instance with AWS CodeDeploy must be running a supported operating system\. For a list, see [Operating Systems Supported by the AWS CodeDeploy Agent](codedeploy-agent.md#codedeploy-agent-supported-operating-systems)\.

If your operating system is not supported, the AWS CodeDeploy agent is available as open source for you to adapt to your needs\. For more information, see the [AWS CodeDeploy Agent](https://github.com/aws/aws-codedeploy-agent) repository in GitHub\.

**Outbound communication**

The on\-premises instance must be able to connect to public AWS service endpoints to communicate with AWS CodeDeploy\.

The AWS CodeDeploy agent communicates outbound using HTTPS over port 443\.

**Administrative control**

The local or network account used on the on\-premises instance to configure the on\-premises instance must be able to run either as `sudo` or `root` \(for Ubuntu Server\) or as an administrator \(for Windows Server\)\.

**IAM permissions**

The IAM identity you use to register the on\-premises instance must be granted permissions to complete the registration \(and to deregister the on\-premises instance, as needed\)\. 

In addition to the policy described in [Getting Started with AWS CodeDeploy](getting-started-codedeploy.md), make sure the calling IAM identity also has the following additional policy attached:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow", 
      "Action": [
        "iam:CreateAccessKey",
        "iam:CreateUser",
        "iam:DeleteAccessKey",
        "iam:DeleteUser",
        "iam:DeleteUserPolicy",
        "iam:ListAccessKeys",
        "iam:ListUserPolicies",
        "iam:PutUserPolicy",
        "iam:GetUser"
      ],
      "Resource": "*"
    }
  ]
}
```