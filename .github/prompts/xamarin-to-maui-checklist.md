---
model: GPT-4.1
mode: agent
description: Comprehensive checklist to ensure successful migration from Xamarin.Forms to .NET MAUI with proper testing and validation.
---
# .NET MAUI Migration Complete Project Checklist

## Objective
Comprehensive checklist to ensure successful migration from Xamarin.Forms to .NET MAUI with proper testing and validation.

## Pre-Migration Assessment

### ✅ Project Analysis
- [ ] Document current Xamarin.Forms version
- [ ] List all NuGet packages and their versions
- [ ] Identify custom renderers and effects
- [ ] Document platform-specific code
- [ ] Identify third-party dependencies
- [ ] Review target platforms (Android, iOS, Windows, macOS)

### ✅ Compatibility Check
- [ ] Verify all packages have MAUI-compatible versions
- [ ] Check for deprecated APIs in current code
- [ ] Identify breaking changes that need addressing
- [ ] Review custom control implementations

## Migration Execution

### ✅ Project Structure
- [ ] Create new MAUI project structure
- [ ] Set up Platforms folders (Android, iOS, Windows, MacCatalyst)
- [ ] Move platform-specific code to appropriate Platforms folders
- [ ] Update solution file structure
- [ ] Remove old platform-specific projects

### ✅ Project Files and Configuration
- [ ] Update .csproj to MAUI format with `<UseMaui>true</UseMaui>`
- [ ] Set correct TargetFrameworks (net8.0-android, net8.0-ios, etc.)
- [ ] Configure application properties (ApplicationId, ApplicationVersion)
- [ ] Update Android manifest and iOS Info.plist
- [ ] Configure app icons and splash screens

### ✅ Package Updates
- [ ] Replace Xamarin.Forms with Microsoft.Maui.Controls
- [ ] Replace Xamarin.Essentials with Microsoft.Maui.Essentials
- [ ] Update all third-party packages to MAUI-compatible versions
- [ ] Remove obsolete packages
- [ ] Add CommunityToolkit.Maui if needed

### ✅ Code Migration
- [ ] Update namespace declarations (Xamarin.Forms → Microsoft.Maui.Controls)
- [ ] Replace DependencyService with dependency injection
- [ ] Update Device.* calls to DeviceInfo.* or equivalent
- [ ] Convert custom renderers to handlers
- [ ] Update platform-specific code to new format
- [ ] Fix compilation errors

### ✅ XAML Updates
- [ ] Update XAML namespace declarations
- [ ] Replace deprecated controls with new equivalents
- [ ] Update resource dictionary structure
- [ ] Add x:DataType for compiled bindings where possible
- [ ] Test XAML rendering on all platforms

### ✅ Application Startup
- [ ] Create MauiProgram.cs with proper configuration
- [ ] Register services and dependencies
- [ ] Configure fonts, colors, and themes
- [ ] Set up logging if needed
- [ ] Remove old App.xaml startup code

## Testing and Validation

### ✅ Build Validation
- [ ] Project builds successfully for all target platforms
- [ ] No compilation errors or warnings
- [ ] NuGet packages restore correctly
- [ ] Platform-specific builds complete without errors

### ✅ Functionality Testing

#### Core App Features
- [ ] App launches successfully on all platforms
- [ ] Navigation works correctly
- [ ] Data binding functions properly
- [ ] User interface renders correctly
- [ ] Platform-specific features work as expected

#### Platform-Specific Testing
- [ ] **Android**: Test on various Android versions and devices
- [ ] **iOS**: Test on iPhone and iPad with different iOS versions
- [ ] **Windows**: Test WinUI 3 functionality
- [ ] **macOS**: Test Mac Catalyst if applicable

#### Performance Testing
- [ ] App startup time is acceptable
- [ ] UI responsiveness is maintained
- [ ] Memory usage is within expected ranges
- [ ] No significant performance regressions

### ✅ Feature Validation
- [ ] Custom controls work correctly
- [ ] Platform-specific services function properly
- [ ] File I/O operations work as expected
- [ ] Network requests function correctly
- [ ] Local data storage works properly
- [ ] Push notifications (if applicable)
- [ ] Background tasks (if applicable)

## Post-Migration Optimization

### ✅ Performance Optimization
- [ ] Enable compiled bindings where possible
- [ ] Optimize layout structures
- [ ] Review and optimize resource usage
- [ ] Enable AOT compilation if beneficial
- [ ] Configure trimming settings

### ✅ Modern MAUI Features
- [ ] Implement new layout controls (VerticalStackLayout, HorizontalStackLayout)
- [ ] Use improved graphics and drawing APIs
- [ ] Leverage new animation capabilities
- [ ] Implement accessibility improvements
- [ ] Use new theming options

### ✅ Code Quality
- [ ] Update to modern C# language features
- [ ] Implement proper error handling
- [ ] Add comprehensive logging
- [ ] Update unit tests
- [ ] Review and update documentation

## Deployment Preparation

### ✅ Build Configuration
- [ ] Configure release builds for all platforms
- [ ] Set up code signing for iOS and Android
- [ ] Configure app store metadata
- [ ] Test release builds thoroughly

### ✅ CI/CD Updates
- [ ] Update build pipelines for MAUI
- [ ] Configure automated testing
- [ ] Set up deployment workflows
- [ ] Update environment variables and secrets

## Documentation and Knowledge Transfer

### ✅ Documentation Updates
- [ ] Update technical documentation
- [ ] Document breaking changes and workarounds
- [ ] Update developer setup instructions
- [ ] Create migration notes for future reference

### ✅ Team Knowledge Transfer
- [ ] Conduct code reviews
- [ ] Share lessons learned
- [ ] Update development guidelines
- [ ] Train team on MAUI-specific features

## Final Validation

### ✅ Production Readiness
- [ ] All critical functionality verified
- [ ] Performance meets requirements
- [ ] No blocking issues identified
- [ ] Rollback plan prepared
- [ ] Monitoring and analytics configured

### ✅ User Acceptance
- [ ] User testing completed
- [ ] Feedback incorporated
- [ ] Known issues documented
- [ ] Support documentation updated

## Success Criteria
- ✅ App runs on all target platforms without crashes
- ✅ All core functionality works as expected
- ✅ Performance is equal to or better than Xamarin.Forms version
- ✅ No data loss or corruption
- ✅ User experience is maintained or improved
- ✅ Development team is comfortable with MAUI tooling

## Common Issues and Solutions

### Build Issues
- Check target framework compatibility
- Verify package versions
- Clear bin/obj folders and rebuild

### Runtime Issues
- Check platform-specific implementations
- Verify service registrations
- Review handler implementations

### UI Issues
- Validate XAML namespace updates
- Check style and resource references
- Test on multiple screen sizes

### Performance Issues
- Enable compiled bindings
- Optimize layout hierarchies
- Review image and resource loading
