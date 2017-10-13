---
title: "Connexion d’Azure Stack à Azure à l’aide d’ExpressRoute"
description: "Découvrez comment connecter des réseaux virtuels dans Azure Stack à des réseaux virtuels dans Azure à l’aide d’ExpressRoute."
services: azure-stack
documentationcenter: 
author: victorar
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: victorh
ms.openlocfilehash: aa6973939c6cfe0688f5781fdcea5d39670249df
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="connect-azure-stack-to-azure-using-expressroute"></a><span data-ttu-id="b9ca0-103">Connexion d’Azure Stack à Azure à l’aide d’ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="b9ca0-103">Connect Azure Stack to Azure using ExpressRoute</span></span>

<span data-ttu-id="b9ca0-104">*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*</span><span class="sxs-lookup"><span data-stu-id="b9ca0-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="b9ca0-105">Deux méthodes vous permettent de connecter des réseaux virtuels Azure Stack à des réseaux virtuels Azure :</span><span class="sxs-lookup"><span data-stu-id="b9ca0-105">There are two supported methods to connect virtual networks in Azure Stack to virtual networks in Azure:</span></span>
   * <span data-ttu-id="b9ca0-106">**De site à site**</span><span class="sxs-lookup"><span data-stu-id="b9ca0-106">**Site-to-Site**</span></span>

     <span data-ttu-id="b9ca0-107">Connexion VPN sur IPsec (IKE v1 et IKE v2).</span><span class="sxs-lookup"><span data-stu-id="b9ca0-107">A VPN connection over IPsec (IKE v1 and IKE v2).</span></span> <span data-ttu-id="b9ca0-108">Ce type de connexion requiert un périphérique VPN ou le service RRAS.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-108">This type of connection requires a VPN device or RRAS.</span></span> <span data-ttu-id="b9ca0-109">Pour en savoir plus, consultez l’article relatif à la [connexion d’Azure Stack à Azure à l’aide d’un VPN](azure-stack-connect-vpn.md).</span><span class="sxs-lookup"><span data-stu-id="b9ca0-109">For more information, see [Connect Azure Stack to Azure using VPN](azure-stack-connect-vpn.md).</span></span>
   * <span data-ttu-id="b9ca0-110">**ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="b9ca0-110">**ExpressRoute**</span></span>

     <span data-ttu-id="b9ca0-111">Connexion directe à Azure depuis votre déploiement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-111">A direct connection to Azure from your Azure Stack deployment.</span></span> <span data-ttu-id="b9ca0-112">ExpressRoute n’est **pas** une connexion VPN établie via le réseau Internet public.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-112">ExpressRoute is **not** a VPN connection over the public Internet.</span></span> <span data-ttu-id="b9ca0-113">Pour en savoir plus sur ExpressRoute, consultez la rubrique [Présentation d’ExpressRoute](../expressroute/expressroute-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b9ca0-113">For more information about Azure ExpressRoute, see [ExpressRoute overview](../expressroute/expressroute-introduction.md).</span></span>

<span data-ttu-id="b9ca0-114">Cet article montre comment utiliser ExpressRoute pour connecter Azure Stack à Azure.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-114">This article shows an example using ExpressRoute to connect Azure Stack to Azure.</span></span>
## <a name="requirements"></a><span data-ttu-id="b9ca0-115">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="b9ca0-115">Requirements</span></span>
<span data-ttu-id="b9ca0-116">Pour connecter Azure Stack et Azure à l’aide d’ExpressRoute, tenez compte des critères suivants :</span><span class="sxs-lookup"><span data-stu-id="b9ca0-116">The following are specific requirements to connect Azure Stack and Azure using ExpressRoute:</span></span>
* <span data-ttu-id="b9ca0-117">Vous devez disposer d’un abonnement Azure pour créer un circuit ExpressRoute et des réseaux virtuels dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-117">An Azure subscription to create an ExpressRoute circuit and VNets in Azure.</span></span>
* <span data-ttu-id="b9ca0-118">Un circuit ExpressRoute doit être configuré via un [fournisseur de connectivité](../expressroute/expressroute-locations.md).</span><span class="sxs-lookup"><span data-stu-id="b9ca0-118">A provisioned ExpressRoute circuit through a [connectivity provider](../expressroute/expressroute-locations.md).</span></span>
* <span data-ttu-id="b9ca0-119">Un routeur avec le circuit ExpressRoute connecté à ses ports WAN.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-119">A router that has the ExpressRoute circuit connected to its WAN ports.</span></span>
* <span data-ttu-id="b9ca0-120">Le côté LAN du routeur doit être lié à la passerelle multi-locataire d’Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-120">The LAN side of the router is linked to the Azure Stack Multitenant Gateway.</span></span>
* <span data-ttu-id="b9ca0-121">Le routeur doit prendre en charge les connexions VPN de site à site entre son interface LAN et la passerelle multi-locataire d’Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-121">The router must support Site-to-Site VPN connections between its LAN interface and Azure Stack Multitenant Gateway.</span></span>
* <span data-ttu-id="b9ca0-122">Si plus d’un locataire est ajouté à votre déploiement Azure Stack, le routeur doit être en mesure de créer plusieurs VRF (Virtual Routing and Forwarding).</span><span class="sxs-lookup"><span data-stu-id="b9ca0-122">If more than one tenant is added in your Azure Stack deployment, the router must be able to create multiple VRFs (Virtual Routing and Forwarding).</span></span>

<span data-ttu-id="b9ca0-123">Le schéma suivant représente la mise en réseau conceptuelle une fois la configuration terminée :</span><span class="sxs-lookup"><span data-stu-id="b9ca0-123">The following diagram shows a conceptual networking view after you complete the configuration:</span></span>

![Schéma conceptuel](media/azure-stack-connect-expressroute/Conceptual.png)

<span data-ttu-id="b9ca0-125">**Schéma 1**</span><span class="sxs-lookup"><span data-stu-id="b9ca0-125">**Diagram 1**</span></span>

<span data-ttu-id="b9ca0-126">Le schéma d’architecture suivant montre comment plusieurs locataires se connectent à Azure depuis l’infrastructure Azure Stack par le biais du routeur ExpressRoute au niveau de la périphérie Microsoft :</span><span class="sxs-lookup"><span data-stu-id="b9ca0-126">The following architecture diagram shows how multiple tenants connect from the Azure Stack infrastructure through the ExpressRoute router to Azure at the Microsoft edge:</span></span>

![Diagramme de l’architecture](media/azure-stack-connect-expressroute/Architecture.png)

<span data-ttu-id="b9ca0-128">**Schéma 2 :**</span><span class="sxs-lookup"><span data-stu-id="b9ca0-128">**Diagram 2**</span></span>

<span data-ttu-id="b9ca0-129">L’exemple présenté dans cet article utilise la même architecture pour établir une connexion à Azure via l’homologation privée ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-129">The example shown in this article uses the same architecture to connect to Azure via ExpressRoute private peering.</span></span> <span data-ttu-id="b9ca0-130">Pour ce faire, une connexion VPN de site à site est établie entre la passerelle de réseau virtuel dans Azure Stack et un routeur ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-130">It is done using a Site-to-Site VPN connection from the virtual network gateway in Azure Stack to an ExpressRoute router.</span></span> <span data-ttu-id="b9ca0-131">Les étapes suivantes vous expliquent comment créer une connexion de bout en bout entre deux réseaux virtuels, depuis deux locataires différents dans Azure Stack, et leurs réseaux virtuels respectifs dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-131">The following steps in this article show how to create an end-to-end connection between two VNets from two different tenants in Azure Stack to their respective VNets in Azure.</span></span> <span data-ttu-id="b9ca0-132">Vous pouvez soit ajouter autant de réseaux virtuels locataires que vous le souhaitez et répéter les étapes pour chaque locataire, soit utiliser cet exemple pour déployer uniquement un seul réseau virtuel locataire.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-132">You can choose to add as many tenant VNets and replicate the steps for each tenant or use this example to deploy just a single tenant VNet.</span></span>

## <a name="configure-azure-stack"></a><span data-ttu-id="b9ca0-133">Configurer Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b9ca0-133">Configure Azure Stack</span></span>
<span data-ttu-id="b9ca0-134">Maintenant, vous devez créer les ressources dont vous avez besoin pour configurer votre environnement Azure Stack comme réseau locataire.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-134">Now you create the resources you need to set up your Azure Stack environment as a tenant.</span></span> <span data-ttu-id="b9ca0-135">Les étapes suivantes vous montrent ce que vous devez faire.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-135">The following steps illustrate what you need to do.</span></span> <span data-ttu-id="b9ca0-136">Ces instructions expliquent comment créer des ressources à l’aide du portail Azure Stack, mais vous pouvez également utiliser PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-136">These instructions show how to create resources using the Azure Stack portal, but you can also use PowerShell.</span></span>

![Étapes de création des ressources réseau](media/azure-stack-connect-expressroute/image2.png)
### <a name="before-you-begin"></a><span data-ttu-id="b9ca0-138">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="b9ca0-138">Before you begin</span></span>
<span data-ttu-id="b9ca0-139">Avant de passer à la configuration, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b9ca0-139">Before you start the configuration, you need:</span></span>
* <span data-ttu-id="b9ca0-140">Un déploiement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-140">An Azure Stack deployment.</span></span>

   <span data-ttu-id="b9ca0-141">Pour en savoir plus sur le déploiement du Kit de développement Azure Stack, consultez la rubrique relative au [démarrage rapide du déploiement du Kit de développement Azure Stack](azure-stack-deploy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b9ca0-141">For information about deploying Azure Stack Development Kit, see [Azure Stack Development Kit deployment quickstart](azure-stack-deploy-overview.md).</span></span>
* <span data-ttu-id="b9ca0-142">Une offre sur Azure Stack à laquelle votre utilisateur peut souscrire.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-142">An offer on Azure Stack that your user can subscribe to.</span></span>

  <span data-ttu-id="b9ca0-143">Pour obtenir des instructions, consultez la rubrique relative à la [mise à disposition de machines virtuelles à vos utilisateurs Azure Stack](azure-stack-tutorial-tenant-vm.md).</span><span class="sxs-lookup"><span data-stu-id="b9ca0-143">For instructions, see [Make virtual machines available to your Azure Stack users](azure-stack-tutorial-tenant-vm.md).</span></span>

### <a name="create-network-resources-in-azure-stack"></a><span data-ttu-id="b9ca0-144">Créer des ressources réseau dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b9ca0-144">Create network resources in Azure Stack</span></span>

<span data-ttu-id="b9ca0-145">Suivez les procédures ci-dessous pour créer les ressources réseau nécessaires dans Azure Stack pour chaque locataire :</span><span class="sxs-lookup"><span data-stu-id="b9ca0-145">Use the following procedures to create the required network resources in Azure Stack for each tenant:</span></span>

#### <a name="create-the-virtual-network-and-vm-subnet"></a><span data-ttu-id="b9ca0-146">Créer le réseau virtuel et le sous-réseau de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b9ca0-146">Create the virtual network and VM subnet</span></span>
1. <span data-ttu-id="b9ca0-147">Connectez-vous au portail utilisateur avec un compte d’utilisateur (locataire).</span><span class="sxs-lookup"><span data-stu-id="b9ca0-147">Sign in the user portal with a user (tenant) account.</span></span>

2. <span data-ttu-id="b9ca0-148">Dans le portail, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-148">In the portal, click **New**.</span></span>

   ![](media/azure-stack-connect-expressroute/MAS-new.png)

3. <span data-ttu-id="b9ca0-149">Sélectionnez **Mise en réseau** dans le menu Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-149">Select **Networking** from the Marketplace menu.</span></span>

4. <span data-ttu-id="b9ca0-150">Cliquez sur **Réseau virtuel** dans le menu.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-150">Click **Virtual network** on the menu.</span></span>

5. <span data-ttu-id="b9ca0-151">Saisissez les valeurs correspondant à chaque champ à l’aide du tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="b9ca0-151">Type the values into the appropriate fields using the following table:</span></span>

   |<span data-ttu-id="b9ca0-152">Champ</span><span class="sxs-lookup"><span data-stu-id="b9ca0-152">Field</span></span>  |<span data-ttu-id="b9ca0-153">Valeur</span><span class="sxs-lookup"><span data-stu-id="b9ca0-153">Value</span></span>  |
   |---------|---------|
   |<span data-ttu-id="b9ca0-154">Nom</span><span class="sxs-lookup"><span data-stu-id="b9ca0-154">Name</span></span>     |<span data-ttu-id="b9ca0-155">Tenant1VNet1</span><span class="sxs-lookup"><span data-stu-id="b9ca0-155">Tenant1VNet1</span></span>         |
   |<span data-ttu-id="b9ca0-156">Espace d’adressage</span><span class="sxs-lookup"><span data-stu-id="b9ca0-156">Address space</span></span>     |<span data-ttu-id="b9ca0-157">10.1.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b9ca0-157">10.1.0.0/16</span></span>|
   |<span data-ttu-id="b9ca0-158">Nom du sous-réseau</span><span class="sxs-lookup"><span data-stu-id="b9ca0-158">Subnet name</span></span>     |<span data-ttu-id="b9ca0-159">Tenant1-Sub1</span><span class="sxs-lookup"><span data-stu-id="b9ca0-159">Tenant1-Sub1</span></span>|
   |<span data-ttu-id="b9ca0-160">Plage d’adresses de sous-réseau</span><span class="sxs-lookup"><span data-stu-id="b9ca0-160">Subnet address range</span></span>     |<span data-ttu-id="b9ca0-161">10.1.1.0/24</span><span class="sxs-lookup"><span data-stu-id="b9ca0-161">10.1.1.0/24</span></span>|

6. <span data-ttu-id="b9ca0-162">Vous devez voir l’abonnement que vous avez créé précédemment rempli dans le champ **Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-162">You should see the Subscription you created earlier populated in the **Subscription** field.</span></span>

    <span data-ttu-id="b9ca0-163">a.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-163">a.</span></span> <span data-ttu-id="b9ca0-164">Dans le champ Groupe de ressources, créez un groupe de ressources ou, si vous en avez déjà un, sélectionnez **Utiliser existant**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-164">For Resource Group, you can either create a Resource Group or if you already have one, select **Use existing**.</span></span>

    <span data-ttu-id="b9ca0-165">b.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-165">b.</span></span> <span data-ttu-id="b9ca0-166">Vérifiez l’emplacement par défaut.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-166">Verify the default location.</span></span>

    <span data-ttu-id="b9ca0-167">c.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-167">c.</span></span> <span data-ttu-id="b9ca0-168">Cliquez sur **Épingler au tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-168">Click **Pin to dashboard**.</span></span>

    <span data-ttu-id="b9ca0-169">d.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-169">d.</span></span> <span data-ttu-id="b9ca0-170">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-170">Click **Create**.</span></span>



#### <a name="create-the-gateway-subnet"></a><span data-ttu-id="b9ca0-171">Créer le sous-réseau de passerelle</span><span class="sxs-lookup"><span data-stu-id="b9ca0-171">Create the gateway subnet</span></span>
1. <span data-ttu-id="b9ca0-172">Ouvrez la ressource de réseau virtuel que vous avez créée (Tenant1VNet1) depuis le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-172">Open the Virtual Network resource you created (Tenant1VNet1) from the dashboard.</span></span>
2. <span data-ttu-id="b9ca0-173">Dans la section Paramètres, sélectionnez **Sous-réseaux**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-173">On the Settings section, select **Subnets**.</span></span>
3. <span data-ttu-id="b9ca0-174">Cliquez sur **Sous-réseau de passerelle** pour ajouter un sous-réseau de passerelle au réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-174">Click **Gateway Subnet** to add a gateway subnet to the virtual network.</span></span>
   
    ![](media/azure-stack-connect-expressroute/gatewaysubnet.png)
4. <span data-ttu-id="b9ca0-175">Par défaut, le nom du sous-réseau est défini sur **GatewaySubnet**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-175">The name of the subnet is set to **GatewaySubnet** by default.</span></span>
   <span data-ttu-id="b9ca0-176">Les sous-réseaux de passerelle sont des éléments spéciaux et doivent porter ce nom pour fonctionner correctement.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-176">Gateway subnets are special and must have this specific name to function properly.</span></span>
5. <span data-ttu-id="b9ca0-177">Dans le champ **Plage d’adresses**, vérifiez que **10.1.0.0/24** est bien l’adresse indiquée.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-177">In the **Address range** field, verify the address is **10.1.0.0/24**.</span></span>
6. <span data-ttu-id="b9ca0-178">Cliquez sur **OK** pour créer le sous réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-178">Click **OK** to create the gateway subnet.</span></span>

#### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="b9ca0-179">Créer la passerelle de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="b9ca0-179">Create the virtual network gateway</span></span>
1. <span data-ttu-id="b9ca0-180">Dans le portail utilisateur Azure Stack, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-180">In the Azure Stack user portal, click **New**.</span></span>
   
2. <span data-ttu-id="b9ca0-181">Sélectionnez **Mise en réseau** dans le menu Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-181">Select **Networking** from the Marketplace menu.</span></span>
3. <span data-ttu-id="b9ca0-182">Sélectionnez **Passerelle de réseau virtuel** dans la liste des ressources réseau.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-182">Select **Virtual network gateway** from the list of network resources.</span></span>
4. <span data-ttu-id="b9ca0-183">Dans le champ **nom**, entrez **GW1**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-183">In the **Name** field type **GW1**.</span></span>
5. <span data-ttu-id="b9ca0-184">Cliquez sur l’élément **Réseau virtuel** pour choisir un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-184">Click the **Virtual network** item to choose a virtual network.</span></span>
   <span data-ttu-id="b9ca0-185">Sélectionnez **Tenant1VNet1** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-185">Select **Tenant1VNet1** from the list.</span></span>
6. <span data-ttu-id="b9ca0-186">Cliquez sur l’élément de menu **Adresse IP publique**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-186">Click the **Public IP address** menu item.</span></span> <span data-ttu-id="b9ca0-187">Lorsque la section **Choisir une adresse IP publique** s’affiche, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-187">When the **Choose public IP address** section opens click **Create new**.</span></span>
7. <span data-ttu-id="b9ca0-188">Dans le champ **Nom**, entrez **GW1-PiP**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-188">In the **Name** field, type **GW1-PiP** and click **OK**.</span></span>
8. <span data-ttu-id="b9ca0-189">Par défaut, le **type de VPN** doit être défini sur **Basé sur un itinéraire**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-189">The **VPN type** should have **Route-based** selected by default.</span></span>
    <span data-ttu-id="b9ca0-190">Conservez ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-190">Keep this setting.</span></span>
9. <span data-ttu-id="b9ca0-191">Vérifiez que l’**abonnement** et l’**emplacement** sont corrects.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-191">Verify that **Subscription** and **Location** are correct.</span></span> <span data-ttu-id="b9ca0-192">Vous pouvez épingler la ressource au tableau de bord si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-192">You can pin the resource to the Dashboard if you want.</span></span> <span data-ttu-id="b9ca0-193">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-193">Click **Create**.</span></span>

#### <a name="create-the-local-network-gateway"></a><span data-ttu-id="b9ca0-194">Créer la passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="b9ca0-194">Create the local network gateway</span></span>

<span data-ttu-id="b9ca0-195">La passerelle de réseau local indique la passerelle distante présente à l’autre extrémité de la connexion VPN.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-195">The purpose of the Local network gateway resource is to indicate the remote gateway at the other end of the VPN connection.</span></span> <span data-ttu-id="b9ca0-196">Pour cet exemple, la partie distante est la sous-interface LAN du routeur ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-196">For this example, the remote side is the LAN subinterface of the ExpressRoute router.</span></span> <span data-ttu-id="b9ca0-197">L’adresse distante de Tenant 1 (locataire 1) est 10.60.3.255, comme indiqué dans le schéma 2.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-197">For Tenant 1 in this example, the remote address is 10.60.3.255 as shown in Diagram 2.</span></span>

1. <span data-ttu-id="b9ca0-198">Connectez-vous à l’ordinateur physique Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-198">Log in to the Azure Stack physical machine.</span></span>
2. <span data-ttu-id="b9ca0-199">Connectez-vous au portail utilisateur avec votre compte d’utilisateur, puis cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-199">Sign in to the user portal with your user account and click **New**.</span></span>
3. <span data-ttu-id="b9ca0-200">Sélectionnez **Mise en réseau** dans le menu Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-200">Select **Networking** from the Marketplace menu.</span></span>
4. <span data-ttu-id="b9ca0-201">Sélectionnez **Passerelle de réseau local** dans la liste des ressources.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-201">Select **local network gateway** from the list of resources.</span></span>
5. <span data-ttu-id="b9ca0-202">Dans le champ **Nom**, saisissez **ER-Router-GW**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-202">In the **Name** field type **ER-Router-GW**.</span></span>
6. <span data-ttu-id="b9ca0-203">Pour le champ **Adresse IP**, reportez-vous au schéma 2.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-203">For the **IP address** field, refer to Diagram 2.</span></span> <span data-ttu-id="b9ca0-204">L’adresse IP de la sous-interface LAN du routeur ExpressRoute pour le locataire 1 est 10.60.3.255.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-204">The IP address of the ExpressRoute router's LAN subinterface for Tenant 1 is 10.60.3.255.</span></span> <span data-ttu-id="b9ca0-205">Pour votre propre environnement, entrez l’adresse IP de l’interface correspondante de votre routeur.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-205">For your own environment, type the IP address of your router's corresponding interface.</span></span>
7. <span data-ttu-id="b9ca0-206">Dans le champ **Espace d’adressage**, entrez l’espace d’adressage des réseaux virtuels auxquels se connecter dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-206">In the **Address Space** field, type the address space of the VNets that you want to connect to in Azure.</span></span> <span data-ttu-id="b9ca0-207">Pour cet exemple, reportez-vous au schéma 2.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-207">For this example, refer to Diagram 2.</span></span> <span data-ttu-id="b9ca0-208">Pour le locataire 1, les sous-réseaux requis sont **192.168.2.0/24** (il s’agit du réseau virtuel Hub dans Azure) et **10.100.0.0/16** (il s’agit du réseau virtuel Spoke dans Azure).</span><span class="sxs-lookup"><span data-stu-id="b9ca0-208">For Tenant 1, notice that the required subnets are **192.168.2.0/24** (this is the Hub Vnet in Azure) and **10.100.0.0/16** (this is the Spoke VNet in Azure).</span></span> <span data-ttu-id="b9ca0-209">Entrez les sous-réseaux correspondants pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-209">Type the corresponding subnets for your own environment.</span></span>
   > [!IMPORTANT]
   > <span data-ttu-id="b9ca0-210">Cet exemple suppose que vous utilisiez des itinéraires statiques pour la connexion VPN de site à site entre la passerelle Azure Stack et le routeur ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-210">This example assumes you are using static routes for the Site-to-Site VPN connection between the Azure Stack gateway and the ExpressRoute router.</span></span>

8. <span data-ttu-id="b9ca0-211">Vérifiez que les champs **Abonnement**, **Groupe de ressources** et **Emplacement** sont corrects, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-211">Verify that your **Subscription**, **Resource Group**, and **Location** are all correct and click **Create**.</span></span>

#### <a name="create-the-connection"></a><span data-ttu-id="b9ca0-212">Créer la connexion</span><span class="sxs-lookup"><span data-stu-id="b9ca0-212">Create the connection</span></span>
1. <span data-ttu-id="b9ca0-213">Dans le portail utilisateur Azure Stack, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-213">In the Azure Stack user portal, click **New**.</span></span>
2. <span data-ttu-id="b9ca0-214">Sélectionnez **Mise en réseau** dans le menu Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-214">Select **Networking** from the Marketplace menu.</span></span>
3. <span data-ttu-id="b9ca0-215">Sélectionnez **Connexion** dans la liste des ressources.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-215">Select **Connection** from the list of resources.</span></span>
4. <span data-ttu-id="b9ca0-216">Dans la section des paramètres **De base**, choisissez **Site à site (IPSec)** comme **Type de connexion**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-216">In the **Basics** settings section, choose **Site-to-site (IPSec)** as the **Connection type**.</span></span>
5. <span data-ttu-id="b9ca0-217">Sélectionnez l’**abonnement**, le **groupe de ressources** et l’**emplacement**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-217">Select the **Subscription**, **Resource Group**, and **Location** and click **OK**.</span></span>
6. <span data-ttu-id="b9ca0-218">Dans la section **Paramètres**, cliquez sur **Passerelle de réseau virtuel**, puis sur **GW1**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-218">In the **Settings** section,  click **Virtual network gateway** click **GW1**.</span></span>
7. <span data-ttu-id="b9ca0-219">Cliquez sur **Passerelle de réseau local**, puis sur **ER Router GW**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-219">Click **Local network gateway**, and click **ER Router GW**.</span></span>
8. <span data-ttu-id="b9ca0-220">Dans le champ **Nom de la connexion**, entrez **ConnectToAzure**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-220">In the **Connection Name** field, type **ConnectToAzure**.</span></span>
9. <span data-ttu-id="b9ca0-221">Dans le champ **Clé partagée (PSK)**, entrez **abc123**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-221">In the **Shared key (PSK)** field, type **abc123** and click **OK**.</span></span>
10. <span data-ttu-id="b9ca0-222">Dans la section **Résumé** , cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-222">On the **Summary** section, click **OK**.</span></span>

    <span data-ttu-id="b9ca0-223">Une fois la connexion créée, l’adresse IP publique est utilisée par la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-223">After the connection is created, you can see the public IP address used by the virtual network gateway.</span></span> <span data-ttu-id="b9ca0-224">Pour rechercher l’adresse dans le portail Azure Stack, accédez à votre passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-224">To find the address in the Azure Stack portal, browse to your Virtual network gateway.</span></span> <span data-ttu-id="b9ca0-225">Dans **Vue d’ensemble**, recherchez l’**adresse IP publique**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-225">In **Overview**, find the **Public IP address**.</span></span> <span data-ttu-id="b9ca0-226">Notez cette adresse ; vous devrez la renseigner dans *Adresse IP interne* dans la section suivante (si votre déploiement l’exige).</span><span class="sxs-lookup"><span data-stu-id="b9ca0-226">Note this address; you will use it as the *Internal IP address* in the next section (if applicable for your deployment).</span></span>

    ![](media/azure-stack-connect-expressroute/GWPublicIP.png)

#### <a name="create-a-virtual-machine"></a><span data-ttu-id="b9ca0-227">Création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b9ca0-227">Create a virtual machine</span></span>
<span data-ttu-id="b9ca0-228">Pour valider les données transitant via la connexion VPN, vous avez besoin de machines virtuelles pour envoyer et recevoir des données dans le réseau virtuel d’Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-228">To validate data traveling through the VPN Connection, you need virtual machines to send and receive data in the Azure Stack Vnet.</span></span> <span data-ttu-id="b9ca0-229">Créez d’abord une machine virtuelle, puis ajoutez-la au sous-réseau de machine virtuelle de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-229">Create a virtual machine now and put it in your VM subnet in your virtual network.</span></span>

1. <span data-ttu-id="b9ca0-230">Dans le portail utilisateur Azure Stack, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-230">In the Azure Stack user portal, click **New**.</span></span>
2. <span data-ttu-id="b9ca0-231">Sélectionnez **Machines virtuelles** dans le menu Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-231">Select **Virtual Machines** from the Marketplace menu.</span></span>
3. <span data-ttu-id="b9ca0-232">Dans la liste des images de machine virtuelle, sélectionnez l’image **Windows Server 2016 Datacenter Eval**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-232">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Eval** image and click **Create**.</span></span>
4. <span data-ttu-id="b9ca0-233">Dans la section **De base**, dans le champ **Nom**, entrez **VM01**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-233">On the **Basics** section, in the **Name** field type **VM01**.</span></span>
5. <span data-ttu-id="b9ca0-234">Entrez un nom d’utilisateur et un mot de passe valides.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-234">Type a valid user name and password.</span></span> <span data-ttu-id="b9ca0-235">Vous utiliserez ce compte pour vous connecter à la machine virtuelle une fois qu’elle aura été créée.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-235">You’ll use this account to log in to the VM after it has been created.</span></span>
6. <span data-ttu-id="b9ca0-236">Remplissez les champs **Abonnement**, **Groupe de ressources** et **Emplacement**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-236">Provide a **Subscription**, **Resource Group**, and **Location** and then click **OK**.</span></span>
7. <span data-ttu-id="b9ca0-237">Dans la section **Taille**, cliquez sur une taille de machine virtuelle pour cette instance, puis sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-237">On the **Size** section, click a virtual machine size for this instance and then click **Select**.</span></span>
8. <span data-ttu-id="b9ca0-238">Dans la section **Paramètres**, acceptez les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-238">On the **Settings** section, you can accept the defaults.</span></span> <span data-ttu-id="b9ca0-239">Toutefois, vérifiez bien que le réseau virtuel sélectionné est **Tenant1VNet1** et que le sous-réseau est défini sur **10.1.1.0/24**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-239">But ensure the virtual network selected is **Tenant1VNet1** and the subnet is set to **10.1.1.0/24**.</span></span> <span data-ttu-id="b9ca0-240">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-240">Click **OK**.</span></span>
9. <span data-ttu-id="b9ca0-241">Vérifiez les paramètres dans la section **Résumé**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-241">Review the settings on the **Summary** section and click **OK**.</span></span>

<span data-ttu-id="b9ca0-242">Pour chaque réseau virtuel locataire à connecter, répétez les étapes précédentes de la section **Créer le réseau virtuel et le sous-réseau de machine virtuelle** à la section **Créer une machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-242">For each tenant VNet you want to connect, repeat the previous steps from **Create the virtual network and VM subnet** through **Create a virtual machine** sections.</span></span>

### <a name="configure-the-nat-virtual-machine-for-gateway-traversal"></a><span data-ttu-id="b9ca0-243">Configurer la machine virtuelle NAT pour la traversée de passerelle</span><span class="sxs-lookup"><span data-stu-id="b9ca0-243">Configure the NAT virtual machine for gateway traversal</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b9ca0-244">Cette section concerne uniquement les déploiements du Kit de développement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-244">This section is for Azure Stack Development Kit deployments only.</span></span> <span data-ttu-id="b9ca0-245">La traduction d’adresses réseau (NAT) n’est pas nécessaire pour les déploiements à plusieurs nœuds.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-245">The NAT is not needed for multi-node deployments.</span></span>

<span data-ttu-id="b9ca0-246">Le Kit de développement Azure Stack est autonome et isolé du réseau sur lequel est déployé l’hôte physique.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-246">The Azure Stack Development Kit is self-contained and isolated from the network on which the physical host is deployed.</span></span> <span data-ttu-id="b9ca0-247">Par conséquent, le réseau VIP « Externe » auquel les passerelles sont connectées n’est pas externe. Il est masqué derrière un routeur qui procède à la traduction d’adresses réseau (NAT).</span><span class="sxs-lookup"><span data-stu-id="b9ca0-247">So, the “External” VIP network that the gateways are connected to is not external, but instead is hidden behind a router doing Network Address Translation (NAT).</span></span>
 
<span data-ttu-id="b9ca0-248">Le routeur est une machine virtuelle Windows Server (**AzS-BGPNAT01**) qui exécute le rôle RRAS (Routing and Remote Access Services) dans l’infrastructure du Kit de développement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-248">The router is a Windows Server virtual machine (**AzS-BGPNAT01**) running the Routing and Remote Access Services (RRAS) role in the Azure Stack Development Kit infrastructure.</span></span> <span data-ttu-id="b9ca0-249">Vous devez configurer la traduction d’adresses réseau sur la machine virtuelle AzS-BGPNAT01 pour permettre à la connexion VPN de site à site de se connecter aux deux extrémités.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-249">You must configure NAT on the AzS-BGPNAT01 virtual machine to allow the Site-to-Site VPN Connection to connect on both ends.</span></span>

#### <a name="configure-the-nat"></a><span data-ttu-id="b9ca0-250">Configurer NAT</span><span class="sxs-lookup"><span data-stu-id="b9ca0-250">Configure the NAT</span></span>

1. <span data-ttu-id="b9ca0-251">Connectez-vous à l’ordinateur physique Azure Stack avec votre compte Administrateur.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-251">Log in to the Azure Stack physical machine with your administrator account.</span></span>
2. <span data-ttu-id="b9ca0-252">Copiez et modifiez le script PowerShell suivant et exécutez-le dans une fenêtre Windows PowerShell ISE avec des privilèges élevés.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-252">Copy and edit the following PowerShell script and run in an elevated Windows PowerShell ISE.</span></span> <span data-ttu-id="b9ca0-253">Remplacez votre mot de passe administrateur.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-253">Replace your administrator password.</span></span> <span data-ttu-id="b9ca0-254">L’adresse renvoyée est votre *adresse BGPNAT externe*.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-254">The address returned is your *External BGPNAT address*.</span></span>

   ```
   cd \AzureStack-Tools-master\connect
   Import-Module .\AzureStack.Connect.psm1
   $Password = ConvertTo-SecureString "<your administrator password>" `
    -AsPlainText `
    -Force
   Get-AzureStackNatServerAddress `
    -HostComputer "azs-bgpnat01" `
    -Password $Password
   ```
4. <span data-ttu-id="b9ca0-255">Pour configurer NAT, copiez et modifiez le script PowerShell suivant et exécutez-le dans une fenêtre Windows PowerShell ISE avec des privilèges élevés.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-255">To configure the NAT, copy and edit the following PowerShell script and run in an elevated Windows PowerShell ISE.</span></span> <span data-ttu-id="b9ca0-256">Modifiez le script pour remplacer l’*adresse BGPNAT externe* et l’*adresse IP interne* (que vous avez notée dans la section **Créer la connexion**).</span><span class="sxs-lookup"><span data-stu-id="b9ca0-256">Edit the script to replace the *External BGPNAT address* and *Internal IP address* (which you noted previously in the **Create the Connection** section).</span></span>

   <span data-ttu-id="b9ca0-257">Dans les schémas, l’*adresse BGPNAT externe* est 10.10.0.62 et l’*adresse IP interne* est 192.168.102.1.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-257">In the example diagrams, the *External BGPNAT address* is 10.10.0.62 and the *Internal IP address* is 192.168.102.1.</span></span>

   ```
   # Designate the external NAT address for the ports that use the IKE authentication.
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 499 `
      -PortEnd 501}
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 4499 `
      -PortEnd 4501}
   # create a static NAT mapping to map the external address to the Gateway
   # Public IP Address to map the ISAKMP port 500 for PHASE 1 of the IPSEC tunnel
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 500 `
      -InternalPort 500}
   # Finally, configure NAT traversal which uses port 4500 to
   # successfully establish the complete IPSEC tunnel over NAT devices
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 4500 `
      -InternalPort 4500}
   ```

