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


# Registration
To register, a user will provide their email, a password, name and other information.  On submitting, they request a token which is generated using their email, password, clientID and a secret.  The username and password will be validated by the server before attempting to create an auth token.  If the user exists, or email / password is not valid respond with a failure.   On success, respond with an authentication token.  With the auth token included in the request header, the client will be able to make a request to register the user entity and store their profile information.

> The request will look something like this
### URL
`/api/v1/auth/token`
#### **Method**:`POST`
#### **URL Params**
#### Request
### Success Response
* **2XX**
* **Auth Token**
### Error Response
* **40X**

# Authentication

> To authorize as a user, you will need to make a request to the server for an access token:

```shell
# With shell, you can just pass the correct header with each request
curl "http://fooddrivr.com/api/v1/auth"
  -H "Authorization: auth_token"
```

> Make sure to replace `auth_token` with the user's token.

The API uses JWT based authentication.  You will make a request, with credentials, for a token.

The API expects for an auth token to be included in all API requests to the server in a header that looks like the following:

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
    "status": 0,
    "types": ["Canned Goods", "Microwave Dinners", "Jelly Beans"],
    "created_at": "2009-06-15T13:45:30",
    "updated_at" : "2009-06-15T13:45:30",
    "participants": {
      "donor": {
        "id": 1,
        "created_at": "2009-06-15T13:45:30",
        "updated_at" : "2009-06-15T13:45:30",
        "name": "Ryan Collins",
        "email": "admin@ryancollins.io",
        "avatar": "http://cloudinary.com/someurl.png",
        "phone" : "2223334444",
        "role": 0
      },
      "driver": {
        "id": 3,
        "created_at": "2009-06-15T13:45:30",
        "updated_at" : "2009-06-15T13:45:30",
        "name": "Harry Potter",
        "email": "harry@hogwarts.edu",
        "avatar": "http://cloudinary.com/harrypotter.png",
        "phone" : "2223334451",
        "role": 0
      }
    },
    "recipient" : {
      "id" : 1243,
      "name": "St. Judes",
      "street_address": "123 Main St.",
      "city": "Boston",
      "zip_code" : "11111",
      "state": "MA",
      "phone": "2223334444"
    },
    "pickup": {
      "latitude": "51.5034070",
      "longitute": "-0.1275920",
      "estimated": "2009-06-15T13:45:30",
      "actual" : "2009-06-15T13:45:30"
    },
    "dropoff": {
      "latitude": "51.5034070",
      "longitute": "-0.1275920",
      "estimated": "2009-06-15T13:45:30",
      "actual" : "2009-06-15T13:45:30"
    },
    "meta": {
      "images": [{
          "url": "http://cloudinary.com/image.png"
        }, {
          "url": "http://cloudinary.com/image.png"
      }],
      "description": "Text description about the items donated"
    }
  },
  {
    "id": 2,
    "status": 1,
    "types": ["Canned Goods", "Microwave Dinners", "Jelly Beans"],
    "created_at": "2009-06-15T13:45:30",
    "updated_at" : "2009-06-15T13:45:30",
    "participants": {
      "donor": {
        "id": 1,
        "created_at": "2009-06-15T13:45:30",
        "updated_at" : "2009-06-15T13:45:30",
        "name": "Ryan Collins",
        "email": "admin@ryancollins.io",
        "avatar": "http://cloudinary.com/someurl.png",
        "phone" : "2223334444",
        "role": 0
      },
      "driver": {
        "id": 3,
        "created_at": "2009-06-15T13:45:30",
        "updated_at" : "2009-06-15T13:45:30",
        "name": "Harry Potter",
        "email": "harry@hogwarts.edu",
        "avatar": "http://cloudinary.com/harrypotter.png",
        "phone" : "2223334451",
        "role": 0
      }
    },
    "recipient" : {
      "id" : 1243,
      "name": "St. Judes",
      "street_address": "123 Main St.",
      "city": "Boston",
      "zip_code" : "11111",
      "state": "MA",
      "phone": "2223334444"
    },
    "pickup": {
      "latitude": "51.5034070",
      "longitute": "-0.1275920",
      "estimated": "2009-06-15T13:45:30",
      "actual" : "2009-06-15T13:45:30"
    },
    "dropoff": {
      "latitude": "51.5034070",
      "longitute": "-0.1275920",
      "estimated": "2009-06-15T13:45:30",
      "actual" : "2009-06-15T13:45:30"
    },
    "meta": {
      "images": [{
          "url": "http://cloudinary.com/image.png"
        }, {
          "url": "http://cloudinary.com/image.png"
      }],
      "description": "Text description about the items donated"
    }
  }
]
```


This endpoint retrieves all donations.

### HTTP Request

`GET http://example.com/api/v1/donations`

### HTTP Response


### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
status    | 0       | Will return the most recent pending donations
embedded | false | If included, user relationships are automatically included in the JSON object. i.e. return donor object in JSON vs. donor_id.

<aside class="warning">
Note: the status must follow the following pattern because the client's expect a numerical value:
```
enum Status: Int {
  pending = 0
  active = 1
  completed = 2
}
```
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
  "id": 1,
  "status": 0,
  "types": ["Canned Goods", "Microwave Dinners", "Jelly Beans"],
  "created_at": "2009-06-15T13:45:30",
  "updated_at" : "2009-06-15T13:45:30",
  "participants": {
    "donor": {
      "id": 1,
      "created_at": "2009-06-15T13:45:30",
      "updated_at" : "2009-06-15T13:45:30",
      "name": "Ryan Collins",
      "email": "admin@ryancollins.io",
      "avatar": "http://cloudinary.com/someurl.png",
      "phone" : "2223334444",
      "role": 0
    },
    "driver": {
      "id": 3,
      "created_at": "2009-06-15T13:45:30",
      "updated_at" : "2009-06-15T13:45:30",
      "name": "Harry Potter",
      "email": "harry@hogwarts.edu",
      "avatar": "http://cloudinary.com/harrypotter.png",
      "phone" : "2223334451",
      "role": 0
    }
  },
  "recipient" : {
    "id" : 1243,
    "name": "St. Judes",
    "street_address": "123 Main St.",
    "city": "Boston",
    "zip_code" : "11111",
    "state": "MA",
    "phone": "2223334444"
  },
  "pickup": {
    "latitude": "51.5034070",
    "longitute": "-0.1275920",
    "estimated": "2009-06-15T13:45:30",
    "actual" : "2009-06-15T13:45:30"
  },
  "dropoff": {
    "latitude": "51.5034070",
    "longitute": "-0.1275920",
    "estimated": "2009-06-15T13:45:30",
    "actual" : "2009-06-15T13:45:30"
  },
  "meta": {
    "images": [{
        "url": "http://cloudinary.com/image.png"
      }, {
        "url": "http://cloudinary.com/image.png"
    }],
    "description": "Text description about the items donated"
  }
}
```

This endpoint retrieves a specific donation.

<aside class="warning">Make sure you pass an auth token<code>&lt;code&gt;</code></aside>

### HTTP Request

`GET http://example.com/api/v1/donations/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the donation to retrieve
