# This is Iaan's test md page using VS2015.

So what did I do? Here's some answers yo:

1. So you can check-in/check-out and manage files in the GitHub repos:
    1. Install VS2015 and choose the 'custom' option. On the next screen, at the bottom, you need to select the two Git-related options.
2. So you can see a preview of your .md files in VS2015: 
    1. Install [VS Web Essentials](http://vswebessentials.com/download "Link to download the latest Web Essentials version - you can also search for it in the extensions manager in VS").


To understand more about how to use GitHub and VS2015, check these out:

- [WDG-CPUB test instructions](https://msdnstage.redmond.corp.microsoft.com/wdg-cpub-test/HelloWorld)
- [The WDG repo on github.com](https://github.com/Microsoft/wdg-cpub-test/tree/master/wdg-cpub-test)
- [Preview (and live) version of the WDG repo on MSDN](https://msdnstage.redmond.corp.microsoft.com/wdg-cpub-test/HelloWorld)
- [Channel 9 guide to connecting GitHub repos to VS2015](https://channel9.msdn.com/Series/ConnectOn-Demand/217 )
- [Tutorial on creating a GitHub project](https://guides.github.com/activities/hello-world/ )

## Here's what we're going to do in our little excursion

### 1.1 Make changes and review them all on github.com

1. Go to the wdg-cpub-test repo on github.com and navigate to the readme.md file
2. Make an update on the site to include this URL for msdnstage:
    1. https://msdnstage.redmond.corp.microsoft.com/wdg-cpub-test/HelloWorld
3. Request a pull change

### 1.2a Use VS2015 to pull files from a repo

1. Click the **Manage Connections** icon at the top of the **Team Explorer** window. You should see a GitHub section  (if this doesn't appear, you may need to sign in first). 
2. Click **Clone** and search for a project (eg *wdg-cpub*) from the list. Make sure it's going in your dedicated GitHub syncs folder. Click **Clone**.

This will pull all the files in the repo onto your local machine. Use File Explorer to go to the location of the repo and you can see the files. 

You can copy the files to somewhere else on your machine to open them and play around with them without fear that you will make changes on the server.

### 1.2b Use VS2015 to push files to a repo

To make changes appear on the server, open up the file from within your local folder and make the changes. Save the file and go back to VS2015.

Generally, you should make branches when you are making changes. See [Team Workflow for more information](https://msdnstage.redmond.corp.microsoft.com/en-us/wdg-cpub-test/tedhudek/workflow).

1. Click the **Manage Connections** icon at the top of the **Team Explorer** window. You should see a GitHub section  (if this doesn't appear, you may need to sign in first). 
2. Double-click the repo you want to update in the list of **Local Git Respositories**. This will open the repo and take you to **Team Explorer**.
3. Click **Branches**. right click on *master* and click *New local branch from...*.
4. Enter a name for the new branch (describing what you did or the date maybe). Click **Create Branch**.
5. Go to **Changes**. You'll see the files you updated, and the new branch should be selected by default. If not, click on the branch name, which will take you to **Branches**. Double-click the new branch, then go back to **Changes**. Enter a description and click **Commit**.
4. Go to **Sync**. You'll see the an open publish request. Click **Publish**. 

Your local changes are now on the github.com server. You can go there to see them.

### 1.3 Use VS2015 to do it all (connect to a github repo, make changes, sync with github.com)

1. Click the **Manage Connections** icon at the top of the **Team Explorer** window. You should see a GitHub section  (if this doesn't appear, you may need to sign in first). 
2. You have two options, which depend on whether you've created a repo on github.com already and want to use it, or if you want to create a new repo right now:
    1. Under GitHub, click **Create**. Enter the name, a description, the local sync path you want to use (it's a good idea to keep all your syncs in one folder, on a non-OS partition). Click **Create**. In this example we'll use *Testing* for the name, and *F:\Gits* for the path.
    2. If you have an existing repo, click **Clone* and select it from the list. Click **Clone**.
3. Your repo will appear in the list of **Local Git Respositories**. Double-click it to open the repo in **Team Explorer**.
4. Under **Solutions** click **New...**.
5. Under **Templates\Other Project Types\Visual Studio Solutions** select <b>Blank Solution</b>, give it the same name as the repo you just created: *Testing*.
6. Change the **Location** to be the parent folder of the repo you just created: *F:\Gits*. 
7. Select **Add to source control** and click <b>OK</b>.
8. Go to Changes, enter a description and click Commit.
9. Go to Sync. You'll see an open push request. Click **Push**. 

You've now created a repo on github.com, and synced it with your local copy. It only contains a readme.md, but if you go to github.com, you'll see the repo has been created.

Now you can start working on files. 

Go to the **Solution Explorer** in VS2015. Here you'll see the files you have. Right-click to add a new file, choose a text document, and call it whatever you want. Make sure it has .md as the extension (this ensures it is a MarkDown document).
You can now edit it in VS2015. 
To push your changes, go to **Team Explorer**, then follow Steps 8 and 9 in Section 1.3 above.

<!--HONumber=Mar16_HO2-->


