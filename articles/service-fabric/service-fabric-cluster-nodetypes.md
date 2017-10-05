---
title: "Types de nœuds Service Fabric et groupes de machines virtuelles identiques | Microsoft Docs"
description: "Décrit la relation entre les types de nœuds Service Fabric et les groupes de machines virtuelles identiques et la connexion à distance à une instance de groupe de machines virtuelles identiques ou à un nœud de cluster."
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
ms.openlocfilehash: 3b1a22bb3653abb68fc73645ad2cb623fabc7736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="the-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="78787-103">Relation entre les types de nœuds Service Fabric et les groupes de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="78787-103">The relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="78787-104">Les groupes de machines virtuelles identiques sont des ressources de calcul Azure que vous pouvez utiliser pour déployer et gérer une collection de machines virtuelles en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="78787-104">Virtual Machine Scale Sets are an Azure Compute resource you can use to deploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="78787-105">Chaque type de nœud qui est défini dans un cluster Service Fabric est configuré en tant que jeu de mise à l’échelle de machine virtuelle distinct.</span><span class="sxs-lookup"><span data-stu-id="78787-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="78787-106">Chaque type de nœud peut ensuite faire l’objet d’une montée ou descente en puissance de manière indépendante, avoir différents jeux de ports ouverts et présenter différentes métriques de capacité.</span><span class="sxs-lookup"><span data-stu-id="78787-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="78787-107">La capture d’écran suivante montre un cluster qui a deux types de nœuds : frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="78787-107">The following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="78787-108">Chaque type de nœud comporte cinq nœuds.</span><span class="sxs-lookup"><span data-stu-id="78787-108">Each node type has five nodes each.</span></span>

![Capture d’écran d’un cluster qui a deux types de nœuds][NodeTypes]

## <a name="mapping-vm-scale-set-instances-to-nodes"></a><span data-ttu-id="78787-110">Mappage des instances du groupe de machines virtuelles identiques sur les nœuds</span><span class="sxs-lookup"><span data-stu-id="78787-110">Mapping VM Scale Set instances to nodes</span></span>
<span data-ttu-id="78787-111">Comme vous pouvez le constater ci-dessus, les instances du groupe de machines virtuelles identiques démarrent à l’instance 0.</span><span class="sxs-lookup"><span data-stu-id="78787-111">As you can see above, the VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="78787-112">Les noms reflètent la numérotation.</span><span class="sxs-lookup"><span data-stu-id="78787-112">The numbering is reflected in the names.</span></span> <span data-ttu-id="78787-113">Par exemple, BackEnd_0 représente l’instance 0 du groupe principal de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="78787-113">For example, BackEnd_0 is instance 0 of the BackEnd VM Scale Set.</span></span> <span data-ttu-id="78787-114">Ce groupe a cinq instances, nommées BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 et BackEnd_4.</span><span class="sxs-lookup"><span data-stu-id="78787-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="78787-115">Quand vous effectuez une montée en puissance sur un groupe de machines virtuelles identiques, une instance est créée.</span><span class="sxs-lookup"><span data-stu-id="78787-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="78787-116">En règle générale, le nom de la nouvelle instance du groupe de machines virtuelles identiques est le nom du groupe de machines virtuelles identiques suivi du numéro d’instance suivant.</span><span class="sxs-lookup"><span data-stu-id="78787-116">The new VM Scale Set instance name will typically be the VM Scale Set name + the next instance number.</span></span> <span data-ttu-id="78787-117">Dans notre exemple, il s’agit de BackEnd_5.</span><span class="sxs-lookup"><span data-stu-id="78787-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-to-each-node-typevm-scale-set"></a><span data-ttu-id="78787-118">Mappage des équilibreurs de charge de groupe de machines virtuelles identiques sur chaque type de nœud/groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="78787-118">Mapping VM scale set load balancers to each node type/VM Scale Set</span></span>
<span data-ttu-id="78787-119">Si vous avez déployé votre cluster à partir du portail ou que vous avez utilisé l’exemple de modèle Resource Manager fourni, les équilibreurs de charge pour chaque type de nœud ou jeu de mise à l’échelle de machine virtuelle apparaissent quand vous obtenez la liste de toutes les ressources sous un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="78787-119">If you have deployed your cluster from the portal or have used the sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see the load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="78787-120">Le nom ressemble à ceci : **LB-&lt;NodeType name&gt;**.</span><span class="sxs-lookup"><span data-stu-id="78787-120">The name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="78787-121">Par exemple, LB-sfcluster4doc-0, comme indiqué dans cette capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="78787-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![Ressources][Resources]

