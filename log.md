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

But then I got an error!

> Error: "/opt/build/repo/themes/hugo-academic/layouts/partials/functions/get_address.html:21:1":
> parse failed: template: partials/functions/get_address.html:21: function "return" not defined

This took me to someone else's misadventures [here][5] and [here][6],
which in turn pointed me to using a [netlify.toml][7] file
at the [project root][8].
I copied contents directly from Netlify (the link just mentioned),
after running `blogdown::hugo_version()` to verify it's the same version I use.
And then it worked.

[1]: https://djnavarro.net/post/starting-blogdown/
[2]: https://twitter.com/djnavarro
[3]: https://github.com/carloscuesta/gitmoji-cli
[4]: https://code.visualstudio.com/
[5]: https://github.com/gcushen/hugo-academic/issues/1453
[6]: https://discourse.gohugo.io/t/academic-theme-netlify-deployment-problems/22186/3
[7]: https://gohugo.io/hosting-and-deployment/hosting-on-netlify/#configure-hugo-version-in-netlify
[8]: https://docs.netlify.com/configure-builds/file-based-configuration/#sample-file"
