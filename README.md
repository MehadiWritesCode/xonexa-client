# 🛍️ Xonexa - Modern Hybrid E-commerce Platform

[![Live Demo](https://img.shields.io/badge/demo-online-green.svg)](https://xonexa-client.vercel.app/)
[![Database](https://img.shields.io/badge/Database-PostgreSQL%20&%20MongoDB-blue.svg)](https://supabase.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**Xonexa** is a high-performance, full-stack e-commerce solution built with a **Hybrid Database Architecture**. It uses MongoDB for flexible product catalogs and PostgreSQL (via Supabase) for secure transactional data like users, orders, and carts.

---

## 📍 Quick Navigation
| [Live Demo](#-live-demo-links) | [Features](#-key-features) | [Tech Stack](#-tech-stack) | [DB Setup (SQL)](#-database-schema-setup) | [Project Report](#-project-report--documentation) | [Installation](#-installation--setup-guide) |
| :--- | :--- | :--- | :--- | :--- | :--- |

---

## 🌐 Live Demo Links
Access the application instantly:
- **Application Live:** [https://xonexa-client.vercel.app/](https://xonexa-client.vercel.app/)

---

## 🚀 Key Features

### 👤 User Experience
- **Authentication:** Secure JWT-based Login and Google One-Tap Sign-In.
- **Shopping:** Advanced search, category filtering, and real-time sorting.
- **Cart & Wishlist:** Persistent storage for user's favorite and selected items.
- **Dashboard:** Order tracking, detailed bill history, and profile management.
- **UI/UX:** Seamless animations powered by **Framer Motion**.

### 🛠️ Admin Features
- **Analytics:** Real-time dashboard for Total Sales, Orders, and Products.
- **Inventory:** Full CRUD for products with Cloudinary image hosting.
- **Management:** Monitor registered users and manage order delivery statuses.

---

## 🛠️ Tech Stack
- **Frontend:** React (Vite), Tailwind CSS, Framer Motion.
- **Backend:** Node.js, Express.js.
- **Databases:** PostgreSQL (Supabase) & MongoDB.
- **Other Tools:** JWT, Bcrypt, Cloudinary, Multer, Joi.

---

## 🗄️ Database Schema Setup (PostgreSQL)

To set up the relational database, run the following SQL script in your **Supabase SQL Editor**:

```sql
-- Create Users Table
CREATE TABLE users (
    user_id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    email VARCHAR UNIQUE NOT NULL,
    password_hash VARCHAR,
    authprovider VARCHAR,
    full_name VARCHAR NOT NULL,
    role VARCHAR DEFAULT 'user'
);

-- Create Orders Table
CREATE TABLE orders (
    order_id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    user_id BIGINT REFERENCES users(user_id),
    total FLOAT8 NOT NULL,
    email VARCHAR,
    address TEXT,
    city VARCHAR,
    zip VARCHAR,
    card_number VARCHAR,
    cvv VARCHAR,
    exp_date VARCHAR,
    status VARCHAR DEFAULT 'pending'
);

-- Create Order Items Table
CREATE TABLE order_items (
    id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    user_id BIGINT REFERENCES users(user_id),
    quantity BIGINT DEFAULT 1,
    size VARCHAR,
    price FLOAT8,
    product_id VARCHAR NOT NULL
);

-- Create Shopping Cart Table
CREATE TABLE shopping_cart (
    cart_id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    added_at TIMESTAMPTZ DEFAULT NOW(),
    user_id BIGINT REFERENCES users(user_id),
    product_id VARCHAR NOT NULL,
    name VARCHAR,
    price FLOAT8,
    quantity BIGINT DEFAULT 1,
    image VARCHAR
);

-- Create Wishlist Table
CREATE TABLE wishlist (
    wishlist_id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    created_at TIMESTAMPTZ DEFAULT NOW(),
    user_id BIGINT REFERENCES users(user_id),
    product_id VARCHAR NOT NULL,
    product_name VARCHAR,
    image VARCHAR,
    price FLOAT8
);

📑 Project Report & Documentation
📂 Download Full Project Report (PDF) (Link your PDF file here)

📑 System Architecture Diagram (Link your ER Diagram here)

💻 Installation & Setup Guide
1. Clone the Repositories
Bash

# Clone Frontend
git clone [https://github.com/your-username/xonexa-client.git](https://github.com/your-username/xonexa-client.git) client

# Clone Backend
git clone [https://github.com/your-username/xonexa-server.git](https://github.com/your-username/xonexa-server.git) server
2. Backend Setup
Bash
cd server
npm install
Create a .env file in the /server folder:


PORT=5000
MONGO_URI=your_mongodb_connection_string
SUPABASE_URL=your_supabase_project_url
SUPABASE_KEY=your_supabase_anon_key
JWT_SECRET=your_secret_key
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
Start Server: npm start

3. Frontend Setup
Bash
cd ../client
npm install
Create a .env file in the /client folder:


VITE_API_URL=http://localhost:5000
VITE_GOOGLE_CLIENT_ID=your_google_id
Start App: npm run dev

Made with ❤️ by Md. Mehadi Hasan
