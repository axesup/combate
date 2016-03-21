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

### Ubuntu 14.04.4 自动安装脚本
演示网址:http://www.icodegame.com:3000
将以下脚本内容保存为 install-coco.sh文件，上传至 root目录，运行脚本自动安装 sudo ./install-coco.sh

    #!/bin/bash
    sleep 5s
    sudo apt-get update
    
    sleep 5s
    sudo apt-get -y install make build-essential curl git zlib1g-dev python2.7 libkrb5-dev
    
    sleep 5s
    sudo mkdir -p coco
    cd coco
    sudo git clone https://github.com/codecombat/codecombat.git
    
    sleep 5s
    sudo wget http://nodejs.org/dist/v5.9.0/node-v5.9.0.tar.gz
    sudo tar xfz node-v5.9.0.tar.gz
    cd node-v5.9.0
    sudo ./configure
    sudo make
    sudo make install
    
    cd ~/coco
    sudo curl -L https://npmjs.org/install.sh | sudo sh
    node -v
    sleep 5s
    npm -v
    sleep 5s
    
    cd ~/coco/codecombat
    sudo npm config set registry https://registry.cnpmjs.org
    sudo npm config set python python2.7
    sudo npm install -g bower --allow-root
    sudo npm install -g brunch
    sudo npm install -g node-gyp
    sudo npm install --phantomjs_cdnurl=http://cnpmjs.org/downloads
    
    sleep 5s
    sudo bower --allow-root install
    sudo bower --allow-root update
    sudo brunch build --env fast
    sleep 5s
    cd ~/coco && mkdir -p mongodl
    cd mongodl
    sudo curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-ubuntu1404-3.2.4.tgz
    sudo tar xfz mongodb-linux-x86_64-ubuntu1404-3.2.4.tgz
    sudo cp mongodb-linux-x86_64-ubuntu1404-3.2.4/bin/* /usr/local/bin
    
    sleep 5s
    cd ~/coco && mkdir -p db
    cd db
    sudo wget http://analytics.codecombat.com:8080/dump.tar.gz
    sudo tar xzvf dump.tar.gz
    
    sleep 5s
    cd ~/coco && mkdir -p log
    sudo ./codecombat/bin/coco-mongodb >~/coco/log/mongodb.log 2>&1 &
    echo Wait 10 seconds
    
    sleep 10s
    cd db && sudo mongorestore --drop dump
    
    sleep 5s
    cd ~/coco
    cat <<- EOF > run-coco.sh
    #!/bin/bash
    echo ----------Run brunch and nodemon
    cd ~/coco/codecombat
    nohup sudo npm run dev >~/coco/log/brunch_nodemon.log 2>&1 &
    echo ----------brunch and nodemon ok!
    EOF
    chmod 777 run-coco.sh
    
    sleep 5s
    cd ~/coco
    cat <<- EOF > run-mongodb.sh
    #!/bin/bash
    echo ----------Run mongodb
    nohup sudo ~/coco/codecombat/bin/coco-mongodb >~/coco/log/mongodb.log 2>&1 &
    echo ----------mongodb ok
    EOF
    chmod 777 run-mongodb.sh
    
    cat <<- EOF > stop-mongodb.sh
    #!/bin/bash
    echo ----------Stop mongodb
    sudo mongo admin --port 27017 --eval "db.shutdownServer()"
    echo ----------Stop Mongodb ok!
    EOF
    chmod 777 stop-mongodb.sh
    
    echo -------------------------------------------------------------------------
    echo ----------ok!
    echo -------------------------------------------------------------------------