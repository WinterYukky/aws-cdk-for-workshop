# AWS CDK Contribution Workshop Agent Guide

This repository is a workshop sandbox based on the AWS CDK codebase. Follow these instructions whenever an AI agent or the CDK Contribution Skill operates in this workspace.

## Workshop scope and safety

- The contribution target is `jaws-ug-cdk/aws-cdk-for-workshop`, not `aws/aws-cdk`.
- Treat every reference to `aws/aws-cdk` in an installed skill as `jaws-ug-cdk/aws-cdk-for-workshop` for this workshop.
- Read issues and search pull requests with `--repo jaws-ug-cdk/aws-cdk-for-workshop`.
- If an `upstream` remote is needed, use `https://github.com/jaws-ug-cdk/aws-cdk-for-workshop.git`.
- Never add `https://github.com/aws/aws-cdk.git` as a remote, push to it, or open a pull request against it during this workshop.
- Work only on issue [#1](https://github.com/jaws-ug-cdk/aws-cdk-for-workshop/issues/1) or [#2](https://github.com/jaws-ug-cdk/aws-cdk-for-workshop/issues/2), unless a facilitator provides another workshop issue.
- Stop for human approval after analysis and planning, before implementation.
- Stop again for human review of the final diff and validation results before committing, pushing, or opening a pull request.
- Run only targeted tests for the selected exercise. An integration test may deploy resources to the participant's AWS account, so explain the impact and obtain approval before running it. Confirm cleanup after it finishes.
- Keep `.contributions/` as local review material. It is ignored by Git and must not be included in the exercise pull request.
- The participant owns every submitted change. Do not submit generated code that the participant has not reviewed and understood.

## Repository layout

| Area | Path |
|---|---|
| Stable L2 constructs | `packages/aws-cdk-lib/aws-{service}/` |
| Unit tests | `packages/aws-cdk-lib/aws-{service}/test/` |
| Stable integration tests | `packages/@aws-cdk-testing/framework-integ/test/aws-{service}/test/` |
| Design guidelines | `docs/DESIGN_GUIDELINES.md` |
| Contributor guide | `CONTRIBUTING.md` |

L1 files named `*.generated.ts` are generated code and must not be edited manually.

## Quick Reference — Commands

| Task | Command | Working Directory |
|---|---|---|
| Install dependencies | `yarn install` | repository root |
| Build everything | `npx lerna run build --concurrency 4` | repository root |
| Build aws-cdk-lib package only | `npx lerna run build --scope=aws-cdk-lib --stream` | repository root |
| Build one module | `yarn build` | `packages/aws-cdk-lib` |
| Build stable module integ tests | `npx lerna run build --scope=@aws-cdk-testing/framework-integ --stream` | repository root |
| Test all in package | `yarn test` | `packages/aws-cdk-lib` |
| Test one module | `yarn test aws-{service}` | `packages/aws-cdk-lib` |
| Test one file | `yarn test aws-{service}/test/{file}.test.ts` | `packages/aws-cdk-lib` |
| Lint | `yarn lint` | `packages/aws-cdk-lib` |
| Lint with auto-fix | `yarn lint --fix` | `packages/aws-cdk-lib` |
| Run all integ snapshots | `yarn integ` | `packages/@aws-cdk-testing/framework-integ` |
| Run integ snapshots in module | `yarn integ --directory aws-{service}/test` | `packages/@aws-cdk-testing/framework-integ` |
| Update an integ snapshot and deploy | `yarn integ aws-{service}/test/{integ-file}.js --update-on-failed` | `packages/@aws-cdk-testing/framework-integ` |

All test, lint, and integration commands require the relevant packages to be built first. Replace `{service}` and `{integ-file}` with the exercise values, such as `sns` and `integ.sns-display-name`.

## Exercise issue commands

```bash
gh issue view 1 --repo jaws-ug-cdk/aws-cdk-for-workshop --comments
gh issue view 2 --repo jaws-ug-cdk/aws-cdk-for-workshop --comments
gh pr list --repo jaws-ug-cdk/aws-cdk-for-workshop --state all --search "<issue-number>"
```

Use the issue URL supplied by the participant as the source of requirements. Existing pull requests may be prior workshop submissions; inspect them only for conflict detection, not as code to copy.
