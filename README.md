Buildpack for Grails
=====================

This is a [buildpack](https://www.cloudcontrol.com/dev-center/Platform%20Documentation#buildpacks-and-the-procfile) for
Grails apps.

## Usage

Create a Git repository for a Grails 1.3.7 or 2.0 app:

    $ cd mygrailsapp
    $ ls
    application.properties    lib        src               target    web-app
    grails-app                scripts    stacktrace.log    test
    $ grails integrate-with --git
    | Created Git project files..
    $ git init
    Initialized empty Git repository in /Users/jjoergensen/mygrailsapp/.git/
    $ git commit -m init
    [master (root-commit) 7febdd9] init
     58 files changed, 2788 insertions(+), 0 deletions(-)
     create mode 100644 .classpath
     create mode 100644 .gitignore
     create mode 100644 .project
     create mode 100644 application.properties
    ...
    
Create a cloudControl app and push your code

    $ cctrlapp APP_NAME create java
    $ cctrlapp APP_NAME push
    [...]
    -----> Receiving push
    -----> Grails 2.2.0 app detected
           WARNING: The Grails buildpack is currently in Beta.
    -----> Installing OpenJDK 1.6...
    -----> Installing Grails 2.2.0.....
    -----> Done
    -----> Executing grails -Divy.default.ivy.user.dir=/srv/tmp/buildpack-cache compile --non-interactive
            [...]
    -----> Executing grails -plain-output -Divy.default.ivy.user.dir=/srv/tmp/buildpack-cache war --non-interactive
            [...]
    -----> No server directory found. Adding webapp-runner 7.0.40.0 automatically.
    -----> Building image
    -----> Uploading image (73M)
    
    To ssh://APP_NAME@cloudcontrolled.com/repository.git
     * [new branch]      master -> master
    

### Auto-detection

cloudControl auto-detects Grails apps by the existence of the `grails-app` directory in the project root and the `application.properties`  file is also expected to exist in the root directory. 

### Using a Customized (Forked) Build Pack
This is our default buildpack for Grails applications. In case you want to introduce some changes, fork our buildpack,
apply changes and test it via [custom buildpack feature](https://www.cloudcontrol.com/dev-center/Guides/Third-Party%20Buildpacks/Third-Party%20Buildpacks):

    $ cctrlapp APP_NAME create custom --buildpack https://github.com/cloudControl/buildpack-grails.git

## License

Licensed under the MIT License. See LICENSE file.
