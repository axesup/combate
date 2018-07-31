## About This Method

NOTE: As we have migrated from Brunch to Webpack, some parts of this setup may be broken (for example, need to update the Vagrant provision script to use Node 6 and make sure your version of Vagrant uses a box from vagrantcloud.com instead of atlas.hashicorp.com). We welcome any contributions to this!

[Vagrant](https://www.vagrantup.com) is a tool for rapidly creating and configuring [virtual machines](http://en.wikipedia.org/wiki/Virtual_machine).

By using Vagrant, we can quickly create an environment for CodeCombat with all the necessary dependencies. Vagrant also simplifies rebuilding the environment and upgrading to newer versions of dependencies.

Vagrant supports a number of virtual machine environments. For this setup we will be using [VirtualBox](https://www.virtualbox.org/).

## Installation

Start by installing [Vagrant](https://www.vagrantup.com), [VirtualBox](https://www.virtualbox.org/), and [Git](http://git-scm.com/). If running on Windows, either [Git for Windows](https://git-scm.com/download/win) or [GitHub for Windows](https://windows.github.com/) may be used.

Choose a folder on your computer for CodeCombat and clone the repository from GitHub. If you are intending to contribute, it is a good idea to fork the repository on GitHub first, then clone your fork. 

If cloning on Windows, the Git section of the [Windows setup guide](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-Windows#repository-setup) may be helpful. You only need to do the steps related to `git clone`.

## Setup

Terminal / Git Bash is recommended, however, a regular Windows command prompt works too.

First open a Terminal window, change directory to where you cloned CodeCombat, then run `vagrant up` to start the virtual machine: 

`path/to/your/project$ vagrant up`

The first time you run, it takes time because it will download a copy of [vagrant "box"](https://www.vagrantup.com/docs/boxes.html), which is actually an Ubuntu Linux VM, along with various required dependencies that we will use to run CodeCombat. If you're running on Windows, you might have to give VirtualBox firewall access as requested.

If there are errors during the process, you can try `vagrant provision` to run the setup script again or `vagrant destroy` followed by `vagrant up` to totally dispose and recreate the virtual machine. If you aren't able to figure it out, try asking in the [CodeCombat chat room](https://www.hipchat.com/gkaufqwnj).

## Running CodeCombat

Once the VM is up and running, change directory in your Terminal window to where you cloned CodeCombat, run `scripts/vagrant/npm run webpack -- --watch` (watches client files) and `scripts/vagrant/npm run proxy` in order to start and connect to CodeCombat's production server:

* Git Bash:
  * `path/to/your/project$ scripts/vagrant/npm.sh run webpack -- --watch`
  * `path/to/your/project$ scripts/vagrant/npm.sh run proxy`
* Windows command prompt:
  * `path\to\your\project\> scripts/vagrant/npm.bat run webpack -- --watch`
  * `path\to\your\project\> scripts/vagrant/npm.bat run proxy`

Once the window shows that it has compiled the files, you can visit [http://localhost:13000](http://localhost:13000) in your browser and see CodeCombat running.

## Shutting down

Run `vagrant halt` to turn off the VM. To start again, just run `vagrant up`.

`path/to/your/project$ vagrant halt`

## Rebuilding the virtual machine

The virtual machine has a copy of the various node dependencies, as well as some other tools used in running CodeCombat, such as MongoDB. It may be necessary to update the virtual machine as dependencies or dependency versions are changed.

To handle dependency changes, open a command window and change to the directory where you cloned CodeCombat. Run `vagrant provision`. Note that this will update the MongoDB database, so be sure to read the section above if you want to save users and achievements.

To rebuild the virtual machine from scratch, run `vagrant destroy` followed by `vagrant up`. This will destroy and re-create the MongoDB database from scratch, so be sure to read the section above if you want to save users and achievements.

## Extra notes

* On Windows, if you hit `Ctrl-C` to interrupt Vagrant while it is in the middle of an operation, it may return to the command prompt but still be running. This prevents any other Vagrant command from working. Just hit `Ctrl-C` again to fully terminate the previous command.
* The CodeCombat directory is visible inside the virtual machine as `/vagrant`. 
  * This uses VirtualBox shared folders, using the VirtualBox Guest Additions. 
  * If the Guest Additions are a different version from the installed VirtualBox (a common occurrence), then symbolic links will not work on Windows. 
  * This is problematic because `npm` likes to make symlinks to executables in `node_modules/.bin`. 
  * To work around this, a directory `/node_modules` is made inside the virtual machine and is mounted over  `/vagrant/node_modules`.
  * This means that the `node_modules` directory will appear empty from outside the virtual machine. It should not be deleted.
* [Brunch](http://brunch.io/) was used by CodeCombat to watch for changes to Coffeescript files and recompile them automatically. In order to allow Brunch running in the virtual machine to detect changes made on the "host" machine, "polling" mode is used. This results in higher CPU usage.
  * In order to avoid this and run Brunch in regular mode, you can start Brunch manually inside the VM by `vagrant ssh`, `cd /vagrant`, and `brunch w`. You will need to have an SSH client installed (e.g. the one installed by Git for Windows).
  * When running Brunch in regular mode, changes must be made from inside the virtual machine (i.e. via `vagrant ssh`). The virtual machine is running Ubuntu Linux, so any of the normal text mode editors may be installed and used.
  * When running on a Mac, if you stop the brunch process from running and then try and start it again, it may throw and error complaining about port forwarding to port 3000. To resolve this issue, find the process running it ``sudo lsof -i :3000`` and kill it: ``sudo kill -9 3267``