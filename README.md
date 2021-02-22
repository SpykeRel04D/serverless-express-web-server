# Serverless Express Web Server & API

In this project we are gonna have running a web server complete with routing using [AWS Lambda](https://aws.amazon.com/lambda/), [Amazon API Gateway](https://aws.amazon.com/api-gateway/) and [AWS Amplify](https://aws.amazon.com/es/amplify/).

---

## 1) Configuration steps before start working

In order to manage our AWS services, we are gonna use **Amplify CLI**.

In case that you have not already installed it, you can do it following the next commands:

```bash
$ npm install -g @aws-amplify/cli
$ amplify configure
```

Once you have installed it, initialize a new Amplify project in the root of your project:

```bash
$ amplify init
# Answer the CLI questions (You can let almost all of them by default)
```

---

## 2) Adding the API

At this point, we are ready to create the API and web server. To do this, we can use Amplify `add` command:

```
$ amplify add api

? Please select from one of the below mentioned services: REST
? Provide a friendly name for your resource to be used as a label for this category in the project: serverlessapi
? Provide a path (e.g., /book/{isbn}): /items
? Choose a Lambda source: Create a new Lambda function
? Provide an AWS Lambda function name: serverlesslambda
? Choose the runtime that you want to use: NodeJS
? Choose the function template that you want to use: Serverless ExpressJS function (Integration with API Gateway)
? Do you want to configure advanced settings? N
? Do you want to edit the local lambda function now? N
? Restrict API access? N
? Do you want to add another path? N
```

After this, we have:

-   API endpoint
-   Lambda function
-   Web server using Serverless Express in the function
-   Some boilerplate code for different methods on the `/items` route
