Sample Data

This dataset offers a realistic six-month snapshot of platform activity. It meticulously captures authentic relationships between all entities, providing a robust foundation. This comprehensive sample is perfectly suited for thoroughly testing every feature within the application.

Sample Data Overview:
Users (5):

2 Hosts (John, Sarah)
2 Guests (Mike, Emma)
1 Admin
John has both host and guest roles
Properties (3):

Beachfront Villa ($350/night)
Downtown Loft ($185/night)
Mountain Cabin ($275/night)
John owns two properties
Bookings (4):

Confirmed beach stay (Mike, July)
Confirmed loft stay (Emma, August)
Pending mountain cabin (Mike, September)
Canceled beach stay (Emma, October)
Demonstrates different statuses
Payments (4):

Completed payments for confirmed bookings
Pending payment for pending booking
Refunded payment for canceled booking
Shows different payment methods (credit card, PayPal, Stripe)
Reviews (3):

Two 5-star reviews for the beach villa
One 4-star review for the downtown loft
Mountain cabin not reviewed yet
Shows multiple reviews per property
Messages (5):

Guest-host conversations about properties
Admin notification to host
Shows both sides of message exchanges
Real-World Data Features:
Temporal Consistency:

Bookings created before their start dates
Reviews created after stays completed
Payment dates aligned with booking dates
Business Logic Validation:

Hosts have host roles assigned
Snapshot prices match property prices at booking time
Review ratings within 1-5 range
Relationship Integrity:

All FKs reference existing records
Users have appropriate roles for actions
Payments correspond to booking statuses
Realistic Scenarios:

Property price updates (beach villa increased price)
Canceled booking with refund
Pending booking with payment authorization
Multiple reviews for popular property
Data Variety:

Different locations (Miami, Chicago, Aspen)
Various price points
Mixed review ratings
Multiple payment methods
To verify the data, you can run:

    -- Check booking totals
    SELECT
    b.booking_id,
    b.start_date,
    b.end_date,
    b.snapshot_price_per_night,
    (b.end_date - b.start_date) AS nights,
    (b.end_date - b.start_date) * b.snapshot_price_per_night AS calculated_total,
    p.amount AS paid_amount
    FROM bookings b
    JOIN payments p ON b.booking_id = p.booking_id;

    -- Check property reviews
    SELECT
    p.name AS property,
    COUNT(r.review_id) AS review_count,
    ROUND(AVG(r.rating), 1) AS avg_rating
    FROM properties p
    LEFT JOIN reviews r ON p.property_id = r.property_id
    GROUP BY p.property_id;

    -- Check user roles
    SELECT
    u.first_name || ' ' || u.last_name AS user,
    STRING_AGG(ur.role, ', ') AS roles
    FROM users u
    JOIN user_roles ur ON u.user_id = ur.user_id
    GROUP BY u.user_id;
