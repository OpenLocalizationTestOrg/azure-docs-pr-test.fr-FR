---
title: aaaMove un VM Linux dans Azure | Documents Microsoft
description: "Déplacer un Linux VM tooanother abonnement Azure ou un groupe de ressources dans le modèle de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 938d04234059111912f03e72d14dabd338bc0678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a>Déplacer un groupe d’abonnement ou une ressource de tooanother Linux VM
Cet article vous guide toomove un VM Linux entre les groupes de ressources ou des abonnements. Déplacer un ordinateur virtuel entre des abonnements peut être pratique si vous avez créé une machine virtuelle dans un abonnement personnel, vous souhaitez toomove il abonnement tooyour société.

> [!IMPORTANT]
>Vous ne pouvez pas déplacer des disques managés pour l’instant. 
>
>Nouveaux ID de ressource sont créés dans le cadre de déplacement de hello. Une fois que hello machine virtuelle a été déplacé, vous devez tooupdate vos outils et scripts toouse hello nouveaux ID de ressource. 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a>Utilisez hello CLI d’Azure toomove une machine virtuelle
toosuccessfully déplacer un ordinateur virtuel, vous devez toomove hello VM et toutes ses ressources de prise en charge. Hello d’utilisation **afficher de groupe azure** commande toolist toutes les ressources hello dans un groupe de ressources et leurs ID. Il permet de sortie de hello toopipe cet tooa du fichier de commandes afin de pouvoir copier et coller hello ID des commandes ultérieures.

    azure group show <resourceGroupName>

toomove une machine virtuelle et son groupe de ressources tooanother ressources, utilisez hello **du déplacement des Ressources azure** commande CLI. Bonjour à l’exemple suivant montre comment toomove une machine virtuelle et ressources courants de hello il requiert. Nous utilisons hello **-i** paramètre et passez une liste séparée par des virgules (sans espaces) d’ID pour hello ressources toomove.

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

Si vous souhaitez toomove hello de machine virtuelle et son abonnement aux ressources de différentes tooa, ajouter hello **--destination-subscriptionId &#60; destinationSubscriptionID &#62;** abonnement de destination paramètre toospecify hello.

Si vous travaillez à partir de l’invite de commandes de hello sur un ordinateur Windows, vous devez tooadd une  **$**  devant les noms de variable hello lorsque vous les déclarez. Cela n’est pas nécessaire sous Linux.

Vous êtes invité tooconfirm que vous souhaitez toomove hello de la ressource spécifiée. Type **Y** tooconfirm que vous souhaitez que les ressources de hello toomove.

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez déplacer de nombreux types de ressources différents entre les groupes de ressources et les abonnements. Pour plus d’informations, consultez [déplacer le groupe de ressources toonew ressources ou d’un abonnement](../../resource-group-move-resources.md).    

