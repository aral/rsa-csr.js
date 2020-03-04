# Fork of RSA-CSR.js that removes telemetry (yes, it had telemetry *smh*)

Original repository: <https://git.coolaj86.com/coolaj86/rsa-csr.js>

Zero-dependency to generate Certificate Signing Requests (CSR) and sign them.

## Usage

Given an array of domains it uses the first for the  Common Name (CN),
also known as Subject, and all of them as the Subject Alternative Names (SANs or altnames).

```js
'use strict';

var rsacsr = require('rsa-csr');
var key = {
  "kty": "RSA",
  "n": "m2tt...-CNw",
  "e": "AQAB",
  "d": "Cpfo...HMQQ",
  "p": "ynG-...sTCE",
  "q": "xIkA...1Q1c",
  "dp": "tzDG...B1QE",
  "dq": "kh5d...aL48",
  "qi": "AlHW...HhFU"
};
var domains = [ 'example.com', 'www.example.com' ];

return rsacsr({ key: key, domains: domains }).then(function (csr) {
  console.log('CSR PEM:');
  console.log(csr);
});
```

The output will look something like this (but much longer):

```
-----BEGIN CERTIFICATE REQUEST-----
MIIClTCCAX0CAQAwFjEUMBIGA1UEAwwLZXhhbXBsZS5jb20wggEiMA0GCSqGSIb3
DQEBAQUAA4IBDwAwggEKAoIBAQCba21UHE+VbDTpmYYFZUOV+OQ8AngOCdjROsPC
0KiEfMvEaEM3NQl58u6QL7G7QsEr.....3pIpUUkx5WbwJY6xDrCyFKG8ktpnee6
WjpTOBnpgHUI1/5ydnf0v29L9N+ALIJGKQxhub3iqB6EhCl93iiQtf4e7M/lzX7l
c1xqsSwVZ3RQVY9bRP9NdGuW4hVvscy5ypqRtXPXQpxMnYwfi9qW5Uo=
-----END CERTIFICATE REQUEST-----
```

### Options

- `key` should be a JWK
- `domains` must be a list of strings representing domain names
  - correctly handles utf-8
  - you may also use punycoded, if needed
- `subject` will be `domains[0]` by default
  - you shouldn't use this unless you need to
  - you may need to if you need utf-8 for domains, but punycode for the subject

## License

[RSA-CSR.js](https://git.coolaj86.com/coolaj86/rsa-csr.js) is licensed under MPL-2.0
