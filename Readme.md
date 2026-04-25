
# Restful Booker – API Testing Project

This project demonstrates a complete API testing workflow for the **Restful Booker** platform, including:

* Test case design
* Bug tracking using Excel and Jira
* API testing using Postman
* Test automation with scripts
* CLI execution via Newman
* Automated report generation

🔗 API Documentation: https://restful-booker.herokuapp.com/apidoc/

---

## Project Structure

The Postman collection is organized into 5 main functional modules:

| Folder | Method | Requests |
| ------ | ------ | -------- |
| Login  | POST   | 6        |
| Create | POST   | 16       |
| Read   | GET    | 7        |
| Update | PUT    | 12       |
| Delete | DELETE | 9        |

---

## Testing Workflow

### 1. Test Case Design

Test cases are designed based on API requirements, covering:

* Functional scenarios (happy path)
* Negative scenarios (invalid input, missing fields)
* Boundary values
* Security testing (SQL Injection, invalid authentication)

Each API is tested with:

* Happy cases
* Negative cases
* Edge cases

---

### 2. Bug Tracking (Jira)

All defects are manually logged in Jira with key information such as summary, reproduction steps, and expected vs actual results.
Postman run reports are attached to Jira issues to provide detailed request/response data.

---

### 3. API Testing with Postman

All API requests are implemented in **Postman**.

#### Features used:

* Environment variables (`{{authToken}}`, `{{last_created_id}}`)
* Pre-request scripts
* Test scripts 

#### Example validations:

```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response has booking id", function () {
    const res = pm.response.json();
    pm.expect(res).to.have.property("bookingid");
});
```

---

### 4. Automation with Scripts

Automation is implemented using:

* **Pre-request Script**

  * Auto-create booking before Update/Delete
  * Handle authentication (auto login if token missing)

* **Test Script**

  * Validate response status
  * Validate response body
  * Store variables for chaining

---

### 5. Running Tests with Newman

Collection is executed via **Newman** for automation and CI/CD integration.

#### Install Newman:

```bash
npm install -g newman
```

#### HTML Report:

```bash
npm install -g newman-reporter-htmlextra
```

#### Run collection:

```bash
newman run "Restful Booker.postman_collection.json" -e "Restful Booker.postman_collection.json" -r htmlextra   --reporter-htmlextra-export report.html
```

---
