Dynamic environment management using [Dotenv](https://www.npmjs.com/package/dotenv)

You can use this plugin if you are storing your environment variables using dontenv module. This will allow you to reference env variables `${env:VAR_NAME}` inside your serverless.yaml and it will load them into your lambdas.

### Install and Setup

First, install the plugin:
```
> npm i -D serverless-dynamic-dotenv
```

Next, add the plugin to your serverless config file:
```
service: myService
plugins:
  - serverless-dotenv-plugin
...
```

Now, just like you would using [dotenv](https://www.npmjs.com/package/dotenv) in any other JS application, create your file with stage name `.env.stage_name` in the root of your app:

```
DB=mongodb://username:password@host:27017
AWS_REGION=us-west-1
SOME_VAR=some_value
```

### Plugin options

Dotenv config file names are dynamic.
Files should be located in the root of the project (beside serverless.yaml)
File names are based `stage` option: `.env.stage`
If you run your serverless command with `--stage dev` option then plugin maps vars from `.env.stage_name`. So that, you can create one .env file per stage.

### Usage

Once loaded, you can now access the vars using the standard method for accessing ENV vars in serverless:
```
...
provider:
  name: aws
  runtime: nodejs6.10
  stage: dev
  region: ${env:AWS_REGION}
...
```

### Lambda Environment Variables

Again, remember that when you deploy your service, the plugin with inject these environment vars into any lambda functions you have and will therefore allow you to reference them as `process.env.AUTH0_CLIENT_ID` (Nodejs example).

