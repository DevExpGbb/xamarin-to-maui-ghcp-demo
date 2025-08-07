# GitHub Copilot Custom Instructions for .NET MAUI Development

## Overview
These instructions guide GitHub Copilot and coding agents when working with .NET MAUI projects, ensuring consistent, high-quality code that follows modern best practices.

## .NET MAUI Specific Guidelines

### 1. Project Structure and Organization

#### Use Single Project Structure
- Always prefer MAUI's single-project approach over multi-project solutions
- Organize platform-specific code in `Platforms/` folders:
  ```
  MyApp/
  ├── Platforms/
  │   ├── Android/
  │   ├── iOS/
  │   ├── Windows/
  │   └── MacCatalyst/
  ├── Resources/
  │   ├── Images/
  │   ├── Fonts/
  │   └── Styles/
  ├── Views/
  ├── ViewModels/
  ├── Models/
  ├── Services/
  └── MauiProgram.cs
  ```

#### Resource Organization
- Place shared resources in appropriate `Resources/` subfolders
- Use descriptive naming for resources (e.g., `icon-user-profile.png`)
- Organize styles in separate XAML files under `Resources/Styles/`

### 2. Dependency Injection Best Practices

#### Service Registration
- Always register services in `MauiProgram.cs` using the builder pattern:
  ```csharp
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

          // Register services
          builder.Services.AddSingleton<IDataService, DataService>();
          builder.Services.AddTransient<MainPageViewModel>();
          builder.Services.AddTransient<MainPage>();

          return builder.Build();
      }
  }
  ```

#### Service Lifetimes
- Use `AddSingleton` for services that maintain state across the app
- Use `AddTransient` for lightweight services and ViewModels
- Use `AddScoped` sparingly, typically for request-scoped operations

#### Constructor Injection
- Always use constructor injection instead of service locator pattern:
  ```csharp
  public partial class MainPage : ContentPage
  {
      private readonly IDataService _dataService;
      private readonly MainPageViewModel _viewModel;

      public MainPage(IDataService dataService, MainPageViewModel viewModel)
      {
          _dataService = dataService;
          _viewModel = viewModel;
          InitializeComponent();
          BindingContext = _viewModel;
      }
  }
  ```

### 3. XAML Best Practices

#### Use Compiled Bindings
- Always specify `x:DataType` for better performance and IntelliSense:
  ```xml
  <ContentPage x:Class="MyApp.MainPage"
               x:DataType="vm:MainPageViewModel">
      <Label Text="{Binding Title}" />
  </ContentPage>
  ```

#### Prefer New Layout Controls
- Use `VerticalStackLayout` and `HorizontalStackLayout` instead of `StackLayout`
- Use `Grid` for complex layouts, `FlexLayout` for responsive designs
- Consider `CollectionView` over `ListView` for better performance

#### Resource Management
- Define styles in separate resource dictionaries
- Use merged dictionaries for organization:
  ```xml
  <Application.Resources>
      <ResourceDictionary>
          <ResourceDictionary.MergedDictionaries>
              <ResourceDictionary Source="Resources/Styles/Colors.xaml" />
              <ResourceDictionary Source="Resources/Styles/Styles.xaml" />
          </ResourceDictionary.MergedDictionaries>
      </ResourceDictionary>
  </Application.Resources>
  ```

### 4. Handler Implementation

#### Follow Handler Pattern
- When creating custom handlers, inherit from appropriate base handlers
- Use property mappers for clean property handling:
  ```csharp
  public class CustomEntryHandler : EntryHandler
  {
      public static readonly IPropertyMapper<CustomEntry, CustomEntryHandler> PropertyMapper = 
          new PropertyMapper<CustomEntry, CustomEntryHandler>(ViewMapper)
          {
              [nameof(CustomEntry.BorderColor)] = MapBorderColor,
          };

      public CustomEntryHandler() : base(PropertyMapper) { }

      private static void MapBorderColor(CustomEntryHandler handler, CustomEntry entry)
      {
          handler.UpdateBorderColor();
      }
  }
  ```

#### Register Handlers Properly
- Register handlers in `MauiProgram.cs`:
  ```csharp
  builder.ConfigureMauiHandlers(handlers =>
  {
      handlers.AddHandler<CustomEntry, CustomEntryHandler>();
  });
  ```

## C# Coding Standards

### 1. Naming Conventions

#### Classes and Methods
- Use PascalCase for classes, methods, properties, and events
- Use camelCase for local variables and parameters
- Use meaningful, descriptive names:
  ```csharp
  // Good
  public class UserProfileService
  {
      public async Task<UserProfile> GetUserProfileAsync(string userId)
      {
          var userProfile = await _repository.GetByIdAsync(userId);
          return userProfile;
      }
  }

  // Avoid
  public class UPS
  {
      public async Task<UserProfile> Get(string id) { }
  }
  ```

#### Constants and Fields
- Use PascalCase for public constants
- Use camelCase with underscore prefix for private fields:
  ```csharp
  public class MyClass
  {
      public const int MaxRetryCount = 3;
      private readonly IService _service;
      private string _cachedValue;
  }
  ```

### 2. Async/Await Best Practices

