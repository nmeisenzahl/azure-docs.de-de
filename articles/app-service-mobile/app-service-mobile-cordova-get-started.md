---
title: Erstellen einer Cordova-App
description: Befolgen Sie dieses Tutorial für die ersten Schritte bei der Verwendung mobiler Azure-App-Back-Ends für die Apache Cordova-Entwicklung.
keywords: cordova,javascript,mobile,client
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: conceptual
ms.date: 06/25/2019
ms.openlocfilehash: 99fb4a4b07ecbd4a85abbc62ec52a0f5960654c5
ms.sourcegitcommit: 6ee876c800da7a14464d276cd726a49b504c45c5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/19/2020
ms.locfileid: "77461571"
---
# <a name="create-an-apache-cordova-app"></a>Erstellen einer Apache Cordova-App
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Übersicht
Dieses Tutorial zeigt Ihnen, wie Sie einen cloudbasierten Back-End-Dienst mithilfe eines mobilen Azure-App-Back-Ends zu einer mobilen Apache Cordova-App hinzufügen.  Sie erstellen sowohl ein neues Mobile App-Back-End als auch eine einfache Apache Cordova-App des Typs *Aufgabenliste*, die App-Daten in Azure speichert.

Das Absolvieren dieses Tutorials ist Voraussetzung für alle anderen Apache Cordova-Tutorials zur Verwendung des Features „Mobile Apps“ von Azure App Service.

## <a name="prerequisites"></a>Voraussetzungen
Zum Durchführen dieses Tutorials benötigen Sie Folgendes:

* Einen PC mit [Visual Studio Community 2017] oder höher
* [Visual Studio-Tools für Apache Cordova].
* Ein [aktives Azure-Konto](https://azure.microsoft.com/pricing/free-trial/).

Sie können auch Visual Studio umgehen und direkt die Apache Cordova-Befehlszeile verwenden.  Die Verwendung der Befehlszeile ist hilfreich, wenn Sie das Tutorial auf einem Macintosh-Computer ausführen.  Das Kompilieren von Apache Cordova-Clientanwendungen über die Befehlszeile wird in diesem Tutorial nicht behandelt.

## <a name="create-an-azure-mobile-app-backend"></a>Erstellen eines Azure Mobile App-Back-Ends
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="create-a-database-connection-and-configure-the-client-and-server-project"></a>Erstellen einer Datenbankverbindung und Konfigurieren des Client- und Serverprojekts
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-apache-cordova-app"></a>Herunterladen und Ausführen der Apache Cordova-App
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/

[Visual Studio Community 2017]: https://www.visualstudio.com/
[Visual Studio-Tools für Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
