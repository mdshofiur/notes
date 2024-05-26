# Unit Test .NET Application with CI/CD

## Package Installation

Install the following packages for unit testing:

- xunit
- xunit.runner.visualstudio
- coverlet.collector
- Microsoft.NET.Test.Sdk

## Unit Test File: `Unit_test/test.cs`

Create a unit test file with the following content:

```csharp
using Xunit;

namespace MyFirstUnitTests
{
    public class UnitTest1
    {
        [Fact]
        public void PassingTest()
        {
            Assert.Equal(4, Add(2, 2));
        }

        [Fact]
        public void PassingTest2()
        {
            Assert.Equal(5, Add(2, 3));
        }

        // [Fact]
        // public void FailingTest()
        // {
        //     Assert.Equal(5, Add(2, 2));
        // }

        int Add(int x, int y)
        {
            return x + y;
        }
    }
}
```
## Run Unit Tests Locally
```
dotnet test --logger "console;verbosity=detailed"
```

## Run Unit Tests in Bitbucket CI/CD Pipeline


```
pipelines:
  branches:
    development:
      - step:
          name: Test and Deploy to Development
          deployment: development
          script:
            - dotnet test --logger "console;verbosity=detailed"
            - echo "Test Passed"
            - echo "Deploying to Development Server"
            - echo "Running Application on Development Server"

```
#### Note: This is a snippet of the CI/CD pipeline code. Ensure you include the complete pipeline configuration as required.



##### Reference: [ Click Here](https://xunit.net/docs/getting-started/netcore/cmdline)