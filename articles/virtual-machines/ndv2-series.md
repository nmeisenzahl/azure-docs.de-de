---
title: 'NDv2-Serie: Azure Virtual Machines'
description: Spezifikationen für die VMs der NDv2-Serie
services: virtual-machines
author: vikancha
ms.service: virtual-machines
ms.topic: article
ms.date: 02/03/2020
ms.author: lahugh
ms.openlocfilehash: 1aa2a6402a58ba69a7b5999803bb10d48169a035
ms.sourcegitcommit: d45fd299815ee29ce65fd68fd5e0ecf774546a47
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/04/2020
ms.locfileid: "78267433"
---
# <a name="updated-ndv2-series-preview"></a>Aktualisierte NDv2-Serie (Vorschau)

Die VMs der NDv2-Serie sind ein neues Mitglied der GPU-Familie und darauf ausgelegt, die Anforderungen von besonders ressourcenintensiven Workloads zu erfüllen – beispielsweise KI-Workloads mit GPU-Beschleunigung, Machine Learning-, Simulations- und HPC-Workloads.

Die VMs der NDv2-Serie sind mit 8 NVIDIA Tesla V100-GPUs mit NVLINK-Bus ausgestattet und umfassen jeweils 32 GB an GPU-Arbeitsspeicher. Jede NDv2-VM verfügt außerdem über 40 Intel Xeon Platinum 8168-Kerne (Skylake) ohne Hyperthreading und 672 GiB an Systemarbeitsspeicher.

NDv2-Instanzen bieten dank CUDA GPU-optimierter Computekernel hervorragende Leistung für HPC- und KI-Workloads sowie für zahlreiche KI-, ML- und Analysetools mit integrierter Unterstützung der GPU-Beschleunigung. Dazu zählen beispielsweise TensorFlow, Pytorch, Caffe, RAPIDS und andere Frameworks.

Entscheidend ist, dass die NDv2-Serie sowohl auf rechenintensive Workloads zum zentralen Hochskalieren (mit 8 GPUs pro VM) als auch auf horizontale Skalierung (mit mehreren kombinierten VMs) ausgelegt ist. Die NDv2-Serie unterstützt ab sofort Back-End-Netzwerke mit InfiniBand EDR (100 Gigabit), ähnlich der Datenrate auf HPC-VMs der HB-Serie, und ermöglicht somit Hochleistungsclustering für parallele Szenarien, z. B. für ein verteiltes Training für KI und ML. Dieses Back-End-Netzwerk unterstützt alle wichtigen InfiniBand-Protokolle – einschließlich derer, die in den NCCL2-Bibliotheken von NDVIA verwendet werden. Dadurch ist ein nahtloses Clustering von GPUs möglich.


> [!NOTE]
> Bei [Aktivierung von InfiniBand](https://docs.microsoft.com/azure/virtual-machines/workloads/hpc/enable-infiniband) auf der ND40rs_v2-VM verwenden Sie bitte den Mellanox OFED-Treiber 4.7-1.0.0.1.
>
> Aufgrund des größeren GPU-Arbeitsspeichers werden für die neue ND40rs_v2-VM [VMs der 2. Generation](https://docs.microsoft.com/azure/virtual-machines/windows/generation-2) und Marketplace-Images benötigt. 
>
> [Registrieren Sie sich, um frühen Zugriff auf die Vorschauversion der NDv2-VM anzufordern.](https://aka.ms/AzureNDrv2Preview)
>
> Hinweis: Die ND40s_v2-VM mit 16 GB Arbeitsspeicher pro GPU ist nicht mehr als Vorschauversion verfügbar und wurde durch die aktualisierte ND40rs_v2-VM ersetzt.

<br>

Storage Premium  Unterstützt

Storage Premium-Zwischenspeicherung:  Unterstützt

Livemigration: Nicht unterstützt

Updates mit Speicherbeibehaltung: Nicht unterstützt

InfiniBand: Unterstützt

| Size | vCPU | Memory: GiB | Temporärer Speicher (SSD): GiB | GPU | GPU-Arbeitsspeicher: GiB | Max. Anzahl Datenträger | Maximaler Durchsatz des Datenträgers ohne Cache: IOPS/MBps | Max. Netzwerkbandbreite | Maximale Anzahl NICs |
|---|---|---|---|---|---|---|---|---|---|
| Standard_ND40rs_v2 | 40 | 672 | 2948 | 8 V100 32 GB (NVLink) | 16 | 32 | 80000/800 | 24.000 MBit/s | 8 |

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../includes/virtual-machines-common-sizes-table-defs.md)]

## <a name="supported-operating-systems-and-drivers"></a>Unterstützte Betriebssysteme und Treiber

Um die GPU-Funktionen von virtuellen Azure-Computern der N-Serie nutzen zu können, müssen NVIDIA-GPU-Treiber installiert werden.

Mit der [NVIDIA-GPU-Treibererweiterung](./extensions/hpccompute-gpu-windows.md) werden entsprechende NVIDIA-CUDA- oder GRID-Treiber auf einem virtuellen Computer der N-Serie installiert. Installieren oder verwalten Sie die Erweiterung mithilfe des Azure-Portals oder mit Tools wie Azure PowerShell oder Azure Resource Manager-Vorlagen. Informationen zu unterstützten Betriebssystemen und Bereitstellungsschritten finden Sie in der [Dokumentation zur NVIDIA-GPU-Treibererweiterung](./extensions/hpccompute-gpu-windows.md). Allgemeine Informationen zu VM-Erweiterungen finden Sie unter [Erweiterungen und Features für virtuelle Azure-Computer](./extensions/overview.md).

Wenn Sie NVIDIA-GPU-Treiber manuell installieren möchten, finden Sie Informationen zu unterstützten Betriebssystemen und Treibern sowie Schritte zur Installation und zur Überprüfung unter [Einrichten von GPU-Treibern der N-Serie für Windows](./windows/n-series-driver-setup.md) bzw. [Einrichten von GPU-Treibern der N-Serie für Linux](./linux/n-series-driver-setup.md).

## <a name="other-sizes"></a>Andere Größen

- [Allgemeiner Zweck](sizes-general.md)
- [Arbeitsspeicheroptimiert](sizes-memory.md)
- [Speicheroptimiert](sizes-storage.md)
- [GPU-optimiert](sizes-gpu.md)
- [High Performance Computing](sizes-hpc.md)
- [Vorherige Generationen](sizes-previous-gen.md)

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen dazu, wie Sie mit [Azure-Computeeinheiten (ACU)](acu.md) die Computeleistung von Azure-SKUs vergleichen können.
