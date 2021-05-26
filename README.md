![activation-day](https://user-images.githubusercontent.com/39171066/119712609-6061f800-be26-11eb-81e6-071d7d53a026.png)

## Presentation material :speech_balloon:
* [AWS Control Tower activation day Overview & Customizations](https://github.com/jarridkleinfelter/awsctactivationday526/files/6548962/AWS.Control.Tower.activation.day.overview-customizations.pdf)
* [AWS Control Tower activation day Multi-Account Strategy](https://github.com/jarridkleinfelter/awsctactivationday526/files/6548959/AWS.Control.Tower.activation.day.multi-account-strategy.pdf)

## Labs :goggles:
### [Link to labs](https://controltower.aws-management.tools/)

## Reference Material :bookmark_tabs:
* [Getting started with AWS Control Tower video](https://www.youtube.com/watch?v=2t-VkWt0rKk)
* [Management & Governance how to videos](https://www.youtube.com/playlist?list=PLhr1KZpdzukcaA06WloeNmGlnM_f1LrdP)
* [AWS Management & Governance Blog](https://aws.amazon.com/blogs/mt/)
* [AWS Organizations documentation](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_introduction.html)
* [Getting started with AWS Control Tower](https://docs.aws.amazon.com/controltower/latest/userguide/getting-started-with-control-tower.html)
* [AWS Well-Architected](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc)

## Question & Answer :raising_hand_woman:
> Do the original IAM configuration for accounts remain after being enrolled into CT?

Yes, users can still log into accounts with existing IAM credentials even after enrolling a new account to Control Tower and enabling SSO

> What is the process to enroll existing account into CT?

* https://docs.aws.amazon.com/controltower/latest/userguide/enroll-account.html
* https://aws.amazon.com/blogs/architecture/field-notes-enroll-existing-aws-accounts-into-aws-control-tower/

> How to use Athena to query logs when the prefix layers include the accts so the structure is different than the documentation for utilizing Athena to access CloudTrail logs -

non-aws blog post - https://alsmola.medium.com/use-aws-glue-to-make-cloudtrail-parquet-partitions-c903470dc3e5

> How to set up Athena to query AWS Config data considering the centralized log bucket is consolidated

2 blogs which describe how to query and visualize AWS Config data using Athena & Quicksight. These blogs focus on setting up tables manually for specific account-region pairs. When you have scale this becomes difficult to manage.
* https://aws.amazon.com/blogs/mt/how-to-query-your-aws-resource-configuration-states-using-aws-config-and-amazon-athena/
* https://aws.amazon.com/blogs/mt/visualizing-aws-config-data-using-amazon-athena-and-amazon-quicksight/#step-3

An option is to use Glue Crawler to target the specific log prefix and exclude non Config prefixes
Include paths    s3://aws-controltower-logs-XXXXXXXXXXXXX-us-east-2/o-XXXXXXXXXX/AWSLogs/
Exclude patterns    /CloudTrail-Digest, /CloudTrail, */Config/ConfigWritabilityCheckFile


> is there an option to add a preventative budget guardrail into a DEV/TEST account, if so, what happens to the account/services in the account, when it hits that budget threshold?

AWS Budgets can be set for notifications or can trigger actions to turn off resources
* https://aws.amazon.com/about-aws/whats-new/2020/10/announcing-aws-budgets-actions/

Also consider proactive measures to address cost such as EC2 instance scheduler
* https://aws.amazon.com/solutions/implementations/instance-scheduler/

> Can customers launch Control Tower into another account other than the Master Payer?

You want Control Tower to be deployed into an account with minimal workloads. Control Tower must be deployed in the management account.

> Is there a list of Control Tower guardrails?

https://docs.aws.amazon.com/controltower/latest/userguide/guardrails-reference.html

> When importing existing accounts into an OU, can they be imported with the existing VPC and CIDRs?

Yes, the enrollment/import process does not change any of that

> Why do accounts still have a VPC in all regions even if they have been disabled in Control Tower account factory

The regions you have de-selected for VPC creation in CT account factory do still contain the default VPC. Control Tower will replace the default with the custom if you have a region selected. If a region is not selected, the default remains.

> Is there differentiation of user accounts so that you can have super admins to manage the whole service, security admins to only view/manage security aspects, etc. In other words, how flexible are the groups/roles?

CloudChekr is built on a RBAC system. They allow policies, permission sets that attach to a role. Users & Accounts map to roles

> How to contact CloudChekr

partners@cloudcheckr.com or check AWS marketplace
