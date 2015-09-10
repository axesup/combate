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

* This new installation steps prepared by blianwmaster!(Experimental environment for Ubuntu 14.04.3 LTS Desktop)
* Choose English language installed 
* Do not use root login, the following steps didn't use the root login, so before the command to add sudo
* My test website http://www.icodegame.com:3000
* This is my share of the database file repair
* Link: http: //pan.baidu.com/s/1mgqzOSw Password: t98l
* The 99% of the picture and sound repair,I compressed coco.tar.gz database file is 81M

#####Installation
Update and install software source compiler environment:

- `sudo apt-get update`
- `sudo apt-get install make build-essential curl git zlib1g-dev`

Create a directory on the desktop：

- `cd ~/Desktop && mkdir -p coco`
- `cd coco`


Fork and download the codecombat git repo:
- Create a git account or sign in
- [Fork](https://github.com/codecombat/codecombat/fork) the CodeCombat repository
- Clone the repository:
    - `git clone https://github.com/[YOUR_USERNAME_OR_ID]/codecombat.git`
    - `cd codecombat`
    - `git remote add upstream https://github.com/codecombat/codecombat.git`
    - `git fetch upstream`
    - `git checkout master`
    - `git merge upstream/master`
    - `git push -u origin master`

Install Other runtime environments for Ubuntu 12.04 LTS Desktop (Experimental environment for Ubuntu 14.04.3 LTS Desktop):
* Add this line to your package.json in
- https://github.com/blianwmaster/codecombat/blob/master/package.json#L55
 
- `sudo add-apt-repository ppa:chris-lea/node.js`
- `sudo apt-get update`
- `sudo apt-get install nodejs`
- `sudo npm install`
- `sudo npm install -g n`
- `sudo n stable`
- `sudo npm update`
- `sudo apt-get install ruby1.9.1 ruby1.9.1-dev`
- `sudo gem install sass`
- `sudo ./node_modules/bower/bin/bower --allow-root install`
- `sudo ./node_modules/bower/bin/bower --allow-root update`

Download and (manually) install mongodb 3.0.6 for Ubuntu:
- `cd ~/Desktop/coco && mkdir -p mongodl`
- `cd mongodl`
- `wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-ubuntu1404-3.0.6.tgz`
- `tar xfz mongodb-linux-x86_64-ubuntu1404-3.0.6.tgz`
- `sudo cp mongodb-linux-x86_64-ubuntu1404-3.0.6/bin/* /usr/local/bin`

Download and unpack database snapshot:
- `cd ~/Desktop/coco && mkdir -p db`
- `cd db`
- `wget http://analytics.codecombat.com:8080/dump.tar.gz`
- `tar xfz dump.tar.gz`

Install database snapshot:
- In first terminal:
   - `cd ~/Desktop/coco/codecombat/bin && sudo ./coco-mongodb`
- In another terminal:
   - `cd ~/Desktop/coco/db && sudo mongorestore --drop dump`

Update CreateJS:
- In another terminal:
   - `cd ~/Desktop/coco/codecombat/bin`
   - `sudo gedit ./coco-update-createjs`
   - * Copy and paste the following text
- * -----------begin---------------------
- `# automatically builds the latest versions of the CreateJS suite`
- `# and puts them into vendor/scripts.`

- `# for this to work:`
- `cd ~/Desktop/coco`
- `mkdir -p CreateJS`
- `cd CreateJS`
- `git clone https://github.com/[YOUR_USERNAME_OR_ID]/EaselJS.git`
- `cd EaselJS`
- `git remote add upstream https://github.com/CreateJS/EaselJS.git`
- `git fetch upstream`
- `git checkout master`
- `git merge upstream/master`
- `git push -u origin master`

- `cd ..`
- `git clone https://github.com/[YOUR_USERNAME_OR_ID]/PreloadJS.git`
- `cd PreloadJS`
- `git remote add upstream https://github.com/CreateJS/PreloadJS.git`
- `git fetch upstream`
- `git checkout master`
- `git merge upstream/master`
- `git push -u origin master`

- `cd ..`
- `git clone https://github.com/[YOUR_USERNAME_OR_ID]/SoundJS.git`
- `cd SoundJS`
- `git remote add upstream https://github.com/CreateJS/SoundJS.git`
- `git fetch upstream`
- `git checkout master`
- `git merge upstream/master`
- `git push -u origin master`

- `cd ..`
- `git clone https://github.com/[YOUR_USERNAME_OR_ID]/TweenJS.git`
- `cd TweenJS`
- `git remote add upstream https://github.com/CreateJS/TweenJS.git`
- `git fetch upstream`
- `git checkout master`
- `git merge upstream/master`
- `git push -u origin master`


- `# then you can run this script to build the latest version whenever`
- `# see the build/README file in any of these libraries on GitHub for more info`
- `# https://github.com/CreateJS/EaselJS/blob/master/build/README.md`



- `cd ~/Desktop/coco/CreateJS/EaselJS/`
- `echo updating Easel`
- `git checkout .`
- `git pull`
- `sudo npm update`
- `cd build`
- `sudo npm update`
- `echo building Easel`
- `sudo ~/Desktop/coco/codecombat/node_modules/grunt-cli/bin/grunt combine`

- `cd ~/Desktop/coco/CreateJS/PreloadJS/`
- `echo updating Preload`
- `git checkout .`
- `git pull`
- `sudo npm update`
- `cd build`
- `sudo npm install`
- `sudo npm update`
- `echo building Preload`
- `sudo ~/Desktop/coco/codecombat/node_modules/grunt-cli/bin/grunt combine`

- `cd ~/Desktop/coco/CreateJS/SoundJS/`
- `echo updating Sound`
- `git checkout .`
- `git pull`
- `sudo npm update`
- `cd build`
- `sudo npm install`
- `sudo npm update`
- `echo building Sound`
- `sudo ~/Desktop/coco/codecombat/node_modules/grunt-cli/bin/grunt combine`

- `cd ~/Desktop/coco/CreateJS/TweenJS/`
- `echo updating Tween`
- `git checkout .`
- `git pull`
- `sudo npm update`
- `cd build`
- `sudo npm install`
- `sudo npm update`
- `echo building Tween`
- `sudo ~/Desktop/coco/codecombat/node_modules/grunt-cli/bin/grunt combine`

- `echo moving to CoCo`
- `cp ~/Desktop/coco/CreateJS/EaselJS/build/output/easeljs-NEXT.combined.js ~/Desktop/coco/codecombat/vendor/scripts`
- `cp ~/Desktop/coco/CreateJS/EaselJS/build/output/movieclip-NEXT.combined.js ~/Desktop/coco/codecombat/vendor/scripts`
- `cp ~/Desktop/coco/CreateJS/EaselJS/src/easeljs/display/SpriteStage.js ~/Desktop/coco/codecombat/vendor/scripts/`
- `cp ~/Desktop/coco/CreateJS/EaselJS/src/easeljs/display/SpriteContainer.js ~/Desktop/coco/codecombat/vendor/scripts/`
- `cp ~/Desktop/coco/CreateJS/SoundJS/lib/soundjs-NEXT.combined.js ~/Desktop/coco/codecombat/vendor/scripts`
- `cp ~/Desktop/coco/CreateJS/PreloadJS/build/output/preloadjs-NEXT.combined.js ~/Desktop/coco/codecombat/vendor/scripts`
- `cp ~/Desktop/coco/CreateJS/TweenJS/build/output/tweenjs-NEXT.combined.js ~/Desktop/coco/codecombat/vendor/scripts`

- *----------end-----------
- https://github.com/codecombat/codecombat/blob/master/config.coffee#L146
- movieclip-NEXT.min.js
- * Replace and Save
- movieclip-NEXT.combined.js

   - `sudo ./coco-update-createjs`

#####Running

Start up mongo:
- Mongo should already be running from your database snapshot install. If not:
   - `cd ~/Desktop/coco/codecombat/bin && sudo ./coco-mongodb`


Start up brunch:
- `cd ~/Desktop/coco/codecombat/bin && sudo ./coco-brunch`
   This should say something like:

   info: compiled 806 files into 597 files, copied 371 in 34766ms

   It will continue to run in the foreground.

Start up the dev server:
- `cd ~/Desktop/coco/codecombat/bin && sudo ./coco-dev-server`

Accessing the local instance of codecombat:
- Start up a local browser and go to: http://localhost:3000.

#####Code Syncing

Pick up upstream changes:
- `git fetch upstream`
- `git checkout master`
- `git merge upstream/master`
- `git push -u origin master`

####Installing the Database
Download the [CodeCombat database](http://analytics.codecombat.com:8080/dump.tar.gz) (updated every 10 minutes) and import it to your locally running database with the following commands:

1. Make sure the database is running on your computer `./bin/coco-mongodb`.

1. Uncompress the file with `tar xzvf [filename]`.

1. Run `mongorestore --drop [path to dump]` if mongorestore is in your path. If mongorestore is not in your path, run `[path to CodeCombat folder]/bin/mongo/mongorestore --drop [path to dump]`.

When downloading a new dump to keep the database up-to-date, use `mongorestore --drop [path to dump]` to clear out all old data (including any local data you have created) and replace with just the new data.