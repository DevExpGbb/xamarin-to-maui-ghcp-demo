---
model: GPT-4.1
mode: agent
description: Convert the project structure and configuration files from Xamarin.Forms to .NET MAUI format.
---

# Convert Xamarin.Forms Project Structure to .NET MAUI

## Objective
Convert the project structure and configuration files from Xamarin.Forms to .NET MAUI format.

## Key Changes Required

### 1. Project File Updates
- Convert `.csproj` files to use the new .NET MAUI project format
- Update `TargetFramework` to `net8.0` or later
- Add `<UseMaui>true</UseMaui>` property
- Replace platform-specific projects with single multi-targeting project
- Update NuGet package references from Xamarin.Forms to Microsoft.Maui

### 2. Platform Configuration
- Move platform-specific code from separate projects to `Platforms` folders
- Update MainActivity.cs (Android) to use MAUI startup
- Update AppDelegate.cs (iOS) to use MAUI startup
- Update MainWindow.xaml.cs (Windows) for WinUI3

### 3. Application Startup
- Replace `App.xaml` with `MauiProgram.cs` for dependency injection and configuration
- Update application lifecycle methods
- Configure services and dependencies using the new builder pattern

### 4. Resource Management
- Move images and assets to appropriate platform folders or use single-project resources
- Update font and color resource declarations
- Convert splash screens to MAUI format

## Example Transformations

### Before (Xamarin.Forms .csproj):
```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
  </PropertyGroup>
  <PackageReference Include="Xamarin.Forms" Version="5.0.0.2196" />
</Project>
```

### After (.NET MAUI .csproj):
```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFrameworks>net8.0-android;net8.0-ios;net8.0-maccatalyst</TargetFrameworks>
    <OutputType>Exe</OutputType>
    <RootNamespace>YourApp</RootNamespace>
    <UseMaui>true</UseMaui>
    <SingleProject>true</SingleProject>
    <ImplicitUsings>enable</ImplicitUsings>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.Maui.Controls" Version="8.0.0" />
  </ItemGroup>
</Project>
```

## Instructions
1. Analyze the current project structure
2. Create a new MAUI project structure
3. Migrate platform-specific code to appropriate Platforms folders
4. Update all project files and references
5. Test compilation and basic functionality
