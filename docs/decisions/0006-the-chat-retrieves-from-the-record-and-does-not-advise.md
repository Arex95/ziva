# 0006 — The chat retrieves from the record and does not advise

Status:    accepted
Date:      2026-09-05
Context:
           A physician-led red-teaming study of 888 chatbot responses to 222
           patient-posed medical questions (npj Digital Medicine 9:241, 2026)
           found problematic responses in 21.6% of cases for the best model
           and 43.2% for the worst, with outright unsafe responses between
           5% and 13% — responses with, in the authors' words, the potential
           to lead to serious patient harm.

           What that study measured is medical advice. It did not measure
           retrieval over a person's own recorded data, which is a different
           task with an opposite risk profile: the answer is checkable
           against the record sitting next to it.

           Separately, intended purpose is what decides regulatory
           classification. MDCG 2019-11 excludes software pursuing purely
           lifestyle or wellness purposes from MDR/IVDR; the AI Act's
           open-source exemption does not survive a high-risk
           classification, so publishing freely is not a shield.

Decision:  The chat answers questions about the household's own recorded
           data and explains terms appearing in the household's own
           documents. It declines diagnosis, dosing, treatment
           recommendation and triage. This list is product specification,
           and refusals are covered by tests.

           Examples in scope: when was this last measured, has this trended
           since March, what was prescribed in April, which evening doses
           went unrecorded last week.

           Examples out of scope: do I have this condition, is this value
           dangerous, should I change the dose, is this urgent.

Consequences:
           Makes easy: verification. A retrieval answer is checkable against
           the record, so the failure mode is visible rather than plausible.
           It is also the capability nobody currently has — no household can
           answer those questions in under twenty minutes of paperwork.

           Makes hard: the product will feel less capable than a general
           assistant, and users will ask the out-of-scope questions anyway.
           Declining well is a design problem, not a disclaimer.

           Requires: only the subset of the record a question needs is sent
           to the model, a local model is a first-class option, and the user
           can see what will be sent. The privacy promise stops at the
           moment the chat is used, and the interface says so — not the
           footer.

Rejected:  A general health assistant with a disclaimer — the disclaimer
           does not change intended purpose, and the measured unsafe rate is
           not something a footer addresses.
           No chat at all — retrieval over one's own history is the single
           capability that makes the record worth keeping.
