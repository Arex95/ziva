# Architecture decisions

One file per decision that constrains work beyond the task that produced it.
Numbered and immutable: a decision that changes is not edited, a new one
supersedes it and the old one is marked. The history is the point.

| # | Decision |
|---|---|
| [0001](./0001-build-for-one-household-and-publish-rather-than-operate-a-service.md) | Build for one household and publish it, rather than operate a service |
| [0002](./0002-license-under-agpl-3-0-with-a-contributor-licence-agreement.md) | Licence under AGPL-3.0 with a contributor licence agreement |
| [0003](./0003-model-a-subject-rather-than-a-patient.md) | Model a Subject rather than a Patient, and treat FHIR as vocabulary |
| [0004](./0004-local-first-core-with-the-server-as-an-optional-profile.md) | Local-first core, with a server as an optional profile |
| [0005](./0005-store-an-append-only-event-log-with-client-generated-identifiers.md) | Store an append-only event log with client-generated identifiers |
| [0006](./0006-the-chat-retrieves-from-the-record-and-does-not-advise.md) | The chat retrieves from the record and does not advise |
| [0007](./0007-write-ziva-in-typescript-and-ship-it-as-an-installable-web-app-first.md) | Write ZIVA in TypeScript and ship it as an installable web app first |

The research these rest on is not in this repository. It lives with the
maintainer's own analysis notes, and each decision restates the evidence it
depends on so that this folder stands alone.
