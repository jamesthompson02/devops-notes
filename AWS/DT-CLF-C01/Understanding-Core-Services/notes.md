# Understanding AWS Core Services


## Interacting witth AWS (new section)

### Methods of Interacting with AWS

3 main ways:
1. AWS Console (just a browser tool)
2. AWS CLI (Command Line Interface for administering AWS resources)
3. AWS Software Developer Kit (programmatic access to manage AWS resources)

Console is a great tool for testing out new AWS services
Repeating tasks can be automated using the CLI or SDK.


### Using the AWS Console


On the toolbar on right-hand-side (just to left pf where you can view your user account details) is where you can set your region.

AWS Lambda lets you run code without having to worry about servers.

Route 53 is a global service. 

Note: in your user account from the top-right-hand corner of the toolbar you can click on ‘Security Credentials’. From here, you can create access keys which permit you to interact with  Amazon APIs.


### Using the AWS CLI

Just note: when creating an access key to interact with amazon APIs, it’s advisable you create these for an IAM account rather than for a root user account. A root user accounts has no permission restrictions on it and can do anything with your account (including deleting it). An IAM account, on the other hand, has limited permissions and, therefore, if the account and key get compromised, it is not as damaging for you.

When you create your access key, it is important that you download/save it ASAP. After it has been created, you cannot access it again.

You can either install the AWS CLi or, alternatively, you can use something called CloudShell. Note: CloudShell is accessible from the toolbar. It is an icon just to the left of the notifications icon and has these characters as the icon >_.

CloudShell has the AWS CLI installed. Note: learning about the kinds of commands you can use in the AWS CLI will require further research and investigation. However, it appears that the AWS CLI commands have similarities with Docker as well as general terminal commands.


 ## Compute Services (new section)

Compute services are simply services that enable you to leverage virtual machines in the cloud for workloads e.g. serving web content, running a database etc.

3 main compute services to consider:

1. Amazon EC2 - provides secure and resizable virtual servers.
2. AWS Elastic Beanstalk - platform for scaling and deploying web apps and services.
3. AWS Lambda  


### Amazon EC2 Overview

#### Use cases for EC2:

1. Host a web application in the cloud. We could spin up an instance of EC2, on that instance a server could be installed, and on that server we could put the files of our web application.
2. Batch Processing
3. Could use it as an API server.
4. Have a desktop in the cloud.


Two types to bear in mind when thinking about EC2: instance types and root device types. Also need to think about Amazon Machine Images as well as Purchase Options.

#### EC2 Instance types


The instance type defines the processor, memory and strorage type. Cannot be changed without downtime. Pricing is based on instance type.

#### EC2 Root Device types


There are two main root device types:
1. Instance Store. This is ephemeral storage that is physically attached to the host that the virtual server is running on. Note that because storage is ephemeral, if you shut down the EC2 instance, all the data stored on it will be wiped.
2. Elastic Block Store. This is persistent storage that exists separately from the host the virtual server is running on. Because this is persistent, even after shutting it down, data will still be stored.

#### Amazon Machine Images


This is a template for an EC2 Instance including configuration, OS, and data.

AWS provides many Amazon Machine Images.

AMIs can be shared across AWS accounts.

Custom AMIs can be created. 


#### Amazon EC2 Purchase Types


There are numerous different purchase types to choose from such as:
1. On-Demand. This is the default option.
2. Reserved. Provides discounts compared to on-demand model when you commit to a specific period of time (e.g. 1 or 3 years).
3. Savings plan. Similar to Reserved except it’s not just an option for EC2. It’s also an option for things like Fargate and AWS Lambda. Moreover, it does not reserve capacity (unlike Reserved). 
4. Spot. Can provide up to 90% discounts when compared to on-demand.
5. Dedicated. Gives you a dedicated physical server but is most expensive option.


#### Launching EC2 Instances


Starting from the homepage of the AWS Console, go to the searchbar at the top and type in EC2. Select EC2 and then scroll down to look for ‘Launch Instance’. Once you click it, you’ll be brought to a set up page to set up your EC2 Instance.

First step: name your EC2 Instance. 

Second step: Select an AMI you wish to use to configure your EC2 instance type. You can choose from QuickStart AMIs or AWS Marketplace AMIs. Note: it’s probable that using the marketplace AMIs will incur extra expenses.

Third step: Select an Instance type. An example of an instance type is t2.micro. These differ according to attributes like number of CPUs and amount of memory storage. 

Fourth Step: Select a key pair. A simplified explanation is that the key pair is a bit like a password that allows you to log into your server and manage it. 

Fifth Step: Configure network settings. With respect to security, configure the ‘Allow SSH traffic from’ option to only be from your IP address. Also you can select the ‘Allow HTTP traffic from the internet’. 

Sixth Step: Configure storage.

Seventh Step (optional): Click on ‘Advanced Details’ and scroll down to where it says “User Data”. This is an input where you can insert scripts for the server to run when starting up.

Eighth Step: Launch instance. Once launched you should see the name of your new Instance. Click on the name. When it starts running look out for Public IPv4 DNS - this is the url for the server.

Ninth Step: to terminate an instance, look for the dropdown menu that says ‘Instance type’.




