# **Software Test Documentation**
---

## **Table of Contents**

| **Section** | **Title**                     |
|-------------|-------------------------------|
| 1           | Objectives and Scope          |
| 2           | Test Strategy                 |
| 3           | Functional Test Scenarios     |

---

## **1. Objectives and Scope**

### **1.1 Objectives**
The objective of this document is to define and execute a comprehensive testing process for the MedPlus Clone, ensuring all modules are fully functional, secure, and user-friendly. Testing focuses on features such as **Medicine Search**, **Prescription Management**, **Order Workflow**, and **Payment Gateways**.

### **1.2 Scope**
**In-Scope**:
- Functional Testing for **User Management**, **Search and Filters**, **Order Placement**, and **Payment Processing**.
- Validation of **API integrations** (e.g., Payment Gateway, Prescription OCR).
- Verification of **responsive design** across devices.

**Out of Scope**:
- Performance and load testing.
- Multi-language and regional compliance testing.

---

## **2. Test Strategy**

### **2.1 Testing Methodology**
- **Manual Testing**: For UI interactions and exploratory workflows.
- **Automated Testing**: Using **Chai** for backend logic and **Selenium** for UI workflows.
- **Regression Testing**: Run automated scripts post every feature addition.

### **2.2 Key Success Metrics**
- Pass rate of **95% or higher** for critical test cases.
- Critical issues, especially in **Payment Processing** and **Prescription Validation**, must have **zero defects**.

### **2.3 Tools and Frameworks**
- **Frontend Testing**: Selenium, Jest.
- **Backend Testing**: Chai
- **API Testing**: Postman

---

## **3. Functional Test Scenarios**

### **3.1 User Management**

#### **Scenario 1: User Registration**
```gherkin
Feature: User Registration

  Scenario: Successful Registration
    Given a user is on the registration page
    When they enter valid details
    And submit the form
    Then their account should be created
    And a confirmation email should be sent
```

**JavaScript Code Example** (using **Mocha/Chai**):
```javascript
const chai = require('chai');
const expect = chai.expect;
const { registerUser } = require('./userController');

describe('User Registration', () => {
  it('should successfully create a user and send confirmation email', () => {
    const registrationData = {
      email: 'testuser@medplus.com',
      password: 'SecurePass123',
      name: 'Test User',
    };

    const response = registerUser(registrationData);
    expect(response.success).to.equal(true);
    expect(response.emailSent).to.equal(true);
  });
});
```

---

### **3.2 Medicine Search and Discovery**

#### **Scenario 2: Search with Filters**
```gherkin
Feature: Medicine Search

  Scenario: Search Results with Filters
    Given a user is on the homepage
    When they search for "Paracetamol"
    And apply the filter "Price < $10"
    Then the results should display medicines under $10
```

**JavaScript Code Example** (using **Jest** for API response testing):
```javascript
const axios = require('axios');

test('Medicine search with filters should return valid results', async () => {
  const response = await axios.get('http://medplus-api.com/medicines?search=paracetamol&price_lt=10');
  expect(response.status).toBe(200);
  expect(response.data.medicines).toHaveLength(5); // Assuming 5 results match the filter
  expect(response.data.medicines[0].price).toBeLessThan(10);
});
```

---

### **3.3 Order Management**

#### **Scenario 3: Cart Management**
```gherkin
Feature: Cart Management

  Scenario: Adding an Item to the Cart
    Given a user is viewing a product page
    When they click "Add to Cart"
    Then the item should be added to their cart
    And the cart count should update
```

**JavaScript Code Example**:
```javascript
describe('Cart Management', () => {
  it('should add an item to the cart and update count', () => {
    const cart = [];
    const addItemToCart = (item) => cart.push(item);

    addItemToCart({ id: 101, name: 'Paracetamol', quantity: 1 });
    expect(cart).toHaveLength(1);
    expect(cart[0].name).toEqual('Paracetamol');
  });
});
```

---

### **3.4 Payment Processing**

#### **Scenario 4: Wallet Payment**
```gherkin
Feature: Wallet Payment

  Scenario: Successful Transaction
    Given a user has sufficient wallet balance
    When they confirm payment
    Then the wallet balance should be deducted
    And the order should be confirmed
```

**JavaScript Code Example**:
```javascript
describe('Wallet Payment', () => {
  it('should process payment and deduct wallet balance', () => {
    let walletBalance = 100;
    const deductPayment = (amount) => (walletBalance -= amount);

    deductPayment(20);
    expect(walletBalance).toEqual(80);
  });
});
```
