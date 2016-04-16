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
`https://wastenotfoodtaxi.herokuapp.com/api/v1/users`
### **Method**:`POST`

### HTTP Request
#### **URL Params**
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

## Get a Single User
Getting a user is as simple as making a GET request with an Auth token in the header.  The user resource is protected to only allow the authenticated user to access their own user data.  

```shell
curl -v \
  -H "Content-Type: application/json" \
  -H "Authorization: auth_token" \
  "https://wastenotfoodtaxi.herokuapp.com/api/v1/user/3"
```

### URL
`https://wastenotfoodtaxi.herokuapp.com/api/v1/users/:auth_token)`
#### **Method**:`GET`

### HTTP Request
Parameter | Type | Description
--------- | ------- | -----------
auth_token      | Int | The user's auth_token
### Success Response
* 200
* A User object, as shown above

### Error Response
* 4XX

## Update a User
To update a user, simply create a PATCH request to the user endpoint.  You will pass in a JSON object containing any of the parameters you need to authenticate.

### URL
`https://wastenotfoodtaxi.herokuapp.com/api/v1/users/:auth_token`
#### **Method**:`PATCH`
### HTTP Request
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
### Success Response
* 2XX
### Error Response
* 4XX
