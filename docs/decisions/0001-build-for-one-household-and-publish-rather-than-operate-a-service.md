# 0001 — Build for one household and publish it, rather than operate a service

Status:    accepted
Date:      2026-09-05
Context:
           Every consumer product in this category has died and taken its
           users' data with it: Google Health (2012), Microsoft HealthVault
           (2019), CareZone (bought by Walmart for ~$200M, app pulled 2021,
           Walmart Health closed 2024), K Health's consumer app (2025),
           Fasten OnPrem (archived 2026). The one survivor, Nightscout, was
           written by a father for his son in 2013, is operated by nobody,
           and has over 39,000 members twelve years later.

           A health record has a fifty-year horizon. A consumer health
           company has about five. That mismatch is structural, and funding
           makes it worse rather than better, because it introduces an
           investor who needs an exit.

           Health app retention is 3-4% at thirty days. Any plan that
           depends on adoption is betting against a documented 96% failure.

Decision:  ZIVA is built for the maintainer's own household and published
           under a free licence in case it is useful to anyone else. It is
           not operated as a service, does not offer support, and adoption
           is not a success criterion.

Consequences:
           Makes easy: the project cannot fail by the metric that kills
           everything else. No infrastructure cost, no data-controller role
           over other people's health data, no jurisdiction question.

           Makes hard: reach. Self-hosting and installation friction filter
           out most families, and no amount of design fully removes that.

           Forecloses: competing on features or convenience. A funded
           competitor wins both, and that is accepted. What ZIVA offers
           instead is that it cannot be taken away — a property of AGPL,
           self-hosting and open formats, not of effort.

           Obliges: the project must survive its own abandonment. See
           0005 for the data format that guarantees it, and 0004 for the
           absence of anything that expires.

           No feature exists for a hypothetical user. Building for users
           who never arrived is where this project's time would go.

Rejected:  A hosted public instance — makes the maintainer responsible for
           strangers' special-category health data, with an infrastructure
           bill nobody pays. The only company that tried it in this exact
           category (Fasten Connect) had to close the open half to fund it.

           Targeting a market and validating it first — a market only
           matters if adoption is the goal, and it is not. The bar is one
           household, and that question is already answered.
