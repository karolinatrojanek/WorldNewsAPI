 # World News API

This API allows you to access to thousands of news sources in over 50 languages from over 150 countries. News are semantically tagged allowing for semantic news search like never before.

The API is available at https://api.apilayer.com/world_news

**I found some mistakes in documentation provided on the site https://apilayer.com/marketplace/world_news-api#endpoints, documentation below is altered version of it after API testing.**

## API Authentication

All requests made to the API must hold a custom HTTP header named "apikey".
API requests can be made over HTTPS or HTTP. 
API requests without authentication will also fail.

## Endpoints

**`GET /extract-news`**

Extract a news article from a website to a well structure JSON object.

**Parameters**

| Name        | Type    | In    | Required | Description                                                                                                | 
| ----------- | ------- | ----- | -------- | -----------------------------------------------------------------------------------------------------------| 
| `url `      | string  | query | Yes      | Source url, any site with news which we want to retrive.                                                   | 
| `analyze`   | boolean | query | No       | Whether to analyze the news. In response additionally you will see params like 'entities' and 'sentiment'  |                                      | 

**Status codes**

| Status code               | Description |
|---------------------------|-------------------------------------------------------------------------|
| 200 OK                    | Indicates a successful response.                                        |
| 401 Unauthorized          | Lack of authorization/API key not provided.                             |
| 500 Internal Server Error | Indicates that something is wrong with URL                              |

Status 200 OK can appears even if URL in params not exists or has an error (status 500 appears only when you tape nothing after 'http//'

Example response:
```
{
    "title": "BBC Homepage",
    "text": "OceanGate: A maverick, rule-breaking founder and a tragic end Stockton Rush wanted to be known as an innovator. It didn't seem to matter how he did it.",
    "url": "https://www.bbc.com/",
    "image": "https://ichef.bbc.co.uk/wwhp/144/cpsprodpb/144E9/production/_130177138_5a8402bb-5f1b-4019-9e44-630d787913a2.jpg",
    "author": "Joe Tidy",
    "language": "en",
    "sentiment": -0.823,
    "entities": []
}
```
