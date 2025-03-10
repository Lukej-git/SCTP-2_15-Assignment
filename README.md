# SCTP-2_15-Assignment

## 1. What is needed to authorize your EC2 to retrieve secrets from AWS Secrets Manager?
To authorize an EC2 instance to retrieve secrets from AWS Secrets Manager, you need:

- An IAM role attached to the EC2 instance with the required permissions.
- An IAM policy granting secretsmanager:GetSecretValue permission on the specific secret.
- Proper trust relationship in the IAM role allowing EC2 to assume it.

## 2. Derive the IAM policy (i.e. JSON)?
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "secretsmanager:GetSecretValue",
            "Resource": "arn:aws:secretsmanager:<region>:<account-id>:secret:prod/cart-service/credentials-*"
        }
    ]
}
```
Replace '<region>' and '<account-id>' with your AWS region and account ID.

## 2a. Using the secret name prod/cart-service/credentials, derive a sensible ARN as the specific resource for access.

```
arn:aws:secretsmanager:<region>:<account-id>:secret:prod/cart-service/credentials-*
```
The wildcard ('-*') at the end ensures access to the secret and its versions, as AWS Secrets Manager appends a random suffix to secret ARNs.
