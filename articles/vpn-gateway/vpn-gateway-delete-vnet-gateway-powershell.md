---
title: "Suppression d’une passerelle de réseau virtuel : PowerShell : Azure Resource Manager | Microsoft Docs"
description: "Supprimez une passerelle de réseau virtuel avec PowerShell dans le modèle de déploiement Resource Manager."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 4d0f085423d5bd60b24d88649ee1d77bcd1d009f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell"></a><span data-ttu-id="b0725-103">Supprimer une passerelle de réseau virtuel avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0725-103">Delete a virtual network gateway using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b0725-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="b0725-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="b0725-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0725-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="b0725-106">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="b0725-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="b0725-107">Deux approches sont possibles afin de supprimer une passerelle de réseau virtuel pour une configuration de passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="b0725-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="b0725-108">Si vous voulez tout supprimer et recommencer, comme dans le cas d’un environnement de test, vous pouvez supprimer le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b0725-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="b0725-109">Supprimer un groupe de ressources supprime toutes les ressources du groupe.</span><span class="sxs-lookup"><span data-stu-id="b0725-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="b0725-110">Cette méthode est recommandée seulement si vous ne voulez conserver aucune des ressources du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b0725-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="b0725-111">Vous ne pouvez pas choisir de supprimer uniquement certaines ressources avec cette approche.</span><span class="sxs-lookup"><span data-stu-id="b0725-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="b0725-112">Si vous souhaitez conserver certaines ressources de votre groupe de ressources, la suppression d’une passerelle de réseau virtuel devient légèrement plus complexe.</span><span class="sxs-lookup"><span data-stu-id="b0725-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="b0725-113">Avant de supprimer la passerelle de réseau virtuel, vous devez commencer par supprimer toutes les ressources qui dépendent de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="b0725-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="b0725-114">Les étapes à suivre dépendent du type de connexions que vous avez créées et des ressources dépendantes de chaque connexion.</span><span class="sxs-lookup"><span data-stu-id="b0725-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="b0725-115">Avant tout chose</span><span class="sxs-lookup"><span data-stu-id="b0725-115">Before beginning</span></span>

### <a name="1-download-the-latest-azure-resource-manager-powershell-cmdlets"></a><span data-ttu-id="b0725-116">1. Téléchargez la dernière version des applets de commande PowerShell Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b0725-116">1. Download the latest Azure Resource Manager PowerShell cmdlets.</span></span>

<span data-ttu-id="b0725-117">Téléchargez et installez la dernière version des applets de commande PowerShell Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b0725-117">Download and install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="b0725-118">Pour plus d’informations sur le téléchargement et l’installation des applets de commande PowerShell, consultez la page [Guide pratique d’installation et de configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b0725-118">For more information about downloading and installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="b0725-119">2. Connectez-vous à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="b0725-119">2. Connect to your Azure account.</span></span>

<span data-ttu-id="b0725-120">Ouvrez la console PowerShell et connectez-vous à votre compte.</span><span class="sxs-lookup"><span data-stu-id="b0725-120">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="b0725-121">Utilisez l’exemple suivant pour faciliter votre connexion :</span><span class="sxs-lookup"><span data-stu-id="b0725-121">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="b0725-122">Vérifiez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="b0725-122">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="b0725-123">Si vous avez plusieurs abonnements, spécifiez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="b0725-123">If you have more than one subscription, specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="b0725-124"><a name="S2S"></a>Supprimer une passerelle VPN de site à site</span><span class="sxs-lookup"><span data-stu-id="b0725-124"><a name="S2S"></a>Delete a Site-to-Site VPN gateway</span></span>

