---
title: "Réinitialiser une passerelle VPN Azure pour rétablir les tunnels IPsec | Microsoft Docs"
description: "Cet article vous guide dans la réinitialisation de votre passerelle VPN Azure pour rétablir les tunnels IPsec. Cet article s’applique aux passerelles VPN dans le modèle de déploiement classique et le modèle de déploiement Resource Manager."
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
ms.openlocfilehash: 7c5ba9310568571991708ab54a5275df6ea84a39
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="ad257-104">Réinitialiser une passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="ad257-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="ad257-105">La réinitialisation d’une passerelle VPN Azure est utile si vous perdez la connectivité VPN entre différents locaux sur un ou plusieurs tunnels VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="ad257-105">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="ad257-106">Dans ce cas, vos périphériques VPN sur site fonctionnent tous correctement, mais ils ne sont pas en mesure d’établir des tunnels IPsec avec les passerelles VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="ad257-106">In this situation, your on-premises VPN devices are all working correctly, but are not able to establish IPsec tunnels with the Azure VPN gateways.</span></span> <span data-ttu-id="ad257-107">Cet article vous permet de réinitialiser votre passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="ad257-107">This article helps you reset your VPN gateway.</span></span>

### <a name="what-happens-during-a-reset"></a><span data-ttu-id="ad257-108">Que se passe-t-il pendant une réinitialisation ?</span><span class="sxs-lookup"><span data-stu-id="ad257-108">What happens during a reset?</span></span>

<span data-ttu-id="ad257-109">Une passerelle VPN se compose de deux instances de machines virtuelles s’exécutant dans une configuration active/de secours.</span><span class="sxs-lookup"><span data-stu-id="ad257-109">A VPN gateway is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="ad257-110">Lorsque vous réinitialisez la passerelle, elle redémarre celle-ci et lui réapplique les configurations entre différents locaux.</span><span class="sxs-lookup"><span data-stu-id="ad257-110">When you reset the gateway, it reboots the gateway, and then reapplies the cross-premises configurations to it.</span></span> <span data-ttu-id="ad257-111">La passerelle conserve l’adresse IP publique qu’elle a déjà.</span><span class="sxs-lookup"><span data-stu-id="ad257-111">The gateway keeps the public IP address it already has.</span></span> <span data-ttu-id="ad257-112">Cela signifie que vous n’avez pas à mettre à jour la configuration du routeur VPN avec une nouvelle adresse IP publique pour la passerelle VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="ad257-112">This means you won’t need to update the VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>

<span data-ttu-id="ad257-113">Quand vous émettez la commande pour réinitialiser la passerelle, l’instance actuellement active de la passerelle VPN Azure est immédiatement redémarrée.</span><span class="sxs-lookup"><span data-stu-id="ad257-113">When you issue the command to reset the gateway, the current active instance of the Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="ad257-114">Un bref laps de temps s’écoule pendant le basculement de l’instance active (en cours de redémarrage) vers l’instance de secours.</span><span class="sxs-lookup"><span data-stu-id="ad257-114">There will be a brief gap during the failover from the active instance (being rebooted), to the standby instance.</span></span> <span data-ttu-id="ad257-115">Cet intervalle doit être inférieur à une minute.</span><span class="sxs-lookup"><span data-stu-id="ad257-115">The gap should be less than one minute.</span></span>

<span data-ttu-id="ad257-116">Si la connexion n’est pas restaurée après le premier redémarrage, exécutez de nouveau la commande pour redémarrer la deuxième instance de machine virtuelle (la nouvelle passerelle active).</span><span class="sxs-lookup"><span data-stu-id="ad257-116">If the connection is not restored after the first reboot, issue the same command again to reboot the second VM instance (the new active gateway).</span></span> <span data-ttu-id="ad257-117">Si les deux redémarrages sont demandés à la suite, il s’écoulera un délai un peu plus long pendant lequel les deux instances de machine virtuelle machine virtuelles (active/veille) sont en cours de redémarrage.</span><span class="sxs-lookup"><span data-stu-id="ad257-117">If the two reboots are requested back to back, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="ad257-118">En conséquence, l’intervalle de connectivité VPN permettant aux machines virtuelles de terminer les redémarrages sera un peu plus long, jusqu’à 2 à 4 minutes.</span><span class="sxs-lookup"><span data-stu-id="ad257-118">This will cause a longer gap on the VPN connectivity, up to 2 to 4 minutes for VMs to complete the reboots.</span></span>

<span data-ttu-id="ad257-119">Après deux redémarrages, si vous continuez de rencontrer des problèmes de connectivité entre différents locaux, ouvrez une demande de support à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ad257-119">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from the Azure portal.</span></span>

