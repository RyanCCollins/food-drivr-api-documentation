# Donations

You can get a list of donations, get a single donation, create a single donation and update a donation.
<aside class="notice">
Note: There are several related fields for each donation, such as the Status of the donation and the Type of donation.  Using the related integer value for these fields is the simplest way to interact with the API.
</aside>

>Example enum in Ryan (a new programming language) for DonationStatus
```
enum DonationStatus: Int {
  PendingAction = 0
  Accepted = 1
  Completed = 2
  Cancelled = 3
}
```

## Get All Donations
To get a list of donations, submit a GET request to the donations endpoint.  Make sure to include your auth token, as described above.  You will get an array of donations (See below).

```shell
curl -v \
  -H "Content-Type: application/json" \
  -H "Authorization: auth_token" \
  "https://wastenotfoodtaxi.herokuapp.com/api/v1/donations"
```

> An example of the data returned from the endpoint is shown below

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
```

### HTTP Request

`GET https://wastenotfoodtaxi.herokuapp.com/api/v1/donations`
### Method
GET

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
