# ProjectCloudBigaDataM1

<!-- TODO -->

# IAM Quiz
### Which statement describes AWS identity and access Management IAM users ?
-Every IAM user for an account must have a unique name.
### How can you grant the same level of permissions to multiple users within an account ?
-Apply an AWS IAM policy to an IAM group. 
### Which statements describe AWS Identity and Access Management IAM roles (select two)
-They can be assumed by individuals, applications or services.
-They provide temporary security credentials. 
### Which Statement describes a resources based policy ? 
-It is always an inline policy
### How does AWS Identity and Access Management IAM evaluate a policy ? 
-It checks for explicit deny statements before it checks for explicit allow statements.
### A team of developers needs access to several services and resources in a virtual private cloud VPC for 9 months. How can you use AWS Identity and Access Management IAM to enable access for them ? 
-Create a IAM user for each developer, put them all in an IAM group, and attach the required IAM policies to the IAM group.
### How does identity federation increase security for an application that is built in Amazon Web Services AWS ? 
-Users can use SSO to access the application through an existing authenticated identity. 

# Networking Quiz
### Which definition describes a virtual private cloud VPC ?
-A logically isolated virtual network that you define in the AWS Cloud
### A company’s VPC has the CIDR block 172.16.0.0/21 (2048 addresses). It has two subnets (A and B). Each subnet must support 100 usable addresses now, but this number is expected to rise to at most 254 usable addresses soon. Which subnet addressing scheme meets the requirements and follows AWS best practices? 
-Subnet A: 172.16.0.0/23 (512 addresses) Subnet B: 172.16.2.0/23 (512 addresses)
### Which combination of actions enables direct internet access for IPv4 hosts in a virtual private cloud (VPC) ? (Select THREE.) 
-Configuring hosts to have or obtain an internet-routable address
-Creating a route for 0.0.0.0/0 that points to the internet gateway
-Configuring security groups and network ACLs to permit internet traffic
###Several EC2 instances launch in a VPC that has internet access. These instances should not be accessible from the internet, but they must be able to download updates from the internet. How should the instances launch?
-Without public IP addresses, in a subnet with a default route to a NAT gateway

# Policies evaluation Quiz
### Question: What actions are allowed for EC2 instances and S3 objects based on this policy? What specific resources are included?
For EC2 instances:
ec2:DescribeVpcs: This action allows the user to describe the virtual private clouds (VPCs) in the AWS account.
ec2:DescribeSubnets: This action allows the user to describe the subnets in the AWS account.
ec2:DescribeSecurityGroups: This action allows the user to describe the security groups in the AWS account.
For S3 objects:
There are no specific actions related to S3 objects mentioned in this policy. The policy only allows actions related to EC2 instances.
Resources:
The policy applies to all resources (denoted by "*"). It doesn't limit the scope to specific resources within EC2 or S3.

### Question: Under what condition does this policy allow access to VPC-related information? Which AWS region is specified?
Condition:
s3:prefix: This condition specifies that the access is allowed only when the S3 object key prefix matches either "documents/" or "images/".
Effect:
Allow: This effect allows the specified actions when the conditions are met.
Actions:
s3:GetObject: Allows getting (reading) objects from the specified S3 bucket and objects matching the specified prefix.
s3:PutObject: Allows putting (writing) objects into the specified S3 bucket and objects matching the specified prefix.
s3:ListBucket: Allows listing the contents (objects) of the specified S3 bucket.
Resources:
"arn:aws:s3:::example-bucket": Refers to the specified S3 bucket named "example-bucket".
"arn:aws:s3:::example-bucket/*": Refers to objects within the "example-bucket" that match any key prefix.
The policy does not specify any AWS region. Therefore, it applies to all regions where the specified S3 bucket exists.

### Question: What actions are allowed on the "example-bucket" and its objects based on this policy? What specific prefixes are specified in the condition?
iam:CreateUser and iam:DeleteUser. The actions are allowed for IAM users, and the specific IAM user is determined by the variable ${aws:username}.
Actions:
iam:CreateUser: Allows creating IAM users.
iam:DeleteUser: Allows deleting IAM users.
Resources:
"arn:aws:iam::123456789012:user/${aws:username}": Refers to the IAM user resource with the AWS account ID "123456789012" and the specific IAM username determined by ${aws:username}.
The policy doesn't specify any specific S3 bucket or object actions. It solely focuses on IAM user creation and deletion.

### Question: What actions are allowed for IAM users based on this policy? How are the resource ARNs constructed?
Actions:
iam:Get*: Allows all actions that start with "iam:Get". This includes actions like iam:GetUser, iam:GetGroup, iam:GetRole, etc. It allows retrieving information about IAM users, groups, roles, policies, and other related resources.
iam:List*: Allows all actions that start with "iam:List". This includes actions like iam:ListUsers, iam:ListGroups, iam:ListRoles, etc. It allows listing information about IAM users, groups, roles, policies, and other related resources.
Resources:
"*": The resource ARN is constructed using the wildcard (*) character, which matches any IAM resource. It allows the specified actions (iam:Get* and iam:List*) to be performed on any IAM resource in the AWS account.

### Questions:
### Which AWS service does this policy grant you access to?
### Does it allow you to create an IAM user, group, policy, or role?
### Go to https://docs.aws.amazon.com/IAM/latest/UserGuide/ and in the left navigation expand Reference > Policy Reference > Actions, Resources, and Condition Keys. Choose Identity And Access Management. Scroll to the Actions Defined by Identity And Access Management list.��Name at least three specific actions that the iam:Get* action allows.

The Policy grants access to the AWS service called Amazon Elastic Compute Cloud (EC2)
The policy allows two actions on EC2 instances:
ec2:RunInstances: This action allows users to launch new EC2 instances.
ec2:StartInstances: This action allows users to start existing EC2 instances.
Regarding IAM-related actions, the policy does not explicitly mention permissions for creating IAM users, groups, policies, or roles. It focuses on EC2 instance-related actions.
here are three specific actions that the iam:Get* action allows :
iam:GetUser: Retrieves information about an IAM user.
iam:GetGroup: Retrieves information about an IAM group.
iam:GetRole: Retrieves information about an IAM role.

### Questions:
### What actions does the policy allow?
### Say that the policy included an additional statement object, like this example:
### How would the policy restrict the access granted to you by this additional statement?
### If the policy included both the statement on the left and the statement in question 2, could you terminate an m3.xlarge instance that existed in the account?

The Policy allows two actions:
ec2:RunInstances: This action allows users to launch new EC2 instances.
ec2:StartInstances: This action allows users to start existing EC2 instances.
The additional statement allows all EC2 actions (wildcard *), which means it grants full access to all EC2 actions available in the AWS API.
In this case, the original policy's Deny effect for the ec2:RunInstances and ec2:StartInstances actions would be overridden by the new Allow statement that allows all EC2 actions. Therefore, you would have permission to terminate an m3.xlarge instance if it existed in the account since the ec2:TerminateInstances action is part of the ec2:* set of actions.


