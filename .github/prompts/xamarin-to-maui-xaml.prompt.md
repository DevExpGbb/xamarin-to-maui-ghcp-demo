---
model: GPT-4.1
mode: agent
description: Update XAML files and styles from Xamarin.Forms to .NET MAUI format with improved performance and new features.Update C# code to use .NET MAUI APIs instead of deprecated Xamarin.Forms APIs.
---
# Convert Xamarin.Forms XAML to .NET MAUI XAML

## Objective
Update XAML files and styles from Xamarin.Forms to .NET MAUI format with improved performance and new features.

## Key Changes

### 1. Namespace Updates
- Update XML namespace declarations
- Replace Xamarin.Forms namespaces with Microsoft.Maui.Controls
- Update platform-specific namespaces

### 2. Style and Resource Updates
- Update StaticResource and DynamicResource usage
- Migrate styles to use new MAUI styling system
- Update color and font resource definitions

### 3. Layout Changes
- Review layout behavior changes
- Update Grid and StackLayout usage where beneficial
- Consider new layout options like VerticalStackLayout and HorizontalStackLayout

### 4. Control Updates
- Update deprecated control properties
- Migrate to new control features
- Review binding syntax and converters

## XAML Transformations

### Before (Xamarin.Forms XAML):
```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="MyApp.MainPage"
             Title="Main Page">
    
    <ContentPage.Resources>
        <ResourceDictionary>
            <Color x:Key="PrimaryColor">#2196F3</Color>
            <Style x:Key="LabelStyle" TargetType="Label">
                <Setter Property="TextColor" Value="{StaticResource PrimaryColor}" />
                <Setter Property="FontSize" Value="18" />
            </Style>
        </ResourceDictionary>
    </ContentPage.Resources>

    <StackLayout Padding="10">
        <Label Text="Welcome to Xamarin.Forms!" 
               Style="{StaticResource LabelStyle}"
               HorizontalOptions="CenterAndExpand" />
        
        <Entry Placeholder="Enter text here"
               TextChanged="OnEntryTextChanged" />
        
        <Button Text="Click Me"
                Clicked="OnButtonClicked"
                BackgroundColor="{StaticResource PrimaryColor}"
                TextColor="White" />
    </StackLayout>
</ContentPage>
```

### After (.NET MAUI XAML):
```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="MyApp.MainPage"
             Title="Main Page">
    
    <ContentPage.Resources>
        <ResourceDictionary>
            <Color x:Key="PrimaryColor">#2196F3</Color>
            <Style x:Key="LabelStyle" TargetType="Label">
                <Setter Property="TextColor" Value="{StaticResource PrimaryColor}" />
                <Setter Property="FontSize" Value="18" />
            </Style>
        </ResourceDictionary>
    </ContentPage.Resources>

    <VerticalStackLayout Padding="10" Spacing="10">
        <Label Text="Welcome to .NET MAUI!" 
               Style="{StaticResource LabelStyle}"
               HorizontalOptions="Center" />
        
        <Entry Placeholder="Enter text here"
               TextChanged="OnEntryTextChanged" />
        
        <Button Text="Click Me"
                Clicked="OnButtonClicked"
                BackgroundColor="{StaticResource PrimaryColor}"
                TextColor="White" />
    </VerticalStackLayout>
</ContentPage>
```

### App.xaml Changes

#### Before (Xamarin.Forms):
```xml
<?xml version="1.0" encoding="utf-8" ?>
<Application xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="MyApp.App">
    <Application.Resources>
        <ResourceDictionary>
            <!-- Global styles -->
        </ResourceDictionary>
    </Application.Resources>
</Application>
```

#### After (.NET MAUI):
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<Application xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="MyApp.App">
    <Application.Resources>
        <ResourceDictionary>
            <ResourceDictionary.MergedDictionaries>
                <ResourceDictionary Source="Resources/Styles/Colors.xaml" />
                <ResourceDictionary Source="Resources/Styles/Styles.xaml" />
            </ResourceDictionary.MergedDictionaries>
        </ResourceDictionary>
    </Application.Resources>
</Application>
```

## Performance Improvements

### 1. Compiled Bindings
```xml
<!-- Enable compiled bindings for better performance -->
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="MyApp.MainPage"
             x:DataType="vm:MainPageViewModel">
    
    <Label Text="{Binding Title}" />
</ContentPage>
```

### 2. New Layout Controls
```xml
<!-- Use new performant layout controls -->
<VerticalStackLayout Spacing="10">
    <Label Text="Item 1" />
    <Label Text="Item 2" />
</VerticalStackLayout>

<HorizontalStackLayout Spacing="10">
    <Button Text="Cancel" />
    <Button Text="OK" />
</HorizontalStackLayout>
```

## Migration Steps
1. Update all namespace declarations in XAML files
2. Replace deprecated layout controls with new ones where beneficial
3. Update resource dictionary structure
4. Add x:DataType for compiled bindings where possible
5. Test all XAML pages for proper rendering
6. Validate data binding functionality
7. Review and optimize layout performance

## Common Issues
- Namespace changes may break custom controls
- Some layout behaviors may change slightly
- Resource loading paths may need adjustment
- Platform-specific XAML may need updates
