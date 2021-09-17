# Workshop - Lab 04

This lab is an optional challenge! The goal of the challenge is to practice using the GitHub fork model with a third party repository. You have to submit a PR that fixes the build errors highlighted by the Travis integration of the [github.com/networktocode/codelint](https://github.com/networktocode/codelint) repository.

If you need a refresher on how to fork and submit a PR, revisit Lab 03!

## Tasks

To get started, perform the following steps:

- Open the [main repository](https://github.com/networktocode/codelint) in your browser on GitHub.
- Inspect the build status on Travis-CI
  + Check the log of the [most recent failed build](https://travis-ci.com/github/networktocode/codelint).
  + Check the build configuration to see what commands are executed. You may also review the `.travis.yml` file in the project repository.

To fix the issues:

- Create a fork of this repository under your own account.
- Clone the fork locally on the lab machine.
- Create a new branch to hold the fixes.
- Run the tests from the Travis-CI build (e.g. `black -v --check .`) and fix the errors.
- Create one or more commits with the fixes.
- Push the branch with the commits to GitHub.
- Create a PR from your fork to the main repository.
- Wait for the Travis-CI build to run and verify it succeeds.
  + If it fails, check the build log and go back to your fork to fix the remaining issues. You may update the PR in place by pushing to your branch until you're done.

If you get stuck at any stage in the process don't hesitate to ask for help. Once your PR's build is green (i.e. succeeds) let your instructor know! Great work!
