

## 🟢 Beginner Level: FastAPI Fundamentals

### 1. **Introduction to FastAPI**

* What is FastAPI?
* Why use FastAPI over Flask/Django?
* Installing FastAPI and Uvicorn

### 2. **Basic App Setup**

* Creating your first FastAPI app
* `@app.get()` and `@app.post()` routes
* Running the server with Uvicorn

### 3. **Request and Response Handling**

* Path parameters
* Query parameters
* Request body with Pydantic models
* Response models
* Status codes and default responses

### 4. **Validation with Pydantic**

* Data types and field validation
* Optional and default fields
* Nested models
* Custom validators

---

## 🟡 Intermediate Level: Building Real APIs

### 5. **CRUD Operations**

* In-memory storage (basic CRUD logic)
* FastAPI Dependency Injection
* Error handling with `HTTPException`
* Path operations with CRUD for real-world entities

### 6. **Database Integration**

* SQLAlchemy basics (Sync & Async)
* Connecting to PostgreSQL/MySQL/SQLite
* ORM models vs Pydantic schemas
* Creating database sessions with dependencies

### 7. **Authentication & Authorization**

* OAuth2 with Password (and hashing)
* JWT-based authentication
* Role-based access control (RBAC)
* Securing endpoints with `Depends`

### 8. **Middleware & CORS**

* Adding custom middleware
* CORS settings
* Logging and request/response hooks

### 9. **Environment Management**

* Using `.env` files and `python-dotenv`
* Separating config into environments (dev/prod)

---

## 🔵 Advanced Level: Production-Ready APIs

### 10. **Asynchronous Programming**

* `async` vs `sync` routes
* Using async DB clients (e.g., `databases`, `Tortoise ORM`)
* Async external HTTP requests with `httpx`

### 11. **Background Tasks & Scheduled Jobs**

* `BackgroundTasks` in FastAPI
* Celery with Redis/RabbitMQ for heavy tasks
* Scheduled jobs with APScheduler or Celery Beat

### 12. **Testing**

* Using `pytest` with FastAPI
* Dependency overrides in tests
* Test client and fixtures
* Mocking external services

### 13. **Documentation and OpenAPI**

* Auto-generated Swagger docs
* Customizing docs with metadata
* Using `tags`, `summary`, `description`

### 14. **File Uploads and Static Files**

* Uploading single/multiple files
* Saving files to disk
* Serving static files

---

## 🔴 Expert Level: Deployment, CI/CD, and Scaling

### 15. **Dockerizing FastAPI**

* Dockerfile and `.dockerignore`
* Building and running FastAPI with Docker
* Using `docker-compose` with DB and app

### 16. **Deployment**

* Deploying to:

  * AWS EC2
  * DigitalOcean
  * Railway/Render
* Running with Gunicorn + Uvicorn workers
* Reverse proxy with Nginx

### 17. **CI/CD Integration**

* GitHub Actions for lint/test/build/deploy
* Example CI/CD workflow for FastAPI

### 18. **Rate Limiting, Caching & Performance**

* Redis for caching and rate limiting
* Async caching with `aioredis`
* Performance profiling with `py-spy` and `locust`

### 19. **WebSockets & Streaming**

* Real-time data with WebSockets
* Server-Sent Events (SSE)
* Use cases: chat apps, live dashboards




Great! Here's a detailed breakdown for the **Beginner Level: FastAPI Fundamentals - Section 1: Introduction to FastAPI**:

---

## 🟢 Beginner Level: FastAPI Fundamentals

### 1. 🚀 **Introduction to FastAPI**

---

#### ✅ **What is FastAPI?**

**FastAPI** is a modern, high-performance, web framework for building APIs with Python 3.7+ based on:

* **Standard Python type hints**
* **ASGI** (Asynchronous Server Gateway Interface)
* Built on top of **Starlette** (for web parts) and **Pydantic** (for data validation)

**Key Features:**

* **Fast**: One of the fastest Python frameworks (thanks to Starlette + Pydantic)
* **Type-safe**: Automatically generates request validation and API docs using type hints
* **Interactive Docs**: Swagger UI and ReDoc out of the box
* **Built-in async support**

---

#### ✅ **Why Use FastAPI Over Flask/Django?**

| Feature              | FastAPI               | Flask                          | Django                     |
| -------------------- | --------------------- | ------------------------------ | -------------------------- |
| Async support        | ✅ Native              | ❌ (workarounds)                | ❌ (limited)                |
| Type hint validation | ✅ Built-in (Pydantic) | ❌                              | ❌                          |
| API documentation    | ✅ Auto-generated      | ❌ (requires Flask-RESTX, etc.) | ❌ (requires DRF + Swagger) |
| Performance          | 🚀 Very High          | ⚡ Moderate                     | 🐢 Low (monolithic)        |
| Learning curve       | 🟢 Beginner friendly  | 🟢 Beginner friendly           | 🟡 Steep (for APIs)        |

Use **FastAPI** when:

* You need **high performance** (e.g., ML services, microservices)
* You care about **developer productivity and fewer bugs**
* You prefer **automatic validation and OpenAPI docs**

---

#### ✅ **Installing FastAPI and Uvicorn**

FastAPI is a web **framework**, and Uvicorn is an **ASGI server** to run it.

##### 📦 Install with pip:

```bash
pip install fastapi uvicorn
```

##### ✅ Verify installation:

Create a simple `main.py`:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello, FastAPI!"}
```

##### ▶️ Run the server:

```bash
uvicorn main:app --reload
```

* `main` → filename without `.py`
* `app` → FastAPI instance
* `--reload` → auto-reloads when code changes (great for development)

Now visit:

* **[http://127.0.0.1:8000](http://127.0.0.1:8000)** → main API
* **[http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)** → Swagger UI (interactive docs)
* **[http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)** → ReDoc (alternative UI)

Perfect! Here's the breakdown for:

---

## 🟢 Beginner Level: FastAPI Fundamentals

### 2. 🛠️ **Basic App Setup**

---

### ✅ **Creating Your First FastAPI App**

Create a file called `main.py`:

```python
from fastapi import FastAPI

app = FastAPI()  # Create an instance of FastAPI
```

This `app` object is the core of your FastAPI app — it will contain all routes, middleware, and configurations.

---

### ✅ **`@app.get()` and `@app.post()` Routes**

You define routes using decorators like `@app.get()` and `@app.post()` which correspond to HTTP methods:

#### 🔹 GET Example:

```python
@app.get("/")
def read_root():
    return {"message": "Welcome to FastAPI!"}
```

#### 🔹 GET with Path Parameter:

```python
@app.get("/items/{item_id}")
def read_item(item_id: int):
    return {"item_id": item_id}
```

FastAPI uses **type hints** (like `int`) to:

* Parse the path parameter
* Validate it
* Auto-generate docs

#### 🔹 POST Example with JSON Body:

```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    price: float

@app.post("/items/")
def create_item(item: Item):
    return {"item_name": item.name, "item_price": item.price}
```

This automatically:

* Validates request body
* Converts JSON to a Python object (`item`)
* Generates docs with schema info

---

### ✅ **Running the Server with Uvicorn**

From your terminal, run:

```bash
uvicorn main:app --reload
```

Explanation:

* `main` → your filename (without `.py`)
* `app` → the FastAPI instance inside that file
* `--reload` → enables hot-reloading for development

#### Access your app:

* [http://127.0.0.1:8000](http://127.0.0.1:8000) → your root route
* [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs) → Swagger UI (interactive)
* [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc) → ReDoc documentation

---

✅ You now have a working FastAPI app with both `GET` and `POST` endpoints!

Excellent! Here’s the in-depth guide for:

---

## 🟢 Beginner Level: FastAPI Fundamentals

### 4. ✅ **Validation with Pydantic**

FastAPI uses **Pydantic** to automatically validate request data using Python type hints. This provides robust error handling and clear, auto-documented input formats.

---

### 🔹 1. **Data Types and Field Validation**

Pydantic supports all common Python types with built-in validation:

```python
from pydantic import BaseModel

class Product(BaseModel):
    name: str
    price: float
    quantity: int
    is_available: bool
```

✅ If a client sends invalid types (like a string instead of a float), FastAPI automatically returns a `422 Unprocessable Entity` with a detailed validation error.

---

### 🔹 2. **Optional and Default Fields**

Use `Optional[...]` (or `| None`) and default values to mark fields as not required:

```python
from typing import Optional

class Product(BaseModel):
    name: str
    description: Optional[str] = None
    price: float = 0.0
    in_stock: bool = True
```

* `description` is optional
* `price` and `in_stock` have default values if omitted

---

### 🔹 3. **Nested Models**

You can nest models inside other models to handle complex structured data:

```python
class Manufacturer(BaseModel):
    name: str
    country: str

class Product(BaseModel):
    name: str
    price: float
    manufacturer: Manufacturer
```

Example JSON input:

```json
{
  "name": "Laptop",
  "price": 1299.99,
  "manufacturer": {
    "name": "TechCorp",
    "country": "USA"
  }
}
```

---

### 🔹 4. **Custom Validators**

Use Pydantic’s `@validator` decorator to add custom validation logic:

```python
from pydantic import validator

class Product(BaseModel):
    name: str
    price: float

    @validator('price')
    def price_must_be_positive(cls, value):
        if value <= 0:
            raise ValueError('Price must be greater than zero')
        return value
```

* You can use class methods to check business rules
* Custom errors are included in FastAPI’s validation responses

---

### ✅ Summary

| Feature          | Syntax Example                      |
| ---------------- | ----------------------------------- |
| Required field   | `name: str`                         |
| Optional field   | `description: Optional[str] = None` |
| Default value    | `in_stock: bool = True`             |
| Nested model     | `manufacturer: Manufacturer`        |
| Custom validator | `@validator('field_name')`          |

---

Awesome! You're now stepping into **Intermediate Level** — where we start building real APIs.

---

## 🟡 Intermediate Level: Building Real APIs

### 5. 🔁 **CRUD Operations**

Let’s implement basic CRUD (Create, Read, Update, Delete) operations using in-memory storage to understand the full API lifecycle.

---

### ✅ **1. In-Memory Storage (Basic CRUD Logic)**

We’ll store a list of items in memory for simplicity.

```python
from fastapi import FastAPI
from pydantic import BaseModel
from typing import List

app = FastAPI()

class Item(BaseModel):
    id: int
    name: str
    description: str = ""
    price: float

# In-memory DB
items_db: List[Item] = []
```

---

### ✅ **2. FastAPI Dependency Injection (Optional for now)**

FastAPI supports DI via `Depends`, but for in-memory demo, we'll skip DB session injection and use the global list. We'll introduce `Depends` in the next section with DB integration.

---

### ✅ **3. Error Handling with `HTTPException`**

Import `HTTPException` to gracefully handle errors like item not found:

```python
from fastapi import HTTPException
```

---

### ✅ **4. CRUD Path Operations for Items**

#### 🔹 Create (POST)

```python
@app.post("/items/", status_code=201)
def create_item(item: Item):
    items_db.append(item)
    return item
```

---

#### 🔹 Read All (GET)

```python
@app.get("/items/", response_model=List[Item])
def read_items():
    return items_db
```

---

#### 🔹 Read One (GET by ID)

```python
@app.get("/items/{item_id}", response_model=Item)
def read_item(item_id: int):
    for item in items_db:
        if item.id == item_id:
            return item
    raise HTTPException(status_code=404, detail="Item not found")
```

---

#### 🔹 Update (PUT)

```python
@app.put("/items/{item_id}", response_model=Item)
def update_item(item_id: int, updated_item: Item):
    for index, item in enumerate(items_db):
        if item.id == item_id:
            items_db[index] = updated_item
            return updated_item
    raise HTTPException(status_code=404, detail="Item not found")
```

---

#### 🔹 Delete (DELETE)

```python
@app.delete("/items/{item_id}", status_code=204)
def delete_item(item_id: int):
    for index, item in enumerate(items_db):
        if item.id == item_id:
            items_db.pop(index)
            return
    raise HTTPException(status_code=404, detail="Item not found")
```

---

### 📌 Summary of Routes:

| Method | Path          | Description       |
| ------ | ------------- | ----------------- |
| POST   | `/items/`     | Create new item   |
| GET    | `/items/`     | Get all items     |
| GET    | `/items/{id}` | Get item by ID    |
| PUT    | `/items/{id}` | Update item by ID |
| DELETE | `/items/{id}` | Delete item by ID |

---

This sets the foundation for RESTful CRUD in FastAPI. Next, you’ll likely want to use a **real database with SQLAlchemy** and start injecting dependencies.

Awesome — now let's dive into **Database Integration** with SQLAlchemy in FastAPI!

---

## 🟡 Intermediate Level: Building Real APIs

### 6. 🗃️ **Database Integration**

FastAPI works great with SQLAlchemy — both sync and async. Here’s how to integrate it step by step.

---

### ✅ **1. SQLAlchemy Basics (Sync & Async)**

#### 🔹 Synchronous SQLAlchemy (Traditional)

Install dependencies:

```bash
pip install sqlalchemy psycopg2-binary  # or use 'aiosqlite' / 'mysqlclient' depending on DB
```

Basic setup:

```python
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

DATABASE_URL = "sqlite:///./test.db"  # or PostgreSQL/MySQL URL

engine = create_engine(DATABASE_URL, connect_args={"check_same_thread": False})  # SQLite
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
Base = declarative_base()
```

#### 🔹 Asynchronous SQLAlchemy (Advanced)

Only use if you're familiar with async workflows. Requires:

```bash
pip install sqlalchemy[asyncio] asyncpg
```

And uses:

```python
from sqlalchemy.ext.asyncio import create_async_engine, AsyncSession
```

For now, we'll continue with **sync SQLAlchemy** (much simpler for CRUD apps).

---

### ✅ **2. Connecting to PostgreSQL / MySQL / SQLite**

**Example for each:**

* **SQLite:** `sqlite:///./test.db`
* **PostgreSQL:** `postgresql://user:password@localhost/dbname`
* **MySQL:** `mysql://user:password@localhost/dbname`

Just replace the `DATABASE_URL` in the engine setup.

