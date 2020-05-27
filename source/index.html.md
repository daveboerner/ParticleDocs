---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Particle Health supports a RESTful Web Service based off the FHIR and CCDA standards. We expose an API by which verified customers (data seekers) may access health records for over 250M unique patients across the U.S. </p>

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.


# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('token')
```

```python
import kittn

api = kittn.authorize('token')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: token"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('token');
```

> Make sure to replace `token` with your API key.

Particle uses API keys to allow access to the API.  <go@particlehealth class="com">Request an API key</go@particlehealth> 

Particle expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: token`

<aside class="notice">
You must replace <code>token</code> with your personal API key.
</aside>

# Clinical

## POST Demographics

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('token')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('token')
api.kittens.get()
```

```shell
curl "https://api.particlehealth.com/particle-sandbox-api/api/v1/queries"
  -H "Authorization: token"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('token');
let kittens = api.kittens.get();
```

> The above command returns JSON matching the body of the POST as well as a state of pending

```json
{
  "id":"fdca637c-9ef6-4969-8160-9a1a8a805887",
  "demographics":
    {
      "given_name":"Ariel",
      "family_name":"Hermiston",
      "date_of_birth":"1966-01-18",
      "gender":"FEMALE",
      "ssn":"123-45-6789",
      "email":"john@doe.com",
      "address_lines":
        ["123 Main St",
        "Apt 4"],
      "address_state":"Massachusetts",
      "address_city":"Cambridge",
      "postal_code":"02138",
      "telephone":"(234) 567-8910",
      "npi":"9876",
      "purpose_of_use":"TREATMENT"
    },
  "state":"PENDING"
}
``` 

### HTTP Request

`POST https://api.particlehealth.com/particle-sandbox-api/api/v1/queries`

### Body Payload

```json
{
  "address_city": "Cambridge",
  "address_lines": [
    "123 Main St",
    "Apt 4"
  ],
  "address_state": "Massachusetts",
  "date_of_birth": "1966-01-18",
  "email": "john@doe.com",
  "family_name": "Hermiston",
  "gender": "FEMALE",
  "given_name": "Ariel",
  "npi": "9876",
  "postal_code": "02138",
  "purpose_of_use": "TREATMENT",
  "ssn": "123-45-6789",
  "telephone": "1-234-567-8910"
}
```

<aside class="success">
address_lines is an array with each street line seperated by a ,
</aside>

## GET Status of all Queries

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('token')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('token')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: token"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('token');
let max = api.kittens.get(2);
```

> The above command returns status of all queries like:

```json
{
  "queries":
  [
    "id":"fdca637c-9ef6-4969-8160-9a1a8a805887",
    "demographics":
      {
        "given_name":"Ariel",
        "family_name":"Hermiston",
        "date_of_birth":"1966-01-18",
        "gender":"FEMALE",
        "ssn":"123-45-6789",
        "email":"john@doe.com",
        "address_lines":
          ["123 Main St",
          "Apt 4"],
        "address_state":"Massachusetts",
        "address_city":"Cambridge",
        "postal_code":"02138",
        "telephone":"(234) 567-8910",
        "npi":"9876",
        "purpose_of_use":"TREATMENT"
      },
    "state":"COMPLETE"
  ]
}
```

This endpoint returns the status of all queries.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET https://api.particlehealth.com/particle-sandbox-api/api/v1/queries/<ID>`

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('token')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('token')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: token"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('token');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

