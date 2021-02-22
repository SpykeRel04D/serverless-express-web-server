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
