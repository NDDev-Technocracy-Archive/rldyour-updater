# Catalogue signing keys

Devices pin exactly ONE trust anchor: `catalog/public-key.hex` (raw 32-byte
Ed25519 public key, hex). The key listed here is the next anchor — it becomes
`public-key.hex` in the same commit that publishes `catalog/stable.json`
sequence 3 signed by the matching private key.

| Key | Role | Status |
|---|---|---|
| `catalog/public-key.hex` (`277e85b3…b1dc`) | seq-1..seq-2 signer | active anchor |
| `keys/rldyour-catalogue-signing-ed25519` (`c5dcc81a…d1eb`) | seq-3+ signer | staged, rotates in on seq-3 |

- Private half: `~/.config/rldyour-updater/keys/rldyour-catalogue-signing-ed25519.pem`
  on the owner's signing host (ubuntu-desktop-spb), mode 600. Never committed.
- `.hex` file = the exact string devices put into
  `rldyour-updater/config.toml` `[release].public_key`.
- `.pub` file = PKCS#8 PEM form of the same key.
- The same key is registered on GitHub account `rldyourmnd` as an SSH
  signing key titled `rldyour-catalogue-signing`, so `git log --show-signature`
  can verify catalogue-related commits if the owner signs them.

## Rotation contract

1. Build seq-3 payload (`rldyour-updater catalog-build --bootstrap <commit>`).
2. Sign: `rldyour-updater catalog-sign --payload seq-3.json --private-key <pem>`.
3. Publish `stable.json` + update `catalog/public-key.hex` to the new hex in
   one commit — devices never see an unsigned gap.
4. Devices rotate `config.toml` `public_key` to the new hex on next run.
