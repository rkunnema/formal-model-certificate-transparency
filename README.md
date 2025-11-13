# Tamarin model for Certificate Transparency

## Files:

- `README.md` This file

### Model:

- `ct.spthy` model for CT and extensions
- `pki.spthy` model for PKI
- `acc_oracle` oracle used to guide proofs in those models

### Use with batch-tamarin

`batch-tamarin` (see below) needs the accountability lemmas to be translated
before running. These files are generated from `ct.spthy` and `pki.spthy` by
clicking "Download" in interactive mode after loading.

- `ct_lemmas_pregen.spthy`
- `pki_lemma_pregen.spthy`
- `ct_lemmas_pregen_receipt.spthy` (generated from `ct.sphy` with `--defines=RECEIPT` see below.)

### Results

- `proofs` We saved important proofs in case reproducibility environment should fail.
- `results` batch-tamarin generates this and puts results in HTML format here 

### Reproducibility:
- `flake.lock` for Nix environment
- `flake.nix` for Nix environment
- `tamarin-1.10-and-batch.Dockerfile` to produce docker image

## Usage:

Use `tamarin-prover --prove={lemmaname}` to prove most lemmas. This can take a while and you need some memory.

The models for revocation (in the appendix) or the addition of receipts to the
SCT auditing model are disable by default and can be activated with the
following flags to tamarin.

- `--defines=REVOCATION` for (simplified: perfect, without delay) revocation model 
- `--defines=RECEIPT` for realistic monitor blaming by combining domain owner and logger knowledge
- `--defines=SUFFICIENCY` to automate `exists-trace` proofs of the sufficiency component of accountability lemmas.

The configuration files for `batch-tamarin` (see Reproducibility, below)
already encode which flags and additional options (some lemmas need an oracle
to guide the proof) need to be set for which model file. We recommend using
batch-tamarin for convenience, otherwise the JSON files state clearly and
formally which combination of flags is to be used for which lemma.

## Running the model

1. Install Tamarin and its dependencies Haskell Stack, Maude and GraphViz:

    - Follow [Tamarin's Installation instructions](https://tamarin-prover.com/manual/master/book/002_installation.html),
        the explain the procedure for various operating systems.

    - Try the reproducible set up below if you have docker.

2. Tamarin's proofs are inherently sensitive to the version of Maude used, and
   its own version, of course. We used this precise version for testing. In case of trouble, try to build the same version from source.

```    
maude tool: 'maude'
checking version: 2.7.1. OK. checking installation: OK. 
Generated from: Tamarin version 1.10.0 Maude version 2.7.1 Git revision: UNKNOWN, branch: UNKNOWN Compiled at: 2024-10-30 14:56:23.355649243 UTC
```

3. Note that: 

    - Lemmas `A_RevokeGossip_1_monitor_blames_log_gossip_root_CA_single`
         and `A_RevokeGossip_1_monitor_blames_log_gossip_intm_CA_single` will FAIL,
        but they consitute other conditions for an accountability lemma that
has an attack (hence there is a provable counter-example against another trace
lemma generated from the same accountability lemma). Hence this lemma does not need to be proved.

    - Sufficiency lemmas from accountability needs `--defines=SUFFICIENCY_PROOF`, see above.

## Reproducibility

We used [batch-tamarin](https://github.com/tamarin-prover/batch-tamarin)
to produce our results. The batch job is defined in the JSON files that we
provide in [proofs](proofs/).

We use their nix flake

 https://github.com/tamarin-prover/batch-tamarin/blob/5f2ce46bbae799dbeabecb4da12951784b0519fc/examples/__dockerfiles__/with-batch-tamarin/tamarin-1.10-and-batch.Dockerfile

for the development environment, which we copied into this repository as `flake.nix`

To run the proofs in the paper:

1. Install nix (the package manager) using
    
    - the generic instructions https://nixos.org/download/#nix-install-linux
    - distribution-specific methods, e.g., for Debian https://packages.debian.org/sid/nix-bin
    - alternatively (but untested) from Docker by doing `docker-make
      tamarin-1.10-and-batch.Dockerfile` (also taken from the `tamarin-batch`
      repository) or basically following what this file does 

2. run `nix develop`. This should re-create a complete environment with
   tamarin, batch-tamarin, and their run-time dependencies. The first time, it
   will take a while, afterwards, the environment should be cached and nearly
   instantanous.

3. `cd proofs` 

4. `batch-tamarin run $FILE` for one of the JSON files in the `proofs` directory. In case individual lemmas unexpectedly fail, batch-tamarin will recommend re-running these.

