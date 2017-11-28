---
title: "aaaCreate autonome de cluster avec les machines virtuelles Azure exécutant Windows | Documents Microsoft"
description: "Découvrez comment toocreate et gérer un cluster Azure Service Fabric sur les machines virtuelles Azure exécutant Windows Server."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="2de5b-103">Créer un cluster Service Fabric autonome à trois nœuds avec des machines virtuelles Azure sous Windows Server</span><span class="sxs-lookup"><span data-stu-id="2de5b-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="2de5b-104">Cet article décrit comment toocreate un cluster sur Windows Azure ordinateurs virtuels (VM), à l’aide de hello programme d’installation de l’infrastructure de Service autonome pour Windows Server.</span><span class="sxs-lookup"><span data-stu-id="2de5b-104">This article describes how toocreate a cluster on Windows-based Azure virtual machines (VMs), using hello standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="2de5b-105">scénario de Hello est un cas spécial de [créer et gérer un cluster exécutant Windows Server](service-fabric-cluster-creation-for-windows-server.md) où les ordinateurs virtuels de hello sont [machines virtuelles Azure exécutant Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), mais vous ne créez pas [Azure cluster Service Fabric informatique](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2de5b-105">hello scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where hello VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="2de5b-106">distinction Hello dans ce modèle est cluster Service Fabric autonomes hello créé par hello comme suit est entièrement géré par vous, tandis que hello Service nuage Azure Fabric clusters sont gérés et mis à niveau par hello Service Fabric fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="2de5b-106">hello distinction in following this pattern is that hello standalone Service Fabric cluster created by hello following steps is entirely managed by you, whereas hello Azure cloud-based Service Fabric clusters are managed and upgraded by hello Service Fabric resource provider.</span></span>

