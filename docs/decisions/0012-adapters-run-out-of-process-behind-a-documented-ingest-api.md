# 0012 — Adapters run out of process, behind a documented ingest API

Status:    accepted
Date:      2026-09-09
Context:
           0001 put integrations with hospital systems and wearable vendors
           outside the critical path, as extension points. What was never
           settled is where the process boundary sits, and it decides two
           unrelated things at once.

           The licensing half: an adapter linked into the server is likely a
           derivative work, so every third-party adapter would have to be
           AGPL. An adapter running as its own program, talking over HTTP,
           likely is not, so a hospital or a vendor could write a closed one.
           Maximum copyleft against maximum reach, and the choice cannot be
           reversed later without breaking everyone who already wrote one.

           The technical half was settled for us by 0009. Go has no viable
           in-process plugin story: the plugin package is Linux-only and
           requires the plugin and host to be built with an identical
           toolchain and dependency set, which is why it is avoided in
           practice. In Go the real options are compiling adapters into the
           binary — which means a fork and a rebuild per adapter — or
           running them outside it.

Decision:  Adapters are separate programs. The server exposes a documented
           ingest API and accepts events from anything that can speak it.
           Nothing is linked in.

           An adapter is therefore not part of ZIVA. It is a program that
           talks to ZIVA, in whatever language its author wants.

Consequences:
           Makes easy: reach, which is the point. Somebody with access to a
           hospital system can write an adapter without opening their code
           or asking permission, and without ZIVA carrying the maintenance
           of a catalogue — the catalogue being the thing that killed
           Fasten.

           Also easy: adapters in the language that suits the format. Some
           medical formats have decent libraries in Python and none in Go,
           and this makes that somebody else's choice rather than a
           constraint on the server.

           And: an adapter that crashes, hangs or leaks does not take the
           record down with it.

           Gives up: copyleft over the adapter layer. Third-party adapters
           may be closed, and over time that is where a lot of other
           people's work would have accumulated. This is deliberate — 0001
           says the value ZIVA offers is that it cannot be taken away, and
           nothing about a closed adapter takes the record away.

           Obliges: the ingest API is a contract from the first version.
           Once someone has written an adapter, breaking it is breaking
           their work, and there is no way to reach them to tell them. It
           gets the versioning discipline the handbook asks of any HTTP
           surface, and events carry the origin and external identifier
           0005 already requires, because two adapters will deliver the same
           reading.

Rejected:  In-process plugins — not viable in Go, and it would put a third
           party's code inside the process that holds the record.
           Compiling adapters into the server — forces a fork per adapter,
           so nobody outside writes one, and the extension point exists on
           paper only.
           Keeping the boundary undecided until an adapter exists — the
           first adapter written sets the answer by accident, and the answer
           it sets is the one that cannot be reversed.
