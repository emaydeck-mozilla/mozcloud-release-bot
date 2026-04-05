# mozcloud-release-bot
Proof of concept repository for MozCloud Release Bot

## Overview and workflow
The purpose of this app is to allow us to establish a formalized release process for the repository. We have created 2 primary workflows to accomplish this: an automatic release and a manual release.

The automatic release begins while the PR is open (sets and reads labels to determine the release level and prepares user for the release) but the actual release occurs once the PR is merged to `main`. The manual release would ideally occur once changes have already been merged into `main`.

### Automatic release

While the PR is open:
1. Determine which charts were modified by the change
2. Determine release level (major/minor/patch) either automatically using the PR title (assumes semantic commit messages are used) or directly using labels set by a user -- the no-release tag will cancel any release activities
3. Post a comment showing a breakdown of the planned release
4. If a user changes the label, this process starts over

Once the PR is merged:
1. Helm chart versions are bumped and chart README files are automatically updated using helm-docs
2. New charts are packaged and pushed to GAR
3. The chart version and README file changes are committed and pushed back to main

### Manual release

This process can be run either while the PR is open or after it's merged to main. It is triggered manually by a user.

1. Helm chart versions are bumped using the release type supplied by the user and chart README files are automatically updated using helm-docs
2. New charts are packaged and pushed to GAR
3. The chart version and README file changes are committed and pushed back to main
