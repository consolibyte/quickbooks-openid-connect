Intuit/QuickBooks OpenID Connect client
=======================================

This is a fork of <https://github.com/jumbojett/OpenID-Connect-PHP> which needed
some tweaks to work with Intuit/QuickBooks.

Thanks Michael Jett @jumbojett !

# Requirements
 1. PHP 5.4 or greater
 2. CURL extension
 3. JSON extension

## Install
 1. Install library using composer
```
composer require consolibyte/quickbooks-openid-connect
```
 2. Include composer autoloader
```
<?php
require __DIR__ . '/vendor/autoload.php';
```

## Example 1: Basic Client

```
<?php
use Jumbojett\OpenIDConnectClient;

$openid = new OpenIDConnectClient('https://developer.api.intuit.com',
                                'ClientIDHere',
                                'ClientSecretHere');

$openid->addScope(array('openid', 'profile', 'email'));
```

### For SANDBOX/dev

```
$openid->setRedirectURL('Your redirect URL');
$openid->providerConfigParam(array('userinfo_endpoint' => 'https://sandbox-accounts.platform.intuit.com/v1/openid_connect/userinfo'));
```

### For PROD

```
$openid->setRedirectURL('Your redirect URL');
```

### Then you can authenticate

```
$oidc->authenticate();
$name = $oidc->requestUserInfo('given_name');
```

## Example 4: Request Client Credentials Token

```
<?php
use Jumbojett\OpenIDConnectClient;

$oidc = new OpenIDConnectClient('https://id.provider.com',
                                'ClientIDHere',
                                'ClientSecretHere');
$oidc->providerConfigParam(array('token_endpoint'=>'https://id.provider.com/connect/token'));
$oidc->addScope('my_scope');

// this assumes success (to validate check if the access_token property is there and a valid JWT) :
$clientCredentialsToken = $oidc->requestClientCredentialsToken()->access_token;
```

## Development Environments

In some cases you may need to disable SSL security on on your development systems.
Note: This is not recommended on production systems.

```
<?php
$oidc->setVerifyHost(false);
$oidc->setVerifyPeer(false);
```
