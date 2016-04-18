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
      "id": 1,
      "description": "American apparel before they sold out brunch art sustainable locavore banh mi.",
      "created_at": "2016-04-17T18:31:13.958Z",
      "status_id": 3,
      "updated_at": "2016-04-17T18:31:13.958Z",
      "participants": {
        "donor": {
          "id": 100,
          "phone": "(444)523-6939 x15071",
          "name": "Manuela Steuber",
          "email": "arlo_mann@graham.ca",
          "avatar": null,
          "created_at": "2016-04-17T18:31:09.818Z",
          "updated_at": "2016-04-17T18:31:09.818Z"
        },
        "driver": {
          "id": 46,
          "phone": "1-612-279-6059 x648",
          "name": "Alivia Baumbach",
          "email": "hellen.boyer@stark.biz",
          "avatar": null,
          "created_at": "2016-04-17T18:31:03.037Z",
          "updated_at": "2016-04-17T18:31:03.037Z"
        }
      },
      "donation_types": ["Jujube", "Lime"],
      "pickup": {
        "id": 1,
        "estimated": "2013-02-08T00:00:00.000Z",
        "actual": "2012-08-21T00:00:00.000Z",
        "latitude": "40.5998084143",
        "longitude": "-73.971638773",
        "created_at": "2016-04-17T18:31:14.906Z",
        "updated_at": "2016-04-17T18:31:14.906Z",
        "donation_id": 1,
        "street_address": "7272 Aron Green",
        "street_address_two": "Suite 919",
        "city": "Port Ludie",
        "state": "Montana",
        "zip": "82184"
      },
      "dropoff": {
        "id": 1,
        "estimated": "2014-03-11T00:00:00.000Z",
        "actual": "2013-09-02T00:00:00.000Z",
        "latitude": "34.3823767403",
        "longitude": "-81.611008",
        "created_at": "2016-04-17T18:31:14.936Z",
        "updated_at": "2016-04-17T18:31:14.936Z",
        "donation_id": 1,
        "street_address": "7284 Omer Manors",
        "street_address_two": "Suite 199",
        "city": "Reichertchester",
        "state": "Vermont",
        "zip": "52878"
      },
      "recipient": {
        "id": 84,
        "name": "Kozey, Sauer and Koss",
        "street_address": "887 McDermott Corner",
        "street_address_two": "Suite 169",
        "city": "South Benjaminport",
        "phone": null,
        "created_at": "2016-04-17T18:31:13.475Z",
        "updated_at": "2016-04-17T18:31:13.475Z",
        "state": "Connecticut",
        "zip": "60759"
      },
      "images": ["http://cloudinary.com/image.png", "http://cloudinary.com/image2.png"]
    },
    {
      "id": 2,
      "description": "Cardigan Pitchfork cliche locavore Wes Anderson biodiesel butcher PBR.",
      "created_at": "2016-04-17T18:31:13.966Z",
      "status_id": 2,
      "updated_at": "2016-04-17T18:31:13.966Z",
      "participants": {
        "donor": {
          "id": 7,
          "phone": "261-917-1247 x195",
          "name": "Isabelle Keebler",
          "email": "william_gutkowski@brekke.ca",
          "avatar": null,
          "created_at": "2016-04-17T18:30:58.804Z",
          "updated_at": "2016-04-17T18:30:58.804Z"
        },
        "driver": {
          "id": 95,
          "phone": "716-919-7270",
          "name": "Matilde Becker",
          "email": "isac@schroederswift.biz",
          "avatar": null,
          "created_at": "2016-04-17T18:31:08.840Z",
          "updated_at": "2016-04-17T18:31:08.840Z"
        }
      },
      "donation_types": [
        "Jambul",
        "Lime"
      ],
      "pickup": {
        "id": 2,
        "estimated": "2015-06-26T00:00:00.000Z",
        "actual": "2013-05-06T00:00:00.000Z",
        "latitude": "26.1180992126",
        "longitude": "-90.3760452271",
        "created_at": "2016-04-17T18:31:14.963Z",
        "updated_at": "2016-04-17T18:31:14.963Z",
        "donation_id": 2,
        "street_address": "83882 Deion Circle",
        "street_address_two": "Apt. 460",
        "city": "Hackettview",
        "state": "Idaho",
        "zip": "63475"
      },
      "dropoff": {
        "id": 2,
        "estimated": "2014-12-18T00:00:00.000Z",
        "actual": "2015-03-25T00:00:00.000Z",
        "latitude": "36.2345447488",
        "longitude": "-118.0646387827",
        "created_at": "2016-04-17T18:31:14.972Z",
        "updated_at": "2016-04-17T18:31:14.972Z",
        "donation_id": 2,
        "street_address": "724 Obie Drive",
        "street_address_two": "Suite 589",
        "city": "Eulaton",
        "state": "North Dakota",
        "zip": "65220"
      },
      "recipient": {
        "id": 79,
        "name": "McClure-Hills",
        "street_address": "9293 Stamm Port",
        "street_address_two": "Apt. 066",
        "city": "New Tobyberg",
        "phone": null,
        "created_at": "2016-04-17T18:31:13.448Z",
        "updated_at": "2016-04-17T18:31:13.448Z",
        "state": "California",
        "zip": "57564"
      },
      "images": ["http://cloudinary.com/image.png", "http://cloudinary.com/image2.png"]
    }
  ]
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
  "donation": {
    "id": 2,
    "description": "Cardigan Pitchfork cliche locavore Wes Anderson biodiesel butcher PBR.",
    "created_at": "2016-04-17T18:31:13.966Z",
    "status_id": 2,
    "updated_at": "2016-04-17T18:31:13.966Z",
    "participants": {
      "donor": {
        "id": 7,
        "phone": "261-917-1247 x195",
        "name": "Isabelle Keebler",
        "email": "william_gutkowski@brekke.ca",
        "avatar": null,
        "created_at": "2016-04-17T18:30:58.804Z",
        "updated_at": "2016-04-17T18:30:58.804Z"
      },
      "driver": {
        "id": 95,
        "phone": "716-919-7270",
        "name": "Matilde Becker",
        "email": "isac@schroederswift.biz",
        "avatar": null,
        "created_at": "2016-04-17T18:31:08.840Z",
        "updated_at": "2016-04-17T18:31:08.840Z"
      }
    },
    "donation_types": [
      "Jambul",
      "Lime"
    ],
    "pickup": {
      "id": 2,
      "estimated": "2015-06-26T00:00:00.000Z",
      "actual": "2013-05-06T00:00:00.000Z",
      "latitude": "26.1180992126",
      "longitude": "-90.3760452271",
      "created_at": "2016-04-17T18:31:14.963Z",
      "updated_at": "2016-04-17T18:31:14.963Z",
      "donation_id": 2,
      "street_address": "83882 Deion Circle",
      "street_address_two": "Apt. 460",
      "city": "Hackettview",
      "state": "Idaho",
      "zip": "63475"
    },
    "dropoff": {
      "id": 2,
      "estimated": "2014-12-18T00:00:00.000Z",
      "actual": "2015-03-25T00:00:00.000Z",
      "latitude": "36.2345447488",
      "longitude": "-118.0646387827",
      "created_at": "2016-04-17T18:31:14.972Z",
      "updated_at": "2016-04-17T18:31:14.972Z",
      "donation_id": 2,
      "street_address": "724 Obie Drive",
      "street_address_two": "Suite 589",
      "city": "Eulaton",
      "state": "North Dakota",
      "zip": "65220"
    },
    "recipient": {
      "id": 79,
      "name": "McClure-Hills",
      "street_address": "9293 Stamm Port",
      "street_address_two": "Apt. 066",
      "city": "New Tobyberg",
      "phone": null,
      "created_at": "2016-04-17T18:31:13.448Z",
      "updated_at": "2016-04-17T18:31:13.448Z",
      "state": "California",
      "zip": "57564"
    },
    "images": ["http://cloudinary.com/image.png", "http://cloudinary.com/image2.png"]
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
