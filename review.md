# AWS Certified DevOps Engineer – Professional (DOP-C02) Practice Questions

This document contains 75 practice questions distributed across the six domains of the AWS Certified DevOps Engineer – Professional (DOP-C02) exam, based on the official weightings: Domain 1 (22%), Domain 2 (17%), Domain 3 (15%), Domain 4 (15%), Domain 5 (14%), Domain 6 (17%). Questions reflect key details and exam focus areas, formatted as multiple-choice or multiple-response to mimic the real exam.

---

## Domain 1: SDLC Automation (22%) - 17 Questions

### Question 1
Your team needs to automate frequent code commits with testing. Which AWS service should you use to trigger builds automatically when code is pushed to a GitHub repository?  
A. AWS CodeCommit  
B. AWS CodePipeline  
C. AWS CodeBuild  
D. AWS CodeDeploy  
**Answer**: B  
**Explanation**: CodePipeline orchestrates CI/CD workflows and can trigger builds on GitHub commits.

### Question 2
A CodePipeline stage fails due to insufficient permissions. What should you check first?  
A. The buildspec.yml file  
B. The IAM role attached to the pipeline  
C. The S3 bucket encryption settings  
D. The CodeBuild environment variables  
**Answer**: B  
**Explanation**: IAM role issues are a common cause of pipeline stage failures.

### Question 3 (Multiple-Response)
Which TWO actions can you take to optimize a slow CodeBuild process?  
A. Increase the compute size of the build environment  
B. Enable dependency caching in buildspec.yml  
C. Switch to a rolling deployment  
D. Add more manual approval stages  
**Answers**: A, B  
**Explanation**: Larger compute and caching improve build performance; C and D are unrelated.

### Question 4
You need zero-downtime deployment to EC2 instances. Which CodeDeploy strategy should you use?  
A. In-place  
B. Blue/Green  
C. Rolling  
D. All at Once  
**Answer**: B  
**Explanation**: Blue/Green ensures zero downtime by switching traffic to new instances.

### Question 5
A CodeDeploy deployment to ECS fails. Where is this defined?  
A. buildspec.yml  
B. appspec.yml  
C. Dockerfile  
D. CloudFormation template  
**Answer**: B  
**Explanation**: `appspec.yml` defines deployment steps for CodeDeploy.

### Question 6
Your company migrates from CodeCommit to GitHub. How should you update CodePipeline?  
A. Reconfigure the Source stage to use GitHub  
B. Redeploy the pipeline with a new IAM role  
C. Update the buildspec.yml file  
D. Enable EventBridge monitoring  
**Answer**: A  
**Explanation**: Source stage reconfiguration integrates GitHub post-deprecation.

### Question 7
Which service manages software dependencies like Maven packages?  
A. AWS CodeStar  
B. AWS CodeArtifact  
C. AWS CodeGuru  
D. AWS CodeBuild  
**Answer**: B  
**Explanation**: CodeArtifact handles package management.

### Question 8
CodeGuru Reviewer flags a resource leak in your Java code. What should you do?  
A. Increase Lambda concurrency  
B. Fix the code based on recommendations  
C. Adjust the buildspec.yml timeout  
D. Deploy with blue/green strategy  
**Answer**: B  
**Explanation**: CodeGuru provides actionable code quality fixes.

### Question 9
A multi-region CodePipeline fails to access artifacts. What’s the likely cause?  
A. Missing S3 bucket versioning  
B. Incorrect IAM permissions for cross-region access  
C. Disabled CloudWatch Events  
D. No manual approval stage  
**Answer**: B  
**Explanation**: Cross-region artifact access requires proper IAM permissions.

### Question 10
Which file specifies build commands for CodeBuild?  
A. appspec.yml  
B. buildspec.yml  
C. Dockerfile  
D. pipeline.yml  
**Answer**: B  
**Explanation**: `buildspec.yml` defines CodeBuild phases.

### Question 11
You need to deploy to Lambda with traffic shifting. Which service integrates with CodePipeline?  
A. AWS CodeDeploy  
B. AWS CodeStar  
C. AWS CodeArtifact  
D. AWS CodeCommit  
**Answer**: A  
**Explanation**: CodeDeploy supports Lambda traffic shifting.

### Question 12
A CodeBuild job needs access to a private RDS instance. What should you configure?  
A. VPC settings in CodeBuild  
B. S3 bucket policy  
C. IAM role permissions  
D. CloudWatch Logs subscription  
**Answer**: A  
**Explanation**: VPC integration allows CodeBuild to access private resources.

### Question 13
Which deployment type should you use for quick iterations in a dev environment?  
A. Blue/Green  
B. Rolling  
C. All at Once  
D. Immutable  
**Answer**: C  
**Explanation**: All at Once is fastest but incurs downtime, suitable for dev.

### Question 14
How does CodeGuru Profiler help with Lambda?  
A. Automates deployments  
B. Identifies performance bottlenecks  
C. Manages package dependencies  
D. Triggers pipeline stages  
**Answer**: B  
**Explanation**: Profiler optimizes runtime performance.

### Question 15
Your pipeline artifacts are missing in S3. What should you verify?  
A. CodeBuild environment variables  
B. CodePipeline stage output configuration  
C. GitHub webhook settings  
D. IAM user permissions  
**Answer**: B  
**Explanation**: Stage output config ensures artifacts are stored in S3.

### Question 16
Which service provides a unified dashboard for CI/CD?  
A. AWS CodePipeline  
B. AWS CodeStar  
C. AWS CodeDeploy  
D. AWS CodeBuild  
**Answer**: B  
**Explanation**: CodeStar offers a unified project management view.

### Question 17
A CodeArtifact repository needs cross-account access. What must you configure?  
A. Domain policy  
B. S3 bucket policy  
C. VPC endpoint  
D. CloudTrail logging  
**Answer**: A  
**Explanation**: Domain policy enables cross-account package sharing.

---

## Domain 2: Configuration Management and IaC (17%) - 13 Questions

### Question 18
A CloudFormation stack fails to create. Where should you look first?  
A. CloudTrail logs  
B. Stack events in the console  
C. S3 bucket permissions  
D. CodePipeline logs  
**Answer**: B  
**Explanation**: Stack events detail creation failures.

### Question 19
Which CloudFormation component is mandatory?  
A. Parameters  
B. Resources  
C. Mappings  
D. Outputs  
**Answer**: B  
**Explanation**: Resources define what’s created; others are optional.

### Question 20
You need to reference an EC2 instance ID in CloudFormation. Which function?  
A. Fn::GetAtt  
B. Fn::Sub  
C. Fn::FindInMap  
D. Fn::Ref  
**Answer**: D  
**Explanation**: `Ref` returns the resource’s physical ID.

### Question 21
A StackSet deployment fails in one region. What’s the likely cause?  
A. Missing IAM permissions  
B. Incorrect S3 bucket name  
C. Disabled CloudWatch metrics  
D. No manual approval  
**Answer**: A  
**Explanation**: StackSets require cross-region/account IAM permissions.

### Question 22
Elastic Beanstalk deployment causes downtime. Which mode should you switch to?  
A. All at Once  
B. Rolling  
C. Blue/Green  
D. Immutable  
**Answer**: C  
**Explanation**: Blue/Green ensures zero downtime by switching environments.

### Question 23
How do you customize an Elastic Beanstalk environment?  
A. Modify buildspec.yml  
B. Use .ebextensions  
C. Update appspec.yml  
D. Adjust StackSet policies  
**Answer**: B  
**Explanation**: `.ebextensions` customizes Beanstalk configurations.

### Question 24
A CloudFormation update rolls back. What should you check?  
A. Resource dependencies  
B. S3 artifact versioning  
C. CodeDeploy hooks  
D. GitHub triggers  
**Answer**: A  
**Explanation**: Dependency issues often cause update failures.

### Question 25
Which deployment mode spins up new instances without downtime in Beanstalk?  
A. Rolling  
B. Immutable  
C. All at Once  
D. Blue/Green  
**Answer**: B  
**Explanation**: Immutable launches new instances, avoiding downtime.

### Question 26
You need to pass a dynamic value to CloudFormation. What should you use?  
A. Parameters  
B. Mappings  
C. Conditions  
D. Outputs  
**Answer**: A  
**Explanation**: Parameters allow dynamic inputs.

### Question 27
A Beanstalk app needs a worker tier. What should you configure?  
A. SQS queue integration  
B. ALB target group  
C. RDS read replica  
D. CloudFormation nested stack  
**Answer**: A  
**Explanation**: Worker tier processes SQS messages.

### Question 28
Which function retrieves an attribute like an EC2 instance’s AZ?  
A. Fn::Ref  
B. Fn::GetAtt  
C. Fn::Sub  
D. Fn::ImportValue  
**Answer**: B  
**Explanation**: `GetAtt` fetches resource attributes.

### Question 29
A CloudFormation stack needs to deploy across accounts. What should you use?  
A. StackSets  
B. Nested Stacks  
C. CodePipeline  
D. Elastic Beanstalk  
**Answer**: A  
**Explanation**: StackSets manage multi-account/region deployments.

### Question 30
You need to test a new Beanstalk version with 10% traffic. Which mode?  
A. Rolling  
B. Blue/Green with traffic splitting  
C. All at Once  
D. Immutable  
**Answer**: B  
**Explanation**: Blue/Green with traffic splitting supports canary testing.

---

## Domain 3: Resilient Cloud Solutions (15%) - 11 Questions

### Question 31
An RDS instance fails over slowly. What should you verify?  
A. Multi-AZ configuration  
B. S3 CRR settings  
C. Lambda concurrency  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: Multi-AZ ensures fast failover for RDS.

### Question 32
Which service provides active-active replication across regions?  
A. RDS Multi-AZ  
B. DynamoDB Global Tables  
C. ElastiCache Multi-AZ  
D. S3 CRR  
**Answer**: B  
**Explanation**: Global Tables support multi-region writes.

### Question 33
Your app requires low RTO in DR. Which strategy?  
A. Backup and Restore  
B. Pilot Light  
C. Warm Standby  
D. Multi-Site  
**Answer**: D  
**Explanation**: Multi-Site offers the lowest RTO.

### Question 34
Lambda functions throttle under high load. What should you adjust?  
A. Memory allocation  
B. Concurrency limit  
C. VPC settings  
D. S3 bucket policy  
**Answer**: B  
**Explanation**: Concurrency limits control throttling.

### Question 35
ECS deployment needs zero downtime. What should you use?  
A. EC2 launch type with rolling  
B. Fargate with blue/green  
C. Lambda aliases  
D. CloudFormation rollback  
**Answer**: B  
**Explanation**: Fargate with blue/green ensures no downtime.

### Question 36
S3 CRR fails to replicate objects. What must be enabled?  
A. Versioning  
B. Multi-AZ  
C. Event notifications  
D. CloudWatch alarms  
**Answer**: A  
**Explanation**: CRR requires versioning on source/destination buckets.

### Question 37
Route 53 health check fails. What’s the likely issue?  
A. Missing IAM permissions  
B. Incorrect endpoint in the health check  
C. Disabled CloudTrail  
D. No S3 bucket policy  
**Answer**: B  
**Explanation**: Health checks need a valid endpoint.

### Question 38
Your app needs minimal DR setup. Which strategy?  
A. Backup and Restore  
B. Pilot Light  
C. Warm Standby  
D. Multi-Site  
**Answer**: B  
**Explanation**: Pilot Light runs a minimal core for DR.

### Question 39
Lambda cold starts impact performance. What should you use?  
A. Provisioned concurrency  
B. Increased memory  
C. Blue/green deployment  
D. S3 event triggers  
**Answer**: A  
**Explanation**: Provisioned concurrency reduces cold starts.

### Question 40
ElastiCache fails over slowly. What should you check?  
A. Multi-AZ settings  
B. S3 CRR configuration  
C. Lambda aliases  
D. CodePipeline stages  
**Answer**: A  
**Explanation**: Multi-AZ enables fast failover for Redis.

### Question 41
ECS Fargate tasks scale poorly. What should you adjust?  
A. Service scaling policy  
B. Lambda concurrency  
C. S3 bucket lifecycle  
D. CloudFormation outputs  
**Answer**: A  
**Explanation**: Service scaling policies control Fargate scaling.

---

## Domain 4: Monitoring and Logging (15%) - 11 Questions

### Question 42
You need to track EC2 memory usage. What should you do?  
A. Enable CloudWatch detailed monitoring  
B. Push custom metrics with the CloudWatch agent  
C. Create an S3 event trigger  
D. Set up a CodeDeploy hook  
**Answer**: B  
**Explanation**: Memory requires custom metrics via the agent.

### Question 43
CloudWatch Logs aren’t appearing. What should you check?  
A. IAM permissions for the agent  
B. S3 bucket versioning  
C. CodePipeline stage config  
D. Lambda concurrency  
**Answer**: A  
**Explanation**: Agent needs IAM permissions to write logs.

### Question 44
An ASG scales unexpectedly. What should you set up?  
A. CloudWatch alarm  
B. S3 event notification  
C. CodeDeploy rollback  
D. Athena query  
**Answer**: A  
**Explanation**: Alarms trigger ASG scaling.

### Question 45
You need to query VPC Flow Logs. Which service?  
A. CloudWatch Logs Insights  
B. Amazon Athena  
C. AWS CodeGuru  
D. EventBridge  
**Answer**: B  
**Explanation**: Athena queries S3-stored logs efficiently.

### Question 46
A scheduled Lambda fails to run. What should you configure?  
A. CloudWatch alarm  
B. EventBridge rule  
C. S3 event trigger  
D. CodePipeline stage  
**Answer**: B  
**Explanation**: EventBridge schedules Lambda executions.

### Question 47
Which log type requires a subscription for real-time processing?  
A. CloudWatch Metrics  
B. CloudWatch Logs  
C. S3 access logs  
D. CloudTrail logs  
**Answer**: B  
**Explanation**: Logs subscriptions enable real-time processing.

### Question 48
You need to alert on high CPU usage. What should you use?  
A. CloudWatch alarm with SNS  
B. Athena query with S3  
C. EventBridge with Lambda  
D. CodeDeploy with rollback  
**Answer**: A  
**Explanation**: Alarms with SNS notify on thresholds.

### Question 49
Athena queries are slow. What should you do?  
A. Convert data to Parquet  
B. Increase Lambda memory  
C. Enable CloudWatch detailed monitoring  
D. Adjust CodePipeline stages  
**Answer**: A  
**Explanation**: Parquet improves query performance.

### Question 50
A cross-account EventBridge rule fails. What should you verify?  
A. Resource-based policy  
B. S3 bucket policy  
C. IAM user permissions  
D. CloudFormation outputs  
**Answer**: A  
**Explanation**: Event buses need resource policies for cross-account access.

### Question 51
You need custom EC2 metrics. Which resolution is high-resolution?  
A. 60 seconds  
B. 30 seconds  
C. 300 seconds  
D. 600 seconds  
**Answer**: B  
**Explanation**: 1/5/10/30 seconds are high-resolution options.

### Question 52
CloudWatch Logs Insights fails to find data. What’s the issue?  
A. Logs are older than 90 days  
B. Incorrect query syntax  
C. S3 export delay  
D. Missing IAM role  
**Answer**: B  
**Explanation**: Insights requires correct query syntax.

---

## Domain 5: Incident and Event Response (14%) - 11 Questions

### Question 53
S3 events aren’t triggering Lambda. What should you check?  
A. Lambda resource policy  
B. CloudWatch alarm settings  
C. CodePipeline stage  
D. RDS Multi-AZ config  
**Answer**: A  
**Explanation**: Lambda needs permission for S3 to invoke it.

### Question 54
GuardDuty flags an SSH brute force attack. What should you do?  
A. Set up an EventBridge rule  
B. Increase Lambda concurrency  
C. Adjust S3 CRR  
D. Enable CloudFormation rollback  
**Answer**: A  
**Explanation**: EventBridge automates responses to findings.

### Question 55
CloudTrail logs stop after 90 days. How do you retain them?  
A. Export to S3  
B. Enable Multi-AZ  
C. Set up Athena queries  
D. Increase Lambda memory  
**Answer**: A  
**Explanation**: S3 export extends retention beyond 90 days.

### Question 56
You need to filter S3 events for .jpg files. Where do you configure this?  
A. S3 bucket policy  
B. Event notification settings  
C. CloudWatch Logs filter  
D. CodeDeploy appspec.yml  
**Answer**: B  
**Explanation**: Event notifications support file filters.

### Question 57
A GuardDuty finding indicates a multi-account issue. What should you configure?  
A. AWS Organization integration  
B. S3 bucket versioning  
C. Lambda aliases  
D. CloudFormation StackSets  
**Answer**: A  
**Explanation**: GuardDuty manages multi-account via Organizations.

### Question 58
CloudTrail doesn’t log S3 object actions. What should you enable?  
A. Data events  
B. Management events  
C. Insights events  
D. Multi-region replication  
**Answer**: A  
**Explanation**: Data events log object-level actions.

### Question 59
An S3 upload should trigger a pipeline. What should you use?  
A. EventBridge  
B. CloudWatch alarm  
C. CodeDeploy  
D. RDS failover  
**Answer**: A  
**Explanation**: EventBridge supports S3 events to trigger pipelines.

### Question 60
GuardDuty misses EKS threats. What should you enable?  
A. EKS Audit Logs  
B. S3 CRR  
C. Lambda concurrency  
D. CloudFormation conditions  
**Answer**: A  
**Explanation**: EKS Audit Logs enhance GuardDuty detection.

### Question 61
You need to investigate an EC2 deletion. Where do you look?  
A. CloudTrail logs  
B. CloudWatch metrics  
C. S3 event logs  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: CloudTrail logs API calls like deletions.

### Question 62
S3 events need multiple targets. What should you use?  
A. EventBridge  
B. CloudWatch Logs subscription  
C. CodeDeploy hooks  
D. Lambda aliases  
**Answer**: A  
**Explanation**: EventBridge supports multiple destinations.

### Question 63
CloudTrail logs are missing. What should you verify?  
A. Trail is enabled for all regions  
B. S3 bucket encryption  
C. Lambda memory size  
D. RDS read replicas  
**Answer**: A  
**Explanation**: All-region trails ensure comprehensive logging.

---

## Domain 6: Security and Compliance (17%) - 12 Questions

### Question 64
AWS Config flags public S3 buckets. What should you do?  
A. Set up a managed rule  
B. Increase Lambda concurrency  
C. Enable S3 CRR  
D. Adjust CodePipeline stages  
**Answer**: A  
**Explanation**: Managed rules detect compliance issues.

### Question 65
A Config rule needs custom logic. What should you use?  
A. Lambda-backed rule  
B. S3 event trigger  
C. CloudWatch alarm  
D. CodeDeploy rollback  
**Answer**: A  
**Explanation**: Custom rules use Lambda for logic.

### Question 66
You need multi-account Config visibility. What should you configure?  
A. Aggregators  
B. StackSets  
C. S3 bucket policy  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Aggregators provide multi-account views.

### Question 67
WAF blocks legitimate traffic. What should you adjust?  
A. Rate-based rule threshold  
B. S3 CRR settings  
C. CloudTrail logging  
D. RDS Multi-AZ  
**Answer**: A  
**Explanation**: Rate-based rules control request limits.

### Question 68
Firewall Manager fails to apply policies. What’s the likely cause?  
A. Missing AWS Organization setup  
B. Incorrect S3 bucket name  
C. Disabled CloudWatch  
D. No Lambda trigger  
**Answer**: A  
**Explanation**: Firewall Manager requires Organizations.

### Question 69
IAM Identity Center users can’t access an app. What should you check?  
A. Permission sets  
B. S3 event triggers  
C. CodePipeline artifacts  
D. RDS failover settings  
**Answer**: A  
**Explanation**: Permission sets define SSO access.

### Question 70
A Config non-compliant resource needs auto-fix. What should you use?  
A. SSM Automation  
B. Lambda concurrency  
C. S3 CRR  
D. CloudFormation outputs  
**Answer**: A  
**Explanation**: SSM Automation remediates non-compliance.

### Question 71
WAF needs CAPTCHA for suspicious requests. Where do you configure it?  
A. Web ACL rule action  
B. S3 bucket policy  
C. CloudTrail logs  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: Web ACL rules support CAPTCHA actions.

### Question 72
You need SSO with Okta. What should you integrate?  
A. IAM Identity Center  
B. AWS Config  
C. CodePipeline  
D. CloudWatch alarms  
**Answer**: A  
**Explanation**: IAM Identity Center supports external IdPs like Okta.

### Question 73
Firewall Manager needs to enforce WAF across regions. What should you do?  
A. Create regional policies  
B. Enable S3 CRR  
C. Adjust Lambda memory  
D. Set up CodeDeploy  
**Answer**: A  
**Explanation**: Policies are region-specific in Firewall Manager.

### Question 74
Config rules deploy inconsistently. What should you use?  
A. Conformance packs  
B. S3 event triggers  
C. CloudTrail insights  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Conformance packs standardize rule deployment.

### Question 75
IAM Identity Center needs attribute-based access. What should you configure?  
A. ABAC policies  
B. S3 bucket policies  
C. CodePipeline stages  
D. RDS Multi-AZ  
**Answer**: A  
**Explanation**: ABAC uses attributes for fine-grained access.

---

# AWS Certified DevOps Engineer – Professional (DOP-C02) Practice Questions (Set 2)

This document provides 75 new practice questions for the AWS Certified DevOps Engineer – Professional (DOP-C02) exam, distributed across six domains per their official weightings: Domain 1 (22%), Domain 2 (17%), Domain 3 (15%), Domain 4 (15%), Domain 5 (14%), Domain 6 (17%). Questions are scenario-based, reflecting key details and exam focus areas, formatted as multiple-choice or multiple-response.

---

## Domain 1: SDLC Automation (22%) - 17 Questions

### Question 1
Your team’s pipeline fails to detect new GitHub commits. What should you configure?  
A. Webhook in GitHub  
B. Manual approval in CodePipeline  
C. S3 bucket lifecycle policy  
D. CloudWatch metric filter  
**Answer**: A  
**Explanation**: A GitHub webhook triggers CodePipeline on commits.

### Question 2
A CodeBuild job times out during testing. What’s the first step to resolve it?  
A. Increase the timeout in buildspec.yml  
B. Add more stages to CodePipeline  
C. Enable S3 versioning  
D. Update IAM user permissions  
**Answer**: A  
**Explanation**: Timeout settings in `buildspec.yml` control job duration.

### Question 3 (Multiple-Response)
Which TWO services are essential for a CI/CD pipeline deploying to ECS?  
A. AWS CodePipeline  
B. AWS CodeDeploy  
C. AWS CodeArtifact  
D. AWS CloudFormation  
**Answers**: A, B  
**Explanation**: CodePipeline orchestrates, and CodeDeploy handles ECS deployments.

### Question 4
You need to roll back a failed EC2 deployment. Where is rollback configured?  
A. CodePipeline stage  
B. CodeDeploy deployment group  
C. buildspec.yml  
D. S3 bucket policy  
**Answer**: B  
**Explanation**: Rollback settings are in CodeDeploy deployment groups.

### Question 5
A Lambda deployment needs gradual traffic shifting. What should you configure?  
A. CodeDeploy with canary deployment  
B. CodePipeline with manual approval  
C. CodeBuild with VPC settings  
D. CloudWatch alarm  
**Answer**: A  
**Explanation**: CodeDeploy supports canary traffic shifting for Lambda.

### Question 6
Post-CodeCommit deprecation, your pipeline uses GitHub. What must be updated?  
A. Source provider in CodePipeline  
B. IAM role in CodeBuild  
C. S3 artifact encryption  
D. CloudTrail logging  
**Answer**: A  
**Explanation**: Source provider must switch to GitHub.

### Question 7
Which service stores npm packages for your pipeline?  
A. AWS CodeArtifact  
B. AWS CodeStar  
C. AWS CodeGuru  
D. AWS CodeCommit  
**Answer**: A  
**Explanation**: CodeArtifact manages npm and other packages.

### Question 8
CodeGuru Profiler shows high CPU usage in a Lambda function. What’s the next step?  
A. Optimize the code based on profiling  
B. Increase CodePipeline stages  
C. Enable S3 event triggers  
D. Adjust buildspec.yml phases  
**Answer**: A  
**Explanation**: Profiler identifies optimization targets.

### Question 9
A cross-region pipeline fails to deploy. What should you ensure?  
A. S3 buckets are replicated  
B. CodeDeploy supports multi-region  
C. IAM roles have regional permissions  
D. CloudWatch Events are enabled  
**Answer**: C  
**Explanation**: IAM roles need cross-region permissions.

### Question 10
Your build needs a custom Docker image. Where do you specify it?  
A. CodePipeline source stage  
B. CodeBuild environment settings  
C. appspec.yml  
D. S3 bucket policy  
**Answer**: B  
**Explanation**: CodeBuild environment settings define custom images.

### Question 11
You need to deploy to ECS with minimal downtime. Which tool?  
A. CodeDeploy with blue/green  
B. CodePipeline with rolling  
C. CodeStar with all at once  
D. CloudFormation with immutable  
**Answer**: A  
**Explanation**: Blue/green minimizes ECS downtime.

### Question 12
A CodeBuild job fails to access an S3 bucket. What should you update?  
A. IAM role permissions  
B. buildspec.yml phases  
C. S3 event notification  
D. CloudWatch Logs subscription  
**Answer**: A  
**Explanation**: IAM roles grant S3 access.

### Question 13
Which deployment mode is cost-effective for a test environment?  
A. Blue/Green  
B. Rolling  
C. All at Once  
D. Immutable  
**Answer**: C  
**Explanation**: All at Once is cheapest but has downtime, fine for testing.

### Question 14
CodeGuru Reviewer suggests a security fix. What should you do?  
A. Apply the fix and re-run the review  
B. Increase Lambda timeout  
C. Adjust CodeDeploy hooks  
D. Enable S3 versioning  
**Answer**: A  
**Explanation**: Reviewer provides actionable security fixes.

### Question 15
Artifacts aren’t transitioning in CodePipeline. What should you check?  
A. Stage transition settings  
B. GitHub webhook  
C. IAM user roles  
D. S3 bucket encryption  
**Answer**: A  
**Explanation**: Stage transitions control artifact flow.

### Question 16
Which service integrates GitHub, CodeBuild, and CodeDeploy?  
A. AWS CodeStar  
B. AWS CodePipeline  
C. AWS CodeArtifact  
D. AWS CodeGuru  
**Answer**: A  
**Explanation**: CodeStar provides a unified CI/CD interface.

### Question 17
CodeArtifact needs to proxy a public npm registry. What should you configure?  
A. Upstream repository  
B. S3 bucket policy  
C. CloudTrail logging  
D. Lambda trigger  
**Answer**: A  
**Explanation**: Upstream repositories proxy external registries.

---

## Domain 2: Configuration Management and IaC (17%) - 13 Questions

### Question 18
A CloudFormation stack update fails. What should you review?  
A. CloudWatch Logs  
B. Change set details  
C. S3 bucket permissions  
D. CodeDeploy logs  
**Answer**: B  
**Explanation**: Change sets preview update issues.

### Question 19
Which section defines variables in CloudFormation?  
A. Parameters  
B. Resources  
C. Outputs  
D. Conditions  
**Answer**: A  
**Explanation**: Parameters allow variable inputs.

### Question 20
You need an ELB’s DNS name in CloudFormation. Which function?  
A. Fn::ImportValue  
B. Fn::GetAtt  
C. Fn::Join  
D. Fn::Ref  
**Answer**: B  
**Explanation**: `GetAtt` retrieves resource attributes like DNSName.

### Question 21
A StackSet doesn’t deploy to a new account. What’s missing?  
A. StackSet execution role  
B. S3 bucket versioning  
C. CodePipeline trigger  
D. CloudWatch alarm  
**Answer**: A  
**Explanation**: Execution roles are required for StackSet deployment.

### Question 22
Elastic Beanstalk update causes app outage. Which mode avoids this?  
A. Rolling with additional batch  
B. All at Once  
C. Blue/Green  
D. Immutable  
**Answer**: C  
**Explanation**: Blue/Green switches environments without outage.

### Question 23
You need to add a custom script to Beanstalk. Where do you define it?  
A. .ebextensions  
B. buildspec.yml  
C. appspec.yml  
D. CloudFormation parameters  
**Answer**: A  
**Explanation**: `.ebextensions` runs custom scripts.

### Question 24
A CloudFormation stack creation hangs. What’s the likely cause?  
A. Circular dependency  
B. S3 artifact missing  
C. CodeDeploy failure  
D. GitHub webhook issue  
**Answer**: A  
**Explanation**: Circular dependencies halt stack creation.

### Question 25
Which Beanstalk mode ensures no capacity loss during update?  
A. Rolling  
B. Immutable  
C. All at Once  
D. Blue/Green  
**Answer**: B  
**Explanation**: Immutable adds new instances before terminating old ones.

### Question 26
You need to map regions to AMIs in CloudFormation. What should you use?  
A. Mappings  
B. Parameters  
C. Outputs  
D. Conditions  
**Answer**: A  
**Explanation**: Mappings define static key-value pairs.

### Question 27
A Beanstalk worker needs to process SNS messages. What should you enable?  
A. SNS subscription  
B. RDS read replica  
C. S3 event trigger  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Workers process SNS or SQS messages.

### Question 28
Which function exports a VPC ID to another stack?  
A. Fn::Export  
B. Fn::GetAtt  
C. Fn::Sub  
D. Fn::ImportValue  
**Answer**: D  
**Explanation**: `ImportValue` imports exported values from other stacks.

### Question 29
You need to deploy IaC across regions. What’s the best tool?  
A. StackSets  
B. CodePipeline  
C. Elastic Beanstalk  
D. Nested Stacks  
**Answer**: A  
**Explanation**: StackSets handle multi-region IaC.

### Question 30
A Beanstalk app needs a custom domain. Where do you configure it?  
A. Route 53 and environment settings  
B. S3 bucket policy  
C. CodeDeploy appspec.yml  
D. CloudFormation conditions  
**Answer**: A  
**Explanation**: Route 53 and Beanstalk settings link domains.

