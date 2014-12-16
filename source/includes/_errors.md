# Errors

The TapResearch API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Double check to make sure you are making a proper request.
401 | Unauthorized -- You do not have access to the resource you requested. Please make sure your authorization header is set correctly.
404 | Not Found -- The resource you have requested cannot be found.
422 | Unprocessable Entity - There was an error with your request. The response should always have a message detailing why an error has occurred.
500 | Internal Server Error -- We had a problem with our server. Please contact **api_support@tapresearch.com** if this problem persists.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.