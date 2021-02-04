# AWS Templates

## Cloud Formation

### SAML User Roles

A cloud formation template that creates three commonly used user roles (Admin, Developer, Operations) and configures them for SAML login. Note, the SAML provider must be created BEFORE using this template.

### Cross Account Code Pipeline

A set of cloud formation templates to create all required roles and deployment permissions for a cross account Code Pipeline deployment using AWS Cloud Formation.

**On Tools Account**
1. Execute the deployment-s3-kms-initial cloudFormation template to provision an S3 bucket for the deployment artifacts and a KMS key used for encrypting the bucket artifacts.
**On Deployment Accounts**
2. Run the deployment-cross-account-role.yaml cloudformation template, this will provision two roles and two policies that are used to provide cross account access to the tools account.
**On Tools Account**
3. Execute the deployment-s3-kms to update the stack created in step 1, this will add permissions for the roles created in the deployment accounts.
**On Deployment Accounts**
4. Execute the deployment-artifact-access cloud formation template on the child accounts, ensuring that the S3 Bucket Name and KMS ARN are set from step 2
**On Tools Account**
5. Execute the deployment-pipelines.yaml cloud formation template on the tools account. This will provision and development and production release pipeline.