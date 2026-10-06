# API Test Cases - JSONPlaceholder

## Execution summary

**10 test cases: 9 PASS, 1 FAIL.** I checked these requests manually in Postman.

Expected and Actual results below come from my test notes. The request data matches the exported collection. PASS and FAIL are manual results; the collection has no automated assertions or saved response examples.

## Common setup

- Import the supplied collection into Postman and have an internet connection.
- Base URL: `https://jsonplaceholder.typicode.com`.
- No authentication or environment file is required.
- Requests with bodies use **raw → JSON**. Keep the saved values, including the intentional syntax error in TC-API-009.
- Existing-user cases use ID `2`; the unknown-ID case uses `999`.
- Write operations are simulated and do not persist. Each case checks its own immediate response and does not depend on a previous write.

## Test index

| ID | Test | Method | Status |
|---|---|---|---|
| TC-API-001 | Get Users | GET | **PASS** |
| TC-API-002 | Get Single User | GET | **PASS** |
| TC-API-003 | Get Non-Existing User | GET | **PASS** |
| TC-API-004 | Create User | POST | **PASS** |
| TC-API-005 | Update User | PUT | **PASS** |
| TC-API-006 | Partially Update User | PATCH | **PASS** |
| TC-API-007 | Delete User | DELETE | **PASS** |
| TC-API-008 | Filter Users by Username | GET | **PASS** |
| TC-API-009 | Create User With Invalid JSON | POST | **FAIL** |
| TC-API-010 | Filter Users by Non-Existing Username | GET | **PASS** |

## Test details

### TC-API-001 - Get Users

**Type:** Positive  
**Purpose:** Retrieve the users collection.

**Request**

```http
GET https://jsonplaceholder.typicode.com/users
```

**Body:** none.

**Steps**

1. Open `TC-API-001 - Get Users` in the imported collection.
2. Check the saved method and URL, then select **Send**.
3. Inspect the HTTP status and response body against the expected result below.

**Expected Result:** API returns `200 OK` and a list of users.

**Actual Result:** API returned `200 OK` with a list of users containing fields such as `id`, `name`, `username`, and `email`.

**Status:** **PASS**

### TC-API-002 - Get Single User

**Type:** Positive  
**Purpose:** Retrieve an existing user by ID.

**Request**

```http
GET https://jsonplaceholder.typicode.com/users/2
```

**Body:** none.

**Steps**

1. Open `TC-API-002 - Get Single User` in the imported collection.
2. Check the saved method and URL, then select **Send**.
3. Inspect the HTTP status and response body against the expected result below.

**Expected Result:** API returns `200 OK` and the user with `id: 2`.

**Actual Result:** API returned `200 OK`. User `id` was `2`, name was `Ervin Howell`, and email was `Shanna@melissa.tv`.

**Status:** **PASS**

### TC-API-003 - Get Non-Existing User

**Type:** Negative  
**Purpose:** Check the response for a user ID that does not exist.

**Request**

```http
GET https://jsonplaceholder.typicode.com/users/999
```

**Body:** none.

**Steps**

1. Open `TC-API-003 - Get Non-Existing User` in the imported collection.
2. Check the saved method and URL, then select **Send**.
3. Inspect the HTTP status and response body against the expected result below.

**Expected Result:** API returns `404 Not Found` because user `999` does not exist.

**Actual Result:** API returned `404 Not Found` with a response body recorded as empty.

**Status:** **PASS**

**Note:** The exact raw response body was not saved. My note describes it as empty.

### TC-API-004 - Create User

**Type:** Positive  
**Purpose:** Submit a new user and inspect the simulated creation response.

**Request**

```http
POST https://jsonplaceholder.typicode.com/users
```

**Body** (raw JSON)

```json
{
  "name": "Aleksandar Test",
  "username": "aradovanovic",
  "email": "aleksandar.test@example.com"
}
```

**Steps**

1. Open `TC-API-004 - Create User` in the imported collection.
2. Check the saved method, URL and body, then select **Send**.
3. Inspect the HTTP status and response body against the expected result below.

**Expected Result:** API returns `201 Created`, returns the submitted user data, and assigns a new ID.

**Actual Result:** API returned `201 Created`, returned the submitted user data, and assigned `id: 11`.

**Status:** **PASS**

### TC-API-005 - Update User

**Type:** Positive  
**Purpose:** Send a PUT request for user 2 with the updated name and the supplied object.

**Request**

```http
PUT https://jsonplaceholder.typicode.com/users/2
```

**Body** (raw JSON)

```json
{
  "id": 2,
  "name": "Ervin Howell Updated",
  "username": "Antonette",
  "email": "Shanna@melissa.tv",
  "address": {
    "street": "Victor Plains",
    "suite": "Suite 879",
    "city": "Wisokyburgh",
    "zipcode": "90566-7771"
  },
  "phone": "010-692-6593 x09125",
  "website": "anastasia.net"
}
```

