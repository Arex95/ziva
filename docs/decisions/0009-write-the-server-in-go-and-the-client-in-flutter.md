# 0009 — Write the server in Go and the client in Flutter

Status:    accepted, supersedes 0007
Date:      2026-09-06
Context:
           0007 chose TypeScript and an installable web application. Its
           premise was 0004's serverless core, which 0008 replaced, so the
           decision has to be retaken rather than adjusted.

           WHO RUNS IT, ON WHAT. A stranger's homelab, possibly a Raspberry
           Pi. This is the input the handbook says decides most often and is
           skipped most often. It eliminates the JVM, whose resident memory
           is the highest of the managed runtimes. It does not separate Go
           from Rust: roughly 20MB against 10MB at idle is noise, and the
           number that mattered was 300-500MB.

           WHAT THE CLIENT IS. Medication reminders that actually fire, and
           on-device wearable hubs (HealthKit, Health Connect), both need a
           native application. So the client is Flutter and the client
           language is Dart regardless of what the server is written in.
           That matters because it removes TypeScript's strongest argument:
           with a Flutter client, TypeScript and Go both mean two
           ecosystems, and the operational properties decide instead.

           AI IS FIRST-CLASS HERE, so SDK maturity is a real criterion. As
           of May 2026 Anthropic's official SDK lineup is Python,
           TypeScript, Java, Go, Ruby, C# and PHP. Rust is absent, with the
           request still open. The official MCP Go SDK is maintained in
           collaboration with Google and ships in the same beta wave as
           Python, TypeScript and C#. Go is first-class; Rust is community
           code at the centre of the product.

           RUST'S ACTUAL ADVANTAGE DOES NOT APPLY. It is memory safety
           without a garbage collector. A household API serving five people
           can afford a garbage collector, so that advantage buys nothing,
           while its costs — months to competence, compile time as a daily
           tax on a project built in evenings — land squarely on this
           project's largest risk, which is abandonment.

           The maintainer has already designed and shipped an offline-first,
           encrypted, export-capable Flutter monorepo in another domain
           (Vantage). Its architecture transfers: real Dart packages rather
           than folders, dependency rules read from pubspec, a pure domain,
           drift with queries as streams, SQLCipher at rest with the key in
           the platform keystore, and export encrypted with the user's own
           passphrase rather than the device key.

Decision:  Go for the server. Flutter for the client, on the Vantage
           architecture. Phase one is the API alone.

           SQLite as the server's database, embedded, one file. A household
           is five people; there is no concurrency Postgres would solve, and
           a backup that is a file somebody can copy is the difference
           between having backups and believing in them.

           The AI provider is a port written here, not a framework adopted.
           The user brings their own key and may bring Anthropic, OpenAI,
           Google or a local model, so the interface has to exist regardless
           — and a dependency that abstracts twenty providers is more than
           this needs, in the most sensitive position in the codebase.

Consequences:
           Makes easy: a single static binary. With a pure-Go SQLite driver
           there is no cgo, so cross-compiling for a stranger's ARM board is
           trivial. Undeclared imports fail the build, which puts the module
           dependency graph at rung 0 for free.

           Makes hard: error handling is manual and therefore skippable, and
           in a health record a swallowed error is a dose that was never
           recorded. Mitigated the way Vantage mitigated its own hazards —
           a lint that fails CI, here errcheck. Rung 2, and a gate that runs
           beats a rung 0 that is a plan.

           Also hard: no high-level multi-provider AI abstraction exists in
           Go, so streaming, tool use, retries and per-provider differences
           are written here. That is real work, not a few hundred lines.

           Phase one being API-only is deliberate: it reaches the risk that
           can kill the project — the cost of getting data in — with no
           interface at all. A PDF, an endpoint and curl answer it.

Rejected:  Rust — no official SDK from the providers this product is built
           around, and its defining advantage is one this problem cannot
           spend.
           TypeScript — would win if the client were a web application,
           because it would make the whole product one ecosystem. With a
           Flutter client it does not, and it carries the largest dependency
           surface of any option, which is a supply-chain question rather
           than a convenience one when the data is medical.
           Java or Kotlin with Spring, the handbook default — ruled out by
           resident memory on the hardware this has to run on.
           Python — indicated when the work is machine learning. This calls
           an HTTP API; it does not train anything.
           Postgres on the server — solves concurrency this does not have,
           at the cost of a second service to run, update and back up.
