# Tamarin model for Certificate Transparency

## Usage:

Use `tamarin-prover --prove` to prove most lemmas. This can take a while and you need some memory.

The models for revocation (in the appendix) or the addition of receipts to the
SCT auditing model are disable by default and can be activated with the
following flags to tamarin.

    - `--defines=REVOCATION` for (simplified: perfect, without delay) revocation model 
    - `--defines=RECEIPT` for realistic monitor blaming by combining domain owner and logger knowledge

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

4. `batch-tamarin run $FILE` for one of the JSON files in the `proofs` directory.


