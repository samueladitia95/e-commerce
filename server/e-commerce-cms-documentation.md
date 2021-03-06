# E-Commerce CMS

E-Commerce CMS is an application to manage e-commerce inventory. This app has :

- RESTful endpoint for asset's CRUD operation
- JSON formatted response

&nbsp;

## RESTful endpoints

### POST /users/login

> Login to application

_Request Header_

```json
{
	"Content-Type": "application/json"
}
```

_Request Body_

```json
{
	"email": "<user email>",
	"password": "<user password>"
}
```

_Response (201)_

```json
{
	"access_token": "<access token generated by server>",
	"display_name": "<user display name>"
}
```

_Response (400 - Bad Request)_

```json
{
	"message": "Must Enter Email and Password"
}
```

_Response (401 - Unauthorized)_

```json
{
	"message": "Wrong Email/Password"
}
```

_Response (500 - Internal Server Error)_

```json
{
	"message": "<internal error messages>"
}
```

### POST /users/login

> Register a User to application

_Request Header_

```json
{
	"Content-Type": "application/json"
}
```

_Request Body_

```json
{
	"email": "<user email>",
	"password": "<user password>",
	"display_name": "<user display name>"
}
```

_Response (201)_

```json
{
  "id": <id generated by server>,
	"email": "<user email>",
  "display_name": "<user display name>",
  "img_url": "<random profile picture>"
}
```

_Response (400 - Bad Request)_

```json
{
	"message": "<validation / contraints error>"
}
```

_Response (500 - Internal Server Error)_

```json
{
	"message": "<internal error messages>"
}
```

### GET /products

> Get all products

_Request Header_

```json
{
	"access_token": "<user access token>"
}
```

_Request Body_

```json
Not Needed
```

_Response (200)_

```json
[
  {
    "id": <product id>,
    "name": "<product name>",
    "img_url": "<product image link>",
    "price": <product price>,
    "stock": <product stock>,
    "category_name": "<product category>"
  },
  {
    "id": <product id>,
    "name": "<product name>",
    "img_url": "<product image link>",
    "price": <product price>,
    "stock": <product stock>,
    "category_name": "<product category>"
  }
]
```

_Response (401 - Unauthorized)_

```json
{
	"message": "<Authentication message>"
}
```

_Response (500 - Internal Server Error)_

```json
{
	"message": "<internal error messages>"
}
```

### POST /products

> Enter a new Product

_Request Header_

```json
{
	"access_token": "<user access token>",
	"Content-Type": "application/json"
}
```

_Request Body_

```json
{
  "name": "<product name>",
  "img_url": "<product image link>",
  "price": <product price>,
  "stock": <product stock>,
  "CategoryId": "<product category id>"
}
```

_Response (200)_

```json
{
  "id": <product id>,
  "name": "<product name>",
}

```

_Response (401 - Unauthorized)_

```json
{
	"message": "<Authentication message>"
}
```

_Response (400 - Bad Request)_

```json
{
	"message": "<Bad Request message>"
}
```

_Response (500 - Internal Server Error)_

```json
{
	"message": "<internal error messages>"
}
```

### PUT /products/:id

> Edit product data

_Request Header_

```json
{
	"access_token": "<user access token>",
	"Content-Type": "application/json"
}
```

_Request Body_

```json
{
  "name": "<product name>",
  "img_url": "<product image link>",
  "price": <product price>,
  "stock": <product stock>,
  "CategoryId": "<product category id>"
}
```

_Response (200)_

```json
{
    "id": <product id>,
    "name": "<new product name>",
    "img_url": "<new product image link>",
    "price": <new product price>,
    "stock": <new product stock>,
    "category_name": "<new product category>"
}

```

_Response (401 - Unauthorized)_

```json
{
	"message": "<Authentication message>"
}
```

_Response (400 - Bad Request)_

```json
{
	"message": "<Bad Request message>"
}
```

_Response (404 - Not Found)_

```json
{
	"message": "<Not Found message>"
}
```

_Response (500 - Internal Server Error)_

```json
{
	"message": "<internal error messages>"
}
```

### DELETE /products/:id

> Delete a product

_Request Header_

```json
{
	"access_token": "<user access token>"
}
```

_Request Body_

```json
Not Needed
```

_Response (200)_

```json
{
	"message": "Product is sucessfully deleted"
}
```

_Response (401 - Unauthorized)_

```json
{
	"message": "<Authentication message>"
}
```

