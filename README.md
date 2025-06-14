# BugThrevs API

A secure Node.js backend API service built with Express and MongoDB, featuring JWT authentication, email verification, and comprehensive user management for bug bounty and security testing platforms.

## ✨ Features

- 🔐 **JWT Authentication** - Secure token-based authentication with refresh tokens
- 👥 **Multi-role System** - Support for users, company users, and admin roles
- ✉️ **Email Verification** - Secure account verification flow
- 🔑 **Password Management** - Secure password reset and update flows
- 🏢 **Company Management** - Company user management with invitations
- 🎯 **Engagement Management** - Create and manage security testing engagements
- 📊 **Dashboard** - Comprehensive reporting and analytics
- 🛡️ **Security** - Rate limiting, input validation, and secure headers
- 📱 **RESTful API** - Clean, consistent, and well-documented endpoints

## 🚀 Quick Start

### Prerequisites

- Node.js 16+
- MongoDB 5.0+
- NPM or Yarn

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/BugThrevs-APIs.git
   cd BugThrevs-APIs
   ```

2. Install dependencies:
   ```bash
   npm install
   # or
   yarn install
   ```

3. Create a `.env` file in the root directory with the following variables:
   ```env
   PORT=7854
   MONGODB_URL=your_mongodb_connection_string
   JWT_SECRET=your_jwt_secret
   JWT_REFRESH_SECRET=your_refresh_token_secret
   
   # Email Configuration
   SMTP_HOST=your_smtp_host
   SMTP_PORT=587
   SMTP_USER=your_smtp_username
   SMTP_PASS=your_smtp_password
   SMTP_SECURE=false
   EMAIL_FROM_NAME="BugThrevs"
   FRONTEND_URL=http://localhost:3000
   ```

4. Start the development server:
   ```bash
   npm run dev
   # or
   yarn dev
   ```

   The API will be available at `http://localhost:7854`

## 📚 API Documentation

### Base URL
```
http://localhost:7854/v1/api
```

### Authentication
All authenticated endpoints require a JWT token in the Authorization header:
```
Authorization: Bearer <access_token>
```

### Endpoints

#### Authentication

**User Login**
```http
POST /login/userlogin
```
Request body:
```json
{
  "email": "user@example.com",
  "password": "securepassword123"
}
```

**Company Login**
```http
POST /login/componylogin
```
Request body:
```json
{
  "email": "company@example.com",
  "password": "companypass123"
}
```

**Email Verification**
```http
GET /verify-email?token=<verification_token>&email=<user_email>
```

#### Engagements

**List Engagements**
```http
GET /engagement/list?page=1
```

**Get Engagement Details**
```http
GET /engagement/details/:id
```

**Create Engagement** (Super User Only)
```http
POST /engagement/create
```
Request body:
```json
{
  "name": "Web Application Test",
  "image": "https://example.com/image.jpg",
  "reward": "$1000-$5000",
  "scope": "example.com, api.example.com",
  "tags": ["web", "api"]
}
```

**Complete Engagement**
```http
POST /engagement/complete/:id
```
Request body:
```json
{
  "tagline": "Security Assessment",
  "summary": "Comprehensive security assessment of web application",
  "minReward": 1000,
  "maxReward": 5000,
  "industryName": "Technology",
  "label": "Web Application",
  "iconVariant": "web",
  "rules": "Standard testing rules apply",
  "policyUrl": "https://example.com/security-policy",
  "outOfScope": "Social engineering, DDoS"
}
```

## 🔧 Error Handling

All error responses follow this format:
```json
{
  "success": false,
  "message": "Error description",
  "code": "ERROR_CODE"
}
```

### Common Error Codes
- `INVALID_CREDENTIALS`: Invalid email or password
- `UNAUTHORIZED`: Missing or invalid authentication token
- `FORBIDDEN`: Insufficient permissions
- `NOT_FOUND`: Requested resource not found
- `VALIDATION_ERROR`: Request validation failed
- `EMAIL_ALREADY_EXISTS`: Email is already registered
- `TOKEN_EXPIRED`: Authentication token has expired

## 🛠️ Development

