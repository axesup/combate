## Requirements

You will need to install MongoDB, Node.js, Git, cURL, "build essentials", and Python 2.7.

**NOTE: These instructions are for installing Node v4, but currently CodeCombat uses v5**. Consider using [nvm](https://github.com/creationix/nvm) instead.

Example for Ubuntu:

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
    echo "deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen" | sudo tee /etc/apt/sources.list.d/mongodb.list
    sudo apt-get update
    sudo apt-get install build-essential python2.7 git curl mongodb-org nodejs-legacy

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

## Database Import

    (cd $(mktemp -d /tmp/coco.XXXXXXXX) && curl http://analytics.codecombat.com:8080/dump.tar.gz | tar xzf - && mongorestore --drop --host 127.0.0.1)

This will download the latest [development database](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-General-Information#database) and overwrite your current development database with it.
## Running

### Database

Your MongoDB server should be running; if not you can start it with a service script.

For example on Ubuntu:

    sudo service mongod start

On other distros with `systemd` you can try something like:

    sudo systemctl start mongodb

### Development Server

    npm run dev

This will start `brunch` (watches client files) and `nodemon` (watches server files). (You can also just use `npm start` to run the server without keeping brunch watching for changes.)

Visit [http://localhost:3000](http://localhost:3000) to see your local CodeCombat setup.