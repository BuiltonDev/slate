# Products

## Product Object

Attribute | Type | Description
--------- | ---- | -------
**name** | `string` | The name of the Product
**price** | `number` | The price of the Product
**currency** |  `string` | Currency (NOK, EUR, ...) ISO 4217
description | `string` | A full description of the Product
short_description | `string` | A brief description of the Product
main_product | `boolean` | Flag that marks whether or not it is a main Product
_sub_products | `array` | A list of sub products under the main Product
parents | `array` | The sub product parent, overhead Product
default_position | `array` | The geo position for the Product
tags | `array` | List of Tags associated with Product
properties | `object` | Product properties
vat | `number` | The percentage of the price of the product that will be paid in addition for the VAT
max_distance | `integer` |
slug | `string` |

## Create a new Product

> Definition

```
POST https://api.shareactor.io/products
```

> Example request:

``` http
POST /products HTTP/1.1
Content-Type: application/json
Authorization: Bearer <jwt>
X-Share-Api-Key: <shareactor-api-key>
Host: api.shareactor.io

{
  "product": 
  {
        "description": "It is a test product",
        "currency": "NOK",
        "price": 3.14,
        "name": "Product Name",
        "vat": 15
    }
}
```

``` http
HTTP/1.1 200 OK
Content-Type: application/json

{  
   "_id":{  
      "$oid":"58f9f856b70e2a56c4a0db3d"
   },
   "max_distance":0,
   "created":{  
      "$date":1492777046366
   },
   "default_position":[  
      -1,
      -1
   ],
   "_cls":"Product",
   "description":"",
   "modified":{  
      "$date":1492777046369
   },
   "_sub_products":[],
   "name":"Product Name",
   "properties":{},
   "price":3.14,
   "active":false,
   "tags":[],
   "vat":15.0,
   "company":{  
      "$oid":"57ee9c71d76d431f8511142f"
   },
   "deleted":false,
   "company_take":-1.0,
   "parents":[],
   "main_product":true,
   "currency":"NOK",
   "path":"/"
}
```

Create a new Product.

Argument | Type | Description
-------- | ---- | -------
**name** | `string` | Name of the product
**price** | `number` | Price of the product
currency | `string` | Currency of the Product. _default set to `NOK`_
vat | `number` | Percentage of price to be paid for VAT. _default set to `0.0`_
description | `string` | Full description of the Product
short_description | `string` | Short description for the product
path | `string` | URL for the product. _default set to `'/'`_
main_product | `boolean` | Flag that marks whether or not it is a main product. _default set to `True`_
_sub_product | `array` | List of sub products under Product. _default set to `[]`_
parents | `array` | List of main product to sub product. _default set to `[]`_
tags | `string` | List of tags associated with product
default_position | `array` | Define product position. _default set to `[-1, -1]`_
properties | `object` | Product properties
max_distance | `integer` | 
provider | `string` | The [`provider`](#providers) assign for the product. Use the id provider
company_take | `number` |
business_rules | `array` |
slug | `array` |


## Retrieve a Product

> Definition

```
GET https://api.shareactor.io/products/<product_id>
```

> Example request:

``` http
GET /products/<product_id> HTTP/1.1
Content-Type: application/json
Authorization: Bearer <jwt>
X-Share-Api-Key: <shareactor-api-key>
Host: api.shareactor.io
```

``` http
HTTP/1.1 200 OK
Content-Type: application/json

{  
   "_cls":"Product",
   "parents":[],
   "tags":[  
      "fuzz",
      "Foo",
      "Bar"
   ],
   "price":3.14,
   "_sub_products":[],
   "deleted":false,
   "company_take":-1.0,
   "max_distance":0,
   "description":"description",
   "created":{  
      "$date":1492781492460
   },
   "vat":0.0,
   "properties":{},
   "active":true,
   "name":"Product Name",
   "modified":{  
      "$date":1492781492461
   },
   "company":{  
      "$oid":"57ee9c71d76d431f8511142f"
   },
   "currency":"NOK",
   "path":"/",
   "main_product":true,
   "_id":{  
      "$oid":"58f9f856b70e2a56c4a0db3d"
   },
   "business_rules":[],
   "default_position":[  
      -1,
      -1
   ]
}
```

Get Product based on product ID

Argument | Type | Description
-------- | ---- | --------
**product_id** | `string` | Product Id


## Get list of all products associated with company

> Definition

```
GET https://api.shareactor.io/products
```

> Example request:

``` http
GET /products HTTP/1.1
Content-Type: application/json
Authorization: Bearer <jwt>
X-Share-Api-Key: <shareactor-api-key>
Host: api.shareactor.io
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

[  
   {  
      "active":true,
      "metadata":{  
         "charge_id":"ch_1ADY0SEeeXxFpLJti58RcN7w"
      },
      "user":{  
         "$oid":"57ee9c72d76d431f85111432"
      },
      "subject":{  
         "_cls":"Invoice",
         "_ref":"57ee9c72d76d431f85111434"
      },
      "company":{  
         "$oid":"57ee9c71d76d431f8511142f"
      },
      "payment_date":{  
         "$date":1493381731652
      },
      "currency":"NOK",
      "created":{  
         "$date":1493381732307
      },
      "_id":{  
         "$oid":"58f9f856b70e2a56c4a0db3d"
      },
      "modified":{  
         "$date":1493381746495
      },
      "human_id":"VPXXN7",
      "payment_method":{  
         "$oid":"<payment_method_id>"
      },
      "current_state":"succeeded",
      "deleted":false,
      "amount":10.0
   }
]
```

Retrieves a list of all Products.

Arguments | Type | Description
--------- | ---- | -----------
size | `integer` | Number of items to retrieve. _default is 10_
page | `integer` | Which page to retrieve. _default is 0_
include_deleted| `boolean` | If `true`, deleted products are also listed
sorting | `string` | Field used for sorting results
lat | `number` | Define the latitude
lng | `number` | Define the longitude
all | `boolean` | If `true` get all products