# IAM
---

IAM offers the following features:
- Centralised control of your AWS account
- Shared Access to your AWS account
- Granular Permissions
- Identity Federation(including Active Directory, facebook, linkedin)
- Multifactor Authentication
- Provide temporary access for users/devices and services where necessary
- Allows you to set your own password policy
- Integrated with many different AWS services

**MFA types**:
	- Virtual MFA device
	- U2F security key
	- Other hardware MFA device

* IAM is universal. It doesnot apply to the regions at this time

---

##### Q: Can IAM users have individual EC2 SSH keys?
Not in the initial release. IAM does not affect EC2 SSH keys or Windows RDP certificates. This means that although each user has separate credentials for accessing web service APIs, they must share SSH keys that are common across the AWS account under which users have been defined.

##### Q: Where can I use my SSH keys?
Currently, IAM users can use their SSH keys only with **AWS CodeCommit** to access their repositories.

##### Q: Do IAM user names have to be email addresses?
**No**, but they can be. User names are just ASCII strings that are unique within a given AWS account. You can assign names using any naming convention you choose, including email addresses.

##### Q: Can I set usage quotas on IAM users?
**No.** All limits are on the AWS account as a whole. For example, if your AWS account has a limit of 20 Amazon EC2 instances, IAM users with EC2 permissions can start instances up to the limit. You cannot limit what an individual user can do.

##### Q: How many IAM roles can I assume?
There is no limit to the number of IAM roles you can assume, but you can only act as one IAM role when making requests to AWS services.


##### Q: How much do IAM roles cost?
IAM roles are free of charge. You will continue to pay for any resources a role in your AWS account consumes.

##### Q: What is the difference between an IAM role and an IAM user?
An IAM user has permanent long-term credentials and is used to directly interact with AWS services. An IAM role does not have any credentials and cannot make direct requests to AWS services. IAM roles are meant to be assumed by authorized entities, such as IAM users, applications, or an AWS service such as EC2.

##### Q: When should I use an IAM user, IAM group, or IAM role?
- An IAM user has permanent long-term credentials and is used to directly interact with AWS services.
- An IAM group is primarily a management convenience to manage the same set of permissions for a set of IAM users. 
- An IAM role is an AWS Identity and Access Management (IAM) entity with permissions to make AWS service requests. IAM roles cannot make direct requests to AWS services; they are meant to be assumed by authorized entities, such as IAM users, applications, or AWS services such as EC2. Use IAM roles to delegate access within or between AWS accounts.

##### Q: How many IAM roles can I create?
You are limited to 1,000 IAM roles under your AWS account. If you need more roles, submit the IAM limit increase request form with your use case, and we will consider your request.

##### Q: Can I add an IAM role to an IAM group?
Not at this time.

##### Q: What are the features of IAM roles for EC2 instances?
IAM roles for EC2 instances provides the following features:

	AWS temporary security credentials to use when making requests from running EC2 instances to AWS services.
	Automatic rotation of the AWS temporary security credentials.
	Granular AWS service permissions for applications running on EC2 instances.


##### Q: Can I associate more than one IAM role with an EC2 instance? 
* **No**. You can only associate one IAM role with an EC2 instance at this time. This limit of one role per instance cannot be increased.

##### Q: Who can access the access keys on an EC2 instance?
Any local user on the instance can access the access keys associated with the IAM role.

##### Q: How do I use the IAM role with my application on the EC2 instance?
If you develop your application with the AWS SDK, the AWS SDK automatically uses the AWS access keys that have been made available on the EC2 instance. If you are not using the AWS SDK, you can retrieve the access keys from the EC2 instance metadata service. 

##### Q: What is a service-linked role?
A service-linked role is a type of role that links to an AWS service (also known as a linked service) such that only the linked service can assume the role. Using these roles, you can delegate permissions to AWS services to create and manage AWS resources on your behalf.

##### Q: What are managed policies?
Managed policies are IAM resources that express permissions using the IAM policy language. You can create, edit, and manage separately from the IAM users, groups, and roles to which they are attached. After you attach a managed policy to multiple IAM users, groups, or roles, you can update that policy in one place and the permissions automatically extend to all attached entities. Managed policies are managed either by you (these are called customer managed policies) or by AWS (these are called AWS managed policies).

##### Q: How do I assign commonly used permissions?
AWS provides a set of commonly used permissions that you can attach to IAM users, groups, and roles in your account. These are called AWS managed policies. One example is read-only access for Amazon S3. When AWS updates these policies, the permissions are applied automatically to the users, groups, and roles to which the policy is attached. AWS managed policies automatically appear in the Policies section of the IAM console. When you assign permissions, you can use an AWS managed policy or you can create your own customer managed policy. Create a new policy based on an existing AWS managed policy, or define your own.

##### Q: What is the difference between assigning permissions using IAM groups and assigning permissions using managed policies?
Use IAM groups to collect IAM users and define common permissions for those users. Use managed policies to share permissions across IAM users, groups, and roles. For example, if you want a group of users to be able to launch an Amazon EC2 instance, and you also want the role on that instance to have the same permissions as the users in the group, you can create a managed policy and assign it to the group of users and the role on the Amazon EC2 instance.

##### Q: Can I use a managed policy as a resource-based policy?
Managed policies can only be attached to IAM users, groups, or roles. You cannot use them as resource-based policies.

##### Q: Is there an authentication API to verify IAM user sign-ins? 
No. There is no programmatic way to verify user sign-ins.

##### Q: What is identity federation? 
AWS Identity and Access Management (IAM) supports identity federation for delegated access to the AWS Management Console or AWS APIs. With identity federation, external identities are granted secure access to resources in your AWS account without having to create IAM users. These external identities can come from your corporate identity provider (such as Microsoft Active Directory or from the AWS Directory Service) or from a web identity provider (such as Amazon Cognito, Login with Amazon, Facebook, Google, or any OpenID Connect-compatible provider).


##### Q: What are federated users? 
Federated users (external identities) are users you manage outside of AWS in your corporate directory, but to whom you grant access to your AWS account using temporary security credentials. They differ from IAM users, which are created and maintained in your AWS account.

##### Q: Do you support SAML? 
Yes, AWS supports the Security Assertion Markup Language (SAML) 2.0.


##### Q. How does AWS MFA work?
There are two primary ways to authenticate using an AWS MFA device:

	AWS Management Console users: When a user with MFA enabled signs in to an AWS website, they are prompted for their user name and password (the first factor–what they know), and an authentication response from their AWS MFA device (the second factor–what they have). All AWS websites that require sign-in, such as the AWS Management Console, fully support AWS MFA. You can also use AWS MFA together with Amazon S3 secure delete for additional protection of your S3 stored versions.
	AWS API users: You can enforce MFA authentication by adding MFA restrictions to your IAM policies. To access APIs and resources protected in this way, developers can request temporary security credentials and pass optional MFA parameters in their AWS Security Token Service (STS) API requests (the service that issues temporary security credentials). MFA-validated temporary security credentials can be used to call MFA-protected APIs and resources. Note: AWS STS and MFA-protected APIs do not currently support U2F security key as MFA.
