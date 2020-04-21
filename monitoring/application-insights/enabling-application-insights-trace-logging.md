trace logs in Application Insights
```csharp
LogLevel logLevel = LogLevel.Warning;
var logLevelSetting = Configuration["Logging:LogLevel:Default"];
if (!string.IsNullOrWhiteSpace(logLevelSetting) && Enum.TryParse<LogLevel>(logLevelSetting, out LogLevel parsedLogLevel))
{
    logLevel = parsedLogLevel;
}
loggerFactory.AddApplicationInsights(app.ApplicationServices, logLevel);
```

to include event id 
```csharp
services
.AddOptions<ApplicationInsightsLoggerOptions>()
.Configure(o => o.IncludeEventId = true);
```