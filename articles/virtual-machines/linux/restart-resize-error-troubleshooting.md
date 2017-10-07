---
title: "aaaVM redémarrage ou redimensionnement de problèmes dans Azure | Documents Microsoft"
description: "Résoudre les problèmes de déploiement Resource Manager liés au redémarrage ou au redimensionnement d’une machine virtuelle Linux existante dans Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d9ff76b64b6646b04565eb93110759c4ebc858e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a>Résoudre les problèmes de déploiement liés au redémarrage ou au redimensionnement d’une machine virtuelle Linux existante dans Azure
Lorsque vous essayez de toostart une Machine virtuelle de Azure (VM) arrêté ou redimensionnez une machine virtuelle Azure existante, les erreurs courantes hello que vous rencontrez sont un échec d’allocation. Cette erreur se produit lorsque le cluster de hello ou la région n’a pas de ressources disponibles ou ne peut pas prise en charge hello demandée taille de machine virtuelle.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a>Collecte des journaux d’activité
toostart résolution des problèmes, activité hello collecter consigne l’erreur de hello de tooidentify associé au problème de hello. Hello suivant liens contiennent des informations détaillées sur les processus hello :

[Voir les opérations de déploiement](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Afficher l’activité des journaux toomanage Azure ressources](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a>Problème : erreur lors du démarrage d’une machine virtuelle arrêtée
Vous essayez de toostart une machine virtuelle arrêtée mais obtenez un échec d’allocation.

### <a name="cause"></a>Cause :
demande Hello toostart hello arrêté la machine virtuelle a toobe émise au cluster d’origine hello qui héberge le service de cloud computing hello. Toutefois, les clusters hello n’ont pas de demande de hello toofulfill disponible d’espace libre.

### <a name="resolution"></a>Résolution :
* Arrêter hello toutes les machines virtuelles dans la disponibilité de hello définir, puis redémarrer chaque machine virtuelle.
  
  1. Cliquez sur **Groupes de ressources** > *votre groupe de ressources* > **Ressources** > *votre groupe à haute disponibilité* > **Machines virtuelles** > *votre machine virtuelle* > **Arrêter**.
  2. Une fois toutes les hello arrêt des machines virtuelles, chacune des machines virtuelles de hello arrêté puis cliquez sur Démarrer.
* Relancez la demande de redémarrage de hello ultérieurement.

## <a name="issue-error-when-resizing-an-existing-vm"></a>Problème : erreur lors du redimensionnement d’une machine virtuelle existante
Vous essayez tooresize une machine virtuelle existante mais un échec d’allocation.

### <a name="cause"></a>Cause :
demande Hello tooresize hello machine virtuelle a toobe tentée au cluster d’origine de hello ce service de cloud hello hôtes. Toutefois, les clusters hello ne prend pas en charge hello demandé la taille de machine virtuelle.

### <a name="resolution"></a>Résolution :
* Réessayez la demande hello à l’aide d’une plus petite taille de machine virtuelle.
* Si hello taille Hello demandé de que machine virtuelle ne peut pas être modifié :
  
  1. Arrêtez tous les ordinateurs virtuels de hello dans hello à haute disponibilité.
     
     * Cliquez sur **Groupes de ressources** > *votre groupe de ressources* > **Ressources** > *votre groupe à haute disponibilité* > **Machines virtuelles** > *votre machine virtuelle* > **Arrêter**.
  2. Une fois toutes les hello arrêt des machines virtuelles, redimensionner hello souhaité VM tooa plus grande taille.
  3. Sélectionnez hello redimensionné la machine virtuelle et cliquez sur **Démarrer**, puis démarrez chaque hello a cessé de machines virtuelles.

## <a name="next-steps"></a>Étapes suivantes
Si vous rencontrez des problèmes lorsque vous créez une machine virtuelle Linux dans Azure, consultez [Résoudre les problèmes de déploiement liés à la création d’une machine virtuelle Linux dans Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

