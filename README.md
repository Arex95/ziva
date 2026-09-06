# ZIVA

A health record for a household, not for one person. ZIVA keeps the medical
history, lab results, wearable readings, diet and medication schedules of every
member of a family in one place, and lets you ask questions about it in plain
language using an AI provider of your choosing.

It is free, it is self-hosted, and there is no ZIVA service to sign up for. You
run it, you hold the data, nobody else has a copy.

> **Status:** design. Nothing is implemented yet. The architecture and the
> decisions behind it are being worked out before the first line of code.

## What ZIVA is not

**ZIVA is not a medical device and does not practise medicine.** Its intended
purpose is to help a household keep, organise and understand records it already
has. It does not diagnose, treat, cure, mitigate or prevent any disease or
condition, and it is not intended to inform any clinical decision.

Concretely, ZIVA will show you your own data and explain what the words in your
own reports mean. It will not tell you what condition you have, what medication
to take, whether to change a dose, or whether something is urgent. Those
questions belong to a clinician, and ZIVA is built to decline them.

**Any answer produced by an AI model can be wrong.** Treat it as a starting
point for a conversation with a professional, never as a substitute for one.

## Where your data goes

Your records stay on hardware you control. There is one exception, and it is
worth being blunt about it: **when you use the AI chat, the information needed
to answer your question is sent to the AI provider whose API key you supplied.**
That provider is your choice and your relationship. ZIVA never holds a key of
its own and never routes anything through a server belonging to the project.

## Licence

[GNU Affero General Public License v3.0](./LICENSE).

You may run, study, modify and share ZIVA freely, for any purpose, forever. If
you modify it and let other people use it over a network, you must offer them
your modified source. That is the whole of the obligation, and it exists so that
improvements to a health record made for families keep reaching families.

Copyright © 2026 Arthur. Contributions are accepted under a
[Contributor Licence Agreement](./CLA.md); see [CONTRIBUTING.md](./CONTRIBUTING.md).

"ZIVA" is the name of this project and is used as a mark by its author.

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md). Design discussion is welcome now —
code will be, once the architecture is settled.
