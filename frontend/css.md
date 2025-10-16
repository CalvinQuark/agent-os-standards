## CSS best practices (Blazor / Fluent UI)

- **Dark Theme Default**: Always configure Fluent UI applications to use dark mode by default (e.g., `<FluentDesignTheme Mode="DesignThemeModes.Dark" />` in App.razor or MainLayout.razor)
- **Fluent UI Design Tokens**: Use Fluent UI's design tokens (CSS custom properties) for colors, spacing, typography, and other design values to maintain consistency
- **Component-Scoped CSS**: Use CSS isolation (`.razor.css` files) for component-specific styles that are automatically scoped to prevent conflicts
- **Minimal Custom CSS**: Leverage Fluent UI Blazor components and their built-in styling to reduce custom CSS maintenance burden
- **Fluent UI Theming**: Customize the application appearance using Fluent UI's theming system rather than overriding individual component styles
- **Avoid Overriding Framework Styles**: Work with Fluent UI's design system and parameters rather than fighting against them with excessive CSS overrides
- **Class and Style Parameters**: Use component `Class` and `Style` parameters to apply custom styling when needed (e.g., `<FluentButton Class="custom-button" />`)
- **Global Styles**: Place global styles in `app.css` or `site.css` and use them sparingly; prefer component-level styling
- **CSS Custom Properties**: Define application-specific CSS custom properties for values not covered by Fluent UI tokens
- **Large Screen Media Queries**: Use custom media queries for displays beyond Fluent UI's 1024px breakpoint (e.g., `@media (min-width: 1920px)` for FHD+, `@media (min-width: 2560px)` for 4K) to optimize layout and content density on large displays
- **Touchscreen Detection**: Use `@media (hover: none)` and `@media (pointer: coarse)` to detect touch-primary devices and adapt interaction patterns accordingly
- **Performance**: Fluent UI Blazor handles CSS optimization automatically; avoid loading unnecessary custom stylesheets
