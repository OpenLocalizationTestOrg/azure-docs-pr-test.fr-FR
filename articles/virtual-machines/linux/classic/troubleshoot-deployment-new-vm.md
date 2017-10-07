---
title: "aaaTroubleshoot Linux VM déploiement classique | Documents Microsoft"
description: "Résoudre les problèmes de déploiement classiques lorsque vous créez une machine virtuelle Linux dans Azure"
services: virtual-machines-linux
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: c8a963fa-6b2a-4c7a-a1f4-7793adb02b19
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cjiang
ms.openlocfilehash: a642bfd9a543cd6d2104b03fe04193d9352ccae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>Résoudre les problèmes de déploiement classiques liés à la création d’une machine virtuelle Linux dans Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-selectors](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-selectors-include.md)]

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Pour la version de gestionnaire de ressources hello de cet article, consultez [ici](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>Collecter des journaux d’audit
toostart résolution des problèmes, d’audit de collecter hello consigne l’erreur de hello de tooidentify associé au problème de hello.

Bonjour portail Azure, cliquez sur **Parcourir** > **virtuels** > *votre machine Windows*  >   **Paramètres** > **journaux d’Audit**.

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**Y:** si hello du système d’exploitation est Linux généralisé et il est téléchargé et/ou capturé avec hello généralisé définissant, n’aura pas toutes les erreurs. De même, si hello du système d’exploitation est spécialisé de Linux, et il est téléchargé et/ou capturé avec hello spécialisée de paramètre, puis n’aura pas toutes les erreurs.

**Erreurs de téléchargement :**

**N<sup>1</sup>:** si hello du système d’exploitation est généralisé de Linux, et il est téléchargé en tant que spécialisé, vous obtiendrez une erreur de délai d’attente de configuration car hello machine virtuelle est bloqué au niveau de hello étape de configuration.

**N<sup>2</sup>:** si hello du système d’exploitation est spécialisé de Linux, et il est téléchargé comme généralisé, vous obtiendrez une erreur d’échec de la configuration, car la nouvelle machine virtuelle hello s’exécute avec le nom de l’ordinateur d’origine hello, nom d’utilisateur et mot de passe.

**Résolution :**

téléchargement de ces deux erreurs, tooresolve hello du disque dur virtuel d’origine, disponible localement, avec hello même configuration que celle pour hello du système d’exploitation (généralisé/spécialisé). tooupload comme généralisé, n’oubliez pas de toorun-tout d’abord annuler le déploiement. Consultez [créer et télécharger un disque dur virtuel que hello Contains système d’exploitation Linux](create-upload-vhd.md) pour plus d’informations.

**Erreurs de capture :**

**N<sup>3</sup>:** si hello du système d’exploitation est généralisé de Linux, et il est capturé en tant que spécialisé, vous obtiendrez une erreur de délai d’attente de configuration car hello original VM n’est pas utilisable car il est marqué comme généralisé.

**N<sup>4</sup>:** si hello du système d’exploitation est spécialisé de Linux, et elle est capturée comme généralisé, vous obtiendrez une erreur d’échec de la configuration, car la nouvelle machine virtuelle hello s’exécute avec le nom de l’ordinateur d’origine hello, nom d’utilisateur et mot de passe. En outre, hello original VM n’est pas utilisable car il est marqué comme spécialisé.

**Résolution :**

tooresolve les deux de ces erreurs, supprimez image actuelle de hello hello portail, et [acquérir à nouveau à partir de hello des disques durs virtuels en cours](capture-image.md) avec hello même configuration que celle pour hello du système d’exploitation (généralisé/spécifique).

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Problème : Image personnalisée / galerie / marketplace ; échec d’allocation
Cette erreur se produit dans les situations lors de la nouvelle demande de machine virtuelle hello est envoyé de cluster tooa qui soit n’a pas de demande de hello tooaccommodate d’espace libre, ou ne peut pas de prendre en charge la taille de machine virtuelle hello demandé. Il n’est pas possible de toomix différentes séries de machines virtuelles dans hello même service cloud. Par conséquent, si vous souhaitez toocreate une nouvelle machine virtuelle de taille différente à ce que votre service cloud peut prendre en charge, demande de calcul hello échoue.

Selon les contraintes du service de cloud hello hello que vous utilisez toocreate hello du nouvel ordinateur virtuel, vous pouvez rencontrer une erreur provoquée par une des deux situations.

**Cause 1 :** service de cloud computing hello est épinglé tooa spécifique du cluster, ou groupe d’affinités de tooan lié et donc épinglé tooa spécifique du cluster par conception. Afin de la nouvelle ressource de calcul des demandes de ce groupe d’affinités sont essayés dans hello où se trouvent les ressources existantes hello du même cluster. Toutefois, hello même cluster peut n’est pas prise en charge hello taille de machine virtuelle demandée ou ont manque d’espace, ce qui entraîne une erreur d’allocation. Cela est vrai si hello nouvelles ressources sont créées via un service cloud ou via un service cloud existant.

**Résolution 1 :**

* Créez un service cloud et associez-le à une région ou à un réseau virtuel basé sur une région.
* Créer une machine virtuelle dans le nouveau service de cloud hello.
  Si vous obtenez une erreur lors de la tentative de toocreate un nouveau service cloud, réessayez ultérieurement, ou modifier la région de hello pour le service cloud hello.

> [!IMPORTANT]
> Si vous essayiez toocreate une nouvelle machine virtuelle dans un service cloud existant, mais n’a pas pu et toocreate un nouveau service cloud pour votre nouvelle machine virtuelle, vous pouvez choisir tooconsolidate toutes vos machines virtuelles Bonjour même service cloud. toodo donc supprimer des machines virtuelles de hello dans le service cloud existant hello et recapturer les à partir de leurs disques dans le nouveau service de cloud hello. Toutefois, il est important tooremember nouveau service de cloud hello qu’un nouveau nom et l’adresse IP virtuelle, vous devez tooupdate ces valeurs pour toutes les dépendances de hello qui utilisent ces informations pour le service cloud existant hello.
> 
> 

**Cause 2 :** service de cloud computing hello est associé à un réseau virtuel qui est le groupe d’affinités de tooan lié, afin qu’il soit épinglé tooa spécifique du cluster par conception. Toutes les nouvelles demandes de ressources de calcul dans ce groupe d’affinités sont par conséquent essayés dans hello où se trouvent les ressources existantes hello du même cluster. Toutefois, hello même cluster peut n’est pas prise en charge hello taille de machine virtuelle demandée ou ont manque d’espace, ce qui entraîne une erreur d’allocation. Cela est vrai si hello nouvelles ressources sont créées via un service cloud ou via un service cloud existant.

**Résolution 2 :**

* Créez un réseau virtuel régional.
* Créer hello nouvelle machine virtuelle dans le réseau virtuel hello.
* [Se connecter à votre réseau virtuel existant](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) toohello de nouveau réseau virtuel. Pour plus d’informations, consultez [Réseaux virtuels régionaux](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/). Vous pouvez également [migrer votre réseau virtuel régional basée sur le groupe d’affinités de réseau virtuel tooa](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/), puis créez hello nouvelle machine virtuelle.

## <a name="next-steps"></a>Étapes suivantes
Si vous rencontrez des problèmes lorsque vous démarrez une machine virtuelle Linux arrêtée ou que vous redimensionnez une machine virtuelle Linux existante dans Azure, consultez [Résoudre les problèmes de déploiement classique liés au redémarrage ou au redimensionnement d’une machine virtuelle Linux existante dans Azure](restart-resize-error-troubleshooting.md).

