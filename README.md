# ofac-sdn-mirror

Automated daily mirror of the **official OFAC SDN CSV** published by the U.S. Department of the
Treasury (`https://www.treasury.gov/ofac/downloads/sdn.csv` — public-domain US government data).

Why this exists: the sanctions-screening worker in [tasty-payment](https://github.com/mohammadJoorsara/tasty-payment)
cannot TLS-reach `sanctionslistservice.ofac.treas.gov` from Cloudflare Workers egress (HTTP 525,
verified 2026-11-20 with per-hop logging). GitHub-hosted runners can. A GitHub Action downloads the
official file at 00:10 UTC daily and commits it here **byte-for-byte, unchanged**; the worker reads
`raw.githubusercontent.com/mohammadJoorsara/ofac-sdn-mirror/main/sdn.csv` as its fallback source
(the live treasury.gov chain is always tried first).

The file is never modified by this repo. Integrity is enforced by the worker's parser (it rejects
a file with zero parseable "Digital Currency Address" entries) and by the commit history here.
