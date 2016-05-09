# Donors

The biggest functionality needed for Donors is the ability to donate food.

### Create a Donation
As a signed in Donor, you can create a Donation

```
{
    "donation": {
        "description": "Legacy field before itemized descriptions was added",
        "note": "A note to the driver, optional",
        "pickup_location": {
          "latitude": 36.3817670,
          "longitude": -75.8288640
        },
        "items": [
            {
                "description": "sushi",
                "quantity": "34",
                "unit": "boxes"
            },
            {
                "description": "bratwurst",
                "quantity": "25",
                "unit": "cans"
            }
        ]
    }
}
```

### Update a Donation
