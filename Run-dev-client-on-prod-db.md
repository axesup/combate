## Problem

You made changes to the client that you want to test on live data on the server.

## Solution

Use `npm run proxy` instead of `npm run nodemon`. You will need to be running `npm run brunch watch` separately.

## Details

When running the dev environment as a proxy, all non-static file requests are proxied to CodeCombat's production servers. While the changes to the server will not be reflected while running the dev environment as a proxy, you can still test new or changed pages. You may log into your live account and see how things look without copying data over to your local mongodb. You don't even need to have mongodb running or installed to run the proxy!