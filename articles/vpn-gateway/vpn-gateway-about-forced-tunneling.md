---
title: "Configurer le tunneling forcé pour les connexions de site à site Azure : modèle de déploiement classique | Microsoft Docs"
description: "Comment tooredirect ou 'force' tous les Internet liées au trafic arrière tooyour emplacement local."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a><span data-ttu-id="7a5aa-103">Configurer le tunneling forcé à l’aide de modèle de déploiement classique de hello</span><span class="sxs-lookup"><span data-stu-id="7a5aa-103">Configure forced tunneling using hello classic deployment model</span></span>

<span data-ttu-id="7a5aa-104">Forcé tunneling permet de rediriger ou de « forcer » tous les Internet liées au trafic tooyour arrière local emplacement via un tunnel VPN de Site à Site pour l’inspection et d’audit.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="7a5aa-105">Il s’agit d’une condition de sécurité critique pour la plupart des stratégies informatiques d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="7a5aa-106">Sans tunneling forcé, le trafic Internet à partir de vos machines virtuelles dans Azure traverse toujours l’infrastructure réseau Azure directement out toohello Internet, sans hello option tooallow vous tooinspect ou audit du trafic hello.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="7a5aa-107">Accès Internet non autorisé peut entraîner la divulgation de tooinformation ou d’autres types de failles de sécurité.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="7a5aa-108">Cet article vous guide dans la configuration forcé tunneling pour les réseaux virtuels créés à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-108">This article walks you through configuring forced tunneling for virtual networks created using hello classic deployment model.</span></span> <span data-ttu-id="7a5aa-109">Le tunneling forcé peut être configuré à l’aide de PowerShell, pas via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="7a5aa-110">Si vous souhaitez tooconfigure tunneling pour le modèle de déploiement du Gestionnaire de ressources hello forcé, sélectionnez l’article classique hello suivant la liste déroulante :</span><span class="sxs-lookup"><span data-stu-id="7a5aa-110">If you want tooconfigure forced tunneling for hello Resource Manager deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a5aa-111">PowerShell - Classique</span><span class="sxs-lookup"><span data-stu-id="7a5aa-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="7a5aa-112">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7a5aa-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a><span data-ttu-id="7a5aa-113">Conditions requises et éléments à prendre en compte</span><span class="sxs-lookup"><span data-stu-id="7a5aa-113">Requirements and considerations</span></span>
<span data-ttu-id="7a5aa-114">Le tunneling forcé dans Azure est configuré par le biais d’itinéraires définis par l’utilisateur de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-114">Forced tunneling in Azure is configured via virtual network user-defined routes (UDR).</span></span> <span data-ttu-id="7a5aa-115">Redirection du trafic tooan local de site est exprimé comme passerelle VPN Azure toohello itinéraire par défaut.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-115">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="7a5aa-116">Hello section suivante répertorie les limite de hello actuelle de la table de routage hello et les itinéraires pour un réseau virtuel Azure :</span><span class="sxs-lookup"><span data-stu-id="7a5aa-116">hello following section lists hello current limitation of hello routing table and routes for an Azure Virtual Network:</span></span>

* <span data-ttu-id="7a5aa-117">Chaque sous-réseau du réseau virtuel dispose d’une table de routage système intégrée.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-117">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="7a5aa-118">table de routage système Hello a hello trois groupes d’itinéraires suivants :</span><span class="sxs-lookup"><span data-stu-id="7a5aa-118">hello system routing table has hello following three groups of routes:</span></span>

  * <span data-ttu-id="7a5aa-119">**Les itinéraires de réseau virtuel locales :** directement toohello machines virtuelles de destination Bonjour même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-119">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="7a5aa-120">**Itinéraires locaux :** passerelle VPN Azure de toohello.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-120">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="7a5aa-121">**L’itinéraire par défaut :** directement toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-121">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="7a5aa-122">Les paquets destinés aux toohello des adresses IP privées non couvertes par les itinéraires hello deux précédents sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-122">Packets destined toohello private IP addresses not covered by hello previous two routes will be dropped.</span></span>
