# Udagram App On AWS

Udagram is a simple cloud application developed alongside the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice. 

It can be run locally and also on a Kubernetes cluster, on AWS.

The app consists of two back-end Nodejs services - /udacity-c3-restapi-feed and /udacity-c3-restapi-user
and a front end ionic service - udacity-c3-frontend

## Running locally

You will need to have:

1. docker https://docs.docker.com/install/ , Nodejs https://nodejs.org/en/ and ionic https://ionicframework.com/docs/installation/cli installed.

2. an AWS account https://aws.amazon.com/ and a PostgreSQL RDS instance set up to save user sign on information. You will also need an S3 bucket set up on AWS to store the image files.

3. the following local environment variables set:

  $POSTGRESS_USERNAME
  $POSTGRESS_PASSWORD 
  $POSTGRESS_DB 
  $POSTGRESS_HOST 
  $AWS_REGION 
  $AWS_PROFILE 
  $AWS_BUCKET
  $JWT_SECRET

From the main directory `cd udacity-c3-deployment/docker`

To run the docker compose file `docker-compose up`

This will start the backend-feed and backed-user services, as well as a reverese proxy, along with the font-end.

You should now be able to go to `http://localhost:8100/home` in your browser and see the application running.

To remove the docker containers `docker-compose down`

## Updating the docker images

If changes are made to source files, the docker images in the docker hub repository can be updated.

From the `/udacity-c3-deployment/docker` directory run `docker-compose -f docker-compose-build.yaml push`

You will need to update the `image:` in the `docker-compose-build.yaml` with your own repository names, where you have push access.

You can then update the images being pulled in the `docker-compose.yaml` with your own repositories.

## Running in Kubernetes on AWS

You will need to have Terraform https://www.terraform.io/downloads.html and KubeOne https://github.com/kubermatic/kubeone/blob/master/README.md installed

You will need to set the following local environment variables:

  $AWS_ACCESS_KEY_ID
  $AWS_SECRET_ACCESS_KEY

You will need to add the following files to the `udacity-cd-deployment/k8s` directory:

aws-secret.yaml
env-config.yaml
env-secret.yaml

templates for these files can be found in this repository:

https://github.com/scheeles/cloud-developer/tree/06-ci/course-03/exercises/udacity-c3-deployment/k8s

The following guide contains detailed steps on how to use Terraform to set up your AWS EC2 instances with three control planes and a Kubernetes cluster.

https://github.com/kubermatic/kubeone/blob/master/docs/quickstart-aws.md

## Using Travis CI tool

The app is set up with Travis CI https://travis-ci.org/ on this GitHub repository.

With the app running on a Kubernetes cluster on AWS, changes pushed to this repository will run a Travis build, creating a new build and pushing it to production.