### Project Structure

```
src/
├── Models/               # Database models
│   ├── UserModel.js      # User accounts
│   ├── CompanyUserModel.js  # Company accounts
│   ├── Ingagements.js    # Engagement model
│   └── ...
│
├── Routes/              # API route handlers
│   ├── LoginRoute.js     # Authentication
│   ├── IngagementsRoute.js # Engagement management
│   ├── TokenRoute.js     # Token management
│   └── ...
│
├── Middleware/          # Custom middleware
│   ├── authMiddleware.js # Authentication
│   ├── superUserAuth.js  # Super user access control
│   └── ...
│
└── utils/              # Utility functions
    ├── emailService.js   # Email templates
    └── emailTransport.js # Email configuration
```

### Environment Variables

| Variable | Description | Required | Default |
|----------|-------------|----------|---------|
| PORT | Server port | No | 7854 |
| MONGODB_URL | MongoDB connection string | Yes | - |
| JWT_SECRET | Secret for JWT signing | Yes | - |
| JWT_REFRESH_SECRET | Secret for refresh tokens | Yes | - |
| SMTP_HOST | SMTP server host | Yes | - |
| SMTP_PORT | SMTP server port | Yes | - |
| SMTP_USER | SMTP username | Yes | - |
| SMTP_PASS | SMTP password | Yes | - |
| SMTP_SECURE | Use SSL/TLS | No | false |
| EMAIL_FROM_NAME | Sender name for emails | No | "BugThrevs" |
| FRONTEND_URL | Base URL for frontend | Yes | - |

## 📝 License

This project is licensed under the ISC License.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 🛠️ Development

### Project Structure

```
src/
├── Models/               # Database models
│   ├── UserModel.js      # User accounts
│   ├── CompanyUserModel.js  # Company accounts
│   ├── Ingagements.js    # Engagement model
│   ├── ReportsModel.js   # Reports
│   ├── LeaderboardModel.js # Leaderboard data
│   ├── HackactivityModel.js # Hacking activity tracking
│   ├── DashboardModel.js # Dashboard data
│   └── AdminUserModel.js # Admin users
│
├── Routes/              # API route handlers
│   ├── 2FARoute.js      # Two-factor authentication
│   ├── LoginRoute.js    # Authentication
│   ├── SignUpRoute.js   # User registration
│   ├── TokenRoute.js    # Token management
│   ├── TokenVerifyRoute.js # Token verification
│   ├── IngagementsRoute.js # Engagement management
│   ├── DashboardRoute.js # Dashboard endpoints
│   ├── CompanyPasswordRoute.js # Company password reset
│   └── PasswordRoute.js # User password reset
│
├── Middleware/         # Custom middleware
│   ├── auth.js          # Authentication
│   ├── authMiddleware.js # JWT verification
│   ├── superUserAuth.js # Super user verification
│   └── engagementAccessMiddleware.js # Engagement access control
│
└── utils/             # Utility functions
    ├── emailService.js  # Email templates
    ├── emailTransport.js # Email configuration
    └── passwordValidator.js # Password validation
```

## 🚀 Technologies Used

- **Node.js** - JavaScript runtime
- **Express** - Web framework
- **MongoDB** - NoSQL database
- **Mongoose** - MongoDB object modeling
- **JWT** - JSON Web Tokens for authentication
- **Nodemailer** - Email sending
- **Bcrypt** - Password hashing
- **Crypto-JS** - Cryptography utilities
- **Speakeasy** - Two-factor authentication
- **QR Code** - QR code generation for 2FA

## 📦 Dependencies

- **express** - Web framework
- **mongoose** - MongoDB ODM
- **jsonwebtoken** - JWT implementation
- **bcrypt** - Password hashing
- **nodemailer** - Email sending
- **crypto-js** - Cryptographic functions
- **dotenv** - Environment variable management
- **cors** - Cross-Origin Resource Sharing
- **qrcode** - QR code generation
- **speakeasy** - Two-factor authentication

### Development Dependencies
- **nodemon** - Development server with hot-reload

# BugThrevs APIs Documentation

### Engagement Management

