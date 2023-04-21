# STARTER-team01-docs

This is a prototype for a repo that can
* create a Storybook based on a React application in another public GitHub repo.
* publish that Storybook on GitHub pages.

## Use case

Normally, we might publish the storybook on the
gh-pages branch of the same repo that contains the
source code.  

However, in cases where we are using the gh-pages branch of the source repo to actually deploy the app itself, such as is the case for <https://github.com/ucsb-cs156-s23/STARTER-team01>, it becomes complicated to also use that branch for the storybook.

In those cases, you can use this starter code to 
create a companion repo where you can publish the storybook.

## Prerequisites

* The React app in the source repo should be entirely contained in the source repo in a directory called `frontend`.  This is a naming convention that is required by the standard way in which a Spring Boot backend and React frontend are combined in [CMPSC 156](https://ucsb-cs156.github.io) projects.

## Setup Instructions

* Create a new empty repo inside the same user or organization as the source repo, with the same name with the suffix `-docs`.  

  For example, if your source repo is `ucsb-cs156-s23/team01-s23-4pm-3`, you should create `ucsb-cs156-s23/team01-s23-4pm-3-docs`

  This naming convention is strict because it 
  allows for minimal configuration; the scripts
  in the starter code just strip `-docs` from the 
  name and look for source code in the resulting
  repo name.
* Clone the new empty blank repo, and cd into the
  resulting directory.  For example, type this (changing `ucsb-cs156-s23/team01-s23-4pm-3-docs` to the name of the repo you created in the previous step):
  ```
  git clone git@github.com:ucsb-cs156-s23/team01-s23-4pm-3-docs.git
  cd team01-s23-4pm-3-docs
  ```

* Add *this* repo as a remote called `starter`:
  ```
  git remote add starter git@github.com:ucsb-cs156-s23/STARTER-team01-docs.git
  ```
* Pull from the starter, and push to the blank repo:
  ```
  git checkout -b main
  git pull starter main
  git push origin main
  ```
* The push to main should trigger a GitHub Actions script to run.  If it doesn't, be sure that GitHub Actions are enabled on your repo.

  The first time the action runs, it may fail
  and produce a red X (❌).  *This is normal*; the
  script fails because it is trying to deploy a GitHub Pages website from `gh-pages` branch; but GitHub pages may not yet be enabled.  
  
  There
  is a chicken/egg problem here: you must have a gh-pages branch before you can set up GitHub Pages, and the first execution of the script creates that branch.
* Once you see that the script has run once, go to the Settings menu for your new repo, 
  and enable GitHub Pages, like this:

  INSERT SCREENSHOT HERE

* Then, trigger the GitHub Action to run again, 
  like this.  It should complete with a green check (✅).  At that point you should be able 
  to see your webpage.  You can enable a link to 
  it at the GitHub website for your URL like this:

  INSERT SCREENSHOT HERE

* From this point forward, any time you want to 
  refresh the website from the source repo, you 
  can trigger the Github Action manually,
  as shown below.

  INSERT SCREENSHOT HERE

### Triggering rebuilds automatically

This repo uses a "pull" model rather than a "push" model to update the content.  That is, the GitHub actions script is located in the same repo
as the GitHub Pages site, and we pull the content
from another repo.

If we want to trigger rebuilds automatically, for example on pushes to main in the source repo, we would need to use a "push" model instead, where the GitHub Actions script lives in the source repo, and pushes changes to the repo where the Github Pages live.  That is possible, but requires the use of various kinds of tokens or ssh keys to authorize one repo's GitHub Actions script to push content to another repo.  This is harder to set up, and may create security vulnerabillities if not done very carefully.

### What about private repos?

This pull model is setup to work easily when the source repo is public.  If the source repo is private, the GitHub actions script would need to be modified to work with token or ssh key based authentication, which is a bit more complicated, and may create security vulnerabillities if not done very carefully.