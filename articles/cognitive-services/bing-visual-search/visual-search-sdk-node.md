---
title: 'Schnellstart: Gewinnen von Erkenntnissen zu Bildern mit dem SDK für Node.js – Visuelle Bing-Suche'
titleSuffix: Azure Cognitive Services
description: Verwenden Sie diese Schnellstartanleitung, um über den Dienst für die visuelle Bing-Suche mithilfe des Node.js SDK Erkenntnisse zu Bildern zu gewinnen.
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: bing-visual-search
ms.topic: quickstart
ms.date: 12/17/2019
ms.author: aahi
ms.openlocfilehash: d99aa2d2827716b2b04d059e47d9768eef8cd690
ms.sourcegitcommit: 98a5a6765da081e7f294d3cb19c1357d10ca333f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2020
ms.locfileid: "77485096"
---
# <a name="quickstart-get-image-insights-using-the-bing-visual-search-sdk-for-nodejs"></a>Schnellstart: Gewinnen von Erkenntnissen zu Bildern mit dem SDK für die visuelle Bing-Suche für Node.js

Verwenden Sie diese Schnellstartanleitung, um über den Dienst für die visuelle Bing-Suche mithilfe des Node.js SDK Erkenntnisse zu Bildern zu gewinnen. Die visuelle Bing-Suche verfügt zwar über eine REST-API, die mit den meisten Programmiersprachen kompatibel ist, aber das SDK ist eine einfache Möglichkeit, den Dienst in Ihre Anwendungen zu integrieren. Den Quellcode für dieses Beispiel finden Sie auf [GitHub](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples/blob/master/Samples/visualSearch.js). 

## <a name="prerequisites"></a>Voraussetzungen
* [Node.js](https://www.nodejs.org/)
* Das SDK für die visuelle Bing-Suche für Node.js
    * Führen Sie die folgenden Befehle aus, um eine Konsolenanwendung mit dem SDK für die visuelle Bing-Suche einzurichten:
        1. `npm install ms-rest-azure`
        2. `npm install azure-cognitiveservices-visualsearch`.


[!INCLUDE [cognitive-services-bing-visual-search-signup-requirements](../../../includes/cognitive-services-bing-visual-search-signup-requirements.md)]

<a name="client"></a>

## <a name="create-and-initialize-the-application"></a>Erstellen und Initialisieren der Anwendung

1. Erstellen Sie eine neue JavaScript-Datei in Ihrer bevorzugten IDE oder Ihrem bevorzugten Editor, und fügen Sie die folgenden Anforderungen hinzu. Dann erstellen Sie Variablen für Ihren Abonnementschlüssel, die benutzerdefinierte Konfigurations-ID und den Dateipfad zu dem Bild, das Sie hochladen möchten. 

    ```javascript
    const os = require("os");
    const async = require('async');
    const fs = require('fs');
    const Search = require('azure-cognitiveservices-visualsearch');
    const CognitiveServicesCredentials = require('ms-rest-azure').CognitiveServicesCredentials;
    
    let keyVar = 'YOUR-VISUAL-SEARCH-ACCESS-KEY';
    let credentials = new CognitiveServicesCredentials(keyVar);
    let filePath = "../Data/image.jpg";
    ```

2. Instanziieren Sie den Client.

    ```javascript
    let visualSearchClient = new Search.VisualSearchClient(credentials);
    ```

## <a name="search-for-images"></a>Suchen nach Bildern

1. Verwenden Sie `fs.createReadStream()`, um die Bilddatei einzulesen, und erstellen Sie Variablen für die Suchanforderung und die Ergebnisse. Dann verwenden Sie den Client, um nach Bildern zu suchen.

    ```javascript
    let fileStream = fs.createReadStream(filePath);
    let visualSearchRequest = JSON.stringify({});
    let visualSearchResults;
    try {
        visualSearchResults = await visualSearchClient.images.visualSearch({
            image: fileStream,
            knowledgeRequest: visualSearchRequest
        });
        console.log("Search visual search request with binary of image");
    } catch (err) {
        console.log("Encountered exception. " + err.message);
    }
    ```

2. Analysieren Sie die Ergebnisse der vorherigen Abfrage:

    ```javascript
    // Visual Search results
    if (visualSearchResults.image.imageInsightsToken) {
        console.log(`Uploaded image insights token: ${visualSearchResults.image.imageInsightsToken}`);
    }
    else {
        console.log("Couldn't find image insights token!");
    }
    
    // List of tags
    if (visualSearchResults.tags.length > 0) {
        let firstTagResult = visualSearchResults.tags[0];
        console.log(`Visual search tag count: ${visualSearchResults.tags.length}`);
    
        // List of actions in first tag
        if (firstTagResult.actions.length > 0) {
            let firstActionResult = firstTagResult.actions[0];
            console.log(`First tag action count: ${firstTagResult.actions.length}`);
            console.log(`First tag action type: ${firstActionResult.actionType}`);
        }
        else {
            console.log("Couldn't find tag actions!");
        }
    
    }
    else {
        console.log("Couldn't find image tags!");
    }
    
    ```

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Erstellen einer Einzelseiten-Web-App](tutorial-bing-visual-search-single-page-app.md)
