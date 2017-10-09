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
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="80b1e-104">Réinitialiser une passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="80b1e-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="80b1e-105">La réinitialisation d’une passerelle VPN Azure est utile si vous perdez la connectivité VPN entre différents locaux sur un ou plusieurs tunnels VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="80b1e-105">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="80b1e-106">Dans ce cas, vos périphériques VPN sur site sont tous les fonctionne correctement, mais sont tooestablish n’a pas pu les tunnels IPsec avec les passerelles VPN Azure hello.</span><span class="sxs-lookup"><span data-stu-id="80b1e-106">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="80b1e-107">Cet article vous permet de réinitialiser votre passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="80b1e-107">This article helps you reset your VPN gateway.</span></span>

### <a name="what-happens-during-a-reset"></a><span data-ttu-id="80b1e-108">Que se passe-t-il pendant une réinitialisation ?</span><span class="sxs-lookup"><span data-stu-id="80b1e-108">What happens during a reset?</span></span>

<span data-ttu-id="80b1e-109">Une passerelle VPN se compose de deux instances de machines virtuelles s’exécutant dans une configuration active/de secours.</span><span class="sxs-lookup"><span data-stu-id="80b1e-109">A VPN gateway is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="80b1e-110">Lorsque vous réinitialisez la passerelle de hello, entraîne le redémarrage de passerelle de hello, puis applique à nouveau hello intersite tooit de configurations.</span><span class="sxs-lookup"><span data-stu-id="80b1e-110">When you reset hello gateway, it reboots hello gateway, and then reapplies hello cross-premises configurations tooit.</span></span> <span data-ttu-id="80b1e-111">passerelle de Hello conserve l’adresse IP publique hello qu'est déjà.</span><span class="sxs-lookup"><span data-stu-id="80b1e-111">hello gateway keeps hello public IP address it already has.</span></span> <span data-ttu-id="80b1e-112">Cela signifie que vous n’aurez pas configuration du routeur tooupdate hello VPN avec une nouvelle adresse IP publique pour la passerelle VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="80b1e-112">This means you won’t need tooupdate hello VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>

<span data-ttu-id="80b1e-113">Lorsque vous émettez la passerelle de hello hello commande tooreset, hello actuel instance active de passerelle VPN Azure de hello est redémarré immédiatement.</span><span class="sxs-lookup"><span data-stu-id="80b1e-113">When you issue hello command tooreset hello gateway, hello current active instance of hello Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="80b1e-114">Il y aura un bref intervalle pendant le basculement hello hello instances actives (redémarrés), instance de secours toohello.</span><span class="sxs-lookup"><span data-stu-id="80b1e-114">There will be a brief gap during hello failover from hello active instance (being rebooted), toohello standby instance.</span></span> <span data-ttu-id="80b1e-115">intervalle de Hello doit être inférieure à une minute.</span><span class="sxs-lookup"><span data-stu-id="80b1e-115">hello gap should be less than one minute.</span></span>

<span data-ttu-id="80b1e-116">Si la connexion de hello n’est pas restaurée après le redémarrage de première hello, problème hello même tooreboot hello deuxième machine virtuelle instance (passerelle active nouvelle hello) réexécutez la commande.</span><span class="sxs-lookup"><span data-stu-id="80b1e-116">If hello connection is not restored after hello first reboot, issue hello same command again tooreboot hello second VM instance (hello new active gateway).</span></span> <span data-ttu-id="80b1e-117">Deux redémarrages de hello tooback arrière demandé, s’il y aura un délai légèrement plus long où les deux instances de machine virtuelle (actives et de secours) sont redémarrés.</span><span class="sxs-lookup"><span data-stu-id="80b1e-117">If hello two reboots are requested back tooback, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="80b1e-118">Cela entraîne un écart de plus de temps sur une connectivité VPN hello des redémarrages de machines virtuelles toocomplete hello too2 too4 minutes.</span><span class="sxs-lookup"><span data-stu-id="80b1e-118">This will cause a longer gap on hello VPN connectivity, up too2 too4 minutes for VMs toocomplete hello reboots.</span></span>

<span data-ttu-id="80b1e-119">Après deux redémarrages, si vous continuez à rencontrer des problèmes de connectivité entre différents locaux, ouvrez une demande de support à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="80b1e-119">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from hello Azure portal.</span></span>