#### List Engagements
```http
GET /v1/api/engagement/list?page=1
```
Public endpoint to list all engagements with pagination. No authentication required.

Query Parameters:
- `page` (optional): Page number, default is 1
- `limit` (fixed): 20 items per page

Response fields: `_id`, `name`, `tagline`, `image`, `minReward`, `maxReward`, `isDemo`, `accessStatus`, `reward`, `scope`, `tags`, `outOfScope`, `reportUrl`, `createdAt`, `isVerified`

#### Get Engagement Details
```http
GET /v1/api/engagement/details/:id
Authorization: Bearer <token>
```
Get detailed information about a specific engagement.

#### Create Engagement
```http
POST /v1/api/engagement/create
Authorization: Bearer <token>
Content-Type: application/json

{
    "name": "Engagement Name",
    "image": "image_url",
    "reward": "$1,000-$50,000",
    "scope": "scope_details",
    "tags": ["tag1", "tag2"]
}
```
Create a new engagement. Requires super-user authentication.

Note: The reward field should be provided as a string in the format "$min-$max" (e.g., "$1,000-$50,000"). The system will automatically convert this to an object with severity levels (critical, high, medium, low) based on the provided range.

#### Update Engagement
```http
PUT /v1/api/engagement/update/:id
Authorization: Bearer <token>
Content-Type: application/json

{
    "name": "Updated Name",
    "image": "updated_image_url",
    // Any other updatable fields
}
```
Update an existing engagement. Super-users can only update their own engagements.

Protected fields that cannot be updated:
- `superUserId`
- `isVerified`
- `verificationStatus`
- `verificationRemarks`
- `verifiedAt`

#### Complete Engagement
```http
POST /v1/api/engagement/complete/:id
Authorization: Bearer <token>
Content-Type: application/json

{
    "tagline": "Engagement tagline",
    "summary": "Detailed summary",
    "minReward": 100,
    "maxReward": 1000,
    "industryName": "Industry",
    "label": "Label",
    "iconVariant": "icon_type",
    "rules": "Engagement rules",
    "policyUrl": "policy_url",
    "outOfScope": "out_of_scope_details",
    "reportUrl": "report_submission_url"
}
```
Complete an engagement setup. Requires:
- Super-user authentication
- Engagement must be verified and approved
- All required fields must be provided

#### Delete Engagement
```http
DELETE /v1/api/engagement/delete/:id
Authorization: Bearer <token>
```
Delete an engagement. Super-users can only delete their own engagements.

### Common Error Responses
```json
{
    "success": false,
    "message": "Engagement not found",
    "code": "ENGAGEMENT_NOT_FOUND"
}
```
```json
{
    "success": false,
    "message": "Access denied. You can only manage your own engagements.",
    "code": "INSUFFICIENT_PERMISSIONS"
}
```
```json
{
    "success": false,
    "message": "Required fields missing",
    "code": "MISSING_FIELDS"
}
```
```json
{
    "success": false,
    "message": "Engagement must be verified and approved before completion.",
    "code": "NOT_VERIFIED"
}
```

### Important Notes

1. **Role-Based Access Control**
   - Members can view and manage their own engagements
   - Administrators can create, update, and delete any engagement
   - Owners have full control over engagements and team members
   - Administrators can manage team members except owners
   - Only owners can manage administrator roles

2. **Engagement States**
   - New engagements start as private and pending verification
   - Full details can only be added after verification is approved
   - Verification status: pending → approved/rejected

3. **Protected Fields**
   The following fields cannot be modified through updates:
   - superUserId (ownership)
   - isVerified
   - verificationStatus
   - verificationRemarks
   - verifiedAt


## Authentication

### User Sign Up
```http
POST /v1/api/signup/usersignup
Content-Type: application/json

{
    "firstname": "John",
    "lastname": "Doe",
    "username": "johndoe",
    "email": "john@example.com",
    "password": "securepassword",
    "country": "US"
}
```

Response:
```json
{
    "success": true,
    "message": "User created successfully. Please verify your email."
}
```