<span data-ttu-id="b0725-125">Pour supprimer une passerelle de réseau virtuel pour une configuration S2S, vous devez d’abord supprimer chaque ressource liée à la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b0725-125">To delete a virtual network gateway for a S2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="b0725-126">Les ressources doivent être supprimées dans un certain ordre en raison des dépendances.</span><span class="sxs-lookup"><span data-stu-id="b0725-126">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="b0725-127">Quand vous travaillez avec les exemples ci-dessous, certaines valeurs doivent être spécifiées, tandis que d’autres sont des résultats en sortie.</span><span class="sxs-lookup"><span data-stu-id="b0725-127">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="b0725-128">Nous utilisons les valeurs suivantes dans les exemples à des fins de démonstration :</span><span class="sxs-lookup"><span data-stu-id="b0725-128">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="b0725-129">Nom du réseau virtuel : VNet1</span><span class="sxs-lookup"><span data-stu-id="b0725-129">VNet name: VNet1</span></span><br>
<span data-ttu-id="b0725-130">Nom du groupe de ressources : RG1</span><span class="sxs-lookup"><span data-stu-id="b0725-130">Resource Group name: RG1</span></span><br>
<span data-ttu-id="b0725-131">Nom de la passerelle de réseau virtuel : GW1</span><span class="sxs-lookup"><span data-stu-id="b0725-131">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="b0725-132">Les étapes suivantes s’appliquent au modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b0725-132">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="b0725-133">1. Récupérez la passerelle de réseau virtuel que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="b0725-133">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="b0725-134">2. Vérifiez si la passerelle de réseau virtuel possède des connexions.</span><span class="sxs-lookup"><span data-stu-id="b0725-134">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
$Conns=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```

### <a name="3-delete-all-connections"></a><span data-ttu-id="b0725-135">3. Supprimez toutes les connexions.</span><span class="sxs-lookup"><span data-stu-id="b0725-135">3. Delete all connections.</span></span>

<span data-ttu-id="b0725-136">Vous serez peut-être invité à confirmer la suppression de chacune des connexions.</span><span class="sxs-lookup"><span data-stu-id="b0725-136">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$Conns | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="4-delete-the-virtual-network-gateway"></a><span data-ttu-id="b0725-137">4. Supprimez la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b0725-137">4. Delete the virtual network gateway.</span></span>

<span data-ttu-id="b0725-138">Vous serez peut-être invité à confirmer la suppression de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="b0725-138">You may be prompted to confirm the deletion of the gateway.</span></span> <span data-ttu-id="b0725-139">Si vous avez une configuration P2S sur ce réseau virtuel en plus de votre configuration S2S, la suppression de la passerelle de réseau virtuel déconnecte automatiquement tous les clients P2S sans avertissement.</span><span class="sxs-lookup"><span data-stu-id="b0725-139">If you have a P2S configuration to this VNet in addition to your S2S configuration, deleting the virtual network gateway will automatically disconnect all P2S clients without warning.</span></span>


```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="b0725-140">À ce stade, votre passerelle de réseau virtuel a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="b0725-140">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="b0725-141">Vous pouvez vous conformer aux étapes suivantes pour supprimer toutes les ressources qui ne sont plus utilisées.</span><span class="sxs-lookup"><span data-stu-id="b0725-141">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="5-delete-the-local-network-gateways"></a><span data-ttu-id="b0725-142">5. Supprimez les passerelles de réseau local.</span><span class="sxs-lookup"><span data-stu-id="b0725-142">5 Delete the local network gateways.</span></span>

<span data-ttu-id="b0725-143">Récupérez la liste des passerelles de réseau local correspondantes.</span><span class="sxs-lookup"><span data-stu-id="b0725-143">Get the list of the corresponding local network gateways.</span></span>

```powershell
$LNG=Get-AzureRmLocalNetworkGateway -ResourceGroupName "RG1" | where-object {$_.Id -In $Conns.LocalNetworkGateway2.Id}
```

