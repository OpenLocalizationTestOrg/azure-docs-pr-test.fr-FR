---
title: "trafic aaaVerify avec Azure réseau Observateur IP flux vérifier - CLI d’Azure | Documents Microsoft"
description: "Cet article décrit comment toocheck si tooor le trafic à partir d’un ordinateur virtuel est autorisé ou refusé à l’aide de CLI d’Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 128a00b4296994551e7e17838a51e6d9de180e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Vérifiez si le trafic est autorisé ou refusé tooor à partir d’une machine virtuelle avec IP flux vérifier un composant de l’Observateur de réseau Azure

> [!div class="op_single_selector"]
> - [Portail Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [API REST Azure](network-watcher-check-ip-flow-verify-rest.md)


Flux d’IP Vérifiez est une fonctionnalité de l’Observateur réseau qui vous permet de tooverify si le trafic est autorisé à tooor à partir d’un ordinateur virtuel. Ce scénario est utile tooget un état actuel de si un ordinateur virtuel peut communiquer avec les ressources externes tooan ou principal. Les flux IP vérifier peut être utilisé tooverify si vos règles de groupe de sécurité réseau (NSG) sont correctement configurés et résoudre les problèmes de flux qui sont bloqués par les règles du groupe de sécurité réseau. Une autre raison de l’utilisation de IP flux Vérifiez à bloquer le trafic de tooensure est bloqué correctement par hello groupe de sécurité réseau.

Cet article utilise notre prochaine génération CLI pour le modèle de déploiement de la gestion des ressources d’hello, Azure CLI 2.0, qui est disponible pour Windows, Mac et Linux.

les étapes tooperform hello dans cet article, vous devez trop[installer hello Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Avant de commencer

Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau ou une instance existante de l’Observateur réseau. scénario de Hello suppose également qu’un groupe de ressources avec un ordinateur virtuel valide existe toobe utilisé.

## <a name="scenario"></a>Scénario

Ce scénario utilise tooverify d’IP de flux de vérifier si un ordinateur virtuel peuvent communiquer avec les tooa connus adresse IP de Bing. Si le trafic de hello est refusé, elle retourne la règle de sécurité hello refuse ce trafic. toolearn en savoir plus sur l’IP de flux de vérifier, visitez [flux vérifier la vue d’ensemble IP](network-watcher-ip-flow-verify-overview.md)

## <a name="get-a-vm"></a>Obtenir une machine virtuelle

Les flux IP vérifier tooor le trafic de tests à partir d’une adresse IP sur un tooor de l’ordinateur virtuel à partir d’une destination à distance. Un Id d’un ordinateur virtuel est requis pour l’applet de commande hello. Si vous connaissez déjà les ID hello de hello machine virtuelle toouse, vous pouvez ignorer cette étape.

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-hello-nics"></a>Obtenir hello cartes réseau

adresse IP de Hello d’une carte réseau sur l’ordinateur virtuel de hello est nécessaire, dans cet exemple, nous récupérons hello cartes d’interface réseau sur un ordinateur virtuel. Si vous connaissez déjà hello IP d’adresses que vous souhaitez tootest sur l’ordinateur virtuel de hello, vous pouvez ignorer cette étape.

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a>Exécuter la vérification des flux IP

Maintenant que nous avons des informations hello nécessaire toorun hello applet de commande, nous exécutons hello `az network watcher test-ip-flow` trafic de hello tootest applet de commande. Dans cet exemple, nous utilisons la première adresse IP de hello sur la carte réseau de première hello.

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> Flux d’IP vérifier requiert que les ressources d’ordinateur virtuel hello est allouée toorun.

## <a name="review-results"></a>Analyser les résultats

Après l’exécution `az network watcher test-ip-flow` hello résultats sont retournés, exemple hello est résultats hello retournés à partir de hello précédant l’étape.

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a>Étapes suivantes

Si le trafic est bloqué et ne doit pas être, consultez [gérer les groupes de sécurité réseau](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack vers le bas hello sécurité et groupe de règles de sécurité réseau qui sont définis.

En savoir tooaudit vos paramètres de groupe de sécurité réseau, consultez [audit réseau sécurité groupes (NSG) avec l’Observateur réseau](network-watcher-nsg-auditing-powershell.md).

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
