# **Representational State API** #
- a standardized software architectural style
- it's basically about communication
-------------------------------------------------------
## **SIMPLE / STANDARD** ##
- no need to worry how to format data
## **SCALABLE / STATELESS** ##
- as the service grows in complexity we can easily make modifications, **stateless** meaning we dont have to worry which data is in which state and keep track of that across client and server
## **HIGH PERFORMANCE / CACHEABLE** ##
- as service gets complex the performance stays high
------------------------------------------------------
- There will be an API endpoint, something like this: http://icecream.com/api/flavours
- **http://icecream.com/api** is called the network location
- **flavours** is what we called as the **resource**
- the main building bloks of the RESTFUL API is the **request** from client to server, and also the **response** from server to client
------------------------------------------------------
| REST        | HTTP METHODS|
| ----------- | ------ | 
| Create      | POST   | 
| Read        | GET    |
| Update      | PUT    | 
| Delete      | DELETE |
------------------------------------------------------
Building Blocks of **REQUEST**:
1. OPERATION (Create,Read, Update, Delete)
2. ENDPOINT
3. PARAMETERS / BODY
4. HEADERS (API key, authentication data, the format of the response data that we want, eg: JSON)

Building Blocks of **RESPONSE**: (typically in the form of JSON)
