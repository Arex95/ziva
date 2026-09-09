# 0010 — Decline advice by redirecting to the record, not by refusing

Status:    accepted
Date:      2026-09-09
Context:
           0006 settled what the chat will not answer. It did not settle
           what it says instead, and that gap is where the product fails.

           The people this was built for are the maintainer's elderly
           parents, at a distance. Part of the reason it exists is that they
           believe what they are told by whoever tells them — a neighbour, a
           forum, a television programme — and act on it.

           Those people will ask exactly the questions 0006 forbids: is this
           dangerous, should I take this, can I skip today's dose. A clean
           refusal is safe and is a product failure, because it leaves them
           with nothing and they return to the source that does give an
           answer. Being safer than the neighbour is worthless if it is also
           less useful than the neighbour.

Decision:  A question the chat will not answer is answered anyway, in a
           different shape: decline the advice, return what their own record
           says, and offer a route.

           ❌ "I cannot answer that. Consult your doctor."
           ✅ "I cannot tell you whether that is dangerous. What I can tell
              you is that your blood pressure over the last three months has
              been X, your doctor checked it in April and wrote Y. If it
              worries you, this is what you could ask them."

           Three rules make it safe rather than a loophole:

           1. Every statement cites the event it came from, with its date,
              so the person can recognise it — "ah, that April test". A
              claim that cannot point at a record is not made.
           2. If the record does not contain the answer, the chat says so.
              A redirect that invents data is worse than a refusal, because
              it is a refusal that sounds authoritative.
           3. The route is a question to take to a clinician, never a
              conclusion dressed as one.

Consequences:
           Makes easy: being more useful than the source the person would
           otherwise trust, which is the actual competition. And it turns
           retrieval — a task the model is good at and whose errors are
           visible — into the answer to a question the model is bad at.

           Makes hard: the tests. A test asserting that a refusal happened
           proves nothing here. The assertion has to be about what the
           person was told. This is the same failure that cost a document in
           Vantage: a suite green for months over accounting code that
           produced wrong numbers, because every test checked the shape of
           the rows and none checked what the account added up to.

           Requires: a corpus of the questions these parents actually ask,
           frozen, with the expected shape of each answer. Built from real
           questions, not invented ones.

Rejected:  A plain refusal — safe, and it returns the person to a worse
           source. This is the whole reason for the ADR.
           Loosening 0006 to answer the question directly — the measured
           unsafe rate on patient-posed medical advice is 5% at best and 13%
           at worst, and this record is read by people who act on it.
           A disclaimer attached to a direct answer — a disclaimer does not
           change what somebody does after reading the answer.
