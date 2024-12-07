# Software Requirements Specification (SRS) for MedPlus Clone

## 1. Introduction

### 1.1 Purpose
The purpose of this Software Requirements Specification (SRS) document is to outline the requirements for the *MedPlus Clone* application. This application aims to provide a platform for users to search for medicines, place orders, upload prescriptions, and track their deliveries. The SRS document defines the functional and non-functional requirements, user expectations, and system specifications in a way that is clear and comprehensible for both developers and stakeholders involved in the project.

### 1.2 Scope
The MedPlus Clone is a web and mobile application that mimics the functionalities of the MedPlus pharmacy system. The system will provide a complete solution for customers to find medicines, place orders, and receive deliveries. Additional features such as prescription uploads, order tracking, and medicine recommendations will be integrated into the platform.

Key Features:
- Medicine Search and Discovery
- Prescription Upload
- Online Medicine Ordering and Delivery
- User Profile Management
- Order Tracking
- User Reviews and Ratings for Medicines

This system will be compatible with Android, iOS, and Web platforms.

### 1.3 Definitions, Acronyms, and Abbreviations

- *User*: The person accessing the MedPlus Clone app (Customer).
- *Admin*: The person managing the back-end operations of the app (Admin User).
- *Prescription*: A digital copy of a user’s medicine prescription.
- *Medicine Search*: A feature allowing users to search for available medicines based on name or category.
- *Order Tracking*: A feature to track the status of the placed orders in real-time.
- *API*: Application Programming Interface for communication between frontend and backend services.

### 1.4 References
- *Swebok V4*: Software Engineering Body of Knowledge (Swebok) version 4 guidelines.
- *ISO/IEC 9126*: Software engineering — Product quality standard.

---

## 2. System Overview

### 2.1 Product Perspective
The MedPlus Clone will act as an e-commerce platform for purchasing medicines, similar to the original MedPlus app. The system will consist of three primary modules:

1. *Customer App (Frontend)*: Users will interact with the platform to search for medicines, place orders, upload prescriptions, and track their deliveries.
2. *Admin Panel (Backend)*: Admins will manage medicine catalogs, process orders, and track user activities.
3. *Database*: A centralized storage system to store information about users, orders, prescriptions, and medicines.

### 2.2 Product Features
The MedPlus Clone app will feature the following functionalities:
- *Medicine Search and Discovery*: Users can search for medicines based on their name, category, or usage.
- *Prescription Upload*: Customers can upload their prescriptions for medicines that require one.
- *Medicine Order and Delivery*: Users can order medicines and choose between home delivery or pharmacy pickup.
- *Order Tracking*: Real-time tracking of order statuses.
- *User Reviews*: Customers can leave ratings and reviews for medicines.
- *Admin Panel*: Admins can manage inventory, monitor orders, and maintain the medicine catalog.

---

## 3. Functional Requirements

### 3.1 User Registration and Authentication
- *Sign Up and Login*: Users can register through their email, phone number, or social media accounts.
- *Profile Management*: Users can update their personal details, including delivery addresses, and track order history.
- *Authentication*: Multi-factor authentication for enhanced security during login.

### 3.2 Medicine Search and Discovery
- *Search Functionality*: Users can search for medicines based on name, category, or disease.
- *Filters*: Apply filters based on price, manufacturer, and availability.
- *Medicine Information*: View details such as dosage, uses, price, availability, and reviews.

### 3.3 Order Management
- *Add to Cart*: Users can add medicines to their cart and modify quantities.
- *Order Placement*: Choose delivery or pickup, and enter shipping details.
- *Order Confirmation*: Instant confirmation of orders through email/SMS.
- *Order Tracking*: Track the order status, including dispatched, in-transit, and delivered stages.

### 3.4 Prescription Upload
- *Prescription Submission*: Users can upload prescriptions for medicines that require one.
- *Prescription Verification*: Admins verify prescriptions before processing orders.
- *Prescription History*: Users can view past prescriptions and related orders.

### 3.5 Payment Processing
- *Payment Methods*: Multiple payment options, including credit/debit cards, UPI, net banking, and wallets.
- *Payment Confirmation*: Users receive order summaries and payment receipts.

### 3.6 Admin Dashboard
- *User Management*: Admins can view and manage user accounts.
- *Inventory Management*: Admins can update stock quantities and details of medicines.
- *Order Monitoring*: Admins can track and manage orders placed by customers.
- *Analytics*: Real-time reports on sales, user engagement, and inventory status.

### 3.7 User Feedback
- *Ratings*: After order completion, users can rate the medicines they ordered.
- *Reviews*: Detailed reviews with the ability to upload photos.
- *Suggestions*: Users can suggest improvements or report issues directly to the app support team.

---

## 4. Non-Functional Requirements

### 4.1 Performance
- *Scalability*: The system must be capable of handling high traffic during peak hours without degradation in performance.
- *Response Time*: The application should respond to user actions in under 2 seconds.
- *Load Handling*: The backend should be able to handle thousands of concurrent requests.

### 4.2 Security
- *Data Encryption*: All sensitive user information, including personal details and payment data, must be encrypted using industry-standard encryption algorithms.
- *Secure Payment Gateway*: All payment transactions must comply with PCI DSS standards.
- *Authentication*: Multi-layered security for user and admin authentication.

### 4.3 Usability
- *User-Friendly Interface*: The app should be intuitive, ensuring that users can easily browse medicines, place orders, and track deliveries.
- *Cross-Platform Consistency*: Ensure a consistent experience across Android, iOS, and web platforms.

### 4.4 Availability
- *Uptime*: The system should have an uptime of 99.9%, with redundancy and failover mechanisms in place.
- *Disaster Recovery*: Implement backup and disaster recovery procedures to ensure continuous service.

### 4.5 Compatibility
- *Device Compatibility*: The application should support Android (version 5.0 and up), iOS (version 11 and up), and the web platform on major browsers like Chrome, Firefox, and Safari.

---

## 5. System Design

### 5.1 Architecture
The system will follow a *client-server architecture*, where the front-end will be responsible for the user interface and interactions, and the backend will handle business logic, database management, and data processing.

### 5.2 Database Schema
The system will utilize a *relational database* to store information related to users, orders, prescriptions, and medicines.

*Entities and Relations*:
- *Users*: Stores user details (ID, name, email, password, address).
- *Medicines*: Stores medicine details (ID, name, description, price, quantity, manufacturer).
- *Orders*: Stores order details (Order ID, user ID, medicine IDs, total amount, status).
- *Prescriptions*: Stores prescription details (Prescription ID, user ID, prescription image, status).

---

## 6. Additional Considerations

### 6.1 Third-Party Integrations
- *Payment Gateway Integration*: Integration with a third-party payment gateway to handle payments.
- *Tracking APIs*: Integration with third-party delivery tracking services for real-time order tracking.
- *Push Notifications*: Integration with push notification services to send order updates, offers, and reminders.

### 6.2 Compliance
- *Regulatory Compliance*: Ensure the app complies with health and safety regulations for medicine sales.
- *Privacy Regulations*: The app must adhere to privacy laws such as GDPR for storing user data.

---

## 7. Conclusion
The MedPlus Clone aims to provide an efficient and user-friendly platform for customers to purchase medicines, upload prescriptions, and track orders. By integrating essential features such as secure payment methods, real-time order tracking, and an admin dashboard, this application is expected to provide an efficient and smooth user experience, ensuring customer satisfaction while maintaining industry-standard performance and security.
