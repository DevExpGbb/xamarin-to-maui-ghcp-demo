---
model: GPT-4.1
mode: agent
description: Identify and update NuGet package references from Xamarin.Forms ecosystem to .NET MAUI compatible versions.
---
# Convert Xamarin.Forms NuGet Packages to .NET MAUI

## Objective
Identify and update NuGet package references from Xamarin.Forms ecosystem to .NET MAUI compatible versions.

## Core Package Updates

### 1. Essential Package Replacements

| Xamarin.Forms Package | .NET MAUI Package | Notes |
|----------------------|-------------------|-------|
| `Xamarin.Forms` | `Microsoft.Maui.Controls` | Core UI controls |
| `Xamarin.Essentials` | `Microsoft.Maui.Essentials` | Cross-platform APIs |
| `Xamarin.Forms.Maps` | `Microsoft.Maui.Controls.Maps` | Map controls |
| `Xamarin.CommunityToolkit` | `CommunityToolkit.Maui` | Community controls and extensions |
| `Xamarin.Forms.Visual.Material` | Built into MAUI | Material design is integrated |

### 2. Platform-Specific Packages
- Remove platform-specific Xamarin packages
- Most functionality is now built into MAUI
- Some may need MAUI-specific alternatives

### 3. Third-Party Package Compatibility
- Check for MAUI-compatible versions
- Look for .NET 6+ compatible alternatives
- Some packages may need replacement or removal

## Package Migration Examples

### Before (Xamarin.Forms packages.config or .csproj):
```xml
<PackageReference Include="Xamarin.Forms" Version="5.0.0.2196" />
<PackageReference Include="Xamarin.Essentials" Version="1.7.0" />
<PackageReference Include="Xamarin.CommunityToolkit" Version="2.0.5" />
<PackageReference Include="Xamarin.Forms.Maps" Version="5.0.0.2196" />
<PackageReference Include="SkiaSharp.Views.Forms" Version="2.88.3" />
<PackageReference Include="Lottie.Forms" Version="5.0.0" />
<PackageReference Include="Plugin.Settings" Version="3.0.1" />
<PackageReference Include="Plugin.Permissions" Version="6.0.1" />
```

### After (.NET MAUI .csproj):
```xml
<PackageReference Include="Microsoft.Maui.Controls" Version="8.0.0" />
<PackageReference Include="Microsoft.Maui.Essentials" Version="8.0.0" />
<PackageReference Include="CommunityToolkit.Maui" Version="7.0.0" />
<PackageReference Include="Microsoft.Maui.Controls.Maps" Version="8.0.0" />
<PackageReference Include="SkiaSharp.Views.Maui.Controls" Version="2.88.6" />
<PackageReference Include="SkiaSharp.Extended.UI.Maui" Version="2.0.0" />
<PackageReference Include="Microsoft.Extensions.Logging.Debug" Version="8.0.0" />
<!-- Plugin.Settings and Plugin.Permissions functionality is now in Maui.Essentials -->
```

## Common Package Migrations

### 1. UI and Controls
```xml
<!-- OLD -->
<PackageReference Include="Syncfusion.Xamarin.SfChart" Version="19.4.0.56" />
<PackageReference Include="Telerik.UI.for.Xamarin" Version="2022.1.119.1" />

<!-- NEW -->
<PackageReference Include="Syncfusion.Maui.Charts" Version="24.1.41" />
<PackageReference Include="Telerik.UI.for.Maui" Version="6.0.0" />
```

### 2. Image Handling
```xml
<!-- OLD -->
<PackageReference Include="FFImageLoading.Forms" Version="2.4.11.982" />

<!-- NEW -->
<!-- Built into MAUI, or use alternatives like: -->
<PackageReference Include="Microsoft.Maui.Graphics" Version="8.0.0" />
```

### 3. HTTP and Networking
```xml
<!-- OLD -->
<PackageReference Include="Refit" Version="6.3.2" />
<PackageReference Include="System.Net.Http" Version="4.3.4" />

<!-- NEW -->
<PackageReference Include="Refit.HttpClientFactory" Version="7.0.0" />
<!-- System.Net.Http is built into .NET 6+ -->
```

### 4. MVVM and Data Binding
```xml
<!-- OLD -->
<PackageReference Include="Prism.Unity.Forms" Version="8.1.97" />
<PackageReference Include="ReactiveUI.XamForms" Version="18.4.1" />

<!-- NEW -->
<PackageReference Include="Prism.Maui" Version="8.1.273" />
<PackageReference Include="ReactiveUI.Maui" Version="19.5.1" />
<!-- Or use built-in -->
<PackageReference Include="CommunityToolkit.Mvvm" Version="8.2.2" />
```

## MauiProgram.cs Registration

### Community Toolkit MAUI Setup:
```csharp
public static class MauiProgram
{
    public static MauiApp CreateMauiApp()
    {
        var builder = MauiApp.CreateBuilder();
        builder
            .UseMauiApp<App>()
            .UseMauiCommunityToolkit()
            .UseMauiMaps()
            .ConfigureFonts(fonts =>
            {
                fonts.AddFont("OpenSans-Regular.ttf", "OpenSansRegular");
            });

        return builder.Build();
    }
}
```

## Package Compatibility Checklist

### ✅ MAUI Compatible (Direct Migration Available)
- Syncfusion controls
- Telerik UI
- DevExpress
- SkiaSharp
- Lottie
- CommunityToolkit
- Prism
- ReactiveUI

### ⚠️ Needs Alternative (No Direct MAUI Version)
- FFImageLoading → Use built-in Image caching or alternatives
- Plugin.Settings → Use MAUI Essentials Preferences
- Plugin.Permissions → Use MAUI Essentials Permissions
- Acr.UserDialogs → Use MAUI Community Toolkit alerts

### ❌ No Longer Needed
- Xamarin.Forms.Visual.Material → Built into MAUI
- Plugin.CurrentActivity → Not needed in MAUI
- Many Xamarin plugins → Replaced by MAUI Essentials

## Migration Steps
1. **Audit Current Packages**: List all NuGet packages in the solution
2. **Check Compatibility**: Verify MAUI support for each package
3. **Find Alternatives**: Research replacements for incompatible packages
4. **Update Project Files**: Replace package references
5. **Update Using Statements**: Change namespaces in code files
6. **Test Functionality**: Verify all features work with new packages
7. **Performance Testing**: Ensure new packages don't impact performance
8. **Documentation**: Update any package-specific documentation

## Testing Strategy
- Test core functionality on all target platforms
- Verify UI rendering and interactions
- Check performance impact of new packages
- Validate platform-specific features
- Test offline scenarios where applicable
