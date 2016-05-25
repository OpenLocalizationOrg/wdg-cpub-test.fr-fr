# Welcome to WDG CPub Open Publishing Playground
We are happy to announce the arrival of the WDG CPub Playground.

![Git logo](../images/github-logo.png) + ![Markdown logo](../images/markdown-logo.png)

Here you can experiment with markdown and GitHub to your heart's content, and then see how your markdown renders in MSDN's Open Publishing environment.

> If you are already familiar with GitHub, are part of the Microsoft organization, and want to dive right in, skip down to the "Set up your personal playground" section.

If you see anything in this topic that is no longer correct or that just bothers you in some way you can't really explain, please fix it by submitting a pull request with the changes.

## Sign up for GitHub and the Microsoft organization
There are two main steps in getting set up for Open Publishing on GitHub: creating a GitHub account and then connecting it to the Microsoft organization.
If you already have a GitHub account you want to use, you can skip the first step.

1. **Sign up for GitHub** -- Go to [https://github.com/](https://github.com/) and sign up as a new user. You can use any email account you want to sign up, and your username doesn't have to match your Microsoft alias.
2. **Connect your GitHub account to your alias and the Microsoft organization** -- For this step, follow the instructions found at  [https://opensourcehub.microsoft.com/articles/how-to-join-microsoft-github-org-self-service](https://opensourcehub.microsoft.com/articles/how-to-join-microsoft-github-org-self-service).

**Note**: Open Source Hub ([https://opensourcehub.microsoft.com](https://opensourcehub.microsoft.com)) is where you manage your connected GitHub profile; you can also create and manage repos and teams.

## Set up your own personal playground
To use the WDG CPub sandbox, all you need to do is:

1. Create folder `<your-alias>` as a child of `wdg-cpub-test`.
2. Start marking down!
3. As needed, add any topics you'd like to the `TOC.md` file to incorporate into the TOC. The TOC uses markdown heading syntax (#, ##, etc.) to designate levels.

## Learn more...
This section provides resources for learning more about using Open Publishing, Git, and markdown.

### ...about Open Publishing
MSDN Open Publishing (aka OP or OPS) has its own set of documentation at [https://int.msdn.microsoft.com/en-us/openpublishing/docs/introduction](https://int.msdn.microsoft.com/en-us/openpublishing/docs/introduction).

Be sure to check out the documentation on performing [local builds](https://int.msdn.microsoft.com/en-us/openpublishing/docs/partnerdocs/local-build-and-preview) to see how you can preview your content locally and publish to stage simply by pushing to the master.

### ...about Git
There are many resources on using Git out there. Great tutorials are available on using GitHub on GitHub itself (see the home page). Here are some additional resources some have found helpful:

* Pro Git online book -- [http://git-scm.com/book/en/v2](http://git-scm.com/book/en/v2)
* Online Git tutorial -- [http://www.sbf5.com/~cduan/technical/git/](http://www.sbf5.com/~cduan/technical/git/)
* Git guided tour -- [http://githowto.com/](http://githowto.com/)
* Blog post on Git best practices -- [http://sethrobertson.github.io/GitBestPractices/](http://sethrobertson.github.io/GitBestPractices/)
* Tutorial on Git branching -- [http://pcottle.github.io/learnGitBranching/](http://pcottle.github.io/learnGitBranching/)

### ...about markdown
Markdown syntax guides are rampant on the Internet, so feel free to search for one you like, but a good introductory one that also talks about the format's goals and the thinking behind it, is [Daring Fireball](http://daringfireball.net/projects/markdown/).

## Choosing the right tools
WDG CPub currently doesn't provide any specific recommendation around which tools you should use for doing markdown authoring and interacting with the repo. What follows are some options that some have recommended over the past year of various pilot projects. If you come across a tool that you think works better, please add it here and tell us why it works so well.

### Markdown editing
* **[VS Code](https://code.visualstudio.com/)** -- the new lightweight IDE from Visual Studio has markdown text support (and Git as well). Many Microsoft markdown authors have become fans of this.
* **[MarkdownPad Pro](http://www.markdownpad.com/)** -- A very good full-featured editor; real-time preview is excellent. A $15 license needed to use the Pro version which is required to use GitHub-flavored markdown (GFM).
* **[Atom](http://atom.io)** -- An extensible text editor that comes with packages that provide markdown preview as well as GitHub integration. Additional packages and updates are constantly being developed.
* **Notepad** -- For the lover of simplicity.
* **Visual Studio** -- The Markdown Mode plugin provides real-time preview, although as of press time it hasn't been confirmed that it works with VS 2016. The Web Essentialls plugin/extension provides a preview and syntax highlighting for .md files in VS2015.

### Git management
* **[GitHub](https://github.com)** -- You can go quite a ways just using the basic GitHub web UI; you can modify content and push directly or create pull requests.
* **[GitHub Desktop](https://git-for-windows.github.io/)** -- Allows you to manage different repos and handle merge conflicts.
* **[Tortoise Git](https://tortoisegit.org/)** -- Once installed, you interact with Git by using contextual menu commands in your local repository.
* **[SourceTree](https://www.atlassian.com/software/sourcetree/overview)** -- Git management through a GUI; more straightforward than GitHub Desktop, this is recommended for those who prefer not to use a command-line interface. (**Note:** Because you've enabled two-factor authentication, you'll need to use a personal access token as your password to clone your repo with SourceTree; see instructions [here](https://confluence.atlassian.com/display/SOURCETREEKB/Two-Factor+Authentication+%282FA%29+with+GitHub+in+SourceTree).)
* **[PoshGit](https://github.com/dahlbyk/posh-git)** -- Integrates Git commands with PowerShell. PowerShell lovers, this is the one for you.
* **[Git-Scm](http://www.git-scm.com/downloads)** -- Git on the command line. Get yourself some markdown in Emacs (which does [exist](http://jblevins.org/projects/markdown-mode/)), and you're kicking it old school.
* **Visual Studio/[VS Code](https://code.visualstudio.com/)** -- These integrate well with GitHub repos as well as VSO. VS2015 also has GitHub repo integration straight out of the box.

## Tips and Tricks
This section is intended for random links to items of interest:

* Command line phobic? Check out [Recommended tools for beginners](../jasgro/tools-for-beginners.md) for a recommendation on how to get started.
* See Ted Hudek's tips for [converting WDCML to markdown](../tedhudek/wdcml-to-open-publish.md) and his crowd-pleasing [markdown tips](../tedhudek/markdown-tips.md).
* Don Marshall has put together instructions for [editing content through the GitHub UI](../domars/Directions_To_Update_Existing_Topic_Using_Browser.md) which can be a very painless way to make quick updates.


<!--HONumber=May16_HO4-->


