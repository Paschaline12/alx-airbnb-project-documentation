# Airbnb Clone - Technical and Functional Requirements

This document outlines the technical and functional requirements for key backend features of the Airbnb Clone project.

---

## 1. User Authentication

### Functional Requirements
- Users must be able to **register, log in, and log out**.
- Authentication must use **JWT tokens** for secure session handling.
- Passwords must be **hashed using bcrypt**.

### API Endpoints
- `POST /api/auth/register` – Register a new user.  
  **Input:** `{ "name": "string", "email": "string", "password": "string" }`  
  **Output:** `{ "message": "User created successfully", "user_id": "uuid" }`  

- `POST /api/auth/login` – Log in a user.  
  **Input:** `{ "email": "string", "password": "string" }`  
  **Output:** `{ "token": "jwt_token", "user_id": "uuid" }`  

### Validation Rules
- Email must be unique and valid format.  
- Password must be at least 8 characters.  

### Performance Criteria
- Authentication requests must respond within **200ms** under normal load.  

---

## 2. Property Management

### Functional Requirements
- Hosts must be able to **add, update, and delete** property listings.  
- Guests must be able to **search properties by location, price, and availability**.

### API Endpoints
- `POST /api/properties` – Add a property.  
  **Input:** `{ "host_id": "uuid", "title": "string", "price": "decimal", "location": "string" }`  
  **Output:** `{ "message": "Property added", "property_id": "uuid" }`  

- `GET /api/properties?location=city` – Search properties.  
  **Output:** `[ { "property_id": "uuid", "title": "string", "price": "decimal" } ]`  

### Validation Rules
- Price must be a positive decimal.  
- Title and location cannot be empty.  

### Performance Criteria
- Property search must return results in **under 500ms**.  

---

## 3. Booking System

### Functional Requirements
- Guests must be able to **book available properties**.  
- System must prevent **double booking** of the same property and date.  
- Confirmed bookings must trigger a **payment process**.  

### API Endpoints
- `POST /api/bookings` – Create a booking.  
  **Input:** `{ "user_id": "uuid", "property_id": "uuid", "start_date": "date", "end_date": "date" }`  
  **Output:** `{ "message": "Booking confirmed", "booking_id": "uuid" }`  

- `GET /api/bookings/:user_id` – Retrieve bookings for a user.  
  **Output:** `[ { "booking_id": "uuid", "property_id": "uuid", "status": "confirmed" } ]`  

### Validation Rules
- Start date must be before end date.  
- Booking dates must not overlap with existing bookings.  

### Performance Criteria
- Booking creation must respond within **400ms**.  

---

## Summary
This document defines the technical and functional requirements for three core backend features:  
- **User Authentication**  
- **Property Management**  
- **Booking System**

It includes API endpoints, validation rules, and performance criteria to ensure a robust and scalable backend.

