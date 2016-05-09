# Drivers
Drivers have a few main actions they can take to initiate a pickup, change the status of a donation and dropoff the food.

When a donation is created, the location where the food will be picked up is set based on the Donor's default address.  If they do not have a default address, you'll need to submit a location along with the donation to be specific.  We do not want Driver's picking up food at the wrong location, so all of the client's need a verify your address step.  To pickup a donation, a driver will accept the donation.  At each step along the way, the driver sends status updates to the server.  Actions that can be accomplished by a driver include: accept to pickup the food,

## Check Status of A Non-Approved Driver
### URL
`https://wastenotfoodtaxi.herokuapp.com/api/v1/driver/status`
#### **Method**:`GET`
### HTTP Request

#### HTTP Response
Success: 2XX + an active field, showing if the driver has yet to be activated
Error: 4XX

> An example of the JSON received back from a status check
```json
{
  "active": false
}
```

## Driver Donations
Although you can interact with donations through the /donations endpoint, it makes more sense to have them semantically accessible through the driver endpoint.  Also, it provides an interface for interacting with donations specific to a driver.  For example, you can get a list of all the donations for a specific driver, including Pending donations that have yet to be assigned to a driver.  You also have convenience methods for getting a Driver's donation list based on the status of the donation.

## Get All Donations (Pending, Accepted, Completed, Cancelled)
### URL
`https://wastenotfoodtaxi.herokuapp.com/api/v1/driver/donations/all`
#### **METHOD**: `GET`

### HTTP Request
N/A
### HTTP Response
Success: 2XX and an array of Donations, All Pending, and all attached to a Driver

## Get all Pending Donations
### URL
`https://wastenotfoodtaxi.herokuapp.com/api/v1/driver/donations/pending`
#### **METHOD**: `GET`

### HTTP Request
N/A
### HTTP Response
Success: 2XX and an array of Donations, All Pending
Error: 4XX

## Get all Accepted Donations Attached to a Driver
### URL
`https://wastenotfoodtaxi.herokuapp.com/api/v1/driver/donations/accepted`
#### **METHOD**: `GET`

### HTTP Request
N/A
### HTTP Response
Success: 2XX and an array of Donations, All Accepted

## Get all Pending Donations and all Donations tied to a Driver
### URL
`https://wastenotfoodtaxi.herokuapp.com/api/v1/driver/donations/all`
#### **METHOD**: `GET`

### HTTP Request
N/A
### HTTP Response
Success: 2XX and an array of Donations, All Completed

## Get all Cancelled Donations
### URL
`https://wastenotfoodtaxi.herokuapp.com/api/v1/driver/donations/cancelled`
#### **METHOD**: `GET`

### HTTP Request
N/A
### HTTP Response
Success: 2XX and an array of Donations, All Cancelled

### Get a Single Donation by ID
<aside class="notice">
Note: if the donation is assigned to another Driver, you will get a 403 Forbidden.  If the donation is not assigned or belongs to the Driver, you will get back a Donation.
</aside>
### URL
`https://wastenotfoodtaxi.herokuapp.com/api/v1/driver/donations/:donation_id`
#### **METHOD**: `GET`

### HTTP Request
N/A
### HTTP Response
Success: 2XX and a single Donation
Error: 403 if the Donation belongs to another driver.

## Update the Status of a Single Donation
To update the status of a donation, send a request to POST
### URL
`https://wastenotfoodtaxi.herokuapp.com/api/v1/driver/donations/:donation_id/status`
#### **METHOD**: `POST`

### HTTP Request

>Note: The below objects match the three status fields to the status updates a driver will send.

> Pending
```
{
    "status": {
        "donation_status": 0,
        "pickup_status": 0,
        "dropoff_status": 0
    }
}
```

>Accepted by driver, but not yet picked up
```json
{
    "status": {
        "donation_status": 1,
        "pickup_status": 1,
        "dropoff_status": 1
    }
}
```

>Picked up by driver
```json
{
    "status": {
        "donation_status": 1,
        "pickup_status": 2,
        "dropoff_status": 1
    }
}
```

> Dropped off by driver
```json
{
    "status": {
        "donation_status": 2,
        "pickup_status": 2,
        "dropoff_status": 2
    }
}
```

>Cancelled:
Note, a 4 in any status field will set the status of the rest to 4
```json
{
    "status": {
        "donation_status": 4,
        "pickup_status": 4,
        "dropoff_status": 4
    }
}
```

### HTTP Response
Success: 2XX and an array of Donations, All Cancelled
