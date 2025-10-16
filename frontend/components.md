## UI component best practices (Blazor / Fluent UI)

- **Single Responsibility**: Each Blazor component should have one clear purpose and do it well
- **Reusability**: Design components to be reused across different contexts with configurable `[Parameter]` properties
- **Composability**: Build complex UIs by combining smaller, simpler components using RenderFragment and child content rather than monolithic structures
- **Clear Interface**: Define explicit, well-documented `[Parameter]` properties with sensible defaults and XML documentation comments
- **Encapsulation**: Keep internal implementation details private; expose only necessary `[Parameter]` properties and public methods
- **Consistent Naming**: Use PascalCase for component files and parameters (e.g., `CustomerGrid.razor`, `[Parameter] public string Title { get; set; }`); follow Blazor conventions
- **Component Structure**: Organize components as `.razor` files with optional code-behind (`.razor.cs`) for complex logic to keep markup clean
- **State Management**: Keep state as local as possible using component fields; use cascading values or state containers only when needed by multiple components
- **Minimal Parameters**: Keep the number of `[Parameter]` properties manageable; if a component needs many parameters, consider composition or splitting it
- **Fluent UI Components**: Prefer Fluent UI Blazor components (FluentButton, FluentDataGrid, FluentTextField, etc.) over custom HTML elements for consistency
- **RenderFragment Usage**: Use `RenderFragment` and `RenderFragment<T>` for flexible content composition (e.g., `[Parameter] public RenderFragment? ChildContent { get; set; }`)
- **Lifecycle Methods**: Use appropriate lifecycle methods (`OnInitialized`, `OnParametersSet`, `OnAfterRender`) and their async variants appropriately
- **Server Interactivity**: Mark interactive components with `@rendermode InteractiveServer` and handle SignalR disconnection scenarios gracefully
- **Dispose Pattern**: Implement `IDisposable` or `IAsyncDisposable` to clean up event handlers, timers, and subscriptions
- **Documentation**: Document component usage, parameters, and provide XML comments for easier adoption by team members
