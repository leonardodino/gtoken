# node-gtoken

[![NPM Version][npm-image]][npm-url]
[![Build Status][travis-image]][travis-url]
[![Dependency Status][david-image]][david-url]
[![devDependency Status][david-dev-image]][david-dev-url]
[![Known Vulnerabilities][snyk-image]][snyk-url]
[![codecov][codecov-image]][codecov-url]
[![style badge][gts-image]][gts-url]

Node.js Google Authentication Service Account Tokens

## Installation

```shell
npm install @leonardodino/gtoken
```

or

```shell
yarn add @leonardodino/gtoken
```

## Usage

```javascript
const key = '-----BEGIN RSA PRIVATE KEY-----\nXXXXXXXXXXX...';
const { GoogleToken } = require('@leonardodino/gtoken');
const gtoken = new GoogleToken({
  email: 'my_service_account_email@developer.gserviceaccount.com',
  scope: ['https://scope1', 'https://scope2'], // or space-delimited string of scopes
  key: key
});
```

## Options

> Various options that can be set when creating initializing the `gtoken` object.

- `options.email or options.iss`: The service account email address.
- `options.scope`: An array of scope strings or space-delimited string of scopes.
- `options.sub`: The email address of the user requesting delegated access.
- `options.key`: The raw RSA private key value.

### .getToken()

> Returns the cached token or requests a new one and returns it.

```javascript
gtoken.getToken(function(err, token) {
  if (err) {
    console.log(err);
    return;
  }
  console.log(token);
});
```
 
You can also use the async/await style API:
 
``` js
const token = await gtoken.getToken()
console.log(token);
```
 
Or use promises:
or

```js
gtoken.getToken()
  .then(token => {
    console.log(token)
  })
  .catch(e => console.error);
```

### Properties

> Various properties set on the gtoken object after call to `.getToken()`.

- `gtoken.token`: The access token.
- `gtoken.expiresAt`: The expiry date as milliseconds since 1970/01/01
- `gtoken.key`: The raw key value.
- `gtoken.rawToken`: Most recent raw token data received from Google.

### .hasExpired()

> Returns true if the token has expired, or token does not exist.

```javascript
gtoken.getToken(function(err, token) {
  if(token) {
    gtoken.hasExpired(); // false
  }
});
```

### .revokeToken()

> Revoke the token if set.

```javascript
gtoken.revokeToken(function(err) {
  if (err) {
    console.log(err);
    return;
  }
  console.log('Token revoked!');
});
```

## Changelog

### 2.0.0 -> 3.0.0
New features:
- Fewer dependencies, code works everywhere.

Breaking changes:
- remove support for reading files (`keyFile` option)
- remove `getCredentials` method.
- remove `ensureEmail` private method.

### 1.2.2 -> 2.0.0
New features:
- API now supports callback and promise based workflows

Breaking changes:
- `GoogleToken` is now a class type, and must be instantiated.
- `GoogleToken.expires_at` renamed to `GoogleToken.expiresAt`
- `GoogleToken.raw_token` renamed to `GoogleToken.rawToken`
- `GoogleToken.token_expires` renamed to `GoogleToken.tokenExpires`

## License

[MIT](LICENSE)

[travis-image]: https://travis-ci.org/leonardodino/gtoken.svg?branch=master
[travis-url]: https://travis-ci.org/leonardodino/gtoken
[codecov-image]: https://codecov.io/gh/leonardodino/gtoken/branch/master/graph/badge.svg
[codecov-url]: https://codecov.io/gh/leonardodino/gtoken
[david-image]: https://david-dm.org/leonardodino/gtoken.svg
[david-url]: https://david-dm.org/leonardodino/gtoken
[david-dev-image]: https://david-dm.org/leonardodino/gtoken/dev-status.svg
[david-dev-url]: https://david-dm.org/leonardodino/gtoken?type=dev
[gts-image]: https://img.shields.io/badge/code%20style-Google-blue.svg
[gts-url]: https://www.npmjs.com/package/gts
[npm-image]: https://img.shields.io/npm/v/@leonardodino/gtoken.svg
[npm-url]: https://npmjs.org/package/@leonardodino/gtoken
[snyk-image]: https://snyk.io/test/github/leonardodino/gtoken/badge.svg
[snyk-url]: https://snyk.io/test/github/leonardodino/gtoken
