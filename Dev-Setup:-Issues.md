### General Troubleshooting

If you are having a problem not listed here, jump into [our dev chat](https://coco-slack-invite.herokuapp.com/) and let's get it fixed and then documented here. You might want to check your versions of node, npm, MongoDB, and Python, and also make sure your GitHub copy of CodeCombat is [up-to-date](https://help.github.com/articles/syncing-a-fork/).

### Database

If you get an error like this:

> Failed: restore error: coco.media.chunks: error restoring from /root/data/dump/coco/media.chunks.bson: insertion error: EOF

Then try using the `--batchSize=100` option:

> mongorestore --drop --batchSize=100 /root/data/dump

### Bower

If you get errors with bower not being able to clone git repositories, try [cloning over https](http://stackoverflow.com/questions/1722807/git-convert-git-urls-to-http-urls/11383587#11383587).

### Sass

If Sass brings up an error about file encodings being wrong, add this to your .bash_profile:
```bash
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8
```

If you only see a white screen, check to see if the first line of app.css is `ERROR: Cannot load compass`. If so, try either uninstalling compass (`gem uninstall compass`) or re-installing it if you actually need it (`gem install compass --pre`).

If you get a white screen on http://localhost:3000 with no JavaScript errors, or if your page loads fine but no CSS is applied, it could be that your brunch isn't compiling Sass properly (`public\stylesheets\app.css` is like 70KB instead of >600KB). We don't know of any current issues that are causing this, or workarounds, but it has been a common symptom in the past with different Sass compilation setups, especially on Windows. 