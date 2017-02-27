Git
===

In order to keep the master branch stable, new development code should be committed to separate feature branches.

For example, let's say you're going to start writing a RESTful endpoint for creating new polls. You would start
by first checking out the master branch with `git checkout master`, pulling any new changes with `git pull`, and
creating a new feature branch (`git branch create-poll-endpoint`).

Start coding and commit your changes at regular intervals to avoid pushing massive chunks. I'd also recommend
pushing to origin (GitHub) after each commit (`git push origin create-poll-endpoint`) so that others can view
your changes as early as possible, and to avoid losing your work when your hard drive blows up.

When you're done building the feature, make sure to push all your changes to origin, and create a new pull
request by opening up the GitHub repository in your browser and clicking **New pull request**. Make sure the
**base** is set to `master` and **compare** points to your feature branch (e.g. `create-poll-endpoint`). After
proofreading your changes, hit **Create pull request**.

Now you may notify other developers to let them know you've completed a feature and it's ready to be reviewed.
A pull request will then be either improved and polished upon the reviewer's request or merged into master.