### AWS Elastic Beanstalk Overview


Automates the process of deploying and scaling workloads on EC2 (PaaS).

Supported application platforms include: python, docker and node.js. 

Elastic Beanstalk handles: monitoring, deployment, scaling and EC2 customisation.

Good for deploying applications when you have minimal knowledge of how to use other AWS products. It also reduces the overall maintenance needed for the application. Good when you only need a general amazon machine image.



### Launching an app on Elastic Beanstalk


First step: having searched for it using the searchbar in the AWS Console, select it and then click on ‘Create application’. 

Second step: give application a name.

Third step: choose the platform (e.g. python, node.js etc).

Fourth step: underneath heading ‘Application code’ select ‘upload your code’. It will then prompt you to upload a ‘local file’. Despite it saying file this is where you upload a zip folder.

Fifth step: click on ‘create application’ to launch it. Once it’s launched it will provide a url where the app is served. 

Sixth step (optional): you can delete the app by going to the dropdown menu that says ‘actions’ and click on ‘Terminate Environment’. 




### AWS Lambda Overview

Enables the running of code without provisioning infrastructure. Only charged for usage based on execution time. Integrates with many AWS Services easily (e.g. S3, dynamoDB). Primary service for serverless architecture.Enables fault tolerance without additional work. Sclaes based on demand. Pricing is based on usage.



### Container Services


Amazon ECS is useful for this.

Two types of container orchestration compute engines: Amazon EC2 and AWS Fargate. 


### Selecting a Container Service

App Runner requires no prerequisite knowledge of containers or infrastructure.

ECS natively integrates with many AWS Services.

EC2 provides maximum control for configuration of scaling with containers. 

Fargate reduces amount of stuff you have to manage for container orchestration.



## Content and Network Delivery Services (new section)

There are 6 networking and content delivery services that are worth remembering:

1. Amazon Route 53
2. Amazon VPC
3. AWS Direct Connect
4. Amazon API Gateway
5. Amazon Cloudfront
6. Elastic Load Balancing

### Amazon VPC (Virtual Private Cloud)

An Amazon VPC is a logically isolated part of the cloud where you can launch AWS resources in a network that you define. In short, this enables virtual networks within AWS.

Amazon VPC also supports both IPv4 and IPv6 addresses.

Allows for config of: IP address range, subnets, route tables and network gateways.

Supports both public and private subnets. Private means that it can’t communicate with the internet at large, whereas with public it can connect to the internet (and vice versa).

Enables a connection to your own data centre.

Can connect to other VPCs.

Supports private connections to many AWS services.


### AWS Direct Connect

A cloud service solution that makes it easy to establish a dedicated network connection from your data centre to AWS.


### Amazon Route 53

This is AWS’s DNS service. 

It’s a domain name service. 

It’s a global service (not regional). This means it does not require region selection. Changes get applied globally (everywhere your app is served).

It’s highly available - so minimal downtime. Also means if a server goes down in one region traffic can quickly be re-routed to rely on a server in a different location.

Enables global resource routing. 

Route 53 Dashboard can be accessed via AWS Console.


### Elastic Load Balancing

The key way it upholds the principle of elasticity is by distributing traffic across multiple targets (E.g. servers), based on the current workload of those targets (targets e.g. servers will receive more traffic than others if they have a lower current workload).

Integrates with EC2, ECS and Lambda. Note: ECS is AWS’s container service (e.g. running docker containers).

Supports 1 or more availability zones in a region.

Has 3 types of load balancers:

1. Application Load Balancer
2. Network Load Balancer
3. Classic Load Balancer


### Scaling on Amazon EC2

Two types of scaling: vertical and horizontal. Vertical is when you have an instance (or multiple instances) and you realise that your servers do not necessarily have the specs to be able to cope with additional demand. In this case, vertical scaling is taking a pre-existing server and upgrading it to something with better specs (E.g. performance, memory, storage etc.). This is usually not advisable since it requires downtime to get the new, upgraded instance up and running.

Alternatively, you can do horizontal scaling. This is essentially when the more instances of the same type are spun up when necessary to meet the challenge of additional demand. This is the preferred method for scaling up.


### Amazon Cloudfront

It’s a service that leverages the edge locations within the AWS Global infrastructure. It’s a content delivery network. Enables content to be served to users from the server that is geographically closest to them (speed is everything). 

Supports static and dynamic content.

Includes advanced cybersecurity features like:

1. AWS Shield for DDOS attacks
2. AWS Web Application Firewall


### Amazon API Gateway

Fully managed API management service. Directly integrates with multiple AWS Services. 

Provides monitoring and metrics on API calls.

Supports VPC and on-premise private applications. 


### AWS Global Accelerator

This is a networking service that sends your users’ traffic AWS global network infrastructure, improving internet user performance substantially. 

Utilises IP addresses that route to edge locations. 

Once request reaches an edge location, it uses an AWS network to route that traffic - rather than just the internet.

Can route requests to many different AWS resources (e.g. EC2 instance).


### When to use AWS Global Accelerator vs. Cloudfront


When using a non-HTTP Protocol. 

Requires a static IP. 


## File Storage Services (new section)
