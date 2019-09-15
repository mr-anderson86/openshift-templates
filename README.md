# openshift-templates

## Description:

This repo contains a simple deployment file to use in OpenShift.

### Main deployments:
* Secret (credentails) for image pulling from the docker registry
* Image Stream, which pulls the image from the remote registry to the local in your namespace
* Deployment Config with:
  * the actual pods
  * readiness and liveness probes
  * Rolling strategy, which will allow you to roll back or forward to spesific deployment version, if current deployment is bad or bugged.
* Service, so that the pods will be accessible from other services/pods within your namespace.
* Route, so that the service (and pods) will be accessible from anywhere (including your own computer).

### Usage:
First, you need to login ;-)
```bash
oc login <OS address> <your credentials or token>
```

The command below will show you the json output, after processing the parameters.  
The below will give the output with default values:
```bash
oc process -f simple-deployment-template.yaml
```
The below will give the output with given values, for example:
```bash
oc process -f simple-deployment-template.yaml -p SERVICE_NAME=my-servicename -p IMAGE_TAG=some-image-tag
```
The command below will perform the actual deployment:
```bash
oc process -f simple-deployment-template.yaml [-p PARAM=value] | oc apply -f -
```
