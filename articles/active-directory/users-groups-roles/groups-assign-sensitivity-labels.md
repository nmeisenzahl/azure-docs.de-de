---
title: Zuweisen von Vertraulichkeitsbezeichnungen zu Gruppen – Azure AD | Microsoft-Dokumentation
description: Erfahren Sie, wie Mitgliedschaftsregeln erstellt werden, um Gruppen automatisch aufzufüllen. Sie finden hier außerdem eine Regelreferenz.
services: active-directory
documentationcenter: ''
author: curtand
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.subservice: users-groups-roles
ms.topic: article
ms.date: 02/24/2020
ms.author: curtand
ms.reviewer: krbain
ms.custom: it-pro
ms.collection: M365-identity-device-management
ms.openlocfilehash: 667fb39aabfec14cff01221b82a45ba8ad1d68d4
ms.sourcegitcommit: 021ccbbd42dea64d45d4129d70fff5148a1759fd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2020
ms.locfileid: "78329731"
---
# <a name="assign-sensitivity-labels-to-office-365-groups-in-azure-active-directory-preview"></a>Zuweisen von Vertraulichkeitsbezeichnungen zu Office 365-Gruppen in Azure Active Directory (Vorschau)

Azure Active Directory (Azure AD) unterstützt das Anwenden von Vertraulichkeitsbezeichnungen, die vom [Microsoft 365 Compliance Center](https://sip.protection.office.com/homepage) für Office 365-Gruppen veröffentlicht werden. Vertraulichkeitsbezeichnungen gelten für Gruppen über Dienste wie Outlook, Microsoft Teams und SharePoint hinweg. Dieses Feature ist zurzeit als öffentliche Preview verfügbar. Weitere Informationen zur Unterstützung von Office 365-Apps finden Sie unter [Office 365-Unterstützung für Vertraulichkeitsbezeichnungen](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-teams-groups-sites#support-for-the-sensitivity-labels).

> [!IMPORTANT]
> Um dieses Feature zu konfigurieren, muss mindestens eine aktive Azure Active Directory Premium P1-Lizenz in Ihrer Azure AD-Organisation vorhanden sein.

## <a name="enable-sensitivity-label-support-in-powershell"></a>Aktivieren der Unterstützung von Vertraulichkeitsbezeichnungen in PowerShell

Damit veröffentlichte Bezeichnungen auf Gruppen angewendet werden können, müssen Sie zunächst das Feature aktivieren. Diese Schritte aktivieren das Feature in Azure AD.

1. Öffnen Sie ein Windows PowerShell-Fenster auf Ihrem Computer. Sie können es ohne erhöhte Rechte öffnen.
1. Führen Sie die folgenden Befehle aus, um die Ausführung der Cmdlets vorzubereiten.

    ```PowerShell
    Import-Module AzureADPreview
    Connect-AzureAD
    ```

    Geben Sie auf der Seite **Bei Ihrem Konto anmelden** Ihr Administratorkonto und das zugehörige Kennwort ein, um eine Verbindung mit dem Dienst herzustellen, und wählen Sie **Anmelden** aus.
1. Rufen Sie die aktuellen Gruppeneinstellungen für die Azure AD-Organisation ab.

    ```PowerShell
    $Setting = Get-AzureADDirectorySetting -Id (Get-AzureADDirectorySetting | where -Property DisplayName -Value "Group.Unified" -EQ).id
    ```

    > [!NOTE]
    > Wenn für diese Azure AD-Organisation keine Gruppeneinstellungen erstellt wurden, müssen Sie zunächst die Einstellungen erstellen. Um Gruppeneinstellungen für diese Azure AD-Organisation zu erstellen, führen Sie die Schritte in [Azure Active Directory-Cmdlets zum Konfigurieren von Gruppeneinstellungen](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-settings-cmdlets) aus.

1. Zeigen Sie als nächstes die aktuellen Gruppeneinstellungen an.

    ```PowerShell
    $Setting.Values
    ```

1. Aktivieren Sie dann das folgende Feature:

    ```PowerShell
    $Setting["EnableMIPLabels"] = "True"
    ```

1. Speichern Sie dann die Änderungen, und übernehmen Sie die Einstellungen:

    ```PowerShell
    Set-AzureADDirectorySetting -Id $Setting.Id -DirectorySetting $Setting
    ```

Das ist alles. Sie haben das Feature aktiviert und können veröffentlichte Bezeichnungen auf Gruppen anwenden.

## <a name="assign-a-label-to-a-new-group-in-azure-portal"></a>Zuweisen einer Bezeichnung zu einer neuen Gruppe im Azure-Portal

1. Melden Sie sich beim [Azure AD Admin Center](https://aad.portal.azure.com) an.
1. Wählen Sie **Gruppen** und anschließend **Neue Gruppe** aus.
1. Wählen Sie auf der Seite **Neue Gruppe** die Option **Office 365** aus, füllen Sie dann die erforderlichen Informationen für die neue Gruppe aus, und wählen Sie anschließend eine Vertraulichkeitsbezeichnung aus der Liste aus.

   ![Zuweisen einer Vertraulichkeitsbezeichnung auf der Seite „Neue Gruppen“](./media/groups-assign-sensitivity-labels/new-group-page.png)

1. Speichern Sie die Änderungen, und wählen Sie **Erstellen** aus.

Ihre Gruppe wird erstellt, und die mit der ausgewählten Bezeichnung verbundenen Standort- und Gruppeneinstellungen werden automatisch durchgesetzt.

## <a name="assign-a-label-to-an-existing-group-in-azure-portal"></a>Zuweisen einer Bezeichnung zu einer vorhandenen Gruppe im Azure-Portal

1. Melden Sie sich beim [Azure AD Admin Center](https://aad.portal.azure.com) mit einem Gruppenadministratorkonto oder als Gruppenbesitzer an.
1. Wählen Sie **Gruppen** aus.
1. Wählen Sie auf der Seite **Alle Gruppen** die Gruppe aus, die Sie bezeichnen möchten.
1. Wählen Sie auf der Seite der ausgewählten Gruppe **Eigenschaften** und anschließend eine Vertraulichkeitsbezeichnung aus der Liste aus.

   ![Zuweisen einer Vertraulichkeitsbezeichnung auf der Übersichtsseite für eine Gruppe](./media/groups-assign-sensitivity-labels/assign-to-existing.png)

1. Wählen Sie **Speichern**, um Ihre Änderungen zu speichern.

## <a name="remove-a-label-from-an-existing-group-in-azure-portal"></a>Entfernen einer Bezeichnung von einer vorhandenen Gruppe im Azure-Portal

1. Melden Sie sich beim [Azure AD Admin Center](https://aad.portal.azure.com) mit einem globalen Administrator- oder Gruppenadministratorkonto oder als Gruppenbesitzer an.
1. Wählen Sie **Gruppen** aus.
1. Wählen Sie auf der Seite **Alle Gruppen** die Gruppe aus, deren Bezeichnung Sie entfernen möchten.
1. Wählen Sie auf der Seite **Gruppe** die Option **Eigenschaften** aus.
1. Wählen Sie **Entfernen**.
1. Klicken Sie zum Übernehmen der Änderungen auf **Speichern**.

## <a name="using-classic-azure-ad-classifications"></a>Verwenden klassischer Azure AD-Klassifizierungen

Nachdem Sie diese Funktion aktiviert haben, werden die „klassischen“ Klassifizierungen für Gruppen nur in vorhandenen Gruppen und Standorten angezeigt. Sie sollten sie nur dann für neue Gruppen verwenden, wenn Sie Gruppen in Apps erstellen, die keine Vertraulichkeitsbezeichnung unterstützen. Ihr Administrator kann sie bei Bedarf später in Vertraulichkeitsbezeichnungen umwandeln. Klassische Klassifizierungen sind die alten Klassifizierungen, die Sie durch Definieren von Werten für die `ClassificationList`-Einstellung in Azure AD PowerShell eingerichtet haben. Wenn dieses Feature aktiviert ist, werden diese Klassifizierungen nicht auf Gruppen angewendet.

## <a name="troubleshooting-issues"></a>Fragen zur Problembehandlung

### <a name="sensitivity-labels-are-not-available-for-assignment-on-a-group"></a>Vertraulichkeitsbezeichnungen sind nicht für die Zuweisung zu einer Gruppe verfügbar.

Die Option „Vertraulichkeitsbezeichnung“ wird nur für Gruppen angezeigt, wenn alle der folgenden Bedingungen erfüllt sind:

1. Für diesen Mandanten werden die Bezeichnungen im Microsoft 365 Compliance Center veröffentlicht.
1. Das Feature ist aktiviert, „EnableMIPLabels“ ist in PowerShell auf „True“ festgelegt.
1. Die Gruppe ist eine Office 365-Gruppe.
1. Der Mandant verfügt über eine Active Azure Active Directory Premium P1-Lizenz.
1. Der aktuell angemeldete Benutzer verfügt über ausreichende Berechtigungen, um Bezeichnungen zuzuweisen. Der Benutzer muss entweder ein globaler Administrator, ein Gruppenadministrator oder der Gruppenbesitzer sein.

Stellen Sie sicher, dass alle Bedingungen erfüllt sind, damit Sie einer Gruppe Bezeichnungen zuweisen können.

### <a name="the-label-i-want-to-assign-is-not-in-the-list"></a>Die Bezeichnung, die ich zuweisen möchte, ist nicht in der Liste enthalten.

Wenn die gesuchte Bezeichnung nicht in der Liste enthalten ist, kann dies einen der folgenden Gründe haben:

- Die Bezeichnung wird möglicherweise nicht im Microsoft 365 Compliance Center veröffentlicht. Dies könnte auch für Bezeichnungen gelten, die nicht mehr veröffentlicht werden. Weitere Informationen erhalten Sie von Ihrem Administrator.
- Die Bezeichnung kann veröffentlicht werden, ist aber für den angemeldeten Benutzer nicht verfügbar. Weitere Informationen zum Zugriff auf die Bezeichnung erhalten Sie von Ihrem Administrator.

### <a name="how-to-change-the-label-on-a-group"></a>Ändern der Bezeichnung einer Gruppe

Bezeichnungen können jederzeit mit denselben folgenden Schritten wie bei der Zuweisung eines Bezeichners zu einer bestehenden Gruppe ausgetauscht werden:

1. Melden Sie sich beim [Azure AD Admin Center](https://aad.portal.azure.com) mit einem globalen Administrator- oder Gruppenadministratorkonto oder als Gruppenbesitzer an.
1. Wählen Sie **Gruppen** aus.
1. Wählen Sie auf der Seite **Alle Gruppen** die Gruppe aus, die Sie bezeichnen möchten.
1. Wählen Sie auf der Seite der ausgewählten Gruppe **Eigenschaften** und anschließend eine neue Vertraulichkeitsbezeichnung aus der Liste aus.
1. Wählen Sie **Speichern** aus.

### <a name="group-setting-changes-to-published-labels-are-not-updated-on-the-groups"></a>Änderungen der Gruppeneinstellungen an veröffentlichten Bezeichnungen werden in den Gruppen nicht aktualisiert.

Als bewährte Methode wird nicht empfohlen, dass Sie die Gruppeneinstellungen für eine Bezeichnung ändern, nachdem die Bezeichnung auf Gruppen angewendet wurde. Wenn Sie Änderungen an den Gruppeneinstellungen vornehmen, die veröffentlichten Bezeichnungen im [Microsoft 365 Compliance Center](https://sip.protection.office.com/homepage) zugeordnet sind, werden diese Richtlinienänderungen nicht automatisch auf die betroffenen Gruppen angewendet.

Wenn Sie eine Änderung vornehmen müssen, verwenden Sie ein [Azure AD PowerShell-Skript](https://github.com/microsoftgraph/powershell-aad-samples/blob/master/ReassignSensitivityLabelToO365Groups.ps1), um Updates manuell auf die betroffenen Gruppen anzuwenden. Diese Methode stellt sicher, dass alle vorhandenen Gruppen die neue Einstellung erzwingen.

## <a name="next-steps"></a>Nächste Schritte

- [Verwenden von Vertraulichkeitsbezeichnungen mit Microsoft Teams, Office 365-Gruppen und SharePoint-Websites](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-teams-groups-sites)
- [Manuelles Aktualisieren von Gruppen nach der Änderung der Bezeichnungsrichtlinie mit einem Azure AD PowerShell-Skript](https://github.com/microsoftgraph/powershell-aad-samples/blob/master/ReassignSensitivityLabelToO365Groups.ps1)
- [Bearbeiten Ihrer Gruppeneinstellungen](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-groups-settings-azure-portal)
- [Verwalten von Gruppen mithilfe von PowerShell-Befehlen](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-settings-v2-cmdlets)
