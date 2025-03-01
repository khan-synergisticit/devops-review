
**An ecommerce company is receiving reports that its order history page is experiencing
delays in reflecting the processing status of orders. The order processing system
consists of an AWS Lambda function that uses reserved concurrency. The Lambda
function processes order messages from an Amazon Simple Queue Service (Amazon
SQS) queue and inserts processed orders into an Amazon DynamoDB table. The
DynamoDB table has auto scaling enabled for read and write capacity.**


A. Check the ApproximateAgeOfOldestMessage metric for the SQS queue. Increase the
Lambda function concurrency limit.
 <br />
B. Check the ApproximateAgeOfOldestMessage metnc for the SQS queue Configure a
redrive policy on the SQS queue.
 <br />
C. Check the NumberOfMessagesSent metric for the SQS queue. Increase the SQS
queue visibility timeout.
 <br />
D. Check the WriteThrottleEvents metric for the DynamoDB table. Increase the
maximum write capacity units (WCUs) for the table's scaling policy.
 <br />
E. Check the Throttles metric for the Lambda function. Increase the Lambda function
Timeout.


To address the delays in the order history page reflecting the processing status of orders, we need to identify and resolve bottlenecks in the system. The setup involves an AWS Lambda function with reserved concurrency pulling messages from an Amazon SQS queue and writing processed orders to an Amazon DynamoDB table with auto-scaling enabled. Delays suggest that either messages are piling up in the queue or the downstream components (Lambda or DynamoDB) aren't keeping up. Let's evaluate the options and determine the two most effective actions.

The ApproximateAgeOfOldestMessage metric in SQS indicates how long the oldest unprocessed message has been waiting in the queue. If this value is high, it means messages aren't being processed quickly enough, pointing to a bottleneck in the Lambda function's ability to consume them. Lambda's reserved concurrency limits how many instances can run simultaneously, so if this limit is too low, it could starve the system of processing power, causing a backlog. Increasing the concurrency limit would allow more Lambda instances to process messages in parallel, reducing the queue delay. This makes option A a strong candidate.

Next, consider the DynamoDB table. Since it has auto-scaling enabled, it should adjust its read and write capacity based on demand. However, if the auto-scaling policy's maximum write capacity units (WCUs) are capped too low, the table might throttle write operations under heavy load, slowing down the Lambda function's ability to insert processed orders. The WriteThrottleEvents metric tracks how often write requests are throttled. If this metric is elevated, it confirms DynamoDB is a bottleneck. Increasing the maximum WCUs in the scaling policy would allow DynamoDB to handle more writes, alleviating delays. This supports option D.

Now, let's assess the other options. Option B suggests checking ApproximateAgeOfOldestMessage and configuring a redrive policy for the SQS queue. A redrive policy moves unprocessable messages to a dead-letter queue (DLQ) after a set number of retries, which is useful for handling poison-pill messages (e.g., malformed orders). However, the problem is about delays, not message failures, and there's no indication of messages failing to process---just that they're slow. A redrive policy wouldn't address the throughput issue, so B is less relevant.

Option C involves checking the NumberOfMessagesSent metric (how many messages are added to the queue) and increasing the SQS visibility timeout. The visibility timeout determines how long a message is hidden from other consumers after being picked up by Lambda. If it's too short, Lambda might not finish processing before the timeout expires, causing messages to reappear in the queue and leading to duplicate processing. However, this would manifest as duplicate entries or errors, not delays in status updates, and the scenario doesn't suggest this issue. Plus, NumberOfMessagesSent reflects input rate, not processing delay, making C a weaker fit.

Option E suggests checking the Throttles metric for Lambda (how often invocations are throttled due to hitting the concurrency limit) and increasing the Lambda timeout. If Throttles is high, it confirms concurrency is exhausted, aligning with option A's fix of increasing concurrency. However, increasing the timeout (how long Lambda waits before giving up) only helps if individual executions are timing out, which would result in failed orders, not delays in status updates. The scenario implies orders are processed eventually, just slowly, so E's timeout adjustment doesn't directly address the issue.

Given the goal is to resolve delays, the most direct actions target throughput bottlenecks. Option A (increase Lambda concurrency) addresses slow queue consumption if ApproximateAgeOfOldestMessage is high, and option D (increase DynamoDB max WCUs) tackles write throttling if WriteThrottleEvents is elevated. These two cover the primary components---Lambda and DynamoDB---without overlap, as concurrency affects processing rate while WCUs affect write capacity.

Final Answer:
A. Check the ApproximateAgeOfOldestMessage metric for the SQS queue. Increase the Lambda function concurrency limit.
D. Check the WriteThrottleEvents metric for the DynamoDB table. Increase the maximum write capacity units (WCUs) for the table’s scaling policy.

***

**To run an application, a DevOps engineer launches an Amazon EC2 instance with public
IP addresses in a public subnet. A user data script obtains the application artifacts and
installs them on the instances upon launch. A change to the security classification of the
application now requires the instances to run with no access to the internet. While the
instances launch successfully and show as healthy, the application does not seem to be
Installed.**

Which of the following should successfully install the application while complying with
the new rule?


A. Launch the instances in a public subnet with Elastic IP addresses attached. Once the
application is installed and running, run a script to disassociate the Elastic IP addresses
afterwards.
 <br />
B. Set up a NAT gateway. Deploy the EC2 instances to a private subnet. Update the
private subnet's route table to use the NAT gateway as the default route.
 <br />
C. Publish the application artifacts to an Amazon S3 bucket and create a VPC endpoint
for S3. Assign an IAM instance profile to the EC2 instances so they can read the
application artifacts from the S3 bucket.
 <br />
D. Create a security group for the application instances and allow only outbound traffic to
the artifact repository. Remove the security group rule once the install is complete.


Let's dive into this problem and figure out whether your choice, B, is correct, while explaining why each option works or doesn't in the context of the new security requirement---no internet access for the EC2 instances---while ensuring the application gets installed.

The scenario starts with an EC2 instance in a public subnet, using a public IP and a user data script to fetch application artifacts from the internet during launch. The instances launch and are healthy, but the application isn't installed because the new rule cuts off internet access, breaking the artifact retrieval. We need a solution that lets the instances access the artifacts without exposing them to the public internet, all while keeping the setup functional.



Option A: Launch in a public subnet with Elastic IPs, then disassociate them after install

This approach keeps the instances in a public subnet with Elastic IPs (public IPs) during launch, allowing the user data script to fetch artifacts from the internet. After installation, a script removes the Elastic IPs, theoretically cutting off internet access. However, this has flaws. First, instances in a public subnet with a route to an internet gateway (IGW) retain internet access via their subnet's routing, even without Elastic IPs, unless you modify the route table post-launch---which isn't mentioned. Second, "no access to the internet" implies a stricter requirement than just removing public IPs; it suggests no outbound connectivity at all. This solution relies on temporary internet access, which might violate the intent of the new rule. Plus, coordinating the disassociation after install adds complexity and potential failure points. This doesn't fully comply with the no-internet rule, so A is incorrect.



Option B: Set up a NAT gateway, deploy to a private subnet, route via NAT

Your choice! Here, the instances move to a private subnet (no public IPs, no direct internet ingress), and a NAT gateway is added in a public subnet with an IGW. The private subnet's route table is updated to send outbound traffic (0.0.0.0/0) to the NAT gateway. The NAT allows instances to initiate outbound connections to the internet (e.g., to fetch artifacts) while blocking inbound internet traffic. During launch, the user data script can still pull artifacts because the NAT provides outbound access, and once installed, the instances remain isolated from inbound internet traffic. However, there's a catch: the instances retain outbound internet access via the NAT, which might conflict with a strict interpretation of "no access to the internet." In AWS, private subnets with a NAT are common for "no public internet" setups, but if the requirement means absolutely no internet connectivity (inbound or outbound), this could be questioned. For the exam, though, NAT in a private subnet is often an acceptable compromise for controlled outbound access. This is likely correct, but let's check the others to confirm.



Option C: Use an S3 bucket with a VPC endpoint and IAM instance profile

This option shifts the artifacts to an S3 bucket and adds an S3 VPC endpoint (a gateway endpoint) in the VPC. The instances, presumably in a private subnet (implied but not stated), get an IAM instance profile to access the S3 bucket. The user data script is updated to fetch artifacts from S3 instead of the internet. The S3 endpoint allows private access to S3 without traversing the internet---no NAT or IGW needed. This fully eliminates internet dependency: the instances have no public IPs, no outbound internet route, and only communicate with S3 via AWS's internal network. It's secure, compliant with "no internet access," and leverages AWS-native features. The catch? It requires modifying the script and infrastructure (S3 bucket, endpoint, IAM role), but that's feasible and aligns with DevOps best practices. This also seems correct---maybe even more so than B.



Option D: Use a security group to allow outbound traffic to the artifact repo, then remove the rule

Here, the instances stay in their current setup (likely public subnet, given the original scenario), and a security group allows outbound traffic only to the artifact repository. The user data script fetches the artifacts, then the rule is removed to block further internet access. This is creative but problematic. First, if the instances are in a public subnet with an IGW route, they still have internet access unless the route table changes---security groups don't override routing. Second, dynamically removing the rule after install is tricky to automate reliably at launch (user data runs once; how do you trigger the removal?). Third, it assumes the instances start with internet access, which might already violate the new rule. This is impractical and doesn't fully comply, so D is incorrect.



Analysis: Is B Correct?

Your pick, B, works because it moves instances to a private subnet and uses a NAT gateway to enable outbound artifact retrieval during launch. The application installs, and the instances lack public IPs or inbound internet access, aligning with many AWS scenarios where "no internet" means "no public exposure." However, C stands out as potentially more correct. It eliminates internet access entirely (no NAT, no outbound internet route) by keeping traffic within the VPC via the S3 endpoint. If the exam interprets "no access to the internet" as zero internet connectivity (inbound and outbound), C wins. AWS exams often favor VPC endpoints for private access over NAT-based solutions when S3 is involved, as it's more secure and cost-effective (no NAT gateway fees).

That said, B isn't wrong in a practical sense---NAT in a private subnet is a standard pattern for controlled outbound access, and the question doesn't specify the artifact source (it could be an external HTTP server, not S3). Without that detail, B remains viable. If this were a real exam question with two correct answers required, B and C might both be intended, but here it's one choice, and C edges out slightly for strict compliance.



Explanation for Your Answer (B)

You're mostly correct with B because it solves the installation issue while reducing internet exposure. The NAT gateway ensures the user data script can fetch artifacts, and the private subnet prevents inbound internet access. The reason it's not perfect is the lingering outbound internet capability, which C avoids. If you assumed the artifacts aren't in S3 or that NAT is sufficient for "no internet" in this context, B is a solid pick. For exam purposes, watch for clues like S3 mentions---here, there's none, so B holds up.

Correct Answer (likely intended):  C, for full internet isolation.

Your Answer (B): Very reasonable, just less strict on "no internet."

What do you think---does that clarify why B works but C might be the exam's preference? Ready for another question?

*** 

**A company wants to use AWS CloudFormation for infrastructure deployment. The
company has strict tagging and resource requirements and wants to limit the deployment
to two Regions. Developers will need to deploy multiple versions of the same application.

Which solution ensures resources are deployed in accordance with company policy?**


A. Create AWS Trusted Advisor checks to find and remediate unapproved
CloudFormation StackSets.
 <br />
B. Create a Cloud Formation drift detection operation to find and remediate unapproved
CloudFormation StackSets.
 <br />
C. Create CloudFormation StackSets with approved CloudFormation templates.
 <br />
D. Create AWS Service Catalog products with approved CloudFormation templates.


Let's tackle this CloudFormation question and see if your pick, C, holds up. The company wants to use AWS CloudFormation for infrastructure deployment with strict tagging and resource requirements, limit deployments to two specific Regions, and allow developers to deploy multiple versions of the same application. We need a solution that enforces policy compliance while meeting these needs. Let's break it down option by option.



Option A: AWS Trusted Advisor checks to find and remediate unapproved CloudFormation StackSets

Trusted Advisor is a tool that provides best-practice recommendations, like cost optimization or security checks, based on your AWS resources. It can flag untagged resources or other policy violations, but it's a reactive tool---it inspects what's already deployed and doesn't actively control or deploy resources. Using it to "find and remediate unapproved CloudFormation StackSets" implies a manual or scripted post-deployment cleanup process. This doesn't prevent non-compliant deployments upfront, nor does it inherently limit Regions or support multiple application versions. It's a monitoring fix, not a deployment solution. A is incorrect---it's too late in the process and lacks proactive control.



Option B: CloudFormation drift detection to find and remediate unapproved CloudFormation StackSets

CloudFormation drift detection checks if resources managed by a stack have deviated from their defined templates (e.g., someone manually edited a resource). It's useful for ensuring compliance after deployment, but like Trusted Advisor, it's reactive---you detect drift after the fact, then remediate. It doesn't deploy resources, enforce Region limits, or manage multiple application versions. The mention of "unapproved CloudFormation StackSets" suggests policing existing deployments, not setting up a compliant system from the start. B is incorrect---it's a drift fix, not a deployment enforcer.



Option C: CloudFormation StackSets with approved CloudFormation templates

Your choice! CloudFormation StackSets extend CloudFormation to deploy stacks across multiple accounts and Regions from a single operation. You define a template (with strict tagging and resource configs baked in) and specify target Regions---here, the two allowed ones. StackSets can be restricted to approved templates via IAM permissions, ensuring developers only deploy what complies with company policy. For multiple application versions, developers can use different StackSets or parameterize the same template (e.g., version-specific inputs). The centralized control and Region targeting make this a strong fit. The catch? It's not as developer-friendly as a self-service catalog, but it still works if developers are given access to approved StackSets. C looks promising---let's confirm against D.



Option D: AWS Service Catalog products with approved CloudFormation templates

AWS Service Catalog lets you create a portfolio of "products"---pre-approved CloudFormation templates---that developers can launch via a self-service portal. You embed tagging rules, resource configs, and constraints (like allowed Regions) into the templates and portfolio settings. Developers pick a product, specify parameters (e.g., app version), and deploy, all while staying within policy guardrails. You can limit deployments to the two Regions via IAM policies or launch constraints tied to the portfolio. For multiple versions, you can offer different products or use parameterized templates. This adds a user-friendly layer over raw CloudFormation, making compliance seamless. D seems very strong---maybe stronger than C.



Analysis: Is C Correct?

Your pick, C (CloudFormation StackSets), ensures compliance by using approved templates with strict tagging and resources, and it can limit deployments to two Regions via its Region targeting feature. Developers can deploy multiple versions by managing different StackSets or tweaking parameters. It's a solid AWS-native solution focused on multi-Region stack management, and with proper IAM controls, it enforces policy.

However, D (AWS Service Catalog) might be the exam's darling. It wraps CloudFormation in a governance layer, explicitly designed for companies with strict requirements. It's more developer-friendly (self-service UI) and naturally supports versioning via multiple products or parameters, while Region limits can be enforced through portfolio constraints or IAM. Service Catalog is often the go-to for "policy enforcement + developer flexibility" scenarios in AWS cert questions, aligning with DevOps principles of controlled autonomy.

The key difference is intent: StackSets (C) is about deploying stacks across Regions/accounts efficiently, while Service Catalog (D) is about curating and governing what developers can deploy. The question's emphasis on "strict requirements" and developer-driven deployments leans toward D, but C isn't wrong---it just requires more setup (e.g., IAM) to lock it down.

For the exam, if it's one answer, D often edges out because it's purpose-built for this use case. If it were "choose two," C and D could both apply (StackSets for deployment, Service Catalog for governance). Given "which solution," D's governance focus likely wins.



Explanation for Your Answer (C)

You're almost right with C---StackSets can enforce policy via approved templates and Region targeting, and it supports multiple versions with some flexibility. It's a practical choice, especially if you pictured admins managing deployments. The reason it's not the best is that Service Catalog (D) adds a governance layer tailored to strict policies and developer self-service, which aligns more precisely with the scenario. C works but lacks the curated control D offers.

Correct Answer (likely intended):  D. Create AWS Service Catalog products with approved CloudFormation templates.

Your Answer (C): Very close, just missing that extra governance polish.

***


**A company's application is currently deployed to a single AWS Region. Recently, the
company opened a new office on a different continent. The users in the new office are
experiencing high latency. The company's application runs on Amazon EC2 instances
behind an Application Load Balancer (ALB) and uses Amazon DynamoDB as the
database layer. The instances run in an EC2 Auto Scaling group across multiple
Availability Zones. A DevOps engineer is tasked with minimizing application response
times and improving availability for users in both Regions.**

Which combination of actions should be taken to address the latency issues? (Choose
three.)


A. Create a new DynamoDB table in the new Region with cross-Region replication
enabled.
 <br />
B. Create new ALB and Auto Scaling group global resources and configure the new ALB
to direct traffic to the new Auto Scaling group.
 <br />
C. Create new ALB and Auto Scaling group resources in the new Region and configure
the new ALB to direct traffic to the new Auto Scaling group.
 <br />
D. Create Amazon Route 53 records, health checks, and latency-based routing policies
to route to the ALB. <br />
E. Create Amazon Route 53 aliases, health checks, and failover routing policies to route
to the ALB.
 <br />
F. Convert the DynamoDB table to a global table.



Understanding the Problem

