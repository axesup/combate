###Index:

* [Automatic Linux Installation](#automatic-linux-installation)
* [Complex Linux Installation](#complex-linux-installation)
* [Ubuntu Installation](#ubuntu-installation)
* [Installing the Database](#installing-the-database)
* [Ubuntu Screencast](http://youtu.be/usN85KSiWUM) (video)

####Automatic Linux Installation

On Linux, you'll need _make_, _build-essential_, _ruby_, _curl_ and _git_ installed (`sudo apt-get install make build-essential ruby curl git`).

1. [Create a GitHub account](https://github.com/join) if you don't already have one.
2. [Set up Git on your computer](https://help.github.com/articles/set-up-git/) to allow your computer to speak to GitHub.
3. (Optional) [Fork](https://github.com/codecombat/codecombat/fork) our CodeCombat repository if you wish to make changes.
4. Open a terminal and navigate to the folder you wish to install CodeCombat under.
5. * If you've forked the repository, paste in the following command (*Replace "your_repository_url" with your repository*):

    ```bash
    curl https://raw.githubusercontent.com/codecombat/codecombat/master/scripts/devSetup/bootstrap.sh | bash -s your_repository_url
    ```
   * If you haven't forked the repository, paste in the following command:
   
    ```bash
    curl https://raw.githubusercontent.com/codecombat/codecombat/master/scripts/devSetup/bootstrap.sh | bash
    ```
    NOTE: The repository will be in the coco subdirectory.  You should not run a separate git clone, as that is taken care of.
6. Ensure you have Python 2 installed with `sudo apt-get install python2`, or your distributional equivalent.  Python 3.1 is also supported, but 3.2+ are not tested.  If that is not working, it is also possible to install it directly from the Ubuntu software center.
7. Follow the on-screen prompts.  The program will download and install all necessary dependencies.  If nothing seems to be happening, try running `sudo python ./coco/scripts/devSetup/setup.py` or join the [HipChat room](https://www.hipchat.com/g3plnOKqa) to fix things.
7.  Run the following commands in separate windows (these are python scripts, so make sure you have a python IDE installed):
    * `./coco/bin/coco-mongodb` - Starts MongoDB
    * `sudo ./coco/bin/coco-brunch` - Starts brunch, which watches for file changes 
    * `./coco/bin/coco-dev-server` - Starts your local web server
9. Setup [MongoDB](#installing-the-database).
9. Visit [http://localhost:3000](http://localhost:3000) to see your CodeCombat development environment!

####Complex Linux Installation

1. [Set up a GitHub account](https://help.github.com/articles/set-up-git) if you don't already have one.
2. [Fork](https://github.com/codecombat/codecombat/fork) the CodeCombat project.
3. `git clone` it to your computer.
4. Install software
  1. `sudo npm install`
  2. `sudo npm install -g bower` - _It might be necessary to do `cd coco`_
  3. `bower install` ( bower install each dependency from bower.json, make sure you're inside the coco directory )
  4. `sudo npm install -g brunch`
  5. Download [MongoDB 3.0](http://www.mongodb.org/downloads)
  6. Start up `mongod` and define the bin folder of coco as your --dbpath variable
5. Run `bin/coco-mongodb`, `bin/coco-brunch` and `bin/coco-dev-server`.
6. Go to [http://localhost:3000](http://localhost:3000) to see your local CodeCombat in action.

####Ubuntu Installation

Thank you to Steve Malmskog for writing this great guide on getting the development environment running on Ubuntu 12.04 LTS (and later)!

* This new installation steps prepared by blianwmaster!(Experimental environment for Ubuntu 12.04.5 LTS Server)
* Choose English language installed 
* Do not use root login, the following steps didn't use the root login, so before the command to add sudo
* My test website http://www.icodegame.com:3000
* This is my share of the database file repair
* Link: http: //pan.baidu.com/s/1mgqzOSw Password: t98l
* The 99% of the picture and sound repair,I compressed coco.tar.gz database file is 81M
```bash
#!/bin/bash
echo -------------------------------------------------------------------------
echo ----------Update software source
echo -------------------------------------------------------------------------

sleep 5s
sudo apt-get update
echo -------------------------------------------------------------------------
echo ----------Install compiler environment
echo -------------------------------------------------------------------------

sleep 5s
sudo apt-get -y install make build-essential curl git zlib1g-dev python-software-properties
echo -------------------------------------------------------------------------
echo ----------Download the codecombat git
echo -------------------------------------------------------------------------

sleep 5s
mkdir -p coco
cd coco
git clone https://github.com/codecombat/codecombat.git
echo -------------------------------------------------------------------------
echo ----------Install npm and Other runtime environments
echo -------------------------------------------------------------------------

sleep 5s
cd codecombat
sudo add-apt-repository -y ppa:chris-lea/node.js
sudo apt-get update
sudo apt-get -y install nodejs
sudo npm install
echo -------------------------------------------------------------------------
echo ----------Install the new version
echo -------------------------------------------------------------------------

sleep 5s
sudo npm install geoip-lite@1.1.6
sudo npm install grunt-cli@0.1.13
sudo npm install node-gyp@0.13.0
sudo npm install sendwithus@2.9.0
sudo npm install auto-reload-brunch@1.8.0
sudo npm install bower@1.5.2
sudo npm install brunch@1.8.5
sudo npm install nodemon@1.4.1
echo -------------------------------------------------------------------------
echo ----------Update npm and install ruby sass
echo -------------------------------------------------------------------------

sleep 5s
sudo npm update
sudo apt-get -y install ruby1.9.1 ruby1.9.1-dev
sudo gem install sass
echo -------------------------------------------------------------------------
echo ----------Install bower
echo -------------------------------------------------------------------------

sleep 5s
sudo ./node_modules/bower/bin/bower --allow-root install
sudo ./node_modules/bower/bin/bower --allow-root update
echo -------------------------------------------------------------------------
echo ----------Download and install mongodb 3.0.6
echo -------------------------------------------------------------------------

sleep 5s
cd ~/coco && mkdir -p mongodl
cd mongodl
curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-ubuntu1204-3.0.6.tgz
tar xfz mongodb-linux-x86_64-ubuntu1204-3.0.6.tgz
sudo cp mongodb-linux-x86_64-ubuntu1204-3.0.6/bin/* /usr/local/bin
echo -------------------------------------------------------------------------
echo ----------Download and unpack database
echo -------------------------------------------------------------------------

sleep 5s
cd ~/coco && mkdir -p db
cd db
wget http://analytics.codecombat.com:8080/dump.tar.gz
tar xzvf dump.tar.gz
echo -------------------------------------------------------------------------
echo ----------Update CreateJS
echo -------------------------------------------------------------------------

sleep 5s
cd ~/coco && mkdir -p CreateJS
cd CreateJS
git clone https://github.com/CreateJS/EaselJS.git
cd EaselJS
sudo npm update
cd build
sudo npm update
echo -------------------------------------------------------------------------
echo ----------building EaselJS
echo -------------------------------------------------------------------------

sleep 5s
sudo ~/coco/codecombat/node_modules/grunt-cli/bin/grunt combine
cd ~/coco/CreateJS
git clone https://github.com/CreateJS/PreloadJS.git
cd PreloadJS
sudo npm update
cd build
sudo npm install
sudo npm update
echo -------------------------------------------------------------------------
echo ----------building PreloadJS
echo -------------------------------------------------------------------------

sleep 5s
sudo ~/coco/codecombat/node_modules/grunt-cli/bin/grunt combine
git clone https://github.com/CreateJS/SoundJS.git
cd SoundJS
sudo npm update
cd build
sudo npm install
sudo npm update
echo -------------------------------------------------------------------------
echo ----------building SoundJS
echo -------------------------------------------------------------------------

sleep 5s
sudo ~/coco/codecombat/node_modules/grunt-cli/bin/grunt combine
git clone https://github.com/CreateJS/TweenJS.git
cd TweenJS
sudo npm update
cd build
sudo npm install
sudo npm update
echo -------------------------------------------------------------------------
echo ----------building TweenJS
echo -------------------------------------------------------------------------

sleep 5s
sudo ~/coco/codecombat/node_modules/grunt-cli/bin/grunt combine
echo -------------------------------------------------------------------------
echo ----------moving to CoCo
echo -------------------------------------------------------------------------

sleep 5s
cp ~/coco/CreateJS/EaselJS/build/output/easeljs-NEXT.combined.js ~/coco/codecombat/vendor/scripts
cp ~/coco/CreateJS/EaselJS/build/output/movieclip-NEXT.combined.js ~/coco/codecombat/vendor/scripts
cp ~/coco/CreateJS/EaselJS/src/easeljs/display/SpriteStage.js ~/coco/codecombat/vendor/scripts/
cp ~/coco/CreateJS/EaselJS/src/easeljs/display/SpriteContainer.js ~/coco/codecombat/vendor/scripts/
cp ~/coco/CreateJS/SoundJS/lib/soundjs-NEXT.combined.js ~/coco/codecombat/vendor/scripts
cp ~/coco/CreateJS/PreloadJS/build/output/preloadjs-NEXT.combined.js ~/coco/codecombat/vendor/scripts
cp ~/coco/CreateJS/TweenJS/build/output/tweenjs-NEXT.combined.js ~/coco/codecombat/vendor/scripts
echo -------------------------------------------------------------------------
echo ----------Install database snapshot
echo -------------------------------------------------------------------------

sleep 5s
cd ~/coco && mkdir -p log
sudo ./codecombat/bin/coco-mongodb >~/coco/log/mongodb.log 2>&1 &
echo Wait 180 seconds

sleep 180s
cd db && sudo mongorestore --drop dump

echo -------------------------------------------------------------------------
echo ----------Fix app/styles/common/common.sass
echo -------------------------------------------------------------------------

sed -i '1i @charset "UTF-8"' ~/coco/codecombat/app/styles/common/common.sass

echo -------------------------------------------------------------------------
echo ----------Generate run-coco file
echo -------------------------------------------------------------------------

sleep 5s
cd ~/coco
cat <<- EOF > run-coco.sh
#!/bin/bash
echo ----------Run mongodb
nohup  ~/coco/codecombat/bin/coco-mongodb >~/coco/log/mongodb.log 2>&1 &
echo ----------mongodb ok,wait 10s

sleep 10s

echo ----------Run brunch
nohup  ~/coco/codecombat/bin/coco-brunch >~/coco/log/brunch.log 2>&1 &
echo ----------brunch ok,wait 120s

sleep 10s

echo ----------Run dev_server
nohup  ~/coco/codecombat/bin/coco-dev-server >~/coco/log/dev_server.log 2>&1 &
echo ----------dev_server ok!
EOF
chmod 777 run-coco.sh
echo -------------------------------------------------------------------------
echo ----------ok!now ,reboot your computer and run run-coco.sh
echo -------------------------------------------------------------------------
```

####Installing the Database
Download the [CodeCombat database](http://analytics.codecombat.com:8080/dump.tar.gz) (updated every 10 minutes) and import it to your locally running database with the following commands:

1. Make sure the database is running on your computer `./bin/coco-mongodb`.

1. Uncompress the file with `tar xzvf [filename]`.

1. Run `mongorestore --drop [path to dump]` if mongorestore is in your path. If mongorestore is not in your path, run `[path to CodeCombat folder]/bin/mongo/mongorestore --drop [path to dump]`.

When downloading a new dump to keep the database up-to-date, use `mongorestore --drop [path to dump]` to clear out all old data (including any local data you have created) and replace with just the new data.