---

### ✅ **3. ORM Models vs Pydantic Schemas**

#### 🔹 SQLAlchemy ORM Model:

```python
class Item(Base):
    __tablename__ = "items"

    id = Column(Integer, primary_key=True, index=True)
    name = Column(String, index=True)
    description = Column(String)
    price = Column(Integer)
```

#### 🔹 Pydantic Schemas:

```python
from pydantic import BaseModel

class ItemCreate(BaseModel):
    name: str
    description: str
    price: int

class ItemResponse(ItemCreate):
    id: int

    class Config:
        orm_mode = True
```

**Why both?**

* SQLAlchemy: DB representation
* Pydantic: Data exchange (request/response validation)

---

### ✅ **4. Creating Database Sessions with Dependencies**

FastAPI uses dependency injection for DB sessions:

```python
from fastapi import Depends

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()
```

Use `Depends(get_db)` in route functions:

```python
from sqlalchemy.orm import Session

@app.post("/items/")
def create_item(item: ItemCreate, db: Session = Depends(get_db)):
    db_item = Item(**item.dict())
    db.add(db_item)
    db.commit()
    db.refresh(db_item)
    return db_item
```

---

### ✅ Recap

| Concept             | What it Does                                |
| ------------------- | ------------------------------------------- |
| `engine`            | Connects to your DB                         |
| `Base`              | Base class for your ORM models              |
| `SessionLocal`      | DB session factory                          |
| `get_db()`          | Dependency to inject DB sessions            |
| ORM Model vs Schema | Separation of DB vs external-facing objects |

---

Great! Now let’s move on to **Authentication & Authorization** in FastAPI.

---

## 🟡 Intermediate Level: Building Real APIs

### 7. 🔐 **Authentication & Authorization**

This section will cover different methods of securing your FastAPI application using OAuth2, JWT, and role-based access control.

---

### ✅ **1. OAuth2 with Password (and Hashing)**

First, install the required dependencies:

```bash
pip install passlib[bcrypt] python-jose
```

**Steps:**

1. **Hashing Passwords**:
   We’ll use `passlib` to hash passwords before storing them in the database.

```python
from passlib.context import CryptContext

pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")

def hash_password(password: str) -> str:
    return pwd_context.hash(password)

def verify_password(plain_password: str, hashed_password: str) -> bool:
    return pwd_context.verify(plain_password, hashed_password)
```

2. **User Authentication**:
   For OAuth2, we’ll use a password flow and authenticate users based on their credentials.

```python
from fastapi import HTTPException, Depends
from fastapi.security import OAuth2PasswordBearer

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

class User(BaseModel):
    username: str

class UserInDB(User):
    hashed_password: str

fake_users_db = {
    "john_doe": {
        "username": "john_doe",
        "hashed_password": hash_password("secret"),
    }
}

def get_user(db, username: str):
    if username in db:
        user_dict = db[username]
        return UserInDB(**user_dict)
    return None
```

---

### ✅ **2. JWT-based Authentication**

We’ll use JSON Web Tokens (JWT) for issuing and verifying tokens.

**Create JWT tokens**:

```python
from datetime import datetime, timedelta
from jose import JWTError, jwt

SECRET_KEY = "your_secret_key"
ALGORITHM = "HS256"
ACCESS_TOKEN_EXPIRE_MINUTES = 30

def create_access_token(data: dict, expires_delta: timedelta = timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)):
    to_encode = data.copy()
    expire = datetime.utcnow() + expires_delta
    to_encode.update({"exp": expire})
    encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)
    return encoded_jwt
```

**Token verification**:

```python
def verify_token(token: str):
    credentials_exception = HTTPException(
        status_code=401, detail="Could not validate credentials"
    )
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        username: str = payload.get("sub")
        if username is None:
            raise credentials_exception
        return username
    except JWTError:
        raise credentials_exception
```

---

### ✅ **3. Role-based Access Control (RBAC)**

Let’s define roles and enforce them using FastAPI’s **Depends** dependency injection.

**Example**:

1. Define roles in your user model (this could be stored in the database):

```python
class UserInDB(User):
    hashed_password: str
    role: str
```

2. Protect endpoints with role-based access:

```python
def get_current_user(token: str = Depends(oauth2_scheme)):
    username = verify_token(token)
    return get_user(fake_users_db, username)

def get_current_admin_user(current_user: UserInDB = Depends(get_current_user)):
    if current_user.role != "admin":
        raise HTTPException(status_code=403, detail="Not authorized")
    return current_user
```

3. Protect routes:

```python
@app.get("/admin/")
def read_admin_data(current_user: UserInDB = Depends(get_current_admin_user)):
    return {"message": "Admin data"}
```

* This ensures that only users with the `admin` role can access the `/admin/` endpoint.

---

### ✅ **4. Securing Endpoints with `Depends`**

Using `Depends` to inject authentication dependencies into endpoints:

1. **Define OAuth2 Dependency**:

```python
from fastapi.security import OAuth2PasswordBearer
oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

@app.post("/token")
def login_for_access_token(form_data: OAuth2PasswordRequestForm = Depends()):
    user = get_user(fake_users_db, form_data.username)
    if not user or not verify_password(form_data.password, user["hashed_password"]):
        raise HTTPException(status_code=401, detail="Invalid credentials")
    access_token = create_access_token(data={"sub": form_data.username})
    return {"access_token": access_token, "token_type": "bearer"}
```

2. **Use Depends for Authorization**:

```python
@app.get("/protected/")
def read_protected_data(current_user: UserInDB = Depends(get_current_user)):
    return {"message": "You have access to protected data", "user": current_user.username}
```

* The `Depends(get_current_user)` ensures the user must be authenticated and the token must be valid.

---

### ✅ **Summary**

| Concept                      | Explanation                                                   |
| ---------------------------- | ------------------------------------------------------------- |
| **Password Hashing**         | Securely store passwords with bcrypt                          |
| **JWT Tokens**               | Use JWT to create and verify authentication tokens            |
| **RBAC (Role-Based Access)** | Use roles to control access to certain routes                 |
| **Depends**                  | Use FastAPI’s `Depends` to inject authentication dependencies |

---

Great! Let’s now cover **Middleware & CORS** and **Environment Management** to enhance your FastAPI app's flexibility and scalability.

---

## 🟡 Intermediate Level: Building Real APIs

### 8. 🛠️ **Middleware & CORS**

Middleware in FastAPI allows you to process requests and responses globally before they reach your route functions or after they leave them. This is useful for tasks like logging, security, or handling cross-origin requests.

---

### ✅ **1. Adding Custom Middleware**

FastAPI provides a simple interface for creating custom middleware using the `BaseHTTPMiddleware` class. This is useful for adding extra logic to the request-response cycle.

#### Example: Logging Middleware

```python
from starlette.middleware.base import BaseHTTPMiddleware
import logging

class LoggingMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request, call_next):
        logger = logging.getLogger("uvicorn")
        logger.info(f"Request: {request.method} {request.url}")
        response = await call_next(request)
        logger.info(f"Response status code: {response.status_code}")
        return response

app.add_middleware(LoggingMiddleware)
```

In this example:

* Every request and response is logged with method, URL, and status code.

---

### ✅ **2. CORS Settings**

**Cross-Origin Resource Sharing (CORS)** is a mechanism to allow or block resources on a web page from being requested from another domain. FastAPI provides an easy way to handle this.

#### Enable CORS:

```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # Allows all domains
    allow_credentials=True,
    allow_methods=["*"],  # Allows all HTTP methods
    allow_headers=["*"],  # Allows all headers
)
```

You can customize the `allow_origins` list to only allow specific domains if needed:

```python
allow_origins=["https://example.com", "https://anotherdomain.com"]
```

---

### ✅ **3. Logging and Request/Response Hooks**

Logging is a crucial part of any application. In addition to custom middleware, FastAPI allows you to add logging hooks using **request** and **response** handlers.

#### Example: Log Request Details and Response Time

```python
from starlette.requests import Request
import time

@app.middleware("http")
async def log_request(request: Request, call_next):
    start_time = time.time()
    response = await call_next(request)
    process_time = time.time() - start_time
    print(f"Request: {request.method} {request.url} - Processed in {process_time:.2f} sec")
    return response
```

This middleware will log the request method, URL, and the time it took to process.

---

## 🟢 Advanced Level: Optimizing FastAPI

### 9. 🌱 **Environment Management**

Environment management is critical for making your app configurable in different environments (development, production). Let’s explore how to manage this effectively using `.env` files and `python-dotenv`.

---

### ✅ **1. Using `.env` Files and `python-dotenv`**

To keep sensitive data and configuration settings outside your source code, you can use `.env` files. These files contain key-value pairs and can be loaded into the environment using the `python-dotenv` library.

#### Install `python-dotenv`:

```bash
pip install python-dotenv
```

#### Create a `.env` File:

```
DATABASE_URL=postgresql://user:password@localhost/dbname
SECRET_KEY=your_secret_key
DEBUG=True
```

#### Load `.env` in FastAPI:

```python
from dotenv import load_dotenv
import os

# Load environment variables from the .env file
load_dotenv()

# Access the variables
database_url = os.getenv("DATABASE_URL")
secret_key = os.getenv("SECRET_KEY")
debug_mode = os.getenv("DEBUG", "False") == "True"
```

---

### ✅ **2. Separating Config into Environments (dev/prod)**

It’s a good practice to have different configurations for different environments (e.g., development and production). You can easily manage this by creating separate `.env` files for each environment.

#### Example `.env` for Development (`.env.dev`):

```
DATABASE_URL=sqlite:///./dev.db
SECRET_KEY=dev_secret_key
DEBUG=True
```

#### Example `.env` for Production (`.env.prod`):

```
DATABASE_URL=postgresql://user:password@prod.db
SECRET_KEY=prod_secret_key
DEBUG=False
```

To load the appropriate configuration, you can conditionally load the correct `.env` file based on the environment:

```python
import os
from dotenv import load_dotenv

env = os.getenv("FASTAPI_ENV", "dev")

if env == "prod":
    load_dotenv(".env.prod")
else:
    load_dotenv(".env.dev")
```

This will load the correct `.env` file based on the `FASTAPI_ENV` environment variable.

---

### ✅ **Summary**

| Concept                | Explanation                                  |
| ---------------------- | -------------------------------------------- |
| **Custom Middleware**  | Add logic to the request-response lifecycle  |
| **CORS**               | Handle cross-origin requests                 |
| **Logging Middleware** | Log request and response details             |
| **python-dotenv**      | Manage environment variables in `.env` files |
| **Environment Config** | Use different settings for dev, prod, etc.   |

---

Great! Let’s now cover **Middleware & CORS** and **Environment Management** to enhance your FastAPI app's flexibility and scalability.

---

## 🟡 Intermediate Level: Building Real APIs

### 8. 🛠️ **Middleware & CORS**

Middleware in FastAPI allows you to process requests and responses globally before they reach your route functions or after they leave them. This is useful for tasks like logging, security, or handling cross-origin requests.

---

### ✅ **1. Adding Custom Middleware**

FastAPI provides a simple interface for creating custom middleware using the `BaseHTTPMiddleware` class. This is useful for adding extra logic to the request-response cycle.

#### Example: Logging Middleware

```python
from starlette.middleware.base import BaseHTTPMiddleware
import logging

class LoggingMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request, call_next):
        logger = logging.getLogger("uvicorn")
        logger.info(f"Request: {request.method} {request.url}")
        response = await call_next(request)
        logger.info(f"Response status code: {response.status_code}")
        return response

app.add_middleware(LoggingMiddleware)
```

In this example:

* Every request and response is logged with method, URL, and status code.

---

### ✅ **2. CORS Settings**

**Cross-Origin Resource Sharing (CORS)** is a mechanism to allow or block resources on a web page from being requested from another domain. FastAPI provides an easy way to handle this.

#### Enable CORS:

```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # Allows all domains
    allow_credentials=True,
    allow_methods=["*"],  # Allows all HTTP methods
    allow_headers=["*"],  # Allows all headers
)
```

You can customize the `allow_origins` list to only allow specific domains if needed:

```python
allow_origins=["https://example.com", "https://anotherdomain.com"]
```

---

### ✅ **3. Logging and Request/Response Hooks**

Logging is a crucial part of any application. In addition to custom middleware, FastAPI allows you to add logging hooks using **request** and **response** handlers.

#### Example: Log Request Details and Response Time

```python
from starlette.requests import Request
import time

@app.middleware("http")
async def log_request(request: Request, call_next):
    start_time = time.time()
    response = await call_next(request)
    process_time = time.time() - start_time
    print(f"Request: {request.method} {request.url} - Processed in {process_time:.2f} sec")
    return response
```

This middleware will log the request method, URL, and the time it took to process.

---

## 🟢 Advanced Level: Optimizing FastAPI

### 9. 🌱 **Environment Management**

Environment management is critical for making your app configurable in different environments (development, production). Let’s explore how to manage this effectively using `.env` files and `python-dotenv`.

---

### ✅ **1. Using `.env` Files and `python-dotenv`**

To keep sensitive data and configuration settings outside your source code, you can use `.env` files. These files contain key-value pairs and can be loaded into the environment using the `python-dotenv` library.

#### Install `python-dotenv`:

```bash
pip install python-dotenv
```

#### Create a `.env` File:

```
DATABASE_URL=postgresql://user:password@localhost/dbname
SECRET_KEY=your_secret_key
DEBUG=True
```

#### Load `.env` in FastAPI:

```python
from dotenv import load_dotenv
import os

# Load environment variables from the .env file
load_dotenv()

# Access the variables
database_url = os.getenv("DATABASE_URL")
secret_key = os.getenv("SECRET_KEY")
debug_mode = os.getenv("DEBUG", "False") == "True"
```

---

### ✅ **2. Separating Config into Environments (dev/prod)**

It’s a good practice to have different configurations for different environments (e.g., development and production). You can easily manage this by creating separate `.env` files for each environment.

#### Example `.env` for Development (`.env.dev`):

```
DATABASE_URL=sqlite:///./dev.db
SECRET_KEY=dev_secret_key
DEBUG=True
```