## <a name="configure-azure"></a><span data-ttu-id="b9ca0-258">Configuration d’Azure</span><span class="sxs-lookup"><span data-stu-id="b9ca0-258">Configure Azure</span></span>
<span data-ttu-id="b9ca0-259">Une fois Azure Stack configuré, vous pouvez déployer certaines ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-259">Now that you have completed the Azure Stack configuration, you can deploy some Azure resources.</span></span> <span data-ttu-id="b9ca0-260">Le schéma suivant représente un réseau virtuel locataire dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-260">The following diagram shows a sample tenant virtual network in Azure.</span></span> <span data-ttu-id="b9ca0-261">Vous pouvez utiliser n’importe quel nom et schéma d’adressage pour désigner votre réseau virtuel dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-261">You can use any name and addressing scheme for your VNet in Azure.</span></span> <span data-ttu-id="b9ca0-262">Toutefois, la plage d’adresses des réseaux virtuels dans Azure et Azure Stack doit être unique et ne doit pas se chevaucher.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-262">However, the address range of the VNets in Azure and Azure Stack must be unique and not overlap.</span></span>

![Réseaux virtuels Azure](media/azure-stack-connect-expressroute/AzureArchitecture.png)

<span data-ttu-id="b9ca0-264">**Schéma 3**</span><span class="sxs-lookup"><span data-stu-id="b9ca0-264">**Diagram 3**</span></span>

