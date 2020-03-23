# Enumerating AWS Resources
One of the bigger challenges in AWS is enumerating resources.
Believe it or not, there is NO WAY to easily view ALL resources in an AWS account (!).
Other cloud providers provide such an "all resources" view. But in AWS, you have to navigate to
virtually every resource type (roughly 147) in every region (20-something) and look. Ouch!

Alas, there are a few *tricks* that can help soften the impact of this odd 
and frustrating limitation.
In any of the solutions below, you will need to have full read access
to *all* resoource type in order to "see" them.
Note that the built-in AWS **ReadOnlyAccess** policy does NOT have sufficient permission to see *all* resource types.

**NOTE:** This document is a *work in progress*. Are you aware of any other approaches?
There are some 3rd party solutions which will provide a view. Comments and suggestions are welcomed!

## Billing Data / Cost Explorer
The one definitiove source of truth is the billing data.
It lists everything that you pay for, and how much each item costs on a daily basis.
While the billing data provides a list of all resources, it does NOT include the detailed configuration of each.
But armed with the list of ARNs, it is easier to retrieve the details for each resource.
The downside to this approach is that any resources created since the last billing day cycle won't appear
(generally 24 hours).

You can view the billing data in the AWS console (portal) using [AWS Cost Explorer](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/).

## Tag Editor
Another approach is to use the [Tag Editor](https://console.aws.amazon.com/resource-groups/tag-editor/find-resources)
to find resources.

https://docs.aws.amazon.com/ARG/latest/userguide/tag-editor.html

There are several limitations:
* The underlying GetResources API is only capable of enumerating resources which have one or more tags (or have been previously tagged).
SEE: https://docs.aws.amazon.com/resourcegroupstagging/latest/APIReference/API_GetResources.html
* Not all AWS resources are capable of being tagged. This will only work with supported resources types. 
SEE: https://docs.aws.amazon.com/ARG/latest/userguide/supported-resources.html

The AWS CLI can be used for each region:
```
$ aws resourcegroupstaggingapi get-resources --region region_name
```


## AWS Config
Yet another approach is 
[AWS Config](http://docs.aws.amazon.com/config/latest/developerguide/WhatIsConfig.html),
which provides a detailed view of the configuration of AWS resources in each AWS account.
This includes how the resources are related to one another and how they were configured in the
past so that you can see how the configurations and relationships change over time.

However, AWS Config only collects information about EC2/VPC-related resources, not everything in your AWS account.
It does not cover services such as lambdas, SNS, SQS, etc.

The AWS CLI can be done for each region and each resource type:
```
$ aws configservice list-discovered-resources
```
Drawbacks here is that you must enable AWS config and it then only captures resources as and when they change.
AWS config  can also be quite expensive.
The console page may be accessed at:
https://console.aws.amazon.com/config/home?region=us-east-1#/resource-listing


## CloudWatch
Another approach might be to use cloudwatch events over time to construct a view of
all resources. A lambda function could be tied to the events which then manages the list of resources
along with the latest configuration in a Neptune or RDS database.  Food for thought...


## Multiple AWS Accounts
Options for enumerating resources across multiple accounts are limited to 3rd party tools,
some free / open source; in additon to paid solutions.


## 3rd Party Open Source Options
Some of the open source tools include:

* https://github.com/awslabs/aws-multi-account-viewer 
* https://www.nccgroup.trust/uk/about-us/newsroom-and-events/blogs/2018/may/aws-inventory-a-tool-for-mapping-aws-resources/
* https://github.com/devops-israel/aws-inventory (dependant on [CORS](https://enable-cors.org/) enablement for AWS services)


---
## Additional Resources

* https://github.com/aws/aws-sdk-js/blob/master/SERVICES.md
* https://stackoverflow.com/questions/44391817/is-there-a-way-to-list-all-resources-in-aws
* https://forums.aws.amazon.com/thread.jspa?threadID=235322
* https://github.com/lesterw1/AwsServices (generates a list of services)


---
## Other Cloud Providers
In comparison, other cloud providers have provided more efficient solutions to resource enumeration.
HINT TO AWS: Provide an enumerate reosurce API please!

### Microsoft Azure
A customer is able to see all resources across all their subscriptions in a single view in the Azure portal.
There is even a "Resources" REST API (and PowerShell cmdlet) which will enumerate all resources across all subscriptions in a given subscription.
More recently, Microsoft has added the **Azure Resource Graph** where kusto queries can be used to rapidly query all resources
across all visible subscriptions in one go (!!). This is VERY impressive and very fast.

### Google Cloud Platform (GCP)
All resources in Google Cloud Platform (GCP) are organized into a hierarchy, with each node (Organizations, Folders, Projects, and so forth) having a reference to its parent. This makes it easy to programmatically iterate trhough and enumerate all resources using 
a single API. See [listing all reosurces](https://cloud.google.com/resource-manager/docs/listing-all-resources) for more information.

---
## Next Steps
I would like to see a solution that has the ability to rapidly query all AWS resources across all accounts using a
query solution similar to that offered by Microsoft's Azure Resource Explorer.

I am tempted to write some scripts which: (a) enumerates all the AWS resources; and then (b) hooks into AWS CloudWatch to capture resource changes; and then (c) pushes the current AWS resource configuration into [Azure Data Explorer](https://azure.microsoft.com/en-us/services/data-explorer/). This would allow Kusto to be used to query the respective resources. Maybe someday...
