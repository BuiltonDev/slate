# Orders

Orders are the result of a User buying a given set of Products and it's what connects Users and Providers.

## Order object

Attributes | Description
---------- | -------
**created** | The date the Order was generated.
**modified** | The date the Order was last modified.
**user** | User associated with Order
human_id | Human readable ID that identifies the Order easily
provider | Provider assigned to Order
items | List of Items associated with an Order
units | Amount of unique Items associated with the Order
total_quantity | Total number of Products in Order
**total_amount** | Amount as a Float with decimal points (`.`). Example: 10.23 NOK.
**currency** | 3 letter ISO currency code as defined by [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217).
top_up_amount | Extra amount to fulfill company's minimum Order value 
delivery_time | Time expected for delivery
delivery_address | Address used for delivery
deliveries | If the Order has multiple deliveries, this is used for storing that Delivery history
billing_address | Address used for billing purposes
payments | List of Payment objects associated with Order
note | Field used to provide extra notes between User and Provider
status | The status of the Invoice. Default is CREATED. Additionally there is: "SCHEDULED", "DONE", "FAILED", "CANCELLED"
**order_status** | Status of the Order. Default is CREATED. Additionally there are: PROCESSING, SUCCESS, CANCELLED, FAILED
**delivery_status** | Status of the Delivery. Default is PENDING. Additionally there are: ACCEPTED, REJECTED, ON_THE_WAY, ARRIVED, DONE, READY_FOR_DELIVERY

## Create an Order

> Definition

```
POST https://api.shareactor.io/orders
```

> Example request:

``` http
POST /orders HTTP/1.1
Content-Type: application/json
Authorization: Bearer <jwt>
X-Share-Api-Key: <shareactor-api-key>
Host: api.shareactor.io

{
  "user": "57ee9c72d76d431f85111432",
  "items": [
    {
      "product": "5703fce3308714000dea1ff1",
      "quantity": 1,
      "discount": 0.1
    },
    {
      "product": "5703fcde308714000dea1fe8",
      "quantity": 3
    }
  ],
  "delivery_time": 1472022000000,
  "delivery_address": {
    "city": "Oslo",
    "geo": [
      59.9294087,
      10.7643042
    ],
    "zip_code": "0557",
    "street_name": "Christies gate 34A",
    "country": "Norway"
  },
  "billing_address": {
    "city": "Oslo",
    "geo": [
      59.9294087,
      10.7643042
    ],
    "zip_code": "0557",
    "street_name": "Christies gate 34A",
    "country": "Norway"
  },
  "currency": "NOK",
  "note": "some type of note"
}
```

``` http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "created": {
    "$date": 1488475795244
  },
  "company": {
    "$oid": "586faf7445ed910006373513"
  },
  "delivery_address": {
    "city": "Oslo",
    "geo": [
      59.9294087,
      10.7643042
    ],
    "zip_code": "0557",
    "street_name": "Christies gate 34A",
    "country": "Norway"
  },
  "billing_address": {
    "city": "Oslo",
    "geo": [
      59.9294087,
      10.7643042
    ],
    "zip_code": "0557",
    "street_name": "Christies gate 34A",
    "country": "Norway"
  },
  "_id": {
    "$oid": "58b85693d76d439fdacea41b"
  },
  "total_amount": 40.0,
  "delivery_time": {
    "$date": 1472022000000
  },
  "note": "some type of note",
  "total_quantity": 4,
  "order_status": "CREATED",
  "items": [
    {
      "product": "5703fce3308714000dea1ff1",
      "quantity": 1,
      "discount": 0.1
    },
    {
      "product": "5703fcde308714000dea1fe8",
      "quantity": 3
    }
  ],
  "user": {
    "$oid": "57ee9c72d76d431f85111432"
  },
  "units": 2,
  "delivery_status": "PENDING",
  "modified": {
    "$date": 1488475795244
  },
  "currency": "NOK"
}
```

Creates a new Order.

Argument | Description
---------- | -------
user | Id of the User who's creating the Order
items | List of Order's items
delivery_time | Time expected for delivery 
delivery_address | Address used for delivery
billing_address | Address used for billing purposes
currency | 3 letter ISO currency code as defined by [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)
note | Field used to provide extra notes between User and Provider