#### Always Use Async Suffix
- Append "Async" to async method names:
  ```csharp
  public async Task<List<User>> GetUsersAsync()
  {
      return await _repository.GetAllAsync();
  }
  ```

#### Avoid Async Void
- Never use `async void` except for event handlers:
  ```csharp
  // Good - Event handler
  private async void OnButtonClicked(object sender, EventArgs e)
  {
      await ProcessDataAsync();
  }

  // Good - Return Task
  public async Task ProcessDataAsync()
  {
      await _service.ProcessAsync();
  }
  ```

#### Use ConfigureAwait(false)
- Use `ConfigureAwait(false)` in library code and services:
  ```csharp
  public async Task<string> GetDataAsync()
  {
      var result = await _httpClient.GetStringAsync(url).ConfigureAwait(false);
      return result;
  }
  ```

### 3. Error Handling

#### Use Specific Exceptions
- Throw specific exception types with meaningful messages:
  ```csharp
  public void ValidateUser(User user)
  {
      if (user == null)
          throw new ArgumentNullException(nameof(user));
      
      if (string.IsNullOrWhiteSpace(user.Email))
          throw new ArgumentException("Email cannot be empty", nameof(user));
  }
  ```

#### Implement Proper Exception Handling
- Handle exceptions appropriately, don't swallow them:
  ```csharp
  try
  {
      await _service.ProcessAsync();
  }
  catch (HttpRequestException ex)
  {
      _logger.LogError(ex, "Failed to process HTTP request");
      // Handle or rethrow with additional context
      throw new ServiceException("Unable to connect to service", ex);
  }
  ```

### 4. MVVM Pattern Implementation

#### ViewModels
- Inherit from `ObservableObject` (CommunityToolkit.Mvvm)
- Use `[ObservableProperty]` for automatic property generation:
  ```csharp
  public partial class MainPageViewModel : ObservableObject
  {
      [ObservableProperty]
      private string title = "Welcome";

      [ObservableProperty]
      private bool isLoading;

      [RelayCommand]
      private async Task LoadDataAsync()
      {
          IsLoading = true;
          try
          {
              // Load data
          }
          finally
          {
              IsLoading = false;
          }
      }
  }
  ```

#### Commands
- Use `[RelayCommand]` attribute for command generation
- Include error handling in command implementations
- Use async commands for async operations

### 5. Performance Best Practices

#### Memory Management
- Dispose of disposable resources properly
- Use `using` statements or `using` declarations:
  ```csharp
  using var httpClient = new HttpClient();
  var response = await httpClient.GetAsync(url);
  ```

#### Collections
- Use appropriate collection types:
  - `List<T>` for most scenarios
  - `ObservableCollection<T>` for data binding
  - `ImmutableList<T>` for immutable data
  - `ConcurrentCollection<T>` for thread-safe operations

#### String Operations
- Use `StringBuilder` for multiple string concatenations
- Use string interpolation for formatting:
  ```csharp
  var message = $"User {user.Name} has {user.Points} points";
  ```

### 6. Code Organization

#### File Structure
- One class per file
- Match file name to class name
- Group related classes in appropriate folders

#### Using Statements
- Sort using statements alphabetically
- Remove unused using statements
- Use global using statements for commonly used namespaces

#### Code Documentation
- Use XML documentation for public APIs:
  ```csharp
  /// <summary>
  /// Retrieves user profile information by user ID.
  /// </summary>
  /// <param name="userId">The unique identifier for the user.</param>
  /// <returns>A task representing the user profile data.</returns>
  public async Task<UserProfile> GetUserProfileAsync(string userId)
  {
      // Implementation
  }
  ```

## Platform-Specific Guidelines

### Android
- Use appropriate Android resource qualifiers for different screen densities
- Implement proper activity lifecycle handling
- Follow Android material design guidelines

### iOS
- Respect iOS Human Interface Guidelines
- Handle safe areas properly
- Implement proper memory management for iOS specifics

### Windows
- Follow WinUI 3 design patterns
- Implement proper window management
- Consider desktop-specific features

## Code Quality Rules

### 1. Always Follow SOLID Principles
- Single Responsibility Principle
- Open/Closed Principle
- Liskov Substitution Principle
- Interface Segregation Principle
- Dependency Inversion Principle

### 2. Use Modern C# Features
- Pattern matching
- Record types for data transfer objects
- Nullable reference types
- Init-only properties
- Target-typed new expressions

### 3. Testing Considerations
- Write unit tests for business logic
- Use dependency injection to enable testability
- Mock external dependencies
- Test ViewModels independently of Views

### 4. Security Best Practices
- Never hardcode sensitive information
- Use secure storage for credentials
- Validate all inputs
- Use HTTPS for network communications

## Tools and Extensions

### Recommended NuGet Packages
- `CommunityToolkit.Mvvm` - MVVM helpers
- `CommunityToolkit.Maui` - Additional controls and features
- `Microsoft.Extensions.Logging` - Logging framework
- `Serilog` - Structured logging

### Code Analysis
- Enable nullable reference types
- Use EditorConfig for consistent formatting
- Enable code analysis rules
- Use StyleCop for style enforcement

These guidelines ensure that all generated code follows modern .NET MAUI best practices, maintains consistency across the project, and provides a solid foundation for maintainable, performant applications.