Error Responses:
```json
{
    "success": false,
    "message": "All fields are required"
}
```
```json
{
    "success": false,
    "message": "User already exists"
}
```
```json
{
    "success": false,
    "message": "Username already exists"
}
```

### User Login
```http
POST /v1/api/login/userlogin
Content-Type: application/json

{
    "email": "john@example.com",
    "password": "securepassword"
}
```

Response:
```json
{
    "success": true,
    "message": "User logged in successfully",
    "data": {
        "firstname": "John",
        "lastname": "Doe",
        "username": "johndoe",
        "email": "john@example.com",
        "country": "US",
        "role": "user",
        "accessToken": "jwt_access_token",
        "refreshToken": "jwt_refresh_token"
    }
}
```

Error Responses:
```json
{
    "success": false,
    "message": "Please provide both email and password",
    "code": "MISSING_FIELDS"
}
```
```json
{
    "success": false,
    "message": "User not found",
    "code": "USER_NOT_FOUND"
}
```
```json
{
    "success": false,
    "message": "Invalid password",
    "code": "INVALID_PASSWORD"
}
```
```json
{
    "success": false,
    "message": "Email not verified. Please verify your email first.",
    "code": "EMAIL_NOT_VERIFIED"
}
```

### Company Login
```http
POST /v1/api/login/componylogin
Content-Type: application/json

{
    "email": "company@example.com",
    "password": "securepassword"
}
```

Response:
```json
{
    "success": true,
    "message": "Company user logged in successfully",
    "data": {
        "firstname": "John",
        "lastname": "Doe",
        "email": "company@example.com",
        "companyname": "ACME Corp",
        "role": "super-user",
        "accessToken": "jwt_access_token",
        "refreshToken": "jwt_refresh_token"
    }
}
```

Error Responses:
```json
{
    "success": false,
    "message": "Please provide both email and password",
    "code": "MISSING_FIELDS"
}
```
```json
{
    "success": false,
    "message": "Company not found",
    "code": "COMPANY_NOT_FOUND"
}
```
```json
{
    "success": false,
    "message": "Invalid password",
    "code": "INVALID_PASSWORD"
}
```

### Token Refresh
```http
POST /v1/api/token/refresh
Content-Type: application/json

{
    "refreshToken": "your-refresh-token",
    "expiredAccessToken": "your-expired-access-token"
}
```

Response:
```json
{
    "success": true,
    "message": "Token refreshed successfully",
    "data": {
        "accessToken": "new-access-token",
        "refreshToken": "new-refresh-token"
    }
}
```

Error Responses:
```json
{
    "success": false,
    "message": "Both refresh token and expired access token are required",
    "code": "TOKENS_REQUIRED"
}
```
```json
{
    "success": false,
    "message": "Refresh token has expired. Please login again",
    "code": "REFRESH_TOKEN_EXPIRED"
}
```
```json
{
    "success": false,
    "message": "Invalid token",
    "code": "INVALID_TOKEN"
}
```

## Email Verification

### Verify Email
```http
GET /v1/api/verify-email?token=verification_token
```

Response:
```json
{
    "success": true,
    "message": "Email verified successfully"
}
```

Error Responses:
```json
{
    "success": false,
    "message": "Invalid verification token",
    "code": "INVALID_TOKEN"
}
```
```json
{
    "success": false,
    "message": "Verification token has expired",
    "code": "TOKEN_EXPIRED"
}
```

### Resend Verification Email
```http
POST /v1/api/verify-email/resend
Content-Type: application/json

{
    "email": "john@example.com"
}
```

Response:
```json
{
    "success": true,
    "message": "Verification email sent successfully"
}
```

Error Responses:
```json
{
    "success": false,
    "message": "Email is required",
    "code": "EMAIL_REQUIRED"
}
```
```json
{
    "success": false,
    "message": "User not found",
    "code": "USER_NOT_FOUND"
}
```

## Password Management

### Request Password Reset
```http
POST /v1/api/password/forgot
Content-Type: application/json

{
    "email": "john@example.com"
}
```

Response:
```json
{
    "success": true,
    "message": "Password reset instructions sent to email"
}
```

