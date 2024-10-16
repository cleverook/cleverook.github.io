# REST API cleverook.com

This documentation is the main documentation on [cleverok.com](htttps://cleverok.com)
## Table of Contents
1. [Endpoints](#Endpoints)
2. [Requests](#Requests)
3. [User account](#user-account)
4. [Campains](#campains)

## Endpoints

The API is accessed by making HTTPS requests to a specific version endpoint URL, in which GET, POST, PUT, and DELETE methods dictate how your interact with the objects available. 

Every endpoint is accessed only via the SSL-enabled HTTPS (port 443) protocol.

Every call through API. must be made to the current url

```sh
    https://api.cleverook.com
```

## Requests
Requests must be sent over HTTPS with any payload(when required) formatted in JSON (application/json). 

Every request must include 
- The headers content-type: application/json and api-key.
- Either `x-client-id`  and `x-client-secret` which can be retrieved from the [account settings](https://cleverook.com/me/my-account). 
- Either `Authorization` whith token which can be retrieved after authentication. 

## Responses
### Format
Each response can either 
- Be empty; for example in case of an update which returns an http 204 response and doesn't need to return additional infos or a JSON object.
- Be with a JSON in case of success the JSON object returned for each endpoint is different.

An error object will contain an error code and a human readable description of the error.

### HTTP response codes
 [cleverok.com](htttps://cleverok.com) returns standard html codes

## User account

### Create new account 
#### Request
```json
    POST ENDPOINT/signup
    content-type: application/json
    
    {
        "email": "user@email.fr",
        "firstName": "Armando",
        "lastName": "Pratt",
        "password": "password",
        "phone": "2929292925",
        "phoneIndex": "269"
    }
```

#### Response
```shell
    EMPTY
```
### Activate account
#### Request
```json
    POST ENDPOINT/activation
    content-type: application/json
    {
        "code": "[CODE FROM EMAIL ADDRESS]"
    }
```

#### Response
```shell
    EMPTY
```

### Login and get jwt account
#### Request
```json
    POST ENDPOINT/signin
    content-type: application/json

    {
        "username": "user@email.fr",
        "password": "password"
    }
```

#### Response
```shell
    {
        "token": "JWT_TOKEN"
    }
```

## Campains
### Create campain

#### Request
```json
    POST ENDPOINT/campains
    Content-Type: application/json
    Authorization: Bearer JWT

    {
        "name":"Campagne WHATSAPP",
        "message":`Bonjour  {{lastName}} \nCeci est un  {{other}}`,
        "whatsapp_template":"",
        "time":"00:00",
        "date":"2027-11-15",
        "informations":[
            "{{lastName}}",
            "Test"
        ],
        "channels":[
            "SMS",
            "WHATSAPP",
            "EMAIL"
        ],
        "guests":[
            {
                "firstName":" Achille OK 1",
                "lastName":"SIMO",
                "email":"guest@mail.com",
                "phoneIndex":"+33",
                "phone":"761705745"
            }
        ]
    }

```

#### Response
```shell
    EMPTY
```


### Get all campains

#### Request
```shell
    GET ENDPOINT/campains
    Content-Type: application/json
    Authorization: Bearer JWT
```

#### Response
```json 

[
  {
    "date": "2024-10-16 00:00",
    "ACCEPTED": 1,
    "channels": [
      "EMAIL",
      "SMS",
      "WHATSAPP"
    ],
    "name": "message.send",
    "INITIAL": 1,
    "ERROR": 1,
    "id": "71744202",
    "contacts": 1
  }
]
```

### Get One campain

#### Request
```shell
    GET ENDPOINT/campains/[ID]
    Content-Type: application/json
    Authorization: Bearer JWT
```

#### Response
```json 
{
  "publicId": "71744202",
  "authorId": "670f734b9b74ac17a69e5c0a",
  "status": "DISABLED",
  "name": "message.send",
  "message": "Bonjour  {{lastName}} \n\nTest message {{other}}",
  "whatsapp_template": "",
  "time": "00:00",
  "date": "2024-10-16",
  "informations": [
    "{{lastName}}",
    "sass"
  ],
  "channels": [
    "EMAIL",
    "SMS",
    "WHATSAPP"
  ],
  "guests": [
    {
      "id": "08d8490b-c510-4d45-9b28-b721a1615564",
      "publicId": "04046983",
      "slug": null,
      "civility": "MR",
      "firstName": "Achille",
      "partner": null,
      "lastName": "SIMO",
      "email": "guest@mail.com",
      "phoneIndex": "33",
      "phone": "761705745",
      "trial": true,
      "stocks": null,
      "others": null,
      "qrCode": null
    }
  ]
}
```

### Get One campain statistics

#### Request
```shell
    GET ENDPOINT/campains/[ID]/statistics
    Content-Type: application/json
    Authorization: Bearer JWT
```

#### Response
```json 

{
  "date": "2024-10-16 00:00",
  "ACCEPTED": 1,
  "channels": [
    "EMAIL",
    "SMS",
    "WHATSAPP"
  ],
  "name": "message.send",
  "INITIAL": 1,
  "ERROR": 1,
  "id": "71744202",
  "contacts": 1
}
```