## <a name="remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="78787-123">Se connecter à distance à une instance du groupe de machines virtuelles identiques ou à un nœud de cluster</span><span class="sxs-lookup"><span data-stu-id="78787-123">Remote connect to a VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="78787-124">Chaque type de nœud qui est défini dans un cluster est configuré comme un jeu de mise à l’échelle de machine virtuelle distinct.</span><span class="sxs-lookup"><span data-stu-id="78787-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="78787-125">Cela signifie que les types de nœuds peuvent subir une montée ou descente en puissance de manière indépendante et comprendre différentes références (SKU) de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="78787-125">That means the node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="78787-126">Contrairement aux machines virtuelles à instance unique, les instances du groupe de machines virtuelles identiques n’obtiennent pas une adresse IP virtuelle qui leur est propre.</span><span class="sxs-lookup"><span data-stu-id="78787-126">Unlike single instance VMs, the VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="78787-127">C’est pourquoi rechercher une adresse IP et un port pour se connecter à distance à une instance spécifique peut s’avérer un peu difficile.</span><span class="sxs-lookup"><span data-stu-id="78787-127">So it can be a bit challenging when you are looking for an IP address and port that you can use to remote connect to a specific instance.</span></span>

<span data-ttu-id="78787-128">Voici la procédure à suivre pour les trouver.</span><span class="sxs-lookup"><span data-stu-id="78787-128">Here are the steps you can follow to discover them.</span></span>

### <a name="step-1-find-out-the-virtual-ip-address-for-the-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="78787-129">Étape 1 : Rechercher l’adresse IP virtuelle du type de nœud, puis les règles NAT de trafic entrant pour RDP</span><span class="sxs-lookup"><span data-stu-id="78787-129">Step 1: Find out the virtual IP address for the node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="78787-130">Pour ce faire, vous devez obtenir les valeurs des règles NAT de trafic entrant qui ont été établies dans le cadre de la définition des ressources pour **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="78787-130">In order to get that, you need to get the inbound NAT rules values that were defined as a part of the resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="78787-131">Dans le portail, accédez au panneau Équilibrage de charge, puis à **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="78787-131">In the portal, navigate to the Load balancer blade and then **Settings**.</span></span>

![Panneau Équilibrage de charge][LBBlade]

<span data-ttu-id="78787-133">Dans **Paramètres**, cliquez sur **Règles NAT de trafic entrant**.</span><span class="sxs-lookup"><span data-stu-id="78787-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="78787-134">Vous disposez à présent de l’adresse IP et du port nécessaires pour vous connecter à distance à la première instance du groupe de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="78787-134">This now gives you the IP address and port that you can use to remote connect to the first VM Scale Set instance.</span></span> <span data-ttu-id="78787-135">Dans la capture d’écran ci-dessous, il s’agit de **104.42.106.156** et **3389**</span><span class="sxs-lookup"><span data-stu-id="78787-135">In the screenshot below, it is **104.42.106.156** and **3389**</span></span>

![Règles NAT][NATRules]

### <a name="step-2-find-out-the-port-that-you-can-use-to-remote-connect-to-the-specific-vm-scale-set-instancenode"></a><span data-ttu-id="78787-137">Étape 2 : Déterminer le port à utiliser pour se connecter à distance à un nœud ou à une instance du groupe de machines virtuelles identiques spécifique</span><span class="sxs-lookup"><span data-stu-id="78787-137">Step 2: Find out the port that you can use to remote connect to the specific VM Scale Set instance/node</span></span>
<span data-ttu-id="78787-138">Plus haut dans ce document, j’ai abordé le mappage des instances du groupe de machines virtuelles identiques sur les nœuds.</span><span class="sxs-lookup"><span data-stu-id="78787-138">Earlier in this document, I talked about how the VM Scale Set instances map to the nodes.</span></span> <span data-ttu-id="78787-139">Nous allons l’utiliser pour déterminer le port exact.</span><span class="sxs-lookup"><span data-stu-id="78787-139">We will use that to figure out the exact port.</span></span>

<span data-ttu-id="78787-140">Les ports sont alloués dans l’ordre croissant des instances du jeu de mise à l’échelle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="78787-140">The ports are allocated in ascending order of the VM Scale Set instance.</span></span> <span data-ttu-id="78787-141">Ainsi, dans mon exemple, pour le type de nœud frontal, les ports pour chacune des cinq instances sont les suivants.</span><span class="sxs-lookup"><span data-stu-id="78787-141">so in my example for the FrontEnd node type, the ports for each of the five instances are the following.</span></span> <span data-ttu-id="78787-142">Vous devez maintenant effectuer le même mappage pour votre instance de jeu de mise à l’échelle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="78787-142">you now need to do the same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="78787-143">**Instance de jeu de mise à l’échelle de machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="78787-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="78787-144">**Port**</span><span class="sxs-lookup"><span data-stu-id="78787-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="78787-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="78787-145">FrontEnd_0</span></span> |<span data-ttu-id="78787-146">3389</span><span class="sxs-lookup"><span data-stu-id="78787-146">3389</span></span> |
| <span data-ttu-id="78787-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="78787-147">FrontEnd_1</span></span> |<span data-ttu-id="78787-148">3390</span><span class="sxs-lookup"><span data-stu-id="78787-148">3390</span></span> |
| <span data-ttu-id="78787-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="78787-149">FrontEnd_2</span></span> |<span data-ttu-id="78787-150">3391</span><span class="sxs-lookup"><span data-stu-id="78787-150">3391</span></span> |
| <span data-ttu-id="78787-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="78787-151">FrontEnd_3</span></span> |<span data-ttu-id="78787-152">3392</span><span class="sxs-lookup"><span data-stu-id="78787-152">3392</span></span> |
| <span data-ttu-id="78787-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="78787-153">FrontEnd_4</span></span> |<span data-ttu-id="78787-154">3393</span><span class="sxs-lookup"><span data-stu-id="78787-154">3393</span></span> |
| <span data-ttu-id="78787-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="78787-155">FrontEnd_5</span></span> |<span data-ttu-id="78787-156">3394</span><span class="sxs-lookup"><span data-stu-id="78787-156">3394</span></span> |

