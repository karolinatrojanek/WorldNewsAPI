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
| `analyze`   | boolean | query | No       | Whether to analyze the news. In response additionally you will see params like 'entities' and 'sentiment'  |                                     

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

**`GET /geo-coordinates`**

Retrieve the latitude and longitude of a location name. Given this information you can fill the location-filter parameter in the news search endpoint.
You can search most of city names, not country.

**Parameters**

| Name        | Type    | In    | Required | Description                        | 
| ----------- | ------- | ----- | -------- | -----------------------------------| 
| `location ` | string  | query | Yes      | Name of the location               | 
                           

**Status codes**

| Status code               | Description |
|---------------------------|---------------------------------------------------------------------------------------------------------|
| 200 OK                    | Indicates a successful response.                                                                        |
| 401 Unauthorized          | Lack of authorization/API key not provided.                                                             |
| 500 Internal Server Error | Indicates that something is wrong with location name param or  that this location coudn't be found      |

Example response:
```
{
    "latitude": 29.99883059999999,
    "longitude": -95.1765978,
    "city": "Atascocita, TX"
}

```

**`Search news`**

Search and filter news.

**Parameters**

| Name        | Type    | In    | Required | Description                        | 
| ----------- | ------- | ----- | -------- | -----------------------------------| 
| `authors ` | string  | query | No      | Just one author's name. Param doesn't accept 2 or more names separeted by comma.              |
| `earliest-publish-date ` | string  | query | No      | The news must have been published after this date. Date in format : YYYY-MM-DD HH:MM:SS . Hour is optional. When you don't give an hour, by default it is 00:00:00, when you don't give specific day, it is by default 01 etc.           |
| `entities ` | string  | query | No      | Filter news by entities, e.g. ORG:Tesla.             |
| `language ` | string  | query | No      | The ISO 6391 language code of the news, e.g. "en" for English.            |
| `latest-publish-date ` | string  | query | No      | The news must have been published before this date. Date in format : YYYY-MM-DD HH:MM:SS . Hour is optional. When you don't give an hour, by default it is 23:59:59, when you don't give specific day, it is by default the end of the month etc.           |          |
| `location-filter ` | string  | query | No      | Filter news by radius around a certain location. Format is "latitude,longitude,radius in kilometers", e.g. 51.050407, 13.737262, 100          |
| `max-sentiment ` | number  | query | No      | The maximal sentiment of the news in range [-1,1].       |
| `min-sentiment ` | number  | query | No      | The minimal sentiment of the news in range [-1,1].      |
| `news-sources ` | string  | query | No      | A comma-separated list of news sources from which the news should originate, e.g. https://www.bbc.co.uk      |
| `number ` | number  | query | No      | The number of news to return in range [1,100]      |
| `offset ` | number  | query | No      | The number of news to skip in range [0,1000]      |
| `sort ` | string  | query | No      | The sorting criteria. (publish-time or sentiment)     |
| `sort-direction ` | string  | query | No      | Whether to sort asc or desc.     |
| `source-countries ` | string  | query | No      | A comma-separated list of ISO 3166 country codes from which the news should originate, e.g. uk,us.   |
| `text  ` | string  | query | No      | The text to match in the news content.  |

**Status codes**

| Status code               | Description |
|---------------------------|---------------------------------------------------------------------------------------------------------|
| 200 OK                    | Indicates a successful response.                                                                        |
| 401 Unauthorized          | Lack of authorization/API key not provided.                                                             |
| 500 Internal Server Error | Indicates that something is wrong with params      |

Example response:
```
{
            "id": 119358598,
            "title": "And Just Like That: Kim Cattrall to reprise role of Samantha Jones in Sex and the City spin-off",
            "text": "Kim Cattrall, known for her role as Samantha Jones in Sex and the City, will return to screens as the PR manager in series spin-off And Just Like That. The Liverpool born actress will resume the role in the finale of the second season, Variety reports. (...)",
            "url": "https://www.edinburghnews.scotsman.com/read-this/kim-cattrall-to-reprise-sex-and-the-city-role-in-and-just-like-that-4165800",
            "image": "https://www.edinburghnews.scotsman.com/jpim-static/image/2023/06/01/12/GettyImages-1488691591.jpg?width=1200&enable=upscale",
            "publish_date": "2023-06-01 13:32:28",
            "author": "Charlotte Hawes",
            "language": "en",
            "source_country": "gb",
            "sentiment": -0.193

}
