---
title: Konfigurieren des einmaliges Anmeldens für Anwendungen | Microsoft-Dokumentation
description: Konfigurieren des einmaliges Anmeldens für eine mit Azure AD entwickelte und registrierte benutzerdefinierte Anwendung
services: active-directory
documentationcenter: ''
author: rwike77
manager: CelesteDG
ms.assetid: ''
ms.service: active-directory
ms.subservice: develop
ms.custom: aaddev
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/15/2019
ms.author: ryanwi
ms.openlocfilehash: bb77f376e22428e9259ff3efc84cf6f1cb3491fe
ms.sourcegitcommit: af6847f555841e838f245ff92c38ae512261426a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/23/2020
ms.locfileid: "76702640"
---
# <a name="how-to-configure-single-sign-on-for-an-application"></a>Konfigurieren des einmaliges Anmeldens für eine Anwendung

Die Aktivierung der einmaligen Verbundanmeldung in Ihrer App wird beim Verbund mit Azure AD für OpenID Connect, SAML 2.0 oder WS-Fed automatisch aktiviert. Wenn sich Ihre Endbenutzer anmelden müssen, anstatt bereits über eine vorhandene Sitzung mit Azure AD zu verfügen, ist es wahrscheinlich, dass Ihre App möglicherweise falsch konfiguriert ist.

* Wenn Sie ADAL/MSAL verwenden, stellen Sie sicher, dass für **PromptBehavior** die Option **Auto** statt **Immer** festgelegt ist.

* Wenn Sie eine mobile App erstellen, sind möglicherweise zusätzliche Konfigurationen erforderlich, um Broker-SSO oder Nicht-Broker-SSO zu aktivieren.

Informationen für Android-Geräte finden Sie unter [Aktivieren von App-übergreifendem SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).<br>

Informationen für iOS-Geräte finden Sie unter [Aktivieren von App-übergreifendem SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).

## <a name="next-steps"></a>Nächste Schritte

[Azure AD-SSO](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[Aktivieren von App-übergreifendem SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[Aktivieren von App-übergreifendem SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[Integrieren von Apps in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[Genehmigen und Zuweisen von Berechtigungen für konvergierte Azure AD V2.0-Apps](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[Azure AD bei Stack Overflow](https://stackoverflow.com/questions/tagged/azure-active-directory)
