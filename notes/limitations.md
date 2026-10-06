# Notes and limitations

## Test records

I recorded the Expected / Actual / Status results during manual testing in Postman. The collection contains the saved methods, URLs, and request bodies.

The result was **9 PASS and 1 FAIL**. The collection has no automated assertions, and its `response` arrays are empty. Saved response examples are not included; the Actual entries summarize my manual observations.

- **TC-API-003:** my note describes the response body as empty. The exact raw response body was not saved.
- **TC-API-006:** my note records user `id: 2`, the changed email, and PASS. I did not separately record the HTTP status code in the Actual result; `200 OK` is the expected status.

Response times and an exact execution date were not recorded.

## Simulated changes

JSONPlaceholder simulates POST, PUT, PATCH, and DELETE operations without persisting the changes. Tests using `/users/2` are independent of the user returned by the create request. A later GET cannot confirm a stored change from these simulated writes. See the [official API guide](https://jsonplaceholder.typicode.com/).

TC-API-005 sends the object saved in the collection. It includes the updated name and other supplied fields, but does not contain `company` or `address.geo`.

## TC-API-009: invalid JSON

The request body intentionally omits its closing `}`. The API returned `500 Internal Server Error` and a JSON parsing stack trace beginning with `SyntaxError: Expected ',' or '}'...`. The full stack trace was not saved.

TC-API-009 is recorded as a failed test based on the expected behavior defined for this practice scenario. It is not reported as a confirmed defect because JSONPlaceholder is a public mock API and no formal requirement specifies that malformed JSON must return HTTP 400.

## Collection

The Postman Collection v2.1 export contains ten requests and is included without changes. It has no scripts, authentication configuration, variables, or external file dependencies. No separate environment file is needed.

The collection file itself is valid JSON. The invalid JSON for TC-API-009 is stored inside its request-body string.
