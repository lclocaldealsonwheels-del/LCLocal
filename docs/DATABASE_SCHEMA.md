# LC Local Database Schema

## Purpose

This document defines the initial data structure for the LC Local platform.

The database will use Firebase Cloud Firestore during the initial development phase.

The schema is designed to support customers, businesses, products, orders, deliveries, drivers, payments, notifications, and Community Care.

---

## Users

Collection:

`users`

Each user account will have one primary platform role.

### Fields

- `userId`
- `firstName`
- `lastName`
- `email`
- `phone`
- `role`
- `profileImage`
- `createdAt`
- `updatedAt`
- `active`
- `notificationPreferences`

### Roles

- `customer`
- `driver`
- `partner`
- `admin`

---

## Businesses

Collection:

`businesses`

Each approved local business will have a business profile.

### Fields

- `businessId`
- `ownerUserId`
- `businessName`
- `description`
- `logoImage`
- `coverImage`
- `phone`
- `email`
- `website`
- `address`
- `latitude`
- `longitude`
- `businessHours`
- `categories`
- `deliveryAvailable`
- `active`
- `partnerStatus`
- `createdAt`
- `updatedAt`

### Partner Status

- `pending`
- `approved`
- `suspended`
- `inactive`

---

## Categories

Collection:

`categories`

Categories organize businesses and products.

### Fields

- `categoryId`
- `name`
- `description`
- `image`
- `icon`
- `active`
- `sortOrder`

Initial categories may include:

- Grocery
- Farm Products
- Produce
- Pet Supplies
- Farm Supplies
- Hardware
- Local Goods
- Restaurants
- Floral
- Seasonal
- Local Services

Categories can expand as LC Local grows.

---

## Products

Collection:

`products`

Products belong to a business.

### Fields

- `productId`
- `businessId`
- `name`
- `description`
- `images`
- `price`
- `categoryId`
- `inventoryQuantity`
- `available`
- `featured`
- `createdAt`
- `updatedAt`

---

## Orders

Collection:

`orders`

An order represents a customer's purchase.

### Fields

- `orderId`
- `customerId`
- `businessIds`
- `items`
- `subtotal`
- `deliveryFee`
- `tax`
- `discount`
- `total`
- `paymentId`
- `deliveryId`
- `status`
- `deliveryAddress`
- `customerNotes`
- `createdAt`
- `updatedAt`

### Order Status

- `pending`
- `confirmed`
- `preparing`
- `readyForPickup`
- `driverAssigned`
- `pickedUp`
- `outForDelivery`
- `delivered`
- `cancelled`

---

## Order Items

Order items will be stored inside an order.

Each item may contain:

- `productId`
- `businessId`
- `productName`
- `quantity`
- `unitPrice`
- `totalPrice`
- `specialInstructions`

Storing the product name and price at the time of purchase preserves the historical order record even if the product later changes.

---

## Drivers

Collection:

`drivers`

Driver records contain information needed to operate the delivery system.

### Fields

- `driverId`
- `userId`
- `vehicleType`
- `vehicleDescription`
- `licenseStatus`
- `insuranceStatus`
- `verificationStatus`
- `active`
- `currentLocation`
- `createdAt`
- `updatedAt`

### Verification Status

- `pending`
- `approved`
- `rejected`
- `suspended`

---

## Deliveries

Collection:

`deliveries`

A delivery connects an order with a driver.

### Fields

- `deliveryId`
- `orderId`
- `driverId`
- `pickupLocations`
- `deliveryAddress`
- `customerId`
- `status`
- `distance`
- `estimatedTime`
- `driverEarnings`
- `assignedAt`
- `pickedUpAt`
- `deliveredAt`
- `createdAt`
- `updatedAt`

### Delivery Status

- `available`
- `assigned`
- `arrivedAtPickup`
- `pickedUp`
- `outForDelivery`
- `delivered`
- `cancelled`

---

## Payments

Collection:

`payments`

Payment records will reference Stripe transactions.

### Fields

- `paymentId`
- `orderId`
- `customerId`
- `amount`
- `currency`
- `status`
- `stripePaymentIntentId`
- `createdAt`
- `updatedAt`

### Payment Status

- `pending`
- `authorized`
- `paid`
- `failed`
- `refunded`
- `partiallyRefunded`

Sensitive card information will not be stored in Firestore.

---

## Favorites

Collection:

`favorites`

Customers can save favorite businesses and products.

### Fields

- `favoriteId`
- `customerId`
- `businessId`
- `productId`
- `createdAt`

---

## Notifications

Collection:

`notifications`

Notifications will allow LC Local to communicate important events to users.

### Fields

- `notificationId`
- `userId`
- `title`
- `message`
- `type`
- `relatedOrderId`
- `read`
- `createdAt`

---

## Community Care

Collection:

`communityCare`

Community Care will support sponsored and donated delivery assistance.

### Fields

- `requestId`
- `customerId`
- `sponsorId`
- `reason`
- `deliveryCredit`
- `status`
- `createdAt`
- `updatedAt`

### Status

- `pending`
- `approved`
- `fulfilled`
- `declined`
- `cancelled`

Community Care access and approval will be controlled through administrative permissions.

---

## Promotions

Collection:

`promotions`

Promotions can be created for businesses or for the LC Local marketplace.

### Fields

- `promotionId`
- `businessId`
- `code`
- `description`
- `discountType`
- `discountValue`
- `minimumOrder`
- `startDate`
- `endDate`
- `active`

---

## Reviews

Collection:

`reviews`

Customers may eventually review businesses and products.

### Fields

- `reviewId`
- `customerId`
- `businessId`
- `productId`
- `orderId`
- `rating`
- `comment`
- `createdAt`
- `updatedAt`

Reviews will only be permitted when appropriate order and purchase conditions have been satisfied.

---

## Audit Logs

Collection:

`auditLogs`

Important administrative actions will be recorded for security and accountability.

### Fields

- `logId`
- `userId`
- `action`
- `targetType`
- `targetId`
- `details`
- `createdAt`

---

## Relationships

The primary relationships are:

```text
User
 ├── Customer → Orders → Deliveries
 ├── Driver → Deliveries
 ├── Partner → Business → Products
 └── Admin → Platform Management

Business
 └── Products

Customer
 ├── Orders
 ├── Favorites
 ├── Reviews
 └── Community Care

Order
 ├── Customer
 ├── Products
 ├── Payment
 └── Delivery

Delivery
 ├── Order
 └── Driver
