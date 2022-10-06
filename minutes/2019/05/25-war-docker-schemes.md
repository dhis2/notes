# Name scheme for `WAR`-files and Docker images

> **This scheme is now maintained here!**:https://github.com/dhis2/operations-handbook/blob/master/releases/war_docker_schemes.md

## `WAR`-file

#### Stable

URL structure: `{version}/dhis2-stable-{version}.war`
                 
- https://releases.dhis2.org/2.32/dhis2-stable-2.32.0.war
- https://releases.dhis2.org/2.31/dhis2-stable-2.31.4.war
additionally,
- https://releases.dhis2.org/2.32/dhis2-stable-latest.war  <-- same as the last 2.32 patch number
- https://releases.dhis2.org/2.31/dhis2-stable-latest.war  <-- same as the last 2.31 patch number

#### Canary

URL structure: `{version}/canary/dhis2-canary-{branch}(-{date}).war`

- https://releases.dhis2.org/master/canary/dhis2-canary-master.war  <-- the latest canary build
- https://releases.dhis2.org/2.32/canary/dhis2-canary-2.32.war  <-- the latest canary build
- https://releases.dhis2.org/2.32/canary/dhis2-canary-2.32-20190523.war  <-- a specific build

Date is optional, for builds that will be kept for a period.

#### Development

URL structure: `{version}/dev/dhis2-dev-{branch}.war`

- https://releases.dhis2.org/2.31/dev/dhis2-dev-2.31.war
- https://releases.dhis2.org/2.32/dev/dhis2-dev-2.32.war
- https://releases.dhis2.org/master/dev/dhis2-dev-master.war

#### Pull requests

URL structure: `/pr/dhis2-pr-{pull-id}.war`

- https://releases.dhis2.org/pr/dhis2-pr-3353.war
- https://releases.dhis2.org/pr/dhis2-pr-239.war

## Docker

### Base images

#### Stable

Repo: `core`
Tag structure: `{version}(-{variant})`

- `dhis2/core:latest`
- `dhis2/core:2.32.0`
- `dhis2/core:2.31.3`

#### Canary

Repo: `core-canary`
Tag structure: `{branch}(-{date})(-{variant})`

- `dhis2/core-canary:master`
- `dhis2/core-canary:2.32`
- `dhis2/core-canary:2.32-20190522`
- `dhis2/core-canary:2.31-20190522`
- `dhis2/core-canary:master-20190522`

#### Development

Repo: `core-dev`
Tag structure: `{branch}(-{variant})`

- `dhis2/core-dev:master`
- `dhis2/core-dev:2.32`
- `dhis2/core-dev:2.31`

#### Pull requests

Repo: `core-pr`
Tag structure: `{pull-id}`

For PR images we can use the pull request id from GitHub:

- `dhis2/core-pr:123`
- `dhis2/core-pr:234`

### Variants

The `(-{variant})` means it is optional, but can be appended to the tag.

Multiple variants can be used, e.g. `(-{variant})(-{variant})`.

- `dhis2/core:2.32.0-tomcat9`
- `dhis2/core:2.32.0-alpine`
- `dhis2/core:2.32.0-tomcat9-alpine`
