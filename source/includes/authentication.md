# Authentication

## Login

> Example Request Body

```json
{
  "email": "demo+partner@takemetour.com",
  "password": "teamtakemetour"
}
```

> Code

```shell
curl 'https://api.staging.takemetour.com/partner/auth/login' \
-H 'content-type: application/json' \
--data-binary '{"email":"demo+partner@takemetour.com","password":"teamtakemetour"}'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/auth/login',
{
  body: JSON.stringify({
    email: 'demo+partner@takemetour.com',
    password: 'teamtakemetour'
  }),
  headers: {
    'content-type': 'application/json'
  },
  method: 'POST',
});
const data = await response.json();
```

> Response

```json
{
  "access_token": "1yOaq7O9Lcp5AKJkzMajBQ2H9gnRq2ex",
  "user": {
    "name": {
      "first": "Dang",
      "last": "Nanglerng"
    },
    "avatar_image": "users/rtitM-14267784330583837.jpg",
    "partner_credit": 50000
  }
}
```
**HTTP Request:** `POST /auth/login`
### Request Body

Parameter | Type | Description
--------- | ---- | -----------
email | **String** | Partner's email which registered with TakeMeTour
password | **String** | Password (at least 8 characters)

### Response

Parameter | Type | Description
--------- | ---- | -----------
access_token | **String** | Access token which identify user (must be added to **x-access-token** header on other request)   
user | **Object** | Object of user's info 
## Logout
> Code

```shell
curl 'https://api.staging.takemetour.com/partner/auth/logout' -X DELETE \
-H 'content-type: application/json' \
-H 'x-access-token: 4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/auth/logout',
{
  headers: {
    'content-type': 'application/json',
    'x-access-token': '4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
  },
  method: 'DELETE',
});
const data = await response.json();
```
> Response

```json
{
  "success": true
}
```
**HTTP Request:** `DELETE /auth/logout`

### Response

Parameter | Type | Description
--------- | ---- | -----------
success | **Boolean** | Return logut status, can be `true` or `false`
## User info
> Code

```shell
curl 'https://api.staging.takemetour.com/partner/auth/me' \
-H 'content-type: application/json' \
-H 'x-access-token: 4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
```
```javascript
const response = await fetch('https://api.staging.takemetour.com/partner/auth/me',
{
  headers: {
    'content-type': 'application/json',
    'x-access-token': '4obGgRjmzYOnZLOEFfFsEycy04w9y8XQ'
  },
  method: 'GET',
});
const data = await response.json();
```
> Response

```json
{
  "isLoggedIn": true,
  "user": {
    "name": {
      "first": "Dang",
      "last": "Nanglerng"
    },
    "avatar_image": "users/rtitM-14267784330583837.jpg",
    "partner_credit": 50000
  }
}
```
**HTTP Request:** `GET /auth/me`

### Response

Parameter | Type | Description
--------- | ---- | -----------
isLoggedIn | **Boolean** | Login status   
user | **Object** | Object of user's info 
