---
title: "Résolution des problèmes de déploiement de la machine virtuelle Linux dans Azure | Microsoft Docs"
description: "Résolution des problèmes de déploiement de la machine virtuelle Linux dans le modèle de déploiement d’Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/03/2017
ms.author: genli
ms.openlocfilehash: 3d0e9a43d9a3c9c770c4ab6159279db1d93f5134
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a>Résolution des problèmes de déploiement de la machine virtuelle Linux dans Azure

Pour résoudre les problèmes de déploiement de la machine virtuelle (VM) dans Azure, passez en revue les [problèmes principaux](#top-issues) pour voir les erreurs courantes et les solutions.

Si vous avez besoin d’une aide supplémentaire à quelque étape que ce soit dans cet article, vous pouvez contacter les experts Azure sur les [forums MSDN Azure et Stack Overflow](https://azure.microsoft.com/support/forums/). Vous pouvez également signaler un incident au support Azure. Accédez au [site du support Azure](https://azure.microsoft.com/support/options/) , puis cliquez sur **Obtenir un support**.

## <a name="top-issues"></a>Problèmes principaux
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="the-cluster-cannot-support-the-requested-vm-size"></a>Le cluster ne peut pas prendre en charge la taille de machine virtuelle demandée
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Relancez la requête en utilisant une taille inférieure pour la machine virtuelle.
- Si la taille de la machine virtuelle requise ne peut pas être modifiée :
    - Arrêtez toutes les machines virtuelles dans le groupe à haute disponibilité. Cliquez sur **Groupes de ressources** > votre groupe de ressources > **Ressources** > votre groupe à haute disponibilité > **Machines virtuelles** > votre machine virtuelle > **Arrêter**.
    - Une fois que toutes les machines virtuelles sont arrêtées, créez une machine virtuelle à la taille souhaitée.
    - Démarrez la nouvelle machine virtuelle en premier, puis sélectionnez chacune des machines virtuelles arrêtées et cliquez sur Démarrer.


## <a name="the-cluster-does-not-have-free-resources"></a>Le cluster n’a pas de ressources libres
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Relancez la requête ultérieurement.
- Si la nouvelle machine virtuelle peut faire partie d’un autre groupe à haute disponibilité
    - Créez une machine virtuelle dans un autre groupe à haute disponibilité (dans la même région).
    - Ajoutez la nouvelle machine virtuelle au même réseau virtuel.

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a>Comment activer mon crédit mensuel pour Visual Studio Enterprise (BizSpark) ?

Pour activer votre crédit mensuel, consultez cet [article](https://azure.microsoft.com/offers/ms-azr-0064p/).

## <a name="why-can-i-not-install-the-gpu-driver-for-an-ubuntu-nv-vm"></a>Pourquoi ne puis-je pas installer le pilote du GPU sur une machine virtuelle Ubuntu NV ?

Actuellement, la prise en charge de GPU Linux est uniquement disponible sur les machines virtuelles NC Azure exécutant Ubuntu Server 16.04 LTS. Pour plus d’informations, consultez [Configuration des pilotes GPU NVIDIA pour les machines virtuelles séries N exécutant Linux](n-series-driver-setup.md).

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a>Il manque des pilotes sur ma machine virtuelle Linux série N

Les pilotes pour les machines virtuelles Linux se trouvent [ici](n-series-driver-setup.md). 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a>Impossible de trouver une instance GPU dans ma machine virtuelle série N

Pour tirer parti des fonctionnalités GPU des machines virtuelles série N Azure exécutant Windows Server 2016 ou Windows Server 2012 R2, vous devez installer des pilotes graphiques NVIDIA sur chaque machine virtuelle après le déploiement. Des informations de configuration du pilote sont disponibles pour [les machines virtuelles Windows](../windows/n-series-driver-setup.md) et [les machines virtuelles Linux](n-series-driver-setup.md).

## <a name="is-n-series-vms-available-in-my-region"></a>Les machines virtuelles Séries N sont-elles disponibles dans ma région ?

Vous pouvez vérifier la disponibilité à l’aide de la [Table des produits disponibles par région](https://azure.microsoft.com/regions/services) ainsi que les tarifications [ici](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).

## <a name="i-am-not-able-to-see-vm-size-family-that-i-want-when-resizing-my-vm"></a>Impossible de voir les différentes familles de taille de machines virtuelles quand je redimensionne ma machine virtuelle.

Lorsqu’un ordinateur virtuel est en cours d’exécution, il est déployé sur un serveur physique. Les serveurs physiques dans les régions Azure sont regroupés dans des clusters de matériel physique commun. La méthode pour redimensionner une machine virtuelle qui doit être transférée vers différents clusters de matériel physique peut varier en fonction du modèle de déploiement utilisé pour déployer la machine virtuelle.

- Si les machines virtuelles sont déployées à partir d’un modèle de déploiement classique, le déploiement du service cloud doit être supprimé et redéployé afin de changer la taille de la machine virtuelle pour une autre famille de taille.

- Si les machines virtuelles sont déployées à partir du modèle de déploiement Resource Manager, vous devez arrêter toutes les machines virtuelles dans le groupe à haute disponibilité avant de changer la taille d’une machine dans le groupe à haute disponibilité.

## <a name="the-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a>La taille de machine virtuelle répertoriée n’est pas prise en charge lors du déploiement dans le groupe à haute disponibilité.

Choisissez une taille prise en charge par le cluster du groupe à haute disponibilité. Lors de la création d’un groupe à haute disponibilité, il est recommandé de choisir la plus grande taille de machine virtuelle dont vous pensez avoir besoin. Ce sera votre premier déploiement dans le groupe à haute disponibilité.

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a>Quelles distributions/versions de Linux sont prises en charges par Azure ?

Vous pouvez trouver la liste sur Linux sur [Distributions prises en charge par Azure](endorsed-distros.md).

## <a name="can-i-add-an-existing-classic-vm-to-an-availability-set"></a>Est-il possible d’ajouter une machine virtuelle classique à un groupe à haute disponibilité ?

Oui. Vous pouvez ajouter une machine virtuelle classique existante à un nouveau groupe ou à un groupe à haute disponibilité déjà existant. Pour plus d’informations, consultez [Ajouter une machine virtuelle existante à un groupe à haute disponibilité](../windows/classic/configure-availability-classic.md#addmachine).


## <a name="next-steps"></a>étapes suivantes
Si vous avez besoin d’une aide supplémentaire à quelque étape que ce soit dans cet article, vous pouvez contacter les experts Azure sur les [forums MSDN Azure et Stack Overflow](https://azure.microsoft.com/support/forums/).

Vous pouvez également signaler un incident au support Azure. Accédez au [site du support Azure](https://azure.microsoft.com/support/options/) , puis cliquez sur **Obtenir un support**.
