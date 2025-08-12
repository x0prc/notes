---
dg-publish: true
permalink:
---






## ==Hash Pointer is:==

- Pointer to where some information is stored and hash of the info.
    
    ### With a Hash Pointer, we can:
    
    - Ask to get the info back and verify it has not changed.

![Untitled.png](/img/user/img/Untitled.png)

## ==Building Blockchains with Hash Pointers==

- Tamper-Evident Log
    
    ![Screenshot_2023-07-09_at_11.43.22_PM.png](/img/user/img/Screenshot_2023-07-09_at_11.43.22_PM.png)
    
- Merkle Tree
    
    ![Screenshot_2023-07-09_at_11.45.52_PM.png](/img/user/img/Screenshot_2023-07-09_at_11.45.52_PM.png)
    
    - Verifying Hashes in Merkle Tree:
    
    ![Screenshot_2023-07-09_at_11.47.35_PM.png](/img/user/img/Screenshot_2023-07-09_at_11.47.35_PM.png)
    
    - Advantages of Merkle Trees:
        - Trees hold many items but just need to remember the root hash.
        - Can verify membership in O(logn) time/space
        - Variant: Sorted Merkle Tree (Can verify non-membership in O(logn)