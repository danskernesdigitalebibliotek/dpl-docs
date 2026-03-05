# Release process

In the past, the release process was complicated, due to several GitHub repos, depending on eachother.

Now, with the dpl-web mono-repo it's pretty easy.

# Creating the release

1. [Create a pull request from the `develop` branch against `main`.](https://github.com/danskernesdigitalebibliotek/dpl-web/compare/main...develop)
2. Wait for Github Actions to run and turn green.
3. Merge the pull request.
4. [Create a new
   release](https://github.com/danskernesdigitalebibliotek/dpl-web/releases/new)
   1. Click "Select tag" => "Create new tag". 
   2. Enter a tag in the format of YYYY.WW.XX (e.g. 2026.10.1)
   3. Select `main` as target.
   4. Click "Generate release notes" to automatically fill out the title
      and description.
   5. Ensure that "Set as the latest release" is selected before
      publishing the release.
5. Your release will now build. It may take ~10 minutes, and you can see the process in [the actions tab of the repo.](https://github.com/danskernesdigitalebibliotek/dpl-web/actions)

Once it is done, your release will be visible on [the releases page](https://github.com/danskernesdigitalebibliotek/dpl-web/releases), and have all the necessary assets/packages linked in the description.


# Deployment to staging and announcement

After creating a release, the torch passes to the DDF team to test and
approve the release before the final deployment to production.

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
   
# Deployment to production

When DDF has tested and approved the new release, they will annouce it
in the above mentioned topic.

The deployment to production is mostly handled by the platform team,
but it's occasionally taken care of by the development team.

The procedure is described in the
[runbook](../../DPL-Platform/runbooks/weekly-release-to-editors-and-moduletests/).

As the deployment takes some time, it's important to post updates to
the topic to keep DDF in the loop. In particular:

* Who's doing what.
* When they're doing it (when starting, with occasional status
  updates).
* What they're doing (deploying sites, redeploying failed deploys,
  syncing moduletest sites).
* When they're interrupted (taking a pause to go home to carry on, for
  instance).
* When it's done.

See [Release
2025.4.0](https://reload.zulipchat.com/#narrow/channel/419623-DDF.2B/topic/Release.202025.2E4.2E0)
for an example.
