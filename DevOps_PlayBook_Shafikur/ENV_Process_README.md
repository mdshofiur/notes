# Setup different environments (i.e.: dev, testing, staging, production)

## Configuring .NET Different Environments Build Process:

## Visit Official Documentation:
* Explore [.NET documentation](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/environments?view=aspnetcore-5.0#launchsettingsjson) for `launchSettings.json` configuration.

## Define Profiles:
* Configure profiles for different environments in `launchSettings.json`.

## Example Command: 
* Use `"dotnet run --launch-profile "development"` to specify a launch profile.

## Environment-specific Endpoints:
* Conditionally map endpoints based on environment variables.

```csharp
if(!app.Environment.IsProduction())
{
    app.MapGet("/prod", () => Results.Problem("This endpoint is only available in production.", statusCode: 500));
}

if(!app.Environment.IsStaging())
{
    app.MapGet("/stage", () => Results.Problem("This endpoint is only available in staging.", statusCode: 500));
}

if(!app.Environment.IsDevelopment())
{
    app.MapGet("/dev", () => Results.Problem("This endpoint is only available in development.", statusCode: 500));
}

* Note: Also You Can Change the building Ways As per Your Requirements.
```



## Configuring Next.js Different Environments Build Process:---

### Install env-cmd:
```
* Install env-cmd via npm as a dev dependency
```

### Define npm Scripts:

```
  "prod": "env-cmd -f .env.production next build && env-cmd -f .env.production next start",
  "staging": "env-cmd -f .env.staging next build && env-cmd -f .env.staging next start",
  "dev": "next dev",
```

### Explanation:---

```
* npm run prod: Builds and starts the Next.js application using production environment 
  settings defined in .env.production
* npm run staging: Builds and starts the application for staging environment using 
  settings from .env.staging
* npm run dev: Starts the application in development mode using settings from 
 .env.developmen
```

### Environment-specific Configuration:---

```
* Ensure that environment-specific configurations (e.g., API endpoints, database connections)
  are properly defined in corresponding .env files for each stage.
  
Note: Also you can Optimize Or Change The Scripts As per Your Requirements.
```

