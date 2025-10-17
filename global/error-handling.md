## Error handling best practices

- **User-Friendly Messages**: Provide clear, actionable error messages to users without exposing technical details or security information
- **Fail Fast and Explicitly**: Validate input and check preconditions early; fail with clear error messages rather than allowing invalid state
- **Specific Exception Types**: Use specific exception/error types rather than generic ones to enable targeted handling
- **Centralized Error Handling**: Handle errors at appropriate boundaries (controllers, API layers) rather than scattering try-catch blocks everywhere
- **Graceful Degradation**: Design systems to degrade gracefully when non-critical services fail rather than breaking entirely
- **Retry Strategies**: Implement exponential backoff for transient failures in external service calls
- **Clean Up Resources**: Always clean up resources (file handles, connections) in finally blocks or equivalent mechanisms

### .NET Aspire Resilience Patterns

- **Aspire resilience integration**: Use Aspire's built-in resilience support via ServiceDefaults rather than manually configuring Polly
- **HTTP resilience**: Apply standard retry, timeout, and circuit breaker policies to HttpClient instances registered through Aspire
- **Connection resilience**: Leverage Aspire component packages (e.g., `Aspire.Microsoft.EntityFrameworkCore.SqlServer`) which include built-in connection retry logic
- **Telemetry for failures**: Rely on Aspire's OpenTelemetry integration to automatically capture and trace failures, retries, and circuit breaker state
- **Health check integration**: Use Aspire health checks to detect unhealthy dependencies early and route traffic accordingly
- **Timeout policies**: Configure appropriate timeouts for HTTP clients and database connections through Aspire's configuration rather than hardcoding values
