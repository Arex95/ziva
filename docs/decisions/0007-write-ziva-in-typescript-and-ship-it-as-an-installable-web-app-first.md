# 0007 — Write ZIVA in TypeScript and ship it as an installable web app first

Status:    accepted
Date:      2026-09-05
Context:
           The four inputs that decide a language here:

           WHO RUNS IT, ON WHAT. A household's own devices — phones,
           laptops — and optionally a small machine for the server profile
           (0004). There is no server class to design for.

           HOW COMPLEX THE DOMAIN IS. It is not. An append-only event log
           (0005), a household of subjects (0003), medication schedules, and
           retrieval over documents (0006). The hard parts are ingest and
           sync, neither of which a language solves.

           HOW LONG IT LIVES AND WHO MAINTAINS IT. Years, one person,
           possibly abandoned (0001). This is the input that decides. A
           second ecosystem is carried forever by a team that is not
           growing: another toolchain, another vulnerability feed to read,
           another set of architecture rules, another support calendar.

           WHAT IS A STATED REQUIREMENT. It must be able to be an
           application on a family's device, not only a server. That single
           requirement removes most of the usual candidates.

           One further constraint discovered rather than assumed: Apple's
           App Store terms impose copy restrictions that the GPL family
           forbids as additional restrictions — the reason VLC was pulled in
           2011. Any plan that depends on the App Store collides with 0002.

Decision:  TypeScript, one language for the client, the optional server and
           the shared domain. pnpm, with the runtime version pinned in
           package.json and read from there by everything else.

           Shipped first as an installable offline web application, storing
           data in SQLite compiled to WebAssembly on the device. No app
           store, so the licence conflict never arises.

           A native shell is added only when on-device wearable hubs
           (HealthKit, Health Connect) are actually needed — which is the
           third step of 0004's build order, not the first. The same
           TypeScript core is wrapped; it is not a rewrite.

Consequences:
           Makes easy: one ecosystem, so the maintenance surface a single
           person carries is halved. Types shared between the client and the
           optional server remove the contract drift that a thin server
           otherwise produces. Distribution is a URL or a folder of static
           files — no store, no signing, no review, no gatekeeper who can
           remove it. That last point is 0001's whole argument, applied to
           distribution.

           Makes hard: the dependency surface is the largest of any option,
           which for a health record is a supply-chain concern rather than a
           convenience one. pnpm's hold on newly published versions is
           mitigation, not a solution. Dependencies are added reluctantly
           and reviewed.

           Also hard: no access to on-device health hubs until the native
           shell exists. Accepted, because wearables are step three and
           documents are step one.

           Requires verification before the record is trusted to browser
           storage: iOS evicts script-writable storage under conditions that
           differ between an installed and a merely visited application.
           Silent data loss is unacceptable for a health record. The
           mitigation is already decided — the exported files are the source
           of truth (0005), not the browser's database — but the eviction
           behaviour must be measured on a real device before the first
           real record is entered.

Rejected:  Java or Kotlin with Spring, the studio default — the largest
           library surface and the best boundary enforcement available, and
           it cannot be the application on a family's phone. The requirement
           decides against it.

           Flutter or Dart — the best native mobile result of the options,
           and it makes the server a second ecosystem or a marginal one.
           Reconsider only if the native shell turns out to be needed from
           the start rather than at step three.

           Go — one static binary, excellent for the server profile, and
           there is no good story for the client. Fasten chose Go and ended
           up a server nobody could install.

           Rust — buys memory safety without a garbage collector, which is
           an advantage this project cannot spend, at a cost in months to
           competence that it cannot afford.

           React Native or Expo as the starting point — the same language
           and a legitimate alternative, and it puts a store in the
           distribution path from day one, which collides with 0002 before
           any of it is necessary.

           What would make this wrong: measuring that browser-resident
           SQLite cannot hold the document volume a household produces, or
           that storage eviction on iOS is not avoidable for an installed
           application. Either would move the decision to Flutter.
