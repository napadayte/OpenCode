# Light Code Policy

------------------------------------------------------------

## Purpose

This workspace allows small helper code, but it must not become an accidental software monolith.

Code is allowed only when it supports the workspace.

------------------------------------------------------------

## Allowed Code

Allowed:

- small scripts
- one-purpose scanners
- data validation helpers
- export helpers
- report generators
- backup verification helpers
- small prototypes
- local-only experiments

------------------------------------------------------------

## Not Allowed Without Promotion

Do not let this workspace silently become:

- a full application
- a production API
- a complex frontend
- a large package
- a multi-service system
- a hidden trading bot
- a financial decision engine

If code grows, promote it into a separate project.

------------------------------------------------------------

## Code Requirements

Every script should document:

- purpose
- inputs
- outputs
- command to run
- dependencies
- environment
- generated files
- risks
- example usage

------------------------------------------------------------

## Dependency Rule

Avoid dependencies unless clearly justified.

Before adding a dependency, document:

- why it is needed
- what problem it solves
- safer alternatives
- installation command
- security risk
- rollback plan

------------------------------------------------------------

## Scanner Rule

For stock scanners or market tools:

- document data source
- document assumptions
- document filters
- document false positive risks
- document false negative risks
- document output meaning
- do not hardcode secrets
- do not claim guaranteed returns
- do not trade automatically without a separate reviewed system

------------------------------------------------------------

## Test Rule

Small code still needs verification.

Minimum verification:

- run the script on a tiny sample
- confirm output path
- confirm generated files are ignored if needed
- confirm no secrets are printed
- confirm no source data is overwritten

------------------------------------------------------------
