# Vendor updates

All DPL projects make use of libraries and other tools managed by third parties
(vendors). This describes our general process for handling updates to these:

1. Vendored code must be kept up to date.
2. Updating vendored is a continual process which is carried out as a part of 
   the normal release cycle.
3. We trust our automated tools to identify updates and locate problems with 
   updates to vendored code.
4. We rely on our knowledge about the projects and vendors to identify updates
   which require further scrutiny.

Projects have a more specific process for managing vendor updates can provide
further information as part of the project-specific documentation.

## Dependabot

We use [Dependabot](https://docs.github.com/en/code-security/getting-started/dependabot-quickstart-guide) 
to monitor vendor code and create pull requests in case there are updates.

### Handling pull requests

When handling a pull request created by Dependabot the developer handling the
pull requests does the following:

1. Consider the risk of the update. High risk updates require are less
   likely to be merged directly. We consider the following factors when 
   determining risk:
   - **Update level**: Major releases are more risky than minor and patch 
     releases as they contain breaking or other significant changes.
   - **Impact**: Updates to core frameworks of the project are more risky than 
     updates to code supporting single features.
   - **Usage**: Updates to dependencies used during development are considered
     less risky than updates used in production.
   - **Test coverage**: Updates to dependencies used in areas which are covered 
     by tests are considered less risky. 
2. Check the status of the GitHub Actions workflows for the pull request. If
   one of these fail then we never apply the update directly.
3. If the person decides that the update is safe to merge they merge the pull
   request directly.
4. If the person decides that the update should not be applied directly they:
   1. Update the Dependabot configuration to [ignore the dependency version](https://docs.github.com/en/code-security/dependabot/working-with-dependabot/dependabot-options-reference#ignore--)
      in question. If a new major version is failing we may still want to 
      include minor and patch releases.
   2. Create an issue in JIRA with the following information:
      - **Title**: *Opgrader [vendor project name] ([DDF project name])*
      - **Description**:
        - A short description of the library, the role it plays 
          within the project, why you do not think the update requires 
          additional scrutiny and a link til the pull request created by 
          Dependabot. All is Danish. This provides context to the business and
          the person handling the update in the future. 
        - Reference to the added ignore configuration (4.1) which must be 
          deleted after the update.
      - **Sprint**: *Opdateringer*
   3. Close the Dependabot pull request.

### Configuration

We configure Dependabot with the following properties:

- **Schedule**: Vendors should be checked weekly at night between sunday and 
  monday. This ensures updates occur frequently and on a regular basis across
  all projetcs.
- **Limit**: Open pull requests should be limited to 10 to avoid cluttering the
  list of pull requests.
- **Groups**
  - In general keep groups to a minimum. This avoids creating pull requests
    which cannot be merged directly due to a single vendor causing status
    checks to fail.
  - Use groups to ensure that dependencies that are usually updated in 
    conjunction (and usually by the same vendor) are handled appropriately 
    without creating multiple pull requests. Examples: 
    - `react`, `react-dom` and their related `@types` packages
    - `drupal/core`, `drupal/core-recommended` and 
      `drupal/core-composer-scaffold`
- **Versioning strategy**: [The minimum version should always be set to the 
  latest version](https://docs.github.com/en/code-security/dependabot/working-with-dependabot/dependabot-options-reference#versioning-strategy--).
  This prevents accidental downgrades.

For some projects creating many pull requests risk affecting other resources.
This may warrant a lower limit on pull requests or additional grouping.
