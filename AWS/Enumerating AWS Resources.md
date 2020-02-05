# Enumerating AWS Resources
One of the bigger challenges in AWS is enumerating resources.
Believe it or not, unlike Azure, there is no single view of all resources in an AWS account.
The brute force way is to navigate to every resource type (roughly 147) in every region (20-something).

Alas, there are a few *tricks* that can help. In any of the cases below, you will need to have full read access
to every resoource type in order to "see" them.
Note that the built-in AWS **ReadOnlyAccess** policy does NOT have sufficient permission to see all resource types.

### Work in Progress
Note that this document is a work-in-progress. Contributions and corrected are welcomed!


## Billing Data / Cost Explorer
The billing data lists everything you have and how much it costs, on a daily basis.
While the billing data provides a list of all resources, it does NOT include the detailed configuration of each.
But armed with the list of ARNs, it is easier to retrieve the details for each resource.
The downside to this approach is that any resources created since the last billing day cycle won't appear.

You can view the billing data in the AWS console (portal) using [AWS Cost Explorer](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/) at:
TBD

## Tag Editor
You can use the [Tag Editor](https://console.aws.amazon.com/resource-groups/tag-editor/find-resources)
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

[AWS Config](http://docs.aws.amazon.com/config/latest/developerguide/WhatIsConfig.html)
provides a detailed view of the configuration of AWS resources in each AWS account.
This includes how the resources are related to one another and how they were configured in the
past so that you can see how the configurations and relationships change over time.

However, AWS Config only collects information about EC2/VPC-related resources, not everything in your AWS account.
It does not cover services such as lambdas, SNS, SQS, etc.

The AWS CLI can be done for each region and each resource type:
```
$ aws configservice list-discovered-resources
```

The console page may be accessed at:
https://console.aws.amazon.com/config/home?region=us-east-1#/resource-listing


## CloudWatch
Another approach might be to use cloudwatch events over time to construct a view of
all resources. A lambda function could be tied to the events which then manages the list of resources
along with the latest configuration in a Neptune or RDS database.  Food for thought...


## Multiple AWS Accounts
Options for enumerating resources across multiple accounts are limited to 3rd party tools.


## 3rd Party Open Source Options
So far

* https://github.com/awslabs/aws-multi-account-viewer 
* https://www.nccgroup.trust/uk/about-us/newsroom-and-events/blogs/2018/may/aws-inventory-a-tool-for-mapping-aws-resources/
* https://github.com/devops-israel/aws-inventory (dependant on [CORS](https://enable-cors.org/) enablement for AWS services)


---
## Additional Resources

* https://github.com/aws/aws-sdk-js/blob/master/SERVICES.md
* https://stackoverflow.com/questions/44391817/is-there-a-way-to-list-all-resources-in-aws
* https://forums.aws.amazon.com/thread.jspa?threadID=235322


---
## Other Cloud Providers

### Azure
In contrast, a customer is able to see all resources across all their subscriptions in a single view in the Azure portal.
There is even a "Resources" REST API (and PowerShell cmdlet) which will enumerate all resources across all subscriptions in a given subscription.
More recently, Microsoft has added the Azure Resource Graph where kusto queries can be used to rapidly query all resources
across all visible subscriptions in one go! Hint hint AWS!

### GCP
TBD
