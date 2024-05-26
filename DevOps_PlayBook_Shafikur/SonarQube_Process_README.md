# SonarQube Integration Process

## Step 1: Run SonarQube Container

```bash
docker run -d --name sonarqube -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true -p 9000:9000 sonarqube:latest
```

## Step 2: Install SonarScanner .NET Global Tool
```
dotnet tool install --global dotnet-sonarscanner

```

## Step 3: Begin SonarScanner Analysis
```
dotnet sonarscanner begin /k:"squ_31e62ce26ff2c02d278a8071a9eab429c8ec5da3" /d:sonar.host.url="http://localhost:9000" /d:sonar.token="squ_31e62ce26ff2c02d278a8071a9eab429c8ec5da3"

```


## Step 4: Build the Project
```
dotnet build

```

## Step 5: End SonarScanner Analysis
```
dotnet sonarscanner end /d:sonar.token="squ_31e62ce26ff2c02d278a8071a9eab429c8ec5da3"

```
