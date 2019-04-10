# Using Container for Deployment of Application

[![Build Status](https://travis-ci.org/marcdomain/deploy-nodejs-app-with-docker.svg?branch=master)](https://travis-ci.org/marcdomain/deploy-nodejs-app-with-docker)

## Getting Started

### Dockerfile

- Using a working react application, create `Dockerfile`, in the root directory, for building a container image of the application.
- Use a node alpine base-image to build the container. This provides only essential dependencies required for a basic node application to work.
- The Dockerfile consist of nine steps and which are placed to ensure efficient build process.
- The first `COPY` command is meant to copy the package.json file and install the app dependencies using the `npm install` command. However, if the application is built subsequently without a change in the package.json file, the installation step would be skipped. This helps to reduce the build time.
- The second `COPY` command is meant to copy the application files on the local machine into the working directory of the container.

### Amazon Elastic Beanstalk

- Creata an Amazon **[IAM](https://console.aws.amazon.com/iam/home?region=us-west-1#/users)** user account, and assign `AWSElasticBeanstalkFullAccess` permission to the user.
- Ensure the region in your URL is your preferred region. Add the name of the user, and select programatic access type. Click `Next: Permissions`.
- Select the `Attach existing policies directly` option.
- Search and select `AWSElasticBeanstalkFullAccess` in the check box. Click `Next: Tags`.
- Add tags. This is optional.
- Review details and click on `Create user`.
- Take note of the user `Access key ID` and `Secret access key`. They will be used for user credentials in travisCI.
- Click on `Services` on the menu bar and access **[Elastic Beanstalk](https://console.aws.amazon.com/elasticbeanstalk)**. Change the region in the URL to your preferred region.
- Follow the guide **[here](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/applications.html)** to create the Elastic Beanstalk.

### travis.yml file

- Create a travis.yml file using the script contained **[here](https://github.com/marcdomain/deploy-nodejs-app-with-docker/blob/master/.travis.yml)**
- In the script section, tag the docker image to your docker username and your project name (preferrably).
- Create the following environment variables `AWS_REGION`, `BUCKET_NAME`, `AWS_ACCESS_KEY_ID`, `AWS_SECRET_KEY` in your travis account assocaited to the github repository.
- Commit your changes in the master branch and push to your github repository
