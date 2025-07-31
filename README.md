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

### Getting Started

1.  **Set Up Postman Environment:**
    *   Create a new Environment in Postman.
    *   Add a variable `baseUrl` with the value `https://restful-booker.herokuapp.com`.
    *   The variables `token` and `bookingid` will be created and updated **dynamically** by the test scripts as you run the collection.
2.  **Run:** Select the environment and run the collection. The requests are designed to be run in order.