<span data-ttu-id="b0725-144">Supprimez les passerelles de réseau local.</span><span class="sxs-lookup"><span data-stu-id="b0725-144">Delete the local network gateways.</span></span> <span data-ttu-id="b0725-145">Vous serez peut-être invité à confirmer la suppression de chacune des passerelles de réseau local.</span><span class="sxs-lookup"><span data-stu-id="b0725-145">You may be prompted to confirm the deletion of each of the local network gateway.</span></span>

```powershell
$LNG | ForEach-Object {Remove-AzureRmLocalNetworkGateway -Name $_.Name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="b0725-146">6. Supprimez les ressources de l’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="b0725-146">6. Delete the Public IP address resources.</span></span>

<span data-ttu-id="b0725-147">Récupérez les configurations IP de la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b0725-147">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="b0725-148">Récupérez la liste des ressources d’adresse IP publique utilisées pour cette passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b0725-148">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="b0725-149">Si la passerelle de réseau virtuel était active-active, vous verrez deux adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="b0725-149">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="b0725-150">Supprimez les ressources de l’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="b0725-150">Delete the Public IP resources.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "RG1"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="b0725-151">7. Supprimez le sous-réseau de passerelle et définissez la configuration.</span><span class="sxs-lookup"><span data-stu-id="b0725-151">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="b0725-152"><a name="v2v"></a>Supprimer une passerelle VPN de réseau virtuel à réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="b0725-152"><a name="v2v"></a>Delete a VNet-to-VNet VPN gateway</span></span>

<span data-ttu-id="b0725-153">Si vous souhaitez supprimer une passerelle de réseau virtuel pour une configuration V2V, vous devez d’abord supprimer chaque ressource liée à la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b0725-153">To delete a virtual network gateway for a V2V configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="b0725-154">Les ressources doivent être supprimées dans un certain ordre en raison des dépendances.</span><span class="sxs-lookup"><span data-stu-id="b0725-154">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="b0725-155">Quand vous travaillez avec les exemples ci-dessous, certaines valeurs doivent être spécifiées, tandis que d’autres sont des résultats en sortie.</span><span class="sxs-lookup"><span data-stu-id="b0725-155">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="b0725-156">Nous utilisons les valeurs suivantes dans les exemples à des fins de démonstration :</span><span class="sxs-lookup"><span data-stu-id="b0725-156">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="b0725-157">Nom du réseau virtuel : VNet1</span><span class="sxs-lookup"><span data-stu-id="b0725-157">VNet name: VNet1</span></span><br>
<span data-ttu-id="b0725-158">Nom du groupe de ressources : RG1</span><span class="sxs-lookup"><span data-stu-id="b0725-158">Resource Group name: RG1</span></span><br>
<span data-ttu-id="b0725-159">Nom de la passerelle de réseau virtuel : GW1</span><span class="sxs-lookup"><span data-stu-id="b0725-159">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="b0725-160">Les étapes suivantes s’appliquent au modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b0725-160">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="b0725-161">1. Récupérez la passerelle de réseau virtuel que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="b0725-161">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="b0725-162">2. Vérifiez si la passerelle de réseau virtuel possède des connexions.</span><span class="sxs-lookup"><span data-stu-id="b0725-162">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="b0725-163">Il peut y avoir d’autres connexions à la passerelle de réseau virtuel qui font partie d’un autre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b0725-163">There may be other connections to the virtual network gateway that are part of a different resource group.</span></span> <span data-ttu-id="b0725-164">Recherchez les connexions supplémentaires dans chacun des autres groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="b0725-164">Check for additional connections in each additional resource group.</span></span> <span data-ttu-id="b0725-165">Dans cet exemple, nous vérifions les connexions à partir de RG2.</span><span class="sxs-lookup"><span data-stu-id="b0725-165">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="b0725-166">Exécutez cette commande pour chacun de vos groupes de ressources qui sont susceptibles d’avoir une connexion à la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b0725-166">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG2" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
```

