```
+------------------------------------------------+
| 2-of-2 multi-sig funding tx confirmed on-chain |
+------------------------------------------------+
      |
      |
      |       +----------------------------------------------------------------------+
      \------| my version of the commitment transaction that I am holding off-chain  |
              +----------------------------------------------------------------------+
                  |  |  |  |
                  |  |  |  |
                  *  *  |  |   output with your channel balance
                  |  |  |  \------------------------------------- you can spend it immediately upon me broadcasting this tx
                  |  |  |
                  *  *  |
                  |  |  |
                  |  |  |
                  *  *  |
                  |  |  |                                     ,-- I can spend it one day after I broadcast this tx (expected outcome)
                  |  |  |  output with my channel balance    /
                  *  *  \-----------------------------------<
                  |  |                                       \
                  |  |                                        `-- you can spend it if I broadcast this tx and I have given you the revocation key (punish breach outcome)
                  *  *
                  |  |
                  |  |
                  *  *
                  |  |                                                                  ,-- you can spend it one day after I broadcast this tx (refund payment)
                  |  |                                                                 /
                  *  *                     ,-- if the absolute timelock expires... ---<
                  |  | my payment to you /                  (refund to me)             \
                  |  \-------------------<                                              `-- you can spend it if I broadcast this tx and you have the revocation key (punish breach outcome)
                  *     (HTLC output)     \
                  |                        `-- you can spend it if I broadcast this tx and you have the secret payment preimage (expected outcome)
                  |                        \
                  *                         `-- you can spend it if I broadcast this tx and you have the revocation key (punish breach outcome)
                  |
                  |
                  *
                  |
                  |                                                                         ,-- I can spend it one day after broadcasting this tx (expected outcome)
                  *                                                                        /
                  |                        ,-- if I have the secret payment preimage ---<
                  |  your payment to me   /                                                \
                  \----------------------<                                                  `-- you can spend it if I broadcast this tx and you have the revocation key (punish breach outcome)
                       (HTLC output)      \
                                           `-- you can spend it if the absolute timelock expires (refund to you)
                                           \
                                            `-- you can spend it if I broadcast this tx and you have the revocation key (punish breach outcome)
```