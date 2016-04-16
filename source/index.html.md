---
title: API Reference

language_tabs:
  - shell


toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction
Most requests require very specific headers.  Make sure to include the Content-Type header and the Authorization header for any request.  The only exception to this is when you are creating a User or a Session, in which case you will not yet have an Auth token.

Checkout the section to to the right for an example of your headers

```shell
  "Content-Type: application/json"  
  "Authorization: your_authorization_token"
```

# Create a User
To create / register a user, you will create a User object containing the Name, Username, Password and Password Confirmation.  Pass the user object to the users endpoint via the POST method and you will get back a User object with an auth_token.  

Make sure to pass in a role_id.  If the user is a driver, pass in 1, otherwise if they are a donor pass in 0.  We will put a mechanism in place for approving drivers, so expect that you will not get an auth token back if the user is a driver until they are approved.

>The object that you submit when creating a User will look like this

```json
{
    "user" : {
        "name": "Frank Robert",
        "email": "frank@helloworld.com",
        "password": "helloworld1234",
        "password_confirmation" :"helloworld1234",
        "role_id": 0
    }
}
```


### URL
`POST https://wastenotfoodtaxi.herokuapp.com/api/v1/users`
### **Method**:`POST`
### **URL Params**
### Request
Parameter | Type | Description
--------- | ------- | -----------
name      | String  |
email    |   String |
password | String |
password_confirmation | String |



### Success Response
* **2XX**
* **User object containing an Auth Token**

>Sample user object

```json
{
  "user": {
    "id": 7,
    "phone": null,
    "name": "Ryan Collins",
    "email": "frank@helloworld.com",
    "avatar": null,
    "role_id": 0,
    "created_at": "2016-04-14T22:28:46.523Z",
    "updated_at": "2016-04-14T22:28:46.523Z",
    "auth_token": "somerandomstringhere",
    "setting": {
      "notifications": true,
      "active": true,
      "created_at": "2016-04-15T16:11:41.186Z",
      "updated_at": "2016-04-15T16:11:41.186Z"
    },
    "organization": {
      TBD
    },
    "permissions": {
      TBD
    }
  }
}
```
### Error Response
* **40X**

The API expects for an auth token to be included in all API requests to the server.

<aside class="notice">
Note: implementation for authorization will change, but this should be enough to get you going.  I will be implementing an OAuth /token endpoint that will serve to make this process more secure.
</aside>

# Users
The users resource is setup primarily to provide a mechanism for interacting with a User's profile.  Most actions taken by a User, either a Donor or A Driver are namespaced so that a Donor and Driver have separate actions they can fulfill via the endpoints.

## Get a user (aka Show)
Getting a user is as simple as making a request with an Auth token.  The user resource is protected to only allow the authenticated user to access their own user data.  

### URL
`GET https://wastenotfoodtaxi.herokuapp.com/api/v1/user/:id`
#### **Method**:`GET`
#### HTTP Request
Parameter | Type | Description
--------- | ------- | -----------
id      | Int | The user's id number
#### HTTP Response
Success: A User object, as shown above
Error: 4XX

> See below for an example request
```shell
curl -v \
  -H "Content-Type: application/json" \
  -H "Authorization: auth_token" \
  "https://wastenotfoodtaxi.herokuapp.com/api/v1/user/3"
```

## Update a User
To update a user, simply create a PATCH request to the user endpoint.  You will pass in a JSON object containing any of the parameters you need to authenticate.

### URL
`PATCH https://wastenotfoodtaxi.herokuapp.com/api/v1/user/:id`
#### **Method**:`PATCH`
#### HTTP Request
Pass an object that contains all of the User data you want to update.  Must match the User JSON model.

>Sample user object

```json
{
  "user": {
    "id": 7,
    "phone": "5555555555",
    "name": "Ryan Collins",
    "email": "frank@helloworld.com",
    "avatar": "http://helloworld.com/helloworld.png",
    "role_id": 0,
    "setting": {
      "notifications": true,
      "active": true,
      "created_at": "2016-04-15T16:11:41.186Z",
      "updated_at": "2016-04-15T16:11:41.186Z",
    },
    "organization": {
      TBD
    },
    "permissions": {
      TBD
    }
  }
}
```
#### HTTP Response
Success: 2XX
Error: 4XX

# Sessions
## Create a Session (sign-in a user)
To authenticate or re-authenticate a user, you will want to create a session.  This will take a username and a password and will return an auth token that can be used to authenticate protected resources.
### URL
`https://wastenotfoodtaxi.herokuapp.com/api/v1/sessions`
#### **Method**:`POST`
#### HTTP Request
Pass an object that contains all of the User data you want to update.  Must match the User JSON model.

>You will send a JSON object for the session like so.
```json
{
    "session" : {
        "email": "frank@helloworld.com",
        "password": "helloworld1234"
    }
}
```
#### HTTP Response
Success: A User object, as shown above under Registering a User.
Error: 4XX


```shell
curl -v \
  -H "Content-Type: application/json" \
  -H "Authorization: auth_token" \
  "https://wastenotfoodtaxi.herokuapp.com/api/v1/sessions"
```

