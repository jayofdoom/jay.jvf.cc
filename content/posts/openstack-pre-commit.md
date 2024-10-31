+++
title = "Setting up pre-commit for the forgetful"
date = "2024-10-31T15:45:52-00:00"
author = "Jay Faulkner"
authorTwitter = "jayofdoom" 
tags = ["pre-commit", "openstack", "tests", "ironic"]
keywords = ["pre-commit", "openstack", "tests", "ironic"]
parent = "posts"
description = "Never forget to run `pre-commit install` again..."
showFullContent = false
+++
# OpenStack + pre-commit 

Many OpenStack projects, including Ironic and many SDK and oslo projects, now
utilize [pre-commit](https://pre-commit.com) to perform linting at commit time.

This tool has a major downside: git hooks have to be enabled locally. If
you're someone who can easily forget things, and works in many diverse repos,
this can lead to not utilizing this tool, which is unfortunate.

Luckily, I've found a solution! Templates are supported for git configs when
you `git clone` or `git init` a repo, these are located. This means we can
enable a pre-commit hook by default in all our repos:

```bash
git clone https://opendev.org/openstack/ironic ironic
cd ironic
pre-commit install
sudo cp .git/hooks/pre-commit /usr/share/git-core/templates/hooks/
```

This means every new cloned or initialized git repo on this system will have
the pre-commit hook by default. This means you get an non-fatal error on
repositories with no pre-commit config -- no big deal for me.

Hope you find this trick helpful!
