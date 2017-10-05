---
title: Configurer un cluster Azure Service Fabric autonome | Microsoft Docs
description: "Créez un cluster de développement autonome avec trois nœuds s’exécutant sur le même ordinateur. Une fois l’installation terminée, vous serez prêt à créer un cluster de plusieurs ordinateurs."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/06/2017
ms.author: dekapur
ms.openlocfilehash: 5c8f4c784eed7b64810a3dd1c36c043d22a66936
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a><span data-ttu-id="3b3ad-104">Créer votre premier cluster Service Fabric autonome</span><span class="sxs-lookup"><span data-stu-id="3b3ad-104">Create your first Service Fabric standalone cluster</span></span>
<span data-ttu-id="3b3ad-105">Vous pouvez créer un cluster Service Fabric autonome sur n’importe quel ordinateur ou machine virtuelle exécutant Windows Server 2012 R2 ou Windows Server 2016, en local ou dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-105">You can create a Service Fabric standalone cluster on any virtual machines or computers running Windows Server 2012 R2 or Windows Server 2016, on-premises or in the cloud.</span></span> <span data-ttu-id="3b3ad-106">Ce démarrage rapide vous aide à créer un cluster de développement autonome en seulement quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-106">This quickstart helps you to create a development standalone cluster in just a few minutes.</span></span>  <span data-ttu-id="3b3ad-107">Une fois que vous avez terminé, vous disposez d’un cluster à trois nœuds s’exécutant sur un seul ordinateur sur lequel vous pouvez déployer des applications.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-107">When you're finished, you have a three-node cluster running on a single computer that you can deploy apps to.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3b3ad-108">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="3b3ad-108">Before you begin</span></span>
<span data-ttu-id="3b3ad-109">Service Fabric fournit un package d’installation pour créer des clusters Service Fabric autonomes.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-109">Service Fabric provides a setup package to create Service Fabric standalone clusters.</span></span>  <span data-ttu-id="3b3ad-110">[Téléchargez le package d’installation](http://go.microsoft.com/fwlink/?LinkId=730690).</span><span class="sxs-lookup"><span data-stu-id="3b3ad-110">[Download the setup package](http://go.microsoft.com/fwlink/?LinkId=730690).</span></span>  <span data-ttu-id="3b3ad-111">Décompressez le package d’installation dans un dossier sur l’ordinateur ou la machine virtuelle sur lequel/laquelle vous configurez le cluster de développement.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-111">Unzip the setup package to a folder on the computer or virtual machine where you are setting up the development cluster.</span></span>  <span data-ttu-id="3b3ad-112">Le contenu du package d’installation est décrit en détail [ici](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="3b3ad-112">The contents of the setup package are described in detail [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="3b3ad-113">L’administrateur de cluster déployant et configurant le cluster doit disposer de privilèges d’administrateur sur l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-113">The cluster administrator deploying and configuring the cluster must have administrator privileges on the computer.</span></span> <span data-ttu-id="3b3ad-114">Vous ne pouvez pas installer Service Fabric sur un contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-114">You cannot install Service Fabric on a domain controller.</span></span>

## <a name="validate-the-environment"></a><span data-ttu-id="3b3ad-115">Valider l’environnement</span><span class="sxs-lookup"><span data-stu-id="3b3ad-115">Validate the environment</span></span>
<span data-ttu-id="3b3ad-116">Le script *TestConfiguration.ps1* contenu dans le package autonome est utilisé pour analyser les meilleures pratiques, afin de vérifier si un cluster peut être déployé dans un environnement donné.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-116">The *TestConfiguration.ps1* script in the standalone package is used as a best practices analyzer to validate whether a cluster can be deployed on a given environment.</span></span> <span data-ttu-id="3b3ad-117">La section [Préparation du déploiement](service-fabric-cluster-standalone-deployment-preparation.md) répertorie les conditions préalables et les exigences de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-117">[Deployment preparation](service-fabric-cluster-standalone-deployment-preparation.md) lists the pre-requisites and environment requirements.</span></span> <span data-ttu-id="3b3ad-118">Exécutez le script pour vérifier si vous pouvez créer le cluster de développement :</span><span class="sxs-lookup"><span data-stu-id="3b3ad-118">Run the script to verify if you can create the development cluster:</span></span>

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-the-cluster"></a><span data-ttu-id="3b3ad-119">Création du cluster</span><span class="sxs-lookup"><span data-stu-id="3b3ad-119">Create the cluster</span></span>
<span data-ttu-id="3b3ad-120">Plusieurs fichiers d’exemples de configuration de cluster sont installés avec le package d’installation.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-120">Several sample cluster configuration files are installed with the setup package.</span></span> <span data-ttu-id="3b3ad-121">*ClusterConfig.Unsecure.DevCluster.json* correspond à la configuration de cluster la plus simple : un cluster à trois nœuds non sécurisé, s’exécutant sur un seul ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-121">*ClusterConfig.Unsecure.DevCluster.json* is the simplest cluster configuration: an unsecure, three-node cluster running on a single computer.</span></span>  <span data-ttu-id="3b3ad-122">Les autres fichiers de configuration décrivent des clusters uniques ou de plusieurs ordinateurs, sécurisés à l’aide de certificats X.509 ou de la sécurité Windows.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-122">Other config files describe single or multi-machine clusters secured with X.509 certificates or Windows security.</span></span>  <span data-ttu-id="3b3ad-123">Vous n’avez pas besoin de modifier les paramètres de configuration par défaut pour ce didacticiel, mais parcourez le fichier de configuration et familiarisez-vous avec les paramètres.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-123">You don't need to modify any of the default config settings for this tutorial, but look through the config file and get familiar with the settings.</span></span>  <span data-ttu-id="3b3ad-124">La section **Nœuds** décrit les trois nœuds du cluster : nom, adresse IP, [type de nœud, domaine d’erreur et domaine de mise à niveau](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="3b3ad-124">The **nodes** section describes the three nodes in the cluster: name, IP address, [node type, fault domain, and upgrade domain](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span></span>  <span data-ttu-id="3b3ad-125">La section **Propriétés** définit la [sécurité, le niveau de fiabilité, la collecte des diagnostics et les types de nœuds](service-fabric-cluster-manifest.md#cluster-properties) pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-125">The **properties** section defines the [security, reliability level, diagnostics collection, and types of nodes](service-fabric-cluster-manifest.md#cluster-properties) for the cluster.</span></span>

<span data-ttu-id="3b3ad-126">Ce cluster n’est pas sécurisé.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-126">This cluster is unsecure.</span></span>  <span data-ttu-id="3b3ad-127">N’importe qui peut se connecter anonymement et effectuer des opérations de gestion. Les clusters de production doivent donc toujours être sécurisés à l’aide de certificats X.509 ou via la sécurité Windows.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-127">Anyone can connect anonymously and perform management operations, so production clusters should always be secured using X.509 certificates or Windows security.</span></span>  <span data-ttu-id="3b3ad-128">La sécurité peut uniquement être configurée au moment de la création du cluster et il n’est pas possible d’activer la sécurité une fois le cluster créé.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-128">Security is only configured at cluster creation time and it is not possible to enable security after the cluster is created.</span></span>  <span data-ttu-id="3b3ad-129">Lisez [Sécuriser un cluster](service-fabric-cluster-security.md) pour en savoir plus sur la sécurité du cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-129">Read [Secure a cluster](service-fabric-cluster-security.md) to learn more about Service Fabric cluster security.</span></span>  

<span data-ttu-id="3b3ad-130">Pour créer le cluster de développement à trois nœuds, exécutez le script *CreateServiceFabricCluster.ps1* à partir d’une session administrateur PowerShell :</span><span class="sxs-lookup"><span data-stu-id="3b3ad-130">To create the three-node development cluster, run the *CreateServiceFabricCluster.ps1* script from an administrator PowerShell session:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="3b3ad-131">Le package de runtime Service Fabric est automatiquement téléchargé et installé lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-131">The Service Fabric runtime package is automatically downloaded and installed at time of cluster creation.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="3b3ad-132">Connexion au cluster</span><span class="sxs-lookup"><span data-stu-id="3b3ad-132">Connect to the cluster</span></span>
<span data-ttu-id="3b3ad-133">Votre cluster de développement à trois nœuds est maintenant en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-133">Your three-node development cluster is now running.</span></span> <span data-ttu-id="3b3ad-134">Le module Service Fabric PowerShell est installé avec le runtime.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-134">The ServiceFabric PowerShell module is installed with the runtime.</span></span>  <span data-ttu-id="3b3ad-135">Vous pouvez vérifier que le cluster s’exécute à partir du même ordinateur ou à partir d’un ordinateur distant avec le runtime Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-135">You can verify that the cluster is running from the same computer or from a remote computer with the Service Fabric runtime.</span></span>  <span data-ttu-id="3b3ad-136">L’applet de commande [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) établit une connexion au cluster.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-136">The [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection to the cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
<span data-ttu-id="3b3ad-137">Pour obtenir des exemples de connexion à un cluster, consultez [Se connecter à un cluster sécurisé](service-fabric-connect-to-secure-cluster.md) .</span><span class="sxs-lookup"><span data-stu-id="3b3ad-137">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting to a cluster.</span></span> <span data-ttu-id="3b3ad-138">Une fois connecté au cluster, utilisez l’applet de commande [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) pour afficher une liste des nœuds du cluster et les informations d’état pour chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-138">After connecting to the cluster, use the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet to display a list of nodes in the cluster and status information for each node.</span></span> <span data-ttu-id="3b3ad-139">**HealthState** doit être à l’état *OK* pour chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-139">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-the-cluster-using-service-fabric-explorer"></a><span data-ttu-id="3b3ad-140">Visualiser votre cluster à l’aide de l’outil Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="3b3ad-140">Visualize the cluster using Service Fabric explorer</span></span>
<span data-ttu-id="3b3ad-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) est un bon outil pour visualiser votre cluster et gérer les applications.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="3b3ad-142">Service Fabric Explorer est un service qui s’exécute dans le cluster, auquel vous accédez à l’aide d’un navigateur en utilisant l’adresse [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="3b3ad-142">Service Fabric Explorer is a service that runs in the cluster, which you access using a browser by navigating to [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> 

<span data-ttu-id="3b3ad-143">Le tableau de bord de cluster fournit une vue d’ensemble de votre cluster, y compris un résumé de l’intégrité de l’application et du nœud.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-143">The cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="3b3ad-144">L’affichage des nœuds montre la disposition physique du cluster.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-144">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="3b3ad-145">Vous pouvez identifier les applications ayant déployé du code sur un nœud donné.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-145">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-the-cluster"></a><span data-ttu-id="3b3ad-147">Supprimer le cluster</span><span class="sxs-lookup"><span data-stu-id="3b3ad-147">Remove the cluster</span></span>
<span data-ttu-id="3b3ad-148">Pour supprimer un cluster, exécutez le script PowerShell *RemoveServiceFabricCluster.ps1* à partir du dossier de package et transmettez le chemin du fichier de configuration JSON.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-148">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span></span> <span data-ttu-id="3b3ad-149">Vous pouvez éventuellement spécifier un emplacement pour le journal de la suppression.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-149">You can optionally specify a location for the log of the deletion.</span></span>

```powershell
# Removes Service Fabric cluster nodes from each computer in the configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

<span data-ttu-id="3b3ad-150">Pour supprimer le runtime Service Fabric de l’ordinateur, exécutez le script PowerShell suivant à partir du dossier de package.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-150">To remove the Service Fabric runtime from the computer, run the following PowerShell script from the package folder.</span></span>

```powershell
# Removes Service Fabric from the current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a><span data-ttu-id="3b3ad-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3b3ad-151">Next steps</span></span>
<span data-ttu-id="3b3ad-152">Maintenant que vous avez configuré un cluster de développement autonome, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="3b3ad-152">Now that you have set up a development standalone cluster, try the following articles:</span></span>
* <span data-ttu-id="3b3ad-153">[Configurez un cluster de plusieurs ordinateurs autonome](service-fabric-cluster-creation-for-windows-server.md) et activez la sécurité.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-153">[Set up a multi-machine standalone cluster](service-fabric-cluster-creation-for-windows-server.md) and enable security.</span></span>
* [<span data-ttu-id="3b3ad-154">Déployer des applications à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b3ad-154">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
