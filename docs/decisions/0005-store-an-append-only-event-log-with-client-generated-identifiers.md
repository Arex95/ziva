# 0005 — Store an append-only event log with client-generated identifiers

Status:    accepted
Date:      2026-09-05
Context:
           Roughly 95% of ZIVA's volume is immutable: a blood pressure
           reading, a lab result, a dose taken, an uploaded report, a meal.
           These are events with an instant, and they are never edited. Only
           a small mutable surface exists — a subject's name, a medication
           schedule, an allergy.

           A set of immutable events with client-generated identifiers is
           the easiest possible case for synchronisation: the union of two
           replicas is the union of their sets, and there is no conflict to
           resolve. The domain hands local-first (0004) over almost free,
           but only if the model is chosen for it now.

           The same data will arrive twice — once through an on-device hub,
           once through a vendor webhook. Without a deduplication key
           present from the first write, that is an unrecoverable data
           problem rather than a bug.

Decision:  Identifiers are generated on the client and are time-ordered.
           The record is append-only with tombstones; a deletion is an
           event. Every event carries its origin adapter and the external
           identifier that adapter saw. Instants are stored in UTC.

           Data is encrypted at the record, not merely in transport.

           Complete export works from the first release and is exercised by
           a test on every release. The exported form is readable without
           ZIVA — plain files in an open format.

Consequences:
           Makes easy: sync in any of the three shapes of 0004, deduplication
           across adapters, and an audit trail that exists by construction.

           Makes hard: nothing that a mutable relational model would make
           easy is lost, but storage grows monotonically and correcting a
           past event means appending a correction rather than editing.

           Guarantees: the project survives its own abandonment. If ZIVA
           stops being maintained, the household keeps a folder of readable
           documents and data any program can open. This is the whole answer
           to "what happens if you stop", and it is verifiable rather than
           promised.

Rejected:  Database-generated sequential keys — collide across replicas and
           leak record counts in any surface that exposes them.
           Mutable rows with UPDATE and DELETE — cheap today, and the reason
           sync becomes a rewrite rather than an addition.
           Encrypting transport only — the data is intended to travel through
           storage the family owns but the project does not.
