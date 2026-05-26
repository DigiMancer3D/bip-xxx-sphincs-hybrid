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
```

## Workflow

1. `./pqc_keygen_new` → creates `pqc_master_YYYYMMDD_HHMMSS.kchain` (master keychain)
2. `./pqc_sphincs_plus <kchain_file> <role_number>` → generates `.sphincs++` file with real Bitcoin keys + Taproot address
3. `./pqc_hybrid_signer <kchain_file> <role_number> "Your message here"` → creates hybrid signature (`.msg`)

All generated files are placed in `../svc-wallet/`.

## Offline Formatting

Use the included `bitaddress.org.html` (open locally in browser) to turn the raw private key from the `.sphincs++` file into a proper WIF and legacy address.

## Files

- `pqc_keygen_new.c` – Master keychain generator (3’s Company HE-SD + PQC keys)
- `pqc_sphincs_plus.c` – SPHINCS++ hybrid derivation + Taproot address
- `pqc_hybrid_signer.c` – Hybrid ECDSA + SPHINCS+ signing
- `bitaddress.org.html` – Offline address/WIF formatter (original from bitaddress.org)

## License

BSD-3-Clause (same as the BIP).

See the full BIP text in the `bip-xxx.mediawiki` file (or in the bitcoin/bips PR once submitted).

---
