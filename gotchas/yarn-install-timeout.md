When running `yarn install` in projects which depend on very large packages Yarn hits the timeout limit and eventually throws the error `ESOCKETTIMEDOUT`.

```sh
yarn install

yarn install v1.13.0
[1/4] Resolving packages...
[2/4] Fetching packages...
info There appears to be trouble with your network connection. Retrying...
info There appears to be trouble with your network connection. Retrying...
info There appears to be trouble with your network connection. Retrying...
info There appears to be trouble with your network connection. Retrying...
error An unexpected error occurred: "<some package name>: ESOCKETTIMEDOUT".
info If you think this is a bug, please open a bug report with the information provided in "/home/varl/dev/dhis2/apps/dashboards-app/yarn-error.log".
info Visit https://yarnpkg.com/en/docs/cli/install for documentation about this command.
```

## Troubleshooting

It is helpful to run the `yarn install` command with the `--verbose` switch to get additional information as well.

```sh
yarn install --verbose

yarn install v1.13.0
verbose 0.568 Found configuration file "/home/varl/.yarnrc".
verbose 0.568 Checking for configuration file "/home/.yarnrc".
verbose 0.572 current time: 2019-03-15T07:25:03.674Z
[1/4] Resolving packages...
[2/4] Fetching packages...
verbose 13.542 Performing "GET" request to "https://registry.yarnpkg.com/material-ui/-/material-ui-0.20.2.tgz".
info There appears to be trouble with your network connection. Retrying...
verbose 13.638 Error: https://registry.yarnpkg.com/@dhis2/d2-i18n/-/d2-i18n-1.0.4.tgz: ESOCKETTIMEDOUT
    at ClientRequest.<anonymous> (/usr/share/yarn/lib/cli.js:130024:19)
    at Object.onceWrapper (events.js:277:13)
    at ClientRequest.emit (events.js:189:13)
    at TLSSocket.emitRequestTimeout (_http_client.js:662:40)
    at Object.onceWrapper (events.js:277:13)
    at TLSSocket.emit (events.js:189:13)
    at TLSSocket.Socket._onTimeout (net.js:443:8)
    at ontimeout (timers.js:436:11)
    at tryOnTimeout (timers.js:300:5)
    at listOnTimeout (timers.js:263:5)
error An unexpected error occurred: "https://registry.yarnpkg.com/@dhis2/d2-i18n/-/d2-i18n-1.0.4.tgz: ESOCKETTIMEDOUT".
info If you think this is a bug, please open a bug report with the information provided in "/home/varl/dev/dhis2/apps/dashboards-app/yarn-error.log".
info Visit https://yarnpkg.com/en/docs/cli/install for documentation about this command.
```

## Solution

Increasing the `network-timeout` for Yarn is one way to fix it. You can choose to increase the limit globally or per-project. I did it globally in the example below. The configuration option accepts milliseconds. Here I set it to 10 minutes for _**OVERKILL**_ 😎.

```sh
yarn config set network-timeout 600000 -g

yarn config v1.13.0
success Set "network-timeout" to "600000".
Done in 0.04s.
```

## Bonus solution

The only package I've seen this problem on is the [`material-design-icons`](https://www.npmjs.com/package/material-design-icons) package which has a ridiculous amount of files in a large package format. If you only need the iconfont, the [`material-design-icons-iconfont`](https://github.com/Jossef/material-design-icons-iconfont) works as a drop-in replacement and is a lot smaller (package-wise).

## Discussion

- [dhis2/notes](https://github.com/dhis2/notes/issues/29)
