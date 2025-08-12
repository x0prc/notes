---
dg-publish: true
permalink:
---






- If a layer receives a chunk of data too large for it, it _==fragments==_ that data into pieces that it can manage.
    - When the data reaches the destination, the ==**destination system reassembles those fragments into a complete unit.**==
    - Fragmentation increases **==load on both the server and the client.==**
- Most systems set a _==maximum transmission unit (MTU)==_, the largest size that can fit through the datalink layer.
    - The **==upper layers of the stack respect this MTU==**, eliminating obvious problems.
    - Older Ethernet has an MTU of 1500 bytes. Some 100Mbs Ethernet, and all gigabit and faster Ethernet, support 9000-byte “jumbo” frames.