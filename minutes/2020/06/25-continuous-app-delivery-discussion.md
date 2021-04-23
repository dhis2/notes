# 2020-06-25, Continuous App Delivery

## Attending

Austin, Erik, Lars, Stian, Zubair, Birk

## Context

The meeting was scheduled to identify and propose solutions for features that we need to support continuous app delivery for core applications.  

Link to related issue and agenda: https://github.com/dhis2/notes/issues/114


## Support multiple versions of the same app

- This was top priority before the meeting, as we wanted to have admins test apps on the instance before installing a new versions.
- People are accustomed to have a staging server, so the need for this is not as urgent.

**Conclusion:**

- This has been postponed for now as there are more urgent issues.
- A nice to have down the line.


## Support for overriding core apps by custom apps

- To be able to update core apps we need them to install them as a "custom app".
- The proposed solution was to have the server check for a custom app of the same name, and use that if it exists.
- We need to support "old" urls (eg. "dhis-web-dashboard") for backwards compatability, these should redirect to a possibly new url (eg. "/apps")
- The issue of collisions of app names were brought up, as users could unintentionally install apps by the same name of the core app, thus overriding it.
- Installing apps should be a locked down permission, and admins should be aware of conflicts.
- We could potentially notify the user the first time a "custom core app" is installed.

**Conclusion:**

- Going forward with implementation of overrides of core apps.
- Jira issue for this: https://jira.dhis2.org/browse/DHIS2-9092

## Re-introduce the proxy through core to App Hub

- The proxy was removed mostly due to the ease of introducing new APIs between the App Hub and management app. 
- Concerns were raised of the removal of the proxy to App Hub.
    - Air gaps, as clients may not have internet access or have poor internet connections.
- Security needs to be considered
- When reintroducing, we need to implement new endpoints like "/channels", and verify that all endpoints are working. 
- We do not want App Hub updates to be delayed by core releases.
- Proposed solution: A wildcard proxy that forwards requests from eg. "/api/apphub/*" to "https://apps.dhis2.org/api/*"

**Conclusion:**

- Re-introduce the proxy. Jira issue: https://jira.dhis2.org/browse/DHIS2-9093
- Research security risks and (hopefully) implement a pass-through proxy to the App Hub.
- Security engineer (Morten S) likely needs to investigate application management security
    - Verify that the server validates the CA-certificate of App Hub. 
    - Investigate vulnerability surface area of wildcard proxy
    - Other: mitigate risks of MITM attacks of intalled apps with eg. hashes of installed apps

## Versioning and release channels

- Need a way to know what the latest version is
    - To support notifications when a new version is released
- This is currently hard, as we do not enforce semantic versioning, and can thus not assume anything about the version-string.
- Cannot use date of upload either, as previous versions may be updated after a higher version.
- Currently, release channels may have multiple versions. Austin pointed out that we could follow the "npm" model of tags, and restrict this to one version per channel, so that "stable" always points to one versions.
    - There's some complexity with this regarding supported DHIS2 versions.
    - There can potentially be overlap of supported DHIS2-versions by different app-versions

**Conclusions:**

- Needs further discussion


## Security of app installation

- This has been discussed a bit before, and we did not go into to much detail.
- Need to consider the security of verifying the app before installing it on the server.
- A proposed lightweight solution is to publish a hash or fingerprint on app hub, and have the user manually input this hash when installing the app. The server can then compute the hash of the installed app, and that it matches the given hash.
- Needs further discussion


## App name translations

- Cannot translate title and application names of third party apps.
- Need to research how this can be integrated to other i18n services.
- May be able to have an array of translations in the Manifest.
- Briefly discussed, no clear solutions as this point
