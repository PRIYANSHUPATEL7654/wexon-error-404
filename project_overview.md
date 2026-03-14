# WEXON (Warehouse EXcellence & Optimization Network)

Hackathon-ready Warehouse Management System aligned to the CoreInventory problem statement.

Default Username and Password:
Email: admin@wexon.in
Password: Qwerty@123

## Repo structure
- `wexon-ui/` (Frontend): Next.js (App Router) + TanStack Query + shadcn/ui + JSONForms
- `wexon-api/` (Backend): Spring Boot + MongoDB + Mongock migrations

## Environments & ports (local)
- API base: `http://localhost:8083/api/v1`
- UI: Next.js dev server (see `wexon-ui/package.json`)

## Auth & API response shape
- Auth: `Authorization: Bearer <token>` (token returned by login)
- Standard response wrapper: `{ "message": string, "data": <payload> }`
  - Note: the frontend Axios instance **already unwraps** the HTTP response to `response.data` in an interceptor.

## Demo data (client demo)
Demo seed migration creates realistic entities and transactions so KPIs and “Move History” look populated.
- Migration: `wexon-api/src/main/java/com/wexon/software/wexon_api/migrations/V1_2_DemoDataSeedMigration.java`
- Creates: vendors, warehouses, locations, products, product inventory, batch inventory, and sample operations
- Adds pending operations (CREATED) so Dashboard counters are non-zero

## Roles (seeded)
Roles are created (idempotent) by:
- `wexon-api/src/main/java/com/wexon/software/wexon_api/migrations/V1_0_DefaultAdminMigration.java` (SUPER_ADMIN + default admin user)
- `wexon-api/src/main/java/com/wexon/software/wexon_api/migrations/V1_3_RolesSeedMigration.java` (ADMIN, MANAGER, STAFF)

## UI pages (key routes)
- Dashboard: `/dashboard` (KPIs + quick actions + recent operations)
- Operations:
  - Receipt (Incoming): `/operations/receipts/create`
  - Delivery (Outgoing): `/operations/delivery-orders/create`
  - Internal Transfer: `/operations/internal-transfers/create`
  - Adjustment: `/operations/adjustments/create`
- Move History: `/move-history`
- Master Entities:
  - Products: `/product/list`
  - Vendors / Parties: `/vendor/list`
  - Warehouses: `/warehouse/list`
  - Locations: `/locations/list`
- Admin (SUPER_ADMIN only): `/users/list` (user management)

## Twilio (SMS)
Twilio credentials are **not committed** (GitHub secret scanning).
Configure via env:
- `TWILIO_ACCOUNT_SID`
- `TWILIO_AUTH_TOKEN`
- `TWILIO_OUTGOING_SMS_NUMBER`
Config file: `wexon-api/src/main/resources/application.yaml`

---

## API Routes (v1)
Base prefix: `/api/v1`

### Auth
- `POST /auth/login`

### Dashboard
- `GET /dashboard/kpis`

### Users (Super Admin)
- `GET /user/getCurrentUser`
- `GET /user/getAll`
- `GET /user/{id}`
- `POST /user`
- `PUT /user/{id}`
- `DELETE /user/{id}`

### Roles
- `GET /roles/getAll`
- `GET /roles/{id}`
- `POST /roles`
- `PUT /roles/{id}`
- `DELETE /roles/{id}`

### Vendors / Parties
- `POST /vendor/create`
- `PUT /vendor/update/{id}`
- `DELETE /vendor/delete/{id}`
- `GET /vendor/get/{id}`
- `POST /vendor/getVendorListWithFilter`
- `POST /vendor/getVendorListWithPaginationAndFilter`

### Products
- `POST /product/create`
- `PUT /product/update/{id}`
- `DELETE /product/delete/{id}`
- `GET /product/get/{id}`
- `POST /product/getProductListWithFilter`
- `POST /product/getProductListWithPaginationAndFilter`

### Warehouses
- `POST /warehouse/create`
- `PUT /warehouse/update/{id}`
- `DELETE /warehouse/delete/{id}`
- `GET /warehouse/get/{id}`
- `POST /warehouse/getWarehouseListWithFilter`
- `POST /warehouse/getWarehouseListWithPaginationAndFilter`
- `GET /warehouse/getStats`

### Warehouse Locations
- `POST /warehouse/locations/create`
- `PUT /warehouse/locations/update/{id}`
- `DELETE /warehouse/locations/delete/{id}`
- `GET /warehouse/locations/get/{id}`
- `POST /warehouse/locations/getAll`
- `POST /warehouse/locations/getAllWithPagination`

### Inventory Transactions (Operations)
- `POST /inventory/transactions/processCreate`
- `POST /inventory/transactions/processApproval/{id}`
- `GET /inventory/transactions/getInventoryTransaction/{id}`
- `DELETE /inventory/transactions/deleteInventoryTransaction/{id}`
- `POST /inventory/transactions/getTransactionListWithFilter`
- `POST /inventory/transactions/getTransactionListWithPaginationAndFilter`

### Inventory Transaction Details
- `POST /inventory/transactions/details/create/{transactionId}`
- `PUT /inventory/transactions/details/update/{id}`
- `DELETE /inventory/transactions/details/delete/{id}`
- `GET /inventory/transactions/details/getTransactionDetail/{id}`
- `POST /inventory/transactions/details/getTransactionDetailListWithFilter`
- `POST /inventory/transactions/details/getTransactionDetailWithPaginationAndFilter`

### Batch Inventory
- `POST /inventory/batch-inventory/getBatchInventoryListWithFilter`
- `POST /inventory/batch-inventory/getBatchInventoryListWithPaginationAndFilter`

### Ledger
- `GET /ledger/account/getLedgerAccountByEntityId/{id}`
- `GET /ledger/transaction/getLedgerTransactionByEntityId/{id}`

### SMS (Twilio)
- `POST /notification/sms/send`

---

## Notes (pagination + filters)
- “WithPaginationAndFilter” routes accept:
  - `filters` as JSON body (object/map)
  - pagination via query params (`page`, `size`, `sort`)
    - example: `?page=0&size=20&sort=createdAt,desc`
