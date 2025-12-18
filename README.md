# biblioApp

**biblioApp** is a full‑stack library management application built with multiple modern technologies, organized as a monorepo. The project demonstrates the integration of a Django backend with an Oracle database, a Node.js/Express REST API for authentication and business logic, and a Quasar/Vue.js frontend.

The application allows users to authenticate using Google Firebase, browse and filter books and authors, borrow books, and manage personal account information.

---

## Architecture Overview

The project is composed of three independent but connected services:

```
biblioApp/
├── biblioApp-django-app    # Django + Oracle DB (Admin & core data)
├── biblioApp-express-api   # Express.js REST API (Auth & integration)
└── biblioApp-quasar-front  # Quasar / Vue.js Frontend
```

Each service can be developed and executed independently, but together they form the complete **biblioApp** ecosystem.

---

## Main Features

* Google Login & Registration using **Firebase Authentication**
* JWT‑based authentication and authorization
* Browse books and authors
* Filter books by author
* Borrow books
* Update user information (email, phone, address, etc.)
* Admin interface for managing library data
* Oracle Autonomous Database integration

---

## 1. biblioApp-django-app

Django application responsible for core data management, admin interface, and Oracle Database integration.

### Technologies

* Django 5
* Django REST Framework
* Oracle Autonomous Database (Always Free tier supported)
* Gunicorn & WhiteNoise (production‑ready setup)

### Requirements

Create a **conda environment** and install the following dependencies:

```
Django==5.0.3
asgiref==3.8.1
djangorestframework==3.16.0
django-filter==25.1
django-widget-tweaks==1.5.0
oracledb==3.1.1
python-decouple==3.8
Markdown==3.8
cryptography==45.0.3
cffi==1.17.1
pycparser==2.22
pillow==10.3.0
gunicorn==21.2.0
whitenoise==6.6.0
requests>=2.31.0
```

### Environment Configuration

Create a `.env` file in the root of `biblioApp-django-app`:

```
SECRET_KEY=your_django_secret_key
DEBUG=True
DB_NAME=your_oracle_tns_high
DB_USER=admin
DB_PASSWORD=your_db_password
```

### Running the Application

Apply migrations:

```
python manage.py migrate
```

Start the development server:

```
python manage.py runserver
```

---

## 2. biblioApp-express-api

REST API built with Express.js. This service handles authentication, JWT validation, Firebase integration, and communication with the Oracle database.

### Technologies

* Node.js
* Express.js
* Firebase Authentication
* JWT
* Oracle Database

### Environment Configuration

1. Create a **Google Firebase Web App**.
2. Retrieve your `firebaseConfig` from:
   **Firebase Console → Project Settings → General**.
3. Create a `secrets.js` file in the root of `biblioApp-express-api`:

```js
import { createSecretKey } from "crypto";

const secret = "anyString";

export const jwtSecret = createSecretKey(secret, "utf-8");

export const oracleSecrets = {
  user: 'admin',
  password: 'your_db_password',
  connectString: 'your_oracle_tns_high'
};

export const firebaseSecrets = {
  apiKey: "your_api_key",
  authDomain: "your_auth_domain",
  projectId: "your_project_id",
  storageBucket: "your_storage_bucket",
  messagingSenderId: "your_sender_id",
  appId: "your_app_id"
};
```

### Running the API

Install dependencies:

```
npm install
```

Start the server:

```
npm run start
```

---

## 3. biblioApp-quasar-front

Frontend application built with **Quasar Framework** and **Vue.js**, responsible for the user interface and user experience.

### Technologies

* Vue.js
* Quasar Framework
* Axios

### Configuration

Before running the application:

* Update Axios base URLs to point to your running Express API.

### Running the Frontend

Install dependencies:

```
npm install
```

Start the development server:

```
quasar dev
```

---

## Development Notes

* All services must be running for full functionality.
* Firebase authentication is required for login and registration.
* Oracle Autonomous Database (Always Free) is recommended for development.
* Environment files (`.env`, `secrets.js`) should **never** be committed to version control.

---

## License

This project is intended for educational and academic purposes. License information can be added as needed.

---

## Author

Developed as a full‑stack academic project to explore modern web architectures, authentication flows, and database integration.
