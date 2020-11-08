Hardware Security Module
---
KMS vs CloudHSM
- KMS => AWS manages the software for encryption
- CloudHSM => AWS provisions encryption hardware and user manages the rest


HSM devices are tamper proof
CloudHSM clusters are spread accross multi AZ
supports both symmetric and asymmetric encryption
good option to use with SSE-C encryption
aws cannot recover your keys if user looses the keys
