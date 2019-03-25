### Installation Guides

Our installation guides are split into per-OS guides which will give you step-by-step instructions on how to get your development environment set up. Aimed at beginners.

* **[Linux Setup](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-Linux)**
* **[Windows Setup](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-Windows)**
* **[Mac Setup](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-Mac)**

### General Setup Instructions
#### For power users who know what they're doing

This is the general overview for what you need in order to set up the development environment. For more specific instructions with recommended paths to success, see the installation guides listed above.

1. Install [Node.js 8](https://nodejs.org/en/download/), npm 6.4.1, and [Git](https://desktop.github.com/)
1. `git clone` [this repository](https://github.com/codecombat/codecombat).
1. `npm install` in the repository's root directory.

### Running The Environment

After installation, you can run your development environment as a proxy to CodeCombat's production servers. Enter the following commands in separate terminals:

1. `npm run proxy` (routes all server calls to CodeCombat's production servers)
1. `npm run webpack -- --watch` (compiles app files to public folder continuously, refreshing the browser window on changes)

If you don't need webpack to restart on changes or build files, you can simply run `npm run proxy` instead.

***

### Issues

There's a [list of dev setup issues and workarounds here](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-Issues). If you have a problem and we figure out how to get around it, please help by updating this page.

### Working in the environment

You don't need any particular IDE to work with CodeCombat. Scott uses WebStorm, Nick uses Emacs, and George uses Sublime Text, so already the most important parts are IDE-agnostic. We need help making it friendly for Linux and Windows, though, since we all develop on Mac.

Whichever editor you use, **be sure to disable removing trailing whitespace from files**, at least for jade files. Sometimes (although rarely) these have significant whitespace.

### Live-coding

If Webpack is running and you make code changes, Webpack will reload the page automatically. So open the page you are working on in your browser, make changes in your editor, save, and the page will refresh so you can see the changes. Try to make whatever you're working on be the first thing you see when you open the page, so you don't have to lose focus on your editor while iterating.

### Third Party Services

API services we use such as MailChimp will not be accessible unless you have an API key. Generally you shouldn't need them to work on the site, but if you do, then let us know.