<span data-ttu-id="b9ca0-265">Les ressources que vous déployez dans Azure sont semblables aux ressources déployées dans Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-265">The resources you deploy in Azure are similar to the resources you deployed in Azure Stack.</span></span> <span data-ttu-id="b9ca0-266">Dans les deux environnements, vous déployez :</span><span class="sxs-lookup"><span data-stu-id="b9ca0-266">Similarly, you deploy:</span></span>
* <span data-ttu-id="b9ca0-267">Des réseaux virtuels et des sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="b9ca0-267">Virtual networks and subnets</span></span>
* <span data-ttu-id="b9ca0-268">Un sous-réseau de passerelle</span><span class="sxs-lookup"><span data-stu-id="b9ca0-268">A gateway subnet</span></span>
* <span data-ttu-id="b9ca0-269">Une passerelle de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="b9ca0-269">A virtual network gateway</span></span>
* <span data-ttu-id="b9ca0-270">Une connexion</span><span class="sxs-lookup"><span data-stu-id="b9ca0-270">A connection</span></span>
* <span data-ttu-id="b9ca0-271">Un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="b9ca0-271">An ExpressRoute circuit</span></span>

<span data-ttu-id="b9ca0-272">L’infrastructure réseau Azure donnée en exemple est configurée de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="b9ca0-272">The example Azure network infrastructure is configured in the following way:</span></span>
* <span data-ttu-id="b9ca0-273">Un modèle de réseau virtuel Hub (192.168.2.0/24) et Spoke (10.100.0.0./16) standard est utilisé.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-273">A standard hub (192.168.2.0/24) and spoke (10.100.0.0./16) VNet model is used.</span></span>
* <span data-ttu-id="b9ca0-274">Les charges de travail sont déployées dans le réseau virtuel Spoke et le circuit ExpressRoute est connecté au réseau virtuel Hub.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-274">The workloads are deployed in the spoke Vnet and the ExpressRoute circuit is connected to the hub VNet.</span></span>
* <span data-ttu-id="b9ca0-275">Ces deux réseaux virtuels sont connectés à l’aide de la fonctionnalité VNet Peering.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-275">The two VNets are linked using the VNet peering feature.</span></span>

