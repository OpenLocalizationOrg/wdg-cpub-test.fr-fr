Converting WDCML to Markdown for Open Publishing
--------------------------

This topic describes how to convert WDCML to Markdown that validates and renders correctly in the MSDN Open Publishing environment.  The preferred way to do this is by using the built-in support in the cbx build command.  Here's how:


1. Go to [IDWeb](https://idweb/identitymanagement/aspx/groups/AllGroups.aspx) and ensure that you are a member of the MSDN Reporting SG for your domain.  You may need to wait up to 24 hours for permissions to propagate.

1.  Install the latest release of [ Pandoc](https://github.com/jgm/pandoc/releases).  Pandoc is updated periodically, so if it's been a while since you installed it, consider upgrading.  A recent fix improved table rendering, for example.  By default, Pandoc installs to `c:\Users\<alias>\AppData\Local\Pandoc\`, which is added to your PATH.

1. Do an `sd sync`.

2. Use `cbx msdn markdown` to build your project into .md files.

 * After the regular cbx build, you will see two passes with progress bars.  The first is a fast pass to change .md formatting to match OP requirements.  The second is the A keyword conversion to URLs, which takes significantly longer.  The whole conversion can take up to an hour for a project containing 1500 topics.
 * If the database pass fails, you will see: Error connecting to db server.  Ensure that you have perms on the MSDN Reporting SG.
 * Sometimes database access can be problematic.  If you can't connect, try again a couple hours later.
 * PROTIP: On rare occasions (ask Jason), you may need to update the local version of `convert-keywords.ps1` with the fully qualified name of the reporting server: reporting.mtps.glbdns2.microsoft.com.

Manual Conversion
-----


If you have problems with the automation, please send a bug report to DDPUB.  

The following steps are what the first pass above does.  They are listed here for posterity.  

1. Fix links as follows:
    * Replace .htm link suffixes with .md, for in-project targets, for example:
        * `[Creating a Driver From Existing Source Files](creating_a_driver_from_existing_source_files.htm)`.  
    * Replace A keywords with URLs, for example:
        * `[Kernel-Mode Driver Framework](kmdf.portal)`
        * `<a href="wmi.mofcomp"><strong>mofcomp</strong></a>`
    * Remove In This Section links at the top

2. Switch references to upper case Images directory to images: `![Visual Studio Solution Explorer Driver Package Project](images/VsSlnExplorer.png)`

3. Remove any %20 in URLs if they exist: `[MSBuild](%20http://go.microsoft.com/fwlink/p/?linkid=262804)`

4. If See Also section is present, prepend asterisks to create bulleted list.

8. If existing, delete second occurrence of local target string: `[Manually installing WDTF on a test computer](dtf.runtime_library#manual_install_wdtf#manual_install_wdtf)`

9. Update embedded video links from: `![]()` to look like this:

    ```
    <iframe src="https://hubs-video.ssl.catalog.video.msn.com/embed/57464a96-8900-4194-b806-813eb1dd6ac6/IA?csid=ux-en-us&MsnPlayerLeadsWith=html&PlaybackMode=Inline&MsnPlayerDisplayShareBar=false&MsnPlayerDisplayInfoButton=false&iframe=true&QualityOverride=HD" width="720" height="405" allowFullScreen="true" frameBorder="0" scrolling="no"></iframe>
    ```
    **Note**:  JasGro to follow up on video plans and correct URL

10. Remove initial span so that OP creates correct topic title for text on browser tab: `<span id="vsdriver.avoiding_floating_point_errors_in_custom_build_environments"></span>`

11. Remove nested parenthetical version selector (v=vs.85, e.g.) from links: `[InfVerif](https://msdn.microsoft.com/en-us/Library/Windows/Hardware/Dn929319(v=vs.85).aspx)`

12. (Hardware team only) For mailto links, replace nested parentheses with %28, %29: `[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[VsDriver\vsdriver]:%20Analyzing%20a%20Driver%20Using%20Code%20Analysis%20and%20Verification%20Tools%20%20RELEASE:%20(9/30/2015)&body=...` Topics that contain parentheses in the topic title also cause additional parentheses in the mailto link: `[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[VsDriver\vsdriver]:%20What%20happens%20when%20you%20provision%20a%20computer%20(WDK%208.0)%20%20RELEASE:%20%289/30/2015%29`

14. Remove extra carriage returns that occur after a **Note** inside a numbered list item, because it causes OP to start numbering again from 1. Leave one blank line remaining.

15. Remove copyright line: `© 2015 Microsoft. All rights reserved.`

16. Change any image file suffixes to lower case, e.g., *.png not *.PNG.

## Post-markdown conversion steps

1. Create TOC.md in parent directory.


<!--HONumber=May16_HO4-->


