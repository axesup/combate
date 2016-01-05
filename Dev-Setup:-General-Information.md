### General Instructions

1. Install [MongoDB](https://www.mongodb.org/downloads#production), [Node.js](https://nodejs.org/en/download/), [Git](https://desktop.github.com/), [Python 2.7](https://www.python.org/download/releases/2.7/)
1. `git clone`
1. `npm install`
1. Start MongoDB and import the [database dump](#database)
1. Run `npm run dev` (live coding) or `npm start` (preview)

***

### Installation Guides

Our installation guides are split into per-OS guides.

* **[Linux Setup](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-Linux)**
* **[Windows Setup](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-Windows)**
* **[Mac Setup](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-Mac)**
* **[Vagrant Setup](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-Vagrant)** (Experimental, all OS)

### Issues

There's a [list of dev setup issues and workarounds here](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-Issues). If you have a problem and we figure out how to get around it, please help by updating this page.

### Working in the environment

You don't need any particular IDE to work with CodeCombat. Scott uses WebStorm, Nick uses Emacs, and George uses Sublime Text, so already the most important parts are IDE-agnostic. We need help making it friendly for Linux and Windows, though, since we all develop on Mac.

### Live-coding

If Brunch is running and you make code changes, Brunch will reload the page automatically. So open the page you are working on in your browser, make changes in your editor, save, and the page will refresh so you can see the changes. Try to make whatever you're working on be the first thing you see when you open the page, so you don't have to lose focus on your editor while iterating. If you edit just the styling, Brunch will apply the new styling without refreshing.

### Database

The link to the database dump is: http://analytics.codecombat.com:8080/dump.tar.gz

To import the database into MongoDB, unpack the archive and run: `mongorestore --drop /path/to/dump`

When building in the dev environment, you have a filtered copy of the live database with just the publicly available data. It may look like what you'll find on the site, but changes you make won't show up on the site. To keep the database dump small, we only include a handful of testing levels, so the first two levels show up, but not the third. If you need to work on a specific level, let us know and we can provide you with more levels.

Currently, there's no easy way to transfer data you make on your dev environment back to production, so be sure to build levels you want to share on [direct.codecombat.com](http://direct.codecombat.com/editor/level), not on the dev server.

### Third Party Services

API services we use such as MailChimp will not be accessible unless you have an API key. Generally you shouldn't need them to work on the site, but if you do, then let us know.