<p align="center">
  <img src="https://github.com/gokulv197-crypto/readme-images/blob/main/expense-tracker/b1d1906722b334d8674254682068c0b9_fgraphic1.png">
</p>

The Expense Tracker is a backend application designed to help users securely manage, track, and analyze their personal financial expenses. It provides a complete system for account management, expense recording, analytics, and account recovery, built with a focus on structured data handling and API-driven interactions.
<br>
<br>
Users can create an account using their email, password, and mobile number. The system ensures strong password policies and validates email and phone number formats before registration. Once registered, users can log in to receive an access token for authenticated interactions and a refresh token for maintaining sessions securely.
<br>
<br>
After authentication, users can create, view, update, and delete their expenses. Each expense includes a title and a monetary amount, allowing users to organize and track their spending efficiently. The system also caches expense data to improve performance and reduce repeated database queries.
<br>
<br>
The application provides analytical insights into user spending. Users can specify a date range to retrieve aggregated data such as total spending, average expense, minimum and maximum expenses, and the total number of transactions. Additionally, item-level analytics allow users to analyze spending patterns for individual expense titles.
<br>
<br>
For account management, users can update their email, password, and mobile number. Security measures such as password verification and rate limiting are applied to sensitive operations to prevent abuse and unauthorized access.
<br>
<br>
The system also includes an account recovery mechanism. If a user forgets their password, they can request a one-time password (OTP) sent to their registered mobile number. After verifying the OTP, the user can reset their password securely. OTPs are time-bound and stored temporarily to ensure safety.
<br>
<br>
Administrative health-check endpoints are provided to monitor the status of the database, cache systems, rate limiter, OTP storage, and messaging service. These endpoints help ensure that all system components are functioning correctly.
<br>
<br>
Overall, the Expense Tracker is a RESTful API-based backend system that combines authentication, data management, caching, rate limiting, and external messaging integration to deliver a structured and scalable expense management solution.

<p align="center">
  <img src="">
</p>

__Expense Tracker__ is a high-performance, asynchronous RESTful API backend designed to securely manage, track, and analyze personal financial data. Built as a scalable expense analytics platform, the system implements a modern microservices-adjacent architecture featuring decoupled storage layers, write-through caching pipelines, defensive security guardrails, and event-driven out-of-band communication systems.

## Built With

- __FastAPI & Asyncio__ – Asynchronous API gateway ecosystem maximizing concurrent throughput
- __Python__ – Core development language utilizing strict type hinting and robust security standard libraries
- __SQLAlchemy__ – Object-Relational Mapping (ORM) framework handling atomic persistent transactions
- __MySQL__ – Relational database infrastructure optimized for structured financial persistence
- __JWT (JSON Web Token)__ – Stateless security mechanism driving dual-token authentication lifecycles
- __Argon2id__ – Memory-hard password hashing standard protecting client credential stores
- __Docker__ – Containerization platform ensuring isolated service environments and deployment parity
- __Twilio API__ – Programmatic communications engine managing out-of-band SMS routing

## System Architecture

- __Asynchronous Enterprise Stack__: Engineered entirely with FastAPI utilizing Python's `asyncio` ecosystem to maximize concurrent throughput. It features persistent storage mapped through SQLAlchemy ORM to a MySQL relational database, optimized with explicit composite indexing and foreign key cascade deletion integrity.
- __Decoupled Multi-Instance Memory Tier__: Implements three isolated Redis data pools to prevent cross-contamination of infrastructure memory: 
    - __High-Speed Cache Engine__: Reduces relational database load by executing an eviction/write-through cache pattern for persistent user transactions.
    - __Atomic Sliding Window Rate Limiter__: Protects sensitive auth and account gateways against brute-force/DDoS requests using Redis Sorted Sets (`ZSET`) grouped within atomic pipeline round-trips.
    - __Time-Bound Ephemeral Key Store__: Manages stateful lifecycle tracking for out-of-band security authentications.
- __Robust Identity Shield & Session Lifecycles__: Features a robust dual-token security topology (JWT-based Access & Refresh Token rotation) transported safely "via" encrypted headers and `HttpOnly`, `SameSite=Strict` browser cookies to systematically insulate the application against XSS and CSRF ambient request attacks.
- __Defensive Cryptography & Security Controls__: Enforces maximum security at the API gateway through memory-hard Argon2id password hashing resistant to GPU parallel cracking, utilizing cryptographic constant-time string matching (`secrets.compare_digest`) to neutralize side-channel timing attacks.
- __Server-Side Data Aggregation & Analytical Engines__: Minimizes API network overhead by offloading heavy arithmetic calculation onto the database engine. Leverages SQL data type casting and server-side mathematical aggregations (`SUM`, `AVG`, `MIN`, `MAX`, `COUNT`) to compile granular, date-bounded itemized financial metrics instantly.
- __Non-Blocking Out-of-Band (OOB) Communications__: Handles secure workflow verification and account recovery routines through Twilio SMS Gateway integration. To preserve zero-latency request processing times, communications are seamlessly offloaded to background execution worker pools using FastAPI `BackgroundTasks`.
- __Active Microservices Diagnostics & Telemetry__: Outfitted with specialized administrative health telemetry endpoints monitoring live service-level connectivity status across all standalone relational, cache, rate-limiting, and external notification networks independently.

# Local Setup
## Prerequisites
- Python 3.9+
- MySQL database
- Dockerized Redis
- Twilio Messaging Account

## Clone the Repository
git clone 
<br>
cd expense-tracker

## Create a Virtual Environment
python -m venv <venv_name>
- __Linux / Mac__: <venv_name>/bin/activate
- __Windows__: <venv_name>\Scripts\activate

## Install Dependencies
pip install -r requirements.txt

## Environment Configuration
Create a `.env` file in the root directory:
- __DATABASE_URL__=mysql+pymysql://[user]:[password]@localhost:3306/<db_name>
- __SECRET_KEY__=<secret_key>
- __REDIS_CACHE_URL__=redis://localhost:6379/<db_number_0-15>
- __REDIS_RATE_LIMITER_URL__=redis://localhost:6379/<db_number_0-15>
- __REDIS_OTP_STORAGE_URL__=redis://localhost:6379/<db_number_0-15>
- __TWILIO_ACCOUNT_SID__=<twilio_account_sid>
- __TWILIO_AUTH_TOKEN__=<twilio_auth_token>
- __TWILIO_PHONE__=<twilio_phone>
- __ADMIN__=[username]
- __PASSWORD__=<admin_password>
- __PHONE_NUMBER__=+[COUNTRY CODE][MOBILE NUMBER]

__Note 1__: Remove `SSL/CA` certificate arguments from the `create_engine` call in `database.py` file.
<br>
__Note 2__: Set `secure=False` within the `response.delete_cookie` call in `crud.py` file and `response.set_cookie` call in `main.py` file to allow the browser to process cookies over a HTTP connection.

## Run the application
uvicorn app.main:app --reload
<br>
<br>
API will be available at: `http://localhost:8000`
<br>
Access the interactive Swagger documentation at: `http://localhost:8000/docs`
