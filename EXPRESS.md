# Express.js Product API

## Getting Started

### 1. Install Dependencies
```
npm install
```

### 2. Run the Server
```
node server.js
```
The server will start on [http://localhost:3000](http://localhost:3000) by default.

---

## Authentication
All requests require an API key in the headers:
```
x-api-key: my-secret-api-key
```

---

## API Endpoints

### 1. List Products
**GET /api/products**
- Query params: `category` (optional), `page` (default 1), `limit` (default 10)

**Example:**
```
GET /api/products?page=1&limit=2&category=electronics
```
**Response:**
```json
{
  "total": 2,
  "page": 1,
  "limit": 2,
  "products": [
    { "id": "1", "name": "Laptop", ... },
    { "id": "2", "name": "Smartphone", ... }
  ]
}
```

---

### 2. Get Product by ID
**GET /api/products/:id**

**Example:**
```
GET /api/products/1
```
**Response:**
```json
{
  "id": "1",
  "name": "Laptop",
  "description": "High-performance laptop with 16GB RAM",
  "price": 1200,
  "category": "electronics",
  "inStock": true
}
```

---

### 3. Create Product
**POST /api/products**
- Body: JSON with `name`, `description`, `price`, `category`, `inStock`

**Example:**
```
POST /api/products
Content-Type: application/json

{
  "name": "Blender",
  "description": "Powerful kitchen blender",
  "price": 99.99,
  "category": "kitchen",
  "inStock": true
}
```
**Response:**
```json
{
  "id": "generated-uuid",
  "name": "Blender",
  "description": "Powerful kitchen blender",
  "price": 99.99,
  "category": "kitchen",
  "inStock": true
}
```

---

### 4. Update Product
**PUT /api/products/:id**
- Body: JSON with all product fields

**Example:**
```
PUT /api/products/1
Content-Type: application/json

{
  "name": "Laptop Pro",
  "description": "Upgraded laptop with 32GB RAM",
  "price": 1500,
  "category": "electronics",
  "inStock": false
}
```
**Response:**
```json
{
  "id": "1",
  "name": "Laptop Pro",
  "description": "Upgraded laptop with 32GB RAM",
  "price": 1500,
  "category": "electronics",
  "inStock": false
}
```

---

### 5. Delete Product
**DELETE /api/products/:id**

**Example:**
```
DELETE /api/products/1
```
**Response:**
```json
{
  "message": "Product deleted",
  "product": { "id": "1", "name": "Laptop", ... }
}
```

---

### 6. Search Products by Name
**GET /api/products/search?name=...**

**Example:**
```
GET /api/products/search?name=coffee
```
**Response:**
```json
[
  {
    "id": "3",
    "name": "Coffee Maker",
    "description": "Programmable coffee maker with timer",
    "price": 50,
    "category": "kitchen",
    "inStock": false
  }
]
```

---

### 7. Product Statistics
**GET /api/products/stats**

**Example:**
```
GET /api/products/stats
```
**Response:**
```json
{
  "electronics": 2,
  "kitchen": 1
}
```

---

## Error Responses
- 401 Unauthorized: Missing or invalid API key
- 404 Not Found: Product not found
- 400 Bad Request: Validation errors
- 500 Internal Server Error: Unexpected errors

---

## Notes
- All endpoints require the `x-api-key` header.
- All request and response bodies are in JSON format. 