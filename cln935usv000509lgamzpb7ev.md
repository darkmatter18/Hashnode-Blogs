---
title: "Git Workflow for Enterprise Application"
datePublished: Fri Sep 29 2023 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: cln935usv000509lgamzpb7ev
slug: git-workflow
tags: github, git, developer, devops

---

# Introduction

If I mention a tool revolutionizing, the software development industry, then [GIT](https://git-scm.com/) will be Number One on the list. But as Uncle Sam told us, “**Great power comes with great responsibility**”.

So like any other tool, we need to learn how we can use GIT in our day-to-day software development life-cycle so that we can use it optimally and we can get the most features out of it.

Here in this story, I will describe an end-to-end GIT workflow to manage Enterprise applications and libraries with the power of GIT and version control.

# Why should you use the model?

The following workflow is created by considering the following facts:

1. The workflow must be flexible and easy to use.
    
2. The workflow must not take very long steps to implement in your existing ecosystem.
    
3. The workflow should use all good features like ***merge***, ***rebase***, ***pull request***, and ***branching***.
    
4. The *production* and the *staging* should be on separate branches for optimal tracking of the releases.
    
5. The workflow also features **hot fixes** for production *to support agility* and separate release and feature branches in place.
    
6. The workflow is also built considering the modern-day **DevOps** ecosystem and *continuous integration and continuous deployment pipelines* ***(CI-CD)***.
    

# Workflow Model

## The Main Branches

![Main branches](https://cdn.hashnode.com/res/hashnode/image/upload/v1696249077403/7bd247a0-31b5-4fad-b8ab-c0002d201f2f.png align="center")

The model suggests considering Git branching strategies. It uses separate branches for the production and staging environment. The central repo holds two main branches with an infinite lifetime:

### 1\. master

We consider `origin/master` to be the main branch where the source code of `HEAD` always reflects a production-ready state.

Therefore, each time changes are merged back into the `master`, this is a new production release *by definition*.

### 2\. develop

Parallel to the `master` branch, another branch exists called `develop`. We consider `origin/develop` to be the main branch where the source code of `HEAD` always reflects a state with the latest delivered development changes for the next release and reflects the staging environment.

When the source code in the `develop` branch reaches a stable point and is ready to be released, all of the changes should be merged back into `master` somehow and then tagged with a release number.

## The Supporting Branches

In addition to the primary branches, `master` and `develop`, our development approach incorporates several **auxiliary branches**.

These auxiliary branches serve multiple purposes, such as facilitating *concurrent development among team members*, *simplifying feature tracking*, *preparing for production releases*, and *providing swift solutions for live production issues*. Unlike the main branches, these auxiliary branches are temporary in nature and are eventually slated for removal.

The different types of branches we may use are:

* Feature branches
    
* Release branches
    
* Hotfix branches
    

### Feature Branches

![Feature Branches](https://cdn.hashnode.com/res/hashnode/image/upload/v1696251336027/63a63cc0-506c-47eb-ad57-87541ef0fb5f.png align="center")

Feature branches, also known as topic branches, are employed for the creation of new features intended for inclusion in either upcoming or more distant future releases.

The core concept of a `feature` branch is its **lifespan**, which extends only for the duration of the feature's development, and it is subsequently removed once the feature is completed.

* Feature Branches are branched off from: `develop`
    
* Feature Branches are merged back into: `develop`
    
* Branch naming convention:
    
    1. starts with `feature/`
        
    2. anything except `master`, `develop`, `release/*`*, or* `hotfix/*`
        
    3. Example: `feature/a`, `feature/b`
        

#### Create a feature branch

```bash
git checkout -b feature/foo develop
# This will create a feature branch named feature/foo from develop
```

#### Incorporating a finished feature on the develop

```bash
git checkout develop
# This will checkout/open the develop branch
git pull
# Let's pull the latest changes from origin
git merge --no-ff feature/foo
# This will merge feature/foo into develop
git branch -d feature/foo
# Delete our short lived feature branch
git push origin develop
# Push our updated develop branch
```

The `--no-ff` flag causes the merge to always create a new commit object, even if the merge could be performed with a fast-forward. This avoids losing information about the historical existence of a feature branch and groups together all commits that together added the feature. [Learn More](https://hackr.io/blog/difference-between-git-merge-and-git-merge-no-ff)

### Release Branches

Release branches support the preparation of a new production release.

The optimal time to create a new release branch from the develop branch is when the develop branch accurately represents the desired state for the upcoming release.

![Release Branch](https://cdn.hashnode.com/res/hashnode/image/upload/v1696257534331/10a5abf0-70da-478c-b6ca-058d6da08e1c.png align="center")

* Release Branches are branched off from: `develop`
    
* Release Branches are merged back into: `develop` and `master`.
    
* Branch naming convention:
    
    1. starts with `release/`
        
    2. anything except `master`, `develop`, `feature/*`*, or* `hotfix/*`
        
    3. Example: `release/v1.0.0`, `release/v1.1.0`
        

#### Create a release branch

```bash
git checkout -b release/v1.2.0 develop
# Switched to a new branch "release-1.2"
./bump-version.sh 1.2.0
# A special file to update the version in the files
git commit -a -m "Chore: v1.2.0"
# Commit for v1.2.0
```

##### What is **bump-version.sh**?

The `bump-version.sh` is a specific file designed to facilitate version updates within our source code. It could be used to update version information in different configuration files or metadata, such as:

1. **Python (setup.py):** You can utilize `bump-version.sh` to increment the version in a Python project's **setup.py** file, which is often used for packaging and distribution.
    
2. **Java (pom.xml):** In a Java project managed by Maven, the script could be used to update the version defined in the **pom.xml** file, a crucial part of Maven-based builds.
    
3. **Ruby (Gemfile):** For Ruby applications managed with Bundler, you might employ the script to adjust the version specified in the **Gemfile**.
    
4. **C# (.csproj):** In a C#/.NET project, it could be used to modify the version in the project's **.csproj** file, which is essential for building and packaging.
    
5. **Docker (Dockerfile):** For containerized applications, the script could update version labels in the Dockerfile, ensuring version consistency across containers.
    
6. **Frontend (package.json, manifest.json):** In web development, it can also be applied to update version information in frontend files like "package.json" (for Node.js projects) or "manifest.json" (for web applications).
    

The **bump-version.sh** file serves as a versatile tool for maintaining version coherence in various development contexts.

Here is an example of **bump-version.sh** file in the context of the package.json file

```bash
#!/bin/bash

# Check if an argument (new version) is provided
if [ $# -eq 0 ]; then
    echo "Usage: ./bump-version.sh <new_version>"
    exit 1
fi

# Define the new version
new_version="$1"

# Update the "version" field in package.json
jq --arg new_version "$new_version" '.version = $new_version' package.json > temp.json && mv temp.json package.json

echo "Version updated to $new_version in package.json"
```

#### Incorporating the release branch

##### Releasing into the master

```bash
git checkout master
# This will checkout/open the master branch
git merge --no-ff release/v1.2.0
# Merge the release branch into master
git tag -a v1.2.0
# Create a tag for v1.2.0 in the master
```

##### Merging back to develop

To keep the changes made in the release branch, we need to merge those back into the `develop` branch, though. In Git:

```bash
git checkout develop
# This will checkout/open the develop branch
git merge --no-ff release/v1.2.0
# Merge the release branch into develop
```

Now we are really done and the release branch may be removed, since we don’t need it anymore:

```bash
git branch -d release/v1.2.0
# Delete our short lived release branch
```

### Hotfix Branches

`Hotfix` branches share similarities with `release` branches, as they also serve the purpose of *preparing for a new production release*, albeit under unplanned circumstances.

They emerge as a response to the urgent need to address an unforeseen issue in a live production version. In situations where a critical bug in a production version demands immediate attention, a hotfix branch can be created by branching off from the corresponding tag on the master branch, which designates the production version.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696260466885/0b5028e6-fc08-4ce4-a5e1-8fb0adc99010.png align="center")

* Hotfix Branches are branched off from: `master`
    
* Hotfix Branches are merged back into: `develop` and `master`.
    
* Branch naming convention:
    
    1. starts with `hotfix/`
        
    2. The name will contain the tag from which you are branching off.
        
    3. anything except `master`, `develop`, `feature/*`*, or* `release/*`
        
    4. Example: `hotfix/v1.0.0`, `hotfix/v1.1.0`
        

#### Create a hotfix branch

```bash
git checkout -b hotfix/v1.2.0 develop
# Switched to a new branch "release-1.2"
```

Now fix the bug(s) and commit the fix in one or more separate commits.

```bash
./bump-version.sh 1.2.1
# A special file to update the version in the files
git commit -a -m "Chore: v1.2.1"
# Commit for v1.2.0
```

#### Incorporating the hotfix

##### Releasing into the master

```bash
git checkout master
# This will checkout/open the master branch
git merge --no-ff hotfix/v1.2.1
# Merge the release branch into master
git tag -a v1.2.1
# Create a tag for v1.2.1 in the master
```

##### Merging back to develop

To keep the changes made in the release branch, we need to merge those back into the `develop` branch, though. In Git:

```bash
git checkout develop
# This will checkout/open the develop branch
git merge --no-ff hotfix/v1.2.1
# Merge the hotfix branch into develop
```

Now we are really done and the release branch may be removed, since we don’t need it anymore:

```bash
git branch -d hotfix/v1.2.1
# Delete our short lived hotfix branch
```

## The Big picture

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696262869173/b5012e5c-11ad-401f-9c6a-7f5c0981f5bc.png align="center")