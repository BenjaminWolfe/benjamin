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

## Getting to MVP

Of course I mean [minimum viable product][9] here.
To me, a minimum viable product has

* no real content yet,
* a modicum of personalization so it looks like my site, and
* no obvious boilerplate content so it looks like someone else's site.

I took care of all of that in my [very next commit][10].
(Commit note: Unfortunately, I no longer have admin privileges on my Mac,
and I can't get `gitmoji-cli` to work.
No more fancy emojis for now.)

Next I wanted to add an icon, though.
[According to the docs][11], the process is different depending on your version.
Before v4.7 it's a bit more complicated.
Thankfully, according to [themes/hugo-academic/data/academic.toml][13],
I'm on v4.7.0.
I simply had to "Save [my] icon as a square 512x512 pixel image
named icon.png and place the image in [my] root assets/images/ folder[.]"
For now—again, as an MVP—that meant using my standard image,
and finding a [simple site][12] to convert it to the right size and type.

[1]: https://djnavarro.net/post/starting-blogdown/
[2]: https://twitter.com/djnavarro
[3]: https://github.com/carloscuesta/gitmoji-cli
[4]: https://code.visualstudio.com/
[5]: https://github.com/gcushen/hugo-academic/issues/1453
[6]: https://discourse.gohugo.io/t/academic-theme-netlify-deployment-problems/22186/3
[7]: https://gohugo.io/hosting-and-deployment/hosting-on-netlify/#configure-hugo-version-in-netlify
[8]: https://docs.netlify.com/configure-builds/file-based-configuration/#sample-file"
[9]: https://en.wikipedia.org/wiki/Minimum_viable_product
[10]: https://github.com/BenjaminWolfe/benjamin/commit/653f8ded2b0bfb7c001af682c15f02e97bffe69d
[11]: https://sourcethemes.com/academic/docs/customization/#website-icon
[12]: http://convert-my-image.com/ImageConverter
[13]: themes/hugo-academic/data/academic.toml
