---
title: 'Tutorial: Skalieren eines Azure Red Hat OpenShift-Clusters'
description: Erfahren Sie, wie Sie einen Microsoft Azure Red Hat OpenShift-Cluster mithilfe der Azure-Befehlszeilenschnittstelle skalieren
author: jimzim
ms.author: jzim
ms.topic: tutorial
ms.service: container-service
ms.date: 05/06/2019
ms.openlocfilehash: bf9172f0c84834c951446520ff0bfcc3ef756c9c
ms.sourcegitcommit: 5397b08426da7f05d8aa2e5f465b71b97a75550b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2020
ms.locfileid: "76278307"
---
# <a name="tutorial-scale-an-azure-red-hat-openshift-cluster"></a>Tutorial: Skalieren eines Azure Red Hat OpenShift-Clusters

Dieses Tutorial ist der zweite Teil einer Reihe. Sie erfahren, wie Sie einen Microsoft Azure Red Hat OpenShift-Cluster mithilfe der Azure-Befehlszeilenschnittstelle erstellen, skalieren und anschließend löschen, um die Ressourcen zu bereinigen.

Im zweiten Teil der Reihe lernen Sie Folgendes:

> [!div class="checklist"]
> * Skalieren eines Red Hat OpenShift-Clusters

In dieser Tutorialserie lernen Sie Folgendes:
> [!div class="checklist"]
> * [Erstellen eines Azure Red Hat OpenShift-Clusters](tutorial-create-cluster.md)
> * Skalieren eines Azure Red Hat OpenShift-Clusters
> * [Löschen eines Azure Red Hat OpenShift-Clusters](tutorial-delete-cluster.md)

## <a name="prerequisites"></a>Voraussetzungen

Bevor Sie mit diesem Tutorial beginnen können, müssen Sie Folgendes tun:

* Erstellen Sie einen Cluster, indem Sie das Tutorial [Erstellen eines Azure Red Hat OpenShift-Clusters](tutorial-create-cluster.md) ausführen.

## <a name="step-1-sign-in-to-azure"></a>Schritt 1: Anmelden bei Azure

Wenn Sie die Azure CLI lokal ausführen, führen Sie `az login` aus, um sich bei Azure anzumelden.

```bash
az login
```

Wenn Sie Zugriff auf mehrere Abonnements haben, führen Sie `az account set -s {subscription ID}` aus, und ersetzen Sie `{subscription ID}` durch das zu verwendende Abonnement.

## <a name="step-2-scale-the-cluster-with-additional-nodes"></a>Schritt 2: Skalieren des Clusters mit zusätzlichen Knoten

Legen Sie in einem Bash-Terminal die Variable CLUSTER_NAME auf den Namen Ihres Clusters fest:

```bash
CLUSTER_NAME=yourclustername
```

Skalieren wir jetzt den Cluster mithilfe der Azure-Befehlszeilenschnittstelle auf fünf Knoten:

```bash
az openshift scale --resource-group $CLUSTER_NAME --name $CLUSTER_NAME --compute-count 5
```

Nach einigen Minuten wird `az openshift scale` erfolgreich abgeschlossen und gibt ein JSON-Dokument zurück, das die Details des skalierten Clusters enthält.

## <a name="next-steps"></a>Nächste Schritte

In diesem Teil des Tutorials haben Sie Folgendes gelernt:

> [!div class="checklist"]
> * Skalieren eines Azure Red Hat OpenShift-Clusters

Fahren Sie mit dem nächsten Tutorial fort:
> [!div class="nextstepaction"]
> [Löschen eines Azure Red Hat OpenShift-Clusters](tutorial-delete-cluster.md)
