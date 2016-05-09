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
       "id": 7,
       "description": "Legacy description field before items were added. Ignore.",
       "note": "Make sure to pull around back",
       "created_at": "2016-05-07T23:45:50.287Z",
       "updated_at": "2016-05-07T23:45:50.287Z",
       "status_id": 1,
       "status": {
         "id": 1,
         "description": "Accepted"
       },
       "participants": {
         "donor": {
           "id": 1,
           "phone": "+1 123 456 789",
           "name": "Donor User",
           "email": "donor@hacksmiths.com",
           "avatar": null
         },
         "driver": {
           "id": 74,
           "phone": "1-775-894-8780",
           "name": "Gennaro Rau",
           "email": "nya@beattysmitham.name",
           "avatar": null
         }
       },
       "pickup": {
         "estimated": null,
         "actual": null,
         "latitude": "0.0",
         "longitude": "0.0",
         "street_address": null,
         "street_address_two": null,
         "city": null,
         "state": null,
         "zip": null,
         "status": {
           "id": 0,
           "description": "Pending"
         },
         "status_id": 0
       },
       "dropoff": {
         "estimated": "2014-01-23T00:00:00.000Z",
         "actual": "2016-03-01T00:00:00.000Z",
         "latitude": "40.8377346033",
         "longitude": "-81.611008",
         "street_address": "13831 Youth Street Northwest",
         "street_address_two": "Apt. 558",
         "city": "North Lawrence",
         "state": "Ohio",
         "zip": "44666",
         "status": {
           "id": 0,
           "description": "Pending"
         },
         "status_id": 0
       },
       "recipient": {
         "id": 5,
         "name": "Christiansen, Crona and West",
         "street_address": "80324 Marcellus Centers",
         "street_address_two": "Suite 947",
         "city": "Weissnatshire",
         "phone": 1,
         "created_at": "2016-05-07T23:45:39.842Z",
         "updated_at": "2016-05-07T23:45:39.842Z",
         "state": "Florida",
         "zip": "05582",
         "country_code": "US",
         "latitude": "0.0",
         "longitude": "0.0"
       },
       "items": [
         {
           "description": "Ostrich",
           "unit": "t",
           "quantity": 4
         },
         {
           "description": "Veal",
           "unit": "gr",
           "quantity": 18
         },
         {
           "description": "Venison",
           "unit": "cwt",
           "quantity": 16
         },
         {
           "description": "Chicken",
           "unit": "gr",
           "quantity": 12
         },
         {
           "description": "Bone soup from allowable meats",
           "unit": "gr",
           "quantity": 11
         },
         {
           "description": "Liver",
           "unit": "gr",
           "quantity": 7
         }
       ],
       "images": []
     },
     {
       "id": 16,
       "description": "Banh mi butcher mlkshk cardigan viral hoodie tofu.",
       "created_at": "2016-05-07T23:45:50.464Z",
       "updated_at": "2016-05-07T23:45:50.464Z",
       "status_id": 1,
       "status": {
         "id": 1,
         "description": "Accepted"
       },
       "participants": {
         "donor": {
           "id": 1,
           "phone": "+1 123 456 789",
           "name": "Donor User",
           "email": "donor@hacksmiths.com",
           "avatar": null
         },
         "driver": {
           "id": 42,
           "phone": "(267)163-4915 x7030",
           "name": "Braulio Jacobi",
           "email": "pearlie.kunde@crooksbuckridge.ca",
           "avatar": null
         }
       },
       "pickup": {
         "estimated": null,
         "actual": null,
         "latitude": "0.0",
         "longitude": "0.0",
         "street_address": null,
         "street_address_two": null,
         "city": null,
         "state": null,
         "zip": null,
         "status": {
           "id": 0,
           "description": "Pending"
         },
         "status_id": 0
       },
       "dropoff": {
         "estimated": "2012-11-23T00:00:00.000Z",
         "actual": "2015-03-04T00:00:00.000Z",
         "latitude": "33.4280828891",
         "longitude": "-87.888795",
         "street_address": "Elmore Road",
         "street_address_two": "Apt. 261",
         "city": "Gordo",
         "state": "Alabama",
         "zip": "35466",
         "status": {
           "id": 0,
           "description": "Pending"
         },
         "status_id": 0
       },
       "recipient": {
         "id": 16,
         "name": "Lowe-Kihn",
         "street_address": "11573 New York 22",
         "street_address_two": "Apt. 524",
         "city": "Comstock",
         "phone": 950,
         "created_at": "2016-05-07T23:45:46.477Z",
         "updated_at": "2016-05-07T23:45:46.477Z",
         "state": "New York",
         "zip": "12821",
         "country_code": "US",
         "latitude": "43.46012",
         "longitude": "-73.4121277"
       },
       "items": [
         {
           "description": "Turtle",
           "unit": "t",
           "quantity": 1
         },
         {
           "description": "Quail",
           "unit": "gr",
           "quantity": 10
         },
         {
           "description": "Pheasant",
           "unit": "lb",
           "quantity": 12
         },
         {
           "description": "Beef liver",
           "unit": "t",
           "quantity": 20
         },
         {
           "description": "Chicken Liver",
           "unit": "t",
           "quantity": 2
         },
         {
           "description": "Ostrich",
           "unit": "lb",
           "quantity": 7
         }
       ],
       "images": []
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
    "id": 7,
    "note": "Optional note to the driver, should they need more instructions about a donation.",
    "created_at": "2016-05-07T23:45:50.287Z",
    "updated_at": "2016-05-07T23:45:50.287Z",
    "status_id": 1,
    "status": {
      "id": 1,
      "description": "Accepted"
    },
    "participants": {
      "donor": {
        "id": 1,
        "phone": "+1 123 456 789",
        "name": "Donor User",
        "email": "donor@hacksmiths.com",
        "avatar": null
      },
      "driver": {
        "id": 74,
        "phone": "1-775-894-8780",
        "name": "Gennaro Rau",
        "email": "nya@beattysmitham.name",
        "avatar": null
      }
    },
    "pickup": {
      "estimated": null,
      "actual": null,
      "latitude": "0.0",
      "longitude": "0.0",
      "street_address": null,
      "street_address_two": null,
      "city": null,
      "state": null,
      "zip": null,
      "status": {
        "id": 0,
        "description": "Pending"
      },
      "status_id": 0
    },
    "dropoff": {
      "estimated": "2014-01-23T00:00:00.000Z",
      "actual": "2016-03-01T00:00:00.000Z",
      "latitude": "40.8377346033",
      "longitude": "-81.611008",
      "street_address": "13831 Youth Street Northwest",
      "street_address_two": "Apt. 558",
      "city": "North Lawrence",
      "state": "Ohio",
      "zip": "44666",
      "status": {
        "id": 0,
        "description": "Pending"
      },
      "status_id": 0
    },
    "recipient": {
      "id": 5,
      "name": "Christiansen, Crona and West",
      "street_address": "80324 Marcellus Centers",
      "street_address_two": "Suite 947",
      "city": "Weissnatshire",
      "phone": 1,
      "created_at": "2016-05-07T23:45:39.842Z",
      "updated_at": "2016-05-07T23:45:39.842Z",
      "state": "Florida",
      "zip": "05582",
      "country_code": "US",
      "latitude": "0.0",
      "longitude": "0.0"
    },
    "items": [
      {
        "description": "Ostrich",
        "unit": "t",
        "quantity": 4
      },
      {
        "description": "Veal",
        "unit": "gr",
        "quantity": 18
      },
      {
        "description": "Venison",
        "unit": "cwt",
        "quantity": 16
      },
      {
        "description": "Chicken",
        "unit": "gr",
        "quantity": 12
      },
      {
        "description": "Bone soup from allowable meats",
        "unit": "gr",
        "quantity": 11
      },
      {
        "description": "Liver",
        "unit": "gr",
        "quantity": 7
      }
    ],
    "images": []
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
