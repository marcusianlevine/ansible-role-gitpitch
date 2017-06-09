marcusianlevine.gitpitch
=========

Installs and configures GitPitch on a standalone server. GitPitch is a presenation framework that reads Markdown files from hosted Git repositories and prepares dynamic Reveal.js presentations.

Role Variables
--------------

### Required
* play_secret_key

### Optional
* domain (if not provided, whichever of hostname or IP is available will be used)

Dependencies
------------

* jpnewman.java
* deiga.sbt

Example Playbook
----------------

    - hosts: servers
      roles:
         - jpnewman.java
         - deiga.sbt
         - { role: marcusianlevine.gitpitch, play_secret_key: 42 }

License
-------

BSD

Author Information
------------------

Written by Marcus Levine for CKM Advisors (mlevine@ckmadvisors.com)