Error Responses:
```json
{
    "success": false,
    "message": "Email is required",
    "code": "EMAIL_REQUIRED"
}
```
```json
{
    "success": false,
    "message": "No account found with this email",
    "code": "EMAIL_NOT_FOUND"
}
```
```json
{
    "success": false,
    "message": "Error sending password reset email",
    "code": "EMAIL_SEND_ERROR"
}
```

### Reset Password
```http
POST /v1/api/password/reset
Content-Type: application/json

{
    "token": "reset_token",
    "newPassword": "new_secure_password"
}
```

Response:
```json
{
    "success": true,
    "message": "Password has been reset successfully. Please login with your new password."
}
```

Error Responses:
```json
{
    "success": false,
    "message": "Token and new password are required",
    "code": "MISSING_FIELDS"
}
```
```json
{
    "success": false,
    "message": "Invalid or expired reset token",
    "code": "INVALID_TOKEN"
}
```

## Profile Management

### Get User Profile
```http
GET /v1/api/signup/profile
Authorization: Bearer your_access_token
```

Response:
```json
{
    "success": true,
    "data": {
        "firstname": "John",
        "lastname": "Doe",
        "username": "johndoe",
        "email": "john@example.com",
        "country": "US"
    }
}
```

Error Responses:
```json
{
    "success": false,
    "message": "No authentication token provided",
    "code": "TOKEN_REQUIRED"
}
```
```json
{
    "success": false,
    "message": "User not found",
    "code": "USER_NOT_FOUND"
}
```

### Update User Profile
```http
PUT /v1/api/signup/profile
Authorization: Bearer your_access_token
Content-Type: application/json

{
    "firstname": "John",
    "lastname": "Doe",
    "country": "US"
}
```

Response:
```json
{
    "success": true,
    "message": "Profile updated successfully",
    "data": {
        "firstname": "John",
        "lastname": "Doe",
        "country": "US"
    }
}
```

Error Responses:
```json
{
    "success": false,
    "message": "No authentication token provided",
    "code": "TOKEN_REQUIRED"
}
```
```json
{
    "success": false,
    "message": "User not found",
    "code": "USER_NOT_FOUND"
}
```

### Profile Management

#### Get User Profile
```http
GET /v1/api/signup/profile
Authorization: Bearer your_access_token
```

#### Update User Profile
```http
PUT /v1/api/signup/profile
Authorization: Bearer your_access_token
Content-Type: application/json

{
    "firstname": "John",
    "lastname": "Doe",
    "country": "US"
}
```

### Password Management

#### Request Password Reset
```http
POST /v1/api/password/forgot
Content-Type: application/json

{
    "email": "john@example.com"
}
```

Response:
```json
{
    "success": true,
    "message": "Password reset instructions sent to email"
}
```

Error Responses:
```json
{
    "success": false,
    "message": "Email is required",
    "code": "EMAIL_REQUIRED"
}
```
```json
{
    "success": false,
    "message": "No account found with this email",
    "code": "EMAIL_NOT_FOUND"
}
```
```json
{
    "success": false,
    "message": "Error sending password reset email",
    "code": "EMAIL_SEND_ERROR"
}
```

#### Reset Password
```http
POST /v1/api/password/reset
Content-Type: application/json

{
    "token": "reset_token",
    "newPassword": "new_secure_password"
}
```

Response:
```json
{
    "success": true,
    "message": "Password has been reset successfully. Please login with your new password."
}
```

Error Responses:
```json
{
    "success": false,
    "message": "Token and new password are required",
    "code": "MISSING_FIELDS"
}
```
```json
{
    "success": false,
    "message": "Invalid or expired reset token",
    "code": "INVALID_TOKEN"
}
```

### Email Verification

#### Verify Email
```http
GET /v1/api/verify-email?token=verification-token
```

#### Resend Verification
```http
POST /v1/api/verify-email/resend
Content-Type: application/json

{
    "email": "john@example.com"
}
```

### Password Management

#### Request Password Reset
```http
POST /v1/api/password/forgot
Content-Type: application/json

{
    "email": "john@example.com"
}
```

