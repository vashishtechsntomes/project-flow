## Main Entities &amp; Relationships

```
flowchart TD
  subgraph ENT[Main Entities & Relationships]
    direction TB
    CE[Company]
    CL[Company Location]
    CP[Contact Person]
    BR[Brand]
    PR[Product]
    U[User]
    UBP[User–Brand Permissions -product_listing, market_survey, brand_list, ...]

    CE -->|has many| CL
    CE -->|has many| BR
    BR -->|has many| PR
    CL -->|managed by| CP
    CE -->|has many| U
    U --- UBP
    UBP --- BR
  end
```
![alt text](<main-entities-relationships.png>)



## Create new or existing company flow
```
---
config:
  layout: dagre
---
flowchart TB
    A0["Start"] --> A1["Admin clicks - Create Company"]
    A1 --> A2[["Modal Opens: Type Company Name"]]
    A2 --> A3["System: Auto-search existing companies"]
    A3 --> A4{"Company found?"}
    A4 -- "No- New Company" --> N1["Form: Company Name, Contact Person Name, Email, Designation"]
    N1 --> N2["System: Create Company + Primary Contact records"]
    N2 --> N3["Send Invite- tokenized, time-limited link"]
    N3 --> N4{"Contact opens link in time?"}
    N4 -- No / Expired --> N3A["Regenerate link & resend"]
    N3A --> N3
    N4 -- Yes --> N5["Onboarding Form"]
    N5 --> N6["Contact fills basic details, Address &amp; Uploads Legal/Compliance Docs"]
    N6 --> N7["Submit -> Status: Pending Approval"]
    N7 --> N8["Admin Review: Company + Location + Docs"]
    N8 --> N9{"Approve?"}
    N9 -- Reject --> N10["Notify with reason"]
    N10 --> N5
    N9 -- Approve --> N11["Create Login for Primary Contact"]
    N11 --> N12["End - Contact can log in"]
    A4 -- "Yes- Existing Company" --> E1["Form: Company Name- auto-filled, New Contact Person Name, Email, Designation"]
    E1 --> E2["System: Create New Location + Contact- linked to existing company"]
    E2 --> E3["Send Invite- tokenized, time-limited link"]
    E3 --> E4{"Contact opens link in time?"}
    E4 -- No / Expired --> E3A["Regenerate link & resend"]
    E3A --> E3
    E4 -- Yes --> E5["Prefilled Onboarding- form with company details"]
    E5 --> n1["Contact fills Address &amp; Uploads Legal/Compliance Docs"]
    E6["Submit -> Status: Pending Approval"] --> E7["Admin Review: Location + Docs"]
    E7 --> E8{"Approve?"}
    E8 -- Reject --> E9["Notify with reason"]
    E9 --> E5
    E8 -- Approve --> E10["Create Login for New Location Contact"]
    E10 --> E11[["Data access scoped to CompanyID + LocationID"]]
    E11 --> E12["End - Contact can log in"]
    n1 --> E6
     A1:::action
     A2:::action
     A3:::store
     N1:::action
     N2:::store
     N3A:::action
     N5:::action
     N7:::store
     N8:::review
     N10:::danger
     N11:::good
     E1:::action
     E2:::store
     E3A:::action
     E5:::action
     E6:::store
     E7:::review
     E9:::danger
     E10:::good
     E11:::store
    classDef action fill:#eef,stroke:#55f,stroke-width:1px
    classDef review fill:#ffe,stroke:#fb0,stroke-width:1px
    classDef danger fill:#fee,stroke:#f66,stroke-width:1px
    classDef good fill:#efe,stroke:#3c6,stroke-width:1px
    classDef store fill:#f3f7ff,stroke:#6aa7ff,stroke-width:1px
```

![alt text](<company-creation.png>)


## After brandadmin login flow

```
---
config:
  layout: dagre
---
flowchart LR
 subgraph subGraph0["User Management"]
        B2["Admin: Add New User Request - Name, Email, Role, Brands, Permissions"]
        B3@{ label: "Upload 'Letter of Authority' - mandatory" }
        B4["Submit -> Status: Pending Approval"]
        B5["Platform Admin Review User + Letter"]
        B6{"Approve User?"}
        B7["Notify Location Admin with reason"]
        B8["System: Create User Account + Assign Brand-level Permissions"]
        n1["Notify user about login details"]
  end
 subgraph subGraph1["Brand Management"]
        B9["User with Brand Rights: Add New Brand"]
        B10["Fill Brand Details: Name, Description, Category"]
        B11["Status: Pending Approval"]
        B12["Platform Admin Review Brand"]
        B13{"Approve Brand?"}
        B14["Notify with reason"]
        B15["Brand Active -> Available in Location Scope"]
  end
 subgraph subGraph2["Product Management"]
        B16["User with Product Rights: Add Product under Approved Brand"]
        B17["Fill Product Details + Attach Compliance Docs"]
        B18["Status: Pending Approval"]
        B19["Platform Admin Review Product"]
        B20{"Approve Product?"}
        B21["Notify with reason"]
        B22["Product Active -> Visible in Brand Catalog"]
  end
    A0["Brand/Location Admin Logs In"] --> B1["Dashboard: Scoped to Assigned Company + Location"] & UserManagement["UserManagement"] & BrandManagement["BrandManagement"] & ProductManagement["ProductManagement"]
    B2 --> B3
    B3 --> B4
    B4 --> B5
    B5 --> B6
    B6 -- Reject --> B7
    B6 -- Approve --> B8
    B9 --> B10
    B10 --> B11
    B11 --> B12
    B12 --> B13
    B13 -- Reject --> B14
    B13 -- Approve --> B15
    B16 --> B17
    B17 --> B18
    B18 --> B19
    B19 --> B20
    B20 -- Reject --> B21
    B20 -- Approve --> B22
    B8 --> n1
    B3@{ shape: rect}
     B2:::action
     B3:::action
     B4:::store
     B5:::review
     B7:::danger
     B8:::good
     B9:::action
     B10:::action
     B11:::store
     B12:::review
     B14:::danger
     B15:::good
     B16:::action
     B17:::action
     B18:::store
     B19:::review
     B21:::danger
     B22:::good
     B1:::store
    classDef action fill:#eef,stroke:#55f,stroke-width:1px
    classDef review fill:#ffe,stroke:#fb0,stroke-width:1px
    classDef danger fill:#fee,stroke:#f66,stroke-width:1px
    classDef good fill:#efe,stroke:#3c6,stroke-width:1px
    classDef store fill:#f3f7ff,stroke:#6aa7ff,stroke-width:1px

```

![alt text](<After-brandadmin-login-flow.png>)