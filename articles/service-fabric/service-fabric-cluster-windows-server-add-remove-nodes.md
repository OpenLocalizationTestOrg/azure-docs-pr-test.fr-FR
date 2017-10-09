---
title: "cluster nœuds tooa autonome Service Fabric aaaAdd ou supprimez | Documents Microsoft"
description: "Découvrez comment tooadd ou supprimez tooan de nœuds Azure Service Fabric de cluster sur un ordinateur physique ou virtuel exécutant Windows Server, qui peut être local ou dans n’importe quel cloud."
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
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="6e862-103">Ajouter ou supprimer le cluster Service Fabric nœuds tooa autonome sont en cours d’exécution sur Windows Server</span><span class="sxs-lookup"><span data-stu-id="6e862-103">Add or remove nodes tooa standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="6e862-104">Une fois que vous avez [créé votre cluster de Service Fabric autonomes sur les ordinateurs Windows Server](service-fabric-cluster-creation-for-windows-server.md), les besoins de votre entreprise peuvent changer et que vous deviez tooadd ou supprimer le cluster tooyour de nœuds.</span><span class="sxs-lookup"><span data-stu-id="6e862-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change and you might need tooadd or remove nodes tooyour cluster.</span></span> <span data-ttu-id="6e862-105">Cet article fournit des instructions détaillées tooachieve cela.</span><span class="sxs-lookup"><span data-stu-id="6e862-105">This article provides detailed steps tooachieve this.</span></span> <span data-ttu-id="6e862-106">Veuillez noter que la fonctionnalité d’ajout/suppression de nœud n’est pas prise en charge dans les clusters de développement locaux.</span><span class="sxs-lookup"><span data-stu-id="6e862-106">Please note that add/remove node functionality is not supported in local development clusters.</span></span>

