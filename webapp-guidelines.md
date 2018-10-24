# Starting a new webapps

# Checklist

- [ ] Source code dir is `{repo}/src`
- [ ] Build dir is `${repo}/build`

## Code style

We use:

- [Create React App](https://github.com/facebook/create-react-app) to
  get a solid foundation for our web applications up and running.

- [code-style](https://github.com/dhis2/code-style) to ensure
  that we have code formatted in an uniform way.

- [deploy-build](https://github.com/dhis2/deploy-build) to deploy
  per-commit builds to a GitHub repo, which can be installed using
  NPM/Yarn.

- [d2-i18n](https://github.com/dhis2/d2-i18n) for internationalisation
  of our applications.

- Yarn for normal operation, NPM for scripts.

## Mono repos

- [packages](https://github.com/dhis2/packages) to manage our packages
  for local development (lerna alternative).

## UI

- [d2-ui](https://github.com/dhis2/d2-ui)
