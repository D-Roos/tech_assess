> Please write an ansible role that is able to deploy the httpd application as an rpm. The written code must meet the following criteria:
  - role should be documented so someone with no knowledge of httpd can use it.
  - must be possible to roll out new version, roll back to older version, re-deploy current version.
  - must keep configuration separate from code.
  - optional bonus: have secrets in vault if any are needed
  - must support managing multiple servers with one instance of httpd each
  - must be able to deploy without affecting customer experience (with cluster of 3 nodes or more)
  - backups are out of scope
  - monitoring is out of scope
  - code must be in git(hub), commit history must be visible
  - must be able to run on centos 7.5
  - application must automatically start when machine is rebooted
  - out of scope: applications must be automatically started if crashed
  - must support ansible 2.6 or later
  - must be idempotent
  - application should be pulled by the server on which the application is to be installed. Not pushing from a central location.
  