---
title: Bitbucket Repo Sync Application
categories:
  - PHP
tags:
  - bitbucket
  - git
---
I always `shift+delete` or `rm -rf` my old project files and keep my workspace *very* clean. Let's say it's a bad habit after working with SVN for several years and relying on server backups. Oh yes, I am not keeping backups of my projects and so comfortable with it!

[Bitbucket](http://bitbucket.org/) is cool with unlimited private repos but the [downtime](http://blog.bitbucket.org/2012/01/05/unplanned-downtime-today/) they had yesterday proved that you shouldn't rely on it if you don't have copies of your repositories on your own disk. I wrote a small console application using [symfony console component](http://symfony.com/doc/2.0/components/console.html) to sync all repositories of a user by utilizing bitbucket API.

Basically, you give your bitbucket credentials and it clones all your git repositories.

## Installation and Usage

```
git clone git@bitbucket.org:eabay/bitbucket-repo-sync.git
cd bitbucket-repo-sync
php composer.phar install
php src/console.php bitbucket:sync username password
```

You can choose the path of repositories:

```
php src/console.php bitbucket:sync username password -d /some/where
```

To get help about the command:

```
php src/console.php help bitbucket:sync
```

The ironic part is that project is [hosted](https://bitbucket.org/eabay/bitbucket-repo-sync) at bitbucket. I think I should define another remote like github. :)

> Notice that repositories are cloned over https schema including your username and password. I mean repositories will have origins with uris like `https://username:password@bitbucket.org/`. If this is a security problem for you, don't use the application!
