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
       |  |  |
       *  *  |
       |  |  |
       |  |  |
       *  *  |
       |  |  |                             ,-> I can spend it one day after I broadcast this tx 
       |  |  |  Output with my balance    /                       (expected outcome)
       *  *  \---------------------------<
       |  |                               \
       |  |                                `-> You can spend it if I broadcast this tx and you have the revocation key 
       *  *                                                       (punish breach outcome)
       |  |
       |  |
       *  *
       |  |                                                               ,-> I can spend it one day after I broadcast this tx 
       |  |                                                              /                   (refund outcome)
       *  *                     ,-- If the absolute timelock expires ---<
       |  | My payment to you  /                                         \
       |  \-------------------<                                           `-> You can spend it if I broadcast this tx and you have the revocation key 
       |       (HTLC output)  |                                                              (punish breach outcome)
       *                       \
       |                        `-- You can spend it if I broadcast this tx and you have the secret payment preimage 
       |                        |                 (expected outcome)
       |                        \
       *                         `- You can spend it if I broadcast this tx and you have the revocation key 
       |                                          (punish breach outcome)
       |
       *
       |
       |                                                                     ,-> I can spend it one day after broadcasting this tx 
       *                                                                    /                      (expected outcome)
       |                        ,-- If I have the secret payment preimage -<
       |  Your payment to me   /                                            \
       \----------------------<                                              `-> You can spend it if I broadcast this tx and you have the revocation key 
             (HTLC output)    |                                                                    (punish breach outcome)
                               \
                                `--> You can spend it if the absolute timelock expires (refund outcome)
                                 |
                                 \
                                  `--> You can spend it if I broadcast this tx and you have the revocation key 
                                                          (punish breach outcome)
```