#### Example `.env` for Production (`.env.prod`):

```
DATABASE_URL=postgresql://user:password@prod.db
SECRET_KEY=prod_secret_key
DEBUG=False
```

To load the appropriate configuration, you can conditionally load the correct `.env` file based on the environment:

```python
import os
from dotenv import load_dotenv

env = os.getenv("FASTAPI_ENV", "dev")

if env == "prod":
    load_dotenv(".env.prod")
else:
    load_dotenv(".env.dev")
```

This will load the correct `.env` file based on the `FASTAPI_ENV` environment variable.

---

### ✅ **Summary**

| Concept                | Explanation                                  |
| ---------------------- | -------------------------------------------- |
| **Custom Middleware**  | Add logic to the request-response lifecycle  |
| **CORS**               | Handle cross-origin requests                 |
| **Logging Middleware** | Log request and response details             |
| **python-dotenv**      | Manage environment variables in `.env` files |
| **Environment Config** | Use different settings for dev, prod, etc.   |

Let's dive into **Asynchronous Programming** in FastAPI!

---

## 🟡 Intermediate Level: Building Real APIs

### 10. ⏳ **Asynchronous Programming**

FastAPI allows you to write asynchronous code with Python's `async` and `await`, which helps your app handle many I/O-bound tasks efficiently. Here's how you can use async programming in FastAPI:

---

### ✅ **1. `async` vs `sync` Routes**

FastAPI supports both **synchronous** (`sync`) and **asynchronous** (`async`) route handlers.

* **Synchronous Routes**: These are traditional functions, blocking until they are finished.

```python
@app.get("/sync")
def sync_route():
    return {"message": "This is a sync route!"}
```

* **Asynchronous Routes**: These can perform non-blocking operations, such as making HTTP requests or querying the database, without blocking the server.

```python
@app.get("/async")
async def async_route():
    return {"message": "This is an async route!"}
```

**When to use async routes:**

* **I/O-bound tasks**: Network calls (e.g., APIs, databases, file systems) are ideal for async because they can free up the server to handle other requests while waiting for data.
* **CPU-bound tasks**: Avoid async for heavy computation as it won’t improve performance for CPU-bound tasks (use a separate task queue like Celery for those).

---

### ✅ **2. Using Async DB Clients**

When using async databases, you can switch from **synchronous** to **asynchronous** database clients. Some popular options for async DB clients in FastAPI are:

#### Using `databases` library (with SQLAlchemy):

The `databases` package provides async support for SQLAlchemy.

```bash
pip install databases asyncpg
```

**Setup Example**:

```python
import databases
import sqlalchemy

DATABASE_URL = "postgresql://user:password@localhost/mydatabase"

database = databases.Database(DATABASE_URL)
metadata = sqlalchemy.MetaData()

engine = sqlalchemy.create_engine(DATABASE_URL)
Base = sqlalchemy.declarative_base(metadata=metadata)

# Define a simple table model
class Item(Base):
    __tablename__ = "items"
    id = sqlalchemy.Column(sqlalchemy.Integer, primary_key=True)
    name = sqlalchemy.Column(sqlalchemy.String)

# Create an async dependency for DB session
async def get_db():
    async with database.transaction():
        yield database
```

**Async Route Using the DB**:

```python
@app.get("/items/")
async def get_items(db: databases.Database = Depends(get_db)):
    query = "SELECT * FROM items"
    result = await db.fetch_all(query)
    return result
```

* Here, the `async with` ensures the database session is properly managed, and `fetch_all` is non-blocking.

#### Using `Tortoise ORM` (Async ORM):

Tortoise ORM is another great option for async DB handling.

```bash
pip install tortoise-orm asyncpg
```

**Basic Setup**:

```python
from tortoise import Tortoise, fields
from tortoise.models import Model

class Item(Model):
    id = fields.IntField(pk=True)
    name = fields.CharField(max_length=50)

# Initialize Tortoise in FastAPI app
@app.on_event("startup")
async def startup():
    await Tortoise.init(
        db_url="postgres://user:password@localhost/mydatabase",
        modules={"models": ["__main__"]},
    )
    await Tortoise.generate_schemas()

@app.on_event("shutdown")
async def shutdown():
    await Tortoise.close_connections()
```

**Async Route Using Tortoise ORM**:

```python
@app.get("/items/")
async def get_items():
    items = await Item.all()
    return items
```

---

### ✅ **3. Async External HTTP Requests with `httpx`**

For making external HTTP requests asynchronously, `httpx` is a fantastic library.

```bash
pip install httpx
```

**Example of Async HTTP Request with `httpx`**:

```python
import httpx

@app.get("/fetch_data/")
async def fetch_data():
    async with httpx.AsyncClient() as client:
        response = await client.get("https://api.example.com/data")
        return response.json()
```

This allows you to make non-blocking HTTP requests and efficiently handle multiple external APIs in parallel.

---

### ✅ **4. Combining Async with Background Tasks**

You can also combine async routes with background tasks for deferred processing (e.g., sending emails, long-running tasks).

**Example with Background Tasks**:

```python
from fastapi import BackgroundTasks

def send_email(email: str):
    # Simulate email sending process
    print(f"Sending email to {email}")

@app.get("/send-email/")
async def send_email_route(background_tasks: BackgroundTasks, email: str):
    background_tasks.add_task(send_email, email)
    return {"message": "Email sending in the background"}
```

Here, the email sending function runs in the background without blocking the main request.

---

### ✅ **5. Summary: Sync vs Async**

| **Sync Route**               | **Async Route**                                     |
| ---------------------------- | --------------------------------------------------- |
| Blocks while waiting for I/O | Non-blocking, can handle many I/O tasks in parallel |
| Best for CPU-bound tasks     | Best for I/O-bound tasks like DB, network, file I/O |
| Example: `def sync_route()`  | Example: `async def async_route()`                  |

---

### Conclusion

FastAPI’s async capabilities make it perfect for building high-performance APIs that handle large amounts of I/O-bound operations. By switching to async with libraries like `databases`, `Tortoise ORM`, and `httpx`, you can dramatically improve the scalability of your application.

Let’s dive into **Background Tasks & Scheduled Jobs** in FastAPI, covering both **simple background tasks** and more **advanced task scheduling** using Celery and APScheduler.

---

## 🟡 Advanced Level: Optimizing FastAPI

### 11. ⏳ **Background Tasks & Scheduled Jobs**

In FastAPI, background tasks are ideal for performing tasks asynchronously without blocking the response to the user. For more complex scenarios, such as heavy or scheduled jobs, **Celery** and **APScheduler** can be used.

---

### ✅ **1. `BackgroundTasks` in FastAPI**

FastAPI provides an easy-to-use `BackgroundTasks` class to handle background operations such as sending emails or logging activities without blocking the main request.

#### Simple Example of Background Tasks:

```python
from fastapi import BackgroundTasks, FastAPI
import time

app = FastAPI()

# Function to run in the background
def write_log(message: str):
    time.sleep(5)  # Simulate a time-consuming task
    with open("log.txt", "a") as log_file:
        log_file.write(message + "\n")

# Route that triggers the background task
@app.get("/log/{message}")
async def log_message(message: str, background_tasks: BackgroundTasks):
    background_tasks.add_task(write_log, message)
    return {"message": "Your message is being logged in the background"}
```

In this example:

* When the `/log/{message}` route is called, the message is passed to the `write_log` function, which runs in the background while the response is returned immediately.

**Use cases** for background tasks:

* Sending emails
* Sending notifications
* Processing files or logs

---

### ✅ **2. Celery with Redis/RabbitMQ for Heavy Tasks**

For more complex, long-running, or distributed background tasks, **Celery** is the go-to choice. It can handle heavier loads by processing tasks in the background and distributing them across multiple workers. You can use **Redis** or **RabbitMQ** as the broker to manage tasks.

#### Setting Up Celery with Redis:

1. **Install Dependencies**:

```bash
pip install celery[redis] fastapi
```

2. **Configure Celery** (with Redis):

Create a file `celery_worker.py` to configure and start the Celery worker:

```python
from celery import Celery

app = Celery(
    'worker',
    broker='redis://localhost:6379/0',  # Redis as broker
    backend='redis://localhost:6379/0'  # Redis as result backend
)

@app.task
def send_email(email: str):
    # Simulate sending an email
    print(f"Sending email to {email}")
```

3. **FastAPI Application with Celery**:

In your FastAPI application, create a route that triggers the Celery task:

```python
from fastapi import FastAPI
from celery_worker import send_email

app = FastAPI()

@app.get("/send-email/{email}")
async def trigger_email(email: str):
    send_email.delay(email)  # Asynchronously call Celery task
    return {"message": "Email sending task triggered!"}
```

* The `send_email.delay()` method sends the task to the Celery worker to be processed asynchronously.

4. **Start Celery Worker**:

Run the Celery worker by executing the following command in your terminal:

```bash
celery -A celery_worker.app worker --loglevel=info
```

This will start the worker that listens for incoming tasks and processes them.

#### **Advantages of Celery**:

* Handles long-running tasks
* Supports multiple workers
* Distributed task queues
* Retry mechanism and result tracking

---

### ✅ **3. Scheduled Jobs with APScheduler or Celery Beat**

For recurring tasks, you can use **APScheduler** or **Celery Beat** to schedule jobs at specific intervals or times.

#### **Using APScheduler with FastAPI**:

APScheduler is a simple and lightweight scheduler for Python.

1. **Install APScheduler**:

```bash
pip install apscheduler
```

2. **Setup APScheduler**:

In your FastAPI app, create scheduled tasks:

```python
from apscheduler.schedulers.background import BackgroundScheduler
from apscheduler.events import EVENT_JOB_EXECUTED, EVENT_JOB_ERROR
from fastapi import FastAPI

app = FastAPI()

# Function to run at scheduled time
def scheduled_task():
    print("Scheduled task is running!")

# Initialize scheduler and add job
scheduler = BackgroundScheduler()
scheduler.add_job(scheduled_task, 'interval', seconds=10)  # Run every 10 seconds
scheduler.start()

@app.on_event("shutdown")
def shutdown_event():
    scheduler.shutdown()
```

In this example, `scheduled_task` will run every 10 seconds, and it is added to the scheduler with the `'interval'` trigger. You can use other triggers like `'cron'` for more complex scheduling.

#### **Using Celery Beat for Scheduled Jobs**:

**Celery Beat** is a scheduler for Celery, which stores the schedule in the database and can periodically trigger Celery tasks.

1. **Install Celery Beat**:

```bash
pip install celery[redis] celery[beat]
```

2. **Set up Celery Beat with FastAPI**:

```python
from celery import Celery
from celery.schedules import crontab

celery_app = Celery(
    'worker',
    broker='redis://localhost:6379/0',
    backend='redis://localhost:6379/0'
)

@celery_app.task
def scheduled_task():
    print("Scheduled task executed!")

# Configure Celery Beat (use crontab for scheduling)
celery_app.conf.beat_schedule = {
    'run-every-minute': {
        'task': 'celery_worker.scheduled_task',
        'schedule': crontab(minute='*/1'),  # Run every minute
    },
}

celery_app.conf.timezone = 'UTC'
```

* The `crontab` trigger allows you to run tasks at specific times (e.g., every minute, daily, etc.).

---

### ✅ **4. Summary**

| **Method**                     | **Use Case**                                         |
| ------------------------------ | ---------------------------------------------------- |
| **FastAPI `BackgroundTasks`**  | Lightweight background tasks (e.g., emails, logging) |
| **Celery with Redis/RabbitMQ** | Heavy, long-running tasks (e.g., data processing)    |
| **APScheduler**                | Simple scheduled tasks (e.g., recurring tasks)       |
| **Celery Beat**                | Scheduled jobs with distributed task handling        |

---

### Conclusion

* **FastAPI BackgroundTasks** is great for simple, quick background tasks like sending emails or logging, without blocking the request cycle.
* **Celery with Redis/RabbitMQ** is ideal for more complex tasks that need to be distributed across workers, such as data processing or integrating with other systems.
* **APScheduler** and **Celery Beat** help you manage scheduled jobs, such as periodic reports or recurring tasks.

Let's dive into **Testing** in FastAPI!

Testing is a crucial part of developing high-quality, maintainable applications. FastAPI has built-in support for testing, and it integrates seamlessly with **pytest**, the popular Python testing framework. Below are key concepts and techniques for testing FastAPI applications.

---

## 🟡 Advanced Level: Optimizing FastAPI

### 12. 🧪 **Testing FastAPI Applications**

Testing FastAPI apps is straightforward thanks to **TestClient** and **dependency overrides**. Here’s how you can set up and structure tests for FastAPI projects.

---

### ✅ **1. Using `pytest` with FastAPI**

First, ensure you have `pytest` installed:

```bash
pip install pytest
```

#### Example FastAPI App:

```python
from fastapi import FastAPI, HTTPException

app = FastAPI()

@app.get("/items/{item_id}")
async def read_item(item_id: int):
    if item_id == 0:
        raise HTTPException(status_code=404, detail="Item not found")
    return {"item_id": item_id}
```

#### Writing Tests with `pytest`:

To test this application, create a new file, such as `test_main.py`, in your project directory.

```python
import pytest
from fastapi.testclient import TestClient
from main import app  # Import your FastAPI app

client = TestClient(app)

def test_read_item():
    response = client.get("/items/1")
    assert response.status_code == 200
    assert response.json() == {"item_id": 1}

def test_read_item_not_found():
    response = client.get("/items/0")
    assert response.status_code == 404
    assert response.json() == {"detail": "Item not found"}
```

In this example:

* `TestClient` is used to simulate HTTP requests to your FastAPI app.
* The `test_read_item` function verifies that the app returns a 200 status code and correct JSON for an item.
* The `test_read_item_not_found` checks the behavior when an invalid item ID is provided.

#### Running the Tests:

```bash
pytest
```

`pytest` will automatically discover and run tests in files prefixed with `test_` or suffixed with `_test.py`.

---

### ✅ **2. Dependency Overrides in Tests**