## Retrieve an Order

> Definition

```
GET https://api.shareactor.io/orders/<orderid>
```

> Example request:

``` http
GET /orders/<orderid> HTTP/1.1
Content-Type: application/json
authorization: Bearer <jwt>
X-Share-Api-Key: <shareactor-api-key>
Host: api.shareactor.io
```

``` http
HTTP/1.1 200 OK
Content-type: application/json

{
   "units":2,
   "delivery_status":"ACCEPTED",
   "currency":"NOK",
   "human_id":"YX4PVL",
   "payments":[],
   "modified":{
      "$date":1495196003948
   },
   "provider":{
      "roles":[
         "provider"
      ],
      "stripe_customer_id":"",
      "tags":[],
      "first_name":"john",
      "max_travel_time":1.0,
      "default_address":{
         "service":"google",
         "alias":""
      },
      "note":"",
      "national_id":"",
      "modified":{
         "$date":1495195999676
      },
      "max_travel_meters":10000.0,
      "voucher":{
         "created":{
            "$date":1495195999422
         },
         "expires":{
            "$date":1526731999423
         },
         "consumed":0,
         "initial_quantity":0,
         "uuid":"d062ecff-50d3-46e7-af26-8c2e830dd84f"
      },
      "company":{
         "$oid":"591ee15db70e2a10acb65362"
      },
      "mobile_phone_number":"492 09 385",
      "_cls":"User.Provider",
      "orders":[],
      "schedule":{
         "valid_from":{
            "$date":1495195200000
         },
         "working_sections":[],
         "day_of_week":[
            {
               "end_minute":59,
               "start_hour":0,
               "start_minute":1,
               "end_hour":23,
               "day_of_week":0
            }
         ]
      },
      "available_on_bank_holidays":False,
      "bio":"",
      "avatar":"",
      "created":{
         "$date":1495195999438
      },
      "last_name":"Doe",
      "products":[],
      "_id":{
         "$oid":"591ee15fb70e2a10acb6537d"
      },
      "addresses":[],
      "auth0_id":"",
      "deleted":False,
      "active":True,
      "country":"NOR",
      "email":"john@email.com",
      "billing_address":{
         "service":"google",
         "alias":""
      }
   },
   "top_up_amount":0.0,
   "stripe_charge_id":"",
   "order_status":"CREATED",
   "company":{
      "$oid":"591ee15db70e2a10acb65362"
   },
   "billing_address":{
      "city":"Danielsen",
      "service":"google",
      "alias":"",
      "country":"Paraguay",
      "zip_code":"0556",
      "state":"Oslo",
      "street_name":"Iversenstien 7"
   },
   "deliveries":[],
   "items":[
      {
         "quantity":60,
         "discount":0.9,
         "product":{
            "properties":{},
            "parents":[],
            "path":"/",
            "default_position":[
               -1,
               -1
            ],
            "created":{
               "$date":1494479087000
            },
            "_id":{
               "$oid":"591ee15eb70e2a10acb65374"
            },
            "tags":[],
            "max_distance":0,
            "main_product":True,
            "modified":{
               "$date":1495195998969
            },
            "deleted":False,
            "name":"Ivar",
            "vat":0.0,
            "company":{
               "$oid":"591ee15db70e2a10acb65362"
            },
            "active":True,
            "_cls":"Product",
            "currency":"USD",
            "company_take":-1.0,
            "_sub_products":[],
            "business_rules":[],
            "price":100.0
         }
      }
   ],
   "note":"",
   "created":{
      "$date":1495264401233
   },
   "delivery_address":{
      "city":"Danielsen",
      "service":"google",
      "alias":"",
      "country":"Paraguay",
      "zip_code":"0556",
      "state":"Oslo",
      "street_name":"Iversenstien 7"
   },
   "total_quantity":120,
   "_id":{
      "$oid":"591ee163b70e2a10acb653a7"
   },
   "total_amount":1200.0,
   "stripe_refund_id":"",
   "override_company_take":-1.0,
   "user":{
      "roles":[
         "user"
      ],
      "note":"",
      "stripe_customer_id":"",
      "tags":[],
      "first_name":"john",
      "avatar":"",
      "created":{
         "$date":1495195998668
      },
      "last_name":"Doe",
      "mobile_phone_number":"+47 4242424",
      "_id":{
         "$oid":"591ee15eb70e2a10acb65372"
      },
      "addresses":[
         {
            "city":"Danielsen",
            "service":"google",
            "alias":"",
            "country":"Paraguay",
            "zip_code":"0556",
            "state":"Oslo",
            "street_name":"Iversenstien 7"
         }
      ],
      "national_id":"",
      "modified":{
         "$date":1495195998670
      },
      "deleted":False,
      "voucher":{
         "created":{
            "$date":1495195998667
         },
         "expires":{
            "$date":1526731998667
         },
         "consumed":0,
         "initial_quantity":0,
         "uuid":"d062ecff-50d3-46e7-af26-8c2e830dd84f"
      },
      "auth0_id":"",
      "company":{
         "$oid":"591ee15db70e2a10acb65362"
      },
      "billing_address":{
         "service":"google",
         "alias":""
      },
      "_cls":"User",
      "email":"john@email.com",
      "bio":""
   },
   "delivery_time":{
      "$date":1497009600000
   }
}
```