# Signout the User (Destroy a Session)
To signout a user, you will need to submit a DELETE request to the sessions endpoint.  Pass in the user's auth token as a URL parameter.  

### URL
`https://wastenotfoodtaxi.herokuapp.com/api/v1/sessions/:id`

#### **Method**:`DELETE`
#### HTTP Request
<aside class="notice">
Note: The id field passed into is the ID of the session, which is your auth_token, not the ID of the user.
</aside>

#### HTTP Response
Success: 204, No Content
Error: 4XX

```shell
curl -v \
  -H "Content-Type: application/json" \
  -H "Authorization: auth_token" \
  "https://wastenotfoodtaxi.herokuapp.com/api/v1/sessions/KoPrTKYYMzqmrEJQsnAb"
```

# Donations

You can get a list of donations, get a single donation, create a single donation and update a donation.
<aside class="notice">
Note: There are several related fields for each donation, such as the Status of the donation and the Type of donation.  Using the related integer value for these fields is the simplest way to interact with the API.
</aside>

Example for DonationStatus
```
enum DonationStatus: Int {
  PendingAction = 0
  Accepted = 1
  Completed = 2
  Cancelled = 3
}
```

## Get All Donations
To get a list of donations, you will need to pass your auth token.  You will get an array of donations (See below).

```shell
curl -v \
  -H "Content-Type: application/json" \
  -H "Authorization: auth_token" \
  "https://wastenotfoodtaxi.herokuapp.com/api/v1/donations"
```

> The above command returns JSON structured like this:

```json
{
  "donations": [
    {
      "id": 2,
      "description": null,
      "created_at": "2016-04-09T21:35:00.520Z",
      "updated_at": "2016-04-09T21:35:00.520Z",
      "participants": {
        "donor": {
          "id": 31,
          "phone": "(443)512-2849",
          "name": "Trinity McGlynn",
          "email": "macey@cummingsauer.info",
          "avatar": null,
          "created_at": "2016-04-09T21:34:54.933Z",
          "updated_at": "2016-04-09T21:34:54.933Z"
        },
        "driver": {
          "id": 73,
          "phone": "843-958-0149 x6609",
          "name": "Sandy Hilpert",
          "email": "jakob.kemmer@hessel.us",
          "avatar": null,
          "created_at": "2016-04-09T21:34:58.004Z",
          "updated_at": "2016-04-09T21:34:58.004Z"
        }
      },
      "pickup": null,
      "dropoff": null,
      "donation_types": ["Canned Goods", "Pizza"]
    },
    {
      "id": 3,
      "description": null,
      "created_at": "2016-04-09T21:35:00.522Z",
      "updated_at": "2016-04-09T21:35:00.522Z",
      "participants": {
        "donor": {
          "id": 23,
          "phone": "(453)995-9600 x36010",
          "name": "Nathan Muller",
          "email": "marion.kulas@fritsch.us",
          "avatar": null,
          "created_at": "2016-04-09T21:34:54.356Z",
          "updated_at": "2016-04-09T21:34:54.356Z"
        },
        "driver": {
          "id": 2,
          "phone": "+1 123 456 789",
          "name": "Driver User",
          "email": "driver@hacksmiths.com",
          "avatar": "http://cloudinary.com/someurl.png",
          "created_at": "2016-04-09T21:34:52.777Z",
          "updated_at": "2016-04-09T21:34:52.777Z"
        }
      },
      "recipient": {
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
      "donation_types": ["Canned Goods", "Pizza"]
    }]
  }

[
  {
    "id": 1,
    "status": 0,
    "donation_types": ["Canned Goods", "Microwave Dinners", "Jelly Beans"],
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

### HTTP Request

`GET https://wastenotfoodtaxi.herokuapp.com/api/v1/donations`

### HTTP Response
Success: 2XX and a Donations array as shown above
Error: 4XX

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
status    | 0       | Will return the most recent pending donations
embedded | true | If included, user relationships are automatically included in the JSON object. i.e. return donor object in JSON vs. donor_id.

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

## Update a Donation
To update a donation, you will submit a PATCH to the donations endpoint.  Submit any parameters that will need to be updated, following the schema above for the donation JSON object.

> An example request
```shell
curl -v \
  -H "Content-Type: application/json" \
  -H "Authorization: auth_token" \
  "https://wastenotfoodtaxi.herokuapp.com/api/v1/donations/:id"
```

<aside class="warning">Make sure you pass an auth token in the header<code>&lt;code&gt;</code></aside>

### HTTP Request
`GET https://wastenotfoodtaxi.herokuapp.com/api/v1/donations/:id`
### URL Parameters
Parameter | Description
--------- | -----------
ID        | The ID of the donation to update
Other Donation Params |  Follow the schema defined above for donations

## Get a Specific Donation

```shell
curl "https://wastenotfoodtaxi.herokuapp.com/api/v1/donations/:id"
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
`GET https://wastenotfoodtaxi.herokuapp.com/api/v1/donations/:id`

### URL Parameters
Parameter | Description
--------- | -----------
ID | The ID of the donation to retrieve
