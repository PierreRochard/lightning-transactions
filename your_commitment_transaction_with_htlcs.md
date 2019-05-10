```
+------------------------------------------------+
| 2-of-2 multi-sig funding tx confirmed on-chain |
+------------------------------------------------+
   |
   |
   |  +-----------------------------------------------------------------------------------------------------------+
   \--| Your version of the commitment transaction that you are holding off-chain in case you need to force close |
      +-----------------------------------------------------------------------------------------------------------+
       |  |  |  |
       |  |  |  |
       *  *  |  |   Output with my balance
       |  |  |  \--------------------------> I can spend it immediately upon you broadcasting this tx
       |  |  |           (P2WPKH)
       *  *  |
       |  |  |
       |  |  |
       *  *  |
       |  |  |                             ,-> You can spend it one day after you broadcast this tx 
       |  |  |  Output with your balance  /             (CSV relative timelock, expected outcome)
       *  *  \---------------------------<
       |  |             (P2WSH)           \
       |  |                                `-> I can spend it if you broadcast this tx and I have the revocation key 
       *  *                                                      (punish breach outcome)
       |  |
       |  |
       *  *
       |  |                                                        
       |  |                                                                       
       *  *                     ,-- If the absolute timelock expires -> 2-of-2 multisig output for HTLC timeout tx 
       |  | Your payment to me /          (CLTV, refund to you)                     (see below)
       |  \-------------------<                                          
       |  (P2WSH, HTLC output)|                                                             
       *                       \
       |                        `-- I can spend it if you broadcast this tx and I have the secret payment preimage 
       |                        |                 (expected outcome)
       |                        \
       *                         `- I can spend it if you broadcast this tx and I have the revocation key 
       |                                          (punish breach outcome)
       |
       *                                                               
       |                        ,-- If you have the secret payment preimage -> 2-of-2 multisig output for HTLC success tx 
       |  My payment to you    /                                                        (see below)
       \----------------------<                                               
        (P2WSH, HTLC output)  |                                                                 
                               \
                                `--> I can spend it if the CLTV absolute timelock expires 
                                 |                        (refund outcome)
                                 \
                                  `--> I can spend it if you broadcast this tx and I have the revocation key 
                                                          (punish breach outcome)

    
    
      +-------------------------------------------------------------------------------------------------------------+
      | Your version of the HTLC timeout transaction that you are holding off-chain in case you need to force close |
      +-------------------------------------------------------------------------------------------------------------+
            input: expired absolute timelock
               |
               |        ,-> You can spend it one day after you broadcast this tx 
               |       /        (CSV relative timelock, refund outcome)
               \------<
                       \ 
                        `-> I can spend it if you broadcast this tx and I have the revocation key 
                                  (punish breach outcome)
                                  
                                  
      +-------------------------------------------------------------------------------------------------------------+
      | Your version of the HTLC success transaction that you are holding off-chain in case you need to force close |
      +-------------------------------------------------------------------------------------------------------------+
            input: secret preimage
               |
               |        ,-> You can spend it one day after you broadcast this tx 
               |       /        (CSV relative timelock, refund outcome)
               \------<
                       \ 
                        `-> I can spend it if you broadcast this tx and I have the revocation key 
                                  (punish breach outcome)
      
      
      
```