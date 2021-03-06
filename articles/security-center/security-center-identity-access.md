---
title: Überwachen von Identität und Zugriff in Azure Security Center | Microsoft-Dokumentation
description: Hier erfahren Sie, wie Sie mithilfe der Identitäts- und Zugriffsfunktion in Azure Security Center die Zugriffsaktivitäten der Benutzer sowie identitätsbezogene Probleme überwachen können.
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.assetid: 9f04e730-4cfa-4078-8eec-905a443133da
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2020
ms.author: memildin
ms.openlocfilehash: 183b81134b2fe72a539cc6460a05d828342aafbb
ms.sourcegitcommit: 20429bc76342f9d365b1ad9fb8acc390a671d61e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/11/2020
ms.locfileid: "79086494"
---
# <a name="monitor-identity-and-access"></a>Überwachen der Identität und des Zugriffs

> [!TIP]
> Ab März 2020 sind Identitäts- und Zugriffsempfehlungen von Azure Security Center in allen Abonnements des Tarifs „Free“ enthalten. Wenn Sie über Abonnements für den Free-Tarif verfügen, wird deren Sicherheitsbewertung beeinträchtigt, da sie nicht vorab im Hinblick auf ihre Identitäts- und Zugriffssicherheit bewertet wurden. 

Werden potenzielle Sicherheitslücken erkannt, erstellt Security Center Empfehlungen, die Sie beim Konfigurieren der erforderlichen Steuerelemente zum Sichern und Schützen Ihrer Ressourcen unterstützen.

Der Fokus bei der Entwicklung des Sicherheitsbereichs wurde von der Netzwerkorientierung auf die Identitätsorientierung verlagert. Bei der Sicherheit geht es immer weniger um die Verteidigung Ihres Netzwerks und immer mehr um die Verteidigung Ihrer Daten sowie um die Verwaltung der Sicherheit Ihrer Apps und Benutzer. Da heutzutage jedoch immer mehr Daten und Apps in die Cloud verlagert werden, ist die Identität zur neuen Grenze geworden.

Durch die Überwachung von Identitätsaktivitäten können Sie proaktive Maßnahmen ergreifen, bevor es zu einem Vorfall kommt, oder einen Angriffsversuch abwehren. Beispiele für Empfehlungen, die möglicherweise im Abschnitt zur Ressourcensicherheit von **Identität und Zugriff** von Azure Security Center angezeigt werden, sind:

- MFA sollte für Konten mit Besitzerberechtigungen in Ihrem Abonnement aktiviert sein.
- Maximal 3 Besitzer sollten für Ihr Abonnement festgelegt sein.
- Veraltete Konten sollten aus Ihrem Abonnement entfernt werden.
- Externe Konten mit Leseberechtigungen sollten aus Ihrem Abonnement entfernt werden

Eine vollständige Liste der Empfehlungen, die hier angezeigt werden können, finden Sie unter [Empfehlungen zu Identität und Zugriff](recommendations-reference.md#recs-identity).

> [!NOTE]
> Wenn Ihr Abonnement mehr als 600 Konten umfasst, kann das Security Center nicht die Identitätsempfehlungen für Ihr Abonnement ausführen. Empfehlungen, die nicht ausgeführt werden, werden unter „Nicht verfügbare Bewertungen“ aufgeführt.
Im Security Center können keine Identitätsempfehlungen für Administrator-Agents eines Cloud Solution Provider-Partners (CSP) ausgeführt werden.
>


Alle Empfehlungen für Identität und Zugriff sind innerhalb von zwei Sicherheitskontrollen auf der Seite **Empfehlungen** verfügbar:

- Zugriff und Berechtigungen verwalten 
- MFA aktivieren

![Die zwei Sicherheitskontrollen mit Empfehlungen für Identität und Zugriff](media/security-center-identity-access/two-security-controls-for-identity-and-access.png)


## <a name="enable-multi-factor-authentication-mfa"></a>Mehrstufige Authentifizierung (Multi-Factor Authentication, MFA) aktivieren

Zum Aktivieren von MFA sind [Berechtigungen für Azure Active Directory (AD)-Mandanten](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) erforderlich. 

- Wenn Sie über eine Premium-Edition von AD verfügen, aktivieren Sie MFA unter Verwendung des [bedingten Zugriffs](https://docs.microsoft.com/azure/active-directory/conditional-access/overview).

- Benutzer der AD Free-Edition können **Sicherheitsstandards** in Azure Active Directory aktivieren, wie in der [AD-Dokumentation](https://docs.microsoft.com/azure/active-directory/fundamentals/concept-fundamentals-security-defaults) beschrieben, aber die Security Center-Empfehlung zum Aktivieren von MFA wird weiterhin angezeigt.


## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zu Empfehlungen für andere Arten von Azure-Ressourcen finden Sie in den folgenden Artikeln:

- [Schützen von Computern und Anwendungen im Azure Security Center](security-center-virtual-machine-protection.md)
- [Schützen Ihres Netzwerks in Azure Security Center](security-center-network-recommendations.md)
- [Schützen des Azure SQL-Diensts und der Daten im Azure Security Center](security-center-sql-service-recommendations.md)