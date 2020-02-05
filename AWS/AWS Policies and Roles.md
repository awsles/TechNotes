# AWS Policies and Roles
One of the first steps in securing an AWS accounts is creating proper role definitions
which not only meet the needs of the business, but also reasonably satisfy
the principles of *least privilege* and *segregation of duty*. 
Sometimes, these principles are treated as laws, resulting in an excessive
number of policy definitions, increased management overhead (forever updating different polices as AWS
services evolve), and a different kind of increased risk.

## Account Segregation
In a larger enterprise, you may have 50 or even 100+ AWS accounts. I strongly recommend that
separate AWS accounts be established for:
1) Development/Test ("DevTest") 
2) Pre-Production / Staging
3) Production

This will allow you to have different roles and policies, based on the account's purpose.

## Standardize Your Policies and Roles
Some people prefer to use the built-in AWS policies to associate with roles and users.
In practice though, I have found that the AWS standard policy definitions are often too 
vertical in nature, and so multiple policicies have to be combined to achieve the desired effect.
And remember, there is a limit of 10 policies that can be associated to any single role or user.
Also, the AWS **ReadOnlyPolicy** lacks quite a few services.

I tend to prefer creating custom roles which better align to business and security needs.
My recommendations include:

* Creating custom policy definitions which align to business and security needs.
* Standardize the policy definitions across all accounts (e.g., a "Developer" policy has the
exact same permissions in every account).
* If a specific permission is required in one account, create (or use a built-in) separate policy for that permission
and attach it to the role. For example, you may not normally grant CDN permissions, but may wish to
allow it as an exception.
* Put your policy JSON documents into an internal GIT repository so that they can be governed.
* Automate the deployment of policy documents and roles. Personally, I wrote a PowerShell
script which allows me to select policy documents and push them to multiple AWS accounts
(note that it does some minimal account number substitutions as needed).
* Standardize your policy and role naming convention.
* Never define a policy or role with an 'AWS' prefix. Such roles are typically created by AWS, so avoid using
anything that looks like AWS may have created it.
* Enable AWS Organizations and aall of the features therein.
* Implement a [Service Control Policy (SCP)](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scp.html).
Note that this requires AWS organizations to be enabled and configured.
* Apply a boundary policy to users and role definitions. The boundary policy should re-iterate any
restrictions of the SCP





## Useful Resources
Below are some useful tools and resources which may help in securing role access in your AWS accounts.

* [Principal Mapper (pmapper)](https://www.nccgroup.trust/uk/our-research/principal-mapper-pmapper/)
-- This tool uses the existing simulator APIs to determine which users and roles have access to each other.
It provides a query interface on top of this data and can help fid prvilege escalation paths.

