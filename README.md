# Pipeline as a Service (Plaas)
A Jenkins Pipeline service that can deploy applications to AWS Cloud environment based on yaml file configurations

## Background
The current industry trend favors micro applications at all layers - front end, back end and anything in between, which naturally multiplies the number of artifacts being deployed and the number of lifecycle environments in enterprise project further contributing to the volume. With Jenkins, the most popular CI/CD tool in integration with github, Pipeline is a preferred choice to port code through different stages before deploying to a target environment.

Some projects prefer to build a separate pipeline for each app, which may not be the best choice in all circumstance. This implementation provides a single pipeline service that could potentially deploy any number of apps.

## How
This is really not any groundbreaking idea but rather one out of simple common sense, most of the companies may be practicing a similar technique in some fashion or other. Hate to repeat the most obvious but here is a common pipeline principle outlined below.

A pipeline simply transports the code through different stages on successful execution (failure case is not shown here) until deploying it in a target environment. The variant between different pipelines is of course the code in flight and several other parameters. Plass service makes generalization possible by identifying those variant parameters, externalizing them and feeding it to a stage as and when required. That's it. As I said, it is not really a big deal.


## Why
Why should one do this? 
* The first and foremost motivation is that it helps with drawing a clear line of responsibility between DevOps team and Application Developers. A set of parameters is provided by both DevOps and App team. DevOps maintains Plaas and provides System level parameters or any parameters thery don't developers to control. App Developers provide app specific parameters.
* There is zero repetition of code - you code once and apply it everywhere. Think of maintenance
* You get clarity on what is going on and what are the parameters needed to run the pipeline