Retrieves an Order with a given ID.

Argument | Type | Description
-------- | ---- | ------
**orderid** | `string` | ID of the queried Order


## List all Orders

> Definition

```
GET https://api.shareactor.io/orders
```

> Example request:

``` http
GET /orders HTTP/1.1
Content-Type: application/json
Authorization: Bearer <jwt>
X-Share-Api-Key: <shareactor-api-key>
Host: api.shareactor.io
```

``` http
HTTP/1.1 200 OK
Content-Type: application/json

[
    {
       "units":2,
       "delivery_status":"ACCEPTED",
       "currency":"NOK",
       "human_id":"YX4PVL",
       "payments":[],
       "modified":{
          "$date":1495196003948
       },
       "provider":{
          "roles":[
             "provider"
          ],
          "stripe_customer_id":"",
          "tags":[],
          "first_name":"john",
          "max_travel_time":1.0,
          "default_address":{
             "service":"google",
             "alias":""
          },
          "note":"",
          "national_id":"",
          "modified":{
             "$date":1495195999676
          },
          "max_travel_meters":10000.0,
          "voucher":{
             "created":{
                "$date":1495195999422
             },
             "expires":{
                "$date":1526731999423
             },
             "consumed":0,
             "initial_quantity":0,
             "uuid":"d062ecff-50d3-46e7-af26-8c2e830dd84f"
          },
          "company":{
             "$oid":"591ee15db70e2a10acb65362"
          },
          "mobile_phone_number":"492 09 385",
          "_cls":"User.Provider",
          "orders":[],
          "schedule":{
             "valid_from":{
                "$date":1495195200000
             },
             "working_sections":[],
             "day_of_week":[
                {
                   "end_minute":59,
                   "start_hour":0,
                   "start_minute":1,
                   "end_hour":23,
                   "day_of_week":0
                }
             ]
          },
          "available_on_bank_holidays":False,
          "bio":"",
          "avatar":"",
          "created":{
             "$date":1495195999438
          },
          "last_name":"Doe",
          "products":[],
          "_id":{
             "$oid":"591ee15fb70e2a10acb6537d"
          },
          "addresses":[],
          "auth0_id":"",
          "deleted":False,
          "active":True,
          "country":"NOR",
          "email":"john@email.com",
          "billing_address":{
             "service":"google",
             "alias":""
          }
       },
       "top_up_amount":0.0,
       "stripe_charge_id":"",
       "order_status":"CREATED",
       "company":{
          "$oid":"591ee15db70e2a10acb65362"
       },
       "billing_address":{
          "city":"Danielsen",
          "service":"google",
          "alias":"",
          "country":"Paraguay",
          "zip_code":"0556",
          "state":"Oslo",
          "street_name":"Iversenstien 7"
       },
       "deliveries":[],
       "items":[
          {
             "quantity":60,
             "discount":0.9,
             "product":{
                "properties":{},
                "parents":[],
                "path":"/",
                "default_position":[
                   -1,
                   -1
                ],
                "created":{
                   "$date":1494479087000
                },
                "_id":{
                   "$oid":"591ee15eb70e2a10acb65374"
                },
                "tags":[],
                "max_distance":0,
                "main_product":True,
                "modified":{
                   "$date":1495195998969
                },
                "deleted":False,
                "name":"Ivar",
                "vat":0.0,
                "company":{
                   "$oid":"591ee15db70e2a10acb65362"
                },
                "active":True,
                "_cls":"Product",
                "currency":"USD",
                "company_take":-1.0,
                "_sub_products":[],
                "business_rules":[],
                "price":100.0
             }
          }
       ],
       "note":"",
       "created":{
          "$date":1495264401233
       },
       "delivery_address":{
          "city":"Danielsen",
          "service":"google",
          "alias":"",
          "country":"Paraguay",
          "zip_code":"0556",
          "state":"Oslo",
          "street_name":"Iversenstien 7"
       },
       "total_quantity":120,
       "_id":{
          "$oid":"591ee163b70e2a10acb653a7"
       },
       "total_amount":1200.0,
       "stripe_refund_id":"",
       "override_company_take":-1.0,
       "user":{
          "roles":[
             "user"
          ],
          "note":"",
          "stripe_customer_id":"",
          "tags":[],
          "first_name":"john",
          "avatar":"",
          "created":{
             "$date":1495195998668
          },
          "last_name":"Doe",
          "mobile_phone_number":"+47 4242424",
          "_id":{
             "$oid":"591ee15eb70e2a10acb65372"
          },
          "addresses":[
             {
                "city":"Danielsen",
                "service":"google",
                "alias":"",
                "country":"Paraguay",
                "zip_code":"0556",
                "state":"Oslo",
                "street_name":"Iversenstien 7"
             }
          ],
          "national_id":"",
          "modified":{
             "$date":1495195998670
          },
          "deleted":False,
          "voucher":{
             "created":{
                "$date":1495195998667
             },
             "expires":{
                "$date":1526731998667
             },
             "consumed":0,
             "initial_quantity":0,
             "uuid":"d062ecff-50d3-46e7-af26-8c2e830dd84f"
          },
          "auth0_id":"",
          "company":{
             "$oid":"591ee15db70e2a10acb65362"
          },
          "billing_address":{
             "service":"google",
             "alias":""
          },
          "_cls":"User",
          "email":"john@email.com",
          "bio":""
       },
       "delivery_time":{
          "$date":1497009600000
       }
    }
]
```

