# README

In this app we cover the the endpoint described in the challenge.

## Endpoints

### Record readings

`POST /readings`

    * `body`: JSON object with the following fields:
        * `id`: string describing the device's id
        * `readings`: Array of objects with the following fields:
            * `timestamp`: string in iso8601 format
            * `count`: number

```
{
    "id": "36d5658a-6908-479e-887e-a949ec199272",
    "readings": [
        {
            "timestamp": "2021-09-29T16:08:15+01:00",
            "count": 2
        },
        {
            "timestamp": "2021-09-29T16:09:15+01:00",
            "count": 15
        }
    ]
}
```

### Get latest readings

    * `GET /readings/:devicce_id/last_reading`

#### Response

```
{
"count": 2,
"timestamp": "2021-12-29T16:08:15.000+01:00"
}`
```

### Get cumulative reading count for a device

    * `GET /readings/:device_id/accumulative`

#### Response

`57`

## Design decisions

The app uses **Redis** as an in-memory storage. Since it's not technicaly a database it should comply with the exercice contraint.
This allows us to have the information available across requests and be able to handle concurrency since it's thread safe.
The use of interactions was used to filter the incoming params so we can count with built-in validation. This also allows us to isolate
the code to a specific part of the business feature. For this instance it might be an overkill but it serves its purpose.

## Nice to have without time constraints

Personally i would have dedicated more time to testing. I must confess that this code is under no circumstances production ready.
There is redundant code that can be seen in the interactions concerning the access of the data stored in **redis** so decoupling this into
a module of some kind would have been nice, i.e an adapter pattern that, according to the used database, could be injected as a dependency.