* <span data-ttu-id="7a5aa-123">Avec la version hello d’itinéraires définis par l’utilisateur, vous pouvez créer un tooadd de table de routage un itinéraire par défaut et associez ensuite hello routage table tooyour réseau virtuel ou les sous-réseaux tooenable forcé tunneling sur ces sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-123">With hello release of user-defined routes, you can create a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="7a5aa-124">Vous devez tooset un « site par défaut » entre le réseau virtuel de hello intersite sites locaux toohello connecté.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-124">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span>
* <span data-ttu-id="7a5aa-125">Le tunneling forcé doit être associé à un réseau virtuel équipé d'une passerelle VPN à routage dynamique (pas de passerelle statique).</span><span class="sxs-lookup"><span data-stu-id="7a5aa-125">Forced tunneling must be associated with a VNet that has a dynamic routing VPN gateway (not a static gateway).</span></span>
* <span data-ttu-id="7a5aa-126">ExpressRoute le tunneling forcé n’est pas configuré via ce mécanisme, mais au lieu de cela, est activé par annonce un itinéraire par défaut via hello BGP ExpressRoute sessions d’homologation.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-126">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="7a5aa-127">Consultez hello [Documentation d’ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-127">Please see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/) for more information.</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="7a5aa-128">Présentation de la configuration</span><span class="sxs-lookup"><span data-stu-id="7a5aa-128">Configuration overview</span></span>
<span data-ttu-id="7a5aa-129">Dans l’exemple suivant de hello, hello frontal sous-réseau n’est pas forcé en tunnel.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-129">In hello following example, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="7a5aa-130">les charges de travail Hello dans le sous-réseau du serveur frontal hello continuer tooaccept et répondre toocustomer demandes de hello Internet directement.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-130">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="7a5aa-131">Hello sous-réseaux de niveau intermédiaire et principaux sont forcés en tunnel.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-131">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="7a5aa-132">Toutes les connexions sortantes à partir de ces toohello deux sous-réseaux Internet sera forcée ou redirigée retour tooan sur site local via l’une des hello que les tunnels VPN de S2S.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-132">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="7a5aa-133">Cela vous permet de toorestrict et inspecter les accès Internet à partir de vos machines virtuelles ou services cloud dans Azure, tout en continuant tooenable votre architecture de service à plusieurs niveaux requise.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-133">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="7a5aa-134">Vous pouvez également appliquer forcé tunneling toohello réseaux virtuels entiers s’il n’y aucune charge de travail sur Internet dans vos réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-134">You also can apply forced tunneling toohello entire virtual networks if there are no Internet-facing workloads in your virtual networks.</span></span>