## <a name="add-nodes-tooyour-cluster"></a><span data-ttu-id="6e862-107">Ajouter tooyour nœuds du cluster</span><span class="sxs-lookup"><span data-stu-id="6e862-107">Add nodes tooyour cluster</span></span>
1. <span data-ttu-id="6e862-108">Préparation hello VM/machine à tooadd tooyour cluster en suivant les étapes de hello mentionnés dans hello [hello de préparer les ordinateurs toomeet conditions préalables de hello pour le déploiement de cluster](service-fabric-cluster-creation-for-windows-server.md) section</span><span class="sxs-lookup"><span data-stu-id="6e862-108">Prepare hello VM/machine you want tooadd tooyour cluster by following hello steps mentioned in hello [Prepare hello machines toomeet hello prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section</span></span>
2. <span data-ttu-id="6e862-109">Identifier les domaine d’erreur et la mise à niveau domaine vous tooadd du cours de cet ordinateur virtuel/ordinateur</span><span class="sxs-lookup"><span data-stu-id="6e862-109">Identify which fault domain and upgrade domain you are going tooadd this VM/machine to</span></span>
3. <span data-ttu-id="6e862-110">Bureau à distance (RDP) dans hello VM/machine que vous souhaitez tooadd toohello cluster</span><span class="sxs-lookup"><span data-stu-id="6e862-110">Remote desktop (RDP) into hello VM/machine that you want tooadd toohello cluster</span></span>
4. <span data-ttu-id="6e862-111">Copie ou [télécharger le package autonome de hello pour Service Fabric pour Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/machine et décompressez le package de hello</span><span class="sxs-lookup"><span data-stu-id="6e862-111">Copy or [download hello standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/machine and unzip hello package</span></span>
5. <span data-ttu-id="6e862-112">Exécuter Powershell avec des privilèges élevés et naviguer toohello l’emplacement du package décompressé de hello</span><span class="sxs-lookup"><span data-stu-id="6e862-112">Run Powershell with elevated privileges, and navigate toohello location of hello unzipped package</span></span>
6. <span data-ttu-id="6e862-113">Exécutez hello *AddNode.ps1* script avec les paramètres de hello décrivant hello nouveau nœud tooadd.</span><span class="sxs-lookup"><span data-stu-id="6e862-113">Run hello *AddNode.ps1* script with hello parameters describing hello new node tooadd.</span></span> <span data-ttu-id="6e862-114">exemple Hello ci-dessous ajoute un nouveau nœud appelé VM5, avec le type NodeType0 et une adresse IP 182.17.34.52, UD1 et fd : / dc1/r0.</span><span class="sxs-lookup"><span data-stu-id="6e862-114">hello example below adds a new node called VM5, with type NodeType0 and IP address 182.17.34.52, into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="6e862-115">Hello *ExistingClusterConnectionEndPoint* est déjà un point de terminaison de connexion pour un nœud de cluster existant de hello, qui peut être adresse IP hello *tout* nœud hello cluster.</span><span class="sxs-lookup"><span data-stu-id="6e862-115">hello *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in hello existing cluster, which can be hello IP address of *any* node in hello cluster.</span></span>

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    <span data-ttu-id="6e862-116">Une fois le script de hello terminée, vous pouvez vérifier si le nouveau nœud de hello a été ajoutée en exécutant hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="6e862-116">Once hello script finishes running, you can check if hello new node has been added by running hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span></span>

7. <span data-ttu-id="6e862-117">cohérence tooensure sur différents nœuds dans un cluster de hello, vous devez lancer une mise à niveau de la configuration.</span><span class="sxs-lookup"><span data-stu-id="6e862-117">tooensure consistency across different nodes in hello cluster, you must initiate a configuration upgrade.</span></span> <span data-ttu-id="6e862-118">Exécutez [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello du dernier fichier de configuration et ajoutez hello nouvellement ajoutés nœud trop section « Nœuds ».</span><span class="sxs-lookup"><span data-stu-id="6e862-118">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and add hello newly added node too"Nodes" section.</span></span> <span data-ttu-id="6e862-119">Il est également recommandé tooalways hello cluster configuration la plus récente disponible dans les cas de hello que vous avez besoin de tooredploy un cluster avec hello même configuration.</span><span class="sxs-lookup"><span data-stu-id="6e862-119">It is also recommended tooalways have hello latest cluster configuration available in hello case that you need tooredploy a cluster with hello same configuration.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. <span data-ttu-id="6e862-120">Exécutez [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) mise à niveau de toobegin hello.</span><span class="sxs-lookup"><span data-stu-id="6e862-120">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="6e862-121">Vous pouvez surveiller la progression de hello de mise à niveau de hello sur Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="6e862-121">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="6e862-122">Vous pouvez également exécuter [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps) pour cela.</span><span class="sxs-lookup"><span data-stu-id="6e862-122">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a><span data-ttu-id="6e862-123">Ajouter des nœuds tooclusters configuré avec la sécurité de Windows à l’aide de service administré de groupe</span><span class="sxs-lookup"><span data-stu-id="6e862-123">Add nodes tooclusters configured with Windows Security using gMSA</span></span>
<span data-ttu-id="6e862-124">Pour les clusters configurés avec un compte de service géré de groupe (gMSA, Group Managed Service Account) (https://technet.microsoft.com/library/hh831782.aspx), un nouveau nœud peut être ajouté à l’aide d’une mise à niveau de la configuration :</span><span class="sxs-lookup"><span data-stu-id="6e862-124">For clusters configured with Group Managed Service Account(gMSA)(https://technet.microsoft.com/library/hh831782.aspx), a new node can be added using a configuration upgrade:</span></span>
1. <span data-ttu-id="6e862-125">Exécutez [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) sur tous les nœuds existants hello tooget hello du dernier fichier de configuration et ajouter des détails sur le nouveau nœud de hello souhaité tooadd dans la section de hello « nœuds ».</span><span class="sxs-lookup"><span data-stu-id="6e862-125">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) on any of hello existing nodes tooget hello latest configuration file and add details about hello new node you want tooadd in hello "Nodes" section.</span></span> <span data-ttu-id="6e862-126">Assurez-vous que le nouveau nœud de hello fait partie de hello compte géré de groupe.</span><span class="sxs-lookup"><span data-stu-id="6e862-126">Make sure hello new node is part of hello same group managed account.</span></span> <span data-ttu-id="6e862-127">Ce compte doit être un compte Administrateur sur tous les ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="6e862-127">This account should be an Administrator on all machines.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. <span data-ttu-id="6e862-128">Exécutez [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) mise à niveau de toobegin hello.</span><span class="sxs-lookup"><span data-stu-id="6e862-128">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    <span data-ttu-id="6e862-129">Vous pouvez surveiller la progression de hello de mise à niveau de hello sur Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="6e862-129">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="6e862-130">Vous pouvez également exécuter [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps) pour cela.</span><span class="sxs-lookup"><span data-stu-id="6e862-130">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-node-types-tooyour-cluster"></a><span data-ttu-id="6e862-131">Ajouter un cluster de tooyour de types de nœud</span><span class="sxs-lookup"><span data-stu-id="6e862-131">Add node types tooyour cluster</span></span>
<span data-ttu-id="6e862-132">Commande tooadd un nouveau type de nœud, modifiez votre configuration tooinclude hello nouveau type de nœud dans la section « NodeTypes » sous « Propriétés » et commencer une configuration de mise à niveau de l’aide [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="6e862-132">In order tooadd a new node type, modify your configuration tooinclude hello new node type in "NodeTypes" section under "Properties" and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span> <span data-ttu-id="6e862-133">Une fois la mise à niveau hello terminée, vous pouvez ajouter le nouveau cluster tooyour de nœuds avec ce type de nœud.</span><span class="sxs-lookup"><span data-stu-id="6e862-133">Once hello upgrade completes, you can add new nodes tooyour cluster with this node type.</span></span>

## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="6e862-134">Supprimer des nœuds de votre cluster</span><span class="sxs-lookup"><span data-stu-id="6e862-134">Remove nodes from your cluster</span></span>
<span data-ttu-id="6e862-135">Un nœud peut être supprimé à partir d’un cluster à l’aide d’une mise à niveau de la configuration, Bonjour suivant de manière :</span><span class="sxs-lookup"><span data-stu-id="6e862-135">A node can be removed from a cluster using a configuration upgrade, in hello following manner:</span></span>

1. <span data-ttu-id="6e862-136">Exécutez [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) le fichier de configuration plus récent tooget hello et *supprimer* nœud hello à partir de la section « Nœuds ».</span><span class="sxs-lookup"><span data-stu-id="6e862-136">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and *remove* hello node from "Nodes" section.</span></span>
<span data-ttu-id="6e862-137">Ajouter hello « NodesToBeRemoved » paramètre trop » le programme d’installation « section au sein de la section de « FabricSettings ».</span><span class="sxs-lookup"><span data-stu-id="6e862-137">Add hello "NodesToBeRemoved" parameter too"Setup" section inside "FabricSettings" section.</span></span> <span data-ttu-id="6e862-138">Hello « valeur » doit être une liste séparée par des virgules des noms de nœud des nœuds qui doivent toobe supprimé.</span><span class="sxs-lookup"><span data-stu-id="6e862-138">hello "value" should be a comma separated list of node names of nodes that need toobe removed.</span></span>

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
2. <span data-ttu-id="6e862-139">Exécutez [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) mise à niveau de toobegin hello.</span><span class="sxs-lookup"><span data-stu-id="6e862-139">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="6e862-140">Vous pouvez surveiller la progression de hello de mise à niveau de hello sur Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="6e862-140">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="6e862-141">Vous pouvez également exécuter [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps) pour cela.</span><span class="sxs-lookup"><span data-stu-id="6e862-141">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

> [!NOTE]
> <span data-ttu-id="6e862-142">La suppression de nœuds peut entraîner plusieurs mises à niveau.</span><span class="sxs-lookup"><span data-stu-id="6e862-142">Removal of nodes may initiate multiple upgrades.</span></span> <span data-ttu-id="6e862-143">Certains nœuds sont marqués avec `IsSeedNode=”true”` de balise et peut être identifiée en interrogeant le cluster de hello manifeste à l’aide de `Get-ServiceFabricClusterManifest`.</span><span class="sxs-lookup"><span data-stu-id="6e862-143">Some nodes are marked with `IsSeedNode=”true”` tag and can be identified by querying hello cluster manifest using `Get-ServiceFabricClusterManifest`.</span></span> <span data-ttu-id="6e862-144">Étant donné que les nœuds de départ hello portera toobe déplacé dans de tels scénarios, la suppression de ces nœuds peut prendre plus de temps que d’autres.</span><span class="sxs-lookup"><span data-stu-id="6e862-144">Removal of such nodes may take longer than others since hello seed nodes will have toobe moved around in such scenarios.</span></span> <span data-ttu-id="6e862-145">cluster de Hello doit maintenir un minimum de 3 nœuds de type de nœud principal.</span><span class="sxs-lookup"><span data-stu-id="6e862-145">hello cluster must maintain a minimum of 3 primary node type nodes.</span></span>
> 
> 

### <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="6e862-146">Supprimer des types de nœuds de votre cluster</span><span class="sxs-lookup"><span data-stu-id="6e862-146">Remove node types from your cluster</span></span>
<span data-ttu-id="6e862-147">Avant de supprimer un type de nœud, vérifiez s’il existe des nœuds référençant le type de nœud hello.</span><span class="sxs-lookup"><span data-stu-id="6e862-147">Before removing a node type, please double check if there are any nodes referencing hello node type.</span></span> <span data-ttu-id="6e862-148">Supprimez ces nœuds avant de supprimer le type de nœud hello correspondant.</span><span class="sxs-lookup"><span data-stu-id="6e862-148">Remove these nodes before removing hello corresponding node type.</span></span> <span data-ttu-id="6e862-149">Une fois que tous les nœuds correspondants sont supprimés, vous pouvez supprimer hello NodeType de configuration du cluster hello et commencer une configuration de mise à niveau de l’aide [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="6e862-149">Once all corresponding nodes are removed, you can remove hello NodeType from hello cluster configuration and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span>


### <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="6e862-150">Remplacer les nœuds principaux de votre cluster</span><span class="sxs-lookup"><span data-stu-id="6e862-150">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="6e862-151">remplacement de Hello de nœuds principaux doit être effectuée un seul nœud après l’autre, au lieu de supprimer, puis ajouter dans des lots.</span><span class="sxs-lookup"><span data-stu-id="6e862-151">hello replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6e862-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6e862-152">Next steps</span></span>
* [<span data-ttu-id="6e862-153">Paramètres de configuration pour un cluster Windows autonome</span><span class="sxs-lookup"><span data-stu-id="6e862-153">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="6e862-154">Sécuriser un cluster autonome sur Windows à l’aide de certificats X509</span><span class="sxs-lookup"><span data-stu-id="6e862-154">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="6e862-155">Créer un cluster Service Fabric autonome avec des machines virtuelles Azure Windows</span><span class="sxs-lookup"><span data-stu-id="6e862-155">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

