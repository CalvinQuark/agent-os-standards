## Responsive design best practices (Blazor / Fluent UI)

- **Mobile-First Development**: Start with mobile layout and progressively enhance for larger screens using Fluent UI's responsive utilities
- **Fluent UI Breakpoints**: Use Fluent UI's built-in responsive breakpoints (320px, 480px, 768px, 1024px) and grid system consistently across the application
- **Large Screen Optimization**: For displays beyond 1024px (including 4K and ultra-wide monitors), use custom CSS media queries (e.g., `@media (min-width: 1920px)` or `@media (min-width: 2560px)`) to optimize layout and content density without overwhelming the user with excessive whitespace
- **Fluid Layouts**: Use percentage-based widths, `FluentGrid`, and `FluentGridItem` components that adapt to screen size
- **Relative Units**: Prefer rem/em units over fixed pixels for better scalability and accessibility; Fluent UI uses relative units by default
- **Content Density on Large Screens**: On displays wider than 1920px, consider multi-column layouts, increased information density, or constrained content widths (e.g., `max-width: 1600px; margin: 0 auto;`) to maintain readability and prevent excessive eye movement
- **Test Across Devices**: Test and verify Blazor pages across multiple screen sizes from mobile to tablet to desktop to 4K displays, ensuring a balanced, user-friendly viewing and reading experience on all
- **Responsive Components**: Leverage Fluent UI component parameters that adapt to screen size (e.g., `FluentDataGrid` responsive columns, `FluentNavMenu` adaptive display)
- **CSS Media Queries**: Use CSS media queries in `.razor.css` files for component-specific responsive behavior when needed
- **Touch-Friendly Design**: Ensure tap targets are appropriately sized (minimum 44x44px) for touch interactions; Fluent UI components are touch-friendly by default but verify on actual touchscreen devices
- **Large Touchscreen Considerations**: On large touchscreens (27+ inches), position frequently-used interactive elements within comfortable reach zones (lower-middle to center-middle of screen) and consider larger touch targets (48-56px) due to arm extension fatigue
- **Hover vs Touch States**: Design interactions that work without hover states for touchscreen devices; use `@media (hover: none)` queries to adapt UI patterns for touch-primary devices
- **Performance on Mobile**: Optimize images and assets for mobile network conditions; consider lazy loading with `<img loading="lazy">` or Fluent UI image components
- **Readable Typography**: Maintain readable font sizes across all breakpoints without requiring zoom; use Fluent UI's typography tokens; on 4K displays, ensure text remains legible at native resolution
- **Content Priority**: Show the most important content first on smaller screens through thoughtful layout decisions; use conditional rendering with `@if` for adaptive UIs; on larger screens, surface additional context and secondary information
- **Server Rendering Performance**: Consider the impact of interactive server rendering on mobile networks; implement loading states and optimize SignalR payload size
