---
title: Verwaltbarkeit und Überwachung – Abfrageaktivität, Ressourcennutzung
description: Hier erfahren Sie, welche Funktionen zum Verwalten und Überwachen von Azure Synapse Analytics zur Verfügung stehen. Verwenden Sie das Azure-Portal und dynamische Verwaltungssichten (DMVs), um Informationen zu Abfrageaktivität und Ressourcennutzung für Ihre Data Warehouse-Instanz zu erhalten.
services: sql-data-warehouse
author: kevinvngo
manager: craigg-msft
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.subservice: manage
ms.date: 02/04/2020
ms.author: kevin
ms.reviewer: jrasnick
ms.custom: azure-synapse
ms.openlocfilehash: 47f142a19ac470fb29e9542941cd94a6b29ce240
ms.sourcegitcommit: 225a0b8a186687154c238305607192b75f1a8163
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/29/2020
ms.locfileid: "78195922"
---
# <a name="monitoring-resource-utilization-and-query-activity-in-azure-synapse-analytics"></a>Überwachen der Ressourcennutzung und Abfrageaktivität in Azure Synapse Analytics
Azure Synapse Analytics bietet umfassende Überwachungsfunktionen im Azure-Portal, um Erkenntnisse zu Ihrer Data Warehouse-Workload zu gewinnen. Das Azure-Portal ist das empfohlene Tool zum Überwachen Ihrer Data Warehouse-Instanz, weil es eine konfigurierbare Aufbewahrungsdauer, Warnungen, Empfehlungen und anpassbare Diagramme und Dashboards für Metriken und Protokolle bietet. Das Portal ermöglicht außerdem eine Integration weiterer Azure-Überwachungsdienste – z.B. Operations Management Suite (OMS) und Azure Monitor (Protokolle), um Ihnen eine umfassende und integrierte Überwachungsoberfläche für Data Warehouse sowie für Ihre gesamte Azure-Analyseplattform zu bieten. In dieser Dokumentation wird beschrieben, welche Überwachungsfunktionen zur Verfügung stehen, um Ihre Analyseplattform mit SQL Analytics zu optimieren und zu verwalten. 

## <a name="resource-utilization"></a>Ressourcenverwendung 
Im Azure-Portal stehen die folgenden Metriken für SQL Analytics zur Verfügung. Diese Metriken werden über [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/data-collection#metrics) angegeben.


| Metrikname             | BESCHREIBUNG                                                  | Aggregationstyp |
| ----------------------- | ------------------------------------------------------------ | ---------------- |
| CPU-Prozentsatz          | CPU-Auslastung für alle Knoten der Data Warehouse-Instanz      | Durchschnitt, Minimum, Maximum    |
| E/A-Prozentsatz für Daten      | E/A-Auslastung für alle Knoten der Data Warehouse-Instanz       | Durchschnitt, Minimum, Maximum    |
| Arbeitsspeicherprozentsatz       | Arbeitsspeicherauslastung (SQL Server) für alle Knoten der Data Warehouse-Instanz | Durchschnitt, Minimum, Maximum   |
| Aktive Abfragen          | Anzahl aktiver Abfragen, die auf dem System ausgeführt werden             | SUM              |
| Abfragen in Warteschlange          | Anzahl von Abfragen in der Warteschlange, die auf die Ausführung warten          | SUM              |
| Erfolgreiche Verbindungen  | Anzahl von erfolgreichen Datenverbindungen                 | Summe, Anzahl       |
| Verbindungsfehler      | Anzahl von Fehlern bei der Verbindungsherstellung mit Data Warehouse           | Summe, Anzahl       |
| Von der Firewall blockiert     | Anzahl von blockierten Anmeldungen bei Data Warehouse     | Summe, Anzahl       |
| DWU-Grenzwert               | Servicelevelziel für Data Warehouse                | Durchschnitt, Minimum, Maximum    |
| DWU in Prozent          | Höchstwert zwischen CPU-Prozentsatz und E/A-Prozentsatz für Daten        | Durchschnitt, Minimum, Maximum    |
| DWU-Verbrauch                | DWU-Limit × DWU-Prozentsatz                                   | Durchschnitt, Minimum, Maximum    |
| Prozentsatz der Cachetreffer    | (Cachetreffer/Cachefehler) × 100, wobei die Cachetreffer die Summe aller Columnstore-Segmenttreffer im lokalen SSD-Cache und die Cachefehler die Columnstore-Segmentfehler im lokalen SSD-Cache repräsentieren, summiert über alle Knoten | Durchschnitt, Minimum, Maximum    |
| Cacheverwendung in Prozent   | (Cacheverwendung/Cachekapazität) × 100, wobei die Cacheverwendung die Summe aller Bytes im lokalen SSD-Cache für alle Knoten darstellt und die Cachekapazität die Summe der Speicherkapazität im lokalen SSD-Cache für alle Knoten repräsentiert | Durchschnitt, Minimum, Maximum    |
| Lokaler tempdb-Prozentsatz | Lokale tempdb-Auslastung für alle Computeknoten, Werte werden alle fünf Minuten ausgegeben | Durchschnitt, Minimum, Maximum    |

Beim Anzeigen von Metriken und Festlegen von Warnungen zu berücksichtigende Aspekte:

- Fehlerhafte und erfolgreiche Verbindungen werden für ein bestimmtes Data Warehouse gemeldet – nicht für den logischen Server.
- Der Prozentsatz des Arbeitsspeichers spiegelt die Auslastung auch dann wider, wenn sich das Data Warehouse im Leerlauf befindet – er gibt nicht die Speichernutzung durch die aktive Workload wieder. Verwenden Sie diese Metrik zusammen mit anderen (tempdb, Gen2-Cache), und verfolgen Sie sie, um eine ganzheitliche Entscheidung darüber zu treffen, ob eine Skalierung auf zusätzliche Cache Kapazität die Workloadleistung entsprechend Ihren Anforderungen steigert.


## <a name="query-activity"></a>Abfrageaktivität
Für eine programmgesteuerte Benutzeroberfläche bei der Überwachung von SQL Analytics über T-SQL bietet der Dienst einen Satz an dynamischen Verwaltungssichten (Dynamic Management Views, DMVs). Diese Sichten sind nützlich für die aktive Problembehandlung und das Identifizieren von Leistungsengpässen in Ihrer Workload.

Eine Liste der von SQL Analytics bereitgestellten DMVs finden Sie in dieser [Dokumentation](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views#sql-data-warehouse-dynamic-management-views-dmvs). 

## <a name="metrics-and-diagnostics-logging"></a>Protokollierung von Metriken und Diagnosedaten
Sowohl Metriken als auch Protokolle können in Azure Monitor exportiert werden, insbesondere die Komponente [Azure Monitor-Protokolle](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview), und auf sie kann programmgesteuert über [Protokollabfragen](https://docs.microsoft.com/azure/log-analytics/log-analytics-tutorial-viewdata) zugegriffen werden. Die Protokolllatenz für SQL Analytics beträgt ca. 10 – 15 Minuten. Weitere Informationen zu den Faktoren, die sich auf die Wartezeit auswirken, finden Sie in der folgenden Dokumentation.


## <a name="next-steps"></a>Nächste Schritte
Die folgenden Anleitungen beschreiben gängige Szenarios und Anwendungsfälle bei der Überwachung und Verwalten Ihrer Data Warehouse-Instanz:

- [Überwachen Ihrer Data Warehouse-Workload mit DMVs](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-manage-monitor)
