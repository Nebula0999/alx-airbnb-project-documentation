## 1. User Authentication
🔧 Functional Requirements
Users must be able to register using email/password or OAuth (Google, Facebook).

Login should issue a JWT token.

Token is required for accessing protected routes.

🌐 API Endpoints
Method	Endpoint	    Description
POST	/api/register	Register a new user
POST	/api/login	    Login with credentials
GET	    /api/profile	Get logged-in user data
PUT	    /api/profile	Update profile info

📥 Input Specifications
POST /api/register

json
{
  "email": "user@example.com",
  "password": "StrongPassword123",
  "role": "guest" // or "host"
}
📤 Output Example
json
{
  "message": "Registration successful",
  "token": "<jwt_token>"
}

**Validation Rules**
Email must be valid and unique.

Password must be at least 8 characters.

Role must be either "guest" or "host".


**Secure password hashing with bcrypt (min 10 rounds).**

## 2. Property Management
**Functional Requirements**
Hosts can create, update, and delete property listings.

Listings should support image uploads and availability scheduling.

🌐 API Endpoints
Method	Endpoint	        Description
POST	/api/properties	    Create a new listing
GET	    /api/properties	    Get all available properties
GET	    /api/properties/:id	Get property details
PUT	    /api/properties/:id	Update property info
DELETE	/api/properties/:id	Delete a property listing

📥 Input Specifications
POST /api/properties

json
{
  "title": "Cozy Cabin",
  "location": "Nairobi, Kenya",
  "price": 100,
  "max_guests": 4,
  "amenities": ["Wi-Fi", "Pool", "Kitchen"],
  "available_dates": ["2025-07-01", "2025-07-05"]
}
📤 Output Example
json
{
  "message": "Property listed successfully",
  "property_id": 123
}
**Validation Rules**
Title must be a string under 100 chars.

Price must be a positive number.

Amenities must be a list of pre-approved options.


## 3. Booking System
🔧 Functional Requirements
Guests can book properties for available dates.

Hosts and guests can cancel bookings based on a policy.

Prevent overlapping bookings.

🌐 API Endpoints
Method	Endpoint	                        Description
POST	/api/bookings	                    Create a booking
GET	    /api/bookings	                    View user’s bookings
PUT	    /api/bookings/:id	                Cancel or update booking
GET	    /api/properties/:id/availability	Check date availability

**Input Specifications**
POST /api/bookings

json
{
  "property_id": 123,
  "start_date": "2025-07-02",
  "end_date": "2025-07-05",
  "guests": 2
}
📤 Output Example
json
{
  "message": "Booking confirmed",
  "booking_id": 456,
  "status": "pending"
}
**Validation Rules**
Date range must not overlap existing bookings.

Start date must be before end date.

Guests must not exceed max_guests for the listing.