---

## Domain 3: Resilient Cloud Solutions (15%) - 11 Questions

### Question 31
RDS read latency increases. What should you implement?  
A. Multi-AZ failover  
B. Read replicas  
C. S3 CRR  
D. Lambda aliases  
**Answer**: B  
**Explanation**: Read replicas offload read traffic.

### Question 32
Which service ensures low-latency global data access?  
A. DynamoDB Global Tables  
B. RDS Multi-AZ  
C. EFS Multi-AZ  
D. S3 versioning  
**Answer**: A  
**Explanation**: Global Tables provide multi-region access.

### Question 33
Your DR plan needs fast recovery with minimal cost. Which approach?  
A. Warm Standby  
B. Backup and Restore  
C. Multi-Site  
D. Pilot Light  
**Answer**: A  
**Explanation**: Warm Standby balances cost and RTO.

### Question 34
Lambda executions fail intermittently. What should you increase?  
A. Timeout  
B. Reserved concurrency  
C. S3 bucket size  
D. CodePipeline stages  
**Answer**: B  
**Explanation**: Reserved concurrency prevents throttling.

### Question 35
ECS needs high availability. What should you configure?  
A. Fargate with ALB  
B. EC2 with rolling updates  
C. Lambda with S3 triggers  
D. CloudFormation with conditions  
**Answer**: A  
**Explanation**: Fargate with ALB ensures HA.

### Question 36
S3 replication skips existing objects. What should you use?  
A. Batch Operations  
B. Multi-AZ  
C. CloudWatch alarms  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: Batch Operations replicate existing objects.

### Question 37
Route 53 latency routing fails. What should you verify?  
A. Health check status  
B. S3 bucket policy  
C. IAM role permissions  
D. CloudTrail logs  
**Answer**: A  
**Explanation**: Latency routing relies on health checks.

### Question 38
Your DR setup needs minimal running resources. Which strategy?  
A. Pilot Light  
B. Warm Standby  
C. Multi-Site  
D. Backup and Restore  
**Answer**: A  
**Explanation**: Pilot Light runs only critical components.

### Question 39
Lambda functions take too long to start. What’s the fix?  
A. Use provisioned concurrency  
B. Enable S3 CRR  
C. Increase CodeDeploy timeout  
D. Adjust CloudWatch metrics  
**Answer**: A  
**Explanation**: Provisioned concurrency mitigates cold starts.

### Question 40
ElastiCache loses data on failover. What should you enable?  
A. Redis AOF persistence  
B. S3 event triggers  
C. Lambda concurrency  
D. CloudFormation outputs  
**Answer**: A  
**Explanation**: AOF ensures data durability.

### Question 41
ECS tasks fail under load. What should you adjust?  
A. Task definition CPU/memory  
B. S3 bucket lifecycle  
C. Lambda timeout  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: CPU/memory settings affect task performance.

---

## Domain 4: Monitoring and Logging (15%) - 11 Questions

### Question 42
You need to monitor disk usage on EC2. What should you do?  
A. Install CloudWatch agent with custom metrics  
B. Enable S3 event logging  
C. Set up CodeDeploy hooks  
D. Adjust RDS Multi-AZ  
**Answer**: A  
**Explanation**: Disk usage requires custom metrics.

### Question 43
CloudWatch Logs stop unexpectedly. What’s the likely issue?  
A. Agent role lacks permissions  
B. S3 bucket versioning disabled  
C. CodePipeline stage failure  
D. Lambda timeout exceeded  
**Answer**: A  
**Explanation**: Agent needs IAM permissions.

### Question 44
An app crashes without notice. What should you configure?  
A. CloudWatch alarm on error metric  
B. S3 event trigger  
C. CodeDeploy rollback  
D. Athena query  
**Answer**: A  
**Explanation**: Alarms notify on crashes.

### Question 45
You need to analyze ELB logs. Which tool?  
A. Amazon Athena  
B. CloudWatch Logs Insights  
C. AWS CodeGuru  
D. EventBridge  
**Answer**: A  
**Explanation**: Athena queries ELB logs in S3.

### Question 46
A nightly backup fails to trigger. What should you use?  
A. EventBridge schedule  
B. CloudWatch alarm  
C. S3 event notification  
D. CodePipeline stage  
**Answer**: A  
**Explanation**: EventBridge schedules nightly tasks.

### Question 47
You need real-time log analysis. What should you set up?  
A. CloudWatch Logs subscription  
B. S3 export task  
C. CodeDeploy hooks  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Subscriptions enable real-time processing.

### Question 48
You need to notify on memory spikes. What should you configure?  
A. CloudWatch alarm with custom metric  
B. Athena query on S3  
C. EventBridge with SQS  
D. CodeDeploy with rollback  
**Answer**: A  
**Explanation**: Alarms monitor custom metrics.

### Question 49
Athena costs are high. What should you implement?  
A. Data compression (e.g., gzip)  
B. Lambda memory increase  
C. CloudWatch detailed monitoring  
D. CodePipeline optimization  
**Answer**: A  
**Explanation**: Compression reduces scanned data.

### Question 50
An EventBridge rule doesn’t fire across regions. What should you check?  
A. Event bus permissions  
B. S3 bucket policy  
C. IAM user roles  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Event buses need cross-region permissions.

### Question 51
You need 10-second metric resolution. What should you enable?  
A. High-resolution metrics  
B. Standard metrics  
C. S3 event triggers  
D. CodeDeploy settings  
**Answer**: A  
**Explanation**: High-resolution supports 10-second intervals.

### Question 52
CloudWatch Logs Insights returns no results. What should you verify?  
A. Log group selection  
B. S3 export delay  
C. IAM role permissions  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: Correct log group must be queried.

---

## Domain 5: Incident and Event Response (14%) - 11 Questions

### Question 53
S3 uploads don’t invoke SNS. What should you configure?  
A. S3 event notification  
B. CloudWatch alarm  
C. CodePipeline stage  
D. RDS failover  
**Answer**: A  
**Explanation**: Event notifications trigger SNS.

### Question 54
GuardDuty detects a crypto miner. What should you automate?  
A. EventBridge rule to isolate instance  
B. Increase Lambda memory  
C. Enable S3 CRR  
D. Adjust CloudFormation  
**Answer**: A  
**Explanation**: EventBridge automates incident response.

### Question 55
CloudTrail logs need long-term storage. What should you do?  
A. Configure S3 lifecycle policy  
B. Enable Multi-AZ  
C. Set up Athena queries  
D. Increase Lambda timeout  
**Answer**: A  
**Explanation**: S3 lifecycle manages retention.

### Question 56
You need S3 events for .png files only. What should you use?  
A. Event prefix filter  
B. CloudWatch Logs filter  
C. CodeDeploy hooks  
D. S3 bucket policy  
**Answer**: A  
**Explanation**: Prefix filters limit events to .png.

### Question 57
GuardDuty findings span accounts. What should you enable?  
A. Delegated administrator in Organizations  
B. S3 bucket versioning  
C. Lambda concurrency  
D. CloudFormation StackSets  
**Answer**: A  
**Explanation**: Delegated admin manages multi-account GuardDuty.

### Question 58
CloudTrail misses Lambda invocations. What should you enable?  
A. Data events  
B. Management events  
C. Insights events  
D. Multi-region setup  
**Answer**: A  
**Explanation**: Data events log Lambda actions.

### Question 59
An S3 delete should notify admins. What should you configure?  
A. EventBridge with SNS  
B. CloudWatch alarm  
C. CodeDeploy rollback  
D. RDS read replica  
**Answer**: A  
**Explanation**: EventBridge supports S3 delete notifications.

### Question 60
GuardDuty misses RDS threats. What should you activate?  
A. RDS Protection  
B. S3 CRR  
C. Lambda aliases  
D. CloudFormation conditions  
**Answer**: A  
**Explanation**: RDS Protection enhances GuardDuty.

### Question 61
A bucket policy change needs auditing. Where do you look?  
A. CloudTrail logs  
B. CloudWatch metrics  
C. S3 event logs  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: CloudTrail logs policy changes.

### Question 62
S3 events need to trigger Lambda and SNS. What should you use?  
A. EventBridge  
B. CloudWatch Logs subscription  
C. CodeDeploy hooks  
D. Lambda concurrency  
**Answer**: A  
**Explanation**: EventBridge supports multiple targets.

### Question 63
CloudTrail logs aren’t comprehensive. What should you ensure?  
A. Global trail is enabled  
B. S3 bucket encryption  
C. Lambda timeout  
D. RDS Multi-AZ  
**Answer**: A  
**Explanation**: Global trails log all regions.

---

## Domain 6: Security and Compliance (17%) - 12 Questions

### Question 64
AWS Config detects unencrypted EBS volumes. What should you set up?  
A. Managed rule  
B. Lambda concurrency  
C. S3 CRR  
D. CodePipeline stages  
**Answer**: A  
**Explanation**: Managed rules check encryption.

### Question 65
A custom Config rule needs complex logic. What should you implement?  
A. Lambda function  
B. S3 event trigger  
C. CloudWatch alarm  
D. CodeDeploy rollback  
**Answer**: A  
**Explanation**: Lambda backs custom rules.

### Question 66
You need a compliance overview across regions. What should you use?  
A. Config Aggregators  
B. StackSets  
C. S3 bucket policy  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Aggregators consolidate multi-region data.

### Question 67
WAF allows SQL injection attempts. What should you configure?  
A. SQL injection rule  
B. S3 bucket policy  
C. CloudTrail logs  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: WAF rules block SQL injections.

### Question 68
Firewall Manager doesn’t protect new accounts. What’s needed?  
A. AWS Organizations integration  
B. S3 bucket versioning  
C. CloudWatch metrics  
D. Lambda trigger  
**Answer**: A  
**Explanation**: Organizations enable account-wide policies.

### Question 69
IAM Identity Center users lack AWS access. What should you verify?  
A. Permission set assignments  
B. S3 event triggers  
C. CodePipeline artifacts  
D. RDS failover settings  
**Answer**: A  
**Explanation**: Permission sets grant AWS access.

### Question 70
A Config rule violation needs automatic correction. What should you use?  
A. SSM Run Command  
B. Lambda timeout  
C. S3 CRR  
D. CloudFormation outputs  
**Answer**: A  
**Explanation**: SSM automates remediation.

### Question 71
WAF needs to challenge bots. What should you enable?  
A. Challenge action in Web ACL  
B. S3 bucket policy  
C. CloudTrail logs  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: Challenge actions verify bots.

### Question 72
SSO with Azure AD fails. What should you integrate?  
A. IAM Identity Center  
B. AWS Config  
C. CodePipeline  
D. CloudWatch alarms  
**Answer**: A  
**Explanation**: IAM Identity Center supports Azure AD.

### Question 73
Firewall Manager needs to enforce Security Groups. What should you create?  
A. Security Group policy  
B. S3 event trigger  
C. Lambda concurrency  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Security Group policies enforce rules.

### Question 74
Config rules need consistent deployment. What should you use?  
A. Conformance packs  
B. S3 event triggers  
C. CloudTrail insights  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Conformance packs ensure consistency.

### Question 75
IAM Identity Center needs dynamic permissions. What should you configure?  
A. ABAC with user attributes  
B. S3 bucket policies  
C. CodePipeline stages  
D. RDS Multi-AZ  
**Answer**: A  
**Explanation**: ABAC uses attributes for dynamic access.

---


# AWS Certified DevOps Engineer – Professional (DOP-C02) Practice Questions (Set 3)

---

## Domain 1: SDLC Automation (22%) - 17 Questions

### Question 1
Your pipeline needs to validate code commits from Bitbucket. What should you configure?  
A. Bitbucket source in CodePipeline  
B. S3 event trigger  
C. Lambda function trigger  
D. CloudWatch Events rule  
**Answer**: A  
**Explanation**: CodePipeline supports Bitbucket as a source provider.

### Question 2
A CodeBuild job fails with a dependency error. What’s the first step?  
A. Check the buildspec.yml artifacts section  
B. Verify dependency installation in buildspec.yml  
C. Update CodePipeline IAM role  
D. Enable S3 bucket versioning  
**Answer**: B  
**Explanation**: Dependency issues are defined in `buildspec.yml`.

### Question 3 (Multiple-Response)
Which TWO options improve CodePipeline scalability?  
A. Use multi-region stages  
B. Enable parallel actions  
C. Increase Lambda concurrency  
D. Add S3 lifecycle policies  
**Answers**: A, B  
**Explanation**: Multi-region and parallel actions enhance scalability.

### Question 4
A deployment to EC2 needs rollback on failure. Where is this set?  
A. CodeDeploy deployment config  
B. CloudFormation template  
C. S3 bucket policy  
D. CodePipeline source stage  
**Answer**: A  
**Explanation**: Deployment config defines rollback behavior.

### Question 5
You need to deploy a Lambda alias with 20% traffic. What should you use?  
A. CodeDeploy with linear deployment  
B. CodePipeline with S3 source  
C. CodeBuild with custom image  
D. CloudWatch alarm  
**Answer**: A  
**Explanation**: Linear deployment shifts traffic gradually.

### Question 6
Your pipeline switches to GitLab. What must you update?  
A. Source stage provider  
B. CodeBuild environment  
C. S3 artifact bucket  
D. CloudTrail settings  
**Answer**: A  
**Explanation**: Source stage must reflect the new provider.

### Question 7
Which service proxies PyPI packages?  
A. AWS CodeArtifact  
B. AWS CodeStar  
C. AWS CodeGuru  
D. AWS CodeDeploy  
**Answer**: A  
**Explanation**: CodeArtifact proxies external package registries.

### Question 8
CodeGuru Profiler flags memory leaks in Python code. What’s next?  
A. Optimize memory usage  
B. Increase CodePipeline timeout  
C. Enable S3 triggers  
D. Adjust buildspec.yml  
**Answer**: A  
**Explanation**: Profiler identifies memory optimization needs.

### Question 9
A pipeline fails to access cross-account artifacts. What should you fix?  
A. S3 bucket policy  
B. CodeDeploy settings  
C. CloudWatch Logs  
D. GitHub webhook  
**Answer**: A  
**Explanation**: Cross-account access requires S3 policies.

### Question 10
Your build requires a specific Node.js version. Where do you specify it?  
A. CodeBuild environment variables  
B. CodePipeline source  
C. appspec.yml  
D. S3 bucket  
**Answer**: A  
**Explanation**: Environment variables set runtime versions.

### Question 11
You need ECS deployment with health checks. What should you use?  
A. CodeDeploy with hooks  
B. CodePipeline with manual approval  
C. CodeStar with S3 source  
D. CloudFormation with outputs  
**Answer**: A  
**Explanation**: Hooks in CodeDeploy validate ECS health.

### Question 12
A CodeBuild job can’t reach an internal API. What should you configure?  
A. VPC endpoint  
B. S3 bucket policy  
C. IAM user role  
D. CloudWatch subscription  
**Answer**: A  
**Explanation**: VPC endpoints enable private API access.

### Question 13
Which deployment mode suits a low-risk prod update?  
A. All at Once  
B. Rolling  
C. Blue/Green  
D. Immutable  
**Answer**: C  
**Explanation**: Blue/Green minimizes prod risk.

### Question 14
CodeGuru Reviewer detects a concurrency issue. What should you do?  
A. Refactor the code  
B. Increase Lambda timeout  
C. Enable S3 versioning  
D. Adjust CodeDeploy settings  
**Answer**: A  
**Explanation**: Concurrency fixes require code changes.

### Question 15
Pipeline artifacts aren’t stored. What should you verify?  
A. CodeBuild output settings  
B. GitHub permissions  
C. IAM role scope  
D. S3 encryption  
**Answer**: A  
**Explanation**: CodeBuild outputs define artifact storage.

### Question 16
Which service provides end-to-end CI/CD visibility?  
A. AWS CodeStar  
B. AWS CodePipeline  
C. AWS CodeArtifact  
D. AWS CodeGuru  
**Answer**: A  
**Explanation**: CodeStar offers a comprehensive view.

### Question 17
CodeArtifact needs to share packages across teams. What should you set?  
A. Repository permissions  
B. S3 lifecycle rules  
C. CloudTrail logs  
D. Lambda triggers  
**Answer**: A  
**Explanation**: Repository permissions enable sharing.

---

## Domain 2: Configuration Management and IaC (17%) - 13 Questions

### Question 18
A CloudFormation stack fails to delete. What should you investigate?  
A. Resource retention policies  
B. S3 bucket versioning  
C. CodeDeploy logs  
D. CloudWatch metrics  
**Answer**: A  
**Explanation**: Retention policies prevent deletion.

### Question 19
Which component sets conditional resource creation?  
A. Conditions  
B. Parameters  
C. Mappings  
D. Resources  
**Answer**: A  
**Explanation**: Conditions control resource logic.

### Question 20
You need an S3 bucket ARN in CloudFormation. Which function?  
A. Fn::Ref  
B. Fn::GetAtt  
C. Fn::Join  
D. Fn::Sub  
**Answer**: B  
**Explanation**: `GetAtt` retrieves ARNs.

### Question 21
StackSets fail in a new region. What should you ensure?  
A. Regional IAM permissions  
B. S3 bucket replication  
C. CodePipeline triggers  
D. CloudWatch alarms  
**Answer**: A  
**Explanation**: Regional permissions are needed.

### Question 22
Beanstalk update impacts users. Which mode prevents this?  
A. Blue/Green  
B. All at Once  
C. Rolling  
D. Immutable  
**Answer**: A  
**Explanation**: Blue/Green avoids user impact.

### Question 23
You need to install nginx on Beanstalk. Where do you define it?  
A. .ebextensions  
B. buildspec.yml  
C. appspec.yml  
D. CloudFormation mappings  
**Answer**: A  
**Explanation**: `.ebextensions` handles custom installs.

### Question 24
A CloudFormation stack update skips resources. What’s the issue?  
A. Change set misconfiguration  
B. S3 artifact absence  
C. CodeDeploy failure  
D. GitHub issue  
**Answer**: A  
**Explanation**: Change sets define updates.

### Question 25
Which Beanstalk mode adds capacity before removing old instances?  
A. Immutable  
B. Rolling  
C. All at Once  
D. Blue/Green  
**Answer**: A  
**Explanation**: Immutable ensures capacity.

### Question 26
You need to output a subnet ID. What should you use?  
A. Outputs  
B. Parameters  
C. Conditions  
D. Mappings  
**Answer**: A  
**Explanation**: Outputs expose resource values.

### Question 27
Beanstalk needs a custom VPC. Where do you configure it?  
A. Environment settings  
B. S3 bucket policy  
C. CodeDeploy appspec.yml  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Environment settings define VPCs.

### Question 28
Which function combines strings in CloudFormation?  
A. Fn::Join  
B. Fn::GetAtt  
C. Fn::Ref  
D. Fn::ImportValue  
**Answer**: A  
**Explanation**: `Join` concatenates strings.

### Question 29
You need IaC across multiple OUs. What’s the best approach?  
A. StackSets  
B. CodePipeline  
C. Elastic Beanstalk  
D. Nested Stacks  
**Answer**: A  
**Explanation**: StackSets support OU deployments.

### Question 30
Beanstalk needs a health check URL. Where do you set it?  
A. Environment config  
B. S3 event trigger  
C. CodeDeploy hooks  
D. CloudFormation conditions  
**Answer**: A  
**Explanation**: Environment config sets health URLs.

---

## Domain 3: Resilient Cloud Solutions (15%) - 11 Questions

### Question 31
RDS write latency spikes. What should you implement?  
A. Multi-AZ standby  
B. DynamoDB Global Tables  
C. S3 CRR  
D. Lambda concurrency  
**Answer**: A  
**Explanation**: Multi-AZ aids write availability.

### Question 32
Which service replicates data across regions with sub-second lag?  
A. Aurora Global Database  
B. RDS Multi-AZ  
C. EFS Multi-AZ  
D. S3 versioning  
**Answer**: A  
**Explanation**: Aurora Global offers low-latency replication.

### Question 33
Your DR needs moderate cost and decent RTO. Which strategy?  
A. Warm Standby  
B. Backup and Restore  
C. Multi-Site  
D. Pilot Light  
**Answer**: A  
**Explanation**: Warm Standby balances cost and RTO.

### Question 34
Lambda fails under sudden traffic. What should you adjust?  
A. Provisioned concurrency  
B. S3 bucket size  
C. CodePipeline stages  
D. Timeout  
**Answer**: A  
**Explanation**: Provisioned concurrency handles spikes.

### Question 35
ECS needs multi-AZ deployment. What should you use?  
A. Fargate with ASG  
B. EC2 with rolling  
C. Lambda with S3  
D. CloudFormation with outputs  
**Answer**: A  
**Explanation**: Fargate with ASG ensures multi-AZ.

### Question 36
S3 CRR doesn’t replicate deletes. What should you enable?  
A. Delete marker replication  
B. Multi-AZ  
C. CloudWatch alarms  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: Delete marker replication syncs deletes.

### Question 37
Route 53 failover doesn’t trigger. What should you check?  
A. Health check configuration  
B. S3 bucket policy  
C. IAM permissions  
D. CloudTrail logs  
**Answer**: A  
**Explanation**: Failover relies on health checks.

### Question 38
Your DR requires low upfront cost. Which approach?  
A. Pilot Light  
B. Warm Standby  
C. Multi-Site  
D. Backup and Restore  
**Answer**: A  
**Explanation**: Pilot Light minimizes initial costs.

### Question 39
Lambda performance degrades on startup. What’s the solution?  
A. Increase memory  
B. Use provisioned concurrency  
C. Enable S3 CRR  
D. Adjust CodeDeploy  
**Answer**: B  
**Explanation**: Provisioned concurrency speeds startups.

### Question 40
ElastiCache fails to scale reads. What should you add?  
A. Read replicas  
B. S3 event triggers  
C. Lambda concurrency  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Read replicas scale Redis reads.

### Question 41
ECS Fargate tasks crash on load. What should you tweak?  
A. Task memory limits  
B. S3 bucket lifecycle  
C. Lambda timeout  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: Memory limits affect task stability.

---

## Domain 4: Monitoring and Logging (15%) - 11 Questions

### Question 42
You need to track network bytes on EC2. What should you do?  
A. Enable CloudWatch agent  
B. Set S3 event logging  
C. Configure CodeDeploy  
D. Adjust RDS Multi-AZ  
**Answer**: A  
**Explanation**: Agent tracks network metrics.

### Question 43
CloudWatch Logs aren’t updating. What should you verify?  
A. Agent configuration  
B. S3 bucket versioning  
C. CodePipeline failure  
D. Lambda timeout  
**Answer**: A  
**Explanation**: Agent config ensures log updates.

### Question 44
An app fails silently. What should you monitor?  
A. CloudWatch custom metric  
B. S3 event trigger  
C. CodeDeploy rollback  
D. Athena query  
**Answer**: A  
**Explanation**: Custom metrics detect silent failures.

### Question 45
You need to search CloudTrail logs. Which tool?  
A. Amazon Athena  
B. CloudWatch Logs Insights  
C. AWS CodeGuru  
D. EventBridge  
**Answer**: A  
**Explanation**: Athena queries S3-stored CloudTrail logs.

### Question 46
A weekly report isn’t generating. What should you schedule?  
A. EventBridge rule  
B. CloudWatch alarm  
C. S3 event notification  
D. CodePipeline stage  
**Answer**: A  
**Explanation**: EventBridge schedules weekly tasks.

### Question 47
You need near-real-time log processing. What should you configure?  
A. CloudWatch Logs subscription  
B. S3 export task  
C. CodeDeploy hooks  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Subscriptions provide near-real-time logs.

### Question 48
You need to alert on disk space. What should you set?  
A. CloudWatch alarm with custom metric  
B. Athena query on S3  
C. EventBridge with SQS  
D. CodeDeploy rollback  
**Answer**: A  
**Explanation**: Alarms monitor disk space.

### Question 49
Athena queries take too long. What should you do?  
A. Partition S3 data  
B. Increase Lambda memory  
C. Enable CloudWatch metrics  
D. Adjust CodePipeline  
**Answer**: A  
**Explanation**: Partitioning speeds queries.

### Question 50
An EventBridge rule fails across accounts. What should you fix?  
A. Event bus policy  
B. S3 bucket policy  
C. IAM user permissions  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Event bus policies enable cross-account rules.

### Question 51
You need 5-second metric intervals. What should you enable?  
A. High-resolution metrics  
B. Standard metrics  
C. S3 event triggers  
D. CodeDeploy settings  
**Answer**: A  
**Explanation**: High-resolution supports 5 seconds.

### Question 52
CloudWatch misses logs. What should you check?  
A. Log stream configuration  
B. S3 export delay  
C. IAM role scope  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: Stream config ensures log capture.

---

## Domain 5: Incident and Event Response (14%) - 11 Questions

### Question 53
S3 uploads don’t trigger SQS. What should you set?  
A. S3 event notification  
B. CloudWatch alarm  
C. CodePipeline stage  
D. RDS failover  
**Answer**: A  
**Explanation**: Event notifications trigger SQS.

### Question 54
GuardDuty finds an anomaly. What should you automate?  
A. EventBridge rule with Lambda  
B. Increase Lambda memory  
C. Enable S3 CRR  
D. Adjust CloudFormation  
**Answer**: A  
**Explanation**: EventBridge automates responses.

### Question 55
CloudTrail logs need archiving. What should you configure?  
A. S3 export with lifecycle  
B. Multi-AZ enablement  
C. Athena queries  
D. Lambda timeout  
**Answer**: A  
**Explanation**: S3 export archives logs.

### Question 56
You need S3 events for .csv files. What should you apply?  
A. Event suffix filter  
B. CloudWatch Logs filter  
C. CodeDeploy hooks  
D. S3 bucket policy  
**Answer**: A  
**Explanation**: Suffix filters target .csv events.

### Question 57
GuardDuty needs centralized management. What should you enable?  
A. AWS Organizations  
B. S3 bucket versioning  
C. Lambda concurrency  
D. CloudFormation StackSets  
**Answer**: A  
**Explanation**: Organizations centralize GuardDuty.

### Question 58
CloudTrail lacks ECS task logs. What should you activate?  
A. Data events  
B. Management events  
C. Insights events  
D. Multi-region setup  
**Answer**: A  
**Explanation**: Data events log ECS actions.

### Question 59
An S3 write should alert via email. What should you use?  
A. EventBridge with SNS  
B. CloudWatch alarm  
C. CodeDeploy rollback  
D. RDS read replica  
**Answer**: A  
**Explanation**: EventBridge with SNS sends emails.

### Question 60
GuardDuty misses Lambda threats. What should you enable?  
A. Lambda Protection  
B. S3 CRR  
C. Lambda aliases  
D. CloudFormation conditions  
**Answer**: A  
**Explanation**: Lambda Protection enhances detection.

### Question 61
A security group change needs tracking. Where do you look?  
A. CloudTrail logs  
B. CloudWatch metrics  
C. S3 event logs  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: CloudTrail tracks security changes.

### Question 62
S3 events need dual triggers. What should you configure?  
A. EventBridge  
B. CloudWatch Logs subscription  
C. CodeDeploy hooks  
D. Lambda concurrency  
**Answer**: A  
**Explanation**: EventBridge supports dual targets.

### Question 63
CloudTrail logs are incomplete. What should you ensure?  
A. Multi-region trail  
B. S3 bucket encryption  
C. Lambda timeout  
D. RDS Multi-AZ  
**Answer**: A  
**Explanation**: Multi-region trails cover all actions.

---

## Domain 6: Security and Compliance (17%) - 12 Questions

### Question 64
AWS Config flags open security groups. What should you implement?  
A. Managed rule  
B. Lambda concurrency  
C. S3 CRR  
D. CodePipeline stages  
**Answer**: A  
**Explanation**: Managed rules detect open SGs.

### Question 65
A Config rule needs custom validation. What should you use?  
A. Lambda function  
B. S3 event trigger  
C. CloudWatch alarm  
D. CodeDeploy rollback  
**Answer**: A  
**Explanation**: Lambda validates custom rules.

### Question 66
You need compliance across OUs. What should you deploy?  
A. Config Aggregators  
B. StackSets  
C. S3 bucket policy  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Aggregators span OUs.

### Question 67
WAF fails to block XSS. What should you add?  
A. XSS match rule  
B. S3 bucket policy  
C. CloudTrail logs  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: XSS rules block cross-site scripting.

### Question 68
Firewall Manager skips new regions. What’s required?  
A. AWS Organizations setup  
B. S3 bucket versioning  
C. CloudWatch metrics  
D. Lambda trigger  
**Answer**: A  
**Explanation**: Organizations enable region coverage.

### Question 69
IAM Identity Center users lack app access. What should you check?  
A. Application assignments  
B. S3 event triggers  
C. CodePipeline artifacts  
D. RDS failover settings  
**Answer**: A  
**Explanation**: Assignments grant app access.

### Question 70
A Config violation needs quick fix. What should you use?  
A. SSM Automation  
B. Lambda timeout  
C. S3 CRR  
D. CloudFormation outputs  
**Answer**: A  
**Explanation**: SSM Automation fixes violations.

### Question 71
WAF needs bot mitigation. What should you enable?  
A. Bot Control rule  
B. S3 bucket policy  
C. CloudTrail logs  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: Bot Control mitigates bots.

### Question 72
SSO fails with OneLogin. What should you integrate?  
A. IAM Identity Center  
B. AWS Config  
C. CodePipeline  
D. CloudWatch alarms  
**Answer**: A  
**Explanation**: IAM Identity Center supports OneLogin.

### Question 73
Firewall Manager needs to enforce WAF globally. What should you do?  
A. Use global policies  
B. Enable S3 CRR  
C. Adjust Lambda memory  
D. Set up CodeDeploy  
**Answer**: A  
**Explanation**: Global policies enforce WAF.

### Question 74
Config rules vary by account. What should you standardize?  
A. Conformance packs  
B. S3 event triggers  
C. CloudTrail insights  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Conformance packs standardize rules.

