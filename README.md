# drone-mkdocs
Basic example for a configuration to setup Drone.io CI to automatically publish mkdocs on a github page.

## github pages and drone
*Github pages* are static html pages that life in a github repository and are published automatically under the domain github.io. *`mkdocs`* is a tool that takes a documentation written in multiple markdown files and creates a static html page from it to be presented on a http server. This two concepts work so well with each other, that `mkdocs` even has a command to directly publish to a github page.

## publish automatically
Github pages with mkdocs are already easy &ndash; your markdown sources live in your master branch (or any branch, really). Mkdocs does all the work for you from building the html, over commiting to a special branch, up to pushing that branch upstream. But you still need a computer with a working `mkdocs` installation handy to fix even a typo. It would be nice to just click `edit` in your repo on github fix the markdown, commit, and get the new version published. 

Of course this can be acheived with a CI system like drone.io. There are few things to consider, if you want your drone server to be able to publish to your github repo.

## usage
This repo consists of not much more than a simple `.drone.yml` that you can copy to your mkdocs repo. Activate that repo in your drone server and it should be triggered on each commit. You will also need to create a ssh key pair. Follow the instructions for 
[github repo deploy keys](https://developer.github.com/v3/guides/managing-deploy-keys/#deploy-keys). The public key needs to be set as deploy key as set in the linked instructions (be sure to anable push privileges). You can also put the public key into your repo into the `deploykey.pub` file. DO NOT ADD THE SECRET KEY TO YOUR REPOSITORY. Anyone who optains that key will be able to write to your repo! Put in a save play (some password manager or such). You need to add it in your drone server as a secret for the repository under the name `DEPLOY_SECRET_KEY` (just add the whole key, multiline as it is).
