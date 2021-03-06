# Braze Meals API

## Introduction

To personalise messages in Braze, the Meals API can be used to get information about the users upcoming/ planned meals for the next day.
Overview

Method: GET
To access the correct information per user, the user_id is required in the cURL.

## Authentication

The API can be called with basic authentication. Credentials are added to Braze.
Status / Error Codes

Status 200 - Everything is working

Status 401 - Authentication failed 

## Rate limit

There is no limit on that endpoint in particular, but the whole API has a limit of 900 requests/5 minutes
(The endpoint can be removed if needed)

## Use
### cURL: 
http://8fit.com/api/1/connected_contents/tomorrow_pending_meals.json?user_id={${user_id}}}

### Params
user_id 
3f35xx78-658x-4x9x-x527-4e0299x5x230 

## Output

```{
 "dinner": {
    "id": "15e9e275-10bf-418a-9538-64fa0fe99ae1",   
    "recipe_id": "43a9dfcf-95e1-4d43-8c40-83d1d2c831ca",    
    "servings": 1,    
    "recipe_name": "Prosciutto, persimmon & arugula salad ",    
    "recipe_image_url": "img url"
  },
  "lunch": {
    "id": "11eb563b-8942-4256-9508-9ccd0d0c744f",
    "recipe_id": "543d3f09356632000e1e0100", 
    "servings": 1,    
    "recipe_name": "Beef & broccoli with rice",
    "recipe_image_url": "img url"
  },
  "breakfast": { 
    "id": "d31f7446-21be-4b34-90ad-365dbd492e9d",   
    "recipe_id": "572870e58198f10011a6bfe6",   
    "servings": 1,    
    "recipe_name": "Chicken breast & ricotta cheese on bread",    
    "recipe_image_url": "img url"
  },
  "date": "August 28, 2018", 
  "total": 3
}
```

## Use In Braze

{% connected_content http://8fit.com/api/1/connected_contents/tomorrow_pending_meals.json?user_id={{${user_id}}} :save meals :basic_auth Meals_Endpoint %} {% if {{meals.total}} < 1 %} 
{% abort_message('Not enough meals Results') %} {% endif %} 

Call the API with “connected_content”, save it in a variable and specify the authentication.
In this case: If the results are less than 1, the message is not being send. The usable parameters within the message are:
* Recipe name
* Servings
* Recipe image URL 
* Recipe ID for the deeplink

