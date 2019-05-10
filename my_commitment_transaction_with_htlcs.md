```
+------------------------------------------------+
| 2-of-2 multi-sig funding tx confirmed on-chain |
+------------------------------------------------+
   |
   |
   |  +----------------------------------------------------------------------------------------------------+
   \--| My version of the commitment transaction that I am holding off-chain in case I need to force close |
      +----------------------------------------------------------------------------------------------------+
       |  |  |  |
       |  |  |  |
       *  *  |  |   Output with your balance
       |  |  |  \--------------------------> You can spend it immediately upon me broadcasting this tx
       |  |  |         (P2WPKH)
       *  *  |
       |  |  |
       |  |  |
       *  *  |
       |  |  |
       |  |  |
       *  *  |
       |  |  |                             ,-> I can spend it one day after I broadcast this tx 
       |  |  |  Output with my balance    /         (CSV relative timelock, expected outcome)
       *  *  \---------------------------<
       |  |           (P2WSH)             \
       |  |                                `-> You can spend it if I broadcast this tx and you have the revocation key 
       *  *                                                       (punish breach outcome)
       |  |
       |  |
       *  *
       |  |
       |  |
       *  *
       |  |                                                             
       |  |                                                           
       *  *                     ,-- If the absolute timelock expires -> 2-of-2 multisig output for HTLC timeout transaction 
       |  | My payment to you  /         (CLTV, refund to me)                       (see below)
       |  \-------------------<                                         
       |  (P2WSH, HTLC output)|                                                   
       *                       \
       |                        `-- You can spend it if I broadcast this tx and you have the secret payment preimage 
       |                        |                 (expected outcome)
       |                        \
       *                         `- You can spend it if I broadcast this tx and you have the revocation key 
       |                                          (punish breach outcome)
       |
       *
       |
       |                                                  
       *                                                         
       |                        ,-- If I have the secret payment preimage -> 2-of-2 multisig output for HTLC success transaction 
       |  Your payment to me   /                                                        (see below)
       \----------------------<                                          
        (P2WSH, HTLC output)  |                                                             
                               \
                                `--> You can spend it if the absolute timelock expires
                                 |                        (refund outcome)
                                 \
                                  `--> You can spend it if I broadcast this tx and you have the revocation key 
                                                          (punish breach outcome)
                                                          
                                                          
      +------------------------------------------------------------------------------------------------------+
      | My version of the HTLC timeout transaction that I am holding off-chain in case I need to force close |
      +------------------------------------------------------------------------------------------------------+
            input: expired absolute timelock
               |
               |        ,-> I can spend it one day after I broadcast this tx 
               |       /        (CSV relative timelock, refund outcome)
               \------<
                       \ 
                        `-> You can spend it if I broadcast this tx and you have the revocation key 
                                  (punish breach outcome)
                                  
                                  
      +------------------------------------------------------------------------------------------------------+
      | My version of the HTLC success transaction that I am holding off-chain in case I need to force close |
      +------------------------------------------------------------------------------------------------------+
            input: secret preimage
               |
               |        ,-> I can spend it one day after I broadcast this tx 
               |       /        (CSV relative timelock, refund outcome)
               \------<
                       \ 
                        `-> You can spend it if I broadcast this tx and you have the revocation key 
                                  (punish breach outcome)
      
```