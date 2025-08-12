```
flowchart TD
    A[Admin Panel]

    %% Dashboard & Analytics
    A --> AB[Dashboard]
    AB --> AC[Product, Order and Sales Analytics]

    %% Company & Brand
    A --> B[Manage Company - Create/Edit/View]
    B --> D[Manage Brand - Create/Edit/View]
    D --> E[Assign Brand to Company - 1 Company to 1 Brand]

    %% Product Management
    A --> F[Manage Products - Create/Edit/View]
    F --> G[Assign Category]
    F --> H[Assign Tags]
    F --> I[Set Attributes]
    F --> J[Set Discount]
    F --> K[Manage Ratings - from Doctors and Customers]

    %% Seller Management
    A --> L[Manage Sellers]
    L --> M[Approve/Reject Seller]

    %% Doctor Management
    A --> N[Manage Doctors]
    N --> O[Approve/Reject Doctor]

    %% Customer Management
    A --> P[Manage Customers]

    %% Order Management
    A --> Q[Manage Orders]
    Q --> R[View/Update Order Status]

    %% Payment Management
    A --> S[Manage Payments]
    S --> T[Track Payment Status]
    S --> U[Refunds and Adjustments]

    %% Relationships
    E --> F
    F --> Q
    Q --> S
    P --> K
    N --> K

    %% Styling
    style A fill:#e5f1ff,stroke:#0275d8,stroke-width:1px
    style M fill:#ffe5e5,stroke:#d9534f,stroke-width:1px
    style O fill:#ffe5e5,stroke:#d9534f,stroke-width:1px
```

![alt text](<admin-flow.png>)