### Question 75
IAM Identity Center needs role-based access. What should you configure?  
A. Permission sets with ABAC  
B. S3 bucket policies  
C. CodePipeline stages  
D. RDS Multi-AZ  
**Answer**: A  
**Explanation**: ABAC enhances role-based access.

---

# AWS Certified DevOps Engineer – Professional (DOP-C02) Practice Questions (Set 4)

---

## Domain 1: SDLC Automation (22%) - 17 Questions

### Question 1
Your pipeline misses GitHub PR updates. What should you add?  
A. GitHub action webhook  
B. S3 event notification  
C. Lambda function  
D. CloudWatch Logs filter  
**Answer**: A  
**Explanation**: Webhooks trigger on PR updates.

### Question 2
A CodeBuild job fails with a timeout error. What should you adjust?  
A. Environment compute type  
B. S3 bucket policy  
C. CodePipeline IAM role  
D. CloudTrail settings  
**Answer**: A  
**Explanation**: Compute type affects timeout capacity.

### Question 3 (Multiple-Response)
Which TWO services support CI/CD for Lambda?  
A. AWS CodePipeline  
B. AWS CodeDeploy  
C. AWS CodeStar  
D. AWS CloudFormation  
**Answers**: A, B  
**Explanation**: Pipeline and Deploy handle Lambda CI/CD.

### Question 4
You need to stop a failed deployment. Where is this configured?  
A. CodeDeploy deployment settings  
B. CloudFormation stack  
C. S3 bucket lifecycle  
D. CodePipeline source  
**Answer**: A  
**Explanation**: Deployment settings control stop behavior.

### Question 5
A Lambda deployment needs 10% traffic testing. What should you use?  
A. CodeDeploy with canary  
B. CodePipeline with S3  
C. CodeBuild with VPC  
D. CloudWatch metric  
**Answer**: A  
**Explanation**: Canary testing shifts 10% traffic.

### Question 6
Your pipeline moves to GitHub Enterprise. What must change?  
A. Source stage configuration  
B. CodeBuild runtime  
C. S3 artifact location  
D. CloudWatch alarms  
**Answer**: A  
**Explanation**: Source stage updates to GitHub Enterprise.

### Question 7
Which service manages Gradle dependencies?  
A. AWS CodeArtifact  
B. AWS CodeStar  
C. AWS CodeGuru  
D. AWS CodePipeline  
**Answer**: A  
**Explanation**: CodeArtifact supports Gradle.

### Question 8
CodeGuru Profiler shows latency spikes. What should you do?  
A. Refactor high-latency code  
B. Increase CodePipeline stages  
C. Enable S3 events  
D. Adjust buildspec.yml  
**Answer**: A  
**Explanation**: Profiler guides latency fixes.

### Question 9
A pipeline can’t fetch artifacts across regions. What’s needed?  
A. S3 cross-region replication  
B. CodeDeploy multi-region  
C. IAM cross-region permissions  
D. CloudWatch Events  
**Answer**: C  
**Explanation**: IAM permissions enable cross-region access.

### Question 10
Your build needs a custom Python version. Where do you set it?  
A. CodeBuild environment  
B. CodePipeline source  
C. appspec.yml  
D. S3 bucket  
**Answer**: A  
**Explanation**: Environment sets Python version.

### Question 11
You need ECS deployment with rollback. What should you use?  
A. CodeDeploy with validation hooks  
B. CodePipeline with approval  
C. CodeStar with S3  
D. CloudFormation with conditions  
**Answer**: A  
**Explanation**: Hooks enable rollback validation.

### Question 12
A CodeBuild job fails to connect to DynamoDB. What should you add?  
A. VPC configuration  
B. S3 bucket policy  
C. IAM user role  
D. CloudWatch subscription  
**Answer**: A  
**Explanation**: VPC config allows DynamoDB access.

### Question 13
Which deployment mode is fastest for a dev update?  
A. Blue/Green  
B. Rolling  
C. All at Once  
D. Immutable  
**Answer**: C  
**Explanation**: All at Once is fastest for dev.

### Question 14
CodeGuru Reviewer flags a race condition. What’s next?  
A. Fix the concurrency bug  
B. Increase Lambda timeout  
C. Enable S3 versioning  
D. Adjust CodeDeploy  
**Answer**: A  
**Explanation**: Race conditions need code fixes.

### Question 15
Pipeline artifacts fail to save. What should you check?  
A. CodeBuild artifact config  
B. GitHub credentials  
C. IAM role limits  
D. S3 encryption settings  
**Answer**: A  
**Explanation**: Artifact config ensures saving.

### Question 16
Which service unifies CI/CD management?  
A. AWS CodeStar  
B. AWS CodePipeline  
C. AWS CodeArtifact  
D. AWS CodeGuru  
**Answer**: A  
**Explanation**: CodeStar unifies CI/CD.

### Question 17
CodeArtifact needs a custom Maven repo. What should you configure?  
A. Upstream repository  
B. S3 lifecycle policy  
C. CloudTrail logs  
D. Lambda trigger  
**Answer**: A  
**Explanation**: Upstream repos proxy Maven.

---

## Domain 2: Configuration Management and IaC (17%) - 13 Questions

### Question 18
A CloudFormation stack fails to launch. What should you check?  
A. Resource limits  
B. S3 bucket versioning  
C. CodeDeploy logs  
D. CloudWatch metrics  
**Answer**: A  
**Explanation**: Limits cause launch failures.

### Question 19
Which component defines static values in CloudFormation?  
A. Mappings  
B. Parameters  
C. Outputs  
D. Conditions  
**Answer**: A  
**Explanation**: Mappings set static values.

### Question 20
You need an RDS endpoint in CloudFormation. Which function?  
A. Fn::GetAtt  
B. Fn::Ref  
C. Fn::Join  
D. Fn::Sub  
**Answer**: A  
**Explanation**: `GetAtt` retrieves endpoints.

### Question 21
StackSets skip a new account. What should you verify?  
A. Account permissions  
B. S3 bucket replication  
C. CodePipeline triggers  
D. CloudWatch alarms  
**Answer**: A  
**Explanation**: Permissions ensure account inclusion.

### Question 22
Beanstalk update disrupts traffic. Which mode avoids this?  
A. Blue/Green  
B. All at Once  
C. Rolling  
D. Immutable  
**Answer**: A  
**Explanation**: Blue/Green maintains traffic.

### Question 23
You need to set Beanstalk env variables. Where do you define them?  
A. .ebextensions  
B. buildspec.yml  
C. appspec.yml  
D. CloudFormation parameters  
**Answer**: A  
**Explanation**: `.ebextensions` sets variables.

### Question 24
A CloudFormation stack fails mid-update. What’s the cause?  
A. Resource conflict  
B. S3 artifact missing  
C. CodeDeploy issue  
D. GitHub failure  
**Answer**: A  
**Explanation**: Conflicts halt updates.

### Question 25
Which Beanstalk mode scales up before scaling down?  
A. Immutable  
B. Rolling  
C. All at Once  
D. Blue/Green  
**Answer**: A  
**Explanation**: Immutable scales up first.

### Question 26
You need to conditionally deploy an EC2. What should you use?  
A. Conditions  
B. Parameters  
C. Mappings  
D. Outputs  
**Answer**: A  
**Explanation**: Conditions control deployment.

### Question 27
Beanstalk needs a custom security group. Where do you set it?  
A. Environment options  
B. S3 bucket policy  
C. CodeDeploy appspec.yml  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Options set security groups.

### Question 28
Which function imports a stack value?  
A. Fn::ImportValue  
B. Fn::GetAtt  
C. Fn::Ref  
D. Fn::Join  
**Answer**: A  
**Explanation**: `ImportValue` imports values.

### Question 29
You need IaC across regions with one template. What’s best?  
A. StackSets  
B. CodePipeline  
C. Elastic Beanstalk  
D. Nested Stacks  
**Answer**: A  
**Explanation**: StackSets deploy regionally.

### Question 30
Beanstalk needs a load balancer timeout. Where do you configure it?  
A. Environment settings  
B. S3 event trigger  
C. CodeDeploy hooks  
D. CloudFormation conditions  
**Answer**: A  
**Explanation**: Settings adjust LB timeouts.

---

## Domain 3: Resilient Cloud Solutions (15%) - 11 Questions

### Question 31
RDS fails during peak load. What should you enable?  
A. Multi-AZ  
B. DynamoDB Global Tables  
C. S3 CRR  
D. Lambda concurrency  
**Answer**: A  
**Explanation**: Multi-AZ enhances availability.

### Question 32
Which service offers multi-region read/write?  
A. DynamoDB Global Tables  
B. RDS Multi-AZ  
C. EFS Multi-AZ  
D. S3 versioning  
**Answer**: A  
**Explanation**: Global Tables support multi-region RW.

### Question 33
Your DR needs fast RTO and high cost. Which strategy?  
A. Multi-Site  
B. Backup and Restore  
C. Warm Standby  
D. Pilot Light  
**Answer**: A  
**Explanation**: Multi-Site offers fast RTO.

### Question 34
Lambda hits execution limits. What should you increase?  
A. Reserved concurrency  
B. S3 bucket size  
C. CodePipeline stages  
D. Timeout  
**Answer**: A  
**Explanation**: Reserved concurrency lifts limits.

### Question 35
ECS needs failover across AZs. What should you use?  
A. Fargate with ALB  
B. EC2 with rolling  
C. Lambda with S3  
D. CloudFormation with outputs  
**Answer**: A  
**Explanation**: Fargate with ALB ensures failover.

### Question 36
S3 CRR misses new objects. What should you check?  
A. Replication rules  
B. Multi-AZ  
C. CloudWatch alarms  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: Rules define replication scope.

### Question 37
Route 53 doesn’t route to backup. What should you fix?  
A. Health check settings  
B. S3 bucket policy  
C. IAM permissions  
D. CloudTrail logs  
**Answer**: A  
**Explanation**: Health checks drive routing.

### Question 38
Your DR needs minimal scaling. Which approach?  
A. Pilot Light  
B. Warm Standby  
C. Multi-Site  
D. Backup and Restore  
**Answer**: A  
**Explanation**: Pilot Light scales minimally.

### Question 39
Lambda startup latency is high. What should you adjust?  
A. Provisioned concurrency  
B. S3 CRR  
C. CodeDeploy timeout  
D. CloudWatch metrics  
**Answer**: A  
**Explanation**: Provisioned concurrency reduces latency.

### Question 40
ElastiCache loses data on reboot. What should you enable?  
A. Redis snapshot  
B. S3 event triggers  
C. Lambda concurrency  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Snapshots preserve data.

### Question 41
ECS Fargate tasks timeout. What should you tweak?  
A. Task CPU limits  
B. S3 bucket lifecycle  
C. Lambda timeout  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: CPU limits affect timeouts.

---

## Domain 4: Monitoring and Logging (15%) - 11 Questions

### Question 42
You need to monitor CPU on-premises. What should you use?  
A. CloudWatch agent  
B. S3 event logging  
C. CodeDeploy hooks  
D. RDS Multi-AZ  
**Answer**: A  
**Explanation**: Agent monitors on-premises CPU.

### Question 43
CloudWatch Logs stop logging. What should you troubleshoot?  
A. Agent permissions  
B. S3 bucket versioning  
C. CodePipeline failure  
D. Lambda timeout  
**Answer**: A  
**Explanation**: Permissions stop logging.

### Question 44
An app logs errors without alerts. What should you set?  
A. CloudWatch alarm on log metric  
B. S3 event trigger  
C. CodeDeploy rollback  
D. Athena query  
**Answer**: A  
**Explanation**: Alarms alert on log metrics.

### Question 45
You need to query S3 access logs. Which tool?  
A. Amazon Athena  
B. CloudWatch Logs Insights  
C. AWS CodeGuru  
D. EventBridge  
**Answer**: A  
**Explanation**: Athena queries S3 logs.

### Question 46
A monthly task isn’t running. What should you configure?  
A. EventBridge schedule  
B. CloudWatch alarm  
C. S3 event notification  
D. CodePipeline stage  
**Answer**: A  
**Explanation**: EventBridge schedules monthly tasks.

### Question 47
You need real-time log alerts. What should you use?  
A. CloudWatch Logs subscription  
B. S3 export task  
C. CodeDeploy hooks  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Subscriptions enable real-time alerts.

### Question 48
You need to alert on network latency. What should you configure?  
A. CloudWatch alarm with custom metric  
B. Athena query on S3  
C. EventBridge with SQS  
D. CodeDeploy rollback  
**Answer**: A  
**Explanation**: Alarms monitor latency.

### Question 49
Athena queries are costly. What should you apply?  
A. ORC format  
B. Lambda memory increase  
C. CloudWatch metrics  
D. CodePipeline stages  
**Answer**: A  
**Explanation**: ORC reduces query costs.

### Question 50
An EventBridge rule fails across regions. What should you verify?  
A. Event bus access policy  
B. S3 bucket policy  
C. IAM user permissions  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Access policies enable cross-region rules.

### Question 51
You need 1-second metrics. What should you enable?  
A. High-resolution metrics  
B. Standard metrics  
C. S3 event triggers  
D. CodeDeploy settings  
**Answer**: A  
**Explanation**: High-resolution supports 1-second intervals.

### Question 52
CloudWatch Logs Insights shows no data. What should you ensure?  
A. Correct time range  
B. S3 export delay  
C. IAM role permissions  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: Time range affects data visibility.

---

## Domain 5: Incident and Event Response (14%) - 11 Questions

### Question 53
S3 deletes don’t trigger Lambda. What should you configure?  
A. S3 event notification  
B. CloudWatch alarm  
C. CodePipeline stage  
D. RDS failover  
**Answer**: A  
**Explanation**: Event notifications trigger Lambda.

### Question 54
GuardDuty detects malware. What should you automate?  
A. EventBridge with remediation  
B. Increase Lambda memory  
C. Enable S3 CRR  
D. Adjust CloudFormation  
**Answer**: A  
**Explanation**: EventBridge automates remediation.

### Question 55
CloudTrail logs need 1-year retention. What should you do?  
A. Export to S3 with lifecycle  
B. Enable Multi-AZ  
C. Set up Athena queries  
D. Increase Lambda timeout  
**Answer**: A  
**Explanation**: S3 lifecycle ensures retention.

### Question 56
You need S3 events for .txt files. What should you set?  
A. Event suffix filter  
B. CloudWatch Logs filter  
C. CodeDeploy hooks  
D. S3 bucket policy  
**Answer**: A  
**Explanation**: Suffix filters target .txt.

### Question 57
GuardDuty misses account-wide threats. What should you enable?  
A. AWS Organizations  
B. S3 bucket versioning  
C. Lambda concurrency  
D. CloudFormation StackSets  
**Answer**: A  
**Explanation**: Organizations enable account-wide GuardDuty.

### Question 58
CloudTrail lacks API Gateway logs. What should you activate?  
A. Data events  
B. Management events  
C. Insights events  
D. Multi-region setup  
**Answer**: A  
**Explanation**: Data events log API Gateway actions.

### Question 59
An S3 read should log to CloudWatch. What should you use?  
A. EventBridge with CloudWatch  
B. CloudWatch alarm  
C. CodeDeploy rollback  
D. RDS read replica  
**Answer**: A  
**Explanation**: EventBridge logs to CloudWatch.

### Question 60
GuardDuty misses EBS threats. What should you enable?  
A. EBS Protection  
B. S3 CRR  
C. Lambda aliases  
D. CloudFormation conditions  
**Answer**: A  
**Explanation**: EBS Protection enhances detection.

### Question 61
A VPC change needs investigation. Where do you check?  
A. CloudTrail logs  
B. CloudWatch metrics  
C. S3 event logs  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: CloudTrail logs VPC changes.

### Question 62
S3 events need SQS and email alerts. What should you configure?  
A. EventBridge  
B. CloudWatch Logs subscription  
C. CodeDeploy hooks  
D. Lambda concurrency  
**Answer**: A  
**Explanation**: EventBridge supports multiple targets.

### Question 63
CloudTrail misses regional actions. What should you ensure?  
A. All-regions trail  
B. S3 bucket encryption  
C. Lambda timeout  
D. RDS Multi-AZ  
**Answer**: A  
**Explanation**: All-regions trails capture all actions.

---

## Domain 6: Security and Compliance (17%) - 12 Questions

### Question 64
AWS Config flags IAM role issues. What should you implement?  
A. Managed rule  
B. Lambda concurrency  
C. S3 CRR  
D. CodePipeline stages  
**Answer**: A  
**Explanation**: Managed rules check IAM.

### Question 65
A Config rule needs runtime checks. What should you use?  
A. Lambda function  
B. S3 event trigger  
C. CloudWatch alarm  
D. CodeDeploy rollback  
**Answer**: A  
**Explanation**: Lambda runs custom checks.

### Question 66
You need compliance across accounts. What should you deploy?  
A. Config Aggregators  
B. StackSets  
C. S3 bucket policy  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Aggregators cover accounts.

### Question 67
WAF allows malicious requests. What should you configure?  
A. Rate-based rule  
B. S3 bucket policy  
C. CloudTrail logs  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: Rate-based rules limit malicious traffic.

### Question 68
Firewall Manager doesn’t apply to new accounts. What’s needed?  
A. AWS Organizations  
B. S3 bucket versioning  
C. CloudWatch metrics  
D. Lambda trigger  
**Answer**: A  
**Explanation**: Organizations apply policies to new accounts.

### Question 69
IAM Identity Center users can’t log in. What should you verify?  
A. Identity provider settings  
B. S3 event triggers  
C. CodePipeline artifacts  
D. RDS failover settings  
**Answer**: A  
**Explanation**: IdP settings affect logins.

### Question 70
A Config rule violation needs fixing. What should you use?  
A. SSM Run Command  
B. Lambda timeout  
C. S3 CRR  
D. CloudFormation outputs  
**Answer**: A  
**Explanation**: SSM fixes violations.

### Question 71
WAF needs to verify users. What should you enable?  
A. CAPTCHA action  
B. S3 bucket policy  
C. CloudTrail logs  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: CAPTCHA verifies users.

### Question 72
SSO with Okta fails. What should you integrate?  
A. IAM Identity Center  
B. AWS Config  
C. CodePipeline  
D. CloudWatch alarms  
**Answer**: A  
**Explanation**: IAM Identity Center integrates Okta.

### Question 73
Firewall Manager needs to secure ALBs. What should you create?  
A. WAF policy  
B. S3 event trigger  
C. Lambda concurrency  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: WAF policies secure ALBs.

### Question 74
Config rules need deployment automation. What should you use?  
A. Conformance packs  
B. S3 event triggers  
C. CloudTrail insights  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Conformance packs automate deployment.

### Question 75
IAM Identity Center needs dynamic access. What should you set?  
A. ABAC policies  
B. S3 bucket policies  
C. CodePipeline stages  
D. RDS Multi-AZ  
**Answer**: A  
**Explanation**: ABAC provides dynamic access.

---


# AWS Certified DevOps Engineer – Professional (DOP-C02) Practice Questions (Set 5)

---

## Domain 1: SDLC Automation (22%) - 17 Questions

### Question 1
A team uses CodePipeline to deploy a Node.js app to EC2. They need to run integration tests before production deployment. Where should you add this step?  
A. Add a CodeBuild action after the source stage  
B. Add a Lambda invoke action after deployment  
C. Modify the appspec.yml with test hooks  
D. Use CloudFormation to run tests  
**Answer**: A  
**Explanation**: A CodeBuild action before deployment runs tests efficiently.

### Question 2
A CodeBuild job fails due to a missing library. What should you check first?  
A. The buildspec.yml install phase  
B. CodePipeline IAM permissions  
C. S3 artifact encryption  
D. CloudWatch Logs retention  
**Answer**: A  
**Explanation**: The install phase in `buildspec.yml` handles dependencies.

### Question 3 (Multiple-Response)
Which TWO actions ensure a blue/green deployment to ECS with CodeDeploy?  
A. Configure an ECS service with a target group  
B. Use an ALB with dynamic port mapping  
C. Set a rolling update in CodePipeline  
D. Define hooks in appspec.yml  
**Answers**: A, B  
**Explanation**: ECS blue/green requires ALB and target group setup.

### Question 4
You need to adjust log levels dynamically during CodeDeploy based on environment. What should you use?  
A. DEPLOYMENT_GROUP_NAME variable in a script  
B. CloudFormation parameters  
C. S3 bucket metadata  
D. CodePipeline manual approval  
**Answer**: A  
**Explanation**: The variable identifies the deployment group dynamically.

### Question 5
A Lambda deployment needs 5% traffic for 10 minutes. What should you configure?  
A. CodeDeploy Canary5Percent10Minutes  
B. CodePipeline with S3 trigger  
C. CodeBuild with test phase  
D. CloudWatch alarm  
**Answer**: A  
**Explanation**: Canary5Percent10Minutes shifts traffic incrementally.

### Question 6
Your pipeline switches from Bitbucket to GitHub. What must you update?  
A. Source action provider in CodePipeline  
B. CodeBuild runtime environment  
C. S3 artifact bucket policy  
D. CloudTrail event filters  
**Answer**: A  
**Explanation**: Source action must reflect the new provider.

### Question 7
Which service caches Ruby gems for builds?  
A. AWS CodeArtifact  
B. AWS CodeStar  
C. AWS CodeGuru  
D. AWS CodeCommit  
**Answer**: A  
**Explanation**: CodeArtifact caches gems securely.

### Question 8
CodeGuru Reviewer finds a logic error in PHP code. What should you do?  
A. Refactor based on suggestions  
B. Increase CodePipeline timeout  
C. Enable S3 versioning  
D. Adjust buildspec.yml  
**Answer**: A  
**Explanation**: Reviewer suggestions guide logic fixes.

### Question 9
A multi-account pipeline fails to deploy. What’s the likely issue?  
A. Missing cross-account IAM roles  
B. CodeDeploy misconfiguration  
C. CloudWatch Logs disabled  
D. GitHub webhook failure  
**Answer**: A  
**Explanation**: Cross-account roles are required for access.

### Question 10
Your build needs a custom Go version. Where do you define it?  
A. CodeBuild environment settings  
B. CodePipeline source stage  
C. appspec.yml  
D. S3 bucket policy  
**Answer**: A  
**Explanation**: Environment settings specify Go versions.

### Question 11
You need to test an ECS app post-deployment. What should you use?  
A. CodeDeploy AfterAllowTestTraffic hook  
B. CodePipeline approval action  
C. CodeStar with S3 source  
D. CloudFormation with outputs  
**Answer**: A  
**Explanation**: Hooks run tests post-deployment.

### Question 12
A CodeBuild job fails to access a private subnet resource. What should you configure?  
A. VPC settings in CodeBuild  
B. S3 bucket ACL  
C. IAM user permissions  
D. CloudWatch Logs filter  
**Answer**: A  
**Explanation**: VPC settings enable private access.

### Question 13
Which deployment mode is safest for a critical prod update?  
A. Blue/Green  
B. Rolling  
C. All at Once  
D. Immutable  
**Answer**: A  
**Explanation**: Blue/Green ensures safe prod updates.

### Question 14
CodeGuru Profiler flags high latency in a Node.js app. What’s next?  
A. Optimize the flagged code  
B. Increase Lambda memory  
C. Enable S3 triggers  
D. Adjust CodeDeploy hooks  
**Answer**: A  
**Explanation**: Profiler identifies latency sources.

### Question 15
Pipeline stages fail to transition. What should you verify?  
A. Stage action configuration  
B. GitHub token  
C. IAM role scope  
D. S3 versioning  
**Answer**: A  
**Explanation**: Action config drives transitions.

### Question 16
Which service simplifies CI/CD setup for small teams?  
A. AWS CodeStar  
B. AWS CodePipeline  
C. AWS CodeArtifact  
D. AWS CodeGuru  
**Answer**: A  
**Explanation**: CodeStar simplifies setup.

### Question 17
CodeArtifact needs to proxy PyPI for a team. What should you set?  
A. Upstream repository policy  
B. S3 bucket lifecycle  
C. CloudTrail logging  
D. Lambda invoke  
**Answer**: A  
**Explanation**: Upstream proxies PyPI.

---

## Domain 2: Configuration Management and IaC (17%) - 13 Questions

### Question 18
A CloudFormation stack fails to update due to an error. What should you review?  
A. Stack events log  
B. S3 bucket permissions  
C. CodeDeploy logs  
D. CloudWatch metrics  
**Answer**: A  
**Explanation**: Stack events pinpoint update issues.

### Question 19
Which component allows user input in CloudFormation?  
A. Parameters  
B. Resources  
C. Outputs  
D. Mappings  
**Answer**: A  
**Explanation**: Parameters accept user input.

### Question 20
You need an ALB ARN in CloudFormation. Which function?  
A. Fn::GetAtt  
B. Fn::Ref  
C. Fn::Sub  
D. Fn::Join  
**Answer**: A  
**Explanation**: `GetAtt` retrieves ARNs.

### Question 21
StackSets don’t deploy to a new OU. What’s missing?  
A. OU-level permissions  
B. S3 bucket replication  
C. CodePipeline triggers  
D. CloudWatch alarms  
**Answer**: A  
**Explanation**: Permissions must include OUs.

### Question 22
Beanstalk update causes downtime. Which mode prevents this?  
A. Blue/Green  
B. All at Once  
C. Rolling  
D. Immutable  
**Answer**: A  
**Explanation**: Blue/Green avoids downtime.

### Question 23
You need to add a cron job to Beanstalk. Where do you define it?  
A. .ebextensions  
B. buildspec.yml  
C. appspec.yml  
D. CloudFormation conditions  
**Answer**: A  
**Explanation**: `.ebextensions` adds cron jobs.

### Question 24
A CloudFormation stack deletion leaves an S3 bucket. What should you add?  
A. DeletionPolicy: Delete  
B. S3 bucket versioning  
C. CodeDeploy hooks  
D. GitHub webhook  
**Answer**: A  
**Explanation**: `DeletionPolicy` ensures cleanup.

### Question 25
Which Beanstalk mode ensures no downtime with new instances?  
A. Immutable  
B. Rolling  
C. All at Once  
D. Blue/Green  
**Answer**: A  
**Explanation**: Immutable deploys new instances first.

### Question 26
You need to export an EBS volume ID. What should you use?  
A. Outputs  
B. Parameters  
C. Conditions  
D. Mappings  
**Answer**: A  
**Explanation**: Outputs export values.

### Question 27
Beanstalk needs a custom port. Where do you configure it?  
A. Environment settings  
B. S3 bucket policy  
C. CodeDeploy appspec.yml  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Settings adjust ports.

### Question 28
Which function links two strings in CloudFormation?  
A. Fn::Join  
B. Fn::GetAtt  
C. Fn::Ref  
D. Fn::ImportValue  
**Answer**: A  
**Explanation**: `Join` links strings.

### Question 29
You need IaC for new accounts via Control Tower. What’s best?  
A. CfCT with StackSets  
B. CodePipeline  
C. Elastic Beanstalk  
D. Nested Stacks  
**Answer**: A  
**Explanation**: CfCT automates Control Tower IaC.

### Question 30
Beanstalk needs IPv6 support. What should you do?  
A. Enable dualstack on ALB  
B. S3 event trigger  
C. CodeDeploy hooks  
D. CloudFormation conditions  
**Answer**: A  
**Explanation**: Dualstack enables IPv6.

---

## Domain 3: Resilient Cloud Solutions (15%) - 11 Questions

### Question 31
RDS fails during updates. What should you configure?  
A. Reader instance with cluster endpoint  
B. DynamoDB Global Tables  
C. S3 CRR  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Reader instances maintain availability.

### Question 32
Which service provides multi-region HA for key-value data?  
A. DynamoDB Global Tables  
B. RDS Multi-AZ  
C. EFS Multi-AZ  
D. S3 versioning  
**Answer**: A  
**Explanation**: Global Tables offer multi-region HA.

### Question 33
Your DR needs low RTO and high cost. Which strategy?  
A. Multi-Site  
B. Backup and Restore  
C. Warm Standby  
D. Pilot Light  
**Answer**: A  
**Explanation**: Multi-Site ensures low RTO.

### Question 34
Lambda cold starts delay responses. What should you use?  
A. Provisioned concurrency  
B. S3 bucket size  
C. CodePipeline stages  
D. Timeout  
**Answer**: A  
**Explanation**: Provisioned concurrency reduces cold starts.

### Question 35
ECS needs AZ redundancy. What should you configure?  
A. Fargate with ASG across AZs  
B. EC2 with rolling  
C. Lambda with S3  
D. CloudFormation outputs  
**Answer**: A  
**Explanation**: Fargate with ASG ensures redundancy.

### Question 36
S3 CRR fails for some objects. What should you enable?  
A. Versioning on both buckets  
B. Multi-AZ  
C. CloudWatch alarms  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: Versioning is required for CRR.

### Question 37
Route 53 doesn’t failover. What should you verify?  
A. Health check thresholds  
B. S3 bucket policy  
C. IAM permissions  
D. CloudTrail logs  
**Answer**: A  
**Explanation**: Thresholds trigger failover.

### Question 38
Your DR needs low cost and moderate RTO. Which approach?  
A. Warm Standby  
B. Multi-Site  
C. Pilot Light  
D. Backup and Restore  
**Answer**: A  
**Explanation**: Warm Standby balances cost and RTO.

### Question 39
Lambda throttles under load. What should you adjust?  
A. Reserved concurrency  
B. S3 CRR  
C. CodeDeploy timeout  
D. CloudWatch metrics  
**Answer**: A  
**Explanation**: Reserved concurrency prevents throttling.

### Question 40
ElastiCache fails during AZ outage. What should you enable?  
A. Multi-AZ replication  
B. S3 event triggers  
C. Lambda concurrency  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Multi-AZ ensures failover.

### Question 41
ECS startup delays increase. What should you use?  
A. Warm pool with lifecycle hooks  
B. S3 bucket lifecycle  
C. Lambda timeout  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: Warm pools speed startup.

---

## Domain 4: Monitoring and Logging (15%) - 11 Questions

### Question 42
You need to track API latency in Lambda. What should you do?  
A. Log metrics to CloudWatch Logs  
B. Enable S3 event logging  
C. Configure CodeDeploy  
D. Adjust RDS Multi-AZ  
**Answer**: A  
**Explanation**: Logs capture latency metrics.

