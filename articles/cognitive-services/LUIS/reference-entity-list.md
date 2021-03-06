---
title: Entität vom Typ „List“ – LUIS
titleSuffix: Azure Cognitive Services
description: Listenentitäten stellen einen festen, abgeschlossenen Satz verwandter Wörter zusammen mit ihren Synonymen dar. LUIS ermittelt keine zusätzlichen Werte für Listenentitäten. Suchen Sie mithilfe des Empfehlungsfeatures nach Vorschlägen für neue Wörter basierend auf der aktuellen Liste.
services: cognitive-services
author: diberry
manager: nitinme
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: reference
ms.date: 11/11/2019
ms.author: diberry
ms.openlocfilehash: 4313a1d644750c0961298bbee3ae211946de360a
ms.sourcegitcommit: c38a1f55bed721aea4355a6d9289897a4ac769d2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2019
ms.locfileid: "74849767"
---
# <a name="list-entity"></a>Entität vom Typ „List“

Listenentitäten stellen einen festen, abgeschlossenen Satz verwandter Wörter zusammen mit ihren Synonymen dar. LUIS ermittelt keine zusätzlichen Werte für Listenentitäten. Suchen Sie mithilfe des Features **Empfehlen** nach Vorschlägen für neue Wörter basierend auf der aktuellen Liste. Wenn mehr als eine Listenentität mit demselben Wert vorhanden ist, wird in der Endpunktabfrage jede Entität zurückgegeben.

Eine Listenentität wird nicht maschinell gelernt. Sie stellt eine genaue Textübereinstimmung dar. LUIS kennzeichnet jede Übereinstimmung für ein Element in einer Liste in der Antwort als eine Entität.

**Diese Entität ist gut geeignet, wenn für die Textdaten Folgendes gilt**:

* Es handelt sich um einen bekannten Satz.
* Sie werden nicht oft geändert. Wenn Sie die Liste häufig ändern oder möchten, dass die Liste selbstständig erweitert wird, stellt eine einfache Entität, die um eine Begriffsliste erweitert wurde, eine bessere Wahl dar.
* Für den Satz werden die maximalen LUIS-[Grenzen](luis-boundaries.md) dieses Entitätstyps nicht überschritten.
* Der Text in der Äußerung ist eine exakte Übereinstimmung mit einem Synonym oder dem kanonischen Namen. LUIS verwendet die Liste über genaue Textübereinstimmungen hinaus nicht. Fuzzyübereinstimmungen, Nicht-Berücksichtigung der Groß- und Kleinschreibung, Wortstammerkennung, Pluralformen und andere Varianten lassen sich mit einer List-Entität nicht auflösen. Um Varianten zu behandeln, sollten Sie die Verwendung eines [Musters](reference-pattern-syntax.md#syntax-to-mark-optional-text-in-a-template-utterance) mit der optionalen Textsyntax in Erwägung ziehen.

![Entität vom Typ „List“](./media/luis-concept-entities/list-entity.png)

## <a name="example-json-to-import-into-list-entity"></a>JSON-Beispiel zum Importieren in die Entität vom Typ „List“

  Sie können Werte in eine vorhandene Entität vom Typ „List“ importieren, indem Sie das folgende JSON-Format verwenden:

  ```JSON
  [
      {
          "canonicalForm": "Blue",
          "list": [
              "navy",
              "royal",
              "baby"
          ]
      },
      {
          "canonicalForm": "Green",
          "list": [
              "kelly",
              "forest",
              "avacado"
          ]
      }
  ]
  ```

## <a name="example-json-response"></a>JSON-Beispielantwort

Angenommen, die App enthält die Liste `Cities`, die Variationen von Städtenamen einschließlich Ort des Flughafens (Sea-tac), Flughafencode (SEA), Postleitzahl (98101) und Vorwahl (206) ermöglicht.

|Listenelement|Elementsynonyme|
|---|---|
|`Seattle`|`sea-tac`, `sea`, `98101`, `206`, `+1` |
|`Paris`|`cdg`, `roissy`, `ory`, `75001`, `1`, `+33`|

`book 2 tickets to paris`

In der Äußerung oben wird das Wort `paris` dem Element Paris als Teil der Listenentität `Cities` zugeordnet. Die Listenentität findet Übereinstimmungen sowohl des normalisierten Elementnamens als auch der Synonyme des Elements.

#### <a name="v2-prediction-endpoint-responsetabv2"></a>[V2 – Antwort für Vorhersageendpunkt](#tab/V2)

```JSON
  "entities": [
    {
      "entity": "paris",
      "type": "Cities",
      "startIndex": 18,
      "endIndex": 22,
      "resolution": {
        "values": [
          "Paris"
        ]
      }
    }
  ]
```

#### <a name="v3-prediction-endpoint-responsetabv3"></a>[V3 – Antwort für Vorhersageendpunkt](#tab/V3)


Dies ist der JSON-Code, wenn `verbose=false` in der Abfragezeichenfolge festgelegt ist:

```json
"entities": {
    "Cities": [
        [
            "Paris"
        ]
    ]
}
```

Dies ist der JSON-Code, wenn `verbose=true` in der Abfragezeichenfolge festgelegt ist:

```json
"entities": {
    "Cities": [
        [
            "Paris"
        ]
    ],
    "$instance": {
        "Cities": [
            {
                "type": "Cities",
                "text": "paris",
                "startIndex": 18,
                "length": 5,
                "modelTypeId": 5,
                "modelType": "List Entity Extractor",
                "recognitionSources": [
                    "model"
                ]
            }
        ]
    }
}
```

* * *

|Datenobjekt|Name der Entität|Wert|
|--|--|--|
|Entität vom Typ „List“|`Cities`|`paris`|


## <a name="next-steps"></a>Nächste Schritte

In diesem [Tutorial](tutorial-list-entity.md) erfahren Sie, wie Sie eine **Listenentität** verwenden, um exakte Textübereinstimmungen aus einer Liste bekannter Elemente zu extrahieren.
