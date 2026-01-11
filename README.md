# Cirreum.Runtime.Persistence.SqlServer

[![NuGet Version](https://img.shields.io/nuget/v/Cirreum.Runtime.Persistence.SqlServer.svg?style=flat-square&labelColor=1F1F1F&color=003D8F)](https://www.nuget.org/packages/Cirreum.Runtime.Persistence.SqlServer/)
[![NuGet Downloads](https://img.shields.io/nuget/dt/Cirreum.Runtime.Persistence.SqlServer.svg?style=flat-square&labelColor=1F1F1F&color=003D8F)](https://www.nuget.org/packages/Cirreum.Runtime.Persistence.SqlServer/)
[![GitHub Release](https://img.shields.io/github/v/release/cirreum/Cirreum.Runtime.Persistence.SqlServer?style=flat-square&labelColor=1F1F1F&color=FF3B2E)](https://github.com/cirreum/Cirreum.Runtime.Persistence.SqlServer/releases)
[![License](https://img.shields.io/github/license/cirreum/Cirreum.Runtime.Persistence.SqlServer?style=flat-square&labelColor=1F1F1F&color=F2F2F2)](https://github.com/cirreum/Cirreum.Runtime.Persistence.SqlServer/blob/main/LICENSE)
[![.NET](https://img.shields.io/badge/.NET-10.0-003D8F?style=flat-square&labelColor=1F1F1F)](https://dotnet.microsoft.com/)

**Simplified `Cirreum.Persistence.SqlServer` configuration for Cirreum runtime applications**

## Overview

**Cirreum.Runtime.Persistence.SqlServer** provides a unified persistence layer configuration for the Cirreum framework. It simplifies database integration by offering a single extension method that automatically registers and configures multiple persistence providers with built-in health checks.

## Installation

```bash
dotnet add package Cirreum.Runtime.Persistence.SqlServer
```

## Usage

Add persistence to your application with a single line:

```csharp
var builder = WebApplication.CreateBuilder(args);

// Add persistence support
builder.AddPersistence();

var app = builder.Build();
```

This automatically:
- Registers SqlServer persistence services
- Configures health checks for database connectivity
- Prevents duplicate service registration
- Integrates with the Cirreum service provider infrastructure

## Supported Providers

| Provider | Package | Database |
|----------|---------|----------|
| SqlServer | `Cirreum.Persistence.SqlServer` | MS SqlServer |

## Features

- **Simple Integration**: One method to configure all persistence needs
- **Health Checks**: Automatic health check registration for monitoring
- **Duplicate Prevention**: Smart registration prevents service conflicts
- **Extensible Design**: Built on the Cirreum service provider pattern for easy extension

## Configuration

Configure persistence providers in `appsettings.json`:

```json
{
  "ServiceProviders": {
	"Persistence": {
	  "SqlServer": {
		"default": {
		  "Name": "MySqlServer",
		  "UseAzureAuthentication": true,
		  "CommandTimeout": 60,
		  "EnableHealthCheck": true
		}
	  }
	}
  },
  "ConnectionStrings": {
	"MySqlServer": "Server=localhost;Database=MyDb;Trusted_Connection=True;" // prefer Azure Key Vault for production
  }
}
```

The `Name` property resolves the connection string via `Configuration.GetConnectionString(name)`. For production, store connection strings in a Key Vault using the naming convention `ConnectionStrings--{Name}`.

For detailed configuration options, see the individual provider documentation:
- [Cirreum.Persistence.Sql](https://github.com/cirreum/Cirreum.Persistence.Sql) (abstractions)
- [Cirreum.Persistence.SqlServer](https://github.com/cirreum/Cirreum.Persistence.SqlServer) (implementation)

## Versioning

Cirreum.Runtime.Persistence follows [Semantic Versioning](https://semver.org/):

- **Major** - Breaking API changes
- **Minor** - Truly new features, backward compatible
- **Patch** - Update nuget packages, Bug fixes, backward compatible

Given its foundational role, major version bumps are rare and carefully considered.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Cirreum Foundation Framework**  
*Layered simplicity for modern .NET*