## <span data-ttu-id="ad257-120"><a name="before"></a>Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="ad257-120"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="ad257-121">Avant de réinitialiser votre passerelle, vérifiez les éléments clés répertoriés ci-dessous pour chaque tunnel VPN IPsec Site à Site (S2S).</span><span class="sxs-lookup"><span data-stu-id="ad257-121">Before you reset your gateway, verify the key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="ad257-122">Toute incohérence dans les éléments entraîne la déconnexion des tunnels VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="ad257-122">Any mismatch in the items will result in the disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="ad257-123">Une vérification et une correction des configurations pour vos passerelles locales et vos passerelles VPN Azure vous évitent des redémarrages et des perturbations sur les autres connexions en cours sur les passerelles.</span><span class="sxs-lookup"><span data-stu-id="ad257-123">Verifying and correcting the configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for the other working connections on the gateways.</span></span>

<span data-ttu-id="ad257-124">Avant de réinitialiser votre passerelle, vérifiez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="ad257-124">Verify the following items before resetting your gateway:</span></span>

* <span data-ttu-id="ad257-125">Les adresses IP Internet (VIP) de la passerelle VPN Azure et de la passerelle VPN locale sont correctement configurées dans Azure et dans les stratégies VPN sur site.</span><span class="sxs-lookup"><span data-stu-id="ad257-125">The Internet IP addresses (VIPs) for both the Azure VPN gateway and the on-premises VPN gateway are configured correctly in both the Azure and the on-premises VPN policies.</span></span>
* <span data-ttu-id="ad257-126">La clé prépartagée doit être la même sur la passerelle VPN Azure et la passerelle VPN locale.</span><span class="sxs-lookup"><span data-stu-id="ad257-126">The pre-shared key must be the same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="ad257-127">Si vous appliquez une configuration IPsec/IKE spécifique, telle que le chiffrement, des algorithmes de hachage et PFS (Perfect Forward Secrecy), vérifiez que les passerelles VPN Azure et locale ont les mêmes configurations.</span><span class="sxs-lookup"><span data-stu-id="ad257-127">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both the Azure and on-premises VPN gateways have the same configurations.</span></span>

## <span data-ttu-id="ad257-128"><a name="portal"></a>Portail Azure</span><span class="sxs-lookup"><span data-stu-id="ad257-128"><a name="portal"></a>Azure portal</span></span>

<span data-ttu-id="ad257-129">Vous pouvez réinitialiser une passerelle VPN Resource Manager à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ad257-129">You can reset a Resource Manager VPN gateway using the Azure portal.</span></span> <span data-ttu-id="ad257-130">Si vous souhaitez réinitialiser une passerelle classique, consultez les étapes relatives à [PowerShell](#resetclassic).</span><span class="sxs-lookup"><span data-stu-id="ad257-130">If you want to reset a classic gateway, see the [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="ad257-131">Modèle de déploiement de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ad257-131">Resource Manager deployment model</span></span>

