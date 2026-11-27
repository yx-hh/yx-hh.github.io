---
title: "Diff-based pipelines: faster builds without false confidence"
description: "Skipping work is easy. Skipping only the work that's safe to skip is the hard part."
tags: [CI/CD, Developer Productivity]
---

## The problem

App code, infrastructure, and docs lived in one repo, and every push rebuilt and redeployed everything. Feedback was slow, and engineers batched changes to avoid waiting, which made each release riskier.

## Principles I lean on

- Map changed paths to affected workflows explicitly, and keep the map in the repo.
- Keep an escape hatch: a full run on the main branch or on a schedule.
- Make infra changes reviewable artifacts (for example a CDK diff) before they reach production.

## Trade-offs

The risk is a false skip: a hidden dependency the path map doesn't know about. The periodic full build catches those, at the price of some duplicate compute.

## Outcome

Build and deploy time dropped by 40–60%, and smaller, more frequent releases became the default.
