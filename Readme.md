# Online Bank Backend

Node.js/Express digital banking backend with customer authentication, banking operations, NIBSS integration, and role-based staff management.

**Live API:** https://online-bank-sd4s.onrender.com

## Role Hierarchy

```text
SUPER ADMIN
     ↓
   ADMIN
     ↓
   STAFF
```

### Staff Authentication

All staff roles use:

```text
POST /staff/login
```

The response includes a JWT and the staff role. The frontend uses the role to display the appropriate dashboard.

### Staff Management

```text
POST   /staff/register
POST   /staff/admins
PATCH  /staff/:staffId/role
PATCH  /staff/:staffId/status
PATCH  /staff/:staffId
DELETE /staff/:staffId
GET    /staff/
GET    /staff/:staffId
```

Only authorized admins and super admins can perform staff-management actions. The super admin cannot be deleted or deactivated.

The first super admin is created securely with:

```bash
node Scripts/createSuperAdmin.js
```

Credentials are stored in `.env`.

## Customer API

```text
POST /customers/register
POST /customers/login
GET  /customers/profile
GET  /customers/transactions
```

## Banking API

```text
GET  /bank/my-accounts
POST /bank/account
POST /bank/name-enquiry
POST /bank/validate-bvn
POST /bank/validate-nin
POST /bank/transfer
POST /bank/transfer-status
POST /bank/account-balance
```

Protected routes require authentication.

## NIBSS Integration

The backend uses a simulated NIBSS API for account creation, name enquiry, BVN/NIN validation, transfers, transaction status, balances, and identity test data.

## Security

- Passwords are hashed with bcrypt.
- Authentication uses JWT.
- Staff roles are enforced by the backend.
- Sensitive credentials are stored in environment variables.
- `.env` must never be committed to GitHub.

## Project Structure

```text
digital-bank/
├── Config/
├── Controllers/
├── Middleware/
├── Models/
├── Routes/
├── Services/
├── Scripts/
│   └── createSuperAdmin.js
├── .gitignore
├── app.js
├── package.json
└── package-lock.json
```

## Status Codes

`200` Success | `201` Created | `400` Bad Request | `401` Unauthorized | `403` Forbidden | `404` Not Found | `409` Conflict | `500` Server Error

## Deployment

**Production:** https://online-bank-sd4s.onrender.com

Environment variables should be configured directly on Render.

**Author:** Versatile
