# API Test Execution Report
## Restful Booker – API Testing Project

**Project:** Restful Booker API Testing  
**Application Under Test:** Restful Booker  
**Base URL:** https://restful-booker.herokuapp.com  
**Testing Tool:** Postman  
**Testing Type:** Manual and Automated API Testing  
**Environment:** Restful Booker - QA  
**Report Date:** November 17, 2026  
**Execution Method:** Postman Collection Runner  

---

## 1. Executive Summary

This project focuses on validating the functionality, responses, and data integrity of the Restful Booker REST API using Postman.

The testing covered authentication, booking retrieval, booking creation, full and partial updates, deletion, and negative test scenarios.

Automated assertions were implemented using JavaScript in Postman's post-response scripts.

The final successful test executions confirmed that the main CRUD operations worked as expected in the tested scenarios.

## 2. Test Objectives

- Validate API response status codes.
- Verify response body structure and data types.
- Validate booking creation and retrieval.
- Verify full booking updates using PUT.
- Verify partial booking updates using PATCH.
- Validate booking deletion and confirm that deleted records cannot be retrieved.
- Test authentication with valid and invalid credentials.
- Execute automated tests using Postman Collection Runner.
- Identify and document unexpected API responses.

## 3. Test Scope and Results

| API Operation | Test Coverage | Result |
|---|---|---|
| GET /ping | Health-check response | Passed |
| POST /auth | Valid credentials and token generation | Passed |
| POST /auth | Invalid credentials | Passed |
| GET /booking | Booking list, valid IDs, response time | Passed |
| GET /booking/{id} | Booking details, data types, date validation | Passed |
| GET /booking/{invalidId} | Non-existing booking returns 404 | Passed |
| POST /booking | Booking creation and response validation | Passed |
| GET /booking/{createdId} | Created booking data verification | Passed |
| PUT /booking/{id} | Full booking update and persistence verification | Passed |
| PATCH /booking/{id} | Partial update and unchanged-field verification | Passed |
| DELETE /booking/{id} | Deletion and post-deletion verification | Passed |

## 4. Test Execution Results

### Regression Test Run

| Metric | Result |
|---|---|
| Automated Assertions | 26 |
| Passed | 26 |
| Failed | 0 |
| Errors | 0 |
| Duration | 3.432 seconds |
| Average Response Time | 251 ms |

The regression run covered the selected health-check, authentication, booking retrieval, negative retrieval, and booking creation/verification requests. It did not include every CRUD update and deletion scenario.

### CRUD Scenario Execution

| Scenario | Assertions Passed | Failed | Errors |
|---|---:|---:|---:|
| Create → Update (PUT) → Verify Updated Booking | 10 | 0 | 0 |
| Create → Partial Update (PATCH) → Verify Data | 9 | 0 | 0 |
| Create → Delete → Verify Deletion | 9 | 0 | 0 |

These results represent separate successful executions and should not be interpreted as a single combined test run.

**Additional verification:** The PUT update was also checked using a separate GET request, confirming that the updated firstname was `Mona` and the total price was `800`.

## 5. Key Test Validations

**Booking Creation**

The API successfully created new bookings and returned a valid booking ID. Assertions checked guest information, price, deposit status, booking dates, and additional needs.

**Full Booking Update**

A PUT request returned HTTP 200. A subsequent GET request confirmed that updated values were persisted.

**Partial Booking Update**

A PATCH request returned HTTP 200. Subsequent verification confirmed that the firstname changed to `Nour`, while selected unchanged fields retained their original values.

**Booking Deletion**

A DELETE request returned HTTP 201. A follow-up GET request returned HTTP 404, confirming that the deleted booking was no longer retrievable in that execution.

**Negative Testing**

Invalid authentication credentials were rejected as expected. Requests for non-existing booking IDs returned HTTP 404.

## 6. Observed Issues and Execution Notes

During earlier testing attempts, some PUT, PATCH, and DELETE requests returned unexpected HTTP 403 or HTTP 405 responses.

The team subsequently configured a shared collection-level pre-request authentication script to obtain and attach an authentication token for protected operations.

Successful PUT, PATCH, and DELETE executions were later observed.

An intermittent DELETE execution also returned HTTP 405 after an earlier successful run. The underlying cause was not conclusively established.

**Current assessment:** The relevant functional scenarios passed in their latest recorded successful runs. The earlier inconsistent responses should remain documented for further investigation if this were a production testing project. They are not classified here as confirmed application defects.

## 7. Tools and Techniques

- Postman for API request execution and collection management.
- JavaScript assertions using `pm.test()` and `pm.expect()`.
- Environment variables for reusable configuration and dynamic booking IDs.
- Collection-level pre-request scripting for authentication.
- Postman Collection Runner for automated scenario execution.
- Positive and negative test cases.
- Response schema and data-type validation.
- Data persistence verification.
- Response time assertions.

## 8. Conclusion

The Restful Booker API testing project successfully demonstrated automated functional API testing across authentication and the major CRUD operations.

All assertions passed in the recorded regression run and the final successful PUT, PATCH, and DELETE scenario runs.

The project demonstrates practical experience with Postman, API test scripting, dynamic variables, authentication handling, test execution, and verification of data changes.

**Overall Status: Passed for the documented successful executions, with intermittent authorization/method-response behavior noted for follow-up.**

---

**Test Evidence:** Postman Collection Runner screenshots and the exported Postman collection can be included as supporting project artifacts.
