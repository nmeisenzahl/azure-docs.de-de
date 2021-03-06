---
title: include file
description: include file
services: cognitive-services
author: diberry
manager: nitinme
ms.service: cognitive-services
ms.subservice: personalizer
ms.topic: include
ms.custom: include file
ms.date: 01/15/2020
ms.author: diberry
ms.openlocfilehash: 786efcb712557da4363384c9d05c33f4f16d6731
ms.sourcegitcommit: 5bbe87cf121bf99184cc9840c7a07385f0d128ae
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/16/2020
ms.locfileid: "76122728"
---
[Referenzdokumentation](https://docs.microsoft.com/javascript/api/@azure/cognitiveservices-personalizer/?view=azure-node-latest) |[Quellcode der Bibliothek](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/cognitiveservices/cognitiveservices-personalizer) | [Paket (NPM)](https://www.npmjs.com/package/@azure/cognitiveservices-personalizer) | [Beispiele](https://github.com/Azure-Samples/cognitive-services-personalizer-samples/blob/master/quickstarts/node/sample.js)

## <a name="prerequisites"></a>Voraussetzungen

* Azure-Abonnement – [Erstellen eines kostenlosen Kontos](https://azure.microsoft.com/free/)
* Die aktuelle Version von [Node.js](https://nodejs.org) und npm

## <a name="using-this-quickstart"></a>Verwenden dieser Schnellstartanleitung


Diese Schnellstartanleitung umfasst mehrere Schritte:

* Erstellen Sie im Azure-Portal eine Personalisierungsressource.
* Ändern Sie im Azure-Portal auf der Seite **Konfiguration** die Häufigkeit der Modellaktualisierung für die Personalisierungsressource in ein sehr kurzes Intervall.
* Erstellen Sie in einem Code-Editor eine Codedatei, und bearbeiten Sie sie.
* Installieren Sie in der Befehlszeile oder im Terminal das SDK über die Befehlszeile.
* Führen Sie die Codedatei in der Befehlszeile oder im Terminal aus.

[!INCLUDE [Create Azure resource for Personalizer](create-personalizer-resource.md)]

[!INCLUDE [!Change model frequency](change-model-frequency.md)]

## <a name="create-a-new-nodejs-application"></a>Erstellen einer neuen Node.js-Anwendung

Erstellen Sie in einem Konsolenfenster (etwa cmd, PowerShell oder Bash) ein neues Verzeichnis für Ihre App, und rufen Sie es auf.

```console
mkdir myapp && cd myapp
```

Führen Sie den Befehl `npm init -y` aus, um die Datei `package.json` zu erstellen.

```console
npm init -y
```

## <a name="install-the-nodejs-library-for-personalizer"></a>Installieren der Node.js-Bibliothek für die Personalisierung

Installieren Sie mit dem folgenden Befehl die Personalisierungsclientbibliothek für Node.js:

```console
npm install @azure/cognitiveservices-personalizer --save
```

Installieren Sie die verbleibenden NPM-Pakete für diese Schnellstartanleitung:

```console
npm install @azure/ms-rest-azure-js @azure/ms-rest-js readline-sync uuid --save
```

## <a name="object-model"></a>Objektmodell

Der Personalisierungsclient ist ein Objekt vom Typ [PersonalizerClient](https://docs.microsoft.com/javascript/api/@azure/cognitiveservices-personalizer/personalizerclient?view=azure-node-latest), das mithilfe der Klasse „Microsoft.Rest.ServiceClientCredentials“, die Ihren Schlüssel enthält, bei Azure authentifiziert wird.

Erstellen Sie zum Anfordern des besten Inhaltselements eine Rangfolgeanforderung ([RankRequest](https://docs.microsoft.com/javascript/api/@azure/cognitiveservices-personalizer/rankrequest?view=azure-node-latest)), und übergeben Sie sie an die Methode [client.Rank](https://docs.microsoft.com/javascript/api/@azure/cognitiveservices-personalizer/personalizerclient?view=azure-node-latest#rank-rankrequest--msrest-requestoptionsbase-). Die Methode „Rank“ gibt eine Rangfolgeantwort (RankResponse) zurück.

Erstellen Sie eine Relevanzanforderung ([RewardRequest](https://docs.microsoft.com/javascript/api/@azure/cognitiveservices-personalizer/rewardrequest?view=azure-node-latest)), und übergeben Sie sie an die Methode [Reward](https://docs.microsoft.com/javascript/api/@azure/cognitiveservices-personalizer/events?view=azure-node-latest#reward-string--rewardrequest--servicecallback-void--) der Klasse „Events“, um eine Relevanz an die Personalisierung zu senden.

Im Rahmen dieser Schnellstartanleitung ist die Bestimmung der Relevanz ganz einfach. In einem Produktionssystem kann die Bestimmung der Einflussfaktoren für die [Relevanzbewertung](../concept-rewards.md) sowie deren jeweilige Gewichtung allerdings eine komplexe Angelegenheit sein und muss unter Umständen im Laufe der Zeit überarbeitet werden. Hierbei handelt es sich um eine der wichtigsten Entwurfsentscheidungen im Zusammenhang mit Ihrer Personalisierungsarchitektur.

## <a name="code-examples"></a>Codebeispiele

In diesen Codeausschnitten werden folgende Vorgänge mit der Personalisierungsclientbibliothek für Node.js veranschaulicht:

* [Erstellen eines Personalisierungsclients](#create-a-personalizer-client)
* [Rangfolge-API](#request-the-best-action)
* [Relevanz-API](#send-a-reward)

## <a name="create-a-new-nodejs-application"></a>Erstellen einer neuen Node.js-Anwendung

Erstellen Sie eine neue Node.js-Anwendung namens `sample.js` in Ihrem bevorzugten Editor oder Ihrer bevorzugten IDE.

## <a name="add-the-dependencies"></a>Hinzufügen der Abhängigkeiten

Öffnen Sie die Datei **sample.js** in Ihrem bevorzugten Editor oder Ihrer bevorzugten IDE. Fügen Sie zum Hinzufügen der NPM-Pakete die folgenden `requires`-Elemente hinzu:

[!code-javascript[Add module dependencies](~/samples-personalizer/quickstarts/node/sample.js?name=Dependencies)]

## <a name="add-personalizer-resource-information"></a>Hinzufügen von Informationen zur Personalisierungsressource

Erstellen Sie Variablen für den Azure-Schlüssel und -Endpunkt Ihrer Ressource, die aus den Umgebungsvariablen gepullt wurden, und nennen Sie sie `PERSONALIZER_KEY` und `PERSONALIZER_ENDPOINT`. Wenn Sie die Umgebungsvariablen nach dem Start der Anwendung erstellen, muss der Editor, die IDE oder die Shell, in dem bzw. in der sie ausgeführt wird, geschlossen und erneut geladen werden, damit auf die Variable zugegriffen werden kann. Die Methoden werden später in dieser Schnellstartanleitung erstellt.

[!code-javascript[Add Personalizer resource information](~/samples-personalizer/quickstarts/node/sample.js?name=AuthorizationVariables)]

## <a name="create-a-personalizer-client"></a>Erstellen eines Personalisierungsclients

Erstellen Sie als Nächstes eine Methode zum Zurückgeben eines Personalisierungsclients. Der Parameter für die Methode lautet `PERSONALIZER_RESOURCE_ENDPOINT`, und der API-Schlüssel (ApiKey) ist `PERSONALIZER_RESOURCE_KEY`.

[!code-javascript[Create a Personalizer client](~/samples-personalizer/quickstarts/node/sample.js?name=Client)]

## <a name="get-content-choices-represented-as-actions"></a>Abrufen von Inhaltsoptionen, dargestellt als Aktionen

Aktionen stellen die Inhaltsoptionen dar, aus denen die Personalisierung das beste Inhaltselement auswählen soll. Fügen Sie der Klasse „Program“ die folgenden Methoden hinzu, um die Gruppe der Aktionen und deren Features darzustellen.

[!code-javascript[Create user features](~/samples-personalizer/quickstarts/node/sample.js?name=createUserFeatureTimeOfDay)]

[!code-javascript[Create actions](~/samples-personalizer/quickstarts/node/sample.js?name=getActions)]

## <a name="create-the-learning-loop"></a>Erstellen der Lernschleife

Die Lernschleife der Personalisierung ist ein Zyklus aus [Rangfolge-](#request-the-best-action) und [Relevanzaufrufen](#send-a-reward). In dieser Schnellstartanleitung folgt auf jeden Rangfolgeaufruf zur Personalisierung des Inhalts ein Relevanzaufruf, um der Personalisierung mitzuteilen, wie gut der Dienst abgeschnitten hat.

Der folgende Code durchläuft einen Zyklus in Form einer Schleife: Der Benutzer wird an der Befehlszeile nach seinen Präferenzen befragt, die Angaben werden zur Wahl der besten Aktion an die Personalisierung gesendet, die Auswahl wird dem Kunden in einer Auswahlliste angezeigt, und anschließend wird eine Relevanz an die Personalisierung gesendet, die angibt, wie gut die Wahl des Diensts war.

[!code-javascript[Create the learning loop](~/samples-personalizer/quickstarts/node/sample.js?name=mainLoop)]

Sehen Sie sich die Rangfolge- und Relevanzaufrufe in den folgenden Abschnitten genauer an.

Fügen Sie vor dem Ausführen der Codedatei die folgenden Methoden hinzu, die die [Inhaltsoptionen abrufen](#get-content-choices-represented-as-actions):

* getActionsList
* getContextFeaturesList

## <a name="request-the-best-action"></a>Anfordern der besten Aktion

Für die Rangfolgeanforderung erfragt das Programm die Präferenzen des Benutzers, um Inhaltsoptionen zu erstellen. Der Prozess kann Inhalte erstellen, die von den Aktionen ausgeschlossen werden sollen (angezeigt als `excludeActions`). Die Rangfolgeanforderung muss die [Aktionen](../concepts-features.md#actions-represent-a-list-of-options) und ihre Features, die Features des aktuellen Kontexts (currentContext), die auszuschließenden Aktionen (excludeActions) und eine eindeutige Rangfolgeereignis-ID enthalten, um die bewertete Antwort zu erhalten.

In dieser Schnellstartanleitung werden die einfachen Kontextmerkmale „Tageszeit“ und „Essenswunsch des Benutzers“ verwendet. In Produktionssystemen kann die Bestimmung und [Auswertung](../concept-feature-evaluation.md) von [Aktionen und Merkmalen](../concepts-features.md) allerdings eine komplexe Angelegenheit sein.

[!code-javascript[The Personalizer learning loop ranks the request.](~/samples-personalizer/quickstarts/node/sample.js?name=rank)]

## <a name="send-a-reward"></a>Senden einer Relevanz


Um die Relevanzbewertung zu erhalten, die in der Relevanzanforderung gesendet wird, ruft das Programm die Auswahl des Benutzers aus der Befehlszeile ab, weist der Auswahl einen numerischen Wert zu und sendet dann die eindeutige Ereignis-ID und die Relevanzbewertung als numerischen Wert an die Relevanz-API.

In dieser Schnellstartanleitung wird als Relevanzbewertung eine einfache Zahl (0 oder 1) zugewiesen. In Produktionssystemen ist die Entscheidung, was wann an den [Relevanzaufruf](../concept-rewards.md) gesendet werden soll (abhängig von Ihren spezifischen Anforderungen), unter Umständen etwas komplizierter.

[!code-javascript[The Personalizer learning loop sends a reward.](~/samples-personalizer/quickstarts/node/sample.js?name=reward)]

## <a name="run-the-program"></a>Ausführen des Programms

Führen Sie die Anwendung mit dem Node.js-Beispiel aus dem Anwendungsverzeichnis aus.

```console
node sample.js
```

![Das Schnellstartprogramm stellt ein paar Fragen zum Sammeln von Benutzereinstellungen – auch bekannt als Features – und stellt dann die am besten bewertete Aktion bereit.](../media/csharp-quickstart-commandline-feedback-loop/quickstart-program-feedback-loop-example.png)
