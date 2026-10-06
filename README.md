# API Testing Practice - JSONPlaceholder

I used Postman to test ten requests on the JSONPlaceholder `/users` resource. For each test, I recorded the expected result, the actual response, and a PASS or FAIL status.

The cases cover reading users, requesting a user that does not exist, creating and updating a user, deleting a user, filtering by username, and sending invalid JSON.

## Results

| Total test cases | PASS | FAIL |
|---|---|---|
| 10 | 9 | 1 |

TC-API-009 failed against the expectation defined for this practice scenario. I expected a client error such as `400 Bad Request` for invalid JSON, but the API returned `500 Internal Server Error` with a JSON parsing stack trace. This is not reported as a confirmed defect because no formal requirement specifies an HTTP 400 response for this public mock API.

These results come from my manual test notes. The collection contains saved requests, with no automated assertions or saved response examples.

## Repository structure

```text
api_testing_practice/
├── README.md
├── test-cases/
│   └── api-test-cases.md
├── postman/
│   └── QA Portfolio - API Testing.postman_collection.json
└── notes/
    └── limitations.md
```

- [Test cases](test-cases/api-test-cases.md): steps, request data, and Expected / Actual / Status for all ten tests.
- [Postman collection](postman/QA%20Portfolio%20-%20API%20Testing.postman_collection.json): the exported Collection v2.1 file.
- [Notes and limitations](notes/limitations.md): API behavior and details about the recorded results.

## Run the requests

1. Import `postman/QA Portfolio - API Testing.postman_collection.json` into Postman.
2. Open **QA Portfolio - API Testing**. No environment file or API key is required.
3. Select a request and check its method, URL, and body against the matching test case.
4. Select **Send** and compare the status code and response body with the expected result.
5. For TC-API-009, keep the missing closing brace. It is the intended invalid input.

The base URL is `https://jsonplaceholder.typicode.com`. All URLs are saved in full. Requests with bodies use **raw → JSON**; Postman sets a content header based on that format. See [Postman's request body documentation](https://learning.postman.com/docs/sending-requests/create-requests/parameters/).

The checks are manual. The collection has no scripts that automatically decide PASS or FAIL. If repeating the tests, record the new results separately from this session.

## Limitations

JSONPlaceholder simulates POST, PUT, PATCH, and DELETE operations. Changes are returned in the response but are not persisted. I checked the immediate responses, not changes stored on the server. See the [official JSONPlaceholder guide](https://jsonplaceholder.typicode.com/).

This project covers basic requests and response inspection. Authentication, performance, security, and database testing are outside its scope.
