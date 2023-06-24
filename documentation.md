# World News API

This API allows you to access to thousands of news sources in over 50 languages from over 150 countries. News are semantically tagged allowing for semantic news search like never before

The API is available at https://api.apilayer.com/world_news

## API Authentication

All endpoints require authentication, they expect the API key to be provided as a query parameter named `apikey`.
All requests made to the API must hold a custom HTTP header named "apikey". Implementation differs with each programming language. Below are some samples.
All API requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without authentication will also fail.
