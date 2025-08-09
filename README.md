# Rabbi E-commerce Application Documentation

## Table of Contents

1. [Introduction](#introduction)
2. [Setup and Installation](#setup-and-installation)
3. [API Documentation](#api-documentation)
4. [Database Schema Reference](#database-schema-reference)
5. [Frontend Components and State Management](#frontend-components-and-state-management)
6. [Deployment](#deployment)
7. [Future Enhancements](#future-enhancements)
8. [Troubleshooting](#troubleshooting)

## 1. Introduction

This e-commerce application is built using Node.js, Express, and MongoDB, with a React frontend using Redux Toolkit for state management. The application allows users to browse and purchase products, with features for user management, product catalog, shopping cart, checkout, and order processing.

## 2. Setup and Installation

### Prerequisites

- Node.js
- npm/yarn
- MongoDB

### Backend Setup

1. Clone the repository.
2. Install dependencies using `npm install`.
3. Configure environment variables in the `.env` file.
4. Run the seeder using `npm run seed`.
5. Start the server using `npm run dev` or `npm start`.

### Frontend Setup (if applicable)

1. Navigate to the frontend directory.
2. Install dependencies.
3. Configure environment variables (e.g., `VITE_BACKEND_URL`).
4. Start the frontend application.

## 3. API Documentation

### Base URL

`http://localhost:3000/api` (or deployed URL)

### Authentication

- `POST /users/register`: Register a new user.
- `POST /users/login`: Authenticate user and get JWT.
- `GET /users/profile`: Get logged-in user profile (Protected).

### Product Endpoints

- `POST /products`: Create product (Admin).
- `PUT /products/:id`: Update product (Admin).
- `DELETE /products/:id`: Delete product (Admin).
- `GET /products`: Get all products with filters (Public).
- `GET /products/best-seller`: Get best-seller (Public).
- `GET /products/new-arrivals`: Get new arrivals (Public).
- `GET /products/:id`: Get single product (Public).
- `GET /products/similar/:id`: Get similar products (Public).

### Cart Endpoints

- `POST /cart`: Add to cart (Public).
- `PUT /cart`: Update cart item quantity (Public).
- `DELETE /cart`: Remove from cart (Public).
- `GET /cart`: Get user/guest cart (Public).
- `POST /cart/merge`: Merge guest cart (Protected).

### Checkout Endpoints

- `POST /checkout`: Create checkout session (Protected).
- `PUT /checkout/:id/pay`: Mark checkout as paid (Protected).
- `POST /checkout/:id/finalize`: Finalize checkout to order (Protected).

### Order Endpoints

- `GET /orders/my-orders`: Get user's orders (Protected).
- `GET /orders/:id`: Get order details (Protected).

### Admin Endpoints

- `GET /admin/users`: Get all users (Admin).
- `POST /admin/users`: Add new user (Admin).
- `PUT /admin/users/:id`: Update user (Admin).
- `DELETE /admin/users/:id`: Delete user (Admin).
- `GET /admin/products`: Get all products (Admin).
- `GET /admin/orders`: Get all orders (Admin).
- `PUT /admin/orders/:id`: Update order status (Admin).
- `DELETE /admin/orders/:id`: Delete order (Admin).

### Other Endpoints

- `POST /upload`: Upload image to Cloudinary (Protected).
- `POST /subscribe`: Newsletter subscription (Public).

## 4. Database Schema Reference

### User Schema

- `_id`: ObjectId
- `name`: String
- `email`: String
- `password`: String
- `role`: String (enum: ["customer", "admin"])

### Product Schema

- `_id`: ObjectId
- `name`: String
- `description`: String
- `price`: Number
- `discountPrice`: Number
- `countInStock`: Number
- `sku`: String
- `category`: String
- `brand`: String
- `sizes`: [String]
- `colors`: [String]
- `collections`: String
- `material`: String
- `gender`: String
- `images`: [Object]
- `isFeatured`: Boolean
- `isPublished`: Boolean
- `rating`: Number
- `numReviews`: Number
- `tags`: [String]
- `dimensions`: Object
- `weight`: Number

### Cart Schema

- `_id`: ObjectId
- `user`: ObjectId (ref: User)
- `guestId`: String
- `products`: [Object]
- `totalPrice`: Number

### Checkout Schema

- `_id`: ObjectId
- `user`: ObjectId (ref: User)
- `checkoutItems`: [Object]
- `shippingAddress`: Object
- `paymentMethod`: String
- `totalPrice`: Number
- `paymentStatus`: String
- `isPaid`: Boolean
- `paidAt`: Date
- `paymentDetails`: Mixed

### Order Schema

- `_id`: ObjectId
- `user`: ObjectId (ref: User)
- `orderItems`: [Object]
- `shippingAddress`: Object
- `paymentMethod`: String
- `totalPrice`: Number
- `isPaid`: Boolean
- `paidAt`: Date
- `isDelivered`: Boolean
- `deliveredAt`: Date
- `paymentStatus`: String
- `status`: String (enum: ["Processing", "Shipped", "Delivered", "Cancelled"])

### Subscriber Schema

- `email`: String
- `subscribedAt`: Date

## 5. Frontend Components and State Management

### Redux Store Structure

The Redux store is composed of multiple reducers, including:

- `authSlice`: User authentication state.
- `productsSlice`: Product catalog state, filters.
- `cartSlice`: Shopping cart state.
- `checkoutSlice`: Checkout process state.
- `orderSlice`: User order history.
- `adminSlice`: Admin user management.
- `adminProductSlice`: Admin product management.
- `adminOrderSlice`: Admin order management.

### Core UI Components

- `AdminLayout`, `AdminSidebar`
- `User Management`, `ProductManagement`, `OrderManagement`
- `CartContents`, `Checkout`, `PayPalButton`
- `Header`, `Footer`

## 6. Deployment

The application can be deployed using Vercel, a serverless platform. The `vercel.json` file is used to configure the deployment.

## 7. Future Enhancements

- Implement search filters for products.
- Add product reviews and ratings.
- Integrate with a payment gateway for secure transactions.
- Implement order tracking and email notifications.
- Improve error handling and logging.

## 8. Troubleshooting

- Common issues and their solutions.
- Debugging techniques for the application.
