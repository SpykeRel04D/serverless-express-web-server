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

---

## 3) Preparing our API to test

We can find our main function handler with the `event` and `context` being proxied to an express server located at `./app.js` in the next path: **amplify/backend/function/serverlesslambda/src/index.js**.

```js
const awsServerlessExpress = require("aws-serverless-express");
const app = require("./app");

const server = awsServerlessExpress.createServer(app);

exports.handler = (event, context) => {
	console.log(`EVENT: ${JSON.stringify(event)}`);
	return awsServerlessExpress.proxy(server, event, context, "PROMISE").promise;
};
```

We can find our express sorver with some boilerplate code on: **amplify/backend/function/serverlesslambda/src/app.js**.

Here, try to find the route for `app.get('/items')` and update it:

```js
app.get("/items", function (req, res) {
	const items = ["This", "is", "the", "method", "route", "for", "/items"];
	res.json({ success: "get call succeed!", url: req.url });
});
```

Before deploying it, we can test if locally.
To do this, we have to install some dependencies corresponding that are already listed in the **package.json** inside `amplify/backend/function/serverlesslambda/src/`.
We can direcly run `npm install` inside this route, or do this by following this command line:

```bash
$ cd amplify/backend/function/serverlesslambda/src && npm install && cd ../../../../../
```

---

## 4) Test our API Locally

As we have said, we can test our API Locally before deploy it.

First, we are gonna define our call execution. To do this, we have to edit `event.json` inside `amplify/backend/function/serverlesslambda/src/`.

```js
{
	"httpMethod": "GET",
	"path": "/items"
}
```

Then, to invoke the function and start thhe server, run the following command:

```bash
$ amplify mock function serverlesslambda
? Provide the pathh to the event JSON object relative to ...: src/event.json
```

If all works fine, we are gonna see a call execution with our `items` array.

[Test the API from terminal Documentation](https://docs.amplify.aws/cli/restapi/testing)

---

## 5) Deploying our API

To deploy the API and function, we can run the `push` command:

```bash
$ amplify push
```

Now, you can interact with your API, for example like:

```js
// Pulling: GET
const items = await API.get("api_url", "/items");

// Pushing: POST
const data = { body: { items: ["some", "new", "items"] } };
await API.post("api_url", "/items", data);
```

In the future, if you want to add additional path, run the following command:

```bash
$ amplify update api
```
