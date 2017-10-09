---
title: "aaaVM le redémarrage ou redimensionnement | Documents Microsoft"
description: "Résoudre les problèmes de déploiement classiques liés au redémarrage ou au redimensionnement d’une machine virtuelle Linux existante dans Azure"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 73f2672c-602e-4766-8948-2b180115d299
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: fb1dc88bb1b83043c434590118bc8810ad402872
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a>Résoudre les problèmes de déploiement classiques liés au redémarrage ou au redimensionnement d’une machine virtuelle Linux existante dans Azure
> [!div class="op_single_selector"]
> * [Classique](restart-resize-error-troubleshooting.md)
> * [Gestionnaire de ressources](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

Lorsque vous essayez de toostart une Machine virtuelle de Azure (VM) arrêté ou redimensionnez une machine virtuelle Azure existante, les erreurs courantes hello que vous rencontrez sont un échec d’allocation. Cette erreur se produit lorsque le cluster de hello ou la région n’a pas de ressources disponibles ou ne peut pas prise en charge hello demandée taille de machine virtuelle.

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Pour la version du Gestionnaire de ressources hello, consultez [ici](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>Collecter des journaux d’audit
toostart résolution des problèmes, d’audit de collecter hello consigne l’erreur de hello de tooidentify associé au problème de hello.

Bonjour portail Azure, cliquez sur **Parcourir** > **virtuels** > *votre machine virtuelle de Linux*  >   **Paramètres** > **journaux d’Audit**.

## <a name="issue-error-when-starting-a-stopped-vm"></a>Problème : erreur lors du démarrage d’une machine virtuelle arrêtée
Vous essayez de toostart une machine virtuelle arrêtée mais obtenez un échec d’allocation.

### <a name="cause"></a>Cause :
demande Hello toostart hello arrêté la machine virtuelle a toobe émise au cluster d’origine hello qui héberge le service de cloud computing hello. Toutefois, les clusters hello n’ont pas de demande de hello toofulfill disponible d’espace libre.

### <a name="resolution"></a>Résolution :
* Créez un service cloud et associez-le à une région ou à un réseau virtuel basé sur une région, mais non à un groupe d’affinités.
* Supprimer hello arrêté la machine virtuelle.
* Recréez hello machine virtuelle dans le nouveau service de cloud hello en utilisant des disques hello.
* Démarrer hello recréé la machine virtuelle.

Si vous obtenez une erreur lors de la tentative de toocreate un nouveau service cloud, réessayez ultérieurement, ou modifier la région de hello pour le service cloud hello.

> [!IMPORTANT]
> nouveau service de cloud Hello aura un nouveau nom et l’adresse IP virtuelle, vous devez toochange ces informations pour toutes les dépendances de hello qui utilisent ces informations pour le service cloud existant hello.
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a>Problème : erreur lors du redimensionnement d’une machine virtuelle existante
Vous essayez tooresize une machine virtuelle existante mais un échec d’allocation.

### <a name="cause"></a>Cause :
demande Hello tooresize hello machine virtuelle a toobe tentée au cluster d’origine de hello ce service de cloud hello hôtes. Toutefois, les clusters hello ne prend pas en charge hello demandé la taille de machine virtuelle.

### <a name="resolution"></a>Résolution :
Réduire hello demandé la taille de machine virtuelle et réessayer hello redimensionner la demande.

* Cliquez sur **Parcourir tout** > **Machines virtuelles (classiques)** > *votre machine virtuelle* > **Paramètres** > **Taille**. Pour des instructions détaillées, consultez [redimensionnement de la machine virtuelle de hello](https://msdn.microsoft.com/library/dn168976.aspx).

Si elle n’est pas possible de tooreduce hello taille de machine virtuelle, procédez comme suit :

* Créer un nouveau service cloud, en veillant à ce qu’il n’est pas lié tooan affinité du groupe et non associé à un réseau virtuel qui est le groupe d’affinités de tooan lié.
* Créez dans ce service une machine virtuelle plus volumineuse.

Vous pouvez consolider toutes vos machines virtuelles Bonjour même service cloud. Si votre service cloud existant est associé à un réseau virtuel en fonction de la région, vous pouvez vous connecter hello nouveau cloud service toohello réseau virtuel existant.

Si le service cloud existant hello n’est pas associé à un réseau virtuel en fonction de la région, puis vous avez toodelete hello machines virtuelles dans le service cloud existant hello et les recréez dans le nouveau service de cloud hello à partir de leurs disques. Toutefois, il est important tooremember nouveau service de cloud hello qu’un nouveau nom et l’adresse IP virtuelle, vous devez tooupdate ces valeurs pour toutes les dépendances de hello qui utilisent ces informations pour le service cloud existant hello.

## <a name="next-steps"></a>Étapes suivantes
Si vous rencontrez des problèmes lorsque vous créez une machine virtuelle Linux dans Azure, consultez [Résoudre les problèmes de déploiement liés à la création d’une machine virtuelle Linux dans Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

