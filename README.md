# LogosLinux-winehqRollbackSteps
Documentation of steps used to rollback `winehq-staging` from `v8.8` to `v8.7`

Issue encountered:
- Followed the steps to install `winehq-staging` which by default installed `v8.8`.
- There seems to be an issue with this version and the ability to index after a Logos installation.

Others reported no issues with `winehq-staging=8.7`
These are the steps and commands run to downgrade to `winehq-staging=8.7`

This was started after a complete purge of `.wine*` from the system, but tested with an install of `v8.8` and then completed the rollback.
