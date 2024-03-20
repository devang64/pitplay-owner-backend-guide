# pitplay-owner-backend-guide
## Table of Contents
1. [Create Ground Api](#ground-creation-api)
2. [Get All Ground List Api](#get-all-grounds)

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

- **Status Code:** 500 Internal Server Error
- **Body:**
   ```json
  {
  "success": false,
  "error": "Error message",
  "message": "Internal Server Error"
  }
  ```

## Get All Grounds

This endpoint retrieves a paginated list of all available grounds.

### Request

- **Method:** GET
- **URL:** /api/ground/groundList
- **Headers:**
    - Content-Type: application/json
    - Authorization: Bearer <token> (if authentication is required)
- **Query Parameters:**
    - page (optional): Page number (default: 1)
    - limit (optional): Number of items per page (default: 10)

### Response

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
      "_id": "ground_id",
      "ground_name": "Ground Name",
      "ground_address": "Ground Address",
      "ground_service": ["Service 1", "Service 2"],
      "ground_sports": ["Sport 1", "Sport 2"],
      "ground_cover_img": "Cover Image URL"
    }
  ],
  "pagination": {
    "totalGrounds": 100, 
    "totalPages": 10, 
    "currentPage": 1 
  }
}

```

###
