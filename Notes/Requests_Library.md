20231016 - 20:40

Status: #idea

Tags: [[Python]]

# Requests

The requests library is a Python library for making HTTP requests. 

Most common HTTP requests are: 
* GET - Requests to read data from a web server. Returns 200 on success. 
* POST - Requests to send data to a server. Returns 201 on success. 
* PUT - Requests to modify data on a server. 
* PATCH - Requests to modify PART of the data. 
* DELETE - Requests to delete data on server. 

HTTP requests will return a status code depending on if the request was a success or not. 
* 100 - 199 : Informational responses
* 200 - 299: Successful responses
* 300-399: Redirection messages
* 400-499: Client error responses
* 500-599: Server error responses

To make a request using Python the easiest way is to use the requests library. 

``` Python
request_object = requests.get("https://www.facebook.com/")
```

Here are a few ways of accessing important attributes of the request object: 

``` Python
status_code = requst_object.status # The status code from the request
text = request_object.text # The text as a string from the requst object
binary_content = request_object.content # Returns a binary representation of the content in the requst
json_content = request_object.json() # Returns the request object cast to a dictionary with keys and values
header = request_object.headers # Returns the header of the request object

```

## Questions for stripe interview
1. Are there any specific programming languages, frameworks or libraries you wish you had known before starting work at Stripe? In other words, are there any specific things I should know so I can hit the ground running if I'm lucky enough to land this internship? 
2. How big is the team you work on, do you guys work agile, with daily stand ups etc? 
3. Do you know what common intern tasks have been? 
4. What is the best part of working at Stripe?
5. Do you think this interview captures what I could expect of a workday at Stripe?
6. How long have you been at Stripe?
7. What does the onboarding process look like? 
8. What would you say is the most important attribute to be successful as a software engineer at Stripe? 
9. How do interns usually fit into teams? 
10. Do you work with Agile?
11. Would you say there are good growth opportunities at Stripe?
\-\-\-
# References
* https://www.geeksforgeeks.org/different-kinds-of-http-requests/