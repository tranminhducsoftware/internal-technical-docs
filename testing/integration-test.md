
---

## 3. `integration-test.md`
```markdown
```
# 🔗 Integration Test Guidelines

## Scope
- **API**: WebApplicationFactory + TestServer (in-memory HTTP).  
- **Database**: EF Core + SQL Server (Testcontainers).  
- **Orleans**: TestCluster → test grain activation, reminders, timers.  
- **RabbitMQ**: Testcontainers RabbitMQ → publish/consume thực tế.  
- **Redis**: Integration với caching, rate-limit counters.

## Tools
- xUnit
- Testcontainers-dotnet
- Microsoft.AspNetCore.Mvc.Testing (WebApplicationFactory)
- Orleans.TestingHost

## Example API Test
```csharp
[Fact]
public async Task Login_Should_Return_Token()
{
    var client = _factory.CreateClient();
    var response = await client.PostAsJsonAsync("/api/v1/auth/login", new { ... });
    response.StatusCode.Should().Be(HttpStatusCode.OK);
}
```
## Database Testing
- Apply migrations trên container SQL.
- Reset DB state sau mỗi test (Respawn hoặc transaction rollback).

## Messaging Testing
- Publish → consume trong queue.
- Assert: đúng routing key, đúng payload schema.