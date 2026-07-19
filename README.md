# SHOW registry

Signed **golden Execution Profiles (EPs)** for models verified against **SHOW**
(Secure Hosted Open Weight), and the **pinned steward root** clients verify against.
Stewarded by Ailemna. *SHOW, don't tell.*

## Trust model — the store is not a trust root
Every record self-verifies: the EP `payload` is signed by the steward key whose
public half is in [`pinned-root.json`](pinned-root.json). Clients **pin that root**
and check the signature **locally** — a compromised or lying mirror can withhold
or tamper, but a tampered record fails verification.

## Layout
- `pinned-root.json` — steward public key (ed25519). Pin this in your client.
- `models/<model_id>/<YYMMDD>.json` — a signed EP record `{ payload, signature, steward_key_id }`.
  Version is a **`YYMMDD`** date code (e.g. `260719`).

> MVP note: the steward key is an MVP dev key; production moves it offline / to an HSM
> and re-signs. The EP's `image_digest` pins the appliance image content; a node booting
> against it needs the matching bundle-assembler (in progress).
