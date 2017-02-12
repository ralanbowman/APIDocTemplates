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

The value you need is the `access_token` which is unique to you. In your API requests this will be a header called the **Bearer** token and will be sent as `"Authorization: Bearer XXXX"`.

--- 

## Step 1. Add a product to a cart

This is the API request that is sent when when a customer adds a product to their shopping cart. 

### Method and Endpoint

`POST /v2/carts/{reference}/items`

### Sample Request

```bash
curl -X POST https://api.moltin.com/v2/carts/{reference}/items \
	-H "Authorization: Bearer XXXX" \
	-d "type: cart_item" \  
	-d "id: 12345" \
	-d "quanity: 1"
```

| Parameter     | Description     |  Type    |  Required    |   Notes   |
|-------------|-----------------|----------|--------------|-----------|
|  **Authorization**  |    Access token  |  Bearer token   |  Required  |      |
|  **type**  |  Type of item to add   |  string   |  Required       | Valid values are `cart_item` or `custom_item`    |
|  **id**  |  Product ID  |  string   |  Required   |  Unique product ID    |
|  **quantity**  | Product count   |  integer   |  Required       |  &nbsp;   |



### Sample Response

START HERE, waiting on reply from Moltin

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


## Step 2. Retrieve cart contents

After the customer adds products to the cart, you can then retrieve the cart contents to start the checkout process. 

### Method and Endpoint

`GET /v2/carts/{reference}/items`

### Sample Request

```bash
curl -X GET https://api.moltin.com/v2/carts/{reference}/items \
	-H "Authorization: Bearer XXXX" \
	-H "X-MOLTIN-CURRECY: USD" \  
	-H "X-MOLTIN-LOCALE: US" 
```

| Parameter   | Description     | Type     | Required     | Notes     |
|-------------|-----------------|----------|--------------|-----------|
|  **Authorization**  |    Access token   |  Bearer token   |  Required  |      |
|  **X-MOLTIN-CURRENCY**  |  Currency set by customer  |  string   |  Optional | Valid values are: `EUR`, `GBP`, and `USD`  |
|  **X-MOLTIN-LOCALE**  | Location set by customer   |  string   |  Optional   | &nbsp;     |



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

Once you have retrieved the cart contents, you can convert them into an order so they can be purchased. 

### Method and Endpoint

`POST /v2/carts/{reference}/checkout`

### Sample Request

```bash
curl -X POST https://api.moltin.com/v2/carts/{reference}/checkout \
  -g \  
  -H "Authorization: Bearer XXXX" \
  -d "customer[name]=John Doe" \  
  -d "customer[email]=jdoe@example.com" \  
  -d "billing_address[first_name]=John" \  
  -d "billing_address[last_name]=Doe" \  
  -d "billing_address[company_name]=JD Company" \  
  -d "billing_address[line_1]=123 Any Way" \ 
  -d "billing_address[line_2]=Anytown" \  
  -d "billing_address[postcode]=12345" \ 
  -d "billing_address[county]=Any county" \  
  -d "billing_address[country]=My country" \  
  -d "shipping_address[first_name]=John" \  
  -d "shipping_address[last_name]=Doe" \  
  -d "shipping_address[company_name]=JD Company" \  
  -d "shipping_address[line_1]=123 Any Way" \ 
  -d "shipping_address[line_2]=Anytown" \  
  -d "shipping_address[postcode]=12345" \ 
  -d "shipping_address[county]=Any county" \  
  -d "shipping_address[country]=My country" \  
  -d "shipping_address[instructions]="Leave at door" 
```

| Parameter   | Description     | Type     | Required     | Notes     |
|-------------|-----------------|----------|--------------|-----------|
|  **Authorization**  | Access token  | Bearer token   |  Required  |      |
|  **data**  |    Cart order data |  JSON object   |  Required       | The cart data that will be converted into the order object  |
|  **customer**  | Customer information   |  JSON object   |  Required  |  |
|  **name**  | Customer name |  string   |  Required   | First and last name  |
|  **email**  |  Email address |  string   |  Required  | Must be a properly formatted email address |
|  **billing_address**  | Address for billing  |  JSON object |  Required |     |
|  **first_name**  |  Customer first name  |  string  |  Required  |      |
|  **last_name**  |    Customer last name |  string   |  Required | |
|  **company_name**  |  Name of company  |  string   |  Optional  | Company name only supplied if this is a business order |
|  **line_1**  |  Street address   |  string   |  Required  | |
|  **line_2**  |  Street address  |  string   |  Optional | Could be used for apartment number  |
|  **postcode**  | Postal code    |  string   |  Required  | Postal Code or ZIP Code (US) |
|  **county**  |  Administrative district  |  string   |  Required  | Some locales may use "parish"  |
|  **country**  |  Country   |  string   |  Required   | |
|  **shipping_address**  |  Address for shipping  |  JSON object  |  Required | Shipping address may differ from billing address |
|  **first_name**  |  Customer first name  |  string  |  Required  |      |
|  **last_name**  |    Customer last name |  string   |  Required | |
|  **company_name**  |  Name of company  |  string   |  Optional  | Company name only supplied if this is a business order |
|  **line_1**  |  Street address   |  string   |  Required  | |
|  **line_2**  |  Street address  |  string   |  Optional | Could be used for apartment number  |
|  **postcode**  | Postal code    |  string   |  Required  | Postal Code or ZIP Code (US) |
|  **county**  |  Administrative district  |  string   |  Required  | Some locales may use "parish"  |
|  **country**  |  Country   |  string   |  Required   | |
|  **instructions**  |  Shipping instructions |  string   |  Optional | Special instructions for shipper |

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

### Method and Endpoint

`GET /v2/carts/{reference}/items`

### Sample Request

```bash
curl -X GET https://api.moltin.com/v2/carts/{reference}/items \
	-H "Authorization: Bearer XXXX" \
	-H "X-MOLTIN-CURRECY: USD" \  
	-H "X-MOLTIN-LOCALE: US" 
```

| Parameter   | Description     | Type     | Required     | Notes     |
|-------------|-----------------|----------|--------------|-----------|
|  **Authorization**  |    Access token   |  Bearer token   |  Required  |      |
|  **X-MOLTIN-CURRENCY**  |  Currency set by customer  |  string   |  Optional | Valid values are: `EUR`, `GPB`, and `USD`  |
|  **X-MOLTIN-LOCALE**  | Location set by customer   |  string   |  Optional   | &nbsp;     |


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

