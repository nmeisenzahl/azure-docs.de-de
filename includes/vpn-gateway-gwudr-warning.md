---
title: include file
description: include file
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 09/28/2019
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: a852807ab685e85b76d26e5b39c99a32f645bbd7
ms.sourcegitcommit: 15e3bfbde9d0d7ad00b5d186867ec933c60cebe6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/03/2019
ms.locfileid: "71838159"
---
Benutzerdefinierte Routen mit einem 0.0.0.0/0-Ziel und NSGs im Gatewaysubnetz-**werden nicht unterstützt**. Die Erstellung von Gateways mit dieser Konfiguration wird blockiert. Gateways benötigen für die ordnungsgemäße Funktion Zugriff auf die Verwaltungscontroller.
