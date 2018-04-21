# Quarteria API

### GET https://api.quarteria.io/v1/getCrowdsaleInfo

To get Number of Tokens Available, Neo/XQT rate, GAS/XQT rate and number of tokens sold.

#### Expected response

200

    {
      "result": {
        tokensAvailable: integer,
        neoRate: integer,
        gasRate: integer,
        tokensSold: integer,
        initialSaleAmount: 73500000
      }
    }

#### Error response

500

{
  "result": error
}

### GET https://api.quarteria.io/v1/getAddressInfo?address=USER_ADDRESS

To get XQT balance, Neo contribution, GAS contribution and KYC registration state.

USER_ADDRESS = user NEO wallet address (i.e APyEx5f4Zm4oCHwFWiSTaph1fPBxZacYVR)

#### Expected response

200

    {
      "result": {
        balance: integer,
        neo: integer,
        gas: integer,
        isRegistered: integer (zero or one)
      }
    }

#### Error response

500

    {
      "result": error
    }

### POST https://api.quarteria.io/v1/register

To register an user

#### Expected request parameters

    {
      name: string,
      email: string,
      password: string
    }

#### Expected response

200

    {
      result: "User stored. You will recieve an email to confirm your registration"
    }
  
#### Error response
400

    {
      "result": "Email is already registered"
    }
    
500

    {
      "result": error
    }

### PUT https://api.quarteria.io/v1/emailVerification?code=UNIQUE_VERIFICATION_CODE

To verify user's email

UNIQUE_VERIFICATION_CODE = code generated in the user's registration.

#### Expected response

200

    {
      result: "Email confirmed"
    }
  
#### Error response

400

    {
      "result": "Invalid link"
    }

### GET https://api.quarteria.io/v1/resendVerificationEmail?email=USER_EMAIL

To resend the verification email

#### Expected response

200

    {
      result: "Verification email sent"
    }
  
#### Error response

if USER_MAIL was not provided

400

    {
      "result": "Invalid request"
    }

if USER_MAIL was not found on DB

400

    {
      "result": "Email not registered"
    }

### GET https://api.quarteria.io/v1/unique?email=USER_EMAIL

To check if email already registered

#### Expected response

200

    {
      result: boolean
    }
  
#### Error response

500

    {
      "result": error
    }

### POST https://api.quarteria.io/v1/login

To sign in an user

#### Expected request parameters

    {
      email: string,
      password: string
    }

#### Expected response

    {
      result: "User stored. You will recieve an email to confirm your registration"
    }
  
#### Error response

401

    {
      "result": "User not registered"
    }

401

    {
      "result": "Password did not match"
    }

### GET https://api.quarteria.io/v1/validPasswordRecovery?code=UNIQUE_VERIFICATION_CODE

To verify password recovery link

UNIQUE_VERIFICATION_CODE = code generated when user reuest password recovery

#### Expected response

200

    {
      result: boolean
    }
  
#### Error response

400

    {
      "result": false
    }

### PUT https://api.quarteria.io/v1/passwordReset?code=UNIQUE_VERIFICATION_CODE

To reset the user's password

UNIQUE_VERIFICATION_CODE = code generated when user reqest password recovery

#### Expected request parameters

    {
      password: string
    }

#### Expected response

200

    {
      result: "Password changed"
    }
  
#### Error response

400

    {
      "result": "Invalid link"
    }

### POST https://api.quarteria.io/v1/forgotPassword

To request password reset and send email with recovery code

#### Expected request parameters

    {
      email: string
    }

#### Expected response

200

    {
      result: "Email sent"
    }
  
#### Error response

When cannot send email

400

    {
      "result": "An error occurred while sending email"
    }

When use an invalid email in the request

400

    {
      "result": "Invalid email"
    }

### GET https://api.quarteria.io/v1/logged

To check if an user session is active


#### Expected response

200

    {
      result: {
        name: string,
        email: string
      }
    }
  
#### Error response

400

Unauthorized

### GET https://api.quarteria.io/v1/logout

To logout an user


#### Expected response

200

    {
      result: "logout"
    }
  
#### Error response

400

Unauthorized
