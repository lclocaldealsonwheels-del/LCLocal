# LC Local App Architecture

## Purpose

This document defines the technical structure of the LC Local platform and how the Customer App, Driver App, Partner Portal, and Admin Control Center will work together.

## Platform Overview

LC Local will be built as one connected ecosystem with separate interfaces for different types of users.

### Customer App

The customer-facing mobile application will allow customers to:

- Create and manage accounts
- Browse local businesses
- Browse products and services
- Search and filter
- Add products to a cart
- Place orders
- Make payments
- Select delivery options
- Track orders
- View order history
- Save favorites
- Receive notifications
- Access Community Care features

### Driver App

The driver application will allow approved drivers to:

- Create and manage driver accounts
- Complete driver verification
- View available deliveries
- Accept delivery assignments
- View pickup information
- Navigate to pickup locations
- Confirm pickups
- Navigate to customers
- Confirm deliveries
- View completed deliveries
- Track earnings

### Partner Portal

The partner business portal will allow approved businesses to:

- Create and manage business profiles
- Manage business hours
- Add and edit products
- Manage pricing
- Manage inventory
- Receive orders
- Update order status
- View sales information
- Communicate important information

### Admin Control Center

The administrative system will provide authorized administrators with control over the platform.

Administrators will be able to:

- Manage customers
- Manage drivers
- Manage partner businesses
- Manage products
- Manage categories
- Manage orders
- Monitor deliveries
- Manage payments
- Manage promotions
- Manage Community Care
- View reports
- Configure platform settings

## Core Data Model

The initial system will be organized around the following major data objects:

### Users

A user account may represent:

- Customer
- Driver
- Partner
- Administrator

Each account will have permissions appropriate to its role.

### Businesses

A business record may contain:

- Business name
- Description
- Address
- Contact information
- Business hours
- Categories
- Products
- Delivery settings
- Partner status

### Products

A product record may contain:

- Product name
- Description
- Images
- Price
- Category
- Inventory quantity
- Business ID
- Availability status

### Orders

An order will connect:

- Customer
- Business or businesses
- Products
- Payment
- Delivery
- Order status

Possible order statuses:

1. Pending
2. Confirmed
3. Preparing
4. Ready for Pickup
5. Driver Assigned
6. Picked Up
7. Out for Delivery
8. Delivered
9. Cancelled

### Deliveries

A delivery record will connect:

- Order
- Driver
- Pickup location
- Delivery location
- Delivery status
- Route information
- Delivery timestamps
- Driver earnings

### Payments

Payment records will connect to orders and will eventually integrate with Stripe.

Sensitive payment information will not be stored directly in the LC Local database.

## User Permissions

The system will use role-based permissions.

### Customer

Customers can access their own:

- Profile
- Orders
- Payments
- Favorites
- Delivery information

### Driver

Drivers can access:

- Their driver profile
- Assigned deliveries
- Available delivery opportunities
- Delivery history
- Earnings

### Partner

Partners can access:

- Their business
- Their products
- Their inventory
- Their orders
- Their sales information

### Administrator

Administrators can access platform-wide management tools according to their assigned permissions.

## Backend

Firebase will initially provide the core backend services.

Planned Firebase services include:

- Authentication
- Cloud Firestore
- Cloud Functions
- Cloud Storage
- Push notifications

The exact Firebase configuration will be established during the computer-based development setup.

## Maps and Delivery

Google Maps services will eventually provide:

- Business locations
- Customer locations
- Driver navigation
- Route information
- Delivery distance calculations

Location data will be handled carefully and only collected when required for the application's functionality.

## Payments

Stripe will be used for secure payment processing.

The application architecture will be designed so payment processing is separated from sensitive payment credentials.

## Notifications

LC Local will eventually support notifications for events such as:

- Order confirmation
- Order preparation
- Driver assignment
- Pickup
- Delivery
- Order completion
- Important partner announcements

## Community Care

Community Care will be integrated into the platform as a dedicated program.

It may support:

- Sponsored deliveries
- Donated delivery credits
- Community organizations
- Assistance requests
- Partner-sponsored assistance

Community Care activity will be controlled through appropriate administrative permissions.

## Application Structure

The eventual Flutter project will be organized to keep shared functionality separate from individual user interfaces.

Planned areas include:

- Authentication
- Customer features
- Driver features
- Partner features
- Admin features
- Shared models
- Shared services
- Firebase services
- Maps services
- Payment services
- Notification services
- Shared UI components

## Security Principles

LC Local will follow these principles:

- Never store passwords in application code
- Never commit API keys or private credentials to GitHub
- Use Firebase Authentication for account authentication
- Use role-based authorization
- Protect database access with security rules
- Keep sensitive configuration outside publicly accessible source code
- Validate important operations on the backend
- Minimize collection of unnecessary personal information

## Development Approach

LC Local will be developed incrementally.

The initial goal is to establish a working customer application and backend foundation.

Additional capabilities will then be added without requiring the entire platform to be rebuilt.

## Current Development Stage

LC Local is in early development.

The GitHub repository currently contains project documentation.

The Flutter application will be generated and connected to the repository when the development computer is available.

---

**LC Local**

*From the heart of Lewis County to your doorstep.*
