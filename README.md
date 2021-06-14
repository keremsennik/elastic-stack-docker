# Elastic Stack on Docker

Elastic Stack: Elasticsearch, Kibana, Beats & APM on Docker.

Environment variables:

* `ELK_VERSION=7.13.1`

## APM

### Install APM .Net Agent

[ref]: https://www.elastic.co/guide/en/apm/agent/dotnet/current/index.html
[Quick start guide]: https://www.elastic.co/guide/en/apm/get-started/current/install-and-run.html

**Download the APM agent**

Add the agent packages from [NuGet](https://www.nuget.org/packages?q=Elastic.apm) to your .NET application. There are multiple NuGet packages available for different use cases.

For an ASP.NET Core application with Entity Framework Core, download the [Elastic.Apm.NetCoreAll](https://www.nuget.org/packages/Elastic.Apm.NetCoreAll) package. This package will automatically add every agent component to your application.

**Add the agent to the application**

For an ASP.NET Core application with the `Elastic.Apm.NetCoreAll` package, call the `UseAllElasticApm` method in the `Configure` method within the `Startup.cs` file:

```c#
public class Startup
{
  public void Configure(IApplicationBuilder app, IHostingEnvironment env)
  {
    app.UseAllElasticApm(Configuration);
    //…rest of the method
  }
  //…rest of the class
}
```

Passing an `IConfiguration` instance is optional and by doing so, the agent will read config settings through this `IConfiguration` instance, for example, from the `appsettings.json` file:

```json
{
    "ElasticApm": {
    "SecretToken": "",
    "ServerUrls": "http://localhost:8200",
    "ServiceName" : "MyApp",
  }
}
```

- **Service name**: Service names are used to differentiate data from each of your services. Elastic APM includes the service name field on every document that it saves in Elasticsearch. If you change the service name after using Elastic APM, you will see the old service name and the new service name as two separate services. Make sure you choose a good service name before you get started.

  The service name can only contain alphanumeric characters, spaces, underscores, and dashes (must match `^[a-zA-Z0-9 _-]+$`).

- **ServerUrls**: The host and port that APM Server listens for events on.

- **SecretToken**: Authentication method for Agent/Server communication. See [secure communication with APM Agents](https://www.elastic.co/guide/en/apm/server/7.13/secure-communication-agents.html) to learn more.

## Beats

### Filebeat

For harvesting Nginx access and error logs.

Used modules:

* [nginx]: https://www.elastic.co/guide/en/beats/filebeat/7.13/filebeat-module-nginx.html

### Heartbeat

For checking service uptime stats:

* Elasticsearch
* Kibana
* APM
* Nginx

Used monitor types:

- [tcp]: https://www.elastic.co/guide/en/beats/heartbeat/current/monitor-tcp-options.html

### Metricbeat

For collecting system and service metrics:

* Host system
* Docker
* Nginx

Used modules:

* [system]: https://www.elastic.co/guide/en/beats/metricbeat/7.13/metricbeat-module-system.html
* [docker]: https://www.elastic.co/guide/en/beats/metricbeat/7.13/metricbeat-module-docker.html
* [nginx]: https://www.elastic.co/guide/en/beats/metricbeat/7.13/metricbeat-module-nginx.html

