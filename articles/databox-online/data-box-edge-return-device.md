---
title: Zurückgeben oder Ersetzen Ihres Azure Data Box Edge-Geräts | Microsoft-Dokumentation
description: Informationen zum Zurückgeben oder Ersetzen eines Azure Data Box Edge-Geräts
services: databox
author: alkohli
ms.service: databox
ms.subservice: edge
ms.topic: article
ms.date: 02/26/2020
ms.author: alkohli
ms.openlocfilehash: 521277b2eed7edfba016f6a80e8f877decfb0ac5
ms.sourcegitcommit: 96dc60c7eb4f210cacc78de88c9527f302f141a9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2020
ms.locfileid: "77651099"
---
# <a name="return-or-replace-your-azure-data-box-edge-device"></a>Zurückgeben oder Ersetzen Ihres Azure Data Box Edge-Geräts

In diesem Artikel wird beschrieben, wie Sie die Daten löschen und Ihr Azure Data Box Edge-Gerät zurückgeben. Nachdem Sie das Gerät zurückgegeben haben, können Sie auch die mit dem Gerät verknüpfte Ressource löschen oder ein Ersatzgerät anfordern.

In diesem Artikel werden folgende Vorgehensweisen behandelt:

> [!div class="checklist"]
> * Löschen der Daten von den Datenträgern des Geräts
> * Öffnen eines Supporttickets zur Rückgabe Ihres Geräts
> * Packen des Geräts und Planen einer Abholung
> * Löschen der Ressourcen im Azure-Portal
> * Anfordern eines Ersatzgeräts

## <a name="erase-data-from-the-device"></a>Löschen der Daten vom Gerät

Um die Daten von den Datenträgern Ihres Geräts zu löschen, müssen Sie Ihr Gerät zurücksetzen. Sie können Ihr Gerät über die lokale Webbenutzeroberfläche oder die PowerShell-Benutzeroberfläche zurücksetzen.

Erstellen Sie bei Bedarf vor dem Zurücksetzen eine Kopie der lokalen Daten auf dem Gerät. Sie können die Daten vom Gerät in einen Azure Storage-Container kopieren.

Führen Sie zum Zurücksetzen Ihres Geräts über die lokale Webbenutzeroberfläche die folgenden Schritte aus.

1. Wechseln Sie auf der lokalen Webbenutzeroberfläche zu **Wartung > Geräterücksetzung**.
2. Wählen Sie **Gerät zurücksetzen** aus.

    ![Zurücksetzen des Geräts](media/data-box-edge-return-device/device-reset-1.png)

3. Wenn Sie zur Bestätigung aufgefordert werden, überprüfen Sie den Warnhinweis, und wählen Sie **Ja** aus, um fortzufahren.

    ![Bestätigen des Zurücksetzens](media/data-box-edge-return-device/device-reset-2.png)  

Beim Zurücksetzen werden die Daten von den Datenträgern des Geräts gelöscht. Abhängig von der Menge der auf Ihrem Gerät gespeicherten Daten dauert dieser Vorgang ca. 30 bis 40 Minuten.

