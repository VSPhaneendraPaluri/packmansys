---
layout: post
title: Creating and Publising NuGet Package using Co-App
date: 2019-09-09 07:18 +0530
tags: nuget, co-app, systemc
---

# My First Experimental Package Using Co-App

Hey guys, I'm trying out my first NuGet package.  NuGet is one of the generic ways of creating, publishing and distributing packages.  But, default users may publish their packages to NuGet.org from where it becomes publicly accessible to every other user.  Else, users may upload it to their server spaces as well, making them available for the destined users only.

There are apparently two ways of creating NuGet packages.
One is the more the XML way of doing it that uses direct interaction with NuGet binaries and other related artefacts.
The other is what would be my topic of my post - "How to use Co-App to creating NuGet packages ?"


# Get Started Building First Package

If you would have known how much effort it takes to build NuGet package using native tools, you might be in for a big surprise the way Co-App helps users to create NuGet packages.  It is to be understood that Co-App is still a tool in the maturing state and might miss few features that are supported by NuGet natively.  If so ever do you think that it good to have such features made available from Co-App, kindly reach out to the Co-App community.


# Co-App Installation

For installation on Windows (powershell), refer [here](http://coapp.org/tutorials/installation.html).
Once, all the required actions like environmental paths and updating of packages is completed, we are good to proceed further.

The site also lists about the step-by-step guide using 'AutoPackage' tool to build NuGet packages.


# Chosen Build is 'SystemC'

I'd like to demonstrate this work of how to package SystemC distributables using Co-App.
For this, one might want to download SystemC from [accellera.org](accellera.org) site.  Try to extract the zip on your machine and try to build the binaries (libraraies) from the sources.  Currently, I'm demonstrating package creation for Windows only.  We can try build packages for different platforms, compilers, compiler versions, etcetera.

Then let's try performing the below mentioned steps:
- First of all, we need to create a file ending in extenion (.autopkg).
- AutoPackage file contents are usually listed as if they are scoped (similar to JSON) just that the keys define the contents type and is not followed by a semi-colon(:) as like in JSON.
- The contents to be packaged using the rules within AutoPackage files could be classified as listed below:
  - '#defines' at the global scope lists the macros to be used throughout the file
  - First scoped contents, apart from '#defines', are listed under 'nuget'
  - 'nuget' contains 'nuspec' grouping type that lists the various attributes of the AutoPackage file, like nuget-id, version, title, authors, owners, license, projectUrl, iconUrl, copyrights, etcetara.
  - Next section would be the 'files' category that lists what all sources are needed to be packaged.  These could include list of:
    - List of include files listed under 'nestedInclude' type
    - List of documentation files listed under 'docs'
    - List of libraries listed under 'pivots' (more is mentioned below)
  - Finally, it is time to specify 'targets' grouping.  Here, user could mention what all typse of include headers, target build types (release or debug) are to be packaged.
  - Users can also mention a one final section related to 'props' defining the property file attributes.
  - Publish the package to NuGet.org by running the following command
  ~~~powershell
    Write-NuGetPackage <'path-to-the-AutoPackage-file'>
  ~~~
- Now, go to NuGet.org and search for your published package using the nuget-id.

## More About Pivots.
- As mentioned above, 'pivots' are a combination of [<'platform'>, <'compiler+version'>, <'build-type'>].
  User can defined as many pivots as possible.  An examples is:
  - [x86, v100, Debug] --> x86 platform, MSVC v10.0, Debug type build

The relevant AutoPackage file to build SystemC NuGet package has been listed over [here]({{ site.repository-path }}/{{ site.baseurl }}/CoApp/SystemC).
