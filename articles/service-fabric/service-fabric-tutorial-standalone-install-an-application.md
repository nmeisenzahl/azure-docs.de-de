---
title: Installieren einer App in einem eigenständigen Cluster
description: In diesem Tutorial erfahren Sie, wie Sie in Ihrem eigenständigen Service Fabric-Cluster eine Anwendung installieren.
author: dkkapur
ms.topic: tutorial
ms.date: 07/22/2019
ms.author: dekapur
ms.custom: mvc
ms.openlocfilehash: 124fc6035c1d0ad504a34b7db227f0f4675f24f7
ms.sourcegitcommit: 003e73f8eea1e3e9df248d55c65348779c79b1d6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2020
ms.locfileid: "75613957"
---
# <a name="tutorial-deploy-an-application-on-your-service-fabric-standalone-cluster"></a>Tutorial: Bereitstellen einer Anwendung in Ihrem eigenständigen Service Fabric-Cluster

Mit eigenständigen Service Fabric-Clustern können Sie Ihre eigene Umgebung wählen und einen Cluster im Rahmen des Service Fabric-Konzepts „Jedes Betriebssystem, jede Cloud“ erstellen. In dieser Tutorialreihe erstellen Sie einen eigenständigen, in AWS gehosteten Cluster und stellen darin eine Anwendung bereit.

Dieses Tutorial ist der dritte Teil einer Reihe.  Mit eigenständigen Service Fabric-Clustern können Sie Ihre eigene Umgebung wählen und einen Cluster im Rahmen unseres Konzepts „Jedes Betriebssystem, jede Cloud“ mit Service Fabric erstellen. In diesem Tutorial erfahren Sie, wie Sie die erforderliche AWS-Infrastruktur zum Hosten dieses eigenständigen Clusters erstellen.

Im dritten Teil der Serie lernen Sie Folgendes:

> [!div class="checklist"]
> * Herunterladen der Beispiel-App
> * Bereitstellen im Cluster

## <a name="prerequisites"></a>Voraussetzungen

Bevor Sie mit diesem Tutorial beginnen können, müssen Sie Folgendes tun:

* [Installieren Sie Visual Studio 2019](https://www.visualstudio.com/) und die Workloads **Azure-Entwicklung** und **ASP.NET und Webentwicklung**.
* [Installieren Sie das Service Fabric SDK](service-fabric-get-started.md).

## <a name="download-the-voting-sample-application"></a>Herunterladen der Beispielanwendung „Voting“

Führen Sie in einem Befehlsfenster den folgenden Befehl aus, um das Beispiel-App-Repository auf Ihren lokalen Computer zu klonen.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

### <a name="deploy-the-app-to-the-service-fabric-cluster"></a>Bereitstellen der App im Service Fabric-Cluster

Die heruntergeladene Anwendung kann direkt über Visual Studio in einem Cluster bereitgestellt werden.

1. Öffnen Sie Visual Studio.

2. Klicken Sie auf **Datei** > **Öffnen**.

3. Navigieren Sie zu dem Ordner mit dem geklonten Git-Repository, und klicken Sie auf „Voting.sln“.

4. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Anwendungsprojekt `Voting`, und klicken Sie anschließend auf **Veröffentlichen**.

5. Klicken Sie auf das Dropdownmenü für den **Verbindungsendpunkt**, und geben Sie den öffentlichen DNS-Namen eines der Knoten in Ihrem Cluster ein.  Beispiel: `ec2-34-215-183-77.us-west-2.compute.amazonaws.com:19000`. Beachten Sie, dass in Azure ein voll qualifizierter Domänenname (Fully Qualified Domain Name, FQDN) nicht automatisch vergeben wird, aber einfach [auf der VM-Übersichtsseite eingerichtet werden kann](https://docs.microsoft.com/azure/virtual-machines/linux/portal-create-fqdn).

6. Öffnen Sie Ihren bevorzugten Browser, und geben Sie die Clusteradresse ein (also den Verbindungsendpunkt, den diese App am Port 8080 bereitstellt; Beispiel: ec2-34-215-183-77.us-west-2.compute.amazonaws.com:8080).

    ![API-Antwort aus dem Cluster](./media/service-fabric-tutorial-standalone-cluster/deployed-app.png)

## <a name="next-steps"></a>Nächste Schritte

Im dritten Teil der Reihe haben Sie gelernt, wie Sie in Ihrem Cluster eine Anwendung bereitstellen:

> [!div class="checklist"]
> * Herunterladen der Beispiel-App
> * Bereitstellen im Cluster

Im vierten Teil der Reihe erfahren Sie, wie Sie Ihren Cluster bereinigen.

> [!div class="nextstepaction"]
> [Bereinigen Ihres eigenständigen Clusters](service-fabric-tutorial-standalone-clean-up.md)