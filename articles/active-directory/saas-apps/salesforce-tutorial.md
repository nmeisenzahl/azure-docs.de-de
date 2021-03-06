---
title: 'Tutorial: Integration des einmaligen Anmeldens (Single Sign-On, SSO) von Azure Active Directory mit Salesforce | Microsoft-Dokumentation'
description: Erfahren Sie, wie Sie das einmalige Anmelden zwischen Azure Active Directory und Salesforce konfigurieren.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: tutorial
ms.date: 02/17/2020
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: a875cee7e6796a2c865bde4a62f2f0463eb12130
ms.sourcegitcommit: 5f39f60c4ae33b20156529a765b8f8c04f181143
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/10/2020
ms.locfileid: "78967721"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-salesforce"></a>Tutorial: Integration des einmaligen Anmeldens (Single Sign-On, SSO) von Azure Active Directory mit Salesforce

In diesem Tutorial erfahren Sie, wie Sie Salesforce in Azure Active Directory (Azure AD) integrieren. Die Integration von Salesforce in Azure AD ermöglicht Folgendes:

* Steuern Sie in Azure AD, wer Zugriff auf Salesforce hat.
* Ermöglichen Sie es Ihren Benutzern, sich mit ihren Azure AD-Konten automatisch bei Salesforce anzumelden.
* Verwalten Sie Ihre Konten zentral im Azure-Portal.

