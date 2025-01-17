---
category: features
slug: /features/security
title: "Security"
description: Everything Yarn does to keep your installs secure.
---

## Audits

Yarn doesn't run audits by default when running `yarn install`, as this should rather be performed in a cron task. You can however perform audits whenever you want by running [`yarn npm audit`](/cli/npm/audit).

:::info
Our implementation has a couple of differences with the npm one. Like most other Yarn commands, `yarn npm audit`, by default, only applies on the direct dependencies from the current workspace. To get a report on the whole project, use the `-A,--all` and/or `-R,--recursive` flags.
:::

:::tip
You can exclude your `devDependencies` (and their transitive dependencies) from the report by running the command with `--environment production`.
:::

## Hardened mode

The hardened mode can be set (or disabled) using either the `enableHardenedMode` setting, or by defining `YARN_ENABLE_HARDENED_MODE` in your environment variables, but in most cases you won't even have to think about it - the hardened mode is enabled by default when Yarn detects it runs in a pull request from a public GitHub repository.

Under this mode, Yarn will automatically enable the `--check-resolutions` and `--refresh-lockfile` flags when running `yarn install`, which should protect you against most attacks caused by [lockfile poisoning](https://snyk.io/blog/why-npm-lockfiles-can-be-a-security-blindspot-for-injecting-malicious-modules/), at the cost of a little bit of install speed.
