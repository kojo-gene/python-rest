YouTube video tutorial

Building a REST API in Python | Home Automation #2 - Jake Wright

Notes:

REST - Representational State Transfer
    - main features of this is that it should be stateless (can't remember you from state to state)

GET request - used to just get information from API. If you make same GET request multiple times, you should get same response (can use over and over again)

POST request - used to create new resource. If you make same POST request multiple times, you'll get same POST that many times (not safe to do over and over again)

DELETE request - used to delete resources. If make same request over and over, it'll have same effect as if you just did it once (safe to use over and over)

Collection: /devices
 - GET - view collection
 - POST - create new resource

Resource: /device/<identifier>
 - GET - view resource
 - DELETE - delete resource

This will be a device registry service

Usage

ALl responses will have the form

``` json
{
    "data": "Mixed type holding the content of the response",
    "message": "Description of what happened"
}
```

Subsequent repsone definitions will only detail the expected value of the 'data field'

### List all devices

`GET /devices`

**Response**
- `200 OK` on success

```json
[
    {
        "identifier": "floor-lamp",
        "name": "Floor lamp",
        "device_type": "switch",
        "controller_gateway": "192.1.68.0.2"
    },
    {
        "identifier": "samsung-tv",
        "name": "Living room tv",
        "device_type": "tv",
        "controller_gateway": "192.1.68.0.2"
    }
]
```

### Registring a new device

`POST /devices`

- `"identifier":string` a globally unique indentifier for this device
- `"name":string` a friendly name for this device
- `"device_type":string` the type of device as understood by client
- `"controller_gateway":string` the IP address of the device's controller

If a device with the given identifier already exists, the exisiting device will be overwritten

**Response**

-`201 Created` on success

```json
{
    "identifier": "floor-lamp",
    "name": "Floor lamp",
    "device_type": "switch",
    "controller_gateway": "192.1.68.0.2"
}
```

