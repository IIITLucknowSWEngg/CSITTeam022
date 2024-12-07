## 1. System Context diagram

![System Context Diagram](sys_context.png)

```plantuml

@startuml
title System Context Diagram: MedPlus Clone

actor "Customer" as Customer
actor "Admin" as Admin
actor "Pharmacy Partner" as Partner

rectangle "MedPlus Clone System" as MedPlus {
  component [Medicine Search]
  component [Order Management]
  component [Prescription Upload]
  component [User Reviews]
  component [Admin Dashboard]
  component [Inventory Management]
}

' Customer Interactions
Customer --> MedPlus : Interacts with features
MedPlus --> [Medicine Search] : Enables medicine discovery
MedPlus --> [Order Management] : Handles orders and tracking
MedPlus --> [Prescription Upload] : Manages prescription uploads
MedPlus --> [User Reviews] : Collects feedback

' Admin Interactions
Admin --> MedPlus : Uses Admin Dashboard
MedPlus --> [Admin Dashboard] : Offers admin tools
[Admin Dashboard] --> [Inventory Management] : Updates inventory, tracks stock

' Pharmacy Partner Interactions
Partner --> MedPlus : Provides inventory data, fulfills orders
MedPlus --> [Inventory Management] : Updates stock, tracks inventory
MedPlus --> [Order Management] : Sends delivery requests

' External Systems
rectangle "External Systems" {
  component [Payment Gateway]
  component [Notification Service]
  component [Delivery Tracking API]
}

' External System Interactions
[Order Management] --> [Payment Gateway] : Processes payments
[Order Management] --> [Delivery Tracking API] : Fetches delivery status
[Order Management] --> [Notification Service] : Sends order notifications
[Prescription Upload] --> [Notification Service] : Sends prescription updates
@enduml
```

---

## 2. Container Diagram

![Container Diagram](container_diagram.png)

```plantuml

@startuml
!define RECTANGLE_WIDTH 280
!define RECTANGLE_HEIGHT 100

actor "Customer" as Customer
actor "Admin" as Admin

rectangle "Frontend (Web & Mobile)" as Frontend {
  component "Customer App" as CustomerApp
  component "Admin Dashboard" as AdminDashboard
}

rectangle "Backend" as Backend {
  component "REST API" as API {
    component "Medicine Search Logic" as SearchLogic
    component "Order Processing Logic" as OrderProcessing
    component "Prescription Management Logic" as PrescriptionManagement
    component "Review Management Logic" as ReviewManagement
  }
}

database "Relational Database" as Database {
  component "Users"
  component "Medicines"
  component "Orders"
  component "Prescriptions"
  component "Reviews"
}

rectangle "External Systems" as ExternalSystems {
  component "Payment Gateway" as PaymentGateway
  component "Notification Service" as NotificationService
  component "Delivery Tracking API" as DeliveryTrackingAPI
}

rectangle "Pharmacy Partner Systems" as PharmacySystems {
  component "Inventory System" as InventorySystem
  component "Delivery Logistics System" as DeliverySystem
}

Customer --> CustomerApp
Admin --> AdminDashboard

CustomerApp --> Backend : Sends API Requests
AdminDashboard --> Backend : Sends Admin API Requests

API --> Database : Reads/Writes Data
API --> PaymentGateway : Processes Payments
API --> NotificationService : Sends Notifications
API --> DeliveryTrackingAPI : Tracks Deliveries

API --> InventorySystem : Fetches Medicines
API --> DeliverySystem : Sends Delivery Info

PharmacyPartner --> InventorySystem : Updates inventory
PharmacyPartner --> DeliverySystem : Handles deliveries
@enduml

```

---

## 3. Component Diagram

### 3.1 Customer Component Diagram

![Customer Component Diagram](cust_comp.png)

```plantuml

@startuml
!define RECTANGLE_WIDTH 250
!define RECTANGLE_HEIGHT 80

package "Customer Web/Mobile App" {
  component "Medicine Search" as MedicineSearch
  component "Order Management" as OrderManagement
  component "Prescription Upload" as PrescriptionUpload
  component "Tracking & Reviews" as TrackingAndReviews
}

package "Backend API" {
  component "Medicine Search Logic" as SearchLogic
  component "Order Processing Logic" as OrderProcessing
  component "Prescription Management Logic" as PrescriptionManagement
  component "Review Management Logic" as ReviewManagement
}

MedicineSearch --> SearchLogic : Queries Medicines
OrderManagement --> OrderProcessing : Places Orders
PrescriptionUpload --> PrescriptionManagement : Submits Prescriptions
TrackingAndReviews --> ReviewManagement : Sends Reviews
@enduml

```

---

### 3.2 Admin Component Diagram

![Admin Component diagram](adm_comp.png)

```plantuml

@startuml
!define RECTANGLE_WIDTH 250
!define RECTANGLE_HEIGHT 80

package "Admin Dashboard" {
  component "User Management" as UserManagement
  component "Inventory Management" as InventoryManagement
  component "Order Monitoring" as OrderMonitoring
  component "Analytics" as Analytics
}

package "Backend API" {
  component "Medicine Search Logic" as SearchLogic
  component "Order Processing Logic" as OrderProcessing
  component "Prescription Management Logic" as PrescriptionManagement
  component "Review Management Logic" as ReviewManagement
}

UserManagement --> SearchLogic : Manages User Profiles
InventoryManagement --> SearchLogic : Manages Inventory
OrderMonitoring --> OrderProcessing : Tracks Orders
Analytics --> OrderProcessing : Views Sales and User Data
Analytics --> ReviewManagement : Gathers Feedback Insights
@enduml

```

