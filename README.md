filefrog/htpasswd
=================

This image wraps up the Apache htpasswd utility for creating,
verifying and updating auth database files, for use in a variety
of web servers.

[See it on Docker Hub!][1]


Running it on Docker
--------------------

To run this in your local Docker daemon:

    $ docker run --rm -it filefrog/htpasswd -nB user
    New password:
    Re-type new password:
    user:$2y$05$G7ettX3mGfcd2AD9RAYZRea7t.z5ZwM9bT5MYqzF16Ru8aLu4euIy

This will prompt for a password, and then emit the line for the
named user, to be appended to an existing auth file, or to use for
creating a brand new one.

If you already have the password, and want to automate, you can
use the `-b` flag and run it thusly:

    $ docker run --rm -it filefrog/htpasswd -bnB user foo
    user:$2y$05$KwL/0RbBVIZibn9Oeah18.y7uZ8G7i1/bDqva7oyHejSKAZL2K5X2

In fact, if you forget how to use htpasswd itself, just run the
image as a container, and pass it the `-h` flag:

    $ docker run --rm -it filefrog/htpasswd -h

This image is so dang useful, I often alias `htpasswd` itself to
the `docker run ...` incantation:

    $ alias htpasswd='docker run --rm -it filefrog/htpasswd'
    $ htpasswd -bnB user password

etc.


Building (and Publishing) to Docker Hub
---------------------------------------

The Makefile handles building pushing.  For jhunt's:

    make push

Is all that's needed for release.  If you want to build it
locally, you can instead use:

    make build

If you want to tag it to your own Dockerhub username:

    IMAGE=you-at-dockerhub/htpasswd make build push

By default, the image is tagged `latest`.  You can supply your own
tag via the `TAG` environment variable:

   IMAGE=... TAG=$(date +%Y%m%d%H%M%S) make build push

Happy Hacking!


[1]: https://hub.docker.com/r/filefrog/htpasswd
