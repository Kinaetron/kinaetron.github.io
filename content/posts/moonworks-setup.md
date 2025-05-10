+++
title = "Moonworks Setup"
date = "2025-05-10T19:15:47+01:00"
#dateFormat = "2006-01-02" # This value can be configured for per-post date formatting
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["Moonworks", "Setup", "Game Development", "C"]
keywords = ["Moonworks", "Setup", "Game Development", "C"]
description = "How to setup a new Moonworks project"
showFullContent = false
readingTime = false
hideComments = false
+++

## Intro

I've been tinkering around With the Moonworks Framework for last few months. I found this to be a great development framework and is pretty much perfect for the kind of games I want to develop. Saying all that though, I do find that the documentation for new people is pretty slim of the ground, so I thought it would be a good idea to write up something that would help other people on their journey to using it. 

What I'm going to do here though is try my best to fill in general gaps of knowledge for people who are coming over from higher level game frameworks like FNA, XNA and Unity, or people who have never really made a game before.

## Visual Studio Code

So what this isn't going to be is a tutorial series for C#, there are plenty around and all of them are way more robust and detailed than anything I would be able to supply here. Personally I would go over to Mircosoft's official video series for beginners, which you can find [here](https://www.youtube.com/watch?v=9THmGiSPjBQ&list=PLdo4fOcmZ0oULFjxrOagaERVAMbmG20Xe). Saying that though it doesn't do the best job at showing you how to install the toolset you'll need to follow the series. That video series uses Visual Studio Code, it's nice, relatively light and most importantly cross platform. You'll also need to .NET SDK which is the library that'll let you write and build C# code.

- Download Visual Studio Code from [here](https://code.visualstudio.com/download)
- Download SDK 9.0 from [here](https://dotnet.microsoft.com/en-us/download/dotnet)

Now open up VSCode, hit Ctrl+Shift+X to go to the extensions view, then search for "C# Dev Kit". Install the kit from the marketplace and let it download. Once that's done you're ready to go.

There are several other resources that'll get you caught up to C# if you look around the internet, if my particular suggestion doesn't suite your learning style. Once you've gotten through your C# resource of choice, come back here to learn Moonworks.

## Git
Git is a project management system for programming projects, which allows users to submit their own code updates and get updates other users make to a programming project you're all contributing to. 9 times out of 10 all this code is stored on a website called Github. Github serves as a decent backup of your coding projects too, so this is useful to use even if you're working by yourself.

Again I won't get into the weeds of this, for the same reasons I didn't for C#, but I would say this is as important to learn before picking up Moonworks as C# is. Personally I would go with this tutorial series to get a grip on this, which you can find [here](https://www.atlassian.com/git).

Again plenty of resources around the web teaching this, so if my choice of learning material isn't to your liking, please pick up something else.

## Download Moonworks
Select somewhere you want to download Moonworks to, I would suggest somewhere that will be easy for your game projects to access it from. Once you selected somewhere either

- Use this command for Git git clone --recursive https://github.com/MoonsideGames/MoonWorks

## Download Native Libraries

Moonworks uses several native libraries for various pieces of functionality, such as window management, input, and audio output.
Here's what we use and why:

- [SDL3](https://github.com/flibitijibibo/SDL3-CS) Window management, Input, Graphics
- [IRO](https://github.com/MoonsideGames/IRO) Image Loading
- [FAudio](https://github.com/FNA-XNA/FAudio) Audio
- [Wellsping](https://github.com/MoonsideGames/Wellspring) Font Rendering
- [dav1dfile](https://github.com/MoonsideGames/dav1dfile) Compressed Video

You can find the libraries precompiled [here](https://moonside.games/files/moonlibs.tar.gz). This contains all of the native libraries for Windows, Linux and Mac.

## Create a Project
Pick your favorite C# IDE and spin up a new console application in it. You'll need to add a direct reference to Moonworks project in your new project you can do this via running the command in command prompt or powershell  
- `dotnet sln add <Rest of Path>/Moonworks/MoonWorks.csproj` 

or you can go into your IDE and just add it directly via their GUI.

You'll also need to copy the native libraries you downloaded in the earlier step each time you build the project. You can do this opening up a text editor and copy the xml below. Take note that at each section where I wrote Rest of Path, you need to point it to the folder (moonlibs) where those native binaries are. Now save this file as CopyMoonlibs.targets in the same folder where the project is at the top level you should see a csproj / sln file in there.

```
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

	<Target Name="Runtime ID"  AfterTargets="Build">
    	<Message Text="Runtime ID: $(RuntimeIdentifier)" Importance="high"/>
	</Target>

	<ItemGroup Condition="$([System.Runtime.InteropServices.RuntimeInformation]::IsOSPlatform($([System.Runtime.InteropServices.OSPlatform]::Windows)))">
		<Content Include="*Rest of Path*\moonlibs\win64\*.*">
			<Link>%(RecursiveDir)%(Filename)%(Extension)</Link>
			<CopyToOutputDirectory>Always</CopyToOutputDirectory>
		</Content>
	</ItemGroup>
	<ItemGroup Condition="$([System.Runtime.InteropServices.RuntimeInformation]::IsOSPlatform($([System.Runtime.InteropServices.OSPlatform]::Linux)))">
		<Content Include="*Rest of Path*\moonlibs\lib64\*.*">
			<Link>%(RecursiveDir)%(Filename)%(Extension)</Link>
			<CopyToOutputDirectory>Always</CopyToOutputDirectory>
		</Content>
	</ItemGroup>
	<ItemGroup Condition="$([System.Runtime.InteropServices.RuntimeInformation]::IsOSPlatform($([System.Runtime.InteropServices.OSPlatform]::OSX)))">
		<Content Include="*Rest of Path*\moonlibs\macos\*.*">
			<Link>%(RecursiveDir)%(Filename)%(Extension)</Link>
			<CopyToOutputDirectory>Always</CopyToOutputDirectory>
		</Content>
	</ItemGroup>
</Project>
```

Then open up your .csproj file and add `<Import Project=".\CopyMoonlibs.targets" />` just before `</PropertyGroup>` So now you should have a VSCode project open with a file called Program.cs. First make sure your project builds correctly.

Press the Run and Debug button and that should just build and run

Create a new file in your project called ExampleGame and copy this section of code into it.

```
using MoonWorks;
using MoonWorks.Graphics;

namespace *Your project name*;

public class ExampleGame : Game
{
    public ExampleGame(
        AppInfo appInfo,
        WindowCreateInfo windowCreateInfo,
        FramePacingSettings framePacingSettings
        ) : base(
            appInfo,
            windowCreateInfo,
            framePacingSettings,
            ShaderFormat.SPIRV | ShaderFormat.DXIL | ShaderFormat.MSL | ShaderFormat.DXBC)
    {
    }

    protected override void Update(TimeSpan delta) { }

    protected override void Draw(double alpha)
    {
        CommandBuffer cmdbuf = GraphicsDevice.AcquireCommandBuffer();
        Texture swapchainTexture = cmdbuf.AcquireSwapchainTexture(MainWindow);
        if (swapchainTexture != null)
        {
            var renderPass = cmdbuf.BeginRenderPass(
                new ColorTargetInfo(swapchainTexture, Color.CornflowerBlue)
            );
            cmdbuf.EndRenderPass(renderPass);
        }
        GraphicsDevice.Submit(cmdbuf);
    }
}
```

Finally open up your Program.cs and copy in the below code

```
using MoonWorks;

namespace *Your project name*;

internal class Program
{
    static void Main()
    {
        var windowCreateInfo = new WindowCreateInfo(
             "Example Game",
             1280,
             720,
             ScreenMode.Windowed
         );

        var framePacingSettings = FramePacingSettings.CreateLatencyOptimized(60);

        var game = new ExampleGame(
            new AppInfo("Example Game", "ExampleGame"),
            windowCreateInfo,
            framePacingSettings);

        game.Run();
    }
}
```

Press the Run and Debug button again and that should just show up an empty blue screen. Congratulations, you've just built and run your first Moonworks game project !