#### Reset Password
```http
POST /v1/api/password/reset
Content-Type: application/json

{
    "token": "reset-token",
    "newpassword": "new-secure-password"
}
```

### Profile Management

#### Get Public Profile
```http
GET /v1/api/profile/:username
```

#### Get Private Profile
```http
GET /v1/api/profile
Authorization: Bearer your-jwt-token
```

#### Update Profile
```http
PUT /v1/api/profile
Authorization: Bearer your-jwt-token
Content-Type: application/json

{
    "firstname": "John",
    "lastname": "Doe",
    "country": "US",
    "biography": "Software Developer",
    "website": "https://johndoe.com",
    "twitter": "@johndoe",
    "linkedln": "johndoe",
    "github": "johndoe"
}
```

### Resume Management

#### Get Resume
```http
GET /v1/api/resume
Authorization: Bearer your-jwt-token
```

#### Update Resume
```http
PUT /v1/api/resume
Authorization: Bearer your-jwt-token
Content-Type: application/json

{
    "rsummery": "Experienced developer...",
    "rexperiance": [...],
    "reducation": [...],
    "rcertifications": [...]
}
```

## Environment Variables

```env
PORT=7854
MONGODB_URL=your-mongodb-url
JWT_SECRET=your-jwt-secret
JWT_REFRESH_SECRET=your-refresh-token-secret

# Email Configuration
SMTP_HOST=smtp.gmail.com
SMTP_PORT=465
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-specific-password
FRONTEND_URL=http://localhost:3000
```

## Security Features

1. **JWT Authentication**
   - Access tokens (15 minutes)
   - Refresh tokens (7 days)
   - Token verification endpoint
   - Token expiry tracking
   - Role-based access control
   - Company-specific tokens

2. **Password Security**
   - Secure password hashing
   - Password reset with expiring tokens
   - All sessions invalidated on password reset

3. **Email Verification**
   - Required email verification
   - Secure verification tokens
   - Token expiration (24 hours)
   - Custom templates for users and businesses
   - Persistent SMTP connections for better performance

4. **API Security**
   - Protected routes with JWT
   - Role-based route protection
   - Rate limiting (optional)
   - Input validation
   - Error handling

## Setup and Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/BugThrevs-APIs.git
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Set up environment variables:
   - Copy `.env.example` to `.env`
   - Update with your configuration

4. Start the development server:
   ```bash
   npm run dev
   ```

## Company Member Management

## Company Member Management

### Invite Member
```http
POST /v1/api/members/invite
Content-Type: application/json
Authorization: Bearer <token>

{
    "email": "user@example.com",
    "role": "member" // member, administrator, owner
}
```
Invite a new member to the company. Only owners and administrators can invite members.

Response:
```json
{
    "success": true,
    "message": "Invitation sent successfully",
    "data": {
        "id": "member_id",
        "email": "user@example.com",
        "role": "member",
        "status": "pending",
        "invitationToken": "token_for_accepting_invite"
    }
}
```

Error Responses:
```json
{
    "success": false,
    "message": "Email and role are required",
    "code": "MISSING_FIELDS"
}
```
```json
{
    "success": false,
    "message": "Invalid role specified",
    "code": "INVALID_ROLE"
}
```

### Accept Invitation
```http
POST /v1/api/accept-invitation
Content-Type: application/json

{
    "token": "invitation_token",
    "email": "user@example.com"
}
```

Response:
```json
{
    "success": true,
    "message": "Invitation accepted successfully"
}
```

### List Members
```http
GET /v1/api/members
Authorization: Bearer <token>
```
List all members of the company. Only owners and administrators can view the list.

Response:
```json
{
    "success": true,
    "data": [{
        "id": "member_id",
        "email": "user@example.com",
        "role": "member",
        "status": "accepted",
        "invitedBy": {
            "firstname": "John",
            "lastname": "Doe",
            "email": "john@example.com"
        }
    }]
}
```

### Remove Member
```http
DELETE /v1/api/members/:memberId
Authorization: Bearer <token>
```
Remove a member from the company. Only owners and administrators can remove members.

