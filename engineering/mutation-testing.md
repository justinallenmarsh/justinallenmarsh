# Parallel mutation testing without shared database state

[Mutineer Mongoid](https://github.com/justinallenmarsh/mutineer-mongoid) extends [Mutineer](https://github.com/davidteren/mutineer), an existing Ruby mutation-testing tool, with Mongoid/RSpec support. The upstream project supplies the mutation engine; this note focuses on the Mongoid integration maintained in the fork.

## The correctness problem

Mutation testing changes application code and asks whether the test suite detects the change. Running mutants in parallel is useful only if their results remain trustworthy. Two workers writing to the same database can make a valid mutant appear caught, or cause a test to fail for a reason unrelated to the changed code.

Booting Rails once and forking workers avoids repeated application startup. That also means dealing explicitly with inherited connections and the data present at boot.

## Isolation and cleanup

The integration captures the default test database's documents, collection options, and indexes at boot. Each coverage check and mutant receives a fresh database with a randomly generated name. Workers therefore begin from the same seed state without sharing writes.

Mongoid connections disconnect before a fork and reconnect in the child. The parent cleans up the disposable database after reaping the child, including when a worker times out or encounters an error. The source database is read only.

Seed data also contributes to the coverage cache key. A cache generated under one seed state must not silently survive a change that affects which lines a test exercises.

## Failure semantics

A lost database connection is an infrastructure error, not evidence that a test caught a mutation. The integration distinguishes these outcomes, including connection failures inside examples and suite hooks. Application-level failures, such as an expected uniqueness constraint violation, retain their ordinary testing meaning.

The integration tests check that serial and parallel reports agree on caught and surviving mutations. That gives parallel execution a behavioral reference rather than treating a faster run as sufficient validation.

## Deliberate limits

The supported scope is one default Mongoid client, ordinary collections, and a test environment. Multiple clients, views, time-series collections, and mixed ActiveRecord/Mongoid applications fail explicitly. Redis and other external services retain the application's own isolation requirements.

A hard kill of the parent can leave a disposable database behind. Database naming makes these identifiable; automatic cleanup cannot be promised once the supervising process is gone.

## Evidence

- [Database lifecycle implementation](https://github.com/justinallenmarsh/mutineer-mongoid/blob/718de2e3ae0e4367d2f122818cbe11ea100ebfbe/lib/mutineer/mongoid_worker_db.rb).
- [Integration tests](https://github.com/justinallenmarsh/mutineer-mongoid/blob/718de2e3ae0e4367d2f122818cbe11ea100ebfbe/test/mongoid_integration_test.rb): seed and index preservation, worker isolation, timeout cleanup, connection failures, coverage-cache invalidation, and serial/parallel parity.
- [Compatibility and installation](https://github.com/justinallenmarsh/mutineer-mongoid#compatibility).

These describe the supported behavior and its test coverage. They are not a throughput benchmark or a claim about every Mongoid application.
