# Jenkins

## What is it?

An automation platform that allows you to build, test and deploy software using pipelines. Helps facilitate continuous integration and continuous deployment.


## Jenkins Infrastructure 

1. Master Server - controls pipelines and assigns builds to Agents
2. Agents - Run the build in their workspace. Tend to be static computers.

## Typical Workflow for Jenkins

1. User pushes some code to a repository (e.g. Github/Bitbucket)
2. Master Server becomes aware that a commit has been pushed and triggers the appropriate pipeline
3. Master Server will then assign an Agent the task of running the new build. It will assign a particular Agent based on configuration labels.
4. Agent will then run build. Usually just a bunch of Linux commands.

## Agent Types

There are two types of agents: 
1. Permanent Node Agents - Dedicated servers for running jobs.
2. Cloud Agents. Dynamic agents spun up on demand. Examples of these types are: Docker, Kubernetes and AWS fleet manager.


## Build Types

1. Freestyle builds. Simplest method to create a build. Like shell scripts, that can be triggered by specific events (e.g. pushing commits).
2. Pipelines. Use the groovy syntax. Use Stages to breakdown Components of builds.

Example of pipeline:   stages {
stage('Clone') {
steps {

}
}
stage('Build') {
steps {

}
}
stage('Test') {
steps {
}
}
stage( 'Package') { 
steps {
}
}
stage(‘Deploy') {
steps {
}
}
}


## Jenkins GUI

### Manage Jenkins

This is a heading that should be apparent after the initial set up of Jenkins. It will be on the left-hand-side of the screen and this is where you can set up and manage agents for the master server.

Configuring Jenkins as an admin user (this is inside the ‘Manage Jenkins’ segment of Jenkins GUI)

Under the ‘System Configuration’ section, you will first want to ‘Configure System’. Subsequent to that, you will want to click on “Manage Plugins”.  

A key one under the ‘System configuration” section is ‘Manage Nodes and Clouds’ - this is where you will set up Agents for the Master Server.

Under the ‘Security’ section, you can see a range of options to configure your security settings. One heading worth note is ‘Manage Credentials’, which is what’s used for things like SSH keys and API keys. Be aware that whilst Jenkins provides this option to store credentials, it’s not obligatory. You could use another credentials manager like AWS Secrets, for example.

Underneath ’Tools and Actions’, there is an option which says ‘Prepare for Shutdown’. Always use this if you wish to shut down Jenkins as this minimises the interruption caused, particularly if Jenkins is already doing other jobs.


### New Item (like Manage Jenkins, should be available on the left when on the main dashboard). - Note, the following assumes you’re choosing a FreeStyle Project rather than a pipeline.

New Item is used to create new projects. Pick a name for your new project (never have spaces in the name of the project, use kebab case (E.g. new-project). The form of item you will probably select is either “FreeStyle Project” or “Pipeline”.  

You will then be taken to the project settings.

First option to examine is the Source Code Management section. Choose Git to manage the source code and give the URL for a specific repo (assumes you’ve already set up the repo). Note: you need to set up credentials if it is a private repo. 

Next option to examine is Build Triggers. Popular option is to have Github send a web hook to your Jenkins server - this may prove impossible to do though due to your Jenkins server being behind a firewall. A get around for this issue is to select “Poll SCM”. This option will allow your Jenkins server to reach out periodically to your Github repo to look for changes. Another option worth considering is ‘Build Periodically’. 


Next option is Build Environment. A common checkbox to tick here is “Delete Workspace before build starts’. This ensures you have a clean workspace each time a build is set up. 

You will then have “Build” and “Post-Build Actions” underneath. For the build step it is common to simply select Execute Shell from the Add build step option. Once execute shell is selected, a command textbox will appear for you to type commands. Just under that textbox there should be an option to see a list of available environment variables. A common environment variable to use is the BUILD_ID. Another is the BUILD_URL.
Commands will typically start with the word echo, and actual commands will be inside speech marks. 

Example: 

echo “Hello, World!”


Once you hit save you will be taken to a new page where you can look at things like the status of your newly created project. There should also be an option on the left which says ‘Build Now’. To edit the settings of your newly created project, go to the “Configure” section which Is also on the left-hand-side of the screen.

After you hit Build Now, you will be taken to the status page. This will let you know whether your build is successful or not. The Console Output option on the left-hand-side is also useful to see the logs of your build. 

The Workspace option on the left-hand-side allows you to look at all the files in the project.

## Exploring Jenkins file system 

To look for files inside a directory when running a Jenkins container, assuming your using a bash terminal:

ls -ltra

Inside the var folder is where you will do a lot of troubleshooting. Folders like updates and plugins are where you might need to go to resolve issues.


## Setting up Docker Cloud Agents

On the main dashboard, go to ‘Manage Jenkins’. Under System Configuration click ‘Manage Nodes and Clouds’. 

To set up a new agent click on Configure Clouds (New Node is the old, deprecated way to set up an agent). Click on ‘go to plugin manager’. Go to the available tab and install the relevant plugin (e.g. Docker). Then restart the Jenkins master. Once you’ve signed back in, go to Manage Jenkins, then ‘Go to Plugin Manager’, and then click on the Installed tab. If you installed Docker, Docker should be there now. 

Assuming you have installed something like Docker correctly through the plugin manager, when you go to the configure clouds option you should have a drop-down menu saying Add a new cloud. Once you’ve selected the type of cloud you want, click on ____ cloud details (___ will be Docker if you have installed Docker). 	

(Rest of notes assumes that Docker has been used).

Once you’ve done that, you need to provide a Docker Host URI. If you want to run the Jenkins server on your own PC, you have to enter unix or tcp address of the docker host. The problem is that since you’re running Jenkins as a container, the container can’t reach docker host unix port. To combat this, you have to run another docker container that can mediate between Jenkins containers and docker host. The mediator container will publish docker host’s unix port as its tcp port. The type of Docker container you need for this role is a socat container. 


When you’ve created your socat container and it is up and running, you will want to run a docker inspect on it. Look underneath Networks for IPAddress.

Once you’ve done that, you can enter for the docker host uri tcp://<socat-container-ipaddress>:<tcp-listen-flag-for-socat-container>

## Creating a Docker Agent Template

Give your Agent Template a label. Enable the label.

Give the agent the same name as the label.

Then give your agent its own Docker Image. 

Instance capacity is important to define too. If you’re working on a personal project, keep this number low (e.g. 2). 

Also make sure you input something for the Remote File System root (e.g. /home/jenkins.

Then scroll down to the bottom and click save. 

Once you’ve created the agent, you can go back into ‘Configure’ for your project and, underneath General, can click Restrict where this project can be run. Then provide the label expression. 


## Customising your Jenkins Agent (assumes you’re using Docker Cloud)

Imagine you need to run a python application 
