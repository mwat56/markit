# markit
[![GitHub Stable Release](https://img.shields.io/badge/Release-4.1.8-blue.svg)](https://github.com/BradleyA/markit/releases/tag/4.1.8)
![GitHub Release Date](https://img.shields.io/github/release-date/BradleyA/markit?color=blue)
[![GitHub Commits Since](https://img.shields.io/github/commits-since/BradleyA/markit/4.1.8?color=orange)](https://github.com/BradleyA/markit/commits/)
[![GitHub Last Commits](https://img.shields.io/github/last-commit/BradleyA/markit.svg)](https://github.com/BradleyA/markit/commits/)

[![GitHub Open Issues](https://img.shields.io/github/issues/BradleyA/markit?color=purple)](https://github.com/BradleyA/markit/issues?q=is%3Aopen+is%3Aissue)
[![GitHub Closed Issues](https://img.shields.io/github/issues-closed/BradleyA/markit?color=purple)](https://github.com/BradleyA/markit/issues?q=is%3Aclosed+is%3Aissue)
[<img alt="GitHub Clones" src="https://img.shields.io/static/v1?label=Clones&message=356&color=blueviolet">](https://github.com/BradleyA/markit/blob/master/images/clone.table.md)
[<img alt="GitHub Views" src="https://img.shields.io/static/v1?label=Views&message=1939&color=blueviolet">](https://github.com/BradleyA/markit/blob/master/images/view.table.md)
[![GitHub Size](https://img.shields.io/github/repo-size/BradleyA/markit.svg)](https://github.com/BradleyA/markit/)
![Language Bash](https://img.shields.io/badge/%20Language-bash-blue.svg)
[![MIT License](http://img.shields.io/badge/License-MIT-blue.png)](LICENSE)

----

Bash script that adds Git Verion Control information into files and pushes them to GitHub, Bitbucket, and/or GitLab.

## Goal
Answer one question over the phone by looking at the code; ***What version are you running?**

#### If you like this repository, select in the upper-right corner, star, [![GitHub stars](https://img.shields.io/github/stars/BradleyA/markit.svg?style=social&label=Star&maxAge=2592000)](https://GitHub.com/BradleyA/markit/stargazers/) thank you.
  
## Description
Markit is a bash script that is a wrapper around these Git commands; git add ${FILE_NAME}, git commit -m "${FILE_MESSAGE}", git tag -a ${RELEASE_VERSION}, and git push –follow-tags. It automates this Git commit process and adds two comment lines of metadata about file changes to all tracked modified files in your local Git repository.  This metadata allows any person to answer the question; What version are you running? 

Markit supports [Semantic Versioning](https://semver.org/) (MAJOR.MINOR.PATCH) and alphanumeric versioning (v0.1.64-alpha).  Markit will display the current version before prompting you to enter the next version.  Markit includes the number of commits with the version in the file(s).  I find this helpful when commiting several different changes while working on the same PATCH.

If environment variable MARKITLOCAL is set to 1, markit automates this git commit process, but does not push to GitHub repository or Bitbucket repository or GitLab project.  I find this helpful when working without network access to a remote Git repository.  If using the bash shell, enter; 'export MARKITLOCAL=1' on the command line to set the MARKITLOCAL environment variable to '1'.  Use the command, 'unset MARKITLOCAL' to remove the exported information from the MARKITLOCAL environment variable.  You are on your own defining environment variables if you are using other shells.

The two comment lines of metadata include:

 * file_name, version.commits, date, time, time zone, repository URL, Git branch, user, hostname, previous version
 * file name(s) updated and a one line breif description about changes made to the file(s)
 
Markit currently supports files with these file extensions:

c(c), C++(cc|cpp|c++|cxx), C header(h|H|hpp), C++ header(hxx|Hxx|HXX), Go(go), HTML(html|htm), Java(java|class|jar), JavaScript(js), Kotlin(kt|kts), Makefile(mk|MK), Pascal(p|pp|paa), Perl(pl|PL|psh), PHP(php|php3|php4|ph3|ph4), PowerShell(ps1|msh), Python(py), R(R), Ruby(rb), Rust(rs|rlib), Scala(scala|sc), Shell(sh|bash|csh|tcsh|ksh), Terraform(tf|tfstate), Text(txt), XML(xml), YAML(yml|yaml)

Markit currently supports these files without file extensions: Dockerfile, Makefile.  There will be a prompt to add comment character(s) for unknown file names when needed and a prompt to add a description about the changes.
     
## Objectives
* Any person without knowledge of Git or GitHub or Bitbucket or GitLab or markit to be able to answer one question; 
  **What version are you running?**
* Supports [Semantic Versioning](https://semver.org/) (MAJOR.MINOR.PATCH) and alphanumeric versioning (v0.1.64-alpha)
* Only update modified files by inserting two comment lines with metadata
* Insert the lines of metadata after the first line in files
* Support GitHub
* Use git commit message as part of metadata
* Use git tag as part of metadata
* Include date and remote Git repository as part of metadata
* Include path with filename in remote Git repository as part of metadata
* Don't create any requirements for markit other than the version and those required by Git
* Support several file extensions for comment character
* Support Bitbucket or GitLab
* Support Git local repository without network access (without 'git push')
* Support push to multiple Git remote repositories at once (edit .git/config)
* I use alias release-notes='git log --graph --pretty=format:'\''%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'\'' --abbrev-commit' to help build release notes

## Clone
To clone this repository, change to a directory you want to download the files into.  If you do not have Git installed then enter; "sudo apt-get install git" if using Ubuntu. Other Linux distribution install methods can be found here: https://git-scm.com/download/linux.  On the GitHub page of this script use the "HTTPS clone URL" with the 'git clone' command.  Copy markit and check-markit to a directory that is included in your PATH (/usr/local/bin, ~/bin).

    git clone https://github.com/BradleyA/markit
    cd markit
    cp -p {./markit,./check-markit,./find-code.sh} /usr/local/bin

## Modify Example File
First modify test file,testfiles/sample.sh, by adding a blank line to learn how markit works.

    vi testfiles/sample.sh

    #!/bin/bash
    #   testfiles/sample.sh  3.197.368  2019-02-08T20:33:53.600661-06:00 (CST)  https://github.com/BradleyA/markit  uadmin  six-rpi3b.cptx86.com 3.196-1-g46f4c0d  
    #      test markit for sample.sh 
    #
    #   ./sample.sh
    ###
    
    echo "Hello World"

## Usage: markit
Mark **tracked modified file(s)**, in your local Git repository and push those changes to a remote Git repository.  This example shows markit pushing to three remote Git repositories; GitHub, GitLab, and Bitbucket.  Enter **markit --help** to see how .git/config was edited to support three repositories.

    markit 

## Output: markit

    $ markit
    Files to be marked and pushed to remote Git repository:

    testfiles/sample.sh

    Current Git repository release number:  4.1.5
    Enter release number to commit files (examples:  3.217  3.1.231  v0.1.64-alpha) or ctrl-c to stop.

    4.1.6

    Using release number:  4.1.6

    Enter a one line description about the changes or ctrl-c to stop.
    	(example:  testfiles/sample.sh   Added logic for --help; closes #12, resolves #14):

    testing markit after editing testfiles/sample.sh

    	testfiles/sample.sh	sh

    [master ef33d26] testfiles/sample.sh -->   testing markit after editing testfiles/sample.sh
     1 file changed, 1 insertion(+), 2 deletions(-)
    Counting objects: 5, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (5/5), done.
    Writing objects: 100% (5/5), 617 bytes | 0 bytes/s, done.
    Total 5 (delta 3), reused 0 (delta 0)
    remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
    To https://github.com/BradleyA/markit.git
       1331dac..ef33d26  master -> master
     * [new tag]         4.1.6 -> 4.1.6
    Counting objects: 5, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (5/5), done.
    Writing objects: 100% (5/5), 617 bytes | 0 bytes/s, done.
    Total 5 (delta 3), reused 0 (delta 0)
    To https://axebbq@bitbucket.org/axebbq/markit.git
       1331dac..ef33d26  master -> master
     * [new tag]         4.1.6 -> 4.1.6
    Counting objects: 5, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (5/5), done.
    Writing objects: 100% (5/5), 617 bytes | 0 bytes/s, done.
    Total 5 (delta 3), reused 0 (delta 0)
    To https://BradleyAxe@gitlab.com/BradleyAxe/markit.git
       1331dac..ef33d26  master -> master
     * [new tag]         4.1.6 -> 4.1.6

    Files marked and stored in remote Git repository.
    View commits example:  git log --graph --decorate --oneline --color --stat
    2020-09-10T16:46:14.812944-05:00 (CDT) five-rpi3b.cptx86.com markit[28951] 4.1.4.803 434 uadmin 10000:10000 [INFO]    Operation finished...

## Usage: check-markit
Check the release version of a file with the remote Git repository release version.  The **check-markit** script allows you to check if there is a newer release version of a file.  The following example uses the file 'markit', but can be used with any file that was marked with markit.

    check-markit markit 

## Output: check-markit
    $ check-markit markit
      % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                     Dload  Upload   Total   Spent    Left  Speed
      0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
    100 2386k    0 2386k    0     0   939k      0 --:--:--  0:00:02 --:--:-- 1412k

      /usr/local/bin/markit release 4.1.4.803, commit date 2020-08-29T22:25:50.210493-05:00

      markit repository release 4.1.4.803, commit date 2020-08-29T22:25:50.210493-05:00

    Repository copy placed in /tmp/markit
    2020-09-10T17:03:50.405525-05:00 (CDT) five-rpi3b.cptx86.com check-markit[747] 4.1.4.803 259 uadmin 10000:10000 [INFO]    Operation finished...

## Getting Started
**Fork https://github.com/BradleyA/markit** repository so you can modify the test files while learning how simple it is to work with markit.  

On your system, git clone the forked copy of markit from \<YOUR-REPOSITORY\>.  

    git clone https://github.com/<YOUR-REPOSITORY>/markit.git

Change into clone directory on your system.

    cd markit

Make a change to testfiles/sample.sh.

    vi testfiles/sample.sh
    
Run ./markit to tag, commit, and push the change in testfiles/sample.sh to your local and remote Git repositories.  Enter the next version number when prompted and a brief description of the changes to testfiles/sample.sh.  You will be prompted for your password when Git pushes testfiles/sample.sh to your remote Git repository.  **That is it!**

    ./markit

Check if your local version of testfiles/sample.sh is the same version that is on your remote Git repository.

    ./check-markit -f ./testfiles/sample.sh

On GitHub go to your Forked markit repository settings page and check the box next to Issues. Then open the first issue on your markit repository, #1.

Make a change to testfiles/sample.sh

    vi testfiles/sample.sh

Run ./markit.  Enter the next version number when prompted and this brief description '[testing markit issue changes close #1](https://help.github.com/articles/closing-issues-using-keywords/)'.  You will be prompted for your GitHub password when git pushes testfiles/sample.sh to your remote Git repository.

    ./markit
    
The file testfiles/sample.sh has been updated with metadata, git tag, git commit, git push, and the issue #1 on GitHub has been [closed](https://help.github.com/articles/closing-issues-using-keywords/).

View ./markit help pages to learn more about how markit works with tracked and untracked files and without network access to remote Git repository. 

    ./markit --help

Continue testing with the other test files to help you integrate markit with your development solutions.  Open a GitHub issue and then modify two test files.   When running markit enter a message and include the GitHub issue number and GitHub will update the issue.

## Install
To install the latest commit of markit, change to the directory you want to download the script to (cd /usr/local/bin) and enter the follow command.

    curl -L https://api.github.com/repos/BradleyA/markit/tarball | tar -xzf - --wildcards */markit ; mv BradleyA*/markit . ; rmdir BradleyA*/

To install the latest commit of check-markit, change markit to check-markit in the above command.

#### Author
[<img id="github" src="images/github.png" width="50" a="https://github.com/BradleyA/">](https://github.com/BradleyA/)    [<img src="images/linkedin.png" style="max-width:100%;" >](https://www.linkedin.com/in/bradleyhallen) [<img id="twitter" src="images/twitter.png" width="50" a="twitter.com/bradleyaustintx/">](https://twitter.com/bradleyaustintx/)       <a href="https://twitter.com/intent/follow?screen_name=bradleyaustintx"> <img src="https://img.shields.io/twitter/follow/bradleyaustintx.svg?label=Follow%20@bradleyaustintx" alt="Follow @bradleyaustintx" />    </a>   

#### System OS script tested
 * Ubuntu 14.04.6 LTS (amd64,armv7l)
 * Ubuntu 16.04.7 LTS (amd64,armv7l)
 * Ubuntu 18.04.5 LTS (amd64,armv7l)
 * Raspbian GNU/Linux 10 (buster)

#### Design Principles
 * Have a simple setup process and a minimal learning curve
 * Be usable as non-root
 * Be easy to install and configure
 
#### Contribute
Please do contribute! Issues and pull requests are welcome.  Thank you for your help improving software.

#### License
MIT License

Copyright (c) 2020  [Bradley Allen](https://www.linkedin.com/in/bradleyhallen)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