In FastAPI, you can override dependencies during testing to mock database connections, external services, or other dependencies. This is particularly useful when you don’t want to interact with a real database during tests.

#### Example: Dependency Override

Suppose your app has a dependency to get a database session:

```python
from fastapi import Depends, FastAPI
from sqlalchemy.orm import Session

app = FastAPI()

# Database dependency
def get_db():
    db = Session()  # Hypothetical DB session
    try:
        yield db
    finally:
        db.close()

@app.get("/items/")
async def read_items(db: Session = Depends(get_db)):
    # Query database for items...
    return {"items": "example"}
```

To override the `get_db` dependency in tests, you can do the following:

```python
from fastapi.testclient import TestClient
from fastapi import Depends
import pytest
from main import app

# Mock database dependency
def override_get_db():
    class MockDB:
        def query(self):
            return "mocked data"
    return MockDB()

# Override dependency for testing
app.dependency_overrides[get_db] = override_get_db

client = TestClient(app)

def test_read_items():
    response = client.get("/items/")
    assert response.status_code == 200
    assert response.json() == {"items": "mocked data"}
```

In this example:

* `override_get_db` is a mock function that simulates a database session.
* `app.dependency_overrides[get_db] = override_get_db` replaces the real dependency with the mock for testing.

---

### ✅ **3. Test Client and Fixtures**

`pytest` fixtures are used to set up common test resources, such as database connections, app clients, or other shared resources.

#### Example: Using Fixtures

You can define a fixture to set up your FastAPI app and reuse it in multiple tests:

```python
import pytest
from fastapi.testclient import TestClient
from main import app

# Fixture to provide a TestClient instance
@pytest.fixture
def client():
    client = TestClient(app)
    yield client
    # Cleanup actions (if needed) after the test is run

def test_read_item(client):
    response = client.get("/items/1")
    assert response.status_code == 200
    assert response.json() == {"item_id": 1}

def test_read_item_not_found(client):
    response = client.get("/items/0")
    assert response.status_code == 404
    assert response.json() == {"detail": "Item not found"}
```

In this example, the `client` fixture creates a `TestClient` instance, and it's injected into each test that requires it.

---

### ✅ **4. Mocking External Services**

When your FastAPI app relies on external APIs or services, you can mock them during testing to avoid making actual requests.

#### Example: Mocking HTTP Requests with `pytest-mock`

1. **Install `pytest-mock`**:

```bash
pip install pytest-mock
```

2. **Mock External API Calls**:

Suppose your FastAPI app makes HTTP requests using `httpx`:

```python
import httpx
from fastapi import FastAPI

app = FastAPI()

@app.get("/external-data")
async def fetch_external_data():
    response = await httpx.get("https://api.external.com/data")
    return response.json()
```

In your test, you can mock the `httpx.get` method to return fake data:

```python
from fastapi.testclient import TestClient
import pytest
from main import app
import httpx

client = TestClient(app)

@pytest.fixture
def mock_http_get(mocker):
    mock_response = mocker.patch("httpx.get", return_value=httpx.Response(200, json={"data": "mocked"}))
    return mock_response

def test_fetch_external_data(mock_http_get):
    response = client.get("/external-data")
    assert response.status_code == 200
    assert response.json() == {"data": "mocked"}
```

In this test:

* `pytest-mock`'s `mocker.patch` is used to mock the `httpx.get` method, so it doesn't actually make an external HTTP request.
* The mock response returns a 200 status and mocked JSON data.

---

### ✅ **5. Summary of Testing Concepts**

| **Concept**                   | **Explanation**                                                     |
| ----------------------------- | ------------------------------------------------------------------- |
| **pytest**                    | Used for discovering and running tests in FastAPI projects.         |
| **TestClient**                | Simulates HTTP requests to your FastAPI app for testing.            |
| **Dependency Overrides**      | Replaces real dependencies with mock versions for testing.          |
| **Fixtures**                  | Used to set up common resources for tests (e.g., client, DB).       |
| **Mocking External Services** | Mock HTTP requests or external APIs to avoid external dependencies. |

---

### Conclusion

Testing FastAPI applications is seamless with **pytest** and **TestClient**. You can:

* Use **dependency overrides** to mock services like databases.
* Utilize **fixtures** for reusable setup logic.
* **Mock external services** to avoid actual HTTP requests during tests.

Let's explore **Documentation and OpenAPI** in FastAPI, a powerful feature that automatically generates interactive documentation for your API. This helps both developers and consumers of your API understand how to interact with it, making the development process much smoother.

---

## 🟡 Advanced Level: Optimizing FastAPI

### 13. 📚 **Documentation and OpenAPI**

FastAPI automatically generates interactive **Swagger** and **ReDoc** documentation based on the routes and models in your application. Additionally, it allows customization to improve the clarity and usability of the documentation.

---

### ✅ **1. Auto-generated Swagger Docs**

FastAPI automatically generates Swagger UI for your API, which provides a great interactive interface for testing and exploring your API.

#### Example:

Consider the following simple FastAPI application:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/{item_id}")
async def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "q": q}
```

Once you run the application using `uvicorn`, you can access the Swagger documentation by visiting:

```
http://127.0.0.1:8000/docs
```

This UI allows you to:

* View all available endpoints
* Test the endpoints by providing input directly from the UI
* See responses and status codes

---

### ✅ **2. Customizing Docs with Metadata**

You can provide additional metadata about your API that will appear in the auto-generated documentation. This can help make the documentation more descriptive and tailored to your needs.

#### Customizing OpenAPI Metadata:

You can pass metadata in the `FastAPI` constructor, such as the title, description, version, and terms of service:

```python
from fastapi import FastAPI

app = FastAPI(
    title="My API",
    description="This is a FastAPI application with detailed documentation.",
    version="1.0.0",
    terms_of_service="http://example.com/terms/",
    contact={
        "name": "API Support",
        "url": "http://example.com/support",
        "email": "support@example.com"
    },
    license_info={
        "name": "MIT License",
        "url": "http://example.com/license"
    }
)
```

This metadata will be visible in the Swagger UI and the OpenAPI schema.

---

### ✅ **3. Using `tags`, `summary`, and `description`**

FastAPI allows you to group routes, provide a summary for each endpoint, and give detailed descriptions to clarify their usage. This helps organize and explain your API more effectively.

#### Using `tags` to Group Routes:

Tags allow you to group related endpoints in the documentation:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/items/", tags=["items"])
async def get_items():
    return {"items": ["item1", "item2"]}

@app.get("/users/", tags=["users"])
async def get_users():
    return {"users": ["user1", "user2"]}
```

In the Swagger UI, these routes will be grouped under the "items" and "users" categories, respectively.

#### Using `summary` and `description`:

* **`summary`**: A short, one-line description of the endpoint’s purpose.
* **`description`**: A more detailed explanation of the endpoint’s functionality.

Example:

```python
@app.get("/items/{item_id}", tags=["items"], summary="Get a specific item", description="Retrieve an item by its ID. Optionally, provide a query parameter to filter results.")
async def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "q": q}
```

In this example:

* The **summary** provides a quick explanation of what the route does.
* The **description** offers more detailed context about the route's behavior.

Both **`summary`** and **`description`** are displayed in the Swagger UI.

---

### ✅ **4. Customizing OpenAPI Schema**

If you need to further customize the OpenAPI schema or add more details like additional metadata or responses, FastAPI gives you the ability to do so.

#### Customizing Responses:

You can provide custom responses and status codes for your endpoints. FastAPI will automatically include these in the OpenAPI documentation.

Example:

```python
from fastapi import FastAPI, HTTPException
from fastapi.responses import JSONResponse

app = FastAPI()

@app.get("/items/{item_id}")
async def read_item(item_id: int):
    if item_id == 0:
        raise HTTPException(status_code=404, detail="Item not found")
    return {"item_id": item_id}

@app.get("/custom-response", response_class=JSONResponse, status_code=200)
async def custom_response():
    return {"message": "This is a custom response"}
```

This will show the response schema in the Swagger documentation, making it easy for users to understand the expected response format.

---

### ✅ **5. Using ReDoc for Documentation**

FastAPI also automatically generates documentation using **ReDoc**, which is another excellent tool for rendering OpenAPI specifications.

#### Access ReDoc:

You can view ReDoc documentation at:

```
http://127.0.0.1:8000/redoc
```

While **Swagger UI** is interactive, **ReDoc** provides a more static, user-friendly, and detailed interface, particularly suited for large APIs.

---

### ✅ **6. Example: Complete Customized FastAPI App**

Here’s a complete example that demonstrates metadata, tags, summaries, descriptions, and responses:

```python
from fastapi import FastAPI, HTTPException
from typing import Optional

app = FastAPI(
    title="My Custom API",
    description="This API handles items and users in a fast and efficient way.",
    version="1.0.0",
    contact={
        "name": "Support Team",
        "url": "http://support.example.com",
        "email": "support@example.com"
    }
)

@app.get("/items/{item_id}", tags=["items"], summary="Get an item by ID", description="Fetch an item by its unique ID. If the item doesn't exist, it will return a 404 error.", responses={404: {"description": "Item not found"}})
async def read_item(item_id: int, q: Optional[str] = None):
    if item_id == 0:
        raise HTTPException(status_code=404, detail="Item not found")
    return {"item_id": item_id, "q": q}

@app.get("/users/{user_id}", tags=["users"], summary="Get user by ID", description="Fetch a user by their ID.")
async def get_user(user_id: int):
    return {"user_id": user_id, "name": f"User {user_id}"}
```

---

### ✅ **7. Custom OpenAPI Schema (Advanced)**

In some cases, you might want to manually edit the OpenAPI schema. FastAPI allows you to customize the OpenAPI schema by providing custom functions or adding custom components.

Here’s how you can override the default OpenAPI schema:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/openapi")
async def custom_openapi():
    return {"openapi": "custom"}  # Your custom OpenAPI spec
```

You can use this to add custom components or paths to your OpenAPI specification.

---

### ✅ **8. Summary of Documentation Features**

| **Feature**          | **Description**                                           |
| -------------------- | --------------------------------------------------------- |
| **Swagger UI**       | Interactive API documentation generated automatically.    |
| **ReDoc**            | Alternative documentation interface with detailed views.  |
| **Metadata**         | Custom metadata (e.g., title, description, version).      |
| **Tags**             | Group related endpoints in the documentation.             |
| **Summary**          | Brief description of each endpoint.                       |
| **Description**      | Detailed explanation of each endpoint’s purpose.          |
| **Custom Responses** | Define response schemas and status codes for better docs. |

---

### Conclusion

FastAPI makes it easy to create clear and interactive API documentation using **Swagger UI** and **ReDoc**. By customizing metadata, grouping endpoints with **tags**, and adding **summary** and **description** fields, you can significantly enhance the usability and clarity of your API documentation.

Let’s explore **File Uploads and Static Files** in FastAPI. This functionality is essential for building applications that need to handle user uploads, such as profile pictures, documents, or any other file types, as well as serving static files like images, stylesheets, and JavaScript files.

---

## 🟡 Advanced Level: Optimizing FastAPI

### 14. 📁 **File Uploads and Static Files**

FastAPI provides simple and efficient ways to handle file uploads, save them to the disk, and serve static files to the client.

---

### ✅ **1. Uploading Single and Multiple Files**

FastAPI makes it easy to upload files through form data using the `File` and `Form` classes from `fastapi`. You can upload a single file or multiple files with just a few lines of code.

#### Uploading a Single File:

To upload a single file, you use the `File` class to define the file parameter in your route:

```python
from fastapi import FastAPI, File, UploadFile
from typing import List

app = FastAPI()

@app.post("/uploadfile/")
async def upload_file(file: UploadFile = File(...)):
    # Read the contents of the file
    contents = await file.read()
    
    # Optionally, save it to disk
    with open(f"uploaded_{file.filename}", "wb") as f:
        f.write(contents)
    
    return {"filename": file.filename}
```

In this example:

* The `UploadFile` class represents the uploaded file. It’s an abstraction over `BytesIO`, which helps avoid memory issues when handling large files.
* The `File(...)` is a dependency that extracts the uploaded file from the request.

#### Uploading Multiple Files:

You can extend this by allowing users to upload multiple files:

```python
@app.post("/uploadfiles/")
async def upload_files(files: List[UploadFile] = File(...)):
    for file in files:
        # Process each file
        contents = await file.read()
        with open(f"uploaded_{file.filename}", "wb") as f:
            f.write(contents)
    
    return {"filenames": [file.filename for file in files]}
```

* **`List[UploadFile]`**: This allows you to accept multiple files, and FastAPI will handle it as a list of `UploadFile` objects.

---

### ✅ **2. Saving Files to Disk**

When saving uploaded files to disk, you can easily manage the file path and handle naming conflicts. Here’s a more detailed example of saving files with unique names:

```python
import os
from fastapi import FastAPI, File, UploadFile
from uuid import uuid4

app = FastAPI()

UPLOAD_FOLDER = "uploaded_files"
os.makedirs(UPLOAD_FOLDER, exist_ok=True)

@app.post("/uploadfile/")
async def upload_file(file: UploadFile = File(...)):
    file_extension = file.filename.split(".")[-1]
    file_id = str(uuid4())  # Unique identifier to avoid name collisions
    file_path = os.path.join(UPLOAD_FOLDER, f"{file_id}.{file_extension}")
    
    # Save the file to the disk
    with open(file_path, "wb") as f:
        f.write(await file.read())
    
    return {"filename": file.filename, "file_path": file_path}
```

In this example:

* The uploaded file is saved to a specific folder (`uploaded_files`).
* Each file gets a unique name by generating a UUID and using it in the file’s name.
* We also extract the file extension to keep the original format.

---

### ✅ **3. Serving Static Files**

Once files are uploaded and saved, you might want to serve them as static content. FastAPI makes this easy with the `StaticFiles` middleware.

#### Serving Static Files:

```python
from fastapi import FastAPI
from fastapi.staticfiles import StaticFiles

app = FastAPI()

