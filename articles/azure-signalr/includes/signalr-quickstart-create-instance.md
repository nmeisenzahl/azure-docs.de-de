---
title: include file
description: include file
author: anthonychu
ms.service: signalr
ms.topic: include
ms.date: 09/14/2018
ms.author: antchu
ms.custom: include file
ms.openlocfilehash: 0a228f6d8b4f72acd3783f27bf192fe6bd13f988
ms.sourcegitcommit: f4f626d6e92174086c530ed9bf3ccbe058639081
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75392140"
---
## <a name="create-an-azure-signalr-service-instance"></a>Erstellen einer Instanz des Azure SignalR-Diensts

Ihre Anwendung stellt eine Verbindung mit einer Instanz des SignalR-Diensts in Azure her.

1. Klicken Sie in der linken oberen Ecke des Azure-Portals auf die Schaltfläche „Neu“. Geben Sie im Bildschirm „Neu“ die Angabe *SignalR-Dienst* in das Suchfeld ein, und drücken Sie die EINGABETASTE.

    ![Suchen nach SignalR-Dienst](../media/signalr-quickstart-azure-functions-javascript/signalr-quickstart-new.png)

1. Wählen Sie **SignalR-Dienst** aus den Suchergebnissen aus, und wählen Sie dann **Erstellen** aus.

1. Geben Sie folgende Einstellungen ein.

    | Einstellung      | Vorgeschlagener Wert  | BESCHREIBUNG                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Ressourcenname** | Global eindeutiger Name | Der Name, der die neue Instanz des SignalR -Diensts identifiziert. Gültige Zeichen sind `a-z`, `0-9` und `-`.  | 
    | **Abonnement** | Ihr Abonnement | Das Abonnement, unter dem diese neue Instanz des SignalR-Diensts erstellt wird. | 
    | **[Ressourcengruppe](../../azure-resource-manager/management/overview.md)** |  myResourceGroup | Der Name für die neue Ressourcengruppe, in der Ihre Instanz des SignalR-Diensts erstellt werden soll. | 
    | **Location** | USA (Westen) | Wählen Sie eine [Region](https://azure.microsoft.com/regions/) in Ihrer Nähe aus. |
    | **Preisstufe** | Kostenlos | Testen Sie den Azure SignalR-Dienst kostenlos. |
    | **Einheitenanzahl** |  Nicht verfügbar | Die Einheitenanzahl gibt an, wie viele Verbindungen Ihre Instanz des SignalR-Diensts akzeptieren kann. Dies kann nur im Tarif „Standard“ konfiguriert werden. |
    | **Dienstmodus** |  Serverlos | Zur Verwendung mit Azure Functions oder der REST-API. |

    ![Erstellen des SignalR-Diensts](../media/signalr-quickstart-azure-functions-javascript/signalr-quickstart-create.png)

1. Wählen Sie **Erstellen** aus, um mit der Bereitstellung der Instanz des SignalR-Diensts zu beginnen.

1. Nachdem die Instanz bereitgestellt wurde, öffnen Sie sie im Portal, und navigieren Sie zur Seite „Einstellungen“. Ändern Sie die Einstellung des Dienstmodus nur dann in *Serverlos*, wenn Sie Azure SignalR Service über eine Azure Functions-Bindung oder REST-API verwenden. Behalten Sie andernfalls die Einstellung *Klassisch* oder *Standard* bei.