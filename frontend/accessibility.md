## UI accessibility best practices (Blazor / Fluent UI)

- **Semantic HTML in Razor**: Use appropriate HTML elements (nav, main, button, etc.) in Razor markup that convey meaning to assistive technologies
- **Fluent UI Accessibility**: Leverage built-in accessibility features of Fluent UI Blazor components (FluentButton, FluentTextField, etc.) which include proper ARIA attributes by default
- **Keyboard Navigation**: Ensure all interactive elements are accessible via keyboard with visible focus indicators; Fluent UI components handle this automatically
- **Touch Target Sizing**: Maintain minimum 44x44px touch targets for standard touchscreens; on large touchscreens (27+ inches), consider 48-56px targets to accommodate arm extension and reduce fatigue
- **Color Contrast**: Maintain sufficient contrast ratios (4.5:1 for normal text) and don't rely solely on color to convey information; use Fluent UI's accessible color tokens
- **Alternative Text**: Provide descriptive alt text for images using the `alt` attribute and meaningful labels for Fluent UI form components using `Label` parameter
- **Screen Reader Testing**: Test and verify that all Blazor pages and components are accessible on screen reading devices
- **ARIA When Needed**: Use ARIA attributes to enhance complex components when semantic HTML and Fluent UI defaults aren't sufficient
- **Logical Heading Structure**: Use heading levels (h1-h6) in proper order within Razor markup to create a clear document outline
- **Focus Management**: Manage focus appropriately using `FocusAsync()` on ElementReference for dynamic content, modals (FluentDialog), and navigation events
- **Server-Side Rendering**: Ensure interactive server components maintain accessibility during SignalR reconnection states with appropriate loading indicators
