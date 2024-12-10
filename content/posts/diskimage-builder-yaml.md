+++
title = "Using diskimage-builder with a single yaml file"
date = "2024-12-10T16:20:00-00:00"
author = "Jay Faulkner"
authorTwitter = "jayofdoom" 
#cover = "What I plan to talk about here, and how it works"
tags = ["ubuntu", "openstack", "images", "diskimage-builder", "ironic"]
keywords = ["ubuntu", "openstack", "images", "diskimage-builder", "ironic"]
parent = "posts"
description = "No more long command line calls to dib..."
showFullContent = false
+++
# diskimage-builder with a single yaml file

## Why diskimage-builder

With the recent move of OpenStack devstack to require/support Ubuntu 24.04
Noble, I needed to make some changes to my local environment. Previously,
I was using an unmodified Ubuntu cloud image as a base, supplying a cloud-init
ISO (created by cockpit-machines) to do just-in-time user and network
configuration.

For environmental reasons mostly irrelevant to this post, that approach doesn't
work for me anymore. So I decided to use [diskimage-builder](https://docs.openstack.org/diskimage-builder/latest/)
to create an image that's ready to go from get-go. While I've used
diskimage-builder in the past -- I actually just fixed the Gentoo element for
it -- I have typically used it to create ramdisks for IPA, and rarely to create
my own cloud base images.

## Why yaml

One of the biggest weaknesses in typical usage of diskimage-builder is that
the most obvious way to configure it is via a complex combination of command
lines and environment variables. This works good for ad-hoc or scripted use
cases, but I wanted to centralize it into one place so I didn't have to
remember (or alias) a command.

So I dug into the support diskimage-builder has for configuration via yaml file.
This support, despite being fairly comprehensive, is not clearly documented.
In the simpliest terms possible; you can convert this command::

```
    # DIB_DEV_USER_USERNAME=jay DIB_DEV_USER_PWDLESS_SUDO=1 \
      DIB_DEV_USER_AUTHORIZED_KEYS=/home/jay/authorized-keys-dib \
      DIB_RELEASE=noble disk-image-create -a amd64 -o devstack-noble.qcow2 \
      -p kitty-terminfo vm ubuntu block-device-efi devuser openssh-server \
      simple-init
```

Into this command and configuration file combo::

```
    # diskimage-builder devstack-noble.yaml
    # cat devstack-noble.yaml
    - imagename: devstack-noble.qcow2
      arch: amd64
      elements:
        - vm
        - ubuntu
        - block-device-efi
        - devuser
        - openssh-server
        - simple-init
      environment:
        DIB_DEV_USER_USERNAME: jay
        DIB_DEV_USER_PWDLESS_SUDO: "1"
        DIB_DEV_USER_AUTHORIZED_KEYS: /home/jay/authorized-keys-dib
        DIB_RELEASE: noble
      packages:
        - kitty-terminfo
```

I think the advantages are obvious -- it's much simpler (at least to me) to
to manage and version a yaml file than a long, complex command line or script.
And feel free to steal my config if you, too, want a simple Ubuntu Noble image
useful as a base for devstack :).

## More information

If your needs are different, you can do even more with the yaml -- just run
`diskimage-builder --help` for a full list of top-level keys in for the yaml.

Please also review the diskimage-builder documentation for full details on all
the elements and configurations -- it's extremely extensible and you might be
surprised what tricks are already implemented for you in diskimage-builder, if
you just know to activate the element.

