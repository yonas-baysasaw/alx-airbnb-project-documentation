erDiagram
    USERS {
        int id PK
        string name
        string email
        string password_hash
        string role  // guest | host | admin
        string profile_photo
        string contact_info
    }

    PROPERTIES {
        int id PK
        int host_id FK
        string title
        string description
        string location
        float price
        string amenities
        string availability
        string images
    }

    BOOKINGS {
        int id PK
        int guest_id FK
        int property_id FK
        date start_date
        date end_date
        string status  // pending | confirmed | canceled | completed
    }

    PAYMENTS {
        int id PK
        int booking_id FK
        float amount
        string currency
        string status  // pending | completed | failed
        date payment_date
    }

    REVIEWS {
        int id PK
        int booking_id FK
        int guest_id FK
        int property_id FK
        int rating
        string comment
        date created_at
    }

    NOTIFICATIONS {
        int id PK
        int user_id FK
        string type  // booking | payment | cancellation
        string message
        boolean is_read
        date created_at
    }

    %% Relationships
    USERS ||--o{ PROPERTIES : "hosts"
    USERS ||--o{ BOOKINGS : "makes"
    USERS ||--o{ REVIEWS : "writes"
    USERS ||--o{ NOTIFICATIONS : "receives"

    PROPERTIES ||--o{ BOOKINGS : "booked in"
    PROPERTIES ||--o{ REVIEWS : "reviewed in"

    BOOKINGS ||--o{ PAYMENTS : "has"
    BOOKINGS ||--o{ REVIEWS : "can have"

    %% Admin has visibility over everything
    USERS ||--|| USERS : "admin manages"
    USERS ||--|| PROPERTIES : "admin monitors"
    USERS ||--|| BOOKINGS : "admin monitors"
    USERS ||--|| PAYMENTS : "admin monitors"
