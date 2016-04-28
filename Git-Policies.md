1. **[Rebase and squash commits](https://help.github.com/articles/about-git-rebase/).** Once you've handled code review feedback on a pull request or branch, squash commits down to a minimum number of meaningful commits. Merge feature branches into master. [Read this article](https://www.atlassian.com/git/articles/git-team-workflows-merge-or-rebase/) for pros and cons of merge or rebase policies.
1. **Follow good Git commit message practices.** These are listed below. [Source](http://chris.beams.io/posts/git-commit/).
  1. Separate subject from body with a blank line
  1. Limit the subject line to 50 characters
  1. Capitalize the subject line
  1. Do not end the subject line with a period
  1. Use the imperative mood in the subject line
  1. Wrap the body at 72 characters
  1. Use the body to explain what and why vs. how

# Notes On Git Rebase

**Set up your text editor beforehand.** This process involves git opening up a text editor, and if you're not familiar with emacs or vim you might have trouble. If you're on Mac, you can run in the terminal `git config --global core.editor open`. This will tell git to open up TextEdit by default during interactive rebases and any other time git needs you to edit a file for input. `open` may be substituted with `atom`, `subl`, `vim`, etc depending on your editor of choice, if you have the corresponding command set up.