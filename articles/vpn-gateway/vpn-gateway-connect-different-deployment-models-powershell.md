---
title: "Connecter des réseaux virtuels classiques tooAzure Gestionnaire de ressources VNets : PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate une connexion VPN entre classique des réseaux virtuels et VNets Gestionnaire de ressources à l’aide de la passerelle VPN et PowerShell"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a><span data-ttu-id="dda14-103">Connecter des réseaux virtuels utilisant des modèles de déploiement différents à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="dda14-103">Connect virtual networks from different deployment models using PowerShell</span></span>



<span data-ttu-id="dda14-104">Cet article vous explique comment tooconnect classique des réseaux virtuels tooResource Manager VNets tooallow hello ressources situées dans toocommunicate de modèles de déploiement distinct hello entre eux.</span><span class="sxs-lookup"><span data-stu-id="dda14-104">This article shows you how tooconnect classic VNets tooResource Manager VNets tooallow hello resources located in hello separate deployment models toocommunicate with each other.</span></span> <span data-ttu-id="dda14-105">étapes de Hello dans cet article utilisent PowerShell, mais vous pouvez également créer cette configuration à l’aide de hello portail Azure en sélectionnant l’article de hello dans cette liste.</span><span class="sxs-lookup"><span data-stu-id="dda14-105">hello steps in this article use PowerShell, but you can also create this configuration using hello Azure portal by selecting hello article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dda14-106">Portail</span><span class="sxs-lookup"><span data-stu-id="dda14-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="dda14-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dda14-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="dda14-108">La connexion d’un tooa de réseau virtuel classique Gestionnaire de ressources du VNet est tooconnecting comme emplacement d’un site réseau virtuel tooan local.</span><span class="sxs-lookup"><span data-stu-id="dda14-108">Connecting a classic VNet tooa Resource Manager VNet is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="dda14-109">Les deux types de connectivité utilisent un tooprovide de passerelle VPN un tunnel sécurisé utilisant IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="dda14-109">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="dda14-110">Vous pouvez créer une connexion entre des réseaux virtuels situés dans des abonnements différents et des régions différentes.</span><span class="sxs-lookup"><span data-stu-id="dda14-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="dda14-111">Vous pouvez également connecter des réseaux virtuels qui ont déjà des connexions tooon des réseaux locaux, tant que passerelle hello qui ils ont été configurés avec est dynamique ou basée sur un itinéraire.</span><span class="sxs-lookup"><span data-stu-id="dda14-111">You can also connect VNets that already have connections tooon-premises networks, as long as hello gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="dda14-112">Pour plus d’informations sur les connexions de réseau virtuel à réseau virtuel, consultez hello [FAQ sur le réseau à](#faq) à fin hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="dda14-112">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span> 

<span data-ttu-id="dda14-113">Si vos réseaux virtuels sont Bonjour même région, vous souhaiterez peut-être tooinstead connectent à l’aide de l’homologation de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="dda14-113">If your VNets are in hello same region, you may want tooinstead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="dda14-114">L’homologation de réseaux virtuels (ou VNet Peering) n’utilise pas de passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="dda14-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="dda14-115">Pour plus d’informations, consultez l’article [Homologation de réseaux virtuels](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dda14-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

## <a name="before-beginning"></a><span data-ttu-id="dda14-116">Avant tout chose</span><span class="sxs-lookup"><span data-stu-id="dda14-116">Before beginning</span></span>

<span data-ttu-id="dda14-117">Bonjour étapes suivantes vous guident tooconfigure nécessaires de paramètres hello une passerelle dynamique ou basée sur un itinéraire pour chaque réseau virtuel et créer une connexion VPN entre les passerelles hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-117">hello following steps walk you through hello settings necessary tooconfigure a dynamic or route-based gateway for each VNet and create a VPN connection between hello gateways.</span></span> <span data-ttu-id="dda14-118">Cette configuration ne prend pas en charge les passerelles statiques ou basées sur des stratégies.</span><span class="sxs-lookup"><span data-stu-id="dda14-118">This configuration does not support static or policy-based gateways.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="dda14-119">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="dda14-119">Prerequisites</span></span>

* <span data-ttu-id="dda14-120">Les deux réseaux virtuels ont déjà été créés.</span><span class="sxs-lookup"><span data-stu-id="dda14-120">Both VNets have already been created.</span></span>
* <span data-ttu-id="dda14-121">plages d’adresses Hello pour hello réseaux virtuels ne se chevauchent entre eux, ni ne se chevauchent avec les plages hello pour les autres connexions qui les passerelles hello peuvent être connectés à.</span><span class="sxs-lookup"><span data-stu-id="dda14-121">hello address ranges for hello VNets do not overlap with each other, or overlap with any of hello ranges for other connections that hello gateways may be connected to.</span></span>
* <span data-ttu-id="dda14-122">Vous avez installé les applets de commande PowerShell dernière hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-122">You have installed hello latest PowerShell cmdlets.</span></span> <span data-ttu-id="dda14-123">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="dda14-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span> <span data-ttu-id="dda14-124">Veillez à qu'installer hello Management Service (SM) et hello applets de commande Gestionnaire de ressources (RM).</span><span class="sxs-lookup"><span data-stu-id="dda14-124">Make sure you install both hello Service Management (SM) and hello Resource Manager (RM) cmdlets.</span></span> 

### <span data-ttu-id="dda14-125"><a name="exampleref"></a>Exemples de paramètres</span><span class="sxs-lookup"><span data-stu-id="dda14-125"><a name="exampleref"></a>Example settings</span></span>

<span data-ttu-id="dda14-126">Vous pouvez utiliser ces valeurs de toocreate un environnement de test, ou consultez toothem toobetter comprendre les exemples hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="dda14-126">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

<span data-ttu-id="dda14-127">**Paramètres de réseau virtuel classique**</span><span class="sxs-lookup"><span data-stu-id="dda14-127">**Classic VNet settings**</span></span>

<span data-ttu-id="dda14-128">Nom du réseau virtuel = ClassicVNet </span><span class="sxs-lookup"><span data-stu-id="dda14-128">VNet Name = ClassicVNet</span></span> <br>
<span data-ttu-id="dda14-129">Emplacement = Ouest des États-Unis</span><span class="sxs-lookup"><span data-stu-id="dda14-129">Location = West US</span></span> <br>
<span data-ttu-id="dda14-130">Espaces d’adressage du réseau virtuel = 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="dda14-130">Virtual Network Address Spaces = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="dda14-131">Sous-réseau-1 = 10.0.0.0/27</span><span class="sxs-lookup"><span data-stu-id="dda14-131">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="dda14-132">Sous-réseau de passerelle : 10.0.0.32/29</span><span class="sxs-lookup"><span data-stu-id="dda14-132">GatewaySubnet = 10.0.0.32/29</span></span> <br>
<span data-ttu-id="dda14-133">Nom du réseau local = RMVNetLocal</span><span class="sxs-lookup"><span data-stu-id="dda14-133">Local Network Name = RMVNetLocal</span></span> <br>
<span data-ttu-id="dda14-134">Type de passerelle = DynamicRouting</span><span class="sxs-lookup"><span data-stu-id="dda14-134">GatewayType = DynamicRouting</span></span>

<span data-ttu-id="dda14-135">**Paramètres de réseau virtuel Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="dda14-135">**Resource Manager VNet settings**</span></span>

<span data-ttu-id="dda14-136">Nom du réseau virtuel = RMVNet </span><span class="sxs-lookup"><span data-stu-id="dda14-136">VNet Name = RMVNet</span></span> <br>
<span data-ttu-id="dda14-137">Groupe de ressources = RG1</span><span class="sxs-lookup"><span data-stu-id="dda14-137">Resource Group = RG1</span></span> <br>
<span data-ttu-id="dda14-138">Espaces d’adressage IP du réseau virtuel = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="dda14-138">Virtual Network IP Address Spaces = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="dda14-139">Sous-réseau-1 = 192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="dda14-139">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="dda14-140">Sous-réseau de passerelle = 192.168.0.0/26</span><span class="sxs-lookup"><span data-stu-id="dda14-140">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="dda14-141">Emplacement = Est des États-Unis</span><span class="sxs-lookup"><span data-stu-id="dda14-141">Location = East US</span></span> <br>
<span data-ttu-id="dda14-142">Nom d’adresse IP publique de passerelle = gwpip</span><span class="sxs-lookup"><span data-stu-id="dda14-142">Gateway public IP name = gwpip</span></span> <br>
<span data-ttu-id="dda14-143">Passerelle de réseau local = ClassicVNetLocal</span><span class="sxs-lookup"><span data-stu-id="dda14-143">Local Network Gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="dda14-144">Nom de passerelle de réseau virtuel = RMGateway</span><span class="sxs-lookup"><span data-stu-id="dda14-144">Virtual Network Gateway name = RMGateway</span></span> <br>
<span data-ttu-id="dda14-145">Configuration d’adressage IP de la passerelle = gwipconfig</span><span class="sxs-lookup"><span data-stu-id="dda14-145">Gateway IP addressing configuration = gwipconfig</span></span>

## <span data-ttu-id="dda14-146"><a name="createsmgw"></a>Section 1 : configurer hello réseau virtuel classique</span><span class="sxs-lookup"><span data-stu-id="dda14-146"><a name="createsmgw"></a>Section 1 - Configure hello classic VNet</span></span>
### <a name="part-1---download-your-network-configuration-file"></a><span data-ttu-id="dda14-147">Partie 1 : Télécharger votre fichier de configuration réseau</span><span class="sxs-lookup"><span data-stu-id="dda14-147">Part 1 - Download your network configuration file</span></span>
1. <span data-ttu-id="dda14-148">Ouvrez une session dans tooyour compte Azure dans la console PowerShell hello avec des droits élevés.</span><span class="sxs-lookup"><span data-stu-id="dda14-148">Log in tooyour Azure account in hello PowerShell console with elevated rights.</span></span> <span data-ttu-id="dda14-149">Hello applet de commande suivante vous demande les informations d’identification de hello pour votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="dda14-149">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="dda14-150">Une fois connecté, il télécharge les paramètres de votre compte afin qu’ils soient disponible tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dda14-150">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span> <span data-ttu-id="dda14-151">Vous utilisez hello toocomplete d’applets de commande PowerShell de SM cette partie de la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-151">You use hello SM PowerShell cmdlets toocomplete this part of hello configuration.</span></span>

  ```powershell
  Add-AzureAccount
  ```
2. <span data-ttu-id="dda14-152">Exportez votre fichier de configuration réseau Azure en exécutant hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="dda14-152">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="dda14-153">Vous pouvez modifier l’emplacement de hello de hello tooexport tooa autre emplacement de fichier si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="dda14-153">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. <span data-ttu-id="dda14-154">Fichier .xml de hello ouverts que vous avez téléchargé tooedit il.</span><span class="sxs-lookup"><span data-stu-id="dda14-154">Open hello .xml file that you downloaded tooedit it.</span></span> <span data-ttu-id="dda14-155">Pour obtenir un exemple de fichier de configuration de réseau hello, consultez hello [schéma de Configuration réseau](https://msdn.microsoft.com/library/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="dda14-155">For an example of hello network configuration file, see hello [Network Configuration Schema](https://msdn.microsoft.com/library/jj157100.aspx).</span></span>

### <a name="part-2--verify-hello-gateway-subnet"></a><span data-ttu-id="dda14-156">Partie 2 - Vérifiez le sous-réseau de passerelle hello</span><span class="sxs-lookup"><span data-stu-id="dda14-156">Part 2 -Verify hello gateway subnet</span></span>
<span data-ttu-id="dda14-157">Bonjour **VirtualNetworkSites** élément, ajouter un tooyour de sous-réseau de passerelle réseau virtuel si aucun n’a pas encore été créé.</span><span class="sxs-lookup"><span data-stu-id="dda14-157">In hello **VirtualNetworkSites** element, add a gateway subnet tooyour VNet if one has not already been created.</span></span> <span data-ttu-id="dda14-158">Lorsque vous travaillez avec un fichier de configuration de réseau hello, sous-réseau de passerelle hello doit être nommé « GatewaySubnet » ou Azure ne peut pas reconnaître et utilisez-le comme un sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="dda14-158">When working with hello network configuration file, hello gateway subnet MUST be named "GatewaySubnet" or Azure cannot recognize and use it as a gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="dda14-159">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="dda14-159">**Example:**</span></span>

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-hello-local-network-site"></a><span data-ttu-id="dda14-160">Partie 3 - Ajouter un site de réseau local hello</span><span class="sxs-lookup"><span data-stu-id="dda14-160">Part 3 - Add hello local network site</span></span>
<span data-ttu-id="dda14-161">vous ajoutez le site réseau local Hello représente hello toowhich de réseau virtuel du Gestionnaire de ressources vous souhaitez tooconnect.</span><span class="sxs-lookup"><span data-stu-id="dda14-161">hello local network site you add represents hello RM VNet toowhich you want tooconnect.</span></span> <span data-ttu-id="dda14-162">Ajouter un **LocalNetworkSites** toohello fichier s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="dda14-162">Add a **LocalNetworkSites** element toohello file if one doesn't already exist.</span></span> <span data-ttu-id="dda14-163">À ce stade dans la configuration de hello, hello élément VPNGatewayAddress peut être une adresse IP publique valide, car nous n’avons pas encore créé la passerelle hello pour hello Gestionnaire de ressources VNet.</span><span class="sxs-lookup"><span data-stu-id="dda14-163">At this point in hello configuration, hello VPNGatewayAddress can be any valid public IP address because we haven't yet created hello gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="dda14-164">Une fois que nous créons la passerelle de hello, nous remplacez cette adresse de l’espace réservé par hello correct adresse IP publique qui a été attribué de passerelle de RM toohello.</span><span class="sxs-lookup"><span data-stu-id="dda14-164">Once we create hello gateway, we replace this placeholder IP address with hello correct public IP address that has been assigned toohello RM gateway.</span></span>

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a><span data-ttu-id="dda14-165">Partie 4 : associer hello réseau virtuel avec un site de réseau local hello</span><span class="sxs-lookup"><span data-stu-id="dda14-165">Part 4 - Associate hello VNet with hello local network site</span></span>
<span data-ttu-id="dda14-166">Dans cette section, nous spécifions le site de réseau local que vous souhaitez tooconnect hello hello virtuel à.</span><span class="sxs-lookup"><span data-stu-id="dda14-166">In this section, we specify hello local network site that you want tooconnect hello VNet to.</span></span> <span data-ttu-id="dda14-167">Dans ce cas, il est hello VNet Gestionnaire de ressources que vous avez référencé précédemment.</span><span class="sxs-lookup"><span data-stu-id="dda14-167">In this case, it is hello Resource Manager VNet that you referenced earlier.</span></span> <span data-ttu-id="dda14-168">Assurez-vous que noms de hello correspondent.</span><span class="sxs-lookup"><span data-stu-id="dda14-168">Make sure hello names match.</span></span> <span data-ttu-id="dda14-169">Cette étape ne vise pas à créer une passerelle.</span><span class="sxs-lookup"><span data-stu-id="dda14-169">This step does not create a gateway.</span></span> <span data-ttu-id="dda14-170">Il spécifie le réseau local, hello hello passerelle se connectera à.</span><span class="sxs-lookup"><span data-stu-id="dda14-170">It specifies hello local network that hello gateway will connect to.</span></span>

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a><span data-ttu-id="dda14-171">Partie 5 : enregistrer le fichier de hello et le téléchargement</span><span class="sxs-lookup"><span data-stu-id="dda14-171">Part 5 - Save hello file and upload</span></span>
<span data-ttu-id="dda14-172">Enregistrez le fichier de hello, puis l’importer tooAzure en exécutant hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="dda14-172">Save hello file, then import it tooAzure by running hello following command.</span></span> <span data-ttu-id="dda14-173">Assurez-vous que vous modifiez le chemin d’accès du fichier hello en fonction de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="dda14-173">Make sure you change hello file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="dda14-174">Vous verrez un résultat similaire indiquant que l’importation de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="dda14-174">You will see a similar result showing that hello import succeeded.</span></span>

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a><span data-ttu-id="dda14-175">Partie 6 - créer une passerelle de hello</span><span class="sxs-lookup"><span data-stu-id="dda14-175">Part 6 - Create hello gateway</span></span>

<span data-ttu-id="dda14-176">Avant d’exécuter cet exemple, consultez toohello fichier de configuration réseau que vous avez téléchargé pour hello exacte des noms que Azure attend toosee.</span><span class="sxs-lookup"><span data-stu-id="dda14-176">Before running this example, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="dda14-177">fichier de configuration de réseau Hello contient des valeurs de hello pour vos réseaux virtuels classiques.</span><span class="sxs-lookup"><span data-stu-id="dda14-177">hello network configuration file contains hello values for your classic virtual networks.</span></span> <span data-ttu-id="dda14-178">Parfois, les noms de hello pour classique des réseaux virtuels sont modifiées dans le fichier de configuration de réseau hello lors de la création des paramètres de réseau virtuel classiques dans hello portail Azure en raison de différences toohello dans les modèles de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-178">Sometimes hello names for classic VNets are changed in hello network configuration file when creating classic VNet settings in hello Azure portal due toohello differences in hello deployment models.</span></span> <span data-ttu-id="dda14-179">Par exemple, si vous avez utilisé hello Azure toocreate portail un réseau virtuel classique nommé « Réseau virtuel classique » et créé un conteneur dans un groupe de ressources nommé 'ClassicRG', nom hello qui est contenue dans le fichier de configuration de réseau hello est converti too'Group réseau virtuel classique de ClassicRG'.</span><span class="sxs-lookup"><span data-stu-id="dda14-179">For example, if you used hello Azure portal toocreate a classic VNet named 'Classic VNet' and created it in a resource group named 'ClassicRG', hello name that is contained in hello network configuration file is converted too'Group ClassicRG Classic VNet'.</span></span> <span data-ttu-id="dda14-180">Lorsque vous spécifiez le nom hello d’un réseau virtuel qui contient des espaces, placez-la entre guillemets les valeur hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-180">When specifying hello name of a VNet that contains spaces, use quotation marks around hello value.</span></span>


<span data-ttu-id="dda14-181">Utilisez hello suivant exemple toocreate une passerelle avec routage dynamique :</span><span class="sxs-lookup"><span data-stu-id="dda14-181">Use hello following example toocreate a dynamic routing gateway:</span></span>

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

<span data-ttu-id="dda14-182">Vous pouvez vérifier l’état de hello de passerelle de hello à l’aide de hello **Get-AzureVNetGateway** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="dda14-182">You can check hello status of hello gateway by using hello **Get-AzureVNetGateway** cmdlet.</span></span>

## <span data-ttu-id="dda14-183"><a name="creatermgw"></a>Section 2 : Configurer hello passerelle de réseau virtuel du Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="dda14-183"><a name="creatermgw"></a>Section 2: Configure hello RM VNet gateway</span></span>
<span data-ttu-id="dda14-184">toocreate une passerelle VPN pour hello réseau virtuel RM, suivez hello suivant les instructions.</span><span class="sxs-lookup"><span data-stu-id="dda14-184">toocreate a VPN gateway for hello RM VNet, follow hello following instructions.</span></span> <span data-ttu-id="dda14-185">Ne pas démarrer les étapes hello jusqu'à ce qu’après avoir récupéré les adresse IP publique hello pour la passerelle de hello classique de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="dda14-185">Don't start hello steps until after you have retrieved hello public IP address for hello classic VNet's gateway.</span></span> 

1. <span data-ttu-id="dda14-186">Ouvrez une session dans tooyour compte Azure dans la console PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-186">Log in tooyour Azure account in hello PowerShell console.</span></span> <span data-ttu-id="dda14-187">Hello applet de commande suivante vous demande les informations d’identification de hello pour votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="dda14-187">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="dda14-188">Après la connexion, les paramètres de votre compte sont téléchargés afin qu’ils soient disponible tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dda14-188">After logging in, your account settings are downloaded so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  <span data-ttu-id="dda14-189">Si vous possédez plusieurs abonnements, procurez-vous la liste de vos abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="dda14-189">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
   
  <span data-ttu-id="dda14-190">Spécifiez un abonnement hello que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="dda14-190">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="dda14-191">Créer une passerelle de réseau local.</span><span class="sxs-lookup"><span data-stu-id="dda14-191">Create a local network gateway.</span></span> <span data-ttu-id="dda14-192">Dans un réseau virtuel, passerelle de réseau local hello fait généralement référence emplacement local de tooyour.</span><span class="sxs-lookup"><span data-stu-id="dda14-192">In a virtual network, hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="dda14-193">Dans ce cas, passerelle de réseau local hello fait référence tooyour classique de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="dda14-193">In this case, hello local network gateway refers tooyour Classic VNet.</span></span> <span data-ttu-id="dda14-194">Lui donner un nom par lequel Azure permettre faire référence tooit et également spécifier le préfixe d’espace adresse hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-194">Give it a name by which Azure can refer tooit, and also specify hello address space prefix.</span></span> <span data-ttu-id="dda14-195">Azure utilise le préfixe d’adresse IP hello vous spécifiez tooidentify les tooyour toosend de trafic emplacement local.</span><span class="sxs-lookup"><span data-stu-id="dda14-195">Azure uses hello IP address prefix you specify tooidentify which traffic toosend tooyour on-premises location.</span></span> <span data-ttu-id="dda14-196">Si vous avez besoin d’informations tooadjust hello ici une version ultérieure, avant de créer votre passerelle, vous pouvez modifier les valeurs hello et exemple hello exécuter à nouveau.</span><span class="sxs-lookup"><span data-stu-id="dda14-196">If you need tooadjust hello information here later, before creating your gateway, you can modify hello values and run hello sample again.</span></span>
   
   <span data-ttu-id="dda14-197">**-Name** est hello nom de passerelle de réseau local tooassign toorefer toohello.</span><span class="sxs-lookup"><span data-stu-id="dda14-197">**-Name** is hello name you want tooassign toorefer toohello local network gateway.</span></span><br><span data-ttu-id="dda14-198">
   **Préfixe d’adresse -** est hello espace d’adressage de votre réseau virtuel classique.</span><span class="sxs-lookup"><span data-stu-id="dda14-198">
   **-AddressPrefix** is hello Address Space for your classic VNet.</span></span><br><span data-ttu-id="dda14-199">
**-GatewayIpAddress** est hello une adresse IP publique de la passerelle de hello classique de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="dda14-199">
**-GatewayIpAddress** is hello public IP address of hello classic VNet's gateway.</span></span> <span data-ttu-id="dda14-200">Veillez à suivant de hello toochange exemple tooreflect hello adresse IP.</span><span class="sxs-lookup"><span data-stu-id="dda14-200">Be sure toochange hello following sample tooreflect hello correct IP address.</span></span><br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. <span data-ttu-id="dda14-201">La demande publique IP adresse toobe toohello alloué passerelle de réseau virtuel pour hello Gestionnaire de ressources VNet.</span><span class="sxs-lookup"><span data-stu-id="dda14-201">Request a public IP address toobe allocated toohello virtual network gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="dda14-202">Vous ne pouvez pas spécifier hello adresse IP que vous toouse.</span><span class="sxs-lookup"><span data-stu-id="dda14-202">You can't specify hello IP address that you want toouse.</span></span> <span data-ttu-id="dda14-203">adresse IP de Hello est allouée dynamiquement la passerelle de réseau virtuel toohello.</span><span class="sxs-lookup"><span data-stu-id="dda14-203">hello IP address is dynamically allocated toohello virtual network gateway.</span></span> <span data-ttu-id="dda14-204">Toutefois, cela ne signifie pas de changements d’adresses IP hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-204">However, this does not mean hello IP address changes.</span></span> <span data-ttu-id="dda14-205">Hello seule fois changements d’adresses IP passerelle hello réseau virtuel est hello lorsque la passerelle est supprimée et recréée.</span><span class="sxs-lookup"><span data-stu-id="dda14-205">hello only time hello virtual network gateway IP address changes is when hello gateway is deleted and recreated.</span></span> <span data-ttu-id="dda14-206">Il ne change pas sur le redimensionnement, la réinitialisation ou autre maintenance/mise à niveau interne de la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-206">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of hello gateway.</span></span>

  <span data-ttu-id="dda14-207">Dans cette étape, nous définissons également une variable qui sera utilisée à une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="dda14-207">In this step, we also set a variable that is used in a later step.</span></span>

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. <span data-ttu-id="dda14-208">Vérifiez que votre réseau virtuel possède un sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="dda14-208">Verify that your virtual network has a gateway subnet.</span></span> <span data-ttu-id="dda14-209">S’il n’existe aucun sous-réseau de passerelle, ajoutez-en un.</span><span class="sxs-lookup"><span data-stu-id="dda14-209">If no gateway subnet exists, add one.</span></span> <span data-ttu-id="dda14-210">Assurez-vous que le sous-réseau de passerelle hello est nommé *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="dda14-210">Make sure hello gateway subnet is named *GatewaySubnet*.</span></span>
5. <span data-ttu-id="dda14-211">Récupérer le sous-réseau hello utilisé pour la passerelle de hello en exécutant hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="dda14-211">Retrieve hello subnet used for hello gateway by running hello following command.</span></span> <span data-ttu-id="dda14-212">Dans cette étape, nous définissons également une variable toobe utilisé à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-212">In this step, we also set a variable toobe used in hello next step.</span></span>
   
   <span data-ttu-id="dda14-213">**-Name** hello désigne votre VNet Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="dda14-213">**-Name** is hello name of your Resource Manager VNet.</span></span><br><span data-ttu-id="dda14-214">
   **-ResourceGroupName** est groupe de ressources hello que hello réseau virtuel est associé.</span><span class="sxs-lookup"><span data-stu-id="dda14-214">
**-ResourceGroupName** is hello resource group that hello VNet is associated with.</span></span> <span data-ttu-id="dda14-215">sous-réseau de passerelle Hello pour ce réseau virtuel doivent déjà exister et doit être nommé *GatewaySubnet* toowork correctement.</span><span class="sxs-lookup"><span data-stu-id="dda14-215">hello gateway subnet must already exist for this VNet and must be named *GatewaySubnet* toowork properly.</span></span><br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. <span data-ttu-id="dda14-216">Créer la configuration d’adressage IP de la passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-216">Create hello gateway IP addressing configuration.</span></span> <span data-ttu-id="dda14-217">configuration de la passerelle Hello définit le sous-réseau de hello et toouse adresse IP publique de hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-217">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="dda14-218">Les exemples suivants de hello utilisation toocreate votre configuration de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="dda14-218">Use hello following sample toocreate your gateway configuration.</span></span>

  <span data-ttu-id="dda14-219">Dans cette étape, hello **- IDSousRéseau** et **- PublicIpAddressId** paramètres doivent être passés propriété d’id hello à partir du sous-réseau de hello et objets d’adresse IP, respectivement.</span><span class="sxs-lookup"><span data-stu-id="dda14-219">In this step, hello **-SubnetId** and **-PublicIpAddressId** parameters must be passed hello id property from hello subnet, and IP address objects, respectively.</span></span> <span data-ttu-id="dda14-220">Vous ne pouvez pas utiliser une chaîne simple.</span><span class="sxs-lookup"><span data-stu-id="dda14-220">You can't use a simple string.</span></span> <span data-ttu-id="dda14-221">Ces variables sont définies dans hello étape toorequest une adresse IP publique et hello étape tooretrieve hello sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="dda14-221">These variables are set in hello step toorequest a public IP and hello step tooretrieve hello subnet.</span></span>

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. <span data-ttu-id="dda14-222">Créer des passerelle de réseau virtuel du Gestionnaire de ressources hello en hello suivant de commande en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="dda14-222">Create hello Resource Manager virtual network gateway by running hello following command.</span></span> <span data-ttu-id="dda14-223">Hello `-VpnType` doit être *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="dda14-223">hello `-VpnType` must be *RouteBased*.</span></span> <span data-ttu-id="dda14-224">Il peut prendre entre 45 minutes ou plus pour hello passerelle toocreate.</span><span class="sxs-lookup"><span data-stu-id="dda14-224">It can take 45 minutes or more for hello gateway toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. <span data-ttu-id="dda14-225">Copiez l’adresse IP publique de hello une fois la passerelle VPN de hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="dda14-225">Copy hello public IP address once hello VPN gateway has been created.</span></span> <span data-ttu-id="dda14-226">Utilisez-la lorsque vous configurez les paramètres de réseau local hello pour votre réseau virtuel classique.</span><span class="sxs-lookup"><span data-stu-id="dda14-226">You use it when you configure hello local network settings for your Classic VNet.</span></span> <span data-ttu-id="dda14-227">Vous pouvez utiliser hello suivant l’adresse IP publique d’applet de commande tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-227">You can use hello following cmdlet tooretrieve hello public IP address.</span></span> <span data-ttu-id="dda14-228">adresse IP publique Hello est répertoriée dans hello retour en tant que *IpAddress*.</span><span class="sxs-lookup"><span data-stu-id="dda14-228">hello public IP address is listed in hello return as *IpAddress*.</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a><span data-ttu-id="dda14-229">Section 3 : Modifier les paramètres de site local de réseau virtuel classiques hello</span><span class="sxs-lookup"><span data-stu-id="dda14-229">Section 3: Modify hello classic VNet local site settings</span></span>

<span data-ttu-id="dda14-230">Dans cette section, vous travaillez avec hello réseau virtuel classique.</span><span class="sxs-lookup"><span data-stu-id="dda14-230">In this section, you work with hello classic VNet.</span></span> <span data-ttu-id="dda14-231">Vous remplacez les adresses IP hello espace réservé que vous avez utilisé lors de la spécification des paramètres du site local hello qui seront utilisé tooconnect toohello passerelle du Gestionnaire de ressources VNet.</span><span class="sxs-lookup"><span data-stu-id="dda14-231">You replace hello placeholder IP address that you used when specifying hello local site settings that will be used tooconnect toohello Resource Manager VNet gateway.</span></span> 

1. <span data-ttu-id="dda14-232">Exporter le fichier de configuration de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-232">Export hello network configuration file.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. <span data-ttu-id="dda14-233">À l’aide d’un éditeur de texte, de modifier la valeur de hello pour l’élément VPNGatewayAddress.</span><span class="sxs-lookup"><span data-stu-id="dda14-233">Using a text editor, modify hello value for VPNGatewayAddress.</span></span> <span data-ttu-id="dda14-234">Remplacez adresse espace réservé de hello hello adresse IP publique de passerelle du Gestionnaire de ressources hello, puis enregistrez les modifications hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-234">Replace hello placeholder IP address with hello public IP address of hello Resource Manager gateway and then save hello changes.</span></span>

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. <span data-ttu-id="dda14-235">Hello d’importation modifiée tooAzure de fichier de configuration de réseau.</span><span class="sxs-lookup"><span data-stu-id="dda14-235">Import hello modified network configuration file tooAzure.</span></span>

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <span data-ttu-id="dda14-236"><a name="connect"></a>Dans la section 4 : Créer une connexion entre les passerelles hello</span><span class="sxs-lookup"><span data-stu-id="dda14-236"><a name="connect"></a>Section 4: Create a connection between hello gateways</span></span>
<span data-ttu-id="dda14-237">Création d’une connexion entre les passerelles hello requiert PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dda14-237">Creating a connection between hello gateways requires PowerShell.</span></span> <span data-ttu-id="dda14-238">Vous devrez peut-être tooadd votre version compte Azure toouse hello classique d’applets de commande PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-238">You may need tooadd your Azure Account toouse hello classic version of hello  PowerShell cmdlets.</span></span> <span data-ttu-id="dda14-239">toodo donc utiliser **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="dda14-239">toodo so, use **Add-AzureAccount**.</span></span>

1. <span data-ttu-id="dda14-240">Dans la console PowerShell hello, définissez votre clé partagée.</span><span class="sxs-lookup"><span data-stu-id="dda14-240">In hello PowerShell console, set your shared key.</span></span> <span data-ttu-id="dda14-241">Avant d’exécuter les applets de commande hello, consultez toohello fichier de configuration réseau que vous avez téléchargé pour hello exacte des noms que Azure attend toosee.</span><span class="sxs-lookup"><span data-stu-id="dda14-241">Before running hello cmdlets, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="dda14-242">Lorsque vous spécifiez le nom hello d’un réseau virtuel qui contient des espaces, utilisez des guillemets simples autour de valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-242">When specifying hello name of a VNet that contains spaces, use single quotation marks around hello value.</span></span><br><br><span data-ttu-id="dda14-243">Dans l’exemple suivant, **- VNetName** hello désigne hello réseau virtuel classique et **LocalNetworkSiteName -** est le nom hello spécifié pour le site de réseau local hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-243">In following example, **-VNetName** is hello name of hello classic VNet and **-LocalNetworkSiteName** is hello name you specified for hello local network site.</span></span> <span data-ttu-id="dda14-244">Hello **SharedKey -** est une valeur que vous générez et que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="dda14-244">hello **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="dda14-245">Dans l’exemple de hello, nous avons utilisé « abc123 », mais vous pouvez également générer et utiliser quelque chose de plus complexe.</span><span class="sxs-lookup"><span data-stu-id="dda14-245">In hello example, we used 'abc123', but you can generate and use something more complex.</span></span> <span data-ttu-id="dda14-246">Hello important est cette valeur hello que vous spécifiez ici doit être hello que même valeur que vous spécifiez dans l’étape suivante de hello lorsque vous créez votre connexion.</span><span class="sxs-lookup"><span data-stu-id="dda14-246">hello important thing is that hello value you specify here must be hello same value that you specify in hello next step when you create your connection.</span></span> <span data-ttu-id="dda14-247">Hello retour doit afficher **état : réussite**.</span><span class="sxs-lookup"><span data-stu-id="dda14-247">hello return should show **Status: Successful**.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. <span data-ttu-id="dda14-248">Créer la connexion de VPN de hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="dda14-248">Create hello VPN connection by running hello following commands:</span></span>
   
  <span data-ttu-id="dda14-249">Définir les variables de hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-249">Set hello variables.</span></span>

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  <span data-ttu-id="dda14-250">Créer la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="dda14-250">Create hello connection.</span></span> <span data-ttu-id="dda14-251">Notez que hello **- ConnectionType** IPSec, Vnet2Vnet pas.</span><span class="sxs-lookup"><span data-stu-id="dda14-251">Notice that hello **-ConnectionType** is IPsec, not Vnet2Vnet.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a><span data-ttu-id="dda14-252">Section 5 : Vérifier vos connexions</span><span class="sxs-lookup"><span data-stu-id="dda14-252">Section 5: Verify your connections</span></span>

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a><span data-ttu-id="dda14-253">connexion de hello tooverify à partir de votre tooyour de réseau virtuel classique Gestionnaire de ressources VNet</span><span class="sxs-lookup"><span data-stu-id="dda14-253">tooverify hello connection from your classic VNet tooyour Resource Manager VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="dda14-254">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dda14-254">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="dda14-255">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="dda14-255">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a><span data-ttu-id="dda14-256">connexion de hello tooverify à partir de votre gestionnaire de ressources du VNet de tooyour réseau virtuel classique</span><span class="sxs-lookup"><span data-stu-id="dda14-256">tooverify hello connection from your Resource Manager VNet tooyour classic VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="dda14-257">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dda14-257">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="dda14-258">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="dda14-258">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="dda14-259"><a name="faq"></a>Forum Aux Questions sur l’interconnexion de réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="dda14-259"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

