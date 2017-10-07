---
title: aaaAzure exemples PowerShell de Machine virtuelle | Documents Microsoft
description: Exemples PowerShell pour les machines virtuelles Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 89fd26aa979687cdcdf9ae4e60be7d0d2eaeae91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-powershell-samples"></a>Exemples PowerShell pour les machines virtuelles Azure

Hello tableau suivant inclut des liens les exemples de scripts tooPowerShell que créer et gérer des machines virtuelles Windows.

| | |
|---|---|
|**Créer des machines virtuelles**||
| [Créer une machine virtuelle entièrement configurée](./../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crée un groupe de ressources, une machine virtuelle et toutes les ressources associées.|
| [Créer des machines virtuelles hautement disponibles](./../scripts/virtual-machines-windows-powershell-sample-create-nlb-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crée plusieurs machines virtuelles dans une configuration haute disponibilité avec équilibrage de charge.|
| [Créer une machine virtuelle et exécuter le script de configuration](./../scripts/virtual-machines-windows-powershell-sample-create-vm-iis.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crée une machine virtuelle et utilise l’extension tooinstall IIS de hello Azure un Script personnalisé. |
| [Créer une machine virtuelle et exécuter la configuration DSC](./../scripts/virtual-machines-windows-powershell-sample-create-iis-using-dsc.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crée une machine virtuelle et utilise tooinstall extension de Configuration d’état souhaité (DSC) Azure hello IIS. |
| [Charger un disque dur virtuel et créer des machines virtuelles](./../scripts/virtual-machines-windows-powershell-upload-generalized-script.md) | Uplaods un disque dur virtuel local tooAzure de fichiers, crée et de l’image à partir de disque dur virtuel de hello et crée ensuite une machine virtuelle à partir de cette image. |
| [Créer une machine virtuelle à partir d’un disque de système d’exploitation géré](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crée une machine virtuelle en attachant un disque géré existant en tant que disque de système d’exploitation. |
| [Créer une machine virtuelle à partir d’une capture instantanée](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crée un ordinateur virtuel à partir d’un instantané en créant d’abord un disque géré à partir de l’instantané, puis d’attacher de nouveau disque managé hello en tant que disque de système d’exploitation. |
|**Gérer le stockage**||
| [Créer un disque géré à partir d’un disque dur virtuel figurant dans le même abonnement ou dans un abonnement différent](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crée un disque géré à partir d’un disque dur virtuel spécialisé tel qu’un disque de système d’exploitation, ou d’un disque dur virtuel de données figurant dans le même abonnement ou dans un abonnement différent.  |
| [Créer un disque géré à partir d’une capture instantanée](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crée un disque géré à partir d’une capture instantanée. |
| [Copiez toosame de disque géré ou un autre abonnement](../scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Copies gérés disque toosame ou autre abonnement, mais dans hello même région que le parent de hello gérés disque. 
| [Exporter une capture instantanée en tant que compte de stockage de disque dur virtuel tooa](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-storage-account.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Exporte un instantané géré en tant que compte de stockage de disque dur virtuel tooa dans autre région. |
| [Créer une capture instantanée d’un disque dur virtuel](../scripts/virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crée instantané à partir d’un disque dur virtuel toocreate plusieurs disques gérés identiques à partir de l’instantané dans peu de temps.  |
| [Copie instantané toosame ou autre abonnement](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Copies instantané toosame ou un abonnement différent mais dans hello même région que l’instantané de hello parent. |
|**Sécuriser les machines virtuelles**||
| [Chiffrer une machine virtuelle et des disques de données](./../scripts/virtual-machines-windows-powershell-sample-encrypt-vm.md?toc=%2fpowershell%2fazure%2ftoc.json) | Crée une solution Key Vault, une clé de chiffrement et le principal de service, puis chiffre une machine virtuelle. |
|**Surveiller les machines virtuelles**||
| [Surveiller une machine virtuelle avec Operations Management Suite](./../scripts/virtual-machines-windows-powershell-sample-create-vm-oms.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Crée un ordinateur virtuel, installe l’agent de Operations Management Suite hello et inscrit hello machine virtuelle dans un espace de travail OMS.  |
| | |

