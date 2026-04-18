---
name: User affiliation — Czech biotech
description: User is a data scientist at a Czech biotech; affects data-license reasoning
type: user
originSessionId: a304eb01-cfde-4c39-9d2b-1e9a6c019e34
---
Florian works as a data scientist at a Czech biotech (SOTIO — there's an `sotio` git remote on the Kraken repo at `git@ssh.dev.azure.com:v3/SOTIO-CZ-IT/Kraken%20application`). Drug development / immunotherapy context.

**Why this matters for future conversations:**

- **Data-use agreements (DUAs) need commercial-use scrutiny.** Many open-access bioinformatics datasets (OpenPedCan, CBTN, Treehouse, Xena compendia) publish under terms that are fine for academic research but more nuanced for commercial R&D. When recommending a data source, proactively flag the DUA/license question rather than assuming academic use.
- **GDPR/EU data-transfer considerations** may apply for any patient-identifying fields. Processed-level public datasets are typically anonymized (pseudonym IDs like `BS_XXXXXXXX`), so this is usually a non-issue but worth noting.
- **dbGaP access** is harder for non-US biotech affiliations. Prefer open-access pathways when feasible.

**How to apply:** When recommending data sources or generation tools, briefly note the license/DUA angle so the user can forward it to legal/compliance if needed. Don't over-lawyer — one sentence flagging the question is usually enough. Don't assume the user can use any dataset without checking.
