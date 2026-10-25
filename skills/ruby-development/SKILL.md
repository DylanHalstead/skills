---
name: ruby-development
description: "Write, test, review, refactor, and debug Ruby code using version-aware idioms and explicit value and failure contracts. Use for Ruby implementation, code review, failing tests, and performance work, including Rails models, concerns, callbacks, components, authorization, feature flags, queries, jobs, and migrations. Skip non-Ruby work."
---

# Ruby development

Follow repository instructions and existing conventions for code organization,
tests, formatting, and dependencies.

## Establish the runtime

Read the project's Ruby version files, `Gemfile`, and `Gemfile.lock` before
using version-dependent syntax or APIs. Use the project's Bundler and binstubs;
the shell's default Ruby may differ from the project's runtime. Inspect the
owning code and its callers rather than inferring a framework from directory
names alone.

For Rails work, read [Rails mechanisms](references/rails.md) in full before
changing models, concerns, callbacks, database queries, controller input,
presenters, components, authorization, feature flags, jobs, or migrations. Do
not load it for plain Ruby scripts or libraries that do not use Rails.

## Values and failures

- Only `nil` and `false` are falsey in Ruby; `0`, `""`, and `[]` are truthy.
  Distinguish an absent key from a present `nil` or `false`. Use `key?` when
  presence matters and `fetch` when a missing key should fail or use a default.
- `value || default` replaces `false` too. Preserve explicit false values when
  they are meaningful input. Standard Ruby `compact` removes `nil`; Rails
  `compact_blank` also removes `false` and other blank values.
- Safe navigation handles a `nil` receiver, not invalid input or a missing
  method on a non-nil object. Do not convert a broken required relationship into
  an unexplained nil result.
- Preserve the owning method's failure contract: a boolean result, a value, or
  an exception are different interfaces. Rescue errors you can handle at that
  boundary; do not turn a failed write or external operation into success.
- Check mutation and object ownership before using bang methods or sharing
  arrays/hashes. A method's `!` suffix signals a more dangerous counterpart, not
  one universal guarantee about mutation or exceptions.

## Objects and construction

Choose an object by its contract, not its directory. Use `Data.define` for a
fixed-member value with value equality and no member writers; use `Struct` or
another mutable object when changing members is part of the contract. A hash
fits genuinely variable keys. Use an ordinary class when construction,
invariants, behavior, or lifecycle need an explicit interface.

`Data` freezes the instance, not nested strings, arrays, or hashes, and does not
validate member types. Copy or freeze nested values when the ownership contract
requires it. Translate external keys, units, and representations at the owning
boundary so callers work with the application's concepts.

## Verification

Use the repository's test framework and fixture conventions rather than adding a
new one. Assert observable results and failures, including omitted, nil, empty,
and false input when those distinctions affect the contract. Make required setup
and evaluation order visible.

Run focused tests and the configured formatter/linter using the project runtime.
Expand checks when shared behavior changes. Report checks that could not run and
their prerequisites; do not infer success from unexecuted tests.
