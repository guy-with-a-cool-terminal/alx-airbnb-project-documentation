This document summarizes the core features and functionalities required for the backend of the Airbnb Clone project. These features ensure the system is functional, scalable, and secure for both guests and hosts.

## Key Functional Areas

1. **User Management**
   - Registration & Login (JWT, OAuth)
   - Profile management with contact info and preferences

2. **Property Management**
   - Hosts can add, update, or remove property listings
   - Listings include title, description, location, price, amenities, and availability

3. **Search & Filtering**
   - Users can search by location, price, guests, and amenities
   - Pagination for large result sets

4. **Booking System**
   - Guests book properties for specific dates
   - Prevent double bookings
   - Booking status management (pending, confirmed, canceled)

5. **Payments**
   - Guests pay upfront using Stripe/PayPal
   - Hosts receive payouts post-booking
   - Support for multiple currencies

6. **Reviews & Ratings**
   - Guests leave reviews and ratings
   - Hosts can respond
   - Tied to completed bookings

7. **Notifications**
   - Email and in-app notifications for key events (booking, payment, cancellations)

8. **Admin Dashboard**
   - Admins manage users, properties, bookings, and payments
