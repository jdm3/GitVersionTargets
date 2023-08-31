# GitVersion.targets

GitVersions.targets is a msbuild/Visual Studio targets file that can be imported into a C++ project to
make the git repository version available as compile defines.

To add to a project, edit its .vcxproj file and import *GetVersion.targets* (typically near the
 end of the project file):

```xml
  <ImportGroup>
    <Import Project="GitVersion.targets" />
  </ImportGroup>
```

Then, your C++ code will have git version strings defined as `GVT_BRANCH` and `GVT_COMMIT`.  e.g.:

```c++
    printf("GVT_BRANCH = %s\n", GVT_BRANCH); // GVT_BRANCH = main
    printf("GVT_COMMIT = %s\n", GVT_COMMIT); // GVT_COMMIT = 2252e7f7f016d064ba9e2821353517a9e1541545-dirty
```

To customize the availability and format of the versions, set any of the following options before importing *GitVersion.targets*:

```xml
  <!-- Optional parameters to customize version, these need to be set before importing GitVersion.props -->
  <PropertyGroup>
      <GVT_ReadBranch>true</GVT_ReadBranch>          <!-- Whether or not to read/set the GVT_BRANCH define -->
      <GVT_ReadCommit>true</GVT_ReadCommit>          <!-- Whether or not to read/set the GVT_COMMIT define -->
      <GVT_CommitHashLength>0</GVT_CommitHashLength> <!-- How many characters of the hash to use in GVT_COMMIT (0==all) -->
      <GVT_DirtySuffix>-dirty</GVT_DirtySuffix>      <!-- What suffix to use on the hash if the repository has modified files -->
  </PropertyGroup>
```
