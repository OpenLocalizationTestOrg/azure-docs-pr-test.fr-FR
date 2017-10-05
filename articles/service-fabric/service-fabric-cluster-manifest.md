---
title: Configurer votre cluster Azure Service Fabric autonome | Microsoft Docs
description: "Découvrez comment configurer votre cluster Service Fabric autonome ou privé."
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
ms.openlocfilehash: 9885dce18dabac4a945dafd219e3ae190e34a83b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="d0387-103">Paramètres de configuration pour un cluster Windows autonome</span><span class="sxs-lookup"><span data-stu-id="d0387-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="d0387-104">Cet article explique comment configurer un cluster Service Fabric autonome à l’aide du fichier ***ClusterConfig.JSON***.</span><span class="sxs-lookup"><span data-stu-id="d0387-104">This article describes how to configure a standalone Service Fabric cluster using the ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="d0387-105">Vous pouvez utiliser ce fichier pour spécifier des informations telles que les nœuds Service Fabric et leurs adresses IP, différents types de nœuds sur le cluster, les configurations de sécurité, ainsi que la topologie du réseau en termes de domaines d’erreur et de mise à niveau, pour votre cluster autonome.</span><span class="sxs-lookup"><span data-stu-id="d0387-105">You can use this file to specify information such as the Service Fabric nodes and their IP addresses, different types of nodes on the cluster, the security configurations as well as the network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="d0387-106">Lorsque vous [téléchargez le package Service Fabric autonome](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), quelques exemples de fichier ClusterConfig.JSON sont téléchargés sur votre ordinateur de travail.</span><span class="sxs-lookup"><span data-stu-id="d0387-106">When you [download the standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of the ClusterConfig.JSON file are downloaded to your work machine.</span></span> <span data-ttu-id="d0387-107">Les exemples comprenant *DevCluster* dans leurs noms vous permettent de créer un cluster avec les trois nœuds sur le même ordinateur, comme des nœuds logiques.</span><span class="sxs-lookup"><span data-stu-id="d0387-107">The samples having *DevCluster* in their names will help you create a cluster with all three nodes on the same machine, like logical nodes.</span></span> <span data-ttu-id="d0387-108">Parmi ces nœuds, au moins un doit être marqué comme nœud principal.</span><span class="sxs-lookup"><span data-stu-id="d0387-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="d0387-109">Ce cluster est utile pour un environnement de test ou de développement et n’est pas pris en charge comme cluster de production.</span><span class="sxs-lookup"><span data-stu-id="d0387-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="d0387-110">Les exemples comprenant *MultiMachine* dans leurs noms vous permettent de créer un cluster de niveau de production, avec chaque nœud sur un ordinateur distinct.</span><span class="sxs-lookup"><span data-stu-id="d0387-110">The samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span>

