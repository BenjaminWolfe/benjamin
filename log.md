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

## Tweaks with My First Post

When I started the wizard to create my first post,
I got an error saying that `blogdown` could not read the YAML
at `content/authors/admin/_index.md`.

Actually, I got a warning, but it was converted to an error
because of this line I added to my `.Rprofile` on a tip from [Jenny Bryan][14]:

```r
options(
  error = rlang::entrace,
  rlang_backtrace_on_error = "branch",
  warn = 2 # handle warnings as errors
)
```

In that file I noticed two things:

1. I had added quotation marks where they were probably not necessary.
1. I had specified `email` twice, the second time with a commented note.

I suspect it was the 2nd of these that made the difference, but I changed both.
Whatever I did fixed it.

Alison Hill recommended [setting a number of other options][20],
which you'll also see in the site's `.Rprofile`.

## Drafts

Considered using `draft: true` in my posts (see [this tweet][15]),
but [Alison Hill][16] [convinced me otherwise][17]
via these posts from [herself][18] and [Garrick Aden-Buie][19].

## Branches

Again following the post from Garrick Aden-Buie above,
I created a new branch called `development`.
I know GAB actually recommended making a new branch for each post,
but I thought I'd keep it simple.

You'll find the ability to create a new branch at the top of GitHub
where it says _Branch: Master_.
Click on that and you'll notice the text box says "Find or create a branch...."
Simply type the name of the branch, hit Enter, and you're done!

Then I had to check out the branch locally.
Git UIs like Atlassian's [SourceTree][21] usually make this a breeze.
But at the moment I was tinkering with the command line,
so I thought I'd try my hand at it.

The relevant commands are as follows:

```bash
cd ~/Documents/GitHub/benjamin
git fetch
git branch -a
git checkout development
```

To walk through those:

* Change directories to where I keep my local repo.
* Fetch changes from GitHub.
* Take a look at what branches there are.
  The ones that start `remote/origin` are out on GitHub.
  The ones that don't live locally.
* Check out the new branch, in my case named `development`.

__A note of caution__ on that last one, as well as a tip.
You might think you're checking out the _remote_ branch,
and use something like this:

```bash
# do not do this!
git checkout origin/development
```

If you try this, as I did, you'll get an error that all git users dread,
saying you're in a 'detached HEAD' state.

And now the tip: If that happens,
just go back and rerun the statement the right way.
Do it right away and you'll be good.
I was.

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
[14]: https://twitter.com/JennyBryan
[15]: https://twitter.com/BenjaminWolfe/status/1234516998157217793
[16]: https://twitter.com/apreshill
[17]: https://twitter.com/apreshill/status/1234519975248875526
[18]: https://alison.rbind.io/post/2019-03-04-hugo-troubleshooting/#dates
[19]: https://www.garrickadenbuie.com/blog/blogdown-netlify-new-post-workflow/
[20]: https://twitter.com/apreshill/status/1234524051692875777
[21]: https://www.sourcetreeapp.com/