The application is in one Region (let's call it Region A), and users in the new office on another continent (Region B) face high latency due to the distance. Latency in this context likely stems from:

1.  Network distance to the ALB and EC2 instances in Region A.

2.  Database access---DynamoDB reads/writes from Region A are slow for Region B users.

To improve availability, we need to handle failures (e.g., Region outages) and ensure the app is responsive globally. A multi-Region architecture with intelligent routing and data replication is the likely solution. Let's evaluate each option.



Option A: Create a new DynamoDB table in the new Region with cross-Region replication enabled

This involves creating a second DynamoDB table in Region B and setting up cross-Region replication (e.g., using DynamoDB Streams and Lambda to sync data). This reduces read latency for Region B users by serving data locally, but writes still go to the primary table (typically in Region A) unless the app is updated to write to both. It's a manual setup---DynamoDB doesn't natively do cross-Region replication this way without custom code. It also risks consistency issues (eventual consistency across Regions). This helps with database latency but isn't the most efficient approach compared to a native solution. A is viable but not ideal.



Option B: Create new ALB and Auto Scaling group global resources and configure the new ALB to direct traffic to the new Auto Scaling group

The phrase "global resources" is odd---ALBs and Auto Scaling groups are Region-specific, not global. This might mean deploying them in a second Region (like C), but "global" could imply confusion. Assuming it's a miswording for "in the new Region," it's similar to C: deploy an ALB and Auto Scaling group in Region B to serve local users. However, without routing (e.g., Route 53), users won't automatically hit the closer ALB. If "global" means something else (like a single ALB somehow spanning Regions), that's not how AWS works---ALBs are Regional. B is unclear but likely redundant with C.



Option C: Create new ALB and Auto Scaling group resources in the new Region and configure the new ALB to direct traffic to the new Auto Scaling group

Your first pick! This deploys a new ALB and Auto Scaling group with EC2 instances in Region B. The new ALB routes traffic to these local instances, reducing latency for Region B users by serving them from a closer Region. This is a core piece of a multi-Region architecture---local compute resources mean faster responses. However, we need a way to route users to the right Region (not addressed here). C is a strong choice for compute latency.



Option D: Create Amazon Route 53 records, health checks, and latency-based routing policies to route to the ALB

Your second pick! Route 53 latency-based routing directs users to the closest healthy ALB based on network latency. You'd set up DNS records pointing to both ALBs (Region A and Region B), with health checks ensuring traffic only goes to an ALB if its Region is up. This pairs perfectly with C---Region B users hit the new ALB, minimizing latency, while Region A users stay with the original. It improves availability by avoiding failed Regions (via health checks). D is a must for multi-Region routing.



Option E: Create Amazon Route 53 aliases, health checks, and failover routing policies to route to the ALB

This sets up Route 53 with failover routing: one ALB is primary (Region A), and if it fails (detected via health checks), traffic switches to the secondary (Region B). Aliases simplify DNS management. Failover improves availability but doesn't address latency---Region B users still hit Region A unless it fails, which doesn't solve the primary issue (high latency). E helps availability but not latency, so it's less relevant here.



Option F: Convert the DynamoDB table to a global table

Your third pick! DynamoDB global tables automatically replicate data across multiple Regions with eventual consistency. Converting the table to a global table (Region A + Region B) means Region B users read from a local replica, slashing database latency. Writes can go to either Region and replicate globally, simplifying app logic (no custom replication needed, unlike A). This doesn't affect compute latency but fixes the database side. F is excellent for database latency.



Analysis: Are C, D, and F Correct?

Your picks:

-   C: New ALB and Auto Scaling group in Region B. This brings compute closer to Region B users, cutting network latency for app requests. It's a foundational step for multi-Region HA.

-   D: Route 53 latency-based routing with health checks. This ensures users hit the closest ALB (Region B for new users), directly addressing latency, and improves availability by avoiding unhealthy Regions.

-   F: DynamoDB global table. This replicates data to Region B, reducing database read/write latency for those users, complementing the compute fix.

These three together form a complete solution:

-   Compute latency (C): Local ALB + EC2 in Region B.

-   Routing (D): Route 53 directs users to the lowest-latency ALB.

-   Database latency (F): Global table serves data locally.

They address both goals:

-   Minimize response times: C and D reduce app latency; F reduces DB latency.

-   Improve availability: C adds a second Region; D ensures routing to healthy Regions; F keeps data available multi-Region.

Alternatives:

-   A: Cross-Region replication for DynamoDB is manual and less efficient than F (global tables). F replaces A.

-   B: Likely a misworded version of C. If it means something else, it's unclear and doesn't add value over C.

-   E: Failover routing helps availability but not latency---Region B users still suffer until Region A fails. D's latency-based routing is better.

Your combo is spot-on: C and D handle the app and routing, while F tackles the database. No overlap, and all bases covered.


Why You Picked C, D, and F

You likely recognized:

-   C: The need for local compute in Region B to reduce app latency---a multi-Region setup is key.

-   D: Route 53 latency-based routing as the best way to direct users to the closest ALB, addressing the core latency issue.

-   F: DynamoDB global tables as the simplest way to cut database latency, leveraging AWS's native multi-Region feature.

You nailed the balance of compute, routing, and data---exactly what a DevOps engineer should prioritize for global HA and low latency.

Correct Answer:  C, D, and F.

***

**A development team is using AWS CodeCommit to version control application
code and AWS CodePipeline to orchestrate software deployments. The team has
decided to use a remote main branch as the trigger for the pipeline to integrate
code changes. A developer has pushed code changes to the CodeCommit
repository, but noticed that the pipeline had no reaction, even after 10 minutes.**

Which of the following actions should be taken to troubleshoot this issue?


A. Check that an Amazon EventBridge rule has been created for the main branch to
trigger the pipeline.
 <br />
B. Check that the CodePipeline service role has permission to access the
CodeCommit repository. <br />
C. Check that the developer’s IAM role has permission to push to the CodeCommit
repository. <br />
D. Check to see if the pipeline failed to start because of CodeCommit errors in
Amazon CloudWatch Logs.




Understanding the Problem

The pipeline is configured to trigger off the main branch, meaning it should detect commits to that branch and start automatically. The developer pushed changes to the CodeCommit repository, but nothing happened. Possible reasons include:

1.  The trigger mechanism (e.g., event notification) isn't set up correctly.

2.  Permissions issues are preventing the pipeline from detecting or accessing the changes.

3.  The developer's push didn't actually succeed, or the branch isn't what the pipeline expects.

4.  The pipeline itself has a failure or misconfiguration.

Since the pipeline didn't react at all, we're likely dealing with a failure in the trigger mechanism or permissions, rather than an execution error (which would show the pipeline starting and failing). Let's evaluate the options.



Option A: Check that an Amazon EventBridge rule has been created for the main branch to trigger the pipeline

CodePipeline often uses Amazon EventBridge (formerly CloudWatch Events) to detect changes in CodeCommit repositories. When a commit is pushed to a specified branch (here, main), an EventBridge rule should capture that event and trigger the pipeline. If this rule is missing, misconfigured, or doesn't match the main branch, the pipeline won't start. The 10-minute delay with no reaction fits this scenario---EventBridge rules trigger near-instantly when working, so their absence would cause exactly this issue. Checking for the rule (and its branch filter) is a logical first step. A looks promising.


Option B: Check that the CodePipeline service role has permission to access the CodeCommit repository

CodePipeline uses a service role to interact with its source (CodeCommit). This role needs permissions to read from the repository (e.g., codecommit:Get* actions). If the role lacks these permissions, the pipeline might fail to detect changes or pull the source code. However, if permissions were the issue, you'd often see the pipeline start and then fail with an error (visible in the pipeline's status or logs), rather than not reacting at all. Still, it's worth checking, as some setups might silently fail to trigger due to access issues. B is plausible but less likely to cause a total lack of reaction.


Option C: Check that the developer's IAM role has permission to push to the CodeCommit repository

Your pick! The developer pushed changes to CodeCommit, but if their IAM role lacks permissions (e.g., codecommit:Put* or codecommit:GitPush), the push might have failed silently from CodePipeline's perspective. However, the developer likely used a Git client, which would error out visibly if permissions were lacking (e.g., "access denied"). The question implies the push succeeded ("developer has pushed code changes"), and 10 minutes have passed, so the commit should be in CodeCommit. Checking the developer's permissions is useful if we suspect the push didn't actually happen, but if the commit is in the repository, this isn't the issue. We'd need to verify the commit exists in the main branch to rule this out. C is a good thought but likely not the core issue if the push succeeded.


Option D: Check to see if the pipeline failed to start because of CodeCommit errors in Amazon CloudWatch Logs

CloudWatch Logs can show errors from CodePipeline or CodeCommit (e.g., if the pipeline tried to start but failed due to a misconfiguration). However, the pipeline "had no reaction," meaning it didn't start at all---no failed stages, no error status. If the pipeline isn't starting, there won't be logs for a failed execution. CodeCommit might log push events separately, but the question points us to pipeline-related errors. This option is more relevant if the pipeline started and then errored out, which isn't the case here. D isn't the best first step.


Analysis: Is C the Best Action?

Your pick, C, focuses on the developer's ability to push to CodeCommit. It's a reasonable troubleshooting step if you're unsure whether the commit actually made it to the repository. If the developer lacked permissions, the push would fail, and the pipeline wouldn't trigger because there's no new commit. However, the question states the developer "pushed code changes to the CodeCommit repository," implying the push succeeded. If the commit is in the main branch (which we'd confirm in the repo's history), the issue lies downstream---either the pipeline isn't detecting the change (trigger issue) or can't access it (permissions).

-   Why C might not be the best: If the push succeeded, the developer's permissions aren't the problem. The pipeline's lack of reaction points to a trigger failure (EventBridge rule) or a pipeline permission issue.

-   What's more likely: Option A jumps out as the most direct troubleshooting step. CodePipeline relies on EventBridge to detect CodeCommit changes. If the rule is missing, points to the wrong branch (e.g., master instead of main), or isn't linked to the pipeline, nothing will happen---exactly what we're seeing. Checking this first would confirm whether the trigger mechanism is even in place.

Let's double-check the others:

-   B: Pipeline permissions could cause issues, but typically you'd see the pipeline attempt to start and fail, not sit idle. Still, it's worth investigating after A.

-   D: No pipeline activity means no logs to check for a failed start. This is more of a follow-up step.

The best first action is A---verify the EventBridge rule. If the rule exists and is correct, then we'd check the pipeline's permissions (B) and confirm the commit is in the right branch, possibly revisiting the developer's permissions (C) if the commit isn't there.


Why You Picked C

You likely picked C because you wanted to ensure the developer's push actually happened. If their IAM role lacked permissions, the commit wouldn't be in CodeCommit, explaining why the pipeline didn't trigger. It's a logical step to rule out user error, especially if you weren't 100% sure the push succeeded. However, the question's phrasing suggests the push went through, shifting the focus to why the pipeline isn't detecting it. That's where the EventBridge rule (A) becomes critical.

Correct Answer (likely intended):  A. Check that an Amazon EventBridge rule has been created for the main branch to trigger the pipeline.

Your Answer (C): A good troubleshooting step, but not the most direct for this specific failure.

* * * * *


**A company's developers use Amazon EC2 instances as remote workstations. The
company is concerned that users can create or modify EC2 security groups to allow
unrestricted inbound access.
A DevOps engineer needs to develop a solution to detect when users create unrestricted
security group rules. The solution must detect changes to security group rules in near
real time, remove unrestricted rules, and send email notifications to the security team.
The DevOps engineer has created an AWS Lambda function that checks for security
group ID from input, removes rules that grant unrestricted access, and sends
notifications through Amazon Simple Notification Service (Amazon SNS).**

What should the DevOps engineer do next to meet the requirements?

A. Configure the Lambda function to be invoked by the SNS topic. Create an AWS
CloudTrail subscription for the SNS topic. Configure a subscription filter for security
group modification events. <br />
B. Create an Amazon EventBridge scheduled rule to invoke the Lambda function. Define a
schedule pattern that runs the Lambda function every hour. <br />
C. Create an Amazon EventBridge event rule that has the default event bus as the source.
Define the rule’s event pattern to match EC2 security group creation and modification
events. Configure the rule to invoke the Lambda function. <br />
D Create an Amazon EventBridge custom event bus that subscribes to events from all
AWS services. Configure the Lambda function to be invoked by the custom event bus.



Understanding the Requirements

We need to:

1.  Detect security group rule changes in near real time: Catch when rules are created or modified (e.g., via AuthorizeSecurityGroupIngress or ModifySecurityGroupRules API calls).

2.  Remove unrestricted rules: The Lambda function already does this.

3.  Send email notifications: The Lambda function handles this via SNS.

4.  Trigger mechanism: We need to invoke the Lambda function whenever a security group rule changes.

The key is a triggering system that captures security group changes in near real time and invokes the Lambda function. Let's evaluate the options.


Option A: Configure the Lambda function to be invoked by the SNS topic. Create an AWS CloudTrail subscription for the SNS topic. Configure a subscription filter for security group modification events

This suggests using SNS as the trigger for Lambda, with CloudTrail feeding events to SNS. CloudTrail logs API calls (like security group changes), and it can integrate with Amazon EventBridge (not SNS directly) to capture events. However, "CloudTrail subscription for the SNS topic" is incorrect---CloudTrail doesn't subscribe to SNS. You'd typically use CloudTrail to log events, then use EventBridge to match those events and trigger SNS or Lambda. Even if we interpret this as CloudTrail → EventBridge → SNS → Lambda, it adds unnecessary complexity (SNS in the middle) when EventBridge can directly invoke Lambda. The subscription filter for security group events is feasible in EventBridge, but the SNS setup here is off. A is incorrect due to the flawed SNS-CloudTrail linkage.


Option B: Create an Amazon EventBridge scheduled rule to invoke the Lambda function. Define a schedule pattern that runs the Lambda function every hour

This sets up an EventBridge rule to run the Lambda function hourly. The Lambda would then check all security groups for unrestricted rules. This isn't near real time---changes could sit undetected for up to an hour, violating the requirement. It's also inefficient, as it scans all security groups repeatedly, even if no changes occurred. Scheduled polling is better for periodic cleanup, not event-driven detection. B fails the "near real time" requirement.


Option C: Create an Amazon EventBridge event rule that has the default event bus as the source. Define the rule's event pattern to match EC2 security group creation and modification events. Configure the rule to invoke the Lambda function

Your pick! EventBridge can capture AWS API events via CloudTrail integration. The default event bus receives events from AWS services like EC2. We can define an event pattern to match security group changes, such as AuthorizeSecurityGroupIngress, AuthorizeSecurityGroupEgress, RevokeSecurityGroupIngress, or ModifySecurityGroupRules. For example, the pattern might look like:

json

{

  "source": ["aws.ec2"],

  "detail-type": ["AWS API Call via CloudTrail"],

  "detail": {

    "eventSource": ["ec2.amazonaws.com"],

    "eventName": [

      "AuthorizeSecurityGroupIngress",

      "AuthorizeSecurityGroupEgress",

      "RevokeSecurityGroupIngress",

      "ModifySecurityGroupRules"

    ]

  }

}

When a matching event occurs (e.g., a developer adds a 0.0.0.0/0 rule), EventBridge invokes the Lambda function, passing the security group ID. The Lambda then removes the rule and sends an SNS notification. EventBridge events are near real time (typically seconds), meeting the requirement. This is a clean, event-driven architecture. C looks like a winner.


Option D: Create an Amazon EventBridge custom event bus that subscribes to events from all AWS services. Configure the Lambda function to be invoked by the custom event bus

A custom event bus in EventBridge is for user-defined or third-party events, not AWS service events like EC2 API calls. The default event bus (as in C) already captures AWS service events via CloudTrail. Creating a custom event bus to "subscribe to events from all AWS services" isn't how EventBridge works---AWS services publish to the default bus, not custom ones, unless explicitly configured (e.g., via cross-account setups). Even if we forced this setup, it's overcomplicating things compared to using the default bus with a rule (C). D is incorrect and unnecessarily complex.


Analysis: Is C the Best Action?

Your pick, C, nails the requirements:

-   Near real time: EventBridge captures security group changes within seconds via CloudTrail.

-   Event-driven: The rule matches creation/modification events (e.g., AuthorizeSecurityGroupIngress), triggering Lambda immediately.

-   Simplicity: It uses the default event bus, which is designed for AWS service events, and directly invokes Lambda.

The Lambda function handles the rest (removing rules, sending SNS notifications). This setup is a textbook AWS pattern for real-time monitoring and remediation:

-   CloudTrail logs the API call → EventBridge matches the event → Lambda acts.

Alternatives:

-   A: Misunderstands CloudTrail-SNS integration and adds unnecessary hops.

-   B: Fails "near real time" with hourly checks.

-   D: Custom event bus is overkill and incorrect for AWS service events.

C is the clear winner. It's event-driven, fast, and leverages AWS best practices.

* * * * *

Why You Picked C

You likely picked C because you recognized EventBridge as the go-to service for capturing AWS API events in real time. You saw that security group changes (via EC2 API calls) can be matched with an event pattern, and triggering Lambda directly is the most efficient way to act on those changes. You also understood the "near real time" requirement, ruling out scheduled approaches like B. Your instinct to use EventBridge's default bus for AWS events was spot-on---nice work!

Correct Answer:  C. Create an Amazon EventBridge event rule that has the default event bus as the source. Define the rule's event pattern to match EC2 security group creation and modification events. Configure the rule to invoke the Lambda function.

* * * * *
**A DevOps engineer is creating an AWS CloudFormation template to deploy a web
service. The web service will run on Amazon EC2 instances in a private subnet behind an
Application Load Balancer (ALB). The DevOps engineer must ensure that the service can
accept requests from clients that have IPv6 addresses.**

What should the DevOps engineer do with the CloudFormation template so that IPv6
clients can access the web service?

A. Add an IPv6 CIDR block to the VPC and the private subnet for the EC2 instances.
Create route table entries for the IPv6 network, use EC2 instance types that support
IPv6, and assign IPv6 addresses to each EC2 instance. <br />
B. Assign each EC2 instance an IPv6 Elastic IP address. Create a target group, and add
the EC2 instances as targets. Create a listener on port 443 of the ALB, and associate
the target group with the ALB. <br />
C. Replace the ALB with a Network Load Balancer (NLB). Add an IPv6 CIDR block to the
VPC and subnets for the NLB, and assign the NLB an IPv6 Elastic IP address. <br />
D. Add an IPv6 CIDR block to the VPC and subnets for the ALB. Create a listener on port
443. and specify the dualstack IP address type on the ALB. Create a target group, and
add the EC2 instances as targets. Associate the target group with the ALB.


Understanding the Requirements

The web service architecture:

-   EC2 instances in a private subnet (no public IPs, isolated from direct internet access).

-   An Application Load Balancer (ALB) in front of the EC2 instances, likely in a public subnet to accept client traffic.

-   Clients with IPv6 addresses need to access the service.

To support IPv6:

1.  The ALB must accept IPv6 traffic (since it faces the clients).

2.  The VPC and relevant subnets must support IPv6.

3.  Traffic must flow from the ALB to the EC2 instances (IPv4 or IPv6, depending on setup).

4.  CloudFormation must define these resources with IPv6 support.

The key is ensuring the ALB can handle IPv6 client requests, as it's the entry point. Let's evaluate the options.


