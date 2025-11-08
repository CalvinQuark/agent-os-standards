## Coding style best practices

- **Consistent Naming Conventions**: Establish and follow naming conventions for variables, functions, classes, and files across the codebase
- **Automated Formatting**: Maintain consistent code style (indenting, line breaks, etc.)
- **Meaningful Names**: Choose descriptive names that reveal intent; avoid abbreviations and single-letter variables except in narrow contexts
- **Small, Focused Functions**: Keep functions small and focused on a single task for better readability and testability
- **Consistent Indentation**: Use consistent indentation (spaces; not tabs) and configure your editor/linter to enforce it
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
- **Target-typed new expressions**: Always use target-typed `new()` expressions to avoid redundant type specifications in object instantiation
  ```csharp
  // Correct - Target-typed new with parameters
  RootCommand rootCommand = new("description");
  StringBuilder stringBuilder = new(100);
  HttpClient httpClient = new();

  // Incorrect - Redundant type specification
  RootCommand rootCommand = new RootCommand("description");
  StringBuilder stringBuilder = new StringBuilder(100);
  HttpClient httpClient = new HttpClient();
  ```

#### Primary Constructors
- **Use primary constructors when appropriate**: Leverage C# 12's primary constructor syntax when a class's constructor only assigns parameters to fields or properties
- **When to use**: Primary constructors are ideal for simple dependency injection, immutable data classes, and straightforward parameter-to-field assignments
- **When NOT to use**: Avoid primary constructors when constructor logic includes validation, initialization beyond simple assignment, or complex setup
- **Syntax**: Declare constructor parameters directly in the class declaration (e.g., `public class OrderService(ILogger logger, IOrderRepository repository)`)
- **Field storage**: Primary constructor parameters are automatically captured and can be used throughout the class without explicit field declarations
- **Example**:
  ```csharp
  // Good: Simple dependency injection
  public class OrderService(ILogger<OrderService> logger, IOrderRepository repository) {
      public void ProcessOrder(Order order) {
          logger.LogInformation("Processing order {OrderId}", order.Id);
          repository.Save(order);
      }
  }

  // Avoid: Complex initialization logic
  public class OrderValidator {
      private readonly ILogger _logger;
      private readonly ValidationRules _rules;

      public OrderValidator(ILogger<OrderValidator> logger, ValidationConfig config) {
          _logger = logger;
          _rules = config.CreateRules(); // Complex setup - traditional constructor is clearer
          _logger.LogInformation("Validator initialized with {RuleCount} rules", _rules.Count);
      }
  }
  ```

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

#### String Literals and Symbol References
- **Use nameof() operator**: Use the `nameof` operator instead of hard-coded string literals when referring to parameter names, method names, property names, or other code symbols
  ```csharp
  // Correct - Using nameof for parameters and methods
  public void ProcessOrder(Order order) {
      if (order == null) {
          throw new ArgumentNullException(nameof(order));
      }
      _logger.LogInformation($"Starting {nameof(ProcessOrder)} for order {order.Id}");
  }

  // Correct - Using nameof() for method references in error messages
  if (_browser == null) {
      throw new InvalidOperationException($"Browser not initialized. Call {nameof(InitializeBrowserAsync)} first.");
  }

  // Incorrect - Hard-coded strings (breaks during refactoring)
  public void ProcessOrder(Order order) {
      if (order == null) {
          throw new ArgumentNullException("order");
      }
      _logger.LogInformation($"Starting ProcessOrder for order {order.Id}");
  }
  ```
- **Property change notifications**: Use `nameof` for property names in `INotifyPropertyChanged` implementations and validation scenarios to maintain refactoring safety
- **Configuration keys**: Consider using `nameof` for configuration keys that correspond to class properties to maintain refactoring safety
- **Benefits**: Symbol name changes are caught at compile-time, IDE refactoring automatically updates references, and typos are prevented

