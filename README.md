# pitplay-owner-backend-guide
## Table of Contents
1. [Create Ground Api](#ground-creation-api)
2. [Update Ground](#update-ground)
3. [Get All Ground List Api](#get-all-grounds)
4. [Show Ground Details Api](#show-ground-details)
5. [Delete Ground Api](#delete-ground-api)
6. [send Otp to mobile number](#send-otp-to-mobile-number-api)
7. [verify otp](#verify-otp)
8. [Bookings List](#bookings-list)
9. [Create Booking](#create-booking)
10. [Show Booking Details](#show-booking-details)


### **Ground Creation API**
### Endpoint:

- **URL:** **`/api/app/ground/addGround`**
- **Method:** POST

### Request Body:

- **Content Type:** JSON

### **Required Fields:**

1. **`ground_name`**: String
    - Description: Name of the ground.
2. **`ground_description`**: String
    - Description: Description of the ground.
3. **`ground_address`**: String
    - Description: Address of the ground.
4. **`city`**: String
    - Description: City where the ground is located.
5. **`state`**: String
    - Description: State where the ground is located.
6. **`pincode`**: Number
    - Description: Pincode of the ground location.
7. **`latitude`**: Number
    - Description: Latitude coordinate of the ground location.
8. **`longitude`**: Number
    - Description: Longitude coordinate of the ground location.
9. **`contact_no`**: String
    - Description: Contact number of the ground.
10. **`ground_opening`**: String
    - Description: Opening time of the ground.
11. **`ground_closing`**: String
    - Description: Closing time of the ground.
12. **`price_per_hour`**: Number
    - Description: Price per hour for using the ground.
13. **`price_per_day`**: Number
    - Description: Price per day for using the ground.
14. **`night_price`**: Number
    - Description: Price for using the ground during night hours.
15. **`weekend_per_day`**: Number
    - Description: Price per day for using the ground on weekends.
16. **`weekend_per_hour`**: Number
    - Description: Price per hour for using the ground on weekends.
17. **`weekend_night_price`**: Number (optional)
    - Description: Price for using the ground during night hours on weekends.
18. **`night_start_time`**: String (optional)
    - Description: Start time of night hours for the ground.
19. **`size_of_ground`**: String (optional)
    - Description: Size of the ground.
20. **`user_id`**: String
    - Description: ID of the user who owns the ground.
21. **`ground_service`**: Array of Objects
    - Description: Services available at the ground.
    - Fields:
        - **`service_id`**: String (Reference ID of the service)
        - **`service_name`**: String (Name of the service)
        - **`service_price_hour`**: Number (price per hour for the service)
        - **`service_price_day`**: Number (price per day for the service)
        - **`status`**: String (availability status of the service: "available" or "unavailable")
22. **`ground_sports`**: Array of Objects
    - Description: Sports facilities available at the ground.
    - Fields:
        - **`sports_id`**: String (Reference ID of the sports facility)
        - **`sports_name`**: String (Name of the sports facility)
        - **`status`**: String (availability status of the sports facility: "available" or "unavailable")
23. **`status`**: String
    - Description: availability status of the ground: "available" or "unavailable" or "booked”.
   
24. **`images`**: Array of image file

    
### Response:

- **Content Type:** JSON

### **Success Response:**

- **Status Code:** 200 OK
- **Body:**
    
    ```json
    
    {
      "success": true,
      "data": {
        "ground_name": "Sample Ground",
        "ground_description": "Description of the sample ground",
        "ground_address": "Sample Address",
        "pincode": 123456,
        "city": "Sample City",
        "state": "Sample State",
        "latitude": 12.345,
        "longitude": 67.89,
        "contact_no": "1234567890",
        "ground_opening": "09:00 AM",
        "ground_closing": "06:00 PM",
        "price_per_hour": 50,
        "price_per_day": 300,
        "night_price": 100,
        "weekend_per_day": 400,
        "weekend_per_hour": 60,
        "weekend_night_price": 150,
        "night_start_time": "06:00 PM",
        "size_of_ground": "Large",
        "user_id": "user_id_123",
        "status": "available",
        "ground_service": [
          {
            "service_id": "service_id_1",
            "service_name": "Service 1",
            "service_price_hour": 10,
            "service_price_day": 50,
            "status": "available"
          },
          {
            "service_id": "service_id_2",
            "service_name": "Service 2",
            "service_price_hour": 20,
            "service_price_day": 100,
            "status": "available"
          }
        ],
        "ground_sports": [
          {
            "sports_id": "sports_id_1",
            "sports_name": "Football",
            "status": "available"
          },
          {
            "sports_id": "sports_id_2",
            "sports_name": "Basketball",
            "status": "available"
          }
        ],
        "images": [
          "image_url_1",
          "image_url_2"
        ],
        "status" : "available"
      },
      "message": "Ground created successfully!"
    }
    
    ```
    

### **Error Response:**

- **Status Code:** 400 Bad Request
- description : This error indicates that one or more required fields are missing in the request body. It prompts the client to provide values for all mandatory fields.
- **Body:**
   ```json
  {
  "success": false,
  "message": "Required field is missing!"
  }
  ```
   
- **Status Code:** 400 Bad Request
- Discription : This error occurs when trying to create a ground with a value for a field that already exists in the database and is meant to be unique. It informs the client that the provided value for the field is a duplicate and cannot be accepted.
- **Body:**
   ```json
  {
  "success": false,
  "message": "Duplicate key 'field value' already exists!"
  }
  ```
   
- **Status Code:** 400 Bad Request
- Description : This error is triggered by validation errors, such as incorrect data types or values failing validation rules. It returns an array of validation error messages to help the client understand what specific issues need to be addressed.
- **Body:**
   ```json
  {
  "success": false,
  "message": ["Validation error message 1", "Validation error message 2"]
  }
  ```
   
- **Status Code:** 500 Internal Server Error
- Description : This error is a generic indication that something unexpected happened on the server-side while processing the request. The error message provides additional details about the nature of the error, which can be useful for debugging purposes.
- **Body:**
   ```json
  {
  "success": false,
  "error": "Error message",
  "message": "Internal Server Error"
  }
  ```
## Update Ground

This endpoint is used to update details of a specific ground.

### Request

- **Method:** POST
- **URL:** `/api/app/ground/updateGround`
- **Body Parameters:**
  - `ground_id`: ID of the ground to be updated (required)
  - `ground_name`: Name of the ground (required)
  - `ground_description`: Description of the ground (required)
  - `ground_address`: Address of the ground (required)
  - `city`: City where the ground is located (required)
  - `state`: State where the ground is located (required)
  - `pincode`: Pincode of the ground location (required)
  - `latitude`: Latitude coordinate of the ground location (required)
  - `longitude`: Longitude coordinate of the ground location (required)
  - `contact_no`: Contact number of the ground (required)
  - `ground_opening`: Opening time of the ground (required)
  - `ground_closing`: Closing time of the ground (required)
  - `price_per_hour`: Price per hour for using the ground (required)
  - `price_per_day`: Price per day for using the ground (required)
  - `weekend_per_day`: Weekend price per day for using the ground (required)
  - `weekend_per_hour`: Weekend price per hour for using the ground (required)
  - `weekend_night_price`: Weekend night price for using the ground (required)
  - `night_start_time`: Start time of night rates for using the ground (required)
  - `size_of_ground`: Size of the ground (required)
  - `user_id`: ID of the user associated with the ground (required)
  - `ground_service`: Array of services available at the ground (required)
  - `ground_sports`: Array of sports available at the ground (required)
  - `status`: Status of the ground (required)
  - `night_price`: Price for using the ground during night time (required)
  - `images`: array of new Images of the ground (optional)
  - `deleted_images`: array of deletd_images (which you want to delete)

### Response

- **Status Code:**
  - 200 OK: Ground details updated successfully.
  - 400 Bad Request: One or more required fields are missing.
  - 500 Internal Server Error: An error occurred while processing the request.

- **Response Body (Success):**

```json
{
  "success": true,
  "data": { ...updatedGroundDetails },
  "message": "Ground updated successfully!"
}
```
## Get All Grounds

This endpoint retrieves a paginated list of all available grounds.

### Request

- **Method:** GET
- **URL:** `/api/app/ground/groundList`
- GET `/api/app/ground/groundList?page=1&pageSize=10&includeTotal=true`
- **Query Parameters:**
    - page (Number, optional): Specifies the page number for pagination (default: 1).
    - pageSize (Number, optional): Specifies the number of items per page (default: 10).
    - search (String, optional): Performs a case-insensitive search across ground name, address, state, and city.

### Response
- pagination: Object containing pagination details.
- pageSize: Number of grounds per page.
- page: Current page number.
- totalPages: Total number of pages.
- totalGrounds: Total count of grounds (if requested).
- prevPageLink: Link to the previous page if available, otherwise null.
- nextPageLink: Link to the next page if available, otherwise null.
- **Status Code:**
    - 200 OK: Successfully retrieved the list of grounds.
    - 404 Not Found: No grounds available.
    - 400 Bad Request: Internal Server Error.
- **Response Body (Success):**

```json
{
  "success": true,
  "data": [
      {
            "_id": "6622273395b62e444a583951",
            "ground_name": "dfsd",
            "ground_description": "This is a sample ground description.",
            "ground_address": "123 Sample Street",
            "pincode": 12345,
            "country": "India",
            "city": "Surat",
            "state": "Gujrat",
            "latitude": 21.2789885,
            "longitude": 72.7989643,
            "contact_no": "123-456-7890",
            "ground_opening": "11:00 PM",
            "ground_closing": "10:00 PM",
            "price_per_hour": 50,
            "price_per_day": 300,
            "night_price": 200,
            "weekend_per_day": 350,
            "weekend_per_hour": 60,
            "weekend_night_price": 75,
            "night_start_time": "06:00",
            "size_of_ground": "60 by 60 ft",
            "ground_service": [
                {
                    "service_id": "6618c8e8b06f0f17e1e49bb2",
                    "service_name": "Bad minton",
                    "service_price_hour": 20,
                    "service_price_day": 100
                }
            ],
            "ground_sports": [
                {
                    "sports_id": "65f2f83972bac300de4bc64f",
                    "sports_name": "football"
                }
            ],
            "status": "booked",
            "images": [
                {
                    "_id": "66223285a9f92d0d33643cba",
                    "ground_id": "6622273395b62e444a583951",
                    "image_order_id": 1,
                    "image_url": "https://res.cloudinary.com/dxyjq5lwk/image/upload/v1713517189/grounds/ipyhdqm9tcet08gavmna.jpg",
                    "image_path": "grounds/ipyhdqm9tcet08gavmna",
                    "thumb_img": true,
                    "__v": 0
                }
            ]
        },
        {
            "_id": "66223eabcb8ec1e4fc7c378b",
            "ground_name": "Test1",
            "ground_description": "tt",
            "ground_address": "hhh",
            "pincode": 654765,
            "country": "India",
            "city": "Asarganj",
            "state": "Bihar",
            "latitude": 25.1475962,
            "longitude": 86.6875465,
            "contact_no": "4536456464",
            "ground_opening": "12:00 AM",
            "ground_closing": "1:00 AM",
            "price_per_hour": 33,
            "price_per_day": 33,
            "night_price": 44,
            "weekend_per_day": 44,
            "weekend_per_hour": 44,
            "weekend_night_price": 55,
            "night_start_time": "2:00 AM",
            "size_of_ground": "44",
            "ground_service": [
                {
                    "service_id": "660ce743b9acda29fb8dfe2e",
                    "service_name": "football",
                    "service_price_hour": 124,
                    "service_price_day": 44
                }
            ],
            "ground_sports": [
                {
                    "sports_id": "661e8b927475c568a6ca50c4",
                    "sports_name": "Test"
                }
            ],
            "status": "available",
            "images": [
                {
                    "_id": "662658f9348aee0c00d3afdf",
                    "ground_id": "66223eabcb8ec1e4fc7c378b",
                    "image_order_id": 1,
                    "image_url": "https://res.cloudinary.com/dxyjq5lwk/image/upload/v1713789177/grounds/q1ak5iqpu5d880ba8fy3.jpg",
                    "image_path": "grounds/q1ak5iqpu5d880ba8fy3",
                    "thumb_img": true,
                    "__v": 0
                }
            ]
        }
  ],
   "pagination": {
    "pageSize": 10,
    "page": 1,
    "totalPages": 3,
    "totalGrounds": 25,
    "prevPageLink": null,
    "nextPageLink": "http://example.com/api/ground/groundList?page=2&pageSize=10&includeTotal=true"
  }
}

```

###

## Show Ground Details

This endpoint retrieves detailed information about a specific ground based on its ID.

### Request

- **Method:** GET
- **URL:** `/api/app/ground/showGround`
- **Body Parameters:**
  - ground_id: ID of the ground (required)

### Response

- **Status Code:** 
  - 200 OK: Successfully retrieved ground details.
  - 404 Not Found: Ground is not available.
  - 500 Bad Request: Internal Server Error.

- **Response Body (Success):**
```json
{
    "success": false,
    "data": {
        "_id": "65f9cc66f99f259c2cf35c26",
        "ground_name": "Vankhede Stadium",
        "ground_description": "This is a sample ground description.",
        "ground_address": "123 Sample Street",
        "pincode": 12345,
        "city": "Mumbai",
        "state": "Maharastra",
        "latitude": 37.7749,
        "longitude": -122.4194,
        "contact_no": "123-456-7890",
        "ground_opening": "08:00",
        "ground_closing": "10:00 ",
        "price_per_hour": 50,
        "price_per_day": 300,
        "night_price": 300,
        "weekend_per_day": 350,
        "weekend_per_hour": 60,
        "weekend_night_price": 75,
        "night_start_time": "06:00",
        "size_of_ground": "60 by 60 ft",
        "ground_service": [
            "bat and ball"
        ],
        "ground_sports": [
            "cricket"
        ],
        "user_id": "65eeb8d3f8ee5dc49064ce74",
        "status": "available",
        "isDeleted": false,
        "createdAt": "2024-03-19T17:33:26.207Z",
        "updatedAt": "2024-03-19T17:33:26.207Z",
        "__v": 0,
        "images": [
            {
                "_id": "65f9cc69f99f259c2cf35c2a",
                "ground_id": "65f9cc66f99f259c2cf35c26",
                "image_order_id": 2,
                "image_url": "https://res.cloudinary.com/dujldtzay/image/upload/v1710869610/grounds/jirlegid1wuzihosd4ul.jpg",
                "image_path": "grounds/jirlegid1wuzihosd4ul",
                "thumb_img": false,
                "__v": 0
            },
            {
                "_id": "65f9cc6bf99f259c2cf35c2b",
                "ground_id": "65f9cc66f99f259c2cf35c26",
                "image_order_id": 1,
                "image_url": "https://res.cloudinary.com/dujldtzay/image/upload/v1710869612/grounds/dgysgqvl3gogmtz7xask.jpg",
                "image_path": "grounds/dgysgqvl3gogmtz7xask",
                "thumb_img": true,
                "__v": 0
            }
        ],
        "totalRatings": 0,
        "ratings": []
    },
    "message": "Ground Details are fetched successfully!"
 }
```
## Delete Ground Api

### Request

- **Method:** POST
- **URL:** `/api/app/ground/deleteGround`
- **Body Parameters:**
  - ground_id: ID of the ground to be deleted (required)

### Response

- **Status Code:** 
  - 200 OK: Ground deleted successfully.
  - 201 Created: Ground not found.
  - 400 Bad Request: Internal Server Error.

- **Response Body (Success):**
```json
{
  "success": true,
  "message": "Ground deleted successfully!"
}
```
## Get Ground Images

### Request

- **Method:** GET
- **URL:** `/api/app/ground/getImageList`
- **Body Parameters:**
  - ground_id: ID of the ground (required)

### Response

- **Status Code:** 
  - 200 OK: Ground images retrieved successfully.
  - 400 Bad Request: ground_id is invalid or Internal Server Error.
  - 404 Not Found: Ground images not found.

- **Response Body (Success):**
```json
{
  "success": true,
  "data": [
        {
            "_id": "65f9cc6bf99f259c2cf35c2b",
            "ground_id": "65f9cc66f99f259c2cf35c26",
            "image_order_id": 1,
            "image_url": "https://res.cloudinary.com/dujldtzay/image/upload/v1710869612/grounds/dgysgqvl3gogmtz7xask.jpg",
            "image_path": "grounds/dgysgqvl3gogmtz7xask",
            "thumb_img": true,
            "__v": 0
        },
    // Additional image objects if available
  ],
  "message": "Ground Images retrieved successfully!"
}

```
# send Otp to mobile number Api

- Description : This endpoint generates an OTP and sends it to the provided mobile number. If the user associated with the mobile number does not exist in the database, it creates a new user record with the mobile number and the generated OTP. and by default user role is 2(Owner).
- **URL:** `/api/app/auth/sendOtp`
- **Method:** POST

## Request Parameters

- **Body:**
  - `mobile_number`: The mobile number to which the OTP will be sent.

## Responses

### Success Response

- **Status Code:**
- 200 OK : OTP SENT
- 400 Bad request Sending multiple OTP requests to the same number is not allowed: Indicate that sending multiple OTP requests to the same mobile number is not permitted to prevent misuse or spamming.
- 400 Bad request Please enter a mobile number!: Returned when the mobile_number field is missing in the request body. Prompt the client to provide a mobile number.
- 500 internal Server Error: An error occurred while processing the request.
- **Body:**
  ```json
  {
    "success": true,
    "data": {
      "sms_status": true,
      "otp": "123456",
      "key": "encryptedId"
    },
    "message": "OTP Sent to <mobile_number>"
  }

## Verify OTP

### Request

- **Method:** POST
- **URL:** `/api/app/auth/verifyOtp`
- **Body Parameters:**
  - key: Encrypted user ID (required)
  - otp: OTP entered by the user (required)

### Response

- **Status Code:**
  - 200 OK: User is successfully authenticated.
  - 400 Bad Request: Key and OTP are required or OTP is not valid.
  - 500 Internal Server Error: An error occurred while processing the request.

- **Response Body (Success):**
```json
{
  "success": true,
  "message": "User is authenticated!"
}
```
## Bookings List

### Request

- **Method:** GET
- **URL:** `/api/app/booking/allBookings/`
- Description : This API endpoint sends an HTTP GET request to /api/app/booking/allBookings to retrieve all bookings, including the total count.
- The request includes the following parameters in the query string:
- `page`: (optional) The page number for pagination.
- `pageSize`: (optional) The number of items per page.
- `status`: (optional) The status of the bookings.
- `contact_no`: (optional) The contact number associated with the bookings.

- **Response Body (Success):**
- Upon a successful request, the API returns a JSON response with a 200 status code. The response body includes the following key-value pairs:
- `success`: A boolean flag indicating the success status of the request.
- `data`: An array containing booking details, including order slot ID, user information, ground details, booking type, date, time, price, booking ID, payment method, transaction ID, discount amount, total amount, creation and update timestamps, and status.
- `pagination`: An object providing pagination details such as page size, page number, total pages, total booked slots, and flags for next and previous pages.
- `message`: A field that may contain additional information or status messages.

```json
{
    "success": true,
    "data": [
        {
            "order_slot_id": "",
            "user": {
                "contact_no": 0,
                "email": "",
                "first_name": "",
                "last_name": ""
            },
            "ground_name": "",
            "ground_address": "",
            "booking_type": "",
            "date": "",
            "from_time": "",
            "to_time": "",
            "price": 0,
            "booking": {
                "booking_id": "",
                "payment_method": "",
                "transaction_id": "",
                "discount_amount": 0,
                "total_amount": 0,
                "createdAt": "",
                "updatedAt": ""
            },
            "status": ""
        }
    ],
    "pagination": {
        "pageSize": null,
        "page": null,
        "totalPages": null,
        "totalBookedSlots": 0,
        "hasNextPage": true,
        "hasPrevPage": true,
        "prevPageLink": "",
        "nextPageLink": null
    },
    "message": "Booking Data fetch successfully"
}
````

## Create Booking

### Request
- **Method:** POST
- **URL:** `/api/app/booking/createBooking/`

- **Request Body (Success):**
  ```json
  {
  "ground_id": "String",
  "coupon_id": "String",
  "payment_method": "String",
  "transaction_id": "String",
  "discount_amount": "Number",
  "total_amount": "Number",
  "slots": [
    {
      "booking_type": "String",
      "date": "Date",
      "from_time": "String",
      "to_time": "String",
      "price": "Number",
      "status": "String"
    }
  ],
  "services": [
    {
      "service_id": "String",
      "service_book_price": "Number"
    }
  ]
  }

  ```
### Response

- **Status Code:**
  - 200 OK: Booking created successfully.
  - 400 Bad Request All fields are required!: Returned when one or more required fields (user_id, payment_method, transaction_id, total_amount) are missing in the request body. Prompt the client to provide all necessary information.
  - 500 Internal Server Error: An error occurred while processing the request.
  - If one or more time slots are already booked, a `400 Bad Request` response will be returned with the message: "One or more time slots are already booked".
  - If the coupon usage limit is `exceeded`, a `400 Bad Request` response will be returned with the message: "Coupon usage limit exceeded!".
  - If the `coupon ID` is invalid, a `400 Bad Request` response will be returned with the message: "Invalid coupon ID!".
  - If an `unexpected error` occurs on the server, a 500 Internal Server Error response will be returned with the message: "Internal Server Error".
 
- **Response Body (Success):**
  ````json
    {
    "success": true,
    "message": "Booking created successfully",
    "data": {
       "booking": { },
       "order_slots": [{},{}],
       "order_services": [{},{}]
      }
    }
  ````

