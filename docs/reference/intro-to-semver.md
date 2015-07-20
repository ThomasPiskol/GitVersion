# Intro to SemVer
For the official Semantic Version docs head to [semver.org](http://semver.org), this is a quick guide for people  getting started and how SemVer is used in GitVersion.

## Why SemVer?
Quick reason is to solve two problems, Version Lock and Version promiscuity. To explain these things lets imagine the scenario where I am building an app which authenticates with facebook (v1.0.0) and twitter (v1.0.0). Both the facebook and twitter libraries use a json library (v1.0.0).

Version lock is when we rely on absolute versions, both **FacebookApi** and **TwitterApi** rely on _v1.0.0_ of **JsonLibrary**. **JsonLibrary** _v1.1.0_ comes out and **FacebookApi** decides to upgrade. If our dependency management relies on exact versions we cannot upgrade our application to use **FacebookApi** because **TwitterApi** references _v1.0.0_. The only way we can upgrade is if **TwitterApi** also upgrades to _v1.1.0_ of **JsonLibrary**.

Version Promiscuity is the opposite problem, **JsonLibrary** releases _v1.1.0_ with some breaking changes then we will just upgrade an **TwitterApi** will break unexpectedly.

SemVer introduces conventions about breaking changes into our version numbers so we can safely upgrade dependencies without fear of unexpected breaking changes while still allowing us to upgrade downstream libraries to get new features and bug fixes. The convention is quite simple.

{major}.{minor}.{patch}-{tag}+{buildmetadata}  
{major} = Only incremented if the release has breaking changes (includes bug fixes which have breaking behavioural changes
{minor} = Incremented if the release has new non-breaking features
{patch} = Incremented if the release only contains non-breaking bug fixes
{tag} = Optional -{tag} denotes a pre-release of the version preceeding
{buildmetadata} = Options +{buildmetadata} contains additional information about the version, but DOES NOT AFFECT the semantic version preceding it.

Only one number should be incremented per release, and all lower parts should be reset to 0 (if major is incrememented then minor and patch should become 0).

For a more complete explaination checkout [semver.org](http://semver.org) which is the official spec. Remember this is a breif introduction and does not cover all parts of semantic versioning, just the important parts to get started.

## SemVer in GitVersion
GitVersion makes it easy to follow semantic versioning in your library by automatically calculating the next semantic version which your library/application is likely to use. In GitFlow the develop branch will bump the *minor* when master is tagged, while GitHubFlow will bump the *patch*.

Because one side does not always fit all, GitVersion provides many [Variables](../more-info/variables.md) for you to use which contain different variations of the version. For example SemVer will be in the format {major}.{minor}.{patch}-{tag}, but FullSemVer will also include build metadata: {major}.{minor}.{patch}-{tag}+{buildmetadata}