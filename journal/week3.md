# Week 3 — Decentralized Authentication
## To implement MFA with Cognito JWT and SMS, you can follow these steps:
   ---------------------------------------------------------------------

1. Create a Cognito user pool and configure MFA settings. In the user pool settings, set the MFA to "Required" and choose the "SMS text message" option for the second factor.

2. Create an App client in the user pool and enable the "Enable username-password (non-SRP) flow for app-based authentication" option. This will allow you to authenticate users using a username and password, and then obtain a JWT token from Cognito.

3. Install the boto3 and cognito_jwt Python libraries:  
```python
pip install boto3
pip install cognito-jwt
```
4. Use the following Python code to authenticate a user, obtain a JWT token, and send an MFA SMS message:  
```python
import boto3
from cognitojwt import decode

# Initialize the Cognito client
client = boto3.client('cognito-idp')

# User authentication
response = client.initiate_auth(
    ClientId='your_app_client_id',
    AuthFlow='USER_PASSWORD_AUTH',
    AuthParameters={
        'USERNAME': 'your_username',
        'PASSWORD': 'your_password',
    },
)

# Obtain the JWT access token
access_token = response['AuthenticationResult']['AccessToken']

# Decode the JWT token to obtain the "cognito:username" and "phone_number_verified" claims
claims = decode(access_token, 'your_user_pool_id', region_name='your_aws_region')

# Check if the phone number is verified
if claims.get('phone_number_verified'):
    # Send the SMS MFA message
    response = client.send_user_mfa_sms_code(
        UserPoolId='your_user_pool_id',
        ClientId='your_app_client_id',
        Username=claims['cognito:username']
    )
    print(f'SMS sent to {response["CodeDeliveryDetails"]["Destination"]}.')
else:
    print('Phone number is not verified.')

``` 
**We have to replace the placeholders *your_app_client_id*, *your_username*, *your_password*, *your_user_pool_id*, and *your_aws_region* with our own values. Also, make sure that the IAM role associated with our AWS credentials has the necessary permissions to interact with Cognito.**
