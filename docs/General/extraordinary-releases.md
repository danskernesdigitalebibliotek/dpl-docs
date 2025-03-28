# Extraordinary releases

Sometimes it may be necessary to create releases outside of [the standard 
release process](release-process). Typical situations involve critical security 
updates or bug fixes. 

The important part of this work is that such releases only include a limited set
of changes instead everything which has subsequently been 

## Creating an extraordinary release

1. Identify the subproject for which to apply the change. This can be:
   1. Design system
   2. React components
   3. CMS
2. Clone the project locally
3. Identify the starting point for the extraordinary release. This will usually 
   be a previous release.
4. Create a branch from the tag corresponding to the previous release. Replace 
   the patch part of the version with an `x`. This branch will be used for all
   changes for the release. Example: `git checkout -b 2025.13.x 2025.13.0`.
5. Push the branch.
6. Create a new branch from this branch to contain an individual change. 
   Example: `git checkout -b important-change 2025.13.x`
7. Commit the necessary changes to this branch. This will often be in the form
   of cherry-picked commits already applied to the `develop` branch of the
   project.
8. Push the new branch and create a pull request from the new branch against the
   release branch.
9. Wait for tests to complete and the pull request to be approved.
10. Repeat steps 6-9 if the release should contain multiple changes.
11. Create the release for the project
    1. Enter the release version as "Choose a tag", and select to
       create it on publish.
    2. Select the release branch as target.
    3. Click "Generate release notes" to automatically fill out title
       and description.
12. Depending on the origin project for the extraordinary release follow through 
    with the release in the other projects using the same release name:
    1. *Design system*: React components and CMS.
    2. *React components*: CMS only.
    3. *CMS*: No other projects.
13. Do not merge the release branch into `main` or `develop` branches for the
    project.

## Deploy the release

To deploy the release follow [the standard deployment and annoncement process](release-process#deployment-and-announcement).
