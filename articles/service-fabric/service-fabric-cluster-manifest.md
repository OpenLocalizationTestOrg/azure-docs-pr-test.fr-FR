---
title: "aaaConfigure votre cluster d’autonome d’Azure Service Fabric | Documents Microsoft"
description: "Découvrez comment tooconfigure votre autonome ou un cluster Service Fabric privé."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="84800-103">Paramètres de configuration pour un cluster Windows autonome</span><span class="sxs-lookup"><span data-stu-id="84800-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="84800-104">Cet article décrit la manière dont un cluster Service Fabric autonomes à l’aide de tooconfigure hello ***ClusterConfig.JSON*** fichier.</span><span class="sxs-lookup"><span data-stu-id="84800-104">This article describes how tooconfigure a standalone Service Fabric cluster using hello ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="84800-105">Vous pouvez utiliser ces informations toospecify de fichier tels que des nœuds de Service Fabric hello et leurs adresses IP, les différents types de nœuds de cluster de hello, configurations de sécurité hello, ainsi que la topologie de réseau hello en termes de domaines de pannes/mise à niveau, pour votre autonome cluster.</span><span class="sxs-lookup"><span data-stu-id="84800-105">You can use this file toospecify information such as hello Service Fabric nodes and their IP addresses, different types of nodes on hello cluster, hello security configurations as well as hello network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="84800-106">Lorsque vous [télécharger le package de Service Fabric autonomes hello](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), quelques exemples de fichier ClusterConfig.JSON de hello sont téléchargés tooyour poste.</span><span class="sxs-lookup"><span data-stu-id="84800-106">When you [download hello standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of hello ClusterConfig.JSON file are downloaded tooyour work machine.</span></span> <span data-ttu-id="84800-107">les exemples Hello ayant *DevCluster* dans leurs noms vous aide à créer un cluster avec tous les trois nœuds hello même ordinateur, comme la logique de nœuds.</span><span class="sxs-lookup"><span data-stu-id="84800-107">hello samples having *DevCluster* in their names will help you create a cluster with all three nodes on hello same machine, like logical nodes.</span></span> <span data-ttu-id="84800-108">Parmi ces nœuds, au moins un doit être marqué comme nœud principal.</span><span class="sxs-lookup"><span data-stu-id="84800-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="84800-109">Ce cluster est utile pour un environnement de test ou de développement et n’est pas pris en charge comme cluster de production.</span><span class="sxs-lookup"><span data-stu-id="84800-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="84800-110">les exemples Hello ayant *MultiMachine* dans leurs noms, vous aide à créer un cluster de qualité production, chaque nœud sur un ordinateur distinct.</span><span class="sxs-lookup"><span data-stu-id="84800-110">hello samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span>

