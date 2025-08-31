# Airbnb Clone Backend - Requirement Specifications

This document provides detailed specifications for three key backend features: **User Authentication**, **Property Management**, and **Booking System**. It includes API endpoints, input/output specifications, validation rules, and performance criteria.

---

## 1. User Authentication

**Description:**  
Handles user registration, login, and session management for Guests, Hosts, and Admins.

### API Endpoints

| Method | Endpoint              | Description                         |
|--------|----------------------|-------------------------------------|
| POST   | /api/auth/register   | Register a new user                 |
| POST   | /api/auth/login      | User login                           |
| GET    | /api/auth/profile    | Retrieve logged-in user profile      |
| PUT    | /api/auth/profile    | Update user profile                  |

Validation Rules

Email must be valid and unique.

Password must be 8+ chars, include uppercase, lowercase, number, special character.

Role must be guest or host.

Performance Criteria

Handle up to 1000 concurrent logins.

Response time < 500ms.

JWT tokens expire after 24 hour

2. Property Management

Description:
Allows hosts to create, update, delete, and retrieve property listings.

### API Endpoints

Method     |     	Endpoint          	    |         Description
POST	            /api/properties	                  Add a new property
GET              	/api/properties	                  Retrieve all properties
GET              	/api/properties/:id	              Retrieve a single property
PUT	              /api/properties/:id	              Update property details
DELETE           	/api/properties/:id	              Delete a property


### Validation Rules

Title and description cannot be empty.

Price > 0.

Availability dates must be valid ISO format and not overlap existing bookings.

Amenities must be from predefined list.

Performance Criteria

Support 100 property additions per minute.

Response time < 500ms.

Pagination support (20 listings per page


3. Booking System

Description:
Manages booking creation, validation, cancellation, and status tracking.

### API Endpoints

Method	       Endpoint                       	Description
POST	        /api/bookings                   	Create a new booking
GET	          /api/bookings	                    Get bookings for a user
GET	          /api/bookings/:id 	              Get booking details
PUT         	/api/bookings/:id/cancel        	Cancel a booking

### Validation Rules

Start date < end date.

Booking dates must not conflict with existing bookings.

Guest count must not exceed property capacity.

Performance Criteria

Prevent double bookings under concurrent requests.

Payment confirmation response < 1 second.

Notifications triggered within 5 seconds.