### Question 43
CloudWatch Logs don’t show Lambda errors. What should you fix?  
A. Lambda execution role permissions  
B. S3 bucket versioning  
C. CodePipeline failure  
D. Lambda timeout  
**Answer**: A  
**Explanation**: Role permissions enable logging.

### Question 44
An app crashes without notice. What should you set up?  
A. CloudWatch alarm on error logs  
B. S3 event trigger  
C. CodeDeploy rollback  
D. Athena query  
**Answer**: A  
**Explanation**: Alarms detect crashes.

### Question 45
You need to analyze ALB logs. Which tool?  
A. Amazon Athena  
B. CloudWatch Logs Insights  
C. AWS CodeGuru  
D. EventBridge  
**Answer**: A  
**Explanation**: Athena queries ALB logs in S3.

### Question 46
A daily backup fails to run. What should you schedule?  
A. EventBridge rule  
B. CloudWatch alarm  
C. S3 event notification  
D. CodePipeline stage  
**Answer**: A  
**Explanation**: EventBridge schedules daily tasks.

### Question 47
You need real-time error alerts. What should you configure?  
A. CloudWatch Logs subscription  
B. S3 export task  
C. CodeDeploy hooks  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Subscriptions provide real-time alerts.

### Question 48
You need to notify on high latency. What should you use?  
A. CloudWatch alarm with metric filter  
B. Athena query on S3  
C. EventBridge with SQS  
D. CodeDeploy rollback  
**Answer**: A  
**Explanation**: Metric filters trigger latency alerts.

### Question 49
Athena queries are slow for VPC logs. What should you do?  
A. Convert logs to Parquet  
B. Increase Lambda memory  
C. Enable CloudWatch metrics  
D. Adjust CodePipeline  
**Answer**: A  
**Explanation**: Parquet speeds queries.

### Question 50
An EventBridge rule fails cross-account. What should you check?  
A. Event bus permissions  
B. S3 bucket policy  
C. IAM user roles  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Permissions enable cross-account rules.

### Question 51
You need 15-second metric resolution. What should you enable?  
A. High-resolution metrics  
B. Standard metrics  
C. S3 event triggers  
D. CodeDeploy settings  
**Answer**: A  
**Explanation**: High-resolution supports 15 seconds.

### Question 52
CloudWatch Logs Insights misses data. What should you verify?  
A. Log group retention  
B. S3 export delay  
C. IAM role permissions  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: Retention affects data availability.

---

## Domain 5: Incident and Event Response (14%) - 11 Questions

### Question 53
S3 puts don’t trigger Lambda. What should you set?  
A. S3 event notification  
B. CloudWatch alarm  
C. CodePipeline stage  
D. RDS failover  
**Answer**: A  
**Explanation**: Notifications trigger Lambda.

### Question 54
GuardDuty detects a threat. What should you automate?  
A. EventBridge rule with SSM  
B. Increase Lambda memory  
C. Enable S3 CRR  
D. Adjust CloudFormation  
**Answer**: A  
**Explanation**: EventBridge automates remediation.

### Question 55
CloudTrail logs need 6-month retention. What should you do?  
A. Export to S3 with lifecycle  
B. Enable Multi-AZ  
C. Set up Athena queries  
D. Increase Lambda timeout  
**Answer**: A  
**Explanation**: S3 lifecycle retains logs.

### Question 56
You need S3 events for .json files. What should you apply?  
A. Event suffix filter  
B. CloudWatch Logs filter  
C. CodeDeploy hooks  
D. S3 bucket policy  
**Answer**: A  
**Explanation**: Suffix filters target .json.

### Question 57
GuardDuty needs multi-account visibility. What should you enable?  
A. AWS Organizations  
B. S3 bucket versioning  
C. Lambda concurrency  
D. CloudFormation StackSets  
**Answer**: A  
**Explanation**: Organizations enable multi-account GuardDuty.

### Question 58
CloudTrail misses S3 deletes. What should you activate?  
A. Data events  
B. Management events  
C. Insights events  
D. Multi-region setup  
**Answer**: A  
**Explanation**: Data events log S3 actions.

### Question 59
An EC2 restart needs notification. What should you use?  
A. EventBridge with SNS  
B. CloudWatch alarm  
C. CodeDeploy rollback  
D. RDS read replica  
**Answer**: A  
**Explanation**: EventBridge with SNS notifies.

### Question 60
GuardDuty misses ECS threats. What should you enable?  
A. ECS Runtime Monitoring  
B. S3 CRR  
C. Lambda aliases  
D. CloudFormation conditions  
**Answer**: A  
**Explanation**: Runtime Monitoring enhances ECS detection.

### Question 61
An IAM policy change needs auditing. Where do you look?  
A. CloudTrail logs  
B. CloudWatch metrics  
C. S3 event logs  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: CloudTrail logs IAM changes.

### Question 62
S3 events need Lambda and SQS triggers. What should you use?  
A. EventBridge  
B. CloudWatch Logs subscription  
C. CodeDeploy hooks  
D. Lambda concurrency  
**Answer**: A  
**Explanation**: EventBridge supports multiple triggers.

### Question 63
CloudTrail logs lack detail. What should you ensure?  
A. All-regions trail  
B. S3 bucket encryption  
C. Lambda timeout  
D. RDS Multi-AZ  
**Answer**: A  
**Explanation**: All-regions trails provide full detail.

---

## Domain 6: Security and Compliance (17%) - 12 Questions

### Question 64
AWS Config flags missing EBS tags. What should you set?  
A. Managed rule with SSM remediation  
B. Lambda concurrency  
C. S3 CRR  
D. CodePipeline stages  
**Answer**: A  
**Explanation**: Managed rules enforce tags.

### Question 65
A Config rule needs custom logic for KMS keys. What should you use?  
A. Lambda-backed rule  
B. S3 event trigger  
C. CloudWatch alarm  
D. CodeDeploy rollback  
**Answer**: A  
**Explanation**: Lambda provides custom logic.

### Question 66
You need compliance across regions. What should you deploy?  
A. Config Aggregators  
B. StackSets  
C. S3 bucket policy  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Aggregators span regions.

### Question 67
WAF misses DDoS attempts. What should you add?  
A. Rate-based rule  
B. S3 bucket policy  
C. CloudTrail logs  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: Rate-based rules catch DDoS.

### Question 68
Firewall Manager skips new ALBs. What’s needed?  
A. AWS Organizations integration  
B. S3 bucket versioning  
C. CloudWatch metrics  
D. Lambda trigger  
**Answer**: A  
**Explanation**: Organizations enforce ALB coverage.

### Question 69
IAM Identity Center users lack SSO. What should you check?  
A. Permission set mappings  
B. S3 event triggers  
C. CodePipeline artifacts  
D. RDS failover settings  
**Answer**: A  
**Explanation**: Mappings grant SSO access.

### Question 70
A Config rule needs auto-fix for untagged resources. What should you use?  
A. SSM Automation  
B. Lambda timeout  
C. S3 CRR  
D. CloudFormation outputs  
**Answer**: A  
**Explanation**: SSM automates tagging.

### Question 71
WAF needs to block bots. What should you enable?  
A. Bot Control rule  
B. S3 bucket policy  
C. CloudTrail logs  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: Bot Control blocks bots.

### Question 72
SSO with SAML fails. What should you integrate?  
A. IAM Identity Center  
B. AWS Config  
C. CodePipeline  
D. CloudWatch alarms  
**Answer**: A  
**Explanation**: IAM Identity Center supports SAML.

### Question 73
Firewall Manager needs to protect APIs. What should you create?  
A. WAF policy  
B. S3 event trigger  
C. Lambda concurrency  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: WAF policies protect APIs.

### Question 74
Config rules need standardization. What should you use?  
A. Conformance packs  
B. S3 event triggers  
C. CloudTrail insights  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Conformance packs standardize rules.

### Question 75
IAM Identity Center needs attribute-based access. What should you set?  
A. ABAC with tags  
B. S3 bucket policies  
C. CodePipeline stages  
D. RDS Multi-AZ  
**Answer**: A  
**Explanation**: ABAC uses attributes for access.

---

# AWS Certified DevOps Engineer – Professional (DOP-C02) Practice Questions (Set 6)

---

## Domain 1: SDLC Automation (22%) - 17 Questions

### Question 1
A team deploys a Python app via CodePipeline to ECS. They need unit tests before staging. Where should you add this?  
A. CodeBuild action post-source  
B. Lambda action post-deploy  
C. appspec.yml with hooks  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: CodeBuild runs tests pre-staging.

### Question 2
A CodeBuild job fails with a network error. What should you troubleshoot?  
A. VPC configuration  
B. CodePipeline permissions  
C. S3 artifact encryption  
D. CloudWatch retention  
**Answer**: A  
**Explanation**: VPC config affects network access.

### Question 3 (Multiple-Response)
Which TWO steps enable canary deployment to Lambda?  
A. Use CodeDeploy with canary config  
B. Configure ALB with target group  
C. Set CodePipeline to rolling  
D. Define validation hooks  
**Answers**: A, D  
**Explanation**: CodeDeploy and hooks support canary.

### Question 4
You need to set environment variables during CodeDeploy based on group. What should you use?  
A. DEPLOYMENT_GROUP_NAME in script  
B. CloudFormation outputs  
C. S3 metadata tags  
D. CodePipeline approval  
**Answer**: A  
**Explanation**: The variable dynamically sets vars.

### Question 5
A Lambda deployment needs 15% traffic for 5 minutes. What should you configure?  
A. CodeDeploy Linear15Percent5Minutes  
B. CodePipeline with S3 source  
C. CodeBuild with tests  
D. CloudWatch alarm  
**Answer**: A  
**Explanation**: Linear15Percent5Minutes shifts traffic.

### Question 6
Your pipeline moves to GitLab Enterprise. What must you change?  
A. Source provider in CodePipeline  
B. CodeBuild environment  
C. S3 artifact policy  
D. CloudTrail filters  
**Answer**: A  
**Explanation**: Source provider updates to GitLab.

### Question 7
Which service manages Go dependencies?  
A. AWS CodeArtifact  
B. AWS CodeStar  
C. AWS CodeGuru  
D. AWS CodeDeploy  
**Answer**: A  
**Explanation**: CodeArtifact manages Go deps.

### Question 8
CodeGuru Reviewer detects a null pointer in Java. What’s next?  
A. Fix based on recommendations  
B. Increase CodePipeline stages  
C. Enable S3 events  
D. Adjust buildspec.yml  
**Answer**: A  
**Explanation**: Recommendations guide fixes.

### Question 9
A pipeline fails in a multi-region setup. What should you check?  
A. IAM roles for regional access  
B. CodeDeploy settings  
C. CloudWatch Logs  
D. GitHub webhook  
**Answer**: A  
**Explanation**: IAM roles enable multi-region access.

### Question 10
Your build needs a custom Ruby version. Where do you specify it?  
A. CodeBuild environment  
B. CodePipeline source  
C. appspec.yml  
D. S3 bucket  
**Answer**: A  
**Explanation**: Environment sets Ruby version.

### Question 11
You need to validate an ECS app post-deploy. What should you use?  
A. CodeDeploy AfterAllowTraffic hook  
B. CodePipeline approval  
C. CodeStar with S3  
D. CloudFormation outputs  
**Answer**: A  
**Explanation**: Hooks validate post-deploy.

### Question 12
A CodeBuild job can’t access an RDS instance. What should you add?  
A. VPC endpoint  
B. S3 bucket ACL  
C. IAM user role  
D. CloudWatch filter  
**Answer**: A  
**Explanation**: VPC endpoints enable RDS access.

### Question 13
Which deployment mode suits a quick test update?  
A. All at Once  
B. Rolling  
C. Blue/Green  
D. Immutable  
**Answer**: A  
**Explanation**: All at Once is quickest for tests.

### Question 14
CodeGuru Profiler shows memory spikes in Python. What should you do?  
A. Optimize memory usage  
B. Increase Lambda timeout  
C. Enable S3 versioning  
D. Adjust CodeDeploy hooks  
**Answer**: A  
**Explanation**: Profiler guides memory fixes.

### Question 15
Pipeline artifacts don’t reach deploy stage. What should you verify?  
A. CodeBuild output config  
B. GitHub creds  
C. IAM role limits  
D. S3 encryption  
**Answer**: A  
**Explanation**: Output config ensures artifact flow.

### Question 16
Which service streamlines CI/CD for startups?  
A. AWS CodeStar  
B. AWS CodePipeline  
C. AWS CodeArtifact  
D. AWS CodeGuru  
**Answer**: A  
**Explanation**: CodeStar streamlines for startups.

### Question 17
CodeArtifact needs to cache npm packages. What should you configure?  
A. Upstream repository  
B. S3 lifecycle policy  
C. CloudTrail logs  
D. Lambda invoke  
**Answer**: A  
**Explanation**: Upstream caches npm.

---

## Domain 2: Configuration Management and IaC (17%) - 13 Questions

### Question 18
A CloudFormation stack fails to create. What should you check?  
A. Resource dependencies  
B. S3 bucket permissions  
C. CodeDeploy logs  
D. CloudWatch metrics  
**Answer**: A  
**Explanation**: Dependencies cause creation failures.

### Question 19
Which component sets region-specific values in CloudFormation?  
A. Mappings  
B. Parameters  
C. Outputs  
D. Conditions  
**Answer**: A  
**Explanation**: Mappings set region-specific values.

### Question 20
You need an EFS ID in CloudFormation. Which function?  
A. Fn::Ref  
B. Fn::GetAtt  
C. Fn::Join  
D. Fn::Sub  
**Answer**: A  
**Explanation**: `Ref` retrieves IDs.

### Question 21
StackSets fail for new accounts. What should you ensure?  
A. Account-level IAM roles  
B. S3 bucket replication  
C. CodePipeline triggers  
D. CloudWatch alarms  
**Answer**: A  
**Explanation**: Roles enable account deployment.

### Question 22
Beanstalk update disrupts users. Which mode prevents this?  
A. Blue/Green  
B. All at Once  
C. Rolling  
D. Immutable  
**Answer**: A  
**Explanation**: Blue/Green avoids disruption.

### Question 23
You need to install a package on Beanstalk. Where do you define it?  
A. .ebextensions  
B. buildspec.yml  
C. appspec.yml  
D. CloudFormation mappings  
**Answer**: A  
**Explanation**: `.ebextensions` installs packages.

### Question 24
A CloudFormation stack leaves an EBS volume. What should you add?  
A. DeletionPolicy: Delete  
B. S3 bucket versioning  
C. CodeDeploy hooks  
D. GitHub webhook  
**Answer**: A  
**Explanation**: `DeletionPolicy` cleans up volumes.

### Question 25
Which Beanstalk mode ensures capacity during updates?  
A. Immutable  
B. Rolling  
C. All at Once  
D. Blue/Green  
**Answer**: A  
**Explanation**: Immutable maintains capacity.

### Question 26
You need to conditionally create an S3 bucket. What should you use?  
A. Conditions  
B. Parameters  
C. Mappings  
D. Outputs  
**Answer**: A  
**Explanation**: Conditions control creation.

### Question 27
Beanstalk needs a custom DB connection. Where do you set it?  
A. Environment variables  
B. S3 bucket policy  
C. CodeDeploy appspec.yml  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Variables set DB connections.

### Question 28
Which function exports an ALB DNS name?  
A. Fn::GetAtt  
B. Fn::Ref  
C. Fn::ImportValue  
D. Fn::Join  
**Answer**: A  
**Explanation**: `GetAtt` exports DNS names.

### Question 29
You need IaC for multi-region deployment. What’s best?  
A. StackSets  
B. CodePipeline  
C. Elastic Beanstalk  
D. Nested Stacks  
**Answer**: A  
**Explanation**: StackSets handle multi-region.

### Question 30
Beanstalk needs a custom SSL cert. Where do you configure it?  
A. Environment config  
B. S3 event trigger  
C. CodeDeploy hooks  
D. CloudFormation conditions  
**Answer**: A  
**Explanation**: Config sets SSL certs.

---

## Domain 3: Resilient Cloud Solutions (15%) - 11 Questions

### Question 31
Aurora fails during maintenance. What should you add?  
A. Reader instance with ANY endpoint  
B. DynamoDB Global Tables  
C. S3 CRR  
D. Lambda concurrency  
**Answer**: A  
**Explanation**: ANY endpoint maintains availability.

### Question 32
Which service offers global HA for relational data?  
A. Aurora Global Database  
B. RDS Multi-AZ  
C. EFS Multi-AZ  
D. S3 versioning  
**Answer**: A  
**Explanation**: Aurora Global provides global HA.

### Question 33
Your DR needs moderate RTO and low cost. Which strategy?  
A. Pilot Light  
B. Multi-Site  
C. Warm Standby  
D. Backup and Restore  
**Answer**: A  
**Explanation**: Pilot Light balances RTO and cost.

### Question 34
Lambda delays under burst traffic. What should you adjust?  
A. Provisioned concurrency  
B. S3 bucket size  
C. CodePipeline stages  
D. Timeout  
**Answer**: A  
**Explanation**: Provisioned concurrency handles bursts.

### Question 35
ECS needs multi-AZ HA. What should you configure?  
A. Fargate with ASG  
B. EC2 with rolling  
C. Lambda with S3  
D. CloudFormation outputs  
**Answer**: A  
**Explanation**: Fargate with ASG ensures HA.

### Question 36
S3 CRR skips deletes. What should you enable?  
A. Delete marker replication  
B. Multi-AZ  
C. CloudWatch alarms  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: Delete markers sync deletes.

### Question 37
Route 53 latency routing fails. What should you check?  
A. Health check status  
B. S3 bucket policy  
C. IAM permissions  
D. CloudTrail logs  
**Answer**: A  
**Explanation**: Health checks drive latency routing.

### Question 38
Your DR needs fast recovery and moderate cost. Which approach?  
A. Warm Standby  
B. Multi-Site  
C. Pilot Light  
D. Backup and Restore  
**Answer**: A  
**Explanation**: Warm Standby offers fast recovery.

### Question 39
Lambda startup slows under load. What should you use?  
A. Provisioned concurrency  
B. S3 CRR  
C. CodeDeploy timeout  
D. CloudWatch metrics  
**Answer**: A  
**Explanation**: Provisioned concurrency speeds startup.

### Question 40
ElastiCache fails on node crash. What should you enable?  
A. Multi-AZ with backups  
B. S3 event triggers  
C. Lambda concurrency  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Multi-AZ with backups ensures recovery.

### Question 41
ECS tasks delay on launch. What should you implement?  
A. Warm pool with hooks  
B. S3 bucket lifecycle  
C. Lambda timeout  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: Warm pools reduce launch delays.

---

## Domain 4: Monitoring and Logging (15%) - 11 Questions

### Question 42
You need to monitor SQS queue depth. What should you do?  
A. Push metrics to CloudWatch Logs  
B. Enable S3 event logging  
C. Configure CodeDeploy  
D. Adjust RDS Multi-AZ  
**Answer**: A  
**Explanation**: Logs push queue metrics.

### Question 43
CloudWatch Logs miss ECS task logs. What should you fix?  
A. Task role permissions  
B. S3 bucket versioning  
C. CodePipeline failure  
D. Lambda timeout  
**Answer**: A  
**Explanation**: Role permissions enable logging.

### Question 44
An app fails without alerts. What should you configure?  
A. CloudWatch alarm on logs  
B. S3 event trigger  
C. CodeDeploy rollback  
D. Athena query  
**Answer**: A  
**Explanation**: Alarms alert on failures.

### Question 45
You need to query ECS logs. Which tool?  
A. Amazon Athena  
B. CloudWatch Logs Insights  
C. AWS CodeGuru  
D. EventBridge  
**Answer**: A  
**Explanation**: Athena queries S3-stored logs.

### Question 46
A weekly task isn’t triggering. What should you schedule?  
A. EventBridge rule  
B. CloudWatch alarm  
C. S3 event notification  
D. CodePipeline stage  
**Answer**: A  
**Explanation**: EventBridge schedules weekly tasks.

### Question 47
You need real-time latency alerts. What should you set?  
A. CloudWatch Logs subscription  
B. S3 export task  
C. CodeDeploy hooks  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Subscriptions alert in real-time.

### Question 48
You need to notify on CPU spikes. What should you use?  
A. CloudWatch alarm with metric  
B. Athena query on S3  
C. EventBridge with SQS  
D. CodeDeploy rollback  
**Answer**: A  
**Explanation**: Alarms notify on CPU spikes.

### Question 49
Athena queries lag for ALB logs. What should you do?  
A. Partition data by date  
B. Increase Lambda memory  
C. Enable CloudWatch metrics  
D. Adjust CodePipeline  
**Answer**: A  
**Explanation**: Partitioning speeds ALB queries.

### Question 50
An EventBridge rule fails cross-region. What should you verify?  
A. Event bus policy  
B. S3 bucket policy  
C. IAM user roles  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Policy enables cross-region rules.

### Question 51
You need 30-second metrics. What should you enable?  
A. High-resolution metrics  
B. Standard metrics  
C. S3 event triggers  
D. CodeDeploy settings  
**Answer**: A  
**Explanation**: High-resolution supports 30 seconds.

### Question 52
CloudWatch Logs Insights lacks recent data. What should you check?  
A. Log ingestion delay  
B. S3 export delay  
C. IAM role permissions  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: Ingestion delay affects recent data.

---

## Domain 5: Incident and Event Response (14%) - 11 Questions

### Question 53
S3 deletes don’t trigger SNS. What should you configure?  
A. S3 event notification  
B. CloudWatch alarm  
C. CodePipeline stage  
D. RDS failover  
**Answer**: A  
**Explanation**: Notifications trigger SNS.

### Question 54
GuardDuty finds a phishing attempt. What should you automate?  
A. EventBridge with Lambda  
B. Increase Lambda memory  
C. Enable S3 CRR  
D. Adjust CloudFormation  
**Answer**: A  
**Explanation**: EventBridge automates responses.

### Question 55
CloudTrail logs need 1-year storage. What should you do?  
A. Export to S3 with lifecycle  
B. Enable Multi-AZ  
C. Set up Athena queries  
D. Increase Lambda timeout  
**Answer**: A  
**Explanation**: S3 lifecycle stores logs.

### Question 56
You need S3 events for .xml files. What should you set?  
A. Event suffix filter  
B. CloudWatch Logs filter  
C. CodeDeploy hooks  
D. S3 bucket policy  
**Answer**: A  
**Explanation**: Suffix filters target .xml.

### Question 57
GuardDuty needs org-wide visibility. What should you enable?  
A. AWS Organizations  
B. S3 bucket versioning  
C. Lambda concurrency  
D. CloudFormation StackSets  
**Answer**: A  
**Explanation**: Organizations provide org-wide visibility.

### Question 58
CloudTrail misses DynamoDB actions. What should you activate?  
A. Data events  
B. Management events  
C. Insights events  
D. Multi-region setup  
**Answer**: A  
**Explanation**: Data events log DynamoDB actions.

### Question 59
A security group change needs alerting. What should you use?  
A. EventBridge with SNS  
B. CloudWatch alarm  
C. CodeDeploy rollback  
D. RDS read replica  
**Answer**: A  
**Explanation**: EventBridge with SNS alerts.

### Question 60
GuardDuty misses EKS threats. What should you enable?  
A. EKS Runtime Monitoring  
B. S3 CRR  
C. Lambda aliases  
D. CloudFormation conditions  
**Answer**: A  
**Explanation**: Runtime Monitoring catches EKS threats.

### Question 61
A bucket ACL change needs tracking. Where do you look?  
A. CloudTrail logs  
B. CloudWatch metrics  
C. S3 event logs  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: CloudTrail tracks ACL changes.

### Question 62
S3 events need SNS and Lambda triggers. What should you use?  
A. EventBridge  
B. CloudWatch Logs subscription  
C. CodeDeploy hooks  
D. Lambda concurrency  
**Answer**: A  
**Explanation**: EventBridge supports multiple triggers.

### Question 63
CloudTrail logs are spotty. What should you ensure?  
A. Global trail  
B. S3 bucket encryption  
C. Lambda timeout  
D. RDS Multi-AZ  
**Answer**: A  
**Explanation**: Global trails ensure full coverage.

---

## Domain 6: Security and Compliance (17%) - 12 Questions

### Question 64
AWS Config flags unencrypted S3 buckets. What should you set?  
A. Managed rule with SSM fix  
B. Lambda concurrency  
C. S3 CRR  
D. CodePipeline stages  
**Answer**: A  
**Explanation**: Managed rules enforce encryption.

### Question 65
A Config rule needs custom IAM checks. What should you use?  
A. Lambda-backed rule  
B. S3 event trigger  
C. CloudWatch alarm  
D. CodeDeploy rollback  
**Answer**: A  
**Explanation**: Lambda provides custom IAM checks.

### Question 66
You need compliance across accounts. What should you deploy?  
A. Config Aggregators  
B. StackSets  
C. S3 bucket policy  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Aggregators cover accounts.

### Question 67
WAF allows SQL injections. What should you configure?  
A. SQL injection rule  
B. S3 bucket policy  
C. CloudTrail logs  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: SQL rules block injections.

### Question 68
Firewall Manager misses new APIs. What’s required?  
A. AWS Organizations  
B. S3 bucket versioning  
C. CloudWatch metrics  
D. Lambda trigger  
**Answer**: A  
**Explanation**: Organizations enforce API coverage.

### Question 69
IAM Identity Center users can’t access apps. What should you verify?  
A. App assignments  
B. S3 event triggers  
C. CodePipeline artifacts  
D. RDS failover settings  
**Answer**: A  
**Explanation**: Assignments grant app access.

### Question 70
A Config rule needs auto-fix for unencrypted volumes. What should you use?  
A. SSM Automation  
B. Lambda timeout  
C. S3 CRR  
D. CloudFormation outputs  
**Answer**: A  
**Explanation**: SSM automates encryption.

### Question 71
WAF needs to challenge users. What should you enable?  
A. CAPTCHA rule  
B. S3 bucket policy  
C. CloudTrail logs  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: CAPTCHA challenges users.

### Question 72
SSO with Azure AD fails. What should you integrate?  
A. IAM Identity Center  
B. AWS Config  
C. CodePipeline  
D. CloudWatch alarms  
**Answer**: A  
**Explanation**: IAM Identity Center integrates Azure AD.

### Question 73
Firewall Manager needs to secure ALBs. What should you create?  
A. WAF policy  
B. S3 event trigger  
C. Lambda concurrency  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: WAF policies secure ALBs.

### Question 74
Config rules need consistent deployment. What should you use?  
A. Conformance packs  
B. S3 event triggers  
C. CloudTrail insights  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Conformance packs ensure consistency.

### Question 75
IAM Identity Center needs dynamic permissions. What should you configure?  
A. ABAC with user attributes  
B. S3 bucket policies  
C. CodePipeline stages  
D. RDS Multi-AZ  
**Answer**: A  
**Explanation**: ABAC provides dynamic permissions.

---


# AWS Certified DevOps Engineer – Professional (DOP-C02) Practice Questions (Set 7)

This set includes 75 scenario-based questions distributed across the six DOP-C02 domains per their official weightings. Questions mirror real-world DevOps challenges, with detailed explanations.

---

## Domain 1: SDLC Automation (22%) - 17 Questions

### Question 1
**Scenario**: A company uses AWS CodePipeline to deploy a Python Flask app hosted on Amazon ECS Fargate, sourced from a private GitHub repository. The pipeline includes a CodeBuild stage for unit tests and a CodeDeploy stage with blue/green deployment. After a recent update, production deployments failed because integration tests weren’t run, causing compatibility issues with a third-party API. The team needs integration tests to execute pre-deployment and halt if they fail, with results visible to developers.  
**Question**: What should a DevOps engineer do to meet these requirements?  
A. Add a CodeBuild action post-source to run integration tests and fail the pipeline if tests fail, publishing results to GitHub via webhooks.  
B. Configure a Lambda function in CodePipeline to invoke integration tests and post results to S3, with a manual approval step.  
C. Update the CodeDeploy appspec.yml with a BeforeAllowTraffic hook to run tests and exit on failure.  
D. Use AWS CodeStar to add an integration test stage and notify via SNS.  
**Answer**: A  
**Explanation**: A CodeBuild action post-source runs integration tests early, fails the pipeline if needed, and integrates with GitHub for visibility, meeting all requirements efficiently. C’s hook runs too late (post-deployment), B adds unnecessary complexity, and D lacks GitHub integration.

### Question 2
**Scenario**: A team’s CodeBuild project compiles a Java app, but builds fail intermittently due to Maven dependency timeouts. The app requires external libraries hosted on a private Nexus repository.  
**Question**: What should a DevOps engineer check first to resolve this?  
A. The buildspec.yml `install` phase for Nexus connectivity  
B. CodePipeline stage permissions  
C. S3 artifact bucket policy  
D. CloudWatch Logs retention settings  
**Answer**: A  
**Explanation**: The `install` phase in `buildspec.yml` configures dependency retrieval; timeouts suggest a connectivity or auth issue with Nexus.

### Question 3 (Multiple-Response)
**Scenario**: A company deploys a Node.js app to EC2 using CodePipeline and CodeDeploy. They want a canary deployment with 10% traffic for 20 minutes, rolling back on errors.  
**Question**: Which TWO steps are required?  
A. Configure CodeDeploy with Canary10Percent20Minutes  
B. Set an ALB with a target group for canary routing  
C. Add a rolling update policy in CodePipeline  
D. Use a BeforeAllowTraffic hook to validate app health  
**Answers**: A, B  
**Explanation**: A sets the canary deployment in CodeDeploy, and B ensures ALB routes traffic correctly. C is irrelevant (rolling is different), and D validates but isn’t required for rollback.

### Question 4
**Scenario**: A company uses CodePipeline to deploy a Ruby app to EC2. They need to adjust app configs based on deployment environment (dev, prod) without multiple app versions.  
**Question**: What should a DevOps engineer use?  
A. DEPLOYMENT_GROUP_NAME variable in a deployment script  
B. CloudFormation stack parameters  
C. S3 bucket metadata tags  
D. CodePipeline environment variables  
**Answer**: A  
**Explanation**: `DEPLOYMENT_GROUP_NAME` dynamically identifies the environment in CodeDeploy, reducing version overhead.

