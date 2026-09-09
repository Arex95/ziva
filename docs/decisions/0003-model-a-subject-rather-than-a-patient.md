# 0003 — Model a Subject rather than a Patient, and treat FHIR as vocabulary

Status:    accepted
Date:      2026-09-05
Context:
           A household contains people and, often, animals. A pet's record
           has the same shape as a person's: vaccinations with expiry,
           monthly and daily medication, weight, vet visits, lab results,
           documents. Supporting it costs nothing if the core is generic and
           costs a rewrite if it is not.

           The animal side also carries something the human side lacks: an
           external forcing function. A boarding kennel demands current
           vaccination proof with timing rules, an EU pet passport is a legal
           document, an insurer wants prior history. Nobody ever compels a
           person to produce their own medical history — which is precisely
           the absence that made Google Health "a static filing cabinet".

           FHIR models the household well (Group, RelatedPerson) but is a
           human standard. A pet is not a Patient and no official household
           profile includes one.

Decision:  The core's primary entity is a Subject, which may be a person or
           an animal. FHIR drops from being the model to being the vocabulary
           of the human side, and the core sits one level above it.

Consequences:
           Makes easy: covering the whole household with one timeline, one
           medication engine and one document store. Also gives a place to
           exercise the full product with no regulatory weight, since MDR,
           IVDR and the AI Act are human-only instruments.

           Makes hard: clean FHIR interoperability. Import and export on the
           human side map to FHIR resources; the core's own shape does not.
           A translation layer is required at that boundary.

           Constraint: no pet-specific feature is built until the
           maintainer's own household needs it (0001). This decision is
           about the data model only.

Rejected:  Patient as the primary entity — correct for FHIR, and a rewrite
           of every table, query and screen the day an animal appears.
           A separate pet module — duplicates the timeline, the medication
           engine and the document store for no gain.
           Adopting a full FHIR server (HAPI, Medplum) — built for
           integrators; the footprint does not fit a family's hardware.
