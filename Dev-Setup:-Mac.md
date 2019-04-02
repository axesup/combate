# Before You Start

For more information about the tools being installed and what they do, see our [[third party software and services]] page.

Most steps take place in the Terminal, which is in `Applications > Utilities`, or can be found with Spotlight Search. When you run a command and it doesn't end, and you want it to end, use the shortcut `Ctrl-C`.

These steps are our **recommended approach** to setting up CodeCombat's development environment. As long as you cover the [General Setup Instructions](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-General-Information#general-setup-instructions), you can install these tools however you prefer.

# Setup Steps

1. **[Install Xcode](http://itunes.apple.com/us/app/xcode/id497799835?ls=1&mt=12).**
1. **Install Xcode Command Line Tools.** Open XCode and go through menus `Xcode -> Preferences -> Downloads`. This will install Git and provide the command line tools for building the development environment.
1. **[Install NVM](https://github.com/creationix/nvm#install-script)**. This will help in installing Node, and NPM, the Node package manager. There are multiple ways to install Node, so if you install the latest Stable version some other way, skip down to setting up GitHub.
1. **Install Node and NPM with NVM.** As of writing, we're using Node 8.15.1, so the command is `nvm install 8.15.1`. Check the node version we're using in [package.json](https://github.com/codecombat/codecombat/blob/master/package.json).
1. **Use Node 8 By Default**. `nvm alias default 8.15.1`. This way Node 8.15.1 is used for every new terminal. Otherwise you'll need to run `nvm use 8.15.1` before running any dev environment commands.
1. **Update npm to 6.4.1**. `npm install -g npm@6.4.1`. We need this version for some of our dependencies to install correctly.
1. **[Create an account on GitHub](https://github.com/join).** This is where our code repository is hosted.
1. **[Configure Git to connect with your GitHub account](https://help.github.com/articles/set-up-git/).**
1. **[Clone the CodeCombat repository](https://help.github.com/articles/cloning-a-repository/).** `git clone https://github.com/codecombat/codecombat`. This will copy our source code and all its history to your computer to be run and modified.
1. **Install and compile CodeCombat source files.** Navigate into the folder where you downloaded the CodeCombat repository (`cd codecombat`) and run `npm install`. This will install the npm (server library) and bower (client library) dependencies, as well as building the `public` directory, which is what the server... serves.
1. **[Run the dev environment](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-General-Information#running-the-environment)**.
1. **Visit [[http://localhost:3000/]]** to see your CodeCombat development environment!