#### Type Safety and Data Structures
- **Enums over dictionaries**: Prefer enums with extension methods over dictionary-based mappings for better type safety, IntelliSense support, and compile-time checking
  ```csharp
  // Correct - Enum with extension methods
  public enum UsBankAccount {
      PersonalChecking,
      SharedPersonalVisa,
      LourdesVisa
  }

  public static class UsBankAccountExtensions {
      public static string GetLast4Digits(this UsBankAccount account) => account switch {
          UsBankAccount.PersonalChecking => "6686",
          UsBankAccount.SharedPersonalVisa => "7230",
          UsBankAccount.LourdesVisa => "2117",
          _ => throw new ArgumentOutOfRangeException(nameof(account), account, null)
      };

      public static int GetAccountId(this UsBankAccount account) => account switch {
          UsBankAccount.PersonalChecking => 3,
          UsBankAccount.SharedPersonalVisa => 4,
          UsBankAccount.LourdesVisa => 5,
          _ => throw new ArgumentOutOfRangeException(nameof(account), account, null)
      };
  }

  // Incorrect - Dictionary mapping (error-prone, no IntelliSense)
  private static readonly Dictionary<string, int> AccountIdMap = new() {
      { "6686", 3 },  // Personal Checking
      { "7230", 4 },  // Shared Personal Visa
      { "2117", 5 }   // Lourdes Visa
  };
  ```

- **Strongly-typed DataTable conversion**: Use extension methods with reflection to convert DTOs to DataTable for table-valued parameters instead of manually constructing DataTables
  ```csharp
  // Correct - Generic extension method for type safety
  public static class DataTableExtensions {
      public static DataTable ToDataTable<T>(this IEnumerable<T> items) {
          DataTable dataTable = new(typeof(T).Name);
          PropertyInfo[] properties = typeof(T).GetProperties(BindingFlags.Public | BindingFlags.Instance);

          // Add columns based on property types
          foreach (PropertyInfo prop in properties) {
              Type columnType = Nullable.GetUnderlyingType(prop.PropertyType) ?? prop.PropertyType;
              dataTable.Columns.Add(prop.Name, columnType);
          }

          // Add rows
          foreach (T item in items) {
              object[] values = new object[properties.Length];
              for (int i = 0; i < properties.Length; i++) {
                  values[i] = properties[i].GetValue(item) ?? DBNull.Value;
              }
              dataTable.Rows.Add(values);
          }

          return dataTable;
      }
  }

  // Usage
  List<AccountTransactionDto> transactions = GetTransactions();
  DataTable tvp = transactions.ToDataTable();

  // Incorrect - Manual DataTable construction (error-prone, no type safety)
  DataTable tvp = new();
  tvp.Columns.Add("AccountId", typeof(int));
  tvp.Columns.Add("Date", typeof(DateTime));
  tvp.Columns.Add("Trans", typeof(string));
  tvp.Columns.Add("Name", typeof(string));
  tvp.Columns.Add("Memo", typeof(string));
  tvp.Columns.Add("Amount", typeof(decimal));
  tvp.Columns.Add("Comment", typeof(string));

  foreach (AccountTransactionDto txn in transactions) {
      tvp.Rows.Add(txn.AccountId, txn.Date, txn.Trans,
                   txn.Name, txn.Memo, txn.Amount, txn.Comment);
  }
  ```

#### Method Modifiers (CA1822)
- **Static methods when possible**: Mark methods as `static` when they do not access instance data (fields, properties, or other instance methods)
- **Performance and clarity**: Static methods improve performance by avoiding unnecessary instance references and clearly signal that the method is stateless
- **CA1822 compliance**: Address CA1822 code analysis warnings by making methods static when they don't use instance members
  ```csharp
  // Correct - Static method that doesn't access instance data
  public static decimal ParseBalanceText(string balanceText) {
      // Implementation that only uses parameters
  }

  // Incorrect - Instance method that doesn't need instance access
  public decimal ParseBalanceText(string balanceText) {
      // Implementation that only uses parameters but is not marked static
  }
  ```

#### Numeric Literals
- **Digit separators**: Use underscores (`_`) as digit separators in large numeric literals for improved readability
  ```csharp
  // Correct - Digit separators improve readability
  decimal accountBalance = 5_824_371.24m;
  long populationCount = 7_800_000_000L;
  int maxRecords = 1_000_000;
  double scientificValue = 299_792_458.0;

  // Also correct - Group by thousands for currency and general numbers
  decimal price = 12_345.67m;
  int year = 2_024;

  // Incorrect - Hard to read large numbers
  decimal accountBalance = 5824371.24m;
  long populationCount = 7800000000L;
  int maxRecords = 1000000;
  ```

- **Separator placement**: Use separators to group digits in a way that makes sense for the number type
  - For decimal numbers: group by thousands (every 3 digits)
  - For binary literals: group by bytes (every 8 or 4 digits)
  - For hexadecimal literals: group by bytes (every 2 or 4 digits)