1. <span data-ttu-id="d0387-111">*ClusterConfig.Unsecure.DevCluster.JSON* et *ClusterConfig.Unsecure.MultiMachine.JSON* montrent comment créer un cluster de test ou de production non sécurisé respectivement.</span><span class="sxs-lookup"><span data-stu-id="d0387-111">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how to create an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="d0387-112">*ClusterConfig.Windows.DevCluster.JSON* et *ClusterConfig.Windows.MultiMachine.JSON* montrent comment créer un cluster de test ou de production sécurisé à l’aide de la [sécurité Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="d0387-112">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how to create test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="d0387-113">*ClusterConfig.X509.DevCluster.JSON* et *ClusterConfig.X509.MultiMachine.JSON* montrent comment créer un cluster de test ou de production sécurisé à l’aide de la [sécurité basée sur un certificat X509](service-fabric-windows-cluster-x509-security.md).</span><span class="sxs-lookup"><span data-stu-id="d0387-113">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how to create test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="d0387-114">Nous allons maintenant examiner les différentes sections d’un fichier ***ClusterConfig.JSON*** comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d0387-114">Now we will examine the various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="d0387-115">Configurations de cluster générales</span><span class="sxs-lookup"><span data-stu-id="d0387-115">General cluster configurations</span></span>
<span data-ttu-id="d0387-116">Cette section couvre les configurations spécifiques à de larges clusters, comme indiqué dans l’extrait de code JSON ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d0387-116">This covers the broad cluster specific configurations, as shown in the JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

<span data-ttu-id="d0387-117">Vous pouvez attribuer un nom convivial à votre cluster Service Fabric en lui assignant la variable **name** .</span><span class="sxs-lookup"><span data-stu-id="d0387-117">You can give any friendly name to your Service Fabric cluster by assigning it to the **name** variable.</span></span> <span data-ttu-id="d0387-118">**clusterConfigurationVersion** est le numéro de version de votre cluster, que vous devez augmenter chaque fois que vous mettez à niveau votre cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d0387-118">The **clusterConfigurationVersion** is the version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="d0387-119">Il est cependant recommandé de conserver la valeur par défaut attribuée à **apiVersion** .</span><span class="sxs-lookup"><span data-stu-id="d0387-119">You should however leave the **apiVersion** to the default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-the-cluster"></a><span data-ttu-id="d0387-120">Nœuds sur le cluster</span><span class="sxs-lookup"><span data-stu-id="d0387-120">Nodes on the cluster</span></span>
<span data-ttu-id="d0387-121">Vous pouvez configurer les nœuds de votre cluster Service Fabric à l’aide de la section **nœuds** , comme le montre l’extrait de code suivant.</span><span class="sxs-lookup"><span data-stu-id="d0387-121">You can configure the nodes on your Service Fabric cluster by using the **nodes** section, as the following snippet shows.</span></span>

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

<span data-ttu-id="d0387-122">Un cluster Service Fabric doit contenir au moins 3 nœuds.</span><span class="sxs-lookup"><span data-stu-id="d0387-122">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="d0387-123">Vous pouvez ajouter d’autres nœuds à cette section, selon votre configuration.</span><span class="sxs-lookup"><span data-stu-id="d0387-123">You can add more nodes to this section as per your setup.</span></span> <span data-ttu-id="d0387-124">Le tableau suivant décrit les paramètres de configuration de chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="d0387-124">The following table explains the configuration settings for each node.</span></span>

| <span data-ttu-id="d0387-125">**Configuration de nœuds**</span><span class="sxs-lookup"><span data-stu-id="d0387-125">**Node configuration**</span></span> | <span data-ttu-id="d0387-126">**Description**</span><span class="sxs-lookup"><span data-stu-id="d0387-126">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="d0387-127">nodeName</span><span class="sxs-lookup"><span data-stu-id="d0387-127">nodeName</span></span> |<span data-ttu-id="d0387-128">Vous pouvez attribuer n’importe quel nom convivial au nœud.</span><span class="sxs-lookup"><span data-stu-id="d0387-128">You can give any friendly name to the node.</span></span> |
| <span data-ttu-id="d0387-129">iPAddress</span><span class="sxs-lookup"><span data-stu-id="d0387-129">iPAddress</span></span> |<span data-ttu-id="d0387-130">Identifiez l’adresse IP de votre nœud en ouvrant une fenêtre de commande puis en tapant `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="d0387-130">Find out the IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="d0387-131">Notez l’adresse IPV4 et assignez-la à la variable **iPAddress** .</span><span class="sxs-lookup"><span data-stu-id="d0387-131">Note the IPV4 address and assign it to the **iPAddress** variable.</span></span> |
| <span data-ttu-id="d0387-132">nodeTypeRef</span><span class="sxs-lookup"><span data-stu-id="d0387-132">nodeTypeRef</span></span> |<span data-ttu-id="d0387-133">Chaque nœud peut être associé à un type de nœud différent.</span><span class="sxs-lookup"><span data-stu-id="d0387-133">Each node can be assigned a different node type.</span></span> <span data-ttu-id="d0387-134">Les [types de nœuds](#nodetypes) sont définis dans la section ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d0387-134">The [node types](#nodetypes) are defined in the section below.</span></span> |
| <span data-ttu-id="d0387-135">faultDomain</span><span class="sxs-lookup"><span data-stu-id="d0387-135">faultDomain</span></span> |<span data-ttu-id="d0387-136">Les domaines d'erreur permettent aux administrateurs de cluster de définir les nœuds physiques qui sont susceptibles de rencontrer un échec en même temps en raison des dépendances physiques partagées.</span><span class="sxs-lookup"><span data-stu-id="d0387-136">Fault domains enable cluster administrators to define the physical nodes that might fail at the same time due to shared physical dependencies.</span></span> |
| <span data-ttu-id="d0387-137">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="d0387-137">upgradeDomain</span></span> |<span data-ttu-id="d0387-138">Les domaines de mise à niveau décrivent des ensembles de nœuds qui sont arrêtés pour les mises à niveau Service Fabric, à peu près au même moment.</span><span class="sxs-lookup"><span data-stu-id="d0387-138">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about the same time.</span></span> <span data-ttu-id="d0387-139">Vous pouvez choisir les nœuds à attribuer aux domaines de mise à niveau car ils ne sont pas limités par des exigences physiques.</span><span class="sxs-lookup"><span data-stu-id="d0387-139">You can choose which nodes to assign to which Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="d0387-140">Propriétés du cluster</span><span class="sxs-lookup"><span data-stu-id="d0387-140">Cluster properties</span></span>
<span data-ttu-id="d0387-141">La section **properties** du fichier ClusterConfig.JSON permet de configurer le cluster comme suit.</span><span class="sxs-lookup"><span data-stu-id="d0387-141">The **properties** section in the ClusterConfig.JSON is used to configure the cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="d0387-142">Fiabilité</span><span class="sxs-lookup"><span data-stu-id="d0387-142">Reliability</span></span>
<span data-ttu-id="d0387-143">Le concept de **reliabilityLevel** définit le nombre de répliques ou instances des services système Service Fabric qui peuvent s’exécuter sur les nœuds principaux du cluster.</span><span class="sxs-lookup"><span data-stu-id="d0387-143">The concept of **reliabilityLevel** defines the number of replicas or instances of the Service Fabric system services that can run on the primary nodes of the cluster.</span></span> <span data-ttu-id="d0387-144">Il détermine augmente la fiabilité de ces services et, par conséquent, du cluster.</span><span class="sxs-lookup"><span data-stu-id="d0387-144">It determines the reliability of these services and hence the cluster.</span></span> <span data-ttu-id="d0387-145">La valeur est calculée par le système au moment de la création et de la mise à niveau du cluster.</span><span class="sxs-lookup"><span data-stu-id="d0387-145">The value is calcuated by the system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="d0387-146">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="d0387-146">Diagnostics</span></span>
<span data-ttu-id="d0387-147">La section **diagnosticsStore** vous permet de configurer des paramètres pour activer les diagnostics et corriger les défaillances de nœud ou du cluster, comme illustré dans l’extrait de code suivant.</span><span class="sxs-lookup"><span data-stu-id="d0387-147">The **diagnosticsStore** section allows you to configure parameters to enable diagnostics and troubleshooting node or cluster failures, as shown in the following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="d0387-148">La section **metadata** est une description du diagnostic de votre cluster et peut être définie selon votre installation.</span><span class="sxs-lookup"><span data-stu-id="d0387-148">The **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="d0387-149">Ces variables vous aident à collecter les journaux de suivi ETW, les vidages sur incident ainsi que les compteurs de performance.</span><span class="sxs-lookup"><span data-stu-id="d0387-149">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="d0387-150">Consultez les sections [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) (Journal de suivi) et [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) pour plus d’informations sur les journaux de suivi ETW.</span><span class="sxs-lookup"><span data-stu-id="d0387-150">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="d0387-151">Tous les journaux, notamment les [vidages sur incident](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) et les [compteurs de performance](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) peuvent être dirigés vers le dossier **connectionString** sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d0387-151">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed to the **connectionString** folder on your machine.</span></span> <span data-ttu-id="d0387-152">Vous pouvez également utiliser *AzureStorage* pour le stockage des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="d0387-152">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="d0387-153">Voici un exemple d’extrait de code.</span><span class="sxs-lookup"><span data-stu-id="d0387-153">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="d0387-154">Sécurité</span><span class="sxs-lookup"><span data-stu-id="d0387-154">Security</span></span>
<span data-ttu-id="d0387-155">La section **security** est nécessaire pour garantir la sécurité d’un cluster Service Fabric autonome.</span><span class="sxs-lookup"><span data-stu-id="d0387-155">The **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="d0387-156">L’extrait de code suivant montre une partie de cette section.</span><span class="sxs-lookup"><span data-stu-id="d0387-156">The following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="d0387-157">La section **metadata** est une description de votre cluster sécurisé et peut être définie selon votre installation.</span><span class="sxs-lookup"><span data-stu-id="d0387-157">The **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="d0387-158">Les propriétés **ClusterCredentialType** et **ServerCredentialType** déterminent le type de sécurité que le cluster et les nœuds implémenteront.</span><span class="sxs-lookup"><span data-stu-id="d0387-158">The **ClusterCredentialType** and **ServerCredentialType** determine the type of security that the cluster and the nodes will implement.</span></span> <span data-ttu-id="d0387-159">Elles peuvent avoir la valeur *X509* pour une sécurité basée sur un certificat, ou *Windows* pour une sécurité basée sur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d0387-159">They can be set to either *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="d0387-160">Le reste de la section **security** varie selon le type de sécurité.</span><span class="sxs-lookup"><span data-stu-id="d0387-160">The rest of the **security** section will be based on the type of the security.</span></span> <span data-ttu-id="d0387-161">Consultez les rubriques [Sécuriser un cluster autonome sur Windows à l’aide de certificats X.509](service-fabric-windows-cluster-x509-security.md) ou [Sécuriser un cluster autonome sur Windows à l’aide de la sécurité Windows](service-fabric-windows-cluster-windows-security.md) pour plus d’informations sur la façon de remplir le reste de la section **security**.</span><span class="sxs-lookup"><span data-stu-id="d0387-161">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how to fill out the rest of the **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="d0387-162">Types de nœuds</span><span class="sxs-lookup"><span data-stu-id="d0387-162">Node Types</span></span>
<span data-ttu-id="d0387-163">La section **nodeTypes** décrit le type des nœuds de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d0387-163">The **nodeTypes** section describes the type of the nodes that your cluster has.</span></span> <span data-ttu-id="d0387-164">Au moins un type de nœud doit être spécifié pour un cluster, comme indiqué dans l’extrait de code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d0387-164">At least one node type must be specified for a cluster, as shown in the snippet below.</span></span> 

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

<span data-ttu-id="d0387-165">La valeur **name** représente le nom convivial de ce type de nœud particulier.</span><span class="sxs-lookup"><span data-stu-id="d0387-165">The **name** is the friendly name for this particular node type.</span></span> <span data-ttu-id="d0387-166">Pour créer un nœud de ce type, affectez son nom convivial à la variable **nodeTypeRef** pour ce nœud, comme indiqué [ci-dessus](#clusternodes).</span><span class="sxs-lookup"><span data-stu-id="d0387-166">To create a node of this node type, assign its friendly name to the **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="d0387-167">Pour chaque type de nœud, définissez les points de terminaison de connexion qui seront utilisés.</span><span class="sxs-lookup"><span data-stu-id="d0387-167">For each node type, define the connection endpoints that will be used.</span></span> <span data-ttu-id="d0387-168">Vous pouvez choisir n’importe quel numéro de port pour ces points de terminaison de connexion, à condition qu’ils n’entrent pas en conflit avec d’autres points de terminaison de ce cluster.</span><span class="sxs-lookup"><span data-stu-id="d0387-168">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="d0387-169">Un cluster à plusieurs nœuds contient un ou plusieurs nœuds principaux (c'est-à-dire que **isPrimary** a la valeur *true*) en fonction du [**reliabilityLevel**](#reliability).</span><span class="sxs-lookup"><span data-stu-id="d0387-169">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set to *true*), depending on the [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="d0387-170">Consultez la rubrique [Considérations en matière de planification de la capacité du cluster Service Fabric](service-fabric-cluster-capacity.md) pour plus d’informations sur **nodeTypes** et **reliabilityLevel** et pour connaître la différence entre les types de nœud principal et non principal.</span><span class="sxs-lookup"><span data-stu-id="d0387-170">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel**, and to know what are primary and the non-primary node types.</span></span> 

#### <a name="endpoints-used-to-configure-the-node-types"></a><span data-ttu-id="d0387-171">Points de terminaison utilisés pour configurer les types de nœuds</span><span class="sxs-lookup"><span data-stu-id="d0387-171">Endpoints used to configure the node types</span></span>
* <span data-ttu-id="d0387-172">*clientConnectionEndpointPort* est le port utilisé par le client pour se connecter au cluster lorsque vous utilisez les API clientes.</span><span class="sxs-lookup"><span data-stu-id="d0387-172">*clientConnectionEndpointPort* is the port used by the client to connect to the cluster, when using the client APIs.</span></span> 
* <span data-ttu-id="d0387-173">*clusterConnectionEndpointPort* est le port sur lequel les nœuds communiquent entre eux.</span><span class="sxs-lookup"><span data-stu-id="d0387-173">*clusterConnectionEndpointPort* is the port at which the nodes communicate with each other.</span></span>
* <span data-ttu-id="d0387-174">*leaseDriverEndpointPort* est le port utilisé par le pilote de lease cluster pour savoir si les nœuds sont toujours actifs.</span><span class="sxs-lookup"><span data-stu-id="d0387-174">*leaseDriverEndpointPort* is the port used by the cluster lease driver to find out if the nodes are still active.</span></span> 
* <span data-ttu-id="d0387-175">*serviceConnectionEndpointPort* est le port utilisé par les applications et les services déployés sur un nœud pour communiquer avec le client Service Fabric sur ce nœud spécifique.</span><span class="sxs-lookup"><span data-stu-id="d0387-175">*serviceConnectionEndpointPort* is the port used by the applications and services deployed on a node, to communicate with the Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="d0387-176">*httpGatewayEndpointPort* est le port utilisé par le Service Fabric Explorer pour se connecter au cluster.</span><span class="sxs-lookup"><span data-stu-id="d0387-176">*httpGatewayEndpointPort* is the port used by the Service Fabric Explorer to connect to the cluster.</span></span>
* <span data-ttu-id="d0387-177">*ephemeralPorts* remplacent les [ports dynamiques utilisés par le système d’exploitation](https://support.microsoft.com/kb/929851).</span><span class="sxs-lookup"><span data-stu-id="d0387-177">*ephemeralPorts* override the [dynamic ports used by the OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="d0387-178">Service Fabric utilise une partie de ces ports d’application et le reste est disponible pour le système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="d0387-178">Service Fabric will use a part of these as application ports and the remaining will be available for the OS.</span></span> <span data-ttu-id="d0387-179">Il mappe également cette plage sur la plage existante dans le système d’exploitation. Vous pouvez donc utiliser en toutes circonstances les plages spécifiées dans les exemples de fichiers JSON.</span><span class="sxs-lookup"><span data-stu-id="d0387-179">It will also map this range to the existing range present in the OS, so for all purposes, you can use the ranges given in the sample JSON files.</span></span> <span data-ttu-id="d0387-180">Vous devez vous assurer que la différence entre les ports de début et de fin est au moins de 255.</span><span class="sxs-lookup"><span data-stu-id="d0387-180">You need to make sure that the difference between the start and the end ports is at least 255.</span></span> <span data-ttu-id="d0387-181">Vous pouvez rencontrer des conflits si cette différence est trop faible, étant donné que cette plage est partagée avec le système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="d0387-181">You may run into conflicts if this difference is too low, since this range is shared with the operating system.</span></span> <span data-ttu-id="d0387-182">Consultez la plage de ports dynamiques configurée en exécutant `netsh int ipv4 show dynamicport tcp`.</span><span class="sxs-lookup"><span data-stu-id="d0387-182">See the configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="d0387-183">*applicationPorts* sont les ports qui sont utilisés par les applications Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d0387-183">*applicationPorts* are the ports that will be used by the Service Fabric applications.</span></span> <span data-ttu-id="d0387-184">La plage des ports d’application doit suffire à couvrir les exigences en matière de points de terminaison de vos applications.</span><span class="sxs-lookup"><span data-stu-id="d0387-184">The application port range should be large enough to cover the endpoint requirement of your applications.</span></span> <span data-ttu-id="d0387-185">Cette plage doit être exclusive à partir de la plage de ports dynamiques de la machine, c’est-à-dire la plage *ephemeralPorts* comme défini dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="d0387-185">This range should be exclusive from the dynamic port range on the machine, i.e. the *ephemeralPorts* range as set in the configuration.</span></span>  <span data-ttu-id="d0387-186">Service Fabric les utilise chaque fois que des nouveaux ports sont nécessaires et prend également en charge l’ouverture du pare-feu pour ces ports.</span><span class="sxs-lookup"><span data-stu-id="d0387-186">Service Fabric will use these whenever new ports are required, as well as take care of opening the firewall for these ports.</span></span> 
* <span data-ttu-id="d0387-187">*reverseProxyEndpointPort* est un point de terminaison de proxy inverse facultatif.</span><span class="sxs-lookup"><span data-stu-id="d0387-187">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="d0387-188">Consultez [Proxy inverse de Service Fabric](service-fabric-reverseproxy.md) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="d0387-188">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="d0387-189">Paramètres du journal</span><span class="sxs-lookup"><span data-stu-id="d0387-189">Log Settings</span></span>
<span data-ttu-id="d0387-190">La section **fabricSettings** vous permet de définir les répertoires racine des données et journaux Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d0387-190">The **fabricSettings** section allows you to set the root directories for the Service Fabric data and logs.</span></span> <span data-ttu-id="d0387-191">Vous pouvez personnaliser ces éléments uniquement lors de la création initiale du cluster.</span><span class="sxs-lookup"><span data-stu-id="d0387-191">You can customize these only during the initial cluster creation.</span></span> <span data-ttu-id="d0387-192">Voici un exemple d’extrait de cette section.</span><span class="sxs-lookup"><span data-stu-id="d0387-192">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="d0387-193">Nous vous recommandons d’utiliser un lecteur autre que celui du système d’exploitation pour FabricDataRoot et FabricLogRoot pour plus de fiabilité en cas de défaillance du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="d0387-193">We recommended using a non-OS drive as the FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="d0387-194">Notez que si vous personnalisez uniquement la racine des données, la racine du journal sera placée un niveau en dessous de la racine des données.</span><span class="sxs-lookup"><span data-stu-id="d0387-194">Note that if you customize only the data root, then the log root will be placed one level below the data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="d0387-195">Paramètres Reliable Service avec état</span><span class="sxs-lookup"><span data-stu-id="d0387-195">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="d0387-196">La section **KtlLogger** section vous permet de définir les paramètres de configuration globaux pour les Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="d0387-196">The **KtlLogger** section allows you to set the global configuration settings for Reliable Services.</span></span> <span data-ttu-id="d0387-197">Pour plus d’informations sur ces paramètres, consultez [Configuration de services fiables (Reliable Services) avec état](service-fabric-reliable-services-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="d0387-197">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="d0387-198">L’exemple ci-dessous montre comment modifier le journal des transactions partagé qui est créé pour sauvegarder toutes les Reliable Collections pour les services avec état.</span><span class="sxs-lookup"><span data-stu-id="d0387-198">The example below shows how to change the the shared transaction log that gets created to back any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="d0387-199">Fonctionnalités supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d0387-199">Add-on features</span></span>
<span data-ttu-id="d0387-200">Pour configurer les fonctionnalités supplémentaires, apiVersion doit être configuré sur « 04-2017 » ou version ultérieure, et addonFeatures doit être configuré :</span><span class="sxs-lookup"><span data-stu-id="d0387-200">To configure add-on features, the apiVersion should be configured as '04-2017' or higher, and addonFeatures needs to be configured:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="d0387-201">Support pour les conteneurs</span><span class="sxs-lookup"><span data-stu-id="d0387-201">Container support</span></span>
<span data-ttu-id="d0387-202">Pour activer le support pour les conteneurs Windows Server et Hyper-V pour les clusters autonomes, la fonctionnalité supplémentaire « DnsService » doit être activée.</span><span class="sxs-lookup"><span data-stu-id="d0387-202">To enable container support for both windows server container and hyper-v container for standalone clusters, the 'DnsService' add-on feature needs to be enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d0387-203">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d0387-203">Next steps</span></span>
<span data-ttu-id="d0387-204">Une fois que vous disposez d’un fichier ClusterConfig.JSON complètement configuré selon votre cluster autonome, vous pouvez déployer votre cluster en suivant les instructions de l’article [Créer un cluster Service Fabric autonome](service-fabric-cluster-creation-for-windows-server.md), puis passez à l’étape [Visualiser votre cluster à l’aide de l’outil Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="d0387-204">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following the article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed to [visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

