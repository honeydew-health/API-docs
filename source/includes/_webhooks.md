# Webhooks

Allow your system to receive live events from Engage.

Absence events can occur at any time of the day or night and on any day of the week. Knowing when to fetch a new data set is not always easy and fetching large sets of data means more data processing at the receiving end. Using webhooks, Engage can tell you when something happens, optimising the data flows.

The specific actions your webhook endpoint may take differs based upon the event. Some examples include:

- Creating a new absence record
- Updating the absence dates and reasons Logging a confirmed return date
- Deleting a previously recorded return date Removing an absence record

## Configuring Webhooks

You can manage webhooks on your Engage account under Administration > Data API > Webhooks.

New webhook endpoints will be authorised through our Firewall by support.

If using bearer token authentication please provide the following to support for configuration: 

- Full Authentication API documentation with credentials, including:
    - Authentication url
        - Expected HTTP headers / HTTP body
        - User id / secret
        - Example HTTP response
    - Token refresh url (optional)
        - Expected HTTP headers / HTTP body
        - User id / secret
        - Example HTTP response

## Webhook Authentication

### HMAC Signature

Webhooks carry a HMAC signature which can be used to verify the authenticity of the request. This will be provided as the HTTP header:

`X-Engage-API-Signature: t=epoch,v1=hmac`

To verify the signature, you should split this value to obtain the epoch timestamp and the hmac separately. In future, there may be multiple versions of the HMAC so be sure to programatically select the correct HMAC version.

The v1 HMAC uses the SHA256 hash algorithm with your api key as the secret. The content is comprised of the epoch timestamp and the HTTP body payload separated by a period.

Here’s an example of creating the hash in Ruby:

`OpenSSL::HMAC.hexdigest('SHA256', api_key, "#{timestamp}.#{body}")`

If you construct your own hash with the same timestamp and the received body this should match the received signature, allowing you to verify the integrity of the HTTP body and the time validity of the request. If either the header epoch value doesn’t match the hash epoch value, or the body doesn’t match the hash body then the signatures will not match.

### OAuth 2.0 Bearer Token

Webhooks can be configured to authenticate against OAuth 2.0 bearer token authentication to retrieve a token from your servers, which will then be included in webhook request headers.

Please provide support with your Authentication API documentation and test/production credentials for verification of compatibility and setup.

## New Absence

`HTTP POST {your_url}`

### Headers

Name | Type | Description
--------- | ------- | -----------
Content-Type | string | application/json
X-Engage-API-Version | string | v1
X-Engage-API-Webhook-Event | string | Absence.Created
X-Engage-API-Signature | string | epoch=x,v1=y [See HMAC Signature](#hmac-signature)
Authorization | string | Bearer abc (if applicable, [See OAuth 2.0 Bearer Token](#oauth-2-0-bearer-token))

> Example JSON body:

```
  "event": {
    "name": "Absence.Created",
    "object_type": "Absence",
    "object_id": 123,
    "object": {
      "absence_id": 123,
      "employee_id": "456",
      "start_date": "2022-06-15",
      "end_date": null,
      "expected_end_date": "2022-06-17",
      "confirmed_return_date": null,
      "half_day_start": 1,
      "half_day_end": 0,
      "absence_cause": null,
      "absence_cause_category": null,
      "medical_appointment_arranged": null,
      "medical_appointment_date": null,
      "created_at": "2022-06-15T08:21:56.000+00:00",
      "updated_at": "2022-06-15T09:35:25.000+00:00"
    } 
  }
```

<aside class="notice notice-info">
  <code>absence_cause</code> and <code>absence_cause_category</code> only returned if privacy settings allow. See Administration > Preferences > Data API on your Engage Account.
</aside>

## Updated Absence

`HTTP POST {your_url}`

### Headers

Name | Type | Description
--------- | ------- | -----------
Content-Type | string | application/json
X-Engage-API-Version | string | v1
X-Engage-API-Webhook-Event | string | Absence.Updated
X-Engage-API-Signature | string | epoch=x,v1=y [See HMAC Signature](#hmac-signature)
Authorization | string | Bearer abc (if applicable, [See OAuth 2.0 Bearer Token](#oauth-2-0-bearer-token))

> Example JSON body:

```
  "event": {
    "name": "Absence.Updated",
    "object_type": "Absence",
    "object_id": 123,
    "object": {
      "absence_id": 123,
      "employee_id": "456",
      "start_date": "2022-06-15",
      "end_date": null,
      "expected_end_date": "2022-06-17",
      "confirmed_return_date": null,
      "half_day_start": 1,
      "half_day_end": 0,
      "absence_cause": null,
      "absence_cause_category": null,
      "medical_appointment_arranged": null,
      "medical_appointment_date": null,
      "created_at": "2022-06-15T08:21:56.000+00:00",
      "updated_at": "2022-06-15T09:35:25.000+00:00"
    } 
  }
```

<aside class="notice notice-info">
  <code>absence_cause</code> and <code>absence_cause_category</code> only returned if privacy settings allow. See Administration > Preferences > Data API on your Engage Account.
</aside>

## Deleted Absence

`HTTP POST {your_url}`

### Headers

Name | Type | Description
--------- | ------- | -----------
Content-Type | string | application/json
X-Engage-API-Version | string | v1
X-Engage-API-Webhook-Event | string | Absence.Deleted
X-Engage-API-Signature | string | epoch=x,v1=y [See HMAC Signature](#hmac-signature)
Authorization | string | Bearer abc (if applicable, [See OAuth 2.0 Bearer Token](#oauth-2-0-bearer-token))

> Example JSON body:

```
  "event": {
    "name": "Absence.Deleted",
    "object_type": "Absence",
    "object_id": 123,
    "object": {
      "id": 123
    } 
  }
```
