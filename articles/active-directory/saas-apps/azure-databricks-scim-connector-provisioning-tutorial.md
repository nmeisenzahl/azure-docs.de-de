---
title: 'Tutorial: Konfigurieren von Azure Databricks SCIM Connector für die automatische Benutzerbereitstellung in Azure Active Directory | Microsoft-Dokumentation'
description: Erfahren Sie, wie Sie Benutzerkonten aus Azure AD für Azure Databricks SCIM Connector automatisch bereitstellen und die Bereitstellung wieder aufheben.
services: active-directory
documentationcenter: ''
author: Zhchia
writer: Zhchia
manager: beatrizd
ms.assetid: b16eaf27-4bd1-4509-be2c-9a4f66b6badc
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2020
ms.author: Zhchia
ms.openlocfilehash: fe1260982edc877c049716bd74f1bb3e90d33b0f
ms.sourcegitcommit: f255f869c1dc451fd71e0cab340af629a1b5fb6b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/16/2020
ms.locfileid: "77370521"
---
# <a name="tutorial-configure-azure-databricks-scim-connector-for-automatic-user-provisioning"></a>Tutorial: Konfigurieren von Azure Databricks SCIM Connector für die automatische Benutzerbereitstellung

In diesem Tutorial werden die Schritte beschrieben, die Sie sowohl in Azure Databricks SCIM Connector als auch in Azure Active Directory (Azure AD) ausführen müssen, um die automatische Benutzerbereitstellung zu konfigurieren. Bei der Konfiguration stellt Azure AD automatisch mithilfe des Azure AD-Bereitstellungsdiensts Benutzer und Gruppen für [Azure Databricks SCIM Connector](https://databricks.com/) bereit bzw. hebt deren Bereitstellung auf. Wichtige Details zum Zweck und zur Funktionsweise dieses Diensts sowie häufig gestellte Fragen finden Sie unter [Automatisieren der Bereitstellung und Bereitstellungsaufhebung von Benutzern für SaaS-Anwendungen mit Azure Active Directory](../manage-apps/user-provisioning.md). 


## <a name="capabilities-supported"></a>Unterstützte Funktionen
> [!div class="checklist"]
> * Erstellen von Benutzern in Azure Databricks SCIM Connector
> * Entfernen von Benutzern aus Azure Databricks SCIM Connector, wenn diese keinen Zugriff mehr benötigen
> * Synchronisieren von Benutzerattributen zwischen Azure AD und Azure Databricks SCIM Connector
> * Bereitstellen von Gruppen und Gruppenmitgliedschaften in Azure Databricks SCIM Connector

## <a name="prerequisites"></a>Voraussetzungen

Das diesem Tutorial zu Grunde liegende Szenario setzt voraus, dass Sie bereits über die folgenden Voraussetzungen verfügen:

* [Azure AD-Mandant](https://docs.microsoft.com/azure/active-directory/develop/quickstart-create-new-tenant) 
* Ein Benutzerkonto in Azure AD mit der [Berechtigung](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) für die Konfiguration von Bereitstellungen (z.B. Anwendungsadministrator, Cloudanwendungsadministrator, Anwendungsbesitzer oder Globaler Administrator). 
* Ein Azure Databricks-Konto mit Administratorrechten.

## <a name="step-1-plan-your-provisioning-deployment"></a>Schritt 1: Planen der Bereitstellung
1. Erfahren Sie, [wie der Bereitstellungsdienst funktioniert](https://docs.microsoft.com/azure/active-directory/manage-apps/user-provisioning).
2. Bestimmen Sie, wer [in den Bereitstellungsbereich](https://docs.microsoft.com/azure/active-directory/manage-apps/define-conditional-rules-for-provisioning-user-accounts) einbezogen werden soll.
3. Legen Sie fest, welche Daten [zwischen Azure AD und Azure AD and Azure Databricks SCIM Connector zugeordnet werden sollen](https://docs.microsoft.com/azure/active-directory/manage-apps/customize-application-attributes). 

## <a name="step-2-configure-azure-databricks-scim-connector-to-support-provisioning-with-azure-ad"></a>Schritt 2: Konfigurieren von Azure Databricks SCIM Connector zur Unterstützung der Bereitstellung mit Azure AD

1. Um die Azure Databricks SCIM-Bereitstellung einzurichten, fügen Sie es als Ressource in Ihrem Azure Active Directory-Mandanten hinzu, und konfigurieren Sie es mit den folgenden Einstellungen.

    ![Azure Databricks-Setup](./media/azure-databricks-scim-provisioning-connector-provisioning-tutorial/setup.png)

2. Informationen zum Generieren eines persönlichen Zugriffstokens in Azure Databricks finden Sie [hier](https://docs.microsoft.com/azure/databricks/dev-tools/api/latest/authentication#token-management).

3. Kopieren Sie das **Token**. Dieser Wert wird im Azure-Portal auf der Registerkarte „Bereitstellung“ Ihrer Azure Databricks SCIM Connector-Anwendung in das Feld „Geheimes Token“ eingegeben.

## <a name="step-3-add-azure-databricks-scim-connector-from-the-azure-ad-application-gallery"></a>Schritt 3: Hinzufügen von Azure Databricks SCIM Connector aus dem Azure AD-Anwendungskatalog

Fügen Sie Azure Databricks SCIM Connector aus dem Azure AD-Anwendungskatalog hinzu, um mit der Verwaltung der Bereitstellung von Azure Databricks SCIM Connector zu beginnen. Wenn Sie Azure Databricks SCIM Connector zuvor für das einmalige Anmelden (SSO) eingerichtet haben, können Sie dieselbe Anwendung verwenden. Es ist jedoch empfehlenswert, beim erstmaligen Testen der Integration eine separate App zu erstellen. [Hier](https://docs.microsoft.com/azure/active-directory/manage-apps/add-gallery-app) erfahren Sie mehr über das Hinzufügen einer Anwendung aus dem Katalog. 

## <a name="step-4-define-who-will-be-in-scope-for-provisioning"></a>Schritt 4. Definieren der Benutzer für den Bereitstellungsbereich 

Mit dem Azure AD-Bereitstellungsdienst können Sie anhand der Zuweisung zur Anwendung oder aufgrund von Attributen für den Benutzer/die Gruppe festlegen, wer in die Bereitstellung einbezogen werden soll. Wenn Sie sich dafür entscheiden, anhand der Zuweisung festzulegen, wer für Ihre App bereitgestellt werden soll, können Sie der Anwendung mithilfe der folgenden [Schritte](../manage-apps/assign-user-or-group-access-portal.md) Benutzer und Gruppen zuweisen. Wenn Sie allein anhand der Attribute des Benutzers oder der Gruppe auswählen möchten, wer bereitgestellt wird, können Sie einen [hier](https://docs.microsoft.com/azure/active-directory/manage-apps/define-conditional-rules-for-provisioning-user-accounts) beschriebenen Bereichsfilter verwenden. 

* Beim Zuweisen von Benutzern und Gruppen zu Azure Databricks SCIM Connector müssen Sie eine andere Rolle als **Standardzugriff** auswählen. Benutzer mit der Rolle „Standardzugriff“ werden von der Bereitstellung ausgeschlossen und in den Bereitstellungsprotokollen als „nicht effektiv berechtigt“ gekennzeichnet. Wenn für die Anwendung nur die Rolle „Standardzugriff“ verfügbar ist, können Sie das [Anwendungsmanifest aktualisieren](https://docs.microsoft.com/azure/active-directory/develop/howto-add-app-roles-in-azure-ad-apps) und weitere Rollen hinzufügen. 

* Fangen Sie klein an. Testen Sie die Bereitstellung mit einer kleinen Gruppe von Benutzern und Gruppen, bevor Sie sie für alle freigeben. Wenn der Bereitstellungsbereich auf zugewiesene Benutzer und Gruppen festgelegt ist, können Sie dies durch Zuweisen von einem oder zwei Benutzern oder Gruppen zur App kontrollieren. Ist der Bereich auf alle Benutzer und Gruppen festgelegt, können Sie einen [attributbasierten Bereichsfilter](https://docs.microsoft.com/azure/active-directory/manage-apps/define-conditional-rules-for-provisioning-user-accounts) angeben. 


## <a name="step-5-configure-automatic-user-provisioning-to-azure-databricks-scim-connector"></a>Schritt 5: Konfigurieren der automatischen Benutzerbereitstellung für Azure Databricks SCIM Connector 

In diesem Abschnitt werden die Schritte zum Konfigurieren des Azure AD-Bereitstellungsdiensts zum Erstellen, Aktualisieren und Deaktivieren von Benutzern bzw. Gruppen in ServiceNow auf der Grundlage von Benutzer- oder Gruppenzuweisungen in Azure AD erläutert.

> [!NOTE]
> Weitere Informationen zum SCIM-Endpunkt von Azure Databricks finden Sie [hier](https://docs.databricks.com/dev-tools/api/latest/scim.html
).

### <a name="to-configure-automatic-user-provisioning-for-azure-databricks-scim-connector-in-azure-ad"></a>So konfigurieren Sie die automatische Benutzerbereitstellung für Azure Databricks SCIM Connector in Azure AD

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com) an. Wählen Sie **Unternehmensanwendungen** und dann **Alle Anwendungen**.

    ![Blatt „Unternehmensanwendungen“](common/enterprise-applications.png)

2. Wählen Sie in der Anwendungsliste **Azure Databricks SCIM Connector** aus.

    ![Azure Databricks SCIM Connector-Verknüpfung in der Anwendungsliste](common/all-applications.png)

3. Wählen Sie die Registerkarte **Bereitstellung**.

    ![Registerkarte „Bereitstellung“](common/provisioning.png)

4. Legen Sie den **Bereitstellungsmodus** auf **Automatisch** fest.

    ![Registerkarte „Bereitstellung“](common/provisioning-automatic.png)

5. Geben Sie im Abschnitt **Administratoranmeldeinformationen** im Feld **Mandanten-URL** den Wert des SCIM-Endpunkts ein. Die Mandanten-URL sollte das Format `https://<region>.azuredatabricks.net/api/2.0/preview/scim` haben. Der Wert für **region** ist in der URL der Azure Databricks-Homepage enthalten. Der SCIM-Endpunkt für die Region **westus** lautet beispielsweise `https://westus.azuredatabricks.net/api/2.0/preview/scim`. Geben Sie den Tokenwert ein, den Sie zuvor unter **Geheimes Token** abgerufen haben. Klicken Sie auf **Verbindung testen**, um sicherzustellen, dass Azure AD eine Verbindung mit Azure Databricks SCIM Connector herstellen kann. Vergewissern Sie sich im Falle eines Verbindungsfehlers, dass Ihr Azure Databricks SCIM Connector-Konto über Administratorberechtigungen verfügt, und versuchen Sie es noch mal.

    ![Bereitstellung](./media/azure-databricks-scim-provisioning-connector-provisioning-tutorial/provisioning.png)

6. Geben Sie im Feld **Benachrichtigungs-E-Mail** die E-Mail-Adresse einer Person oder Gruppe ein, die Benachrichtigungen zu Bereitstellungsfehlern erhalten soll, und aktivieren Sie das Kontrollkästchen **Bei Fehler E-Mail-Benachrichtigung senden**.

    ![Benachrichtigungs-E-Mail](common/provisioning-notification-email.png)

7. Wählen Sie **Speichern** aus.

8. Klicken Sie im Abschnitt **Zuordnungen** auf die Option zum **Synchronisieren von Azure Active Directory-Benutzern mit Azure Databricks SCIM Connector**.

9. Überprüfen Sie im Abschnitt **Attributzuordnungen** die Benutzerattribute, die von Azure AD mit Azure Databricks SCIM Connector synchronisiert werden. Die als **Matching** (übereinstimmende) Eigenschaften ausgewählten Attribute werden für den Abgleich der Benutzerkonten in Azure Databricks SCIM Connector für Aktualisierungsvorgänge verwendet. Wenn Sie sich dafür entscheiden, das [übereinstimmende Zielattribut](https://docs.microsoft.com/azure/active-directory/manage-apps/customize-application-attributes) zu ändern, müssen Sie sicherstellen, dass die Azure Databricks SCIM Connector-API das Filtern von Benutzern anhand dieses Attributs unterstützt. Wählen Sie die Schaltfläche **Speichern**, um alle Änderungen zu übernehmen.

   |attribute|type|
   |---|---|
   |userName|String|
   |displayName|String|
   |aktiv|Boolean|

10. Klicken Sie im Abschnitt **Zuordnungen** auf die Option zum **Synchronisieren von Azure Active Directory-Gruppen mit Azure Databricks SCIM Connector**.

11. Überprüfen Sie im Abschnitt **Attributzuordnungen** die Gruppenattribute, die von Azure AD mit Azure Databricks SCIM Connector synchronisiert werden. Die als **Matching** (übereinstimmende) Eigenschaften ausgewählten Attribute werden für den Abgleich der Gruppen in Azure Databricks SCIM Connector für Aktualisierungsvorgänge verwendet. Wählen Sie die Schaltfläche **Speichern**, um alle Änderungen zu übernehmen.

     |attribute|type|
     |---|---|
     |displayName|String|
     |members|Verweis|

11. Klicken Sie im Abschnitt **Zuordnungen** auf die Option zum **Synchronisieren von Azure Active Directory-Gruppen mit Azure Databricks SCIM Connector**.

12. Ändern Sie im Abschnitt **Einstellungen** den **Bereitstellungsstatus** in **Ein**, um den Azure AD-Bereitstellungsdienst für Azure Databricks SCIM Connector zu aktivieren.

    ![Aktivierter Bereitstellungsstatus](common/provisioning-toggle-on.png)

13. Legen Sie die Benutzer und/oder Gruppen fest, die in Azure Databricks SCIM Connector bereitgestellt werden sollen, indem Sie im Abschnitt **Einstellungen** unter **Bereich** die gewünschten Werte auswählen.

    ![Bereitstellungsbereich](common/provisioning-scope.png)

14. Wenn Sie fertig sind, klicken Sie auf **Speichern**.

    ![Speichern der Bereitstellungskonfiguration](common/provisioning-configuration-save.png)

Durch diesen Vorgang wird der erstmalige Synchronisierungszyklus für alle Benutzer und Gruppen gestartet, die im Abschnitt **Einstellungen** unter **Bereich** definiert wurden. Der erste Zyklus dauert länger als nachfolgende Zyklen, die ungefähr alle 40 Minuten erfolgen, solange der Azure AD-Bereitstellungsdienst ausgeführt wird. 

## <a name="step-6-monitor-your-deployment"></a>Schritt 6: Überwachen der Bereitstellung
Nachdem Sie die Bereitstellung konfiguriert haben, können Sie mit den folgenden Ressourcen die Bereitstellung überwachen:

* Mithilfe der [Bereitstellungsprotokolle](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-provisioning-logs) können Sie ermitteln, welche Benutzer erfolgreich bzw. nicht erfolgreich bereitgestellt wurden.
* Anhand der [Fortschrittsleiste](https://docs.microsoft.com/azure/active-directory/manage-apps/application-provisioning-when-will-provisioning-finish-specific-user) können Sie den Status des Bereitstellungszyklus überprüfen und den Fortschritt der Bereitstellung verfolgen.
* Wenn sich die Bereitstellungskonfiguration in einem fehlerhaften Zustand zu befinden scheint, wird die Anwendung unter Quarantäne gestellt. Weitere Informationen zu den verschiedenen Quarantänestatus finden Sie [hier](https://docs.microsoft.com/azure/active-directory/manage-apps/application-provisioning-quarantine-status).  

## <a name="troubleshooting-tips"></a>Tipps zur Problembehandlung
* Databricks konvertiert die Werte ihrer Benutzernamen immer in Kleinbuchstaben, wenn sie in ihrem Verzeichnis gespeichert werden, unabhängig von der Groß- und Kleinschreibung, die wir ihnen über SCIM senden.
* Derzeit unterscheiden GET-Anforderungen für die SCIM-API von Azure Databricks für Benutzer die Groß- und Kleinschreibung. Bei einer Abfrage nach USER@contoso.com werden keine Ergebnisse zurückgegeben, da es als user@contoso.com gespeichert wird.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Verwalten der Benutzerkontobereitstellung für Unternehmens-Apps](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

## <a name="next-steps"></a>Nächste Schritte

* [Erfahren Sie, wie Sie Protokolle überprüfen und Berichte zu Bereitstellungsaktivitäten abrufen.](../manage-apps/check-status-user-account-provisioning.md)
