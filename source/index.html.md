---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='mailto:go@particlehealth.com'>Request a developer key</a>


includes:
  - errors

search: true
---

# Introduction

Particle Health supports a RESTful Web Service based off the FHIR and CCDA standards. We expose an API by which verified customers (data seekers) may access health records for over 250M unique patients across the U.S. </p>

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Architecture

By simply requesting information with a minimum set of demographic parameters, Particle is able to query partner Health Information Networks (data holders), producing aggregated data in a seamless, efficient and HIPAA compliant manner. 
    
Particle has designed this process with security, simplicity and elegance as central tenets. What took numerous coordinated IHE and RESTful queries across numerous networks has been distilled to a simple API to access data across the health ecosystem - regardless of geographic boundaries or vendor systems. 

Please visit our <a href="https://api.particlehealth.com/portal/">developer portal</a>. 
<img src="images/phdiagram.png" class="logo" alt="Logo" />

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

Particle uses API keys to allow access to the API.  <a href='mailto:go@particlehealth.com'>Request a developer key</a> 

Particle expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: token`

<aside class="notice">
You must replace <code>token</code> with your personal API key.
</aside>

# Clinical API Operations

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
  -X "POST"
  -H "Authorization: token"
  -H "accept: application/json"
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


{
  "address_city": "Cambridge",
  "address_lines": 
  [
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


<aside class="success">
address_lines is an array with each street line seperated by a ,
</aside>

## GET status of all Queries

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
curl "https://api.particlehealth.com/particle-sandbox-api/api/v1/queries/{id}"
  -H "accept: application/json"
  -H "Authorization: token"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('token');
let max = api.kittens.get(2);
```

> The above command returns status of all queries in json like:

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

### HTTP Request

`GET https://api.particlehealth.com/particle-sandbox-api/api/v1/queries/`

## GET status of a Query

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
curl "https://api.particlehealth.com/particle-sandbox-api/api/v1/queries/{id}"
  -H "Authorization: token"
  -H "accept: application/json"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('token');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

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
    "state":"COMPLETE",
    "files":
      [
        {"id":"8d83a62a-f4e0-4ca8-983b-07d8cdcc5329",
      "title":"019713e6-e7c1-4e30-873f-eb5b33f8ff55",
      "type":"application/xml",
      "url":"/api/v1/files/fdca637c-9ef6-4969-8160-9a1a8a805887/8d83a62a-f4e0-4ca8-983b-07d8cdcc5329"
       }
      ]
  ]
}
```

This endpoint retrieves all file pointers associated with a query.

### HTTP Request

`GET https://api.particlehealth.com/particle-sandbox-api/api/v1/queries/{query_id}'

### URL Parameters

Parameter | Description
--------- | -----------
query_id | The ID of the query to request files of

## GET Zip File

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
curl "https://api.particlehealth.com/particle-sandbox-api/api/v1/files/{query_id}"
  -H "accept: application/zip"
  -H "Authorization: token"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('token');
let max = api.kittens.delete(2);
```

> The above command returns a zip file of all files found for the patient.

This endpoint retrieves all files associated with a query as a zip file for download.

### HTTP Request

`GET https://api.particlehealth.com/particle-sandbox-api/api/v1/files/{query_id}/zip

### URL Parameters

Parameter | Description
--------- | -----------
query_id | The ID of the query to request a zipped file of

## GET File

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
curl "https://api.particlehealth.com/particle-sandbox-api/api/v1/files/{query_id}/{file_id}"
  -H "accept: application/octet-stream"
  -H "Authorization: token"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('token');
let max = api.kittens.delete(2);
```

> The above command returns a specified file found for the patient.

This endpoint retrieves a specified file found for the patient.

### HTTP Request

`GET https://api.particlehealth.com/particle-sandbox-api/api/v1/files/{query_id}/{file_id}'

### URL Parameters

Parameter | Description
--------- | -----------
query_id | The ID of the query to request
file_id | The ID of the file to request