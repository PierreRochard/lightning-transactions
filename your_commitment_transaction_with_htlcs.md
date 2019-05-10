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
       |  |  |
       *  *  |
       |  |  |
       |  |  |
       *  *  |
       |  |  |
       |  |  |
       *  *  |
       |  |  |                             ,-> You can spend it one day after you broadcast this tx 
       |  |  |  Output with your balance  /             (CSV relative timelock, expected outcome)
       *  *  \---------------------------<
       |  |                               \
       |  |                                `-> I can spend it if you broadcast this tx and I have the revocation key 
       *  *                                                      (punish breach outcome)
       |  |
       |  |
       *  *
       |  |
       |  |
       *  *
       |  |                                                               ,-> You can spend it one day after you broadcast this tx 
       |  |                                                              /            (CSV relative timelock, refund outcome)
       *  *                     ,-- If the absolute timelock expires ---<
       |  | Your payment to me /          (CLTV, refund to you)          \
       |  \-------------------<                                           `-> I can spend it if you broadcast this tx and I have the revocation key 
       |       (HTLC output)  |                                                              (punish breach outcome)
       *                       \
       |                        `-- I can spend it if you broadcast this tx and I have the secret payment preimage 
       |                        |                 (expected outcome)
       |                        \
       *                         `- I can spend it if you broadcast this tx and I have the revocation key 
       |                                          (punish breach outcome)
       |
       *
       |
       |                                                                       ,-> You can spend it one day after broadcasting this tx 
       *                                                                      /        (CSV relative timelock, expected outcome)
       |                        ,-- If you have the secret payment preimage -<
       |  My payment to you    /                                              \
       \----------------------<                                                `-> I can spend it if you broadcast this tx and I have the revocation key 
             (HTLC output)    |                                                                  (punish breach outcome)
                               \
                                `--> I can spend it if the CLTV absolute timelock expires 
                                 |                        (refund outcome)
                                 \
                                  `--> I can spend it if you broadcast this tx and I have the revocation key 
                                                          (punish breach outcome)
```