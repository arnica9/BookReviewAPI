# Book Review System API

A RESTful API built using Django and Django REST Framework (DRF) that allows users to browse books and manage reviews.

## Authentication Mechanism
The system uses JWT (JSON Web Tokens) via the djangorestframework-simplejwt package for securing endpoints.
* To access protected endpoints, users must log in to receive an Access Token.
* This token must be included in the HTTP headers of subsequent requests as: Authorization: Bearer <your_access_token>.

---

## Features & Endpoints

### 1. Authentication
* POST /api/register/ - Register a new user.
* POST /api/token/ - Login and obtain JWT access & refresh tokens.
* POST /api/token/refresh/ - Refresh the access token.
* POST /api/change-password/ - Change password for authenticated users.

### 2. Books Management
* GET /api/books/ - List all books (Public).
* POST /api/books/ - Add a new book (Admin only).
* GET /api/books/<id>/ - Retrieve details of a specific book (Public).
* PUT/PATCH/DELETE /api/books/<id>/ - Update or delete a book (Admin only).

### 3. Reviews Management
* GET /api/books/<book_id>/reviews/ - List all reviews for a specific book (Public).
* POST /api/books/<book_id>/reviews/ - Add a review for a specific book (Authenticated users).
* GET /api/reviews/<id>/ - Retrieve details of a specific review (Public).
* PUT /api/reviews/<id>/ - Update or edit a review (Only allowed for the review owner).
* DELETE /api/reviews/<id>/ - Delete a review (Only allowed for the review owner)
## How to Test the Endpoints using Postman

To test this API using Postman, follow these steps for each scenario:

### 1. Public Endpoints (No Authentication Required)
* List Books: Set the method to GET and enter http://127.0.0.1:8000/api/books/. Click Send.
* View Book Details: Set the method to GET and enter http://127.0.0.1:8000/api/books/1/.
* View Book Reviews: Set the method to GET and enter http://127.0.0.1:8000/api/books/1/reviews/.
* View Review Details: Set the method to GET and enter http://127.0.0.1:8000/api/reviews/1/.

### 2. User Authentication (JWT)
* Register: Set the method to POST, URL to http://127.0.0.1:8000/api/register/. In the Body tab, select raw and JSON, then provide credentials:
```json
{
  "username": "testuser",
  "password": "password123"
* *Login (Obtain Token):* Set the method to POST, URL to http://127.0.0.1:8000/api/token/. Provide the credentials in the JSON body. 
Copy the "access" token from the response.

### 3. Protected Endpoints (Authentication Required)
* *Add a Review / Add a Book:* Set the required method (POST) and URL. 
* Go to the *Authorization* tab in Postman.
* Select *Bearer Token* from the Type dropdown.
* Paste the copied *Access Token* into the Token field, then click *Send*.

### 4. Review Owner Endpoints (Edit / Delete)
* *Edit Review:* Set the method to PUT, URL to http://127.0.0.1:8000/api/reviews/1/. In *Authorization, use the **Bearer Token* of the owner.
* *Delete Review:* Set the method to DELETE, URL to http://127.0.0.1:8000/api/reviews/1/. In *Authorization, use the **Bearer Token* of the owner, then click *Send*.

---

## Setup & Installation (Local Run)

1. Clone the repository.
2. Create and activate a virtual environment.
3. Install dependencies:
```bash
pip install django djangorestframework djangorestframework-simplejwt

python manage.py makemigrations
python manage.py migrate
python manage.py runserver