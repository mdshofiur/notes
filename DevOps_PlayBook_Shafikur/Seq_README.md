# Logging in .NET 8 with Serilog and Seq

## Setting up Docker Compose

```yaml
version: '3.8'

services:
  seq:
    image: datalust/seq:latest
    ports:
      - '80:80'
      - '5341:5341'
    environment:
      ACCEPT_EULA: Y
      $HOST_PATH_TO_SEQ: /data
```

## Installing and Configuring Serilog

* Install Serilog Packages

```
dotnet add package Serilog
dotnet add package Serilog.Sinks.Console
dotnet add package Serilog.Sinks.File
dotnet add package Serilog.AspNetCore
dotnet add package Serilog.Sinks.Seq
```

## Configuring Serilog in Program.cs

```
using Serilog;
using Serilog.Core;

Log.Logger = new LoggerConfiguration()
    .WriteTo.Console()
    .CreateLogger();
try
{
    Log.Information("Starting server.");

    var builder = WebApplication.CreateBuilder(args);
    
    builder.Host.UseSerilog((context, loggerConfiguration) =>
    {
        loggerConfiguration.WriteTo.Console();
        loggerConfiguration.ReadFrom.Configuration(context.Configuration);
    });

    builder.Services.AddEndpointsApiExplorer();
    builder.Services.AddSwaggerGen();
    builder.Services.AddHttpClient();
  

    var app = builder.Build();
    
    // if (app.Environment.IsDevelopment())
    // {
    //     app.UseSwagger();
    //     app.UseSwaggerUI();
    // }

    app.UseHttpsRedirection();
    app.UseSerilogRequestLogging();

    app.Run();
}
catch (Exception ex)
{
    Log.Fatal(ex, "Server terminated unexpectedly");
}
finally
{
    Log.CloseAndFlush();
}
```

## Appsettings.json Configuration

```
{
   "Serilog": {
      "MinimumLevel": {
         "Default": "Information",
         "Override": {
            "Microsoft": "Warning",
            "Microsoft.AspNetCore.Hosting.Diagnostics": "Error",
            "Microsoft.Hosting.Lifetime": "Information"
         }
      },
      "WriteTo": [
         {
            "Name": "Seq",
            "Args": {
               "serverUrl": "http://localhost:5341",
               "path": "D:\\Logs\\log.txt",
               "rollingInterval": "Day",
               "formatter": "Serilog.Formatting.Compact.CompactJsonFormatter, Serilog.Formatting.Compact",
               "Enrich": ["FromLogContext", "WithMachineName", "WithThreadId"]
            }
         }
      ]
   },
   "AllowedHosts": "*"
}
```


