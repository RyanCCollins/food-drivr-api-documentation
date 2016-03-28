---
title: API Reference

language_tabs:
  - shell
  - ruby
  - javascript
  - swift

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Food Drivr API! This documentation should serve as a point of reference for connecting to the API as a user and for interacting with the database.

We have language bindings in Javascript, Ruby, Shell and Swift! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize as a user, you will need to make a request to the server for an access token:

```ruby

```

```swift

```

```shell
# With shell, you can just pass the correct header with each request
curl "http://fooddrivr.com/api/v1/auth"
  -H "Authorization: auth_token"
```

> Make sure to replace `auth_token` with an API token.

The API uses JWT based authentication.  You will make a request, with credentials, for a token.

The Food Drivr API expects for an auth token to be included in all API requests to the server in a header that looks like the following:

`Authorization: auth_token`

<aside class="notice">
Note that the auth token is generated when a user registers or authenticates with a username and password.
</aside>

# Donations

## Get All Donations

```ruby

```

```swift

```

```shell
curl "http://example.com/api/v1/donations"
  -H "Authorization: auth_token"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "donor_id": "12346",
    "driver_id": "12345",
    "coordinates": {
      "latitude": ,
      "longitute": ,
      "accuracy": ,
      "address_listed":
    },
    "initiated": {
      "date_time": "2009-06-15T13:45:30"
    },
    "pickup": {
      "date_time": "2009-06-15T13:45:30"
    },
    "meta": {
      "images": [{
          "url": "http://someimageurl.com/image.png"
        }, {
          "url": "http://someimageurl.com/image.png"
      }],
      "description": "Text description about the items donated"
    }
  },
  {
    "id": 2,
    "donor_id": "12346",
    "driver_id": "12345",
    "coordinates": {
      "latitude": ,
      "longitute": ,
      "accuracy": ,
      "address_listed":
    },
    "initiated": {
      "date_time": "2009-06-15T13:45:30"
    },
    "pickup": {
      "date_time": "2009-06-15T13:45:30"
    },
    "meta": {
      "images": [{
          "url": "http://someimageurl.com/image.png"
        }, {
          "url": "http://someimageurl.com/image.png"
      }],
      "description": "Text description about the items donated"
    }
  }
]
```

This endpoint retrieves all donations.

### HTTP Request

`GET http://example.com/api/v1/donations`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
completed | false | If set to true, the result will include completed requests.
date_range |        | If included, will send a specific date range

<aside class="success">
Remember - you need to include an auth token!
</aside>

## Get a Specific Donation

```ruby

```

```javascript

```

```shell
curl "http://example.com/api/v1/donations/2"
  -H "Authorization: user_token"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "donor_id": "12346",
  "driver_id": "12345",
  "coordinates": {
    "latitude": ,
    "longitute": ,
    "accuracy": ,
    "address_listed":
  },
  "initiated": {
    "date_time": "2009-06-15T13:45:30"
  },
  "pickup": {
    "date_time": "2009-06-15T13:45:30"
  },
  "meta": {
    "images": [{
        "url": "http://someimageurl.com/image.png"
      }, {
        "url": "http://someimageurl.com/image.png"
    }],
    "description": "Text description about the items donated"
  }
},
```

This endpoint retrieves a specific donation.

<aside class="warning">Make sure you pass an auth token<code>&lt;code&gt;</code></aside>

### HTTP Request

`GET http://example.com/api/v1/donations/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the donation to retrieve
