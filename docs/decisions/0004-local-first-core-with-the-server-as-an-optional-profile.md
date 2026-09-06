# 0004 — Local-first core, with a server as an optional profile

Status:    superseded by 0008
Date:      2026-09-05
Context:
           The maintainer operates nothing (0001), so the question is not
           whether there is a server but which parts genuinely need a process
           that is always on and reachable from the internet.

           Measured, not assumed: Whoop is webhook-only, Garmin and Oura
           notify by webhook. A phone cannot be the target of a webhook, so
           that ingest path requires a public endpoint.

           But Apple HealthKit, Google Health Connect and Samsung Health are
           on-device hubs, and the vendor apps for Oura, Whoop and Garmin
           write into them. The same reading from the same watch arrives
           with no server, no webhook and no developer portal registration.

           Requiring Docker as the only way in filters out every household
           without a technical member — the self-hosting community is still,
           by its own account, an enthusiast bubble.

Decision:  The core runs entirely on one device with no network. A server is
           an optional profile that adds only the adapters needing to be
           always on — vendor webhooks, unattended ingest, retention.

           Build order: one device offline, then sync through storage the
           family already pays for, then the optional server.

Consequences:
           Makes easy: installation by an ordinary household, offline use,
           and a privacy story that is true by construction rather than by
           policy.

           Makes hard: multi-device and multi-member sync, which becomes a
           design problem instead of a free consequence of having a server.
           Encrypted sync with merge is still an active research area.

           Forecloses: any core assumption of network, server or background
           process. Sync is an adapter like any other, not a privileged
           layer.

           Requires: sync is not built in v1. The first version is one
           device, and that version is finished, not reduced.

Rejected:  Docker server as the only entry point — natural for webhooks,
           and it loses the households this exists for.
           Pure local-first with no server ever — forecloses vendor webhook
           ingest permanently, which is a real capability for advanced users.
