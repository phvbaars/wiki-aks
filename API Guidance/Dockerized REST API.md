## Generate a Dockerized REST API template

Below is a production-ready Dockerized REST API template for .NET (ASP.NET Core Web API).
It works out of the box with VS Code, Docker, OpenAPI, and is AKS-friendly.

```
📁 Project structure
dotnet-rest-api/
├── src/
│   └── Api/
│       ├── Controllers/
│       │   └── HealthController.cs
│       ├── Program.cs
│       ├── Api.csproj
│       └── Properties/
│           └── launchSettings.json
├── tests/
│   └── Api.Tests/
│       ├── HealthTests.cs
│       └── Api.Tests.csproj
├── Dockerfile
├── docker-compose.yml
├── .dockerignore
└── README.md
```

🚀 Create the project (CLI)

```
Bash:
dotnet new webapi -n Api -o src/Api
dotnet new xunit -n Api.Tests -o tests/Api.Tests
```

🧠 Application code
Program.cs

```
csharp:
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

app.UseSwagger();
app.UseSwaggerUI();

app.MapControllers();

app.MapGet("/", () => Results.Ok(new
{
    service = "dotnet-rest-api",
    status = "running"
}));

app.Run();
```

Controllers/HealthController.cs

```
using Microsoft.AspNetCore.Mvc;

namespace Api.Controllers;

[ApiController]
[Route("api/health")]
public class HealthController : ControllerBase
{
    [HttpGet]
    public IActionResult Get()
    {
        return Ok(new
        {
            status = "ok",
            service = "dotnet-rest-api"
        });
    }
}
```

🧪 Test example
tests/Api.Tests/HealthTests.cs

```
using System.Net;
using Microsoft.AspNetCore.Mvc.Testing;
using Xunit;

public class HealthTests : IClassFixture<WebApplicationFactory<Program>>
{
    private readonly HttpClient _client;

    public HealthTests(WebApplicationFactory<Program> factory)
    {
        _client = factory.CreateClient();
    }

    [Fact]
    public async Task Health_ReturnsOk()
    {
        var response = await _client.GetAsync("/api/health");

        Assert.Equal(HttpStatusCode.OK, response.StatusCode);
    }
}
```

📦 Project file
Api.csproj
```
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>net8.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
  </PropertyGroup>

</Project>
```

🐳 Docker (multi-stage, production-ready)

Dockerfile
```
# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY src/Api/*.csproj ./Api/
RUN dotnet restore ./Api/Api.csproj
COPY src ./Api
WORKDIR /src/Api
RUN dotnet publish -c Release -o /app/publish

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
EXPOSE 8080
ENV ASPNETCORE_URLS=http://+:8080
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "Api.dll"]
```

docker-compose.yml
```
version: "3.9"

services:
  api:
    build: .
    ports:
      - "8080:8080"
    environment:
      - ASPNETCORE_ENVIRONMENT=Development
```

.dockerignore
```
bin/
obj/
.git/
.vscode/
.env
```

📘 README.md
```
# Dockerized .NET REST API

## Run locally
```bash
docker compose up --build
```

Endpoints
- GET /
- GET /api/health

OpenAPI
- Swagger UI: http://localhost:8080/swagger
- OpenAPI JSON: http://localhost:8080/swagger/v1/swagger.json

```
---

## ✅ What this template gives you

✔ ASP.NET Core Web API  
✔ OpenAPI / Swagger  
✔ Health endpoint (AKS-ready)  
✔ Multi-stage Docker build  
✔ VS Code friendly  
✔ Test project scaffold  

---

## ☁️ AKS / Azure-ready improvements (optional)

If deploying to **AKS**, consider adding:
- `/healthz` & `/readyz` endpoints
- Kubernetes probes
- Non-root Docker user
- Application Insights
- Helm or Kustomize manifests

---

## Suggested `agent.md` rules for this repo

```md
- Follow ASP.NET Core best practices
- Prefer minimal APIs and controllers
- Keep APIs stateless and container-friendly
- Ensure OpenAPI documentation stays updated
- Validate changes by running tests
```

If you want, I can:
- Convert this to Minimal APIs only
- Add OpenAPI-first generation
- Add AKS manifests
- Add Azure Container Registry + CI/CD

