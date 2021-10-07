# docker-gentoo-web

N.B. In order to build the container image from this repo, the base images
     built by
     [docker-gentoo-build](https://github.com/srcshelton/docker-gentoo-build)
     must be present on or available to the local system.

To make use of the content container which this repo builds, you need to follow
these steps:

* Check-out this repo;
* At the top-level, add a `content` directory;
* Within this directory, create the following items:
  * A file named `group` which contains an `/etc/group` excerpt containig any
    additional groups which must exist within the container;
  * A file named `passwd` which contains an `/etc/passwd` exceprt containing
    any additional users who must be defined within the container;
  * A directory named `sites` with any static content to be created directly
    under `/var/www/`;
  * A directory named `htdocs` with any static content to be created directly
    under `/var/www/localhost/htdocs`;
  * A directory named `config` with any *override* files to be copied to webapp
    directories under `/var/www/localhost/htdocs` if the webapp is installed.
    e.g. `config/phpsysinfo/phpsysinfo.ini` would be created within the
         container as `/var/www/localhost/htdocs/phpsysinfo/phpsysinfo.ini` if
	 the webapp `phpsysinfo` is installed;
  * A directory named `cgi-bin`, which may be left empty if not further used;
  * A file named `webapps.conf` defining a shell-variable named `webapp_pkgs`
    which specifies the web-apps to install - see webapps.conf.example.

Building the container creates the content, running the container with
`/bin/true` as the entrypoint then creates volumes which can be mounted to
containers running a webserver and/or PHP in order to serve the embedded
content (noting that even FPM PHP via UNIX domain or network socket still
requires the same content as seen by the webserver process to be available on
the same path).

<!-- vi: set colorcolumn=80: -->
