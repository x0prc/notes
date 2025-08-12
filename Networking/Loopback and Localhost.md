---
dg-publish: true
permalink:
---






- Loopback interface is a **==logical interface, with no hardware representation.==**
    - It can only be accessed from the local machine, **==and can only be used to connect to the local machine.==**
- Every loopback interface gets the IPv4 address 127.0.0.1/8, **==the localhost address.==**
- When a program wants to connect to something running on the local machine, **==it connects to the localhost address.==**
- Configuring a piece of software to connect to 127.0.0.1 is a sure way to make **==absolutely certain it connects to the local machine.==**