# Serve static files from a folder called "static"
app.mount("/static", StaticFiles(directory="static"), name="static")
```

* This example will serve static files located in the `static` folder in the project directory.
* Files can be accessed at `http://127.0.0.1:8000/static/<filename>`, e.g., `http://127.0.0.1:8000/static/image.jpg`.

#### Custom Static File Serving:

You can also set up routes to serve specific files dynamically, perhaps based on a database entry or user request.

```python
from fastapi.responses import FileResponse

@app.get("/get-file/{file_name}")
async def get_file(file_name: str):
    file_path = f"./uploaded_files/{file_name}"
    return FileResponse(file_path)
```

* This allows you to return any file stored in the `uploaded_files` directory as a response. The user will be able to download the file via this endpoint.

---

### ✅ **4. File Upload Validation and Limits**

You might want to restrict the file size or check for specific file types during the upload process. FastAPI provides a way to handle these checks easily.

#### File Size Limitation:

To limit file size, you can use the `max_length` parameter of the `File` class:

```python
from fastapi import FastAPI, File, UploadFile, HTTPException

app = FastAPI()

MAX_FILE_SIZE = 10 * 1024 * 1024  # 10 MB

@app.post("/uploadfile/")
async def upload_file(file: UploadFile = File(...)):
    # Check file size
    if len(await file.read()) > MAX_FILE_SIZE:
        raise HTTPException(status_code=400, detail="File is too large")
    
    # Save file logic...
    return {"filename": file.filename}
```

* **File Size Check**: This checks the size of the uploaded file before saving it to disk. If the file exceeds the defined size, an exception is raised.

#### File Type Validation:

You can also validate the file type by checking the file’s extension or MIME type:

```python
ALLOWED_EXTENSIONS = {"jpg", "jpeg", "png", "gif"}

@app.post("/uploadfile/")
async def upload_file(file: UploadFile = File(...)):
    file_extension = file.filename.split(".")[-1].lower()
    if file_extension not in ALLOWED_EXTENSIONS:
        raise HTTPException(status_code=400, detail="Invalid file type")
    
    # Save file logic...
    return {"filename": file.filename}
```

* **File Type Check**: This example checks that the uploaded file has a valid extension before allowing the upload.

---

### ✅ **5. Example: Complete File Upload and Static File Example**

Here’s a complete example of a FastAPI app that handles both file uploads and static file serving:

```python
import os
from fastapi import FastAPI, File, UploadFile, HTTPException
from fastapi.staticfiles import StaticFiles
from uuid import uuid4

app = FastAPI()

UPLOAD_FOLDER = "uploaded_files"
os.makedirs(UPLOAD_FOLDER, exist_ok=True)

# Serve static files from the "uploaded_files" folder
app.mount("/static", StaticFiles(directory=UPLOAD_FOLDER), name="static")

@app.post("/uploadfile/")
async def upload_file(file: UploadFile = File(...)):
    file_extension = file.filename.split(".")[-1]
    file_id = str(uuid4())  # Generate unique ID
    file_path = os.path.join(UPLOAD_FOLDER, f"{file_id}.{file_extension}")
    
    # Save file to disk
    with open(file_path, "wb") as f:
        f.write(await file.read())
    
    return {"filename": file.filename, "file_path": f"/static/{file_id}.{file_extension}"}

@app.get("/get-file/{file_name}")
async def get_file(file_name: str):
    file_path = os.path.join(UPLOAD_FOLDER, file_name)
    if not os.path.exists(file_path):
        raise HTTPException(status_code=404, detail="File not found")
    return FileResponse(file_path)
```

In this example:

* Users can upload a file via `/uploadfile/`, and the file is saved with a unique name.
* The uploaded file is served from the `/static/` URL.
* You can also retrieve files directly via the `/get-file/{file_name}` endpoint.

---

### ✅ **6. Summary of File Uploads and Static Files**

| **Feature**                  | **Description**                                                     |
| ---------------------------- | ------------------------------------------------------------------- |
| **Uploading Single File**    | Upload one file using `UploadFile` and `File`.                      |
| **Uploading Multiple Files** | Upload multiple files using `List[UploadFile]`.                     |
| **Saving Files to Disk**     | Save uploaded files to disk, possibly with unique names using UUID. |
| **Serving Static Files**     | Serve static files using the `StaticFiles` middleware.              |
| **File Size Limitation**     | Set file size limits with the `max_length` parameter.               |
| **File Type Validation**     | Check file extensions or MIME types for validation.                 |

---

### Conclusion

FastAPI provides robust support for file uploads and static file serving, with features like automatic size validation, file type checks, and dynamic file serving. It’s an excellent choice for applications that require user-generated content or media handling.

### 🔴 **Expert Level: Deployment, CI/CD, and Scaling**

---

## **15. Dockerizing FastAPI**

Dockerizing your FastAPI application allows you to create a containerized environment for your app, which can run consistently across various environments (local, testing, production). This is a critical step for making your application portable, scalable, and easily deployable.

Here’s a comprehensive guide for **Dockerizing FastAPI**.

---

### ✅ **1. Dockerfile and `.dockerignore`**

#### **Creating a Dockerfile**

The **Dockerfile** is a script that contains instructions to build the Docker image for your FastAPI application.

Here’s a typical `Dockerfile` for a FastAPI app:

```dockerfile
# Use official Python image as base
FROM python:3.9-slim

# Set environment variables to prevent Python from writing pyc files to disc
# and to enable unbuffered output, which is useful for logging
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set the working directory in the container
WORKDIR /app

# Copy the requirements.txt first to leverage Docker cache
COPY requirements.txt /app/

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the entire project
COPY . /app/

# Expose the port FastAPI will run on
EXPOSE 8000

# Command to run the app using Uvicorn in production mode
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]
```

### Explanation:

