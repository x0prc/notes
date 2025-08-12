---
dg-publish: true
permalink:
---






## ==6 Basic Steps==

1. Join the network, listen for transactions
2. Listen for new blocks, maintain block chain
3. Assemble a new valid block
4. Find the nonce to make your block valid
5. Hope everybody accepts new block
6. Profit!

  

> [!important] The target hash has become so small that
> 
> the block header nonce alone isn’t generally large enough to allow miners to  
> search enough of the hash output space to find a valid block  

  

![Screenshot_2023-07-13_at_7.33.29_PM.png](/img/user/img/Screenshot_2023-07-13_at_7.33.29_PM.png)

## ==Setting the mining difficulty==

- Every two weeks compute:
    
    ```Python
    next_difficulty = previous_difficulty * (2 weeks)/(time to mine last 2016 blocks)
    ```
    
- Current Difficulty Estimate : ==**50.7 T at 10.6 minutes avg**==
- It depends on the activity in the market. How many new miners are getting into the game, which may be affected by the current exchange rate of Bitcoin.

## ==CPU Mining==

```Java
while (1) {
		HDR[kNoncePos]++;
IF (SHA256(SHA256(HDR)) < (65535 << 208)/  DIFFICULTY)
		return;
}
```

- Throughput on a high end PC = 10-20 MHz/Hash

## ==GPU Mining==

- Implemented in OpenCL
- Easily available, easy to set up
- Work in SLI for 1 CPU comfort
- Current rate = 173 with 100 cards to hash

> goodput = throughput x success rate

## ==ASIC Mining (Application Specific Integrated Circuit)==

- Built specifically to mine coins.
- A $6,000 machine ships about 2TH/s of compute power but still takes 14 months on average to find a block!
    
    ### ==Market Dynamics==
    
    - Most boards obsolete within 3-6 months
    - Half of profits made in first 6 weeks!
    - Shipping delays are devastating to customers
    - Most companies require pre-orders
    - Most individual customers lose interest/competition

## ==Estimating Energy Usage==

- Each block worth approximately $15,000
- Approx $25/s generated
- Industrial Electricity : $0.03/MJ
- **==Upper bound on electricity consumed : 900MJ/s = 900MW==**