# Documentation Site

This project exists to consolidate and standardize documentation across DPL
(Danish Public Libraries) repositories. It's based on [mkdocs
material](https://squidfunk.github.io/mkdocs-material/) and uses a handy
[multirepo-plugin](https://github.com/jdoiro3/mkdocs-multirepo-plugin) to import
markdown and build documentation from other DPL repositories dynamically.

## Adding documentation

Any repository you want to add to the documentation site, must have a `docs/`
folder in the project root on github and relevant markdown must be moved inside.

If you wish to further divide your documentation into subfolders, mkdocs will
accomodate this and build the site navigation accordingly. Here is an example:

``` shell
docs/
| README.md # Primary docs/index file for your navigation header
└───folder1 # Left pane navigation category
│   │ file01.md
│   └───subfolder1 # Expandable sub-navigation of folder1
│       │  file02.md
│       │  file03.md
└───folder2 # Additional left pane navigation category
    │  file04.md
```

The `docs/` folder is self-contained, meaning that any relative links e.g.
`"../../"` linking outside the docs/ directory, should use an absolute URL like:
<https://github.com/danskernesdigitalebibliotek/dpl-docs/blob/main/README.md>

Otherwise, following the link from the documentation site will cause a 404.

## Site development

The documentation project is hosted
[here](https://github.com/danskernesdigitalebibliotek/dpl-docs).

It uses a Github workflow to build and publish to github pages. Since
documentation can be updated independently from other repos, a cron has been
established to publish the site every 6 hours. While this covers most use cases,
it's also possible to trigger it adhoc through [Github
actions](https://github.com/danskernesdigitalebibliotek/dpl-docs/actions/workflows/build-publish.yml)
with the workflow_dispatch event trigger.

Customizations (colors, font, social links) and general site configuration can
be configured in
[mkdocs.yml](https://github.com/danskernesdigitalebibliotek/dpl-docs/blob/main/mkdocs.yml)

### Requirements

- [mkdocs
  material](https://squidfunk.github.io/mkdocs-material/getting-started/)
- [multirepo-plugin](https://github.com/jdoiro3/mkdocs-multirepo-plugin)
