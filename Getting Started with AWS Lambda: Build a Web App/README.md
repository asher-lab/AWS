**# Title: Getting Started with AWS Lambda: Build a Web App**

**Weblink:** [https://github.com/aws-samples/aws-serverless-workshop-innovator-island](https://github.com/aws-samples/aws-serverless-workshop-innovator-island)

[https://www.eventbox.dev/published/lesson/innovator-island/0-setup/3-aws-cloud9-ide.html](https://www.eventbox.dev/published/lesson/innovator-island/0-setup/3-aws-cloud9-ide.html)

Verify that your user is the one running the environement:

aws sts get-caller-identity

You will be given a return like this:

{

&quot;Account&quot;: &quot;478482699325&quot;,

&quot;UserId&quot;: &quot;478482699325&quot;,

&quot;Arn&quot;: &quot;arn:aws:iam::478482699325:root&quot;

}

A bash command if you are running in the correct region:

-

AWS\_REGION=$(curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone | sed &#39;s/\(.\*\)[a-z]/\1/&#39;)

-

SUPPORTED\_REGIONS=(&quot;us-west-2&quot; &quot;us-east-1&quot; &quot;us-east-2&quot; &quot;eu-central-1&quot; &quot;eu-west-1&quot; &quot;ap-southeast-2&quot; )

-

if [[! &quot; ${SUPPORTED\_REGIONS[@]} &quot; =~ &quot; ${AWS\_REGION} &quot; ]]; then

/bin/echo -e &quot;\e[1;31m&#39;$AWS\_REGION&#39; is not a supported AWS Region, delete this Cloud9 instance and restart the workshop in a supported AWS Region.\e[0m&quot;

else

/bin/echo -e &quot;\e[1;32m&#39;$AWS\_REGION&#39; is a supported AWS Region\e[0m&quot;

fi

You will be given a return like this:

&#39;us-east-1&#39; is a supported AWS Region

**Cloning a github repo**

cd ~/environment/

git clone https://github.com/aws-samples/aws-serverless-workshop-innovator-island ./theme-park-backend

Install cmd json processor:

sudo yum install jq -y

# Overview

The theme park application consists of a frontend and backend - in this module, you will set up the frontend and then connect it to the backend.

The frontend is a [Progressive Web App](https://en.wikipedia.org/wiki/Progressive_web_applications) (PWA) developed in [Vue.js](https://vuejs.org/).

The frontend code is provided so you will only need to download the code and deploy into your own Git-based code repository stored in CodeCommit. Using [AWS Amplify Console](https://aws.amazon.com/amplify/console/), you will create a continuous deployment pipeline to publish your frontend application.

The backend is a set of serverless microservices. In this section we will set up the following:

- A DynamoDB table containing information about all the rides and attractions throughout the park.
- A Lambda function which performs a table scan on the DynamoDB to return all the items.
- An API Gateway API which creates a public http endpoint for the front-end application to query. This invokes the Lambda function to return a list of rides and attractions.

Once you have built the back-end resources needed, you will update the front-end application configuration to query the API Gateway endpoint and display the information about all the rides and attractions.

Each of the following sections provides an implementation overview and detailed, Step-by-step instructions. Remember: if you have any questions, contact one of the AWS employees located around the room.