### Question 5
**Scenario**: A company runs a microservices-based application on Amazon ECS with an Application Load Balancer (ALB) in front. They use AWS CodePipeline to deploy updates from a GitHub repository, with a build stage using AWS CodeBuild and a deployment stage using AWS CodeDeploy with a blue/green strategy. Recently, deployments have failed intermittently because some ECS tasks fail health checks due to database migrations not completing before traffic shifts. The company wants deployments to wait until migrations are verified and roll back if they fail, with minimal manual intervention.  
**Question**: Which combination of steps should a DevOps engineer take to meet these requirements? (Choose two.)  
A. Add a CodeBuild action post-source to run migration scripts and output a success flag to an S3 artifact.  
B. Modify the CodeDeploy appspec.yml to include an AfterAllowTestTraffic hook that checks the S3 artifact flag and exits with an error if migrations fail.  
C. Configure a manual approval action in CodePipeline before deployment to verify migrations.  
D. Use an EventBridge rule to trigger a Lambda function that runs migrations and updates an SSM parameter, checked by CodeDeploy hooks.  
E. Update the ECS service definition to include a health check grace period of 300 seconds to allow migrations to complete.  
**Answers**: B, D  
**Explanation**: B uses a hook to verify migrations pre-traffic shift with rollback, and D automates migrations via EventBridge and SSM, minimizing intervention. A lacks rollback integration, C requires manual effort, and E delays but doesn’t verify.

### Question 6
**Scenario**: A pipeline switches from GitHub to GitLab. The build stage uses CodeBuild, and deployment targets Lambda.  
**Question**: What must be updated?  
A. Source action in CodePipeline to GitLab  
B. CodeBuild runtime environment  
C. S3 artifact bucket policy  
D. CloudTrail event rules  
**Answer**: A  
**Explanation**: The source action must reflect the new GitLab provider.

### Question 7
**Scenario**: A team uses CodeArtifact to manage Python dependencies for a CodeBuild project. Builds fail because a required package isn’t available.  
**Question**: What should a DevOps engineer configure?  
A. An upstream PyPI repository in CodeArtifact  
B. A new CodeStar project  
C. CodeGuru profiling  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: An upstream PyPI repo ensures external packages are cached.

### Question 8
**Scenario**: CodeGuru Reviewer flags a potential SQL injection in a PHP app during a CodePipeline build.  
**Question**: What should a DevOps engineer do?  
A. Refactor code per recommendations  
B. Increase CodePipeline timeout  
C. Enable S3 versioning  
D. Adjust buildspec.yml phases  
**Answer**: A  
**Explanation**: Fixing the code addresses the security flaw directly.

### Question 9
**Scenario**: A multi-region CodePipeline fails to deploy to us-west-2 due to artifact access issues.  
**Question**: What’s the likely cause?  
A. Missing IAM permissions for cross-region S3 access  
B. CodeDeploy misconfiguration  
C. CloudWatch Logs disabled  
D. GitHub webhook failure  
**Answer**: A  
**Explanation**: Cross-region S3 access requires IAM permissions.

### Question 10
**Scenario**: A build requires a specific Java version not in the default CodeBuild image.  
**Question**: Where should a DevOps engineer specify this?  
A. CodeBuild environment settings  
B. CodePipeline source stage  
C. appspec.yml  
D. S3 bucket policy  
**Answer**: A  
**Explanation**: Environment settings define custom runtimes.

### Question 11
**Scenario**: A team deploys an ECS app with CodeDeploy and needs to verify database connectivity post-deployment.  
**Question**: What should be used?  
A. AfterAllowTraffic hook in appspec.yml  
B. CodePipeline approval action  
C. CodeStar notifications  
D. CloudFormation outputs  
**Answer**: A  
**Explanation**: The hook verifies connectivity post-deployment.

### Question 12
**Scenario**: A CodeBuild job fails to access a private API Gateway endpoint.  
**Question**: What should a DevOps engineer configure?  
A. VPC settings in CodeBuild  
B. S3 bucket policy  
C. IAM user permissions  
D. CloudWatch Logs subscription  
**Answer**: A  
**Explanation**: VPC settings enable private endpoint access.

### Question 13
**Scenario**: A team needs a low-risk deployment for a critical ECS app update.  
**Question**: Which mode should be used?  
A. Blue/Green  
B. Rolling  
C. All at Once  
D. Immutable  
**Answer**: A  
**Explanation**: Blue/Green minimizes risk with a separate environment.

### Question 14
**Scenario**: CodeGuru Profiler shows high CPU usage in a Node.js Lambda function during a CodePipeline deploy.  
**Question**: What should a DevOps engineer do?  
A. Optimize the function based on profiling  
B. Increase Lambda memory  
C. Enable S3 triggers  
D. Adjust CodeDeploy hooks  
**Answer**: A  
**Explanation**: Profiling guides CPU optimization.

### Question 15
**Scenario**: Pipeline artifacts aren’t reaching the deploy stage from CodeBuild.  
**Question**: What should be verified?  
A. CodeBuild output artifact settings  
B. GitHub credentials  
C. IAM role scope  
D. S3 encryption policy  
**Answer**: A  
**Explanation**: Output settings ensure artifact transfer.

### Question 16
**Scenario**: A small team needs a simple CI/CD setup for a Django app.  
**Question**: Which service should they use?  
A. AWS CodeStar  
B. AWS CodePipeline  
C. AWS CodeArtifact  
D. AWS CodeGuru  
**Answer**: A  
**Explanation**: CodeStar simplifies CI/CD for small teams.

### Question 17
**Scenario**: CodeArtifact needs to proxy a private npm registry for a team.  
**Question**: What should be configured?  
A. Upstream repository in CodeArtifact  
B. S3 bucket lifecycle policy  
C. CloudTrail logging  
D. Lambda trigger  
**Answer**: A  
**Explanation**: Upstream repos proxy private registries.

---

## Domain 2: Configuration Management and IaC (17%) - 13 Questions

### Question 18
**Scenario**: A CloudFormation stack fails to deploy an RDS instance due to a missing parameter value during a multi-account rollout.  
**Question**: What should a DevOps engineer review?  
A. Stack parameters section  
B. S3 bucket permissions  
C. CodeDeploy logs  
D. CloudWatch metrics  
**Answer**: A  
**Explanation**: Missing parameters cause deployment failures.

### Question 19
**Scenario**: A team needs to define environment-specific AMIs in CloudFormation.  
**Question**: Which component should be used?  
A. Mappings  
B. Parameters  
C. Outputs  
D. Conditions  
**Answer**: A  
**Explanation**: Mappings define static, environment-specific values.

### Question 20
**Scenario**: A CloudFormation stack needs an EC2 instance’s private IP.  
**Question**: Which function retrieves this?  
A. Fn::GetAtt  
B. Fn::Ref  
C. Fn::Join  
D. Fn::Sub  
**Answer**: A  
**Explanation**: `GetAtt` retrieves instance attributes like PrivateIp.

### Question 21
**Scenario**: A company uses AWS CloudFormation to provision a VPC, an Amazon RDS instance, and an EC2 Auto Scaling group across multiple accounts in an AWS Organizations structure. During a recent deployment, a stack in a new account failed because the RDS instance couldn’t be created due to a missing subnet group, which wasn’t exported from the VPC stack. The company wants to ensure future deployments automatically share subnet details across stacks and accounts with minimal overhead.  
**Question**: What should a DevOps engineer do to resolve this issue and prevent recurrence?  
A. Update the VPC stack to export subnet IDs using Outputs, and use Fn::ImportValue in the RDS stack to reference them.  
B. Create a StackSet in the management account to deploy the VPC and RDS stacks together with a single template.  
C. Use AWS Service Catalog to bundle the VPC and RDS templates as a product, enforcing subnet group creation.  
D. Modify the RDS stack to dynamically query subnet IDs using a Lambda-backed custom resource.  
**Answer**: A  
**Explanation**: Exporting subnet IDs with Outputs and importing via `Fn::ImportValue` ensures cross-stack sharing with minimal overhead. B adds complexity, C is overkill, and D is unnecessarily complex.

### Question 22
**Scenario**: A Beanstalk deployment update causes app downtime due to instance replacement.  
**Question**: Which mode prevents this?  
A. Blue/Green  
B. All at Once  
C. Rolling  
D. Immutable  
**Answer**: A  
**Explanation**: Blue/Green uses a separate environment, avoiding downtime.

### Question 23
**Scenario**: A team needs to configure a custom log path for a Beanstalk app.  
**Question**: Where should this be defined?  
A. .ebextensions  
B. buildspec.yml  
C. appspec.yml  
D. CloudFormation parameters  
**Answer**: A  
**Explanation**: `.ebextensions` customizes log paths.

### Question 24
**Scenario**: A CloudFormation stack fails to delete, leaving an ELB behind.  
**Question**: What should be added?  
A. DeletionPolicy: Delete  
B. S3 bucket versioning  
C. CodeDeploy hooks  
D. GitHub webhook  
**Answer**: A  
**Explanation**: `DeletionPolicy: Delete` ensures ELB cleanup.

### Question 25
**Scenario**: A Beanstalk update needs to maintain capacity without downtime.  
**Question**: Which mode should be used?  
A. Immutable  
B. Rolling  
C. All at Once  
D. Blue/Green  
**Answer**: A  
**Explanation**: Immutable adds new instances first, maintaining capacity.

### Question 26
**Scenario**: A stack needs to output a VPC CIDR block for another stack.  
**Question**: What should be used?  
A. Outputs  
B. Parameters  
C. Conditions  
D. Mappings  
**Answer**: A  
**Explanation**: Outputs share values between stacks.

### Question 27
**Scenario**: A Beanstalk app requires a custom timeout for HTTP requests.  
**Question**: Where should this be configured?  
A. Environment options  
B. S3 bucket policy  
C. CodeDeploy appspec.yml  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Environment options set timeouts.

### Question 28
**Scenario**: A stack needs to combine a prefix with an instance ID.  
**Question**: Which function should be used?  
A. Fn::Join  
B. Fn::GetAtt  
C. Fn::Ref  
D. Fn::ImportValue  
**Answer**: A  
**Explanation**: `Fn::Join` combines strings.

### Question 29
**Scenario**: A team needs to deploy IaC to new Control Tower accounts automatically.  
**Question**: What’s the best approach?  
A. Customizations for Control Tower (CfCT)  
B. CodePipeline  
C. Elastic Beanstalk  
D. Nested Stacks  
**Answer**: A  
**Explanation**: CfCT automates IaC in Control Tower.

### Question 30
**Scenario**: A Beanstalk app needs a custom health check path.  
**Question**: Where should this be set?  
A. Environment configuration  
B. S3 event trigger  
C. CodeDeploy hooks  
D. CloudFormation conditions  
**Answer**: A  
**Explanation**: Config sets health check paths.

---

## Domain 3: Resilient Cloud Solutions (15%) - 11 Questions

### Question 31
**Scenario**: An app on EC2 with RDS experiences downtime during AZ failures due to manual failover delays.  
**Question**: What should be configured?  
A. Multi-AZ RDS with Auto Scaling EC2  
B. Single-AZ RDS with Route 53 latency routing  
C. Aurora global database with ELB  
D. S3 CRR for data redundancy  
**Answer**: A  
**Explanation**: Multi-AZ RDS auto-fails over, and Auto Scaling ensures EC2 HA.

### Question 32
**Scenario**: A company runs a web application on EC2 instances behind an ALB, with data stored in an Amazon Aurora MySQL cluster with a single writer instance. During a recent AZ failure, the application was unavailable for 15 minutes until manual failover was performed. The company needs to minimize downtime during future AZ failures and ensure session data persists across regions for disaster recovery, with automatic failover within 5 minutes.  
**Question**: Which solution meets these requirements?  
A. Enable Multi-AZ on the Aurora cluster and use DynamoDB global tables for session data with Route 53 failover routing.  
B. Add a read replica in another AZ and configure Route 53 latency-based routing with health checks to the ALB.  
C. Create an Aurora global database and use Elastic Beanstalk with session stickiness across regions.  
D. Use EC2 Auto Scaling with Multi-AZ and store session data in S3 with cross-region replication.  
**Answer**: A  
**Explanation**: Multi-AZ Aurora auto-fails within 5 minutes, DynamoDB global tables replicate session data, and Route 53 failover ensures DR. B lacks write failover, C is for cross-region (not AZ), and D misuses S3 for sessions.

### Question 33
**Scenario**: DR requires low RPO and moderate cost for an ECS app.  
**Question**: Which strategy should be used?  
A. Warm Standby  
B. Multi-Site  
C. Pilot Light  
D. Backup and Restore  
**Answer**: A  
**Explanation**: Warm Standby offers low RPO at moderate cost.

### Question 34
**Scenario**: A Lambda function experiences 8-second cold starts during peak traffic.  
**Question**: What should be adjusted?  
A. Provisioned concurrency  
B. S3 bucket size  
C. CodePipeline stages  
D. Timeout  
**Answer**: A  
**Explanation**: Provisioned concurrency reduces cold starts.

### Question 35
**Scenario**: An ECS app needs HA across AZs with minimal latency.  
**Question**: What should be configured?  
A. Fargate with ALB across AZs  
B. EC2 with rolling updates  
C. Lambda with S3 triggers  
D. CloudFormation outputs  
**Answer**: A  
**Explanation**: Fargate with ALB ensures HA and low latency.

### Question 36
**Scenario**: S3 CRR fails to replicate tags.  
**Question**: What should be enabled?  
A. Tag replication in CRR rules  
B. Multi-AZ  
C. CloudWatch alarms  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: Tag replication must be explicitly enabled in CRR.

### Question 37
**Scenario**: Route 53 failover doesn’t switch during an outage.  
**Question**: What should be verified?  
A. Health check configuration  
B. S3 bucket policy  
C. IAM permissions  
D. CloudTrail logs  
**Answer**: A  
**Explanation**: Health checks trigger failover.

### Question 38
**Scenario**: DR needs fast recovery and high cost tolerance for an API.  
**Question**: Which approach?  
A. Multi-Site  
B. Warm Standby  
C. Pilot Light  
D. Backup and Restore  
**Answer**: A  
**Explanation**: Multi-Site ensures fast recovery.

### Question 39
**Scenario**: Lambda throttles during a traffic surge.  
**Question**: What should be increased?  
A. Reserved concurrency  
B. S3 CRR  
C. CodeDeploy timeout  
D. CloudWatch metrics  
**Answer**: A  
**Explanation**: Reserved concurrency prevents throttling.

### Question 40
**Scenario**: ElastiCache loses data during a failover.  
**Question**: What should be enabled?  
A. Redis persistence (AOF)  
B. S3 event triggers  
C. Lambda concurrency  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: AOF ensures data persistence.

### Question 41
**Scenario**: ECS startup delays impact SLAs due to data downloads.  
**Question**: What should be implemented?  
A. Warm pool with lifecycle hooks  
B. S3 bucket lifecycle  
C. Lambda timeout  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: Warm pools pre-download data, reducing delays.

---

## Domain 4: Monitoring and Logging (15%) - 11 Questions

### Question 42
**Scenario**: A team needs to monitor ECS task CPU usage across a cluster.  
**Question**: What should be done?  
A. Log CPU metrics to CloudWatch Logs  
B. Enable S3 event logging  
C. Configure CodeDeploy  
D. Adjust RDS Multi-AZ  
**Answer**: A  
**Explanation**: Logs push CPU metrics to CloudWatch.

### Question 43
**Scenario**: CloudWatch Logs don’t capture Lambda request IDs.  
**Question**: What should be fixed?  
A. Lambda execution role permissions  
B. S3 bucket versioning  
C. CodePipeline failure  
D. Lambda timeout  
**Answer**: A  
**Explanation**: Role permissions enable logging.

### Question 44
**Scenario**: A company’s API runs on API Gateway with Lambda backends, serving thousands of requests daily. After a recent update, customers reported intermittent errors, but the team lacks visibility into request-specific metrics like latency and error codes per endpoint. The Lambda functions log request details to CloudWatch Logs. The company needs to track these metrics per endpoint and alert on error spikes within 5 minutes.  
**Question**: What should a DevOps engineer do to meet these requirements?  
A. Enable X-Ray tracing on API Gateway and Lambda, create custom metrics from traces, and set CloudWatch alarms.  
B. Configure a CloudWatch Logs metric filter to extract endpoint, latency, and error codes, with dimensions, and set an alarm.  
C. Use API Gateway access logs to S3, query with Athena, and trigger Lambda notifications on error thresholds.  
D. Enable CloudWatch Logs Insights to query logs hourly and send SNS notifications on error counts.  
**Answer**: B  
**Explanation**: Metric filters extract endpoint metrics with dimensions, enabling 5-minute alarms. A is trace-focused, C isn’t real-time, and D lacks continuous tracking.

### Question 45
**Scenario**: A team needs to analyze VPC Flow Logs for security incidents.  
**Question**: Which tool should be used?  
A. Amazon Athena  
B. CloudWatch Logs Insights  
C. AWS CodeGuru  
D. EventBridge  
**Answer**: A  
**Explanation**: Athena queries Flow Logs in S3.

### Question 46
**Scenario**: A nightly ETL job fails to trigger.  
**Question**: What should be scheduled?  
A. EventBridge rule  
B. CloudWatch alarm  
C. S3 event notification  
D. CodePipeline stage  
**Answer**: A  
**Explanation**: EventBridge schedules nightly tasks.

### Question 47
**Scenario**: A team needs real-time alerts on API errors.  
**Question**: What should be configured?  
A. CloudWatch Logs subscription  
B. S3 export task  
C. CodeDeploy hooks  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Subscriptions provide real-time alerts.

### Question 48
**Scenario**: A team needs alerts on high memory usage in ECS tasks.  
**Question**: What should be set up?  
A. CloudWatch alarm with custom metric  
B. Athena query on S3  
C. EventBridge with SQS  
D. CodeDeploy rollback  
**Answer**: A  
**Explanation**: Alarms monitor custom memory metrics.

### Question 49
**Scenario**: Athena queries are slow for ECS logs.  
**Question**: What should be done?  
A. Convert logs to ORC format  
B. Increase Lambda memory  
C. Enable CloudWatch metrics  
D. Adjust CodePipeline  
**Answer**: A  
**Explanation**: ORC improves query performance.

### Question 50
**Scenario**: An EventBridge rule fails to trigger across accounts.  
**Question**: What should be verified?  
A. Event bus resource policy  
B. S3 bucket policy  
C. IAM user permissions  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Resource policies enable cross-account triggers.

### Question 51
**Scenario**: A team needs 10-second resolution for API latency metrics.  
**Question**: What should be enabled?  
A. High-resolution metrics  
B. Standard metrics  
C. S3 event triggers  
D. CodeDeploy settings  
**Answer**: A  
**Explanation**: High-resolution supports 10-second intervals.

### Question 52
**Scenario**: CloudWatch Logs Insights shows outdated data.  
**Question**: What should be checked?  
A. Log group ingestion lag  
B. S3 export delay  
C. IAM role permissions  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: Ingestion lag affects data freshness.

---

## Domain 5: Incident and Event Response (14%) - 11 Questions

### Question 53
**Scenario**: S3 uploads don’t trigger a Lambda function for processing.  
**Question**: What should be configured?  
A. S3 event notification  
B. CloudWatch alarm  
C. CodePipeline stage  
D. RDS failover  
**Answer**: A  
**Explanation**: Event notifications trigger Lambda.

### Question 54
**Scenario**: GuardDuty detects an unauthorized EC2 login attempt.  
**Question**: What should be automated?  
A. EventBridge rule with SSM remediation  
B. Increase Lambda memory  
C. Enable S3 CRR  
D. Adjust CloudFormation  
**Answer**: A  
**Explanation**: EventBridge with SSM automates responses.

### Question 55
**Scenario**: A company uses an S3 bucket to store critical logs, processed by a Lambda function triggered by S3 events. Recently, some log files caused processing errors, leaving them unprocessed in the bucket. The team needs to retain failed logs for review, automatically retry processing after fixes, and notify engineers within 10 minutes of failures.  
**Question**: Which solution meets these requirements?  
A. Configure a dead-letter queue (DLQ) on the Lambda function, set a redrive policy with SQS, and use SNS for notifications.  
B. Use EventBridge to detect Lambda failures, move failed logs to another bucket, and trigger SNS notifications.  
C. Add a CloudWatch Logs subscription to filter errors, invoke a Lambda to copy logs to S3, and notify via SNS.  
D. Enable S3 versioning and configure a Lambda retry policy with SNS notifications on max retries.  
**Answer**: A  
**Explanation**: A DLQ retains failed events, redrive retries after fixes, and SNS notifies within 10 minutes. B lacks retry, C misses event retention, and D misuses versioning.

### Question 56
**Scenario**: A team needs S3 events for .log files only.  
**Question**: What should be applied?  
A. Event suffix filter  
B. CloudWatch Logs filter  
C. CodeDeploy hooks  
D. S3 bucket policy  
**Answer**: A  
**Explanation**: Suffix filters target .log files.

### Question 57
**Scenario**: GuardDuty findings need to be centralized across 20 accounts.  
**Question**: What should be enabled?  
A. AWS Organizations  
B. S3 bucket versioning  
C. Lambda concurrency  
D. CloudFormation StackSets  
**Answer**: A  
**Explanation**: Organizations centralize GuardDuty.

### Question 58
**Scenario**: CloudTrail misses Lambda execution logs.  
**Question**: What should be activated?  
A. Data events  
B. Management events  
C. Insights events  
D. Multi-region setup  
**Answer**: A  
**Explanation**: Data events log Lambda executions.

### Question 59
**Scenario**: A team needs alerts on EC2 instance restarts.  
**Question**: What should be used?  
A. EventBridge with SNS  
B. CloudWatch alarm  
C. CodeDeploy rollback  
D. RDS read replica  
**Answer**: A  
**Explanation**: EventBridge with SNS alerts on restarts.

### Question 60
**Scenario**: GuardDuty misses RDS anomalies.  
**Question**: What should be enabled?  
A. RDS Protection  
B. S3 CRR  
C. Lambda aliases  
D. CloudFormation conditions  
**Answer**: A  
**Explanation**: RDS Protection enhances detection.

### Question 61
**Scenario**: A KMS key rotation needs auditing.  
**Question**: Where should a DevOps engineer look?  
A. CloudTrail logs  
B. CloudWatch metrics  
C. S3 event logs  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: CloudTrail logs KMS actions.

### Question 62
**Scenario**: S3 events need to trigger Lambda and SNS simultaneously.  
**Question**: What should be used?  
A. EventBridge  
B. CloudWatch Logs subscription  
C. CodeDeploy hooks  
D. Lambda concurrency  
**Answer**: A  
**Explanation**: EventBridge supports multiple targets.

### Question 63
**Scenario**: CloudTrail logs are missing regional events.  
**Question**: What should be ensured?  
A. Multi-region trail  
B. S3 bucket encryption  
C. Lambda timeout  
D. RDS Multi-AZ  
**Answer**: A  
**Explanation**: Multi-region trails capture all events.

---

## Domain 6: Security and Compliance (17%) - 12 Questions

### Question 64
**Scenario**: AWS Config detects untagged EC2 instances.  
**Question**: What should be implemented?  
A. Managed rule with SSM remediation  
B. Lambda concurrency  
C. S3 CRR  
D. CodePipeline stages  
**Answer**: A  
**Explanation**: Managed rules with SSM enforce tagging.

### Question 65
**Scenario**: A Config rule needs to check S3 bucket encryption levels.  
**Question**: What should be used?  
A. Lambda-backed custom rule  
B. S3 event trigger  
C. CloudWatch alarm  
D. CodeDeploy rollback  
**Answer**: A  
**Explanation**: Lambda provides custom encryption checks.

### Question 66
**Scenario**: A company needs compliance visibility across 10 accounts.  
**Question**: What should be deployed?  
A. Config Aggregators  
B. StackSets  
C. S3 bucket policy  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Aggregators provide multi-account visibility.

### Question 67
**Scenario**: WAF fails to block XSS attacks on an API Gateway endpoint.  
**Question**: What should be configured?  
A. XSS match rule  
B. S3 bucket policy  
C. CloudTrail logs  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: XSS rules block cross-site scripting.

### Question 68
**Scenario**: Firewall Manager doesn’t apply to new ALBs in an organization.  
**Question**: What’s required?  
A. AWS Organizations integration  
B. S3 bucket versioning  
C. CloudWatch metrics  
D. Lambda trigger  
**Answer**: A  
**Explanation**: Organizations enforce ALB policies.

### Question 69
**Scenario**: IAM Identity Center users can’t access a SAML-integrated app.  
**Question**: What should be verified?  
A. SAML attribute mappings  
B. S3 event triggers  
C. CodePipeline artifacts  
D. RDS failover settings  
**Answer**: A  
**Explanation**: Mappings enable app access.

### Question 70
**Scenario**: A company shares encrypted AMIs across accounts using AWS KMS keys in a source account. A recent audit found that target accounts couldn’t launch instances from the AMIs because the Auto Scaling group lacked KMS permissions. The company needs to automate AMI sharing and ensure target accounts can decrypt and launch instances without manual key management.  
**Question**: Which steps should a DevOps engineer take? (Choose three.)  
A. Copy the AMI in the source account with the KMS key and share the encrypted AMI with the target account.  
B. Update the KMS key policy in the source account to allow the target account’s Auto Scaling service-linked role to decrypt.  
C. Create a KMS grant in the source account for the target account’s Auto Scaling role to use the key.  
D. Share the unencrypted AMI with the target account and enable default EBS encryption in the target account.  
E. Create a new KMS key in the target account and re-encrypt the AMI using Lambda before launch.  
F. Modify the Auto Scaling launch template to include an IAM role with KMS decrypt permissions.  
**Answers**: A, C, F  
**Explanation**: A encrypts and shares the AMI, C grants automated decryption, and F ensures instances can decrypt. B is manual, D violates encryption, and E adds complexity.

### Question 71
**Scenario**: WAF allows bot traffic to an ALB.  
**Question**: What should be enabled?  
A. Bot Control rule  
B. S3 bucket policy  
C. CloudTrail logs  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: Bot Control blocks bot traffic.

### Question 72
**Scenario**: SSO with Okta fails after a config update.  
**Question**: What should be integrated?  
A. IAM Identity Center  
B. AWS Config  
C. CodePipeline  
D. CloudWatch alarms  
**Answer**: A  
**Explanation**: IAM Identity Center integrates Okta.

### Question 73
**Scenario**: Firewall Manager needs to secure new API Gateway endpoints.  
**Question**: What should be created?  
A. WAF policy  
B. S3 event trigger  
C. Lambda concurrency  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: WAF policies secure API Gateway.

### Question 74
**Scenario**: Config rules vary across accounts.  
**Question**: What should be used to standardize?  
A. Conformance packs  
B. S3 event triggers  
C. CloudTrail insights  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Conformance packs standardize rules.

### Question 75
**Scenario**: IAM Identity Center needs department-based access.  
**Question**: What should be configured?  
A. ABAC with department tags  
B. S3 bucket policies  
C. CodePipeline stages  
D. RDS Multi-AZ  
**Answer**: A  
**Explanation**: ABAC uses tags for department access.

---


# AWS Certified DevOps Engineer – Professional (DOP-C02) Practice Questions (Set 8)

This set includes 75 scenario-based questions distributed across the six DOP-C02 domains per their official weightings. Questions reflect complex DevOps challenges with detailed explanations.

---

## Domain 1: SDLC Automation (22%) - 17 Questions

### Question 1
**Scenario**: A company deploys a Go app to Amazon EKS via CodePipeline, with a CodeBuild stage for compiling and a CodeDeploy stage for Kubernetes manifests. Recently, a deployment introduced a memory leak, undetected until production, costing downtime. The team wants automated memory tests before deployment, with results posted to Slack for review.  
**Question**: What should a DevOps engineer implement?  
A. Add a CodeBuild action to run memory tests and post results to Slack via a webhook.  
B. Configure a Lambda function to trigger tests and notify Slack after deployment.  
C. Update CodeDeploy with a hook to run tests and log results to CloudWatch.  
D. Use CodeStar to integrate Slack and run tests in a new stage.  
**Answer**: A  
**Explanation**: A CodeBuild action pre-deployment runs tests and notifies Slack, preventing issues proactively. B is post-deployment, C lacks Slack integration, and D adds unnecessary complexity.

### Question 2
**Scenario**: A CodeBuild job fails due to a missing Go module from a private repository.  
**Question**: What should a DevOps engineer verify?  
A. buildspec.yml `install` phase for repo auth  
B. CodePipeline IAM role  
C. S3 artifact encryption  
D. CloudWatch Logs retention  
**Answer**: A  
**Explanation**: The `install` phase handles module retrieval; auth issues are likely.

### Question 3 (Multiple-Response)
**Scenario**: A team deploys a Python app to Lambda with CodePipeline and CodeDeploy. They need a linear deployment shifting 20% traffic every 10 minutes.  
**Question**: Which TWO steps are required?  
A. Configure CodeDeploy with Linear20Percent10Minutes  
B. Set an ALB with dynamic routing  
C. Add a validation hook in appspec.yml  
D. Enable rolling updates in CodePipeline  
**Answers**: A, C  
**Explanation**: A sets the linear shift, and C validates deployment health. B is irrelevant (Lambda uses aliases), and D applies to ECS/EC2.

### Question 4
**Scenario**: A team needs to set different timeout values for an app during CodeDeploy based on deployment group (test, prod).  
**Question**: What should be used?  
A. DEPLOYMENT_GROUP_NAME in a script  
B. CloudFormation parameters  
C. S3 metadata  
D. CodePipeline variables  
**Answer**: A  
**Explanation**: `DEPLOYMENT_GROUP_NAME` dynamically adjusts timeouts.