* **FROM python:3.9-slim**: The base image is a lightweight version of Python.
* **ENV**: These environment variables ensure no `.pyc` files are created and that output is unbuffered.
* **WORKDIR /app**: Sets the working directory inside the container to `/app`.
* **COPY requirements.txt /app/**: First, copy only the `requirements.txt` to leverage Docker's caching mechanism (this avoids re-installing packages every time).
* **RUN pip install**: Installs the dependencies inside the container.
* **COPY . /app/**: Copy the entire project into the container.
* **EXPOSE 8000**: Exposes port 8000 (the default FastAPI port).
* **CMD**: The command that runs FastAPI using **Uvicorn**. We use `--reload` for development; for production, this should be omitted.

---

#### **Creating a `.dockerignore`**

A `.dockerignore` file is important to prevent unnecessary files from being included in the Docker image. It’s similar to `.gitignore`.

Example `.dockerignore`:

```
__pycache__
*.pyc
*.pyo
*.pyd
.env
.git
.gitignore
tests/
```

This will prevent the inclusion of unnecessary files such as Python bytecode, environment files, or test directories, which aren’t required in the production environment.

---

### ✅ **2. Building and Running FastAPI with Docker**

#### **Building the Docker Image**

Once your `Dockerfile` is ready, you can build the Docker image using the `docker build` command.

```bash
docker build -t fastapi-app .
```

* **-t fastapi-app**: Tags the image with the name `fastapi-app`.

#### **Running the Docker Container**

To run the FastAPI app in a container, use the `docker run` command:

```bash
docker run -d -p 8000:8000 fastapi-app
```

* **-d**: Runs the container in detached mode (in the background).
* **-p 8000:8000**: Maps port 8000 on the host machine to port 8000 in the container.

Now, your FastAPI app will be accessible on `http://localhost:8000`.

---

### ✅ **3. Using `docker-compose` with DB and App**

`docker-compose` allows you to define and run multi-container Docker applications. It’s perfect when your FastAPI app requires other services, like a database (PostgreSQL, MySQL, etc.).

Here’s an example `docker-compose.yml` for FastAPI and PostgreSQL:

#### **docker-compose.yml**

```yaml
version: '3.8'

services:
  fastapi:
    build: .
    container_name: fastapi_app
    ports:
      - "8000:8000"
    depends_on:
      - db
    environment:
      - DATABASE_URL=postgresql://user:password@db:5432/mydb
    networks:
      - fastapi-network

  db:
    image: postgres:13
    container_name: fastapi_db
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=mydb
    ports:
      - "5432:5432"
    networks:
      - fastapi-network

networks:
  fastapi-network:
    driver: bridge
```

#### Explanation:

* **fastapi**: The FastAPI app service. It builds the image from the Dockerfile, maps port 8000, and waits for the `db` service to start.
* **db**: A PostgreSQL service. We use the official `postgres:13` image. The `POSTGRES_*` environment variables are used to configure the database user, password, and database.
* **depends\_on**: Ensures the FastAPI app waits until the database is available.
* **networks**: Defines a custom network to allow communication between services.
* **DATABASE\_URL**: You can pass environment variables like `DATABASE_URL` to the FastAPI app to connect to the database.

---

#### **Running the Containers**

Once your `docker-compose.yml` is ready, you can use `docker-compose` to build and start the services.

1. **Build the containers:**

```bash
docker-compose build
```

2. **Start the containers:**

```bash
docker-compose up
```

3. **Stop the containers:**

```bash
docker-compose down
```

Now, FastAPI will be running on `http://localhost:8000` and connected to a PostgreSQL database on `localhost:5432`.

---

### ✅ **4. Optimizing Docker for Production**

In a production environment, you might want to optimize the Docker image and container to improve security, performance, and scalability.

#### **Using a Multi-Stage Dockerfile**

A multi-stage Dockerfile is a way to build your image in stages, keeping the final image smaller by excluding unnecessary build dependencies.

```dockerfile
# Build stage
FROM python:3.9-slim AS build

WORKDIR /app

COPY requirements.txt /app/
RUN pip install --no-cache-dir -r requirements.txt

# Production stage
FROM python:3.9-slim

WORKDIR /app

COPY --from=build /app /app

COPY . /app/

EXPOSE 8000

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

* **Build Stage**: This stage installs dependencies and prepares everything.
* **Production Stage**: This stage copies only the necessary files from the build stage into the production image.

---

#### **Using `gunicorn` for Production**

For production environments, it’s common to use `gunicorn` as a web server to serve FastAPI. You can configure `gunicorn` with Uvicorn workers.

```bash
CMD ["gunicorn", "-w", "4", "-k", "uvicorn.workers.UvicornWorker", "main:app"]
```

This will run the app using 4 workers for better concurrency.

---

### ✅ **5. Automating Deployment with CI/CD**

For a seamless development-to-production pipeline, integrating **CI/CD (Continuous Integration / Continuous Deployment)** is key.

Here’s a simple **GitHub Actions** workflow for CI/CD with Docker:

#### **.github/workflows/deploy.yml**

```yaml
name: Deploy FastAPI to Docker

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Docker
        uses: docker/setup-buildx-action@v1

      - name: Build Docker image
        run: |
          docker build -t your_dockerhub_username/fastapi-app .

      - name: Push Docker image
        run: |
          docker push your_dockerhub_username/fastapi-app

      - name: Deploy to server (optional)
        run: |
          ssh username@your_server 'docker pull your_dockerhub_username/fastapi-app && docker run -d -p 8000:8000 fastapi-app'
```

In this example:

* The workflow triggers on pushes to the `main` branch.
* It builds the Docker image and pushes it to Docker Hub.
* The last step deploys the updated image to a server (this step would be tailored to your server setup).

---

### ✅ **6. Summary of Dockerizing FastAPI**

| **Topic**                   | **Description**                                                                   |
| --------------------------- | --------------------------------------------------------------------------------- |
| **Dockerfile**              | Defines the build instructions for the FastAPI app Docker image.                  |
| **.dockerignore**           | Prevents unnecessary files from being included in the Docker image.               |
| **Docker Run**              | Runs the FastAPI app in a Docker container.                                       |
| **docker-compose**          | Orchestrates multi-container applications (e.g., FastAPI + DB).                   |
| **Production Optimization** | Multi-stage builds, using `gunicorn` for production, and image size optimization. |
| **CI/CD with Docker**       | GitHub Actions or other CI/CD tools to automate the Docker deployment process.    |

---

### Conclusion

Dockerizing FastAPI ensures portability and simplifies deployment. By using **Docker Compose**, you can integrate services like databases seamlessly. For production, optimizing the image size and using a production server like **gunicorn** can improve performance.

### 🔴 **Expert Level: Deployment, CI/CD, and Scaling**

---

## **16. Deployment**

Deploying your FastAPI application in a production environment is crucial for scaling, ensuring reliability, and delivering high performance. This section covers the deployment process on different platforms (AWS EC2, DigitalOcean, Railway/Render), as well as setting up **Gunicorn + Uvicorn** workers and **Nginx** as a reverse proxy for production.

---

### ✅ **1. Deploying to AWS EC2**

AWS EC2 (Elastic Compute Cloud) provides scalable virtual servers to host your FastAPI application. Here's a step-by-step guide to deploy FastAPI to EC2.

#### **Steps to Deploy FastAPI to AWS EC2:**

1. **Create an EC2 Instance**:

   * Go to the **AWS Management Console**.
   * Launch a new EC2 instance (choose an appropriate AMI like **Ubuntu Server**).
   * Set up security groups to allow traffic on port 22 (SSH), 80 (HTTP), and 443 (HTTPS).
   * Create and download an **SSH key pair** for connecting to the instance.

2. **SSH into EC2**:
   Use the downloaded `.pem` key to SSH into your EC2 instance:

   ```bash
   chmod 400 your-key.pem
   ssh -i "your-key.pem" ubuntu@your-ec2-ip
   ```

3. **Update System & Install Dependencies**:
   Update the system and install necessary dependencies:

   ```bash
   sudo apt update
   sudo apt install python3-pip python3-venv git
   ```

4. **Set Up Virtual Environment**:
   On your EC2 instance, set up a Python virtual environment and install your app’s dependencies.

   ```bash
   python3 -m venv fastapi-env
   source fastapi-env/bin/activate
   git clone your-repository-url
   cd your-repository
   pip install -r requirements.txt
   ```

5. **Install Gunicorn + Uvicorn**:
   Install **Gunicorn** (with **Uvicorn** worker) to serve the FastAPI app.

   ```bash
   pip install gunicorn uvicorn
   ```

6. **Run FastAPI with Gunicorn**:
   You can run the app using Gunicorn and Uvicorn as workers:

   ```bash
   gunicorn -w 4 -k uvicorn.workers.UvicornWorker main:app --bind 0.0.0.0:8000
   ```

   * `-w 4`: Start 4 workers.
   * `-k uvicorn.workers.UvicornWorker`: Use Uvicorn as the worker class.

7. **Set Up Reverse Proxy with Nginx**:
   For better performance and security, use **Nginx** as a reverse proxy.

   * Install Nginx:

     ```bash
     sudo apt install nginx
     ```

   * Configure Nginx to forward traffic from port 80 to Gunicorn (port 8000).

   **Create an Nginx configuration file:**

   ```bash
   sudo nano /etc/nginx/sites-available/fastapi
   ```

   Add the following configuration:

   ```nginx
   server {
       listen 80;
       server_name your-ec2-public-ip-or-domain;

       location / {
           proxy_pass http://127.0.0.1:8000;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header X-Forwarded-Proto $scheme;
       }
   }
   ```

   * Enable the Nginx configuration:

     ```bash
     sudo ln -s /etc/nginx/sites-available/fastapi /etc/nginx/sites-enabled
     sudo systemctl restart nginx
     ```

8. **Allow Traffic on Port 80**:
   Ensure that your EC2 security group allows HTTP traffic on port 80. You can do this in the AWS Management Console.

9. **Access the FastAPI App**:
   Your FastAPI app should now be accessible via your EC2 public IP address or domain name.

---

### ✅ **2. Deploying to DigitalOcean**

DigitalOcean provides cost-effective cloud infrastructure to deploy web apps. Here’s how to deploy FastAPI on DigitalOcean.

#### **Steps to Deploy FastAPI to DigitalOcean:**

1. **Create a DigitalOcean Droplet**:

   * Sign up for a DigitalOcean account and create a new Droplet (Ubuntu is a good choice).
   * Set up SSH keys for secure login.

2. **SSH into the Droplet**:
   Once the Droplet is created, SSH into it:

   ```bash
   ssh root@your-droplet-ip
   ```

3. **Install Dependencies**:
   On the Droplet, install Python, pip, and virtualenv:

   ```bash
   sudo apt update
   sudo apt install python3-pip python3-venv git
   ```

4. **Clone Your Project**:
   Clone your FastAPI project from GitHub or any other version control system:

   ```bash
   git clone your-repository-url
   cd your-repository
   ```

5. **Set Up Virtual Environment**:
   Create and activate a virtual environment:

   ```bash
   python3 -m venv fastapi-env
   source fastapi-env/bin/activate
   ```

6. **Install Project Dependencies**:
   Install the dependencies listed in `requirements.txt`:

   ```bash
   pip install -r requirements.txt
   ```

7. **Install Gunicorn + Uvicorn**:
   Install Gunicorn and Uvicorn workers for serving FastAPI:

   ```bash
   pip install gunicorn uvicorn
   ```

8. **Run the FastAPI App with Gunicorn**:
   Run FastAPI using Gunicorn with Uvicorn workers:

   ```bash
   gunicorn -w 4 -k uvicorn.workers.UvicornWorker main:app --bind 0.0.0.0:8000
   ```

9. **Set Up Nginx**:
   Install and configure Nginx as a reverse proxy (similar to AWS EC2 deployment). You can follow the same steps as mentioned above in the EC2 section.

10. **Access the FastAPI App**:
    Your FastAPI app should now be live on your DigitalOcean droplet’s IP address or domain name.

---

### ✅ **3. Deploying to Railway/Render**

Platforms like **Railway** and **Render** offer serverless deployment options with minimal configuration.

#### **Deploying FastAPI to Railway:**

1. **Create a Railway Account**:

   * Sign up for Railway ([https://railway.app](https://railway.app)).

2. **Create a New Project**:

   * Connect your GitHub repository with your Railway account.
   * Select your FastAPI repository.

3. **Configure Railway Environment**:
   Railway will automatically detect the Python app and deploy it.

   * If Railway doesn’t automatically detect dependencies, you can create a `Dockerfile` and set up a `Procfile`.

4. **Deploy**:
   Railway will deploy your app and provide a public URL once it’s done.

#### **Deploying FastAPI to Render:**

1. **Create a Render Account**:

   * Sign up for Render ([https://render.com](https://render.com)).

2. **Create a New Web Service**:

   * Choose the option to deploy a **Web Service**.
   * Connect your GitHub repository to Render.

3. **Configure Render**:

   * Render automatically detects your Python app and installs dependencies.
   * You can set up environment variables and custom Dockerfiles if necessary.

4. **Deploy**:
   Once configured, Render will deploy your app, providing a live URL.

---

### ✅ **4. Running with Gunicorn + Uvicorn Workers**

When deploying FastAPI, it's common to use **Gunicorn** with **Uvicorn workers** for performance and scalability.

* **Gunicorn**: WSGI server for Python web apps.
* **Uvicorn**: ASGI server for async applications, like FastAPI.

To run the app with Gunicorn and Uvicorn workers:

```bash
gunicorn -w 4 -k uvicorn.workers.UvicornWorker main:app --bind 0.0.0.0:8000
```

* `-w 4`: Number of worker processes (typically set based on the number of CPUs).
* `-k uvicorn.workers.UvicornWorker`: Specifies Uvicorn as the worker class.
* `main:app`: Refers to the FastAPI app in `main.py`.

---

### ✅ **5. Reverse Proxy with Nginx**

A reverse proxy is crucial for forwarding requests to your FastAPI application, as well as handling HTTPS encryption.

1. **Install Nginx**:

   ```bash
   sudo apt install nginx
   ```

2. **Configure Nginx**:
   Create a new config file for your FastAPI app in `/etc/nginx/sites-available/fastapi`:

   ```nginx
   server {
       listen 80;
       server_name your-domain-or-ip;

       location / {
           proxy_pass http://127.0.0.1:8000;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header X-Forwarded-Proto $scheme;
       }
   }
   ```

3. **Enable Configuration**:

   ```bash
   sudo ln -s /etc/nginx/sites-available/fastapi /etc/nginx/sites-enabled
   sudo systemctl restart nginx
   ```

4. **Secure with SSL** (optional):
   Use **Let's Encrypt** to set up SSL for HTTPS:

   ```bash
   sudo apt install certbot python3-certbot-nginx
   sudo certbot --nginx -d your-domain.com
   ```

---

### Conclusion

Now, you have several deployment options for your FastAPI app:

* **AWS EC2**: Provides full control over the server.
* **DigitalOcean**: Simple and affordable cloud hosting.
* **Railway/Render**: Serverless, automatic deployment for quick setups.
* **Gunicorn + Uvicorn**: Best practice for serving FastAPI in production.
* **Nginx**: Reverse proxy for performance and security.

### 🔴 **Expert Level: CI/CD, Performance, and Scaling**

---

## **17. CI/CD Integration**

Continuous Integration (CI) and Continuous Deployment (CD) pipelines are crucial for automating the testing, building, and deployment of your FastAPI applications. GitHub Actions is a great tool to streamline these processes.

### ✅ **1. GitHub Actions for Lint, Test, Build, and Deploy**

GitHub Actions allow you to automate various tasks in your development workflow. Here's how to set up a CI/CD pipeline for a FastAPI project using GitHub Actions.

#### **Steps to Set Up GitHub Actions for FastAPI:**

1. **Create a GitHub Workflow File**:
   Create a `.github/workflows/ci.yml` file in your project root directory.

2. **Define the Workflow**:
   Below is an example of a CI/CD workflow that performs linting, testing, building, and deploying a FastAPI app.

   ```yaml
   name: FastAPI CI/CD Pipeline

   on:
     push:
       branches:
         - main
     pull_request:
       branches:
         - main

   jobs:
     lint:
       runs-on: ubuntu-latest
       steps:
         - name: Checkout code
           uses: actions/checkout@v2

         - name: Set up Python
           uses: actions/setup-python@v2
           with:
             python-version: 3.9

         - name: Install dependencies
           run: |
             python -m venv venv
             source venv/bin/activate
             pip install -r requirements.txt

         - name: Run Linter (flake8)
           run: |
             source venv/bin/activate
             flake8 .

     test:
       runs-on: ubuntu-latest
       needs: lint
       steps:
         - name: Checkout code
           uses: actions/checkout@v2

         - name: Set up Python
           uses: actions/setup-python@v2
           with:
             python-version: 3.9

         - name: Install dependencies
           run: |
             python -m venv venv
             source venv/bin/activate
             pip install -r requirements.txt

         - name: Run Tests (pytest)
           run: |
             source venv/bin/activate
             pytest --maxfail=1 --disable-warnings -q

     build:
       runs-on: ubuntu-latest
       needs: test
       steps:
         - name: Checkout code
           uses: actions/checkout@v2

         - name: Set up Python
           uses: actions/setup-python@v2
           with:
             python-version: 3.9

         - name: Install dependencies
           run: |
             python -m venv venv
             source venv/bin/activate
             pip install -r requirements.txt

         - name: Build Docker Image
           run: |
             docker build -t your-image-name .

     deploy:
       runs-on: ubuntu-latest
       needs: build
       steps:
         - name: Checkout code
           uses: actions/checkout@v2

         - name: Set up Python
           uses: actions/setup-python@v2
           with:
             python-version: 3.9

         - name: Install dependencies
           run: |
             python -m venv venv
             source venv/bin/activate
             pip install -r requirements.txt

         - name: Deploy to AWS EC2
           run: |
             ssh -o StrictHostKeyChecking=no -i ${{ secrets.EC2_SSH_KEY }} ubuntu@${{ secrets.EC2_IP }} 'bash -s' < deploy_script.sh
           env:
             EC2_SSH_KEY: ${{ secrets.EC2_SSH_KEY }}
             EC2_IP: ${{ secrets.EC2_IP }}
   ```

#### **Explanation of Workflow**:

* **Lint Job**: Runs `flake8` to ensure code quality and style compliance.
* **Test Job**: Executes tests using `pytest` to make sure the code works as expected.
* **Build Job**: Builds a Docker image for your FastAPI app.
* **Deploy Job**: Deploys the Docker image to an EC2 instance using SSH. You’ll need to create a `deploy_script.sh` that handles the deployment process.

---

### ✅ **2. Example CI/CD Workflow for FastAPI**

The workflow example above integrates multiple steps into one pipeline. Here is a quick breakdown:

* **Push to Main Branch**: The workflow triggers on every push to the `main` branch.
* **Linting**: Ensures your code follows the set style guide using `flake8`.
* **Testing**: Runs your test suite using `pytest`.
* **Build**: Builds a Docker image of your app.
* **Deploy**: Deploys your FastAPI app to a server, such as AWS EC2.

You can adapt this workflow to fit your specific needs and deployment platform (e.g., AWS, DigitalOcean, etc.).

---

## **18. Rate Limiting, Caching, and Performance**

In production, it’s important to consider performance optimizations like rate limiting, caching, and monitoring.

### ✅ **1. Redis for Caching and Rate Limiting**

**Redis** is a powerful in-memory data structure store that is often used for caching and rate limiting. It can drastically improve the performance of your FastAPI application by reducing database load and limiting the number of requests a user can make.

#### **Steps to Integrate Redis for Rate Limiting and Caching:**

1. **Install Redis and aioredis**:

   * Install the Redis server (make sure Redis is running on your system or Docker container).
   * Install the `aioredis` library for async interaction with Redis:

     ```bash
     pip install aioredis
     ```

2. **Basic Redis Caching**:

   You can use Redis to cache data that doesn’t change frequently, improving the performance of your FastAPI app.

   ```python
   import aioredis
   from fastapi import FastAPI

   app = FastAPI()

   # Create a Redis connection pool
   redis = aioredis.from_url("redis://localhost", decode_responses=True)

   @app.get("/cache-example")
   async def get_data():
       # Try to fetch data from Redis
       data = await redis.get("my_data_key")
       if not data:
           # If no data in cache, simulate fetching from DB
           data = "Fetched from database"
           await redis.set("my_data_key", data)
       return {"data": data}
   ```

3. **Rate Limiting with Redis**:

   Rate limiting restricts how often a client can access a specific resource. Redis can store request timestamps and enforce rate limits.

   Example of rate limiting logic using Redis:

   ```python
   from fastapi import HTTPException
   import aioredis
   from datetime import datetime, timedelta

   redis = aioredis.from_url("redis://localhost", decode_responses=True)

   @app.get("/rate-limited")
   async def rate_limited(endpoint: str):
       user_id = "user_123"  # This could be fetched from authentication data
       current_time = datetime.now()

       # Check if the user has exceeded the allowed rate limit
       last_request_time = await redis.get(f"last_request_time:{user_id}")
       if last_request_time:
           last_request_time = datetime.fromisoformat(last_request_time)
           if current_time - last_request_time < timedelta(seconds=60):
               raise HTTPException(status_code=429, detail="Too many requests")

       # Update last request time in Redis
       await redis.set(f"last_request_time:{user_id}", current_time.isoformat())
       return {"message": "Request successful"}
   ```

---

### ✅ **2. Async Caching with aioredis**

When working with async frameworks like FastAPI, it’s important to use asynchronous Redis clients. `aioredis` is designed to work seamlessly with FastAPI’s async capabilities, ensuring non-blocking operations.

#### **Example of Async Caching with aioredis**:

```python
import aioredis
from fastapi import FastAPI

app = FastAPI()

# Async Redis client
redis = aioredis.from_url("redis://localhost", decode_responses=True)

@app.get("/get-cache/{key}")
async def get_cache(key: str):
    # Fetch from Redis
    value = await redis.get(key)
    if value is None:
        return {"message": "Cache miss"}
    return {"key": key, "value": value}

@app.post("/set-cache/{key}")
async def set_cache(key: str, value: str):
    # Set data in Redis
    await redis.set(key, value)
    return {"message": "Cache set successfully"}
```

---

### ✅ **3. Performance Profiling with py-spy and Locust**

Performance profiling is crucial to identify bottlenecks in your application and ensure scalability.

#### **Using py-spy for Profiling**:

**`py-spy`** is a Python profiler that helps you visualize performance bottlenecks in real-time.

1. Install **py-spy**:

   ```bash
   pip install py-spy
   ```

2. Run **py-spy** to profile your FastAPI app:

   ```bash
   py-spy top --pid <your_fastapi_pid>
   ```

   This will give you real-time profiling data, such as which functions are taking the most time.

#### **Using Locust for Load Testing**:

**`Locust`** is a powerful tool for load testing web applications.

1. Install **locust**:

   ```bash
   pip install locust
   ```

2. Create a `locustfile.py` to define the load test:

   ```python
   from locust import HttpUser, task

   class FastAPIUser(HttpUser):
       @task
       def get_home(self):
           self.client.get("/")

   ```

3. Run Locust:

   ```bash
   locust -f locustfile.py
   ```

   This will start a web interface for testing the performance of your FastAPI app under load.

---

### Conclusion

With **CI/CD pipelines**, **Redis for caching and rate limiting**, and **performance profiling** using tools like **py-spy** and **Locust**, you can streamline your development, improve your app's performance, and handle production-scale traffic effectively. These tools and practices will help ensure that your FastAPI application is production-ready, scalable, and resilient.

### 🔴 **Expert Level: WebSockets & Streaming**

---

## **19. WebSockets & Streaming**

Real-time data communication is crucial for many modern web applications, such as chat apps, live dashboards, and collaborative platforms. FastAPI provides excellent support for WebSockets and Server-Sent Events (SSE), which allows for two-way communication between the server and the client, making real-time updates seamless and efficient.

### ✅ **1. Real-Time Data with WebSockets**

WebSockets enable full-duplex communication channels over a single, long-lived connection. This is perfect for applications requiring real-time updates like chat systems or live notifications.

#### **Steps to Implement WebSockets with FastAPI**:

1. **Install FastAPI and Uvicorn** (if you haven't already):

   ```bash
   pip install fastapi uvicorn
   ```

2. **Basic WebSocket Example**:

   Here's how you can set up a WebSocket server with FastAPI:

   ```python
   from fastapi import FastAPI, WebSocket
   from fastapi.responses import HTMLResponse

   app = FastAPI()

   # WebSocket route
   @app.websocket("/ws/{client_id}")
   async def websocket_endpoint(websocket: WebSocket, client_id: str):
       await websocket.accept()
       await websocket.send_text(f"Hello, Client {client_id}!")
       while True:
           data = await websocket.receive_text()
           await websocket.send_text(f"Message from client {client_id}: {data}")

   # HTML page to test WebSocket connection
   @app.get("/")
   async def get():
       return HTMLResponse("""
       <html>
           <body>
               <h1>WebSocket Test</h1>
               <input type="text" id="messageInput" placeholder="Type a message">
               <button onclick="sendMessage()">Send</button>
               <p id="response"></p>
               <script>
                   const socket = new WebSocket("ws://localhost:8000/ws/123");

                   socket.onopen = () => {
                       console.log("Connected to WebSocket");
                   };

                   socket.onmessage = (event) => {
                       document.getElementById("response").innerText = event.data;
                   };

                   function sendMessage() {
                       const message = document.getElementById("messageInput").value;
                       socket.send(message);
                   }
               </script>
           </body>
       </html>
       """)
   ```

   **Explanation**:

   * **WebSocket Endpoint**: The `/ws/{client_id}` route opens a WebSocket connection and continuously listens for messages from the client.
   * **Client-side Code**: A simple HTML page that connects to the WebSocket server and sends/receives messages.

3. **Run the Application**:
   To run the FastAPI app, use `uvicorn`:

   ```bash
   uvicorn main:app --reload
   ```

   Access the WebSocket test page by visiting `http://localhost:8000`.

#### **Use Cases for WebSockets**:

* **Chat Applications**: Instant message exchange between users.
* **Real-Time Notifications**: Push notifications to clients for various updates (e.g., new messages, order status updates).
* **Collaborative Apps**: Real-time updates for collaborative editing tools (e.g., Google Docs).

---

### ✅ **2. Server-Sent Events (SSE)**

Server-Sent Events (SSE) allow servers to push updates to the browser over a single HTTP connection. Unlike WebSockets, SSE is a one-way communication from the server to the client, making it suitable for scenarios like live dashboards and real-time updates without the need for a complex bidirectional setup.

#### **Steps to Implement SSE with FastAPI**:

1. **Create SSE Endpoint**:

   SSE works by sending a stream of data from the server to the client over HTTP. FastAPI makes it easy to send this stream:

   ```python
   from fastapi import FastAPI
   from fastapi.responses import EventSourceResponse
   import time

   app = FastAPI()

   # SSE endpoint
   async def event_stream():
       while True:
           # Simulate sending data every 1 second
           yield f"data: {time.time()}\n\n"
           time.sleep(1)

   @app.get("/events")
   async def sse():
       return EventSourceResponse(event_stream())
   ```

   **Explanation**:

   * **Event Stream**: The `event_stream` function generates real-time data that will be sent to the client. It uses a loop to simulate sending time-based updates (e.g., every second).
   * **SSE Route**: The `/events` route returns the `EventSourceResponse` containing the stream of events.

2. **Client-side HTML**:

   Here's how to consume the SSE stream in the browser using JavaScript:

   ```html
   <html>
       <body>
           <h1>Server-Sent Events Test</h1>
           <p id="message"></p>
           <script>
               const eventSource = new EventSource("/events");

               eventSource.onmessage = function(event) {
                   document.getElementById("message").innerText = "Data: " + event.data;
               };

               eventSource.onerror = function() {
                   eventSource.close();
               };
           </script>
       </body>
   </html>
   ```

   **Explanation**:

   * **EventSource**: The browser creates a connection to the `/events` route, which sends updates in real-time.
   * **onmessage**: This event handler updates the content on the webpage with new data sent from the server.

3. **Run the Application**:
   Run the app using `uvicorn` and visit the SSE test page to see real-time data updates.

---

### ✅ **3. Use Cases: Chat Apps, Live Dashboards, and More**

#### **Chat Applications**:

WebSockets are ideal for creating chat applications where real-time two-way communication is needed. Each client connects via a WebSocket connection, and messages are sent and received in real-time.

* **Advantages**:

  * Low latency.
  * Real-time interaction between multiple users.
* **Implementation**: Use FastAPI’s WebSocket functionality to create multiple routes for different chat rooms or direct messaging between users.

#### **Live Dashboards**:

SSE can be used to update dashboards in real-time, such as displaying the latest metrics, logs, or events. For example, you could stream server metrics like CPU usage, memory usage, or traffic data.

* **Advantages**:

  * Simpler setup than WebSockets for one-way communication.
  * Ideal for real-time monitoring systems.

#### **Collaborative Platforms**:

For applications that require real-time updates from multiple users, like document editing, WebSockets or SSE can be used to broadcast changes to all connected clients. This ensures that every user sees updates immediately.

---

### Conclusion

FastAPI provides excellent support for both **WebSockets** and **Server-Sent Events (SSE)**, enabling you to build real-time applications like chat systems, live dashboards, and collaborative platforms. While WebSockets allow for bidirectional communication, SSE is a great choice for one-way server-to-client updates. By leveraging these technologies, you can significantly improve the user experience of your applications.


example 

To implement a REST API CRUD application using the **MVC (Model-View-Controller)** architecture with FastAPI and a database, let's go through the process step-by-step. For this example, we’ll use **SQLAlchemy** for the ORM (database model) and **SQLite** for the database. We'll also set up a typical MVC structure, where:

* **Model**: The database schema (SQLAlchemy models).
* **View**: In FastAPI, views are typically your HTTP endpoints (controllers).
* **Controller**: The logic for handling the requests and interacting with the models.

---

### 1. **Install Required Packages**

First, install FastAPI, Uvicorn, SQLAlchemy, and the SQLite driver:

```bash
pip install fastapi uvicorn sqlalchemy sqlite3
```

---

### 2. **Folder Structure**

Your project directory should look like this:

```
.
├── app
│   ├── main.py             # FastAPI app
│   ├── models.py           # Database models
│   ├── crud.py             # CRUD operations
│   ├── schemas.py          # Pydantic schemas
│   ├── database.py         # Database setup
│   └── controllers.py      # Routes and request handlers
└── requirements.txt
```

---

### 3. **Database Setup** (`database.py`)

Set up the SQLAlchemy database connection.

```python
# app/database.py
from sqlalchemy import create_engine
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

DATABASE_URL = "sqlite:///./test.db"  # SQLite database

# Create engine
engine = create_engine(DATABASE_URL, connect_args={"check_same_thread": False})

# Create session local factory
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)

# Base class for models
Base = declarative_base()
```

---

### 4. **Model Setup** (`models.py`)

Define the database model (e.g., `Item`).

```python
# app/models.py
from sqlalchemy import Column, Integer, String
from app.database import Base

class Item(Base):
    __tablename__ = "items"

    id = Column(Integer, primary_key=True, index=True)
    name = Column(String, index=True)
    description = Column(String, index=True)
    price = Column(Integer)

```

---

### 5. **Pydantic Schema** (`schemas.py`)

Define the request and response validation models (Pydantic).

```python
# app/schemas.py
from pydantic import BaseModel
from typing import Optional

class ItemBase(BaseModel):
    name: str
    description: Optional[str] = None
    price: int

class ItemCreate(ItemBase):
    pass

class Item(ItemBase):
    id: int

    class Config:
        orm_mode = True
```

---

### 6. **CRUD Operations** (`crud.py`)

Define the functions for creating, reading, updating, and deleting items.

```python
# app/crud.py
from sqlalchemy.orm import Session
from app import models, schemas

# Create item
def create_item(db: Session, item: schemas.ItemCreate):
    db_item = models.Item(name=item.name, description=item.description, price=item.price)
    db.add(db_item)
    db.commit()
    db.refresh(db_item)
    return db_item

# Get item by ID
def get_item(db: Session, item_id: int):
    return db.query(models.Item).filter(models.Item.id == item_id).first()

# Get all items
def get_items(db: Session, skip: int = 0, limit: int = 10):
    return db.query(models.Item).offset(skip).limit(limit).all()

# Update item
def update_item(db: Session, item_id: int, item: schemas.ItemCreate):
    db_item = db.query(models.Item).filter(models.Item.id == item_id).first()
    if db_item:
        db_item.name = item.name
        db_item.description = item.description
        db_item.price = item.price
        db.commit()
        db.refresh(db_item)
    return db_item

# Delete item
def delete_item(db: Session, item_id: int):
    db_item = db.query(models.Item).filter(models.Item.id == item_id).first()
    if db_item:
        db.delete(db_item)
        db.commit()
    return db_item
```

---

### 7. **Controllers/Routes** (`controllers.py`)

Create the FastAPI routes (controller layer).

```python
# app/controllers.py
from fastapi import APIRouter, Depends, HTTPException
from sqlalchemy.orm import Session
from app import crud, schemas, models, database

router = APIRouter()

# Dependency to get the database session
def get_db():
    db = database.SessionLocal()
    try:
        yield db
    finally:
        db.close()

# Create item
@router.post("/items/", response_model=schemas.Item)
def create_item(item: schemas.ItemCreate, db: Session = Depends(get_db)):
    return crud.create_item(db=db, item=item)

# Get item by ID
@router.get("/items/{item_id}", response_model=schemas.Item)
def read_item(item_id: int, db: Session = Depends(get_db)):
    db_item = crud.get_item(db=db, item_id=item_id)
    if db_item is None:
        raise HTTPException(status_code=404, detail="Item not found")
    return db_item

# Get all items
@router.get("/items/", response_model=list[schemas.Item])
def read_items(skip: int = 0, limit: int = 10, db: Session = Depends(get_db)):
    return crud.get_items(db=db, skip=skip, limit=limit)

# Update item
@router.put("/items/{item_id}", response_model=schemas.Item)
def update_item(item_id: int, item: schemas.ItemCreate, db: Session = Depends(get_db)):
    db_item = crud.update_item(db=db, item_id=item_id, item=item)
    if db_item is None:
        raise HTTPException(status_code=404, detail="Item not found")
    return db_item

# Delete item
@router.delete("/items/{item_id}", response_model=schemas.Item)
def delete_item(item_id: int, db: Session = Depends(get_db)):
    db_item = crud.delete_item(db=db, item_id=item_id)
    if db_item is None:
        raise HTTPException(status_code=404, detail="Item not found")
    return db_item
```

---

### 8. **Main FastAPI Application** (`main.py`)

Set up the FastAPI app and include the routes.

```python
# app/main.py
from fastapi import FastAPI
from app import controllers, models, database

# Create the database tables
models.Base.metadata.create_all(bind=database.engine)

# FastAPI app initialization
app = FastAPI()

# Include the controllers (routes)
app.include_router(controllers.router)
```

---

### 9. **Run the Application**

To run the FastAPI app, use the `uvicorn` server:

```bash
uvicorn app.main:app --reload
```

Now, the FastAPI application will be running at `http://localhost:8000`. You can test the CRUD operations through the following routes:

* **POST** `/items/` — Create an item.
* **GET** `/items/{item_id}` — Get an item by ID.
* **GET** `/items/` — Get all items.
* **PUT** `/items/{item_id}` — Update an item by ID.
* **DELETE** `/items/{item_id}` — Delete an item by ID.

---

### Summary of MVC Structure:

* **Model**: `models.py` defines the database schema.
* **View**: FastAPI routes in `controllers.py` handle the HTTP requests and responses.
* **Controller**: CRUD functions in `crud.py` interact with the database and encapsulate the business logic.

This setup provides a clean MVC architecture, separating concerns between models, routes, and CRUD operations.


To implement **JWT (JSON Web Token)** authentication in a FastAPI CRUD application, we will need to add functionality for:

1. **User authentication**: User login and token generation.
2. **Secure routes**: Protect CRUD operations by validating JWT tokens.

We'll break it down as follows:

1. **Install Required Packages**:
   You need `fastapi`, `uvicorn`, `sqlalchemy`, `pyjwt`, and `passlib` for JWT and password hashing.

   ```bash
   pip install fastapi uvicorn sqlalchemy pyjwt passlib
   ```

---

### 1. **JWT Authentication Setup**

Let's implement JWT authentication by adding a **User** model, **login** functionality, and a **token generation and validation** system.

---

### 2. **Update Project Structure**

```
.
├── app
│   ├── main.py             # FastAPI app
│   ├── models.py           # Database models
│   ├── crud.py             # CRUD operations
│   ├── schemas.py          # Pydantic schemas
│   ├── database.py         # Database setup
│   ├── controllers.py      # Routes and request handlers
│   ├── auth.py             # JWT Auth helper
└── requirements.txt
```

---

### 3. **JWT Authentication Helper** (`auth.py`)

This file contains utility functions to create JWT tokens and verify them.

```python
# app/auth.py
import jwt
from datetime import datetime, timedelta
from passlib.context import CryptContext
from fastapi import Depends, HTTPException
from fastapi.security import OAuth2PasswordBearer
from sqlalchemy.orm import Session
from app import models, crud, database

# Secret key to encode/decode JWT tokens
SECRET_KEY = "your_secret_key"
ALGORITHM = "HS256"
ACCESS_TOKEN_EXPIRE_MINUTES = 30

# Password hashing
pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")

# OAuth2PasswordBearer is used to extract the token from the Authorization header
oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

# Create JWT token
def create_access_token(data: dict, expires_delta: timedelta = timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)):
    to_encode = data.copy()
    expire = datetime.utcnow() + expires_delta
    to_encode.update({"exp": expire})
    encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)
    return encoded_jwt

# Verify password
def verify_password(plain_password, hashed_password):
    return pwd_context.verify(plain_password, hashed_password)

# Hash password
def get_password_hash(password):
    return pwd_context.hash(password)

# Decode and validate JWT token
def decode_jwt_token(token: str):
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        return payload
    except jwt.PyJWTError:
        raise HTTPException(status_code=401, detail="Invalid token")
```

---

### 4. **User Model** (`models.py`)

Add a `User` model and update the database schema.

```python
# app/models.py
from sqlalchemy import Column, Integer, String
from app.database import Base

class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True, index=True)
    username = Column(String, unique=True, index=True)
    password = Column(String)
```

---

### 5. **User CRUD Operations** (`crud.py`)

Define CRUD functions for user operations, like creating users and fetching users by username.

```python
# app/crud.py
from sqlalchemy.orm import Session
from app import models, schemas, auth

# Create a new user
def create_user(db: Session, user: schemas.UserCreate):
    db_user = models.User(username=user.username, password=auth.get_password_hash(user.password))
    db.add(db_user)
    db.commit()
    db.refresh(db_user)
    return db_user

# Get user by username
def get_user(db: Session, username: str):
    return db.query(models.User).filter(models.User.username == username).first()
```

---

### 6. **Schemas for User and Token** (`schemas.py`)

Add Pydantic models to validate and serialize user data and JWT token.

```python
# app/schemas.py
from pydantic import BaseModel
from typing import Optional

class UserBase(BaseModel):
    username: str

class UserCreate(UserBase):
    password: str

class User(UserBase):
    id: int

    class Config:
        orm_mode = True

class Token(BaseModel):
    access_token: str
    token_type: str

class TokenData(BaseModel):
    username: str
```

---

### 7. **Login and Token Route** (`controllers.py`)

Create an endpoint for user login, where the user provides their credentials and receives a JWT token in response.

```python
# app/controllers.py
from fastapi import APIRouter, Depends, HTTPException
from sqlalchemy.orm import Session
from app import crud, schemas, auth, database

router = APIRouter()

# Dependency to get the database session
def get_db():
    db = database.SessionLocal()
    try:
        yield db
    finally:
        db.close()

# Login and get token
@router.post("/token", response_model=schemas.Token)
def login_for_access_token(form_data: schemas.UserCreate, db: Session = Depends(get_db)):
    user = crud.get_user(db, username=form_data.username)
    if not user or not auth.verify_password(form_data.password, user.password):
        raise HTTPException(status_code=401, detail="Invalid credentials")

    # Create JWT token
    access_token = auth.create_access_token(data={"sub": user.username})
    return {"access_token": access_token, "token_type": "bearer"}
```

---

### 8. **Protect CRUD Routes with JWT** (`controllers.py`)

Protect CRUD routes (e.g., creating, updating, or deleting items) by requiring a valid JWT token.

```python
# app/controllers.py
from fastapi import APIRouter, Depends, HTTPException, status
from sqlalchemy.orm import Session
from app import crud, schemas, models, database, auth

router = APIRouter()

# Dependency to get the database session
def get_db():
    db = database.SessionLocal()
    try:
        yield db
    finally:
        db.close()

# Dependency to get the current user
def get_current_user(token: str = Depends(auth.oauth2_scheme), db: Session = Depends(get_db)):
    credentials_exception = HTTPException(
        status_code=status.HTTP_401_UNAUTHORIZED,
        detail="Could not validate credentials",
        headers={"WWW-Authenticate": "Bearer"},
    )
    try:
        payload = auth.decode_jwt_token(token)
        username: str = payload.get("sub")
        if username is None:
            raise credentials_exception
        user = crud.get_user(db, username=username)
        if user is None:
            raise credentials_exception
    except auth.JWTError:
        raise credentials_exception
    return user

# Create item
@router.post("/items/", response_model=schemas.Item)
def create_item(item: schemas.ItemCreate, db: Session = Depends(get_db), current_user: models.User = Depends(get_current_user)):
    return crud.create_item(db=db, item=item)

# Get item by ID
@router.get("/items/{item_id}", response_model=schemas.Item)
def read_item(item_id: int, db: Session = Depends(get_db), current_user: models.User = Depends(get_current_user)):
    db_item = crud.get_item(db=db, item_id=item_id)
    if db_item is None:
        raise HTTPException(status_code=404, detail="Item not found")
    return db_item

# Other CRUD routes (GET, PUT, DELETE) can be similarly protected with `current_user` dependency
```

---

### 9. **Main FastAPI Application** (`main.py`)

Include the new authentication routes.

```python
# app/main.py
from fastapi import FastAPI
from app import controllers, models, database

# Create the database tables
models.Base.metadata.create_all(bind=database.engine)

# FastAPI app initialization
app = FastAPI()

# Include the routes
app.include_router(controllers.router)
```

---

### 10. **Run the Application**

To run the FastAPI app, use the `uvicorn` server:

```bash
uvicorn app.main:app --reload
```

### **Test the Application**:

1. **Create a user** (using a POST endpoint).
2. **Login** (POST `/token`) with your username and password to get a JWT token.
3. **Access protected routes** like `/items/` (POST, GET, PUT, DELETE) by passing the JWT token in the `Authorization` header (Bearer token).

Example headers for requests:

```text
Authorization: Bearer <JWT_TOKEN>
```

---

### Summary of Key Points:

* **JWT Authentication**: User logs in with username and password, receives a JWT token which is used for subsequent requests.
* **Protected Routes**: CRUD operations are secured by requiring a valid JWT token in the `Authorization` header.
* **OAuth2PasswordBearer**: FastAPI's `OAuth2PasswordBearer` is used to extract the token from requests.


Job scheduling in **FastAPI** can be accomplished using several methods, depending on the complexity of the task and the requirements for background processing. Below are some of the most common techniques for job scheduling in FastAPI:

---

### **1. Background Tasks with FastAPI**

FastAPI has a built-in mechanism for running background tasks using the `BackgroundTasks` class. This is useful for lightweight, non-blocking tasks that can be executed after the response is sent to the client.

#### **Features:**

* Simple to implement for background tasks.
* Ideal for tasks like sending emails, logging, or processing after a request.
* Does not block the main thread (async behavior).

#### **Example:**

```python
from fastapi import FastAPI, BackgroundTasks
import time

app = FastAPI()

def write_log(message: str):
    with open("log.txt", mode="a") as log:
        log.write(f"{message}\n")
        time.sleep(5)  # Simulating a long task
        log.write("Job completed\n")

@app.get("/")
async def root(background_tasks: BackgroundTasks):
    background_tasks.add_task(write_log, "Started the background task")
    return {"message": "Job is running in the background!"}
```

#### **Explanation:**

* The background task will run asynchronously after the response is returned to the client.
* You can add the background task using `background_tasks.add_task()`.

---

### **2. APScheduler (Advanced Scheduler for Periodic Jobs)**

For more advanced scheduling with cron-like jobs, FastAPI can integrate with **APScheduler**. This library allows you to schedule jobs to run periodically, at fixed intervals, or at specific times.

#### **Features:**

* Cron-style job scheduling.
* Interval-based jobs (e.g., run every 10 minutes).
* Persistent job storage and retry logic.
* Task monitoring and job persistence in databases.

#### **Example:**

```python
from fastapi import FastAPI
from apscheduler.schedulers.background import BackgroundScheduler
import time

app = FastAPI()
scheduler = BackgroundScheduler()

def scheduled_job():
    print("Running scheduled task...")

# Add a job that runs every 10 seconds
scheduler.add_job(scheduled_job, 'interval', seconds=10)
scheduler.start()

@app.get("/")
async def root():
    return {"message": "Job is scheduled every 10 seconds!"}
```

#### **Explanation:**

* The `APScheduler` library allows you to schedule jobs at specific intervals (in this case, every 10 seconds).
* Jobs can be scheduled using cron-style, interval-based, or date-based schedules.
* This approach is better suited for periodic tasks that need to run at fixed intervals.

#### **Persistent Job Storage:**

You can also persist jobs in databases (e.g., SQLite, PostgreSQL) by configuring the scheduler to use persistent storage.

---

### **3. Celery with FastAPI for Distributed Task Queues**

**Celery** is a powerful task queue system for Python that allows you to distribute work across multiple workers. It is especially useful for background tasks that are complex, long-running, or need to be distributed over multiple servers.

#### **Features:**

* Supports complex workflows with task dependencies.
* Uses brokers like Redis or RabbitMQ for task distribution.
* Supports retries, scheduling, and monitoring.
* Ideal for distributed, asynchronous task execution.

#### **Example:**

1. **Install Dependencies:**

   ```bash
   pip install celery redis
   ```

2. **Create the Celery Application:**

   ```python
   from celery import Celery

   app = Celery('worker', broker='redis://localhost:6379/0')

   @app.task
   def process_data(data):
       print(f"Processing data: {data}")
       return f"Processed {data}"
   ```

3. **Integrate with FastAPI:**

   ```python
   from fastapi import FastAPI
   from celery.result import AsyncResult
   from worker import process_data

   app = FastAPI()

   @app.post("/process/")
   async def process_item(data: str):
       task = process_data.apply_async(args=[data])
       return {"task_id": task.id, "status": "Task is being processed."}

   @app.get("/status/{task_id}")
   async def get_task_status(task_id: str):
       task = AsyncResult(task_id)
       return {"task_id": task.id, "status": task.status}
   ```

#### **Explanation:**

* **Celery** handles tasks like sending emails, processing long-running jobs, or other complex workflows.
* Tasks are queued and distributed across workers, which can be running on different servers.
* Redis is used as the broker for task distribution.

---

### **4. Periodic Task Execution with FastAPI and Redis (Using Celery Beat)**

**Celery Beat** can be used to schedule periodic tasks in Celery. This is often used for cron-like tasks where jobs need to run at specific times.

#### **Example:**

1. **Install Dependencies:**

   ```bash
   pip install celery redis celery[redis] apscheduler
   ```

2. **Create the Celery Application:**

   ```python
   from celery import Celery
   from celery.schedules import crontab

   app = Celery('worker', broker='redis://localhost:6379/0')

   @app.task
   def periodic_task():
       print("This task runs periodically!")

   app.conf.beat_schedule = {
       'run-every-minute': {
           'task': 'periodic_task',
           'schedule': crontab(minute='*'),
       },
   }
   ```

3. **Start Celery Beat alongside Celery Worker:**

   ```bash
   celery -A worker.app worker --loglevel=info
   celery -A worker.app beat --loglevel=info
   ```

#### **Explanation:**

* This configuration allows you to run the `periodic_task` function every minute.
* You can schedule multiple tasks with cron expressions in the `beat_schedule`.

---

### **5. Using Redis for Task Queues and Scheduling (via `rq` Library)**

If you want a simpler alternative to Celery, you can use the **rq** library, which is built on top of Redis. It’s a simpler solution for queuing tasks without all the complexity of Celery.

#### **Features:**

* Lightweight and easy to set up.
* Uses Redis for task queue management.
* Supports task retries, job status monitoring, and delayed jobs.

#### **Example:**

1. **Install Dependencies:**

   ```bash
   pip install rq redis
   ```

2. **Create Task and Scheduler:**

   ```python
   from rq import Queue
   from redis import Redis
   from fastapi import FastAPI
   import time

   redis_conn = Redis()
   q = Queue(connection=redis_conn)

   def my_background_task(n):
       time.sleep(n)
       return f"Task completed after {n} seconds"

   app = FastAPI()

   @app.post("/enqueue/")
   def enqueue_task(n: int):
       job = q.enqueue(my_background_task, n)
       return {"job_id": job.id}

   @app.get("/status/{job_id}")
   def job_status(job_id: str):
       job = q.fetch_job(job_id)
       return {"status": job.get_status() if job else "Job not found"}
   ```

#### **Explanation:**

* **RQ** is a simple way to enqueue background tasks and manage task queues.
* Jobs are enqueued in Redis, and workers process the tasks asynchronously.

---

### **Conclusion**

FastAPI provides several ways to handle job scheduling, depending on your project’s requirements:

* **Simple tasks**: Use **FastAPI's BackgroundTasks** for lightweight background processing.
* **Periodic tasks**: Use **APScheduler** or **Celery Beat** for advanced periodic job scheduling.
* **Distributed task queues**: Use **Celery** (with Redis or RabbitMQ) for more complex and scalable distributed task handling.
* **Simple job queues**: Use **RQ** if you need a lightweight task queue with Redis.

Choose the right tool based on the scale and complexity of the background tasks you need to manage.









