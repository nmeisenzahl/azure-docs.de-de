---
title: Azure Application Insights – unterstützte Features von Azure Functions
description: In Application Insights unterstützte Features von Azure Functions
ms.topic: reference
author: TimothyMothra
ms.author: tilee
ms.date: 4/23/2019
ms.reviewer: mbullwin
ms.openlocfilehash: cf0c97fd65f9966bf42fa22e2c8f92263952cb7a
ms.sourcegitcommit: 747a20b40b12755faa0a69f0c373bd79349f39e3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77655649"
---
# <a name="application-insights-for-azure-functions-supported-features"></a>Unterstützte Features in Application Insights für Azure Functions

Azure Functions bietet [von Haus aus Integration](../../azure-functions/functions-monitoring.md) in Application Insights, die über die ILogger-Schnittstelle verfügbar ist. Unten folgt die Liste der aktuell unterstützten Features. Arbeiten Sie zum [Einstieg](../../azure-functions/functions-monitoring.md#enable-application-insights-integration) das Azure Functions-Handbuch durch.

Weitere Informationen zu den Functions-Runtimeversionen finden Sie [hier](../../azure-functions/functions-versions.md).

Weitere Informationen zu kompatiblen Versionen von Application Insights finden Sie unter [Abhängigkeiten](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Logging.ApplicationInsights/).

## <a name="supported-features"></a>Unterstützte Features

| Azure-Funktionen                       | V1                | V2 und V3   | 
|-----------------------------------    |---------------    |------------------ |
| | | | 
| **Automatische Sammlung von**        |                 |                   |               
| &bull;Anforderungen                     | Ja             | Ja               | 
| &bull;Ausnahmen                   | Ja             | Ja               | 
| &bull; Leistungsindikatoren         | Ja             | Ja               |
| &bull;Abhängigkeiten                   |                   |                   |               
| &nbsp;&nbsp;&nbsp;&mdash; HTTP      |                 | Ja               | 
| &nbsp;&nbsp;&nbsp;&mdash; ServiceBus|                 | Ja               | 
| &nbsp;&nbsp;&nbsp;&mdash; EventHub  |                 | Ja               | 
| &nbsp;&nbsp;&nbsp;&mdash; SQL       |                 | Ja               | 
| | | | 
| **Unterstützte Features**                |                   |                   |               
| &bull; QuickPulse/LiveMetrics       | Ja             | Ja               | 
| &nbsp;&nbsp;&nbsp;&mdash; Sicherer Steuerkanal|                 | Ja               | 
| &bull; Stichprobenentnahme                     | Ja             | Ja               | 
| &bull; Heartbeats                   |                 | Ja               | 
| | | | 
| **Korrelation**                       |                   |                   |               
| &bull; ServiceBus                     |                   | Ja               | 
| &bull; EventHub                       |                   | Ja               | 
| | | | 
| **Konfigurierbar**                      |                   |                   |           
| &bull;Vollständig konfigurierbar.<br/>Anweisungen finden Sie unter [Azure Functions](https://github.com/Microsoft/ApplicationInsights-aspnetcore/issues/759#issuecomment-426687852).<br/>Alle Optionen finden Sie unter [Asp.NET Core](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Custom-Configuration).               |                   | Ja                   | 


## <a name="performance-counters"></a>Leistungsindikatoren

Automatische Erfassung von Leistungsindikatoren kann nur für Windows-Computer verwendet werden.


## <a name="live-metrics--secure-control-channel"></a>Livemetriken und sicherer Steuerkanal

Die von Ihnen angegebenen benutzerdefinierten Filterkriterien werden an die Livemetrikkomponente des Application Insights SDK zurückgesendet. Der Filter können potenziell vertrauliche Informationen wie z.B. Kunden-IDs enthalten. Sie können den Kanal mit einem geheimen API-Schlüssel sicher machen. Anleitungen dazu finden Sie unter [Sichern des Steuerkanals](https://docs.microsoft.com/azure/azure-monitor/app/live-stream#secure-the-control-channel).

## <a name="sampling"></a>Stichproben

Azure Functions aktiviert die Stichprobenentnahme in der Konfiguration standardmäßig. Weitere Informationen finden Sie unter [Configure Sampling](https://docs.microsoft.com/azure/azure-functions/functions-monitoring#configure-sampling) (Konfigurieren der Stichprobenentnahme).

Wenn Ihr Projekt zur manuellen Nachverfolgung der Telemetrie vom Application Insights SDK abhängig ist, kann ein unerwartetes Verhalten auftreten, wenn Ihre Konfiguration der Stichprobenentnahme von der Konfiguration in Functions abweicht. 

Es wird empfohlen, die gleiche Konfiguration wie Functions zu verwenden. Bei **Functions v2** können Sie mithilfe der Abhängigkeitsinjektion in Ihrem Konstruktor die gleiche Konfiguration erzielen:

```csharp
using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.Extensibility;

public class Function1 
{

    private readonly TelemetryClient telemetryClient;

    public Function1(TelemetryConfiguration configuration)
    {
        this.telemetryClient = new TelemetryClient(configuration);
    }

    [FunctionName("Function1")]
    public async Task<IActionResult> Run(
        [HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)] HttpRequest req, ILogger logger)
    {
        this.telemetryClient.TrackTrace("C# HTTP trigger function processed a request.");
    }
}
```
