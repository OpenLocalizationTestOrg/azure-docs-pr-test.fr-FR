---
title: "Ajouter ou supprimer des nœuds d’un cluster Service Fabric autonome | Microsoft Docs"
description: "Apprenez à ajouter ou supprimer des nœuds d’un cluster Azure Service Fabric sur une machine physique ou virtuelle sous Windows Server, qu’elle soit locale ou dans un cloud."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 9c6035e97de38ff63ef074109afd9f3c7484f828
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="add-or-remove-nodes-to-a-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="84acd-103">Ajouter ou supprimer des nœuds d’un cluster Service Fabric autonome sous Windows Server</span><span class="sxs-lookup"><span data-stu-id="84acd-103">Add or remove nodes to a standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="84acd-104">Une fois que vous avez [créé votre cluster Service Fabric autonome sur des ordinateurs Windows Server](service-fabric-cluster-creation-for-windows-server.md), les besoins de votre entreprise peuvent évoluer et vous devrez peut-être ajouter ou supprimer des nœuds de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="84acd-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change and you might need to add or remove nodes to your cluster.</span></span> <span data-ttu-id="84acd-105">Cet article fournit des étapes détaillées pour effectuer ces tâches.</span><span class="sxs-lookup"><span data-stu-id="84acd-105">This article provides detailed steps to achieve this.</span></span> <span data-ttu-id="84acd-106">Veuillez noter que la fonctionnalité d’ajout/suppression de nœud n’est pas prise en charge dans les clusters de développement locaux.</span><span class="sxs-lookup"><span data-stu-id="84acd-106">Please note that add/remove node functionality is not supported in local development clusters.</span></span>