## <a name="steps-toocreate-hello-standalone-cluster"></a><span data-ttu-id="2de5b-107">Cluster d’étapes toocreate hello autonome</span><span class="sxs-lookup"><span data-stu-id="2de5b-107">Steps toocreate hello standalone cluster</span></span>
1. <span data-ttu-id="2de5b-108">Connectez-vous à toohello portail Azure et créer un nouveau Windows Server 2012 R2 Datacenter ou Windows Server 2016 VM de centre de données dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="2de5b-108">Sign in toohello Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="2de5b-109">Lire l’article de hello [créer une machine virtuelle Windows Bonjour Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="2de5b-109">Read hello article [Create a Windows VM in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="2de5b-110">Ajouter quelques toohello de machines virtuelles plus même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="2de5b-110">Add a couple more VMs toohello same resource group.</span></span> <span data-ttu-id="2de5b-111">Assurez-vous que chacune des machines virtuelles de hello a hello même nom d’utilisateur administrateur et un mot de passe lors de la création.</span><span class="sxs-lookup"><span data-stu-id="2de5b-111">Ensure that each of hello VMs has hello same administrator user name and password when created.</span></span> <span data-ttu-id="2de5b-112">Une fois créé, vous devez voir tous les trois machines virtuelles Bonjour même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="2de5b-112">Once created you should see all three VMs in hello same virtual network.</span></span>
3. <span data-ttu-id="2de5b-113">Se connecter tooeach Hello machines virtuelles et de désactiver le pare-feu Windows à l’aide de hello hello [Gestionnaire de serveur, tableau de bord de serveur Local](https://technet.microsoft.com/library/jj134147.aspx).</span><span class="sxs-lookup"><span data-stu-id="2de5b-113">Connect tooeach of hello VMs and turn off hello Windows Firewall using hello [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="2de5b-114">Cela garantit que le trafic réseau de hello peut communiquer entre les machines hello.</span><span class="sxs-lookup"><span data-stu-id="2de5b-114">This ensures that hello network traffic can communicate between hello machines.</span></span> <span data-ttu-id="2de5b-115">Lors de l’ordinateur de tooeach connecté, obtenir l’adresse IP de hello en ouvrant une invite de commandes et en tapant `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="2de5b-115">While connected tooeach machine, get hello IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="2de5b-116">Vous pouvez également voir hello IP adresse de chaque ordinateur sur le portail hello, en sélectionnant des ressources du réseau virtuel hello pour le groupe de ressources hello et en vérifiant les interfaces réseau de hello créés pour chacun de ces ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="2de5b-116">Alternatively you can see hello IP address of each machine on hello portal, by selecting hello virtual network resource for hello resource group and checking hello network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="2de5b-117">Se connecter tooone Hello machines virtuelles et test ping hello autres deux machines virtuelles avec succès.</span><span class="sxs-lookup"><span data-stu-id="2de5b-117">Connect tooone of hello VMs and test that you can ping hello other two VMs successfully.</span></span>
5. <span data-ttu-id="2de5b-118">Se connecter tooone Hello machines virtuelles et [télécharger le package de Service Fabric hello autonome pour Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) dans un nouveau dossier sur hello machine et extraire le package de hello.</span><span class="sxs-lookup"><span data-stu-id="2de5b-118">Connect tooone of hello VMs and [download hello standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on hello machine and extract hello package.</span></span>
6. <span data-ttu-id="2de5b-119">Ouvrez hello *ClusterConfig.Unsecure.MultiMachine.json* dans le bloc-notes et modifier chaque nœud avec des adresses IP hello trois ordinateurs de hello.</span><span class="sxs-lookup"><span data-stu-id="2de5b-119">Open hello *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with hello three IP addresses of hello machines.</span></span> <span data-ttu-id="2de5b-120">Modifier le nom du cluster hello haut hello et enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="2de5b-120">Change hello cluster name at hello top and save hello file.</span></span>  <span data-ttu-id="2de5b-121">Voici un exemple partiels hello du manifeste du cluster.</span><span class="sxs-lookup"><span data-stu-id="2de5b-121">A partial example of hello cluster manifest is shown below.</span></span>
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. <span data-ttu-id="2de5b-122">Si vous envisagez cette toobe un cluster sécurisé, décider de mesures de sécurité hello vous comme toouse et suivez les étapes de hello en hello associés lien : [X509 certificat](service-fabric-windows-cluster-x509-security.md) ou [sécurité Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="2de5b-122">If you intend this toobe a secure cluster, decide hello security measure you would like toouse and follow hello steps at hello associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="2de5b-123">Si la configuration de cluster hello à l’aide de la sécurité de Windows, vous devez tooset d’un toomanage de contrôleur de domaine Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2de5b-123">If setting up hello cluster using Windows Security, you will need tooset up a domain controller toomanage Active Directory.</span></span> <span data-ttu-id="2de5b-124">Notez que l’utilisation d’un ordinateur de contrôleur de domaine en tant que nœud Service Fabric n'est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="2de5b-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="2de5b-125">Ouvrez une [fenêtre PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span><span class="sxs-lookup"><span data-stu-id="2de5b-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="2de5b-126">Accédez toohello dossier où vous extrait le package de programme d’installation autonome téléchargé hello et enregistré le fichier de configuration de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2de5b-126">Navigate toohello folder where you extracted hello downloaded standalone installer package and saved hello cluster configuration file.</span></span> <span data-ttu-id="2de5b-127">Exécutez hello suivant du cluster de hello de toodeploy de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="2de5b-127">Run hello following PowerShell command toodeploy hello cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="2de5b-128">script de Hello configure à distance cluster Service Fabric de hello et doit créer un rapport Progression comme déploiement restaure via.</span><span class="sxs-lookup"><span data-stu-id="2de5b-128">hello script will remotely configure hello Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="2de5b-129">Après environ une minute, vous pouvez vérifier si le cluster de hello est opérationnel en vous connectant toohello Service Fabric Explorer à l’aide de IP l’ordinateur hello adresses, par exemple à l’aide de `http://10.1.0.5:19080/Explorer/index.html`.</span><span class="sxs-lookup"><span data-stu-id="2de5b-129">After about a minute, you can check if hello cluster is operational by connecting toohello Service Fabric Explorer using one of hello machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2de5b-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2de5b-130">Next steps</span></span>
* [<span data-ttu-id="2de5b-131">Créer des clusters Service Fabric autonomes sur un serveur Windows Server ou Linux</span><span class="sxs-lookup"><span data-stu-id="2de5b-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="2de5b-132">Ajouter ou supprimer le cluster Service Fabric de nœuds tooa autonome</span><span class="sxs-lookup"><span data-stu-id="2de5b-132">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="2de5b-133">Paramètres de configuration pour un cluster Windows autonome</span><span class="sxs-lookup"><span data-stu-id="2de5b-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="2de5b-134">Sécuriser un cluster autonome sur Windows à l’aide de la sécurité Windows</span><span class="sxs-lookup"><span data-stu-id="2de5b-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="2de5b-135">Sécuriser un cluster autonome sur Windows à l’aide de certificats X509</span><span class="sxs-lookup"><span data-stu-id="2de5b-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