### Question 5
**Scenario**: A company uses CodeCommit for a Python app, with CodePipeline deploying to EC2 via CodeDeploy. Developers frequently merge pull requests without running security scans, leading to vulnerabilities in production. The company wants automated scans on every pull request, visible to reviewers, with failed scans blocking merges.  
**Question**: What should a DevOps engineer implement?  
A. Create an EventBridge rule on `pullRequestCreated`, trigger a CodeBuild scan, and post results as a comment via Lambda.  
B. Add a CodeBuild stage in CodePipeline to scan code and fail the pipeline if vulnerabilities are found.  
C. Use CodeGuru Reviewer on CodeCommit and configure an approval rule to block merges on scan failures.  
D. Set a CodeCommit approval rule with a Lambda function to invoke scans and reject merges on failures.  
**Answer**: A  
**Explanation**: A uses EventBridge to trigger scans pre-merge, posts results via Lambda, and allows manual blocking, meeting all needs. B is post-merge, C lacks blocking, and D doesn’t post results.

### Question 6
**Scenario**: A pipeline moves from GitLab to Bitbucket for an ECS app.  
**Question**: What must be updated?  
A. Source action in CodePipeline  
B. CodeBuild runtime  
C. S3 artifact policy  
D. CloudTrail rules  
**Answer**: A  
**Explanation**: Source action updates to Bitbucket.

### Question 7
**Scenario**: A team uses CodeArtifact for Node.js dependencies, but a package is missing.  
**Question**: What should be configured?  
A. Upstream npm registry  
B. CodeStar project  
C. CodeGuru profiling  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: Upstream npm ensures package availability.

### Question 8
**Scenario**: CodeGuru Reviewer flags a race condition in a Go app.  
**Question**: What should a DevOps engineer do?  
A. Refactor based on suggestions  
B. Increase CodePipeline timeout  
C. Enable S3 versioning  
D. Adjust buildspec.yml  
**Answer**: A  
**Explanation**: Refactoring fixes the race condition.

### Question 9
**Scenario**: A cross-account pipeline fails to deploy to a target account.  
**Question**: What’s the likely issue?  
A. Missing cross-account IAM roles  
B. CodeDeploy config  
C. CloudWatch Logs  
D. GitHub webhook  
**Answer**: A  
**Explanation**: Cross-account roles are required.

### Question 10
**Scenario**: A build needs a custom Node.js version.  
**Question**: Where should this be specified?  
A. CodeBuild environment  
B. CodePipeline source  
C. appspec.yml  
D. S3 bucket  
**Answer**: A  
**Explanation**: Environment settings define Node.js versions.

### Question 11
**Scenario**: An EKS app needs post-deployment validation with CodeDeploy.  
**Question**: What should be used?  
A. AfterAllowTraffic hook  
B. CodePipeline approval  
C. CodeStar notifications  
D. CloudFormation outputs  
**Answer**: A  
**Explanation**: The hook validates post-deployment.

### Question 12
**Scenario**: A CodeBuild job can’t access a private S3 bucket.  
**Question**: What should be configured?  
A. IAM role with S3 access  
B. S3 bucket ACL  
C. VPC endpoint  
D. CloudWatch filter  
**Answer**: A  
**Explanation**: IAM role grants S3 access.

### Question 13
**Scenario**: A team needs a quick deployment for a non-critical update.  
**Question**: Which mode?  
A. All at Once  
B. Rolling  
C. Blue/Green  
D. Immutable  
**Answer**: A  
**Explanation**: All at Once is fastest for non-critical.

### Question 14
**Scenario**: CodeGuru Profiler flags latency in a Python Lambda.  
**Question**: What should be done?  
A. Optimize based on profiling  
B. Increase Lambda timeout  
C. Enable S3 triggers  
D. Adjust CodeDeploy hooks  
**Answer**: A  
**Explanation**: Profiling guides latency fixes.

### Question 15
**Scenario**: Pipeline artifacts fail to deploy from CodeBuild.  
**Question**: What should be checked?  
A. CodeBuild artifact settings  
B. GitHub credentials  
C. IAM role limits  
D. S3 encryption  
**Answer**: A  
**Explanation**: Artifact settings ensure deployment.

### Question 16
**Scenario**: A startup needs a quick CI/CD setup for a Rails app.  
**Question**: Which service?  
A. AWS CodeStar  
B. AWS CodePipeline  
C. AWS CodeArtifact  
D. AWS CodeGuru  
**Answer**: A  
**Explanation**: CodeStar simplifies CI/CD.

### Question 17
**Scenario**: CodeArtifact needs to proxy a private PyPI repo.  
**Question**: What should be set?  
A. Upstream repository  
B. S3 lifecycle policy  
C. CloudTrail logs  
D. Lambda trigger  
**Answer**: A  
**Explanation**: Upstream proxies private PyPI.

---

## Domain 2: Configuration Management and IaC (17%) - 13 Questions

### Question 18
**Scenario**: A CloudFormation stack fails to update due to a resource conflict.  
**Question**: What should be reviewed?  
A. Stack change set  
B. S3 bucket permissions  
C. CodeDeploy logs  
D. CloudWatch metrics  
**Answer**: A  
**Explanation**: Change sets identify conflicts.

### Question 19
**Scenario**: A stack needs to conditionally deploy based on region.  
**Question**: Which component?  
A. Conditions  
B. Parameters  
C. Outputs  
D. Mappings  
**Answer**: A  
**Explanation**: Conditions control regional deployment.

### Question 20
**Scenario**: A stack needs an RDS endpoint.  
**Question**: Which function?  
A. Fn::GetAtt  
B. Fn::Ref  
C. Fn::Join  
D. Fn::Sub  
**Answer**: A  
**Explanation**: `GetAtt` retrieves endpoints.

### Question 21
**Scenario**: StackSets fail to deploy to a new region due to permission issues.  
**Question**: What should be ensured?  
A. Regional IAM permissions  
B. S3 bucket replication  
C. CodePipeline triggers  
D. CloudWatch alarms  
**Answer**: A  
**Explanation**: Regional permissions are required.

### Question 22
**Scenario**: A Beanstalk update causes outage during instance swaps.  
**Question**: Which mode prevents this?  
A. Blue/Green  
B. All at Once  
C. Rolling  
D. Immutable  
**Answer**: A  
**Explanation**: Blue/Green avoids outages.

### Question 23
**Scenario**: A Beanstalk app needs a custom nginx config.  
**Question**: Where should this be defined?  
A. .ebextensions  
B. buildspec.yml  
C. appspec.yml  
D. CloudFormation parameters  
**Answer**: A  
**Explanation**: `.ebextensions` customizes nginx.

### Question 24
**Scenario**: A CloudFormation stack leaves an S3 bucket after deletion.  
**Question**: What should be added?  
A. DeletionPolicy: Delete  
B. S3 bucket versioning  
C. CodeDeploy hooks  
D. GitHub webhook  
**Answer**: A  
**Explanation**: `DeletionPolicy` ensures cleanup.

### Question 25
**Scenario**: A Beanstalk update needs zero downtime and capacity.  
**Question**: Which mode?  
A. Immutable  
B. Rolling  
C. All at Once  
D. Blue/Green  
**Answer**: A  
**Explanation**: Immutable ensures capacity and no downtime.

### Question 26
**Scenario**: A stack needs to share an ELB ARN.  
**Question**: What should be used?  
A. Outputs  
B. Parameters  
C. Conditions  
D. Mappings  
**Answer**: A  
**Explanation**: Outputs share ARNs.

### Question 27
**Scenario**: A Beanstalk app needs a custom env variable.  
**Question**: Where should it be set?  
A. Environment options  
B. S3 bucket policy  
C. CodeDeploy appspec.yml  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Options set variables.

### Question 28
**Scenario**: A stack needs to import a subnet ID.  
**Question**: Which function?  
A. Fn::ImportValue  
B. Fn::GetAtt  
C. Fn::Ref  
D. Fn::Join  
**Answer**: A  
**Explanation**: `Fn::ImportValue` imports values.

### Question 29
**Scenario**: A team needs IaC across multiple OUs in Organizations.  
**Question**: What’s best?  
A. StackSets  
B. CodePipeline  
C. Elastic Beanstalk  
D. Nested Stacks  
**Answer**: A  
**Explanation**: StackSets deploy across OUs.

### Question 30
**Scenario**: A Beanstalk app needs IPv6 client support.  
**Question**: What should be done?  
A. Enable dualstack on ALB  
B. S3 event trigger  
C. CodeDeploy hooks  
D. CloudFormation conditions  
**Answer**: A  
**Explanation**: Dualstack supports IPv6.

---

## Domain 3: Resilient Cloud Solutions (15%) - 11 Questions

### Question 31
**Scenario**: An app on ECS with Aurora fails during AZ outages.  
**Question**: What should be configured?  
A. Multi-AZ Aurora with ECS ASG  
B. Single-AZ Aurora with Route 53  
C. DynamoDB with ELB  
D. S3 CRR  
**Answer**: A  
**Explanation**: Multi-AZ Aurora and ASG ensure HA.

### Question 32
**Scenario**: A company runs a serverless API with API Gateway, Lambda, and DynamoDB. Lambda functions experience cold-start delays of 5-7 seconds during traffic spikes, impacting customer experience. The API handles 100 requests per minute normally, spiking to 1,000 during peak hours. The company needs to reduce latency to under 2 seconds at all times with minimal cost overhead.  
**Question**: Which solution meets these requirements?  
A. Configure provisioned concurrency on Lambda with a fixed value of 10 and enable DynamoDB DAX.  
B. Set reserved concurrency on Lambda to 1,000 and scale API Gateway throttling to match.  
C. Use Application Auto Scaling with provisioned concurrency, setting a min of 5 and max of 200, based on CloudWatch metrics.  
D. Deploy Lambda@Edge with API Gateway and use DynamoDB global tables for lower latency.  
**Answer**: C  
**Explanation**: Auto-scaling provisioned concurrency (5-200) reduces latency cost-effectively. A is too static, B limits execution, and D is overkill.

### Question 33
**Scenario**: DR needs low RTO and moderate cost for an EC2 app.  
**Question**: Which strategy?  
A. Warm Standby  
B. Multi-Site  
C. Pilot Light  
D. Backup and Restore  
**Answer**: A  
**Explanation**: Warm Standby balances RTO and cost.

### Question 34
**Scenario**: Lambda fails under sudden load spikes.  
**Question**: What should be adjusted?  
A. Provisioned concurrency  
B. S3 bucket size  
C. CodePipeline stages  
D. Timeout  
**Answer**: A  
**Explanation**: Provisioned concurrency handles spikes.

### Question 35
**Scenario**: An EKS app needs HA across AZs.  
**Question**: What should be configured?  
A. Fargate with ALB across AZs  
B. EC2 with rolling  
C. Lambda with S3  
D. CloudFormation outputs  
**Answer**: A  
**Explanation**: Fargate with ALB ensures HA.

### Question 36
**Scenario**: S3 CRR fails for existing objects.  
**Question**: What should be used?  
A. Batch Operations  
B. Multi-AZ  
C. CloudWatch alarms  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: Batch Operations replicate existing objects.

### Question 37
**Scenario**: Route 53 doesn’t route to a backup region.  
**Question**: What should be checked?  
A. Health check settings  
B. S3 bucket policy  
C. IAM permissions  
D. CloudTrail logs  
**Answer**: A  
**Explanation**: Health checks drive routing.

### Question 38
**Scenario**: DR needs minimal cost and moderate RPO.  
**Question**: Which approach?  
A. Pilot Light  
B. Warm Standby  
C. Multi-Site  
D. Backup and Restore  
**Answer**: A  
**Explanation**: Pilot Light minimizes cost with moderate RPO.

### Question 39
**Scenario**: Lambda cold starts delay an API response.  
**Question**: What should be used?  
A. Provisioned concurrency  
B. S3 CRR  
C. CodeDeploy timeout  
D. CloudWatch metrics  
**Answer**: A  
**Explanation**: Provisioned concurrency reduces delays.

### Question 40
**Scenario**: ElastiCache fails during an AZ outage.  
**Question**: What should be enabled?  
A. Multi-AZ replication  
B. S3 event triggers  
C. Lambda concurrency  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Multi-AZ ensures failover.

### Question 41
**Scenario**: EKS startup delays increase due to config downloads.  
**Question**: What should be implemented?  
A. Warm pool with hooks  
B. S3 bucket lifecycle  
C. Lambda timeout  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: Warm pools pre-download configs.

---

## Domain 4: Monitoring and Logging (15%) - 11 Questions

### Question 42
**Scenario**: A team needs to track Lambda invocation counts.  
**Question**: What should be done?  
A. Log counts to CloudWatch Logs  
B. Enable S3 event logging  
C. Configure CodeDeploy  
D. Adjust RDS Multi-AZ  
**Answer**: A  
**Explanation**: Logs push invocation counts.

### Question 43
**Scenario**: CloudWatch Logs miss ECS container logs.  
**Question**: What should be fixed?  
A. Task role permissions  
B. S3 bucket versioning  
C. CodePipeline failure  
D. Lambda timeout  
**Answer**: A  
**Explanation**: Role permissions enable logging.

### Question 44
**Scenario**: A company’s ECS application logs to CloudWatch Logs, with tasks running across multiple AZs. After a recent outage, the team found that logs weren’t available for failed tasks because they weren’t flushed before termination. The company needs near-real-time log collection and analysis, with alerts on task failures within 2 minutes, and logs retained for 90 days.  
**Question**: Which combination of steps should a DevOps engineer take? (Choose two.)  
A. Update the ECS task definition to use the `awslogs` driver with a 90-day retention period.  
B. Configure a CloudWatch Logs subscription filter to stream logs to a Kinesis Data Firehose, delivering to S3.  
C. Set up a CloudWatch alarm on the ECS TaskStopped event with an SNS notification.  
D. Enable ECS task auto-recovery to restart failed tasks and log to CloudWatch Logs Insights.  
E. Use X-Ray to trace task failures and export logs to S3 with a lifecycle policy.  
**Answers**: B, C  
**Explanation**: B streams logs near-real-time to S3 with retention, and C alerts on failures within 2 minutes. A sets retention incorrectly, D doesn’t collect logs, and E is trace-focused.

### Question 45
**Scenario**: A team needs to query API Gateway logs.  
**Question**: Which tool?  
A. Amazon Athena  
B. CloudWatch Logs Insights  
C. AWS CodeGuru  
D. EventBridge  
**Answer**: A  
**Explanation**: Athena queries S3-stored logs.

### Question 46
**Scenario**: A monthly report job fails to run.  
**Question**: What should be scheduled?  
A. EventBridge rule  
B. CloudWatch alarm  
C. S3 event notification  
D. CodePipeline stage  
**Answer**: A  
**Explanation**: EventBridge schedules monthly tasks.

### Question 47
**Scenario**: A team needs real-time alerts on ECS failures.  
**Question**: What should be configured?  
A. CloudWatch Logs subscription  
B. S3 export task  
C. CodeDeploy hooks  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Subscriptions alert in real-time.

### Question 48
**Scenario**: A team needs alerts on high CPU in Lambda.  
**Question**: What should be set up?  
A. CloudWatch alarm with custom metric  
B. Athena query on S3  
C. EventBridge with SQS  
D. CodeDeploy rollback  
**Answer**: A  
**Explanation**: Alarms monitor CPU metrics.

### Question 49
**Scenario**: Athena queries lag for Lambda logs.  
**Question**: What should be done?  
A. Partition logs by timestamp  
B. Increase Lambda memory  
C. Enable CloudWatch metrics  
D. Adjust CodePipeline  
**Answer**: A  
**Explanation**: Partitioning speeds queries.

### Question 50
**Scenario**: An EventBridge rule fails cross-region.  
**Question**: What should be verified?  
A. Event bus policy  
B. S3 bucket policy  
C. IAM user roles  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: Policy enables cross-region rules.

### Question 51
**Scenario**: A team needs 5-second latency metrics.  
**Question**: What should be enabled?  
A. High-resolution metrics  
B. Standard metrics  
C. S3 event triggers  
D. CodeDeploy settings  
**Answer**: A  
**Explanation**: High-resolution supports 5 seconds.

### Question 52
**Scenario**: CloudWatch Logs Insights lacks error logs.  
**Question**: What should be checked?  
A. Log group filters  
B. S3 export delay  
C. IAM role permissions  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: Filters affect log visibility.

---

## Domain 5: Incident and Event Response (14%) - 11 Questions

### Question 53
**Scenario**: S3 puts don’t trigger an SNS topic.  
**Question**: What should be configured?  
A. S3 event notification  
B. CloudWatch alarm  
C. CodePipeline stage  
D. RDS failover  
**Answer**: A  
**Explanation**: Notifications trigger SNS.

### Question 54
**Scenario**: GuardDuty detects a malware scan on EC2.  
**Question**: What should be automated?  
A. EventBridge with Lambda isolation  
B. Increase Lambda memory  
C. Enable S3 CRR  
D. Adjust CloudFormation  
**Answer**: A  
**Explanation**: EventBridge with Lambda automates isolation.

### Question 55
**Scenario**: CloudTrail logs need 2-year retention.  
**Question**: What should be done?  
A. Export to S3 with lifecycle  
B. Enable Multi-AZ  
C. Set up Athena queries  
D. Increase Lambda timeout  
**Answer**: A  
**Explanation**: S3 lifecycle retains logs.

### Question 56
**Scenario**: A team needs S3 events for .csv files.  
**Question**: What should be applied?  
A. Event suffix filter  
B. CloudWatch Logs filter  
C. CodeDeploy hooks  
D. S3 bucket policy  
**Answer**: A  
**Explanation**: Suffix filters target .csv.

### Question 57
**Scenario**: GuardDuty needs visibility across 15 accounts.  
**Question**: What should be enabled?  
A. AWS Organizations  
B. S3 bucket versioning  
C. Lambda concurrency  
D. CloudFormation StackSets  
**Answer**: A  
**Explanation**: Organizations centralize visibility.

### Question 58
**Scenario**: CloudTrail misses API Gateway calls.  
**Question**: What should be activated?  
A. Data events  
B. Management events  
C. Insights events  
D. Multi-region setup  
**Answer**: A  
**Explanation**: Data events log API Gateway calls.

### Question 59
**Scenario**: A team needs alerts on S3 bucket deletes.  
**Question**: What should be used?  
A. EventBridge with SNS  
B. CloudWatch alarm  
C. CodeDeploy rollback  
D. RDS read replica  
**Answer**: A  
**Explanation**: EventBridge with SNS alerts on deletes.

### Question 60
**Scenario**: GuardDuty misses Lambda anomalies.  
**Question**: What should be enabled?  
A. Lambda Protection  
B. S3 CRR  
C. Lambda aliases  
D. CloudFormation conditions  
**Answer**: A  
**Explanation**: Lambda Protection enhances detection.

### Question 61
**Scenario**: An IAM role change needs tracking.  
**Question**: Where should a DevOps engineer look?  
A. CloudTrail logs  
B. CloudWatch metrics  
C. S3 event logs  
D. CodePipeline artifacts  
**Answer**: A  
**Explanation**: CloudTrail tracks IAM changes.

### Question 62
**Scenario**: S3 events need Lambda and SQS triggers.  
**Question**: What should be used?  
A. EventBridge  
B. CloudWatch Logs subscription  
C. CodeDeploy hooks  
D. Lambda concurrency  
**Answer**: A  
**Explanation**: EventBridge supports multiple triggers.

### Question 63
**Scenario**: CloudTrail logs miss us-east-2 events.  
**Question**: What should be ensured?  
A. All-regions trail  
B. S3 bucket encryption  
C. Lambda timeout  
D. RDS Multi-AZ  
**Answer**: A  
**Explanation**: All-regions trails capture all events.

---

## Domain 6: Security and Compliance (17%) - 12 Questions

### Question 64
**Scenario**: AWS Config flags public ELBs.  
**Question**: What should be implemented?  
A. Managed rule with SSM remediation  
B. Lambda concurrency  
C. S3 CRR  
D. CodePipeline stages  
**Answer**: A  
**Explanation**: Managed rules with SSM block public access.

### Question 65
**Scenario**: A Config rule needs to verify KMS key rotation.  
**Question**: What should be used?  
A. Lambda-backed rule  
B. S3 event trigger  
C. CloudWatch alarm  
D. CodeDeploy rollback  
**Answer**: A  
**Explanation**: Lambda verifies rotation.

### Question 66
**Scenario**: A company uses AWS Organizations with 50 accounts, centrally managing security via a delegated administrator account. A recent audit found some accounts had public S3 buckets, violating policy. The security team requires all new and existing buckets to block public access, with automatic remediation and notifications to the team if changes occur, without disrupting existing bucket operations.  
**Question**: Which solution meets these requirements?  
A. Enable AWS Config with the `s3-bucket-public-read-prohibited` rule, set an SSM remediation action, and use CloudTrail with EventBridge to notify via SNS.  
B. Deploy a CloudFormation StackSet to apply a bucket policy denying public access and configure GuardDuty to alert on public bucket findings.  
C. Use Firewall Manager to enforce a WAF policy on S3 buckets and notify via SNS on policy violations.  
D. Create an SCP to deny `s3:PutBucketPublicAccessBlock` actions and use Trusted Advisor to email alerts.  
**Answer**: A  
**Explanation**: Config detects and remediates public buckets, and EventBridge notifies via SNS, meeting all needs. B lacks remediation, C misuses WAF, and D prevents changes but doesn’t remediate.

### Question 67
**Scenario**: WAF allows SQL injections on an ALB.  
**Question**: What should be configured?  
A. SQL injection rule  
B. S3 bucket policy  
C. CloudTrail logs  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: SQL rules block injections.

### Question 68
**Scenario**: Firewall Manager skips new EC2 instances.  
**Question**: What’s required?  
A. AWS Organizations  
B. S3 bucket versioning  
C. CloudWatch metrics  
D. Lambda trigger  
**Answer**: A  
**Explanation**: Organizations enforce policies.

### Question 69
**Scenario**: IAM Identity Center users lack app access post-SSO setup.  
**Question**: What should be verified?  
A. Permission set assignments  
B. S3 event triggers  
C. CodePipeline artifacts  
D. RDS failover settings  
**Answer**: A  
**Explanation**: Assignments grant access.

### Question 70
**Scenario**: A Config rule needs to auto-fix unencrypted RDS instances.  
**Question**: What should be used?  
A. SSM Automation  
B. Lambda timeout  
C. S3 CRR  
D. CloudFormation outputs  
**Answer**: A  
**Explanation**: SSM automates encryption fixes.

### Question 71
**Scenario**: WAF allows bot traffic to API Gateway.  
**Question**: What should be enabled?  
A. Bot Control rule  
B. S3 bucket policy  
C. CloudTrail logs  
D. CodeDeploy hooks  
**Answer**: A  
**Explanation**: Bot Control blocks bots.

### Question 72
**Scenario**: SSO with OneLogin fails after an update.  
**Question**: What should be integrated?  
A. IAM Identity Center  
B. AWS Config  
C. CodePipeline  
D. CloudWatch alarms  
**Answer**: A  
**Explanation**: IAM Identity Center integrates OneLogin.

### Question 73
**Scenario**: Firewall Manager needs to secure new ALBs.  
**Question**: What should be created?  
A. WAF policy  
B. S3 event trigger  
C. Lambda concurrency  
D. CloudFormation stack  
**Answer**: A  
**Explanation**: WAF policies secure ALBs.

### Question 74
**Scenario**: Config rules differ across regions.  
**Question**: What should be used?  
A. Conformance packs  
B. S3 event triggers  
C. CloudTrail insights  
D. Lambda aliases  
**Answer**: A  
**Explanation**: Conformance packs standardize rules.

### Question 75
**Scenario**: IAM Identity Center needs role-based access by team.  
**Question**: What should be configured?  
A. ABAC with team attributes  
B. S3 bucket policies  
C. CodePipeline stages  
D. RDS Multi-AZ  
**Answer**: A  
**Explanation**: ABAC uses team attributes for access.

---



# AWS Certified DevOps Engineer – Professional (DOP-C02) Practice Questions (Set 9)

This set includes 75 complex, scenario-based questions distributed across the six DOP-C02 domains per their official weightings. Questions reflect real-world DevOps challenges with detailed explanations.

---

## Domain 1: SDLC Automation (22%) - 17 Questions

### Question 1
**Scenario**: A company uses AWS CodePipeline to deploy a Java Spring Boot application to Amazon ECS Fargate, sourced from a private Bitbucket repository. The pipeline includes a CodeBuild stage for compilation and unit tests, followed by a CodeDeploy stage using a blue/green deployment strategy. After a recent deployment, a memory leak crashed half the ECS tasks, unnoticed until customer complaints surfaced 30 minutes later. The team wants to run stress tests before shifting production traffic, automatically roll back if tests fail, and notify developers via Microsoft Teams within 5 minutes of a failure, all with minimal manual intervention.  
**Question**: Which combination of steps should a DevOps engineer take to meet these requirements? (Choose two.)  
A. Add a CodeBuild action after the source stage to run stress tests and publish results to an S3 artifact.  
B. Modify the CodeDeploy `appspec.yml` to include a `BeforeAllowTraffic` hook that runs stress tests via a script, exiting with an error code if tests fail, and triggers a Lambda function to notify Teams.  
C. Configure a manual approval action in CodePipeline post-build to verify stress test results before deployment.  
D. Use an EventBridge rule to detect CodeDeploy deployment states, trigger a Lambda function to run stress tests, and notify Teams via a webhook if tests fail.  
E. Update the ECS service definition to include a 10-minute health check grace period to allow stress tests to complete.  
**Answers**: B, D  
**Explanation**:  
- **B**: The `BeforeAllowTraffic` hook runs pre-traffic shift, allowing stress tests with automatic rollback on failure (exit code), and Lambda notifies Teams, minimizing intervention.  
- **D**: EventBridge detects deployment states, runs tests via Lambda, and notifies Teams within 5 minutes if tests fail, complementing the hook’s rollback.  
- **Why not A**: A pre-deployment CodeBuild action doesn’t integrate with CodeDeploy’s rollback or notification flow.  
- **Why not C**: Manual approval contradicts minimal intervention.  
- **Why not E**: Grace periods delay health checks but don’t run tests or notify.

### Question 2
**Scenario**: A team’s CodeBuild project compiles a .NET Core app, but builds fail intermittently because a private NuGet package hosted on an internal server isn’t downloaded. The build logs show a “connection timeout” error, despite the server being accessible from the team’s VPC. The pipeline uses a standard CodeBuild image and deploys to EC2 via CodeDeploy.  
**Question**: What should a DevOps engineer troubleshoot first to resolve this issue?  
A. The CodeBuild project’s VPC settings and security group rules for outbound traffic to the NuGet server.  
B. The CodePipeline IAM role for permissions to access the NuGet server.  
C. The S3 artifact bucket policy for cross-VPC access.  
D. The CodeBuild environment variables for a misconfigured NuGet feed URL.  
**Answer**: A  
**Explanation**: A “connection timeout” suggests a network issue; CodeBuild needs VPC settings and security group rules to reach the internal server. B is permission-related (not timeout), C is irrelevant (S3 isn’t involved), and D might misconfigure the URL but wouldn’t cause timeouts.

### Question 3 (Multiple-Response)
**Scenario**: A company deploys a Ruby on Rails app to Amazon ECS using CodePipeline and CodeDeploy. They want a canary deployment shifting 5% traffic for 15 minutes, followed by 25% for 30 minutes, with automatic rollback on task failure and health check results visible in Slack. The app runs behind an ALB with dynamic port mapping.  
**Question**: Which THREE steps should a DevOps engineer take to meet these requirements?  
A. Configure CodeDeploy with a custom deployment configuration defining 5% for 15 minutes and 25% for 30 minutes.  
B. Set up an ALB target group with health checks for ECS tasks and integrate it with CodeDeploy.  
C. Add a `AfterAllowTestTraffic` hook in the `appspec.yml` to log health check results to CloudWatch and trigger a Lambda function to post to Slack.  
D. Enable rolling updates in CodePipeline with a 5% increment every 15 minutes.  
E. Use an EventBridge rule to monitor CodeDeploy failures and notify Slack via SNS.  
**Answers**: A, B, C  
**Explanation**:  
- **A**: A custom deployment config in CodeDeploy defines the canary steps (5%/15m, 25%/30m) with rollback on failure.  
- **B**: ALB target groups with health checks are required for ECS blue/green deployments and rollback.  
- **C**: The hook logs results post-test traffic, and Lambda posts to Slack for visibility.  
- **Why not D**: Rolling updates are for EC2, not ECS blue/green.  
- **Why not E**: EventBridge notifies on failure but doesn’t show health check results.

### Question 4
**Scenario**: A financial services company deploys a Node.js app to EC2 using CodePipeline and CodeDeploy. They need to dynamically adjust database connection strings based on deployment groups (staging, prod) without maintaining separate app versions. The app uses a MySQL database in RDS, and connection strings are sensitive.  
**Question**: Which solution should a DevOps engineer implement to meet these requirements with the highest security?  
A. Store connection strings in AWS Secrets Manager, retrieve them in a script using `DEPLOYMENT_GROUP_NAME`, and reference the script in the `appspec.yml` `BeforeInstall` hook.  
B. Hardcode connection strings in CloudFormation parameters and pass them to CodeDeploy via environment variables.  
C. Use CodePipeline variables to store connection strings and inject them into the app at runtime.  
D. Store connection strings in an S3 bucket and fetch them during deployment using an IAM role.  
**Answer**: A  
**Explanation**: Secrets Manager securely stores sensitive strings, and `DEPLOYMENT_GROUP_NAME` dynamically selects them in a script, avoiding multiple versions. B hardcodes secrets (insecure), C exposes secrets in plain text, and D is less secure than Secrets Manager.