_Response (404 - Not Found)_

```json
{
	"message": "<Not Found message>"
}
```

_Response (500 - Internal Server Error)_

```json
{
	"message": "<internal error messages>"
}
```

### GET /cart

> Get all Product in a cart that still processed

_Request Header_

```json
{
	"access_token": "<user access token>"
}
```

_Request Body_

```json
Not Needed
```

_Response (200)_

```json
[
  {
    "id": <cart id>,
    "UserId": "<User ID>",
    "status": "processing",
    "quantity": <cart order quantity>,
    "Product": {
      "id": <product id>,
      "name": "<product name>",
      "img_url": "<product image link>",
      "price": <product price>,
      "stock": <product stock>,
      "CategoryID": <product category>,
      "createdAt": "<time cart created>",
      "updatedAt": "<time cart updated>",
      "Category": {
        "id": <category id>,
        "name": "<category name>",
        "createdAt": "<time category created>",
        "updatedAt": "<time category updated>",
      }
    },
  },
  {
    "id": <cart id>,
    "UserId": "<User ID>",
    "status": "processing",
    "quantity": <cart order quantity>,
    "Product": {
      "id": <product id>,
      "name": "<product name>",
      "img_url": "<product image link>",
      "price": <product price>,
      "stock": <product stock>,
      "CategoryID": <product category>,
      "createdAt": "<time cart created>",
      "updatedAt": "<time cart updated>",
      "Category": {
        "id": <category id>,
        "name": "<category name>",
        "createdAt": "<time category created>",
        "updatedAt": "<time category updated>",
      }
    },
  },
]
```

_Response (401 - Unauthorized)_

```json
{
	"message": "<Authentication message>"
}
```

_Response (500 - Internal Server Error)_

```json
{
	"message": "<internal error messages>"
}
```

### POST /cart

> Add Product to Cart

_Request Header_

```json
{
	"access_token": "<user access token>",
	"Content-Type": "application/json"
}
```

_Request Body_

```json
{
  "ProductId": <Product id that added to cart>,
	"quantity": <Product quantity>
}
```

_Response (200)_

```json
{
  "id": <Cart ID>,
  "UserId": <User ID>,
  "ProductId": <Product ID>,
  "status": "<cart status>",
  "quantity": <Product quantity in cart>
}

```

_Response (401 - Unauthorized)_

```json
{
	"message": "<Authentication message>"
}
```

_Response (400 - Bad Request)_

```json
{
	"message": "<Bad Request message>"
}
```

_Response (500 - Internal Server Error)_

```json
{
	"message": "<internal error messages>"
}
```

### PATCH /cart/:id

> Update product quantity in a cart

_Request Header_

```json
{
	"access_token": "<user access token>",
	"Content-Type": "application/json"
}
```

_Request Body_

```json
{
  "quantity": <Product quantity in cart>
}
```

_Response (200)_

```json
{
	"message": "Product quantity updated"
}
```

_Response (401 - Unauthorized)_

```json
{
	"message": "<Authentication message>"
}
```

_Response (400 - Bad Request)_

```json
{
	"message": "<Bad Request message>"
}
```

_Response (404 - Not Found)_

```json
{
	"message": "<Not Found message>"
}
```

_Response (500 - Internal Server Error)_

```json
{
	"message": "<internal error messages>"
}
```

### DELETE /cart/:id

> Delete order in cart

_Request Header_

```json
{
	"access_token": "<user access token>"
}
```

_Request Body_

```json
Not Needed
```

_Response (200)_

```json
{
	"message": "Delete Order successful"
}
```

_Response (401 - Unauthorized)_

```json
{
	"message": "<Authentication message>"
}
```

_Response (404 - Not Found)_

```json
{
	"message": "<Not Found message>"
}
```

_Response (500 - Internal Server Error)_

```json
{
	"message": "<internal error messages>"
}
```

### PATCH /checkout

> Finish Order processing, change order status to finished in cart

_Request Header_

```json
{
	"access_token": "<user access token>"
}
```

_Request Body_

```json
Not Needed
```

_Response (200)_

```json
{
	"message": "Order finished being processed"
}
```

_Response (401 - Unauthorized)_

```json
{
	"message": "<Authentication message>"
}
```

_Response (400 - Bad Request)_

```json
{
	"message": "Stock is not enough"
}
```

_Response (500 - Internal Server Error)_

```json
{
	"message": "<internal error messages>"
}
```

