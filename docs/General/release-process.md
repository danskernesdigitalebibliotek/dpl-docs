# Release process

Creating a new release involves creating a new release of the design
system, the react components and the CMS itself. It's important that
it's done in that order, due to the dependencies between the projects.

In the following you'll need to use the "Bypass branch protection"
option when merging to skip having someone review the changes.

# Creating the release

## [Design system](https://github.com/danskernesdigitalebibliotek/dpl-design-system)

1. Create a pull request from the `develop` branch against `main`.
2. Wait for Github Actions to run and turn green.
3. Merge the pull request.
4. [Create a new
release](https://github.com/danskernesdigitalebibliotek/dpl-design-system/releases/new)
     1. Enter the release version as "Choose a tag", and select to
        create it on publish.
     2. Select `main` as target.
     3. Click "Generate release notes" to automatically fill out title
        and description.
     4. Ensure that "Set as the latest release" is selected before
        publishing the release.


### Update DPL React for local development

These steps are not critical for release, but are required for
developers to get the latest version of the design system when
developing.

In order to update the dependencies, you need to be [authenticated
with the GitHub NPM package
repository](https://danskernesdigitalebibliotek.github.io/dpl-docs/DPL-React/#requirements).

In https://github.com/danskernesdigitalebibliotek/dpl-react:

1. Create a new branch locally from `develop` (remember to `git pull` first).
2. Ensure you're using the right version of `node`. You can use `nvm
   use` for this.
3. Update the version of the design system used by running `yarn add
   @danskernesdigitalebibliotek/dpl-design-system@[version]`, you can
   find the latest version of the design system [in the package on
   Github](https://github.com/danskernesdigitalebibliotek/dpl-design-system/pkgs/npm/dpl-design-system)
   NOTE: You need to be certified for this.
4. Commit and push the changes.
5. Create a pull request from your branch against `develop`.
6. Wait for actions to turn green.
7. Merge the pull request.

## [DPL React](https://github.com/danskernesdigitalebibliotek/dpl-react)

1. Create a pull request from the `develop` against `main`.
2. Wait for actions to go green.
3. Merge pull request.
4. [Create a new
   release](https://github.com/danskernesdigitalebibliotek/dpl-react/releases/new)
   in the same way as with the Design system.

## [DPL CMS](https://github.com/danskernesdigitalebibliotek/dpl-cms)

1. Create a new branch locally from `develop` (remember to `git pull` first).
2. Merge `main` into your branch.
3. Update the version of the Design System used: `RELEASE=[version]
   VERSION=[version] task dev:composer:update-design-system`. Refer to
   `task dev:composer:update-design-system --summary` if needed.
4. Update the version of React components used: `RELEASE=[version]
   VERSION=[version] task dev:composer:update-react`
5. Commit, push your branch and create a pull request against `develop`.
6. Wait for actions to go green.
7. Merge your pull request.
8. Create a new pull request from `develop` against `main`.
9. Wait for actions to go green.
10. Merge your pull request.
11. [Create a new
    release](https://github.com/danskernesdigitalebibliotek/dpl-cms/releases/new)
    in the same way as with the Design system.
    
# Deployment and announcement

After creating a release, there's only a few housecleaning tasks left.

## Deployment to staging

In order to deploy the new release to staging so that DDF can test it,
refer to [Platform
runbook](../../DPL-Platform/runbooks/how-release-a-new-version-for-approval-testing/).
This will require access to Azure in order to run the deployment.

## JIRA and communication

That was the technical part, now you need to tell somebody about your
shiny new release.

Do the following for both the
[Hermod](https://reload.atlassian.net/jira/software/c/projects/DDFHER/boards/497)
and
[Brahma](https://reload.atlassian.net/jira/software/c/projects/DDFBRA/boards/498)
projecs in Jira (this obviously requires Jira access).

1. Rename the `upcoming` release to the released version.
2. Mark the release as released.
3. Create a new unrelased `upcoming` release if it doesn't happen automatically.
4. When the release has been [deployed to
   staging](#deployment-to-staging), tell DDF by creating a new topic
   in the the `#DDF+` Zulip channel with the release name in the
   subject and links to the release on staging and the release notes
   for the projects that has contributed to the release. Take a look
   at past release announcements in Zulip for an
   [example](https://reload.zulipchat.com/#narrow/channel/419623-DDF.2B/topic/Release.202024.2E46.2E0/near/482035323)
   
