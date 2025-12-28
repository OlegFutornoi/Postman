# Docs: API Documentation page + Postman collection for Admin/User cabinet
https://marketgrow.lovable.app/docs

## Overview

This update adds a dedicated API documentation page and a ready-to-use Postman collection for both Admin and User flows.

- New `/docs` page with grouped, ready-to-run endpoints.
- Downloadable Postman collection with environment variables and test scripts to chain requests.
- “Create User” endpoint added to the Admin Users section.
- “Create Product” endpoint expanded to full `CreateProductData` payload, including metadata, images, params, and store links.

---

## Admin API

### Auth

- `POST /auth/v1/token?grant_type=password`  
  Issue access token for an existing user.
- `POST /auth/v1/signup`  
  Register a new user account.

### Users

- `GET /functions/v1/users`  
  List users with filters/pagination (where applicable).
- `POST /functions/v1/users`  
  Create a new user (Admin side, “Create User”).
- `PATCH /functions/v1/users/{id}`  
  Update an existing user by ID.
- `DELETE /functions/v1/users/{id}`  
  Delete a user by ID.

### Permissions

- `GET /functions/v1/permissions?user_id={{user_id}}`  
  Get permissions for a specific user.
- `POST /functions/v1/permissions`  
  Create or update user permissions.

---

## User API

### Shops

- `POST /functions/v1/user-shops-list`  
  List shops for the current user.
- `POST /functions/v1/create-shop`  
  Create a new shop.
- `POST /functions/v1/update-shop`  
  Update shop data.
- `POST /functions/v1/delete-shop`  
  Delete a shop.
- `POST /functions/v1/store-categories-list`  
  List categories for a store.
- `POST /functions/v1/delete-store-categories-with-products`  
  Delete categories and all related products.
- `POST /functions/v1/get-store-products-count`  
  Get the number of products per store.

### Store Currencies

- `POST /functions/v1/store-currencies-list`  
  List currencies configured for a store.
- `POST /functions/v1/add-store-currency`  
  Add a new currency to a store.
- `POST /functions/v1/set-base-store-currency`  
  Set base currency for a store.
- `POST /functions/v1/update-store-currency-rate`  
  Update currency rate for a store.
- `POST /functions/v1/delete-store-currency`  
  Remove a store currency.
- `POST /functions/v1/get-available-currencies`  
  List available global currencies.

### Suppliers

- `POST /functions/v1/suppliers-list`  
  List suppliers for the current user/store.
- `POST /functions/v1/suppliers-limit`  
  Get or validate supplier limits.
- `POST /functions/v1/suppliers-create`  
  Create a supplier.
- `POST /functions/v1/suppliers-update`  
  Update supplier data.
- `POST /functions/v1/suppliers-delete`  
  Delete a supplier.

### Products

- `POST /functions/v1/user-products-list`  
  List products for the current user/store with filters/pagination.
- `POST /functions/v1/create-product`  
  Create a product with full `CreateProductData` payload, including:
  - store / supplier / category / currency
  - names and localized names
  - vendor, article
  - availability and stock quantity
  - prices and custom prices
  - description and docket
  - state / status fields
  - images (R2 keys / URLs)
  - custom params
  - store product links
- `POST /functions/v1/update-product`  
  Update existing product by ID.
- `POST /functions/v1/delete-product`  
  Delete product by ID.
- `POST /functions/v1/duplicate-product`  
  Duplicate existing product with its metadata and links.

### Supplier Categories

- `POST /functions/v1/categories`  
  Unified endpoint with `action` parameter:
  - `action: 'list'` – list categories.
  - `action: 'get_supplier_categories'` – list categories for a specific supplier.

---

## Postman Collection

- The `/docs` page provides an **Export** button that generates a Postman collection.
- Collection includes predefined variables:
  - `base_url`
  - `access_token`
  - `store_id`
  - `supplier_id`
  - `currency_code`
  - `product_id`
  - and other IDs needed for chained requests.
- Test scripts:
  - Extract IDs (user, store, supplier, product, etc.) from responses.
  - Persist them into collection variables for use in subsequent requests.
- Authentication:
  - Automatically attaches `apikey` for `/auth/v1` and `/rest/v1` endpoints.
  - Uses `access_token` variable in `Authorization: Bearer {{access_token}}` where required.

