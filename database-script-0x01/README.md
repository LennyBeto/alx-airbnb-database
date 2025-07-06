# Database Schema

This schema meticulously incorporates all normalization improvements, ensuring the robust functionality of AirBnB's core features. A precisely implemented trigger guarantees that only users designated with a 'host' role can list properties, while snapshot pricing mechanisms are in place to meticulously preserve historical data integrity.

## Key Features of the Schema:

### Normalization Compliance:

1NF: All attributes atomic (multi-valued roles handled in separate table)
2NF: No partial dependencies (snapshot_price captures historical rate)
3NF: No transitive dependencies (host validation through trigger)

### Data Integrity Constraints:

-- Role validation
PRIMARY KEY (user_id, role)  -- Composite PK ensures unique roles

-- Host validation trigger
BEFORE INSERT OR UPDATE ON properties

-- Review uniqueness
UNIQUE (property_id, user_id)  -- One review per user per property

-- Date validation
CHECK (end_date > start_date)

-- Rating validation
CHECK (rating BETWEEN 1 AND 5)

### Performance Optimization:

Indexes on all foreign keys and search columns
Composite indexes for common queries (dates, roles)
UUID primary keys for distributed systems

### Business Logic Enforcement:

snapshot_price_per_night preserves historical pricing
Payment-Booking 1:1 relationship (UNIQUE constraint)
Automatic timestamps (DEFAULT CURRENT_TIMESTAMP)
ON DELETE CASCADE for data integrity

### Security Considerations:

Password hashing instead of plain text
Role-based access control
Host verification before property listing

### Schema Highlights:

#### User Management:

Supports multi-role users (guest/host/admin)
Secure authentication with password hashing
Contact information with uniqueness constraints

#### Property System:

Historical price tracking via snapshot_price_per_night
Automatic timestamp updates (updated_at)
Location-based indexing for search

#### Booking Engine:

Date range validation
Status tracking (pending/confirmed/canceled)
Financial data integrity checks

#### Payment Processing:

Separate status lifecycle (pending/completed/refunded)
Payment method tracking
Amount validation

#### Review System:

Rating validation (1-5)
Prevention of duplicate reviews
Timestamped records

#### Messaging:

Sender/recipient tracking
Full-text message bodies
Conversation history preservation
