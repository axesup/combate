# Before You Start

For more information about the tools being installed and what they do, see our [[third party software and services]] page.

Most steps take place in the Terminal, which is in `Applications > Utilities`, or can be found with Spotlight Search. When you run a command and it doesn't end, and you want it to end, use the shortcut `Ctrl-C`.

These steps are our **recommended approach** to setting up CodeCombat's development environment. As long as you cover the [General Setup Instructions](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-General-Information#general-setup-instructions), you can install these tools however you prefer.

# Setup Steps

1. **[Install Xcode](http://itunes.apple.com/us/app/xcode/id497799835?ls=1&mt=12).**
1. **Install Xcode Command Line Tools.** Open XCode and go through menus `Xcode -> Preferences -> Downloads`. This will install Git and provide the command line tools for building the development environment.
1. **[Install Homebrew](http://brew.sh/).** This will help install MongoDB, CodeCombat's database.
1. **[Install MongoDB with HomeBrew]((https://docs.mongodb.org/manual/tutorial/install-mongodb-on-os-x/)).** `brew install mongodb`.
1. **[Install NVM](https://github.com/creationix/nvm#install-script)**. This will help in installing Node, the server and NPM, the Node package manager. There are multiple ways to install Node, so if you install the latest Stable version some other way, skip down to setting up GitHub.
1. **Install Node and NPM with NVM.** As of writing, we're using Node 5.1.1, so the command is `nvm install 5.1.1`. Check the node version we're using in [package.json](https://github.com/codecombat/codecombat/blob/master/package.json).
1. **Use Node 5 (Stable) By Default**. `nvm alias default 5.1.1`. This way Node 5.1.1 is used for every new terminal. Otherwise you'll need to run `nvm use 5.1.1` before running any dev environment commands.
1. **[Create an account on GitHub](https://github.com/join).** This is where our code repository is hosted.
1. **[Configure Git to connect with your GitHub account](https://help.github.com/articles/set-up-git/).**
1. **[Clone the CodeCombat repository](https://help.github.com/articles/cloning-a-repository/).** This will copy our source code and all its history to your computer to be run and modified.
1. **Install and compile CodeCombat source files.** Navigate into the folder where you downloaded the CodeCombat repository and run `npm install`. This will install npm and bower (client library) dependencies, as well as building the public directory, which is what the server... serves.
1. **Add data to MongoDB.** [See below](#installing-the-database).
1. **[Run the dev environment](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-General-Information#running-the-environment)**.
1. **Visit [[http://localhost:3000/]]** to see your CodeCombat development environment!

### Installing the Database

Download the [CodeCombat database](http://analytics.codecombat.com:8080/dump.tar.gz) (updated every 10 minutes) and import it to your locally running database:

1. **Start MongoDB**. From the codecombat folder, run `./bin/coco-mongodb`. You should now be able to, from another terminal, run `mongo` and connect.
1. **Uncompress the dump**. Open a new terminal and navigate to the folder where you downloaded the dump.tar.gz file and run `tar xzvf [filename]`. This will create a `dump` folder.
1. **Load the uncompressed dump folder into the database**. Run `mongorestore --drop [path to dump]`.

Following these same steps will also clear out all old data (including any local data you have created) and replace it with just the new data.

*If you see an error like `no reachable servers` when running mongorestore, and mongo is running, try adding `--host=127.0.0.1` to the command line options.*

*In version 3.0.7 of mongoDB is a bug in mongorestore. If you see an error like `Failed: restore error: [some file name]: error restoring from dump/[some file name]: insertion error: EOF` when running mongorestore, then try adding `--batchSize=100` to the command. (try 1000, or 100, or even smaller)* [see here for a discussion on that](https://jira.mongodb.org/browse/TOOLS-939)