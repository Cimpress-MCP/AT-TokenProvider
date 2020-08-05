# ATSquad Token Provider

A simple library to resolve JWT tokens.

It uses AWS KMS to decrypt the client secret and then calls the specified token endpoint the retrieve JWT. 

## Using this library

Install the library.

```bash
yarn add @atsquad/token-provider
```

### Token Provider

```javascript
const axios = require('axios');
const TokenProvider = require('@atsquad/token-provider');

const configuration = {
  clientId: 'CLIENT_ID',
  encryptedClientSecret: 'BASE64_KMS_ENCRYPTED_CLIENT_SECRET',
  audience: 'https://example.com/',
  tokenEndpoint: 'https://example.com/oauth/token'
};

let kmsClient = new aws.KMS({ region: 'eu-west-1' });
let tokenProvider = new TokenProvider({
  httpClient: axios.create(),
  kmsClient: kmsClient,
  tokenConfiguration: configuration
});

// recommended way to retrieve token (utilizes caching and takes care of token expiration)
let accessToken = await tokenProvider.getToken();

// or bypass caching and get new token
accessToken = await tokenProvider.getTokenWithoutCache();
```

## Contribution

We value your input as part of direct feedback to us, by filing issues, or preferably by directly contributing improvements:

1. Fork this repository
1. Create a branch
1. Contribute
1. Pull request
