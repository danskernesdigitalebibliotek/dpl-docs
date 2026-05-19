# Hotfix releases

Sometimes it may be necessary to create releases outside of [the standard 
release process](release-process.md). Typical situations involve critical security
updates or bug fixes. 

The important part of this work is that such releases only include a limited set
of changes instead of all development that's happened since the last release.

## Creating an extraordinary release

Hotfix releases basically follow the same procedures as regular
releases, with a few adjustments:

When creating the first hotfix release for an existing version, a
branch is created for hotfixes to that version, regardless of whether
its the latest release.

For instance, if creating a hotfix for `2026.18.0`, a branch of that
tag named `2026.18.x` is created and pushed.

The needed changes is applied to this branch, preferably by opening
pull request against it, but as hotfixes can span multiple versions,
require multiple changes and have a time pressure element, this is not
a hard requirement.

Do take care that changes applied to hotfixes is either already on
`develop`, or has an existing pull request.

When the required changes is ready on the hotfix branch, a release is
created on it just like it's done for normal releases on `main`
(example using a hotfix for `2026.18.0`):

2. [Create a new
   release](https://github.com/danskernesdigitalebibliotek/dpl-web/releases/new)
   1. Click "Select tag" => "Create new tag". 
   2. Enter a tag in the format of YYYY.WW.XX (e.g. 2026.18.1)
   3. Select `2026.18.x` as target.
   4. Click "Generate release notes" to automatically fill out the title
      and description.
   5. Ensure that "Set as the latest release" is selected before
      publishing the release.
2. Your release is build. It may take ~10 minutes, and you can see the
   process in [the actions tab of the
   repo.](https://github.com/danskernesdigitalebibliotek/dpl-web/actions)
   
The release notes will be rather empty if the fixes were applied
without pull requests, so adding a few words describing the nature of
the hotfix is preferable.
   
If creating a hotfix on an existing hotfix, simply reuse the hotfix branch. 
   
## Deploy the release

To deploy the release follow [the standard deployment and annoncement process](release-process#deployment-and-announcement).
