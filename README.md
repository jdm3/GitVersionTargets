# GitVersion.targets

GitVersions.targets is a msbuild/Visual Studio targets file that can be imported into a project to make the git repository version available to source code.

To add to a project, edit its project file (.vcxproj for C++ or .csproj for C#) and import *GetVersion.targets* near the end of the project file:

```xml
  <Import Project="GitVersion.targets" />
```

C++ code will then have git version strings available as compiler defines `GVT_BRANCH` and `GVT_COMMIT` e.g.:

```c++
    printf("GVT_BRANCH = %s\n", GVT_BRANCH); // GVT_BRANCH = main
    printf("GVT_COMMIT = %s\n", GVT_COMMIT); // GVT_COMMIT = 2252e7f7f016d064ba9e2821353517a9e1541545-dirty
```

and C# code will have them available as members of a static class `GVT.BRANCH` and `GVT.COMMIT` e.g.:

```c#
    Console.WriteLine($"GVT.BRANCH = {GVT.BRANCH}");
    Console.WriteLine($"GVT.COMMIT = {GVT.COMMIT}");
```

For the C# case, the build generates a file named *GVT_Version.cs* in the project directory; which you may want to add to your *.gitignore* file as it doesn't need to be checked in.

To customize the availability and format of the versions, set any of the following options in your project file, before importing *GitVersion.targets*:

```xml
  <!-- Optional parameters to customize version, these need to be set before importing GitVersion.props -->
  <PropertyGroup>
    <GVT_ReadBranch>true</GVT_ReadBranch>          <!-- Whether or not to read/set the GVT_BRANCH define -->
    <GVT_ReadCommit>true</GVT_ReadCommit>          <!-- Whether or not to read/set the GVT_COMMIT define -->
    <GVT_CommitHashLength>0</GVT_CommitHashLength> <!-- How many characters of the hash to use in GVT_COMMIT (0==all) -->
    <GVT_DirtySuffix>-dirty</GVT_DirtySuffix>      <!-- What suffix to use on the hash if the repository has modified files -->
  </PropertyGroup>
```
