Best tools for Git + markdown neophytes
=======================================

Git can be confusing for those used to single checkin/checkout mechanisms. Many Git tools are also command-line based which are powerful but can be complicated.

Here is my recommendation for **someone brand new to Git** who wants to get started right away:

1. Download and install **[VSCode](https://code.visualstudio.com/)**. This is your markdown editor.
2. Download and install **[GitHub desktop](https://desktop.github.com/)**. This is your graphical interface for your GitHub interactions. See the [help docs](https://help.github.com/desktop/) for information on using the client.

The following recommendation is for someone who **wants a GUI with more functionality** and doesn't mind spending some additional configuration time.

1. Download and install **[Atom](http://atom.io)**. This is your customizable and extensible markdown editor.
2. Download and install **[SourceTree](https://www.atlassian.com/software/sourcetree/overview)**. This is your graphical interface for Git interactions.
3. Connect your SourceTree instance to a GitHub repo by clicking **Clone/New** and then using the URL to the main GitHub repo (where you see the `.gitignore` file).
4. Provide a personal access token from GitHub as the password as described in [this SourceTree article](https://confluence.atlassian.com/display/SOURCETREEKB/Two-Factor+Authentication+%282FA%29+with+GitHub+in+SourceTree). To generate the token, go to **Settings** in GitHub (click your profile to see the menu), then click **Personal access tokens** and generate one for use as your password.

> Some have been unable to get authentication to work this way; if you encounter issues and are able to resolve them, please update this topic with your findings.

Want to just **get started without installing anything**? You can do that! Check out the topic on [using the GitHub UI to edit content](..\domars\Directions_To_Update_Existing_Topic_Using_Browser.md). Many minor and even major changes can be made directly through your web browser.

> The [Markdown Writer](https://atom.io/packages/markdown-writer) package for Atom provides configurable keyboard shortcuts for most markdown formatting.

This is not an all-in-one solution (i.e., it's not a CMS). You'll use an editor for content updates and preview but most use Windows Explorer to manipulate the files or add new things. (Some functionality for this exists within Atom as well if you're just browsing between files.) You'll then use your Git management tools (command line or GUI) to commit the changes and push to the GitHub remote master.

> If you do local builds or end up with other files in your local source that you don't want to push to GitHub, select these files before they're staged, right-click and **Discard** them.

As described on the [Welcome page](../Welcome.md), there are many different mix-and-match options with Git and markdown, but the above should get you up and running quickly. If you have more to add, just make a change and submit a pull request.


<!--HONumber=Mar16_HO2-->


