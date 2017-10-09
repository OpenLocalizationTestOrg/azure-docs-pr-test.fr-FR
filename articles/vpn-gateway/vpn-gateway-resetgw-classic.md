---
title: "Réinitialiser un tooreestablish de passerelle VPN Azure tunnels IPsec | Documents Microsoft"
description: "Cet article vous guide tout au long de la réinitialisation de votre passerelle VPN à Azure tooreestablish les tunnels IPsec. article de Hello concerne les passerelles tooVPN dans hello classique et modèles de déploiement du Gestionnaire de ressources hello."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: cherylmc
ms.openlocfilehash: 84dd741f0bebd6b18cb235216a68a88da5fe17b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reset-a-vpn-gateway"></a>Réinitialiser une passerelle VPN

La réinitialisation d’une passerelle VPN Azure est utile si vous perdez la connectivité VPN entre différents locaux sur un ou plusieurs tunnels VPN de site à site. Dans ce cas, vos périphériques VPN sur site sont tous les fonctionne correctement, mais sont tooestablish n’a pas pu les tunnels IPsec avec les passerelles VPN Azure hello. Cet article vous permet de réinitialiser votre passerelle VPN.

### <a name="what-happens-during-a-reset"></a>Que se passe-t-il pendant une réinitialisation ?

Une passerelle VPN se compose de deux instances de machines virtuelles s’exécutant dans une configuration active/de secours. Lorsque vous réinitialisez la passerelle de hello, entraîne le redémarrage de passerelle de hello, puis applique à nouveau hello intersite tooit de configurations. passerelle de Hello conserve l’adresse IP publique hello qu'est déjà. Cela signifie que vous n’aurez pas configuration du routeur tooupdate hello VPN avec une nouvelle adresse IP publique pour la passerelle VPN Azure.

Lorsque vous émettez la passerelle de hello hello commande tooreset, hello actuel instance active de passerelle VPN Azure de hello est redémarré immédiatement. Il y aura un bref intervalle pendant le basculement hello hello instances actives (redémarrés), instance de secours toohello. intervalle de Hello doit être inférieure à une minute.

Si la connexion de hello n’est pas restaurée après le redémarrage de première hello, problème hello même tooreboot hello deuxième machine virtuelle instance (passerelle active nouvelle hello) réexécutez la commande. Deux redémarrages de hello tooback arrière demandé, s’il y aura un délai légèrement plus long où les deux instances de machine virtuelle (actives et de secours) sont redémarrés. Cela entraîne un écart de plus de temps sur une connectivité VPN hello des redémarrages de machines virtuelles toocomplete hello too2 too4 minutes.

Après deux redémarrages, si vous continuez à rencontrer des problèmes de connectivité entre différents locaux, ouvrez une demande de support à partir de hello portail Azure.

## <a name="before"></a>Avant de commencer

Avant de réinitialiser votre passerelle, vérifiez les éléments clés hello répertoriées ci-dessous pour chaque tunnel IPsec de Site à Site (S2S) VPN. Une incompatibilité dans les éléments de hello entraîne une déconnexion hello des tunnels VPN de S2S. Vérification et correction des configurations hello pour vos locaux et les passerelles VPN de Azure permet d’éviter de redémarrages inutiles et interruptions hello autres connexions de travail sur les passerelles hello.

Vérifiez que hello éléments suivants avant la réinitialisation de votre passerelle :

* Hello IP Internet adresses (VIP) pour les deux passerelle VPN Azure de hello hello locaux et passerelle VPN sont correctement configurés dans les deux stratégies VPN de site sur Azure et hello hello.
* clé prépartagée de Hello doit être hello même sur les passerelles VPN Azure et locales.
* Si vous appliquez la configuration d’IPsec/IKE spécifique, telles que le chiffrement, les algorithmes de hachage et PFS (Perfect Forward Secrecy), vérifiez à la fois hello Azure et les passerelles VPN local ont hello mêmes configurations.

## <a name="portal"></a>Portail Azure

Vous pouvez réinitialiser la passerelle VPN du Gestionnaire de ressources à l’aide de hello portail Azure. Si vous souhaitez tooreset une passerelle classique, consultez hello [PowerShell](#resetclassic) étapes.

### <a name="resource-manager-deployment-model"></a>Modèle de déploiement de Resource Manager

1. Ouvrez hello [portail Azure](https://portal.azure.com) et accédez de passerelle de réseau virtuel toohello Gestionnaire de ressources que vous souhaitez tooreset.
2. Dans Panneau de hello pour la passerelle de réseau virtuel hello, cliquez sur « Réinitialiser ».

  ![Panneau Réinitialiser la passerelle VPN](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. Sur hello réinitialiser panneau, cliquez sur hello **réinitialiser** bouton.

## <a name="ps"></a>PowerShell

### <a name="resource-manager-deployment-model"></a>Modèle de déploiement de Resource Manager

Hello applet de commande pour réinitialiser une passerelle est **Reset-AzureRmVirtualNetworkGateway**. Avant d’effectuer une réinitialisation, assurez-vous que vous avez la version la plus récente de hello hello [applets de commande PowerShell de gestionnaire de ressources](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0). Hello exemple suivant réinitialise une passerelle de réseau virtuel nommée VNet1GW hello TestRG1 groupe de ressources :

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

Résultat :

Lorsque vous recevez un résultat, vous pouvez supposer hello passerelle réinitialisation a réussi. Toutefois, il est rien dans le résultat obtenu hello qui indique explicitement qui réinitialisent hello a réussi. Si vous souhaitez toolook étroitement à hello historique toosee exactement quand les passerelle hello réinitialisation s’est produite, vous pouvez afficher ces informations dans hello [portail Azure](https://portal.azure.com). Dans le portail de hello, accédez trop**'GatewayName' -> contrôle d’intégrité**.

### <a name="resetclassic"></a>Modèle de déploiement classique

Hello applet de commande pour réinitialiser une passerelle est **Reset-AzureVNetGateway**. Avant d’effectuer une réinitialisation, assurez-vous que vous avez la version la plus récente de hello hello [applets de commande PowerShell de gestion de Service (SM)](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0). Hello exemple suivant réinitialise passerelle hello pour un réseau virtuel nommé « ContosoVNet » :

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

Résultat :

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <a name="cli"></a>Interface CLI Azure

passerelle de hello tooreset, utilisez hello [réinitialisation de la passerelle de réseau virtuel de réseau az](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) commande. Hello exemple suivant réinitialise une passerelle de réseau virtuel nommée VNet5GW hello TestRG5 groupe de ressources :

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

Résultat :

Lorsque vous recevez un résultat, vous pouvez supposer hello passerelle réinitialisation a réussi. Toutefois, il est rien dans le résultat obtenu hello qui indique explicitement qui réinitialisent hello a réussi. Si vous souhaitez toolook étroitement à hello historique toosee exactement quand les passerelle hello réinitialisation s’est produite, vous pouvez afficher ces informations dans hello [portail Azure](https://portal.azure.com). Dans le portail de hello, accédez trop**'GatewayName' -> contrôle d’intégrité**.