### GET /history

> Get all Product in a cart that have finished status

_Request Header_

```json
{
	"access_token": "<user access token>"
}
```

_Request Body_

```json
Not Needed
```

_Response (200)_

```json
[
  {
    "id": <cart id>,
    "UserId": "<User ID>",
    "status": "finished",
    "quantity": <cart order quantity>,
    "Product": {
      "id": <product id>,
      "name": "<product name>",
      "img_url": "<product image link>",
      "price": <product price>,
      "stock": <product stock>,
      "CategoryID": <product category>,
      "createdAt": "<time cart created>",
      "updatedAt": "<time cart updated>",
      "Category": {
        "id": <category id>,
        "name": "<category name>",
        "createdAt": "<time category created>",
        "updatedAt": "<time category updated>",
      }
    },
  },
  {
    "id": <cart id>,
    "UserId": "<User ID>",
    "status": "finished",
    "quantity": <cart order quantity>,
    "Product": {
      "id": <product id>,
      "name": "<product name>",
      "img_url": "<product image link>",
      "price": <product price>,
      "stock": <product stock>,
      "CategoryID": <product category>,
      "createdAt": "<time cart created>",
      "updatedAt": "<time cart updated>",
      "Category": {
        "id": <category id>,
        "name": "<category name>",
        "createdAt": "<time category created>",
        "updatedAt": "<time category updated>",
      }
    },
  },
]
```

_Response (401 - Unauthorized)_

```json
{
	"message": "<Authentication message>"
}
```

_Response (500 - Internal Server Error)_

```json
{
	"message": "<internal error messages>"
}
```

### GET /wishlist

> Get all Product in a Wish List

_Request Header_

```json
{
	"access_token": "<user access token>"
}
```

_Request Body_

```json
Not Needed
```

_Response (200)_

```json
[
  {
    "id": <wishlist ID>,
    "UserId": <User ID>,
    "ProductId": <Product ID>,
    "Product": {
      "id": <product id>,
      "name": "<product name>",
      "img_url": "<product image link>",
      "price": <product price>,
      "stock": <product stock>,
      "CategoryID": <product category>,
      "createdAt": "<time cart created>",
      "updatedAt": "<time cart updated>",
      "Category": {
        "id": <category id>,
        "name": "<category name>",
        "createdAt": "<time category created>",
        "updatedAt": "<time category updated>",
      }
    },
  },
  {
    "id": <wishlist ID>,
    "UserId": <User ID>,
    "ProductId": <Product ID>,
    "Product": {
      "id": <product id>,
      "name": "<product name>",
      "img_url": "<product image link>",
      "price": <product price>,
      "stock": <product stock>,
      "CategoryID": <product category>,
      "createdAt": "<time cart created>",
      "updatedAt": "<time cart updated>",
      "Category": {
        "id": <category id>,
        "name": "<category name>",
        "createdAt": "<time category created>",
        "updatedAt": "<time category updated>",
      }
    },
  },
]
```

_Response (401 - Unauthorized)_

```json
{
	"message": "<Authentication message>"
}
```

_Response (500 - Internal Server Error)_

```json
{
	"message": "<internal error messages>"
}
```

### DELETE /wishlist/:id

> Delete product from wishlist

_Request Header_

```json
{
	"access_token": "<user access token>"
}
```

_Request Body_

```json
Not Needed
```

_Response (200)_

```json
{
	"message": "Delete a Wish successful"
}
```

_Response (401 - Unauthorized)_

```json
{
	"message": "<Authentication message>"
}
```

_Response (404 - Not Found)_

```json
{
	"message": "<Not Found message>"
}
```

_Response (500 - Internal Server Error)_

```json
{
	"message": "<internal error messages>"
}
```

### POST /wishlist

> Add Product to Wishlist

_Request Header_

```json
{
	"access_token": "<user access token>",
	"Content-Type": "application/json"
}
```

_Request Body_

```json
{
  "ProductId": <Product id that added to Wishlist>
}
```

_Response (201)_

```json
{
	"message": "Product successfully added to Wish List / Product Already added to Wish List"
}
```

_Response (401 - Unauthorized)_

```json
{
	"message": "<Authentication message>"
}
```

_Response (400 - Bad Request)_

```json
{
	"message": "<Bad Request message>"
}
```

_Response (500 - Internal Server Error)_

```json
{
	"message": "<internal error messages>"
}
```
