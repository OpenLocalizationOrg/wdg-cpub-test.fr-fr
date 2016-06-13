# Welcome to the WDG CPub Open Publishing Playground
We are happy to announce the official grand opening of the WDG CPub Open Publishing Playground (or WDGCPOPP, pronounced "wedge-kuh-pop").

![Git logo](images/github-logo.png) **+**&nbsp;&nbsp;![Markdown logo](images/markdown-logo.png)

Here you can experiment with markdown and GitHub to your heart's content and then see how your markdown renders in MSDN's Open Publishing environment.

> **Note** If you are already familiar with GitHub *and* are part of the Microsoft organization, skip to the ["Set up your own personal playground"](Welcome.md#set-up-your-own-personal-playground) section.

## Sign up for GitHub and the Microsoft organization
There are two steps getting set up for Open Publishing on GitHub:

1. **Sign up for GitHub** -- Go to [https://github.com/](https://github.com/) and sign up as a new user. You can use any email account you want to sign up, and your username doesn't have to match your Microsoft alias.
2. **Connect your GitHub account to your alias and the Microsoft organization** -- For this step, follow the instructions at [How to Join the Microsoft Organization](https://opensourcehub.microsoft.com/articles/how-to-join-microsoft-github-org-self-service).

[Open Source Hub](https://opensourcehub.microsoft.com) is where you manage your connected GitHub profile; you can also create and manage repos and teams.

## Set up your own personal playground
If you are not familiar with Git and markdown, read the [Learn More](Welcome.md#learn-more) section below.

When you are ready to jump in:

1. Create a folder `<your-alias>` as a child of `wdg-cpub-test`.
2. Start writing!
3. To incorporate content into the table of contents, add the topics to the `TOC.md` file, using markdown heading syntax (#, ##, etc.) to designate hierarchy.

> **Important** Any broken link in the repo, including image references, will break the build. Before pushing to the remote, please check your links and follow the [local build instructions](https://ppe.msdn.microsoft.com/en-us/openpublishing/docs/partnerdocs/local-build-and-preview) to ensure you're not blocking updates to the rendered site. If you're not sure what "pushing to the remote" means, see ["learn more about Git"](Welcome.md#about-git).

## Learn more
This section provides resources for learning more about [Open Publishing](Welcome.md#about-open-publishing), [Git](Welcome.md#about-git), and [markdown](Welcome.md#about-markdown).

### ...about Open Publishing
MSDN Open Publishing (aka OP) has its own set of [documentation](https://ppe.msdn.microsoft.com/en-us/openpublishing/docs/introduction) which contains information on performing local builds, HTML whitelists, and other Open Publishing-specific information.

### ...about Git
There are many resources on using Git available online. Great tutorials are available on using GitHub (see the [GitHub home page](https://github.com)). Here are some additional resources some have found helpful:

* [Pro Git online book](http://git-scm.com/book/en/v2) -- Exhaustive and authoritative reference on all things Git
* [Online Git tutorial](http://www.sbf5.com/~cduan/technical/git/) -- An introduction to Git basics
* [Interactive tutorial on Git branching](http://pcottle.github.io/learnGitBranching/) -- Work through a series of lessons on Git fundamentals

### ...about markdown
Markdown syntax guides are rampant on the Internet, so feel free to search for one you like, but a good introductory one that also talks about the format's goals and the thinking behind it, is [Daring Fireball](http://daringfireball.net/projects/markdown/).

## Choosing the right tools
WDG CPub doesn't provide specific tools recommendations. What follows are some options that have been used during various pilot projects. As you experiment with different tools, please update these lists with your findings.

### ...for markdown authoring
* **[VS Code](https://code.visualstudio.com/)** -- the new lightweight IDE from Visual Studio has markdown text support (and Git as well). Many Microsoft markdown authors have become fans of this.
* **[MarkdownPad Pro](http://www.markdownpad.com/)** -- A very good full-featured editor; real-time preview is excellent. A $15 license needed to use the Pro version which is required to use GitHub-flavored markdown (GFM).
* **[Atom](http://atom.io)** -- An extensible text editor that comes with packages that provide markdown preview as well as GitHub integration. Additional packages and updates are constantly being developed.
* **Notepad** -- For the lover of simplicity.
* **Visual Studio** -- The Markdown Mode plugin provides real-time preview, although as of press time it hasn't been confirmed that it works with VS 2016. The Web Essentials plugin/extension provides a preview and syntax highlighting for .md files in VS2015.

### ...for Git management
* **[GitHub UI](https://github.com)** -- You can go quite a ways just using the basic GitHub web UI; you can modify content and push directly or create pull requests.
* **[GitHub Desktop](https://git-for-windows.github.io/)** -- Allows you to manage different repos offline and handle merge conflicts.
* **[Tortoise Git](https://tortoisegit.org/)** -- Once installed, you interact with Git by using contextual menu commands in your local repository.
* **[SourceTree](https://www.atlassian.com/software/sourcetree/overview)** -- A more feature-rich GUI than GitHub Desktop. (**Note:** Because you've enabled two-factor authentication, you'll need to use a personal access token as your password to clone your repo with SourceTree; see instructions [here](https://confluence.atlassian.com/display/SOURCETREEKB/Two-Factor+Authentication+%282FA%29+with+GitHub+in+SourceTree).)
* **[PoshGit](https://github.com/dahlbyk/posh-git)** -- Integrates Git commands with PowerShell.
* **[Git-Scm](http://www.git-scm.com/downloads)** -- Git on the command line. (For real retro charm, write [markdown in Emacs](http://jblevins.org/projects/markdown-mode/).)
* **Visual Studio and [VS Code](https://code.visualstudio.com/)** -- These integrate well with GitHub repos as well as VSO.

## Tips and Tricks
* Brand new to Git? Command-line phobic? Check out [Recommended tools for beginners](jasgro/tools-for-beginners.md) for recommendations on how to get started.
* Instructions for [editing content through the GitHub UI](domars/Directions_To_Update_Existing_Topic_Using_Browser.md), a way to make updates without a local clone.
* Tables have you down? Check out some [markdown table creation tips](jasgro/table_creation_tools.md).
* This is only for TEST1111111


<!--HONumber=Jun16_HO1-->


