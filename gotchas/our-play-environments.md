## Overview

We have several environments online for people to use for testing, debugging, etc.:

* debug.dhis2.org is meant for devs
* verify.dhis2.org is meant for QA team (i.e. please consider it out-of-bounds!)
* empty.dhis2.org for testing with empty db (mainly for QA)

The idea is that you administer the instances, creating as necessary then cleaning up after yourself! Logs go to an ELK-stack server (logs.dhis2.org)
