# JWT Authentication Guide 🚀

![JWT](https://img.shields.io/badge/JWT-Authentication-blue.svg)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-Security-green.svg)

## 📌 Overview
JSON Web Token (JWT) is an **open standard** used for securely transmitting information between parties as a **JSON object**. It is digitally signed using algorithms like **HMAC, RSA, or ECDSA**, ensuring **data integrity and authenticity**.

## ❓ Why Use JWT?
✅ **Authorization** → Allows access to protected routes without repeated authentication.  
✅ **Information Exchange** → Ensures secure and reliable data transfer between users and systems.

---

## 📜 JWT Structure
A JWT consists of three parts:

1. **Header**  
   - Defines the type of token (JWT) and the signing algorithm (e.g., HS256).  
2. **Payload**  
   - Contains **claims** (user data & metadata).  
   - Example: User ID, role, expiration time.  
3. **Signature**  
   - Ensures the token's integrity using **HMAC, RSA, or Base64 encoding**.  

🔗 Example JWT:
```json
{
  "alg": "HS256",
  "typ": "JWT"
}
{
  "sub": "1234567890",
  "name": "John Doe",
  "iat": 1516239022
}
[Signature]
```
## 🔄 JWT Authentication Flow

1. User Signs In
   - The client sends credentials (username & password) to the authentication server.

2. Server Authenticates the User
   - Checks credentials against the database.
   - If valid, generates a JWT token.

3. JWT is Sent to the User
   - The server sends the token back to the client.

4. User Makes API Requests
   - The user includes the JWT in the Authorization header (Bearer JWT).

5. Server Validates JWT
   - If the token is valid and not expired, access is granted to protected routes.

## ⚙️ Steps to Implement JWT in Backend

### 1️⃣ User Registration (Sign Up)
``` java
// Validate request body
@Valid @RequestBody

// Check if the user already exists
userRepository.findByUsername(username);
userRepository.existsByEmail(email);

// Password Handling
passwordEncoder.encode(password);

// Role Management
@Document(collection = "users")
@DBRef
```
### 2️⃣ User Login (Sign In)

``` java
// Use Authentication Manager to validate user credentials
authenticationManager.authenticate(
    new UsernamePasswordAuthenticationToken(username, password)
);

// If authentication is successful, generate a JWT token
String token = jwtUtils.generateJwtToken(authentication);
```
## 🔐 Security with Spring Security

✅ Security Filter Chain → Ensures each request is checked before accessing secure endpoints.
✅ CSRF Protection (Cross-Site Request Forgery) → Prevents unauthorized actions on behalf of authenticated users.
✅ Authorization Filtering → Uses Http.addFilterBefore() to verify JWT before processing requests.

## 🔍 JWT Validation & Access Control

- The token is verified for validity and user roles.
- If valid → Access is granted to protected resources.
- If invalid or expired → Access is denied, and the user must re-authenticate.

## 🛠️ Technologies Used

- Spring Boot (Security & JWT)
- Java
- Maven
- MongoDB

#### Happy Coding 🚀