## <span data-ttu-id="80b1e-120"><a name="before"></a>Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="80b1e-120"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="80b1e-121">Avant de réinitialiser votre passerelle, vérifiez les éléments clés hello répertoriées ci-dessous pour chaque tunnel IPsec de Site à Site (S2S) VPN.</span><span class="sxs-lookup"><span data-stu-id="80b1e-121">Before you reset your gateway, verify hello key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="80b1e-122">Une incompatibilité dans les éléments de hello entraîne une déconnexion hello des tunnels VPN de S2S.</span><span class="sxs-lookup"><span data-stu-id="80b1e-122">Any mismatch in hello items will result in hello disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="80b1e-123">Vérification et correction des configurations hello pour vos locaux et les passerelles VPN de Azure permet d’éviter de redémarrages inutiles et interruptions hello autres connexions de travail sur les passerelles hello.</span><span class="sxs-lookup"><span data-stu-id="80b1e-123">Verifying and correcting hello configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for hello other working connections on hello gateways.</span></span>

<span data-ttu-id="80b1e-124">Vérifiez que hello éléments suivants avant la réinitialisation de votre passerelle :</span><span class="sxs-lookup"><span data-stu-id="80b1e-124">Verify hello following items before resetting your gateway:</span></span>

* <span data-ttu-id="80b1e-125">Hello IP Internet adresses (VIP) pour les deux passerelle VPN Azure de hello hello locaux et passerelle VPN sont correctement configurés dans les deux stratégies VPN de site sur Azure et hello hello.</span><span class="sxs-lookup"><span data-stu-id="80b1e-125">hello Internet IP addresses (VIPs) for both hello Azure VPN gateway and hello on-premises VPN gateway are configured correctly in both hello Azure and hello on-premises VPN policies.</span></span>
* <span data-ttu-id="80b1e-126">clé prépartagée de Hello doit être hello même sur les passerelles VPN Azure et locales.</span><span class="sxs-lookup"><span data-stu-id="80b1e-126">hello pre-shared key must be hello same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="80b1e-127">Si vous appliquez la configuration d’IPsec/IKE spécifique, telles que le chiffrement, les algorithmes de hachage et PFS (Perfect Forward Secrecy), vérifiez à la fois hello Azure et les passerelles VPN local ont hello mêmes configurations.</span><span class="sxs-lookup"><span data-stu-id="80b1e-127">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both hello Azure and on-premises VPN gateways have hello same configurations.</span></span>

## <span data-ttu-id="80b1e-128"><a name="portal"></a>Portail Azure</span><span class="sxs-lookup"><span data-stu-id="80b1e-128"><a name="portal"></a>Azure portal</span></span>

