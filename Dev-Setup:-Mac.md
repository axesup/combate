##Index:

* [Simple Mac Tutorial](#simple-mac-tutorial)
* [Vagrant Tutorial](#the-do-it-yourself-vagrant-vm-method)
* [Installing the Database](#installing-the-database)
* [Mac OS X Screencast](https://www.youtube.com/watch?v=fom1ksXSbKM) (video)

### Simple Mac Tutorial

This method should work on Mac, if it doesn't, join our [HipChat room](https://www.hipchat.com/g3plnOKqa). This tutorial requires you to have the [XCode Developer Tools](http://itunes.apple.com/us/app/xcode/id497799835?ls=1&mt=12).

1. [Create a GitHub account](https://github.com/join) if you don't already have one.
2. [Set up Git on your computer](https://help.github.com/articles/set-up-git/) to allow your computer to speak to GitHub.
3. _(Optional)_ [Fork](https://github.com/codecombat/codecombat/fork) our CodeCombat repository if you wish to make changes.
4. Open a terminal and navigate to the folder you wish to install CodeCombat under.
5. * If you've forked the repository, paste in the following command (*Replace "your_repository_url" with your repository*):

    ```bash
    curl https://raw.githubusercontent.com/codecombat/codecombat/master/scripts/devSetup/bootstrap.sh | bash -s your_repository_url  
    ```
   * If you haven't forked the repository, paste in the following command:

    ```bash
    curl https://raw.githubusercontent.com/codecombat/codecombat/master/scripts/devSetup/bootstrap.sh | bash
    ```

    NOTE: The repository will be in the coco subdirectory. You should not run a separate git clone, as that is taken care of.
6. Ensure you have Python 2 installed with `brew install python`, or your distributional equivalent.  Python 3.1 is also supported, but 3.2+ are not tested.
7. Follow the on-screen prompts.  The program will download and install all necessary dependencies. If nothing seems to be happening, try running `sudo python ./coco/scripts/devSetup/setup.py` or join the [HipChat room](https://www.hipchat.com/g3plnOKqa) to fix things.
8.  Run the following commands in separate windows:
    * `./coco/bin/coco-mongodb` - Starts MongoDB
    * `sudo ./coco/bin/coco-brunch` - Starts brunch, which watches for file changes 
    * `./coco/bin/coco-dev-server` - Starts your local web server
9. Setup [MongoDB](#installing-the-database). **Soon to be made optional**
10. Visit [http://localhost:3000](http://localhost:3000) to see your CodeCombat development environment!

If you get errors with bower not being able to clone git repositories, try [cloning over https](http://stackoverflow.com/questions/1722807/git-convert-git-urls-to-http-urls/11383587#11383587). If SASS brings up an error about file encodings being wrong, add this to your .bash_profile:

```bash
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8
```

If you only see a white screen, check if the first line of app.css is `ERROR: Cannot load compass`. If so, try either uninstalling compass (`gem uninstall compass`) or re-installing it if you actually need it (`gem install compass --pre`).

###Installing the Database
Download the [CodeCombat database](http://analytics.codecombat.com:8080/dump.tar.gz) (updated every 10 minutes) and import it to your locally running database with the following commands:

1. Make sure the database is running on your computer (`./bin/coco-mongodb`).

1. Uncompress the file with `tar xzvf [filename]`).

1. Run `mongorestore --drop [path to dump]` if mongorestore is in your path. If mongorestore is not in your path, run `[path to CodeCombat folder]/bin/mongo/mongorestore --drop [path to dump]`.

When downloading a new dump to keep the database up-to-date, use `mongorestore --drop [path to dump]` to clear out all old data (including any local data you have created) and replace with just the new data.

*If you see an error like `no reachable servers` when running mongorestore, and mongo is running, try adding `--host=127.0.0.1` to the command line options.*