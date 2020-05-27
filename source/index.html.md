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

> The above command returns JSON matching the body of the POST as well as a state of pending<

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

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

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

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

