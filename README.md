# Pipeline as a Service (Plaas)
A Jenkins Pipeline service that can deploy applications to AWS Cloud environment based on yaml file configurations

## Background
The current industry trend favors micro applications at all layers - front end, back end and anything in between, which naturally multiplies the number of artifacts being deployed and the number of lifecycle environments in enterprise project further contributing to the volume. With Jenkins, the most popular CI/CD tool in integration with github, Pipeline is a preferred choice to port code through different stages before deploying to a target environment.

Some projects prefer to build a separate pipeline for each app, which may not be the best choice in all circumstances. This implementation provides a single pipeline service that could potentially deploy any number of apps.

## How
This is really not any groundbreaking idea but rather one out of simple common sense, most of the companies may be practicing a similar technique in some fashion or other. Hate to repeat the most obvious but here is a common pipeline principle outlined below.

![alt text](https://github.com/vgthoppae/plaas/blob/master/images/plaas-pipe.png "A pipeline template")

A pipeline simply transports the code through different stages on successful execution (failure paths are not shown here) until deploying it in a target environment. The variant between different pipelines is of course the code in flight and several other parameters. Plass service makes generalization possible by identifying those variant parameters, externalizing them and feeding them to a stage as and when required. That's it. As I said, it is not really a big deal.

All the initial stages through scanner are implemented with groovy while the next two stages leverage Ansible to take advantage of native integration with Jinja template library.

The laborious and somewhat complicated step is building the cloudformation template. But you build a template once for a certain flavor of stack - for example a stack consisting of Apache, JBoss and DynamoDB (unique combination here...), or Apache, EC2, DMS, RDS, S3 etc., All the fields that would vary between apps are externalized and defined in app specific params file.

Typically two git repositories are involved. In this implmentation,

* https://github.com/vgthoppae/plaas is the repo for DevOps which consists of pipeline code and app specific params file
I use an app called cheddar which consists of a single RDS instance.

... <https://github.com/vgthoppae/plaas/app-metadata/cheddar-params.yml> contains system parameters maintained by the DevOps team

* <https://github.com/vgthoppae/plaas-cheddar-app> is the repo for the cheddar application, which in this case contans nothing by the deployment params due to the brevity of the app

... <https://github.com/vgthoppae/plaas-cheddar-app/vt-plaas/deployment/params.yml> contains application parameters supplied by the application team

App team would typically build a pipeline from a screen like this, where they choose their application name and hit the button. Needless to say, you can add other parameters to further customize the experience say adding the desired stages, choosing the repo, branch etc.,

![alt text](https://github.com/vgthoppae/plaas/blob/master/images/plaas-buildjob.png "Developers experience")

## Why
Why should one do this? 
* The first and foremost motivation is that it helps with drawing a clear line of responsibility between DevOps team and Application Developers. A set of parameters is provided by both DevOps and App team. DevOps maintains Plaas and provides System level parameters or any parameters thery don't developers to control. App Developers provide app specific parameters.
* There is zero repetition of code - you code once and apply it everywhere. Think of maintenance
* You get clarity on what is going on and what are the parameters needed to run the pipeline
* It is really really simple and easier than maintaining 100 piplines 
* Dollars..Dollars..Dollars: A significant cost savings with upfront development and ongoing maintenance

## Onboarding new apps
This is really the best feeling you would have once you got this implemented.

* Write AWS cloudformation stack with jinja style markup templates remembering to use placeholder parameters for all variable sections
* Define system level parameters at plaas/app-metadata/<app name>-params.yaml
* Have developers define app specific params in their repo at <project root>/deployment/params.yml
* Add the new app name in the pipeline parameter choice 
* Rock and Roll...


## Questions

* I don't like to put all eggs in one basket...
Well..you could still use this as a master pipeline and clone it to create other pipelines. You can go as granular as you want. But still there is only one code base for all the pipelines. Only the Jenkins artifact is separate for each pipeline

* I don't think this idea would scale up to an enterprise level project. Yours is a very trivial app..
I highly doubt it, though you could argue that there is not enough ROI in implementing this for your project, which is a different story. But technically it is feasible. If you like code not getting repeated in 100 different places, you should take a look at it or a similar technique

* Can I replace ansible steps with other tools?
Yes, very well. Anything that helps support write markup templates and that can interface with AWS SDK.