## <a name="add-nodes-to-your-cluster"></a><span data-ttu-id="84acd-107">Ajouter des nœuds à votre cluster</span><span class="sxs-lookup"><span data-stu-id="84acd-107">Add nodes to your cluster</span></span>
1. <span data-ttu-id="84acd-108">Préparez la machine virtuelle/l’ordinateur que vous souhaitez ajouter à votre cluster en suivant les étapes présentées dans la section [Préparer les machines à la configuration requise pour le déploiement de cluster](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="84acd-108">Prepare the VM/machine you want to add to your cluster by following the steps mentioned in the [Prepare the machines to meet the prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section</span></span>
2. <span data-ttu-id="84acd-109">Identifiez le domaine d’erreur et le domaine de mise à niveau auxquels vous allez ajouter cette machine virtuelle ou cet ordinateur.</span><span class="sxs-lookup"><span data-stu-id="84acd-109">Identify which fault domain and upgrade domain you are going to add this VM/machine to</span></span>
3. <span data-ttu-id="84acd-110">Avec Bureau à distance (RDP), accédez à la machine virtuelle ou à l’ordinateur que vous souhaitez ajouter au cluster.</span><span class="sxs-lookup"><span data-stu-id="84acd-110">Remote desktop (RDP) into the VM/machine that you want to add to the cluster</span></span>
4. <span data-ttu-id="84acd-111">Copiez ou [téléchargez le package autonome Service Fabric pour Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) sur cette machine virtuelle ou cet ordinateur et décompressez le package.</span><span class="sxs-lookup"><span data-stu-id="84acd-111">Copy or [download the standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) to the VM/machine and unzip the package</span></span>
5. <span data-ttu-id="84acd-112">Exécutez PowerShell avec des privilèges élevés, puis naviguez jusqu’à l’emplacement du package décompressé.</span><span class="sxs-lookup"><span data-stu-id="84acd-112">Run Powershell with elevated privileges, and navigate to the location of the unzipped package</span></span>
6. <span data-ttu-id="84acd-113">Exécutez le script *AddNode.ps1* avec les paramètres qui décrivent le nouveau nœud à ajouter.</span><span class="sxs-lookup"><span data-stu-id="84acd-113">Run the *AddNode.ps1* script with the parameters describing the new node to add.</span></span> <span data-ttu-id="84acd-114">L’exemple ci-dessous ajoute un nouveau nœud nommé VM5, de type NodeType0, avec l’adresse IP 182.17.34.52, à UD1 et fd:/dc1/r0.</span><span class="sxs-lookup"><span data-stu-id="84acd-114">The example below adds a new node called VM5, with type NodeType0 and IP address 182.17.34.52, into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="84acd-115">*ExistingClusterConnectionEndPoint* est un point de terminaison de connexion pour un nœud déjà présent dans le cluster existant. Il peut s’agir de l’adresse IP de *n’importe quel nœud* du cluster.</span><span class="sxs-lookup"><span data-stu-id="84acd-115">The *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in the existing cluster, which can be the IP address of *any* node in the cluster.</span></span>

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    <span data-ttu-id="84acd-116">Une fois le script exécuté, vous pouvez vérifier si le nouveau nœud a été ajouté en exécutant la cmdlet [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="84acd-116">Once the script finishes running, you can check if the new node has been added by running the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span></span>

7. <span data-ttu-id="84acd-117">Pour garantir la cohérence entre les différents nœuds du cluster, vous devez lancer une mise à niveau de la configuration.</span><span class="sxs-lookup"><span data-stu-id="84acd-117">To ensure consistency across different nodes in the cluster, you must initiate a configuration upgrade.</span></span> <span data-ttu-id="84acd-118">Exécutez [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) pour obtenir le dernier fichier de configuration, et ajoutez le nœud nouvellement ajouté à la section « Nodes ».</span><span class="sxs-lookup"><span data-stu-id="84acd-118">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) to get the latest configuration file and add the newly added node to "Nodes" section.</span></span> <span data-ttu-id="84acd-119">Il est également recommandé de disposer en permanence de la dernière configuration de cluster disponible au cas où vous devriez redéployer un cluster avec la même configuration.</span><span class="sxs-lookup"><span data-stu-id="84acd-119">It is also recommended to always have the latest cluster configuration available in the case that you need to redploy a cluster with the same configuration.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. <span data-ttu-id="84acd-120">Exécutez [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) pour commencer la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="84acd-120">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

    ```
    <span data-ttu-id="84acd-121">Vous pouvez surveiller la progression de la mise à niveau avec Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="84acd-121">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="84acd-122">Vous pouvez également exécuter [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps) pour cela.</span><span class="sxs-lookup"><span data-stu-id="84acd-122">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-nodes-to-clusters-configured-with-windows-security-using-gmsa"></a><span data-ttu-id="84acd-123">Ajouter des nœuds aux clusters configurés avec la sécurité Windows à l’aide de gMSA</span><span class="sxs-lookup"><span data-stu-id="84acd-123">Add nodes to clusters configured with Windows Security using gMSA</span></span>
<span data-ttu-id="84acd-124">Pour les clusters configurés avec un compte de service géré de groupe (gMSA, Group Managed Service Account) (https://technet.microsoft.com/library/hh831782.aspx), un nouveau nœud peut être ajouté à l’aide d’une mise à niveau de la configuration :</span><span class="sxs-lookup"><span data-stu-id="84acd-124">For clusters configured with Group Managed Service Account(gMSA)(https://technet.microsoft.com/library/hh831782.aspx), a new node can be added using a configuration upgrade:</span></span>
1. <span data-ttu-id="84acd-125">Exécutez [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) sur l’un des nœuds existants pour obtenir le dernier fichier de configuration, et ajoutez des détails sur le nouveau nœud à ajouter dans la section « Nodes ».</span><span class="sxs-lookup"><span data-stu-id="84acd-125">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) on any of the existing nodes to get the latest configuration file and add details about the new node you want to add in the "Nodes" section.</span></span> <span data-ttu-id="84acd-126">Assurez-vous que le nouveau nœud fait partie du même compte géré de groupe.</span><span class="sxs-lookup"><span data-stu-id="84acd-126">Make sure the new node is part of the same group managed account.</span></span> <span data-ttu-id="84acd-127">Ce compte doit être un compte Administrateur sur tous les ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="84acd-127">This account should be an Administrator on all machines.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. <span data-ttu-id="84acd-128">Exécutez [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) pour commencer la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="84acd-128">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>
    ```
    <span data-ttu-id="84acd-129">Vous pouvez surveiller la progression de la mise à niveau avec Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="84acd-129">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="84acd-130">Vous pouvez également exécuter [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps) pour cela.</span><span class="sxs-lookup"><span data-stu-id="84acd-130">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-node-types-to-your-cluster"></a><span data-ttu-id="84acd-131">Ajouter des types de nœuds à votre cluster</span><span class="sxs-lookup"><span data-stu-id="84acd-131">Add node types to your cluster</span></span>
<span data-ttu-id="84acd-132">Pour ajouter un nouveau type de nœud, modifiez votre configuration afin de l’inclure dans la section « NodeTypes », sous « Properties », puis commencez une mise à niveau de la configuration à l’aide de [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="84acd-132">In order to add a new node type, modify your configuration to include the new node type in "NodeTypes" section under "Properties" and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span> <span data-ttu-id="84acd-133">Une fois la mise à niveau effectuée, vous pouvez ajouter de nouveaux nœuds à votre cluster avec ce type de nœud.</span><span class="sxs-lookup"><span data-stu-id="84acd-133">Once the upgrade completes, you can add new nodes to your cluster with this node type.</span></span>

## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="84acd-134">Supprimer des nœuds de votre cluster</span><span class="sxs-lookup"><span data-stu-id="84acd-134">Remove nodes from your cluster</span></span>
<span data-ttu-id="84acd-135">Pour supprimer un nœud d’un cluster à l’aide d’une mise à niveau de la configuration, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="84acd-135">A node can be removed from a cluster using a configuration upgrade, in the following manner:</span></span>

1. <span data-ttu-id="84acd-136">Exécutez [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) pour obtenir le dernier fichier de configuration et *supprimez* le nœud de la section « Nodes ».</span><span class="sxs-lookup"><span data-stu-id="84acd-136">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) to get the latest configuration file and *remove* the node from "Nodes" section.</span></span>
<span data-ttu-id="84acd-137">Ajoutez le paramètre « NodesToBeRemoved » à la section « Setup », dans la section « FabricSettings ».</span><span class="sxs-lookup"><span data-stu-id="84acd-137">Add the "NodesToBeRemoved" parameter to "Setup" section inside "FabricSettings" section.</span></span> <span data-ttu-id="84acd-138">La valeur indiquée sous « value » doit être une liste des noms des nœuds à supprimer, séparés par des virgules.</span><span class="sxs-lookup"><span data-stu-id="84acd-138">The "value" should be a comma separated list of node names of nodes that need to be removed.</span></span>

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. <span data-ttu-id="84acd-139">Exécutez [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) pour commencer la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="84acd-139">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) to begin the upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path to Configuration File>

    ```
    <span data-ttu-id="84acd-140">Vous pouvez surveiller la progression de la mise à niveau avec Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="84acd-140">You can monitor the progress of the upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="84acd-141">Vous pouvez également exécuter [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps) pour cela.</span><span class="sxs-lookup"><span data-stu-id="84acd-141">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

> [!NOTE]
> <span data-ttu-id="84acd-142">La suppression de nœuds peut entraîner plusieurs mises à niveau.</span><span class="sxs-lookup"><span data-stu-id="84acd-142">Removal of nodes may initiate multiple upgrades.</span></span> <span data-ttu-id="84acd-143">Certains nœuds sont marqués avec la balise `IsSeedNode=”true”` et peuvent être identifiés en interrogeant le manifeste de cluster à l’aide de `Get-ServiceFabricClusterManifest`.</span><span class="sxs-lookup"><span data-stu-id="84acd-143">Some nodes are marked with `IsSeedNode=”true”` tag and can be identified by querying the cluster manifest using `Get-ServiceFabricClusterManifest`.</span></span> <span data-ttu-id="84acd-144">La suppression de ces nœuds peut prendre plus de temps car, dans ce cas, les nœuds initiaux devront être déplacés.</span><span class="sxs-lookup"><span data-stu-id="84acd-144">Removal of such nodes may take longer than others since the seed nodes will have to be moved around in such scenarios.</span></span> <span data-ttu-id="84acd-145">Le cluster doit conserver au moins 3 nœuds de type nœud principal.</span><span class="sxs-lookup"><span data-stu-id="84acd-145">The cluster must maintain a minimum of 3 primary node type nodes.</span></span>
> 
> 

### <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="84acd-146">Supprimer des types de nœuds de votre cluster</span><span class="sxs-lookup"><span data-stu-id="84acd-146">Remove node types from your cluster</span></span>
<span data-ttu-id="84acd-147">Avant de supprimer un type de nœud, vérifiez s’il existe des nœuds qui référencent le type de nœud concerné.</span><span class="sxs-lookup"><span data-stu-id="84acd-147">Before removing a node type, please double check if there are any nodes referencing the node type.</span></span> <span data-ttu-id="84acd-148">Supprimez ces nœuds avant de supprimer le type de nœud correspondant.</span><span class="sxs-lookup"><span data-stu-id="84acd-148">Remove these nodes before removing the corresponding node type.</span></span> <span data-ttu-id="84acd-149">Une fois que tous les nœuds correspondants sont supprimés, vous pouvez supprimer le NodeType de la configuration du cluster et commencer une mise à niveau de la configuration à l’aide de [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="84acd-149">Once all corresponding nodes are removed, you can remove the NodeType from the cluster configuration and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span>


### <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="84acd-150">Remplacer les nœuds principaux de votre cluster</span><span class="sxs-lookup"><span data-stu-id="84acd-150">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="84acd-151">Le remplacement des nœuds principaux doit être effectué un nœud à la fois, au lieu de supprimer, puis d’ajouter des nœuds par lots.</span><span class="sxs-lookup"><span data-stu-id="84acd-151">The replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="84acd-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="84acd-152">Next steps</span></span>
* [<span data-ttu-id="84acd-153">Paramètres de configuration pour un cluster Windows autonome</span><span class="sxs-lookup"><span data-stu-id="84acd-153">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="84acd-154">Sécuriser un cluster autonome sur Windows à l’aide de certificats X509</span><span class="sxs-lookup"><span data-stu-id="84acd-154">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="84acd-155">Créer un cluster Service Fabric autonome avec des machines virtuelles Azure Windows</span><span class="sxs-lookup"><span data-stu-id="84acd-155">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

