## What is RTL?
RTL (Ride The Lightning) is a full function, device agnostic, web user interface to help manage lightning node operations. RTL is available on LND, C-Lightning and Eclair implementations.

Visit the development repository [ShahanaFarooqui/RTL](https://github.com/ShahanaFarooqui/RTL) for more information.
Follow [@RTL_App](https://twitter.com/rtl_app) on Twitter for important announcements.

## Table of contents
* [RTL-Design](#rtl-design)
* [Gitflow ❤️ Design](#gitflow-%EF%B8%8F-design)
  * [Workflow](#workflow)
  * [Main Branches](#main-branches)
  * [Supporting Branches](#supporting-branches)
  * [Future Work](#future-work)
* [Contributing](#contributing)
  * [Software Recommendations](#software-recommendations)
  * [Prerequisites](#prerequisites)
  * [Folder Structure](#folder-structure)
  * [Version Control](#version-control)
    * [Sketch](#sketch)
  * [Proprietary Files](#proprietary-files)
  * [Getting Started](#getting-started)
    * [Github Desktop Application](#github-desktop-application---step-by-step-guide)
    * [Terminal](#terminal---step-by-step-guide)
* [Contact](#contact)
* [Acknowledgements](#acknowledgements)
* [License](#license)

## RTL-Design
This is the Github repository for the design work stream of RTL. It exists as a way to mitigate issues commonly found in design workflows of open-source software projects where the work created never comes into git. Which means such work is not being tracked and doesn't have an auditable history. Files also might not be stored in a common place accessible to everyone, so its always a hit and miss on how to gain access to them, and sometimes due to these being created with proprietary software they can sit behind a closed gateway and as contributors come and go from the project their access can be lost.

By using git we make things easier and open for anyone wanting to collaborate and hopefully streamlining the work process by connecting the development and design repositories together. For this to work a success we need to adopt a design workflow that focus on open-source ideals, so that no one is restricted by proprietary software and gatekeepers. We introduce such workflow bellow which we have been testing, It's called **Gitflow Design** and It's based on the popular [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/) (Gitflow) by [Vincent Driessen](https://nvie.com/about/), but adapted to a design workflow.

## Gitflow ❤️ Design
Gitflow design as mentioned above is a git workflow for designers and design work. It's meant to be open, platform agnostic and help minimise dependencies on proprietary software and help to increase collaboration.

By using git, we get to take advantage of a lot of useful features available such as controlled access, review process, feedback system, version control files, preview changes in context with side-by-side *diffs*, detailed history of changes and more, something developers had for years, but that designers never really took advantage of.

### Workflow

<p align="left"><img src="images/gitflowdesigndiagram.png" width="90%"></p>

### Main Branches

**master** / **design**

Instead of a single master branch, this workflow uses two main branches to record the history. The **master** branch stores all the signed off releases from the design branch, and the **design** branch servers as an integration branch for all the features. It's in the design branch where supporting branches are fully reviewed before being merged onto it.


### Supporting Branches

**ux/feature** / **ui/feature**

New features being designed should have their own branches. There are two types of feature branches, one for the user experience work with the prefix **ux/** and the second for interface design work with the prefix **ui/**, and if all went to plan one follows the other.

As an example we might have an upcoming feature named **helpsystem**, for this to start, a ux feature branch should be created and named **ux/helpsystem**. This is where the user experience work will be done. When the ux is finalised and ready for review, the designer will create a pull-request to start the final review process to merge it to the design branch. If the reviewers are happy with the work that was done and it has been signed off, the pull request is accepted and the branch merged onto design and then deleted.

At this point the **ux/helpsystem** is ready to progress into ui design. It starts with a new feature branch created and named **ui/helpsystem**. It now follows the same steps as before and when the ui work is finalised, the branch should be pushed and a pull-request created to initiate the review process so it can be signed off and merged onto the design.


Following that we now have both the **ux/helpsystem** and **ui/helpsystem** branches merged in design, so now, the next step is for a reviewer to merge design onto the master so the feature is pushed.

You can read the step by step guide on how to follow this workflow further down the page.

## Future Work

Couple of ideas for future improvements with the goal of having everything within github and publicly accessible.

* Look into Github LFS (Large File Storage) for big binary files.
* How can shared/master components work within this workflow?
* Github Pages to host:
  * Design System
  * Exports Gallery/Showcase
  * Handoff specs for developers? (Zeplin/Sketch Measure)

If you have any ideas on how to solve any of these, please get in touch! 👍

## Contributing
🎉First things first, thanks for showing interest in contributing to RTL 🎉

This workflow is still a work in progress and we are still changing it, so if you have any suggestions on how to improve it, please get in touch!

### Software Recommendations
We want to keep the workflow open to anyone who wants to contribute, so it tries to focus on using open file formats that can be easily accessible to others and are not dependant on proprietary software.

**Free open source software you can use:**

* Inkscape (Vector graphics editor) - https://inkscape.org/
* GIMP (Image editor) - https://www.gimp.org/

### Prerequisites

The workflow can be followed with the Github Desktop App, but also via the terminal. There's a guide for both, so follow the one you're most comfortable with.

* [Github Desktop App](https://desktop.github.com) - Recommended
* [Git for Command Line](https://git-scm.com/) - Only if you are familiar with git and terminal, it can become quite complex.

### Folder structure

This is an example of the folder structure being used to keep things organised and manageable for all of us.

    .
    ├── documentation                  # Supporting documents
    │   └── research                   # Research material
    ├── images                         # Assorted images
    └── lnd                            # Lightning implementations
        └── dashboard                  # Feature files
            ├── ux                     # User experience work
            │    ├── exports           # Exported artboards
            │    └── source            # Source files
            │        ├── sketch        # Editable file being used
            │        └── svg           # Open format alternative
            └── ui                     # User interface work
                ├── exports            # Exported assets
                └── source             # Source files
                    ├── psd            # Editable file being used
                    └── xcf            # Open format alternative





When using proprietary software, please make sure you always keep copies of the editable file in open file formats.
For example if you use Sketch, keep the .sketch file in the source, but also export all your artboards into separate **.svg** files.

### Version Control

More and more companies are opening their file formats and as they do this sometimes we can take advantage of that and version control their files. When this is the case, we will include a guide on how to do it.

#### Sketch
Sketch 43, Introduced a new open file format where .sketch documents are now stored as .ZIP archives containing .JSON files and what that allows us is to use git to keep track of changes made to the files. The .sketch file in itself isn't ready out of the box to be versioned in git, so there is a bit of a manual process in order to make it work. but you can read more about it here [sketchflow.md](/sketchflow.md).

### Getting started
This step by step guide will walk you through the basics of **Gitflow Design**.

It will cover, cloning the RTL-Design repo, creating a new feature branch, pushing your changes to github and creating a pull request to get your work reviewed. All this is shown  through both the desktop application and via terminal.

### Github Desktop application - Step by Step Guide
If you're not familiar with the terminal or command line applications, the Github Desktop application is the perfect solution. It works perfectly out of the box and makes interacting with git a lot easier.

#### Step 1 - First Launch

Launch the Github Desktop app and click to `Clone a repository from the Internet`
<p><img src="images/guide/Flow01.png" width="70%"></p><br>

#### Step 2 - Clone the Repo

Enter the RTL-Design repository URL or username/repo:  `diogorsergio/RTL-Design`
<p><img src="images/guide/Flow02.png" width="70%"></p><br>

#### Step 3 - Design Branch

Switch from the **master** branch to **design**.
<p><img src="images/guide/Flow03.png" width="70%"></p><br>

#### Step 4 - Feature Branches

Create a new feature branch based on the **design** branch. There are two types of prefix for feature branches **ux/** and **ui/** and these are based on the type of work to be done. Prefixes should be followed by the feature name e.g.: **ux/lightning**.
<p><img src="images/guide/Flow04.png" width="70%"></p><br>

#### Step 5 - Do the work

At this point you are ready to start working, but please make sure you follow the correct folder structure when creating your files.
<p><img src="images/guide/Flow05.png" width="70%"></p><br>

#### Step 6 - Commit the Changes

When you finish a design iteration and are ready to show it to gather feedback, you will have to **commit** the changes you just made so they can be pushed to github for everyone to see. Commit titles should start with **[UX]** or **[UI]** accordingly to the work they include and a couple words describing the scope of the work. The **description** field is optional.
 <p><img src="images/guide/Flow06.png" width="70%"></p><br>

#### Step 7 - Push Changes to Github

 Once your changes are committed, they are still local and not available in github, to make them available for everyone you will have to **publish** this branch.
 <p><img src="images/guide/Flow07.png" width="70%"></p><br>

#### Step 8 - Do more work

If your work still isn't finished, you can continue to work on your local files and do more changes, and these will be added for the next commit. At this point you can also take advantage of the Diff visualiser and check the differences between the current commit and the branch, and if everything seems okay, you can **commit** the changes and **push** them afterwards as you've done before.
<p><img src="images/guide/Flow08.png" width="70%"></p><br>

#### Step 9 - Push and Pull Request

The changes are now pushed and available for everyone to see in github, so the last step is to get them reviewed by the design team. In order to do this, you will have to create a **pull request**
<p><img src="images/guide/Flow09.png" width="70%"></p><br>

#### Step 10 - Pull Request

This will open github on your browser and show the **pull request** interface. Select **design** as the base, the title should have the prefix of the work done **[UX], [UI]** or **[UX/UI]** and write a description about the work included. Anything that will help reviewers.
<p><img src="images/guide/Flow10.png" width="70%"></p><br>

### Terminal - Step by Step Guide

If you're quite comfortable with command line applications and prefer to interact with git that way, then this will give you an overview on how to do it.

#### Step 1 - Clone the repo

```bash
# Open the directory to where you want to download the repository.
$ cd ~Documents

# Clone the repository.
$ git clone https://github.com/diogorsergio/RTL-Design.git

# Go into its directory.
$ cd RTL-Design
```
#### Step 2 - Switch to Design Branch

```bash
# You're now in the master branch, so let's switch to the design branch.
$ git checkout design
```

#### Step 3 - Create Feature Branch

```bash
# Always create feature branches based on design. Use prefixes accordingly ux/ or ui/.
# Name should follow prefix/featurename.
$ git checkout -b ux/lightning design
```
#### Step 4 - Do The Work

```bash
# At this point you are ready to start working.
# Make sure you follow the correct folder structure when creating your files.

# Check the status of the current branch, after working on it.
$ git status
```
#### Step 5 - Add and Commit Changes

When you finish a design iteration and are ready to show it to gather feedback, you will have to **commit** the changes you just made so they can be pushed to github for everyone to see. Commit titles should start with **[UX]** or **[UI]** accordingly to the work they include and a couple words describing the scope of the work.
```bash
# First you need to add the changes, you have just made.
# -A stands for --All.
$ git add -A

# Now that the files are added, you can commit them.
# The title should include the prefix followed by the scope of the work.
$ git commit -m '[UX] - Lightning Transactions'
```
#### Step 6 - Push Changes to Github

Once your changes are committed, they are still local and not available in github, to make them available for everyone you will have to push to publish this branch.
```bash
# You have to push them up-stream (-u) to origin
$ git push -u origin ux/lightning
```

#### Step 7 - Pull Request

The changes are now pushed and available for everyone to see in github, so the last step is to get them reviewed by the design team. In order to do this, you will have to create a **pull request**.
```bash
# When you pushed the commit the output should have been something similar to this.

remote: Create a pull request for 'ux/lightning' on GitHub by visiting:
remote: https://github.com/diogorsergio/RTL-Design/pull/new/ux/lightning

# You can just open the URL and it will open the Github with the Pull Request interface on it.

```

## Contact
* Twitter: [@diogorsergio](https://twitter.com/diogorsergio)
* IRC: #rtl-dev on [freenode.net](https://freenode.net)

## Acknowledgements
* A successful Git branching model by [Vincent Driessen](https://nvie.com/posts/a-successful-git-branching-model/)
* Designers Git-It; A unified design system workflow by  [Stephen Hathaway](https://www.youtube.com/watch?v=A-lNv6Szu3M)

## License

Distributed under the MIT License. See [LICENSE](/LICENSE.md) for more information.
