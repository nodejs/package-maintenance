# Baseline practice: use 2FA when publishing

## Potential solutions

### Release manager

- Cons: 
    - complexity
    - compatibility
    - effort to build
    - maintenance

### Remote OTP

#### Approval via mobile 

POC: https://github.com/nearform/optic

- Cons: 
    - dependency on Firebase
    - needs a server

#### Entry via chatbot
 
POC: ask https://twitter.com/MarshallOfSound

- Cons: 
    - dependency on Slack
    - needs a server
    - needs the OTP to actually be typed out

#### SaaS

- Cons: 
    - none publicly available and free
    - trust

### Use remote decryption service

- Cons: 
    - requires setup

### Use GitHub releases / alternative registries for staging

Cons: 
    - requires setup
    - requires a manual action
