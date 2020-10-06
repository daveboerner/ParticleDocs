---
title: API Reference


language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  #- ruby
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

We have language bindings in Shell, JavaScript and Python! You can view code examples in the dark area to the right, just select the tab of your prefered language.

# Authentication

> To authorize, use this code:

<!--
```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('token')
```
-->

```python
import requests

url = 'api_endpoint_here'
headers = {'Authorization': 'token'}
r = requests.get(url, headers=headers)
```


```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" -H "Authorization: token"
```


```javascript
var url ='api_endpoint_here';
var headers = {
  "Content-Type": "application/json",
  "Authorization": "token"
}
```


> Make sure to replace `token` with your API key.

When making requests to the Particle API, the data seeker must include an authorization token in the HTTP Header of the request like:

`Authorization: token`

<aside class="notice">
You must replace <code>token</code> with your personal API key.
</aside>

Only accredited data seekers will be credentialed to perform queries against the Particle network.

<a href='mailto:go@particlehealth.com'>Request a developer key</a> 

# Clinical API Operations

## POST Demographics

<!--
```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('token')
api.kittens.get
```
-->
```python
import requests

url = 'https://api.particlehealth.com/particle-sandbox-api/api/v1/queries'
headers = {"Content-Type": "application/json",
'Authorization': 'token'}
data = {
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
r = requests.post(url, headers=headers, json=data)

print(r.json())
```


```shell
curl -X POST "https://api.particlehealth.com/particle-sandbox-api/api/v1/queries" -H "accept: application/json" -H "Authorization: token" -H "Content-Type: application/json" -d "{ \"address_city\": \"Cambridge\", \"address_lines\": [ \"123 Main St\", \"Apt 4\" ], \"address_state\": \"Massachusetts\", \"date_of_birth\": \"1966-01-18\", \"email\": \"john@doe.com\", \"family_name\": \"Hermiston\", \"gender\": \"FEMALE\", \"given_name\": \"Ariel\", \"npi\": \"9876\", \"postal_code\": \"02138\", \"purpose_of_use\": \"TREATMENT\", \"ssn\": \"123-45-6789\", \"telephone\": \"1-234-567-8910\"}"
```

```javascript
const fetch = require('node-fetch');

var url ='https://api.particlehealth.com/particle-sandbox-api/api/v1/queries';
var headers = {
  "Content-Type": "application/json",
  "Authorization": "token"
}

var data = {
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
  var datain = JSON.stringify(data);
  fetch(url, { method: 'POST', headers: headers, body: datain})
  .then((res) => {
     return res.json()
})
.then((json) => {
  console.log(json);
  // Do something with the returned data.
});


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


`
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
`


<aside class="success">
address_lines is an array with each street line seperated by a ,
</aside>

## GET status of all Queries

<!--
```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('token')
api.kittens.get(2)
```
-->
```python
import requests

url = 'https://api.particlehealth.com/particle-sandbox-api/api/v1/queries'
headers = {"Content-Type": "application/json",
'Authorization': 'token'}
r = requests.get(url, headers=headers)

print(r.json())
```

```shell
curl -X GET "https://api.particlehealth.com/particle-sandbox-api/api/v1/queries/" -H "accept: application/json" -H "Authorization: token"
```


```javascript
const fetch = require('node-fetch');

var url ='https://api.particlehealth.com/particle-sandbox-api/api/v1/queries/';
var headers = {
  "Content-Type": "application/json",
  "Authorization": "token"
}

fetch(url, { method: 'GET', headers: headers})
  .then((res) => {
     return res.json()
})
.then((json) => {
  console.log(json);
  // Do something with the returned data.
});
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

<!--
```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('token')
api.kittens.delete(2)
```
-->
```python
import requests

url = 'https://api.particlehealth.com/particle-sandbox-api/api/v1/queries/{query_id}'
headers = {"Content-Type": "application/json",
'Authorization': 'token'}
r = requests.get(url, headers=headers)

print(r.json())
```


```shell
curl -X GET "https://api.particlehealth.com/particle-sandbox-api/api/v1/queries/{query_id}" -H "accept: application/json" -H "Authorization: token"
```


