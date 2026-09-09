# 0002 — Licence under AGPL-3.0 with a contributor licence agreement

Status:    accepted
Date:      2026-09-05
Context:
           The repository was created under MIT. MIT permits anyone to host
           ZIVA as a closed paid service without giving anything back, which
           is the one outcome that contradicts why the project exists (0001).

           GPL-3.0 triggers copyleft on distribution only; running software
           on a server to provide a service is not distribution. For
           self-hosted software the two licences behave identically almost
           always — the difference appears exactly in the scenario above.

           Separately, licence and ownership are different systems. Once an
           external contribution is merged, its author holds copyright to it,
           and the project can no longer change licence or offer a commercial
           one without locating every contributor.

Decision:  AGPL-3.0, plus a contributor licence agreement granting the
           maintainer the right to sublicense and relicense, enforced by a
           bot on every pull request.

Consequences:
           Makes easy: a third party may sell hosted ZIVA with support —
           this is what happens around Nightscout — and their improvements
           come back. An organisation that will not comply with the AGPL has
           a second door: buying a commercial licence, which is possible
           only because of the CLA. Families never pay, in either case.

           Also makes possible: distributing a build through an app store
           later. Apple's App Store terms impose copy restrictions the GPL
           family forbids as additional restrictions — the reason VLC was
           pulled in 2011. As copyright holder plus CLA, the maintainer can
           ship his own build under separate terms. Nobody else can.

           Makes hard: corporate contribution. Many companies forbid
           touching AGPL, and a CLA deters some individual contributors.
           For a project shaped like this, that cost is low.

           Cannot be revoked: every published version stays under the AGPL
           permanently, including by the maintainer. The CLA says so.

Rejected:  MIT — does not close the closed-hosting scenario.
           GPL-3.0 — the SaaS loophole is exactly the gap that matters here.
           A DCO instead of a CLA — certifies provenance but grants no
           relicensing right, so the project would be frozen by the first
           unreachable contributor.
           PolyForm Noncommercial, as HealthLog moved to — not open source,
           and "free for families" does not require restricting commerce.
