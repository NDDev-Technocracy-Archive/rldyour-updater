# Catalogue signing keys

Naming note: `nddev-*` is the NDS-system key family — it replaces the
legacy rldyour-* naming as the estate moves to the new repository stack.

Devices pin exactly ONE trust anchor: `catalog/public-key.hex` (raw 32-byte
Ed25519 public key, hex). Rotation executed in the seq-3 publish commit:
`public-key.hex` now contains the nddev key.

| Key | Role | Status |
|---|---|---|
| (`277e85b3…b1dc`) | seq-1..seq-2 signer | retired at seq-3 |
| `catalog/public-key.hex` (`c5dcc81a…d1eb`) | seq-3..seq-8 signer | active anchor |

- Private half: `~/.config/rldyour-updater/keys/nddev-catalogue-signing-ed25519.pem`
  on the owner's signing host, mode 600. Never committed.
- `.hex` file = the exact string devices put into
  `rldyour-updater/config.toml` `[release].public_key`.
- `.pub` file = PKCS#8 PEM form of the same key.
- The same key is registered on GitHub account `rldyourmnd` as an SSH
  signing key titled `nddev-catalogue-signing`, so `git log --show-signature`
  can verify catalogue-related commits if the owner signs them.

## Rotation contract

1. Build the next payload (`rldyour-updater catalog-build --bootstrap <commit> --sequence <n>`).
2. Sign: `rldyour-updater catalog-sign --payload seq-<n>.json --private-key <pem>`.
3. Publish `stable.json` + update `catalog/public-key.hex` to the new hex in
   one commit — devices never see an unsigned gap.
4. Devices rotate `config.toml` `public_key` to the new hex on next run.