### <a name="3-get-the-list-of-connections-in-both-directions"></a><span data-ttu-id="b0725-167">3. Récupérez la liste des connexions dans les deux sens.</span><span class="sxs-lookup"><span data-stu-id="b0725-167">3. Get the list of connections in both directions.</span></span>

<span data-ttu-id="b0725-168">Dans la mesure où il s’agit d’une configuration de réseau virtuel à réseau virtuel, vous avez besoin de la liste des connexions dans les deux sens.</span><span class="sxs-lookup"><span data-stu-id="b0725-168">Because this is a VNet-to-VNet configuration, you need the list of connections in both directions.</span></span>

```powershell
$ConnsL=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="b0725-169">Dans cet exemple, nous vérifions les connexions à partir de RG2.</span><span class="sxs-lookup"><span data-stu-id="b0725-169">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="b0725-170">Exécutez cette commande pour chacun de vos groupes de ressources qui sont susceptibles d’avoir une connexion à la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b0725-170">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
 $ConnsR=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "<NameOfResourceGroup2>" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
 ```

### <a name="4-delete-all-connections"></a><span data-ttu-id="b0725-171">4. Supprimez toutes les connexions.</span><span class="sxs-lookup"><span data-stu-id="b0725-171">4. Delete all connections.</span></span>

<span data-ttu-id="b0725-172">Vous serez peut-être invité à confirmer la suppression de chacune des connexions.</span><span class="sxs-lookup"><span data-stu-id="b0725-172">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$ConnsL | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
$ConnsR | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="5-delete-the-virtual-network-gateway"></a><span data-ttu-id="b0725-173">5. Supprimez la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b0725-173">5. Delete the virtual network gateway.</span></span>

<span data-ttu-id="b0725-174">Vous serez peut-être invité à confirmer la suppression de la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b0725-174">You may be prompted to confirm the deletion of the virtual network gateway.</span></span> <span data-ttu-id="b0725-175">Si vous avez des configurations P2S sur vos réseaux virtuels en plus de votre configuration V2V, la suppression des passerelles de réseau virtuel déconnecte automatiquement tous les clients P2S sans avertissement.</span><span class="sxs-lookup"><span data-stu-id="b0725-175">If you have P2S configurations to your VNets in addition to your V2V configuration, deleting the virtual network gateways will automatically disconnect all P2S clients without warning.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="b0725-176">À ce stade, votre passerelle de réseau virtuel a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="b0725-176">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="b0725-177">Vous pouvez vous conformer aux étapes suivantes pour supprimer toutes les ressources qui ne sont plus utilisées.</span><span class="sxs-lookup"><span data-stu-id="b0725-177">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="b0725-178">6. Supprimez les ressources de l’adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="b0725-178">6. Delete the Public IP address resources</span></span>

<span data-ttu-id="b0725-179">Récupérez les configurations IP de la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b0725-179">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="b0725-180">Récupérez la liste des ressources d’adresse IP publique utilisées pour cette passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b0725-180">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="b0725-181">Si la passerelle de réseau virtuel était active-active, vous verrez deux adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="b0725-181">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="b0725-182">Supprimez les ressources de l’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="b0725-182">Delete the Public IP resources.</span></span> <span data-ttu-id="b0725-183">Vous serez peut-être invité à confirmer la suppression de l’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="b0725-183">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="b0725-184">7. Supprimez le sous-réseau de passerelle et définissez la configuration.</span><span class="sxs-lookup"><span data-stu-id="b0725-184">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="b0725-185"><a name="deletep2s"></a>Suppression d’une passerelle VPN de point à site</span><span class="sxs-lookup"><span data-stu-id="b0725-185"><a name="deletep2s"></a>Delete a Point-to-Site VPN gateway</span></span>

