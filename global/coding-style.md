## Coding style best practices

- **Consistent Naming Conventions**: Establish and follow naming conventions for variables, functions, classes, and files across the codebase
- **Automated Formatting**: Maintain consistent code style (indenting, line breaks, etc.)
- **Meaningful Names**: Choose descriptive names that reveal intent; avoid abbreviations and single-letter variables except in narrow contexts
- **Small, Focused Functions**: Keep functions small and focused on a single task for better readability and testability
- **Consistent Indentation**: Use consistent indentation (spaces or tabs) and configure your editor/linter to enforce it
- **Remove Dead Code**: Delete unused code, commented-out blocks, and imports rather than leaving them as clutter
- **Backward compatability only when required:** Unless specifically instructed otherwise, assume you do not need to write additional code logic to handle backward compatability.
- **DRY Principle**: Avoid duplication by extracting common logic into reusable functions or modules

### C# Specific Standards

#### Braces and Formatting
- **Opening braces on same line**: Place ALL opening braces `{` on the same line as the statement that precedes them (K&R style) - applies to classes, methods, properties, control flow statements, lambda expressions, and event handlers
- **All branches use braces**: Surround all `if` and `else` statement branches with braces, regardless of whether they are single-line statements

#### Type Declarations
- **Explicit types over var**: Use explicit type names instead of `var` for better code clarity and maintainability
- **Collection expressions**: Use C# 12's collection expression syntax `[]` for initializing collections (e.g., `List<string> items = [];`)
- **Target-typed new**: When collection expressions aren't available, use target-typed new expressions (e.g., `List<string> items = new();`)

#### Variable Naming
- **Class-level variables**: Use underscore-prefixed camelCase (e.g., `_customerName`, `_orderId`, `_connectionString`)
- **Local variables**: Use camelCase without prefix (e.g., `customerName`, `totalPrice`)
- **Type-suffixed variables**: For non-trivial types, suffix variable names with the type name (e.g., `spinePhraseAcrosticFont`, `primaryDatabaseConnection`)
- **Single type variables**: When only one instance of a type exists in scope, use just the type name in camelCase (e.g., `artboard`, `httpClient`)

#### Method and Class Naming
- **Methods**: PascalCase and descriptive (e.g., `CalculateTotalPrice`, `ProcessCustomerOrder`)
- **Classes**: PascalCase and descriptive (e.g., `OrderProcessor`, `CustomerDataValidator`)
- **Avoid capital sequences**: Use PascalCase with only the first letter of each word capitalized, even for acronyms (e.g., `HtmlUpdater` not `HTMLUpdater`, `JsonSerializer` not `JSONSerializer`, `XmlParser` not `XMLParser`)
- **Parameters**: camelCase and descriptive (e.g., `customerId`, `customerName`, `emailAddress`)
- **Properties**: PascalCase and descriptive (e.g., `CustomerName`, `OrderDate`, `TotalAmount`)

#### Nullable Reference Types
- **Nullable always enabled**: Assume `<Nullable>enable</Nullable>` is always set in project files
- **No unnecessary null checks**: Do not check non-nullable parameters for null; only check parameters explicitly declared as nullable (e.g., `Order?`)
- **Null checks for nullable types**: When a parameter is nullable, perform null checks and throw `ArgumentNullException` if appropriate
