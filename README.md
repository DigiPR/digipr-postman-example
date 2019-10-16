# Postman Example
This example illustrates how a REST API can be called with the help of Postman.

#### Contents:
- [Pre-requisite: Postman](#pre-requisite-postman)
- [Task: Make a Sample Call](#task-make-a-sample-call)
    - [Echo-Endpoint](#echo-endpoint)
- [Echo Endpoint on PutsReq](#echo-endpoint-on-putsreq)

## Pre-requisite: Postman

This guide is going to illustrate how API engineering and testing can be done using the API development environment Postman.

You can download Postman from here: https://www.getpostman.com/apps

## Task: Make a Sample Call

The only task in this little example is to call the following `Echo-Endpoint` with the help of Postman:

### Echo-Endpoint
**URL**: [`https://www.putsreq.com/tGemy9dwjunY1e19JcLt`](https://www.putsreq.com/tGemy9dwjunY1e19JcLt) 

**Method:** `POST`

**Sample Request**  • *Header:* `Content-Type: application/json` • *Body:*

```JSON
{
    "variableA": "Data A",
    "variableB": "Data B",
    "businessKey": "case-001"
}
```

• *Optional:* `businessKey`
  
**Success Response**  • *Code:* `200 OK` • *Sample Body:*

```JSON
{
    "variableA": "Data A ECHO!!!",
    "variableB": "Data B ECHO!!!",
    "businessKey": "case-001"
}
```

**Error Response** • *Code:* `404 NOT FOUND`

> Try to figure out how this information can be used to call the `Echo-Endpoint` in Postman.

## Echo Endpoint on PutsReq

> This is optional: Just in case the predefined endpoint is not working or may want to create an own instantiation.

You may create an own version of the Echo-Endpoint on [PutsReq](https://www.putsreq.com) using the following script:

```JavaScript
if (request.headers['CONTENT-TYPE']!='application/json') {
        response.status = 404;
        response.headers = {};
        response.body = 'no JSON body';
} else {
    parsedBody = JSON.parse(request.body);
        
    if (parsedBody.variableA && parsedBody.variableB) {
        response.status = 200;
        response.headers['Content-Type'] = 'application/json';
        response.body = {
            variableA: parsedBody.variableA + " ECHO!!!",
            variableB: parsedBody.variableB  + " ECHO!!!",
            businessKey: parsedBody.businessKey // optional
        };
    } else {
        response.status = 404;
        response.headers = {};
        response.body = 'not found';
    }
}
```
