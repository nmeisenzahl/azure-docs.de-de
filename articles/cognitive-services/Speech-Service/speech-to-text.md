---
title: Spracherkennung – Speech-Dienst
titleSuffix: Azure Cognitive Services
description: Die Spracherkennungsfunktion (Sprache-zu-Text) ermöglicht die Echtzeittranskription von Audiostreams in Text. Diese Texteingaben können von Ihren Anwendungen, Tools oder Geräten verwendet, angezeigt und verarbeitet werden. Dieser Dienst arbeitet problemlos mit den Features Sprachsynthese (Text-to-Speech) und Sprachübersetzung zusammen.
services: cognitive-services
author: erhopf
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 12/11/2019
ms.author: erhopf
ms.openlocfilehash: 8518f92a4f4df1686d4b338783a93d969e04d219
ms.sourcegitcommit: f4f626d6e92174086c530ed9bf3ccbe058639081
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75379951"
---
# <a name="what-is-speech-to-text"></a>Was ist die Spracherkennung?

Die Spracherkennung des Speech-Diensts (auch als Sprache-zu-Text bezeichnet) ermöglicht die Echtzeittranskription von Audiostreams in Text. Diese Texteingaben können von Ihren Anwendungen, Tools oder Geräten verwendet, angezeigt und als Befehlseingabe verarbeitet werden. Dieser Dienst nutzt dieselbe Erkennungstechnologie, die Microsoft auch bei Cortana und Office-Produkten einsetzt. Er funktioniert nahtlos mit den Dienstangeboten für <a href="./speech-translation.md" target="_blank">Übersetzung<span class="docon docon-navigate-external x-hidden-focus"></span></a> und <a href="./text-to-speech.md" target="_blank">Sprachsynthese<span class="docon docon-navigate-external x-hidden-focus"></span></a>. Eine vollständige Liste der Spracherkennungssprachen finden Sie unter [Unterstützte Sprachen](language-support.md#speech-to-text).

Der Spracherkennungsdienst verwendet standardmäßig das sogenannte Universal Language Model. Dieses Modell wurde mit Microsoft-Daten trainiert, und es wird in der Cloud bereitgestellt. Es eignet sich besonders für Gesprächs- oder Diktatszenarios. Wenn Sie die Spracherkennung für die Erkennung und Transkription in einer individuellen Umgebung verwenden, können Sie benutzerdefinierte Akustik-, Sprach- und Aussprachemodelle erstellen und trainieren. Anpassungen sind hilfreich für das Kompensieren von Umgebungsgeräuschen oder bei branchenspezifischem Vokabular.

> [!NOTE]
> Die Bing-Spracheingabe wurde am 15. Oktober 2019 eingestellt. Wenn Ihre Anwendungen, Tools oder Produkte die Bing-Spracheingabe-APIs oder Custom Speech verwenden, finden Sie in den nachfolgend aufgelisteten Leitfäden Informationen zur Migration zum Speech-Dienst.
> - [Migrieren von der Bing-Spracheingabe zum Speech-Dienst](how-to-migrate-from-bing-speech.md)
> - [Migrieren von Custom Speech zum Speech-Dienst](how-to-migrate-from-custom-speech-service.md)

## <a name="get-started-with-speech-to-text"></a>Erste Schritte mit der Spracherkennung

Der Spracherkennungsdienst ist über das [Speech SDK](speech-sdk.md) verfügbar. Es gibt mehrere häufige Szenarien, die als Schnellstarts für verschiedene Sprachen und Plattformen verfügbar sind:

 - [Schnellstart: Erkennen von Sprache mit Mikrofoneingabe](quickstarts/speech-to-text-from-microphone.md)
 - [Schnellstart: Erkennen von Sprache aus einer Datei](quickstarts/speech-to-text-from-file.md)
 - [Schnellstart: Erkennen von Sprache aus einem Blobspeicher](quickstarts/from-blob.md)

Wenn Sie den Spracherkennungs-REST-Dienst verwenden möchten, finden Sie weitere Informationen unter [REST-APIs](rest-speech-to-text.md).

## <a name="tutorials-and-sample-code"></a>Tutorials und Beispielcode

Nachdem Sie Gelegenheit hatten, den Speech-Dienst zu verwenden, erfahren Sie in unserem Tutorial, wie Sie mithilfe des Speech SDK und LUIS Absichten in gesprochener Sprache erkennen.

- [Tutorial: Erkennen von Absichten anhand von gesprochener Sprache mit dem Speech SDK und LUIS in C#](how-to-recognize-intents-from-speech-csharp.md)

Beispielcode für das Speech SDK finden Sie auf GitHub. In den Beispielen werden gängige Szenarios wie etwa das Lesen von Audiodaten aus einer Datei oder einem Stream, die kontinuierliche und einmalige Erkennung oder die Verwendung benutzerdefinierter Modelle behandelt.

- [Speech-to-text samples (SDK) (Spracherkennungsbeispiele (SDK))](https://github.com/Azure-Samples/cognitive-services-speech-sdk)
- [Batch transcription samples (REST) (Batchtranskriptionsbeispiele (REST))](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/samples/batch)

## <a name="customization"></a>Anpassung

Zusätzlich zum Standardmodell des Speech-Diensts können Sie auch benutzerdefinierte Modelle erstellen. Mithilfe von Anpassungen überwinden Sie Grenzen der Spracherkennung wie z. B. Sprachstil, Vokabular und Hintergrundgeräusche. Weitere Informationen finden Sie unter [Custom Speech](how-to-custom-speech.md). Die Anpassungsoptionen variieren je nach Sprache/Gebietsschema. Weitere Informationen zur Unterstützung erhalten Sie unter [Unterstützte Sprachen](supported-languages.md).

[!INCLUDE [speech-reference-doc-links](includes/speech-reference-doc-links.md)]

## <a name="next-steps"></a>Nächste Schritte

- [Kostenloses Testen des Speech-Diensts](get-started.md)
- [Abrufen des Speech SDK](speech-sdk.md)