```javascript
const fetch = require('node-fetch');

var url ='https://api.particlehealth.com/particle-sandbox-api/api/v1/queries/{query_id}';
var headers = {
  "Content-Type": "application/json",
  "Authorization": "token"
}

fetch(url, { method: 'GET', headers: headers})
  .then((res) => {
     return res.json()
})
.then((json) => {
  console.log(json);
  // Do something with the returned data.
});
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

`GET https://api.particlehealth.com/particle-sandbox-api/api/v1/queries/{query_id}`

### URL Parameters

Parameter | Description
--------- | -----------
query_id | The ID of the query to request files of

## GET Zip File

<!--
```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('token')
api.kittens.delete(2)
```
-->
```python
import requests

url = 'https://api.particlehealth.com/particle-sandbox-api/api/v1/files/fdca637c-9ef6-4969-8160-9a1a8a805887'
headers = {"Content-Type": "application/zip",
'Authorization': 'token'}
r = requests.get(url, headers=headers)
```


```shell
curl -X GET "https://api.particlehealth.com/particle-sandbox-api/api/v1/files/{query_id}/zip" -H "accept: application/zip" -H "Authorization: token"
```


```javascript
const fetch = require('node-fetch');

var url ='https://api.https://api.particlehealth.com/particle-sandbox-api/api/v1/files/{query_id}/zip.com/particle-sandbox-api/api/v1/queries/';
var headers = {
  "Content-Type": "application/zip",
  "Authorization": "token"
}

fetch(url, { method: 'GET', headers: headers})
  .then((res) => {
     return res.json()
})
.then((json) => {
  console.log(json);
  // Do something with the returned data.
});


```


> The above command returns a zip file of all files found for the patient.

This endpoint retrieves all files associated with a query as a zip file for download.

### HTTP Request

`GET https://api.particlehealth.com/particle-sandbox-api/api/v1/files/{query_id}/zip`

### URL Parameters

Parameter | Description
--------- | -----------
query_id | The ID of the query to request a zipped file of

## GET File

<!--
```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('token')
api.kittens.delete(2)
```
-->
```python
import requests

url = 'https://api.particlehealth.com/particle-sandbox-api/api/v1/files/{query_id}/{file_id}'
headers = {"Content-Type": "octet-stream",
'Authorization': 'token'}
r = requests.get(url, headers=headers)

print(r.text)
```


```shell
curl -X GET "https://api.particlehealth.com/particle-sandbox-api/api/v1/files/{query_id}/{file_id}" -H "accept: application/octet-stream" -H "Authorization: token"
```

```javascript
const fetch = require('node-fetch');

var url ='https://api.particlehealth.com/particle-sandbox-api/api/v1/files/{query_id}/{file_id}';
var headers = {
  "Content-Type": "application/octet-stream",
  "Authorization": "token"
}

fetch(url, { method: 'GET', headers: headers})
  .then((res) => {
     return res.json()
})
.then((json) => {
  console.log(json);
  // Do something with the returned data.
});
```

> The above command returns a specified file found for the patient.

This endpoint retrieves a specified file found for the patient.

### HTTP Request

`GET https://api.particlehealth.com/particle-sandbox-api/api/v1/files/{query_id}/{file_id}`

### URL Parameters

Parameter | Description
--------- | -----------
query_id | The ID of the query to request
file_id | The ID of the file to request

# Architecture

By simply requesting information with a minimum set of demographic information, Particle is able to query partner Health Information Networks (data holders), producing aggregated data in a seamless, efficient and HIPAA compliant manner. 

The demographics to include in the initial POST operation body include:

- Last Name - family_name
- First Name - given_name
- Date of Birth - date_of_birth
- Zip - postal_code - postal_code
- Gender - gender
- Purpose Of Use - purpose_of_use
- NPI : National Provider Identifier - npi (optional - required for treatment based queries)
- City - address_city 
- State - address_state 
- Address - address_lines (optional - success rate increase of ~30%)
- Phone - telephone (optional)
- Social Security Number - ssn (optional)
    
Particle has designed this process with security, simplicity and elegance as central tenets. What took numerous coordinated IHE and RESTful queries across numerous networks has been distilled to a simple API to access data across the health ecosystem - regardless of geographic boundaries or vendor systems. 

Please visit our <a href="https://api.particlehealth.com/portal/">developer portal</a>. 
<img src="images/phdiagram.png" class="logo" alt="Logo" />