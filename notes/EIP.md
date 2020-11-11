Elastic IP
---

- Used when you need a fixed ip address for instance
- You can only have 5 Elastic IP in your account (You can ask aws to increase that)
- Try to avoid using Elastic IP
  - They reflect poor architectural decisions
  - Instead, use a random public ip and register a DNS to it (more scalable than using Elastic IP)
  - Best way is to use a load balancer and not use public IP at all