### <a name="step-3-remote-connect-to-the-specific-vm-scale-set-instance"></a><span data-ttu-id="78787-157">Étape 3 : Se connecter à distance à une instance spécifique du groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="78787-157">Step 3: Remote connect to the specific VM Scale Set instance</span></span>
<span data-ttu-id="78787-158">Dans la capture d’écran ci-dessous, j’utilise Connexion Bureau à distance pour me connecter à l’instance FrontEnd_1 :</span><span class="sxs-lookup"><span data-stu-id="78787-158">In the screenshot below I use Remote Desktop Connection to connect to the FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-to-change-the-rdp-port-range-values"></a><span data-ttu-id="78787-160">Comment modifier les valeurs des plages de ports RDP</span><span class="sxs-lookup"><span data-stu-id="78787-160">How to change the RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="78787-161">Avant le déploiement du cluster</span><span class="sxs-lookup"><span data-stu-id="78787-161">Before cluster deployment</span></span>
<span data-ttu-id="78787-162">Quand vous configurez le cluster à l’aide d’un modèle Resource Manager, vous pouvez spécifier la plage dans **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="78787-162">When you are setting up the cluster using an Resource Manager template, you can specify the range in the **inboundNatPools**.</span></span>

<span data-ttu-id="78787-163">Accédez à la définition de ressource pour **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="78787-163">Go to the resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="78787-164">Sous celle-ci se trouve la description de **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="78787-164">Under that you find the description for **inboundNatPools**.</span></span>  <span data-ttu-id="78787-165">Remplacez les valeurs *frontendPortRangeStart* et *frontendPortRangeEnd*.</span><span class="sxs-lookup"><span data-stu-id="78787-165">Replace the *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="78787-167">Après le déploiement du cluster</span><span class="sxs-lookup"><span data-stu-id="78787-167">After cluster deployment</span></span>
<span data-ttu-id="78787-168">Cette procédure est un peu plus complexe et peut aboutir au recyclage des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="78787-168">This is a bit more involved and may result in the VMs getting recycled.</span></span> <span data-ttu-id="78787-169">Vous devez maintenant définir de nouvelles valeurs à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78787-169">You will now have to set new values using Azure PowerShell.</span></span> <span data-ttu-id="78787-170">Vérifiez qu’Azure PowerShell 1.0 ou version ultérieure est installé sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="78787-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="78787-171">Si ce n’est déjà fait, je vous recommande vivement de suivre les étapes décrites dans [Installation et configuration d’Azure PowerShell](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="78787-171">If you have not done this before, I strongly suggest that you follow the steps outlined in [How to install and configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="78787-172">Connectez-vous à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="78787-172">Sign in to your Azure account.</span></span> <span data-ttu-id="78787-173">Si cette commande PowerShell échoue pour une raison quelconque, vous devez vérifier si Azure PowerShell est correctement installé.</span><span class="sxs-lookup"><span data-stu-id="78787-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="78787-174">Exécutez la commande suivante pour obtenir les détails de votre équilibrage de charge et découvrir les valeurs qui décrivent **inboundNatPools**:</span><span class="sxs-lookup"><span data-stu-id="78787-174">Run the following to get details on your load balancer and you see the values for the description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="78787-175">À présent, définissez *frontendPortRangeEnd* et *frontendPortRangeStart* sur les valeurs souhaitées.</span><span class="sxs-lookup"><span data-stu-id="78787-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* to the values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use the API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="78787-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="78787-176">Next steps</span></span>
* [<span data-ttu-id="78787-177">Vue d’ensemble de la fonction « Déployer n’importe où » et comparaison avec les clusters gérés par Azure</span><span class="sxs-lookup"><span data-stu-id="78787-177">Overview of the "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="78787-178">Sécurité des clusters</span><span class="sxs-lookup"><span data-stu-id="78787-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="78787-179"> Kit de développement logiciel (SDK) de Service Fabric et prise en main</span><span class="sxs-lookup"><span data-stu-id="78787-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