### <a name="configure-vnets"></a><span data-ttu-id="b9ca0-276">Configurer les réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="b9ca0-276">Configure Vnets</span></span>
1. <span data-ttu-id="b9ca0-277">Connectez-vous au portail Azure avec vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-277">Sign in to the Azure portal with your Azure credentials.</span></span>
2. <span data-ttu-id="b9ca0-278">Créez le réseau virtuel Hub en utilisant l’espace d’adressage 192.168.2.0/24.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-278">Create the hub VNet using the 192.168.2.0/24 address space.</span></span> <span data-ttu-id="b9ca0-279">Créez un sous-réseau à l’aide de la plage d’adresses 192.168.2.0/25 et ajoutez un sous-réseau de passerelle à l’aide de la plage d’adresses 192.168.2.128/27.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-279">Create a subnet using the 192.168.2.0/25 address range, and add a gateway subnet using the 192.168.2.128/27 address range.</span></span>
3. <span data-ttu-id="b9ca0-280">Créez le réseau virtuel Spoke et le sous-réseau en utilisant la plage d’adresses 10.100.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-280">Create the spoke VNet and subnet using the 10.100.0.0/16 address range.</span></span>


<span data-ttu-id="b9ca0-281">Pour en savoir plus sur la création de réseaux virtuels dans Azure, consultez la rubrique [Créer un réseau virtuel comprenant plusieurs sous-réseaux](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="b9ca0-281">For more information about creating virtual networks in Azure, see [Create a virtual network with multiple subnets](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

### <a name="configure-an-expressroute-circuit"></a><span data-ttu-id="b9ca0-282">Configurer un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="b9ca0-282">Configure an ExpressRoute circuit</span></span>

1. <span data-ttu-id="b9ca0-283">Passez en revue la configuration requise d’ExpressRoute dans [Configuration requise pour ExpressRoute et liste de contrôle](../expressroute/expressroute-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="b9ca0-283">Review the ExpressRoute prerequisites in [ExpressRoute prerequisites & checklist](../expressroute/expressroute-prerequisites.md).</span></span>
2. <span data-ttu-id="b9ca0-284">Suivez les étapes décrites dans la rubrique [Création et modification d’un circuit ExpressRoute](../expressroute/expressroute-howto-circuit-portal-resource-manager.md) pour créer un circuit ExpressRoute via votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-284">Follow the steps in [Create and modify an ExpressRoute circuit](../expressroute/expressroute-howto-circuit-portal-resource-manager.md) to create an ExpressRoute circuit using your Azure subscription.</span></span>
3. <span data-ttu-id="b9ca0-285">Partagez la clé de service obtenue à l’étape précédente via votre fournisseur/hébergeur pour approvisionner l’extrémité de votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-285">Share the service key from the previous step with your hoster/provider to provision your ExpressRoute circuit at their end.</span></span>
4. <span data-ttu-id="b9ca0-286">Suivez les étapes décrites dans la rubrique [Créer et modifier l’homologation pour un circuit ExpressRoute](../expressroute/expressroute-howto-routing-portal-resource-manager.md) pour configurer l’homologation privée sur le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-286">Follow the steps in [Create and modify peering for an ExpressRoute circuit](../expressroute/expressroute-howto-routing-portal-resource-manager.md) to configure private peering on the ExpressRoute circuit.</span></span>

### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="b9ca0-287">Créer la passerelle de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="b9ca0-287">Create the virtual network gateway</span></span>

* <span data-ttu-id="b9ca0-288">Suivez les étapes décrites dans la rubrique [Configurer une passerelle de réseau virtuel pour ExpressRoute à l’aide de PowerShell](../expressroute/expressroute-howto-add-gateway-resource-manager.md) pour créer une passerelle de réseau virtuel pour ExpressRoute dans le réseau virtuel Hub.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-288">Follow the steps in [Configure a virtual network gateway for ExpressRoute using PowerShell](../expressroute/expressroute-howto-add-gateway-resource-manager.md) to create a virtual network gateway for ExpressRoute in the hub VNet.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="b9ca0-289">Créer la connexion</span><span class="sxs-lookup"><span data-stu-id="b9ca0-289">Create the connection</span></span>

* <span data-ttu-id="b9ca0-290">Pour connecter le circuit ExpressRoute au réseau virtuel Hub, suivez les étapes décrites dans [Connecter un réseau virtuel à un circuit ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b9ca0-290">To link the ExpressRoute circuit to the hub VNet, follow the steps in [Connect a virtual network to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>

### <a name="peer-the-vnets"></a><span data-ttu-id="b9ca0-291">Homologuer les réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="b9ca0-291">Peer the Vnets</span></span>

* <span data-ttu-id="b9ca0-292">Homologuez les réseaux virtuels Hub et Spoke en suivant les étapes décrites dans la rubrique [Créer une homologation de réseaux virtuels - Resource Manager - Même abonnement](../virtual-network/virtual-networks-create-vnetpeering-arm-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b9ca0-292">Peer the Hub and Spoke VNets using the steps in [Create a virtual network peering using the Azure portal](../virtual-network/virtual-networks-create-vnetpeering-arm-portal.md).</span></span> <span data-ttu-id="b9ca0-293">Lors de la configuration de VNet Peering, sélectionnez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="b9ca0-293">When configuring VNet peering, ensure you select the following options:</span></span>
   * <span data-ttu-id="b9ca0-294">De Hub à Spoke : **Autoriser le transit par passerelle**</span><span class="sxs-lookup"><span data-stu-id="b9ca0-294">From hub to spoke: **Allow gateway transit**</span></span>
   * <span data-ttu-id="b9ca0-295">De Spoke à Hub : **Utiliser la passerelle distante par défaut**</span><span class="sxs-lookup"><span data-stu-id="b9ca0-295">From spoke to hub: **Use remote gateway**</span></span>

### <a name="create-a-virtual-machine"></a><span data-ttu-id="b9ca0-296">Création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b9ca0-296">Create a virtual machine</span></span>

* <span data-ttu-id="b9ca0-297">Déployez les machines virtuelles de votre charge de travail dans le réseau virtuel Spoke.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-297">Deploy your workload virtual machines into the spoke VNet.</span></span>

<span data-ttu-id="b9ca0-298">Répétez ces étapes pour connecter d’autres réseaux virtuels locataires dans Azure via leurs circuits ExpressRoute respectifs.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-298">Repeat these steps for any additional tenant VNets you want to connect in Azure through their respective ExpressRoute circuits.</span></span>

## <a name="configure-the-router"></a><span data-ttu-id="b9ca0-299">Configuration du routeur</span><span class="sxs-lookup"><span data-stu-id="b9ca0-299">Configure the router</span></span>

<span data-ttu-id="b9ca0-300">Vous pouvez vous référer au schéma suivant pour configurer votre routeur ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-300">You can use the following end-to-end infrastructure diagram to guide the configuration of your ExpressRoute Router.</span></span> <span data-ttu-id="b9ca0-301">Ce schéma représente deux locataires (Tenant 1 et Tenant 2) avec leurs circuits ExpressRoute respectifs.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-301">This diagram shows two tenants (Tenant 1 and Tenant 2) with their respective Express Route circuits.</span></span> <span data-ttu-id="b9ca0-302">Chaque locataire est connecté à son propre VRF (Virtual Routing and Forwarding) du côté LAN et WAN du routeur ExpressRoute pour garantir une isolation de bout en bout entre les deux locataires.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-302">Each is linked to their own VRF (Virtual Routing and Forwarding) in the LAN and WAN side of the ExpressRoute router to ensure end-to-end isolation between the two tenants.</span></span> <span data-ttu-id="b9ca0-303">Notez les adresses IP utilisées dans les interfaces du routeur au fur et à mesure de la configuration.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-303">Note the IP addresses used in the router interfaces as you follow the sample configuration.</span></span>

![Schéma de bout en bout](media/azure-stack-connect-expressroute/EndToEnd.png)

<span data-ttu-id="b9ca0-305">**Schéma 4**</span><span class="sxs-lookup"><span data-stu-id="b9ca0-305">**Diagram 4**</span></span>

<span data-ttu-id="b9ca0-306">Vous pouvez utiliser n’importe quel routeur qui prend en charge le VPN IKEv2 et BGP pour mettre fin à la connexion VPN de site à site établie depuis Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-306">You can use any router that supports IKEv2 VPN and BGP to terminate the Site-to-Site VPN connection from Azure Stack.</span></span> <span data-ttu-id="b9ca0-307">Le même routeur est utilisé pour se connecter à Azure via un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-307">The same router is used to connect to Azure using an ExpressRoute circuit.</span></span> 

<span data-ttu-id="b9ca0-308">Voici un exemple de configuration d’un routeur Cisco ASR 1000 qui prend en charge l’infrastructure réseau représentée dans le schéma 4 :</span><span class="sxs-lookup"><span data-stu-id="b9ca0-308">Here is a sample configuration from a Cisco ASR 1000 that supports the network infrastructure shown in Diagram 4:</span></span>

```
ip vrf Tenant 1
 description Routing Domain for PRIVATE peering to Azure for Tenant 1
 rd 1:1
!
ip vrf Tenant 2
 description Routing Domain for PRIVATE peering to Azure for Tenant 2
 rd 1:5
!
crypto ikev2 proposal V2-PROPOSAL2 
description IKEv2 proposal for Tenant 1 
encryption aes-cbc-256
 integrity sha256
 group 2
crypto ikev2 proposal V4-PROPOSAL2 
description IKEv2 proposal for Tenant 2 
encryption aes-cbc-256
 integrity sha256
 group 2
!
crypto ikev2 policy V2-POLICY2 
description IKEv2 Policy for Tenant 1 
match fvrf Tenant 1
 match address local 10.60.3.255
 proposal V2-PROPOSAL2
description IKEv2 Policy for Tenant 2
crypto ikev2 policy V4-POLICY2 
 match fvrf Tenant 2
 match address local 10.60.3.251
 proposal V4-PROPOSAL2
!
crypto ikev2 profile V2-PROFILE
description IKEv2 profile for Tenant 1 
match fvrf Tenant 1
 match address local 10.60.3.255
 match identity remote any
 authentication remote pre-share key abc123
 authentication local pre-share key abc123
 ivrf Tenant 1
!
crypto ikev2 profile V4-PROFILE
description IKEv2 profile for Tenant 2
 match fvrf Tenant 2
 match address local 10.60.3.251
 match identity remote any
 authentication remote pre-share key abc123
 authentication local pre-share key abc123
 ivrf Tenant 2
!
crypto ipsec transform-set V2-TRANSFORM2 esp-gcm 256 
 mode tunnel
crypto ipsec transform-set V4-TRANSFORM2 esp-gcm 256 
 mode tunnel
!
crypto ipsec profile V2-PROFILE
 set transform-set V2-TRANSFORM2 
 set ikev2-profile V2-PROFILE
!
crypto ipsec profile V4-PROFILE
 set transform-set V4-TRANSFORM2 
 set ikev2-profile V4-PROFILE
!
interface Tunnel10
description S2S VPN Tunnel for Tenant 1
 ip vrf forwarding Tenant 1
 ip address 11.0.0.2 255.255.255.252
 ip tcp adjust-mss 1350
 tunnel source TenGigabitEthernet0/1/0.211
 tunnel mode ipsec ipv4
 tunnel destination 10.10.0.62
 tunnel vrf Tenant 1
 tunnel protection ipsec profile V2-PROFILE
!
interface Tunnel20
description S2S VPN Tunnel for Tenant 2
 ip vrf forwarding Tenant 2
 ip address 11.0.0.2 255.255.255.252
 ip tcp adjust-mss 1350
 tunnel source TenGigabitEthernet0/1/0.213
 tunnel mode ipsec ipv4
 tunnel destination 10.10.0.62
 tunnel vrf VNET3
 tunnel protection ipsec profile V4-PROFILE
!
interface GigabitEthernet0/0/1
 description PRIMARY Express Route Link to AZURE over Equinix
 no ip address
 negotiation auto
!
interface GigabitEthernet0/0/1.100
description Primary WAN interface of Tenant 1
 description PRIMARY ER link supporting Tenant 1 to Azure
 encapsulation dot1Q 101
 ip vrf forwarding Tenant 1
 ip address 192.168.1.1 255.255.255.252
!
interface GigabitEthernet0/0/1.102
description Primary WAN interface of Tenant 2
 description PRIMARY ER link supporting Tenant 2 to Azure
 encapsulation dot1Q 102
 ip vrf forwarding Tenant 2
 ip address 192.168.1.17 255.255.255.252
!
interface GigabitEthernet0/0/2
 description BACKUP Express Route Link to AZURE over Equinix
 no ip address
 negotiation auto
!
interface GigabitEthernet0/0/2.100
description Secondary WAN interface of Tenant 1
 description BACKUP ER link supporting Tenant 1 to Azure
 encapsulation dot1Q 101
 ip vrf forwarding Tenant 1
 ip address 192.168.1.5 255.255.255.252
!
interface GigabitEthernet0/0/2.102
description Secondary WAN interface of Tenant 2 
description BACKUP ER link supporting Tenant 2 to Azure
 encapsulation dot1Q 102
 ip vrf forwarding Tenant 2
 ip address 192.168.1.21 255.255.255.252
!
interface TenGigabitEthernet0/1/0
 description Downlink to ---Port 1/47
 no ip address
!
interface TenGigabitEthernet0/1/0.211
 description LAN interface of Tenant 1
description Downlink to --- Port 1/47.211
 encapsulation dot1Q 211
 ip vrf forwarding Tenant 1
 ip address 10.60.3.255 255.255.255.254
!
interface TenGigabitEthernet0/1/0.213
description LAN interface of Tenant 2
 description Downlink to --- Port 1/47.213
 encapsulation dot1Q 213
 ip vrf forwarding Tenant 2
 ip address 10.60.3.251 255.255.255.254
!
router bgp 65530
 bgp router-id <removed>
 bgp log-neighbor-changes
 description BGP neighbor config and route advertisement for Tenant 1 VRF 
 address-family ipv4 vrf Tenant 1
  network 10.1.0.0 mask 255.255.0.0
  network 10.60.3.254 mask 255.255.255.254
  network 192.168.1.0 mask 255.255.255.252
  network 192.168.1.4 mask 255.255.255.252
  neighbor 10.10.0.62 remote-as 65100
  neighbor 10.10.0.62 description VPN-BGP-PEER-for-Tenant 1
  neighbor 10.10.0.62 ebgp-multihop 5
  neighbor 10.10.0.62 activate
  neighbor 10.60.3.254 remote-as 4232570301
  neighbor 10.60.3.254 description LAN peer for CPEC:INET:2112 VRF
  neighbor 10.60.3.254 activate
  neighbor 10.60.3.254 route-map BLOCK-ALL out
  neighbor 192.168.1.2 remote-as 12076
  neighbor 192.168.1.2 description PRIMARY ER peer for Tenant 1 to Azure
  neighbor 192.168.1.2 ebgp-multihop 5
  neighbor 192.168.1.2 activate
  neighbor 192.168.1.2 soft-reconfiguration inbound
  neighbor 192.168.1.2 route-map Tenant 1-ONLY out
  neighbor 192.168.1.6 remote-as 12076
  neighbor 192.168.1.6 description BACKUP ER peer for Tenant 1 to Azure
  neighbor 192.168.1.6 ebgp-multihop 5
  neighbor 192.168.1.6 activate
  neighbor 192.168.1.6 soft-reconfiguration inbound
  neighbor 192.168.1.6 route-map Tenant 1-ONLY out
  maximum-paths 8
 exit-address-family
 !
description BGP neighbor config and route advertisement for Tenant 2 VRF 
address-family ipv4 vrf Tenant 2
  network 10.1.0.0 mask 255.255.0.0
  network 10.60.3.250 mask 255.255.255.254
  network 192.168.1.16 mask 255.255.255.252
  network 192.168.1.20 mask 255.255.255.252
  neighbor 10.10.0.62 remote-as 65300
  neighbor 10.10.0.62 description VPN-BGP-PEER-for-Tenant 2
  neighbor 10.10.0.62 ebgp-multihop 5
  neighbor 10.10.0.62 activate
  neighbor 10.60.3.250 remote-as 4232570301
  neighbor 10.60.3.250 description LAN peer for CPEC:INET:2112 VRF
  neighbor 10.60.3.250 activate
  neighbor 10.60.3.250 route-map BLOCK-ALL out
  neighbor 192.168.1.18 remote-as 12076
  neighbor 192.168.1.18 description PRIMARY ER peer for Tenant 2 to Azure
  neighbor 192.168.1.18 ebgp-multihop 5
  neighbor 192.168.1.18 activate
  neighbor 192.168.1.18 soft-reconfiguration inbound
  neighbor 192.168.1.18 route-map VNET-ONLY out
  neighbor 192.168.1.22 remote-as 12076
  neighbor 192.168.1.22 description BACKUP ER peer for Tenant 2 to Azure
  neighbor 192.168.1.22 ebgp-multihop 5
  neighbor 192.168.1.22 activate
  neighbor 192.168.1.22 soft-reconfiguration inbound
  neighbor 192.168.1.22 route-map VNET-ONLY out
  maximum-paths 8
 exit-address-family
!
ip forward-protocol nd
!
ip as-path access-list 1 permit ^$
ip route vrf Tenant 1 10.1.0.0 255.255.0.0 Tunnel10
ip route vrf Tenant 2 10.1.0.0 255.255.0.0 Tunnel20
!
ip prefix-list BLOCK-ALL seq 5 deny 0.0.0.0/0 le 32
!
route-map BLOCK-ALL permit 10
 match ip address prefix-list BLOCK-ALL
!
route-map VNET-ONLY permit 10
 match as-path 1
!
```

## <a name="test-the-connection"></a><span data-ttu-id="b9ca0-309">Tester la connexion</span><span class="sxs-lookup"><span data-stu-id="b9ca0-309">Test the connection</span></span>

<span data-ttu-id="b9ca0-310">Lorsque la connexion de site à site et le circuit ExpressRoute sont établis, testez votre connexion.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-310">Test your connection after establishing the Site-to-Site connection and the ExpressRoute circuit.</span></span> <span data-ttu-id="b9ca0-311">Pour cela, rien de plus simple.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-311">This task is simple.</span></span>  <span data-ttu-id="b9ca0-312">Connectez-vous à l’une des machines virtuelles créées dans votre réseau virtuel Azure et effectuez un test ping sur la machine virtuelle créée dans l’environnement Azure Stack, ou vice versa.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-312">Log on to one of the virtual machines you created in your Azure VNet and ping the virtual machine you created in the Azure Stack environment, or vice versa.</span></span> 

<span data-ttu-id="b9ca0-313">Pour vérifier que vous envoyez bien le trafic via les connexions site à site et ExpressRoute, vous devez effectuer un test ping aux deux extrémités avec l’adresse IP dédiée de la machine virtuelle, et non avec son adresse IP virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-313">To ensure you are sending the traffic through the Site-to-Site and ExpressRoute connections, you must ping the dedicated IP (DIP) address of the virtual machine at both ends and not the VIP address of the virtual machine.</span></span> <span data-ttu-id="b9ca0-314">Pour cela, vous devez rechercher et noter l’adresse à l’autre extrémité de la connexion.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-314">So, you must find and note the address on the other end of the connection.</span></span>

### <a name="allow-icmp-in-through-the-firewall"></a><span data-ttu-id="b9ca0-315">Autoriser la transmission du protocole ICMP via le pare-feu</span><span class="sxs-lookup"><span data-stu-id="b9ca0-315">Allow ICMP in through the firewall</span></span>
<span data-ttu-id="b9ca0-316">Par défaut, Windows Server 2016 n’autorise pas la transmission des paquets ICMP via le pare-feu.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-316">By default, Windows Server 2016 does not allow ICMP packets in through the firewall.</span></span> <span data-ttu-id="b9ca0-317">Par conséquent, pour chaque machine virtuelle utilisée dans le test, exécutez la cmdlet suivante dans une fenêtre PowerShell avec des privilèges élevés :</span><span class="sxs-lookup"><span data-stu-id="b9ca0-317">So, for every virtual machine you use in the test, run the following cmdlet in an elevated PowerShell window:</span></span>


   ```
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

### <a name="ping-the-azure-stack-virtual-machine"></a><span data-ttu-id="b9ca0-318">Effectuer un test ping sur la machine virtuelle Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b9ca0-318">Ping the Azure Stack virtual machine</span></span>

1. <span data-ttu-id="b9ca0-319">Connectez-vous au portail utilisateur Azure Stack avec un compte locataire.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-319">Sign in to the Azure Stack user portal using a tenant account.</span></span>
2. <span data-ttu-id="b9ca0-320">Cliquez sur **Machines virtuelles** dans la barre de navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-320">Click **Virtual Machines** in the left navigation bar.</span></span>
3. <span data-ttu-id="b9ca0-321">Recherchez la machine virtuelle créée précédemment et cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-321">Find the virtual machine that you previously created and click it.</span></span>
4. <span data-ttu-id="b9ca0-322">Dans la section de la machine virtuelle, cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-322">On the section for the virtual machine, click **Connect**.</span></span>
5. <span data-ttu-id="b9ca0-323">Ouvrez une fenêtre PowerShell avec des privilèges élevés et tapez **ipconfig /all**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-323">Open an elevated PowerShell window, and type **ipconfig /all**.</span></span>
6. <span data-ttu-id="b9ca0-324">Recherchez l’adresse IPv4 dans la sortie et notez-la.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-324">Find the IPv4 Address in the output and note it.</span></span> <span data-ttu-id="b9ca0-325">Effectuez un test ping à partir de la machine virtuelle dans le réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-325">Ping this address from the virtual machine in the Azure VNet.</span></span> <span data-ttu-id="b9ca0-326">Dans l’environnement représenté en exemple, l’adresse provient du sous-réseau 10.1.1.x/24.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-326">In the example environment, the address is from the 10.1.1.x/24 subnet.</span></span> <span data-ttu-id="b9ca0-327">Dans votre environnement, l’adresse peut être différente.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-327">In your environment, the address might be different.</span></span> <span data-ttu-id="b9ca0-328">Toutefois, elle doit figurer dans le sous-réseau que vous avez créé pour le sous-réseau du réseau virtuel locataire.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-328">However, it should be within the subnet you created for the Tenant VNet subnet.</span></span>


### <a name="view-data-transfer-statistics"></a><span data-ttu-id="b9ca0-329">Afficher les statistiques de transfert de données</span><span class="sxs-lookup"><span data-stu-id="b9ca0-329">View data transfer statistics</span></span>

<span data-ttu-id="b9ca0-330">Si vous souhaitez connaître le volume de trafic qui transite via votre connexion, accédez à la section Connexion du portail utilisateur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-330">If you want to know how much traffic is passing through your connection, you can find this information on the Connection section in the Azure Stack user portal.</span></span> <span data-ttu-id="b9ca0-331">Ainsi, vous pourrez également vérifier que le test ping que vous venez d’effectuer est passé par les connexions VPN et ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-331">This information is also another good way to verify that the ping you just sent actually went through the VPN and ExpressRoute connections.</span></span>

1. <span data-ttu-id="b9ca0-332">Connectez-vous au portail utilisateur Microsoft Azure Stack avec votre compte locataire.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-332">Sign in to the Microsoft Azure Stack user portal using your tenant account.</span></span>
2. <span data-ttu-id="b9ca0-333">Accédez au groupe de ressources dans lequel votre passerelle VPN a été créée et sélectionnez le type d’objet **Connexions**.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-333">Navigate to the resource group where your VPN Gateway was created and select the **Connections** object type.</span></span>
3. <span data-ttu-id="b9ca0-334">Cliquez sur la connexion **ConnectToAzure** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-334">Click the **ConnectToAzure** connection in the list.</span></span>
4. <span data-ttu-id="b9ca0-335">Dans la section **Connexion**, vous pouvez visualiser les statistiques de **données entrantes** et de **données sortantes**. Vous devriez voir des valeurs non nulles.</span><span class="sxs-lookup"><span data-stu-id="b9ca0-335">On the **Connection** section, you can see statistics for **Data in** and **Data out**. You should see some non-zero values there.</span></span>

   ![Données entrantes et sortantes](media/azure-stack-connect-expressroute/DataInDataOut.png)

## <a name="next-steps"></a><span data-ttu-id="b9ca0-337">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b9ca0-337">Next steps</span></span>
[<span data-ttu-id="b9ca0-338">Déployer des applications sur Azure et Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b9ca0-338">Deploy apps to Azure and Azure Stack</span></span>](azure-stack-solution-pipeline.md)