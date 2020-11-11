# Web Identity Federation
Web identity Federation lets you give your users access to aws resources after they have successfully authenticated with a web-based identity provider like Amazon, Facebook, Google. Following successful authentication, the user receives an authentication code from the web ID provider, which they can trade for temporary security credentials.

Amazon Cognito provides Web identity federation with the following features.
- Sign-in and Sign-up to your apps
- Access for guest users
- Acts as an identity broker between your app and web ID providers, so you don't need to write any additional code.
- Sync user data for multiple devices
- Recommended for all mobile applications AWS services


User Pools
---
User pool is user based. It handles things like user registration, authentication and account recovery

Identity Pools
---
Identity pools authorize access to your aws resources


- A user logs in using fb account
- FB authenthicates credentials and passes authentication token to cognito (user pool)
- Cognito turns authentication token to JWT
- User sends that JWT to cognito (Identity Pool)
- Identity Pool grants an IAM role and user can access AWS using that IAM role


Cognito Synchronization
---
Cognito tracks Association between user identity and the various different devices they signin from. In order to provide a seamless User experience for your application, cognito uses Push synchronisation to push updates and synchronise user data across multiple devices. Cognito uses SNS to send a notification to all the devices associated with a given user identity whenever data is stored in the cloud changes
