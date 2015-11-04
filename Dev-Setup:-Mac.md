This tutorial requires you to have the [Xcode Developer Tools](http://itunes.apple.com/us/app/xcode/id497799835?ls=1&mt=12), and have installed the Xcode Command Line Tools (which can be found under the menu `Xcode -> Preferences -> Downloads`).

1. Make sure you have MongoDB and Node.js installed. Git comes with Xcode and Python 2.7 should already be installed.
    1. [MongoDB instructions here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-os-x/). We recommend using [Homebrew](http://brew.sh/).
    1. The [Node.js installer](https://nodejs.org/en/download/) is easy to use.
2. [Create a GitHub account](https://github.com/join) if you don't already have one.
3. [Set up Git on your computer](https://help.github.com/articles/set-up-git/) to allow your computer to speak to GitHub.
4. _(Optional)_ [Fork](https://github.com/codecombat/codecombat/fork) our CodeCombat repository if you wish to make changes.
5. Open a terminal and navigate to the folder you wish to install CodeCombat under.
6. Run `git clone https://github.com/$GITHUB_USERNAME/codecombat.git && cd codecombat`
7. Run `npm install`. This will install npm and bower dependencies, as well as building the static files.
8. Start up and setup [MongoDB](#installing-the-database).
9. Run `npm start` to just preview the site, or `npm run dev` to live code.
10. Visit [http://localhost:3000](http://localhost:3000) to see your CodeCombat development environment!

### Installing the Database

Download the [CodeCombat database](http://analytics.codecombat.com:8080/dump.tar.gz) (updated every 10 minutes) and import it to your locally running database with the following commands:

1. Make sure the database is running on your computer.
1. Uncompress the file with `tar xzvf [filename]`).
1. Run `mongorestore --drop [path to dump]` if mongorestore is in your path. If mongorestore is not in your path, run `[path to where you downloaded MongoDB]/mongorestore --drop [path to dump]`.

When downloading a new dump to keep the database up-to-date, use `mongorestore --drop [path to dump]` to clear out all old data (including any local data you have created) and replace with just the new data.

*If you see an error like `no reachable servers` when running mongorestore, and mongo is running, try adding `--host=127.0.0.1` to the command line options.*