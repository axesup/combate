## Problem

You made changes to the client that you want to test on live data on the server.

## Solution

Use `npm run proxy` instead of `npm run nodemon`. You will need to be running `npm run brunch watch` separately. You do not need MongoDB running locally in this case.

## Details

When running the dev environment as a proxy, all non-static file requests are proxied to CodeCombat's production servers. This way you may log into your live account and see how changes look without the hassle of importing or constructing a local version of the data.

Note that changes you make to the server will not be reflected in proxy mode; this is solely for strictly front-end development. Changes you make through the proxy will be reflected on [[https://codecombat.com]].