### Question 5
**Scenario**: A media company uses CodePipeline to deploy a PHP Laravel app to Elastic Beanstalk, sourced from GitLab. The pipeline includes a CodeBuild stage for tests and a deployment stage. After switching from GitHub, deployments stopped triggering, despite new commits appearing in GitLab. The team needs automatic deployments on commits to the `main` branch and error notifications via email within 10 minutes if the pipeline fails.  
**Question**: Which combination of steps should a DevOps engineer take to resolve this and meet the requirements? (Choose two.)  
A. Update the CodePipeline source action to use GitLab and configure a webhook in GitLab to trigger the pipeline on `main` branch commits.  
B. Reconfigure the CodeBuild project to poll GitLab every 5 minutes and trigger deployments manually.  
C. Create an EventBridge rule to detect CodePipeline failures, targeting an SNS topic with email subscriptions for notifications within 10 minutes.  
D. Modify the Elastic Beanstalk environment to pull commits directly from GitLab and notify via CloudWatch alarms.  
E. Add a Lambda function to the pipeline to check GitLab commits and email the team on failures.  
**Answers**: A, C  
**Explanation**:  
- **A**: Updating the source action and adding a GitLab webhook ensures automatic triggers on `main` commits.  
- **C**: EventBridge with SNS notifies on failures within 10 minutes, leveraging pipeline state events.  
- **Why not B**: Polling is inefficient and manual.  
- **Why not D**: Beanstalk doesn’t pull commits; it’s deployment-driven.  
- **Why not E**: Lambda adds complexity over EventBridge.

### Question 6
**Scenario**: A team’s CodePipeline deploys a Python Flask app to Lambda, recently migrated from CodeCommit to GitHub Enterprise. Post-migration, the pipeline no longer triggers on commits, and builds fail due to missing GitHub credentials. The team needs to restore automatic triggers and secure credential handling.  
**Question**: What should a DevOps engineer do to resolve this issue?  
A. Update the CodePipeline source to GitHub Enterprise, store credentials in Secrets Manager, and configure CodePipeline to use them via an IAM role.  
B. Revert to CodeCommit and adjust the pipeline source action accordingly.  
C. Add GitHub credentials to CodeBuild environment variables and trigger manually.  
D. Use a Lambda function to poll GitHub Enterprise and trigger CodePipeline with stored credentials.  
**Answer**: A  
**Explanation**: Updating to GitHub Enterprise with Secrets Manager and an IAM role restores triggers securely. B avoids migration, C is insecure and manual, and D is overly complex.

### Question 7
**Scenario**: A startup uses CodeArtifact to manage Maven dependencies for a Java app in a CodeBuild project. Builds fail because a critical library from a corporate repository isn’t fetched, despite being accessible via VPN. The pipeline deploys to ECS via CodeDeploy.  
**Question**: What should a DevOps engineer configure to ensure dependency retrieval?  
A. Add an upstream repository in CodeArtifact pointing to the corporate Maven repo and configure CodeBuild with VPC access.  
B. Update CodeStar to include the corporate repo and redeploy the pipeline.  
C. Modify CodeGuru to fetch dependencies and integrate with CodeBuild.  
D. Hardcode the repo URL in the `buildspec.yml` and use IAM credentials.  
**Answer**: A  
**Explanation**: An upstream repo in CodeArtifact proxies the corporate repo, and VPC access ensures connectivity. B misuses CodeStar, C is irrelevant, and D is insecure.

### Question 8
**Scenario**: During a CodePipeline run, CodeGuru Reviewer identifies a potential buffer overflow in a C++ app deploying to EC2. The team needs to address this before deployment and track fix effectiveness.  
**Question**: Which solution should a DevOps engineer implement?  
A. Refactor the code per CodeGuru recommendations, re-run the pipeline, and monitor performance with CloudWatch metrics post-deployment.  
B. Increase the CodeBuild timeout to allow manual code review before deployment.  
C. Enable S3 versioning to rollback if the issue persists after deployment.  
D. Adjust the `appspec.yml` to skip deployment if CodeGuru flags issues.  
**Answer**: A  
**Explanation**: Refactoring fixes the issue, re-running validates it, and CloudWatch tracks effectiveness. B delays without fixing, C is reactive, and D isn’t a CodeGuru feature.

### Question 9
**Scenario**: A multi-region CodePipeline deploys a Django app to ECS in us-east-1 and eu-west-1. Deployments to eu-west-1 fail because CodeDeploy can’t access artifacts in an us-east-1 S3 bucket, despite cross-region replication being enabled. The team needs reliable multi-region deployments.  
**Question**: What should a DevOps engineer do to resolve this issue?  
A. Update the CodeDeploy IAM role with permissions for cross-region S3 access and ensure the replication rule includes artifact prefixes.  
B. Reconfigure CodePipeline to use a single-region artifact store and disable replication.  
C. Add a Lambda function to copy artifacts to an eu-west-1 bucket during deployment.  
D. Modify CloudWatch Logs to monitor replication and retry deployments manually.  
**Answer**: A  
**Explanation**: Proper IAM permissions and replication rules ensure artifact access. B limits multi-region, C adds complexity, and D is manual.

### Question 10
**Scenario**: A CodeBuild project for a Rust app requires a specific toolchain version not in the standard image, causing build failures during a CodePipeline run to Lambda.  
**Question**: How should a DevOps engineer specify the custom toolchain?  
A. Define a custom Docker image with the toolchain in CodeBuild environment settings and reference it in the project.  
B. Update the CodePipeline source stage to include the toolchain binary.  
C. Add the toolchain to the `appspec.yml` for Lambda deployment.  
D. Store the toolchain in an S3 bucket and fetch it during build.  
**Answer**: A  
**Explanation**: A custom Docker image in CodeBuild settings ensures the toolchain is available. B is impractical, C is deployment-specific, and D adds overhead.

### Question 11
**Scenario**: A team deploys a microservices app to ECS with CodeDeploy blue/green. Post-deployment, some services fail due to misconfigured environment variables, unnoticed until traffic shifts. They need validation before production traffic and rollback on failure.  
**Question**: What should a DevOps engineer configure to meet these requirements?  
A. Add an `AfterAllowTestTraffic` hook in `appspec.yml` to validate environment variables via a script, exiting with an error on failure to trigger rollback.  
B. Configure a CodePipeline approval action post-build to manually check variables.  
C. Use CodeStar to validate variables and redeploy on failure.  
D. Update CloudFormation to include variable checks and rollback logic.  
**Answer**: A  
**Explanation**: The hook validates pre-traffic shift with rollback, meeting automation needs. B is manual, C misuses CodeStar, and D is for IaC, not deployment.

### Question 12
**Scenario**: A CodeBuild project for a Node.js app fails to connect to a private RDS instance during integration tests in a CodePipeline run to EC2. The RDS instance is in a VPC with private subnets, and builds use a standard image.  
**Question**: What should a DevOps engineer configure to enable connectivity?  
A. Update the CodeBuild project with VPC settings, including private subnets and a security group allowing RDS access.  
B. Add an S3 bucket policy to proxy RDS traffic during builds.  
C. Modify the IAM role to include RDS connection permissions.  
D. Configure a CloudWatch Logs subscription to debug connectivity issues.  
**Answer**: A  
**Explanation**: VPC settings with subnets and security groups enable RDS access. B is irrelevant, C addresses permissions (not connectivity), and D debugs but doesn’t fix.

### Question 13
**Scenario**: A retail company deploys a PHP app to ECS with CodeDeploy. A critical holiday update must minimize risk and downtime, with a full rollback option if issues arise post-deployment. The app uses an ALB with dynamic port mapping.  
**Question**: Which deployment strategy should a DevOps engineer choose to meet these requirements?  
A. Blue/Green with a 10-minute traffic shift delay and rollback enabled via CodeDeploy.  
B. Rolling updates with a 5% increment every 5 minutes in CodePipeline.  
C. All-at-once deployment with manual rollback via CloudFormation.  
D. Immutable deployment with a 15-minute health check grace period.  
**Answer**: A  
**Explanation**: Blue/Green ensures zero downtime, low risk, and full rollback, ideal for critical updates. B risks partial downtime, C is high-risk, and D isn’t a CodeDeploy strategy.

### Question 14
**Scenario**: CodeGuru Profiler flags excessive I/O wait times in a Python Flask app during a CodePipeline deploy to Lambda. The app reads large files from S3, impacting latency. The team needs to optimize this before production.  
**Question**: What should a DevOps engineer do to address this issue?  
A. Optimize file reads based on Profiler insights, using streaming or caching, and validate with a test deployment.  
B. Increase Lambda timeout to allow I/O completion without optimization.  
C. Enable S3 versioning to rollback if optimization fails.  
D. Adjust CodeDeploy hooks to skip I/O-heavy operations.  
**Answer**: A  
**Explanation**: Optimization per Profiler fixes the root cause, validated pre-production. B masks the issue, C is reactive, and D avoids but doesn’t solve it.

### Question 15
**Scenario**: A CodePipeline fails to pass artifacts from CodeBuild to CodeDeploy for an ECS app. Logs show “artifact not found” errors, despite successful builds. The artifact is a Docker image pushed to Amazon ECR.  
**Question**: What should a DevOps engineer verify to resolve this?  
A. The CodeBuild `buildspec.yml` artifact output configuration and ECR push commands match the CodeDeploy input.  
B. GitLab credentials for repository access in the source stage.  
C. IAM role permissions for cross-service artifact handling.  
D. S3 bucket encryption settings for artifact storage.  
**Answer**: A  
**Explanation**: Misaligned `buildspec.yml` outputs or ECR push issues cause “not found” errors. B is source-related, C is permission-related (not indicated), and D is irrelevant (ECR, not S3).

### Question 16
**Scenario**: A small team deploys a Vue.js app to Lambda using CodePipeline, with builds failing due to complex dependency management. They need a simplified CI/CD setup with dependency caching and minimal configuration.  
**Question**: Which solution should a DevOps engineer implement?  
A. Use AWS CodeStar with CodeArtifact integration for dependency caching and streamlined pipeline setup.  
B. Configure CodePipeline with manual dependency uploads to S3.  
C. Add CodeGuru to manage dependencies and optimize builds.  
D. Use CodeDeploy with a custom script to cache dependencies locally.  
**Answer**: A  
**Explanation**: CodeStar simplifies CI/CD, and CodeArtifact caches dependencies, reducing complexity. B is manual, C misuses CodeGuru, and D is for deployment, not build.

### Question 17
**Scenario**: A company uses CodeArtifact for Ruby gems in a CodeBuild project deploying to ECS. A new gem from a private Gemfury repo isn’t available, causing build failures, despite network access being confirmed. The team needs to integrate this repo securely.  
**Question**: What should a DevOps engineer configure to resolve this?  
A. Add an upstream repository in CodeArtifact for Gemfury with authentication via a Secrets Manager-stored token.  
B. Update CodePipeline to fetch gems directly from Gemfury using IAM credentials.  
C. Modify CodeBuild to bypass CodeArtifact and pull from Gemfury with a hardcoded token.  
D. Use CloudFormation to deploy a proxy server for Gemfury access.  
**Answer**: A  
**Explanation**: An upstream repo with Secrets Manager integrates Gemfury securely. B bypasses CodeArtifact, C is insecure, and D is overly complex.

---

## Domain 2: Configuration Management and IaC (17%) - 13 Questions

### Question 18
**Scenario**: A company uses CloudFormation to deploy an ECS cluster, ALB, and DynamoDB table across multiple regions in an AWS Organizations setup. During a recent deployment to ap-southeast-1, the stack failed because the ALB couldn’t resolve a Route 53 alias due to a missing hosted zone ID, which wasn’t shared from a central networking stack in us-east-1. The team needs to ensure cross-region resource dependencies are resolved automatically with minimal manual updates.  
**Question**: What should a DevOps engineer do to resolve this and prevent future issues?  
A. Update the networking stack to export the hosted zone ID via Outputs and use `Fn::ImportValue` in the ECS stack, deploying via StackSets.  
B. Consolidate all resources into a single StackSet in us-east-1 with hardcoded region mappings.  
C. Use AWS Service Catalog to create a product with embedded hosted zone IDs for each region.  
D. Add a Lambda-backed custom resource to the ECS stack to query Route 53 dynamically for the hosted zone ID.  
**Answer**: A  
**Explanation**: Exporting via Outputs and importing with `Fn::ImportValue` via StackSets resolves dependencies automatically. B limits flexibility, C adds overhead, and D is unnecessarily complex.

### Question 19
**Scenario**: A CloudFormation stack deploys an EC2 instance with an EBS volume. The team needs to deploy the instance only in us-west-2 and use a specific AMI based on that region.  
**Question**: Which component should a DevOps engineer use to define the region-specific AMI?  
A. Mappings with region-to-AMI key-value pairs  
B. Parameters with a default AMI value  
C. Conditions based on region parameters  
D. Outputs referencing the AMI ID  
**Answer**: A  
**Explanation**: Mappings define static region-specific AMIs efficiently. B lacks region logic, C is for deployment (not selection), and D is for sharing, not selection.

### Question 20
**Scenario**: A CloudFormation stack needs an ECS service’s DNS name for an external system post-deployment. The service uses an ALB with a dynamic hostname.  
**Question**: Which function should a DevOps engineer use to retrieve this?  
A. `Fn::GetAtt` on the ALB resource to get the DNSName attribute  
B. `Fn::Ref` on the ECS service to get its ID  
C. `Fn::Join` to concatenate a static hostname  
D. `Fn::Sub` to substitute a variable DNS name  
**Answer**: A  
**Explanation**: `Fn::GetAtt` retrieves the ALB’s dynamic DNSName. B gets an ID (not DNS), C is static, and D requires manual input.

### Question 21
**Scenario**: A company uses StackSets to deploy an API Gateway, Lambda, and S3 bucket across 10 accounts in an organization. A new account deployment failed because the Lambda function couldn’t access the S3 bucket due to a missing cross-account role. The team needs to ensure future deployments include necessary permissions automatically.  
**Question**: Which solution should a DevOps engineer implement?  
A. Update the StackSet template to include an IAM role with S3 access permissions and a trust relationship to the Lambda execution role, deploying across accounts.  
B. Manually create an IAM role in each new account post-deployment with S3 permissions.  
C. Use a custom resource in the StackSet to invoke a Lambda function granting S3 access per account.  
D. Configure CodePipeline to deploy the role separately after StackSet completion.  
**Answer**: A  
**Explanation**: Including the role in the StackSet template ensures automatic permissions. B is manual, C adds complexity, and D separates deployment unnecessarily.

### Question 22
**Scenario**: A company deploys a Python Flask app to Elastic Beanstalk with an ALB. During a recent update, the app experienced 10 minutes of downtime because instances were terminated before new ones were healthy, impacting customer transactions. The team needs zero-downtime updates with health checks confirming readiness.  
**Question**: Which deployment strategy should a DevOps engineer configure to meet these requirements?  
A. Use blue/green deployment with a swap environment step after health checks pass, monitored via ALB target group status.  
B. Set rolling updates with a 50% batch size and 5-minute health check delay.  
C. Configure all-at-once deployment with a 10-minute grace period for health checks.  
D. Enable immutable updates with a pre-deployment health check script in `.ebextensions`.  
**Answer**: A  
**Explanation**: Blue/green ensures zero downtime by swapping after health checks, using ALB status. B risks downtime, C terminates all at once, and D adds complexity without full rollback.

### Question 23
**Scenario**: A team uses Elastic Beanstalk to host a Node.js app with Redis caching via ElastiCache. They need to configure a custom Redis client library during instance launch without modifying the app code, ensuring compatibility across environments.  
**Question**: How should a DevOps engineer accomplish this?  
A. Create an `.ebextensions` file with a `commands` section to install the Redis client library via npm on instance boot.  
B. Update the `buildspec.yml` to include the library in the app package during CodeBuild.  
C. Add the library installation to the `appspec.yml` `Install` hook for CodeDeploy.  
D. Embed the library in a CloudFormation parameter and pass it to Beanstalk.  
**Answer**: A  
**Explanation**: `.ebextensions` installs the library on instances without code changes, ensuring consistency. B modifies the app, C is for CodeDeploy, and D misuses parameters.

### Question 24
**Scenario**: A CloudFormation stack deploys an S3 bucket, ECS service, and ALB. After deletion, the S3 bucket persists with objects, causing stack deletion failures and manual cleanup. The team needs automatic cleanup on stack termination without retaining objects.  
**Question**: What should a DevOps engineer add to the template to resolve this?  
A. Set `DeletionPolicy: Delete` on the S3 bucket resource and add a custom resource with a Lambda function to empty the bucket on delete.  
B. Enable S3 versioning and set a lifecycle policy to expire objects on stack deletion.  
C. Use a CodeDeploy hook to delete bucket contents before stack termination.  
D. Configure the ECS service to empty the bucket via a lifecycle event in CloudFormation.  
**Answer**: A  
**Explanation**: `DeletionPolicy: Delete` with a Lambda custom resource ensures bucket cleanup. B retains versions, C is deployment-specific, and D misuses ECS.

### Question 25
**Scenario**: A company uses Elastic Beanstalk for a Java app with an RDS backend. During a peak traffic update, capacity dropped by 50% due to rolling updates terminating instances before new ones were ready, causing request timeouts. They need to maintain full capacity with zero downtime.  
**Question**: Which deployment option should a DevOps engineer configure?  
A. Immutable deployment with health-based scaling to launch new instances before terminating old ones.  
B. Rolling deployment with a 25% batch size and 5-minute health check interval.  
C. All-at-once deployment with a pre-scaled environment to handle peak load.  
D. Blue/green deployment with a manual swap after capacity doubles.  
**Answer**: A  
**Explanation**: Immutable launches new instances first, maintaining capacity and avoiding downtime. B reduces capacity, C risks downtime, and D requires manual intervention.

### Question 26
**Scenario**: A CloudFormation stack deploys an API Gateway and Lambda function. The team needs to share the API endpoint URL with an external partner post-deployment, but the URL changes with each update due to stage redeployments.  
**Question**: How should a DevOps engineer ensure the endpoint is consistently shareable?  
A. Use an Outputs section to export the API Gateway `InvokeURL` attribute and reference it with `Fn::GetAtt`.  
B. Hardcode the URL in a Parameter and update it manually after each deployment.  
C. Add a Condition to fix the stage name and use `Fn::Ref` to retrieve the URL.  
D. Store the URL in an S3 bucket and fetch it via a Lambda function post-deployment.  
**Answer**: A  
**Explanation**: Outputs with `Fn::GetAtt` dynamically exports the URL, avoiding manual updates. B is error-prone, C misuses conditions, and D adds complexity.

### Question 27
**Scenario**: A team uses Elastic Beanstalk for a Ruby app with an ALB. They need to configure a custom SSL certificate for HTTPS traffic, ensuring it persists across environment updates without app changes.  
**Question**: Where should a DevOps engineer configure the certificate?  
A. In the Beanstalk environment configuration under `aws:elbv2:listener:443`, specifying the certificate ARN from ACM.  
B. In an S3 bucket policy with the certificate ARN and reference it in `.ebextensions`.  
C. In the `appspec.yml` `Install` hook to apply the certificate to the ALB.  
D. In a CloudFormation stack output passed to Beanstalk as an environment variable.  
**Answer**: A  
**Explanation**: Environment config applies the certificate persistently. B misuses S3, C is for CodeDeploy, and D is indirect.

### Question 28
**Scenario**: A CloudFormation stack needs to construct a bucket name from a prefix and environment (e.g., `prod-myapp-bucket`). The prefix is dynamic based on user input, and the environment is fixed per deployment.  
**Question**: Which function should a DevOps engineer use to achieve this?  
A. `Fn::Join` with a Parameter for the prefix and a static environment string  
B. `Fn::GetAtt` to retrieve the bucket name from another resource  
C. `Fn::Ref` to reference a predefined bucket name  
D. `Fn::ImportValue` to import a name from another stack  
**Answer**: A  
**Explanation**: `Fn::Join` combines dynamic and static values. B is for attributes, C lacks flexibility, and D requires external stacks.

### Question 29
**Scenario**: A company uses AWS Organizations with CloudFormation StackSets to deploy a VPC, ECS cluster, and ALB across 20 accounts. A recent deployment to a new OU failed because the ALB listener rule referenced a non-existent target group due to deployment order issues. They need consistent, ordered deployments across OUs.  
**Question**: What should a DevOps engineer do to ensure proper deployment sequencing?  
A. Use nested stacks within the StackSet, defining the VPC first, then ECS with a `DependsOn` attribute for the ALB, ensuring target group creation precedes listener rules.  
B. Deploy a single monolithic StackSet with hardcoded resource order and retry on failure.  
C. Configure CodePipeline to sequence deployments across OUs with separate stacks.  
D. Add a Lambda custom resource to check resource existence before ALB deployment.  
**Answer**: A  
**Explanation**: Nested stacks with `DependsOn` enforce order in StackSets. B risks failures, C misuses CodePipeline, and D adds complexity.

### Question 30
**Scenario**: A team deploys a Go app to Elastic Beanstalk with an ALB in a VPC. They need to support IPv6 clients accessing the app via a custom domain, ensuring seamless updates without DNS changes. The VPC lacks IPv6 support initially.  
**Question**: Which combination of steps should a DevOps engineer take? (Choose two.)  
A. Add an IPv6 CIDR block to the VPC and subnets hosting the ALB, enabling dual-stack mode on the ALB listener.  
B. Update the Beanstalk environment configuration to use the ALB with a Route 53 alias record pointing to the dual-stack endpoint.  
C. Assign an IPv6 Elastic IP to each Beanstalk instance and update Route 53 with instance-specific records.  
D. Replace the ALB with an NLB and configure IPv6-only routing in CloudFormation.  
E. Use a Lambda function to dynamically update Route 53 with IPv6 addresses post-deployment.  
**Answers**: A, B  
**Explanation**:  
- **A**: Adding an IPv6 CIDR and enabling dual-stack on the ALB supports IPv6 clients.  
- **B**: A Route 53 alias to the ALB ensures seamless updates without DNS changes.  
- **Why not C**: Elastic IPs on instances break Beanstalk scaling.  
- **Why not D**: NLB isn’t required; ALB supports dual-stack.  
- **Why not E**: Lambda updates add unnecessary complexity.

---

## Domain 3: Resilient Cloud Solutions (15%) - 11 Questions

### Question 31
**Scenario**: A company runs a Node.js app on Amazon EKS with a Network Load Balancer (NLB) and an Amazon Aurora PostgreSQL cluster with a single writer instance in us-east-1. During a recent AZ failure, the app was unavailable for 20 minutes due to manual database failover, and session data in Redis was lost because ElastiCache wasn’t replicated. The company needs automatic failover within 5 minutes, session persistence across regions, and zero downtime for future AZ failures.  
**Question**: Which solution should a DevOps engineer implement?  
A. Enable Multi-AZ on Aurora with automatic failover, deploy ElastiCache with Multi-AZ replication, and use DynamoDB global tables for session data with Route 53 failover routing to a secondary region.  
B. Add an Aurora read replica in another AZ and configure NLB health checks with Route 53 latency routing.  
C. Create an Aurora global database with Elastic Beanstalk across regions and store sessions in S3 with CRR.  
D. Use EKS Auto Scaling with Multi-AZ and Redis in a single AZ with manual backups to S3.  
**Answer**: A  
**Explanation**: Multi-AZ Aurora fails over in under 5 minutes, Multi-AZ ElastiCache ensures local redundancy, and DynamoDB global tables provide cross-region session persistence with Route 53 failover, ensuring zero downtime. B lacks write failover and session persistence, C misuses global databases for AZ issues, and D risks data loss.

### Question 32
**Scenario**: A retail app on EC2 with an ALB and RDS MySQL experiences 15-minute outages during AZ failures due to manual RDS failover. The team needs to reduce this to under 3 minutes with minimal latency impact and maintain session data during regional DR scenarios.  
**Question**: Which combination of steps should a DevOps engineer take? (Choose two.)  
A. Enable Multi-AZ on RDS MySQL with automatic failover to a standby instance.  
B. Use DynamoDB global tables for session data with Route 53 failover routing to a secondary region.  
C. Add a read replica in another AZ and configure ALB health checks for failover.  
D. Deploy EC2 Auto Scaling with cross-region replication to S3 for session data.  
E. Set up RDS Proxy to handle failover latency and store sessions in ElastiCache.  
**Answers**: A, B  
**Explanation**:  
- **A**: Multi-AZ RDS auto-fails over in under 3 minutes with low latency impact.  
- **B**: DynamoDB global tables ensure session persistence with Route 53 for DR.  
- **Why not C**: Read replicas don’t support write failover.  
- **Why not D**: S3 isn’t real-time for sessions.  
- **Why not E**: RDS Proxy aids connections but doesn’t reduce failover time to 3 minutes.

### Question 33
**Scenario**: A company needs a DR strategy for an ECS app with Aurora, requiring an RTO of 10 minutes and RPO of 5 minutes, balancing cost and recovery speed. The app handles financial transactions with strict data consistency needs.  
**Question**: Which DR strategy should a DevOps engineer choose?  
A. Warm Standby with Aurora read replicas and ECS tasks pre-deployed in a secondary region, synced via binlog replication.  
B. Multi-Site with active-active ECS clusters and Aurora global databases across regions.  
C. Pilot Light with minimal ECS tasks and Aurora snapshots restored on demand.  
D. Backup and Restore with hourly S3 backups and manual ECS redeployment.  
**Answer**: A  
**Explanation**: Warm Standby with read replicas and pre-deployed tasks meets RTO (10 min) and RPO (5 min) cost-effectively via binlog sync. B exceeds needs (costly), C exceeds RTO/RPO, and D is too slow.

### Question 34
**Scenario**: A serverless payment processing API using Lambda and API Gateway experiences 6-second cold starts during peak hours (500 requests/minute), delaying transactions. The API must respond in under 1 second consistently, with minimal cost during off-peak (50 requests/minute).  
**Question**: Which solution should a DevOps engineer implement?  
A. Configure Application Auto Scaling with provisioned concurrency, setting a minimum of 2 and maximum of 50, based on API Gateway request metrics.  
B. Set reserved concurrency to 500 and increase Lambda memory to 1024 MB.  
C. Deploy Lambda@Edge with a fixed concurrency of 10 for edge caching.  
D. Use provisioned concurrency with a fixed value of 20 and enable DynamoDB DAX.  
**Answer**: A  
**Explanation**: Auto-scaling provisioned concurrency adjusts to load (2-50), keeping latency under 1 second cost-effectively. B over-provisions, C misuses Lambda@Edge, and D is static and unnecessary with DAX.

### Question 35
**Scenario**: A gaming app on ECS Fargate with an ALB requires HA across three AZs in us-west-2. During a recent AZ outage, 33% of capacity was lost, causing latency spikes. The team needs full capacity and sub-second failover during AZ failures without manual intervention.  
**Question**: What should a DevOps engineer configure to meet these requirements?  
A. Deploy ECS Fargate with an Auto Scaling group spanning three AZs, using an ALB with cross-zone load balancing and target group health checks for automatic failover.  
B. Use ECS with EC2 instances in a single AZ and manual failover to a secondary AZ.  
C. Configure Lambda with ALB routing and DynamoDB for stateless HA.  
D. Set up CloudFormation with a static ECS cluster and manual AZ failover scripts.  
**Answer**: A  
**Explanation**: Fargate with Auto Scaling and cross-zone ALB ensures full capacity and sub-second failover via health checks. B loses HA, C misapplies Lambda, and D is manual.

### Question 36
**Scenario**: A document management app uses S3 with cross-region replication (CRR) to eu-central-1 for DR. After enabling CRR, new objects replicate, but metadata updates (e.g., tags) don’t, breaking app functionality in the DR region. The team needs consistent metadata replication.  
**Question**: What should a DevOps engineer do to resolve this?  
A. Update the CRR rule to include metadata replication and enable versioning on both buckets.  
B. Switch to Multi-AZ S3 with automatic metadata sync.  
C. Use CloudWatch Events to trigger a Lambda function copying metadata updates.  
D. Deploy CodeDeploy to sync metadata across regions post-replication.  
**Answer**: A  
**Explanation**: CRR supports metadata replication when enabled with versioning. B isn’t an S3 feature, C adds complexity, and D misuses CodeDeploy.

### Question 37
**Scenario**: A company uses Route 53 with latency-based routing for an ECS app in us-east-1 and ap-south-1. During a us-east-1 outage, traffic didn’t shift to ap-south-1, causing a 30-minute downtime. Health checks were configured but failed to detect the outage due to a misconfigured endpoint.  
**Question**: What should a DevOps engineer fix to ensure automatic failover?  
A. Update Route 53 health checks to monitor the ECS ALB endpoint in each region and associate them with latency records.  
B. Change to failover routing with a static S3 bucket as the secondary endpoint.  
C. Adjust IAM permissions for Route 53 to allow automatic updates.  
D. Enable CloudTrail to log routing failures and manually adjust DNS.  
**Answer**: A  
**Explanation**: Correct health checks on ALB endpoints ensure failover. B loses app functionality, C is irrelevant, and D is manual.

### Question 38
**Scenario**: A media streaming app on EKS needs a DR plan with an RTO of 1 hour and RPO of 15 minutes, minimizing costs while ensuring content availability. The app uses S3 for media files and Aurora for metadata.  
**Question**: Which DR strategy should a DevOps engineer choose?  
A. Pilot Light with minimal EKS nodes and Aurora read replicas in a secondary region, using S3 CRR for media sync.  
B. Warm Standby with pre-scaled EKS and Aurora Multi-AZ in both regions.  
C. Multi-Site with active-active EKS and Aurora global databases.  
D. Backup and Restore with daily S3 snapshots and Aurora backups to S3.  
**Answer**: A  
**Explanation**: Pilot Light with CRR and read replicas meets RTO (1 hr) and RPO (15 min) at low cost. B increases costs, C exceeds needs, and D fails RTO/RPO.

### Question 39
**Scenario**: A Lambda-based API experiences throttling during a marketing campaign (1,000 requests/minute), dropping 20% of requests despite a 2 GB memory allocation. The API must handle all requests with sub-second latency during peaks.  
**Question**: What should a DevOps engineer adjust to resolve this?  
A. Increase reserved concurrency to 1,500 and configure provisioned concurrency with Application Auto Scaling up to 200.  
B. Set reserved concurrency to 500 and double memory to 4 GB.  
C. Deploy Lambda@Edge with a fixed concurrency of 100.  
D. Reduce timeout to 5 seconds and increase concurrency to 2,000.  
**Answer**: A  
**Explanation**: Reserved concurrency (1,500) lifts throttling, and auto-scaling provisioned concurrency (200) ensures sub-second latency. B under-provisions, C misuses Lambda@Edge, and D risks timeouts.

