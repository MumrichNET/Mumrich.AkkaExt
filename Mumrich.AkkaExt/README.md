# Mumrich.AkkaExt

## AkkaServiceBase

Example usage:

```csharp
class MyAkkaService : AkkaServiceBase, IHostedService
{
  private readonly IHostApplicationLifetime _appLifetime;

  public MyAkkaService(IServiceProvider serviceProvider) : base("my-akka-service", serviceProvider)
  {
    _appLifetime = serviceProvider.GetRequiredService<IHostApplicationLifetime>();
  }

  public Task StartAsync(CancellationToken cancellationToken)
  {
    RegisterApplicationShutdownIfAkkaSystemTerminates(_appLifetime, cancellationToken);

    return Task.CompletedTask;
  }

  public async Task StopAsync(CancellationToken cancellationToken)
  {
    await GracefullyShutdownAkkaSystemAsync();
  }
}
```
