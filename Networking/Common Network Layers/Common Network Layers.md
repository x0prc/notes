---
dg-publish: true
permalink:
---






- To understand modern Internet-attach network we need five layers :
    
    ## ==**Physical**==
    
    1. Networks must travel over something. If you can trip over it, snag it, it’s the physical layer.
    2. ==**The physical layer is commonly referred to the wire**==, although it can be radio waves or coaxial cable or any number of things.
    
    ## ==**Datalink**==
    
    1. The datalink layer transforms the network’s upper layers into the ==**signals transmitted over the wire.**==
    2. A single lump of datalink data is called a _==frame==_.
    
    ## ==**Network**==
    
    1. The network layer provides a consistent interface to network programs, so they can **==use the network over any physical and datalink layers.==**
    2. A single chunk of network data is called a _==packet==_.
    
    ## ==**Transport**==
    
    1. The lower layers of the stack exist to **==support the transport layer.==** A piece of transport layer data is a _==segment==_.
    
    ### ==Internet Control Message Protocol (ICMP)==
    
    - Handles low-level connectivity messages between hosts.
    - It is where hosts respond to ping requests and tell traffic to go around the other way.
    
    ### ==Transmission Control Protocol (TCP)==
    
    - Carry data between hosts.
    - Both are so common that the suits of IPs is usually called TCP/IP.
    - TCP segments are 536 bytes or smaller.
    
    ### ==User Datagram Protocol (UDP)==
    
    - Offers the minimal services needed to transmit data over the network.
    - Most applications speak either TCP or UDP. Some use both (TCP & UDP).
    
    ## ==Session, Presentation and Application==
    
    - ==**Session layer**== handles opening, using, and closing transport layer connections.
    - **==Presentation layer==** lets programs exchange data with one another.
    - **==Application layer==** is the actual protocol spoken over these connections.
    
      
    
    ![Screenshot_2023-08-18_at_7.35.15_PM.png](/img/user/img/Screenshot_2023-08-18_at_7.35.15_PM.png)