### Question 40
**Scenario**: An ElastiCache Redis cluster serving an ECS app loses 50% of its data during a node failure in us-east-1a, impacting user sessions. The app requires HA and data durability across AZs with sub-minute failover.  
**Question**: What should a DevOps engineer configure?  
A. Enable Multi-AZ replication with Redis AOF persistence and automatic failover.  
B. Use a single-AZ Redis cluster with S3 backups triggered by CloudWatch Events.  
C. Deploy Lambda to sync Redis data to DynamoDB every minute.  
D. Configure CloudFormation to redeploy Redis on failure with manual restores.  
**Answer**: A  
**Explanation**: Multi-AZ with AOF ensures HA and durability with sub-minute failover. B risks data loss, C adds latency, and D is manual.

### Question 41
**Scenario**: A real-time analytics app on ECS Fargate downloads 500 MB of reference data from S3 on startup, delaying task readiness by 5 minutes during scaling events. The app must be ready within 1 minute to meet SLAs, with minimal cost overhead.  
**Question**: Which solution should a DevOps engineer implement?  
A. Configure an ECS warm pool with lifecycle hooks to pre-download data, keeping tasks in a stopped state until needed.  
B. Increase ECS task CPU/memory to speed downloads and scale proactively.  
C. Use Lambda to pre-stage data in EFS and mount it to ECS tasks.  
D. Deploy CloudFormation to cache data in ElastiCache pre-launch.  
**Answer**: A  
**Explanation**: A warm pool pre-downloads data, meeting the 1-minute SLA cost-effectively. B increases costs, C adds complexity, and D misuses ElastiCache.

---

## Domain 4: Monitoring and Logging (15%) - 11 Questions

### Question 42
**Scenario**: A company runs a Python Flask app on ECS Fargate with an ALB, logging request latency to CloudWatch Logs. After a surge, latency spiked to 5 seconds, but the team couldn’t identify affected endpoints due to missing granularity. They need endpoint-specific latency metrics and alerts on spikes above 2 seconds within 5 minutes.  
**Question**: Which solution should a DevOps engineer implement?  
A. Configure a CloudWatch Logs metric filter to extract endpoint and latency with dimensions, and set an alarm with a 5-minute period to notify via SNS.  
B. Enable ALB access logs to S3, query with Athena, and trigger Lambda notifications hourly.  
C. Use X-Ray to trace requests and create custom metrics for latency with CloudWatch alarms.  
D. Set up CloudWatch Logs Insights to query latency daily and email results via SES.  
**Answer**: A  
**Explanation**: Metric filters provide endpoint-specific metrics with alarms within 5 minutes. B isn’t real-time, C focuses on traces (not logs), and D lacks timeliness.

### Question 43
**Scenario**: A Lambda function processing S3 uploads logs errors to CloudWatch Logs, but no logs appear during intermittent failures, delaying debugging by hours. The function uses a custom IAM role, and logs are critical for compliance.  
**Question**: What should a DevOps engineer troubleshoot first to resolve this?  
A. The Lambda IAM role permissions for `logs:PutLogEvents` to the correct log group.  
B. The S3 bucket policy for log delivery permissions.  
C. CodePipeline configuration for log output settings.  
D. CloudWatch Logs retention period expiration settings.  
**Answer**: A  
**Explanation**: Missing `logs:PutLogEvents` permissions prevent logging. B is irrelevant (S3 doesn’t log here), C is deployment-related, and D affects retention, not capture.

### Question 44
**Scenario**: A company’s microservices app on EKS logs to CloudWatch Logs across multiple namespaces. During a recent incident, logs from failed pods weren’t available due to pod termination before log flush, delaying root cause analysis by 12 hours. The team needs near-real-time log collection, failure alerts within 3 minutes, and 180-day retention.  
**Question**: Which combination of steps should a DevOps engineer take? (Choose two.)  
A. Deploy the CloudWatch Logs agent as a DaemonSet on EKS nodes to stream logs with a 180-day retention policy.  
B. Configure a CloudWatch Logs subscription filter to send logs to Kinesis Data Firehose, delivering to S3 with a 180-day lifecycle policy.  
C. Set up an EventBridge rule to detect pod termination events from EKS and notify via SNS within 3 minutes.  
D. Enable EKS auto-recovery to restart failed pods and log via CloudWatch Logs Insights.  
E. Use X-Ray to trace pod failures and export logs to S3 hourly with a retention policy.  
**Answers**: B, C  
**Explanation**:  
- **B**: Subscription with Firehose streams logs near-real-time to S3 with retention.  
- **C**: EventBridge detects failures and notifies within 3 minutes.  
- **Why not A**: DaemonSet logs nodes, not pods directly, missing flush issues.  
- **Why not D**: Auto-recovery doesn’t collect logs.  
- **Why not E**: X-Ray traces, not logs, and isn’t real-time.

### Question 45
**Scenario**: A security team needs to analyze ALB access logs for a Node.js app on ECS to detect brute-force attempts, stored in S3 with 100 GB of monthly data. Queries take 20 minutes, delaying incident response.  
**Question**: Which solution should a DevOps engineer implement to speed up analysis?  
A. Partition the S3 logs by date and hour, and use Athena with a partitioned table for sub-minute queries.  
B. Increase Lambda memory to process logs faster and query via CloudWatch Logs Insights.  
C. Enable CloudWatch Metrics for ALB logs and filter brute-force attempts.  
D. Use CodeGuru to profile log data and optimize query performance.  
**Answer**: A  
**Explanation**: Partitioning reduces query time in Athena significantly. B misapplies Lambda, C isn’t log-specific, and D is for code, not logs.

### Question 46
**Scenario**: A nightly backup Lambda function fails to trigger, causing 24-hour data gaps. Logs show no invocation attempts, and the function is critical for compliance.  
**Question**: What should a DevOps engineer configure to ensure reliable execution?  
A. Create an EventBridge rule with a cron schedule (e.g., `0 0 * * ? *`) targeting the Lambda function and add an SNS notification on failure.  
B. Set a CloudWatch alarm to trigger the function nightly and log failures to S3.  
C. Configure an S3 event notification to invoke the function nightly via a dummy object upload.  
D. Update CodePipeline to run the function nightly with a manual approval step.  
**Answer**: A  
**Explanation**: EventBridge cron ensures reliable scheduling with SNS for failure alerts. B misuses alarms, C is roundabout, and D is manual.

### Question 47
**Scenario**: A company needs real-time alerts on ECS task failures for an app logging to CloudWatch Logs, notifying ops via Slack within 2 minutes of failure to meet SLAs. Logs include failure reasons for immediate triage.  
**Question**: What should a DevOps engineer configure?  
A. Create a CloudWatch Logs subscription filter to stream failure logs to a Lambda function, which posts to Slack within 2 minutes.  
B. Export logs to S3 and use Athena to query failures hourly, notifying via SES.  
C. Set up CodeDeploy hooks to detect failures and notify Slack directly.  
D. Use CloudWatch Logs Insights to scan logs daily and alert via SNS.  
**Answer**: A  
**Explanation**: Subscriptions stream logs real-time, enabling Lambda to alert within 2 minutes. B and D aren’t real-time, and C is deployment-specific.

### Question 48
**Scenario**: A team needs alerts on Lambda timeouts exceeding 5 seconds for an API, notifying SREs via email within 5 minutes to maintain 99.9% uptime. The function logs timeout details to CloudWatch Logs.  
**Question**: What should a DevOps engineer set up?  
A. Configure a CloudWatch Logs metric filter for timeout events, create an alarm with a 5-minute period, and notify via SNS with email subscriptions.  
B. Use X-Ray to trace timeouts and set an alarm with SES notifications.  
C. Export logs to S3 and trigger a Lambda email notification hourly via Athena.  
D. Enable CloudWatch Metrics for Lambda and alert on duration via CloudWatch Events.  
**Answer**: A  
**Explanation**: Metric filters extract timeouts, and alarms notify within 5 minutes via SNS. B traces but doesn’t log details, C isn’t real-time, and D misses log context.

### Question 49
**Scenario**: A company’s VPC Flow Logs in S3 (50 TB) take hours to query with Athena for security audits, missing daily compliance deadlines. Logs are stored unpartitioned with a year’s data.  
**Question**: What should a DevOps engineer do to reduce query time to minutes?  
A. Partition logs by date and region in S3, re-create the Athena table with partitions, and optimize queries with WHERE clauses.  
B. Increase Lambda memory to 4 GB and process logs in-memory with Athena.  
C. Convert logs to CloudWatch Logs Insights for faster querying.  
D. Use CodePipeline to preprocess logs into a smaller dataset daily.  
**Answer**: A  
**Explanation**: Partitioning reduces scanned data, speeding queries to minutes. B misapplies Lambda, C loses S3 benefits, and D adds overhead.

### Question 50
**Scenario**: An EventBridge rule fails to trigger a Lambda function across accounts for ECS task monitoring, despite successful single-account tests. The rule targets a custom event bus with task state changes.  
**Question**: What should a DevOps engineer verify to resolve this?  
A. The custom event bus resource policy in the target account allows cross-account events from the source account.  
B. The S3 bucket policy for event storage allows cross-account access.  
C. The IAM user permissions in the source account include `events:PutEvents`.  
D. The CloudFormation stack deploying the rule includes cross-account roles.  
**Answer**: A  
**Explanation**: The event bus policy must permit cross-account events. B is irrelevant (no S3), C is user-specific (not rule), and D misapplies CloudFormation.

### Question 51
**Scenario**: A team needs 1-second resolution for API Gateway latency metrics to debug microsecond-level issues in a trading app, currently logged at 1-minute intervals to CloudWatch Logs.  
**Question**: What should a DevOps engineer enable?  
A. Enable high-resolution metrics on API Gateway and configure a CloudWatch Logs metric filter to push 1-second latency data.  
B. Set standard metrics to 1-second intervals via CloudWatch Events.  
C. Use S3 event triggers to log latency at 1-second granularity.  
D. Deploy CodeDeploy to adjust API Gateway logging frequency.  
**Answer**: A  
**Explanation**: High-resolution metrics with a filter enable 1-second granularity. B isn’t configurable, C misuses S3, and D is deployment-related.

### Question 52
**Scenario**: A company’s CloudWatch Logs Insights queries for Lambda errors return no results despite known failures, delaying incident response by hours. Logs are confirmed to exist in the correct log group with a 30-day retention.  
**Question**: What should a DevOps engineer check to resolve this?  
A. The Insights query syntax and time range to ensure they match the log format and failure window.  
B. The S3 export delay settings for log group archiving.  
C. The IAM role permissions for Insights access to the log group.  
D. The CodePipeline configuration for log output redirection.  
**Answer**: A  
**Explanation**: Incorrect syntax or time range causes empty results. B affects exports (not Insights), C is permission-related (not indicated), and D is deployment-specific.

---

## Domain 5: Incident and Event Response (14%) - 11 Questions

### Question 53
**Scenario**: A company’s S3 bucket triggers a Lambda function to process uploaded CSV files, but the function isn’t invoked for files uploaded via a third-party tool, despite manual uploads working. The bucket policy allows public writes, and logs show no event failures. The team needs reliable triggering for all uploads with failure alerts within 5 minutes.  
**Question**: Which solution should a DevOps engineer implement?  
A. Configure an S3 event notification with a `.csv` suffix filter, targeting the Lambda function, and add an EventBridge rule to detect Lambda invocation failures with SNS notifications within 5 minutes.  
B. Update the bucket policy to require S3 event triggers and notify via CloudWatch alarms on failures.  
C. Use CodeDeploy to redeploy the Lambda with a manual invocation check and SES alerts.  
D. Enable S3 versioning and set a CloudWatch Logs subscription to alert on missed triggers.  
**Answer**: A  
**Explanation**: S3 events with a filter ensure triggering, and EventBridge with SNS alerts within 5 minutes. B misuses policy, C is deployment-related, and D lacks event focus.

### Question 54
**Scenario**: GuardDuty detects an EC2 instance scanning ports externally, risking a security breach. The instance runs a critical app, and the team needs to isolate it automatically within 10 minutes, notify security via Slack, and retain logs for forensics without terminating the instance.  
**Question**: Which combination of steps should a DevOps engineer take? (Choose two.)  
A. Create an EventBridge rule to detect GuardDuty findings, triggering a Lambda function to update the instance’s security group to block outbound traffic.  
B. Configure a CloudWatch Logs subscription to stream instance logs to S3 and set an SNS notification to Slack within 10 minutes of the finding.  
C. Use SSM Automation to terminate the instance and notify security via SES with logs exported to S3.  
D. Enable EC2 auto-recovery to restart the instance and alert via CloudWatch Events.  
E. Deploy CodeDeploy to redeploy the app to a new instance with Slack notifications.  
**Answers**: A, B  
**Explanation**:  
- **A**: EventBridge with Lambda isolates the instance within 10 minutes.  
- **B**: Logs subscription retains logs and notifies Slack.  
- **Why not C**: Termination violates retention.  
- **Why not D**: Restart doesn’t isolate or notify.  
- **Why not E**: Redeployment isn’t required.

### Question 55
**Scenario**: A company’s CloudTrail logs in us-east-1 need 5-year retention for compliance, but after 90 days, logs vanish, risking audits. The logs track S3 and Lambda actions across regions, and manual exports have failed due to oversight.  
**Question**: What should a DevOps engineer configure to meet this requirement?  
A. Enable a multi-region CloudTrail with S3 export, setting a 5-year lifecycle policy with Glacier transition after 1 year.  
B. Increase CloudTrail retention to 5 years in the us-east-1 log group settings.  
C. Use Athena to query logs daily and store results in S3 for 5 years.  
D. Configure CodePipeline to export logs to S3 monthly with a retention policy.  
**Answer**: A  
**Explanation**: Multi-region CloudTrail with S3 export and a lifecycle policy ensures 5-year retention cost-effectively. B isn’t an option (90-day max), C is query-focused, and D is manual.

### Question 56
**Scenario**: A team uses S3 to store JSON config files, triggering a Lambda function to update ECS tasks. They need events only for `.json` files uploaded to a `configs/` prefix, but all uploads currently trigger the function, causing errors.  
**Question**: What should a DevOps engineer configure to filter these events?  
A. Update the S3 event notification with a prefix filter (`configs/`) and suffix filter (`.json`) targeting the Lambda function.  
B. Add a CloudWatch Logs filter to process only `.json` files post-trigger.  
C. Use CodeDeploy hooks to validate file types before Lambda execution.  
D. Modify the bucket policy to allow triggers only for `.json` files in `configs/`.  
**Answer**: A  
**Explanation**: S3 event filters (prefix/suffix) ensure correct triggering. B post-processes (inefficient), C is deployment-specific, and D misuses policy.

### Question 57
**Scenario**: A company with 30 AWS accounts in an organization uses GuardDuty, but findings are scattered across accounts, delaying incident response by days. The security team needs centralized visibility and alerts within 15 minutes of critical findings across all accounts.  
**Question**: What should a DevOps engineer do to meet these requirements?  
A. Enable GuardDuty in all accounts via AWS Organizations, designate a delegated administrator account, and configure an EventBridge rule in the admin account to notify via SNS within 15 minutes of critical findings.  
B. Deploy GuardDuty individually per account and use CloudWatch Logs to aggregate findings hourly.  
C. Use CodePipeline to collect findings from each account and email security daily.  
D. Enable S3 event notifications to centralize findings with SES alerts.  
**Answer**: A  
**Explanation**: Organizations with a delegated admin centralizes GuardDuty, and EventBridge ensures 15-minute alerts. B scatters findings, C is slow, and D misuses S3.

### Question 58
**Scenario**: A company’s CloudTrail in us-west-2 logs management events but misses S3 object deletes, critical for auditing a data pipeline. The bucket is in us-west-2, and logs are exported to S3.  
**Question**: What should a DevOps engineer activate to capture these events?  
A. Enable data events for S3 in the CloudTrail configuration, specifying the bucket.  
B. Turn on management events for S3 in CloudTrail settings.  
C. Use CloudWatch Insights to log S3 deletes separately.  
D. Deploy CodeDeploy to track S3 actions via hooks.  
**Answer**: A  
**Explanation**: Data events capture S3 object actions. B is already enabled, C isn’t event-focused, and D misuses CodeDeploy.

### Question 59
**Scenario**: A team needs real-time alerts on ECS task failures for a payment app, notifying ops via email within 4 minutes to meet SLAs. Failures are logged to CloudWatch Logs, and ECS runs in us-east-1 with Fargate.  
**Question**: What should a DevOps engineer configure?  
A. Create an EventBridge rule to detect ECS task state changes (`FAILED`), targeting an SNS topic with email subscriptions within 4 minutes.  
B. Set a CloudWatch alarm on task metrics with SES notifications hourly.  
C. Use CodeDeploy to redeploy failed tasks and email via SES.  
D. Configure S3 event notifications for task logs with Lambda alerts.  
**Answer**: A  
**Explanation**: EventBridge detects failures real-time, notifying within 4 minutes via SNS. B is slow, C is deployment-focused, and D misuses S3.

### Question 60
**Scenario**: GuardDuty misses API Gateway abuse incidents in a serverless app, despite enabled findings for EC2 and S3. The team needs to detect API misuse (e.g., rate limit evasion) within 10 minutes for compliance.  
**Question**: What should a DevOps engineer enable?  
A. Enable GuardDuty API Gateway protection and configure an EventBridge rule to alert via SNS within 10 minutes of findings.  
B. Use S3 CRR to sync API logs and alert via CloudWatch Logs.  
C. Deploy Lambda aliases to monitor API traffic and notify via SES.  
D. Configure CloudFormation to redeploy GuardDuty with API coverage.  
**Answer**: A  
**Explanation**: API Gateway protection in GuardDuty detects abuse, and EventBridge alerts within 10 minutes. B is log-focused, C is custom, and D misuses CloudFormation.

### Question 61
**Scenario**: A company needs to audit DynamoDB table configuration changes (e.g., TTL updates) after a compliance breach. CloudTrail logs are enabled in us-east-1 with management events, but changes aren’t visible.  
**Question**: Where should a DevOps engineer look, and what should be enabled?  
A. Check CloudTrail logs after enabling data events for DynamoDB in the trail configuration.  
B. Review CloudWatch Metrics for DynamoDB config changes.  
C. Query S3 event logs for DynamoDB actions.  
D. Use CodePipeline artifacts to track table updates.  
**Answer**: A  
**Explanation**: Data events in CloudTrail log DynamoDB config changes. B tracks usage, C is S3-specific, and D is irrelevant.

### Question 62
**Scenario**: An S3 bucket triggers a Lambda function and an SNS topic for object creates, but notifications overlap, causing duplicate processing and alerts. The team needs streamlined, distinct triggers for each target with failure notifications within 5 minutes.  
**Question**: What should a DevOps engineer configure?  
A. Use EventBridge to route S3 create events separately to Lambda and SNS, with a failure rule notifying via SNS within 5 minutes.  
B. Configure CloudWatch Logs subscriptions to split events and notify on failures.  
C. Update CodeDeploy to manage S3 event triggers and alerts.  
D. Set Lambda concurrency to 1 and SNS to delay notifications.  
**Answer**: A  
**Explanation**: EventBridge separates triggers and alerts failures within 5 minutes. B is log-focused, C misuses CodeDeploy, and D delays without solving overlap.

### Question 63
**Scenario**: CloudTrail logs in us-east-1 miss Lambda invocations from eu-west-1, critical for debugging a cross-region app. The trail is single-region with S3 export, and compliance requires all events.  
**Question**: What should a DevOps engineer do to capture these events?  
A. Enable a multi-region CloudTrail covering all regions, exporting logs to S3 with consolidated trails.  
B. Increase S3 bucket size to store missed events from eu-west-1.  
C. Use CloudWatch Events to log Lambda invocations separately in eu-west-1.  
D. Deploy CodePipeline to sync logs across regions manually.  
**Answer**: A  
**Explanation**: Multi-region CloudTrail captures all events. B is irrelevant, C duplicates effort, and D is manual.

---

## Domain 6: Security and Compliance (17%) - 12 Questions

### Question 64
**Scenario**: A company uses AWS Config to monitor EC2 instances across 50 accounts in an organization. An audit found instances without required tags (e.g., `Environment`), risking compliance. The team needs automatic tagging with `Environment=prod` for untagged instances and notifications to security within 10 minutes of non-compliance.  
**Question**: Which solution should a DevOps engineer implement?  
A. Configure an AWS Config managed rule (`required-tags`) with an SSM Automation remediation to add `Environment=prod`, and an EventBridge rule to notify via SNS within 10 minutes of non-compliance findings.  
B. Deploy a Lambda function via CodePipeline to tag instances and email security hourly.  
C. Use CloudFormation StackSets to enforce tags and alert via CloudWatch Logs.  
D. Enable S3 event notifications to tag instances and notify via SES daily.  
**Answer**: A  
**Explanation**: Config with SSM auto-tags, and EventBridge notifies within 10 minutes. B is slow, C misuses StackSets, and D is irrelevant.

### Question 65
**Scenario**: A company needs an AWS Config rule to verify that all S3 buckets use AES-256 encryption with customer-managed KMS keys, rejecting default SSE-S3. The rule must flag non-compliant buckets and auto-remediate within 15 minutes.  
**Question**: What should a DevOps engineer configure?  
A. Create a Lambda-backed custom Config rule to check KMS encryption, with an SSM Automation remediation to update bucket encryption to AES-256 with a KMS key.  
B. Use a managed Config rule for S3 encryption with a CloudWatch alarm for remediation.  
C. Deploy CodeDeploy to enforce encryption and notify via SNS.  
D. Configure S3 event triggers to apply KMS encryption and log compliance.  
**Answer**: A  
**Explanation**: A custom Lambda rule checks KMS specifics, and SSM remediates within 15 minutes. B lacks KMS granularity, C misuses CodeDeploy, and D is event-driven, not compliance-focused.

### Question 66
**Scenario**: A company with 100 accounts in AWS Organizations needs centralized compliance visibility for S3 bucket policies across us-east-1 and eu-west-1. An audit found inconsistent policies, delaying quarterly reviews by weeks. The team requires aggregated data in a delegated administrator account.  
**Question**: What should a DevOps engineer deploy?  
A. Enable AWS Config with an organization aggregator in the delegated admin account, collecting S3 policy data from all accounts and regions.  
B. Use CloudFormation StackSets to deploy S3 policy checks and aggregate results in S3.  
C. Configure CodePipeline to scan policies and store results in CloudWatch Logs.  
D. Deploy Lambda functions per account to email policy data to security daily.  
**Answer**: A  
**Explanation**: Config aggregator centralizes multi-region, multi-account data. B misuses StackSets, C is deployment-focused, and D is decentralized.

### Question 67
**Scenario**: A company’s ALB with WAF allows SQL injection attempts, bypassing existing rules during a penetration test. The app on ECS behind the ALB processes payments, and the team needs to block these attacks with minimal latency impact and log blocked requests for auditing.  
**Question**: Which solution should a DevOps engineer implement?  
A. Add a WAF SQL injection match rule with a block action, and enable WAF logging to CloudWatch Logs for auditing.  
B. Update the S3 bucket policy to deny SQL payloads and log to S3.  
C. Use CloudTrail to detect injections and block via Lambda.  
D. Configure CodeDeploy to redeploy the app with input validation.  
**Answer**: A  
**Explanation**: WAF SQL rules block injections with low latency, and logging aids auditing. B misuses S3, C is reactive, and D shifts responsibility to the app.

### Question 68
**Scenario**: A company uses Firewall Manager to enforce WAF rules on ALBs across 20 accounts in an organization. After adding a new account, its ALBs lack WAF protection, exposing a web app to attacks for 48 hours. The team needs automatic WAF application for new accounts.  
**Question**: What should a DevOps engineer configure?  
A. Enable Firewall Manager integration with AWS Organizations, setting a WAF policy to apply to all accounts and ALB resources automatically.  
B. Deploy CloudFormation StackSets to add WAF rules per account manually.  
C. Use CodePipeline to apply WAF rules to new ALBs daily.  
D. Configure S3 event notifications to trigger WAF attachment for new ALBs.  
**Answer**: A  
**Explanation**: Organizations integration auto-applies WAF policies. B is manual, C is slow, and D misuses S3.

### Question 69
**Scenario**: A company uses IAM Identity Center with Okta SSO across 50 accounts. After a config update, developers in the `DevTeam` group can’t access an ECS management app, despite other apps working. Access should be restricted to `DevTeam` members with the `Team=Dev` attribute.  
**Question**: What should a DevOps engineer verify to resolve this?  
A. The IAM Identity Center permission set for the ECS app includes an ABAC policy with a condition for `Team=Dev` and is assigned to the `DevTeam` group.  
B. The S3 bucket policy for app resources allows `DevTeam` access.  
C. The CodePipeline configuration includes `DevTeam` permissions.  
D. The RDS failover settings grant `DevTeam` access post-update.  
**Answer**: A  
**Explanation**: ABAC with `Team=Dev` in the permission set restricts access, needing verification. B, C, and D are irrelevant to SSO app access.

### Question 70
**Scenario**: A company uses AWS Config to monitor Lambda functions across 10 regions. An audit found functions without dead-letter queues (DLQs), risking data loss during failures. The team needs automatic DLQ attachment (to an SQS queue) and Slack notifications within 15 minutes of non-compliance.  
**Question**: Which solution should a DevOps engineer implement?  
A. Create a custom Config rule with Lambda to check DLQs, use SSM Automation to attach an SQS DLQ, and set an EventBridge rule to notify Slack via SNS within 15 minutes.  
B. Deploy CloudFormation StackSets to enforce DLQs and email via SES daily.  
C. Use CodeDeploy to redeploy functions with DLQs and log to CloudWatch.  
D. Configure S3 event triggers to update functions and notify via Lambda.  
**Answer**: A  
**Explanation**: Custom rule detects DLQ absence, SSM remediates, and EventBridge notifies within 15 minutes. B is slow, C misuses CodeDeploy, and D is irrelevant.

### Question 71
**Scenario**: A company’s API Gateway with WAF experiences bot-driven DDoS attacks, overwhelming rate-based rules and costing $10,000 in overages. The team needs to block bots with user verification and log attempts to S3 for analysis with minimal cost.  
**Question**: What should a DevOps engineer configure?  
A. Add a WAF Bot Control rule with CAPTCHA action and enable WAF logging to S3 with a lifecycle policy for cost management.  
B. Update the S3 bucket policy to block bot IPs and log to CloudWatch Logs.  
C. Use CloudTrail to detect bot requests and block via Lambda.  
D. Deploy CodeDeploy to filter bots and log to S3 manually.  
**Answer**: A  
**Explanation**: Bot Control with CAPTCHA blocks bots, and S3 logging is cost-effective. B misuses S3, C is reactive, and D is manual.

### Question 72
**Scenario**: A company uses IAM Identity Center with Azure AD SSO across 25 accounts. After a tenant update, SREs in the `SRE` group can’t access AWS Console, despite app access working. Access should be role-based with `Role=SRE`.  
**Question**: What should a DevOps engineer verify?  
A. The IAM Identity Center permission set for AWS Console includes an ABAC policy with `Role=SRE` and is assigned to the `SRE` group.  
B. The S3 bucket policy for console resources allows `SRE` access.  
C. The CodePipeline configuration grants `SRE` console permissions.  
D. The RDS failover settings include `SRE` post-update.  
**Answer**: A  
**Explanation**: ABAC with `Role=SRE` ensures console access, needing verification. B, C, and D are irrelevant.

### Question 73
**Scenario**: Firewall Manager fails to apply WAF rules to new API Gateway endpoints in a 15-account organization, leaving a payment API exposed for 24 hours. The team needs automatic WAF protection for all new endpoints.  
**Question**: What should a DevOps engineer configure?  
A. Enable Firewall Manager with AWS Organizations, creating a WAF policy for API Gateway resources across all accounts.  
B. Use CloudFormation StackSets to deploy WAF rules per account nightly.  
C. Configure CodePipeline to apply WAF to new endpoints manually.  
D. Set S3 event notifications to trigger WAF attachment for new APIs.  
**Answer**: A  
**Explanation**: Organizations with Firewall Manager auto-applies WAF. B is slow, C is manual, and D misuses S3.

### Question 74
**Scenario**: A company uses AWS Config across 40 accounts, but rules vary (e.g., some lack encryption checks), risking compliance gaps. The team needs standardized rules deployed automatically to new accounts with minimal overhead.  
**Question**: What should a DevOps engineer deploy?  
A. Use AWS Config conformance packs with a predefined template, deployed via Organizations to all accounts and OUs automatically.  
B. Deploy CodePipeline to push rules to each account daily with Lambda updates.  
C. Configure CloudTrail Insights to standardize rules and notify via SNS.  
D. Use S3 event triggers to deploy rules per account manually.  
**Answer**: A  
**Explanation**: Conformance packs standardize rules with automatic deployment. B adds overhead, C misuses Insights, and D is manual.

### Question 75
**Scenario**: A company uses IAM Identity Center with SAML SSO for 50 accounts. Developers need access to S3 buckets based on their `Project` attribute (e.g., `Project=Alpha`), but access is currently unrestricted, risking data leaks. The team needs least-privilege access with dynamic scoping.  
**Question**: Which solution should a DevOps engineer implement?  
A. Configure IAM Identity Center with ABAC policies using the `Project` attribute in permission sets, restricting S3 access to matching bucket tags.  
B. Update S3 bucket policies to hardcode developer IDs with project-specific access.  
C. Use CodePipeline to assign project-based roles per developer manually.  
D. Deploy CloudFormation to create static S3 policies per project daily.  
**Answer**: A  
**Explanation**: ABAC with `Project` attributes ensures dynamic, least-privilege access. B is static, C is manual, and D lacks scalability.

---




