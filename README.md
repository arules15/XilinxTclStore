# XilinxTclStore

Welcome to the Xilinx Tcl App Store GitHub Repository!

A Tcl app store is an open source repository of Tcl code designed primarily, but not necessarily for use with the Xilinx Vivado Design Suite.  An app is a grouping or collection of one or more Tcl scripts that is published and maintained by an owner.  The app owner acts as a gatekeeper for that code and we only accept contributions for an app from the owner.  In addition, the entire repository is managed by a Xilinx gatekeeper that controls pushes to the public repo.

This project is currently in a "beta" phase, and we are limiting access.  To contribute, either by adding a new app, or by modifying an existing app, please send an email to:
tclstore@xilinx.com

[Click Here to go to the Wiki](https://github.com/Xilinx/XilinxTclStore/wiki/Xilinx-Tcl-App-Store-Home)


## To Contribute
1. Get a github account \<USER\> and download and install git on your machine (GitHub for Windows)
2. Ask for permission to XilinxTclStore repository by sending e-mail to tclstore@xilinx.com
3. Sign on to github.com
4. Switch to Xilinx at upper left side by your account name \<USER\>
5. Click Xilinx/XilinxTclStore under Repositories<p>
   Press "Fork"(upper right hand side) and create fork of XilinxTclStore to your account<p>
   https://help.github.com/articles/fork-a-repo
6. Switch to a shell on your machine (we recommend GitShell for windows)

### Checkout the Repository

If you have already cloned the repository then skip this step. Otherwise to pull this repository from within a firewall you will need to configure http.proxy and https.proxy as some company might enforce HTTPS over HTTP.  Note this setting may be different for your system.  If you have questions contact your IT network administrator:
```bash
git config --global https.proxy https://proxy:80
git config --global http.proxy http://proxy:80
```

### Setting up User Name and Email

```bash
#Create and cd to a working directory, for instance ~/github/
mkdir <WORKING_DIR>
cd <WORKING_DIR>
git config --global USER.name <USER>  #github USER name
git config --global USER.email your_email@your_company.com
```

5. Clone the repository

We recommend working off of only the master branch for simplicity.  You can work on a different branch but this requires additional syncing and merging.  If you are familiar with this methodology you can use it, otherwise stick with working off the master branch of each repo.  You need to clone your fork of the Xilinx master repo to your local area.  Don't foget to substitute \<USER\> for your real github account name:

On Windows

```bash
cd <WORKING_DIR>
git clone https://github.com/<USER>/XilinxTclStore.git
```

On Linux

```bash
cd <WORKING_DIR>
git clone https://<USER>@github.com/<USER>/XilinxTclStore.git
```

You will need to enter your github password when prompted.

Now you have cloned the repo directories under "\<WORKING_DIR\>/XilinxTclStore"

cd \<WORKING_DIR\>/XilinxTclStore

```bash
git status
```

6. Set up remote to point to the Xilinx master repo if this has not been done yet.  This is required to be able to sync the local repo with the Xilinx master repo

```bash
git remote add upstream https://github.com/Xilinx/XilinxTclStore.git
```

7. Check out the entire master branch (you can also check out individual files by passing the specific file name).  Below is the command for checking out the entire default branch.
```bash
git checkout 
```

8. Add your application code to the respective directory.  For a new app, create the directories following the taxonomy tclapp/\<YOUR_COMPANY\>/\<YOUR_APP\> (for an example see tclapp/mycompany/myapp), including test code.  Note you can use your github account name in place of \<YOUR_COMPANY\> if you would like.<p>
    For more information on creating application, refer to the following section<p>
    ####My First Vivado Tcl App.

9. Mark files for adding. Make sure you add all necessary files, including the tclIndex, pkgIndex.tcl, and package provider files  (3 in addition to the "normal" tcl source files.  The tclIndex and pkgIndex.tcl files are generated by Vivado - described later in the section for My First Vivado Tcl App. 
```bash
cd ./XilinxTclStore
git add tclapp/<YOUR_COMPANY>/<YOUR_APP>
```

10. Commit to local repository
```bash
git commit -m "your description of the changes"
```

11. Push to your cloned master \<USER\>/XilinxTclStore in Github
```bash
git push origin
```

12. Send Pull Request.  Switch back to github.com in a web browser, and navigate to your repo
https://help.github.com/articles/creating-a-pull-request
Press "Pull Request" button right upper-ish <p>
Add any additiona note if you wish<p>

Done!


## As a Gate Keeper (app owner)

Make sure you are set up as a normal contributor (name/email/proxy config settings)

Since you will be merging content from other branches and repos, you need to set some merge configuration options:
```bash
git config --global merge.defaultToUpstream true
```

1. Create a repository by cloning XilinxTclStore, skip to next step if repository already exists locally
```bash
On Windows
git clone https://github.com/<USER>/XilinxTclStore.git
On Linux
git clone https://<USER>@github.com/<USER>/XilinxTclStore.git
```

2. Update local repo with github master
```bash
git fetch
```

3. Merge any changes
```bash
git merge --ff
```

4. Set up remote to point to the Xilinx master repo if this has not been done yet.  This is required to be able to sync the local repo with the Xilinx master repo
```bash
git remote add upstream https://github.com/Xilinx/XilinxTclStore.git
```

5. Update local repo with \<USER\> branch
```bash
git fetch remote_name
```

6. Merge changes from \<USER\> branch.  Use "master" or the name of the branch if the user forked.
```bash
git merge remote_name/remote_branch
e.g.
git merge upstream/master
```

7. Fix any merge conlicts

8. Add the changes and commit
```bash
git add .
git commit -m "update notes"
```

9. Run tests and check content

10. Push to github or go to step 11
```bash
git push origin master
```
go to Step 12

11. Go to Github.com
Pull Request from the \<USER\>.<p>
If everything is good, merge, add comments and close the pull request.<p>
If something is not good, add comments so the requester can make changes.<p>
If something is bad, add comments, reject it and close the pull request.<p>
https://help.github.com/articles/merging-a-pull-request

12. Delete the local repository, or forked branch if you created one.
```bash
git branch -r -d remote_name/remote_branch
e.g.
git branch -r -d raj/rajklair
```
 Or in browser, delete this branch after merging when prompted.

Done

## My First Vivado Tcl App

### Let Vivado know where your cloned Tcl repository is located

Before you start Vivado, there is an environment variable to change the location of the default repository.  YOu need to change this to your local working directory to test the app and generate some needed files.  Set XILINX_TCLAPP_REPO to the location of your cloned repository.  NOTE - this environment variable will be replaced with a Tcl param in 2014.1, but for now (2013.4) you will need to use an env variable.
```bash
export XILINX_TCLAPP_REPO=<WORKING_DIR>/XilinxTclStore
```
Some of the Tcl app related commmands in Vivado require a Tcl repo to be present so it is important the
env variable is set before you start Vivado.  Once this is set - do not change it without restarting vivado, we do not currently support multiple repos, and there can be issues if code is not located where it is expected.  We will improve this over time.

### Fetch and merge updates to your cloned repository

If you have already cloned the repository, then you may want to fetch and merge the latest updates into your clone.<p>
The lastest and greatest official apps are available in the "master" branch so this is where you want to merge into.<p>

```bash
cd XilinxTclStore
git checkout master
git fetch
git merge
```

### Create the Directory Structure

The directory structure should follow \<WORKING_DIR\>/tclapp/\<YOUR_COMPANY\>/\<YOUR_APP\>/...
```bash
mkdir -p ./tclapp/mycompany/myapp
cd ./tclapp/mycompany/myapp
```

More directory and testing structure can be found in tclapp/README.

### Create the Package Provider

Every app needs a tcl script that provides packaging information to Vivado.  This is called the package provider.  The name of the script can be whatever you like, but the contents of the file must be the same as published below.  We suggest a .tcl file with the same name as your app, \<YOUR_APP\>. See one of the existing apps for an example.
```bash
vi ./myapp.tcl
```

Change the version and namespace to match your app.  Note that you can also require specific Vivado versions.  See other apps in the repository for examples.  Create a tcl file with the name of your app in the appropriate app directory and paste the following code in it - again modified appropirately for your app:
```tcl
# tclapp/mycompany/myapp/myapp.tcl
package require Tcl 8.5

namespace eval ::tclapp::mycompany::myapp {

    # Allow Tcl to find tclIndex
    variable home [file join [pwd] [file dirname [info script]]]
    if {[lsearch -exact $::auto_path $home] == -1} {
    lappend ::auto_path $home
    }

}
package provide ::tclapp::mycompany::myapp 1.0
```


### Customize the App

Your app scripts will not be able to have this same name, but could be placed inside of this package provider file.
If you already have the app created, then copy it into \<WORKING_DIR\>/tclapp/\<YOUR_COMPANY\>/\<YOUR_APP\>/.
If you are creating the app from scratch, then:
```bash
vi ./myfile.tcl
```

You need to make sure of a couple things:

1. You must have all procs in namespaces, for example:
```tcl
# tclapp/mycompany/myapp/myfile.tcl
proc ::tclapp::mycompany::myapp::myproc1 {arg1 {optional1 ,}} {
    ...
}
```

2. Add the commands that you would like to export to the top of each file.  It is important
that you are explicit about the commands, in other words, do *not* use wildcards.
```tcl
# tclapp/mycompany/myapp/myfile.tcl
namespace eval ::tclapp::mycompany::myapp {
    # Export procs that should be allowed to import into other namespaces
    namespace export myproc1
}
proc ::tclapp::mycompany::myapp::myproc1 {arg1 {optional1 ,}} {
    ...
}
```

3. You **must** have 4 "meta-comments" which describe your procedure interfaces - inside of the procedures,
and each meta-comment **must** be seperated by new lines (without comments)
```tcl
# tclapp/mycompany/myapp/myfile.tcl
namespace eval ::tclapp::mycompany::myapp {
    # Export procs that should be allowed to import into other namespaces
    namespace export myproc1
}
proc ::tclapp::xilinx::test::myproc1 {arg1 {optional1 ,}} {

    # Summary: A one line summary of what this proc does

    # Argument Usage:
    # -arg1 <arg> : A one line summary of this argument which takes a value indicated by <arg>.
    # [-optional1 <arg> = <opt1_default>] : A one line summary of an optional argument that takes a value and which has a default
    # [-optional2] : A one line summary of an optional arg that does not take a value (aka a flag)

    # Return Value:
    # TCL_OK is returned with result set to a string

    # Categories: xilinxtclstore, projutils


    ...
}
```
Each of these meta-comments is interpreted by Vivado at run-time. It is critical that they be present and correct in your app
or it may not function correctly. The following is a description of each meta-comment.

#### Summary

The text following "Summary:" should be a brief, one-line description of your app.

#### Argument Usage

This is the most complex of the meta-comments. As shown in the above example, there should be one line for each mandatory or
optional arg supported by your app. Optional args should be enclosed within []. Args which should be accompanied by a
value **must** be followed by the literal text <, "arg", and >, indicating to the USER where the value should be placed. The
summary should explain what are the valid values that a USER might use.
You can also specify a default value, which is a value which will be assumed if the USER does not specify the given optional
arg. You can also have optional args that do not take any value (these are often referred to as "flags"). For a flag,
it's presence on the command line implies a value of true, indicating that some optional action should be take by
the app. An exception to this rule is if the name of the flag is prefixed with "no_" (for example, -no_cleanup), in which case
a value of false is implied, indicating that the app will not take some action which by default it normally performs.

You can also specify positional args. A positional arg is for which just a value is specified
and that has no corresponding flag (e.g. -arg1).

Here is a more concrete example:

```tcl
        # Argument Usage:
        # file: Name of  file to generate
        # -owner <arg>: USERname of the owner of the file to be generated.
        # [-date <arg> = <todays_date>]: The date to use in yyyy/mm/dd format, will default to today's date if not specified.
```

This example app has one mandatory positional arg, which is the name of a file it will generate. It also has a mandatory
flag -owner, and an optional arg -date, which has a default value. Assuming this app was called "touch", an example usage might be:

touch /home/joe_USER/myfile -owner root

Use of this command would result in the creation of a file named /home/joe_USER/myfile, owned by root, and with
a file creation date of today.


#### Return Value

Use this meta-comment to specify the possible return values for your app.

#### Categories

Use this meta-comment to specify which categories in the Vivado help system your app should be listed. "Categories:"
should be followed by a comma-separated list. By convention, the first category listed should always be "xilinxtclstore".
Any additional categories are up to you as the app developer.


### Create the Package Index and Tcl Index

To create neccessary tcl index and package files, invoke Vivado (without creating log and journal files).  The instructions below will run commands to create these necessary files in the current directory.

```bash
cd ~/XilinxTclStore/tclapp/mycompany/myapp
vivado -mode tcl -nolog -nojournal
```

In Vivado, now issue these Tcl commands:

```tcl
Vivado% pkg_mkIndex .
Vivado% auto_mkindex .
Vivado% exit
```


### Running the Linter

There is tool in Vivado that checks some basic requirements for the Tcl app store.  This is called a "linting" tool.

If you are not already in Vivado:
```bash
vivado -mode tcl -nolog -nojournal
```

There should be a lint_files command available at this point:
```tcl
Vivado% lint_files [glob XilinxTclStore/tclapp/mycompany/myapp/*.tcl]
```

Correct anything the linter identifies as a problem.  Exit Vivado when you are done.


### Check the App before you Deploy

1. Set XILINX_TCLAPP_REPO to point where the local XilinxTclStore is
```bash
export XILINX_TCLAPP_REPO=<WORKING_DIR>/XilinxTclStore
```
or just the path
```bash
export XILINX_TCLAPP_REPO=<WORKING_DIR>
```
Run Vivado
```bash
vivado -mode tcl
```

When the env variable is set, Vivado automatically adds the location of the repository to the
auto_load path in Tcl.

2. Start testing<p>

Require the package that was provided by the app

```tcl
vivado% package require ::tclapp::mycompany::myapp
```

Optionally import an exported proc

```tcl
namespace import ::tclapp::mycompany::myapp::*
myproc1
...
```

### Setting up a per repository User Name and Email

```bash
cd ~/XilinxTclStore
git config USER.name “johnd”
git config USER.email “johnd@mycompany.com”
```


### Commit Changes

Make sure you commit your \<USER\> branch.

```bash
cd ~/XilinxTclStore
git checkout myorg-johnd
git add .
git status
git commit -m "created myapp for mycompany"
git push origin mycompany
```

