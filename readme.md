<p align='center'><img src="images/rtl-logo.png" width="236"></p>

## What is RTL?
RTL (Ride The Lightning) is a full function, device agnostic, web user interface to help manage lightning node operations.RTL is available on LND and C-Lightning implementations.

Visit the development repository [ShahanaFarooqui/RTL](https://github.com/ShahanaFarooqui/RTL) for more information.  
Follow [@RTL_App](https://twitter.com/rtl_app) on Twitter for important announcements.

## RTL-Design
This is the GitHub repository for the design work stream of RTL. It exists as a way to  mitigate an issue commonly found in FOSS projects, where the design work happens on an ad hoc basis by contributors, most of the times using proprietary software and files which are not accessible to all, and that are not stored in a common place, so as contributors come and go from the project these can get lost.

By using git we make sure that all the work and decisions are tracked over time, that the files are stored and available to everyone in a common place and with the added bonus that the design and dev repositories can now be tied together streamlining the work process and increasing collaboration between developers and designers and if that is not enough, by doing all of this in git, now the design work will also  be control versioned by default ( 🤯) albeit with some caveats that will be explained bellow.

For all this to function as intended, there's a workflow in place that needs to be followed by contributors. Its based on the popular [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/) (Gitflow) by [Vincent Driessen](https://nvie.com/about/), but adapted to a design process.

## Gitflow ❤️ Design
Gitflow design as mentioned above is a git workflow for designers and design work. Its meant to be open, platform agnostic and help minimise dependencies on proprietary design software and increase collaboration.

With git at the heart of everything, we get to take advantage of a lot state of the art features in project management/development, such as controlled access, review process, feedback systems,  version control, preview changes in context, side-by-side Diffs, detailed history of changes and more. Something that developers had available for years, but that designers never took advantage off.

#### Workflow

<p align="left"><img src="images/gitflowdesigndiagram.png" width="90%"></p>

##### Main Branches
* master
* design

The **master** branch is where you can find all the signed off work ready for implementation. This means the work you encounter there has been discussed, reviewed and accepted for development.

The **design** branch is where the **feature** branches come together in order to be reviewed before being accepted and ready to be merged to **master**.

##### Supporting Branches

* ux/feature
* ui/feature

Feature branches have two separate work streams one for UX and one UI and are named accordingly. Ideally they follow a certain order in the workflow.

As an example we might have an upcoming feature named **helpsystem**, with this, a UX feature branch should be created and named **ux/helpsystem** and this where the user experience work will be done. When the UX is finalised and ready for review, the branch will be pushed and a pull request created to merge it to **design**, this is where the review process takes place. If no problem arises, the **ux/helpsystem** pull request is accepted and the branch merged into design.

At this point the feature is ready to progress  into UI design. If it's picked up a new feature branch shall be created and named **ui/helpsystem** and the UI work can start. When the UI work is finalised the UI branch will follow the same steps as the UX counterpart and should be pushed and a pull request created to start the review process and merge it to **design**.

At this point if everything went to plan and the work reviewed and accepted we have both the **ux/helpsystem** and **ui/helpsystem** branches merged in **design**, so now the last step before being ready for development, is to create pull request in order to merge **design** into the **master** branch.

Well this is gist of it, and there is a lot more to it, but this is the foundation, we will explain further concepts further down.

## Contributing
👍🎉 First off, thanks for taking the time to contribute! 🎉👍
