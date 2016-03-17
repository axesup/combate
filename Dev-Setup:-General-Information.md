### Installation Guides

Our installation guides are split into per-OS guides which will give you step-by-step instructions on how to get your development environment set up. Aimed at beginners.

* **[Linux Setup](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-Linux)**
* **[Windows Setup](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-Windows)**
* **[Mac Setup](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-Mac)**
* **[Vagrant Setup](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-Vagrant)** (Experimental, all OS)

### General Setup Instructions
#### For power users who know what they're doing

This is the general overview for what you need in order to set up the development environment. For more specific instructions with recommended paths to success, see the installation guides listed above.

1. Install [MongoDB](https://www.mongodb.org/downloads#production), [Node.js **Stable** version](https://nodejs.org/en/download/), [Git](https://desktop.github.com/), and [Python 2.7](https://www.python.org/download/releases/2.7/)
1. `git clone` this repository.
1. `npm install` in the repository's root directory.
1. Start MongoDB and import the [database dump](#database)

### Running The Environment

After installation, to run the site locally, enter the following commands in separate terminals:

1. `./bin/coco-mongodb` (runs the MongoDB server)
1. `npm run nodemon` (runs the server, automatically restarting on server-side changes)
1. `npm run brunch watch` (compiles app files to public folder continuously, refreshing the browser window on changes)

You can also use the command `npm run dev` to both run brunch and the server in one terminal. If you don't need nodemon or brunch to restart on changes or build files, you can simply run `npm run start` instead.

***

### Issues

There's a [list of dev setup issues and workarounds here](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-Issues). If you have a problem and we figure out how to get around it, please help by updating this page.

### Working in the environment

You don't need any particular IDE to work with CodeCombat. Scott uses WebStorm, Nick uses Emacs, and George uses Sublime Text, so already the most important parts are IDE-agnostic. We need help making it friendly for Linux and Windows, though, since we all develop on Mac.

Whichever editor you use, **be sure to disable removing trailing whitespace from files**, at least for jade files. Sometimes (although rarely) these have significant whitespace.

### Live-coding

If Brunch is running and you make code changes, Brunch will reload the page automatically. So open the page you are working on in your browser, make changes in your editor, save, and the page will refresh so you can see the changes. Try to make whatever you're working on be the first thing you see when you open the page, so you don't have to lose focus on your editor while iterating. If you edit just the styling, Brunch will apply the new styling without refreshing.

### Database

The link to the database dump is: http://analytics.codecombat.com:8080/dump.tar.gz

To import the database into MongoDB, unpack the archive and run: `mongorestore --drop /path/to/dump`

When building in the dev environment, you have a filtered copy of the live database with just the publicly available data. It may look like what you'll find on the site, but changes you make won't show up on the site. To keep the database dump small, we only include a handful of testing levels, so the first two levels show up, but not the third. If you need to work on a specific level, let us know and we can provide you with more levels.

Currently, there's no easy way to transfer data you make on your dev environment back to production, so be sure to build levels you want to share on [direct.codecombat.com](http://direct.codecombat.com/editor/level), not on the dev server.

### Third Party Services

API services we use such as MailChimp will not be accessible unless you have an API key. Generally you shouldn't need them to work on the site, but if you do, then let us know.