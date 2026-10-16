# Justin Marsh

Software engineer in Berlin. I build web applications, developer tools, and software for working with music and video.

I build and operate [TangoTube](https://tangotube.tv), a platform for discovering Argentine tango performances. My work spans Rails applications, Go command-line tools, and Rust audio processing. I care about data integrity, repeatable tests, and making systems straightforward to operate.

## Selected work

### [Mutineer Mongoid](https://github.com/justinallenmarsh/mutineer-mongoid)

A maintained fork of [Mutineer](https://github.com/davidteren/mutineer) that adds parallel mutation testing for Rails applications using Mongoid and RSpec. The integration isolates each mutant's database, preserves seed data and indexes, and distinguishes infrastructure errors from mutations caught by tests.

[Implementation](https://github.com/justinallenmarsh/mutineer-mongoid/blob/main/lib/mutineer/mongoid_worker_db.rb) · [Integration tests](https://github.com/justinallenmarsh/mutineer-mongoid/blob/main/test/mongoid_integration_test.rb) · [Design notes](engineering/mutation-testing.md)

### [TangoTube CLI](https://github.com/justinallenmarsh/tangotube-cli)

A Go CLI for searching tango videos, managing a personal library, and creating practice clips. It supports interactive terminal use, structured JSON output, and an MCP interface for coding agents.

[Documentation](https://github.com/justinallenmarsh/tangotube-cli/tree/main/docs) · [Tests](https://github.com/justinallenmarsh/tangotube-cli/tree/main/e2e) · [Design notes](engineering/command-line-interfaces.md)

### [TangoTube](https://tangotube.tv)

A Rails product that organizes performances around dancers, music, and events. It brings together a searchable catalogue, music identification, and tools for dancers to explore and practice. The application source is private; the CLI above is open source.

## Working with me

My main tools are Ruby, Rails, PostgreSQL, Go, Rust, and TypeScript. I prefer clear domain models, explicit interfaces, and tests that exercise real behavior.

[Email](mailto:jmarsh24@gmail.com) · [GitHub](https://github.com/justinallenmarsh)
