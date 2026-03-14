# WEXON

### Warehouse EXcellence & Optimization Network

WEXON is a modern, modular **Inventory Management System (IMS)** designed to digitize and streamline warehouse and stock operations within an organization.

Many businesses still rely on manual registers, spreadsheets, or fragmented tracking systems to manage inventory. WEXON replaces these approaches with a **centralized, real-time, and scalable platform** that provides complete visibility and control over inventory across warehouses and storage locations.

The platform focuses on operational clarity, stock accuracy, and traceability of every inventory movement.


Important Note:  
In the video, the frontend is executed directly in development mode instead of running the built production version. Because of this, during the demo there may be a short delay while the application compiles. This happens due to the heavy load caused by running both Spring Boot and Next.js servers simultaneously.



---

# Vision

Inventory management is a critical operational function for any organization dealing with physical goods. However, many existing processes lack transparency, consistency, and real-time insight.

WEXON aims to establish a unified platform where organizations can:

* Track inventory in real time
* Manage multi-warehouse operations efficiently
* Maintain accurate stock records
* Reduce operational errors
* Monitor complete inventory movement history

The system is designed to evolve into a comprehensive **warehouse optimization network**.

---

# Target Users

WEXON is designed for operational teams responsible for inventory control and warehouse management.

### Inventory Managers

Inventory managers are responsible for monitoring and controlling stock levels across warehouses.

Typical responsibilities include:

* Monitoring incoming and outgoing inventory
* Reviewing inventory levels and alerts
* Managing product information
* Analyzing stock movement history

### Warehouse Staff

Warehouse personnel perform day-to-day operational tasks within the warehouse.

Typical responsibilities include:

* Receiving goods from suppliers
* Picking and packing items for delivery
* Performing internal stock transfers
* Conducting physical inventory checks

---

# Authentication

The system includes a secure authentication flow for user access.

Authentication features include:

* User registration and login
* OTP-based password reset mechanism
* Secure session handling
* Automatic redirection to the inventory dashboard after successful authentication

---

# Dashboard

The dashboard provides a consolidated view of current inventory activity and operational metrics.

### Key Performance Indicators

The dashboard highlights important inventory statistics such as:

* Total products currently in stock
* Low-stock or out-of-stock items
* Pending incoming receipts
* Pending delivery orders
* Scheduled internal transfers

### Dynamic Filters

Users can filter dashboard data based on:

* Document type

  * Receipts
  * Delivery Orders
  * Internal Transfers
  * Inventory Adjustments

* Operational status

  * Draft
  * Waiting
  * Ready
  * Completed
  * Cancelled

* Warehouse or storage location

* Product category

---

# Core Modules

## Product Management

The product module manages the master catalog of items stored within the inventory system.

Key capabilities include:

* Creating and updating products
* Assigning SKU or product codes
* Defining product categories
* Configuring units of measure
* Setting optional initial stock values
* Viewing stock availability across locations

---

## Receipts (Incoming Inventory)

Receipts represent goods entering the warehouse from suppliers or vendors.

### Workflow

1. Create a new receipt document
2. Select the supplier
3. Add products and quantities received
4. Validate the receipt

Once validated, the system automatically updates inventory levels by **increasing the available stock**.

Example:

Receiving **50 units of Steel Rods** results in an increase of inventory by 50 units.

---

## Delivery Orders (Outgoing Inventory)

Delivery orders represent the shipment of goods from the warehouse to customers or other destinations.

### Workflow

1. Pick items from available inventory
2. Pack items for shipment
3. Validate the delivery order

After validation, the system automatically **reduces the available stock** for the delivered products.

Example:

A sales order requiring **10 chairs** results in the stock quantity of chairs being reduced by 10 units.

---

## Internal Transfers

Internal transfers allow organizations to move stock between different locations within the same company.

Examples include:

* Main warehouse to production floor
* Storage rack A to storage rack B
* Warehouse 1 to Warehouse 2

Internal transfers do not change the **total inventory quantity**, but they update the **physical location of the stock**.

