### Tools

You will need to install the following:

* [Node.js](https://nodejs.org/en/download/) (LTS version should be fine, but Stable is preferred)
* [Git](https://help.github.com/articles/set-up-git/#setting-up-git)
* [Python 2.7](https://www.python.org/downloads/windows/)

### Set Up

*First open up `cmd.exe`/Powershell/Git Bash/any terminal.*

You'll want to fork the repo on Github, then clone it to your machine.

    git clone https://github.com/$GITHUB_USERNAME/codecombat.git
    cd codecombat
    git remote add -f upstream https://github.com/codecombat/codecombat.git

You'll then want to install the dependencies and build the asset files.

    npm install --global --production windows-build-tools@3.1.0
    npm install

### Running

    npm run webpack -- --watch
    npm run proxy

Either run both of the above commands (live coding) or just `npm run proxy` (just previewing) to run the website locally.

Visit [http://localhost:3000](http://localhost:3000) to see your CodeCombat setup in action.