---
model: GPT-4.1
mode: agent
description: Migrate custom renderers from Xamarin.Forms to the new Handler architecture in .NET MAUI.
---
# Convert Xamarin.Forms Custom Renderers to .NET MAUI Handlers

## Objective
Migrate custom renderers from Xamarin.Forms to the new Handler architecture in .NET MAUI.

## Key Concepts

### 1. Architecture Changes
- Renderers are replaced with Handlers
- Handlers are more lightweight and performant
- Direct access to native views through PlatformView
- Cleaner separation of cross-platform and platform-specific code

### 2. Handler Structure
- `CreatePlatformView()` - Creates the native view
- `ConnectHandler()` - Sets up event handlers and initial state
- `DisconnectHandler()` - Cleanup when handler is disposed
- Property mappers for handling property changes

### 3. Registration
- Register handlers in MauiProgram.cs using ConfigureMauiHandlers()
- Use builder pattern for configuration

## Migration Examples

### Before (Xamarin.Forms Custom Renderer):
```csharp
// Shared code
public class CustomEntry : Entry
{
    public static readonly BindableProperty BorderColorProperty = 
        BindableProperty.Create(nameof(BorderColor), typeof(Color), typeof(CustomEntry), Color.Default);

    public Color BorderColor
    {
        get => (Color)GetValue(BorderColorProperty);
        set => SetValue(BorderColorProperty, value);
    }
}

// Android Renderer
[assembly: ExportRenderer(typeof(CustomEntry), typeof(CustomEntryRenderer))]
public class CustomEntryRenderer : EntryRenderer
{
    protected override void OnElementChanged(ElementChangedEventArgs<Entry> e)
    {
        base.OnElementChanged(e);
        
        if (Control != null && Element is CustomEntry customEntry)
        {
            UpdateBorderColor();
        }
    }

    protected override void OnElementPropertyChanged(object sender, PropertyChangedEventArgs e)
    {
        base.OnElementPropertyChanged(sender, e);
        
        if (e.PropertyName == CustomEntry.BorderColorProperty.PropertyName)
        {
            UpdateBorderColor();
        }
    }

    private void UpdateBorderColor()
    {
        if (Element is CustomEntry customEntry)
        {
            var gd = new GradientDrawable();
            gd.SetStroke(2, customEntry.BorderColor.ToAndroid());
            Control.SetBackground(gd);
        }
    }
}
```

### After (.NET MAUI Handler):
```csharp
// Shared code (same)
public class CustomEntry : Entry
{
    public static readonly BindableProperty BorderColorProperty = 
        BindableProperty.Create(nameof(BorderColor), typeof(Color), typeof(CustomEntry), Colors.Transparent);

    public Color BorderColor
    {
        get => (Color)GetValue(BorderColorProperty);
        set => SetValue(BorderColorProperty, value);
    }
}

// Handler
public class CustomEntryHandler : Microsoft.Maui.Handlers.EntryHandler
{
    public static readonly IPropertyMapper<CustomEntry, CustomEntryHandler> PropertyMapper = 
        new PropertyMapper<CustomEntry, CustomEntryHandler>(ViewMapper)
        {
            [nameof(CustomEntry.BorderColor)] = MapBorderColor,
        };

    public CustomEntryHandler() : base(PropertyMapper)
    {
    }

    protected override AppCompatEditText CreatePlatformView()
    {
        var editText = base.CreatePlatformView();
        return editText;
    }

    protected override void ConnectHandler(AppCompatEditText platformView)
    {
        base.ConnectHandler(platformView);
        UpdateBorderColor();
    }

    private static void MapBorderColor(CustomEntryHandler handler, CustomEntry entry)
    {
        handler.UpdateBorderColor();
    }

    private void UpdateBorderColor()
    {
        if (VirtualView is CustomEntry customEntry && PlatformView != null)
        {
            var gd = new GradientDrawable();
            gd.SetStroke(2, customEntry.BorderColor.ToPlatform());
            PlatformView.SetBackground(gd);
        }
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
            .ConfigureMauiHandlers(handlers =>
            {
                handlers.AddHandler<CustomEntry, CustomEntryHandler>();
            });

        return builder.Build();
    }
}
```

## Migration Steps
1. Identify all custom renderers in the project
2. Create corresponding handlers for each renderer
3. Move platform-specific logic to appropriate platform folders
4. Update property mapping to use the new mapper system
5. Register handlers in MauiProgram.cs
6. Test all custom controls thoroughly
7. Remove old renderer files and ExportRenderer attributes

## Key Differences
- No more `OnElementChanged` - use `ConnectHandler` instead
- No more `OnElementPropertyChanged` - use property mappers
- Access native view through `PlatformView` instead of `Control`
- Registration is explicit in MauiProgram.cs instead of assembly attributes
- Better performance and cleaner architecture
