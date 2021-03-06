---
title: Erstellen von Webdienst-Endpunkten
titleSuffix: ML Studio (classic) - Azure
description: Erstellen von Webdienst-Endpunkten in Azure Machine Learning Studio (klassisch) Jeder Endpunkt im Webdienst wird unabhängig adressiert, gedrosselt und verwaltet.
services: machine-learning
ms.service: machine-learning
ms.subservice: studio
ms.topic: conceptual
author: likebupt
ms.author: keli19
ms.custom: seodec18
ms.date: 02/15/2019
ms.openlocfilehash: 96f5eb84f356089124708738f8a9e56b031c76bf
ms.sourcegitcommit: bdf31d87bddd04382effbc36e0c465235d7a2947
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2020
ms.locfileid: "77168828"
---
# <a name="create-endpoints-for-deployed-azure-machine-learning-studio-classic-web-services"></a>Erstellen von Endpunkten für bereitgestellte (klassische) Azure Machine Learning Studio-Webdienste

> [!NOTE]
> Die in diesem Thema beschriebenen Verfahren beziehen sich auf einen **klassischen** Machine Learning-Webdienst.

Nach der Bereitstellung eines Webdiensts wird ein Standardendpunkt für den Dienst erstellt. Der Standardendpunkt kann über seinen API-Schlüssel aufgerufen werden. Über das Webdienstportal können Sie zusätzliche Endpunkte mit eigenen Schlüsseln hinzufügen.
Jeder Endpunkt im Webdienst wird unabhängig adressiert, gedrosselt und verwaltet. Zu jedem Endpunkt gehören eine eindeutige URL und ein Autorisierungsschlüssel, den Sie zur Verteilung an Ihre Kunden nutzen können.

## <a name="add-endpoints-to-a-web-service"></a>Hinzufügen von Endpunkten zu einem Webdienst

Mithilfe des Azure Machine Learning-Webdienstportals können Sie einen Endpunkt zu einem Webdienst hinzufügen. Nach dem Erstellen kann der Endpunkt über synchrone APIs, Batch-APIs und Excel-Arbeitsblätter genutzt werden.

> [!NOTE]
> Wenn Sie dem Webdienst zusätzliche Endpunkte hinzugefügt haben, können Sie den Standardendpunkt nicht löschen.

1. Klicken Sie in Machine Learning Studio (klassisch) in der linken Navigationsspalte auf „Webdienste“.
2. Klicken Sie unten im Dashboard des Webdiensts auf **Manage endpoints** (Endpunkte verwalten). Das Azure Machine Learning-Webdienstportal wird mit der Seite mit den Endpunkten für den Webdienst geöffnet.
3. Klicken Sie auf **Neu**.
4. Geben Sie einen Namen und eine Beschreibung für den neuen Endpunkt ein. Endpunktnamen dürfen maximal 24 Zeichen lang sein und müssen aus Kleinbuchstaben oder Zahlen bestehen. Wählen Sie die Protokollierungsstufe aus, und legen Sie fest, ob Beispieldaten aktiviert sind. Weitere Informationen zur Protokollierung finden Sie unter [Aktivieren der Protokollierung für Machine Learning-Webdienste](web-services-logging.md).

## <a id="scaling"></a> Skalieren eines Webdiensts durch Hinzufügen zusätzlicher Endpunkte

Standardmäßig ist jeder veröffentlichte Webdienst so konfiguriert, dass er 20 Anforderungen gleichzeitig unterstützt, wobei maximal 200 Anforderungen gleichzeitig unterstützt werden können. Azure Machine Learning Studio (klassisch) optimiert die Einstellung automatisch, um die beste Leistung für Ihren Webdienst zu bieten. Der Wert aus dem Portal wird ignoriert.

Wenn Sie die API stärker als mit dem unterstützen Maximalwert von 200 gleichzeitigen Aufrufen auslasten möchten, müssen Sie mehrere Endpunkte im gleichen Webdienst erstellen. Sie können die Last dann wahllos auf alle Endpunkte verteilen.

Die Skalierung eines Webdiensts ist eine gängige Aufgabe. Gründe für die Skalierung sind eine Unterstützung von mehr als 200 gleichzeitigen Anforderungen, das Erhöhen der Verfügbarkeit mittels mehrerer Endpunkte oder das Bereitstellen getrennter Endpunkte für den Webdienst. Sie können die Skalierung erhöhen, indem Sie über das [Azure Machine Learning-Webdienstportal](https://services.azureml.net/) zusätzliche Endpunkte für den gleichen Webdienst hinzufügen.

Bedenken Sie, dass sich eine hohe Anzahl gleichzeitiger Aufrufe nachteilig auswirken kann, wenn die API nicht mit einer entsprechend hohen Rate aufgerufen wird. Es können sporadische Timeouts und/oder Spitzen in die Latenz auftreten, wenn eine für eine hohe Auslastung konfigurierte API relativ gering ausgelastet wird.

Die synchronen APIs werden in der Regel in Situationen verwendet, in denen eine niedrige Latenz erwünscht ist. Mit Latenz ist hier der Zeitraum gemeint, der von der API benötigt wird, um eine Anforderung abzuschließen, wobei keinerlei Netzwerkverzögerungen berücksichtigt werden. Angenommen, Sie haben eine API mit einer Latenz von 50 ms (Millisekunden). Um die verfügbare Kapazität mit der Drosselungsstufe High (Hoch) und einer Höchstzahl gleichzeitiger Anrufe = 20 voll nutzen zu können, müssen Sie diese API 20 * 1000 / 50 = 400 Mal pro Sekunde aufrufen. Wenn dieses Beispiel fortgesponnen wird, ermöglicht eine Höchstzahl von 200 gleichzeitigen Aufrufen 4.000 Aufrufe der API pro Sekunde, sofern die Latenz 50 ms beträgt.

## <a name="next-steps"></a>Nächste Schritte

[Nutzen eines Azure Machine Learning-Webdiensts](consume-web-services.md)