1. <span data-ttu-id="84800-111">*ClusterConfig.Unsecure.DevCluster.JSON* et *ClusterConfig.Unsecure.MultiMachine.JSON* montrent comment cluster respectivement toocreate un test non sécurisé ou production.</span><span class="sxs-lookup"><span data-stu-id="84800-111">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how toocreate an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="84800-112">*ClusterConfig.Windows.DevCluster.JSON* et *ClusterConfig.Windows.MultiMachine.JSON* indiquent comment toocreate cluster de test ou de production, sécurisées à l’aide de [sécurité Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="84800-112">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how toocreate test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="84800-113">*ClusterConfig.X509.DevCluster.JSON* et *ClusterConfig.X509.MultiMachine.JSON* indiquent comment toocreate cluster de test ou de production, sécurisés à l’aide [X509 sécurité basée sur certificat](service-fabric-windows-cluster-x509-security.md).</span><span class="sxs-lookup"><span data-stu-id="84800-113">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how toocreate test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="84800-114">Maintenant, nous allons examiner hello différentes sections d’un ***ClusterConfig.JSON*** de fichiers comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="84800-114">Now we will examine hello various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="84800-115">Configurations de cluster générales</span><span class="sxs-lookup"><span data-stu-id="84800-115">General cluster configurations</span></span>
<span data-ttu-id="84800-116">Cette rubrique décrit hello cluster large des configurations spécifiques, comme indiqué dans l’extrait de JSON hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="84800-116">This covers hello broad cluster specific configurations, as shown in hello JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

<span data-ttu-id="84800-117">Vous pouvez attribuer à n’importe quel cluster Service Fabric de tooyour nom convivial en lui assignant toohello **nom** variable.</span><span class="sxs-lookup"><span data-stu-id="84800-117">You can give any friendly name tooyour Service Fabric cluster by assigning it toohello **name** variable.</span></span> <span data-ttu-id="84800-118">Hello **clusterConfigurationVersion** est le numéro de version de hello de votre cluster, vous devez l’augmenter chaque fois que vous mettez à niveau votre cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="84800-118">hello **clusterConfigurationVersion** is hello version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="84800-119">Vous devez laisser toutefois hello **apiVersion** toohello par défaut.</span><span class="sxs-lookup"><span data-stu-id="84800-119">You should however leave hello **apiVersion** toohello default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a><span data-ttu-id="84800-120">Nœuds de cluster de hello</span><span class="sxs-lookup"><span data-stu-id="84800-120">Nodes on hello cluster</span></span>
<span data-ttu-id="84800-121">Vous pouvez configurer des nœuds de hello sur votre cluster Service Fabric à l’aide de hello **nœuds** section, comme hello ci-dessous illustre d’extrait de code.</span><span class="sxs-lookup"><span data-stu-id="84800-121">You can configure hello nodes on your Service Fabric cluster by using hello **nodes** section, as hello following snippet shows.</span></span>

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

<span data-ttu-id="84800-122">Un cluster Service Fabric doit contenir au moins 3 nœuds.</span><span class="sxs-lookup"><span data-stu-id="84800-122">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="84800-123">Vous pouvez ajouter la section de toothis plusieurs nœuds conformément à votre installation.</span><span class="sxs-lookup"><span data-stu-id="84800-123">You can add more nodes toothis section as per your setup.</span></span> <span data-ttu-id="84800-124">Hello tableau suivant décrit les paramètres de configuration de hello pour chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="84800-124">hello following table explains hello configuration settings for each node.</span></span>

| <span data-ttu-id="84800-125">**Configuration de nœuds**</span><span class="sxs-lookup"><span data-stu-id="84800-125">**Node configuration**</span></span> | <span data-ttu-id="84800-126">**Description**</span><span class="sxs-lookup"><span data-stu-id="84800-126">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="84800-127">nodeName</span><span class="sxs-lookup"><span data-stu-id="84800-127">nodeName</span></span> |<span data-ttu-id="84800-128">Vous pouvez donner n’importe quel nœud de toohello nom convivial.</span><span class="sxs-lookup"><span data-stu-id="84800-128">You can give any friendly name toohello node.</span></span> |
| <span data-ttu-id="84800-129">iPAddress</span><span class="sxs-lookup"><span data-stu-id="84800-129">iPAddress</span></span> |<span data-ttu-id="84800-130">Rechercher adresse IP de hello du nœud en ouvrant une fenêtre de commande et en tapant `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="84800-130">Find out hello IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="84800-131">Notez l’adresse de hello IPV4 et affectez-le toohello **iPAddress** variable.</span><span class="sxs-lookup"><span data-stu-id="84800-131">Note hello IPV4 address and assign it toohello **iPAddress** variable.</span></span> |
| <span data-ttu-id="84800-132">nodeTypeRef</span><span class="sxs-lookup"><span data-stu-id="84800-132">nodeTypeRef</span></span> |<span data-ttu-id="84800-133">Chaque nœud peut être associé à un type de nœud différent.</span><span class="sxs-lookup"><span data-stu-id="84800-133">Each node can be assigned a different node type.</span></span> <span data-ttu-id="84800-134">Hello [types de nœuds](#nodetypes) sont définis dans la section hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="84800-134">hello [node types](#nodetypes) are defined in hello section below.</span></span> |
| <span data-ttu-id="84800-135">faultDomain</span><span class="sxs-lookup"><span data-stu-id="84800-135">faultDomain</span></span> |<span data-ttu-id="84800-136">Erreur domaines activer administrateurs toodefine hello physiques nœuds de cluster risque d’échouer au hello même moment en raison des dépendances de physique tooshared.</span><span class="sxs-lookup"><span data-stu-id="84800-136">Fault domains enable cluster administrators toodefine hello physical nodes that might fail at hello same time due tooshared physical dependencies.</span></span> |
| <span data-ttu-id="84800-137">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="84800-137">upgradeDomain</span></span> |<span data-ttu-id="84800-138">Domaines de mise à niveau décrivent les jeux de nœuds qui ne sont pas arrêtés pour Service Fabric met à niveau à hello sur la même heure.</span><span class="sxs-lookup"><span data-stu-id="84800-138">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about hello same time.</span></span> <span data-ttu-id="84800-139">Vous pouvez choisir le toowhich tooassign de nœuds domaines de mise à niveau, car ils ne sont pas limités par des exigences physiques.</span><span class="sxs-lookup"><span data-stu-id="84800-139">You can choose which nodes tooassign toowhich Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="84800-140">Propriétés du cluster</span><span class="sxs-lookup"><span data-stu-id="84800-140">Cluster properties</span></span>
<span data-ttu-id="84800-141">Hello **propriétés** section Bonjour ClusterConfig.JSON est le cluster de hello tooconfigure utilisés comme suit.</span><span class="sxs-lookup"><span data-stu-id="84800-141">hello **properties** section in hello ClusterConfig.JSON is used tooconfigure hello cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="84800-142">Fiabilité</span><span class="sxs-lookup"><span data-stu-id="84800-142">Reliability</span></span>
<span data-ttu-id="84800-143">concept Hello de **reliabilityLevel** définit le nombre hello de réplicas ou les instances de services de système de Service Fabric hello pouvant s’exécuter sur les nœuds principaux hello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="84800-143">hello concept of **reliabilityLevel** defines hello number of replicas or instances of hello Service Fabric system services that can run on hello primary nodes of hello cluster.</span></span> <span data-ttu-id="84800-144">Il détermine la fiabilité hello de ces services et donc hello cluster.</span><span class="sxs-lookup"><span data-stu-id="84800-144">It determines hello reliability of these services and hence hello cluster.</span></span> <span data-ttu-id="84800-145">valeur de Hello est calculée par le système de hello au moment de la création et la mise à niveau de cluster.</span><span class="sxs-lookup"><span data-stu-id="84800-145">hello value is calcuated by hello system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="84800-146">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="84800-146">Diagnostics</span></span>
<span data-ttu-id="84800-147">Hello **diagnosticsStore** section vous permet de diagnostics de tooenable tooconfigure paramètres et nœud de résolution des problèmes ou défaillances de cluster, comme indiqué dans hello suivant extrait de code.</span><span class="sxs-lookup"><span data-stu-id="84800-147">hello **diagnosticsStore** section allows you tooconfigure parameters tooenable diagnostics and troubleshooting node or cluster failures, as shown in hello following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="84800-148">Hello **métadonnées** est une description de diagnostics de votre cluster et peut être définie en fonction de votre installation.</span><span class="sxs-lookup"><span data-stu-id="84800-148">hello **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="84800-149">Ces variables vous aident à collecter les journaux de suivi ETW, les vidages sur incident ainsi que les compteurs de performance.</span><span class="sxs-lookup"><span data-stu-id="84800-149">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="84800-150">Consultez les sections [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) (Journal de suivi) et [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) pour plus d’informations sur les journaux de suivi ETW.</span><span class="sxs-lookup"><span data-stu-id="84800-150">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="84800-151">Tous les journaux, y compris [vidages sur incident](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) et [les compteurs de performance](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) peut être dirigé toohello **connectionString** dossier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="84800-151">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed toohello **connectionString** folder on your machine.</span></span> <span data-ttu-id="84800-152">Vous pouvez également utiliser *AzureStorage* pour le stockage des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="84800-152">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="84800-153">Voici un exemple d’extrait de code.</span><span class="sxs-lookup"><span data-stu-id="84800-153">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="84800-154">Sécurité</span><span class="sxs-lookup"><span data-stu-id="84800-154">Security</span></span>
<span data-ttu-id="84800-155">Hello **sécurité** section n’est nécessaire pour un cluster de Service Fabric autonomes sécurisé.</span><span class="sxs-lookup"><span data-stu-id="84800-155">hello **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="84800-156">Hello suivant extrait de code montre une partie de cette section.</span><span class="sxs-lookup"><span data-stu-id="84800-156">hello following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="84800-157">Hello **métadonnées** est une description de votre cluster sécurisé et peut être définie en fonction de votre installation.</span><span class="sxs-lookup"><span data-stu-id="84800-157">hello **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="84800-158">Hello **ClusterCredentialType** et **ServerCredentialType** déterminer le type hello de sécurité qui implémentent les cluster hello et les nœuds de hello.</span><span class="sxs-lookup"><span data-stu-id="84800-158">hello **ClusterCredentialType** and **ServerCredentialType** determine hello type of security that hello cluster and hello nodes will implement.</span></span> <span data-ttu-id="84800-159">Ils peuvent être définies tooeither *X509* pour une sécurité basée sur certificat, ou *Windows* pour une sécurité basée sur Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="84800-159">They can be set tooeither *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="84800-160">Hello reste Hello **sécurité** section reposera sur le type hello de sécurité de hello.</span><span class="sxs-lookup"><span data-stu-id="84800-160">hello rest of hello **security** section will be based on hello type of hello security.</span></span> <span data-ttu-id="84800-161">Lecture [sécurité basée sur les certificats dans un cluster autonome](service-fabric-windows-cluster-x509-security.md) ou [sécurité Windows dans un cluster autonome](service-fabric-windows-cluster-windows-security.md) pour plus d’informations sur comment toofill out hello reste de hello **sécurité**section.</span><span class="sxs-lookup"><span data-stu-id="84800-161">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how toofill out hello rest of hello **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="84800-162">Types de nœuds</span><span class="sxs-lookup"><span data-stu-id="84800-162">Node Types</span></span>
<span data-ttu-id="84800-163">Hello **nodeTypes** section décrit le type hello de nœuds de hello votre cluster.</span><span class="sxs-lookup"><span data-stu-id="84800-163">hello **nodeTypes** section describes hello type of hello nodes that your cluster has.</span></span> <span data-ttu-id="84800-164">Type de nœud au moins doit être spécifié pour un cluster, comme indiqué dans l’extrait de code hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="84800-164">At least one node type must be specified for a cluster, as shown in hello snippet below.</span></span> 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

<span data-ttu-id="84800-165">Hello **nom** est hello le nom convivial pour ce type de nœud particulier.</span><span class="sxs-lookup"><span data-stu-id="84800-165">hello **name** is hello friendly name for this particular node type.</span></span> <span data-ttu-id="84800-166">toocreate un nœud de ce type de nœud, attribuer son nom convivial de toohello **le nodeTypeRef** variable pour ce nœud, comme indiqué [ci-dessus](#clusternodes).</span><span class="sxs-lookup"><span data-stu-id="84800-166">toocreate a node of this node type, assign its friendly name toohello **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="84800-167">Pour chaque type de nœud, définissez hello connexion points de terminaison qui seront utilisés.</span><span class="sxs-lookup"><span data-stu-id="84800-167">For each node type, define hello connection endpoints that will be used.</span></span> <span data-ttu-id="84800-168">Vous pouvez choisir n’importe quel numéro de port pour ces points de terminaison de connexion, à condition qu’ils n’entrent pas en conflit avec d’autres points de terminaison de ce cluster.</span><span class="sxs-lookup"><span data-stu-id="84800-168">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="84800-169">Dans un cluster à plusieurs nœud, il y aura un ou plusieurs nœuds principales (autrement dit, **isPrimary** défini trop*true*), en fonction de hello [ **reliabilityLevel** ](#reliability).</span><span class="sxs-lookup"><span data-stu-id="84800-169">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set too*true*), depending on hello [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="84800-170">Lecture [les considérations de planification de la capacité de cluster Service Fabric](service-fabric-cluster-capacity.md) pour plus d’informations sur **nodeTypes** et **reliabilityLevel**et tooknow les principaux et hello types de nœud principal.</span><span class="sxs-lookup"><span data-stu-id="84800-170">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel**, and tooknow what are primary and hello non-primary node types.</span></span> 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a><span data-ttu-id="84800-171">Points de terminaison utilisés des types de nœuds hello tooconfigure</span><span class="sxs-lookup"><span data-stu-id="84800-171">Endpoints used tooconfigure hello node types</span></span>
* <span data-ttu-id="84800-172">*clientConnectionEndpointPort* est hello le port utilisé par hello client tooconnect toohello le cluster, lors de l’utilisation des API clientes hello.</span><span class="sxs-lookup"><span data-stu-id="84800-172">*clientConnectionEndpointPort* is hello port used by hello client tooconnect toohello cluster, when using hello client APIs.</span></span> 
* <span data-ttu-id="84800-173">*clusterConnectionEndpointPort* est le port hello à laquelle les nœuds hello communiquent entre eux.</span><span class="sxs-lookup"><span data-stu-id="84800-173">*clusterConnectionEndpointPort* is hello port at which hello nodes communicate with each other.</span></span>
* <span data-ttu-id="84800-174">*leaseDriverEndpointPort* est hello le port utilisé par le pilote du bail hello cluster toofind out si les nœuds de hello sont toujours actifs.</span><span class="sxs-lookup"><span data-stu-id="84800-174">*leaseDriverEndpointPort* is hello port used by hello cluster lease driver toofind out if hello nodes are still active.</span></span> 
* <span data-ttu-id="84800-175">*serviceConnectionEndpointPort* est le port hello utilisé par les applications hello et les services déployés sur un nœud, toocommunicate avec le client de Service Fabric hello sur ce nœud particulier.</span><span class="sxs-lookup"><span data-stu-id="84800-175">*serviceConnectionEndpointPort* is hello port used by hello applications and services deployed on a node, toocommunicate with hello Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="84800-176">*httpGatewayEndpointPort* est hello le port utilisé par hello Service Fabric Explorer tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="84800-176">*httpGatewayEndpointPort* is hello port used by hello Service Fabric Explorer tooconnect toohello cluster.</span></span>
* <span data-ttu-id="84800-177">*ephemeralPorts* remplacer hello [ports dynamiques utilisés par hello du système d’exploitation](https://support.microsoft.com/kb/929851).</span><span class="sxs-lookup"><span data-stu-id="84800-177">*ephemeralPorts* override hello [dynamic ports used by hello OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="84800-178">L’infrastructure de service utilisera une partie de ces ports d’application et hello restant sera disponible pour hello du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="84800-178">Service Fabric will use a part of these as application ports and hello remaining will be available for hello OS.</span></span> <span data-ttu-id="84800-179">Il sera également mapper cette plage toohello plage existante dans hello du système d’exploitation, pour tous les besoins, vous pouvez utiliser des plages hello données dans les fichiers JSON exemple hello.</span><span class="sxs-lookup"><span data-stu-id="84800-179">It will also map this range toohello existing range present in hello OS, so for all purposes, you can use hello ranges given in hello sample JSON files.</span></span> <span data-ttu-id="84800-180">Vous devez toomake que différence hello entre le début de hello et les ports finaux hello est au moins de 255.</span><span class="sxs-lookup"><span data-stu-id="84800-180">You need toomake sure that hello difference between hello start and hello end ports is at least 255.</span></span> <span data-ttu-id="84800-181">Vous pouvez rencontrer des conflits si cette différence est trop faible, étant donné que cette plage est partagée avec le système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="84800-181">You may run into conflicts if this difference is too low, since this range is shared with hello operating system.</span></span> <span data-ttu-id="84800-182">Afficher la plage de ports dynamiques hello configuré en exécutant `netsh int ipv4 show dynamicport tcp`.</span><span class="sxs-lookup"><span data-stu-id="84800-182">See hello configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="84800-183">*applicationPorts* sont des ports hello qui seront utilisées par les applications de Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="84800-183">*applicationPorts* are hello ports that will be used by hello Service Fabric applications.</span></span> <span data-ttu-id="84800-184">plage de ports d’application Hello doit être suffisamment grand toocover exigence de point de terminaison hello de vos applications.</span><span class="sxs-lookup"><span data-stu-id="84800-184">hello application port range should be large enough toocover hello endpoint requirement of your applications.</span></span> <span data-ttu-id="84800-185">Cette plage doit être exclusif à partir de la plage de ports dynamiques hello sur ordinateur hello, c'est-à-dire hello *ephemeralPorts* plage défini dans la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="84800-185">This range should be exclusive from hello dynamic port range on hello machine, i.e. hello *ephemeralPorts* range as set in hello configuration.</span></span>  <span data-ttu-id="84800-186">L’infrastructure de service utilisera ces chaque fois que les nouveaux ports sont nécessaires, ainsi que la prenez soin d’ouvrir le pare-feu hello pour ces ports.</span><span class="sxs-lookup"><span data-stu-id="84800-186">Service Fabric will use these whenever new ports are required, as well as take care of opening hello firewall for these ports.</span></span> 
* <span data-ttu-id="84800-187">*reverseProxyEndpointPort* est un point de terminaison de proxy inverse facultatif.</span><span class="sxs-lookup"><span data-stu-id="84800-187">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="84800-188">Consultez [Proxy inverse de Service Fabric](service-fabric-reverseproxy.md) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="84800-188">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="84800-189">Paramètres du journal</span><span class="sxs-lookup"><span data-stu-id="84800-189">Log Settings</span></span>
<span data-ttu-id="84800-190">Hello **fabricSettings** section vous permet de répertoires de racines tooset hello pour les données de Service Fabric hello et les journaux.</span><span class="sxs-lookup"><span data-stu-id="84800-190">hello **fabricSettings** section allows you tooset hello root directories for hello Service Fabric data and logs.</span></span> <span data-ttu-id="84800-191">Vous pouvez personnaliser ces uniquement lors de la création initiale du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="84800-191">You can customize these only during hello initial cluster creation.</span></span> <span data-ttu-id="84800-192">Voici un exemple d’extrait de cette section.</span><span class="sxs-lookup"><span data-stu-id="84800-192">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="84800-193">Il est recommandé à l’aide d’un disque du système d’exploitation non hello FabricDataRoot et FabricLogRoot car il fournit une fiabilité accrue contre les pannes du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="84800-193">We recommended using a non-OS drive as hello FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="84800-194">Notez que si vous personnalisez uniquement la racine de données hello, puis racine de journal hello sera placé un niveau sous la racine de données hello.</span><span class="sxs-lookup"><span data-stu-id="84800-194">Note that if you customize only hello data root, then hello log root will be placed one level below hello data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="84800-195">Paramètres Reliable Service avec état</span><span class="sxs-lookup"><span data-stu-id="84800-195">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="84800-196">Hello **KtlLogger** section vous permet de paramètres de configuration globale tooset hello pour les Services fiables.</span><span class="sxs-lookup"><span data-stu-id="84800-196">hello **KtlLogger** section allows you tooset hello global configuration settings for Reliable Services.</span></span> <span data-ttu-id="84800-197">Pour plus d’informations sur ces paramètres, consultez [Configuration de services fiables (Reliable Services) avec état](service-fabric-reliable-services-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="84800-197">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="84800-198">exemple Hello ci-dessous montre le journal des transactions partagées toochange hello hello qui obtient la création de tooback toutes les collections fiables pour les services avec état.</span><span class="sxs-lookup"><span data-stu-id="84800-198">hello example below shows how toochange hello hello shared transaction log that gets created tooback any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="84800-199">Fonctionnalités supplémentaires</span><span class="sxs-lookup"><span data-stu-id="84800-199">Add-on features</span></span>
<span data-ttu-id="84800-200">fonctionnalités du module complémentaire tooconfigure, hello apiVersion doit être configuré en tant que « 04-2017' ou une version ultérieure, et addonFeatures doit toobe configuré :</span><span class="sxs-lookup"><span data-stu-id="84800-200">tooconfigure add-on features, hello apiVersion should be configured as '04-2017' or higher, and addonFeatures needs toobe configured:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="84800-201">Support pour les conteneurs</span><span class="sxs-lookup"><span data-stu-id="84800-201">Container support</span></span>
<span data-ttu-id="84800-202">tooenable conteneur prise en charge à la fois de conteneur windows server et de conteneur hyper-v pour les clusters d’autonome, fonctionnalité des modules complémentaires 'DnsService' hello doit toobe activé.</span><span class="sxs-lookup"><span data-stu-id="84800-202">tooenable container support for both windows server container and hyper-v container for standalone clusters, hello 'DnsService' add-on feature needs toobe enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="84800-203">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="84800-203">Next steps</span></span>
<span data-ttu-id="84800-204">Une fois que vous avez un fichier ClusterConfig.JSON complet configuré conformément à votre installation de cluster autonome, vous pouvez déployer votre cluster par article hello suivant [créer un cluster de Service Fabric autonomes](service-fabric-cluster-creation-for-windows-server.md) , puis effectuez trop[visualiser votre cluster avec Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="84800-204">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following hello article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed too[visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