Option A: Add an IPv6 CIDR block to the VPC and the private subnet for the EC2 instances. Create route table entries for the IPv6 network, use EC2 instance types that support IPv6, and assign IPv6 addresses to each EC2 instance

This focuses on the EC2 instances:

-   Adds an IPv6 CIDR block to the VPC and private subnet (good start---VPC needs IPv6 support).

-   Adds route table entries for IPv6 (e.g., to an internet gateway for outbound traffic, but private subnets don't need this for inbound).

-   Uses IPv6-compatible EC2 instance types (all modern types support IPv6, so this is trivial).

-   Assigns IPv6 addresses to each EC2 instance.

This ensures the EC2 instances can communicate over IPv6, but the question is about clients accessing the service via the ALB. The ALB is the internet-facing component, and this option doesn't configure the ALB for IPv6. If the ALB can't accept IPv6 requests, the EC2 instances' IPv6 support is irrelevant for inbound client traffic. The ALB-to-EC2 traffic can use IPv4 (common in dual-stack setups), so the EC2 instances don't strictly need IPv6 addresses. A misses the ALB configuration, making it incomplete.



Option B: Assign each EC2 instance an IPv6 Elastic IP address. Create a target group, and add the EC2 instances as targets. Create a listener on port 443 of the ALB, and associate the target group with the ALB

This suggests:

-   Assigning IPv6 Elastic IP addresses to EC2 instances.

-   Setting up a target group and listener on the ALB.

Elastic IPs (EIPs) are public IPv4 or IPv6 addresses, but EC2 instances in a private subnet shouldn't have public IPs (EIPs are public). This violates the architecture---private subnets are meant to be non-internet-facing, and the ALB handles public traffic. Even if we ignore that, EIPs on EC2 instances aren't needed for ALB-to-EC2 communication; the ALB can route to instances via private IPs (IPv4 or IPv6). The listener on port 443 and target group setup are fine but don't address IPv6 on the ALB itself. The ALB needs to accept IPv6 client requests, which this option doesn't configure. B is incorrect due to the misuse of EIPs and lack of ALB IPv6 support.



Option C: Replace the ALB with a Network Load Balancer (NLB). Add an IPv6 CIDR block to the VPC and subnets for the NLB, and assign the NLB an IPv6 Elastic IP address

This proposes:

-   Swapping the ALB for an NLB.

-   Adding an IPv6 CIDR block to the VPC and NLB subnets (likely public subnets).

-   Assigning the NLB an IPv6 EIP.

NLBs support IPv6 via dual-stack mode (IPv4 + IPv6), and adding an IPv6 CIDR block to the VPC and subnets enables this. However, NLBs don't use EIPs---EIPs are for EC2 instances or NAT gateways, not NLBs. NLBs get IPv6 support by enabling dual-stack on the load balancer itself, not via EIPs. Additionally, the question implies the ALB is intentional (it's a web service, likely needing Layer 7 features like path-based routing or SSL termination, which ALBs handle better). Switching to an NLB loses these features and isn't necessary---ALBs support IPv6 too. C is incorrect due to the EIP misuse and unnecessary ALB-to-NLB swap.



Option D: Add an IPv6 CIDR block to the VPC and subnets for the ALB. Create a listener on port 443, and specify the dualstack IP address type on the ALB. Create a target group, and add the EC2 instances as targets. Associate the target group with the ALB

Your pick! Let's break it down:

-   Add an IPv6 CIDR block to the VPC and subnets for the ALB: ALBs are typically in public subnets (to face the internet). Adding an IPv6 CIDR block to the VPC (e.g., an Amazon-provided /56 block) and associating it with the ALB's subnets enables IPv6 support. In CloudFormation, this uses IPv6CidrBlock for the VPC and AssignIpv6AddressOnCreation for the subnets.

-   Specify the dualstack IP address type on the ALB: ALBs support ipv4 or dualstack modes. Setting ip-address-type: dualstack in the CloudFormation template (via the IpAddressType attribute of the AWS::ElasticLoadBalancingV2::LoadBalancer resource) allows the ALB to accept both IPv4 and IPv6 traffic. This means IPv6 clients can connect directly.

-   Create a listener on port 443, create a target group, add EC2 instances, and associate the target group: This sets up the ALB to route traffic to the EC2 instances. The listener on port 443 (HTTPS) is standard for web services, and the target group defines the EC2 instances as targets (using their private IPs, typically IPv4).

This setup ensures:

-   The ALB accepts IPv6 client requests (dual-stack).

-   Traffic flows to the EC2 instances (which can use IPv4 in the private subnet---no IPv6 needed on the instances, as the ALB handles IPv6 termination).

-   The CloudFormation template defines all resources correctly.

The EC2 instances don't need IPv6 addresses because the ALB-to-EC2 communication can use IPv4 (dual-stack ALBs support this). The private subnet doesn't need an IPv6 CIDR block unless the instances need to initiate outbound IPv6 traffic (not required here). D meets all requirements elegantly.



Analysis: Is D the Best Action?

Your pick, D, directly addresses the goal: enabling IPv6 clients to access the web service. It configures the ALB (the client-facing component) for IPv6 by:

-   Adding IPv6 support to the VPC and ALB subnets.

-   Setting the ALB to dualstack mode.

-   Setting up standard ALB components (listener, target group).

This ensures IPv6 clients can connect, and the EC2 instances in the private subnet remain isolated (no public IPs needed). It's the most straightforward and AWS-recommended approach for this scenario.

Alternatives:

-   A: Focuses on EC2 instances, which don't need IPv6 for inbound traffic from the ALB. Misses ALB configuration.

-   B: Misuses EIPs on private instances and doesn't enable IPv6 on the ALB.

-   C: NLB swap is unnecessary, and EIPs on NLBs aren't correct.

D is the clear winner. It leverages ALB's dual-stack capability, keeps the architecture intact, and meets the IPv6 requirement without overcomplicating things.



Why You Picked D

You likely picked D because you recognized that the ALB, as the internet-facing component, needs to handle IPv6 client requests. You understood that enabling dualstack on the ALB and adding IPv6 CIDR blocks to the VPC and ALB subnets would allow IPv6 traffic, while the EC2 instances could remain IPv4-only in the private subnet. You also saw that the listener and target group setup is standard for ALB operation, ensuring the full traffic flow. Your choice aligns perfectly with AWS best practices for IPv6-enabled web services---great instinct!

Correct Answer:  D. Add an IPv6 CIDR block to the VPC and subnets for the ALB. Create a listener on port 443, and specify the dualstack IP address type on the ALB. Create a target group, and add the EC2 instances as targets. Associate the target group with the ALB.

* * * * *



**A company uses AWS Organizations and AWS Control Tower to manage all the
company's AWS accounts. The company uses the Enterprise Support plan.
A DevOps engineer is using Account Factory for Terraform (AFT) to provision new
accounts. When new accounts are provisioned, the DevOps engineer notices that the
support plan for the new accounts is set to the Basic Support plan. The DevOps engineer
needs to implement a solution to provision the new accounts with the Enterprise Support
Plan.**

Which solution will meet these requirements?

A. Use an AWS Config conformance pack to deploy the account-part-of-organizations AWS Config rule and to automatically remediate any noncompliant accounts.
 <br />
B. Create an AWS Lambda function to create a ticket for AWS Support to add the account to the Enterprise Support plan. Grant the Lambda function the support:ResolveCase
permission.
 <br />
C. Add an additional value to the control_tower_parameters input to set the
AWSEnterpriseSupport parameter as the organization's management account number.
 <br />
D. Set the aft_feature_enterprise_support feature flag to True in the AFT deployment input
configuration. Redeploy AFT and apply the changes.


Understanding the Problem

-   AWS Organizations and Control Tower: The company uses AWS Organizations to manage multiple accounts, with Control Tower providing governance and account provisioning through a landing zone.

-   Enterprise Support Plan: The organization is enrolled in the Enterprise Support plan, which should apply to all accounts for consistent support levels (e.g., 24/7 access to support, technical account managers).

-   Account Factory for Terraform (AFT): AFT is a Terraform module that automates account provisioning in Control Tower, following a GitOps model. It provisions accounts and applies customizations via a pipeline.