![Tunneling forcé](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a><span data-ttu-id="7a5aa-136">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="7a5aa-136">Before you begin</span></span>
<span data-ttu-id="7a5aa-137">Vérifiez que vous avez hello suivant d’éléments de configuration avant la configuration de début.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-137">Verify that you have hello following items before beginning configuration.</span></span>

* <span data-ttu-id="7a5aa-138">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-138">An Azure subscription.</span></span> <span data-ttu-id="7a5aa-139">Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a5aa-139">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7a5aa-140">Un réseau virtuel configuré.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-140">A configured virtual network.</span></span> 
* <span data-ttu-id="7a5aa-141">version la plus récente Hello Hello applets de commande PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-141">hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="7a5aa-142">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur l’installation des applets de commande PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-142">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

## <a name="configure-forced-tunneling"></a><span data-ttu-id="7a5aa-143">Configurer un tunneling forcé</span><span class="sxs-lookup"><span data-stu-id="7a5aa-143">Configure forced tunneling</span></span>
<span data-ttu-id="7a5aa-144">Hello procédure vous permet de spécifier un tunneling forcé pour un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-144">hello following procedure will help you specify forced tunneling for a virtual network.</span></span> <span data-ttu-id="7a5aa-145">les étapes de configuration de Hello correspondent toohello fichier de configuration de réseau de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-145">hello configuration steps correspond toohello VNet network configuration file.</span></span>

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

<span data-ttu-id="7a5aa-146">Dans cet exemple, réseau virtuel de hello 'MultiTier-VNet' a trois sous-réseaux : sous-réseaux « Frontal », « Intermédiaire » et « Principal », avec des connexions de site entre quatre : 'DefaultSiteHQ' et trois Branches.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-146">In this example, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend' subnets, with four cross premises connections: 'DefaultSiteHQ', and three Branches.</span></span> 

<span data-ttu-id="7a5aa-147">étapes de Hello seront hello 'DefaultSiteHQ' en tant que connexion de site par défaut hello pour le tunneling forcé et configurez hello intermédiaire et principal sous-réseaux toouse le tunneling forcé.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-147">hello steps will set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello Midtier and Backend subnets toouse forced tunneling.</span></span>

1. <span data-ttu-id="7a5aa-148">Créez une table de routage.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-148">Create a routing table.</span></span> <span data-ttu-id="7a5aa-149">Utilisez hello suivant toocreate de l’applet de commande de votre table d’itinéraires.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-149">Use hello following cmdlet toocreate your route table.</span></span>

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. <span data-ttu-id="7a5aa-150">Ajouter une table de routage toohello de routage par défaut.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-150">Add a default route toohello routing table.</span></span> 

  <span data-ttu-id="7a5aa-151">Hello exemple suivant ajoute une table routage toohello itinéraire par défaut créée à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-151">hello following example adds a default route toohello routing table created in Step 1.</span></span> <span data-ttu-id="7a5aa-152">Notez que hello uniquement les itinéraires pris en charge est le préfixe de destination hello de « 0.0.0.0/0 » toohello saut suivant de « VPNGateway ».</span><span class="sxs-lookup"><span data-stu-id="7a5aa-152">Note that hello only route supported is hello destination prefix of "0.0.0.0/0" toohello "VPNGateway" NextHop.</span></span>

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. <span data-ttu-id="7a5aa-153">Associer des sous-réseaux toohello table routage hello.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-153">Associate hello routing table toohello subnets.</span></span> 

  <span data-ttu-id="7a5aa-154">Après une table de routage est créée et un itinéraire ajouté, utilisez hello suivant exemple tooadd ou associer le sous-réseau de réseau virtuel tooa hello itinéraire table.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-154">After a routing table is created and a route added, use hello following example tooadd or associate hello route table tooa VNet subnet.</span></span> <span data-ttu-id="7a5aa-155">Hello exemple ajoute hello itinéraire table « MyRouteTable » toohello intermédiaire et principaux sous-réseaux de VNet MultiTier-VNet.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-155">hello example adds hello route table "MyRouteTable" toohello Midtier and Backend subnets of VNet MultiTier-VNet.</span></span>

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. <span data-ttu-id="7a5aa-156">Affectez un site par défaut pour le tunneling forcé.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-156">Assign a default site for forced tunneling.</span></span> 

  <span data-ttu-id="7a5aa-157">Bonjour précédant l’étape, hello exemples applet de commande de script créé hello table de routage et associé hello itinéraire table tootwo des sous-réseaux du réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-157">In hello preceding step, hello sample cmdlet scripts created hello routing table and associated hello route table tootwo of hello VNet subnets.</span></span> <span data-ttu-id="7a5aa-158">étape restante de Hello est tooselect un site local parmi les connexions de plusieurs sites hello du réseau virtuel de hello en tant que site par défaut de hello ou tunnel.</span><span class="sxs-lookup"><span data-stu-id="7a5aa-158">hello remaining step is tooselect a local site among hello multi-site connections of hello virtual network as hello default site or tunnel.</span></span>

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a><span data-ttu-id="7a5aa-159">Autres applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a5aa-159">Additional PowerShell cmdlets</span></span>
### <a name="toodelete-a-route-table"></a><span data-ttu-id="7a5aa-160">toodelete une table de routage</span><span class="sxs-lookup"><span data-stu-id="7a5aa-160">toodelete a route table</span></span>

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a><span data-ttu-id="7a5aa-161">toolist une table de routage</span><span class="sxs-lookup"><span data-stu-id="7a5aa-161">toolist a route table</span></span>

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a><span data-ttu-id="7a5aa-162">toodelete un itinéraire à partir d’une table de routage</span><span class="sxs-lookup"><span data-stu-id="7a5aa-162">toodelete a route from a route table</span></span>

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a><span data-ttu-id="7a5aa-163">tooremove un itinéraire à partir d’un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="7a5aa-163">tooremove a route from a subnet</span></span>

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a><span data-ttu-id="7a5aa-164">table d’itinéraires hello toolist associée à un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="7a5aa-164">toolist hello route table associated with a subnet</span></span>

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a><span data-ttu-id="7a5aa-165">tooremove un site par défaut à partir d’une passerelle VPN du VNet</span><span class="sxs-lookup"><span data-stu-id="7a5aa-165">tooremove a default site from a VNet VPN gateway</span></span>

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```