All transfer operations are recorded in the inventory movement ledger.

---

## Stock Adjustments

Stock adjustments are used to reconcile differences between system records and physical inventory counts.

### Adjustment Process

1. Select the product and storage location
2. Enter the physically counted quantity
3. The system calculates the difference
4. The adjustment is recorded in the inventory ledger

Example:

If **3 kg of steel is damaged**, the system records a negative adjustment to reflect the loss.

---

# Inventory Flow Example

The following simplified scenario demonstrates a typical inventory lifecycle.

### Step 1 — Receive Goods from Vendor

A supplier delivers **100 kg of steel**.

The system records an increase in inventory.

---

### Step 2 — Move Inventory Within Warehouse

The steel is transferred from the **Main Store** to the **Production Rack**.

Total stock remains unchanged, but the storage location is updated.

---

### Step 3 — Deliver Finished Goods

The warehouse ships **20 steel units** to a customer.

The system reduces the available inventory accordingly.

---

### Step 4 — Adjust Damaged Inventory

During inspection, **3 kg of steel is identified as damaged**.

The system records a negative adjustment to maintain accurate inventory records.

All inventory changes are recorded in the **stock ledger**, ensuring complete traceability.

---

# Additional Features

The platform includes several additional capabilities to enhance inventory management:

* Low stock alerts
* Multi-warehouse support
* SKU-based product search
* Advanced filtering for inventory operations
* Complete inventory movement history
* Centralized stock ledger for auditing and traceability

---

# System Modules

The system is organized into the following primary modules:

* Products
* Inventory Operations

  * Receipts
  * Delivery Orders
  * Internal Transfers
  * Stock Adjustments
* Inventory Movement History
* Dashboard
* Warehouse Configuration
* User Profile Management

---

# Design Principles

WEXON is designed according to the following architectural principles:

* Modular system design
* Scalability for growing warehouse operations
* Extensibility for future integrations
* Real-time inventory updates
* Clear operational workflows

The architecture supports future expansion into areas such as:

* advanced analytics
* automated reorder rules
* ERP integrations
* multi-tenant warehouse environments

# Technology Stack

WEXON is built using a modern, scalable technology stack that separates the frontend user experience from the backend business logic and data persistence layer.

The architecture follows a **full-stack, API-driven design** to ensure maintainability, flexibility, and long-term scalability.

## Frontend

The frontend application is developed using **Next.js**, a React-based framework designed for building modern web applications.

Key advantages include:

* Server-side rendering and optimized performance
* Component-based architecture for maintainable UI development
* Efficient routing and page management
* Seamless integration with REST APIs
* Scalable frontend architecture suitable for enterprise systems

The user interface focuses on delivering a clear and responsive experience for warehouse staff and inventory managers.

## Backend

The backend services are implemented using **Spring Boot**, a widely adopted Java framework for building enterprise-grade applications.

Spring Boot provides:

* Robust REST API development
* Modular application structure
* Dependency injection and configuration management
* Secure authentication and authorization mechanisms
* Integration with data storage and external services

The backend is responsible for:

* Inventory business logic
* Stock movement processing
* Product management
* Transaction validation
* Inventory ledger generation

## Database

WEXON uses **MongoDB** as the primary database for storing inventory data.

MongoDB was selected due to its flexibility and scalability when managing complex inventory structures.

Key advantages include:

* Document-oriented data model
* High scalability for growing datasets
* Flexible schema design for evolving inventory requirements
* Efficient handling of nested inventory documents such as product batches and stock movements

## Architecture Overview

The system follows a **client–server architecture** where:

* The **Next.js application** acts as the user interface layer.
* The **Spring Boot backend** exposes REST APIs for all business operations.
* **MongoDB** stores product data, inventory movements, and operational records.

This layered architecture ensures a clear separation of concerns and enables the system to scale independently across frontend, backend, and data layers.

# Project Status

WEXON is currently under development as a foundational inventory management platform. The long-term objective is to evolve the system into a comprehensive warehouse excellence and optimization network.

---

# License

The licensing model for this project will be defined in a future release.