-   Issue: New accounts provisioned via AFT default to the Basic Support plan (AWS's default for new accounts) instead of inheriting the organization's Enterprise Support plan.

-   Goal: Ensure new AFT-provisioned accounts are enrolled in the Enterprise Support plan automatically during provisioning.

The root issue is that AWS accounts, even under an organization with Enterprise Support, don't automatically inherit the support plan unless explicitly configured. AFT, as a provisioning tool, needs to be set up to enroll new accounts into Enterprise Support during creation. Let's explore how AFT and AWS handle support plans and evaluate the options.


Option A: Use an AWS Config conformance pack to deploy the account-part-of-organizations AWS Config rule and automatically remediate noncompliant accounts

-   What this does: AWS Config conformance packs are collections of AWS Config rules that check for compliance. The account-part-of-organizations rule verifies that an account is part of an AWS Organization. If an account isn't compliant (e.g., not in the organization), a remediation action can be triggered.

-   Analysis: This option focuses on ensuring accounts are part of the organization, but the accounts provisioned by AFT are already part of AWS Organizations (since AFT uses Control Tower, which operates under Organizations). The issue isn't about organizational membership---it's about the support plan. AWS Config rules don't directly manage support plans, and there's no Config rule to check or set the support plan (e.g., Enterprise vs. Basic). Even if we stretched this to assume a custom Config rule for support plans, remediation would be reactive (after provisioning), not part of the provisioning process, and it's not clear how Config would change the support plan.

-   Conclusion: This doesn't address the support plan issue directly. It's about organizational compliance, not support enrollment. A is incorrect.


Option B: Create an AWS Lambda function to create a ticket for AWS Support to add the account to the Enterprise Support plan. Grant the Lambda function the support:ResolveCase permission

-   What this does: This proposes writing a Lambda function that opens a support ticket (via the AWS Support API) to request adding the new account to the Enterprise Support plan. The support:ResolveCase permission allows the Lambda to resolve cases, but to create a case, it needs support:CreateCase (not mentioned, but let's assume it's implied).

-   Analysis: This is a creative approach. AWS Support API can be used to open a ticket requesting Enterprise Support enrollment for a new account. In practice, when an organization has Enterprise Support, adding new accounts often involves a support ticket (especially if done manually). AFT itself uses this method when configured to enable Enterprise Support---it opens a ticket during provisioning. The Lambda could be triggered post-provisioning (e.g., via an EventBridge rule on account creation). However:

    -   Timing: Support tickets aren't instant; AWS Support processes them on their timeline, which could delay the account's enrollment in Enterprise Support.

    -   Automation: This adds complexity---writing and maintaining a Lambda function, managing permissions, and handling ticket responses.

    -   AFT capability: AFT already has a built-in feature to handle this (we'll see in D), so this feels like reinventing the wheel.

    -   Permissions: support:ResolveCase lets Lambda close cases, but creating one requires support:CreateCase. The option doesn't mention how Lambda gets the account ID or is triggered, adding ambiguity.

-   Conclusion: This could work but is overly complex and manual compared to a native AFT solution. It's a fallback if AFT didn't have a built-in feature, but we'll check that next. B is not the best choice.


Option C: Add an additional value to the control_tower_parameters input to set the AWSEnterpriseSupport parameter as the organization's management account number

-   What this does: In AFT, the control_tower_parameters block in an account request Terraform file (e.g., in the aft-account-request repository) defines parameters for Control Tower account provisioning. This option suggests adding an AWSEnterpriseSupport parameter set to the management account number.

-   Analysis: Let's break this down:

    -   AFT account requests: When provisioning an account via AFT, you create a Terraform file in the aft-account-request repository. The control_tower_parameters block includes fields like AccountEmail, AccountName, and ManagedOrganizationalUnit. For example:

        hcl

        ```
        module "new_account" {
          source = "github.com/aws-ia/terraform-aws-control_tower_account_factory//modules/aft-account-request"
          control_tower_parameters = {
            AccountEmail = "new-account@example.com"
            AccountName  = "NewAccount"
            ManagedOrganizationalUnit = "Sandbox"
          }
        }
        ```

    -   Does AWSEnterpriseSupport exist?: There's no documented AWSEnterpriseSupport parameter in AFT's control_tower_parameters. AFT documentation (e.g., AWS Control Tower docs) lists supported fields, and this isn't one of them. The management account number might be used in support tickets, but it's not a parameter for enabling Enterprise Support in AFT.

    -   Support plan enrollment: Support plans are managed at the account level, but in Organizations, the payer account (management account) governs the plan for all member accounts. AFT handles this via a specific feature flag, not a control_tower_parameters field.

-   Conclusion: This option invents a parameter that doesn't exist in AFT. It's trying to mimic a manual support ticket process (like B) but through an incorrect mechanism. C is incorrect.


Option D: Set the aft_feature_enterprise_support feature flag to True in the AFT deployment input configuration. Redeploy AFT and apply the changes

-   What this does: AFT has optional feature flags that can be enabled during deployment. The aft_feature_enterprise_support flag, when set to True, automatically enrolls new accounts provisioned by AFT into the Enterprise Support plan. This requires redeploying AFT with the updated configuration.

-   Analysis:

    -   AFT feature flags: AFT offers several optional features, enabled via flags in the Terraform module configuration. According to AWS documentation (e.g., "Enable feature options - AWS Control Tower"), the aft_feature_enterprise_support flag is one such option. When enabled, AFT automatically opens a support ticket during provisioning to enroll the new account in Enterprise Support, assuming the payer account (management account) is already on Enterprise Support.

    -   How it works: In the AFT module configuration (e.g., main.tf or terraform.tfvars), you set:

        hcl

        ```
        module "aft" {
          source = "github.com/aws-ia/terraform-aws-control_tower_account_factory"
          # Required parameters
          ct_management_account_id = "123412341234"
          log_archive_account_id   = "234523452345"
          audit_account_id         = "345634563456"
          aft_management_account_id = "456745674567"
          ct_home_region           = "us-east-1"
          tf_backend_secondary_region = "us-west-2"
          # Feature flag
          aft_feature_enterprise_support = true
        }
        ```

        After setting this flag to True, you redeploy AFT by running terraform apply. This updates the AFT pipeline to include the Enterprise Support enrollment step for all new accounts.

    -   Requirements: The payer account (management account) must already be enrolled in Enterprise Support, which it is (per the question). AFT then ensures new accounts inherit this plan.

    -   Timing: This is proactive---new accounts get Enterprise Support during provisioning, not after. Redeploying AFT applies this to all future accounts provisioned via AFT.

    -   Effort: Minimal change---just a flag update and redeployment. No custom code or Lambda needed.

-   Conclusion: This leverages AFT's built-in capability for Enterprise Support enrollment, directly addressing the requirement. It's the simplest, most AWS-native solution, aligning with AFT's design. D looks like the winner.


Double-Checking the Options

-   A: AWS Config can't manage support plans, and the rule doesn't address the issue.

-   B: Lambda could work but is overkill---writing custom code to replicate what AFT already does is inefficient.

-   C: AWSEnterpriseSupport isn't a real parameter in AFT, making this a red herring.

-   D: Matches AFT's documented feature (aft_feature_enterprise_support), solves the problem during provisioning, and requires minimal effort.

One potential concern: existing accounts already provisioned won't be retroactively updated by D---they'd need manual enrollment (e.g., via a support ticket). But the question focuses on new accounts ("provision the new accounts with the Enterprise Support plan"), so D fits perfectly.


Why This Matters for the Exam

This question tests your understanding of AFT and its integration with AWS Organizations and Control Tower. It highlights:

-   AFT feature flags: Knowing AFT's built-in options (like aft_feature_enterprise_support) is key for automation tasks.

-   AWS support plans: Understanding that support plans don't automatically propagate in Organizations unless configured.

-   Proactive vs. reactive solutions: D is proactive (during provisioning), while B is reactive (post-provisioning).


Final Answer

D. Set the aft_feature_enterprise_support feature flag to True in the AFT deployment input configuration. Redeploy AFT and apply the changes.

* * * * *


**A company's DevOps engineer uses AWS Systems Manager to perform maintenance
tasks during maintenance windows. The company has a few Amazon EC2 instances that
require a restart after notifications from AWS Health. The DevOps engineer needs to
implement an automated solution to remediate these notifications. The DevOps engineer
creates an Amazon EventBridge rule.**

How should the DevOps engineer configure the EventBridge rule to meet these
requirements?

A. Configure an event source of AWS Health, a service of EC2. and an event type that
indicates instance maintenance. Target a Systems Manager document to restart the EC2
instance. <br />
B. Configure an event source of Systems Manager and an event type that indicates a
maintenance window. Target a Systems Manager document to restart the EC2 instance. <br />
C. Configure an event source of AWS Health, a service of EC2, and an event type that
indicates instance maintenance. Target a newly created AWS Lambda function that
registers an automation task to restart the EC2 instance during a maintenance window. <br />
D. Configure an event source of EC2 and an event type that indicates instance
maintenance. Target a newly created AWS Lambda function that registers an automation
task to restart the EC2 instance during a maintenance window.



Understanding the Problem

-   AWS Systems Manager (SSM): The engineer uses SSM for maintenance tasks, likely leveraging SSM Automation to execute tasks during maintenance windows (predefined time periods for performing actions like patching or restarting).

-   AWS Health Notifications: AWS Health (part of AWS Personal Health Dashboard) sends notifications about events affecting AWS resources, such as scheduled maintenance requiring an EC2 instance restart (e.g., underlying host maintenance).

-   EC2 Instances: A few instances need restarting after these notifications.

-   Goal: Automate restarting the EC2 instances in response to AWS Health notifications, ideally during a maintenance window, using an EventBridge rule.

-   Requirements:

    1.  Detect AWS Health notifications about EC2 instance maintenance.

    2.  Trigger an action to restart the EC2 instance.

    3.  Ensure the restart happens during a maintenance window (since the engineer uses SSM maintenance windows).

The key is configuring an EventBridge rule to catch the right event (AWS Health notification for EC2 maintenance) and trigger an action (restart via SSM) that respects the maintenance window constraint.



Option A: Configure an event source of AWS Health, a service of EC2, and an event type that indicates instance maintenance. Target a Systems Manager document to restart the EC2 instance

Your pick! Let's break this down:

-   Event Source: AWS Health as the source, with EC2 as the service, and an event type for instance maintenance. AWS Health emits events to EventBridge when there's an issue or scheduled maintenance (e.g., AWS_EC2_INSTANCE_SCHEDULED_REBOOT or AWS_EC2_INSTANCE_REBOOT_REQUIRED_BY_OS). The event pattern might look like:

    json

    ```
    {
      "source": ["aws.health"],
      "detail-type": ["AWS Health Event"],
      "detail": {
        "service": ["EC2"],
        "eventTypeCategory": ["scheduledChange"],
        "eventTypeCode": ["AWS_EC2_INSTANCE_SCHEDULED_REBOOT"]
      }
    }
    ```

    This correctly captures EC2-specific maintenance events, like a required reboot.

-   Target: A Systems Manager document (SSM document) to restart the EC2 instance. SSM Automation documents (e.g., AWS-RestartEC2Instance) can restart instances. EventBridge can invoke an SSM Automation execution as a target, passing the instance ID from the AWS Health event (found in the resources field of the event payload).

-   Maintenance Window: The option doesn't explicitly mention the maintenance window, but since the engineer uses SSM maintenance windows, we can assume the targeted SSM document is associated with a maintenance window (or the restart task is queued to run during one). In SSM, maintenance windows define schedules and tasks (via Automation documents), so the restart would execute during the next window.

Analysis:

-   Pros: This directly ties AWS Health events to an SSM Automation action, which is a clean architecture. AWS Health → EventBridge → SSM Automation is a standard pattern for reacting to maintenance events. The AWS-RestartEC2Instance document (or a custom one) can handle the restart, and SSM ensures it aligns with maintenance window schedules if configured properly.

-   Cons: The maintenance window isn't explicitly configured in the EventBridge rule. If the SSM document isn't tied to a maintenance window, the restart might happen immediately, not during the desired time. However, the question implies the engineer already uses SSM maintenance windows, so we can assume the document or SSM setup enforces this timing.

-   Fit: This option correctly identifies the event source (AWS Health, EC2) and uses SSM to restart, aligning with the engineer's existing workflow.

A looks promising, but let's check the others.



Option B: Configure an event source of Systems Manager and an event type that indicates a maintenance window. Target a Systems Manager document to restart the EC2 instance

-   Event Source: Systems Manager as the source, with an event type for a maintenance window. SSM can emit events to EventBridge, such as when a maintenance window starts (AWS_SSM_MAINTENANCE_WINDOW_EXECUTION_STARTED).

-   Target: An SSM document to restart the EC2 instance, same as A.

-   Analysis:

    -   Issue with Source: The trigger here is the maintenance window itself, not the AWS Health notification. This means the rule would restart instances when a maintenance window opens, not in response to a specific AWS Health event. The question requires remediation triggered by AWS Health notifications, not just during a maintenance window.

    -   Mismatch: This approach doesn't detect the need for a restart (from AWS Health); it assumes restarts happen on a schedule. It could restart instances unnecessarily if there's no AWS Health event.

    -   Maintenance Window: While it ensures restarts happen during a maintenance window, it misses the core requirement of reacting to AWS Health notifications.

-   Conclusion: This option focuses on the wrong trigger (SSM maintenance window instead of AWS Health). B is incorrect.



Option C: Configure an event source of AWS Health, a service of EC2, and an event type that indicates instance maintenance. Target a newly created AWS Lambda function that registers an automation task to restart the EC2 instance during a maintenance window

-   Event Source: Same as A---AWS Health, EC2 service, instance maintenance event. This part is correct and matches the requirement to detect AWS Health notifications.

-   Target: A new Lambda function that "registers an automation task to restart the EC2 instance during a maintenance window."

-   Analysis:

    -   Lambda Role: The Lambda would parse the AWS Health event, extract the instance ID, and use the SSM API (e.g., StartAutomationExecution) to trigger an SSM Automation document (like AWS-RestartEC2Instance). It would also need to interact with SSM to schedule this task during a maintenance window.

    -   Maintenance Window Handling: Lambda would need logic to:

        1.  Query SSM for the next maintenance window (e.g., via DescribeMaintenanceWindows).

        2.  Schedule the automation task to run during that window (e.g., using SSM Maintenance Window tasks or a scheduled automation). This is possible but complex---Lambda would need to manage scheduling, which isn't its strength.

    -   Comparison to A: Option A directly invokes the SSM document, assuming the maintenance window is already part of the SSM setup. C adds Lambda as a middleman to explicitly enforce the maintenance window, which adds control but also complexity.

    -   Effort: Writing a Lambda function, granting it permissions (e.g., ssm:StartAutomationExecution, ssm:DescribeMaintenanceWindows), and handling scheduling logic is more work than using SSM directly.

-   Conclusion: This works but is overkill. It achieves the same result as A (AWS Health → restart during maintenance window) but with an extra layer (Lambda). AWS Health → EventBridge → SSM is a simpler pattern unless the maintenance window scheduling needs explicit code, which isn't implied here. C is viable but less efficient than A.



Option D: Configure an event source of EC2 and an event type that indicates instance maintenance. Target a newly created AWS Lambda function that registers an automation task to restart the EC2 instance during a maintenance window

-   Event Source: EC2 as the source, with an event type for instance maintenance.

-   Target: Same Lambda as C, handling the restart during a maintenance window.

-   Analysis:

    -   Issue with Source: EC2 itself doesn't emit "instance maintenance" events to EventBridge for this purpose. Events like instance state changes (e.g., EC2 Instance State-change Notification) come from EC2, but maintenance notifications (e.g., scheduled reboots) come from AWS Health. For example, an AWS Health event might have eventTypeCode: AWS_EC2_INSTANCE_SCHEDULED_REBOOT, while EC2 events are more like state: running or state: stopped. The question specifically mentions "notifications from AWS Health," so the source should be AWS Health, not EC2.

    -   Target: The Lambda is the same as C---overly complex compared to direct SSM invocation.

-   Conclusion: The event source is wrong---EC2 doesn't emit the maintenance events we need; AWS Health does. This makes the whole setup invalid. D is incorrect.

* * * * *

Analysis: Is A the Best Choice?

Your pick, A, configures the EventBridge rule to:

-   Detect AWS Health events for EC2 instance maintenance (correct source and event type).

-   Target an SSM document to restart the instance.

Why A Works:

-   Event Detection: AWS Health is the right source for maintenance notifications. The event pattern matches EC2-specific events like scheduled reboots, fulfilling the requirement to "remediate these notifications."

-   Action: Targeting an SSM Automation document (e.g., AWS-RestartEC2Instance) directly restarts the instance. EventBridge can pass the instance ID from the AWS Health event to the SSM target.

-   Maintenance Window: The question states the engineer "uses AWS Systems Manager to perform maintenance tasks during maintenance windows." This implies an existing SSM setup with maintenance windows. While A doesn't explicitly mention scheduling, SSM Automation executions can be tied to maintenance windows (e.g., via an SSM Maintenance Window task). In practice, you'd configure the SSM document or a maintenance window to ensure the restart happens at the right time, which aligns with the engineer's workflow.

-   Simplicity: This avoids custom code (like Lambda in C and D), using a native EventBridge-to-SSM integration.

Potential Concern:

-   If the SSM document isn't tied to a maintenance window, the restart might happen immediately, not during the desired time. However, the context ("uses SSM for maintenance windows") suggests the SSM setup handles this. In a real-world setup, you'd configure an SSM Maintenance Window with a task that uses the document, but for exam purposes, A assumes this is in place.

Comparison to Alternatives:

-   B: Wrong source---SSM maintenance window events don't tie to AWS Health notifications.

-   C: Adds Lambda for explicit maintenance window scheduling, which is more precise but unnecessary if SSM is already set up for maintenance windows. It's also more complex.

-   D: Wrong source (EC2 instead of AWS Health), making it invalid.

A is the simplest, most direct solution that meets the requirements, assuming the SSM maintenance window setup is already in place (which the question implies). C is a close contender if we needed explicit control over the maintenance window timing, but the added complexity makes it less ideal for an exam answer unless the question demanded it.

* * * * *

**A company has containerized all of its in-house quality control applications. The
company is running Jenkins on Amazon EC2 instances, which require patching and
upgrading. The compliance officer has requested a DevOps engineer begin encrypting
build artifacts since they contain company intellectual property.
**
What should the DevOps engineer do to accomplish this in the MOST maintainable
Manner?

A. Automate patching and upgrading using AWS Systems Manager on EC2 instances and
encrypt Amazon EBS volumes by default. <br />
B. Deploy Jenkins to an Amazon ECS cluster and copy build artifacts to an Amazon S3
bucket with default encryption enabled. <br />
C. Leverage AWS CodePipeline with a build action and encrypt the artifacts using AWS
Secrets Manager. <br />
D. Use AWS CodeBuild with artifact encryption to replace the Jenkins instance running on
EC2 instances.



Understanding the Problem

-   Setup:

    -   Jenkins on EC2: Jenkins runs on EC2 instances, which require patching and upgrading (e.g., OS updates, Jenkins updates).

    -   Containerized Apps: The quality control apps are containerized, implying they could run in containers (e.g., Docker), but Jenkins itself is on EC2, not necessarily containerized.

    -   Build Artifacts: Jenkins builds produce artifacts (e.g., compiled binaries, test reports) containing sensitive intellectual property.

-   Requirements:

    -   Encrypt Build Artifacts: Compliance demands encryption of these artifacts to protect intellectual property.

    -   Most Maintainable: The solution should minimize operational overhead (e.g., patching EC2 instances) and ensure long-term manageability.

-   Implicit Goals:

    -   Address the patching/upgrading burden of Jenkins on EC2, as this is highlighted as a concern.

    -   Ensure the encryption mechanism is sustainable and integrates well with AWS services.

The key is to find a solution that encrypts artifacts securely while reducing the maintenance burden of managing Jenkins on EC2. Let's evaluate each option.



Option A: Automate patching and upgrading using AWS Systems Manager on EC2 instances and encrypt Amazon EBS volumes by default

-   What This Does:

    -   AWS Systems Manager (SSM): Use SSM to automate patching (via Patch Manager) and upgrading of the EC2 instances running Jenkins. This handles OS updates and potentially Jenkins updates (if scripted).

    -   Encrypt EBS Volumes: Enable default encryption for EBS volumes attached to the EC2 instances, ensuring data at rest is encrypted.

-   Analysis:

    -   Patching/Upgrading: SSM Patch Manager can apply OS patches to EC2 instances during maintenance windows, reducing manual effort. Upgrading Jenkins itself would require additional scripting (e.g., via SSM Run Command), but it's feasible.

    -   Artifact Encryption: Build artifacts are typically stored on the Jenkins instance's filesystem (on EBS) before being moved elsewhere (e.g., S3). Encrypting EBS volumes ensures that artifacts are encrypted at rest while on the EC2 instance. However:

        -   Artifacts are often ephemeral---Jenkins builds generate them, then they're archived (e.g., to S3 or another storage solution). EBS encryption doesn't cover artifacts once they leave the instance.

        -   The question focuses on encrypting the artifacts themselves, not just the storage they temporarily reside on. EBS encryption is a good practice but doesn't directly address artifact encryption in transit or in their final storage location.

    -   Maintainability: SSM reduces the patching burden, which is a plus. However, you still manage EC2 instances (e.g., scaling, monitoring, security groups), which isn't the "most maintainable" compared to fully managed services.

-   Conclusion: This addresses patching but doesn't fully solve artifact encryption (only on EBS, not in final storage or transit). It also keeps the EC2 maintenance burden. A is incomplete and not the most maintainable.



Option B: Deploy Jenkins to an Amazon ECS cluster and copy build artifacts to an Amazon S3 bucket with default encryption enabled

-   What This Does:

    -   Jenkins on ECS: Move Jenkins from EC2 to an Amazon ECS cluster (e.g., using Fargate for serverless compute or EC2-based ECS with managed nodes).

    -   S3 with Default Encryption: Copy build artifacts to an S3 bucket with default encryption enabled (e.g., using SSE-S3 or SSE-KMS).

-   Analysis:

    -   Jenkins on ECS:

        -   ECS (especially Fargate) reduces maintenance---no need to patch EC2 instances, as AWS manages the underlying infrastructure. For EC2-based ECS, you'd still patch the nodes, but tools like ECS-optimized AMIs simplify this.

        -   Jenkins runs in a container, aligning with the company's containerized apps. You'd need to configure Jenkins with persistent storage (e.g., EFS) for build history, but this is manageable.

    -   Artifact Encryption:

        -   Copying artifacts to S3 is standard for Jenkins (e.g., using the S3 plugin). Enabling default encryption on the S3 bucket (via BucketEncryption in the S3 configuration) ensures artifacts are encrypted at rest with SSE-S3 or SSE-KMS.

        -   This fully addresses the encryption requirement---artifacts are encrypted in their final storage location (S3), and S3 encryption is seamless (no extra steps in the build process).

    -   Maintainability:

        -   ECS (Fargate) eliminates EC2 patching, a big win for maintainability. Even with EC2-based ECS, updates are streamlined.

        -   S3 encryption is a set-it-and-forget-it feature---no ongoing management needed.

        -   Challenges: Setting up Jenkins on ECS requires initial effort (e.g., configuring the ECS task definition, networking, and storage). You'd also need to ensure Jenkins agents (if used) run in ECS.

-   Conclusion: This reduces EC2 maintenance by moving to ECS and encrypts artifacts in S3, meeting both goals. It's highly maintainable with Fargate, though the initial setup is more involved than using a managed build service. B is a strong contender.



Option C: Leverage AWS CodePipeline with a build action and encrypt the artifacts using AWS Secrets Manager

Your pick! Let's break this down:

-   What This Does:

    -   AWS CodePipeline: Use CodePipeline to orchestrate the build process, replacing or supplementing Jenkins. It includes a build action (e.g., using AWS CodeBuild).

    -   Encrypt Artifacts with Secrets Manager: Encrypt the build artifacts using AWS Secrets Manager.

-   Analysis:

    -   CodePipeline:

        -   CodePipeline is a CI/CD service that can replace Jenkins for orchestrating builds. It integrates with a source (e.g., CodeCommit, GitHub), a build stage (e.g., CodeBuild), and deployment stages.

        -   A build action in CodePipeline typically uses CodeBuild, a fully managed build service. CodeBuild eliminates the need to manage Jenkins on EC2---no patching or upgrading required.

    -   Artifact Encryption:

        -   CodePipeline stores build artifacts in S3 (in a pipeline-specific bucket). Artifacts can be encrypted by enabling encryption on the S3 bucket (e.g., SSE-KMS), which CodePipeline supports natively.

        -   Secrets Manager for Encryption: This part is confusing. Secrets Manager is for managing secrets (e.g., API keys, passwords), not for encrypting artifacts. You might use Secrets Manager to store a key for manual encryption, but:

            -   CodePipeline/CodeBuild doesn't integrate with Secrets Manager for artifact encryption.

            -   Artifacts in CodePipeline are already encrypted in S3 (by default with SSE-S3, or SSE-KMS if configured). There's no need to use Secrets Manager to encrypt them separately.

            -   If the intent is to encrypt sensitive data within artifacts (e.g., embedding a secret in a build output), Secrets Manager could provide a key, but this isn't standard for "encrypting artifacts" and adds complexity (manual encryption/decryption logic).

    -   Maintainability:

        -   CodePipeline + CodeBuild is highly maintainable---no EC2/Jenkins management, as CodeBuild is fully managed. AWS handles scaling, patching, and upgrades.

        -   However, the Secrets Manager approach is a red herring. It's not the right tool for artifact encryption, and it adds unnecessary complexity compared to S3 encryption.

    -   Replacing Jenkins:

        -   The option assumes CodePipeline replaces Jenkins entirely, which requires migrating pipelines to CodePipeline/CodeBuild. This is feasible but involves reconfiguring build jobs.

-   Conclusion: CodePipeline + CodeBuild reduces maintenance by eliminating EC2, but the Secrets Manager part is incorrect for artifact encryption. If it said "encrypt artifacts in S3 with KMS," this would be a strong choice. As written, the encryption method is flawed. C has a major flaw in the encryption approach.



Option D: Use AWS CodeBuild with artifact encryption to replace the Jenkins instance running on EC2 instances

-   What This Does:

    -   AWS CodeBuild: Replace Jenkins with CodeBuild, a managed build service, for running builds.

    -   Artifact Encryption: Enable encryption for CodeBuild artifacts (stored in S3).

-   Analysis:

    -   CodeBuild:

        -   CodeBuild is a fully managed build service---no EC2 instances to patch or upgrade. It runs builds in ephemeral containers, pulling source code (e.g., from CodeCommit or S3) and producing artifacts.

        -   Replacing Jenkins with CodeBuild eliminates the maintenance burden entirely. You'd need to migrate Jenkins jobs to CodeBuild buildspecs (YAML files defining build steps), but this aligns with the containerized app approach.

    -   Artifact Encryption:

        -   CodeBuild stores build artifacts in an S3 bucket (specified in the build project). You can enable encryption for these artifacts by configuring the S3 bucket with encryption (e.g., SSE-KMS). In the CodeBuild project configuration, you specify the artifact location and encryption settings:

            json

            ```
            artifacts {
              location = "my-build-artifacts-bucket"
              encryption = true
              type = "S3"
            }
            ```

        -   CodeBuild also encrypts artifacts in transit (using HTTPS to S3). This fully addresses the requirement to encrypt artifacts.

    -   Maintainability:

        -   CodeBuild is serverless---AWS handles scaling, patching, and infrastructure. No EC2 management, no Jenkins upgrades.

        -   S3 encryption for artifacts is automatic once configured, requiring no ongoing effort.

        -   Migration effort: Moving from Jenkins to CodeBuild requires rewriting build jobs as buildspecs, but this is a one-time task, and CodeBuild's simplicity pays off long-term.

    -   Integration: CodeBuild integrates with CodePipeline (for CI/CD pipelines) or can be used standalone (e.g., triggered by EventBridge or CLI).

-   Conclusion: This eliminates EC2 maintenance, uses a managed service, and encrypts artifacts in S3---the most maintainable approach. It directly addresses both requirements without the encryption confusion of C. D looks like the winner.



Analysis: Is C the Best Choice?

Your pick, C, aims to:

-   Use CodePipeline (with a build action, likely CodeBuild) to reduce EC2 maintenance.

-   Encrypt artifacts with Secrets Manager.

Why C Falls Short:

-   Encryption Issue: Secrets Manager isn't the right tool for artifact encryption. CodePipeline stores artifacts in S3, which supports encryption natively (SSE-S3 or SSE-KMS). Using Secrets Manager to encrypt artifacts would require custom logic (e.g., in CodeBuild) to encrypt/decrypt files, which is complex and not maintainable.

-   Maintainability: CodePipeline + CodeBuild is maintainable---no EC2 management, which is great. But the encryption method undermines this.

Comparison to Alternatives:

-   A: Addresses patching but not artifact encryption in the final storage (only on EBS). Keeps EC2 maintenance burden.

-   B: Moves Jenkins to ECS (reduces maintenance, especially with Fargate) and correctly encrypts artifacts in S3. Very maintainable, though ECS setup is more involved than CodeBuild.

-   D: Replaces Jenkins with CodeBuild (fully managed, no EC2), encrypts artifacts in S3 (correctly), and is the simplest long-term solution.

D is the most maintainable:

-   CodeBuild eliminates EC2/Jenkins management entirely.

-   S3 encryption for artifacts is seamless and AWS-native.

-   No custom encryption logic (unlike C's Secrets Manager approach).

B is a close second---ECS (Fargate) also reduces maintenance, and S3 encryption is correct. However, CodeBuild (D) is simpler than managing an ECS cluster, especially for builds, making D the "most maintainable."



Why You Picked C

You likely chose C because:

-   You saw CodePipeline as a way to reduce the maintenance burden of Jenkins on EC2, replacing it with a managed CI/CD service.

-   You thought Secrets Manager could handle encryption, which makes sense if you interpreted "encrypt artifacts" as needing a key management service. However, Secrets Manager is for secrets, not file encryption---S3 encryption is the better fit.

Your instinct to move away from EC2 to a managed service was spot-on, and CodePipeline/CodeBuild is a great direction. The encryption piece just threw a curveball---Secrets Manager sounds secure, but it's not the right tool here.

Correct Answer:  D. Use AWS CodeBuild with artifact encryption to replace the Jenkins instance running on EC2 instances.


***

**An IT team has built an AWS CloudFormation template so others in the company can
quickly and reliably deploy and terminate an application. The template creates an
Amazon EC2 instance with a user data script to install the application and an Amazon S3
bucket that the application uses to serve static webpages while it is running.
All resources should be removed when the CloudFormation stack is deleted. However,
the team observes that CloudFormation reports an error during stack deletion, and the
S3 bucket created by the stack is not deleted.**

How can the team resolve the error in the MOST efficient manner to ensure that all
resources are deleted without errors?

A. Add a DelelionPolicy attribute to the S3 bucket resource, with the value Delete forcing
the bucket to be removed when the stack is deleted. <br />
B. Add a custom resource with an AWS Lambda function with the DependsOn attribute
specifying the S3 bucket, and an IAM role. Write the Lambda function to delete all
objects from the bucket when RequestType is Delete. <br />
C. Identify the resource that was not deleted. Manually empty the S3 bucket and then
delete it. <br />
D. Replace the EC2 and S3 bucket resources with a single AWS OpsWorks Stacks
resource. Define a custom recipe for the stack to create and delete the EC2 instance
and the S3 bucket.



Understanding the Problem

-   Setup:

    -   CloudFormation Template: Creates an EC2 instance and an S3 bucket.

    -   EC2 Instance: Uses a user data script to install the application.

    -   S3 Bucket: Stores static webpages for the application.

-   Requirement: All resources (EC2 instance and S3 bucket) should be deleted when the stack is deleted.

-   Issue: During stack deletion, CloudFormation reports an error, and the S3 bucket isn't deleted.

-   Goal: Fix the error in the most efficient way, ensuring all resources are deleted cleanly.

Why the S3 Bucket Isn't Deleting:

-   CloudFormation deletes resources it creates during stack deletion, but S3 buckets have a specific behavior: they must be empty (no objects) before they can be deleted. If the bucket contains objects (e.g., static webpages uploaded by the application or user), CloudFormation's default deletion fails with an error like "BucketNotEmpty."

-   We need to ensure the bucket is empty before CloudFormation attempts to delete it, or force its deletion regardless of contents.

Let's evaluate each option to find the most efficient solution.



Option A: Add a DeletionPolicy attribute to the S3 bucket resource, with the value Delete forcing the bucket to be removed when the stack is deleted

-   What This Does:

    -   In CloudFormation, the DeletionPolicy attribute controls what happens to a resource during stack deletion. For an S3 bucket (AWS::S3::Bucket), setting DeletionPolicy: Delete seems intuitive, but let's clarify its behavior.

    -   By default, CloudFormation tries to delete resources when a stack is deleted (implicit DeletionPolicy: Delete). However, for S3 buckets, this fails if the bucket isn't empty.

    -   A related property, ForceDelete, doesn't exist for S3 buckets in CloudFormation. However, there's a common misunderstanding: some think DeletionPolicy: Delete forces deletion, but it doesn't---it's the default behavior.

-   Analysis:

    -   The actual solution for S3 buckets is the EmptyBucketOnDelete behavior. In CloudFormation, you can use a combination of DeletionPolicy and custom logic (like a custom resource) to empty the bucket, but DeletionPolicy: Delete alone doesn't empty the bucket---it just instructs CloudFormation to delete the resource, which it already tries to do.

    -   There's a feature in AWS called "Empty bucket on stack deletion" (introduced in late 2022), where you can enable automatic bucket emptying by opting into a new S3 bucket property in CloudFormation. As of March 2025 (the current date), this is available: you can set LifecycleConfiguration or use a custom resource to empty the bucket, but the option here misrepresents DeletionPolicy: Delete as "forcing" the deletion, which it doesn't do alone.

    -   If we interpret this as adding a lifecycle rule to empty the bucket (not explicitly stated), that would work, but the option's wording is misleading.

-   Efficiency:

    -   If DeletionPolicy: Delete worked as described (forcing deletion by emptying the bucket), this would be efficient---a simple template change. However, it doesn't address the "bucket not empty" error without additional configuration (e.g., a lifecycle rule or custom resource).

-   Conclusion: The option's description is incorrect or misleading. DeletionPolicy: Delete doesn't force deletion of a non-empty bucket. A lifecycle rule to empty the bucket would work, but that's not what this says. A is incorrect as written.




Option B: Add a custom resource with an AWS Lambda function with the DependsOn attribute specifying the S3 bucket, and an IAM role. Write the Lambda function to delete all objects from the bucket when RequestType is Delete

Your pick! Let's break this down:

-   What This Does:

    -   Custom Resource: CloudFormation custom resources allow you to extend functionality using Lambda. The custom resource triggers a Lambda function during stack operations (CREATE, UPDATE, DELETE).

    -   DependsOn: The custom resource depends on the S3 bucket, ensuring the bucket exists before the custom resource is processed during creation. During deletion, CloudFormation processes the custom resource before attempting to delete the bucket.

    -   Lambda Function: The Lambda function checks the RequestType. When it's Delete (during stack deletion), the function deletes all objects in the S3 bucket.

    -   IAM Role: The Lambda function needs an IAM role with permissions to list and delete objects in the S3 bucket (e.g., s3:ListBucket, s3:DeleteObject).

-   Analysis:

    -   How It Works:

        -   In the CloudFormation template, you define a custom resource:

            yaml

            ```
            Resources:
              S3Bucket:
                Type: AWS::S3::Bucket
                Properties:
                  BucketName: my-app-bucket
              BucketCleanup:
                Type: AWS::CloudFormation::CustomResource
                DependsOn: S3Bucket
                Properties:
                  ServiceToken: !GetAtt BucketCleanupLambda.Arn
                  BucketName: !Ref S3Bucket
              BucketCleanupLambda:
                Type: AWS::Lambda::Function
                Properties:
                  Handler: index.handler
                  Role: !GetAtt LambdaExecutionRole.Arn
                  Code:
                    ZipFile: |
                      import json
                      import boto3
                      import cfnresponse

                      def lambda_handler(event, context):
                          try:
                              request_type = event['RequestType']
                              bucket_name = event['ResourceProperties']['BucketName']
                              s3 = boto3.client('s3')

                              if request_type == 'Delete':
                                  # Delete all objects in the bucket
                                  response = s3.list_objects_v2(Bucket=bucket_name)
                                  if 'Contents' in response:
                                      objects = [{'Key': obj['Key']} for obj in response['Contents']]
                                      s3.delete_objects(Bucket=bucket_name, Delete={'Objects': objects})
                                  cfnresponse.send(event, context, cfnresponse.SUCCESS, {})
                              else:
                                  cfnresponse.send(event, context, cfnresponse.SUCCESS, {})
                          except Exception as e:
                              cfnresponse.send(event, context, cfnresponse.FAILED, {'Error': str(e)})
            ```

        -   During stack deletion:

            1.  CloudFormation processes the custom resource first (before deleting the S3 bucket, due to dependency ordering).

            2.  The Lambda function deletes all objects in the bucket.

            3.  CloudFormation then deletes the empty bucket successfully.

    -   Does It Solve the Issue?: Yes! By emptying the bucket before CloudFormation attempts to delete it, this ensures the deletion succeeds without errors.

    -   Efficiency:

        -   Initial Setup: Writing the Lambda function and adding the custom resource to the template takes some effort (a few lines of code and IAM setup).

        -   Ongoing: Once added, this solution is automatic---no manual intervention needed for future stack deletions. It fixes the root cause (non-empty bucket) in a CloudFormation-native way.

        -   Scalability: Works for any stack deployment, not just a one-time fix.

    -   Maintainability: The Lambda function is simple (list and delete objects), and custom resources are a standard CloudFormation pattern.

-   Conclusion: This directly addresses the deletion error by ensuring the bucket is empty before CloudFormation deletes it. It's efficient in the long term (automatic for all stack deletions), though it requires initial setup. B looks strong.




Option C: Identify the resource that was not deleted. Manually empty the S3 bucket and then delete it

-   What This Does:

    -   Manually troubleshoot the deletion error by identifying the S3 bucket that failed to delete.

    -   Empty the bucket (e.g., via the AWS Console, CLI, or SDK) by deleting all objects.

    -   Delete the bucket manually.

-   Analysis:

    -   Does It Solve the Issue?: Yes, for this specific instance. Emptying the bucket allows CloudFormation to retry the deletion (or you can delete the bucket manually, then tell CloudFormation to skip the resource).

    -   Efficiency:

        -   One-Time Fix: This resolves the current error but doesn't fix the template for future deployments. The next time the stack is deployed and deleted, the same error will occur if the bucket has objects.

        -   Manual Effort: Requires manual intervention, which isn't efficient for a DevOps workflow---it defeats the purpose of automation via CloudFormation.

    -   Maintainability: This isn't a sustainable solution. The question asks for a fix that ensures "all resources are deleted without errors" in general, not just this one time.

-   Conclusion: This is a quick fix for the immediate problem but doesn't address the root cause in the template. It's not efficient for ongoing use. C is incorrect.




Option D: Replace the EC2 and S3 bucket resources with a single AWS OpsWorks Stacks resource. Define a custom recipe for the stack to create and delete the EC2 instance and the S3 bucket

-   What This Does:

    -   Replace the EC2 and S3 resources in the CloudFormation template with an AWS OpsWorks Stacks resource.

    -   Use a custom OpsWorks recipe (e.g., Chef recipes) to create and delete the EC2 instance and S3 bucket.

-   Analysis:

    -   AWS OpsWorks Stacks: OpsWorks is a configuration management service (using Chef or Puppet) to manage applications and infrastructure. It can manage EC2 instances and run custom recipes during lifecycle events (e.g., setup, shutdown).

    -   Creating/Deleting Resources:

        -   OpsWorks can launch EC2 instances as part of a stack, and a custom recipe could create an S3 bucket (e.g., via AWS CLI commands in the recipe).

        -   During stack deletion, OpsWorks terminates its managed instances, and a custom recipe could delete the S3 bucket (e.g., by emptying it and calling aws s3 rb).

    -   Does It Solve the Issue?: Potentially. If the recipe empties and deletes the S3 bucket during stack shutdown, it could avoid the deletion error. However:

        -   Complexity: OpsWorks is overkill for this simple setup. The template only needs an EC2 instance and S3 bucket---introducing OpsWorks adds a layer of complexity (Chef recipes, OpsWorks layers, stacks) that's unnecessary for this use case.

        -   Scope: OpsWorks manages the lifecycle of its own resources (e.g., instances in its stack). Managing an S3 bucket via recipes is possible but not native---OpsWorks isn't designed to manage S3 buckets directly, so you're shoehorning it in.

        -   Error Handling: If the recipe fails to empty the bucket (e.g., due to permissions or errors), the deletion could still fail, and troubleshooting OpsWorks is harder than a simple Lambda custom resource.

    -   Efficiency:

        -   Initial Effort: Rewriting the entire template to use OpsWorks, learning Chef recipes, and setting up an OpsWorks stack is a massive overhaul compared to a small template change.

        -   Ongoing: OpsWorks adds operational overhead (managing stacks, recipes, Chef server) compared to a native CloudFormation solution.

-   Conclusion: This solves the problem but in a highly inefficient way. It's a sledgehammer approach for a problem that needs a scalpel. D is incorrect.




Analysis: Is B the Most Efficient?

Your pick, B, uses a custom resource with a Lambda function to empty the S3 bucket during stack deletion:

-   Does It Meet Requirements?: Yes. It ensures the bucket is empty before CloudFormation deletes it, preventing the "BucketNotEmpty" error. All resources (EC2 instance and S3 bucket) are deleted cleanly.

-   Efficiency:

    -   Initial Setup: Writing a small Lambda function (list and delete objects) and adding a custom resource to the template takes a bit of effort---about 20-30 lines of code and IAM setup.

    -   Ongoing: Once added, it's automatic for all stack deletions. No manual intervention, no recurring errors.

    -   Scalability: Works for any future deployments of the stack.

-   Maintainability: The Lambda function is simple and reusable. Custom resources are a standard CloudFormation pattern for handling edge cases like this.

-   Comparison to Alternatives:

    -   A: Misrepresents DeletionPolicy: Delete. If it meant adding a lifecycle rule to empty the bucket, that'd be efficient too, but the wording is wrong.

    -   C: A manual fix---quick for this instance but not a solution for the template. Inefficient for ongoing use.

    -   D: OpsWorks is a massive overcomplication, requiring a rewrite of the entire template and adding operational overhead.

B is the most efficient:

-   It's a one-time template change that fixes the issue permanently.

-   It's CloudFormation-native (custom resource + Lambda is a common pattern).

-   It requires minimal effort compared to overhauls (D) or manual fixes (C).

A Potential Alternative (Not Listed):

-   As of 2022, CloudFormation supports an S3 bucket property to empty the bucket on deletion. You can add a lifecycle rule to the bucket to delete all objects when the stack is deleted:

    yaml

    ```
    Resources:
      S3Bucket:
        Type: AWS::S3::Bucket
        Properties:
          BucketName: my-app-bucket
          LifecycleConfiguration:
            Rules:
              - Id: EmptyBucketOnDelete
                Status: Enabled
                ExpirationInDays: 1  # Ensures objects are deleted quickly
    ```

-   This would be the simplest fix---just a few lines in the template---but it's not an option here. B achieves the same result via a custom resource.


Why You Picked B

You likely chose B because:

-   You recognized that the S3 bucket deletion fails because it's not empty---a common CloudFormation issue.

-   You knew CloudFormation can't empty buckets by default, so you need to intervene before deletion.

-   You saw that a custom resource with Lambda can empty the bucket during stack deletion, ensuring a clean removal. The DependsOn attribute ensures proper ordering (empty bucket before deletion attempt).

-   You understood that this is a template-level fix, making it efficient for all future stack deletions, not just a one-time manual fix.

Your reasoning aligns perfectly with AWS best practices---using a custom resource to handle S3 bucket cleanup is a standard solution for this exact problem.

Correct Answer:  B. Add a custom resource with an AWS Lambda function with the DependsOn attribute specifying the S3 bucket, and an IAM role. Write the Lambda function to delete all objects from the bucket when RequestType is Delete.

* * * * *

**A company runs an application on one Amazon EC2 instance. Application metadata is
stored in Amazon S3 and must be retrieved if the instance is restarted. The instance must
restart or relaunch automatically if the instance becomes unresponsive.**

Which solution will meet these requirements?

A. Create an Amazon CloudWatch alarm for the StatusCheckFailed metric. Use the recover
action to stop and start the instance. Use an S3 event notification to push the metadata
to the instance when the instance is back up and running. <br />
B. Configure AWS OpsWorks, and use the auto healing feature to stop and start the
instance. Use a lifecycle event in OpsWorks to pull the metadata from Amazon S3 and
update it on the instance. <br />
C. Use EC2 Auto Recovery to automatically stop and start the instance in case of a failure.
Use an S3 event notification to push the metadata to the instance when the instance is
back up and running. <br />
D. Use AWS CloudFormation to create an EC2 instance that includes the UserData
property for the EC2 resource. Add a command in UserData to retrieve the application
metadata from Amazon S3.


Understanding the Problem

-   Setup:

    -   Single EC2 Instance: The application runs on one EC2 instance.

    -   Metadata in S3: Application metadata is stored in an S3 bucket and needs to be retrieved if the instance restarts.

    -   Unresponsiveness: The instance must automatically restart or relaunch if it becomes unresponsive.

-   Requirements:

    1.  Automatic Recovery: If the instance becomes unresponsive, it should automatically restart or relaunch.

    2.  Metadata Retrieval: After a restart or relaunch, the instance must retrieve the metadata from S3.

-   Key Considerations:

    -   Unresponsiveness could mean the instance fails health checks (e.g., Status Check failures in AWS, like a system failure or loss of network connectivity).

    -   Metadata retrieval implies the instance needs to pull the data from S3 post-restart, likely during startup.

    -   The solution should be simple and reliable for a single instance, without overcomplicating the architecture.

Let's evaluate each option to see which one meets both requirements effectively.



Option A: Create an Amazon CloudWatch alarm for the StatusCheckFailed metric. Use the recover action to stop and start the instance. Use an S3 event notification to push the metadata to the instance when the instance is back up and running

-   What This Does:

    -   CloudWatch Alarm for StatusCheckFailed:

        -   EC2 instances have two status checks: System Status (checks the underlying hardware/network) and Instance Status (checks the instance's OS/software).

        -   The StatusCheckFailed metric triggers if either check fails (e.g., StatusCheckFailed_System or StatusCheckFailed_Instance).

        -   A CloudWatch alarm can monitor this metric and take an action when it fails.

    -   Recover Action:

        -   The "recover" action for EC2 (available since 2017) automatically stops and restarts the instance on the same underlying hardware (if possible). If the hardware is the issue, it might move the instance to new hardware.

        -   This is a lightweight recovery mechanism for EC2 instances, designed for scenarios like this where you want to recover a single instance.

    -   S3 Event Notification:

        -   S3 event notifications can trigger actions (e.g., Lambda, SQS, SNS) when objects are created/updated in a bucket.

        -   The idea here is to "push" metadata to the instance after it restarts, using an S3 event notification.

-   Analysis:

    -   Automatic Recovery:

        -   The CloudWatch alarm with the recover action meets the requirement for automatic restart/relaunch. If the instance becomes unresponsive (e.g., fails system or instance status checks), the alarm triggers, and AWS attempts to recover the instance.

        -   Recovery typically takes a few minutes and preserves the instance's ID, IP addresses, and EBS volumes.

    -   Metadata Retrieval:

        -   The S3 event notification part is problematic. S3 events are triggered by bucket actions (e.g., object creation), not by instance state changes. There's no direct way for an S3 event to "push" metadata to an instance when it restarts.

        -   Possible interpretation:

            -   After the instance restarts, a script on the instance could upload a "restart marker" object to S3, triggering an S3 event.

            -   The S3 event could invoke a Lambda function to "push" the metadata to the instance (e.g., via SSM Run Command or by writing to a known location the instance polls).

        -   This is convoluted and unreliable:

            -   The instance would need to know when to upload the marker object (requires user data scripting).

            -   "Pushing" metadata to an instance isn't straightforward---SSM Run Command could work, but it's complex and assumes the instance is reachable.

            -   A simpler approach would be for the instance to pull the metadata from S3 during startup (e.g., via user data), not rely on S3 events to push.

    -   Does It Meet Requirements?:

        -   Recovery: Yes, the recover action handles unresponsiveness.

        -   Metadata: No, S3 event notifications aren't a practical way to push metadata to an instance. It overcomplicates what should be a simple pull operation.

-   Conclusion: The recovery part works, but the metadata retrieval is flawed. A is not the best solution.



Option B: Configure AWS OpsWorks, and use the auto healing feature to stop and start the instance. Use a lifecycle event in OpsWorks to pull the metadata from Amazon S3 and update it on the instance

Your pick! Since you're not familiar with OpsWorks, I'll explain it thoroughly.

-   What This Does:

    -   AWS OpsWorks:

        -   AWS OpsWorks Stacks is a configuration management service that uses Chef or Puppet to manage instances and applications. It organizes instances into stacks and layers (e.g., a web server layer).

        -   You define a stack (e.g., "App Stack"), a layer (e.g., "Web Layer"), and add the EC2 instance to the layer. OpsWorks manages the instance's lifecycle.

    -   Auto Healing:

        -   OpsWorks has an "auto healing" feature: if an instance fails health checks (e.g., it stops responding to OpsWorks agent pings), OpsWorks automatically terminates and relaunches the instance.

        -   This is similar to EC2 Auto Scaling's health checks but managed by OpsWorks.

    -   Lifecycle Event:

        -   OpsWorks supports lifecycle events (e.g., setup, configure, deploy, undeploy, shutdown) that trigger Chef recipes on the instance.

        -   The setup event runs after an instance boots, making it ideal for initialization tasks.

        -   You can write a Chef recipe to pull metadata from S3 (e.g., using the AWS CLI: aws s3 cp s3://my-bucket/metadata.json /path/to/metadata) and update the instance (e.g., place the file in the right directory or update app config).

-   Analysis:

    -   Automatic Recovery:

        -   OpsWorks auto healing meets the requirement. If the instance becomes unresponsive, OpsWorks detects the failure (via its agent) and relaunches the instance. This is a straightforward way to handle unresponsiveness for a single instance.

        -   Note: OpsWorks relaunches the instance (new instance ID), unlike EC2 recovery (which tries to preserve the ID). This still meets the "restart or relaunch" requirement.

    -   Metadata Retrieval:

        -   Using a lifecycle event (e.g., setup) to pull metadata from S3 is a clean approach. The Chef recipe runs automatically after the instance boots:

            ruby

            ```
            # Chef recipe (e.g., recipes/setup.rb)
            execute 'download_metadata' do
              command 'aws s3 cp s3://my-bucket/metadata.json /app/metadata.json'
              action :run
            end
            ```

        -   This ensures the metadata is retrieved post-restart, fulfilling the requirement. The instance pulls the data directly---no need for complex event notifications.

    -   Does It Meet Requirements?:

        -   Recovery: Yes, auto healing handles unresponsiveness.

        -   Metadata: Yes, the lifecycle event pulls metadata from S3 during startup.

    -   Drawbacks:

        -   Complexity: OpsWorks is a heavyweight solution for a single EC2 instance. It requires setting up a stack, layer, and Chef recipes, which is overkill for this simple use case. OpsWorks is better suited for managing fleets of instances or complex applications with multiple layers (e.g., web, app, DB).

        -   Learning Curve: Since you're not familiar with OpsWorks, it's worth noting there's a learning curve---understanding stacks, layers, and Chef recipes takes time.

        -   Overhead: OpsWorks adds operational complexity (e.g., managing the OpsWorks agent, Chef server) compared to simpler EC2-native solutions.

-   Conclusion: This meets both requirements but isn't the simplest approach. OpsWorks works, but it's more complex than necessary for a single instance. B is viable but not the most efficient.



Option C: Use EC2 Auto Recovery to automatically stop and start the instance in case of a failure. Use an S3 event notification to push the metadata to the instance when the instance is back up and running

-   What This Does:

    -   EC2 Auto Recovery:

        -   This refers to the same mechanism as A's "recover" action but via a different setup. You can enable EC2 Auto Recovery by creating a CloudWatch alarm on the StatusCheckFailed_System metric with the recover action.

        -   It automatically stops and restarts the instance if it fails system status checks (e.g., hardware failure, network issues).

    -   S3 Event Notification: Same as A---use an S3 event to "push" metadata to the instance after it restarts.

-   Analysis:

    -   Automatic Recovery:

        -   EC2 Auto Recovery works for unresponsiveness. It's effectively the same as A's CloudWatch alarm with the recover action, just described differently.

        -   It restarts the instance on the same hardware (or new hardware if needed), preserving the instance ID and IPs.

    -   Metadata Retrieval:

        -   As in A, the S3 event notification approach is flawed. S3 events are triggered by bucket actions, not instance restarts. "Pushing" metadata to an instance via an S3 event is impractical---it would require the instance to trigger the event (e.g., by uploading an object) and then a mechanism (e.g., Lambda + SSM) to push data back, which is overly complex.

        -   A simpler approach is for the instance to pull the metadata itself during startup.

    -   Does It Meet Requirements?:

        -   Recovery: Yes, EC2 Auto Recovery handles unresponsiveness.

        -   Metadata: No, the S3 event notification method is impractical.

-   Conclusion: Same as A---the recovery part works, but the metadata retrieval is flawed. C is not the best solution.



Option D: Use AWS CloudFormation to create an EC2 instance that includes the UserData property for the EC2 resource. Add a command in UserData to retrieve the application metadata from Amazon S3

-   What This Does:

    -   CloudFormation Template:

        -   Define an EC2 instance in CloudFormation with a UserData script.

        -   The UserData script runs on instance boot and includes a command to pull metadata from S3.

    -   UserData:

        -   Example script in the CloudFormation template:

            yaml

            ```
            Resources:
              EC2Instance:
                Type: AWS::EC2::Instance
                Properties:
                  ImageId: ami-12345678
                  InstanceType: t3.micro
                  UserData:
                    Fn::Base64: |
                      #!/bin/bash
                      aws s3 cp s3://my-bucket/metadata.json /app/metadata.json
                      # Restart the application if needed
                      systemctl restart my-app
            ```

        -   UserData runs on every instance boot, including after a restart or relaunch.

-   Analysis:

    -   Automatic Recovery:

        -   This option doesn't address the recovery requirement. CloudFormation creates the instance but doesn't handle unresponsiveness. You'd need to add a recovery mechanism (e.g., a CloudWatch alarm as in A/C, or use Auto Scaling with a single instance).

        -   Without recovery, this fails the "restart or relaunch automatically" requirement.

    -   Metadata Retrieval:

        -   The UserData script is a perfect way to pull metadata from S3. On boot (including after a restart), the instance runs the script, downloads the metadata, and updates the application.

        -   This is simple and reliable---no need for S3 event notifications or external triggers.

    -   Does It Meet Requirements?:

        -   Recovery: No, CloudFormation alone doesn't handle unresponsiveness.

        -   Metadata: Yes, UserData handles metadata retrieval cleanly.

-   Conclusion: This only solves half the problem. While the metadata retrieval is spot-on, it misses the automatic recovery requirement. D is incomplete.



Analysis: Is B the Best Choice?

Your pick, B, uses AWS OpsWorks with auto healing and a lifecycle event:

-   Does It Meet Requirements?:

    -   Recovery: Yes, OpsWorks auto healing stops and starts the instance if it becomes unresponsive.

    -   Metadata: Yes, the setup lifecycle event pulls metadata from S3 post-restart.

-   Is It the Most Logical?:

    -   You chose B because it seemed logical---it addresses both requirements in one solution. OpsWorks handles recovery (via auto healing) and metadata retrieval (via lifecycle event), making it a cohesive approach.

    -   However, OpsWorks is overkill for a single instance. It's designed for managing fleets of instances with complex configurations, not a simple single-instance app.

Comparison to Alternatives:

-   A and C: Both use EC2 Auto Recovery (via CloudWatch alarm), which is a simpler recovery mechanism for a single instance. However, their S3 event notification approach for metadata is impractical.

-   D: Nails metadata retrieval with UserData but misses recovery entirely.

What's Missing?:

-   The ideal solution would combine the simplicity of EC2 Auto Recovery (from A/C) with the metadata retrieval of UserData (from D). For example:

    -   Use CloudFormation to create the EC2 instance with a UserData script to pull metadata (like D).

    -   Add a CloudWatch alarm with the recover action to handle unresponsiveness (like A/C).

-   This isn't an option, so we must pick the best available.

Why B Isn't Optimal:

-   OpsWorks adds unnecessary complexity for a single instance. Setting up a stack, layer, and Chef recipes is more effort than needed compared to EC2 Auto Recovery + UserData.

-   A simpler solution (not listed) would be better, but among the options, B is the only one that fully meets both requirements.

Best Available Choice:

-   B is the only option that addresses both requirements, even if it's overkill. A and C fail on metadata retrieval, and D fails on recovery.

Correct Answer:  B. Configure AWS OpsWorks, and use the auto healing feature to stop and start the instance. Use a lifecycle event in OpsWorks to pull the metadata from Amazon S3 and update it on the instance.


Why You Picked B

You chose B because it logically addresses both requirements:

-   Recovery: OpsWorks auto healing restarts the instance if unresponsive.

-   Metadata: The lifecycle event pulls metadata from S3 post-restart.

Your reasoning makes sense---B is the only option that fully meets the requirements in one package. You weren't familiar with OpsWorks, but you recognized it as a tool that could handle both recovery and metadata retrieval, which shows great intuition! OpsWorks does work here, but in a real-world scenario, you'd likely use a simpler approach (e.g., EC2 Auto Recovery + UserData) to avoid the overhead of OpsWorks for a single instance.


More on AWS OpsWorks (Since You're Unfamiliar)

-   What Is OpsWorks?:

    -   OpsWorks Stacks is a configuration management service that helps you manage applications and infrastructure using Chef or Puppet.

    -   You organize resources into stacks (a collection of resources) and layers (e.g., a web layer, app layer).

    -   Each layer can manage EC2 instances, and OpsWorks runs a Chef agent on those instances to execute recipes during lifecycle events.

-   Key Features:

    -   Auto Healing: If an instance fails health checks (e.g., the OpsWorks agent stops responding), OpsWorks relaunches it.

    -   Lifecycle Events: Events like setup (post-boot), configure (config changes), and deploy (app deployment) trigger Chef recipes to automate tasks.

-   Use Case in This Question:

    -   You'd create a stack with a single layer (e.g., "App Layer"), add the EC2 instance to it, enable auto healing, and write a Chef recipe to pull metadata from S3 during the setup event.

-   Why It's Overkill:

    -   OpsWorks is designed for complex apps with multiple instances/layers (e.g., web servers, app servers, databases). For a single EC2 instance, simpler tools like EC2 Auto Recovery and CloudFormation are more appropriate.



***

**A developer is maintaining a fleet of 50 Amazon EC2 Linux servers. The servers are part
of an Amazon EC2 Auto Scaling group, and also use Elastic Load Balancing for load
balancing.
Occasionally, some application servers are being terminated after failing ELB HTTP
health checks. The developer would like to perform a root cause analysis on the issue,
but before being able to access application logs, the server is terminated.**

How can log collection be automated?

A. Use Auto Scaling lifecycle hooks to put instances in a Pending:Wait state. Create an
Amazon CloudWatch alarm for EC2 Instance Terminate Successful and trigger an AWS
Lambda function that invokes an SSM Run Command script to collect logs, push them to
Amazon S3, and complete the lifecycle action once logs are collected. <br />
B. Use Auto Scaling lifecycle hooks to put instances in a Terminating:Wait state. Create an
AWS Config rule for EC2 Instance-terminate Lifecycle Action and trigger a step function
that invokes a script to collect logs, push them to Amazon S3, and complete the lifecycle
action once logs are collected. <br />
C. Use Auto Scaling lifecycle hooks to put instances in a Terminating:Wait state. Create an
Amazon CloudWatch subscription filter for EC2 Instance Terminate Successful and
trigger a CloudWatch agent that invokes a script to collect logs, push them to Amazon
S3, and complete the lifecycle action once logs are collected. <br />
D. Use Auto Scaling lifecycle hooks to put instances in a Terminating:Wait state. Create an
Amazon EventBridge rule for EC2 Instance-terminate Lifecycle Action and trigger an
AWS Lambda function that invokes an SSM Run Command script to collect logs, push
them to Amazon S3, and complete the lifecycle action once logs are collected.




Understanding the Problem

-   Setup:

    -   EC2 Instances: 50 Linux servers in an Auto Scaling group.

    -   Elastic Load Balancing (ELB): The ASG integrates with ELB, which performs HTTP health checks on the instances.

    -   Health Check Failures: Some instances fail ELB HTTP health checks, causing the ASG to mark them as unhealthy and terminate them.

    -   Log Collection Issue: Instances are terminated before the developer can access application logs for root cause analysis.

-   Requirements:

    -   Automate log collection before the instance is terminated.

    -   Ensure logs are preserved (e.g., by pushing them to a durable location like S3).

    -   Allow the termination to proceed after log collection.

-   Key Mechanism:

    -   When an instance fails ELB health checks, the ASG marks it unhealthy and initiates termination.

    -   We need to intercept the termination process, collect logs, and then allow the termination to complete.

Auto Scaling Termination Process:

-   When an instance is marked unhealthy (e.g., by ELB), the ASG starts the termination process.

-   By default, the instance is terminated immediately, and logs on the instance (e.g., in /var/log) are lost unless preserved.

Solution Approach:

-   Use Auto Scaling lifecycle hooks to pause the termination process, giving time to collect logs.

-   Trigger an action during this pause to collect logs, push them to S3, and then complete the termination.

Let's evaluate each option to find the best approach.


Option A: Use Auto Scaling lifecycle hooks to put instances in a Pending:Wait state. Create an Amazon CloudWatch alarm for EC2 Instance Terminate Successful and trigger an AWS Lambda function that invokes an SSM Run Command script to collect logs, push them to Amazon S3, and complete the lifecycle action once logs are collected

-   What This Does:

    -   Lifecycle Hooks:

        -   Lifecycle hooks allow you to pause an ASG instance during state transitions (e.g., launching or terminating).

        -   Pending:Wait is a state during instance launch (not termination). The correct state for termination is Terminating:Wait.

        -   This option incorrectly uses Pending:Wait, which applies when an instance is launching, not terminating. We need to catch the instance before it terminates, so this is a red flag.

    -   CloudWatch Alarm:

        -   The alarm triggers on the EC2 Instance Terminate Successful metric, which indicates an instance has already terminated.

        -   If the instance is already terminated, it's too late to collect logs---the instance is gone, and its EBS volumes (if not set to persist) are deleted.

    -   Lambda and SSM Run Command:

        -   The Lambda function invokes an SSM Run Command script to collect logs (e.g., aws s3 cp /var/log/app.log s3://my-bucket/logs/) and push them to S3.

        -   SSM Run Command requires the instance to be running and the SSM Agent to be active, which isn't possible if the instance is already terminated.

    -   Completing the Lifecycle Action:

        -   The Lambda would complete the lifecycle action (e.g., using CompleteLifecycleAction), but since the hook state is wrong, this step is irrelevant.

-   Analysis:

    -   Lifecycle Hook State: Pending:Wait is incorrect for termination---it's for launching instances. The correct state is Terminating:Wait.

    -   Trigger Timing: EC2 Instance Terminate Successful happens after termination, so logs can't be collected at that point.

    -   Does It Meet Requirements?: No. The hook state is wrong, and the trigger is too late.

-   Conclusion: This option fails due to the incorrect lifecycle state and late trigger. A is incorrect.


Option B: Use Auto Scaling lifecycle hooks to put instances in a Terminating:Wait state. Create an AWS Config rule for EC2 Instance-terminate Lifecycle Action and trigger a step function that invokes a script to collect logs, push them to Amazon S3, and complete the lifecycle action once logs are collected

Your pick! Let's break this down:

-   What This Does:

    -   Lifecycle Hooks:

        -   Terminating:Wait is the correct state. When an instance is marked for termination (e.g., due to failing ELB health checks), the lifecycle hook pauses the instance in the Terminating:Wait state.

        -   During this state, the instance is still running, giving us time to collect logs.

        -   You configure the hook to send a notification (e.g., to EventBridge or an SNS topic) when the instance enters this state.

    -   AWS Config Rule:

        -   AWS Config rules evaluate the compliance of resources against desired configurations.

        -   The rule here is for EC2 Instance-terminate Lifecycle Action, implying it triggers when a lifecycle action occurs (e.g., termination).

        -   AWS Config rules can integrate with EventBridge to react to events, but Config rules are typically for compliance checks (e.g., "is an instance tagged correctly?"), not for reacting to lifecycle events.

        -   Auto Scaling lifecycle hooks emit events to EventBridge (e.g., autoscaling:EC2_INSTANCE_TERMINATING), but AWS Config isn't the right mechanism to catch these events---EventBridge or CloudWatch Events rules are.

    -   Step Function:

        -   The Config rule triggers an AWS Step Function, which orchestrates a workflow to:

            1.  Invoke a script to collect logs (e.g., via SSM Run Command or a Lambda invoking a script).

            2.  Push logs to S3.

            3.  Complete the lifecycle action (e.g., using CompleteLifecycleAction API).

-   Analysis:

    -   Lifecycle Hook: Terminating:Wait is correct. The instance pauses before termination, giving us a window to act.

    -   Trigger Mechanism:

        -   AWS Config rules aren't designed to react to lifecycle events like EC2_INSTANCE_TERMINATING. Config rules evaluate resource state changes (e.g., via CloudTrail logs), but lifecycle hooks emit events directly to EventBridge.

        -   The correct approach is to use an EventBridge rule to catch the lifecycle event (autoscaling:EC2_INSTANCE_TERMINATING), not AWS Config.

        -   If we stretch this, AWS Config could theoretically detect a state change (via CloudTrail), but it's not the idiomatic way to handle lifecycle events, and Config rules don't directly "trigger" on lifecycle actions---they evaluate compliance.

    -   Step Function:

        -   A Step Function is a good orchestrator for this workflow:

            -   Step 1: Invoke SSM Run Command to collect logs (e.g., /var/log/app.log).

            -   Step 2: Push logs to S3.

            -   Step 3: Complete the lifecycle action.

        -   Step Functions add reliability (e.g., retries, error handling), but they're overkill for a simple task that a single Lambda can handle.

    -   Does It Meet Requirements?:

        -   Log Collection: Yes, if we assume the script collects logs while the instance is in Terminating:Wait.

        -   Preservation: Yes, logs are pushed to S3.

        -   Termination: Yes, the lifecycle action is completed.

    -   Issue: The AWS Config rule is the wrong trigger. Lifecycle hooks emit events to EventBridge, not AWS Config. This makes the solution technically incorrect as written.

-   Conclusion: The lifecycle hook state is correct, and the Step Function could work, but AWS Config isn't the right way to detect lifecycle events. B is incorrect due to the Config rule.


Option C: Use Auto Scaling lifecycle hooks to put instances in a Terminating:Wait state. Create an Amazon CloudWatch subscription filter for EC2 Instance Terminate Successful and trigger a CloudWatch agent that invokes a script to collect logs, push them to Amazon S3, and complete the lifecycle action once logs are collected

-   What This Does:

    -   Lifecycle Hooks: Terminating:Wait is correct, pausing the instance before termination.

    -   CloudWatch Subscription Filter:

        -   A subscription filter in CloudWatch Logs typically filters log events and streams them to a destination (e.g., Lambda).

        -   EC2 Instance Terminate Successful isn't a log event---it's a CloudWatch metric (from A), not something you'd find in CloudWatch Logs.

        -   Even if we interpret this as a CloudWatch Logs event (e.g., from CloudTrail logging ASG actions), the "Terminate Successful" event happens after termination---too late to collect logs.

    -   CloudWatch Agent:

        -   The CloudWatch agent (Unified CloudWatch Agent) collects logs and metrics from instances and sends them to CloudWatch Logs.

        -   Here, it's supposed to invoke a script to collect logs, but if the instance is already terminated (per the trigger), the agent can't run.

-   Analysis:

    -   Trigger Timing: EC2 Instance Terminate Successful is too late---logs are gone.

    -   Subscription Filter: This is the wrong mechanism. Subscription filters are for log streams, not lifecycle events or metrics.

    -   CloudWatch Agent: The agent can't collect logs from a terminated instance.

-   Conclusion: The lifecycle hook state is correct, but the trigger and agent usage are wrong. C is incorrect.


Option D: Use Auto Scaling lifecycle hooks to put instances in a Terminating:Wait state. Create an Amazon EventBridge rule for EC2 Instance-terminate Lifecycle Action and trigger an AWS Lambda function that invokes an SSM Run Command script to collect logs, push them to Amazon S3, and complete the lifecycle action once logs are collected

-   What This Does:

    -   Lifecycle Hooks: Terminating:Wait is correct, pausing the instance before termination.

    -   EventBridge Rule:

        -   When an instance enters Terminating:Wait, the lifecycle hook emits an event to EventBridge (or CloudWatch Events, its predecessor).

        -   The event is autoscaling:EC2_INSTANCE_TERMINATING, indicating the instance is about to terminate.

        -   An EventBridge rule can match this event:

            json

            ```
            {
              "source": ["aws.autoscaling"],
              "detail-type": ["EC2 Instance-terminate Lifecycle Action"]
            }
            ```

    -   Lambda Function:

        -   The Lambda is triggered by the EventBridge rule.

        -   It extracts the instance ID from the event payload.

        -   It invokes an SSM Run Command script (e.g., AWS-RunShellScript) to:

            1.  Collect logs (e.g., cp /var/log/app.log /tmp/).

            2.  Push logs to S3 (e.g., aws s3 cp /tmp/app.log s3://my-bucket/logs/).

        -   It completes the lifecycle action using the Auto Scaling API (CompleteLifecycleAction), allowing termination to proceed.

-   Analysis:

    -   Lifecycle Hook: Correct state (Terminating:Wait).

    -   Trigger: EventBridge is the right tool. Lifecycle hooks emit events to EventBridge, and the EC2 Instance-terminate Lifecycle Action event is exactly what we need.

    -   Log Collection:

        -   SSM Run Command runs a script on the instance while it's still in Terminating:Wait (instance is running, SSM Agent is active).

        -   The script collects logs and pushes them to S3.

    -   Completing the Action: Lambda calls CompleteLifecycleAction, allowing the ASG to proceed with termination.

    -   Does It Meet Requirements?:

        -   Log Collection: Yes, SSM Run Command collects logs before termination.

        -   Preservation: Yes, logs are pushed to S3.

        -   Termination: Yes, the lifecycle action is completed.

    -   Efficiency:

        -   EventBridge → Lambda → SSM Run Command is a standard AWS pattern for this use case.

        -   Minimal setup: create a lifecycle hook, an EventBridge rule, and a Lambda function (with IAM permissions for SSM and ASG).

-   Conclusion: This is the cleanest, most AWS-native solution. It uses the right trigger (EventBridge), a reliable execution mechanism (SSM Run Command), and completes the lifecycle action. D looks like the winner.


Analysis: Is B the Best Choice?

Your pick, B, uses:

-   Auto Scaling lifecycle hooks (Terminating:Wait)---correct.

-   AWS Config rule to trigger a Step Function---incorrect trigger mechanism.

-   Step Function to collect logs and complete the action---works but overkill.

Why B Isn't the Best:

-   Trigger Issue: AWS Config isn't the right way to catch lifecycle events. Auto Scaling emits EC2_INSTANCE_TERMINATING events to EventBridge, not AWS Config. Config rules are for compliance (e.g., "is this resource compliant?"), not for reacting to lifecycle actions.

-   Complexity: Step Functions are great for orchestration but unnecessary here. A single Lambda (as in D) can handle this task more simply.

Comparison to Alternatives:

-   A: Wrong lifecycle state (Pending:Wait) and wrong trigger timing (post-termination).

-   C: Wrong trigger (CloudWatch subscription filter) and timing (post-termination).

-   D: Correct lifecycle state, correct trigger (EventBridge), and efficient execution (Lambda + SSM).

D is the best choice:

-   It uses EventBridge to catch the lifecycle event, which is the standard approach.

-   Lambda + SSM Run Command is a simple, reliable way to collect logs.

-   It minimizes complexity while meeting all requirements.


Why You Picked B

You chose B because it seemed the most logical:

-   Lifecycle Hook: You correctly identified that Terminating:Wait is the right state to pause termination and collect logs.

-   AWS Config Rule: You might have thought Config could monitor lifecycle actions, which is a reasonable guess if you're not familiar with how lifecycle hooks integrate with EventBridge. Config rules do evaluate resource changes, but lifecycle hooks emit events directly to EventBridge, making D the better fit.

-   Step Function: You likely saw this as a way to orchestrate the log collection process, which is a good instinct for reliability, but a Lambda (as in D) is simpler for this task.

Your reasoning was solid---you got the lifecycle hook right, which is the core mechanism. The trigger (AWS Config vs. EventBridge) was the tricky part, and now you know EventBridge is the go-to for lifecycle events.

Correct Answer:  D. Use Auto Scaling lifecycle hooks to put instances in a Terminating:Wait state. Create an Amazon EventBridge rule for EC2 Instance-terminate Lifecycle Action and trigger an AWS Lambda function that invokes an SSM Run Command script to collect logs, push them to Amazon S3, and complete the lifecycle action once logs are collected.


***

**A company has migrated its container-based applications to Amazon EKS and want to
establish automated email notifications. The notifications sent to each email address are
for specific activities related to EKS components. The solution will include Amazon SNS
topics and an AWS Lambda function to evaluate incoming log events and publish
messages to the correct SNS topic.
**
Which logging solution will support these requirements?

A. Enable Amazon CloudWatch Logs to log the EKS components. Create a CloudWatch
subscription filter for each component with Lambda as the subscription feed destination. <br />
B. Enable Amazon CloudWatch Logs to log the EKS components. Create CloudWatch
Logs Insights queries linked to Amazon EventBridge events that invoke Lambda. <br />
C. Enable Amazon S3 logging for the EKS components. Configure an Amazon
CloudWatch subscription filter for each component with Lambda as the subscription feed
destination. <br />
D. Enable Amazon S3 logging for the EKS components. Configure S3 PUT Object event
notifications with AWS Lambda as the destination.


Understanding the Problem

-   Setup:

    -   Amazon EKS: The company's applications run on Amazon EKS (Elastic Kubernetes Service), a managed Kubernetes service.

    -   EKS Components: These likely include EKS cluster components like the control plane, worker nodes, kube-apiserver, kube-controller-manager, or application-level logs (e.g., pod logs).

    -   Notifications: Email notifications are sent to specific email addresses based on activities related to EKS components.

    -   SNS and Lambda:

        -   SNS topics will send notifications (e.g., one topic per component or activity type, with email subscriptions).

        -   A Lambda function will evaluate incoming log events and publish messages to the appropriate SNS topic.

-   Requirements:

    -   Log EKS component activities.

    -   Process these logs to identify specific events.

    -   Route events to a Lambda function for evaluation.

    -   Lambda publishes messages to the correct SNS topic for email notifications.

-   Key Considerations:

    -   EKS logging: What logs are available, and where are they stored?

    -   How do we get logs to the Lambda function for processing?

    -   The solution must support filtering logs per component and triggering Lambda in near real time.

Let's evaluate each option to find the best logging solution.



Option A: Enable Amazon CloudWatch Logs to log the EKS components. Create a CloudWatch subscription filter for each component with Lambda as the subscription feed destination

Your pick! Let's break this down:

-   What This Does:

    -   CloudWatch Logs for EKS:

        -   EKS integrates with Amazon CloudWatch Logs to capture logs from various components:

            -   Control Plane Logs: EKS can send control plane logs (e.g., API server, scheduler, controller manager) to CloudWatch Logs. You enable this in the EKS cluster settings (e.g., enabledClusterLogTypes: ["api", "scheduler"]).

            -   Pod Logs: Pods running on EKS worker nodes can send logs to CloudWatch Logs using a logging agent like Fluentd or Fluent Bit (via the aws-observability/aws-for-fluent-bit Helm chart or a DaemonSet).

            -   Worker Node Logs: System logs (e.g., kubelet, container runtime) can also be sent to CloudWatch Logs via the CloudWatch Agent.

        -   Logs are organized into log groups (e.g., /aws/eks/<cluster-name>/cluster for control plane logs, or custom log groups for pod logs).

    -   CloudWatch Subscription Filter:

        -   A subscription filter in CloudWatch Logs allows you to stream log events in near real time to a destination (e.g., Lambda, Kinesis, or another service).

        -   You create a filter for each EKS component (e.g., one for API server logs, one for scheduler logs, one for pod logs of a specific app).

        -   The filter pattern matches log events for that component (e.g., {"component": "kube-apiserver"} or error keywords like Failed).

        -   The destination is the Lambda function, which receives the log events, evaluates them, and publishes to the appropriate SNS topic.

    -   Lambda and SNS:

        -   Lambda processes each log event, determines the activity (e.g., "pod failed to start"), and sends a message to the corresponding SNS topic.

        -   SNS topics are subscribed to email addresses, sending notifications.

-   Analysis:

    -   Logging EKS Components:

        -   CloudWatch Logs is the standard logging solution for EKS. Control plane logs are natively supported, and pod/worker logs can be sent via agents (Fluentd/Fluent Bit or CloudWatch Agent).

        -   This meets the requirement to log EKS components.

    -   Filtering per Component:

        -   Subscription filters allow you to define patterns for each component (e.g., filter API server logs separately from scheduler logs).

        -   You can create multiple filters within the same log group (e.g., /aws/eks/<cluster-name>/cluster) or across different log groups (e.g., one per app).

    -   Triggering Lambda:

        -   Subscription filters stream logs to Lambda in near real time (typically within seconds), which is ideal for automated notifications.

        -   Lambda can process the events, decide which SNS topic to publish to, and send the notification.

    -   Does It Meet Requirements?:

        -   Log Collection: Yes, CloudWatch Logs captures EKS component logs.

        -   Processing: Yes, subscription filters route logs to Lambda for evaluation.

        -   Notifications: Yes, Lambda publishes to SNS topics for email notifications.

    -   Efficiency:

        -   This is a standard AWS pattern: CloudWatch Logs → Subscription Filter → Lambda → SNS.

        -   It's scalable (handles large log volumes) and near real-time (seconds delay).

-   Conclusion: This looks like a strong solution. It leverages CloudWatch Logs for EKS logging, uses subscription filters to route logs per component, and integrates with Lambda and SNS as required. A is promising.



Option B: Enable Amazon CloudWatch Logs to log the EKS components. Create CloudWatch Logs Insights queries linked to Amazon EventBridge events that invoke Lambda

-   What This Does:

    -   CloudWatch Logs for EKS: Same as A---enable CloudWatch Logs to capture EKS component logs.

    -   CloudWatch Logs Insights:

        -   Logs Insights is a query tool for analyzing logs in CloudWatch Log groups. You write queries (e.g., fields @message | filter component = "kube-apiserver" | filter @message like /Failed/) to find specific events.

    -   Linked to EventBridge Events:

        -   Logs Insights queries can be scheduled (e.g., via CloudWatch Metric Filters or Contributor Insights) to detect patterns and emit metrics or events.

        -   You'd need to set up a mechanism to trigger EventBridge events based on query results (e.g., using a CloudWatch Alarm on a metric derived from the query).

    -   Invoke Lambda:

        -   EventBridge events trigger the Lambda function, which evaluates the event and publishes to SNS.

-   Analysis:

    -   Logging: CloudWatch Logs works for EKS, as in A.

    -   Logs Insights:

        -   Logs Insights is great for ad-hoc analysis or scheduled queries, but it's not designed for real-time streaming.

        -   To link to EventBridge, you'd:

            1.  Create a Metric Filter to detect patterns in logs (e.g., "Failed" messages).

            2.  Emit a CloudWatch Metric based on the filter.

            3.  Set a CloudWatch Alarm on the metric to trigger an EventBridge event.

            4.  EventBridge invokes Lambda.

        -   This process is delayed---Metric Filters and Alarms aren't near real-time (they aggregate over minutes, e.g., 1-minute periods).

    -   Per Component:

        -   You'd need a separate Metric Filter and Alarm for each component, which is feasible but cumbersome.

    -   Does It Meet Requirements?:

        -   Log Collection: Yes, CloudWatch Logs works.

        -   Processing: Yes, but with delays---Logs Insights and Alarms aren't real-time (minutes delay vs. seconds in A).

        -   Notifications: Yes, Lambda can publish to SNS, but the delay impacts responsiveness.

    -   Efficiency:

        -   This is more complex than A: Metric Filters → Metrics → Alarms → EventBridge → Lambda.

        -   It's not near real-time, which is a drawback for "automated notifications."

-   Conclusion: This works but is less efficient than A due to delays and complexity. Subscription filters (A) are the better choice for real-time log streaming. B is not the best.



Option C: Enable Amazon S3 logging for the EKS components. Configure an Amazon CloudWatch subscription filter for each component with Lambda as the subscription feed destination

-   What This Does:

    -   S3 Logging for EKS:

        -   This implies storing EKS component logs in S3 (e.g., as log files).

        -   Issue: EKS doesn't natively send logs to S3. EKS integrates with CloudWatch Logs for control plane and pod logs (via agents like Fluentd). You could configure a custom solution to write logs to S3 (e.g., Fluentd with an S3 output plugin), but this isn't standard for EKS.

    -   CloudWatch Subscription Filter:

        -   Subscription filters apply to CloudWatch Logs, not S3. If logs are in S3, you can't directly apply a CloudWatch subscription filter.

        -   To use subscription filters, logs must first be in CloudWatch Logs, contradicting the "S3 logging" premise.

-   Analysis:

    -   Logging: EKS doesn't natively send logs to S3. You'd need a custom pipeline (e.g., Fluentd → S3), which adds complexity and isn't mentioned.

    -   Subscription Filter: This only works with CloudWatch Logs, not S3. The option is internally inconsistent.

    -   Does It Meet Requirements?: No---S3 isn't the right logging destination for EKS, and subscription filters don't apply to S3.

-   Conclusion: This is incorrect due to the mismatch between S3 logging and CloudWatch subscription filters. C is incorrect.


Option D: Enable Amazon S3 logging for the EKS components. Configure S3 PUT Object event notifications with AWS Lambda as the destination

-   What This Does:

    -   S3 Logging for EKS: Same as C---implies storing EKS logs in S3, which isn't native for EKS.

    -   S3 PUT Object Event Notifications:

        -   S3 can trigger events (e.g., Lambda, SQS, SNS) when objects are created (PUT operations).

        -   If logs are written to S3 as objects, an S3 event notification can invoke the Lambda function for each new log file.

-   Analysis:

    -   Logging: As in C, EKS doesn't natively send logs to S3. You'd need a custom setup (e.g., Fluentd → S3), which isn't standard and adds complexity.

    -   S3 Event Notifications:

        -   If logs are in S3, this works---each new log file triggers Lambda, which processes the file and publishes to SNS.

        -   However, this is file-based, not event-based. Logs are batched into files, so notifications are delayed until the file is written (e.g., every 5 minutes with Fluentd's buffering).

        -   Per Component: S3 events don't easily filter "per component"---you'd need to organize logs into separate prefixes (e.g., logs/kube-apiserver/, logs/scheduler/) and set up separate event notifications, which is cumbersome.

    -   Does It Meet Requirements?:

        -   Log Collection: No, EKS doesn't natively log to S3.

        -   Processing: Yes, if logs were in S3, but with delays (file-based, not real-time).

        -   Notifications: Yes, Lambda can publish to SNS.

    -   Efficiency:

        -   Requires a custom logging pipeline to get EKS logs to S3.

        -   S3 events are less real-time than CloudWatch subscription filters (A).

-   Conclusion: This is impractical due to EKS's lack of native S3 logging and the delayed, file-based nature of S3 events. D is incorrect.


Analysis: Is A the Best Choice?

Your pick, A, uses:

-   CloudWatch Logs to capture EKS component logs.

-   Subscription filters per component to stream logs to Lambda.

-   Lambda to evaluate logs and publish to SNS.

Why A Works:

-   Logging: CloudWatch Logs is the native logging solution for EKS---control plane logs, pod logs, and worker node logs can all be sent here.

-   Per Component: Subscription filters allow filtering by component (e.g., via log patterns or separate log groups), meeting the requirement for component-specific notifications.

-   Real-Time: Subscription filters stream logs to Lambda in near real time (seconds), ideal for automated notifications.

-   Integration: CloudWatch Logs → Lambda → SNS is a standard AWS pattern for log-driven notifications.

Comparison to Alternatives:

-   B: CloudWatch Logs Insights with EventBridge is slower (minutes delay) and more complex (Metric Filters → Alarms → EventBridge).

-   C: S3 logging isn't native for EKS, and subscription filters don't apply to S3.

-   D: S3 logging isn't native, and S3 events are file-based (delayed, harder to filter per component).

A is the best choice:

-   It uses the right logging destination (CloudWatch Logs).

-   It provides real-time streaming (subscription filters).

-   It supports per-component filtering and integrates seamlessly with Lambda and SNS.


Why You Picked A

You chose A because:

-   You recognized that CloudWatch Logs is the standard way to capture EKS logs (control plane, pods, etc.).

-   You understood that subscription filters can stream logs to Lambda in real time, allowing for quick evaluation and notification.

-   You saw that this approach aligns with the architecture (Lambda evaluating logs, publishing to SNS for emails).

Your reasoning is spot-on! CloudWatch Logs with subscription filters is exactly the right pattern for this use case---real-time, component-specific, and AWS-native.

Correct Answer:  A. Enable Amazon CloudWatch Logs to log the EKS components. Create a CloudWatch subscription filter for each component with Lambda as the subscription feed destination.

* * * * *
 
**A company is implementing an Amazon Elastic Container Service (Amazon ECS) cluster
to run its workload. The company architecture will run multiple ECS services on the
cluster. The architecture includes an Application Load Balancer on the front end and
uses multiple target groups to route traffic.
A DevOps engineer must collect application and access logs. The DevOps engineer then
needs to send the logs to an Amazon S3 bucket for near-real-time analysis.**

Which combination of steps must the DevOps engineer take to meet these requirements?
(Choose three.)

A. Download the Amazon CloudWatch Logs container instance from AWS. Configure
this instance as a task. Update the application service definitions to include the logging
task. <br />
B. Install the Amazon CloudWatch Logs agent on the ECS instances. Change the
logging driver in the ECS task definition to awslogs. <br />
C. Use Amazon EventBridge to schedule an AWS Lambda function that will run every 60
seconds and will run the Amazon CloudWatch Logs create-export-task command. Then
point the output to the logging S3 bucket. <br />
D. Activate access logging on the ALB. Then point the ALB directly to the logging S3
bucket. <br />
E. Activate access logging on the target groups that the ECS services use. Then send
the logs directly to the logging S3 bucket. <br />
F. Create an Amazon Kinesis Data Firehose delivery stream that has a destination of the
logging S3 bucket. Then create an Amazon CloudWatch Logs subscription filter for
Kinesis Data Firehose.




Understanding the Problem

-   Setup:

    -   Amazon ECS Cluster: Runs multiple ECS services (likely using tasks on EC2 or Fargate launch types).

    -   Application Load Balancer (ALB): Fronts the ECS services, routing traffic to multiple target groups (one per service).

    -   Logs to Collect:

        -   Application Logs: Logs generated by the containers in the ECS tasks (e.g., app-specific logs like /var/log/app.log).

        -   Access Logs: Logs from the ALB capturing HTTP requests (e.g., client IPs, request paths, response codes).

    -   Destination: An S3 bucket for near-real-time analysis.

-   Requirements:

    -   Collect application logs from ECS services.

    -   Collect access logs from the ALB.

    -   Send logs to an S3 bucket in near real time (implies minimal delay, ideally seconds).

-   Key Considerations:

    -   ECS application logs typically go to a logging driver (e.g., awslogs for CloudWatch Logs), but need to end up in S3.

    -   ALB access logs are natively supported and can be sent to S3 directly.

    -   "Near real-time" suggests streaming or frequent exports, not batch processes with long delays (e.g., hourly exports).

Let's evaluate each option to find the three steps that meet these requirements.




Option A: Download the Amazon CloudWatch Logs container instance from AWS. Configure this instance as a task. Update the application service definitions to include the logging task

-   What This Does:

    -   CloudWatch Logs Container Instance:

        -   This likely refers to a containerized version of the CloudWatch Logs Agent (e.g., amazon/cloudwatch-agent or aws-observability/aws-for-fluent-bit).

        -   You run this as a sidecar container in your ECS task to collect logs from other containers and send them to CloudWatch Logs.

    -   Configure as a Task:

        -   Add the CloudWatch Logs container as a sidecar to each ECS task definition, alongside the application container.

    -   Update Service Definitions:

        -   Update the ECS service to use the new task definition with the logging sidecar.

-   Analysis:

    -   Application Logs:

        -   A sidecar container (e.g., Fluent Bit or CloudWatch Agent) can collect logs from the application container (e.g., by mounting a shared volume or reading stdout/stderr) and send them to CloudWatch Logs.

        -   This works for ECS, especially on Fargate, where you can't install agents directly on the host (unlike EC2).

    -   Path to S3:

        -   Logs go to CloudWatch Logs first, but the requirement is to send them to S3. You'd need an additional step (e.g., a subscription filter to Kinesis Firehose, then to S3) to get logs from CloudWatch to S3.

        -   This option doesn't address the S3 step, leaving the solution incomplete.

    -   Access Logs:

        -   This doesn't address ALB access logs at all---it's only for application logs.

    -   Near Real-Time:

        -   Sidecar logging to CloudWatch Logs is near real-time (seconds delay), but getting logs to S3 requires another mechanism.

    -   Complexity:

        -   Using a sidecar is a valid approach but more complex than using the awslogs driver (B), which is built into ECS and achieves the same result (logs to CloudWatch) without a separate container.

-   Conclusion: This collects application logs but doesn't address S3 delivery or ALB access logs. It's also less efficient than the awslogs driver. A is not the best choice.



Option B: Install the Amazon CloudWatch Logs agent on the ECS instances. Change the logging driver in the ECS task definition to awslogs

Your first pick! Let's break this down:

-   What This Does:

    -   CloudWatch Logs Agent on ECS Instances:

        -   If the ECS cluster uses the EC2 launch type, the "ECS instances" are EC2 instances running the ECS agent.

        -   Installing the CloudWatch Logs Agent on these instances prepares them to send logs to CloudWatch Logs.

        -   However, for container logs, the agent isn't strictly necessary if you use the awslogs logging driver (more on this below).

    -   Logging Driver to awslogs:

        -   In an ECS task definition, the logConfiguration specifies the logging driver for containers:

            json

            ```
            "logConfiguration": {
              "logDriver": "awslogs",
              "options": {
                "awslogs-group": "/ecs/my-app",
                "awslogs-region": "us-east-1",
                "awslogs-stream-prefix": "ecs"
              }
            }
            ```

        -   The awslogs driver sends container logs (stdout/stderr) directly to CloudWatch Logs, without needing a separate agent.

        -   If using Fargate, the awslogs driver is supported natively---no agent installation required.

-   Analysis:

    -   Application Logs:

        -   The awslogs driver sends container logs to CloudWatch Logs, which is the standard logging solution for ECS.

        -   For EC2 launch type, the ECS instances need the CloudWatch Logs Agent (or proper IAM permissions) to send logs, but modern ECS setups often rely on the awslogs driver directly, which uses the ECS agent's permissions.

        -   For Fargate, no agent installation is needed---awslogs works out of the box.

    -   Path to S3:

        -   Logs go to CloudWatch Logs first. To get them to S3, we need another step (e.g., a subscription filter to Kinesis Firehose, then to S3).

        -   This option doesn't address the S3 delivery, but it's a foundational step for application logs.

    -   Access Logs:

        -   This doesn't address ALB access logs---it's only for ECS application logs.

    -   Near Real-Time:

        -   awslogs sends logs to CloudWatch in near real time (seconds delay), but S3 delivery requires another step.

    -   Agent Installation:

        -   If using EC2 launch type, installing the CloudWatch Logs Agent might be necessary for older setups, but the awslogs driver typically doesn't require it---the ECS agent handles log forwarding (as long as the instance role has CloudWatch permissions).

        -   For Fargate, this step is irrelevant---no agent can be installed.

-   Conclusion: This is a key step for collecting application logs from ECS tasks. It's the most straightforward way to get container logs to CloudWatch Logs, which can then be routed to S3 (via another step). The agent installation part is questionable (often unnecessary), but the awslogs driver is spot-on. B is a good choice for application logs.



Option C: Use Amazon EventBridge to schedule an AWS Lambda function that will run every 60 seconds and will run the Amazon CloudWatch Logs create-export-task command. Then point the output to the logging S3 bucket

-   What This Does:

    -   EventBridge Schedule:

        -   Schedule a Lambda function to run every 60 seconds using an EventBridge rule.

    -   Lambda Function:

        -   The Lambda runs the create-export-task command for CloudWatch Logs, which exports logs from a log group to an S3 bucket.

    -   Output to S3:

        -   The exported logs are written to the specified S3 bucket.

-   Analysis:

    -   Application Logs:

        -   If application logs are in CloudWatch Logs (e.g., via awslogs driver from B), this exports them to S3.

    -   Access Logs:

        -   ALB access logs aren't in CloudWatch Logs---they go directly to S3 (via D). This doesn't address access logs.

    -   Near Real-Time:

        -   create-export-task is a batch operation---it exports a range of logs (e.g., from a start time to an end time) to S3.

        -   Running every 60 seconds helps, but it's not truly near real-time:

            -   Export tasks take time to complete (minutes for large log volumes).

            -   Logs are batched, not streamed---there's a delay between log generation and S3 availability.

        -   Near real-time typically means seconds, not minutes. A streaming solution (e.g., subscription filter to Kinesis Firehose) is better.

    -   Efficiency:

        -   Exporting every 60 seconds creates many S3 objects (e.g., one per export task), which can complicate analysis.

        -   It's less efficient than streaming logs directly to S3.

-   Conclusion: This gets logs from CloudWatch to S3 but isn't near real-time (batch exports take minutes) and doesn't address ALB access logs. It's a partial solution for application logs but not the best approach. C is not the best choice.



Option D: Activate access logging on the ALB. Then point the ALB directly to the logging S3 bucket

Your second pick! Let's break this down:

-   What This Does:

    -   ALB Access Logging:

        -   ALBs support access logs, which capture HTTP request details (e.g., client IP, request URL, response code).

        -   You enable access logging on the ALB and specify an S3 bucket as the destination:

            json

            ```
            Attributes:
              access_logs.enabled: true
              access_logs.s3.enabled: true
              access_logs.s3.bucket: my-logging-bucket
              access_logs.s3.prefix: alb-logs
            ```

    -   Direct to S3:

        -   ALB writes access logs directly to the specified S3 bucket (e.g., as files like alb-logs/2025/03/01/logfile.gz).

-   Analysis:

    -   Access Logs:

        -   This directly addresses the requirement to collect ALB access logs.

        -   ALB access logs are written to S3 natively---no intermediate steps needed.

    -   Application Logs:

        -   This doesn't address ECS application logs---it's only for ALB access logs.

    -   Near Real-Time:

        -   ALB access logs are written to S3 in near real time---logs are typically available within seconds to a few minutes (AWS batches them into files every 5 minutes or so, but this is still considered near real-time for most use cases).

    -   Efficiency:

        -   This is the simplest, most direct way to get ALB access logs to S3---no additional services or processing required.

-   Conclusion: This is a necessary step for ALB access logs. It meets the requirement for access logs and delivers them to S3 in near real time. D is a great choice.



Option E: Activate access logging on the target groups that the ECS services use. Then send the logs directly to the logging S3 bucket

Your third pick! Let's break this down:

-   What This Does:

    -   Access Logging on Target Groups:

        -   Target groups are part of the ALB configuration---they route traffic to ECS tasks.

        -   However, target groups do not support access logging. Access logging is a feature of the ALB itself, not the target groups.

    -   Send Logs to S3:

        -   If target groups supported logging, this would send logs to S3.

-   Analysis:

    -   Access Logs:

        -   This is factually incorrect---target groups don't have access logging. ALB access logging (D) captures all relevant request data, including which target group handled the request (via the target_group_arn field in the log).

        -   There's no need to log at the target group level---ALB logging already covers this.

    -   Does It Meet Requirements?:

        -   No, because target groups don't support access logging.

-   Conclusion: This option is incorrect due to a misunderstanding of ALB and target group capabilities. ALB access logging (D) is the correct approach. E is incorrect.



Option F: Create an Amazon Kinesis Data Firehose delivery stream that has a destination of the logging S3 bucket. Then create an Amazon CloudWatch Logs subscription filter for Kinesis Data Firehose

-   What This Does:

    -   Kinesis Data Firehose:

        -   Firehose is a streaming service that can deliver data to destinations like S3.

        -   You create a Firehose delivery stream with the logging S3 bucket as the destination.

    -   CloudWatch Logs Subscription Filter:

        -   A subscription filter in CloudWatch Logs (e.g., on the ECS log group) streams logs to Firehose.

        -   Firehose buffers the logs (e.g., for 60 seconds or 1 MB) and writes them to S3.

-   Analysis:

    -   Application Logs:

        -   If ECS logs are in CloudWatch Logs (e.g., via awslogs driver from B), this subscription filter streams them to Firehose, which delivers them to S3.

        -   This completes the path for application logs: ECS → CloudWatch Logs → Firehose → S3.

    -   Access Logs:

        -   This doesn't address ALB access logs, which aren't in CloudWatch Logs---ALB logs go directly to S3 (via D).

    -   Near Real-Time:

        -   Firehose streams logs to S3 in near real time---buffering delays are typically 60 seconds (configurable), which qualifies as near real-time for this use case.

        -   This is much better than batch exports (e.g., create-export-task in C, which takes minutes).

    -   Efficiency:

        -   Firehose is a managed service, handling scaling and buffering automatically.

        -   It's a standard pattern for streaming CloudWatch Logs to S3.

-   Conclusion: This is a critical step for getting application logs from CloudWatch Logs to S3 in near real time. It complements B (collecting logs) by providing the delivery mechanism. F is a great choice.



Analysis: Are B, D, and E the Right Combination?

Your picks:

-   B: Install the CloudWatch Logs agent on ECS instances and use the awslogs driver in the task definition.

-   D: Activate ALB access logging and send logs to S3.

-   E: Activate access logging on target groups and send logs to S3.

Evaluation:

-   B:

    -   Correct for application logs---awslogs sends ECS container logs to CloudWatch Logs.

    -   The agent installation part is unnecessary for Fargate and often not needed for EC2 (the ECS agent handles awslogs with proper IAM permissions), but the awslogs driver is the key piece.

    -   This is a necessary step, but it needs a way to get logs to S3 (which E doesn't provide).

-   D:

    -   Correct for ALB access logs---enables logging on the ALB and sends logs directly to S3.

    -   Meets the access logs requirement in near real time.

-   E:

    -   Incorrect---target groups don't support access logging. ALB logging (D) already covers this.

What's Missing?:

-   Application Logs Path to S3: B gets logs to CloudWatch, but we need a step to stream them to S3. F (Kinesis Firehose with a subscription filter) completes this path.

-   Correct Combination:

    -   B: Collect application logs (awslogs driver → CloudWatch Logs).

    -   D: Collect ALB access logs (ALB → S3).

    -   F: Stream application logs to S3 (CloudWatch Logs → Firehose → S3).

Why E Doesn't Fit:

-   Target group logging isn't a thing---D already handles ALB access logs.

Correct Combination: B, D, and F.

-   B: Sets up application log collection to CloudWatch Logs.

-   D: Handles ALB access logs to S3.

-   F: Streams application logs from CloudWatch to S3 in near real time.



Why You Picked B, D, and E

-   B: You recognized that ECS uses the awslogs driver to send container logs to CloudWatch Logs, a standard practice for application logs.

-   D: You correctly identified that ALB access logs can be sent directly to S3, meeting the access logs requirement.

-   E: You might have thought target groups could log separately to capture service-specific traffic, but ALB logging (D) already includes target group details in its logs (e.g., target_group_arn field).

You were very close---B and D are spot-on, and E was a reasonable guess if you weren't sure about target group logging. Now you know that ALB logging covers it, and F completes the application logs path to S3.

Correct Answer: B, D, and F.

-   B. Install the Amazon CloudWatch Logs agent on the ECS instances. Change the logging driver in the ECS task definition to awslogs.

-   D. Activate access logging on the ALB. Then point the ALB directly to the logging S3 bucket.

-   F. Create an Amazon Kinesis Data Firehose delivery stream that has a destination of the logging S3 bucket. Then create an Amazon CloudWatch Logs subscription filter for Kinesis Data Firehose.

* * * * *


 <br />
  <br />