**Steps**

1. Open `TC-API-005 - Update User` in the imported collection.
2. Check the saved method, URL and body, then select **Send**.
3. Inspect the HTTP status and response body against the expected result below.

**Expected Result:** API returns `200 OK`, keeps `id: 2`, and returns the updated name `Ervin Howell Updated`.

**Actual Result:** API returned `200 OK`. User ID remained `2`, the name was changed to `Ervin Howell Updated`, and the submitted data was returned correctly.

**Status:** **PASS**

**Note:** The submitted object does not include `company` or `address.geo`.

### TC-API-006 - Partially Update User

**Type:** Positive  
**Purpose:** Send only the email field in a PATCH request for user 2.

**Request**

```http
PATCH https://jsonplaceholder.typicode.com/users/2
```

**Body** (raw JSON)

```json
{
  "email": "new.email@example.com"
}
```

**Steps**

1. Open `TC-API-006 - Partially Update User` in the imported collection.
2. Check the saved method, URL and body, then select **Send**.
3. Inspect the HTTP status and response body against the expected result below.

**Expected Result:** API returns `200 OK`, keeps `id: 2`, and updates only the requested email field.

**Actual Result:** API returned user `id: 2` with the email changed to `new.email@example.com`. The update behaved as expected.

**Status:** **PASS**

**Note:** I recorded PASS, but did not separately record the HTTP status code in the Actual result.

### TC-API-007 - Delete User

**Type:** Positive  
**Purpose:** Inspect the response to a deletion request for user 2.

**Request**

```http
DELETE https://jsonplaceholder.typicode.com/users/2
```

**Body:** none.

**Steps**

1. Open `TC-API-007 - Delete User` in the imported collection.
2. Check the saved method and URL, then select **Send**.
3. Inspect the HTTP status and response body against the expected result below.

**Expected Result:** API successfully processes deletion of user `2`.

**Actual Result:** API returned `200 OK` with an empty JSON object `{}`.

**Status:** **PASS**

### TC-API-008 - Filter Users by Username

**Type:** Positive  
**Purpose:** Filter the users collection by an existing username.

**Request**

```http
GET https://jsonplaceholder.typicode.com/users?username=Antonette
```

**Body:** none.

**Steps**

1. Open `TC-API-008 - Filter Users by Username` in the imported collection.
2. Check the saved method and URL, then select **Send**.
3. Inspect the HTTP status and response body against the expected result below.

**Expected Result:** API returns `200 OK` and only users matching `username=Antonette`.

**Actual Result:** API returned `200 OK` with one matching user: `id: 2`, username `Antonette`.

**Status:** **PASS**

### TC-API-009 - Create User With Invalid JSON

**Type:** Negative  
**Purpose:** Check how the API handles a request body with malformed JSON.

**Request**

```http
POST https://jsonplaceholder.typicode.com/users
```

**Body** (raw, intentionally invalid JSON)

```text
{
  "name": "Aleksandar Test",
  "username": "aradovanovic",
  "email": "aleksandar.test@example.com"
```

The closing `}` is intentionally missing. Keep it missing when repeating this negative test.

**Steps**

1. Open `TC-API-009 - Create User With Invalid JSON` in the imported collection.
2. Check the saved method, URL and body, then select **Send**.
3. Inspect the HTTP status and response body against the expected result below.

**Expected Result:** Invalid JSON should be rejected with a client error such as `400 Bad Request`.

**Actual Result:** API returned `500 Internal Server Error` and exposed a JSON parsing stack trace beginning with `SyntaxError: Expected ',' or '}'...`.

**Status:** **FAIL**

**Note:** TC-API-009 is recorded as a failed test based on the expected behavior defined for this practice scenario. It is not reported as a confirmed defect because JSONPlaceholder is a public mock API and no formal requirement specifies that malformed JSON must return HTTP 400.

### TC-API-010 - Filter Users by Non-Existing Username

**Type:** Negative - no matching data  
**Purpose:** Filter the users collection by a username with no matching user.

**Request**

```http
GET https://jsonplaceholder.typicode.com/users?username=NonExistingUser
```

**Body:** none.

**Steps**

1. Open `TC-API-010 - Filter Users by Non-Existing Username` in the imported collection.
2. Check the saved method and URL, then select **Send**.
3. Inspect the HTTP status and response body against the expected result below.

**Expected Result:** API returns `200 OK` with an empty array because no users match the filter.

**Actual Result:** API returned `200 OK` with `[]`, meaning zero matching users were found.

**Status:** **PASS**

See [notes and limitations](../notes/limitations.md) for details about the test records and JSONPlaceholder behavior.
