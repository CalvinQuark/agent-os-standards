## Responsive design best practices (Blazor / Fluent UI)

- **Mobile-First Development**: Start with mobile layout and progressively enhance for larger screens using Fluent UI's responsive utilities
- **Fluent UI Breakpoints**: Use Fluent UI's built-in responsive breakpoints and grid system consistently across the application
- **Fluid Layouts**: Use percentage-based widths, `FluentGrid`, and `FluentGridItem` components that adapt to screen size
- **Relative Units**: Prefer rem/em units over fixed pixels for better scalability and accessibility; Fluent UI uses relative units by default
- **Test Across Devices**: Test and verify Blazor pages across multiple screen sizes from mobile to tablet to desktop and ensure a balanced, user-friendly viewing and reading experience on all
- **Responsive Components**: Leverage Fluent UI component parameters that adapt to screen size (e.g., `FluentDataGrid` responsive columns, `FluentNavMenu` adaptive display)
- **CSS Media Queries**: Use CSS media queries in `.razor.css` files for component-specific responsive behavior when needed
- **Touch-Friendly Design**: Ensure tap targets are appropriately sized (minimum 44x44px) for mobile users; Fluent UI components are touch-friendly by default
- **Performance on Mobile**: Optimize images and assets for mobile network conditions; consider lazy loading with `<img loading="lazy">` or Fluent UI image components
- **Readable Typography**: Maintain readable font sizes across all breakpoints without requiring zoom; use Fluent UI's typography tokens
- **Content Priority**: Show the most important content first on smaller screens through thoughtful layout decisions; use conditional rendering with `@if` for adaptive UIs
- **Server Rendering Performance**: Consider the impact of interactive server rendering on mobile networks; implement loading states and optimize SignalR payload size
