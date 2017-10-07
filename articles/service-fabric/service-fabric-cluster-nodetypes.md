---
title: "l’ensemble fibre optique d’aaaService types de nœuds et les jeux de mise à l’échelle de machine virtuelle | Documents Microsoft"
description: "Décrit l’interaction avec les types de nœud de Service Fabric tooVM identiques et comment tooremote connecter instance d’ensemble d’échelle de machine virtuelle tooa ou un nœud de cluster."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="2f334-103">relation Hello entre les types de nœuds de l’infrastructure de Service et les machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="2f334-103">hello relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="2f334-104">Machines virtuelles identiques sont une ressource de calcul Azure, vous pouvez utiliser toodeploy et gérer une collection d’ordinateurs virtuels en tant qu’ensemble.</span><span class="sxs-lookup"><span data-stu-id="2f334-104">Virtual Machine Scale Sets are an Azure Compute resource you can use toodeploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="2f334-105">Chaque type de nœud qui est défini dans un cluster Service Fabric est configuré en tant que jeu de mise à l’échelle de machine virtuelle distinct.</span><span class="sxs-lookup"><span data-stu-id="2f334-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="2f334-106">Chaque type de nœud peut ensuite faire l’objet d’une montée ou descente en puissance de manière indépendante, avoir différents jeux de ports ouverts et présenter différentes métriques de capacité.</span><span class="sxs-lookup"><span data-stu-id="2f334-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="2f334-107">Hello suivant capture d’écran montre un cluster qui possède deux types de nœuds : serveur frontal et principal.</span><span class="sxs-lookup"><span data-stu-id="2f334-107">hello following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="2f334-108">Chaque type de nœud comporte cinq nœuds.</span><span class="sxs-lookup"><span data-stu-id="2f334-108">Each node type has five nodes each.</span></span>

