---
title: Konfigurieren der Workloadpriorität
description: Hier erfahren Sie, wie Sie die Priorität der Anforderungsebene in Azure Synapse Analytics festlegen.
services: sql-data-warehouse
author: ronortloff
manager: craigg
ms.service: sql-data-warehouse
ms.subservice: workload-management
ms.topic: conceptual
ms.date: 02/04/2020
ms.author: rortloff
ms.reviewer: jrasnick
ms.custom: azure-synapse
ms.openlocfilehash: 8b2a4333717938edf9f3039e29e8df88cece7cc1
ms.sourcegitcommit: 225a0b8a186687154c238305607192b75f1a8163
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/29/2020
ms.locfileid: "78196796"
---
# <a name="configure-workload-importance-in-azure-synapse-analytics"></a>Konfigurieren der Workloadpriorität in Azure Synapse Analytics

Durch Festlegen der Priorität in SQL Analytics für Azure Synapse können Sie die Zeitplanung von Abfragen beeinflussen. Abfragen mit höherer Priorität werden so geplant, dass sie vor Abfragen mit niedrigerer Priorität ausgeführt werden. Um Abfragen Priorität zuzuweisen, müssen Sie einen Workloadklassifizierer erstellen.

## <a name="create-a-workload-classifier-with-importance"></a>Erstellen eines Workloadklassifizierers mit Priorität

Oft gibt es in einem Data Warehouse-Szenario Benutzer, deren Abfragen schnell ausgeführt werden müssen.  Der Benutzer könnte eine Führungskraft im Unternehmen sein, die Berichte ausführen muss, oder ein Analyst, der eine Ad-hoc-Abfrage ausführt. Sie erstellen einen Workloadklassifizierer, um einer Abfrage eine bestimmte Priorität zuzuweisen.  Bei den nachstehenden Beispielen wird die neue Syntax [CREATE WORKLOAD CLASSIFIER](/sql/t-sql/statements/create-workload-classifier-transact-sql?view=azure-sqldw-latest) verwendet, um zwei Klassifizierer zu erstellen.  „MEMBERNAME“ kann ein einzelner Benutzer oder eine Gruppe sein. Einzelbenutzerklassifizierungen haben Vorrang vor Rollenklassifizierungen. Für die Suche nach vorhandenen Data Warehouse-Benutzern führen Sie aus:

```sql
Select name from sys.sysusers
```

Zum Erstellen eines Workloadklassifizierers für einen Benutzer mit höherer Priorität führen Sie aus:

```sql
CREATE WORKLOAD CLASSIFIER ExecReportsClassifier  
    WITH (WORKLOAD_GROUP = 'xlargerc'
         ,MEMBERNAME     = 'name'  
         ,IMPORTANCE     =  above_normal);  

```

Zum Erstellen eines Workloadklassifizierers für einen Benutzer, der Ad-hoc-Abfragen mit niedrigerer Priorität ausführt, führen Sie aus:  

```sql
CREATE WORKLOAD CLASSIFIER AdhocClassifier  
    WITH (WORKLOAD_GROUP = 'xlargerc'
         ,MEMBERNAME     = 'name'  
         ,IMPORTANCE     =  below_normal);  
```

## <a name="next-steps"></a>Nächste Schritte
- Weitere Informationen zur Workloadverwaltung finden Sie unter [Workloadklassifizierung](sql-data-warehouse-workload-classification.md).
- Weitere Informationen zu Priorität finden Sie unter [Workloadpriorität](sql-data-warehouse-workload-importance.md).

> [!div class="nextstepaction"]
> [Wechseln zu „Verwalten“ und Überwachen der Workloadpriorität](sql-data-warehouse-how-to-manage-and-monitor-workload-importance.md)
