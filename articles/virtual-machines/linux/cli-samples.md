---
title: "aaaAzure CLI échantillons | Documents Microsoft"
description: "Exemples d’interface de ligne de commande Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/08/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 776c947e6daca564242fc77b0527dcb124fa057d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-linux-virtual-machines"></a>Exemples d’interface de ligne de commande Azure pour machines virtuelles Linux

Hello tableau suivant inclut des liens toobash scripts créés à l’aide de hello CLI d’Azure.

| | |
|---|---|
|**Créer des machines virtuelles**||
| [Créer une machine virtuelle](./../scripts/virtual-machines-linux-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | Crée une machine virtuelle Linux avec une configuration minimale. |
| [Créer une machine virtuelle entièrement configurée](./../scripts/virtual-machines-linux-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | Crée un groupe de ressources, une machine virtuelle et toutes les ressources associées.|
| [Créer des machines virtuelles hautement disponibles](./../scripts/virtual-machines-linux-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | Crée plusieurs machines virtuelles dans une configuration haute disponibilité avec équilibrage de charge. |
| [Créer une machine virtuelle prenant en charge Docker](./../scripts/virtual-machines-linux-cli-sample-create-docker-host.md?toc=%2fcli%2fazure%2ftoc.json) | Crée une machine virtuelle, configure cette machine virtuelle en tant qu’hôte Docker et exécute un conteneur NGINX. |
| [Créer une machine virtuelle et exécuter le script de configuration](./../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md?toc=%2fcli%2fazure%2ftoc.json) | Crée une machine virtuelle et utilise l’extension tooinstall NGINX de hello Azure un Script personnalisé. |
| [Créer une machine virtuelle avec WordPress](./../scripts/virtual-machines-linux-cli-sample-create-vm-wordpress.md?toc=%2fcli%2fazure%2ftoc.json) | Crée une machine virtuelle et utilise l’extension tooinstall WordPress de hello Azure un Script personnalisé. |
| [Créer une machine virtuelle à partir d’un disque de système d’exploitation géré](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json) | Crée une machine virtuelle en attachant un disque géré existant en tant que disque de système d’exploitation. |
| [Créer une machine virtuelle à partir d’une capture instantanée](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | Crée un ordinateur virtuel à partir d’un instantané en créant d’abord un disque géré à partir de l’instantané, puis d’attacher de nouveau disque managé hello en tant que disque de système d’exploitation. |
|**Gérer le stockage**||
| [Créer un disque géré à partir d’un disque dur virtuel](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json) | Crée un disque géré à partir d’un disque dur virtuel spécialisé en tant que disque du système d’exploitation ou d’un disque dur virtuel de données en tant que disque de données.  |
| [Créer un disque géré à partir d’une capture instantanée](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | Crée un disque géré à partir d’une capture instantanée. |
| [Copiez toosame de disque géré ou un autre abonnement](../scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Copies gérés disque toosame ou autre abonnement, mais dans hello même région que le parent de hello gérés disque. 
| [Exporter une capture instantanée en tant que compte de stockage de disque dur virtuel tooa](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-storage-account.md?toc=%2fcli%2fmodule%2ftoc.json) | Exporte un instantané géré en tant que compte de stockage de disque dur virtuel tooa dans autre région. |
| [Copie instantané toosame ou autre abonnement](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Copies instantané toosame ou un abonnement différent mais dans hello même région que l’instantané de hello parent. |
|**Mettre en réseau des machines virtuelles**||
| [Sécuriser le trafic réseau entre les machines virtuelles](./../scripts/virtual-machines-linux-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | Crée deux machines virtuelles, toutes les ressources associées, ainsi qu’un groupe de sécurité réseau interne et un groupe de sécurité réseau externe. |
|**Sécuriser les machines virtuelles**||
| [Chiffrer une machine virtuelle et des disques de données](./../scripts/virtual-machines-linux-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | Crée une solution Key Vault, une clé de chiffrement et le principal de service, puis chiffre une machine virtuelle. |
|**Surveiller les machines virtuelles**||
| [Surveiller une machine virtuelle avec Operations Management Suite](./../scripts/virtual-machines-linux-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | Crée un ordinateur virtuel, installe l’agent de Operations Management Suite hello et inscrit hello machine virtuelle dans un espace de travail OMS.  |
|**Résoudre les problèmes liés aux machines virtuelles**||
| [Résoudre les problèmes liés au disque du système d’exploitation de machines virtuelles](./../scripts/virtual-machines-linux-cli-sample-mount-os-disk.md?toc=%2fcli%2fazure%2ftoc.json) | Monte le disque du système d’exploitation hello à partir d’une machine virtuelle comme disque de données sur une deuxième machine virtuelle. |
| | |
