# serverless-dynamodb-rest-poc
This example provides a starter for using [Serverless](https://serverless.com) 
and [DynamoDB](https://aws.amazon.com/dynamodb/) to create a REST API. It utilizes [serverless-offline](https://github.com/dherault/serverless-offline)
and [serverless-dynamodb-local](https://github.com/99xt/serverless-dynamodb-local) to provide
a development environment on your local machine.

This project demos a REST API to manage Todos stored in a DynamoDB, modified from [aws-node-rest-api-with-dynamodb-and-offline](https://github.com/serverless/examples/tree/master/aws-node-rest-api-with-dynamodb-and-offline).

Understand that that managing multiple "controllers" in one service could get complicated and 
might not be the recommended solution for your use case. A larger project with multiple smaller 
services, one for each "controller", might be a more reasonable solution for you.

## Project Structure
```text
.
+-- package.json                        # Node package.json
+-- serverless.yml                      # Serverless configuration file
+-- README.md                           # This file
+-- _ handlers                          # Function handler directory
|   +-- _ todos                         #   A group of related functions handlers dir
|       +-- create.js                   #       A functions handler
|       v etc                           # (Fill more as you build out)
+-- _ resources                         # Resources directory 
|   +-- dynamodb-tables.yml             # DynamoDB table resources for serverless.yml
|   +-- iam-role-stmt-resources.yml     # IAM role statement resources for serverless.yml
|   +-- root-functions.yml              # Functions for serverless.yml
|   +-- _ dev_certs                     # Development cert directory (Used for https)
|   +-- _ functions                     #   Functions directory 
|       +-- todos.yml                   #       A function group declaration
|       v etc                           # (Fill more as you build out)
+-- _ offline                           # Serverless Offline directory 
|   +-- _ migrations                    #   Migrations directory 
|       +-- todos.json                  #       Migration file
|       v etc                           # (Fill more as you build out)
```

## Build
### Local
`npm run dev-install` to install   
`npm run dev-start` to start api  
`npm run auto-start` to do both  
or
```bash
npm install
serverless dynamodb install
serverless offline start --migrate
```
## Deploy
`npm run deploy`  
or
```bash
serverless deploy --stage prod
```
## Usage

You can create, retrieve, update, or delete todos with the following commands:

### Create a Todo

```bash
curl -X POST -H "Content-Type:application/json" http://localhost:3000/v1/todos --data '{ "text": "Learn Serverless" }'
```

Example Result:
```bash
{"text":"Learn Serverless","id":"ee6490d0-aa81-11e6-9ede-afdfa051af86","createdAt":1479138570824,"checked":false,"updatedAt":1479138570824}%
```

### List all Todos

```bash
curl -H "Content-Type:application/json" http://localhost:3000/v1/todos
```

Example output:
```bash
[{"text":"Deploy my first service","id":"ac90fe80-aa83-11e6-9ede-afdfa051af86","checked":true,"updatedAt":1479139961304},{"text":"Learn Serverless","id":"20679390-aa85-11e6-9ede-afdfa051af86","createdAt":1479139943241,"checked":false,"updatedAt":1479139943241}]%
```

### Get one Todo

```bash
# Replace the <id> part with a real id from your todos table
curl -H "Content-Type:application/json" http://localhost:3000/v1/todos/<id>
```

Example Result:
```bash
{"text":"Learn Serverless","id":"ee6490d0-aa81-11e6-9ede-afdfa051af86","createdAt":1479138570824,"checked":false,"updatedAt":1479138570824}%
```

### Update a Todo

```bash
# Replace the <id> part with a real id from your todos table
curl -X PUT -H "Content-Type:application/json" http://localhost:3000/v1/todos/<id> --data '{ "text": "Learn Serverless", "checked": true }'
```

Example Result:
```bash
{"text":"Learn Serverless","id":"ee6490d0-aa81-11e6-9ede-afdfa051af86","createdAt":1479138570824,"checked":true,"updatedAt":1479138570824}%
```

### Delete a Todo

```bash
# Replace the <id> part with a real id from your todos table
curl -X DELETE -H "Content-Type:application/json" http://localhost:3000/v1/todos/<id>
```

No output

## License 
This project uses the GNU GPL v3 license that is available [here](./LICENSE.txt) 👀