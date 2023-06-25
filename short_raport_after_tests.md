# Short raport after tests
Below I gathered some remarks about failed endpoint's tests.

## Endpoints

**`GET /extract-news`**

Parameter 'analyze' is not required. Without it, or when the param has different value, like e.g. 'false'- we still have status 200 OK.
With 'analyze=true' in query params we just have another value in response - 'en

