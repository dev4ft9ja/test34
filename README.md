---

# PORJECT ANYON

This a comprehensive documentation to the entire backend enpoint and workflow for the project Anyone.

## Prerequisites

Before you begin, ensure you have the following installed:

- **Python:** The application runs on python. If you haven't installed it yet, you can download by searching on google.
- **Chat Application Backend:** Ensure the backend server of the Chat Application is up and running. You can find the backend code and setup instructions in the [Chat Application Backend Repository](https://github.com/Nwafor6/Chatapp-BE.git).

## Installation

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/Nwafor6/Chatapp-FE.git
   cd <project-folder>
   ```

2. **Install Dependencies:**
   ```bash
   npm install
   ```

3. **Set Environment Variables:**
   If your frontend application communicates with the backend, make sure to set the appropriate backend API endpoint as an environment variable in your `.env` file.

4. **Start the Application:**
   ```bash
   npm start
   ```

## API Endpoints and workflow

# Signup Workflow
The project Anyon has two registration enpoint first which is this "api/register/" and the other which is the 
"api/sign-with-google/". The "api/register/"; This enpoint is used to register users who wants to sign up into the platform using the signup option using their email and password. After a successful registration, a success messge telling them a token has been sent 
to their mail and the users details is also attached to the response. The verification token will be used to verify their account.

The "api/sign-with-google/", This enpoint is used to register users who wants to sign up into the platform using the signin with google option using their gmail account. After a successful registration, the refresh, access and user details is returned as a response. 

# Quick note. 
- This users who uses this enpoint do not require account verification. Their accounts are auto verified from google.
- This enpoint signs the up and log them in at first request. At subsequent request, the enpoint only signs then in.


See example of these two enpoints below.

- **POST /api/register/: Register a new user using email **
  see paramter values example below.

   ```bash
   
      {
         "email":"email@example.com",
         "password":"passqord",
         "firstname":"Glory",
         "lastname":"Ebube"
      }

   ```

   # Response
   ```bash
   
      {
         "detail": "A token has been sent to your mail",
         "user": {
            "id": 22,
            "email": "nwafor13@gmail.com",
            "firstname": "Glory",
            "lastname": "Ebube",
            "has_2fa": false,
            "twofa_type": "none",
            "signup_type": "email",
            "totp_url": null,
            "date_joined": "2023-11-20T12:16:22.814990Z",
            "last_login": null
         }
    }

   ```

   - **POST /api/sign-with-google/: Register a new user using google **
  see paramter values example below.

   ```bash
   
      {
         "email":"email@example.com",
         "firstname":"Glory",
         "lastname":"Ebube"
      }

   ```

   # Response
   ```bash
   
      {
         "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTcwMzkzOTE3OSwiaWF0IjoxNzAwNDgzMTc5LCJqdGkiOiI0NTM2ZTVhM2M1ZWM0ODI1YTYwN2JiODRhMTZiMGJlZCIsInVzZXJfaWQiOjI0fQ.eSFmjUFYnXVlBPUClNeZNmizvlK8CrYZEBmcqNH6fmA",
         "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNzAzMDc1MTc5LCJpYXQiOjE3MDA0ODMxNzksImp0aSI6ImE5MTM5NzMzZWQzYjRkOTQ4YzcwZDQ1YzU4Zjk1Nzg5IiwidXNlcl9pZCI6MjR9.9lB0ITiSXFqQcBTslM9cZZjLjOYMVJ9iD__BsJsEvlg",
         "user": {
            "id": 24,
            "email": "nwafor16@gmail.com",
            "firstname": "Glory",
            "lastname": "Ebube",
            "has_2fa": false,
            "twofa_type": "none",
            "signup_type": "google",
            "totp_url": null,
            "date_joined": "2023-11-20T12:26:14.943569Z",
            "last_login": "2023-11-20T12:26:14.943341Z"
         }
      }

   ```


# Resend token .
Users who did not get verification token can request for a resend of the verification token using this 
enpoint sending their email as a params.

- **PUT /api/register/?email=email@example.com

# Response
```bash

   "Token Resent"

```

# verify token .

Verification token sent to email signup user, is sent to this enpoint to activate the users account.

- **PUT /api/verify_token/

# 
```bash

   {
      "token":"123456",
      "user_email":"example@.com"
   }

```
# Response
```bash

   {
      "detail": "Account verifed."
   }

```

# Signin Enpoint

## Workflow.

There exists two enpoint for sigin into the platform. The first which is with the 
user's email and password and the otger which is with google.

- **POST /api/login/ **
  see paramter values example below.

   ```bash
   
      {
         "email":"email@example.com",
         "password":"password"
      }

   ```

   # Response
   ```bash
   
      {
         "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTcwMzkzOTE3OSwiaWF0IjoxNzAwNDgzMTc5LCJqdGkiOiI0NTM2ZTVhM2M1ZWM0ODI1YTYwN2JiODRhMTZiMGJlZCIsInVzZXJfaWQiOjI0fQ.eSFmjUFYnXVlBPUClNeZNmizvlK8CrYZEBmcqNH6fmA",
         "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNzAzMDc1MTc5LCJpYXQiOjE3MDA0ODMxNzksImp0aSI6ImE5MTM5NzMzZWQzYjRkOTQ4YzcwZDQ1YzU4Zjk1Nzg5IiwidXNlcl9pZCI6MjR9.9lB0ITiSXFqQcBTslM9cZZjLjOYMVJ9iD__BsJsEvlg",
         "user": {
            "id": 24,
            "email": "nwafor16@gmail.com",
            "firstname": "Glory",
            "lastname": "Ebube",
            "has_2fa": false,
            "twofa_type": "none",
            "signup_type": "email",
            "totp_url": null,
            "date_joined": "2023-11-20T12:26:14.943569Z",
            "last_login": "2023-11-20T12:26:14.943341Z"
         }
      }

   ```

# Set up 2FA

## Workflow.

Setup 2fa for user account. The available options are [email, authapps, sms].

- The "email" turns on email 2fa on 
- The "authapps" turns on authapps 2fa option.
- The "sms" turns on sms 2fa option.

To turn of 2fa,use the same enpoint which same action key.

## authapp

- **POST /api/2fa_on_off/ **
  see paramter values example below.

   ```bash
   
      {
         "action":"authapps"
      }

   ```

   # Response
   ```bash
   
      {
         "detail": "2FA turn on successsfully",
         "qr_url": "media/nwafor2@gmail.com_totp_qr.png",
         "user": {
            "id": 11,
            "email": "nwafor2@gmail.com",
            "firstname": "Glory",
            "lastname": "Ebube",
            "has_2fa": true,
            "twofa_type": "authapps",
            "signup_type": "none",
            "totp_url": "/media/media/nwafor2%40gmail.com_totp_qr.png",
            "date_joined": "2023-11-16T08:58:03.923828Z",
            "last_login": "2023-11-20T12:42:46.457235Z"
         }
      }

   ```

# Sigin with 2fa

Users who has set 2FA on from their dashboard, are required to provide the token via this endpoint

## Workflow.
The users has to use the login enpoint, and this will trigger the token which will be sent to their email for "email 2fa" and phone number for "sms 2fa". User with authapps, will have to get the token from their authentication application.

## authapp

- **POST /api/login-with-2fa/ **
  see paramter values example below.

   ```bash
   
      {
      "email":"nwafor2@gmail.com",
      "password":"1234",
      "token":"779416"
      }
   ```

   # Response
   ```bash

      {
            "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTcwMzkzOTE3OSwiaWF0IjoxNzAwNDgzMTc5LCJqdGkiOiI0NTM2ZTVhM2M1ZWM0ODI1YTYwN2JiODRhMTZiMGJlZCIsInVzZXJfaWQiOjI0fQ.eSFmjUFYnXVlBPUClNeZNmizvlK8CrYZEBmcqNH6fmA",
            "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNzAzMDc1MTc5LCJpYXQiOjE3MDA0ODMxNzksImp0aSI6ImE5MTM5NzMzZWQzYjRkOTQ4YzcwZDQ1YzU4Zjk1Nzg5IiwidXNlcl9pZCI6MjR9.9lB0ITiSXFqQcBTslM9cZZjLjOYMVJ9iD__BsJsEvlg",
            "user": {
               "id": 24,
               "email": "nwafor16@gmail.com",
               "firstname": "Glory",
               "lastname": "Ebube",
               "has_2fa": false,
               "twofa_type": "none",
               "signup_type": "email",
               "totp_url": null,
               "date_joined": "2023-11-20T12:26:14.943569Z",
               "last_login": "2023-11-20T12:26:14.943341Z"
            }
         }

   ```

# PROFILE
After a successful login an activation, users are directed to their dashboard where they can update their profile as please.

- **PUT /api/profile**: 
    
    ```bash
   
      {
         "address":"Abujeeee",
         "paypal_address":"sdf",
         "profile_img":"image",
         "phone":"!23456789",
         "proof_of_id":"file",
         "proof_of_address":"file",
         "bank_name":"fcmb",
         "account_number":"2345678"
      }

   ```

   # Response
   ```bash

            {
            "detail": {
               "user": 11,
               "address": "Abujeeee",
               "referral_code": "",
               "profile_img": null,
               "phone": null,
               "proof_of_id": null,
               "proof_of_address": null,
               "bank_name": null,
               "account_number": null,
               "paypal_address": "sdf"
            },
            "user": {
               "id": 11,
               "email": "nwafor2@gmail.com",
               "firstname": "Glory",
               "lastname": "Ebube",
               "has_2fa": true,
               "twofa_type": "authapps",
               "signup_type": "none",
               "totp_url": "/media/media/nwafor2%40gmail.com_totp_qr.png",
               "date_joined": "2023-11-16T08:58:03.923828Z",
               "last_login": "2023-11-20T12:42:46.457235Z"
            }
      }

   ```

- **GET /api/profile**:

   # Response
   ```bash

            {
            "detail": {
               "user": 11,
               "address": "Abujeeee",
               "referral_code": "",
               "profile_img": null,
               "phone": null,
               "proof_of_id": null,
               "proof_of_address": null,
               "bank_name": null,
               "account_number": null,
               "paypal_address": "sdf"
            },
            "user": {
               "id": 11,
               "email": "nwafor2@gmail.com",
               "firstname": "Glory",
               "lastname": "Ebube",
               "has_2fa": true,
               "twofa_type": "authapps",
               "signup_type": "none",
               "totp_url": "/media/media/nwafor2%40gmail.com_totp_qr.png",
               "date_joined": "2023-11-16T08:58:03.923828Z",
               "last_login": "2023-11-20T12:42:46.457235Z"
            }
      }

   ```

# Update password from Dashbaord
**POST /api/update-password-dashboard/**

```bash

   {
      "current_password":"12345",
      "new_password1":"1234",
      "new_password2":"1234"
   }


```

# Response

```bash

   {
      "detail": "Password updated successfully"
   }

```

# Forgotten password

The reset password or forgotten password can be completed in 3 steps which include;,
- Request for password reset token
- confirm/check token validity 
- update password if reset token is valid

Note: The reset token is only valid for 10mins after which it becomes invalid by default and the users would have to generate another token.

## Step One: REQUEST RESET TOKEN

**POST /api/reset-password/**

```bash

   {
      "email":"nwafor2@gmail.com"
   }


```

# Response

```bash

   {
      "detail": "Reset password token has been sent to your email. Token will expire in 10mins"
   }

```

## Step Two: CONFIRM RESET TOKEN

NOTE: Step two can be skipped to  step three, since step3 also validates token before updating the 
user's password. 

**GET /api/reset-password/?email=nwafor2@gmail.com&token=72696964**


# Response 200

```bash

   {
      "detail": "OK"
   }

```

# Response 400

```bash

   {
      "detail": "Invalid token"
   }

```

## Step Three: UPDATE PASSWORD

**PUT /api/reset-password/**

```bash

   {
      "email":"nwafor2@gmail.com",
      "token":"72696964",
      "new_password1":"1234",
      "new_password2":"1234"
   }

```

# Response

```bash

   {
      "detail": "Password updated successfully"
   }

```
# Other error responses
# Response 400

- Invalid token or expired token

```bash

   {
      "detail": "Invalid token"
   }

```

# Response 400

- If new passwords do not match

```bash

   {
      "detail": "new_password1 and new_passowrd2 must match"
   }

```

# Response 400

- If a wrong email is attached to the token

```bash

   {
      "detail": "User with this email not found."
   }

```

