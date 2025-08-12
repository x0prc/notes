---
dg-publish: true
permalink:
---






## ==Current Consensus Fees==

No fee if

- tx less than 1000 bytes in size
- all outputs are 0.01 BTC or larger, and
- priority is large enough

- **==Priority = (sum of inputAge*inputValue) / (trans size)==**

> Otherwise fee is 0.0001 BTC per 1000 bytes

## ==Transaction-Demand Model==

T = total transaction value mediated via BTC ($/sec)

D = duration that BTC is needed by a transaction (sec)

S = supply of BTC (not including BTC as long-term investments)

- **==S/D = BTC become available/second==**
- **==T/P = BTC needed/second==**