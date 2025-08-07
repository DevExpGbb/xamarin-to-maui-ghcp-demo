---
model: GPT-4.1
mode: agent
description: Migrate platform-specific code from separate Xamarin.Forms projects to .NET MAUI's unified project structure with Platforms folders.
---
# Convert Xamarin.Forms Platform-Specific Code to .NET MAUI

## Objective
Migrate platform-specific code from separate Xamarin.Forms projects to .NET MAUI's unified project structure with Platforms folders.

## New Platform Structure

### 1. Folder Organization
```
YourApp/
├── Platforms/
│   ├── Android/
│   │   ├── MainActivity.cs
│   │   ├── MainApplication.cs
│   │   ├── AndroidManifest.xml
│   │   └── Resources/
│   ├── iOS/
│   │   ├── AppDelegate.cs
│   │   ├── Info.plist
│   │   └── Entitlements.plist
│   ├── MacCatalyst/
│   │   ├── AppDelegate.cs
│   │   └── Info.plist
│   └── Windows/
│       ├── App.xaml
│       ├── App.xaml.cs
│       └── Package.appxmanifest
├── MauiProgram.cs
└── App.xaml
```

## Platform Code Migration

### Android Changes

#### Before (Xamarin.Forms Android):
```csharp
// MainActivity.cs
[Activity(Label = "MyApp", Icon = "@mipmap/icon", Theme = "@style/MainTheme")]
public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsAppCompatActivity
{
    protected override void OnCreate(Bundle savedInstanceState)
    {
        TabLayoutResource = Resource.Layout.Tabbar;
        ToolbarResource = Resource.Layout.Toolbar;

        base.OnCreate(savedInstanceState);
        
        Xamarin.Essentials.Platform.Init(this, savedInstanceState);
        global::Xamarin.Forms.Forms.Init(this, savedInstanceState);
        LoadApplication(new App());
    }
}
```

#### After (.NET MAUI Android):
```csharp
// Platforms/Android/MainActivity.cs
[Activity(Theme = "@style/Maui.SplashTheme", MainLauncher = true, LaunchMode = LaunchMode.SingleTop)]
public class MainActivity : MauiAppCompatActivity
{
}

// Platforms/Android/MainApplication.cs
[Application]
public class MainApplication : MauiApplication
{
    public MainApplication(IntPtr handle, JniHandleOwnership ownership)
        : base(handle, ownership)
    {
    }

    protected override MauiApp CreateMauiApp() => MauiProgram.CreateMauiApp();
}
```

### iOS Changes

#### Before (Xamarin.Forms iOS):
```csharp
// AppDelegate.cs
[Register("AppDelegate")]
public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate
{
    public override bool FinishedLaunching(UIApplication app, NSDictionary options)
    {
        global::Xamarin.Forms.Forms.Init();
        LoadApplication(new App());

        return base.FinishedLaunching(app, options);
    }
}
```

#### After (.NET MAUI iOS):
```csharp
// Platforms/iOS/AppDelegate.cs
[Register("AppDelegate")]
public class AppDelegate : MauiUIApplicationDelegate
{
    protected override MauiApp CreateMauiApp() => MauiProgram.CreateMauiApp();
}
```

### Windows Changes

#### After (.NET MAUI Windows):
```csharp
// Platforms/Windows/App.xaml.cs
public partial class App : MauiWinUIApplication
{
    public App()
    {
        this.InitializeComponent();
    }

    protected override MauiApp CreateMauiApp() => MauiProgram.CreateMauiApp();
}
```

## Service Registration and Platform-Specific Implementation

### Before (Xamarin.Forms with DependencyService):
```csharp
// Shared interface
public interface IDeviceService
{
    string GetDeviceInfo();
}

// Android implementation
[assembly: Dependency(typeof(DeviceService))]
public class DeviceService : IDeviceService
{
    public string GetDeviceInfo()
    {
        return $"{Build.Manufacturer} {Build.Model}";
    }
}

// Usage
var deviceService = DependencyService.Get<IDeviceService>();
```

### After (.NET MAUI with Dependency Injection):
```csharp
// Shared interface (same)
public interface IDeviceService
{
    string GetDeviceInfo();
}

// Platform implementation in Platforms/Android/
public class DeviceService : IDeviceService
{
    public string GetDeviceInfo()
    {
        return $"{Build.Manufacturer} {Build.Model}";
    }
}

// Registration in MauiProgram.cs
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

#if ANDROID
        builder.Services.AddSingleton<IDeviceService, Platforms.Android.DeviceService>();
#elif IOS
        builder.Services.AddSingleton<IDeviceService, Platforms.iOS.DeviceService>();
#endif

        return builder.Build();
    }
}

// Usage with dependency injection
public partial class MainPage : ContentPage
{
    private readonly IDeviceService _deviceService;

    public MainPage(IDeviceService deviceService)
    {
        _deviceService = deviceService;
        InitializeComponent();
    }
}
```

## Resource and Asset Migration

### 1. Images and Icons
- Move images from platform-specific resource folders to shared Resources/Images
- Update references in platform configuration files
- Use the new single-project resource system

### 2. Fonts
- Move fonts to Resources/Fonts
- Register fonts in MauiProgram.cs

### 3. Colors and Styles
- Move to Resources/Styles
- Update App.xaml to reference new locations

## Migration Steps
1. Create new Platforms folder structure
2. Migrate MainActivity/AppDelegate code to new format
3. Move platform-specific implementations to appropriate Platform folders
4. Update service registration to use dependency injection
5. Migrate resources to new folder structure
6. Update manifest and configuration files
7. Test platform-specific functionality on each target platform

## Key Benefits
- Single project instead of multiple platform projects
- Better resource sharing
- Improved dependency injection
- Cleaner platform-specific code organization
- Better build performance
