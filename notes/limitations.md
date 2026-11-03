# Notes and limitations

## Test records

I recorded the Expected / Actual / Status results during manual testing in Postman. The collection contains the saved methods, URLs, and request bodies.

The current result is **11 executed test cases: 10 PASS and 1 FAIL**. The collection has no automated assertions, and its `response` arrays are empty. Saved response examples are not included; the Actual entries summarize my manual observations.

- **TC-API-003:** my note describes the response body as empty. The exact raw response body was not saved.
- **TC-API-006:** I repeated the PATCH request and confirmed HTTP `200 OK`, user `id: 2`, and email "new.email@example.com" in the response. The updated Actual Result is recorded as PASS.
- **TC-API-011:** I checked HTTP `200 OK`, user `id: 2`, and the nested fields `address.city` ("Wisokyburgh") and `company.name` ("Deckow-Crist"). The result is recorded as PASS.

Response times and exact execution dates are not included in these repository test records.

## Simulated changes

JSONPlaceholder simulates POST, PUT, PATCH, and DELETE operations without persisting the changes. Tests using `/users/2` are independent of the user returned by the create request. A later GET cannot confirm a stored change from these simulated writes. See the [official API guide](https://jsonplaceholder.typicode.com/).

TC-API-005 sends the object saved in the collection. It includes the updated name and other supplied fields, but does not contain `company` or `address.geo`.

## TC-API-009: invalid JSON

The request body intentionally omits its closing `}`. The API returned `500 Internal Server Error` and a JSON parsing stack trace beginning with `SyntaxError: Expected ',' or '}'...`. The full stack trace was not saved.

TC-API-009 is recorded as a failed test based on the expected behavior defined for this practice scenario. It is not reported as a confirmed defect because JSONPlaceholder is a public mock API and no formal requirement specifies that malformed JSON must return HTTP 400.

## Collection

The Postman Collection v2.1 file contains eleven saved requests, including TC-API-011. It has no automated test scripts, authentication configuration, variables, or external file dependencies. No separate environment file is needed.

The collection file itself is valid JSON. The invalid JSON for TC-API-009 is stored inside its request-body string.
