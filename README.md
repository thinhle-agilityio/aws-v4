# aws-v4

A small utility to generate [AWS Signature V4](https://docs.aws.amazon.com/general/latest/gr/signing_aws_api_requests.html) using vanilla nodejs.

Use case is especially for AWS API GATEWAY (excute-api) service.

## Installation

```
npm install aws-v4
```

## Example

Below example is using `post` request, you can also use other request such as: `get`, `put`, `delete`

```javascript
const axios  = require('axios');
const awsV4 = require('aws-v4');

// Sign your request
// This example is post request, you can 
const signedRequest = awsV4.newClient({
    accessKey: <AWS_ACCESS_KEY_ID>,
    secretKey: <AWS_SECRET_KEY>,
    region: <AWS_REGION>,
    endpoint: <AWS_API_GATEWAY_ENDPOINT>
  }).signRequest({
    method: 'post',
    path: '/example/path',
    headers: {
      'Content-Type': 'application/json'
    },
    queryParams: {},
    body: {}
  });

// Make http request with your signed request
const options = {
  url: signedRequest.url,
  method: 'post',
  headers: signedRequest.headers,
  data: {}
}

axios(options)
  .then(res => console.log(res))
  .catch(err => console.log(err))
```