Alternativ können Sie eine Verbindung mit der PowerShell-Schnittstelle des Geräts herstellen und die Daten mit dem `Reset-HcsAppliance`-Cmdlet von den Datenträgern löschen. Weitere Informationen finden Sie unter [Zurücksetzen Ihres Geräts](data-box-edge-connect-powershell-interface.md#reset-your-device).

> [!NOTE]
> - Bei einem Geräteaustausch oder Upgrade auf ein neues Gerät sollten Sie Ihr Gerät erst zurücksetzen, nachdem Sie das neue Gerät erhalten haben.
> - Beim Zurücksetzen werden nur alle lokalen Daten vom Gerät gelöscht. Die Daten in der Cloud werden nicht gelöscht, und für sie fallen [Kosten](https://azure.microsoft.com/pricing/details/storage/) an. Diese Daten müssen mithilfe eines Cloudspeicher-Verwaltungstools wie [Azure Storage-Explorer](https://azure.microsoft.com/features/storage-explorer/) separat gelöscht werden.

## <a name="open-a-support-ticket"></a>Öffnen eines Supporttickets

Beginnen Sie den Rückgabeprozess mit den folgenden Schritten.

1. Öffnen Sie ein Supportticket beim Microsoft-Support, um anzugeben, dass Sie das Gerät zurückgeben möchten. Wählen Sie als Problemtyp **Data Box Edge-Hardware** aus.

    ![Öffnen eines Supporttickets](media/data-box-edge-return-device/open-support-ticket-1.png)  

2. Sie werden durch einen Microsoft-Supporttechniker kontaktiert. Halten Sie die Versanddetails bereit.
3. Wenn Sie einen Karton für die Rückgabe benötigen, können Sie ihn anfordern. Antworten Sie mit **Ja** auf die Frage **Benötigen Sie einen leeren Karton für die Rückgabe?** .


## <a name="schedule-a-pickup"></a>Planen der Abholung

1. Fahren Sie das Gerät herunter. Wechseln Sie auf der lokalen Webbenutzeroberfläche zu **Wartung > Power settings** (Energieeinstellungen).
2. Wählen Sie **Herunterfahren** aus. Wenn Sie zur Bestätigung aufgefordert werden, klicken Sie auf **Ja**, um fortzufahren. Weitere Informationen finden Sie unter [Verwalten der Energieeinstellungen](data-box-gateway-manage-access-power-connectivity-mode.md#manage-power).
3. Trennen Sie die Netzkabel, und entfernen Sie alle Netzwerkkabel vom Gerät.
4. Bereiten Sie das Versandpaket vor, indem Sie Ihren eigenen Karton verwenden oder den leeren, den Sie von Azure erhalten haben. Bringen Sie das Gerät und die mitgelieferten Netzkabel im Karton unter.
5. Bringen Sie das Adressetikett, das Sie von Azure erhalten haben, auf dem Paket an.
6. Planen Sie eine Abholung mit Ihrem regionalen Paketdienst. Bei Rückgabe des Geräts in den USA ist dies UPS oder FedEx. So planen Sie eine Abholung durch UPS

    1. Rufen Sie Ihre lokale UPS-Versandstelle an (landesspezifische kostenfreie Telefonnummer).
    2. Geben Sie bei dem Telefonat die Nachverfolgungsnummer für die Rücksendung an, die Sie auf dem gedruckten Etikett finden.
    3. Wenn Sie keine Nachverfolgungsnummer angeben, fordert UPS eine Zusatzgebühr, die Sie bei der Abholung entrichten müssen.

    Wenn Sie keine Abholung planen können oder möchten, können Sie das Data Box Edge-Gerät auch an der nächstgelegenen Versandstelle abgeben.

## <a name="delete-the-resource"></a>Löschen der Ressource

Nachdem das Gerät im Azure-Rechenzentrum eingegangen ist, wird das Gerät auf Beschädigungen oder Anzeichen von Manipulation untersucht.

- Wenn das Gerät intakt und in gutem Zustand eintrifft, endet die Rechnungsstellung für diese Ressource. Der Microsoft-Support wird Sie kontaktieren, um zu bestätigen, dass das Gerät zurückgegeben wurde. Anschließend können Sie die Ressource löschen, die im Azure-Portal mit dem Gerät verknüpft ist.
- Wenn das Gerät erheblich beschädigt eintrifft, fallen möglicherweise Geldbußen an. Weitere Informationen finden Sie unter [häufig gestellten Fragen zu verloren gegangenen oder beschädigten Geräten](https://azure.microsoft.com/pricing/details/databox/edge/) und [Produktbestimmungen](https://www.microsoft.com/licensing/product-licensing/products).  


Sie können das Gerät im Azure-Portal löschen:
-   Nachdem Sie die Bestellung aufgegeben haben und bevor das Gerät von Microsoft vorbereitet wird.
-   Nachdem Sie das Gerät an Microsoft zurückgegeben haben, durchläuft es die physische Kontrolle im Azure-Rechenzentrum, und der Microsoft-Support bestätigt telefonisch, dass das Gerät zurückgegeben wurde.

Wenn Sie das Gerät mit einem anderen Abonnement oder Standort aktiviert haben, verschiebt Microsoft Ihre Bestellung innerhalb eines Geschäftstags an das neue Abonnement oder den neuen Standort. Nach dem Verschieben der Bestellung können Sie diese Ressource löschen.


Löschen Sie mit folgenden Schritten das Gerät und die Ressource im Azure-Portal.

1. Navigieren Sie im Azure-Portal zu Ihrer Ressource und anschließend zu **Übersicht**. Wählen Sie in der Befehlsleiste **Löschen** aus.

    ![Auswählen von „Löschen“](media/data-box-edge-return-device/delete-resource-1.png)

2. Geben Sie auf dem Blatt **Gerät löschen** den Namen des zu löschenden Geräts ein, und wählen Sie **Löschen** aus.

    ![Bestätigen des Löschens](media/data-box-edge-return-device/delete-resource-2.png)

Sie werden nach erfolgreichem Löschen von Gerät und zugeordneter Ressource benachrichtigt.

## <a name="get-a-replacement-device"></a>Anfordern eines Ersatzgeräts

Es wird ein Ersatzgerät benötigt, wenn das vorhandene Gerät einen Hardwarefehler aufweist oder ein Upgrade erforderlich ist. Führen Sie die folgenden Schritte aus, wenn Ihr Gerät einen Hardwarefehler aufweist:

1. [Öffnen Sie ein Supportticket für ein Hardwareproblem.](#open-a-support-ticket) Der Microsoft-Support prüft dann, ob ein Ersatzteil für die betreffende Instanz verfügbar oder ein Hardwareupgrade nötig ist. In beiden Fällen bestellt der Support ein Ersatzgerät.
2. [Erstellen Sie eine neue Ressource](data-box-edge-deploy-prep.md#create-a-new-resource) für das Ersatzgerät. Achten Sie dabei darauf, das Kontrollkästchen für die Option **Ich habe ein Data Box Edge-Gerät** zu aktivieren. 
3. Sobald Sie das Ersatzgerät erhalten haben, sollten Sie es für die neue Ressource [installieren](data-box-edge-deploy-install.md) und [aktivieren](data-box-edge-deploy-connect-setup-activate.md).
4. Gehen Sie wie folgt vor, um das Originalgerät zurückzugeben:
    1. Öffnen Sie ein weiteres Ticket, um das Originalgerät zurückzugeben.
    2. [Löschen Sie alle Daten von dem Gerät.](#erase-data-from-the-device)
    3. [Planen Sie die Abholung.](#schedule-a-pickup)
    5. [Löschen Sie die Ressource](#delete-the-resource), die dem zurückgegebenen Gerät zugeordnet ist.



## <a name="next-steps"></a>Nächste Schritte

- Erfahren Sie, wie Sie [Bandbreite verwalten](data-box-edge-manage-bandwidth-schedules.md).
