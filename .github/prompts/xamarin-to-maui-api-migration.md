---
model: GPT-4.1
mode: agent
description: Update C# code to use .NET MAUI APIs instead of deprecated Xamarin.Forms APIs.
---
# Convert Xamarin.Forms Code to .NET MAUI APIs

## Objective
Update C# code to use .NET MAUI APIs instead of deprecated Xamarin.Forms APIs.

## Key API Changes

### 1. Namespace Updates
- Replace `using Xamarin.Forms;` with `using Microsoft.Maui.Controls;`
- Replace `using Xamarin.Essentials;` with `using Microsoft.Maui.Essentials;`
- Update platform-specific namespaces

### 2. Application Lifecycle
- Replace `Xamarin.Forms.Application` with `Microsoft.Maui.Controls.Application`
- Update `OnStart()`, `OnSleep()`, `OnResume()` methods
- Migrate to new lifecycle events in MauiProgram

### 3. Dependency Service Changes
- Replace `DependencyService.Get<T>()` with dependency injection
- Move interface implementations to platform-specific folders
- Register services in MauiProgram.cs

### 4. Device Information
- Update `Device.RuntimePlatform` to `DeviceInfo.Platform`
- Replace `Device.OS` with `DeviceInfo.Platform`
- Update device-specific checks

### 5. Navigation Changes
- Update `Navigation.PushAsync()` and `Navigation.PopAsync()` usage
- Review Shell navigation if applicable
- Update modal navigation patterns

### 6. Renderer Updates
- Convert Custom Renderers to Handlers
- Update Effect implementations
- Migrate platform-specific UI customizations

## Common Replacements

### Before (Xamarin.Forms):
```csharp
using Xamarin.Forms;
using Xamarin.Essentials;

public partial class App : Application
{
    public App()
    {
        InitializeComponent();
        MainPage = new MainPage();
    }

    protected override void OnStart()
    {
        // Handle when your app starts
    }
}

// Dependency Service usage
var service = DependencyService.Get<IMyService>();

// Device checks
if (Device.RuntimePlatform == Device.iOS)
{
    // iOS specific code
}
```

### After (.NET MAUI):
```csharp
using Microsoft.Maui.Controls;

public partial class App : Application
{
    public App()
    {
        InitializeComponent();
        MainPage = new AppShell();
    }
}

// In MauiProgram.cs
public static class MauiProgram
{
    public static MauiApp CreateMauiApp()
    {
        var builder = MauiApp.CreateBuilder();
        builder
            .UseMauiApp<App>()
            .ConfigureFonts(fonts =>
            {
                fonts.AddFont("OpenSans-Regular.ttf", "OpenSansRegular");
            });

        builder.Services.AddSingleton<IMyService, MyService>();
        return builder.Build();
    }
}

// Dependency injection usage
// Inject in constructor: IMyService myService

// Device checks
if (DeviceInfo.Platform == DevicePlatform.iOS)
{
    // iOS specific code
}
```

## Migration Steps
1. Update all namespace declarations
2. Replace deprecated API calls with MAUI equivalents
3. Convert DependencyService to dependency injection
4. Update device and platform detection code
5. Migrate custom renderers to handlers
6. Test all functionality thoroughly
