---
title: HDP-Upgrade und Fehlen von Daten in Apache Phoenix-Sichten in Azure HDInsight
description: HDP-Upgrade bewirkt das Fehlen von Daten in Apache Phoenix-Sichten in Azure HDInsight
ms.service: hdinsight
ms.topic: troubleshooting
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.date: 08/08/2019
ms.openlocfilehash: ffec5cb4b1d36a2a2a7ca3ae7bbc40e20e075d4b
ms.sourcegitcommit: 8e9a6972196c5a752e9a0d021b715ca3b20a928f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/11/2020
ms.locfileid: "75887273"
---
# <a name="scenario-hdp-upgrade-causes-no-data-in-apache-phoenix-views-in-azure-hdinsight"></a>Szenario: HDP-Upgrade bewirkt das Fehlen von Daten in Apache Phoenix-Sichten in Azure HDInsight

In diesem Artikel werden Schritte zur Problembehandlung und mögliche Lösungen für Probleme bei der Interaktion mit Azure HDInsight-Clustern beschrieben.

## <a name="issue"></a>Problem

Eine Apache Phoenix-Sicht enthält nach dem Upgrade von HDP 2.4 auf HDP 2.5 keine Daten.

## <a name="cause"></a>Ursache

Die Indextabelle für Sichten (alle Indizes für die Sicht werden in einer einzigen physischen Apache HBase-Tabelle gespeichert) wird beim Upgrade abgeschnitten.

## <a name="resolution"></a>Lösung

Löschen Sie alle Sichten nach dem Upgrade, und erstellen Sie sie neu.

## <a name="next-steps"></a>Nächste Schritte

Wenn Ihr Problem nicht aufgeführt ist oder Sie es nicht lösen können, besuchen Sie einen der folgenden Kanäle, um weitere Unterstützung zu erhalten:

* Nutzen Sie den [Azure-Communitysupport](https://azure.microsoft.com/support/community/), um Antworten von Azure-Experten zu erhalten.

* Herstellen einer Verbindung mit [@AzureSupport](https://twitter.com/azuresupport), dem offiziellen Microsoft Azure-Konto zum Verbessern der Kundenfreundlichkeit. Verbinden der Azure-Community mit den richtigen Ressourcen: Antworten, Support und Experten.

* Sollten Sie weitere Unterstützung benötigen, senden Sie eine Supportanfrage über das [Azure-Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade/). Wählen Sie dazu auf der Menüleiste die Option **Support** aus, oder öffnen Sie den Hub **Hilfe und Support**. Ausführlichere Informationen hierzu finden Sie unter [Erstellen einer Azure-Supportanfrage](https://docs.microsoft.com/azure/azure-portal/supportability/how-to-create-azure-support-request). Zugang zu Abonnementverwaltung und Abrechnungssupport ist in Ihrem Microsoft Azure-Abonnement enthalten. Technischer Support wird über einen [Azure-Supportplan](https://azure.microsoft.com/support/plans/) bereitgestellt.
