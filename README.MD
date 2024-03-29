# Flask CI - Dor Dagani

Flask CI is a flask based application build by ci/cd concept with complete automation of building testing and deploying the software.

**Server access information will be sent separately!**

**The repository contains the code that I wrote (with Jenkinsfile): https://github.com/dordagani/dor_app**


## Pre-requistes

Two Linux servers (the guide is tested on Amazon Linux AMI):

1. Install the first server ("CI_Server") according to the [following guide](guides/ci_server.MD#section)


2. Install the second server ("Docker-Prod_Server") according to the [following guide](guides/docker.MD#section)


## Config


Adding a GitHub Webhook in Your Jenkins Pipeline :

1. Go to your project repository.
2. Go to "settings" in the right corner.
3. Click on "webhooks."
4. Click "Add webhooks."
5. Write the Payload URL as
   http://<jenkins_ip>/github-webhook/

<p align="center"><img src="/images/git_webhook.png" /></p>

Create a pipeline job from the Jenkins interface :

1. Click New Item on your Jenkins home page, enter a name for your (pipeline) job, select Pipeline, and click OK.
2. Check the "GitHub hook trigger for GITScm polling" option below the Build Triggers area. 
3. Change Pipeline Definition to "Pipeline script from SCM", set the SCM to "Git" and add the Repository URL (https://github.com/dordagani/dor_app.git)
4. Click Save.

<p align="center"><img src="/images/pipeline_job.png" /></p>

Add Docker Hub Credentials: 

1. Click Credentials -> System -> Global Credentials 
2. Add your Docker Hub credentials as the type Username with password, with the ID docker-hub-credentials
3. Click OK

<p align="center"><img src="/images/docker_hub_cred.png" /></p>

Add Docker Production SSH Credentials ("Docker-Prod_Server"): 

1. Click Credentials -> System -> Global Credentials 
2. Add your Docker Production SSH credentials as the type Username with password, with the ID docker-prod-credentials
3. Click OK

<p align="center"><img src="/images/docker_prod_cred.png" /></p>

Change the local IP address of the Docker-Prod_Server in the file /provision/inventory.ini so that Ansible will be able to connect to the correct Docker server

## Usage 

When user performs git push to GitHub repository, the following process is performed automatically:

![flow](/images/dor-ci.png)
