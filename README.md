# User Management Service

This is a basic HTTP web server in Go that provides user management capabilities. The service allows creating, retrieving, and deleting user records stored in a simple in-memory cache.

## Features

- **Create User**: Adds a new user to the cache.
- **Get User by ID**: Retrieves a user from the cache by their ID.
- **Delete User by ID**: Removes a user from the cache by their ID.

## Endpoints

### Root Endpoint

#### `GET /`

Returns a simple "Hello World" message.

### Create User

#### `POST /users`

Creates a new user.

- **Request Body**:

  ```json
  {
    "name": "John Doe"
  }
  ```

- **Response**:

  - Status Code: `201 Created` if the user is successfully created.

- **Error Responses**:

  - `400 Bad Request`: If the request body is invalid or if the name is missing.

### Get User by ID

#### `GET /users/{id}`

Retrieves a user by ID.

- **Path Parameter**:

  - `id`: The ID of the user.

- **Response**:

  - Status Code: `200 OK` with user information.
  - Body:
    ```json
    {
      "name": "John Doe"
    }
    ```

- **Error Responses**:

  - `400 Bad Request`: If the ID is not a valid integer.
  - `404 Not Found`: If the user with the specified ID does not exist.

### Delete User by ID

#### `DELETE /users/{id}`

Deletes a user by ID.

- **Path Parameter**:

  - `id`: The ID of the user.

- **Response**:

  - Status Code: `200 Status OK` if the user is successfully deleted.

- **Error Responses**:

  - `400 Bad Request`: If the ID is not a valid integer.
  - `404 Not Found`: If the user with the specified ID does not exist.

## Implementation Details

- Uses a `sync.RWMutex` for thread-safe access to the in-memory user cache.
- The cache is a map of user IDs to `User` structs.

### User Struct

```go
 type User struct {
     Name string `json:"name"`
 }
```

## Running the Application

1. Ensure you have Go installed.
2. Clone this repository.
3. Run the server:
   ```sh
   go run main.go
   ```
4. The server will start on port `8080`. You can use tools like `curl` or Postman to interact with the endpoints.

## Example Requests

### Create a User

```sh
curl -X POST -d '{"name":"Alice"}' -H "Content-Type: application/json" http://localhost:8080/users
```

### Get a User

```sh
curl http://localhost:8080/users/1
```

### Delete a User

```sh
curl -X DELETE http://localhost:8080/users/1
```

## License

This project is licensed under the MIT License.
