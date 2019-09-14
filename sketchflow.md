## Git Versioning Control For Sketch Files.
**Sketch 43** 🙌introduced a new open file format where `.sketch` documents are now stored as `.ZIP` archives containing `.JSON` data and what this allows us is to use git to keep track of changes made to the files. So basically we can now use git in a design workflow to version control `.sketch` files. 🤯

### Get Started
The `.sketch` file in itself isn't ready out of the box to be versioned in git, so there is a bit of a manual process in order to make it work. To do that we need to unzip its contents so they reveal the `.JSON` files which can be tracked in git.

### Workflow

So the idea for the git workflow is that you work as you normally do on the `.sketch` file, and when you're happy with the work you have done and are ready to commit its changes, you have to unzip the `.sketch` and add all its files to the commit of your local branch.

#### Preparing the .sketch file to commit it to git

The first thing you need to do is open the folder where the `.sketch` file is located on your computer in the command line.

```bash
# Let's say my file is Documents/SketchProject, lets change the directory to there.
$ cd ~Documents/SketchProject/
```
Now that we are in the right directory we have to unzip the file.

```bash
# Unzip the contents of the .sketch file into a folder named sketch.
$ unzip filename.sketch -d sketch
```

The `.sketch` file is now unzipped if we look in the directory we can see all the extracted `.JSON` files that can now be tracked within git. The only thing that is left is to commit the files to your local branch. For more on this check [Gitflow Design](https://github.com/diogorsergio/RTL-Design/blob/master/sketchflow.md).

**Keep in mind that every time you change the `.sketch` file you will have to unzip it so that changes can be tracked in git.**
