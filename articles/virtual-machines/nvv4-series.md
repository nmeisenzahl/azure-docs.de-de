---
title: 'NVv4-Serie: Azure Virtual Machines'
description: Spezifikationen für die VMs der NVv4-Serie
services: virtual-machines
author: vikancha
ms.service: virtual-machines
ms.topic: article
ms.date: 02/03/2020
ms.author: lahugh
ms.openlocfilehash: 0295ed7d44d64fcc1aeb68e1beaa37987b177edb
ms.sourcegitcommit: d45fd299815ee29ce65fd68fd5e0ecf774546a47
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/04/2020
ms.locfileid: "78273846"
---
# <a name="nvv4-series"></a>NVv4-Serie 

Die virtuellen Computer der NVv4-Serie basieren auf GPUs vom Typ [AMD Radeon Instinct MI25](https://www.amd.com/en/products/professional-graphics/instinct-mi25) sowie auf CPUs vom Typ AMD EPYC 7V12 (Rome). Mit der NVv4-Serie führt Azure virtuelle Computer mit partiellen GPUs ein. Wählen Sie den virtuellen Computer mit der passenden Größe für GPU-beschleunigte Grafikanwendungen und virtuelle Desktops aus – angefangen bei einer Achtel-GPU mit 2 GiB Framepuffer bis hin zu einer vollständigen GPU mit 16 GiB Framepuffer. Von virtuellen Computern der NVv4-Serie wird derzeit nur das Windows-Gastbetriebssystem unterstützt.

<br>

Storage Premium  Unterstützt

Storage Premium-Zwischenspeicherung:  Unterstützt

Livemigration: Nicht unterstützt

Updates mit Speicherbeibehaltung: Nicht unterstützt

| Size | vCPU | Memory: GiB | Temporärer Speicher (SSD): GiB | GPU | GPU-Arbeitsspeicher: GiB | Max. Anzahl Datenträger | Maximale Anzahl NICs |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_NV4as_v4 |4 |14 |88 | 1/8 | 2 | 4 | 2 |
| Standard_NV8as_v4 |8 |28 |176 | 1/4 | 4 | 8 | 4 |
| Standard_NV16as_v4 |16 |56 |352 | 1/2 | 8 | 16 | 8 |
| Standard_NV32as_v4 |32 |112 |704 | 1 | 16 | 32 | 8 |

<sup>1</sup> Virtuelle Computer der NVv4-Serie verfügen über AMD-Technologie für gleichzeitiges Multithreading.

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../includes/virtual-machines-common-sizes-table-defs.md)]

## <a name="supported-operating-systems-and-drivers"></a>Unterstützte Betriebssysteme und Treiber

Um die GPU-Funktionen von virtuellen Computern der Azure NVv4-Serie unter Windows nutzen zu können, müssen AMD-GPU-Treiber installiert werden.

Für die manuelle Installation von AMD-GPU-Treibern finden Sie Informationen zu unterstützten Betriebssystemen, Treibern und Installation sowie Schritte zur Überprüfung unter [Einrichten von AMD-GPU-Treibern der N-Serie für Windows](./windows/n-series-amd-driver-setup.md).

## <a name="other-sizes"></a>Andere Größen

- [Allgemeiner Zweck](sizes-general.md)
- [Arbeitsspeicheroptimiert](sizes-memory.md)
- [Speicheroptimiert](sizes-storage.md)
- [GPU-optimiert](sizes-gpu.md)
- [High Performance Computing](sizes-hpc.md)
- [Vorherige Generationen](sizes-previous-gen.md)

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen dazu, wie Sie mit [Azure-Computeeinheiten (ACU)](acu.md) die Computeleistung von Azure-SKUs vergleichen können.
