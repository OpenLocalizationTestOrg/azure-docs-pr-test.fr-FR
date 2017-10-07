---
title: "Ajouter une passerelle de réseau virtuel à un réseau virtuel pour ExpressRoute : portail Azure | Microsoft Docs"
description: "Cet article vous explique comment ajouter une passerelle de réseau virtuel à un réseau virtuel Resource Manager déjà créé pour ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: cherylmc
ms.openlocfilehash: 2bd0cf8be87937044ad515a2c6f253b1711bb2bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-the-azure-portal"></a><span data-ttu-id="9d36d-103">Configurer une passerelle de réseau virtuel pour ExpressRoute à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="9d36d-103">Configure a virtual network gateway for ExpressRoute using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9d36d-104">Resource Manager - Portail Azure</span><span class="sxs-lookup"><span data-stu-id="9d36d-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="9d36d-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d36d-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="9d36d-106">Classic - PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d36d-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="9d36d-107">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="9d36d-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="9d36d-108">Cet article détaille la procédure requise pour ajouter une passerelle de réseau virtuel pour un réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="9d36d-108">This article walks you through the steps to add a virtual network gateway for a pre-existing VNet.</span></span> <span data-ttu-id="9d36d-109">Cet article vous montre les étapes nécessaires pour ajouter, redimensionner et supprimer une passerelle de réseau virtuel pour un réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="9d36d-109">This article walks you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="9d36d-110">Les étapes de cette configuration sont spécifiquement adaptées aux réseaux virtuels qui ont été créés à l’aide du modèle de déploiement Resource Manager qui sera utilisé dans une configuration ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d36d-110">The steps for this configuration are specifically for VNets that were created using the Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="9d36d-111">Pour plus d’informations sur les passerelles de réseau virtuel et les paramètres de configuration de passerelle pour ExpressRoute, consultez [À propos des passerelles de réseau virtuel pour ExpressRoute](expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="9d36d-111">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="9d36d-112">Avant tout chose</span><span class="sxs-lookup"><span data-stu-id="9d36d-112">Before beginning</span></span>

<span data-ttu-id="9d36d-113">Les étapes de cette tâche utilisent un réseau virtuel basé sur les valeurs figurant dans la liste de référence de configuration suivante.</span><span class="sxs-lookup"><span data-stu-id="9d36d-113">The steps for this task use a VNet based on the values in the following configuration reference list.</span></span> <span data-ttu-id="9d36d-114">Nous utilisons cette liste dans notre exemple de procédure.</span><span class="sxs-lookup"><span data-stu-id="9d36d-114">We use this list in our example steps.</span></span> <span data-ttu-id="9d36d-115">Vous pouvez copier la liste et l’utiliser en tant que référence, en remplaçant les valeurs par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="9d36d-115">You can copy the list to use as a reference, replacing the values with your own.</span></span>

<span data-ttu-id="9d36d-116">**Liste de référence de configuration**</span><span class="sxs-lookup"><span data-stu-id="9d36d-116">**Configuration reference list**</span></span>

* <span data-ttu-id="9d36d-117">Nom du réseau virtuel : « TestVNet »</span><span class="sxs-lookup"><span data-stu-id="9d36d-117">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="9d36d-118">Espace d’adressage du réseau virtuel : 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="9d36d-118">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="9d36d-119">Nom du sous-réseau : « FrontEnd »</span><span class="sxs-lookup"><span data-stu-id="9d36d-119">Subnet Name = "FrontEnd"</span></span> 
    * <span data-ttu-id="9d36d-120">Espace d’adressage du sous-réseau : « 192.168.1.0/24 »</span><span class="sxs-lookup"><span data-stu-id="9d36d-120">Subnet address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="9d36d-121">Groupe de ressources : « TestRG »</span><span class="sxs-lookup"><span data-stu-id="9d36d-121">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="9d36d-122">Emplacement = « Est des États-Unis »</span><span class="sxs-lookup"><span data-stu-id="9d36d-122">Location = "East US"</span></span>
* <span data-ttu-id="9d36d-123">Nom de sous-réseau de passerelle : « GatewaySubnet » Vous devez toujours nommer un sous-réseau de passerelle *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="9d36d-123">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
    * <span data-ttu-id="9d36d-124">Espace d'adressage du sous-réseau de passerelle : « 192.168.200.0/26 »</span><span class="sxs-lookup"><span data-stu-id="9d36d-124">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="9d36d-125">Nom de la passerelle : « ERGW »</span><span class="sxs-lookup"><span data-stu-id="9d36d-125">Gateway Name = "ERGW"</span></span>
* <span data-ttu-id="9d36d-126">Nom d’adresse IP de la passerelle : « MyERGWVIP »</span><span class="sxs-lookup"><span data-stu-id="9d36d-126">Gateway IP Name = "MyERGWVIP"</span></span>
* <span data-ttu-id="9d36d-127">Type de passerelle : « ExpressRoute ». Ce type est requis pour une configuration ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d36d-127">Gateway type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="9d36d-128">Nom d’adresse IP publique de passerelle = « MyERGWVIP »</span><span class="sxs-lookup"><span data-stu-id="9d36d-128">Gateway Public IP Name = "MyERGWVIP"</span></span>

<span data-ttu-id="9d36d-129">Vous pouvez afficher une [vidéo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network) de ces étapes avant de commencer votre configuration.</span><span class="sxs-lookup"><span data-stu-id="9d36d-129">You can view a [Video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network) of these steps before beginning your configuration.</span></span>

## <a name="create-the-gateway-subnet"></a><span data-ttu-id="9d36d-130">Création d’un sous-réseau de passerelle</span><span class="sxs-lookup"><span data-stu-id="9d36d-130">Create the gateway subnet</span></span>

1. <span data-ttu-id="9d36d-131">Dans le [portail](http://portal.azure.com), accédez au réseau virtuel Resource Manager pour lequel vous souhaitez créer une passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="9d36d-131">In the [portal](http://portal.azure.com), navigate to the Resource Manager virtual network for which you want to create a virtual network gateway.</span></span>
2. <span data-ttu-id="9d36d-132">Dans la section**Paramètres** du panneau de votre réseau virtuel, cliquez sur **Sous-réseaux** pour développer le panneau Sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="9d36d-132">In the **Settings** section of your VNet blade, click **Subnets** to expand the Subnets blade.</span></span>
3. <span data-ttu-id="9d36d-133">Dans le panneau **Sous-réseaux**, cliquez sur **+Sous-réseau de passerelle** pour ouvrir le panneau **Ajouter un sous-réseau**.</span><span class="sxs-lookup"><span data-stu-id="9d36d-133">On the **Subnets** blade, click **+Gateway subnet** to open the **Add subnet** blade.</span></span> 
   
    <span data-ttu-id="9d36d-134">![Ajouter un sous-réseau de passerelle](./media/expressroute-howto-add-gateway-portal-resource-manager/addgwsubnet.png "Ajouter un sous-réseau de passerelle")</span><span class="sxs-lookup"><span data-stu-id="9d36d-134">![Add the gateway subnet](./media/expressroute-howto-add-gateway-portal-resource-manager/addgwsubnet.png "Add the gateway subnet")</span></span>


4. <span data-ttu-id="9d36d-135">Le **Nom** de votre sous-réseau est automatiquement rempli avec la valeur « GatewaySubnet ».</span><span class="sxs-lookup"><span data-stu-id="9d36d-135">The **Name** for your subnet is automatically filled in with the value 'GatewaySubnet'.</span></span> <span data-ttu-id="9d36d-136">Cette valeur est nécessaire pour qu’Azure puisse reconnaître le sous-réseau en tant que sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="9d36d-136">This value is required in order for Azure to recognize the subnet as the gateway subnet.</span></span> <span data-ttu-id="9d36d-137">Ajustez les valeurs de **plage d’adresses** renseignées automatiquement pour qu’elles correspondent à la configuration requise.</span><span class="sxs-lookup"><span data-stu-id="9d36d-137">Adjust the auto-filled **Address range** values to match your configuration requirements.</span></span> <span data-ttu-id="9d36d-138">Nous vous recommandons de créer un sous-réseau de passerelle avec /27 ou plus (/26, /25, etc.).</span><span class="sxs-lookup"><span data-stu-id="9d36d-138">We recommend creating a gateway subnet with a /27 or larger (/26, /25, etc.).</span></span> <span data-ttu-id="9d36d-139">Puis, cliquez sur **OK** pour enregistrer les valeurs et créer le sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="9d36d-139">Then, click **OK** to save the values and create the gateway subnet.</span></span>

    <span data-ttu-id="9d36d-140">![Ajout du sous-réseau](./media/expressroute-howto-add-gateway-portal-resource-manager/addsubnetgw.png "Ajout du sous-réseau")</span><span class="sxs-lookup"><span data-stu-id="9d36d-140">![Adding the subnet](./media/expressroute-howto-add-gateway-portal-resource-manager/addsubnetgw.png "Adding the subnet")</span></span>

## <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="9d36d-141">Créer la passerelle de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="9d36d-141">Create the virtual network gateway</span></span>

1. <span data-ttu-id="9d36d-142">Dans le portail, sur le côté gauche, cliquez sur **+**, puis tapez « Passerelle de réseau virtuel » dans la recherche.</span><span class="sxs-lookup"><span data-stu-id="9d36d-142">In the portal, on the left side, click **+** and type 'Virtual Network Gateway' in search.</span></span> <span data-ttu-id="9d36d-143">Recherchez **passerelle de réseau virtuel** dans la zone de recherche et cliquez sur l’entrée.</span><span class="sxs-lookup"><span data-stu-id="9d36d-143">Locate **Virtual network gateway** in the search return and click the entry.</span></span> <span data-ttu-id="9d36d-144">Dans le panneau **Passerelle de réseau virtuel**, cliquez sur **Créer** en bas du panneau.</span><span class="sxs-lookup"><span data-stu-id="9d36d-144">On the **Virtual network gateway** blade, click **Create** at the bottom of the blade.</span></span> <span data-ttu-id="9d36d-145">Cette opération ouvre le panneau **Créer une passerelle de réseau virtuel**.</span><span class="sxs-lookup"><span data-stu-id="9d36d-145">This opens the **Create virtual network gateway** blade.</span></span>
2. <span data-ttu-id="9d36d-146">Dans le panneau **Créer une passerelle réseau virtuel**, renseignez les valeurs pour votre passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="9d36d-146">On the **Create virtual network gateway** blade, fill in the values for your virtual network gateway.</span></span>

    <span data-ttu-id="9d36d-147">![Champs du panneau Créer une passerelle de réseau virtuel](./media/expressroute-howto-add-gateway-portal-resource-manager/gw.png "Champs du panneau Créer une passerelle de réseau virtuel")</span><span class="sxs-lookup"><span data-stu-id="9d36d-147">![Create virtual network gateway blade fields](./media/expressroute-howto-add-gateway-portal-resource-manager/gw.png "Create virtual network gateway blade fields")</span></span>
3. <span data-ttu-id="9d36d-148">**Nom** : nommez votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="9d36d-148">**Name**: Name your gateway.</span></span> <span data-ttu-id="9d36d-149">Cela ne revient pas au même que de nommer un sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="9d36d-149">This is not the same as naming a gateway subnet.</span></span> <span data-ttu-id="9d36d-150">Il s’agit du nom de l’objet de passerelle que vous créez.</span><span class="sxs-lookup"><span data-stu-id="9d36d-150">It's the name of the gateway object you are creating.</span></span>
4. <span data-ttu-id="9d36d-151">**Type de passerelle** : sélectionnez **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="9d36d-151">**Gateway type**: Select **ExpressRoute**.</span></span>
5. <span data-ttu-id="9d36d-152">**Référence** : sélectionnez la référence de passerelle dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="9d36d-152">**SKU**: Select the gateway SKU from the dropdown.</span></span>
6. <span data-ttu-id="9d36d-153">**Emplacement** : définissez le champ **Emplacement** pour pointer sur l’emplacement dans lequel le réseau virtuel est situé.</span><span class="sxs-lookup"><span data-stu-id="9d36d-153">**Location**: Adjust the **Location** field to point to the location where your virtual network is located.</span></span> <span data-ttu-id="9d36d-154">Si l’emplacement ne pointe pas vers la région où se trouve votre réseau virtuel, le réseau virtuel n’apparaît pas dans la liste déroulante « Choisir un réseau virtuel ».</span><span class="sxs-lookup"><span data-stu-id="9d36d-154">If the location is not pointing to the region where your virtual network resides, the virtual network doesn't appear in the 'Choose a virtual network' dropdown.</span></span>
7. <span data-ttu-id="9d36d-155">Choisissez le réseau virtuel auquel vous souhaitez ajouter cette passerelle.</span><span class="sxs-lookup"><span data-stu-id="9d36d-155">Choose the virtual network to which you want to add this gateway.</span></span> <span data-ttu-id="9d36d-156">Cliquez sur **Réseau virtuel** pour ouvrir le panneau **Choisir un réseau virtuel**.</span><span class="sxs-lookup"><span data-stu-id="9d36d-156">Click **Virtual network** to open the **Choose a virtual network** blade.</span></span> <span data-ttu-id="9d36d-157">Sélectionnez le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="9d36d-157">Select the VNet.</span></span> <span data-ttu-id="9d36d-158">Si vous ne voyez pas votre réseau virtuel, assurez-vous que le champ **Emplacement** pointe sur la région dans laquelle se trouve votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="9d36d-158">If you don't see your VNet, make sure the **Location** field is pointing to the region in which your virtual network is located.</span></span>
9. <span data-ttu-id="9d36d-159">Définissez une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="9d36d-159">Choose a public IP address.</span></span> <span data-ttu-id="9d36d-160">Cliquez sur **l’adresse IP publique** pour ouvrir le panneau **Choisir une adresse IP publique**.</span><span class="sxs-lookup"><span data-stu-id="9d36d-160">Click **Public IP address** to open the **Choose public IP address** blade.</span></span> <span data-ttu-id="9d36d-161">Cliquez sur **Créer** pour ouvrir le panneau **Créer une adresse IP publique**.</span><span class="sxs-lookup"><span data-stu-id="9d36d-161">Click **+Create New** to open the **Create public IP address blade**.</span></span> <span data-ttu-id="9d36d-162">Donnez à un nom à votre adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="9d36d-162">Input a name for your public IP address.</span></span> <span data-ttu-id="9d36d-163">Ce panneau crée un objet d’adresse IP publique à laquelle une adresse IP publique sera être affectée dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="9d36d-163">This blade creates a public IP address object to which a public IP address will be dynamically assigned.</span></span> <span data-ttu-id="9d36d-164">Cliquez sur **OK** pour enregistrer vos modifications à ce panneau.</span><span class="sxs-lookup"><span data-stu-id="9d36d-164">Click **OK** to save your changes to this blade.</span></span>
10. <span data-ttu-id="9d36d-165">**Abonnement** : vérifiez que l’abonnement approprié est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="9d36d-165">**Subscription**: Verify that the correct subscription is selected.</span></span>
11. <span data-ttu-id="9d36d-166">**Groupe de ressources** : ce paramètre est déterminé par le réseau virtuel que vous sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="9d36d-166">**Resource group**: This setting is determined by the Virtual Network that you select.</span></span>
12. <span data-ttu-id="9d36d-167">Ne changez pas **l’emplacement** après avoir spécifié les paramètres ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="9d36d-167">Don't adjust the **Location** after you've specified the previous settings.</span></span>
13. <span data-ttu-id="9d36d-168">Vérifiez les paramètres.</span><span class="sxs-lookup"><span data-stu-id="9d36d-168">Verify the settings.</span></span> <span data-ttu-id="9d36d-169">Si vous souhaitez que votre passerelle apparaisse sur le tableau de bord, vous pouvez sélectionner **Épingler au tableau de bord** en bas du panneau.</span><span class="sxs-lookup"><span data-stu-id="9d36d-169">If you want your gateway to appear on the dashboard, you can select **Pin to dashboard** at the bottom of the blade.</span></span>
14. <span data-ttu-id="9d36d-170">Cliquez sur **Créer** pour créer la passerelle.</span><span class="sxs-lookup"><span data-stu-id="9d36d-170">Click **Create** to begin creating the gateway.</span></span> <span data-ttu-id="9d36d-171">Les paramètres sont validés et la passerelle se déploie.</span><span class="sxs-lookup"><span data-stu-id="9d36d-171">The settings are validated and the gateway deploys.</span></span> <span data-ttu-id="9d36d-172">La création d’une passerelle de réseau virtuel peut prendre jusqu’à 45 minutes.</span><span class="sxs-lookup"><span data-stu-id="9d36d-172">Creating virtual network gateway can take up to 45 minutes to complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d36d-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9d36d-173">Next steps</span></span>
<span data-ttu-id="9d36d-174">Une fois que vous avez créé la passerelle de réseau virtuel, vous pouvez lier votre réseau virtuel à un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9d36d-174">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="9d36d-175">Consultez [Liaison d’un réseau virtuel à un circuit ExpressRoute](expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9d36d-175">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>