# Fundamental Cloud Concepts for AWS


## Understanding Cloud Computing (new section)


### Advantages of Cloud Computing (versus Traditional Data Centres) 


1. Traditional data centres require a large upfront investment to build. This includes finding commercial property, paying the rent on that property, buying different types of servers for that data centre (e.g. server for the website content, server for users to upload own content (e.g. pictures/videos) and database server to store user information like emails, usernames and passwords). Cloud computing avoids this.
2. For a traditional data centre to be profitable, the business has to be very good at forecasting demand. Cloud computing does require forecasting demand.
3. Deploying new traditonal data centres is a lengthy time process. It often takes months to get them to a point where they can start serving the business. Cloud can simply spin up new instances when required.
4. Maintenance of trad data centres is expensive. 
5. Building a traditional data centre means placing all the security and regulatory burden upon yourself. Cloud computing means outsourcing that burden to somebody else.
6. Cloud computing benefits from economies of scale.

Key concept: Elasticity. The ability to acquire resources when needed and release them when they’re not needed. Cloud does this automatically.

Key concept: Reliability. AWS has global infrastructure so even if it goes down in one area it can be used in other areas of the globe.

Key concept: Agility. Cloud lowers costs for businesses who wish to experiment with new ideas. Reduces time required to maintain infrastructure. Also reduces security and compliance risk.



### Types of Cloud Computing


Think of cloud computing as a spectrum. On one end, you have have maximum control over your servers in the cloud. On the opposite end, you have minimum control (but also minimal burdens and responsibility) over your servers in the end.


The maximum control end of the spectrum can be thought of as Infrastructure as a service (IaaS). This means we can do things like change the OS on the servers and have complete control over their configurations. We also have to do maintenance on the servers.



The minimal control end of the spectrum can be thought of as Software as a System (SaaS). 


In the middle of the spectrum there is something called Platform as a Service (PaaS). This is where our servers our deployed for us but we have to think about how to customise these servers to suit our needs. 



### Cloud Deployment Models


1. Public Cloud. This is the most relevant one. This is where the cloud is deployed onto a public cloud provider like AWS, Microsoft Azure etc.
2. Private (on Premises) Cloud. Examples include VMWare. 
3. Hybrid Cloud. Combo of public and private.



## AWS Global Infrastructure (new section)

4 distinct areas to bear in mind:

1. Regions
2. Availability Zones
3. Local Zones
4. Edge locations


### AWS Regions and Availability Zones

Each region is located in a specific georgraphic location.Each geographic location has a cluster of data centres.AWS has approximately 30 regions. 

Availabilty zones contain multiple data centres. Having multiple availabilty zones within each region ensures that anything your application relies on doesn’t go down. In other words, if one availability zone goes down, another one should be able to take its place from the same region.


### Region and availability zone naming conventions

Example: us-east-2a => the letter at the end is for the availabilty zone. us-east-2 is the region name. 


### Local and Wavelength Zones


Local zones are intended to bring services closer to end users. Each local zone location is an extension of the region.

Wavelength zones is to do with 5g. 



### AWS Edge Locations

Points of Presence are elements of AWS global infrastructure that exist outside of regions. Points of presence can be split into two categories: edge locations and regional edge caches. 

Edge locations are used as nodes in global content delivery network. Amazon Cloudfront and Amazon Route 53 use these locations. Allows AWS to serve content from locations closest to end users. 



## Understanding Cloud Economics (new section)


Two key concepts to bear in mind: capital expenditure and operating expenditure. Capital expenditure relates to those upfront costs related to attaining a fixed asset. This fixed asset could be the purchase of a building, servers and other support equipment - all items needed to build a data centre. Operating expenditure is more closely associated with maintenance costs. When you use the cloud, you only have to worry about operating expenditure - capex is a thing of the past.


### Organising and optimising AWS Costs


A useful tool for organising and analysing the costs of AWS is the AWS Cost Explorer. This tool provides breakdowns of costs according to: services, cost tags etc. It also provides predictions of what your costs will be for the next 3 months. 

Another tool is AWS Budgets. This tool takes data from the AWS Cost EXplorer to track your usage across each AWS service. 

Another tool is the AWS Pricing Calculator. Enables analysis of the cost of using multiple AWS services. 

Another tool is the AWS Migration Hub. Provides a business case for transitioning apps to the cloud. 

Be aware of deprecated tools like AWS TCO calculator, AWS Simply Monthly Calcultor. 

AWS Resource tags are simply metadata that get assigned to resources within your account. You can use these to name resources you’re using on AWS. Benefit of it is that you can quickly search for how much money is being spent on resources with that tag name. Also used to distinguish between different departments, environments and projects. 

Another tool is AWS Organizations. Allows companies to manage multiple accounts under a single master account. 


### Using the AWS Pricing Calculator


Used to estimate future monthly costs and workloads. 



## Supporting AWS Infrastructure (new section)


### AWS Support


A key tool is AWS Support. Allows you to file support requests with AWS Resources. Within AWS Support, there are 2 notable services: AWS Personal Health Dashboard and AWS Trusted Advisor. AWS Support is provided in different tiers (based on need and scope). 

AWS Personal Health Dashboard. This tool provides alerts and remediation guidance when events are happening that may impact you.

AWS Trusted Advisor. Automated tool that allows you to check your usage against best practices. Can be accessed from the AWS Console. Trusted Advisor has a number of different checks which can be divided into 5 main categories:
1. Cost Optimisation
2. Performance
3. Security
4. Fault tolerance
5. Service limits


### AWS Support Plan Tiers


Differences between the various AWS support plan tiers can be broken down into 4 categories:
1. Communication method
2. Response time
3. cost
4. Type of guidance

AWS Basic suport is the first tier that everyone has access to. Access to Trusted Advisor. Don’t have access to support engineers.

AWS Developer support. Get everything in AWS Basic Support as well as: access to support engineers, starts at $29/ month.

AWS Business Support. Can access support engineers at any time. Provides 3rd-party software support (e.g. Docker). Price starts at $100/month.

AWS Enterprise Support. Starts at $15,000/month.



### AWS Support Tools

AWS console is just a webpage. 



### Assistance for Cloud Workloads

One useful tool is AWS Quick Starts. 

Another is the AWS Partner Network Consulting Partners. 

Another is the AWS Professional Services. 
