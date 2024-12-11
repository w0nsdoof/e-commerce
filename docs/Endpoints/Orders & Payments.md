# Orders

## 1. Payment Create
- **Request Type:** POST
- **Path:** `/api/payment/{{order_id}}/`
- **Description:** This request is used to create a payment for an order. It's not essential for order creation, but is included for completeness.
- **Input:**
  ```json
  {
    "product": 1,
    "rating": 9
  }
  ```
- **Output:**
  ```json
  {
    "error": "Payment already exists for this order."
  }
  ```

## 2. Retrieve Payments
- **Request Type:** GET
- **Path:** `/api/payment/check_payments/`
- **Description:** Checks the status of payments and marks any expired payments as failed.
- **Input:** No input required.
- **Output:**
  ```json
  {
    "message": "0 payments marked as failed."
  }
  ```
## 3. Confirm Payment
- **Request Type:** GET
- **Path:** `/api/payment/{payment_token}/`
- **Description:** Confirms the payment when the user visits the link sent by email. The payment_token is unique for each payment.
- **Input:** No input required.
- **Output:**
```json
{
  "message": "Payment confirmed successfully."
}
```

## 3. Create Order From Cart
- **Request Type:** POST
- **Path:** `/api/orders/create_from_cart/`
- **Description:** Creates an order from the cart. Transfers items from the cart to the order. Doesn't create an order if the cart is empty.
- **Input:** No input required.
- **Output:**
  ```json
  {
    "order": {
      "id": 6,
      "user": 1,
      "order_status": "pending",
      "total_amount": "1600.00",
      "items": [
        {
          "id": 6,
          "product": { "id": 1, "name": "Cola 2l", "price": "800.00" },
          "quantity": 2,
          "subtotal": 1600
        }
      ],
      "total_items": 2,
      "created_at": "2024-12-11T20:14:24Z",
      "updated_at": "2024-12-11T20:14:24Z"
    },
    "payment_url": "http://127.0.0.1:8000/api/payment/1fe5317a-7be5-4ef3-8ae8-ac7d95e500b6/"
  }
  ```

## 4. Get Orders
- **Request Type:** GET
- **Path:** `/api/orders/`
- **Description:** Retrieves information about all orders placed by the user. It serves for development purposes, as emails are sent with order details.
- **Input:** No input required.
- **Output:**
  ```json
  [
    {
      "id": 6,
      "user": 1,
      "order_status": "pending",
      "total_amount": "1600.00",
      "items": [
        {
          "id": 6,
          "product": { "id": 1, "name": "Cola 2l", "price": "800.00" },
          "quantity": 2,
          "subtotal": 1600
        }
      ],
      "total_items": 2,
      "created_at": "2024-12-11T20:14:24Z",
      "updated_at": "2024-12-11T20:14:24Z"
    }
  ]
  ```

## 5. Cancel Order
- **Request Type:** POST
- **Path:** `/api/orders/{{order_id}}/cancel_order/`
- **Description:** Cancels an order if it is still in the "pending" status.
- **Input:**
  ```json
  {
    "order_id": 1
  }
  ```
- **Output:**
  ```json
  {
    "id": 5,
    "order_status": "cancelled",
    "total_amount": "4000.00",
    "items": [
      {
        "id": 5,
        "product": { "id": 1, "name": "Cola 2l", "price": "800.00" },
        "quantity": 5,
        "subtotal": 4000
      }
    ],
    "total_items": 5,
    "created_at": "2024-12-11T20:12:13Z",
    "updated_at": "2024-12-11T20:14:12Z"
  }
  ```