---

### 3.3 Pharmacy Partner Component Diagram

![Pharmacy Partner Component Diagram](pharm_comp.png)

```plantuml

@startuml
!define RECTANGLE_WIDTH 250
!define RECTANGLE_HEIGHT 80

package "Pharmacy Partner Systems" {
  component "Inventory System" as InventorySystem
  component "Delivery Logistics System" as DeliverySystem
}

package "Backend API" {
  component "Medicine Search Logic" as SearchLogic
  component "Order Processing Logic" as OrderProcessing
  component "Prescription Management Logic" as PrescriptionManagement
}

InventorySystem --> SearchLogic : Updates Medicine Availability
DeliverySystem --> OrderProcessing : Manages Delivery Logistics
DeliverySystem --> PrescriptionManagement : Handles Prescription Orders
@enduml

```

---

## 4. Deployment Diagram

![Deployment Diagram](deployment_diagram.png)

```plantuml

@startuml
node "Load Balancer" as LoadBalancer {
  artifact "Distributes Requests"
}

package "Backend Tier" {
  node "Backend API Server" as BackendAPI {
    artifact "Medicine Search Logic"
    artifact "Order Processing Logic"
    artifact "Prescription Management Logic"
    artifact "Review Management Logic"
  }
  database "Centralized Database" as Database {
    artifact "Users"
    artifact "Medicines"
    artifact "Orders"
    artifact "Prescriptions"
    artifact "Reviews"
  }
}

package "Frontend Tier" {
  node "Customer Web App" as CustomerWeb
  node "Customer Mobile App" as CustomerMobile
  node "Admin Dashboard" as AdminDashboard
}

package "Pharmacy Partner Systems" {
  node "Inventory System" as InventorySystem
  node "Delivery Logistics System" as DeliverySystem
}

package "External Services" {
  node "Payment Gateway" as PaymentGateway
  node "Notification Service" as NotificationService
  node "Delivery Tracking API" as DeliveryAPI
}

CustomerWeb --> LoadBalancer : API Requests
CustomerMobile --> LoadBalancer : API Requests
AdminDashboard --> LoadBalancer : Admin Requests

LoadBalancer --> BackendAPI : Routes Requests
BackendAPI --> Database : Reads/Writes Data
BackendAPI --> PaymentGateway : Processes Payments
BackendAPI --> NotificationService : Sends Notifications
BackendAPI --> DeliveryAPI : Tracks Deliveries

InventorySystem --> BackendAPI : Updates Medicine Stock
DeliverySystem --> BackendAPI : Manages Delivery Info
@enduml

```

---

## 5. ER Diagram

![ER Diagram](ER_diagram.png)

```plantuml

@startuml
entity "Users" {
    * user_id : UUID
    ---
    - name : String
    - email : String
    - password : String
    - address : String
    - phone_number : String
    - role : String <<enum>> (Customer, Admin, PharmacyPartner)
    - created_at : DateTime
}

entity "Medicines" {
    * medicine_id : UUID
    ---
    - name : String
    - description : String
    - category : String
    - manufacturer : String
    - price : Decimal
    - prescription_required : Boolean
    - created_at : DateTime
}

entity "Inventory" {
    * inventory_id : UUID
    ---
    - medicine_id : UUID
    - pharmacy_partner_id : UUID
    - stock_quantity : Integer
    - restock_threshold : Integer
}

entity "Orders" {
    * order_id : UUID
    ---
    - user_id : UUID
    - total_amount : Decimal
    - order_status : String <<enum>> (Pending, Approved, Dispatched, Delivered, Canceled)
    - created_at : DateTime
}

entity "Order_Items" {
    * order_item_id : UUID
    ---
    - order_id : UUID
    - medicine_id : UUID
    - quantity : Integer
    - price_per_unit : Decimal
}

entity "Prescriptions" {
    * prescription_id : UUID
    ---
    - user_id : UUID
    - prescription_file_path : String
    - status : String <<enum>> (Pending, Approved, Rejected)
    - created_at : DateTime
}

entity "Reviews" {
    * review_id : UUID
    ---
    - user_id : UUID
    - medicine_id : UUID
    - rating : Integer (1-5)
    - comment : String
    - created_at : DateTime
}

entity "Pharmacy_Partners" {
    * pharmacy_partner_id : UUID
    ---
    - name : String
    - address : String
    - contact_number : String
    - created_at : DateTime
}

entity "Delivery_Tracking" {
    * tracking_id : UUID
    ---
    - order_id : UUID
    - current_status : String <<enum>> (In-Transit, Out-for-Delivery, Delivered)
    - location : String
    - updated_at : DateTime
}

' Relationships
Users ||--o{ Orders : places
Orders ||--o{ Order_Items : contains
Order_Items }o--|| Medicines : references
Orders ||--o| Prescriptions : "if required"
Users ||--o{ Prescriptions : uploads
Users ||--o{ Reviews : writes
Reviews }o--|| Medicines : evaluates
Pharmacy_Partners ||--o{ Inventory : manages
Inventory ||--o| Medicines : stocks
Orders ||--o{ Delivery_Tracking : updates
@enduml

```

---