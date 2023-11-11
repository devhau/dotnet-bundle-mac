# dotnet-bundle-mac

Command-line interface tools for bundling .NET Core projects into MacOS applications (.app)

### Installation

Install MSBuild task via NuGet package: `MacBundle.DotNet`

[![NuGet](https://img.shields.io/nuget/v/MacBundle.DotNet.svg)](https://www.nuget.org/packages/MacBundle.DotNet/)

```
<PackageReference Include="MacBundle.DotNet" Version="*" />
```
dotnet nuget push MacBundle.DotNet.0.9.14.nupkg --api-key oy2f66dodqki5sconpgqcv2w4qmjrz6ura7fnc66v2vioe --source https://api.nuget.org/v3/index.json

### Development
* `cd TestBundle`
* run `dotnet msbuild -t:BundleAppMac -p:RuntimeIdentifier=osx-x64`
* verify `Build/Debug/net5.0/osx-x64/publish` contents

### Using the tool

```
dotnet msbuild -t:BundleAppMac -p:RuntimeIdentifier=osx-x64 [-p: ...]
```

### Properties

Define properties to override default bundle values

```
<PropertyGroup>
    <CFBundleName>AppName</CFBundleName> <!-- Also defines .app file name -->
    <CFBundleDisplayName>App Name</CFBundleDisplayName>
    <CFBundleIdentifier>com.example</CFBundleIdentifier>
    <CFBundleVersion>1.0.0</CFBundleVersion>
    <CFBundlePackageType>APPL</CFBundlePackageType>
    <CFBundleSignature>????</CFBundleSignature>
    <CFBundleExecutable>AppName</CFBundleExecutable>
    <CFBundleIconFile>AppName.icns</CFBundleIconFile> <!-- Will be copied from output directory -->
    <NSPrincipalClass>NSApplication</NSPrincipalClass>
    <NSHighResolutionCapable>true</NSHighResolutionCapable>

    <!-- Optional -->
    <NSRequiresAquaSystemAppearance>true</NSRequiresAquaSystemAppearance>
</PropertyGroup>

<ItemGroup>
    <!-- Optional URLTypes.Check TestBundle.csproj for a working example. -->
    <CFBundleURLTypes Include="dummy"> <!-- The name of this file is irrelevant, it's a MSBuild requirement.-->
        <CFBundleURLName>TestApp URL</CFBundleURLName>
        <CFBundleURLSchemes>testappurl;testappurl://</CFBundleURLSchemes> <!-- Note the ";" separator-->
    </CFBundleURLTypes>
    <CFBundleURLTypes Include="dummy">
        <CFBundleURLName>TestApp URL2</CFBundleURLName>
        <CFBundleURLSchemes>test://</CFBundleURLSchemes>
    </CFBundleURLTypes>
</ItemGroup>
```

More info: https://developer.apple.com/library/archive/documentation/CoreFoundation/Conceptual/CFBundles/BundleTypes/BundleTypes.html
