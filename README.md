
# Mr. Proctor - Backend

## About
The backend of Mr. Proctor is setup using `Node.js` and `Express.js`. It will store the user's data and images received from the frontend. Images will be retrieved from `cloudinary storage` and all the user information along with stored images will be available on an Admin Dashboard deployed on `render`.


## API Reference

#### Get all data

```http
  GET /retrieve-data
```
The /retrieve-data endpoint will retrieve all user data and images stored on the server. The endpoint accepts a GET request with no query parameters. The endpoint returns an array of all user data and their images stored on the server.


#### Request
```
Method: GET
Endpoint: /retrieve-data
Query Parameters: none
```

#### Response
```
Status Code: 200 OK
Body:
data: an array containing all user data and their images stored on the server
```

#### Example
Retrieving all user data and images:
```
GET /retrieve-data
```
```
Status: 200 OK
{
  "data": [
    {
        "_id": "644a3dd8610d0dd70e1bce5d",
        "firstName": "Nancy",
        "lastName": "Greenberg",
        "email": "nancy231@gmail.com",
        "testInvitation": "123456",
        "id": "1633521057017",
        "images": [
        {
          "url": "https://example.com/image1.jpg",
          "timestamp": 1633521057017
        },
        {
          "url": "https://example.com/image2.jpg",
          "timestamp": 1633521063119
        }
      ],
      "__v": 0
    },
    {
        "_id": "644a5bf4b72bc09234f58694",
        "firstName": "Pragti",
        "lastName": "Chauhan",
        "email": "abc@gmail.com",
        "testInvitation": "123456",
        "id": "1633521068371",
        "images": [
        {
          "url": "https://example.com/image3.jpg",
          "timestamp": 1633521068371
        }
      ],
      "__v": 0
    }
  ]
}

```

### POST New User

```http
  POST /createUser
```
- The /createUser endpoint is used to create a new user in the system. This endpoint accepts a JSON object in the POST request body with the following properties:

```
firstName (required): The first name of the user.
lastName (required): The last name of the user.
email (required): The email address of the user.
testInvitation (required): The invitation code for the, test the user is taking.

```
- The API endpoint generates a unique id for the user and stores the user's information, along with an empty array of images, in the database

#### Request
```
HTTP Method: POST
Endpoint: /createUser
Request Body: JSON object with the following properties:
firstName (string, required)
lastName (string, required)
email (string, required)
testInvitation (string, required)
```

```
Example Request:
POST /createUser
Content-Type: application/json

{
  "firstName" : "Tina",
  "lastName" :"Johns",
  "email" : "johnstina@gmail.com",
  "testInvitation" : "123456"
}
```

#### Response
- HTTP Status Code: 200 if successful, 500 if an error occurred
- Response Body: JSON object with the following properties:
```
userid (string): The unique id assigned to the new user
error (string): If an error occurred while creating the user.
```
- In response you will get unique userid of user

```
HTTP/1.1 200 OK
Content-Type: application/json

{
    "userid": "1646726117427",
}

```

### POST Upload Image of User in storage
```http
  POST /upload-image
```

- The /upload-image route is used to upload an image for a specific user to the cloud. The route accepts a POST request and expects two parameters in the request body: image and userid.

- The image parameter should contain the base64-encoded image data. The userid parameter should contain the user ID for which the image is being uploaded.

- Upon receiving the request, the route generates a timestamp and uses it to create a unique file name for the image. It then uploads the image data to the cloud using the Cloudinary API and saves the image URL in the user's record in the database.

- If there is an error in uploading the image, the route responds with a 500 status code and an error message. If the image is uploaded successfully, the route responds with a 200 status code and a JSON object containing the interval.

####
```
HTTP Method: POST

Endpoint: /upload-image

Headers:

Content-Type: application/json
```
Body:
```
{
  "image": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAPoAAAD6CAIAAAC0tAIdAAAgAElEQVR4nOzde5zU1d8/8D/rZKlNtSpJhN....", // base64 encoded image data
  "userid": "12345" // User ID to associate the image with
}
```

#### Response:
```
HTTP Status Code: 200 OK
```
Body:
```
{
  "interval": 120000 // Time interval set for capturing screenshots in milliseconds
}
```
- If an error occurs during the image upload process, the response will have an HTTP status code of 500 and the body will contain an error message, for example:

- HTTP Status Code: 500 Internal Server Error

- Body:

```
{
  "error": "Failed to save image"
}
```


### SET New Interval

```http
  GET /set_interval?interval=value
```

- The /set_interval endpoint is used to set the interval of image capturing in the extension. The endpoint accepts a GET request with the interval query parameter. The value of the interval parameter is in minutes, which is then converted to milliseconds and set as the interval for capturing images.
- The route accepts a single query parameter.
- `interval`: The time interval, in minutes, between image uploads. This parameter is required.
#### Request
```
Method: GET
Endpoint: /set_interval
Query Parameters:
interval: a number representing the interval in minutes (e.g., interval=1)

```

#### Response
```
Status Code: 200 OK
Body:
success: a boolean value (true) indicating that the interval was set successfully
```

#### Example
Setting the interval to 2 minutes:
```
GET /set_interval?interval=2
```
```
Status: 200 OK
{
  "success": true
}

```


## Tech Stack

- Node
- Express
- MongoDB
- cloudinary storage


## Acknowledgements

 - [Awesome Readme Templates](https://awesomeopensource.com/project/elangosundar/awesome-README-templates)
 - [Referrence for Backend Setup](https://github.com/om-mapari/proctor-vision-backendn)
 - [Easy and Quick Database Deployment](https://www.mongodb.com/docs/atlas/tutorial/create-new-cluster/)

