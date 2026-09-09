# 0011 — Visibility is granted per subject, by the subject

Status:    accepted
Date:      2026-09-09
Context:
           The precedent this project keeps measuring itself against,
           Nightscout, watches a child. A parent has authority over a
           child's data, so "the family sees everything" is correct there.

           ZIVA's first real case is the inverse: adult children watching
           adult parents. Needing help does not remove autonomy, and an
           adult has a standing interest in deciding what their children
           know about their health. There are diagnoses people do not tell
           their families, and that is their right.

           This has a practical edge as well as a moral one. A system that
           feels like surveillance is a system that gets uninstalled, and
           this one only works if the parents keep it. Dignity here is a
           feature, not a courtesy.

Decision:  A subject's record is visible to that subject. Any other
           visibility is granted by the subject, to a named person, and is
           revocable by the subject at any time.

           The household groups; it does not authorise. Belonging to the
           same household conveys no access on its own.

           Every read of another subject's record is recorded, and the
           subject can see who looked and when. This is what makes the grant
           trustworthy rather than nominal.

           A guardian relationship exists for the case where the subject
           cannot operate the application at all — an infant, an animal,
           advanced dementia. It is explicit, recorded, and never inferred
           from age, relationship or household membership.

Consequences:
           Makes easy: the honest conversation when installing it. "You
           decide what I see, and you can see when I looked" is the sentence
           that gets a parent to accept it.

           Makes hard: every query is scoped by grant rather than by
           household, which is more work in every endpoint and is the kind
           of rule that erodes quietly. It belongs in the architecture tests
           the handbook already requires, not in review.

           Forecloses: any screen that assumes a caregiver sees the whole
           household. What a viewer sees is the union of their grants, and
           the interface has to be built for a partial view from the start.

           Also forecloses: sync substrates where access control is the
           storage provider's. A shared cloud folder gives everyone with the
           link everything in it, which cannot express this. That is a
           second, independent reason for 0008.

Rejected:  Household-wide access with per-screen hiding — hiding is not
           access control, and the first raw query bypasses it.
           Roles (parent, child, carer) — a role is a guess about what
           somebody should see. The subject is not guessing.
           Guardianship inferred from age or relationship — the assumption
           that an old person's records belong to their children is exactly
           the assumption this decision exists to refuse.
