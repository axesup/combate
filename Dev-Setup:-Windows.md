### Tools

You will need to install the following:

* [Node.js](https://nodejs.org/en/download/) (LTS version should be fine)
* [Git](https://help.github.com/articles/set-up-git/#setting-up-git)
* [Python 2.7](https://www.python.org/downloads/windows/)
* [MongoDB](https://github.com/git-for-windows/git/releases) (You should also [setup a service script](https://docs.mongodb.org/master/tutorial/install-mongodb-on-windows/#manually-create-a-windows-service-for-mongodb))

### Set Up

*First open up `cmd.exe`/Powershell/Git Bash/any terminal.*

You'll want to fork the repo on Github, then clone it to your machine.

    git clone https://github.com/$GITHUB_USERNAME/codecombat.git
    cd codecombat
    git remote add -f origin https://github.com/codecombat/codecombat.git

You'll then want to install the dependencies and build the asset files.

    npm install

Start MongoDB if you haven't, then download the database dump at http://analytics.codecombat.com:8080/dump.tar.gz, extract the contents ([7-Zip](http://www.7-zip.org/) is a good option), then

    mongorestore --drop path/to/dump

*(If it says that there are no reachable servers but there is a mongod process running try adding `--host=127.0.0.1` to the end of the command.)*

### Running

Either run `npm run dev` (live coding) or `npm start` (just previewing) to start the server.

Visit http://localhost:3000 to see your CodeCombat setup in action.