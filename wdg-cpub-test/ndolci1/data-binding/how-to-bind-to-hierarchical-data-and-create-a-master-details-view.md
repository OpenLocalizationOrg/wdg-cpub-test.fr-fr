---
ms.assetid: 0C69521B-47E0-421F-857B-851B0E9605F2
title: Bind hierarchical data and create a master/details view
description: You can make a multi-level master/details (also known as list-details) view of hierarchical data by binding items controls to CollectionViewSource instances that are bound together in a chain.
---
Bind hierarchical data and create a master/details view
===========================================================================

\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]


**Note**  Also see the [Master/detail sample](http://go.microsoft.com/fwlink/p/?linkid=619991).

 

You can make a multi-level master/details (also known as list-details) view of hierarchical data by binding items controls to [**CollectionViewSource**](https://msdn.microsoft.com/library/windows/apps/BR209833) instances that are bound together in a chain. In this topic we use the [{x:Bind} markup extension](https://msdn.microsoft.com/library/windows/apps/Mt204783) where possible, and the more flexible (but less performant) [{Binding} markup extension](https://msdn.microsoft.com/library/windows/apps/Mt204782) where necessary.

One common structure for Universal Windows Platform (UWP) apps is to navigate to different details pages when a user makes a selection in a master list. This is useful when you want to provide a rich visual representation of each item at every level in a hierarchy. Another option is to display multiple levels of data on a single page. This is useful when you want to display a few simple lists that let the user quickly drill down to an item of interest. This topic describes how to implement this interaction. The [**CollectionViewSource**](https://msdn.microsoft.com/library/windows/apps/BR209833) instances keep track of the current selection at each hierarchical level.

We'll create a view of a sports team hierarchy that is organized into lists for leagues, divisions, and teams, and includes a team details view. When you select an item from any list, the subsequent views update automatically.

![master/details view of a sports hierarchy](images/xaml-masterdetails.png)

Prerequisites
-------------------------------------------------------------------------------------------------------------

This topic assumes that you know how to create a basic UWP app. For instructions on creating your first UWP app, see [Create your first UWP app using C# or Visual Basic](https://msdn.microsoft.com/library/windows/apps/Hh974581).

Create the project
---------------------------------------------------------------------------------------------------------------------------------

Create a new **Blank Application (Windows Universal)** project. Name it "MasterDetailsBinding".

Create the data model
---------------------------------------------------------------------------------------------------------------------------------------------

Add a new class to your project, name it ViewModel.cs, and add this code to it. This will be your binding source class.

<span codelanguage="CSharp"></span>
<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">C#</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><pre><code>using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace MasterDetailsBinding { public class Team { public string Name { get; set; } public int Wins { get; set; } public int Losses { get; set; } }

    public class Division
    {
        public string Name { get; set; }
        public IEnumerable&lt;Team&gt; Teams { get; set; }
    }

    public class League
    {
        public string Name { get; set; }
        public IEnumerable&lt;Division&gt; Divisions { get; set; }
    }

    public class LeagueList : List&lt;League&gt;
    {
        public LeagueList()
        {
            this.AddRange(GetLeague().ToList());
        }

        public IEnumerable&lt;League&gt; GetLeague()
        {
            return from x in Enumerable.Range(1, 2)
                   select new League
                   {
                       Name = &quot;League &quot; + x,
                       Divisions = GetDivisions(x).ToList()
                   };
        }

        public IEnumerable&lt;Division&gt; GetDivisions(int x)
        {
            return from y in Enumerable.Range(1, 3)
                   select new Division
                   {
                       Name = String.Format(&quot;Division {0}-{1}&quot;, x, y),
                       Teams = GetTeams(x, y).ToList()
                   };
        }

        public IEnumerable&lt;Team&gt; GetTeams(int x, int y)
        {
            return from z in Enumerable.Range(1, 4)
                   select new Team
                   {
                       Name = String.Format(&quot;Team {0}-{1}-{2}&quot;, x, y, z),
                       Wins = 25 - (x * y * z),
                       Losses = x * y * z
                   };
        }
    }
}</code></pre></td>
</tr>
</tbody>
</table>

Create the view
---------------------------------------------------------------------------------------------------------------------

Next, expose the binding source class from the class that represents your page of markup. We do that by adding a property of type **LeagueList** to **MainPage**.

<span codelanguage="CSharp"></span>
<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">C#</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><pre><code>namespace MasterDetailsBinding
{
    /// &lt;summary&gt;
    /// An empty page that can be used on its own or navigated to within a Frame.
    /// &lt;/summary&gt;
    public sealed partial class MainPage : Page
    {
        public MainPage()
        {
            this.InitializeComponent();
            this.ViewModel = new LeagueList();
        }
        public LeagueList ViewModel { get; set; }
    }
}</code></pre></td>
</tr>
</tbody>
</table>

Finally, replace the contents of the MainPage.xaml file with the following markup, which declares three [**CollectionViewSource**](https://msdn.microsoft.com/library/windows/apps/BR209833) instances and binds them together in a chain. The subsequent controls can then bind to the appropriate **CollectionViewSource**, depending on its level in the hierarchy.

<span codelanguage="XAML"></span>
<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">XAML</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><pre><code>&lt;Page
    x:Class=&quot;MasterDetailsBinding.MainPage&quot;
    xmlns=&quot;http://schemas.microsoft.com/winfx/2006/xaml/presentation&quot;
    xmlns:x=&quot;http://schemas.microsoft.com/winfx/2006/xaml&quot;
    xmlns:local=&quot;using:MasterDetailsBinding&quot;
    xmlns:d=&quot;http://schemas.microsoft.com/expression/blend/2008&quot;
    xmlns:mc=&quot;http://schemas.openxmlformats.org/markup-compatibility/2006&quot;
    mc:Ignorable=&quot;d&quot;&gt;

    &lt;Page.Resources&gt;
        &lt;CollectionViewSource x:Name=&quot;Leagues&quot;
            Source=&quot;{x:Bind ViewModel}&quot;/&gt;
        &lt;CollectionViewSource x:Name=&quot;Divisions&quot;
            Source=&quot;{Binding Divisions, Source={StaticResource Leagues}}&quot;/&gt;
        &lt;CollectionViewSource x:Name=&quot;Teams&quot;
            Source=&quot;{Binding Teams, Source={StaticResource Divisions}}&quot;/&gt;

        &lt;Style TargetType=&quot;TextBlock&quot;&gt;
            &lt;Setter Property=&quot;FontSize&quot; Value=&quot;15&quot;/&gt;
            &lt;Setter Property=&quot;FontWeight&quot; Value=&quot;Bold&quot;/&gt;
        &lt;/Style&gt;

        &lt;Style TargetType=&quot;ListBox&quot;&gt;
            &lt;Setter Property=&quot;FontSize&quot; Value=&quot;15&quot;/&gt;
        &lt;/Style&gt;

        &lt;Style TargetType=&quot;ContentControl&quot;&gt;
            &lt;Setter Property=&quot;FontSize&quot; Value=&quot;15&quot;/&gt;
        &lt;/Style&gt;

    &lt;/Page.Resources&gt;

    &lt;Grid Background=&quot;{ThemeResource ApplicationPageBackgroundThemeBrush}&quot;&gt;

        &lt;StackPanel Orientation=&quot;Horizontal&quot;&gt;

            &lt;!-- All Leagues view --&gt;

            &lt;StackPanel Margin=&quot;5&quot;&gt;
                &lt;TextBlock Text=&quot;All Leagues&quot;/&gt;
                &lt;ListBox ItemsSource=&quot;{Binding Source={StaticResource Leagues}}&quot; 
                    DisplayMemberPath=&quot;Name&quot;/&gt;
            &lt;/StackPanel&gt;

            &lt;!-- League/Divisions view --&gt;

            &lt;StackPanel Margin=&quot;5&quot;&gt;
                &lt;TextBlock Text=&quot;{Binding Name, Source={StaticResource Leagues}}&quot;/&gt;
                &lt;ListBox ItemsSource=&quot;{Binding Source={StaticResource Divisions}}&quot; 
                    DisplayMemberPath=&quot;Name&quot;/&gt;
            &lt;/StackPanel&gt;

            &lt;!-- Division/Teams view --&gt;

            &lt;StackPanel Margin=&quot;5&quot;&gt;
                &lt;TextBlock Text=&quot;{Binding Name, Source={StaticResource Divisions}}&quot;/&gt;
                &lt;ListBox ItemsSource=&quot;{Binding Source={StaticResource Teams}}&quot; 
                    DisplayMemberPath=&quot;Name&quot;/&gt;
            &lt;/StackPanel&gt;

            &lt;!-- Team view --&gt;

            &lt;ContentControl Content=&quot;{Binding Source={StaticResource Teams}}&quot;&gt;
                &lt;ContentControl.ContentTemplate&gt;
                    &lt;DataTemplate&gt;
                        &lt;StackPanel Margin=&quot;5&quot;&gt;
                            &lt;TextBlock Text=&quot;{Binding Name}&quot; 
                                FontSize=&quot;15&quot; FontWeight=&quot;Bold&quot;/&gt;
                            &lt;StackPanel Orientation=&quot;Horizontal&quot; Margin=&quot;10,10&quot;&gt;
                                &lt;TextBlock Text=&quot;Wins:&quot; Margin=&quot;0,0,5,0&quot;/&gt;
                                &lt;TextBlock Text=&quot;{Binding Wins}&quot;/&gt;
                            &lt;/StackPanel&gt;
                            &lt;StackPanel Orientation=&quot;Horizontal&quot; Margin=&quot;10,0&quot;&gt;
                                &lt;TextBlock Text=&quot;Losses:&quot; Margin=&quot;0,0,5,0&quot;/&gt;
                                &lt;TextBlock Text=&quot;{Binding Losses}&quot;/&gt;
                            &lt;/StackPanel&gt;
                        &lt;/StackPanel&gt;
                    &lt;/DataTemplate&gt;
                &lt;/ContentControl.ContentTemplate&gt;
            &lt;/ContentControl&gt;

        &lt;/StackPanel&gt;

    &lt;/Grid&gt;
&lt;/Page&gt;</code></pre></td>
</tr>
</tbody>
</table>

Note that by binding directly to the [**CollectionViewSource**](https://msdn.microsoft.com/library/windows/apps/BR209833), you're implying that you want to bind to the current item in bindings where the path cannot be found on the collection itself. There's no need to specify the **CurrentItem** property as the path for the binding, although you can do that if there's any ambiguity). For example, the [**ContentControl**](https://msdn.microsoft.com/library/windows/apps/BR209365) representing the team view has its [**Content**](https://msdn.microsoft.com/library/windows/apps/BR209365-content) property bound to the `Teams`**CollectionViewSource**. However, the controls in the [**DataTemplate**](https://msdn.microsoft.com/library/windows/apps/BR242348) bind to properties of the `Team` class because the **CollectionViewSource** automatically supplies the currently selected team from the teams list when necessary.

 

 



<!--HONumber=Jun16_HO1-->


