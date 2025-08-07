# Xamarin.Forms to .NET MAUI Migration Guide

## Overview
This folder contains comprehensive prompts and guides for migrating Xamarin.Forms applications to .NET MAUI. Each prompt focuses on a specific aspect of the migration process.

## Available Prompts

### 1. [Project Structure Migration](./xamarin-to-maui-project-structure.md)
Covers the conversion of project files, solution structure, and basic configuration from Xamarin.Forms to .NET MAUI format.

**Key Topics:**
- Project file updates (.csproj changes)
- Platform consolidation
- Resource management
- Application startup configuration

### 2. [API Migration](./xamarin-to-maui-api-migration.md)
Focuses on updating C# code to use .NET MAUI APIs instead of deprecated Xamarin.Forms APIs.

**Key Topics:**
- Namespace updates
- Application lifecycle changes
- Dependency Service to Dependency Injection
- Device information APIs
- Navigation pattern updates

### 3. [Custom Renderers to Handlers](./xamarin-to-maui-handlers.md)
Detailed guide for converting Xamarin.Forms custom renderers to the new .NET MAUI Handler architecture.

**Key Topics:**
- Handler architecture overview
- Property mapping system
- Platform-specific view creation
- Handler registration
- Performance improvements

### 4. [XAML Migration](./xamarin-to-maui-xaml.md)
Covers XAML file updates, namespace changes, and new MAUI-specific XAML features.

**Key Topics:**
- XAML namespace declarations
- Style and resource updates
- New layout controls
- Compiled bindings
- Performance optimizations

### 5. [Platform-Specific Code](./xamarin-to-maui-platform-code.md)
Guide for migrating platform-specific implementations from separate projects to MAUI's unified structure.

**Key Topics:**
- Platforms folder organization
- MainActivity/AppDelegate updates
- Service implementation migration
- Resource and asset management
- Dependency injection setup

### 6. [NuGet Package Migration](./xamarin-to-maui-packages.md)
Comprehensive guide for updating NuGet packages from Xamarin.Forms ecosystem to MAUI-compatible versions.

**Key Topics:**
- Core package replacements
- Third-party package compatibility
- Alternative package recommendations
- MauiProgram registration
- Testing strategy

### 7. [Complete Migration Checklist](./xamarin-to-maui-checklist.md)
Comprehensive checklist to ensure thorough and successful migration with proper testing and validation.

**Key Topics:**
- Pre-migration assessment
- Step-by-step migration process
- Testing and validation procedures
- Performance optimization
- Deployment preparation

## How to Use These Prompts

### For Complete Migration
1. Start with the **Project Structure Migration** prompt
2. Follow with **API Migration** for code updates
3. Use **Platform-Specific Code** for platform implementations
4. Apply **XAML Migration** for UI updates
5. Convert custom controls using **Custom Renderers to Handlers**
6. Update dependencies with **NuGet Package Migration**
7. Validate everything using the **Complete Migration Checklist**

### For Specific Issues
- Use individual prompts when you need to focus on a particular aspect
- Reference the checklist for validation steps
- Cross-reference related prompts for comprehensive understanding

### Best Practices
- Always backup your project before starting migration
- Test frequently during the migration process
- Migrate one aspect at a time for easier debugging
- Use the checklist to ensure nothing is missed
- Document any custom solutions for future reference

## Additional Resources

### Microsoft Documentation
- [.NET MAUI Documentation](https://docs.microsoft.com/en-us/dotnet/maui/)
- [Upgrade from Xamarin.Forms](https://docs.microsoft.com/en-us/dotnet/maui/migration/)

### Community Resources
- [.NET MAUI Community Toolkit](https://github.com/CommunityToolkit/Maui)
- [MAUI Samples Repository](https://github.com/dotnet/maui-samples)

### Tools
- [.NET Upgrade Assistant](https://docs.microsoft.com/en-us/dotnet/core/porting/upgrade-assistant-overview)
- [XAML Hot Reload](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/xaml/hot-reload)

## Contributing
If you find issues with these prompts or have suggestions for improvements, please create an issue or submit a pull request.

## Support
For specific migration questions or issues, refer to:
- Official .NET MAUI documentation
- Stack Overflow with the `maui` tag
- .NET MAUI GitHub repository discussions
