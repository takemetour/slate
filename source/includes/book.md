# Book

## Book Product

> Required Request body for any product type

```json
{
  "name": {
    "first": "John",
    "last": "Doe"
  },
  "email": "john+doe@takemetour.com",
  "mobile": "+66856667571",
  "country": "TH",
  "trip_id": "58ff211702b3ea0011efe846",
  "trip_date": "2018-04-08T17:00:00.000Z",
  "meeting_point": "BTS Station - Asok"
}
```

**HTTP Request:** `POST /transactions/book`

To book our product (a.k.a. create transaction). **There is required field for any product type** as shown below.

Parameter | Type | Description
--------- | ---- | -----------
name | **Object** | Customer first name and last name. Specific in `first` and `last` key. Max length for first name and last name are 255 characters
email | **String (Max Length: 255)** | Customer email
mobile | **String (Max Length: 20)** | Customer mobile (with prefix country code)
country | **String** | Country code (See [appendix](#country-code))
trip_id | **String (Exact Length: 24)** | `_id` of product to be book
trip_date | **ISODate string (GMT +07:00)** | Date to book the product (in case of product type `souvenir` this field is use as "delivery date" if the product is required date) in 
meeting_point | **String (Max length: 255)** | Meeting point for customer (See [appendix](#meeting-point) / if product has `is_hide_meeting_point` value as `true` this field can be omit)

**Note**

- Our API now only support payment method by using partner credit to your account.
- Make sure that your credit is sufficient for each transaction. (Checking `grandTotal` from [Get Product Price](#get-product-price) and your `partner_credit` from [User info](#user-info))

## Book Local Experience Trips

> Request body to book product type `trip`

```json
{
  "name": {
    "first": "John",
    "last": "Doe"
  },
  "email": "john+doe@takemetour.com",
  "mobile": "+66856667571",
  "country": "TH",
  "trip_id": "58ff211702b3ea0011efe846",
  "trip_date": "2018-04-08T17:00:00.000Z",
  "meeting_point": "BTS Station - Asok",
  "quantity": 2,
  "selected_options": []
}
```

>Code

```shell
curl 'https://api.staging.takemetour.com/partner/transactions/book' \
-H 'content-type: application/json' \
-H 'x-access-token: 0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3' \
--data-binary '{"name":{"first":"John","last":"Doe"},"email":"john+doe@takemetour.com","mobile":"+66856667571","country":"TH","trip_id":"58ff211702b3ea0011efe846","trip_date":"2018-04-08T17:00:00.000Z","meeting_point":"BTS Station - Asok","quantity":2,"selected_options":[]}'
```

```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/transactions/book',
{
  headers: {
    'content-type': 'application/json',
    'x-access-token': '0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
  },
  body: JSON.stringify({
    "name": {
      "first": "John",
      "last": "Doe"
    },
    "email": "john+doe@takemetour.com",
    "mobile": "+66856667571",
    "country": "TH",
    "trip_id": "58ff211702b3ea0011efe846",
    "trip_date": "2018-04-08T17:00:00.000Z",
    "meeting_point": "BTS Station - Asok",
    "quantity": 2,
    "selected_options": []
  }),
  method: 'POST'
});
const data = await response.json();
```
> Request body to book product type `trip` with additional options

```json
{
  "name": {
    "first": "John",
    "last": "Doe"
  },
  "email": "john+doe@takemetour.com",
  "mobile": "+66856667571",
  "country": "TH",
  "trip_id": "58ff211702b3ea0011efe846",
  "trip_date": "2018-04-08T17:00:00.000Z",
  "meeting_point": "Florida Hotel, Phayathai, Bangkok",
  "quantity": 3,
  "selected_options": [
    {
      "key": "children",
      "currency": "THB",
      "quantity_type": "sum_max_travelers",
      "price": 290,
      "type": "child_price",
      "title": "Child (Age 2-12)",
      "_id": "599e66640ea28b0011b3f147",
      "lx_price": 290,
      "is_front": false,
      "quantity": 2,
      "is_included_for_booking_fee": true
    },
    {
      "_id": "59db3d06909883001003d38e",
      "title": "Hotel Pickup",
      "type": "book.checkbox",
      "price": 500,
      "quantity_type": "boolean",
      "currency": "THB",
      "key": "hotel",
      "lx_price": 0,
      "is_front": false,
      "quantity": 1,
      "is_included_for_booking_fee": false
    }
  ]
}
```

>Code

```shell
curl 'https://api.staging.takemetour.com/partner/transactions/book' \
-H 'content-type: application/json' \
-H 'x-access-token: 0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3' \
--data-binary '{"name":{"first":"John","last":"Doe"},"email":"john+doe@takemetour.com","mobile":"+66856667571","country":"TH","trip_id":"58ff211702b3ea0011efe846","trip_date":"2018-04-08T17:00:00.000Z","meeting_point":"Florida Hotel, Phayathai, Bangkok","quantity":2,"selected_options":[{"key":"children","currency":"THB","quantity_type":"sum_max_travelers","price":290,"type":"child_price","title":"Child (Age 2-12)","_id":"599e66640ea28b0011b3f147","lx_price":290,"is_front":false,"quantity":0,"is_included_for_booking_fee":true},{"_id":"59db3d06909883001003d38e","title":"Hotel Pickup","type":"book.checkbox","price":500,"quantity_type":"boolean","currency":"THB","key":"hotel","lx_price":0,"is_front":false,"quantity":1,"is_included_for_booking_fee":false}]}'
```

```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/transactions/book',
{
  headers: {
    'content-type': 'application/json',
    'x-access-token': '0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
  },
  body: JSON.stringify({
    "name": {
      "first": "John",
      "last": "Doe"
    },
    "email": "john+doe@takemetour.com",
    "mobile": "+66856667571",
    "country": "TH",
    "trip_id": "58ff211702b3ea0011efe846",
    "trip_date": "2018-04-08T17:00:00.000Z",
    "meeting_point": "Florida Hotel, Phayathai, Bangkok",
    "quantity": 2,
    "selected_options": [
      {
        "key": "children",
        "currency": "THB",
        "quantity_type": "sum_max_travelers",
        "price": 290,
        "type": "child_price",
        "title": "Child (Age 2-12)",
        "_id": "599e66640ea28b0011b3f147",
        "lx_price": 290,
        "is_front": false,
        "quantity": 0,
        "is_included_for_booking_fee": true
      },
      {
        "_id": "59db3d06909883001003d38e",
        "title": "Hotel Pickup",
        "type": "book.checkbox",
        "price": 500,
        "quantity_type": "boolean",
        "currency": "THB",
        "key": "hotel",
        "lx_price": 0,
        "is_front": false,
        "quantity": 1,
        "is_included_for_booking_fee": false
      }
    ]
  }),
  method: 'POST'
});
const data = await response.json();
```

> Response

```json
{
  "success": true,
  "booking_id": TransactionId
}
```

For product type `trip` you must add `quantity` and also `selected_options` for the product that has `child` key in `additional_options` field of product.

### Request body (add from [basic book parameters](#book-product))

Parameter | Type | Description
--------- | ---- | -----------
quantity | **Number (quantity + child quantity must not exceed `max_travelers` from [product detail](#get-product-detail))** | Quantity of customer
selected_options | **Array of option** | See  [additional options](#additional-options) for more detail

### Response
Response will return `success` to show that the booking process is success or not, and `transaction_id`.

Parameter | Type | Description
--------- | ---- | -----------
success | **Boolean** | Transaction is success or not
transaction_id | **String (Exact Length: 24)** | Transaction unique id
message | **String** | If transaction is not success. Message will provide

**Remark:** If `success` equal to `false` but still return `transaction_id` please contact us.

## Book Attraction Tickets

> Request body to book product type `ticket`

```json
{
  "name": {
    "first": "John",
    "last": "Doe"
  },
  "email": "john+doe@takemetour.com",
  "mobile": "+66856667571",
  "country": "TH",
  "trip_id": "5a3a0af6c0214700127dadf5",
  "trip_date": "2018-04-11T17:00:00.000Z",
  "multi_tier_quantity": [
    {
      "tier": "Admission Fee - Aquarium Only",
      "_id": "5a1e87a5b549a700121cb93d",
      "sub_tiers": [
        {
          "display_price": 990,
          "price": 600,
          "name": "Adult",
          "_id": "5a1e87a5b549a700121cb93f",
          "globaltix_ticket_id": "4136",
          "has_availability": true,
          "globaltix_questions": [
            {
              "type": "FREETEXT",
              "question": "Customer name",
              "id": 11968
            }
          ],
          "globaltix_redeem": {
            "end": "2018-12-31T23:59:00",
            "start": "2018-01-10T00:00:00"
          },
          "globaltix_cost": 1500,
          "quantity": 0
        },
        {
          "display_price": 790,
          "price": 550,
          "name": "Child",
          "_id": "5a1e87a5b549a700121cb93e",
          "globaltix_ticket_id": "4136",
          "has_availability": true,
          "globaltix_questions": [
            {
              "type": "FREETEXT",
              "question": "Customer name",
              "id": 11968
            }
          ],
          "globaltix_redeem": {
            "end": "2018-12-31T23:59:00",
            "start": "2018-01-10T00:00:00"
          },
          "globaltix_cost": 1500,
          "quantity": 0
        }
      ]
    },
    {
      "tier": "COMBO: Aquarium + 4D Movie",
      "_id": "5a1e87a5b549a700121cb93a",
      "sub_tiers": [
        {
          "display_price": 1090,
          "price": 700,
          "name": "Adult",
          "_id": "5a1e87a5b549a700121cb93c",
          "globaltix_ticket_id": "4138",
          "has_availability": false,
          "globaltix_questions": [
            {
              "type": "DATE",
              "question": "Service Date",
              "id": 11969,
              "answer": "2018-04-12"
            },
            {
              "type": "FREETEXT",
              "question": "Nationality",
              "id": 11970,
              "answer": "Thailand"
            },
            {
              "options": [
                "Afternoon",
                "Morning"
              ],
              "type": "OPTION",
              "question": "Select Time",
              "id": 11971,
              "answer": "Afternoon"
            }
          ],
          "globaltix_redeem": {
            "end": "2018-12-31T23:59:00",
            "start": "2018-01-10T00:00:00"
          },
          "globaltix_cost": 270,
          "quantity": 2
        },
        {
          "display_price": 890,
          "price": 650,
          "name": "Child",
          "_id": "5a1e87a5b549a700121cb93b",
          "globaltix_ticket_id": "4139",
          "has_availability": false,
          "globaltix_questions": [
            {
              "type": "DATE",
              "question": "Service Date",
              "id": 11969,
              "answer": "2018-04-12"
            },
            {
              "type": "FREETEXT",
              "question": "Nationality",
              "id": 11970,
              "answer": "Thailand"
            },
            {
              "options": [
                "Afternoon",
                "Morning"
              ],
              "type": "OPTION",
              "question": "Select Time",
              "id": 11971,
              "answer": "Afternoon"
            }
          ],
          "globaltix_redeem": {
            "end": "2018-12-31T23:59:00",
            "start": "2018-01-10T00:00:00"
          },
          "globaltix_cost": 220,
          "quantity": 1
        }
      ]
    },
    {
      "tier": "Photo Pack : Aquarium + Photo (6\" x 9\")",
      "_id": "5a1e87a5b549a700121cb937",
      "sub_tiers": [
        {
          "display_price": 1190,
          "price": 800,
          "name": "Adult",
          "_id": "5a1e87a5b549a700121cb939",
          "quantity": 0
        },
        {
          "display_price": 990,
          "price": 750,
          "name": "Child",
          "_id": "5a1e87a5b549a700121cb938",
          "quantity": 0
        }
      ]
    },
    {
      "tier": "Aquarium + Glass Bottom Boat (GBB)",
      "_id": "5a1e87a5b549a700121cb934",
      "sub_tiers": [
        {
          "display_price": 1340,
          "price": 700,
          "name": "Adult",
          "_id": "5a1e87a5b549a700121cb936",
          "quantity": 0
        },
        {
          "display_price": 1140,
          "price": 650,
          "name": "Child",
          "_id": "5a1e87a5b549a700121cb935",
          "quantity": 0
        }
      ]
    },
    {
      "tier": "COMBI: SEA LIFE + MADAME TUSSAUDS TICKET",
      "_id": "5a1e87a5b549a700121cb931",
      "sub_tiers": [
        {
          "display_price": 1980,
          "price": 1000,
          "name": "Adult",
          "_id": "5a1e87a5b549a700121cb933",
          "quantity": 0
        },
        {
          "display_price": 1580,
          "price": 850,
          "name": "Child",
          "_id": "5a1e87a5b549a700121cb932",
          "quantity": 0
        }
      ]
    }
  ]
}
```

> Code

```shell
curl 'https://api.staging.takemetour.com/partner/transactions/book' \
-H 'content-type: application/json' \
-H 'x-access-token: 0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3' \
--data-binary '{"name":{"first":"John","last":"Doe"},"email":"john+doe@takemetour.com","mobile":"+66856667571","country":"TH","trip_id":"5a3a0af6c0214700127dadf5","trip_date":"2018-04-11T17:00:00.000Z","multi_tier_quantity":[{"tier":"Admission Fee - Aquarium Only","_id":"5a1e87a5b549a700121cb93d","sub_tiers":[{"display_price":990,"price":600,"name":"Adult","_id":"5a1e87a5b549a700121cb93f","globaltix_ticket_id":"4136","has_availability":true,"globaltix_questions":[{"type":"FREETEXT","question":"Customer name","id":11968}],"globaltix_redeem":{"end":"2018-12-31T23:59:00","start":"2018-01-10T00:00:00"},"globaltix_cost":1500,"quantity":0},{"display_price":790,"price":550,"name":"Child","_id":"5a1e87a5b549a700121cb93e","globaltix_ticket_id":"4136","has_availability":true,"globaltix_questions":[{"type":"FREETEXT","question":"Customer name","id":11968}],"globaltix_redeem":{"end":"2018-12-31T23:59:00","start":"2018-01-10T00:00:00"},"globaltix_cost":1500,"quantity":0}]},{"tier":"COMBO: Aquarium + 4D Movie","_id":"5a1e87a5b549a700121cb93a","sub_tiers":[{"display_price":1090,"price":700,"name":"Adult","_id":"5a1e87a5b549a700121cb93c","globaltix_ticket_id":"4138","has_availability":false,"globaltix_questions":[{"type":"DATE","question":"Service Date","id":11969,"answer":"2018-04-12"},{"type":"FREETEXT","question":"Nationality","id":11970,"answer":"Thailand"},{"options":["Afternoon","Morning"],"type":"OPTION","question":"Select Time","id":11971,"answer":"Afternoon"}],"globaltix_redeem":{"end":"2018-12-31T23:59:00","start":"2018-01-10T00:00:00"},"globaltix_cost":270,"quantity":2},{"display_price":890,"price":650,"name":"Child","_id":"5a1e87a5b549a700121cb93b","globaltix_ticket_id":"4139","has_availability":false,"globaltix_questions":[{"type":"DATE","question":"Service Date","id":11969,"answer":"2018-04-12"},{"type":"FREETEXT","question":"Nationality","id":11970,"answer":"Thailand"},{"options":["Afternoon","Morning"],"type":"OPTION","question":"Select Time","id":11971,"answer":"Afternoon"}],"globaltix_redeem":{"end":"2018-12-31T23:59:00","start":"2018-01-10T00:00:00"},"globaltix_cost":220,"quantity":1}]},{"tier":"Photo Pack : Aquarium + Photo (6\" x 9\")","_id":"5a1e87a5b549a700121cb937","sub_tiers":[{"display_price":1190,"price":800,"name":"Adult","_id":"5a1e87a5b549a700121cb939","quantity":0},{"display_price":990,"price":750,"name":"Child","_id":"5a1e87a5b549a700121cb938","quantity":0}]},{"tier":"Aquarium + Glass Bottom Boat (GBB)","_id":"5a1e87a5b549a700121cb934","sub_tiers":[{"display_price":1340,"price":700,"name":"Adult","_id":"5a1e87a5b549a700121cb936","quantity":0},{"display_price":1140,"price":650,"name":"Child","_id":"5a1e87a5b549a700121cb935","quantity":0}]},{"tier":"COMBI: SEA LIFE + MADAME TUSSAUDS TICKET","_id":"5a1e87a5b549a700121cb931","sub_tiers":[{"display_price":1980,"price":1000,"name":"Adult","_id":"5a1e87a5b549a700121cb933","quantity":0},{"display_price":1580,"price":850,"name":"Child","_id":"5a1e87a5b549a700121cb932","quantity":0}]}]}'
```

```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/transactions/book',
{
  headers: {
    'content-type': 'application/json',
    'x-access-token': '0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
  },
  body: JSON.stringify({
    "name": {
      "first": "John",
      "last": "Doe"
    },
    "email": "john+doe@takemetour.com",
    "mobile": "+66856667571",
    "country": "TH",
    "trip_id": "5a3a0af6c0214700127dadf5",
    "trip_date": "2018-04-11T17:00:00.000Z",
    "multi_tier_quantity": [
      {
        "tier": "Admission Fee - Aquarium Only",
        "_id": "5a1e87a5b549a700121cb93d",
        "sub_tiers": [
          {
            "display_price": 990,
            "price": 600,
            "name": "Adult",
            "_id": "5a1e87a5b549a700121cb93f",
            "globaltix_ticket_id": "4136",
            "has_availability": true,
            "globaltix_questions": [
              {
                "type": "FREETEXT",
                "question": "Customer name",
                "id": 11968
              }
            ],
            "globaltix_redeem": {
              "end": "2018-12-31T23:59:00",
              "start": "2018-01-10T00:00:00"
            },
            "globaltix_cost": 1500,
            "quantity": 0
          },
          {
            "display_price": 790,
            "price": 550,
            "name": "Child",
            "_id": "5a1e87a5b549a700121cb93e",
            "globaltix_ticket_id": "4136",
            "has_availability": true,
            "globaltix_questions": [
              {
                "type": "FREETEXT",
                "question": "Customer name",
                "id": 11968
              }
            ],
            "globaltix_redeem": {
              "end": "2018-12-31T23:59:00",
              "start": "2018-01-10T00:00:00"
            },
            "globaltix_cost": 1500,
            "quantity": 0
          }
        ]
      },
      {
        "tier": "COMBO: Aquarium + 4D Movie",
        "_id": "5a1e87a5b549a700121cb93a",
        "sub_tiers": [
          {
            "display_price": 1090,
            "price": 700,
            "name": "Adult",
            "_id": "5a1e87a5b549a700121cb93c",
            "globaltix_ticket_id": "4138",
            "has_availability": false,
            "globaltix_questions": [
              {
                "type": "DATE",
                "question": "Service Date",
                "id": 11969,
                "answer": "2018-04-12"
              },
              {
                "type": "FREETEXT",
                "question": "Nationality",
                "id": 11970,
                "answer": "Thailand"
              },
              {
                "options": [
                  "Afternoon",
                  "Morning"
                ],
                "type": "OPTION",
                "question": "Select Time",
                "id": 11971,
                "answer": "Afternoon"
              }
            ],
            "globaltix_redeem": {
              "end": "2018-12-31T23:59:00",
              "start": "2018-01-10T00:00:00"
            },
            "globaltix_cost": 270,
            "quantity": 2
          },
          {
            "display_price": 890,
            "price": 650,
            "name": "Child",
            "_id": "5a1e87a5b549a700121cb93b",
            "globaltix_ticket_id": "4139",
            "has_availability": false,
            "globaltix_questions": [
              {
                "type": "DATE",
                "question": "Service Date",
                "id": 11969,
                "answer": "2018-04-12"
              },
              {
                "type": "FREETEXT",
                "question": "Nationality",
                "id": 11970,
                "answer": "Thailand"
              },
              {
                "options": [
                  "Afternoon",
                  "Morning"
                ],
                "type": "OPTION",
                "question": "Select Time",
                "id": 11971,
                "answer": "Afternoon"
              }
            ],
            "globaltix_redeem": {
              "end": "2018-12-31T23:59:00",
              "start": "2018-01-10T00:00:00"
            },
            "globaltix_cost": 220,
            "quantity": 1
          }
        ]
      },
      {
        "tier": "Photo Pack : Aquarium + Photo (6\" x 9\")",
        "_id": "5a1e87a5b549a700121cb937",
        "sub_tiers": [
          {
            "display_price": 1190,
            "price": 800,
            "name": "Adult",
            "_id": "5a1e87a5b549a700121cb939",
            "quantity": 0
          },
          {
            "display_price": 990,
            "price": 750,
            "name": "Child",
            "_id": "5a1e87a5b549a700121cb938",
            "quantity": 0
          }
        ]
      },
      {
        "tier": "Aquarium + Glass Bottom Boat (GBB)",
        "_id": "5a1e87a5b549a700121cb934",
        "sub_tiers": [
          {
            "display_price": 1340,
            "price": 700,
            "name": "Adult",
            "_id": "5a1e87a5b549a700121cb936",
            "quantity": 0
          },
          {
            "display_price": 1140,
            "price": 650,
            "name": "Child",
            "_id": "5a1e87a5b549a700121cb935",
            "quantity": 0
          }
        ]
      },
      {
        "tier": "COMBI: SEA LIFE + MADAME TUSSAUDS TICKET",
        "_id": "5a1e87a5b549a700121cb931",
        "sub_tiers": [
          {
            "display_price": 1980,
            "price": 1000,
            "name": "Adult",
            "_id": "5a1e87a5b549a700121cb933",
            "quantity": 0
          },
          {
            "display_price": 1580,
            "price": 850,
            "name": "Child",
            "_id": "5a1e87a5b549a700121cb932",
            "quantity": 0
          }
        ]
      }
    ]
  }),
  method: 'POST'
});
const data = await response.json();
```

For attraction tickets, specify `multi_tier_quantity` with the same structure as [get attraction tickets pricing](#attraction-tickets-pricing-ticket).

But more than that, attraction ticket also has **questions** that need to be answered. Questions can be found in `globaltix_questions` in the sub tier of tier which you want to booked. (You can get it from get product API)

<pre class="center-column">
{
  "globaltix_questions": [
    {
      "type": "DATE",
      "question": "Service Date",
      "id": 11969
    },
    {
      "type": "FREETEXT",
      "question": "Nationality",
      "id": 11970
    },
    {
      "options": [
        "Afternoon",
        "Morning"
      ],
      "type": "OPTION",
      "question": "Select Time",
      "id": 11971
    }
  ]
}
</pre>

The questions has 3 types that can identify via field `type`

- DATE: Answer must be date with format 'YYYY-MM-DD' (ex. 2018-02-01).
- OPTION: Answer must be one of the value in `options`. From the example, the third question has options "Afternoon" and "Morning" so answer should be one of those.
- FREETEXT: Answer can be a free text.

For example. If you want to book tier **COMBO: Aquarium + 4D Movie** you will see sub tiers of this tier. And inside each sub tier you will see `globaltix_questions`

<pre class="center-column">
{
  "tier": "COMBO: Aquarium + 4D Movie",
  "_id": "5a1e87a5b549a700121cb93a",
  "sub_tiers": [
    {
      "display_price": 1090,
      "price": 700,
      "name": "Adult",
      "_id": "5a1e87a5b549a700121cb93c",
      "globaltix_ticket_id": "4138",
      "has_availability": false,
      "globaltix_questions": [
        {
          "type": "DATE",
          "question": "Service Date",
          "id": 11969
        },
        {
          "type": "FREETEXT",
          "question": "Nationality",
          "id": 11970
        },
        {
          "options": [
            "Afternoon",
            "Morning"
          ],
          "type": "OPTION",
          "question": "Select Time",
          "id": 11971
        }
      ],
      "globaltix_redeem": {
        "end": "2018-12-31T23:59:00",
        "start": "2018-01-10T00:00:00"
      },
      "globaltix_cost": 270,
      "quantity": 2
    },
    {
      "display_price": 890,
      "price": 650,
      "name": "Child",
      "_id": "5a1e87a5b549a700121cb93b",
      "globaltix_ticket_id": "4139",
      "has_availability": false,
      "globaltix_questions": [
        {
          "type": "DATE",
          "question": "Service Date",
          "id": 11969
        },
        {
          "type": "FREETEXT",
          "question": "Nationality",
          "id": 11970
        },
        {
          "options": [
            "Afternoon",
            "Morning"
          ],
          "type": "OPTION",
          "question": "Select Time",
          "id": 11971
        }
      ],
      "globaltix_redeem": {
        "end": "2018-12-31T23:59:00",
        "start": "2018-01-10T00:00:00"
      },
      "globaltix_cost": 220,
      "quantity": 3
    }
  ]
}
</pre>

Next thing you need to do is find all unique questions that unique by id. From the example, all of unique questions are these.

<pre class="center-column">
[
  {
    "type": "DATE",
    "question": "Service Date",
    "id": 11969
  },
  {
    "type": "FREETEXT",
    "question": "Nationality",
    "id": 11970
  },
  {
    "options": [
      "Afternoon",
      "Morning"
    ],
    "type": "OPTION",
    "question": "Select Time",
    "id": 11971
  }
]
</pre>

So you have to answer 3 questions. The field to put answer in is `answer` inside each of question object. But you don't have to put the answer in every sub tier object. Only selected tier is required.

In an example case. We chose to book **COMBO: Aquarium + 4D Movie** tier so the answer must be provide in every sub tier as shown below. (Notice that in other tier the question still there but there is no need to answer. Even it has the same question id)

<pre class="center-column">
{
  "multi_tier_quantity": [
    {
      "tier": "Admission Fee - Aquarium Only",
      "_id": "5a1e87a5b549a700121cb93d",
      "sub_tiers": [
        {
          "display_price": 990,
          "price": 600,
          "name": "Adult",
          "_id": "5a1e87a5b549a700121cb93f",
          "globaltix_ticket_id": "4136",
          "has_availability": true,
          "globaltix_questions": [
            {
              "type": "FREETEXT",
              "question": "Customer name",
              "id": 11968
            }
          ],
          "globaltix_redeem": {
            "end": "2018-12-31T23:59:00",
            "start": "2018-01-10T00:00:00"
          },
          "globaltix_cost": 1500,
          "quantity": 0
        },
        {
          "display_price": 790,
          "price": 550,
          "name": "Child",
          "_id": "5a1e87a5b549a700121cb93e",
          "globaltix_ticket_id": "4136",
          "has_availability": true,
          "globaltix_questions": [
            {
              "type": "FREETEXT",
              "question": "Customer name",
              "id": 11968
            }
          ],
          "globaltix_redeem": {
            "end": "2018-12-31T23:59:00",
            "start": "2018-01-10T00:00:00"
          },
          "globaltix_cost": 1500,
          "quantity": 0
        }
      ]
    },
    {
      "tier": "COMBO: Aquarium + 4D Movie",
      "_id": "5a1e87a5b549a700121cb93a",
      "sub_tiers": [
        {
          "display_price": 1090,
          "price": 700,
          "name": "Adult",
          "_id": "5a1e87a5b549a700121cb93c",
          "globaltix_ticket_id": "4138",
          "has_availability": false,
          "globaltix_questions": [
            {
              "type": "DATE",
              "question": "Service Date",
              "id": 11969,
              "answer": "2018-03-30"
            },
            {
              "type": "FREETEXT",
              "question": "Nationality",
              "id": 11970,
              "answer": "Thai"
            },
            {
              "options": [
                "Afternoon",
                "Morning"
              ],
              "type": "OPTION",
              "question": "Select Time",
              "id": 11971,
              "answer": "Morning"
            }
          ],
          "globaltix_redeem": {
            "end": "2018-12-31T23:59:00",
            "start": "2018-01-10T00:00:00"
          },
          "globaltix_cost": 270,
          "quantity": 2
        },
        {
          "display_price": 890,
          "price": 650,
          "name": "Child",
          "_id": "5a1e87a5b549a700121cb93b",
          "globaltix_ticket_id": "4139",
          "has_availability": false,
          "globaltix_questions": [
            {
              "type": "DATE",
              "question": "Service Date",
              "id": 11969,
              "answer": "2018-03-30"
            },
            {
              "type": "FREETEXT",
              "question": "Nationality",
              "id": 11970,
              "answer": "Thai"
            },
            {
              "options": [
                "Afternoon",
                "Morning"
              ],
              "type": "OPTION",
              "question": "Select Time",
              "id": 11971,
              "answer": "Morning"
            }
          ],
          "globaltix_redeem": {
            "end": "2018-12-31T23:59:00",
            "start": "2018-01-10T00:00:00"
          },
          "globaltix_cost": 220,
          "quantity": 3
        }
      ]
    },
    {
      "tier": "Photo Pack : Aquarium + Photo (6\" x 9\")",
      "_id": "5a1e87a5b549a700121cb937",
      "sub_tiers": [
        {
          "display_price": 1190,
          "price": 800,
          "name": "Adult",
          "_id": "5a1e87a5b549a700121cb939",
          "quantity": 0
        },
        {
          "display_price": 990,
          "price": 750,
          "name": "Child",
          "_id": "5a1e87a5b549a700121cb938",
          "quantity": 0
        }
      ]
    },
    {
      "tier": "Aquarium + Glass Bottom Boat (GBB)",
      "_id": "5a1e87a5b549a700121cb934",
      "sub_tiers": [
        {
          "display_price": 1340,
          "price": 700,
          "name": "Adult",
          "_id": "5a1e87a5b549a700121cb936",
          "quantity": 0
        },
        {
          "display_price": 1140,
          "price": 650,
          "name": "Child",
          "_id": "5a1e87a5b549a700121cb935",
          "quantity": 0
        }
      ]
    },
    {
      "tier": "COMBI: SEA LIFE + MADAME TUSSAUDS TICKET",
      "_id": "5a1e87a5b549a700121cb931",
      "sub_tiers": [
        {
          "display_price": 1980,
          "price": 1000,
          "name": "Adult",
          "_id": "5a1e87a5b549a700121cb933",
          "quantity": 0
        },
        {
          "display_price": 1580,
          "price": 850,
          "name": "Child",
          "_id": "5a1e87a5b549a700121cb932",
          "quantity": 0
        }
      ]
    }
  ]
}
</pre>

And the above object is `multi_tier_quantity` that can be used to book.

### Request body (add from [basic book parameters](#book-product))

Parameter | Type | Description
--------- | ---- | -----------
multi_tier_quantity | **Array of multi tier quantity** | Quantity of ticket with the `answer` added to the sub tier that you chose.

**Note:** `meeting_point` field is not required for `ticket`


### Response
The response is similar to the response of [Book Local Experience Trips](#book-local-experience-trips)

## Book Tangible Products

> Request body to book product type `souvenir`, `meeting_point` is required by default with format `Hotel name: {hotelName}, room: {hotelRoom}`. (If product tags don't contain tag `not_require_pickup_location` then `meeting_point` field can be omit.)

```json
{
  "quantity": 1,
  "trip_id": "5a39ee73fdeeab0012005d50",
  "meeting_point": "Hotel name: Florida Hotel, room: 404",
  "name": {
    "first": "John",
    "last": "Doe"
  },
  "email": "john+doe@takemetour.com",
  "trip_date": "2018-03-30T17:00:00.000Z",
  "mobile": "+66856667571",
  "country": "TH"
}
```

> Code

```shell
curl 'https://api.staging.takemetour.com/partner/book' \
-H 'content-type: application/json' \
-H 'x-access-token: 0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3' \
-X POST \
--data-binary '{"quantity":1,"trip_id":"5a39ee73fdeeab0012005d50","meeting_point":"Hotel name: Florida Hotel, room: 404","name":{"first":"John","last":"Doe"},"email":"john+doe@takemetour.com","trip_date":"2018-03-30T17:00:00.000Z","mobile":"+66856667571","country":"TH"}'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/book',
{
  headers: {
    'content-type': 'application/json',
    'x-access-token': '0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
  },
  body: JSON.stringify({
    "quantity": 5,
    "trip_id": "5a3782ebbec78a00117fc04b",
    "meeting_point": "Hotel name: Florida Hotel, room: 404",
    "name": {
      "first": "John",
      "last": "Doe"
    },
    "email": "john+doe@takemetour.com",
    "trip_date": "2018-03-29T17:00:00.000Z",
    "mobile": "+66856667571",
    "country": "TH"
  }),
  method: 'POST',
});
const data = await response.json();
```

> If product has tag `match_passport_name`, customer first name must have name title

```json
{
  "quantity": 5,
  "trip_id": "5a3782ebbec78a00117fc04b",
  "meeting_point": "Hotel name: Florida Hotel, room: 404",
  "name": {
    "first": "Mr.John",
    "last": "Doe"
  },
  "email": "john+doe@takemetour.com",
  "trip_date": "2018-03-29T17:00:00.000Z",
  "mobile": "+66856667571",
  "country": "TH"
}
```

> Code

```shell
curl 'https://api.staging.takemetour.com/partner/book' \
-H 'content-type: application/json' \
-H 'x-access-token: 0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
--data-binary: '{"quantity":5,"trip_id":"5a3782ebbec78a00117fc04b","meeting_point":"Hotel name: Florida Hotel, room: 404","name":{"first":"Mr.John","last":"Doe"},"email":"john+doe@takemetour.com","trip_date":"2018-03-29T17:00:00.000Z","mobile":"+66856667571","country":"TH"}'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/book',
{
  headers: {
    'content-type': 'application/json',
    'x-access-token': '0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
  },
  body: JSON.stringify({
    "quantity": 5,
    "trip_id": "5a3782ebbec78a00117fc04b",
    "meeting_point": "Hotel name: Florida Hotel, room: 404",
    "name": {
      "first": "Mr.John",
      "last": "Doe"
    },
    "email": "john+doe@takemetour.com",
    "trip_date": "2018-03-29T17:00:00.000Z",
    "mobile": "+66856667571",
    "country": "TH"
  }),
  method: 'POST',
});
const data = await response.json();
```

For tangible product, `quantity` must be provided. And it also has some condition which you need some field to add for.

- If product doesn't contain tag `not_require_pickup_location`. You must provide delivery location which is the customer's hotel (for now we will deliver the product to the customer's hotel) in the format **Hotel name: {hotelName}, room: {hotelRoom}** to the `meeting_point` field.

<pre class="center-column">
{
  "quantity": 1,
  "trip_id": "5a39ee73fdeeab0012005d50",
  "name": {
    "first": "John",
    "last": "Doe"
  },
  "email": "john+doe@takemetour.com",
  "trip_date": "2018-03-30T17:00:00.000Z",
  "mobile": "+66856667571",
  "country": "TH",
  "meeting_point": "Hotel name: Dusti Thani, room: 404"
}
</pre>

- If product contain tag `not_require_pickup_location`. Delivery location doesn't need. `meeting_point` field can be omit

- If product contain tag `match_passport_name`. You must specific name title (Mr. / Mrs. / Miss) alongside with `name.first` in request body object.

<pre class="center-column">
{
  "quantity": 1,
  "trip_id": "5a39ee73fdeeab0012005d50",
  "name": {
    "first": "Mr.John",
    "last": "Doe"
  },
  "email": "john+doe@takemetour.com",
  "trip_date": "2018-03-30T17:00:00.000Z",
  "mobile": "+66856667571",
  "country": "TH",
  "meeting_point": "Hotel name: Dusti Thani, room: 404"
}
</pre>

### Request body (add from [basic book parameters](#book-product))

Parameter | Type | Description
--------- | ---- | -----------
quantity | **Number (max to 12)** | Quantity of product to be buy
meeting_point | **String (Max length: 255)** | If product `tags` doesn't contains `not_require_pickup_location` meeting_point is delivery address (hotel only).

### Response
The response is similar to the response of [Book Local Experience Trips](#book-local-experience-trips)

## Book Car Rental Product

For car rental product, there is multiple type of this product which are

- **Ferry Transfer:** Product will have `is_ferry_transfer` flag as `true` alongside with `ferry_options`
- **Airport to Hotel Transfer:** Product will have `is_ferry_transfer` flag as `false` and `fixed_quantity` equal to `1`

### Book Ferry Transfer

> Code

```shell
curl 'https://api.staging.takemetour.com/partner/book' \
-H 'content-type: application/json' \
-H 'x-access-token: 0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
--data-binary: '{"quantity": 1,"trip_id": "5c9862237511dda74df329de","name": {"first": "John","last": "Doe"},"email": "john+doe@takemetour.com","trip_date": "2019-03-29T17:00:00.000Z","mobile": "+66856667571","country": "TH","meeting_point": "Hotel Pickup: 12:45 - 13:00 at Sample Hotel (Ferry Time: 13:00)"}'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/book',
{
  headers: {
    'content-type': 'application/json',
    'x-access-token': '0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
  },
  body: JSON.stringify({
    "quantity": 1,
    "trip_id": "5c9862237511dda74df329de",
    "name": {
      "first": "John",
      "last": "Doe"
    },
    "email": "john+doe@takemetour.com",
    "trip_date": "2019-03-29T17:00:00.000Z",
    "mobile": "+66856667571",
    "country": "TH",
    "meeting_point": "Hotel Pickup: 12:45 - 13:00 at Sample Hotel (Ferry Time: 13:00)"
  }),
  method: 'POST',
});
const data = await response.json();
```

Ferry Transfer has `ferry_options` with structure like these

<pre class="center-column">
"ferry_options": {
  "options": [
    {
      "time": "8:30",
      "_id": "5bb44d6e9c6632001410eb4e",
      "sub_options": [
        "07:00 - 07:15 Patong, Kata, Karon, Nai Harn, Rawai",
        "08:00 - 08:15 Phuket Town"
      ]
    },
    {
      "time": "11:00",
      "_id": "5bb44d6e9c6632001410eb4d",
      "sub_options": [
        "09:15 - 09:30 Patong, Kata, Karon",
        "09:45 - 10:00 Phuket Town"
      ]
    },
    {
      "time": "13:00",
      "_id": "5bb44d6e9c6632001410eb4c",
      "sub_options": [
        "12:00 - 12:15 Patong, Kata, Karon, Nai Harn, Rawai",
        "12:45 - 13:00 Phuket Town"
      ]
    },
    {
      "time": "15:00",
      "_id": "5bb44d6e9c6632001410eb4b",
      "sub_options": [
        "13:15 - 13:30 Patong, Kata, Karon",
        "13:45 - 14:00 Phuket Town"
      ]
    }
  ],
  "label": "Ferry Time"
}
</pre>

Inside `options` there is an array to describe a ferry schedule which can represent as table to make it easier to understand.

Ferry Time | Pickup Time
---------- | -----------
8:30 | 07:00 - 07:15 Patong, Kata, Karon, Nai Harn, Rawai
 | 08:00 - 08:15 Phuket Town
11: 00 | 09:15 - 09:30 Patong, Kata, Karon
 | 09:45 - 10:00 Phuket Town
13:00 | 12:00 - 12:15 Patong, Kata, Karon, Nai Harn, Rawai
 | 12:45 - 13:00 Phuket Town
15:00 | 13:15 - 13:30 Patong, Kata, Karon
 | 13:45 - 14:00 Phuket Town

- `time` in the `options` represent ferry time. Ferry time is a time that ferry leave the pier.
- `sub_options` for each option is the time that driver will pickup at hotel.
- Example. If you choose 13:00 it's mean that you should to take ferry transfer at 13:00. And you need to choose which time to make hotel pickup to the ferry. In this case you have to choice "12:00 - 12:15 Patong, Kata, Karon, Nai Harn, Rawai" or "12:45 - 13:00 Phuket Town".
- You must provide these option into string format **Hotel Pickup: {selected sub option} at {hotel name} ({ferry_options.label}: {selected time})** to the `meeting_point` field.
- From above example. If you choose ferry time at 13:00 and pickup time 12:45 - 13:00 Phuket Town. Formatted string is **"Hotel Pickup: 12:45 - 13:00 at Sample Hotel (Ferry Time: 13:00)"**

Below JSON is an example request to book ferry transfer.

<pre class="center-column">
{
  "quantity": 1,
  "trip_id": "5c9862237511dda74df329de",
  "name": {
    "first": "John",
    "last": "Doe"
  },
  "email": "john+doe@takemetour.com",
  "trip_date": "2019-03-29T17:00:00.000Z",
  "mobile": "+66856667571",
  "country": "TH",
  "meeting_point": "Hotel Pickup: 12:45 - 13:00 at Sample Hotel (Ferry Time: 13:00)"
}
</pre>

### Request body (add from [basic book parameters](#book-product))

Parameter | Type | Description
--------- | ---- | -----------
meeting_point | **String (Max length: 255)** | String formatted in **Hotel Pickup: {selected sub option} at {hotel name} ({ferry_options.label}: {selected time})**

### Response
The response is similar to the response of [Book Local Experience Trips](#book-local-experience-trips)

### Book Airport to Hotel Transfer

> Code

```shell
curl 'https://api.staging.takemetour.com/partner/book' \
-H 'content-type: application/json' \
-H 'x-access-token: 0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
--data-binary: '{"quantity": 1,"trip_id": "59edbafc6892f400105fe9ae","name": {"first": "John","last": "Doe"},"email": "john+doe@takemetour.com","trip_date": "2019-03-29T17:00:00.000Z","mobile": "+66856667571","country": "TH","meeting_point": "Airport: DMK, Flight: TG154, Hotel name: Baan 2459, pickup time: 00:45"}'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/book',
{
  headers: {
    'content-type': 'application/json',
    'x-access-token': '0TKOeCA5sLimUiGYcIdWOb9NoiYEgJJ3'
  },
  body: JSON.stringify({
    "quantity": 1,
    "trip_id": "59edbafc6892f400105fe9ae",
    "name": {
      "first": "John",
      "last": "Doe"
    },
    "email": "john+doe@takemetour.com",
    "trip_date": "2019-03-29T17:00:00.000Z",
    "mobile": "+66856667571",
    "country": "TH",
    "meeting_point": "Airport: DMK, Flight: TG154, Hotel name: Baan 2459, pickup time: 00:45"
  }),
  method: 'POST',
});
const data = await response.json();
```

This type is much more simple. Additional details you need are

- Flight Number
- Pickup Time (HH:mm 24-hour format)
- Pickup Airport (Only DMK and BKK)
- Drop off hotel

You must provide these option into string format **Airport: {airport}, Flight: {flight nunber}, Hotel name: {hotel name}, pickup time: {pickup time}** to the `meeting_point` field.


Below JSON is an example request to book airport transfer to hotel

<pre class="center-column">
{
  "quantity": 1,
  "trip_id": "59edbafc6892f400105fe9ae",
  "name": {
    "first": "John",
    "last": "Doe"
  },
  "email": "john+doe@takemetour.com",
  "trip_date": "2019-03-29T17:00:00.000Z",
  "mobile": "+66856667571",
  "country": "TH",
  "meeting_point": "Airport: DMK, Flight: TG154, Hotel name: Baan 2459, pickup time: 00:45"
}
</pre>

### Request body (add from [basic book parameters](#book-product))

Parameter | Type | Description
--------- | ---- | -----------
meeting_point | **String (Max length: 255)** | String formatted in **Airport: {airport}, Flight: {flight nunber}, Hotel name: {hotel name}, pickup time: {pickup time}**

### Response
The response is similar to the response of [Book Local Experience Trips](#book-local-experience-trips)