Weitere Informationen zur Integration von SaaS-Apps in Azure AD finden Sie unter [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

## <a name="prerequisites"></a>Voraussetzungen

Für die ersten Schritte benötigen Sie Folgendes:

* Ein Azure AD-Abonnement Falls Sie über kein Abonnement verfügen, können Sie ein [kostenloses Azure-Konto](https://azure.microsoft.com/free/) verwenden.
* Salesforce-Abonnement, für das einmaliges Anmelden (Single Sign-On, SSO) aktiviert ist

## <a name="scenario-description"></a>Beschreibung des Szenarios

In diesem Tutorial konfigurieren und testen Sie das einmalige Anmelden von Azure AD in einer Testumgebung.

* Salesforce unterstützt **SP**-initiiertes einmaliges Anmelden.

* Salesforce unterstützt die [**automatisierte** Benutzerbereitstellung und Bereitstellungsaufhebung](salesforce-provisioning-tutorial.md) (empfohlen).

* Salesforce unterstützt die **Just-in-Time**-Benutzerbereitstellung.

* Die mobile Salesforce-Anwendungen kann nun mit Azure AD konfiguriert werden, um SSO zu ermöglichen. In diesem Tutorial konfigurieren und testen Sie das einmalige Anmelden von Azure AD in einer Testumgebung.
* Nach dem Konfigurieren von Salesforce können Sie die Sitzungssteuerung erzwingen, die in Echtzeit vor der Exfiltration und Infiltration vertraulicher Unternehmensdaten schützt. Die Sitzungssteuerung basiert auf bedingtem Zugriff. [Hier](https://docs.microsoft.com/cloud-app-security/proxy-deployment-aad) erfahren Sie, wie Sie die Sitzungssteuerung mit Microsoft Cloud App Security erzwingen.

## <a name="adding-salesforce-from-the-gallery"></a>Hinzufügen von Salesforce aus dem Katalog

Zum Konfigurieren der Integration von Salesforce in Azure AD müssen Sie Salesforce aus dem Katalog zur Liste der verwalteten SaaS-Apps hinzufügen.

1. Melden Sie sich mit einem Geschäfts-, Schul- oder Unikonto oder mit einem persönlichen Microsoft-Konto beim [Azure-Portal](https://portal.azure.com) an.
1. Wählen Sie im linken Navigationsbereich den Dienst **Azure Active Directory** aus.
1. Navigieren Sie zu **Unternehmensanwendungen**, und wählen Sie dann **Alle Anwendungen** aus.
1. Wählen Sie zum Hinzufügen einer neuen Anwendung **Neue Anwendung** aus.
1. Geben Sie im Abschnitt **Aus Katalog hinzufügen** den Suchbegriff **Salesforce** in das Suchfeld ein.
1. Wählen Sie im Ergebnisbereich **Salesforce** aus, und fügen Sie dann die App hinzu. Warten Sie einige Sekunden, während die App Ihrem Mandanten hinzugefügt wird.

## <a name="configure-and-test-azure-ad-single-sign-on-for-salesforce"></a>Konfigurieren und Testen des einmaligen Anmeldens von Azure AD für Salesforce

Konfigurieren und testen Sie das einmalige Anmelden von Azure AD mit Salesforce mithilfe eines Testbenutzers mit dem Namen **B. Simon**. Damit einmaliges Anmelden funktioniert, muss eine Linkbeziehung zwischen einem Azure AD-Benutzer und dem entsprechenden Benutzer in Salesforce eingerichtet werden.

Führen Sie zum Konfigurieren und Testen des einmaligen Anmeldens von Azure AD mit Salesforce die folgenden Schritte aus:

1. **[Konfigurieren des einmaligen Anmeldens von Azure AD](#configure-azure-ad-sso)** , um Ihren Benutzern die Verwendung dieses Features zu ermöglichen.
    * **[Erstellen eines Azure AD-Testbenutzers](#create-an-azure-ad-test-user)** , um das einmalige Anmelden von Azure AD mit dem Testbenutzer B. Simon zu testen.
    * **[Zuweisen des Azure AD-Testbenutzers](#assign-the-azure-ad-test-user)** , um B. Simon die Verwendung des einmaligen Anmeldens von Azure AD zu ermöglichen.
1. **[Konfigurieren des einmaligen Anmeldens für Salesforce](#configure-salesforce-sso)** , um die Einstellungen für einmaliges Anmelden auf der Anwendungsseite zu konfigurieren
    * **[Erstellen eines Salesforce-Testbenutzers](#create-salesforce-test-user)** , um ein Pendant von B. Simon in Salesforce zu erhalten, das mit ihrer Darstellung in Azure AD verknüpft ist
1. **[Testen des einmaligen Anmeldens](#test-sso)** , um zu überprüfen, ob die Konfiguration funktioniert

## <a name="configure-azure-ad-sso"></a>Konfigurieren des einmaligen Anmeldens (Single Sign-On, SSO) von Azure AD

Gehen Sie wie folgt vor, um das einmalige Anmelden von Azure AD im Azure-Portal zu aktivieren.

1. Navigieren Sie im [Azure-Portal](https://portal.azure.com/) auf der Anwendungsintegrationsseite für **Salesforce** zum Abschnitt **Verwalten**, und wählen Sie **Einmaliges Anmelden** aus.
1. Wählen Sie auf der Seite **SSO-Methode auswählen** die Methode **SAML** aus.
1. Klicken Sie auf der Seite **Einmaliges Anmelden (SSO) mit SAML einrichten** auf das Bearbeitungs- bzw. Stiftsymbol für **Grundlegende SAML-Konfiguration**, um die Einstellungen zu bearbeiten.

   ![Bearbeiten der SAML-Basiskonfiguration](common/edit-urls.png)

1. Geben Sie im Abschnitt **Grundlegende SAML-Konfiguration** die Werte für die folgenden Felder ein:

    a. Geben Sie im Textfeld **Anmelde-URL** den Wert im folgenden Format ein:

    Enterprise-Konto: `https://<subdomain>.my.salesforce.com`

    Developer-Konto: `https://<subdomain>-dev-ed.my.salesforce.com`

    b. Geben Sie im Textfeld **Bezeichner** den Wert in folgendem Format ein:

    Enterprise-Konto: `https://<subdomain>.my.salesforce.com`

    Developer-Konto: `https://<subdomain>-dev-ed.my.salesforce.com`

    > [!NOTE]
    > Hierbei handelt es sich um Beispielwerte. Ersetzen Sie diese Werte durch die tatsächliche Anmelde-URL und den tatsächlichen Bezeichner. Wenden Sie sich an das [Kundensupportteam von Salesforce](https://help.salesforce.com/support), um diese Werte zu erhalten.

1. Navigieren Sie auf der Seite **Einmaliges Anmelden (SSO) mit SAML einrichten** im Abschnitt **SAML-Signaturzertifikat** zu **Verbundmetadaten-XML**, und wählen Sie **Herunterladen** aus, um das Zertifikat herunterzuladen und auf Ihrem Computer zu speichern.

    ![Downloadlink für das Zertifikat](common/metadataxml.png)

1. Kopieren Sie im Abschnitt **Salesforce einrichten** die entsprechenden URLs basierend auf Ihren Anforderungen.

    ![Kopieren der Konfiguration-URLs](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Erstellen eines Azure AD-Testbenutzers

In diesem Abschnitt erstellen Sie im Azure-Portal einen Testbenutzer mit dem Namen B. Simon.

1. Wählen Sie im linken Bereich des Microsoft Azure-Portals **Azure Active Directory** > **Benutzer** > **Alle Benutzer** aus.
1. Wählen Sie oben im Bildschirm die Option **Neuer Benutzer** aus.
1. Führen Sie unter den Eigenschaften für **Benutzer** die folgenden Schritte aus:
   1. Geben Sie im Feld **Name** die Zeichenfolge `B.Simon` ein.  
   1. Geben Sie im Feld **Benutzername** die Zeichenfolge username@companydomain.extension ein. Beispiel: `B.Simon@contoso.com`.
   1. Aktivieren Sie das Kontrollkästchen **Kennwort anzeigen**, und notieren Sie sich den Wert aus dem Feld **Kennwort**.
   1. Klicken Sie auf **Erstellen**.

### <a name="assign-the-azure-ad-test-user"></a>Zuweisen des Azure AD-Testbenutzers

In diesem Abschnitt ermöglichen Sie B. Simon die Verwendung des einmaligen Anmeldens von Azure, indem Sie ihr Zugriff auf Salesforce gewähren.

1. Wählen Sie im Azure-Portal **Unternehmensanwendungen** > **Alle Anwendungen** aus.
1. Wählen Sie in der Liste der Anwendungen **Salesforce** aus.
1. Navigieren Sie auf der Übersichtsseite der App zum Abschnitt **Verwalten**, und wählen Sie **Benutzer und Gruppen** aus.

   ![Link „Benutzer und Gruppen“](common/users-groups-blade.png)

1. Wählen Sie **Benutzer hinzufügen** und anschließend im Dialogfeld **Zuweisung hinzufügen** die Option **Benutzer und Gruppen** aus.

    ![Link „Benutzer hinzufügen“](common/add-assign-user.png)

1. Wählen Sie im Dialogfeld **Benutzer und Gruppen** in der Liste „Benutzer“ den Eintrag **B. Simon** aus, und klicken Sie dann unten auf dem Bildschirm auf die Schaltfläche **Auswählen**.
1. Wenn Sie einen beliebigen Rollenwert in der SAML-Assertion erwarten, wählen Sie im Dialogfeld **Rolle auswählen** die entsprechende Rolle für den Benutzer in der Liste aus, und klicken Sie dann im unteren Bildschirmbereich auf die Schaltfläche **Auswählen**.
1. Klicken Sie im Dialogfeld **Zuweisung hinzufügen** auf die Schaltfläche **Zuweisen**.

## <a name="configure-salesforce-sso"></a>Konfigurieren des einmaligen Anmeldens für Salesforce

1. Wenn Sie die Konfiguration in Salesforce automatisieren möchten, müssen Sie die **Browsererweiterung „Meine Apps“ für die sichere Anmeldung** installieren, indem Sie auf **Erweiterung installieren** klicken.

    ![Erweiterung „Meine Apps“](common/install-myappssecure-extension.png)

1. Klicken Sie nach dem Hinzufügen der Erweiterung zum Browser auf **Salesforce einrichten**, um zur Salesforce-SSO-Anwendung weitergeleitet zu werden. Geben Sie dort die Administratoranmeldeinformationen ein, um sich bei Salesforce anzumelden. Die Browsererweiterung konfiguriert die Anwendung automatisch für Sie und automatisiert die Schritte 3 bis 13.

    ![Einrichtungskonfiguration](common/setup-sso.png)

1. Wenn Sie Salesforce manuell einrichten möchten, melden Sie sich in einem neuen Webbrowserfenster bei der Salesforce-Unternehmenswebsite als Administrator an, und führen Sie die folgenden Schritte aus:

1. Klicken Sie in der oberen rechten Ecke der Seite unter dem **Einstellungssymbol** auf **Setup**.

    ![Einmaliges Anmelden konfigurieren](./media/salesforce-tutorial/configure1.png)

1. Scrollen Sie im Navigationsbereich nach unten bis zu den **SETTINGS** (EINSTELLUNGEN), und klicken Sie auf **Identity** (Identität), um den zugehörigen Bereich zu erweitern. Klicken Sie dann auf **Einstellungen für einmaliges Anmelden**.

    ![Einmaliges Anmelden konfigurieren](./media/salesforce-tutorial/sf-admin-sso.png)

1. Klicken Sie auf der Seite **Einstellungen für einmaliges Anmelden** auf die Schaltfläche **Bearbeiten**.

    ![Einmaliges Anmelden konfigurieren](./media/salesforce-tutorial/sf-admin-sso-edit.png)

    > [!NOTE]
    > Wenn Sie keine Einstellungen für die einmalige Anmeldung für Ihr Salesforce-Konto aktivieren können, müssen Sie sich an das [Kundensupportteam von Salesforce](https://help.salesforce.com/support) wenden.

1. Wählen Sie **SAML aktiviert**, und klicken Sie dann auf **Speichern**.

    ![Einmaliges Anmelden konfigurieren](./media/salesforce-tutorial/sf-enable-saml.png)

1. Klicken Sie auf **Neu aus Metadatendatei**, um Ihre SAML-Einstellungen für einmaliges Anmelden zu konfigurieren.

    ![Einmaliges Anmelden konfigurieren](./media/salesforce-tutorial/sf-admin-sso-new.png)

1. Klicken Sie auf **Datei auswählen**, um die Metadaten-XML-Datei hochzuladen, die Sie aus dem Azure-Portal heruntergeladen haben, und klicken Sie dann auf **Erstellen**.

    ![Einmaliges Anmelden konfigurieren](./media/salesforce-tutorial/xmlchoose.png)

1. Auf der Seite **SAML-Einstellungen für einmaliges Anmelden** werden die Felder automatisch aufgefüllt. Wählen Sie **Benutzerbereitstellung aktiviert** aus, und klicken Sie dann auf **Speichern**.

    ![Einmaliges Anmelden konfigurieren](./media/salesforce-tutorial/salesforcexml.png)

1. Klicken Sie in Salesforce im linken Navigationsbereich auf **Company Settings** (Unternehmenseinstellungen), um den zugehörigen Abschnitt zu erweitern, und klicken Sie dann auf **My Domain** (Meine Domäne).

    ![Einmaliges Anmelden konfigurieren](./media/salesforce-tutorial/sf-my-domain.png)

1. Führen Sie einen Bildlauf nach unten zum Abschnitt **Authentifizierungskonfiguration** aus, und klicken Sie auf die Schaltfläche **Bearbeiten**.

    ![Einmaliges Anmelden konfigurieren](./media/salesforce-tutorial/sf-edit-auth-config.png)

1. Wählen Sie im Abschnitt **Konfiguration der Authentifizierung** die Option **AzureSSO** als **Authentifizierungsdienst** Ihrer SAML-SSO-Konfiguration, und klicken Sie dann auf **Speichern**.

    ![Einmaliges Anmelden konfigurieren](./media/salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > Wenn mehrere Authentifizierungsdienste aktiviert sind, werden Benutzer aufgefordert, einen Authentifizierungsdienst zur Anmeldung auszuwählen, wenn das einmalige Anmelden bei der Salesforce-Umgebung initiiert wird. Wenn Sie dies nicht möchten, sollten Sie **alle anderen Authentifizierungsdienste deaktiviert lassen**.

### <a name="create-salesforce-test-user"></a>Erstellen eines Salesforce-Testbenutzers

In diesem Abschnitt wird ein Benutzer mit dem Namen B. Simon in Salesforce erstellt. Salesforce unterstützt die Just-in-Time-Bereitstellung, die standardmäßig aktiviert ist. Für Sie steht in diesem Abschnitt kein Aktionselement zur Verfügung. Falls ein Benutzer nicht bereits in Salesforce vorhanden ist, wird beim Versuch, auf Salesforce zuzugreifen, ein neuer Benutzer erstellt. Außerdem unterstützt Salesforce die automatische Benutzerbereitstellung. Weitere Informationen zum Konfigurieren der automatischen Benutzerbereitstellung finden Sie [hier](salesforce-provisioning-tutorial.md).

## <a name="test-sso"></a>Testen des einmaligen Anmeldens

In diesem Abschnitt testen Sie die Azure AD-Konfiguration für einmaliges Anmelden über den Zugriffsbereich.

Wenn Sie im Zugriffsbereich auf die Kachel „Salesforce“ klicken, sollten Sie automatisch bei Ihrer Salesforce-Anwendung angemeldet werden. Weitere Informationen zum Zugriffsbereich finden Sie unter [Einführung in den Zugriffsbereich](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).

## <a name="test-sso-for-salesforce-mobile"></a>Testen des einmaligen Anmeldens für Salesforce (mobil)

1. Öffnen Sie die mobile Salesforce-Anwendung. Klicken Sie auf der Anmeldeseite auf **Use Custom Domain** (Benutzerdefinierte Domäne verwenden).

    ![Mobile Salesforce-App](media/salesforce-tutorial/mobile-app1.png)

1. Geben Sie in das Textfeld **Custom Domain** (Benutzerdefinierte Domäne) Ihren registrierten benutzerdefinierten Domänenamen ein, und klicken Sie auf **Continue** (Weiter).

    ![Mobile Salesforce-App](media/salesforce-tutorial/mobile-app2.png)

1. Geben Sie Ihre Azure AD-Anmeldeinformationen ein, um sich bei der Salesforce-Anwendung anzumelden, und klicken Sie auf **Next** (Weiter).

    ![Mobile Salesforce-App](media/salesforce-tutorial/mobile-app3.png)

1. Klicken Sie auf der nachfolgend gezeigten Seite **Allow Access** (Zugriff zulassen) auf **Allow** (Zulassen), um den Zugriff auf die Salesforce-Anwendung zuzulassen.

    ![Mobile Salesforce-App](media/salesforce-tutorial/mobile-app4.png)

1. Nach erfolgreicher Anmeldung wird die Startseite der Anwendung angezeigt:

    ![Mobile Salesforce-App](media/salesforce-tutorial/mobile-app5.png) ![Mobile Salesforce-App](media/salesforce-tutorial/mobile-app6.png)

## <a name="additional-resources"></a>Zusätzliche Ressourcen

- [Liste der Tutorials zur Integration von SaaS-Apps in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Was ist bedingter Zugriff?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

- [Konfigurieren der Benutzerbereitstellung](salesforce-provisioning-tutorial.md)

- [Salesforce mit Azure AD ausprobieren](https://aad.portal.azure.com)

- [Was ist Sitzungssteuerung in Microsoft Cloud App Security?](https://docs.microsoft.com/cloud-app-security/proxy-intro-aad)

- [Schützen von Apps mit der App-Steuerung für bedingten Zugriff von Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/protect-salesforce)