# Checkout flow 

## Quickstart 

The checkout flow adds products to a customer’s shopping cart, retrieves the cart contents, and moves them through the order and payment process. The process consists of four steps:  

1. Add a product to a cart   
2. Get cart contents   
3. Convert cart to an order  
4. Process payment  


This Quickstart will walk you through the API requests needed to complete the checkout process.

---

## Before you begin - authentication 

In order to send API requests, you will need a bearer token that is generated from your store keys, which are found in the [Accounts Management Dashboard](https://accounts.moltin.com/ "Accounts Management Dashboard"). You will need your **Client ID** and your **Client Secret**. 

### Bearer token request

To retrieve the bearer token, make a `POST` request using your unique `client_id` (Client ID) and `client_secret` (Client Secret), with a `grant_type` of `client_credentials`. 

```bash
curl -X POST https://api.moltin.com/oauth/access_token \ 
  -d "client_id=XXX" \
  -d "client_secret=XXX" \
  -d "grant_type=client_credentials"
  ```

### Response 

```json
{
  "expires": 246810,
  "identifier": "client_credentials",
  "expires_in": 3600,
  "access_token": "XXXXX",
  "token_type": "Bearer"
}
```

The value you need is the `access_token` which is unique to you. In your API requests this will be called the **Bearer** token. 

--- 

## Step 1. Add a product to a cart

Add a selected product into the customer's shopping cart 

### Method and Endpoint

`POST /v2/carts/{reference}/items`

### Sample Request

```
curl -X POST https://api.moltin.com/v2/carts/{reference}/items \
	-H "Authorization: Bearer XXXX" \
	-d "type: cart_item" \  
	-d "id: 12345" \
	-d "quanity: 1"
```

| Parameter     | Description     |  Type    |  Required    |   Notes   |
|-------------|-----------------|----------|--------------|-----------|
|  **Authorization**  |    Authorization token        |  Bearer token   |  Required  |      |
|  **type**  |  Cart item   |  string   |  Required       |  `cart_item` or `custom_item`    |
|  **id**  |  Product ID  |  string   |  Required   |  Unique product ID    |
|  **quantity**  | Product count   |  integer   |  Required       |  &nbsp;   |



### Sample Response

{
  "query": {
    "tool": "tool",
    "domain": "example.com"
  },
    "response": {
      "parameter": "parameter response"
  }
}



| Element     |   Description   |   Type   |   Notes   |
|-------------|-----------------|----------|-----------|
|  **Value**  |    Value        |  Value   |  Value    |
|  **Value**  |    Value        |  Value   |  Value    |
|  **Value**  |    Value        |  Value   |  Value    |
|  **Value**  |    Value        |  Value   |  Value    |


## Step 2. Get cart contents
(what the endpoint actually does, like "Retrieve all user names")

Description (a description, such as "Retrieves all user names available in customer account")

### Endpoint

`resource/endpoint/{parameter}`

### Method and URL

`METHOD https://api.example.com/resource/endpoint/{parameter}`


### Query parameters

| Parameter   | Description     | Type     | Required     | Notes     |
|-------------|-----------------|----------|--------------|-----------|
|  **Value**  |    Value        |  Value   |  Value       | Value     |
|  **Value**  |    Value        |  Value   |  Value       | Value     |
|  **Value**  |    Value        |  Value   |  Value       | Value     |


### Sample Request

`METHOD https://api.example.com/resource/endpoint/{parameter}`

`curl --get --include 'https://api.example.com/resource/endpoint/parameter`


### Sample Response

{
  "query": {
    "tool": "tool",
    "domain": "example.com"
  },
    "response": {
      "parameter": "parameter response"
  }
}



| Element     |   Description   |   Type   |   Notes   |
|-------------|-----------------|----------|-----------|
|  **Value**  |    Value        |  Value   |  Value    |
|  **Value**  |    Value        |  Value   |  Value    |
|  **Value**  |    Value        |  Value   |  Value    |
|  **Value**  |    Value        |  Value   |  Value    |

## Step 3. Convert cart to an order 
(what the endpoint actually does, like "Retrieve all user names")

Description (a description, such as "Retrieves all user names available in customer account")

### Endpoint

`resource/endpoint/{parameter}`

### Method and URL

`METHOD https://api.example.com/resource/endpoint/{parameter}`


### Query parameters

| Parameter   | Description     | Type     | Required     | Notes     |
|-------------|-----------------|----------|--------------|-----------|
|  **Value**  |    Value        |  Value   |  Value       | Value     |
|  **Value**  |    Value        |  Value   |  Value       | Value     |
|  **Value**  |    Value        |  Value   |  Value       | Value     |


### Sample Request

`METHOD https://api.example.com/resource/endpoint/{parameter}`

`curl --get --include 'https://api.example.com/resource/endpoint/parameter`


### Sample Response

{
  "query": {
    "tool": "tool",
    "domain": "example.com"
  },
    "response": {
      "parameter": "parameter response"
  }
}



| Element     |   Description   |   Type   |   Notes   |
|-------------|-----------------|----------|-----------|
|  **Value**  |    Value        |  Value   |  Value    |
|  **Value**  |    Value        |  Value   |  Value    |
|  **Value**  |    Value        |  Value   |  Value    |
|  **Value**  |    Value        |  Value   |  Value    |


## Step 4. Process payment
(what the endpoint actually does, like "Retrieve all user names")

Description (a description, such as "Retrieves all user names available in customer account")

### Endpoint

`resource/endpoint/{parameter}`

### Method and URL

`METHOD https://api.example.com/resource/endpoint/{parameter}`


### Query parameters

| Parameter   | Description     | Type     | Required     | Notes     |
|-------------|-----------------|----------|--------------|-----------|
|  **Value**  |    Value        |  Value   |  Value       | Value     |
|  **Value**  |    Value        |  Value   |  Value       | Value     |
|  **Value**  |    Value        |  Value   |  Value       | Value     |


### Sample Request

`METHOD https://api.example.com/resource/endpoint/{parameter}`

`curl --get --include 'https://api.example.com/resource/endpoint/parameter`


### Sample Response

{
  "query": {
    "tool": "tool",
    "domain": "example.com"
  },
    "response": {
      "parameter": "parameter response"
  }
}



| Element     |   Description   |   Type   |   Notes   |
|-------------|-----------------|----------|-----------|
|  **Value**  |    Value        |  Value   |  Value    |
|  **Value**  |    Value        |  Value   |  Value    |
|  **Value**  |    Value        |  Value   |  Value    |
|  **Value**  |    Value        |  Value   |  Value    |

---

### Status Codes and Errors

|     Code    | Description     |  Notes       |
|-------------|-----------------|--------------|
|  **Value**  |    Value        |  Value       |
|  **Value**  |    Value        |  Value       |
|  **Value**  |    Value        |  Value       |
