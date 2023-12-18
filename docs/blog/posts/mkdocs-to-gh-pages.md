---
authors:
  - mpinilla
categories:
  - Software Practice
date: 2023-12-13
draft: false
title: Publishing Documentation to GH Pages
author: Miguel Pinilla
Copyright: (c) Miguel Pinilla, All rights reserved
License: "This work is licensed under the Creative Commons License CC BY-NC-SA 4.0: https://creativecommons.org/licenses/by-nc-sa/4.0/"
email: miguel.pinilla@saldubatech.com
share: "true"
---

The use case I was trying to fulfill:

1. Have a reasonably unified authoring environment for the different content that I intend to write.
2. Favor some sort of open source markup language over proprietary WYSIWYG editors. Candidates were Markdown, Latex, ReSTructured Text.
3. Benefit from the version and change control that Github provides
4. Be able to share the results with colleagues
5. Be able to reuse the set up to document other projects in Github.
6. Be able to easily embed rich math expressions and UML or similar diagrams
7. Bonus:
   1. Be able to publish to Medium and other syndication platforms.
   2. Somewhat just for nostalgic reasons, be able to author Latex documents in the same environment and publish them.

<!-- end_excerpt -->

!!! note
    These are not step by step instructions, they are a summary of the notes I took when setting up my environment. To follow them, you should be familiar with your OS (mine is MacOS), Python, Pip, Mkdocs and Github Actions

## The Tools I chose

1. For the editing language, [Markdown](https://www.markdownguide.org/) with [Mkdocs](https://www.mkdocs.org/) and its [material](https://squidfunk.github.io/mkdocs-material/) theme and utilities.
2. For Math typesetting, the [Latex](https://www.latex-project.org/) math notation supported by the [pymdown.arithmatex](https://facelessuser.github.io/pymdown-extensions/extensions/arithmatex/) mkdocs extension.
3. For Diagrams, [PlantUml](https://plantuml.com/) as supported by the [plantuml-markdown](https://github.com/mikitex70/plantuml-markdown) mkdocs extension
4. For editing, I chose two different environments:
   1. [VS Code](https://code.visualstudio.com/) for short editing and managing the tools, scripts, etc. with the extensions:
      1. [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)
      2. [Markdown Preview Enhanced](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced)
      3. [Markdown Plantuml Preview](https://marketplace.visualstudio.com/items?itemName=myml.vscode-markdown-plantuml-preview)
      4. [PlantUML](https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml)
5. [Obsidian](https://obsidian.md/) For long editing sessions, focused on contents, with a number of extensions for PlantUml, etc. and the [Longform](https://github.com/kevboh/longform) extension for organizing multi-part manuscripts.
6. For sharing/publishing, host an Mkdocs generated site in GithubPages.

## The Github pages publishing setup

Github actions are a very convenient way to publish html sites to github pages. To do that, the steps to follow are:

1. Enable Github Actions in the repository settings in `Settings->Actions->General`
2. Enable Github pages in the repository by going to `Settings->Pages` and selecting the Source to be `GitHub Actions`.
3. Create a github actions workflow in `.github/workflows` with the following content (see inline comments for clarifications):

{% raw %}

```yaml
---
# Pick your own name that is unique in your repo
name: mkdocs-publish
on: 
  push:
    branches:
      # or any branch you want
      - main
  # Convenient for testing
  workflow_dispatch:

# The GITHUB_TOKEN permissions to be able to write to the gh-pages environment.
permissions:
  contents: write
  pages: write
  id-token: write

jobs:
  # This job builds the docs and publishes them to a GHA artifact
  mkdocs-build:
    name: Build mkdocs
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      - name: Build Documents
        id: build-docs
        # See https://github.com/jmpicnic/actions-gen-mkdocs for details
        uses: jmpicnic/actions-gen-mkdocs@v1
        with:
          docs-dir: the-repo-subdirectory-for-the-documentation-root
          site-target-dir: the-subdirectory-where-the-html-will-be
          requirements-file-name: the-pip-freeze-requirements.txt
          mkdocs-file-name: the-mkdocs.yml-file-location
      - name: Upload Pages artifact
        uses: actions/upload-pages-artifact@v2 
        with:
          path: ${{ steps.build-docs.outputs.generated-site }}      
  deploy:
    # Add a dependency to the build job
    needs: mkdocs-build
    # Specify runner + deployment step
    runs-on: ubuntu-latest

  # Grant GITHUB_TOKEN the permissions required to make a Pages deployment
  # (this can be omitted if the permissions are at the top)
    permissions:
      pages: write      # to deploy to Pages
      id-token: write   # to verify the deployment originates from an appropriate source

    # Deploy to the github-pages environment
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}

    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2 # or the latest "vX.X.X" version tag for this action
```

{% endraw %}

## Additional notes

1. The public action [jmpicnic/actions-gen-mkdocs](https://github.com/jmpicnic/actions-gen-mkdocs) encapsulates the building of mkdocs with the tools needed to run latex and plantuml. You can also copy it and modify to your heart content.

2. The `requirements.txt` is dependent on the packages and extensions that you have for `mkdocs`. You can see an example in [this repository](https://github.com/jmpicnic/obsidian-docs/blob/main/requirements.txt)

3. Publishing to Medium and other formats is still a very manual process that involves merging multiple markdown files, using [pandoc](https://pandoc.org/) to create html or other formats and upload/import/cut-paste to the target system. Then do a manual editing pass. The longform extension in Obsidian and other mkdocs extensions hold promise to make it easier, but they will require more time.

4. Using Latex for authoring is still just a wish.