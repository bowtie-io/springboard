# Getting Started with BowTie and Jekyll

BowTie leans heavily on the [Jekyll](http://jekyllrb.com/) static site
generator. Jekyll is popular, well supported, and easy to use. By adding several
unique features, BowTie turns Jekyll into a system capable of hosting full
applications, not just small static content sites.

## Installing the BowTie gem

BowTie provides a command line utility to assist with your development process.
You'll need to install the `bowtie-io` gem on your development system to develop
locally:

```bash
$ gem install bowtie-io
Fetching: bowtie-io-1.0.2.gem (100%)
Successfully installed bowtie-io-1.0.2
Parsing documentation for bowtie-io-1.0.2
Installing ri documentation for bowtie-io-1.0.2
Done installing documentation for bowtie-io after 0 seconds
1 gem installed
```

You can run `$ bowtie --help` for a full list of supported options.

## Generating an SSH Key

Just as with GitHub and BitBucket, BowTie authenticates repository access with
SSH. You'll need to set up an SSH keypair and configure BowTie to use it. To
generate a key:

```bash
$ ssh-keygen
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/james/.ssh/id_rsa.
Your public key has been saved in /Users/james/.ssh/id_rsa.pub.
The key fingerprint is:
6f:10:2d:b6:67:f0:99:8f:b9:61:dc:7c:3f:a1:84:5f james@Jamess-MacBook-Pro.local
The key's randomart image is:
+--[ RSA 2048]----+
|                 |
|         .       |
|        = .      |
|       . * o     |
|        S * .    |
|         * B . E |
|          O * + .|
|         o o + o |
|          .     o|
```

For the purposes of this guide, we'll configure a default key at
`~/.ssh/id_rsa[.pub]`. BowTie will work with an alternative key, but this guide
will not consider custom key locations in its scope.


## Copying an SSH Key to BowTie

For OSX systems, run `$ pbcopy < ~/.ssh/id_rsa.pub` to copy the contents of your
public key into the clipboard. If you're running another system, just open the
`~/.ssh/id_rsa.pub` file and copy the contents manually.

Visit the [BowTie Account Keys](https://bowtie.io/keys/new) page and paste the
contents of your clipboard into the "Key" field. Give the key a title that
you'll remember this machine by and hit "Save."

You'll see a list of Keys that you've added to the system by their title and
a fingerprint. To determine the fingerprint of the key on your system, you can
run

```bash
$ ssh-keygen -l -f ~/.ssh/id_rsa.pub
2048 6f:10:2d:b6:67:f0:99:8f:b9:61:dc:7c:3f:a1:84:5f james@Jamess-MacBook-Pro.local (RSA)
```

When debugging Repository access, comparing the key fingerprints is a good place to start.

## Cloning the Repository

After creating a Project with BowTie's web-based Dashboard, your Project
repository will contain a Jekyll installation with a new theme. Cloning your
repository to your local system

```bash
$ git clone git@git.bowtie.io/example
Cloning into 'example'...
remote: Counting objects: 215, done.
remote: Compressing objects: 100% (205/205), done.
remote: Total 215 (delta 18), reused 0 (delta 0)
Receiving objects: 100% (215/215), 1.57 MiB | 576.00 KiB/s, done.
Resolving deltas: 100% (18/18), done.
Checking connectivity... done.
```

Now you'll have a directory at `./example` with the following contents:

```bash
$ ls
400.html      404.html      _config.yml   _layouts      _sass         about.md
favicon.ico   img           index.json    maintenance   settings.json
403.html      500.html      _includes     _posts        _site         css
feed.xml      index.html    js            posts.html    vendor
```

## BowTie Files

### Settings

BowTie installs the `settings.json` file containing several values used for
running BowTie tools and configuring site settings. We don't advise making
modifications to this file directly at this point in time.

### Splash Page

The `index.html` and `index.json` file contain the contents and the data for
generating your BowTie splash page, and interact closely with the Splash Page
Editor on the BowTie Project Dashboard.

The `index.html` file contains a number of handlebars templates - these will
differ from the liquid-based templates that Jekyll uses. Please take care when
making modifications here if you expect to make most of your edits from the
Splash Page Editor and not manually.

### Maintenance

The contents of the `maintenance` folder become your site root when a Project's
maintenance mode is enabled.

### Error Pages

The `{400,403,404,500}.html` files contain your error documents. If a request
submitted to your application is not found, the `404.html` file will be served.
If a request submitted to your application generates a server error, the
`500.html` file will be served.

Any HTTP status code within the 400's that's not more explicitly specified by
another file will be handled with the `400.html` file.

## Jekyll

All other content in your repository is purely Jekyll based. `_config.yml` is
the base Jekyll configuration file. `_layouts` contains Jekyll layouts that
you'll probably want to modify to adjust your site's layout and appearance.
`_posts` contains blog posts for your site in markdown.

The `_site` folder is the Jekyll build folder and should not be committed.

Please [see the Jekyll Documentation](http://jekyllrb.com), and especially the
[Directory Structure](http://jekyllrb.com/docs/structure/) section to get an
overall familiarity with how Jekyll is structured.

## Development

If you're unfamiliar with
[Git](http://git-scm.com), please thoroughly read the documentation and
[Getting Started](http://git-scm.com/book/en/v2/Getting-Started-About-Version-Control)
guides before starting development.

### Branches

Your Project directory (your local clone) contains three remote branches and one
local branch.

```bash
$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/development
  remotes/origin/master
  remotes/origin/staging
```

Changes to the `master` branch will be rendered in the live production version of your
Project. We recommend checking out the `development` branch while performing site
development:

```bash
$ git checkout development
Branch development set up to track remote branch development from origin by rebasing.
Switched to a new branch 'development'
```

You'll now have a local `development` branch that tracks the origin development branch,
which basically means that Git expects the branches to represent the same line of
development.

### Previewing Changes

In your cloned Project's directory (your local checkout), run the BowTie client:

```bash
$ bowtie serve
Configuration file: /Users/james/example/_config.yml
            Source: /Users/james/example
       Destination: /Users/james/example/_site
      Generating...
                    done.
 Auto-regeneration: enabled for '/Users/james/example'
Configuration file: /Users/james/example/_config.yml
[2015-02-03 15:52:02] INFO  WEBrick 1.3.1
[2015-02-03 15:52:02] INFO  ruby 2.1.3 (2014-09-19) [x86_64-darwin13.0]
[2015-02-03 15:52:02] INFO  WEBrick::HTTPServer#start: pid=66488 port=4000
```

This launches the development server at "http://localhost:4000", which you
should now be able to browse to.

Changes to files within the example directory triggers a rebuild without
needing to restart the server.

The BowTie client wraps the general Jekyll system, and captures requests to
`/users/*` and `/bowtie/*` which BowTie's platform will handle for you.

I'll add a quick blog post to our Project:

```bash
$ vim ./_posts/2015-02-03-lack-of-sleep-and-startups.markdown
```

```text
---
layout: post
title:  "Sometimes I Just Need a Nap"
date:   2015-02-03 02:36:00
categories: startups
---

# The Origins of Sleep

...

# Why a Nap is Enough

...

# Why You're Going to Wake Up Too Soon, Anyway

...
```

And then commit the change:

```bash
$ git status

On branch development
Your branch is up-to-date with 'origin/development'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        _posts/2015-02-03-lack-of-sleep-and-startups.markdown

nothing added to commit but untracked files present (use "git add" to track)

$ git add _posts/2015*
$ git commit -a -m "Adds Post on Lack of Sleep"
[development 98f2005] Adds Post on Lack of Sleep
 1 file changed, 18 insertions(+)
 create mode 100644 _posts/2015-02-03-lack-of-sleep-and-startups.markdown
```

## Pushing Changes

Once you've made your local chnages and you're ready to see those changes on the
BowTie site, you just need to push those changes to BowTie:

```bash
$ git push origin development

unting objects: 4, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 572 bytes | 0 bytes/s, done.
Total 4 (delta 1), reused 0 (delta 0)
remote: Initiating Project Render for 'development'
remote: Extracting Project Snapshot
remote: Rendering
remote: WARNING: Your kernel does not support swap limit capabilities. Limitation discarded.
remote: [23:12:41] Working directory changed to ~container
remote: [23:12:43] Using gulpfile ~container/Gulpfile.js
remote: [23:12:43] Starting 'default'...
remote: [23:12:43] Starting 'build'...
remote: Configuration file: /container/snapshot/_config.yml
remote: Configuration file: /container/snapshot/_config_bowtie.yml
remote: Configuration file: /container/_jekyll_config_overrides.yml
remote:             Source: /container/snapshot
remote:        Destination: /container/staging
remote:       Generating...
remote:                     done.
remote:  Auto-regeneration: disabled. Use --watch to enable.
remote:
remote:
remote: [23:12:46] Finished 'build' after 3.59 s
remote: [23:12:46] Starting 'upload'...
...
remote: [23:12:47] [create] jan31-a/development/startups/2015/02/03/lack-of-sleep-and-startups.html
remote: [23:12:47] [skip]   jan31-a/development/vendor/magnific-popup/src/js/gallery.js
...
remote: [23:12:47] Finished 'upload' after 553 ms
remote: [23:12:47] Finished 'default' after 4.15 s
remote: Completed Project Render for 'development'
To git@git.bowtie.io:jan31-a.git
   67187f6..98f2005  development -> development
```

BowTie received the commit, rebuilt your Project, and pushed it to it's content delivery
system.

Visiting your development site (in this case "https://example-development.bowtied.io/"),
shows the changes have been applied.

## Working up to Production

After a serious round of development you're ready to push the changes from your development
branch into the master branch and onto your production system:

```bash
$ git checkout staging
$ git merge development
$ git push origin staging
...
```

Once our changes have been reviewed - generally by someone who's not you, but in any case,
it's always good to make a sanity check, we're ready to push to production:

```bash
$ git checkout production
$ git merge staging
$ git push origin production
```

Assuming there are no conflicts (if you run into these please read the Git documentation
on resolving them carefully), you'll see the rebuild process take place on BowTie,
and once it's done, your updated Project will be living on the production environment!
