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