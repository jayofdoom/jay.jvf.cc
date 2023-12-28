+++
title = "Running OpenStack Ironic Unit Tests in PyCharm"
date = "2023-12-28T14:33:52-07:00"
author = "Jay Faulkner"
authorTwitter = "jayofdoom" 
#cover = "What I plan to talk about here, and how it works"
tags = ["pycharm", "openstack", "tests", "jetbrains", "ironic"]
keywords = ["pycharm", "openstack", "tests", "jetbrains", "ironic"]
parent = "posts"
description = "It's easy, but it's nice to have a guide :)"
showFullContent = false
+++
# OpenStack Ironic + PyCharm + Unit Tests

I assumed for a long time it was likely trivial to get OpenStack Ironic unit
tests running in PyCharm, but never took the time to get a reliably working
configuration -- until today. I'm going to describe the configuration here so
hopefully it can be replicated by others.

It's my belief this should work for most OpenStack projects using oslotest, but
I've only used this method so far with Ironic-based projects. As always, please
check the codebase and documentation if anything doesn't work; this is a
point-in-time blogpost with limited scope not a full document.

## Environmental information:
- Gentoo Linux
- PyCharm Professional 2023.3.2
- Python 3.11.7
- Ironic master branch @ cf7b182ac38e852e12e97494a5e184992fb3b2b6

## Initial IDE setup:
As always, when loading up a new Ironic checkout without a virtualenv, PyCharm
offered to create one. I accepted the offer and created one in
`ironic/.tox/pycharmvenv`. Putting the environment inside the `.tox` directory
is  useful to ensure that directory will be ignored by OpenStack projects'
linters and `.gitignore` files while also keeping it alongside the code.

The initial setup will default to pulling in your `requirements.txt` packages,
however for Ironic and most other OpenStack projects, there are additional
packages to install for testing and optional features. So I open the built-in
terminal, which has a `(pycharmvenv)` because it was already activated. Inside
this environment, I installed the remaining requirements:
`pip install -r test-requirements.txt -r driver-requirements.txt`. 

At this point have PyCharm is configured for Ironic, with all needed libraries
loaded. This is a useful state for doing development in generally, as I can now
easily reference library code and signatures, and get improved autocompletion.

## Unit test configuration:
Now, I set up a unit test configuration. There is a `tox` test runner in
PyCharm, however, it does not do a great job of showing individual results or
allowing single tests to be re-run. This makes it not extremely useful for my
purposes, especially since I already have a configured virtual environment.

Instead, I used the `unittest` based runner. I went into the Run/Debug
configurations dialog, clicked the plus on the top left of the toolbar, and
chose Python Tests -> Unittests. I changed target to "Module name", input
`ironic.tests` as the module name, verified the Python interpreter was
configured to the previously configured virtual environment and left the other
options as default.

Now I can click "Run" on this configuration and run all unit tests.
Additionally, for running single tests, I can click the play button beside a
single test method or class. Note that tests can be broken in such a way that
they fail unless run with other tests in their class.

## Unit Test Debugging
This was most of what I needed to do to get debugging working, too. Due to our
reliance on eventlet/greenlet, I needed to change one setting in PyCharm -- in
Settings -> Build, Execution, Deployment -> Python Debugger, I checked "Gevent
compatible" to enable Gevent compatability mode, which fixes compatability
issues with greenlet as well.

Once this option was set, I could set a breakpoint, right click a test, and
choose to debug it and it worked flawlessly.

## Other useful notes
- I tried to use IDEA Ultimate instead of PyCharm for python for a while. The
  virtualenv integration is completely missing, and it's worth every penny just
  to upgrade to the full set of IDEs so you can use PyCharm if you like
  JetBrains IDEs.
- This process mostly works on Windows as well, although I used the built-in
  support for setting up a virtualenv via WSL on Windows (and I used IPA unit
  tests, which I know work in WSL).
- JetBrains offers free PyCharm licenses for use by OpenStack community 
  contributors to use to contribute to Open Source. See 
  [the mailing list](https://lists.openstack.org/pipermail/openstack-discuss/2020-July/016039.html)
  for more information.
- I still run `tox -epep8` and `tox -epy3` on any changes before pushing
  them up. These better mimic the gate and ensure things are in good shape,
  even if I find the IDE-based tests more convenient for development.


Disclaimer: I pay out of my own pocket for all my JetBrains licenses. This was
not any kind of paid endorsement, I'm just documenting my process so I can
remember it and maybe you can get some help out of it as well.