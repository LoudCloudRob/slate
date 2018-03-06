---
title: API Reference

language_tabs:
  - shell: cURL

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://cannactrl.com'></a>

<!-- includes: -->
  <!-- - errors -->

search: true
---

# Intro

Welcome to the CannaCtrl API! You can use our API to access Dispensary API endpoints, which can get information on various menu items, store information, and real time inventory in our database.

All requests are made using HTTP requests. You can view code examples in the dark area to the right.


# Authentication

> username and password must be included in every request

```shell
curl "https://us-central1-cannactrl-menu.cloudfunctions.net/menu"
  -H "Content-Type: application/json"
  -X POST {"username": 'myUserName', "password": 'myPassword'}
```

> Make sure to replace `myUserName` and `myPassword` with the credentials we provide.

CannCtrl uses username and password to allow access to the API. You can register a new CannaCtrl API credentials by emailing info@CannaCtrl.com

CannCtrl expects for the username and password to be included in all API requests to the server in the body that looks like the following:

`username: myUserName`,
`password: myPassword`

<aside class="notice">
You must replace <code>myUserName</code> & <code>myPassword</code> with your credentials.
</aside>

You must obtain an API token from the collectives you choose to request information from

# Menu Items

## Get All Menu Items

```shell
curl "https://us-central1-cannactrl-menu.cloudfunctions.net/menu"
  -X POST { "collective_token": 'collective_token', "username": 'myUserName', "password": 'myPassword'}
```
> Make sure to obtain a `collective_token` from each dispensary
> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Brownie Bites",
    "brand_name": "Milf 'n Cookies",
    "product_type": "Edible",
    "product_subtype": "Brownies",
    "description": "Spoil yourself with this sinful blend of silky, rich chocolate.",
    "product_prices" : [{"unit": "unit", "amount": 1, "price": 10.00}]
  },
  {
    "id": 2,
    "name": "Purple Punch",
    "brand_name": "Jungle Boys",
    "product_type": "Flower",
    "product_subtype": "Indica",
    "description": "Spoil yourself with this sinful blend of silky, rich chocolate.",
    "product_prices" : [
        {"unit": "gram", "amount": 1, "price": 10.00},
        {"unit": "ounce", "amount": 0.125, "price": 50.00},
        {"unit": "ounce", "amount": 0.5, "price": 100.00},
        {"unit": "ounce", "amount": 1, "price": 180.00}
        ]
  }
]
```

This endpoint retrieves all Menu Items.

### HTTP Request

`POST https://us-central1-cannactrl-menu.cloudfunctions.net/menu`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
collective_token | String | Must be obtained from each dispensary.
active | Bool | Automatically set to true, the result only includes active menu items

### Response

Parameter | Type | Description
--------- | ------- | -----------
product_type | String | Flower, Edible, Concentrate, Tincture, Drink, Wax, Preroll, Gear
product_subtype | String | i.e. Indica, Sativa, Hybrid, Brownies, Indica Hybrid (Indica dominant hybrid)
active | Bool | Default set to true, the result will only include active menu items
product_prices | [Array] | An array of Prices. See Product Prices Schema below

### Product Prices

Parameter | Type | Description
--------- | ------- | -----------
unit | String | gram, ounce, or unit(each)
amount | Number | quantity of the units (i.e. 0.125 ounce = 1/8)
price | Number | price of product