Response:
```json
{
    "success": true,
    "message": "Member removed successfully"
}
```

Error Responses:
```json
{
    "success": false,
    "message": "Member not found",
    "code": "MEMBER_NOT_FOUND"
}
```
```json
{
    "success": false,
    "message": "Cannot remove the last owner",
    "code": "LAST_OWNER"
}
```

### Token Management

#### Verify Token
```http
POST /v1/api/verify-token
Content-Type: application/json

{
    "token": "your_access_token"
}
```

Response:
```json
{
    "success": true,
    "message": "Token is valid",
    "data": {
        "valid": true,
        "expired": false,
        "userId": "user_id",
        "email": "user@example.com",
        "type": "user_type",
        "expiresIn": {
            "seconds": 3600,
            "minutes": 60,
            "hours": 1
        },
        "expiryTime": "2025-05-25T15:29:53+05:30"
    }
}
```

Error Responses:
```json
{
    "success": false,
    "message": "Token is required",
    "code": "TOKEN_REQUIRED"
}
```
```json
{
    "success": false,
    "message": "Token has expired",
    "code": "TOKEN_EXPIRED"
}
```

#### Refresh Token
```http
POST /v1/api/token/refresh
Content-Type: application/json

{
    "refreshToken": "your_refresh_token",
    "expiredAccessToken": "your_expired_access_token"
}
```

Response:
```json
{
    "success": true,
    "message": "Token refreshed successfully",
    "data": {
        "accessToken": "new_access_token",
        "refreshToken": "new_refresh_token"
    }
}
```

#### Revoke Token (Logout)
```http
POST /v1/api/token/revoke
Content-Type: application/json

{
    "refreshToken": "your_refresh_token"
}
```

Response:
```json
{
    "success": true,
    "message": "Logged out successfully"
}
```

## Available Scripts

- `npm start`: Run production server
- `npm run dev`: Run development server with hot-reload
- `npm test`: Run tests (if configured)

## Error Handling

All API endpoints return consistent error responses:

```json
{
    "success": false,
    "message": "Error description",
    "code": "ERROR_CODE"
}
```

## Error Codes Reference

**Authentication Errors:**
- `TOKEN_REQUIRED`: Authentication token missing
- `TOKEN_EXPIRED`: JWT has expired
- `INVALID_TOKEN`: Token is invalid
- `INSUFFICIENT_PERMISSIONS`: User lacks required role or permissions

**User Management:**
- `USER_NOT_FOUND`: User doesn't exist
- `EMAIL_NOT_VERIFIED`: Email verification required
- `EMAIL_SEND_ERROR`: Email delivery failed
- `INVALID_CREDENTIALS`: Wrong email or password

**Engagement Errors:**
- `ENGAGEMENT_NOT_FOUND`: Requested engagement doesn't exist
- `MISSING_FIELDS`: Required fields not provided
- `NOT_VERIFIED`: Engagement not yet verified
- `UNAUTHORIZED_ACCESS`: Cannot access other users' engagements

**Server Errors:**
- `SERVER_ERROR`: Internal server error
- `DATABASE_ERROR`: Database operation failed

## Environment Variables

Create a `.env` file in the root directory with the following variables:

```env
# Database
MONGODB_URL=mongodb://localhost:27017/bugthrevs

# Authentication
JWT_SECRET=your_jwt_secret_key
JWT_REFRESH_SECRET=your_refresh_token_secret

# Email Configuration
SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_USER=your_email@example.com
SMTP_PASS=your_email_password

# Application
FRONTEND_URL=http://localhost:3000
API_VERSION=v1
NODE_ENV=development
```

## Security Features

1. **Authentication**
   - JWT-based authentication
   - Refresh token rotation
   - Token blacklisting
   - Role-based access control

2. **Email Security**
   - Required email verification
   - Secure verification tokens
   - Custom templates for different user types
   - Rate limiting for email sends

3. **Data Protection**
   - Password hashing with bcrypt
   - Protected routes with role checks
   - Engagement ownership verification
   - Protected fields in updates

4. **API Security**
   - Input validation
   - Rate limiting
   - CORS protection
   - Error code standardization



