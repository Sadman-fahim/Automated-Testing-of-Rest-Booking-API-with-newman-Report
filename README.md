### **Rest Booking API Testing with Postman Newman**
This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API. 

### **Features**

- Tests for GET, POST, PUT requests
- Collection of tests covering different API endpoints
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations

## API Documentation:
https://documenter.getpostman.com/view/39704688/2sAYBSktho
  
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
  git clone https://github.com/Sadman-fahim/Automated-Testing-of-Rest-Booking-API-with-newman-Report.git
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
	var firstName=pm.variables.replaceIn("{{$randomFirstName}}")
	console.log(firstName)
	pm.environment.set("firstName",firstName)

	var LastName=pm.variables.replaceIn("{{$randomLastName}}")
	console.log(LastName)
	pm.environment.set("LastName",LastName)

	var Price=pm.variables.replaceIn("{{$randomInt}}")
	console.log(Price)
	pm.environment.set("Price",Price)

	//date
	const moment=require('moment')
	const today=moment()
	console.log(today.format("YYYY-MM-DD"))
	var checkin=today.add(3,'D').add(3,'M').format("YYYY-MM-DD")
	pm.environment.set("checkin",checkin)
	var checkout=today.add(3,'D').add(8,'M').format("YYYY-MM-DD")
	pm.environment.set("checkout",checkout)


	var deposit=pm.variables.replaceIn("{{$randomBoolean}}")
	console.log(deposit)
	pm.environment.set("deposit",deposit)



var needs=pm.variables.replaceIn("{{$randomProduct}}")
console.log(needs)
pm.environment.set("needs",needs)
```
  **Request Body:** 
 ```console 
  {
	  "firstname" : "{{firstName}}",
	  "lastname" : "{{lastName}}",
	  "totalprice" : {{Price}},
	  "depositpaid" : {{deposit}},
	  "bookingdates" : {
    	  "checkin" : "{{checkin}}",
    	  "checkout" : "{{checkout}}"
	  },
	  "additionalneeds" : "{{Needs}}"
  }
```
  **Response Body:**
 ```console 
  {
    "bookingid": 709,
    "booking": {
        "firstname": "Esperanza",
        "lastname": "Ferry",
        "totalprice": 608,
        "depositpaid": false,
        "bookingdates": {
            "checkin": "2025-02-23",
            "checkout": "2025-10-23"
        },
        "additionalneeds": "Tuna"
    }
}
```
 ## _**2. Get Booking Details By ID**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: GET
### Response Body:
 ```console 
{
    "firstname": "Esperanza",
    "lastname": "Ferry",
    "totalprice": 608,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2025-02-23",
        "checkout": "2025-10-23"
    },
    "additionalneeds": "Tuna"
}
```
## _**3. Create A Token For Authentication.**_
### Request URL: https://restful-booker.herokuapp.com/auth
### Request Method: POST
### Pre-request Script: None
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
    "token": "b671950701aff9d"
}
```

 ## _**4. Update the Booking Details**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: PUT
### Pre-request Script:
```console 
    var updated_firstName= pm.variables.replaceIn("{{$randomFirstName}}")
	pm.environment.set("updated_firstName",updated_firstName)

	//last name update
	var updated_lastName= pm.variables.replaceIn("{{$randomLastName}}")
	pm.environment.set("updated_lastName",updated_lastName)

	//update price
	var updated_price= pm.variables.replaceIn("{{$randomInt}}")
	pm.environment.set("updated_price",updated_price)

	//update deposit
	var updated_deposit= pm.variables.replaceIn("{{$randomBoolean}}")
	pm.environment.set("updated_deposit",updated_deposit)

	//update date
	const moment=require('moment')
	const today=moment()
	var updated_checkin=today.add(3,'D').add(3,'M').format("YYYY-MM-DD")
	pm.environment.set("updated_checkin",updated_checkin)

	// checkout
	const updated_checkout = today.add(7, 'days').format("YYYY-MM-DD")
	pm.environment.set("updated_checkout", updated_checkout)
	console.log("Check-out Date:", updated_checkout)


	//update additional needs
	var updated_needs=pm.variables.replaceIn("{{$randomProduct}}")
	pm.environment.set("updated_needs",updated_needs)

```
  **Request Body:** 
 ```console 
  {
	"firstname" : "{{updated_firstName}}",
	"lastname" : "{{updated_lastName}}",
	"totalprice" : {{updated_price}},
	"depositpaid" :{{updated_deposit}} ,
	"bookingdates" : 
	{
	"checkin" : "{{updated_checkin}}",
	"checkout" : "{{updated_checkout}}"
	},
	"additionalneeds" : "{{updated_needs}}"
}
```
  **Response Body:**
 ```console 
  {
		"firstname": "Eudora",
		"lastname": "Schmeler",
		"totalprice": 413,
		"depositpaid": true,
		"bookingdates":
		{
        "checkin": "2025-02-23",
        "checkout": "2025-03-02"
		},
		"additionalneeds": "Ball"
  }
```

  

## Run Command:  
- Run Command for Console: 
```console 
newman run FAHIM_SADMAN_TALUKDER.postman_collection.json -e FAHIM_SADMAN_TALUKDER.postman_environment.json 
```
- Run Command for Report: 
```console 
newman run FAHIM_SADMAN_TALUKDER.postman_collection.json -e FAHIM_SADMAN_TALUKDER.postman_environment.json -r htmlextra
```

## Newman Report Summary:
![Newman Report Summary]![Report](https://github.com/user-attachments/assets/d70a6db9-5a87-47b8-b3a1-561100bb7e94)

![Newman Report Summary]![Report1](https://github.com/user-attachments/assets/28463ea5-bee4-4174-8356-b7b0acc69596)

![image]![Screenshot (32)](https://github.com/user-attachments/assets/cf4b14bf-8c26-47e9-8e19-f066034032d0)

![image]!![Screenshot (33)](https://github.com/user-attachments/assets/9dca6217-2615-442a-9fef-d6a58be88862)