<span data-ttu-id="80b1e-129">Vous pouvez réinitialiser la passerelle VPN du Gestionnaire de ressources à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="80b1e-129">You can reset a Resource Manager VPN gateway using hello Azure portal.</span></span> <span data-ttu-id="80b1e-130">Si vous souhaitez tooreset une passerelle classique, consultez hello [PowerShell](#resetclassic) étapes.</span><span class="sxs-lookup"><span data-stu-id="80b1e-130">If you want tooreset a classic gateway, see hello [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="80b1e-131">Modèle de déploiement de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="80b1e-131">Resource Manager deployment model</span></span>

1. <span data-ttu-id="80b1e-132">Ouvrez hello [portail Azure](https://portal.azure.com) et accédez de passerelle de réseau virtuel toohello Gestionnaire de ressources que vous souhaitez tooreset.</span><span class="sxs-lookup"><span data-stu-id="80b1e-132">Open hello [Azure portal](https://portal.azure.com) and navigate toohello Resource Manager virtual network gateway that you want tooreset.</span></span>
2. <span data-ttu-id="80b1e-133">Dans Panneau de hello pour la passerelle de réseau virtuel hello, cliquez sur « Réinitialiser ».</span><span class="sxs-lookup"><span data-stu-id="80b1e-133">On hello blade for hello virtual network gateway, click 'Reset'.</span></span>

  ![Panneau Réinitialiser la passerelle VPN](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. <span data-ttu-id="80b1e-135">Sur hello réinitialiser panneau, cliquez sur hello **réinitialiser** bouton.</span><span class="sxs-lookup"><span data-stu-id="80b1e-135">On hello Reset blade, click hello **Reset** button.</span></span>

## <span data-ttu-id="80b1e-136"><a name="ps"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="80b1e-136"><a name="ps"></a>PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="80b1e-137">Modèle de déploiement de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="80b1e-137">Resource Manager deployment model</span></span>

<span data-ttu-id="80b1e-138">Hello applet de commande pour réinitialiser une passerelle est **Reset-AzureRmVirtualNetworkGateway**.</span><span class="sxs-lookup"><span data-stu-id="80b1e-138">hello cmdlet for resetting a gateway is **Reset-AzureRmVirtualNetworkGateway**.</span></span> <span data-ttu-id="80b1e-139">Avant d’effectuer une réinitialisation, assurez-vous que vous avez la version la plus récente de hello hello [applets de commande PowerShell de gestionnaire de ressources](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="80b1e-139">Before performing a reset, make sure you have hello latest version of hello [Resource Manager PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span> <span data-ttu-id="80b1e-140">Hello exemple suivant réinitialise une passerelle de réseau virtuel nommée VNet1GW hello TestRG1 groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="80b1e-140">hello following example resets a virtual network gateway named VNet1GW in hello TestRG1 resource group:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

<span data-ttu-id="80b1e-141">Résultat :</span><span class="sxs-lookup"><span data-stu-id="80b1e-141">Result:</span></span>

<span data-ttu-id="80b1e-142">Lorsque vous recevez un résultat, vous pouvez supposer hello passerelle réinitialisation a réussi.</span><span class="sxs-lookup"><span data-stu-id="80b1e-142">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="80b1e-143">Toutefois, il est rien dans le résultat obtenu hello qui indique explicitement qui réinitialisent hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="80b1e-143">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="80b1e-144">Si vous souhaitez toolook étroitement à hello historique toosee exactement quand les passerelle hello réinitialisation s’est produite, vous pouvez afficher ces informations dans hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="80b1e-144">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="80b1e-145">Dans le portail de hello, accédez trop**'GatewayName' -> contrôle d’intégrité**.</span><span class="sxs-lookup"><span data-stu-id="80b1e-145">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>

### <span data-ttu-id="80b1e-146"><a name="resetclassic"></a>Modèle de déploiement classique</span><span class="sxs-lookup"><span data-stu-id="80b1e-146"><a name="resetclassic"></a>Classic deployment model</span></span>

<span data-ttu-id="80b1e-147">Hello applet de commande pour réinitialiser une passerelle est **Reset-AzureVNetGateway**.</span><span class="sxs-lookup"><span data-stu-id="80b1e-147">hello cmdlet for resetting a gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="80b1e-148">Avant d’effectuer une réinitialisation, assurez-vous que vous avez la version la plus récente de hello hello [applets de commande PowerShell de gestion de Service (SM)](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="80b1e-148">Before performing a reset, make sure you have hello latest version of hello [Service Management (SM) PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span></span> <span data-ttu-id="80b1e-149">Hello exemple suivant réinitialise passerelle hello pour un réseau virtuel nommé « ContosoVNet » :</span><span class="sxs-lookup"><span data-stu-id="80b1e-149">hello following example resets hello gateway for a virtual network named "ContosoVNet":</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

<span data-ttu-id="80b1e-150">Résultat :</span><span class="sxs-lookup"><span data-stu-id="80b1e-150">Result:</span></span>

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <span data-ttu-id="80b1e-151"><a name="cli"></a>Interface CLI Azure</span><span class="sxs-lookup"><span data-stu-id="80b1e-151"><a name="cli"></a>Azure CLI</span></span>

<span data-ttu-id="80b1e-152">passerelle de hello tooreset, utilisez hello [réinitialisation de la passerelle de réseau virtuel de réseau az](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) commande.</span><span class="sxs-lookup"><span data-stu-id="80b1e-152">tooreset hello gateway, use hello [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) command.</span></span> <span data-ttu-id="80b1e-153">Hello exemple suivant réinitialise une passerelle de réseau virtuel nommée VNet5GW hello TestRG5 groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="80b1e-153">hello following example resets a virtual network gateway named VNet5GW in hello TestRG5 resource group:</span></span>

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

<span data-ttu-id="80b1e-154">Résultat :</span><span class="sxs-lookup"><span data-stu-id="80b1e-154">Result:</span></span>

<span data-ttu-id="80b1e-155">Lorsque vous recevez un résultat, vous pouvez supposer hello passerelle réinitialisation a réussi.</span><span class="sxs-lookup"><span data-stu-id="80b1e-155">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="80b1e-156">Toutefois, il est rien dans le résultat obtenu hello qui indique explicitement qui réinitialisent hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="80b1e-156">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="80b1e-157">Si vous souhaitez toolook étroitement à hello historique toosee exactement quand les passerelle hello réinitialisation s’est produite, vous pouvez afficher ces informations dans hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="80b1e-157">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="80b1e-158">Dans le portail de hello, accédez trop**'GatewayName' -> contrôle d’intégrité**.</span><span class="sxs-lookup"><span data-stu-id="80b1e-158">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>
