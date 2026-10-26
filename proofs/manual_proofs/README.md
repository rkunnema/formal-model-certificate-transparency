The provided manual proofs can be checked using Tamarin by running these commands inside the evaluation environment in this folder:

- For sufficiency lemmas:

`tamarin-prover manual_proofs_check.spthy --defines=SUFFICIENCY_PROOF`

- For the provided helper lemmas:

`tamarin-prover manual_proofs_check.spthy`

`manual_proofs_check.spthy` contains the ct_gossip model where the manual proofs are provided to the respective lemmas. Invoking tamarin on this file will check these proofs against the model again.
The output produced by Tamarin contains in particular these rows:

```
  A_Gossip_0_rootCA_rogue_gossip_suff (exists-trace): verified (68 steps)
  A_Gossip_0_rootCA_benign_gossip_suff (exists-trace): verified (70 steps)
  A_Gossip_0_rootCA_rogue_gossip_single (exists-trace): verified (76 steps)
  A_Gossip_0_rootCA_benign_gossip_single (exists-trace): verified (70 steps)
  A_Gossip_1_rootCA_rogue_gossip_mon_honest_suff (exists-trace): verified (68 steps)
  A_Gossip_1_rootCA_benign_gossip_mon_honest_suff (exists-trace): verified (70 steps)
  A_Gossip_1_rootCA_rogue_gossip_mon_honest_single (exists-trace): verified (76 steps)
  A_Gossip_1_rootCA_benign_gossip_mon_honest_single (exists-trace): verified (70 steps)
  A_Gossip_2_rootCA_rogue_gossip_log_honest_suff (exists-trace): verified (74 steps)
  A_Gossip_2_rootCA_benign_gossip_log_honest_suff (exists-trace): verified (76 steps)
  A_Gossip_2_rootCA_rogue_gossip_log_honest_single (exists-trace): verified (82 steps)
  A_Gossip_2_rootCA_benign_gossip_log_honest_single (exists-trace): verified (76 steps)
```

for the sufficiency variant and:

```
  A_Gossip_helper (all-traces): verified (147 steps)
  T_Gossip_verif_empty_helper1 (all-traces): verified (64 steps)
  T_Gossip_verif_empty_helper2 (all-traces): verified (67 steps)
```


for the helper lemmas.