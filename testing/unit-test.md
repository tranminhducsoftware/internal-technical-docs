# 🧩 Unit Test Guidelines

## Scope
- Business logic trong Application & Domain layer.
- CQRS handlers (MediatR) với repository/service mock.
- Orleans Grain methods (dùng TestCluster khi không cần external I/O).

## Tools
- Framework: **xUnit**  
- Assertions: **FluentAssertions**  
- Mocking: **Moq**  

## Conventions
- Tên file: `{ClassName}Tests.cs`
- Tên method: `MethodName_Should_ExpectedBehavior`

Ví dụ:
```csharp
[Fact]
public async Task PlaceOrder_Should_Create_Order_When_Valid()
{
    var handler = new PlaceOrderHandler(mockRepo.Object);
    var result = await handler.Handle(new PlaceOrderCommand(...));
    result.Should().NotBeNull();
}
