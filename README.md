# Documentation

Every app has its own README which should include most info you need. We
also have an online resource for documentation on dhis2.github.io.

## Links

- [https://dhis2.github.io/](https://dhis2.github.io/)

## Issue tracking

### Functional

- [JIRA](http://jira.dhis2.org/)

### Technical

- Every app has its own issue tracker on Github where technical issues
  are documented.

# Shared libraries

We have a set of shared libraries which should be used in webapps to
standardise the way we interact with the DHIS2 instances.

- [d2](https://github.com/dhis2/d2)
- [d2-ui](https://github.com/dhis2/d2-ui)

# Code convention plugins

- [eslint-config-dhis2](https://github.com/dhis2/eslint-config-dhis2)
- editorconfig (per project)

# A new frontend app

- Use [create-react-app](https://github.com/dhis2/eslint-config-dhis2)
  as a starting point

# Way of Work

## Cheatsheet

1. clone your repo
2. checkout a new branch for the work you are going to do
3. do some changes
4. commit
5. repeat 3-4
6. open a pull request
7. ask someone on slack #frontend if they can have a look
8. merge PR
8. a. some apps require that you deploy now
8. b. for other apps you are done now

## Deployment

There are multiple meanings to "deploy" within the DHIS2 ecosystem.

### to NPM

On one hand, when talking about d2 and d2-ui a deployment means pushing
a new version to NPM and a new tag to Github.

### to DHIS2

On the other hand, most apps we build need to be deployed to a DHIS2
instance.

Core applications, like the maintenance-app, are bundled with the DHIS2
WAR-file in each release and shipped as the "core" application suite.

This way of shipping core-apps is being phased out, but as of 2.29 it is
still the primary way of shipping core applications.

## Versioning

The basic principle is to follow semver (major.minor.patch).

- Major is used to track against the DHIS2 version (e.g. 28 for DHIS2 version 2.28)
- Minor for marking breaking changes
- Patch is for fixes and patches

**N.B. Check the README for the instructions for your specific app**

