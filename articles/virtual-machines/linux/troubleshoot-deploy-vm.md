---
title: "aaaTroubleshoot déploiement des problèmes d’ordinateur virtuel Linux dans Azure | Documents Microsoft"
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
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a>Résolution des problèmes de déploiement de la machine virtuelle Linux dans Azure

problèmes de déploiement d’ordinateur virtuel (VM) tootroubleshoot dans Azure, passez en revue les hello [problèmes principaux](#top-issues) des défaillances et des solutions courantes.

Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure sur [hello forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/support/forums/). Vous pouvez également signaler un incident au support Azure. Accédez toohello [site de support technique Azure](https://azure.microsoft.com/support/options/) et sélectionnez **obtenir prend en charge**.

## <a name="top-issues"></a>Problèmes principaux
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a>cluster de Hello ne peut pas prendre en charge hello demandé la taille de machine virtuelle
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Réessayez la demande hello à l’aide d’une plus petite taille de machine virtuelle.
- Si hello taille Hello demandé de que machine virtuelle ne peut pas être modifié :
    - Arrêtez tous les ordinateurs virtuels de hello dans hello à haute disponibilité. Cliquez sur **Groupes de ressources** > votre groupe de ressources > **Ressources** > votre groupe à haute disponibilité > **Machines virtuelles** > votre machine virtuelle > **Arrêter**.
    - Une fois toutes les hello arrêt des machines virtuelles, créez des hello machine virtuelle de taille de hello souhaité.
    - Démarrer hello nouvelle machine virtuelle tout d’abord, puis sélectionnez chacun des hello s’est arrêté de machines virtuelles, puis cliquez sur Démarrer.


## <a name="hello-cluster-does-not-have-free-resources"></a>cluster de Hello n’a pas de libérer des ressources
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- Réessayez la demande de hello plus tard.
- Si hello nouvelle machine virtuelle peut être définie partie d’une haute disponibilité distincts
    - Créer une machine virtuelle dans un ensemble différent de disponibilité (Bonjour même région).
    - Ajouter hello nouvelle machine virtuelle toohello même réseau virtuel.

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a>Comment activer mon crédit mensuel pour Visual Studio Enterprise (BizSpark) ?

tooactivate votre mensuel de crédit, consultez ce [article](https://azure.microsoft.com/offers/ms-azr-0064p/).

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a>Pourquoi ne puis-je pas installer pilote GPU hello pour une machine virtuelle NV de Ubuntu ?

Actuellement, la prise en charge de GPU Linux est uniquement disponible sur les machines virtuelles NC Azure exécutant Ubuntu Server 16.04 LTS. Pour plus d’informations, consultez [Configuration des pilotes GPU NVIDIA pour les machines virtuelles séries N exécutant Linux](n-series-driver-setup.md).

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a>Il manque des pilotes sur ma machine virtuelle Linux série N

Les pilotes pour les machines virtuelles Linux se trouvent [ici](n-series-driver-setup.md). 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a>Impossible de trouver une instance GPU dans ma machine virtuelle Série N

avantage tootake hello GPU des fonctionnalités de machines virtuelles N-series Azure exécutant Windows Server 2016 ou Windows Server 2012 R2, vous devez installer les pilotes de graphiques NVIDIA sur chaque machine virtuelle après le déploiement. Des informations de configuration du pilote sont disponibles pour [les machines virtuelles Windows](../windows/n-series-driver-setup.md) et [les machines virtuelles Linux](n-series-driver-setup.md).

## <a name="is-n-series-vms-available-in-my-region"></a>Les machines virtuelles Séries N sont-elles disponibles dans ma région ?

Vous pouvez vérifier la disponibilité de hello de hello [produits disponibles par la table region](https://azure.microsoft.com/regions/services)et la tarification [ici](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a>Je ne suis pas famille de taille de machine virtuelle en mesure de toosee que je veux lors du redimensionnement de ma machine virtuelle.

Lorsqu’un ordinateur virtuel est en cours d’exécution, il est déployé tooa des serveurs physiques. Hello des serveurs physiques dans des régions Azure sont regroupés dans des clusters de matériel physique commun. Redimensionnement d’une machine virtuelle qui nécessite des clusters matériels de hello VM toobe déplacé toodifferent diffère selon le modèle de déploiement a été utilisé toodeploy hello machine virtuelle.

- Machines virtuelles déployées dans le modèle de déploiement classique, déploiement de service cloud hello doivent être supprimés et redéploiement taille de tooa toochange hello machines virtuelles dans une autre famille de taille.

- Machines virtuelles déployées dans le modèle de déploiement de gestionnaire de ressources, vous devez arrêter toutes les machines virtuelles hello groupe à haute disponibilité avant de modifier la taille de hello de n’importe quel ordinateur virtuel à haute disponibilité hello.

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a>Hello répertorié taille de machine virtuelle n'est pas pris en charge lors du déploiement de haute disponibilité.

Choisissez une taille qui est pris en charge sur le cluster de l’ensemble de disponibilité hello. Il est recommandé lorsque vous créez qu'un ensemble de disponibilité toochoose hello plus grande taille de machine virtuelle vous pensez que vous avez besoin et que vous avez être votre première toohello de déploiement à haute disponibilité.

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a>Quelles distributions/versions de Linux sont prises en charges par Azure ?

Vous trouverez la liste hello à Linux sur [Azure-Endorsed Distributions](endorsed-distros.md).

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a>Puis-je ajouter un ensemble de disponibilité tooan classique de machine virtuelle existant ?

Oui. Vous pouvez ajouter un tooa d’ordinateur virtuel classique existante nouvelle ou existante à haute disponibilité. Pour plus d’informations, consultez [ajouter un ensemble de disponibilité tooan machine virtuelle existante](../windows/classic/configure-availability.md#addmachine).


## <a name="next-steps"></a>Étapes suivantes
Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure sur [hello forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/support/forums/).

Vous pouvez également signaler un incident au support Azure. Accédez toohello [site de support technique Azure](https://azure.microsoft.com/support/options/) et sélectionnez **obtenir prend en charge**.
