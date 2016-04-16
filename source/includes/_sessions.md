
# Sessions

## Create a Session
To signin a user, you will want to create a session.  This will take a username and a password and will return an auth token that can be used to authenticate protected resources.
### URL
`https://wastenotfoodtaxi.herokuapp.com/api/v1/sessions`
#### **Method**:`POST`
### HTTP Request
You will pass the email address and password as a session JSON object.

>You will send a JSON object to create the session as shown below.

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

## Destroy a Session
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
