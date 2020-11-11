Global service that allows to manage multiple AWS accounts in your organization
- The main account is called master account and it cant be changed
- Other accounts are called member accounts. One member account can be part of only one organization
- One member account can be moved from one master account to another (migration)
- Pros:
  - Consolidated billing. One payment method for all accounts
  - Pricing benefits (discounts) for aggregated usage
  
## Multi Account Strategies
Create multiple accounts per department, per cost center, per dev/test/prod, for better resource isolation (VPC), isolated logging etc.

### Multi Accounts VS One Account Multi VPC
In multi accounts, users are spearated. In one account with multi vpc, users might get access to multiple VPCs or reosurces might talk to one and another


### Organizational Units (OU)
Master Account
- Sales OU
  - Sales Acc 1
  - Sales Acc 2
- Retail OU
  - Retail Acc 1
  - Retail Acc 2
- Finance OU
  - Finance Acc 1
  - Finance Acc 2
  
OR

Master Account
- Production OU
  - Production Acc 1
  - Production Acc 2
- Development OU
  - Development Acc 1
  - Development Acc 2
- Test OU
  - Test Acc 1
  - Test Acc 2
  
 OR
 
 Master Account
- Project1 OU
  - Project1 Acc 1
  - Project1 Acc 2
- Project2 OU
  - Project2 Acc 1
  - Project2 Acc 2
- Project3 OU
  - Project3 Acc 1
  - Project3 Acc 2
  
  
### Service Control Policies (SCP)
SCP at accoubt level is overwritten by SCP at OU level
  
