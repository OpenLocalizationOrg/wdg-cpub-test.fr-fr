Team Workflow
-----------

This page describes the Open Publishing workflow in use by the WDG Partner & ITPro CPub team.

It is based on [GitHub Flow](http://scottchacon.com/2011/08/31/github-flow.html), as described by Scott Chacon.  The golden rule of the workflow is that anything in the master branch is deployable.

To make the changes on the GitHub site:

1. Open the file you want to change and click the pencil icon to enter edit mode.

2. Make your changes.

3. When you're done, scroll to the bottom of the page and choose Create a new branch.  Change the name of the new branch, if you like.  Then click Propose file change.

4. At this point, you can continue adding more changes to your new branch, or you can immediately submit a pull request.

To make the changes in a local clone, use the following steps:

* To work on something new, create a descriptively named branch off of master (ie: enterprise-wdk):

  ```
  git checkout -b <branch_name>
  ```

* Commit to that branch locally and regularly push your work to the same named branch on the server.

  ```
  git commit -am "<message>"
  git push -u origin <branch_name> ### for first push
  git push ### for subsequent pushes
  ```

* Iterate with others (tech review, edit) in your branch.

* When the branch is ready to publish, open a pull request.

* A peer or admin repo reviews the changes and merges the content into master.

* Once it is in master, a repo admin may deploy to the live branch at any time.
 


<!--HONumber=May16_HO4-->


