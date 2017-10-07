---
title: "déploiement de machine virtuelle Windows dans Windows Azure d’aaaTroubleshoot | Documents Microsoft"
description: "Résoudre les problèmes de déploiement de Resource Manager lors de la création d’une machine virtuelle Windows dans Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: afc6c1a4-2769-41f6-bbf9-76f9f23bcdf4
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c27d4f63b67db2d1c9f117f05a2eba9ef130ef37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-when-creating-a-new-windows-vm-in-azure"></a>Résoudre les problèmes de déploiement lors de la création d’une machine virtuelle Windows dans Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a>Problèmes principaux
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

Pour toute autre question ou problème concernant le déploiement de machine virtuelle, consultez [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md) (Résolution des problèmes de déploiement de la machine virtuelle Linux dans Azure).

## <a name="collect-activity-logs"></a>Collecte des journaux d’activité
toostart résolution des problèmes, activité hello collecter consigne l’erreur de hello de tooidentify associé au problème de hello. Hello liens suivants contiennent des informations détaillées sur hello processus toofollow.

[Voir les opérations de déploiement](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Afficher l’activité des journaux toomanage Azure ressources](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

**Y:** si hello du système d’exploitation est Windows généralisé et il est téléchargé et/ou capturé avec hello généralisé définissant, n’aura pas toutes les erreurs. De même, si hello du système d’exploitation est Windows spécialisé, et il est téléchargé et/ou capturé avec hello spécialisée de paramètre, puis n’aura pas toutes les erreurs.

**Erreurs de téléchargement :**

**N<sup>1</sup>:** si hello du système d’exploitation est Windows généralisé, et il est téléchargé en tant que spécialisé, vous obtiendrez une erreur de délai d’attente de configuration avec hello VM bloqué au niveau de l’écran OOBE hello.

**N<sup>2</sup>:** si hello du système d’exploitation est Windows spécialisé, et il est téléchargé comme généralisé, vous obtiendrez une erreur d’échec approvisionnement par hello VM bloqué au niveau de l’écran OOBE hello car hello nouvel ordinateur virtuel est en cours d’exécution avec l’ordinateur d’origine de hello nom, nom d’utilisateur et mot de passe.

**Résolution :**

l’utilisation de ces deux erreurs, tooresolve [Add-AzureRmVhd tooupload hello disque dur virtuel d’origine](https://msdn.microsoft.com/library/mt603554.aspx), disponible localement, avec hello même paramètre que celui pour hello du système d’exploitation (généralisé/spécifique). tooupload comme généralisé, n’oubliez pas tout d’abord toorun sysprep.

**Erreurs de capture :**

**N<sup>3</sup>:** si hello du système d’exploitation est Windows généralisé, et il est capturé en tant que spécialisé, vous obtiendrez une erreur de délai d’attente de configuration car hello original VM n’est pas utilisable car il est marqué comme généralisé.

**N<sup>4</sup>:** si hello du système d’exploitation est spécialisé de Windows, et elle est capturée comme généralisé, vous obtiendrez une erreur d’échec de la configuration, car la nouvelle machine virtuelle hello s’exécute avec le nom de l’ordinateur d’origine hello, nom d’utilisateur et mot de passe. En outre, hello original VM n’est pas utilisable car il est marqué comme spécialisé.

**Résolution :**

tooresolve les deux de ces erreurs, supprimez image actuelle de hello hello portail, et [acquérir à nouveau à partir de hello des disques durs virtuels en cours](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avec hello même configuration que celle pour hello du système d’exploitation (généralisé/spécifique).

## <a name="issue-customgallerymarketplace-image-allocation-failure"></a>Problème : image personnalisée/de la galerie/de la Place de marché ; échec d’allocation
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
Si vous rencontrez des problèmes lorsque vous démarrez une machine virtuelle Windows arrêtée ou que vous redimensionnez Windows une machine virtuelle existante dans Azure, consultez [Résoudre les problèmes de déploiement Resource Manager liés au redémarrage ou au redimensionnement d’une machine virtuelle Windows existante dans Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