Retrieves a list of all Orders associated with the company.

Arguments | Type | Description
--------- | ---- | -------
from_date | `timestamp` | Start date. _default is None_
to_date | `timestamp` | End date. _default is None_
date_filter | `string` | Date field used for filter results. _default is created_
size | `int` | Number of items to retrieve. _default is 10_
page | `int` | Which page to retrieve. _default is 0_
order_status | `string` | Return Orders with specific status
delivery_status | `string` | Return Order with specific delivery status
sort | `string` | Field used for sorting results

### date_filter

Arguments | Description
--------- | ------
created | Order by created order date 
delivery | Order by delivery time

### order_status

Arguments | Description
--------- | ------
created | Order is created
processing | Order is on processing
declined | Order is declined for some reason
failed | Order is failed for some reason
success | Order is succeeded
cancelled | Order is cancelled

### delivery_status

Arguments | Description
--------- | -----
CREATED | Delivery is created
PENDING | Delivery is on pending
PROCESSING | Delivery is on processing
ASSIGNING | Delivery assign to provider
PICKUP_STARTED | Delivery pickup the stuff
PICKUP_ARRIVED | Delivery drop the stuff in company
DROPOFF_STARTED | Start to drop the stuff to customer
DROPOFF_ARRIVED | Drop stuff is finished
CANCELLED | Delivery is cancelled
DONE | Delivery task is done
UNKNOWN | Delivery is unknown
QUEUED | Delivery is on queue