# WAR-file

#### Stable

URL structure: `/{version}.war`
                 
- https://releases.dhis2.org/2.32.0.war
- https://releases.dhis2.org/2.31.4.war

#### Canary

URL structure: `/canary/{branch}(-{date}).war`

- https://releases.dhis2.org/canary/master.war
- https://releases.dhis2.org/canary/2.32.war
- https://releases.dhis2.org/canary/2.32-20190523.war

Date is optional.

#### Development

URL structure: `/dev/{branch}.war`

- https://releases.dhis2.org/dev/2.31.war
- https://releases.dhis2.org/dev/2.32.war
- https://releases.dhis2.org/dev/master.war

#### Pull requests

URL structure: `/PR/{pull-id}.war`

- https://releases.dhis2.org/PR/3353.war
- https://releases.dhis2.org/PR/239.war

# Docker

### Base images

#### Release

Repo: `core`
Tag structure: `{version}`

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
