---
authors:
  - mpinilla
categories:
  - Software Practice
date: 2023-12-13
draft: false
title: Publish to GH Packages from Sbt without plugins
author: Miguel Pinilla
Copyright: (c) Miguel Pinilla, All rights reserved
License: "This work is licensed under the Creative Commons License CC BY-NC-SA 4.0: https://creativecommons.org/licenses/by-nc-sa/4.0/"
email: miguel.pinilla@saldubatech.com
share: "true"
---

Use a zero cost Maven repository to publish my hobby project packages and do that from Scala/sbt without needing additional plugins.

<!-- end_excerpt -->

!!! note
    These are not step by step instructions, they are a summary of the notes I took when setting up my environment. To follow them, you should be familiar with your OS (mine is MacOS), Python, Pip, Mkdocs and Github Actions

## The Quick Solution

### Create a Repository in Github

This repository will be the *host* for the maven registry.

It can be under your user or an organization that you have enough permissions.

### Create a Personal Access Token

With `read` and `write` access to the repository you just created.

Configure that access token in an environment variable of the system that will run sbt. This is in your local machine or a a Secret in a Git Hub action that feeds an environment variable.

### Put everything together in `build.sbt`

You will need:

1. Your github user name: `<user>`
2. The name of the Token Environment variable: `<TOKEN_VAR>`
3. The name of the repository:
   1. User or organization: `<org>`
   2. Repo Name: `<repo>`

Note that the values of `ghRepoName` and `repoHost` below should **NOT** be changed.

```sbt
enablePlugins (
  JavaAppPackaging
)

val user = <user>
val repo = <repo>
val org = <org>
val tk_var = <TOKEN_VAR>

val ghRepoName = "GitHub Package Registry"
val repoHost = "maven.pkg.github.com"

sys.env.get(tk_var).map{ 
    ghTk => Credentials(ghRepoName, repoHost, user, ghTk)
  }.match  {
    case None => Nil
    case Some(cred) => credentials += cred
  }
val packagesRepo = s"https://$repoHost/$user/$repo"

publishTo := { Some(new DependencyBuilders{}).toRepositoryName(ghRepoName).at(packagesRepo) }
```

### Test and execute

```bash
% sbt publishLocal
```

```bash
% sbt publish
```
