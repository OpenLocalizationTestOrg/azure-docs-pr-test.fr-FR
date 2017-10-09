---
title: "aaaTroubleshoot Linux VM déploiement-RM | Documents Microsoft"
description: "Résoudre les problèmes de déploiement Resource Manager liés à la création d’une machine virtuelle Linux dans Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>Résoudre les problèmes de déploiement Resource Manager liés à la création d’une machine virtuelle Linux dans Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a>Problèmes principaux
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

Pour toute autre question ou problèmes concernant le déploiement de machine virtuelle, consultez [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md) (Résolution des problèmes de déploiement de la machine virtuelle Linux dans Azure).
## <a name="collect-activity-logs"></a>Collecte des journaux d’activité
toostart résolution des problèmes, activité hello collecter consigne l’erreur de hello de tooidentify associé au problème de hello. Hello liens suivants contiennent des informations détaillées sur hello processus toofollow.

[Voir les opérations de déploiement](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Afficher l’activité des journaux toomanage Azure ressources](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**Y:** si hello du système d’exploitation est Linux généralisé et il est téléchargé et/ou capturé avec hello généralisé définissant, n’aura pas toutes les erreurs. De même, si hello du système d’exploitation est spécialisé de Linux, et il est téléchargé et/ou capturé avec hello spécialisée de paramètre, puis n’aura pas toutes les erreurs.

**Erreurs de téléchargement :**

**N<sup>1</sup>:** si hello du système d’exploitation est généralisé de Linux, et il est téléchargé en tant que spécialisé, vous obtiendrez une erreur de délai d’attente de configuration car hello machine virtuelle est bloqué au niveau de hello étape de configuration.

**N<sup>2</sup>:** si hello du système d’exploitation est spécialisé de Linux, et il est téléchargé comme généralisé, vous obtiendrez une erreur d’échec de la configuration, car la nouvelle machine virtuelle hello s’exécute avec le nom de l’ordinateur d’origine hello, nom d’utilisateur et mot de passe.

**Résolution :**

téléchargement de ces deux erreurs, tooresolve hello du disque dur virtuel d’origine, disponible localement, avec hello même configuration que celle pour hello du système d’exploitation (généralisé/spécialisé). tooupload comme généralisé, n’oubliez pas de toorun-tout d’abord annuler le déploiement.

**Erreurs de capture :**

**N<sup>3</sup>:** si hello du système d’exploitation est généralisé de Linux, et il est capturé en tant que spécialisé, vous obtiendrez une erreur de délai d’attente de configuration car hello original VM n’est pas utilisable car il est marqué comme généralisé.

**N<sup>4</sup>:** si hello du système d’exploitation est spécialisé de Linux, et elle est capturée comme généralisé, vous obtiendrez une erreur d’échec de la configuration, car la nouvelle machine virtuelle hello s’exécute avec le nom de l’ordinateur d’origine hello, nom d’utilisateur et mot de passe. En outre, hello original VM n’est pas utilisable car il est marqué comme spécialisé.

**Résolution :**

tooresolve les deux de ces erreurs, supprimez image actuelle de hello hello portail, et [acquérir à nouveau à partir de hello des disques durs virtuels en cours](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) avec hello même configuration que celle pour hello du système d’exploitation (généralisé/spécifique).

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Problème : Image personnalisée / galerie / marketplace ; échec d’allocation
Cette erreur se produit dans les situations lors de la nouvelle demande de machine virtuelle hello est cluster tooa épinglé qui ne peut pas de prendre en charge la taille de machine virtuelle hello demandé, ou n’a pas de demande de hello tooaccommodate d’espace libre.

**Cause 1 :** prend en charge les clusters hello hello demandé la taille de machine virtuelle.

**Résolution 1 :**

* Réessayez la demande hello à l’aide d’une plus petite taille de machine virtuelle.
* Si hello taille Hello demandé de que machine virtuelle ne peut pas être modifié :
  * Arrêtez tous les ordinateurs virtuels de hello dans hello à haute disponibilité.
    Cliquez sur **Groupes de ressources** > *votre groupe de ressources* > **Ressources** > *votre groupe à haute disponibilité* > **Machines virtuelles** > *votre machine virtuelle* > **Arrêter**.
  * Une fois que tous les hello arrêt des machines virtuelles, créer hello taille de machine virtuelle Bonjour souhaitée.
  * Démarrer hello nouvelle machine virtuelle tout d’abord, puis sélectionnez chacun des hello a cessé de machines virtuelles et cliquez sur **Démarrer**.

**Cause 2 :** cluster de hello n’a pas de libérer des ressources.

**Résolution 2 :**

* Réessayez la demande de hello ultérieurement.
* Si hello nouvelle machine virtuelle peut être définie partie d’une haute disponibilité distincts
  * Créer une machine virtuelle dans un ensemble différent de disponibilité (Bonjour même région).
  * Ajouter hello nouvelle machine virtuelle toohello même réseau virtuel.

## <a name="next-steps"></a>Étapes suivantes
Si vous rencontrez des problèmes lorsque vous démarrez une machine virtuelle Linux arrêtée ou que vous redimensionnez une machine virtuelle Linux existante dans Azure, consultez [Résoudre les problèmes de déploiement Resource Manager liés au redémarrage ou au redimensionnement d’une machine virtuelle Linux existante dans Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

