# Postman API Test Collections

This repository contains Postman collections for performing Quality Assurance (QA) tests on popular public APIs.

---

## 1. OpenWeatherMap API - QA Tests

This Postman collection provides a set of basic QA checks for the OpenWeatherMap **Current Weather Data** API endpoints. It's designed to validate the core functionality and response structure.

### Features & Tests Included

*   **Successful Request (200 OK):** Verifies a successful API response when searching for a valid city.
*   **Response Body Validation:**
    *   Checks that the response body is not empty and is valid JSON.
    *   Asserts the presence of key properties like `coord`, `weather`, `main`, and `name`.
    *   Validates the data types of essential fields (e.g., `id` is a number, `name` is a string).
*   **Negative Tests:**
    *   **Invalid API Key (401 Unauthorized):** Checks that the API correctly rejects requests with a bad API key.
    *   **City Not Found (404 Not Found):** Checks that the API returns a 404 error for a non-existent city.

### Getting Started

1.  **Get an API Key:** Sign up on the [OpenWeatherMap](https://openweathermap.org/appid) website to get your free API key.
2.  **Set Up Postman Environment:**
    *   Create a new Environment in Postman.
    *   Add a variable named `baseUrl` with the value `https://api.openweathermap.org`.
    *   Add a variable named `apiKey` and paste your API key as the value.
3.  **Run:** Select the created environment and run the collection using the Postman Collection Runner.

---

## 2. Restful Booker API - QA Tests (Cookie Auth)

This is a full collection for testing the [Restful Booker API](https://restful-booker.herokuapp.com/apidoc/index.html). It demonstrates a complete CRUD workflow (Create, Read, Update, Delete) and uses **token-based authentication via a cookie**.

### Features & Tests Included

The requests are ordered to follow a logical test flow.

*   **Health Check:** A simple `Ping` request to ensure the API is online.
*   **Authentication (`Auth - Create Token`):**
    *   Sends credentials to the `/auth` endpoint.
    *   A test script automatically extracts the `token` from the response and saves it to an environment variable.
*   **CRUD Workflow:**
    *   **Create Booking:** Creates a new booking and saves its `bookingid` to an environment variable.
    *   **Get Booking:** Retrieves the booking details using the saved `bookingid`.
    *   **Update Booking (PUT):** Updates the entire booking record. Requires the `token` to be passed in a `Cookie` header (e.g., `Cookie: token={{token}}`).
    *   **Partial Update Booking (PATCH):** Updates a specific field in the booking. Also requires the auth token cookie.
    *   **Delete Booking:** Deletes the created booking. Requires the auth token cookie.

# Restful-Booker API Postman Collection 1

This repository contains a Postman collection designed to test and demonstrate the core functionality of the **Restful-Booker API**. The collection provides a clear, sequential workflow for creating, authenticating, updating, and retrieving a booking.

## What is Restful-Booker?

Restful-Booker is a web API specifically created for learning and practicing how to test web services. It mimics a real-world booking system, offering endpoints for CRUD (Create, Read, Update, Delete) operations.

You can find the official API documentation here: [https://restful-booker.herokuapp.com/apidoc/index.html](https://restful-booker.herokuapp.com/apidoc/index.html)

## How to Use This Collection

### Prerequisites
- You must have [Postman](https://www.postman.com/downloads/) installed on your machine.

### 1. Import the Collection
1.  Download the `restful-booker.postman_collection.json` file from this repository.
2.  Open Postman.
3.  Click the **Import** button in the top-left corner.
4.  Upload the downloaded JSON file.
5.  The collection, named **"collection 1 - Restful Booker"**, will now appear in your workspace.

### 2. Understanding the Workflow
This collection is designed to be run in a specific order. It uses **Collection Variables** to pass data between requests automatically.

- `{{baseUrl}}` is pre-configured to `https://restful-booker.herokuapp.com`.
- `{{bookingId}}` and `{{authToken}}` will be populated automatically as you run the requests.

### 3. Execution Flow
Run the requests in the following order to see the full workflow in action:

1.  **`Create Booking`**
    - **Action:** Sends a `POST` request to `/booking` to create a new booking entry.
    - **Automation:** The `Tests` script automatically captures the `bookingid` from the response and saves it to the `{{bookingId}}` collection variable.

2.  **`Auth - Create Token`**
    - **Action:** Sends a `POST` request to `/auth` with admin credentials to get an authentication token.
    - **Automation:** The `Tests` script captures the `token` from the response and saves it to the `{{authToken}}` collection variable. This token is required for updating or deleting bookings.

3.  **`Update Booking`**
    - **Action:** Sends a `PUT` request to `/booking/{{bookingId}}` to modify the booking created in the first step.
    - **Automation:** It uses the `{{bookingId}}` variable in the URL and the `{{authToken}}` as a cookie for authentication. The request body contains the updated booking details.

4.  **`Get Booking by ID`**
    - **Action:** Sends a `GET` request to `/booking/{{bookingId}}` to retrieve the details of a single booking.
    - **Automation:** It uses the `{{bookingId}}` variable in the URL.
    - **Purpose:** This request is perfect for verifying that the `Update Booking` request was successful and that the data has been changed.

You can now run these requests sequentially to test the complete booking lifecycle.
