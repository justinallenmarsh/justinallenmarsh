# TangoTube: organizing performances around a music catalogue

[TangoTube](https://tangotube.tv) helps dancers find performances by dancer, music, and event. I build and operate the application. Its source is private; this overview describes the architecture at a high level, with the [open-source CLI](https://github.com/justinallenmarsh/tangotube-cli) providing a public entry point into the product.

## Domain model

A composition, a recording of that composition, and a dance performance using the recording are different things. A composition can have multiple takes by the same orchestra, and a take can appear in multiple transfers or releases. Keeping these distinctions in the catalogue supports more precise discovery than matching a title alone.

The web application uses Rails and PostgreSQL, with an Inertia/React/TypeScript interface. Domain models hold catalogue behavior; Elasticsearch provides search indexes. Background jobs handle work such as media identification and index synchronization outside interactive requests.

## Audio identification

Historical recordings introduce a practical matching problem: different transfers can play at slightly different speeds, changing pitch and tempo together. The Rust audio-processing component compares fingerprints across playback speeds and records a best candidate, alternatives, and a confidence margin. An inconclusive match needs to remain distinguishable from a confirmed identification.

## Interfaces and operation

The Go CLI exposes catalogue search and personal-library operations to terminal users and automation. Its documented JSON and MCP interfaces provide a way to inspect the integration contract without access to the Rails source.

The application also models backup runs and verification results, including restore checks. An uploaded database dump and a successfully restored database are separate outcomes worth recording.

## What to inspect

- [Live product](https://tangotube.tv): the catalogue and discovery experience.
- [CLI source and documentation](https://github.com/justinallenmarsh/tangotube-cli): the public client and its contracts.
- [CLI interface design](command-line-interfaces.md): terminal and automation behavior.

This overview describes the implementation approach. It makes no claims about traffic, latency, identification accuracy, or operating scale without a published measurement.