1. <span data-ttu-id="ad257-132">Ouvrez le [portail Azure](https://portal.azure.com) et accédez à la passerelle de réseau virtuel Resource Manager que vous souhaitez réinitialiser.</span><span class="sxs-lookup"><span data-stu-id="ad257-132">Open the [Azure portal](https://portal.azure.com) and navigate to the Resource Manager virtual network gateway that you want to reset.</span></span>
2. <span data-ttu-id="ad257-133">Dans le panneau de la passerelle de réseau virtuel, cliquez sur « Réinitialiser ».</span><span class="sxs-lookup"><span data-stu-id="ad257-133">On the blade for the virtual network gateway, click 'Reset'.</span></span>

  ![Panneau Réinitialiser la passerelle VPN](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. <span data-ttu-id="ad257-135">Dans le panneau Réinitialiser, cliquez sur le bouton **Réinitialiser**.</span><span class="sxs-lookup"><span data-stu-id="ad257-135">On the Reset blade, click the **Reset** button.</span></span>

## <span data-ttu-id="ad257-136"><a name="ps"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad257-136"><a name="ps"></a>PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="ad257-137">Modèle de déploiement de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ad257-137">Resource Manager deployment model</span></span>

<span data-ttu-id="ad257-138">La cmdlet permettant de réinitialiser une passerelle est **AzureRmVirtualNetworkGateway-Reset**.</span><span class="sxs-lookup"><span data-stu-id="ad257-138">The cmdlet for resetting a gateway is **Reset-AzureRmVirtualNetworkGateway**.</span></span> <span data-ttu-id="ad257-139">Avant d’effectuer une réinitialisation, vérifiez que vous disposez de la dernière version des [cmdlets PowerShell Resource Manager](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="ad257-139">Before performing a reset, make sure you have the latest version of the [Resource Manager PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span> <span data-ttu-id="ad257-140">L’exemple suivant réinitialise une passerelle de réseau virtuel nommée VNet1GW dans le groupe de ressources TestRG1 :</span><span class="sxs-lookup"><span data-stu-id="ad257-140">The following example resets a virtual network gateway named VNet1GW in the TestRG1 resource group:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

<span data-ttu-id="ad257-141">Résultat :</span><span class="sxs-lookup"><span data-stu-id="ad257-141">Result:</span></span>

<span data-ttu-id="ad257-142">Quand vous recevez un résultat de retour, vous pouvez supposer que la réinitialisation de la passerelle a réussi.</span><span class="sxs-lookup"><span data-stu-id="ad257-142">When you receive a return result, you can assume the gateway reset was successful.</span></span> <span data-ttu-id="ad257-143">Toutefois, rien dans le résultat de retour ne l’indique explicitement.</span><span class="sxs-lookup"><span data-stu-id="ad257-143">However, there is nothing in the return result that indicates explicitly that the reset was successful.</span></span> <span data-ttu-id="ad257-144">Si vous voulez examiner en détail l’historique pour voir exactement à quel moment la réinitialisation de la passerelle s’est produite, vous pouvez afficher ces informations dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad257-144">If you want to look closely at the history to see exactly when the gateway reset occurred, you can view that information in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ad257-145">Dans le portail, accédez à **« GatewayName » -> Resource Health**.</span><span class="sxs-lookup"><span data-stu-id="ad257-145">In the portal, navigate to **'GatewayName' -> Resource Health**.</span></span>

### <span data-ttu-id="ad257-146"><a name="resetclassic"></a>Modèle de déploiement classique</span><span class="sxs-lookup"><span data-stu-id="ad257-146"><a name="resetclassic"></a>Classic deployment model</span></span>

<span data-ttu-id="ad257-147">La cmdlet permettant de réinitialiser une passerelle est **Reset-AzureVNetGateway**.</span><span class="sxs-lookup"><span data-stu-id="ad257-147">The cmdlet for resetting a gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="ad257-148">Avant d’effectuer une réinitialisation, vérifiez que vous disposez de la dernière version des [cmdlets PowerShell Service Management (SM)](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="ad257-148">Before performing a reset, make sure you have the latest version of the [Service Management (SM) PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span></span> <span data-ttu-id="ad257-149">L’exemple suivant réinitialise la passerelle d’un réseau virtuel appelé « ContosoVNet » :</span><span class="sxs-lookup"><span data-stu-id="ad257-149">The following example resets the gateway for a virtual network named "ContosoVNet":</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

<span data-ttu-id="ad257-150">Résultat :</span><span class="sxs-lookup"><span data-stu-id="ad257-150">Result:</span></span>

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <span data-ttu-id="ad257-151"><a name="cli"></a>Interface CLI Azure</span><span class="sxs-lookup"><span data-stu-id="ad257-151"><a name="cli"></a>Azure CLI</span></span>

<span data-ttu-id="ad257-152">Pour réinitialiser la passerelle, utilisez la commande [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset).</span><span class="sxs-lookup"><span data-stu-id="ad257-152">To reset the gateway, use the [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) command.</span></span> <span data-ttu-id="ad257-153">L’exemple suivant réinitialise une passerelle de réseau virtuel nommée VNet5GW dans le groupe de ressources TestRG5 :</span><span class="sxs-lookup"><span data-stu-id="ad257-153">The following example resets a virtual network gateway named VNet5GW in the TestRG5 resource group:</span></span>

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

<span data-ttu-id="ad257-154">Résultat :</span><span class="sxs-lookup"><span data-stu-id="ad257-154">Result:</span></span>

<span data-ttu-id="ad257-155">Quand vous recevez un résultat de retour, vous pouvez supposer que la réinitialisation de la passerelle a réussi.</span><span class="sxs-lookup"><span data-stu-id="ad257-155">When you receive a return result, you can assume the gateway reset was successful.</span></span> <span data-ttu-id="ad257-156">Toutefois, rien dans le résultat de retour ne l’indique explicitement.</span><span class="sxs-lookup"><span data-stu-id="ad257-156">However, there is nothing in the return result that indicates explicitly that the reset was successful.</span></span> <span data-ttu-id="ad257-157">Si vous voulez examiner en détail l’historique pour voir exactement à quel moment la réinitialisation de la passerelle s’est produite, vous pouvez afficher ces informations dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad257-157">If you want to look closely at the history to see exactly when the gateway reset occurred, you can view that information in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ad257-158">Dans le portail, accédez à **« GatewayName » -> Resource Health**.</span><span class="sxs-lookup"><span data-stu-id="ad257-158">In the portal, navigate to **'GatewayName' -> Resource Health**.</span></span>