# Developer Log
## First Steps

* Refreshed my memory a bit with [this post][1] from [@djnavarro][2].
* Simply used the New Project dialog to create a new blogdown site,
  with theme `gcushen/hugo-academic`. Could have said to use version control.
  Didn't.
* Made a bare repository in GitHub.
* Made gitignore with `.Rproj.user`, `.Rhistory`, `.DS_Store`.
* `cd` to the directory then `git init` then `git remote add origin`
  and the repo URL.
* From here on in it's normal git stuff... add, commit, push, etc.
* Emojis are added with [gitmoji-cli][3].
* [VSCode][4] is actually a really reasonable UI for it.

## Netlify

* Already had a site up and running (still boilerplate, never used).
* Changed the site settings to deploy the master branch of this repo.
  Left the build command as `hugo` & the directory to be published as `public`.
* Then yes, realized my nagging suspicion was right;
  I had not yet built the site in the first place.
  Ran `blogdown::build_site()` to build for deployment.
  Naturally, Netlify had failed in the meantime
  *because there was no public folder*.

[1]: https://djnavarro.net/post/starting-blogdown/
[2]: https://twitter.com/djnavarro
[3]: https://github.com/carloscuesta/gitmoji-cli
[4]: https://code.visualstudio.com/
