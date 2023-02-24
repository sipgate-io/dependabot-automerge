# dependabot-automerge

This reusable GitHub Action workflow reacts to dependabot pull requests and merges them if no tests fail.

It supports projects built on NPM, Maven, Gradle or Python `unittest`. If none of these test-suites failed, the pull request will be merged.

Regardless of the outcome, a Slack message will be sent to the webhook defined in the `SLACK_WEBHOOK` secret. If the vulnerability score is critical (CVSS >= 9) and the tests failed, it will additionally add an `@channel` ping to this message.

## Usage
To use this action as part of your workflow, you need to trigger it on Pull Requests by adding it like this:
```yml
name: Run tests on pull request and auto merge dependabot pull requests

on: pull_request

permissions: write-all

jobs:
  dependabot_merge:
    uses: sipgate-io/dependabot-automerge/.github/workflows/dependabot_automerge.yml@main
    secrets: inherit
```