![Capture d’écran d’un cluster qui a deux types de nœuds][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a><span data-ttu-id="2f334-110">Mappage toonodes d’instances ensemble d’échelle de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="2f334-110">Mapping VM Scale Set instances toonodes</span></span>
<span data-ttu-id="2f334-111">Comme vous pouvez le voir ci-dessus, les instances d’ensemble d’échelle de machine virtuelle hello démarrer à partir de l’instance 0 et puis remonte.</span><span class="sxs-lookup"><span data-stu-id="2f334-111">As you can see above, hello VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="2f334-112">la numérotation Hello est répercutée dans les noms de hello.</span><span class="sxs-lookup"><span data-stu-id="2f334-112">hello numbering is reflected in hello names.</span></span> <span data-ttu-id="2f334-113">Par exemple, BackEnd_0 est instance 0 du hello ensemble d’échelle de machine virtuelle principale.</span><span class="sxs-lookup"><span data-stu-id="2f334-113">For example, BackEnd_0 is instance 0 of hello BackEnd VM Scale Set.</span></span> <span data-ttu-id="2f334-114">Ce groupe a cinq instances, nommées BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 et BackEnd_4.</span><span class="sxs-lookup"><span data-stu-id="2f334-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="2f334-115">Quand vous effectuez une montée en puissance sur un groupe de machines virtuelles identiques, une instance est créée.</span><span class="sxs-lookup"><span data-stu-id="2f334-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="2f334-116">Hello nouvel ensemble d’échelle de machine virtuelle nom de l’instance sera généralement le nom d’ensemble d’échelle de machine virtuelle hello + numéro d’instance suivant hello.</span><span class="sxs-lookup"><span data-stu-id="2f334-116">hello new VM Scale Set instance name will typically be hello VM Scale Set name + hello next instance number.</span></span> <span data-ttu-id="2f334-117">Dans notre exemple, il s’agit de BackEnd_5.</span><span class="sxs-lookup"><span data-stu-id="2f334-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a><span data-ttu-id="2f334-118">Mappage des machines virtuelles identiques charger équilibrages tooeach nœud type/machine virtuelle ensemble d’échelle</span><span class="sxs-lookup"><span data-stu-id="2f334-118">Mapping VM scale set load balancers tooeach node type/VM Scale Set</span></span>
<span data-ttu-id="2f334-119">Si vous avez déployé votre cluster à partir du portail de hello ou que vous avez utilisé hello exemple Gestionnaire de ressources de modèle que nous avons fournis, puis lorsque vous obtenez une liste de toutes les ressources sous un groupe de ressources vous verrez les équilibreurs de charge hello pour chaque type de nœud ou ensemble d’échelle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2f334-119">If you have deployed your cluster from hello portal or have used hello sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see hello load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="2f334-120">Hello nom serait quelque chose comme : **LB -&lt;NodeType nom&gt;**.</span><span class="sxs-lookup"><span data-stu-id="2f334-120">hello name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="2f334-121">Par exemple, LB-sfcluster4doc-0, comme indiqué dans cette capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="2f334-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![Ressources][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="2f334-123">Instance de tooa ensemble d’échelle de machine virtuelle ou un nœud de cluster de connexion à distance</span><span class="sxs-lookup"><span data-stu-id="2f334-123">Remote connect tooa VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="2f334-124">Chaque type de nœud qui est défini dans un cluster est configuré comme un jeu de mise à l’échelle de machine virtuelle distinct.</span><span class="sxs-lookup"><span data-stu-id="2f334-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="2f334-125">Que signifie hello des types de nœud peut être mis à l’échelle vers le haut ou vers le bas de manière indépendante et vous pouvez établir des références SKU de machine virtuelle différente.</span><span class="sxs-lookup"><span data-stu-id="2f334-125">That means hello node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="2f334-126">Contrairement aux ordinateurs virtuels d’instance unique, les instances d’ensemble d’échelle de machine virtuelle hello n’obtiennent pas une adresse IP virtuelle de leurs propres.</span><span class="sxs-lookup"><span data-stu-id="2f334-126">Unlike single instance VMs, hello VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="2f334-127">Il peut être un peu difficile lorsque vous recherchez une adresse IP adresse et le port que vous pouvez utiliser tooremote connectent instance spécifique de tooa.</span><span class="sxs-lookup"><span data-stu-id="2f334-127">So it can be a bit challenging when you are looking for an IP address and port that you can use tooremote connect tooa specific instance.</span></span>

<span data-ttu-id="2f334-128">Voici les étapes hello vous pouvez suivre toodiscover les.</span><span class="sxs-lookup"><span data-stu-id="2f334-128">Here are hello steps you can follow toodiscover them.</span></span>

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="2f334-129">Étape 1 : Découvrir les adresse IP virtuelle hello hello type de nœud, puis les règles NAT entrantes pour RDP</span><span class="sxs-lookup"><span data-stu-id="2f334-129">Step 1: Find out hello virtual IP address for hello node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="2f334-130">Dans tooget de commande, vous avez besoin tooget hello NAT de trafic entrant règles des valeurs qui ont été définies dans le cadre de la définition de ressource hello pour **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="2f334-130">In order tooget that, you need tooget hello inbound NAT rules values that were defined as a part of hello resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="2f334-131">Dans le portail hello, accédez au panneau de programme d’équilibrage de charge toohello, puis **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="2f334-131">In hello portal, navigate toohello Load balancer blade and then **Settings**.</span></span>

![Panneau Équilibrage de charge][LBBlade]

<span data-ttu-id="2f334-133">Dans **Paramètres**, cliquez sur **Règles NAT de trafic entrant**.</span><span class="sxs-lookup"><span data-stu-id="2f334-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="2f334-134">Cela maintenant donne vous hello d’adresse IP et port que vous pouvez utiliser tooremote connecter toohello première instance ensemble d’échelle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2f334-134">This now gives you hello IP address and port that you can use tooremote connect toohello first VM Scale Set instance.</span></span> <span data-ttu-id="2f334-135">Dans la capture d’écran de hello ci-dessous, il est **104.42.106.156** et **3389**</span><span class="sxs-lookup"><span data-stu-id="2f334-135">In hello screenshot below, it is **104.42.106.156** and **3389**</span></span>

![Règles NAT][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a><span data-ttu-id="2f334-137">Étape 2 : Découvrez les port hello que vous pouvez utiliser tooremote connecter toohello ensemble d’échelle de machine virtuelle instance/nœud spécifique</span><span class="sxs-lookup"><span data-stu-id="2f334-137">Step 2: Find out hello port that you can use tooremote connect toohello specific VM Scale Set instance/node</span></span>
<span data-ttu-id="2f334-138">Plus haut dans ce document, j’ai parlé comment mappent des nœuds de toohello par les instances de hello ensemble d’échelle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2f334-138">Earlier in this document, I talked about how hello VM Scale Set instances map toohello nodes.</span></span> <span data-ttu-id="2f334-139">Nous utiliserons cette toofigure port exact de hello.</span><span class="sxs-lookup"><span data-stu-id="2f334-139">We will use that toofigure out hello exact port.</span></span>

<span data-ttu-id="2f334-140">ports de Hello sont allouées dans l’ordre croissant d’instance d’ensemble d’échelle de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="2f334-140">hello ports are allocated in ascending order of hello VM Scale Set instance.</span></span> <span data-ttu-id="2f334-141">Par conséquent, dans mon exemple pour le type de nœud de serveur frontal de hello, ports hello pour chacun des cinq instances de hello sont suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="2f334-141">so in my example for hello FrontEnd node type, hello ports for each of hello five instances are hello following.</span></span> <span data-ttu-id="2f334-142">vous maintenant toodo devez hello même mappage de votre instance de l’ensemble d’échelle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2f334-142">you now need toodo hello same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="2f334-143">**Instance de jeu de mise à l’échelle de machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="2f334-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="2f334-144">**Port**</span><span class="sxs-lookup"><span data-stu-id="2f334-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="2f334-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="2f334-145">FrontEnd_0</span></span> |<span data-ttu-id="2f334-146">3389</span><span class="sxs-lookup"><span data-stu-id="2f334-146">3389</span></span> |
| <span data-ttu-id="2f334-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="2f334-147">FrontEnd_1</span></span> |<span data-ttu-id="2f334-148">3390</span><span class="sxs-lookup"><span data-stu-id="2f334-148">3390</span></span> |
| <span data-ttu-id="2f334-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="2f334-149">FrontEnd_2</span></span> |<span data-ttu-id="2f334-150">3391</span><span class="sxs-lookup"><span data-stu-id="2f334-150">3391</span></span> |
| <span data-ttu-id="2f334-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="2f334-151">FrontEnd_3</span></span> |<span data-ttu-id="2f334-152">3392</span><span class="sxs-lookup"><span data-stu-id="2f334-152">3392</span></span> |
| <span data-ttu-id="2f334-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="2f334-153">FrontEnd_4</span></span> |<span data-ttu-id="2f334-154">3393</span><span class="sxs-lookup"><span data-stu-id="2f334-154">3393</span></span> |
| <span data-ttu-id="2f334-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="2f334-155">FrontEnd_5</span></span> |<span data-ttu-id="2f334-156">3394</span><span class="sxs-lookup"><span data-stu-id="2f334-156">3394</span></span> |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a><span data-ttu-id="2f334-157">Étape 3 : Instance d’ensemble d’échelle de machine virtuelle spécifique toohello de se connecter à distance</span><span class="sxs-lookup"><span data-stu-id="2f334-157">Step 3: Remote connect toohello specific VM Scale Set instance</span></span>
<span data-ttu-id="2f334-158">Dans la capture d’écran hello ci-dessous utiliser Connexion Bureau à distance tooconnect toohello FrontEnd_1 :</span><span class="sxs-lookup"><span data-stu-id="2f334-158">In hello screenshot below I use Remote Desktop Connection tooconnect toohello FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a><span data-ttu-id="2f334-160">Comment les valeurs de plage de toochange hello port RDP</span><span class="sxs-lookup"><span data-stu-id="2f334-160">How toochange hello RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="2f334-161">Avant le déploiement du cluster</span><span class="sxs-lookup"><span data-stu-id="2f334-161">Before cluster deployment</span></span>
<span data-ttu-id="2f334-162">Lorsque vous configurez un cluster hello à l’aide d’un modèle de gestionnaire de ressources, vous pouvez spécifier la plage de hello Bonjour **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="2f334-162">When you are setting up hello cluster using an Resource Manager template, you can specify hello range in hello **inboundNatPools**.</span></span>

<span data-ttu-id="2f334-163">Obtenir la définition de ressource toohello **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="2f334-163">Go toohello resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="2f334-164">Sous que vous recherchez description hello pour **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="2f334-164">Under that you find hello description for **inboundNatPools**.</span></span>  <span data-ttu-id="2f334-165">Remplacez hello *frontal* et *frontal* valeurs.</span><span class="sxs-lookup"><span data-stu-id="2f334-165">Replace hello *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="2f334-167">Après le déploiement du cluster</span><span class="sxs-lookup"><span data-stu-id="2f334-167">After cluster deployment</span></span>
<span data-ttu-id="2f334-168">Cela est un peu plus complexe et peut entraîner des machines virtuelles de hello recyclés.</span><span class="sxs-lookup"><span data-stu-id="2f334-168">This is a bit more involved and may result in hello VMs getting recycled.</span></span> <span data-ttu-id="2f334-169">Vous avez maintenant tooset nouvelles valeurs à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f334-169">You will now have tooset new values using Azure PowerShell.</span></span> <span data-ttu-id="2f334-170">Vérifiez qu’Azure PowerShell 1.0 ou version ultérieure est installé sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2f334-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="2f334-171">Si vous n’avez pas fait avant, je vous recommande vivement que vous suivez hello étapes [comment tooinstall et configurer Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="2f334-171">If you have not done this before, I strongly suggest that you follow hello steps outlined in [How tooinstall and configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="2f334-172">Se connecter tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="2f334-172">Sign in tooyour Azure account.</span></span> <span data-ttu-id="2f334-173">Si cette commande PowerShell échoue pour une raison quelconque, vous devez vérifier si Azure PowerShell est correctement installé.</span><span class="sxs-lookup"><span data-stu-id="2f334-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="2f334-174">Exécutez hello suivant détaille tooget de votre équilibreur de charge et vous pouvez voir description hello pour les valeurs hello **inboundNatPools**:</span><span class="sxs-lookup"><span data-stu-id="2f334-174">Run hello following tooget details on your load balancer and you see hello values for hello description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="2f334-175">À présent définir *frontal* et *frontal* toohello les valeurs souhaitées.</span><span class="sxs-lookup"><span data-stu-id="2f334-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* toohello values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="2f334-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2f334-176">Next steps</span></span>
* [<span data-ttu-id="2f334-177">Vue d’ensemble de la fonctionnalité de « Déployer n’importe où » hello et une comparaison avec des clusters de géré Azure</span><span class="sxs-lookup"><span data-stu-id="2f334-177">Overview of hello "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="2f334-178">Sécurité des clusters</span><span class="sxs-lookup"><span data-stu-id="2f334-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="2f334-179"> Kit de développement logiciel (SDK) de Service Fabric et prise en main</span><span class="sxs-lookup"><span data-stu-id="2f334-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
