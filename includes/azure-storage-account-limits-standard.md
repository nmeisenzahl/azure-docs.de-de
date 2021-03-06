---
title: include file
description: include file
services: storage
author: tamram
ms.service: storage
ms.topic: include
ms.date: 02/27/2020
ms.author: tamram
ms.custom: include file
ms.openlocfilehash: e29cdd56d1c43b3d0e8fc6ca233ac19d8b0004ff
ms.sourcegitcommit: 021ccbbd42dea64d45d4129d70fff5148a1759fd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78357432"
---
In der folgenden Tabelle werden die Standardgrenzwerte für Azure-Speicherkonten vom Typ „Universell V1“ (GPv1) und „Universell V2“ (GPv2) sowie für Blobspeicherkonten, Blockblob-Speicherkonten vom Typ „Premium“ und für Speicherkonten mit Data Lake Gen2 erläutert. Der Grenzwert für *eingehend* bezieht sich auf alle Daten, die an ein Speicherkonto gesendet werden. Der Grenzwert für *ausgehend* bezieht sich auf alle Daten, die von einem Speicherkonto empfangen werden.

| Resource | Standardlimit |
| --- | --- |
| Anzahl von Speicherkonten pro Region und Abonnement, einschließlich Standard-, Premium- und Data Lake Gen2-Konten<sup>3</sup> | 250 |
| Maximale Speicherkontokapazität | 5 PiB<sup>1</sup>|
| Maximale Anzahl an Blobcontainern, Blobs, Dateifreigaben, Tabellen, Warteschlangen, Entitäten oder Meldungen pro Speicherkonto | Keine Begrenzung |
| Maximale Anforderungsrate<sup>1</sup> pro Speicherkonto | 20.000 Anforderungen pro Sekunde |
| Maximaler Eingang<sup>1</sup> pro Speicherkonto (Regionen US, Europa) | 25GBit/s |
| Maximaler Eingang<sup>1</sup> pro Speicherkonto (Regionen außerhalb von USA und Europa) | 5 GBit/s bei aktiviertem RA-GRS/GRS, 10 GBit/s für LRS/ZRS<sup>2</sup> |
| Maximaler Ausgang für universelle v2-Speicherkonten und Blobspeicherkonten (alle Regionen) | 50 GBit/s |
| Maximaler Ausgang für universelle v1-Speicherkonten (US-Regionen) | 20 GBit/s bei aktiviertem RA-GRS/GRS, 30 GBit/s für LRS/ZRS<sup>2</sup> |
| Maximaler Ausgang für universelle v1-Speicherkonten (US-fremde Regionen) | 10 GBit/s bei aktiviertem RA-GRS/GRS, 15 GBit/s für LRS/ZRS<sup>2</sup> |
| Maximale Anzahl von VNET-Regeln pro Speicherkonto | 200 |
| Maximale Anzahl von Regeln für IP-Adressen pro Speicherkonto | 200 |

<sup>1</sup> Azure Storage Standard-Konten unterstützen höhere Grenzwerte für Kapazität und Eingang auf Anforderung. Wenden Sie sich an den [Azure-Support](https://azure.microsoft.com/support/faq/), um eine Erhöhung der Kontogrenzwerte anzufordern.

<sup>2</sup> Wenn für Ihr Speicherkonto Lesezugriff mit georedundantem Speicher (RA-GRS) oder geozonenredundantem Speicher (RA-GZRS) aktiviert ist, sind die Ausgangsziele für den sekundären Standort mit denen des primären Standorts identisch. Für die [Azure Storage-Replikation](https://docs.microsoft.com/azure/storage/common/storage-redundancy) sind folgende Optionen verfügbar:

[!INCLUDE [azure-storage-redundancy](azure-storage-redundancy.md)]

<sup>3</sup> [Azure Data Lake Storage Gen2](../articles/storage/blobs/data-lake-storage-introduction.md) setzt auf Azure Blob Storage auf und bietet eine Reihe von Funktionen für die Big Data-Analyse. Einschränkungen für Azure Storage und Blob Storage gelten für Data Lake Gen2.

> [!NOTE]
> Microsoft empfiehlt, für die meisten Szenarien Speicherkonten vom Typ „Allgemein v2“ zu verwenden. Sie können ganz einfach ein Upgrade von einem Konto vom Typ „Allgemein v1“ oder einem Blob Storage-Konto auf ein Konto vom Typ „Allgemein v2“ durchführen. Dabei treten keine Ausfallzeiten auf, und Sie müssen keine Daten kopieren. Weitere Informationen finden Sie unter [Durchführen eines Upgrades auf ein Speicherkonto vom Typ „Allgemein v2“](../articles/storage/common/storage-account-upgrade.md).

Wenn die Anforderungen Ihrer Anwendung die Skalierbarkeitsziele eines einzelnen Speicherkontos überschreiten, können Sie die Anwendung so erstellen, dass mehrere Speicherkonten verwendet werden. Sie können Ihre Datenobjekte dann basierend auf diesen Speicherkonten partitionieren. Informationen zu Volumenpreisen finden Sie unter [Preise für Azure Storage](https://azure.microsoft.com/pricing/details/storage/).

Alle Speicherkonten werden unabhängig von ihrem Erstellungszeitpunkt in einer flachen Netzwerktopologie ausgeführt. Weitere Informationen zur flachen Netzwerkarchitektur von Azure Storage sowie zur Skalierbarkeit finden Sie unter [Microsoft Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency](https://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx) (Hochverfügbarer Cloud-Speicherdienst mit starker Konsistenz). Für den Multiprotokollzugriff kann zusätzlich zum flachen Namespace ein [hierarchischer Namespace für ein Data Lake Gen2-Konto aktiviert werden](../articles/storage/blobs/data-lake-storage-namespace.md). Sowohl Speicherkonten mit flachem Namespace als auch Speicherkonten mit hierarchischem Namespace unterstützen die gleichen in diesem Artikel erläuterten Skalierbarkeits- und Leistungsziele.