<span data-ttu-id="b0725-186">Pour supprimer une passerelle de réseau virtuel pour une configuration P2S, vous devez d’abord supprimer chaque ressource liée à la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b0725-186">To delete a virtual network gateway for a P2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="b0725-187">Les ressources doivent être supprimées dans un certain ordre en raison des dépendances.</span><span class="sxs-lookup"><span data-stu-id="b0725-187">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="b0725-188">Quand vous travaillez avec les exemples ci-dessous, certaines valeurs doivent être spécifiées, tandis que d’autres sont des résultats en sortie.</span><span class="sxs-lookup"><span data-stu-id="b0725-188">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="b0725-189">Nous utilisons les valeurs suivantes dans les exemples à des fins de démonstration :</span><span class="sxs-lookup"><span data-stu-id="b0725-189">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="b0725-190">Nom du réseau virtuel : VNet1</span><span class="sxs-lookup"><span data-stu-id="b0725-190">VNet name: VNet1</span></span><br>
<span data-ttu-id="b0725-191">Nom du groupe de ressources : RG1</span><span class="sxs-lookup"><span data-stu-id="b0725-191">Resource Group name: RG1</span></span><br>
<span data-ttu-id="b0725-192">Nom de la passerelle de réseau virtuel : GW1</span><span class="sxs-lookup"><span data-stu-id="b0725-192">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="b0725-193">Les étapes suivantes s’appliquent au modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b0725-193">The following steps apply to the Resource Manager deployment model.</span></span>


>[!NOTE]
> <span data-ttu-id="b0725-194">Lorsque vous supprimez la passerelle VPN, tous les clients connectés sont déconnectés du réseau virtuel sans avertissement.</span><span class="sxs-lookup"><span data-stu-id="b0725-194">When you delete the VPN gateway, all connected clients will be disconnected from the VNet without warning.</span></span>
>
>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="b0725-195">1. Récupérez la passerelle de réseau virtuel que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="b0725-195">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-delete-the-virtual-network-gateway"></a><span data-ttu-id="b0725-196">2. Supprimez la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b0725-196">2. Delete the virtual network gateway.</span></span>

<span data-ttu-id="b0725-197">Vous serez peut-être invité à confirmer la suppression de la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b0725-197">You may be prompted to confirm the deletion of the virtual network gateway.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="b0725-198">À ce stade, votre passerelle de réseau virtuel a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="b0725-198">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="b0725-199">Vous pouvez vous conformer aux étapes suivantes pour supprimer toutes les ressources qui ne sont plus utilisées.</span><span class="sxs-lookup"><span data-stu-id="b0725-199">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="3-delete-the-public-ip-address-resources"></a><span data-ttu-id="b0725-200">3. Supprimez les ressources de l’adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="b0725-200">3. Delete the Public IP address resources</span></span>

<span data-ttu-id="b0725-201">Récupérez les configurations IP de la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b0725-201">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="b0725-202">Récupérez la liste des adresses IP publiques utilisées pour cette passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b0725-202">Get the list of Public IP addresses used for this virtual network gateway.</span></span> <span data-ttu-id="b0725-203">Si la passerelle de réseau virtuel était active-active, vous verrez deux adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="b0725-203">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="b0725-204">Supprimez les adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="b0725-204">Delete the Public IPs.</span></span> <span data-ttu-id="b0725-205">Vous serez peut-être invité à confirmer la suppression de l’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="b0725-205">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="4-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="b0725-206">4. Supprimez le sous-réseau de passerelle et définissez la configuration.</span><span class="sxs-lookup"><span data-stu-id="b0725-206">4. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="b0725-207"><a name="delete"></a>Supprimer une passerelle VPN en supprimant le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="b0725-207"><a name="delete"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="b0725-208">Si vous n’avez pas besoin de conserver de ressources dans le groupe de ressources et que vous voulez simplement recommencer à zéro, vous pouvez supprimer tout un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b0725-208">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="b0725-209">Il s’agit d’un moyen rapide de tout supprimer.</span><span class="sxs-lookup"><span data-stu-id="b0725-209">This is a quick way to remove everything.</span></span> <span data-ttu-id="b0725-210">Les étapes suivantes s’appliquent uniquement au modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b0725-210">The following steps apply only to the Resource Manager deployment model.</span></span>

