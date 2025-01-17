### **Rest Booking API Testing with Postman Newman**
This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API. 

### **Features**

- Tests for GET, POST, PUT, DELETE requests
- Collection of tests covering different API endpoints
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations

- ## API Documentation:
- https://documenter.getpostman.com/view/34055865/2sAYQZJsbv
  
### **Technology used:**
- Postman
- Newman

### **Prerequisite:**
- Node Js
- Newman
- Newman Html Report Library

### **Installation**

1. Postman: If you haven't already, [download and install Postman.](https://www.postman.com/downloads/)
2. Clone the repository:
 ```console 
  git clone https://github.com/ahsanhabib082/Api_Testing.git
```
3. Import the Postman collection:
    - Open Postman.
    - Click on the Import button.
    - Select the file from the repository.
4. Import the Postman environment:
    - In Postman, click on the gear icon in the top right corner.
    - Select **Import** and choose the file.
5. Newman and Report Installation Process:
    - Newman Install Command:
     ```console 
      npm install -g newman
    ```
    - Newman Html Report Install Command:
     ```console 
      npm install -g newman-reporter-htmlextra
    ```


 ### **Usage**
1. Select Environment:
    -   In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.
3. Run Collection:
    -   Select the imported collection from the Collections sidebar.
    -   Click on the Runner button to open the collection runner.
    -   Select the desired environment.
    -   Click Start Test to run the collection.
8. View Results:
    -   Once the tests are complete, view the results in the Runner tab.
    -   Detailed test results can be viewed for each request.

## **Testing**

## Test Case Scenarios:

## _**1. Create New Booking**_

### Request URL: https://restful-booker.herokuapp.com/booking/
### Request Method: POST
### Pre-request Script:
```console
var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
console.log(firstName)
pm.environment.set("firstName",firstName)



//Last Name
var lastName = pm.variables.replaceIn("{{$randomLastName}}")
pm.environment.set("lastName",lastName)


// Total price
var totalPrice = pm.variables.replaceIn("{{$randomInt}}")
pm.environment.set("totalPrice",totalPrice)


//DepositPaid
var depositpaid = pm.variables.replaceIn("{{$randomBoolean}}")
pm.environment.set("depositpaid",depositpaid)



//Date
const moment = require ('moment')
const today = moment()
//console.log(today.add(1, 'd').add(3, 'M').format("YYYY-MM-DD"))

var checkin = today.add(1, 'd').add(3, 'M').format("YYYY-MM-DD")
pm.environment.set("checkin", checkin)


var checkout = today.add(1, 'd').add(3, 'M').format("YYYY-MM-DD")
pm.environment.set("checkout", checkout)



var additionalneeds = pm.variables.replaceIn("{{$randomProduct}}")
pm.environment.set("additionalneeds",additionalneeds)
```

 **Request Body:** 
 ```console 

{
	"firstname" : "{{firstName}}",
	"lastname" : "{{lastName}}",
	"totalprice" : {{totalPrice}},
	"depositpaid" : {{depositpaid}},
	"bookingdates" : {
    	"checkin" : "{{checkin}}",
    	"checkout" : "{{checkout}}"
	},
	"additionalneeds" : "{{additionalneeds}}"
}
```

 **Response Body:**
 ```console
{
    "bookingid": 5112,
    "booking": {
        "firstname": "Camylle",
        "lastname": "Fay",
        "totalprice": 289,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2025-04-18",
            "checkout": "2025-07-19"
        },
        "additionalneeds": "Bacon"
    }
}
```
## _**2. Get Booking Details By ID**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: GET
### Response Body:
 ```console
{
    "firstname": "Camylle",
    "lastname": "Fay",
    "totalprice": 289,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2025-04-18",
        "checkout": "2025-07-19"
    },
    "additionalneeds": "Bacon"
}
```
### Request Body:
```console

{
	"firstname" : "{{firstName}}",
	"lastname" : "{{lastName}}",
	"totalprice" : {{totalPrice}},
	"depositpaid" : {{depositpaid}},
	"bookingdates" : {
    	"checkin" : "{{checkin}}",
    	"checkout" : "{{checkout}}"
	},
	"additionalneeds" : "{{additionalneeds}}"
}
```
### Response Body:
```console
{
    "firstname": "Camylle",
    "lastname": "Fay",
    "totalprice": 289,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2025-04-18",
        "checkout": "2025-07-19"
    },
    "additionalneeds": "Bacon"
}
```

## _**3. Create A Token For Authentication.**_
### Request URL: https://restful-booker.herokuapp.com/auth
### Request Method: POST
### Pre-request Script: None
### Post-request Script:
```console
var jsonData = pm.response.json()
pm.environment.set("acess_token",jsonData.token)
```
### Request Body:
 ```console 
{
	"username": "admin",
	"password": "password123"
}
```
  **Response Body:**
 ```console 
{
    "token": "06eb798bf6f2caa"
}
```

