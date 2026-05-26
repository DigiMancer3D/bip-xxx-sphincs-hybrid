# BIP-XXX Reference Implementation: Hybrid SPHINCS+ / secp256k1 Bitcoin Wallets

Reference code for the proposed **BIP-XXX: Hybrid SPHINCS+ / secp256k1 Key Derivation for Quantum-Resistant Bitcoin Wallets**.

This repository contains the exact three C programs that implement the full workflow described in the BIP.

## Quick Start

```bash
# Install dependencies (Ubuntu/Debian example)
sudo apt update
sudo apt install build-essential liboqs-dev libjansson-dev libssl-dev

# Compile all three tools
gcc -o pqc_keygen_new pqc_keygen_new.c -loqs -ljansson -lcrypto -lm
gcc -o pqc_sphincs_plus pqc_sphincs_plus.c -loqs -ljansson -lcrypto -lm
gcc -o pqc_hybrid_signer pqc_hybrid_signer.c -loqs -ljansson -lcrypto -lm
