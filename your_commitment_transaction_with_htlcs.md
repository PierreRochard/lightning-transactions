```
+------------------------------------------------+
| 2-of-2 multi-sig funding tx confirmed on-chain |
+------------------------------------------------+
      |
      |
      |
      |
      |
      |
      |
      |       +---------------------------------------------------------------------------+
      \------| your version of the commitment transaction that you are holding off-chain  |
              +---------------------------------------------------------------------------+
                  |  |  |  |
                  |  |  |  |
                  *  *  |  |   output with my channel balance
                  |  |  |  \------------------------------------- I can spend it immediately upon you broadcasting this tx
                  |  |  |
                  *  *  |
                  |  |  |
                  |  |  |
                  *  *  |
                  |  |  |                                     ,-- you can spend it one day after you broadcast this tx
                  |  |  |  output with your channel balance  /
                  *  *  \-----------------------------------<
                  |  |                                       \
                  |  |                                        `-- I can spend it if you broadcast this tx and I have the revocation key (punishment!)
                  *  *
                  |  |
                  |  |
                  *  *
                  |  |                                                                  ,-- you can spend it one day after you broadcast this tx
                  |  |                                                                 /
                  *  *                     ,-- if the absolute timelock expires... ---<
                  |  | your payment to me /                  (refund to you)           \
                  |  \-------------------<                                              `-- I can spend it if you broadcast this tx and I have the revocation key (punishment!)
                  *     (HTLC output)     \
                  |                        `-- I can spend it if you broadcast this tx and I have the secret payment preimage
                  |                        \
                  *                         `- I can spend it if you broadcast this tx and I have the revocation key (punishment!)
                  |
                  |
                  *
                  |
                  |                                                                         ,-- you can spend it one day after broadcasting this tx
                  *                                                                        /
                  |                        ,-- if you have the secret payment preimage ---<
                  |  my payment to you    /                                                \
                  \----------------------<                                                  `-- I can spend it if you broadcast this tx and I have the revocation key (punishment!)
                       (HTLC output)      \
                                           `-- I can spend it if the absolute timelock expires (refund to me)
                                           \
                                            `- I can spend it if you broadcast this tx and I have the revocation key (punishment!)
```