### <a name="1-get-a-list-of-all-the-resource-groups-in-your-subscription"></a><span data-ttu-id="b0725-211">1. Récupérez la liste des groupes de ressources de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="b0725-211">1. Get a list of all the resource groups in your subscription.</span></span>

```powershell
Get-AzureRmResourceGroup
```

### <a name="2-locate-the-resource-group-that-you-want-to-delete"></a><span data-ttu-id="b0725-212">2. Recherchez le groupe de ressources que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="b0725-212">2. Locate the resource group that you want to delete.</span></span>

<span data-ttu-id="b0725-213">Localisez le groupe de ressources que vous souhaitez supprimer et affichez la liste des ressources qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="b0725-213">Locate the resource group that you want to delete and view the list of resources in that resource group.</span></span> <span data-ttu-id="b0725-214">Dans l’exemple, le nom du groupe de ressources est RG1.</span><span class="sxs-lookup"><span data-stu-id="b0725-214">In the example, the name of the resource group is RG1.</span></span> <span data-ttu-id="b0725-215">Modifiez l’exemple pour récupérer la liste de toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="b0725-215">Modify the example to retrieve a list of all the resources.</span></span>

```powershell
Find-AzureRmResource -ResourceGroupNameContains RG1
```

### <a name="3-verify-the-resources-in-the-list"></a><span data-ttu-id="b0725-216">3. Vérifiez les ressources de la liste.</span><span class="sxs-lookup"><span data-stu-id="b0725-216">3. Verify the resources in the list.</span></span>

<span data-ttu-id="b0725-217">Lorsque la liste est renvoyée, passez-la en revue afin de vérifier que vous souhaitez supprimer toutes les ressources du groupe de ressources, ainsi que le groupe de ressources lui-même.</span><span class="sxs-lookup"><span data-stu-id="b0725-217">When the list is returned, review it to verify that you want to delete all the resources in the resource group, as well as the resource group itself.</span></span> <span data-ttu-id="b0725-218">Si vous voulez conserver certaines des ressources dans le groupe de ressources, utilisez les étapes des sections précédentes de cet article pour supprimer votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="b0725-218">If you want to keep some of the resources in the resource group, use the steps in the earlier sections of this article to delete your gateway.</span></span>

### <a name="4-delete-the-resource-group-and-resources"></a><span data-ttu-id="b0725-219">4. Supprimez le groupe de ressources et les ressources.</span><span class="sxs-lookup"><span data-stu-id="b0725-219">4. Delete the resource group and resources.</span></span>

<span data-ttu-id="b0725-220">Pour supprimer le groupe de ressources et toutes les ressources qu’il contient, modifiez l’exemple et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="b0725-220">To delete the resource group and all the resource contained in the resource group, modify the example and run.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name RG1
```

### <a name="5-check-the-status"></a><span data-ttu-id="b0725-221">5. Vérifiez l’état.</span><span class="sxs-lookup"><span data-stu-id="b0725-221">5. Check the status.</span></span>

<span data-ttu-id="b0725-222">Azure met quelque temps à supprimer toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="b0725-222">It takes some time for Azure to delete all the resources.</span></span> <span data-ttu-id="b0725-223">Vous pouvez vérifier l’état de votre groupe de ressources avec cette applet de commande.</span><span class="sxs-lookup"><span data-stu-id="b0725-223">You can check the status of your resource group by using this cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName RG1
```

<span data-ttu-id="b0725-224">Le résultat retourné indique « Réussi ».</span><span class="sxs-lookup"><span data-stu-id="b0725-224">The result that is returned shows 'Succeeded'.</span></span>

```
ResourceGroupName : RG1
Location          : eastus
ProvisioningState : Succeeded
```