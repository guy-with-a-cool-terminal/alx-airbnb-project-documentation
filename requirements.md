# Backend Feature Requirements – Airbnb Clone

This document outlines the technical and functional specifications for key backend features of the Airbnb Clone system.

---

## 1. 🔐 User Authentication

### ✅ Functional Requirements
- Users can register as a guest or host.
- Users can log in using email and password.
- Sessions are maintained using JWT (JSON Web Token).
- Passwords must be securely hashed.

### 🔌 API Endpoints

| Method | Endpoint         | Description             |
|--------|------------------|-------------------------|
| POST   | /api/register     | Register a new user     |
| POST   | /api/login        | Login with credentials  |
| GET    | /api/profile      | Get current user profile (Auth required) |

### 🔍 Input Specifications

- `first_name` (string, required)
- `last_name` (string, required)
- `email` (string, required, unique, valid email format)
- `password` (string, required, min 8 chars)
- `role` (enum: `guest`, `host`, required)

### 🎯 Output Example

```json
{
  "user": {
    "id": "uuid",
    "email": "user@example.com",
    "token": "jwt-token"
  }
}
````

### 🛡️ Validation Rules

* Passwords must be hashed (e.g., bcrypt).
* Duplicate emails must return an error.
* All fields must be validated for type and format.

---

## 2. 🏡 Property Management

### ✅ Functional Requirements

* Hosts can add, update, and delete properties.
* Guests can view and search available properties.
* Listings include title, description, price, location, amenities.

### 🔌 API Endpoints

| Method | Endpoint             | Description               |
| ------ | -------------------- | ------------------------- |
| POST   | /api/properties      | Create new listing (Host) |
| PUT    | /api/properties/\:id | Update a listing          |
| DELETE | /api/properties/\:id | Delete a listing          |
| GET    | /api/properties      | Get all listings          |
| GET    | /api/properties/\:id | Get property by ID        |

### 🔍 Input Specifications

* `name` (string, required)
* `description` (text, required)
* `location` (string, required)
* `pricepernight` (decimal, required)
* `host_id` (uuid, auto from JWT)

### 🎯 Output Example

```json
{
  "property": {
    "id": "uuid",
    "name": "Ocean View Apartment",
    "location": "Miami",
    "pricepernight": 120.00
  }
}
```

### 🛡️ Validation Rules

* Only users with role `host` can create or edit listings.
* Price must be positive.
* Required fields cannot be empty.

---

## 3. 📅 Booking System

### ✅ Functional Requirements

* Guests can book available properties.
* Booking must check for date conflicts.
* Hosts can confirm or cancel bookings.
* System calculates total price automatically.

### 🔌 API Endpoints

| Method | Endpoint           | Description               |
| ------ | ------------------ | ------------------------- |
| POST   | /api/bookings      | Create a booking          |
| GET    | /api/bookings      | View bookings (User only) |
| PUT    | /api/bookings/\:id | Update booking status     |
| DELETE | /api/bookings/\:id | Cancel a booking          |

### 🔍 Input Specifications

* `property_id` (uuid, required)
* `start_date` (date, required)
* `end_date` (date, required)
* `user_id` (auto from JWT)

### 🎯 Output Example

json
{
  "booking": {
    "id": "uuid",
    "property_id": "uuid",
    "start_date": "2025-07-01",
    "end_date": "2025-07-05",
    "total_price": 480.00,
    "status": "confirmed"
  }
}

### 🛡️ Validation Rules

* Check for overlapping bookings on `property_id`.
* `start_date` must be before `end_date`.
* Only property owners can confirm or cancel a booking.

---

## 🧪 Performance Criteria

* All endpoints must respond within 300ms under normal load.
* Rate limiting for sensitive routes like login: 5 req/min/IP.
* Pagination required for listing endpoints (default 10/page).

---

## 🔒 Security Requirements

* All routes must be secured via JWT.
* Sensitive data (passwords) are never stored or returned in plaintext.
* Admin routes must be protected via role-based middleware.

---

## 🌐 Optional Enhancements (Future)

* OAuth support (Google/Facebook)
* Host payout tracking
* Real-time availability calendar


