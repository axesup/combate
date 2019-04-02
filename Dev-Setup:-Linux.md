## Requirements

You will need to install Node.js, Git, "build essentials", and Python 2.7.

**NOTE: These instructions are for installing Node v4, but currently CodeCombat uses Node 8**. Consider using [nvm](https://github.com/creationix/nvm) instead.

Example for Ubuntu:

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
    sudo apt-get update
    sudo apt-get install build-essential python2.7

If your default Python version is 3, then you'll also want to

    npm config set python `which python2.7`

If you have not [set up Git](https://help.github.com/articles/set-up-git/#platform-linux), then at least do the following:

    git config --global user.name "$YOUR_NAME"
    git config --global user.email "$YOUR_EMAIL_ADDRESS"

## Cloning

First fork and clone the [CodeCombat repository][repo], and track upstream.

    git clone https://github.com/$GITHUB_USERNAME/codecombat.git
    cd codecombat
    git remote add -f upstream https://github.com/codecombat/codecombat.git

[repo]: https://github.com/codecombat/codecombat

## Installing Dependencies

    npm install

This will take care of installing npm and bower dependencies, as well as building the asset files.
## Running

### Development Server

    npm run webpack -- --watch
    npm run proxy

This will start `webpack` (watches client files) and `proxy` (routes all server calls to CodeCombat's production servers). (You can also just use `npm run proxy` to run the server without keeping webpack watching for changes.)

Visit [http://localhost:3000](http://localhost:3000) to see your local CodeCombat setup.