# 0008 — Require a self-hosted server as the household's record

Status:    accepted, supersedes 0004
Date:      2026-09-06
Context:
           0004 made the server optional and put a local-first core at the
           centre, on the reading that "the maintainer operates nothing"
           meant "there is no server". Those are different statements. A
           server the household runs on its own VPS or homelab operates
           nothing on the maintainer's side and is still a server.

           Removing it cost more than it saved. Without a shared record,
           two devices in two homes must reconcile copies, which drags in
           a sync engine, conflict handling and key distribution across
           members. With one, all of that disappears: there is a single
           truth and nothing to merge.

           The alternative examined was syncing through storage the family
           already owns, with the household head's Drive as the substrate.
           It works, and it fails on dependency: Google shut down the
           Google Fit APIs and Fitbit's Web API is being switched off this
           month. A record meant to last fifty years cannot rest on another
           company's API terms — that is the CareZone failure with a
           different logo. Google Drive also cannot receive vendor webhooks,
           its shared folders are visible and deletable by any member, and
           iCloud is per-Apple-ID, so a household with one Android member
           cannot use it at all.

           The audience this narrows to — people who will run a service on
           their own hardware — is Nightscout's audience, and it is 39,000
           households.

Decision:  ZIVA requires a server, deployed by the household on
           infrastructure it controls. That server holds the record and is
           the single source of truth. Clients are clients.

           The maintainer runs one for his own family and operates no other.

Consequences:
           Makes easy: authorisation with real per-subject permissions
           rather than "whoever can read the folder sees everything";
           vendor webhooks, which need a public endpoint; and the removal
           of the entire synchronisation problem.

           Makes hard: reach. This excludes households with no technical
           member, and that is accepted — for the case that motivated the
           project, the maintainer installs it and his parents open a link.

           The risk it introduces: a server is a thing that can stop being
           paid for, and a health record that dies with a lapsed VPS is the
           failure this project exists to prevent. This is already covered
           rather than newly accepted: 0005 requires complete export from
           the first release, so the server may die and the record does not.

           Obliges: accounts, sessions, permissions, migrations, backups,
           TLS and updates now exist and are the maintainer's work. Known
           work, not research.

Rejected:  Local-first with no server (0004) — the reading it rested on was
           wrong, and it forecloses webhook ingest permanently.
           Sync through the family's own cloud storage — depends on a third
           party's API for the substrate of the record, cannot receive
           webhooks, and iCloud excludes mixed households.
           A hosted instance operated by the maintainer — rejected in 0001
           and unchanged.
