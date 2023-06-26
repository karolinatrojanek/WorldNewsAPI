# Short raport after tests
Below I gathered some remarks about failed endpoint's tests.

## Endpoints

**`GET /extract-news`**

Parameter 'analyze' is not required. Without it, or when the param has different value, like e.g. 'false'- we still have status 200 OK.
With 'analyze=true' in query params we just have another value in response - ''entities' and 'sentiment'

**`GET /search-news`**

Optional parameter 'sort-direction' doesn't work properly, even with added another param 'sort'. In majority, yes, it works but there is always some mistake with order. 

