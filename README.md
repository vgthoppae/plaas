# Pipeline as a Service (Plaas)
A Jenkins Pipeline service that can deploy applications to AWS Cloud environment based on yaml file configurations

## Background
The current industry trend favors micro applications at all layers - front end, back end and anything in between, which naturally multiplies the number of artifacts being deployed and the number of lifecycle environments in enterprise project further contributing to the volume. With Jenkins, the most popular CI/CD tool in integration with github, Pipeline is a preferred choice to port code through different stages before deploying to a target environment.

Some projects prefer to build a separate pipeline for each app, which may not be the best choice in all circumstances. This implementation provides a single pipeline service that could potentially deploy any number of apps.

## How
This is really not any groundbreaking idea but rather one out of simple common sense, most of the companies may be practicing a similar technique in some fashion or other. Hate to repeat the most obvious but here is a common pipeline principle outlined below.

![A pipeline template] https://github.com/vgthoppae/plaas/blob/master/images/plaas-pipe.png

A pipeline simply transports the code through different stages on successful execution (failure paths are not shown here) until deploying it in a target environment. The variant between different pipelines is of course the code in flight and several other parameters. Plass service makes generalization possible by identifying those variant parameters, externalizing them and feeding it to a stage as and when required. That's it. As I said, it is not really a big deal.


## Why
Why should one do this? 
* The first and foremost motivation is that it helps with drawing a clear line of responsibility between DevOps team and Application Developers. A set of parameters is provided by both DevOps and App team. DevOps maintains Plaas and provides System level parameters or any parameters thery don't developers to control. App Developers provide app specific parameters.
* There is zero repetition of code - you code once and apply it everywhere. Think of maintenance
* You get clarity on what is going on and what are the parameters needed to run the pipeline
* It is really really simple and easier than maintaining 100 piplines 


##Onboarding new apps
This is really the best feeling you would have once you got this implemented.

* Write AWS cloudformation stack with jinja style markup templates remembering to use placeholder parameters for all variable sections
* Define system level parameters at plaas/app-metadata/<app name>-params.yaml
* Have developers define app specific params in their repo at <project root>/deployment/params.yml
* Add Je


## Questions

* I don't like to put all eggs in one basket...
Well..you could still use this as a master pipeline and clone it to create other pipelines. You can go as granular as you want. But still there is only one code base for all the pipelines. Only the Jenkins artifact is separate for each pipeline

* I don't think this idea would scale up to an enterprise level project. Yours is a very trivial app..
I highly doubt it, though you could argue that there is not enough ROI in implementing this for your project, which is a different story. But technically it is feasible. If you like code not getting repeated in 100 different places, you should take a look at it or a similar technique






