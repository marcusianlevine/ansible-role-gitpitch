marcusianlevine.gitpitch
=========

Installs and configures GitPitch on a standalone server. [GitPitch](https://github.com/gitpitch/gitpitch) is a presenation framework that reads Markdown files from hosted Git repositories and prepares dynamic Reveal.js presentations.

This role follows the [offical GitPitch Server Deploy guide](https://github.com/gitpitch/gitpitch/wiki/Server-Deploy-Instructions) very closely.

Role Variables
--------------

### Required
* play_secret_key

This is a long ASCII string that is used to sign sessions and cookies. The more worried you are about security, the longer it should be — at least 64 characters.

You can generate a key using either a random string generator of your choice, or using the [offical Play framework command line utility](https://playframework.com/documentation/2.5.x/ApplicationSecret#Generating-an-application-secret).

Since this value is sensitive, you shoud use [Ansible Vault](http://docs.ansible.com/ansible/playbooks_vault.html) to encrypt it in your playbooks.

### Optional

* domain
  * If not provided, whichever of hostname or IP is available will be used
* git_key_file
  * If the version of gitpitch you would like to deploy is not hosted in a public repository, you can provide a key file which will be used to authenticate when cloning the repo
* gitpitch_repo_services
  * If you wish to use custom [Git Repo Services](https://github.com/gitpitch/gitpitch/wiki/Git-Repo-Services), provide a list of dictionaries of the form found in `defaults/main.yml`
* use_ssl
  * if you plan to setup SSL termination in front of your GitPitch server, setting this to true will configure Play for HTTPS traffic
* gitpitch_host
  * if you want to specify the host address at which the GitPitch server should listen
  * Default: 127.0.0.1 (localhost)
* gitpitch_port
  * if you want to specify the port that the GitPitch server should listen on
  * Default: 9000

If you are using an unreleased custom version of GitPitch, you can provide a repo URL and/or branch specification with the following pair of variables:
* gitpitch_repo
* gitpitch_branch

Prerequisites
------------

This role does not install Java, so you need to make sure it is already installed on the hosts to be configured.

If your target OS is supported, you can easily add [the Galaxy role `jpnewman.java`](https://galaxy.ansible.com/jpnewman/java/) to your playbook.

Dependencies
------------

* marcusianlevine.sbt

Example Playbook
----------------

    - hosts: servers
      roles:
         - jpnewman.java
         - deiga.sbt
         - { role: marcusianlevine.gitpitch, play_secret_key: 42 }

Limitations
-----------

Note that this role only installs and builds GitPitch, it does not:

* configure a reverse proxy server or SSL termination as recommended in the official [Play production deployment guide](https://playframework.com/documentation/2.5.x/HTTPServer)
* start the Play server as a background process using e.g. systemd, initd, or supervisord

License
-------

BSD

Author Information
------------------

Written by Marcus Levine for CKM Advisors (mlevine@ckmadvisors.com)
