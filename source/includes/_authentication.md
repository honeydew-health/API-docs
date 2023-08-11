# Authentication

## OAuth 2.0 Token Bearer

Engage supports bearer token authentication with a client credentials grant type.
Within Engage you can generate API Client Applications, each of which has a unique id and secret. Your app should authenticate with this id and secret to obtain a JWT token. That token can be passed as a bearer token to authorise subsequent API requests.
The token has a lifetime of up to 2 hours, once expired you will need to authenticate again to obtain a new token.

<aside class="notice">
  The token returned by our Bearer Token authentication is a valid JWT (JSON Web Token). You can therefore decode and verify the token and its signature - for manual testing check <a href="https://www.jwt.io">www.jwt.io</a>.
</aside>

## Authorising your requests

After [authenticating and obtaining a token](#obtain-a-token) provide this token with all requests as the following header parameter.

```
curl /example -H "Authorization: Bearer abc"
```

### Header Parameters

Parameter | Type | Description
--------- | ------- | -----------
Authorization | string | <span class="label label-info">required</span> Bearer abc

## Obtain a token

### HTTP Request
`POST /auth/token`

Authenticate with the API and obtain a JWT token

```
curl -X POST /auth/token -H "Content-Type: application/json" -d '{
    "grant_type": "client_credentials", 
    "client_id": "123", 
    "client_secret": "abc"
  }' 
```

> Example JSON Response:

```
{
     "access_token": "abc",
     "token_type": "Bearer",
     "expires_in": 7200,
     "created_at": 1691747914
}
```

### Parameters

Parameter | Type | Description
--------- | ------- | -----------
grant_type | string | <span class="label label-info">required</span> The type of grant requested
client_id | integer | <span class="label label-info">required</span> Your API Client Application ID
client_secret | integer | <span class="label label-info">required</span> Your API Client Application Secret

<aside class="notice notice-info">
  Each token granted will expire in 2 hours.
</aside>

## Verify a token

### HTTP Request
`POST /auth/token/info`

```
curl -X POST /auth/token/info -H "Content-Type: application/json" -H "Authorization: [omitted]"
```

> Example JSON Response:

```
{
    "resource_owner_id": null,
    "scope": [],
    "expires_in": 6540,
    "application": {
        "uid": “abc”
    },
    "created_at": 1653667738
}
```

### Header Parameters

Parameter | Type | Description
--------- | ------- | -----------
Authorization | string | <span class="label label-info">required</span> Your authorization token

## Revoke a token

### HTTP Request
`POST /auth/revoke`

```
curl -X POST /auth/revoke -H "Content-Type: application/json" -H "Authorization: Basic abc" -d '{
  "token": "abc"
  }'
```

### Header Parameters

Parameter | Type | Description
--------- | ------- | -----------
Authorization | string | <span class="label label-info">required</span> Basic HTTP Authentication with your Base64 encoded "client_id:client_secret"

### Parameters

Parameter | Type | Description
--------- | ------- | -----------
token | string | <span class="label label-info">required</span> Your token


## API Keys

<span class="label label-info">Deprecated</span>

<aside class="warning">
  This authentication method may be deprecated at a future date and is not recommended for future implementations.
</aside>

This is a simple API Key that should be provided along with any requests to the API via QueryString in the format /?api_key={your api key}.

As all API requests are made over SSL this value is always encrypted.
You can view or generate a new API Key on your Engage account under Administration > Preferences > Data API.

## IP Whitelisting

<span class="label label-info">Deprecated</span>

<aside class="warning">
  This authentication method may be deprecated at a future date and is not recommended for future implementations.
</aside>

<aside class="notice">
  This option only works in conjunction with API Key authentication and is ignored when using Bearer token authentication.
</aside>

All requests will be validated against a defined list of IP addresses, you can configure these addresses on your Engage account under Administration > Preferences > Data API.
