---
title: machines virtuelles de calcul aaaLinux dans un cluster HPC Pack | Documents Microsoft
description: "Découvrez comment toocreate et utilisez un HPC Pack du cluster dans Azure pour Linux à haute performance des charges de travail (HPC)"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="ecd73-103">Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="ecd73-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="ecd73-104">Configurez un cluster [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) dans Azure, contenant un nœud principal qui exécute Windows Server et plusieurs nœuds de calcul qui exécutent une distribution Linux.</span><span class="sxs-lookup"><span data-stu-id="ecd73-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="ecd73-105">Explorer les options toomove des données entre les nœuds de Linux hello et nœud de cluster de hello tête de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-105">Explore options toomove data among hello Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="ecd73-106">Découvrez comment toosubmit Linux HPC travaux toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="ecd73-106">Learn how toosubmit Linux HPC jobs toohello cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="ecd73-107">À un niveau élevé, hello diagramme suivant montre hello HPC Pack cluster vous créez et manipulez.</span><span class="sxs-lookup"><span data-stu-id="ecd73-107">At a high level, hello following diagram shows hello HPC Pack cluster you create and work with.</span></span>

![Cluster HPC Pack avec nœuds Linux][scenario]

<span data-ttu-id="ecd73-109">Pour les autres options de toorun Linux HPC les charges de travail dans Azure, consultez [ressources techniques pour le traitement et l’informatique hautes performances](../../../batch/big-compute-resources.md).</span><span class="sxs-lookup"><span data-stu-id="ecd73-109">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="ecd73-110">Déployer un cluster HPC Pack avec des nœuds de calcul Linux</span><span class="sxs-lookup"><span data-stu-id="ecd73-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="ecd73-111">Cet article explique les toodeploy deux options vous un cluster HPC Pack dans Azure avec les nœuds de calcul Linux.</span><span class="sxs-lookup"><span data-stu-id="ecd73-111">This article shows you two options toodeploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="ecd73-112">Les deux méthodes utilisent une image de Marketplace de Windows Server avec du nœud principal HPC Pack toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-112">Both methods use a Marketplace image of Windows Server with HPC Pack toocreate hello head node.</span></span> 

* <span data-ttu-id="ecd73-113">**Modèle de gestionnaire de ressources Azure** -utiliser un modèle à partir de hello Azure Marketplace, ou un modèle de démarrage rapide de communauté hello, tooautomate la création du cluster hello dans le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-113">**Azure Resource Manager template** - Use a template from hello Azure Marketplace, or a quickstart template from hello community, tooautomate creation of hello cluster in hello Resource Manager deployment model.</span></span> <span data-ttu-id="ecd73-114">Par exemple, hello [cluster HPC Pack pour les charges de travail Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) modèle Bonjour Azure Marketplace permet de créer une infrastructure de cluster HPC Pack complète pour Linux HPC les charges de travail.</span><span class="sxs-lookup"><span data-stu-id="ecd73-114">For example, hello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="ecd73-115">**Script PowerShell** -hello d’utilisation [script de déploiement IaaS de Microsoft HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-hpciaascluster.ps1**) tooautomate un déploiement de la création du cluster dans le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-115">**PowerShell script** - Use hello [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) tooautomate a complete cluster deployment in hello classic deployment model.</span></span> <span data-ttu-id="ecd73-116">Ce script Azure PowerShell utilise une image de machine virtuelle HPC Pack Bonjour Azure Marketplace pour le déploiement rapide et fournit un ensemble complet de toodeploy des paramètres de configuration des nœuds de calcul Linux.</span><span class="sxs-lookup"><span data-stu-id="ecd73-116">This Azure PowerShell script uses an HPC Pack VM image in hello Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters toodeploy Linux compute nodes.</span></span>

<span data-ttu-id="ecd73-117">Pour plus d’informations sur les options de déploiement de cluster HPC Pack dans Azure, consultez [toocreate les Options et de gérer un cluster informatique de hautes performances (HPC) dans Azure avec Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ecd73-117">For more information about HPC Pack cluster deployment options in Azure, see [Options toocreate and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ecd73-118">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ecd73-118">Prerequisites</span></span>
* <span data-ttu-id="ecd73-119">**Abonnement Azure** -vous pouvez utiliser un abonnement soit Bonjour service Global Azure ou Azure Chine.</span><span class="sxs-lookup"><span data-stu-id="ecd73-119">**Azure subscription** - You can use a subscription in either hello Azure Global or Azure China service.</span></span> <span data-ttu-id="ecd73-120">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="ecd73-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="ecd73-121">**Quota de cœurs** -vous devrez peut-être le quota de hello tooincrease de cœurs, en particulier si vous choisissez toodeploy plusieurs nœuds de cluster avec des tailles de machine virtuelle multicœurs.</span><span class="sxs-lookup"><span data-stu-id="ecd73-121">**Cores quota** - You might need tooincrease hello quota of cores, especially if you choose toodeploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="ecd73-122">tooincrease un quota, ouvrez une demande de support technique en ligne sans frais.</span><span class="sxs-lookup"><span data-stu-id="ecd73-122">tooincrease a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="ecd73-123">**Les distributions Linux** -actuellement HPC Pack prend en charge hello suivant des distributions de Linux pour les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="ecd73-123">**Linux distributions** - Currently HPC Pack supports hello following Linux distributions for compute nodes.</span></span> <span data-ttu-id="ecd73-124">Vous pouvez utiliser les versions Marketplace de ces distributions dans la mesure où elles sont disponibles, ou fournissez la vôtre.</span><span class="sxs-lookup"><span data-stu-id="ecd73-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="ecd73-125">**Basée sur centOS** : 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, HPC 6.5, HPC 7.1</span><span class="sxs-lookup"><span data-stu-id="ecd73-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="ecd73-126">**Red Hat Enterprise Linux** : 6.7, 6.8, 7.2</span><span class="sxs-lookup"><span data-stu-id="ecd73-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="ecd73-127">**SUSE Linux Enterprise Server** : SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 pour HPC, SLES 12 pour HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="ecd73-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="ecd73-128">**Ubuntu Server** : 14.04 LTS, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="ecd73-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="ecd73-129">réseau de RDMA Azure hello toouse avec l’une des tailles de machine virtuelle hello prenant en charge RDMA, spécifiez une image de SUSE Linux Enterprise Server 12 HPC ou HPC de base CentOS hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ecd73-129">toouse hello Azure RDMA network with one of hello RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from hello Azure Marketplace.</span></span> <span data-ttu-id="ecd73-130">Pour plus d’informations, consultez [Tailles de machine virtuelle de calcul haute performance](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ecd73-130">For more information, see [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="ecd73-131">Cluster hello du toodeploy autres conditions préalables à l’aide du script de déploiement IaaS de HPC Pack hello :</span><span class="sxs-lookup"><span data-stu-id="ecd73-131">Additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="ecd73-132">**Ordinateur client** -vous avez besoin d’un script de déploiement de clients basés sur Windows ordinateur toorun hello cluster.</span><span class="sxs-lookup"><span data-stu-id="ecd73-132">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="ecd73-133">**Azure PowerShell** - [installez et configurez Azure PowerShell](/powershell/azure/overview) (version 0.8.10 ou ultérieure) sur votre ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="ecd73-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="ecd73-134">**Script de déploiement IaaS de HPC Pack** - Téléchargez et décompressez hello dernière version de script hello hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="ecd73-134">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="ecd73-135">Vous pouvez vérifier la version hello du script de hello en exécutant `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="ecd73-135">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="ecd73-136">Cet article est basé sur la version 4.4.1 ou ultérieures du script de hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-136">This article is based on version 4.4.1 or later of hello script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="ecd73-137">Option de déploiement 1.</span><span class="sxs-lookup"><span data-stu-id="ecd73-137">Deployment option 1.</span></span> <span data-ttu-id="ecd73-138">Utiliser un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ecd73-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="ecd73-139">Accédez toohello [cluster HPC Pack pour les charges de travail Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) modèle dans hello Azure Marketplace, puis cliquez sur **déployer**.</span><span class="sxs-lookup"><span data-stu-id="ecd73-139">Go toohello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="ecd73-140">Hello portail Azure, passez en revue les informations hello et puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="ecd73-140">In hello Azure portal, review hello information and then click **Create**.</span></span>
   
    ![Création de portail][portal]
3. <span data-ttu-id="ecd73-142">Sur hello **notions de base** panneau, entrez un nom pour le cluster de hello, qui nomme également la machine virtuelle du nœud principal hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-142">On hello **Basics** blade, enter a name for hello cluster, which also names hello head node VM.</span></span> <span data-ttu-id="ecd73-143">Vous pouvez choisir un groupe de ressources existant ou créer un groupe pour le déploiement de hello dans un emplacement qui est tooyou disponible.</span><span class="sxs-lookup"><span data-stu-id="ecd73-143">You can choose an existing resource group or create a group for hello deployment in a location that's available tooyou.</span></span> <span data-ttu-id="ecd73-144">emplacement Hello affecte disponibilité hello de certaines tailles de machine virtuelle et d’autres services Azure (consultez [produits disponibles par région](https://azure.microsoft.com/regions/services/)).</span><span class="sxs-lookup"><span data-stu-id="ecd73-144">hello location affects hello availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="ecd73-145">Sur hello **principal des paramètres de nœud** panneau, pour un premier déploiement, vous pouvez généralement accepter les paramètres par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-145">On hello **Head node settings** blade, for a first deployment, you can generally accept hello default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="ecd73-146">Hello **l’URL du script de post-configuration** est facultative définissant toospecify un script Windows PowerShell disponible au public que vous souhaitez toorun sur la machine virtuelle du nœud principal hello quand il est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ecd73-146">hello **Post-configuration script URL** is an optional setting toospecify a publicly available Windows PowerShell script that you want toorun on hello head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="ecd73-147">Sur hello **paramètres du nœud de calcul** panneau, sélectionnez un modèle d’affectation de noms pour les nœuds de hello, nombre de hello et taille des nœuds de hello et hello toodeploy de distribution de Linux.</span><span class="sxs-lookup"><span data-stu-id="ecd73-147">On hello **Compute node settings** blade, select a naming pattern for hello nodes, hello number and size of hello nodes, and hello Linux distribution toodeploy.</span></span>
6. <span data-ttu-id="ecd73-148">Sur hello **paramètres d’Infrastructure** panneau, entrez les noms de réseau virtuel de hello et Active Directory domaine, le domaine et les informations d’identification d’administrateur de machine virtuelle et un modèle d’affectation de noms pour les comptes de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-148">On hello **Infrastructure settings** blade, enter names for hello virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for hello storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ecd73-149">HPC Pack utilise hello les utilisateurs Active Directory domaine tooauthenticate cluster.</span><span class="sxs-lookup"><span data-stu-id="ecd73-149">HPC Pack uses hello Active Directory domain tooauthenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="ecd73-150">Une fois l’exécution des tests de validation hello et que vous passez en revue les conditions d’utilisation de hello, cliquez sur **bon**.</span><span class="sxs-lookup"><span data-stu-id="ecd73-150">After hello validation tests run and you review hello terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a><span data-ttu-id="ecd73-151">Option de déploiement 2.</span><span class="sxs-lookup"><span data-stu-id="ecd73-151">Deployment option 2.</span></span> <span data-ttu-id="ecd73-152">Utilisez le script de déploiement IaaS hello</span><span class="sxs-lookup"><span data-stu-id="ecd73-152">Use hello IaaS deployment script</span></span>
<span data-ttu-id="ecd73-153">Voici cluster de hello toodeploy autres conditions préalables à l’aide du script de déploiement IaaS de HPC Pack hello :</span><span class="sxs-lookup"><span data-stu-id="ecd73-153">Following are additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="ecd73-154">**Ordinateur client** -vous avez besoin d’un script de déploiement de clients basés sur Windows ordinateur toorun hello cluster.</span><span class="sxs-lookup"><span data-stu-id="ecd73-154">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="ecd73-155">**Azure PowerShell** - [installez et configurez Azure PowerShell](/powershell/azure/overview) (version 0.8.10 ou ultérieure) sur votre ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="ecd73-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="ecd73-156">**Script de déploiement IaaS de HPC Pack** - Téléchargez et décompressez hello dernière version de script hello hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="ecd73-156">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="ecd73-157">Vous pouvez vérifier la version hello du script de hello en exécutant `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="ecd73-157">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="ecd73-158">Cet article est basé sur la version 4.4.1 ou ultérieures du script de hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-158">This article is based on version 4.4.1 or later of hello script.</span></span>

<span data-ttu-id="ecd73-159">**Fichier de configuration XML**</span><span class="sxs-lookup"><span data-stu-id="ecd73-159">**XML configuration file**</span></span>

<span data-ttu-id="ecd73-160">Hello script de déploiement IaaS de HPC Pack utilise un fichier de configuration XML en tant que cluster HPC de hello toodescribe d’entrée.</span><span class="sxs-lookup"><span data-stu-id="ecd73-160">hello HPC Pack IaaS deployment script uses an XML configuration file as input toodescribe hello  HPC cluster.</span></span> <span data-ttu-id="ecd73-161">Hello exemple de fichier de configuration suivant spécifie un petit cluster constitué d’un nœud principal HPC Pack et deux nœuds de calcul taille A7, CentOS Linux 7.0.</span><span class="sxs-lookup"><span data-stu-id="ecd73-161">hello following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="ecd73-162">Modifier le fichier de hello en fonction des besoins de votre environnement et la configuration de cluster souhaité et enregistrez-le sous un nom tel que HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="ecd73-162">Modify hello file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="ecd73-163">Par exemple, vous devez toosupply votre nom d’abonnement et un nom de compte de stockage unique et un nom de service cloud.</span><span class="sxs-lookup"><span data-stu-id="ecd73-163">For example, you need toosupply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="ecd73-164">En outre, vous pourriez toochoose une autre prise en charge Linux image pour les nœuds de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-164">Additionally, you might want toochoose a different supported Linux image for hello compute nodes.</span></span> <span data-ttu-id="ecd73-165">Pour plus d’informations sur les éléments de hello dans le fichier de configuration hello, consultez fichier Manual.rtf de hello dans le dossier de scripts hello et [créer un cluster HPC avec hello script de déploiement IaaS de HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ecd73-165">For more information about hello elements in hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="ecd73-166">**toorun hello script de déploiement IaaS de HPC Pack**</span><span class="sxs-lookup"><span data-stu-id="ecd73-166">**toorun hello HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="ecd73-167">Ouvrez Windows PowerShell sur l’ordinateur client de hello en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ecd73-167">Open Windows PowerShell on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="ecd73-168">Modification toohello du répertoire où le script de hello est installé (E:\IaaSClusterScript dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="ecd73-168">Change directory toohello folder where hello script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="ecd73-169">Exécutez hello suivant du cluster HPC Pack de commande toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-169">Run hello following command toodeploy hello HPC Pack cluster.</span></span> <span data-ttu-id="ecd73-170">Cet exemple suppose que ce fichier de configuration hello se trouve dans E:\HPCDemoConfig.xml</span><span class="sxs-lookup"><span data-stu-id="ecd73-170">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="ecd73-171">a.</span><span class="sxs-lookup"><span data-stu-id="ecd73-171">a.</span></span> <span data-ttu-id="ecd73-172">Étant donné que hello **AdminPassword** n’est pas spécifié dans hello précédant la commande, vous êtes invité à tooenter hello mot de passe utilisateur *MyAdminName*.</span><span class="sxs-lookup"><span data-stu-id="ecd73-172">Because hello **AdminPassword** is not specified in hello preceding command, you are prompted tooenter hello password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="ecd73-173">b.</span><span class="sxs-lookup"><span data-stu-id="ecd73-173">b.</span></span> <span data-ttu-id="ecd73-174">script de Hello démarre ensuite le fichier de configuration toovalidate hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-174">hello script then starts toovalidate hello configuration file.</span></span> <span data-ttu-id="ecd73-175">Il peut prendre jusqu'à minutes tooseveral dépend de la connexion de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-175">It can take up tooseveral minutes depending on hello network connection.</span></span>
   
    ![Validation][validate]
   
    <span data-ttu-id="ecd73-177">c.</span><span class="sxs-lookup"><span data-stu-id="ecd73-177">c.</span></span> <span data-ttu-id="ecd73-178">Une fois les validations passer, script de hello répertorie toocreate de ressources de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-178">After validations pass, hello script lists hello cluster resources toocreate.</span></span> <span data-ttu-id="ecd73-179">Entrez *Y* toocontinue.</span><span class="sxs-lookup"><span data-stu-id="ecd73-179">Enter *Y* toocontinue.</span></span>
   
    ![Ressources][resources]
   
    <span data-ttu-id="ecd73-181">d.</span><span class="sxs-lookup"><span data-stu-id="ecd73-181">d.</span></span> <span data-ttu-id="ecd73-182">script de Hello démarrage toodeploy hello HPC Pack cluster et termine la configuration hello sans davantage les étapes manuelles.</span><span class="sxs-lookup"><span data-stu-id="ecd73-182">hello script starts toodeploy hello HPC Pack cluster and completes hello configuration without further manual steps.</span></span> <span data-ttu-id="ecd73-183">script de Hello peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="ecd73-183">hello script can run for several minutes.</span></span>
   
    ![Déployer][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="ecd73-185">Dans cet exemple, hello script génère un fichier journal automatiquement depuis hello **- LogFile** paramètre n’est pas spécifié.</span><span class="sxs-lookup"><span data-stu-id="ecd73-185">In this example, hello script generates a log file automatically since hello **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="ecd73-186">Hello journaux ne sont pas écrites en temps réel, mais sont collectés à fin hello de validation de hello et de déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-186">hello logs aren't written in real time, but are collected at hello end of hello validation and hello deployment.</span></span> <span data-ttu-id="ecd73-187">Si hello processus PowerShell est arrêté pendant l’exécution du script de hello, des journaux sont perdues.</span><span class="sxs-lookup"><span data-stu-id="ecd73-187">If hello PowerShell process is stopped while hello script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-toohello-head-node"></a><span data-ttu-id="ecd73-188">Se connecter toohello du nœud principal</span><span class="sxs-lookup"><span data-stu-id="ecd73-188">Connect toohello head node</span></span>
<span data-ttu-id="ecd73-189">Une fois que vous déployez un cluster HPC Pack hello dans Azure, [connexion Bureau à distance](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) à l’aide de machine virtuelle de nœud principal toohello hello des informations d’identification de domaine vous avez fourni lors du déploiement de cluster de hello (par exemple, *hpc\\ clusteradmin*).</span><span class="sxs-lookup"><span data-stu-id="ecd73-189">After you deploy hello HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="ecd73-190">Vous gérez un cluster de hello à partir du nœud principal hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-190">You manage hello cluster from hello head node.</span></span>

<span data-ttu-id="ecd73-191">Sur le nœud principal de hello, démarrez état hello de HPC Cluster Manager toocheck de cluster HPC Pack de hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-191">On hello head node, start HPC Cluster Manager toocheck hello status of hello HPC Pack cluster.</span></span> <span data-ttu-id="ecd73-192">Vous pouvez gérer et surveiller des nœuds de calcul Linux hello même façon que vous utilisez avec Windows nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="ecd73-192">You can manage and monitor Linux compute nodes hello same way you work with Windows compute nodes.</span></span> <span data-ttu-id="ecd73-193">Par exemple, vous voyez les nœuds de Linux hello répertoriés dans **gestion des ressources** (ces nœuds sont déployés avec hello **LinuxNode** modèle).</span><span class="sxs-lookup"><span data-stu-id="ecd73-193">For example, you see hello Linux nodes listed in **Resource Management** (these nodes are deployed with hello **LinuxNode** template).</span></span>

![Gestion des nœuds][management]

<span data-ttu-id="ecd73-195">Vous voyez également des nœuds Linux hello hello **thermique** vue.</span><span class="sxs-lookup"><span data-stu-id="ecd73-195">You also see hello Linux nodes in hello **Heat Map** view.</span></span>

![Carte thermique][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="ecd73-197">Comment toomove les données dans un cluster avec des nœuds Linux</span><span class="sxs-lookup"><span data-stu-id="ecd73-197">How toomove data in a cluster with Linux nodes</span></span>
<span data-ttu-id="ecd73-198">Vous avez plusieurs données toomove de choix entre des nœuds Linux et le nœud principal de Windows hello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-198">You have several choices toomove data among Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="ecd73-199">Voici trois méthodes courantes, décrits plus en détail dans les sections suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="ecd73-199">Here are three common methods, described in more detail in hello following sections:</span></span>

* <span data-ttu-id="ecd73-200">**Fichier Azure** -expose une managé toostore données SMB fichier partage de fichiers dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ecd73-200">**Azure File** - Exposes a managed SMB file share toostore data files in Azure storage.</span></span> <span data-ttu-id="ecd73-201">Les nœuds de Windows et Linux peuvent monter un partage de fichiers Azure comme un lecteur ou dossier à hello même moment, même si elles sont déployées dans des réseaux virtuels différents.</span><span class="sxs-lookup"><span data-stu-id="ecd73-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at hello same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="ecd73-202">**Partager du nœud principal SMB** -monte un dossier partagé Windows standard de nœud principal de hello des nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="ecd73-202">**Head node SMB share** - Mounts a standard Windows shared folder of hello head node on Linux nodes.</span></span>
* <span data-ttu-id="ecd73-203">**Head node NFS server** : fournit une solution de partage de fichiers pour un environnement mixte Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="ecd73-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="ecd73-204">Présentation du stockage de fichiers</span><span class="sxs-lookup"><span data-stu-id="ecd73-204">Azure File storage</span></span>
<span data-ttu-id="ecd73-205">Hello [fichier Azure](https://azure.microsoft.com/services/storage/files/) service expose les partages de fichiers à l’aide du protocole SMB 2.1 standard de hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-205">hello [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using hello standard SMB 2.1 protocol.</span></span> <span data-ttu-id="ecd73-206">Machines virtuelles Azure et les services de cloud computing peuvent partager des données de fichier entre les composants d’application via des partages montés, et des applications locales peuvent accéder les données de fichier dans un partage via hello API de stockage de fichier.</span><span class="sxs-lookup"><span data-stu-id="ecd73-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through hello File storage API.</span></span> 

<span data-ttu-id="ecd73-207">Pour obtenir des instructions détaillées toocreate un fichier Azure partager et montez-le sur le nœud principal de hello, consultez [prise en main avec un stockage de fichier Azure sur Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span><span class="sxs-lookup"><span data-stu-id="ecd73-207">For detailed steps toocreate an Azure File share and mount it on hello head node, see [Get started with Azure File storage on Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span></span> <span data-ttu-id="ecd73-208">partage de fichiers Azure hello toomount des nœuds de Linux hello, consultez [comment toouse stockage Azure files avec Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ecd73-208">toomount hello Azure File share on hello Linux nodes, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="ecd73-209">tooset des connexions persistantes, consultez [Persisting connexions tooMicrosoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecd73-209">tooset up persisting connections, see [Persisting connections tooMicrosoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="ecd73-210">Dans l’exemple suivant de hello, créer un partage de fichiers Azure sur un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ecd73-210">In hello following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="ecd73-211">toomount hello partager sur hello du nœud principal, ouvrez une invite de commandes, puis entrez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="ecd73-211">toomount hello share on hello head node, open a Command Prompt and enter hello following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="ecd73-212">Dans cet exemple, allvhdsje est le nom de votre compte de stockage, storageaccountkey est votre clé de compte de stockage et rdma est le nom de partage de fichiers Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is hello Azure File share name.</span></span> <span data-ttu-id="ecd73-213">partage de fichiers Azure Hello est monté en tant que Z: sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-213">hello Azure File share is mounted as Z: on hello head node.</span></span>

<span data-ttu-id="ecd73-214">partage de fichiers Azure hello toomount des nœuds Linux, exécutez un **clusrun** commande sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-214">toomount hello Azure File share on Linux nodes, run a **clusrun** command on hello head node.</span></span> <span data-ttu-id="ecd73-215">**[ClusRun](https://technet.microsoft.com/library/cc947685.aspx)**  est un toocarry d’outil HPC Pack utile des tâches d’administration sur plusieurs nœuds.</span><span class="sxs-lookup"><span data-stu-id="ecd73-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool toocarry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="ecd73-216">(Voir aussi [Clusrun pour les nœuds Linux](#Clusrun-for-Linux-nodes) dans cet article.)</span><span class="sxs-lookup"><span data-stu-id="ecd73-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="ecd73-217">Ouvrez une fenêtre Windows PowerShell, puis entrez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="ecd73-217">Open a Windows PowerShell window and enter hello following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="ecd73-218">Hello première commande crée un dossier nommé /rdma sur tous les nœuds dans le groupe de LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-218">hello first command creates a folder named /rdma on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="ecd73-219">commande deuxième Hello monte hello Azure fichier partage allvhdsjw.file.core.windows.net/rdma sur le dossier /rdma hello too777 de jeu de bits en mode dir et fichier.</span><span class="sxs-lookup"><span data-stu-id="ecd73-219">hello second command mounts hello Azure File share allvhdsjw.file.core.windows.net/rdma onto hello /rdma folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="ecd73-220">Dans la deuxième commande de hello, allvhdsje est le nom de votre compte de stockage et storageaccountkey est votre clé de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ecd73-220">In hello second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="ecd73-221">Hello »\\`« symbole dans la deuxième commande de hello est un symbole d’échappement pour PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ecd73-221">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="ecd73-222">«\\`, « signifie que hello », » (virgule) est une partie de la commande hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-222">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="ecd73-223">Partage du nœud principal</span><span class="sxs-lookup"><span data-stu-id="ecd73-223">Head node share</span></span>
<span data-ttu-id="ecd73-224">Vous pouvez également monter un dossier partagé de nœud principal de hello des nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="ecd73-224">Alternatively, mount a shared folder of hello head node on Linux nodes.</span></span> <span data-ttu-id="ecd73-225">Fournit d’un partage de fichiers tooshare hello la plus simple, mais du nœud principal de hello et tous les nœuds de Linux doivent être déployés dans hello même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="ecd73-225">A share provides hello simplest way tooshare files, but hello head node and all Linux nodes must be deployed in hello same virtual network.</span></span> <span data-ttu-id="ecd73-226">Voici les étapes hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-226">Here are hello steps.</span></span>

1. <span data-ttu-id="ecd73-227">Créez un dossier sur le nœud principal de hello et tooEveryone le partager avec des autorisations en lecture/écriture.</span><span class="sxs-lookup"><span data-stu-id="ecd73-227">Create a folder on hello head node and share it tooEveryone with Read/Write permissions.</span></span> <span data-ttu-id="ecd73-228">Par exemple, partager D:\OpenFOAM sur le nœud principal de hello en tant que \\CentOS7RDMA-HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="ecd73-228">For example, share D:\OpenFOAM on hello head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="ecd73-229">CentOS7RDMA-HN Voici hello les nom d’hôte de nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-229">Here CentOS7RDMA-HN is hello hostname of hello head node.</span></span>
   
    ![Autorisations des partages de fichiers][fileshareperms]
   
    ![Partage de fichiers][filesharing]
2. <span data-ttu-id="ecd73-232">Ouvrez une fenêtre Windows PowerShell et exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="ecd73-232">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="ecd73-233">Hello première commande crée un dossier nommé /openfoam sur tous les nœuds dans le groupe de LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-233">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="ecd73-234">commande deuxième Hello monte hello partagé dossier //CentOS7RDMA-HN/OpenFOAM sur le dossier hello avec too777 de jeu de bits en mode dir et fichier.</span><span class="sxs-lookup"><span data-stu-id="ecd73-234">hello second command mounts hello shared folder //CentOS7RDMA-HN/OpenFOAM onto hello folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="ecd73-235">Hello nom d’utilisateur et mot de passe dans la commande hello doivent être nom d’utilisateur hello et un mot de passe d’un utilisateur de cluster sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-235">hello username and password in hello command should be hello username and password of a cluster user on hello head node.</span></span> <span data-ttu-id="ecd73-236">(Consultez la page [Add or Remove Cluster Users](https://technet.microsoft.com/library/ff919330.aspx)(Ajouter ou supprimer des utilisateurs du cluster).)</span><span class="sxs-lookup"><span data-stu-id="ecd73-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="ecd73-237">Hello »\\`« symbole dans la deuxième commande de hello est un symbole d’échappement pour PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ecd73-237">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="ecd73-238">«\\`, « signifie que hello », » (virgule) est une partie de la commande hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-238">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="ecd73-239">Serveur NFS</span><span class="sxs-lookup"><span data-stu-id="ecd73-239">NFS server</span></span>
<span data-ttu-id="ecd73-240">Hello service NFS vous permet de tooshare et migrer des fichiers entre les ordinateurs exécutant le système d’exploitation de hello Windows Server 2012 à l’aide du protocole SMB de hello et basés sur Linux à l’aide du protocole NFS de hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-240">hello NFS service enables you tooshare and migrate files between computers running hello Windows Server 2012 operating system using hello SMB protocol and Linux-based computers using hello NFS protocol.</span></span> <span data-ttu-id="ecd73-241">Hello du serveur NFS et tous les autres nœuds ont toobe déployé Bonjour même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="ecd73-241">hello NFS server and all other nodes have toobe deployed in hello same virtual network.</span></span> <span data-ttu-id="ecd73-242">Il offre une meilleure compatibilité avec les nœuds Linux en comparaison d’un partage SMB.</span><span class="sxs-lookup"><span data-stu-id="ecd73-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="ecd73-243">Par exemple, il prend en charge les liaisons de fichiers.</span><span class="sxs-lookup"><span data-stu-id="ecd73-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="ecd73-244">tooinstall et configurer un serveur NFS, suivez les étapes de hello dans [serveur pour le partage premier du système de fichiers réseau de bout en bout](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecd73-244">tooinstall and set up an NFS server, follow hello steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="ecd73-245">Par exemple, créez un partage NFS nommé nfs avec hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="ecd73-245">For example, create an NFS share named nfs with hello following properties:</span></span>
   
    ![Autorisation NFS][nfsauth]
   
    ![Autorisations des partages NFS][nfsshare]
   
    ![Autorisations NTFS NFS][nfsperm]
   
    ![Propriétés de la gestion NFS][nfsmanage]
2. <span data-ttu-id="ecd73-250">Ouvrez une fenêtre Windows PowerShell et exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="ecd73-250">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="ecd73-251">Hello première commande crée un dossier nommé /nfsshared sur tous les nœuds dans le groupe de LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-251">hello first command creates a folder named /nfsshared on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="ecd73-252">deuxième commande hello de montage NFS Hello partager HN-CentOS7RDMA : / nfs sur hello dossier.</span><span class="sxs-lookup"><span data-stu-id="ecd73-252">hello second command mounts hello NFS share CentOS7RDMA-HN:/nfs onto hello folder.</span></span> <span data-ttu-id="ecd73-253">Ici HN-CentOS7RDMA : / nfs hello un chemin d’accès à distance de votre partage NFS.</span><span class="sxs-lookup"><span data-stu-id="ecd73-253">Here CentOS7RDMA-HN:/nfs is hello remote path of your NFS share.</span></span>

## <a name="how-toosubmit-jobs"></a><span data-ttu-id="ecd73-254">Comment les travaux toosubmit</span><span class="sxs-lookup"><span data-stu-id="ecd73-254">How toosubmit jobs</span></span>
<span data-ttu-id="ecd73-255">Il existe des clusters de HPC Pack toohello plusieurs façons toosubmit travaux :</span><span class="sxs-lookup"><span data-stu-id="ecd73-255">There are several ways toosubmit jobs toohello HPC Pack cluster:</span></span>

* <span data-ttu-id="ecd73-256">Gestionnaire de cluster HPC ou interface graphique utilisateur du Gestionnaire de travaux HPC</span><span class="sxs-lookup"><span data-stu-id="ecd73-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="ecd73-257">Portail web HPC</span><span class="sxs-lookup"><span data-stu-id="ecd73-257">HPC web portal</span></span>
* <span data-ttu-id="ecd73-258">API REST</span><span class="sxs-lookup"><span data-stu-id="ecd73-258">REST API</span></span>

<span data-ttu-id="ecd73-259">Soumission de travaux de cluster toohello dans Azure via le portail web HPC hello et les outils de l’interface utilisateur graphique de HPC Pack sont hello même que pour les nœuds de calcul Windows.</span><span class="sxs-lookup"><span data-stu-id="ecd73-259">Job submission toohello cluster in Azure via HPC Pack GUI tools and hello HPC web portal are hello same as for Windows compute nodes.</span></span> <span data-ttu-id="ecd73-260">Consultez [Gestionnaire de travaux HPC Pack](https://technet.microsoft.com/library/ff919691.aspx) et [comment toosubmit travaux à partir d’un ordinateur de client local](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ecd73-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How toosubmit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="ecd73-261">travaux toosubmit via hello API REST, consultez trop[création et envoi de travaux à l’aide de l’API REST Microsoft HPC Pack hello](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecd73-261">toosubmit jobs via hello REST API, refer too[Creating and Submitting Jobs by Using hello REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="ecd73-262">travaux toosubmit à partir d’un client Linux, également faire référence exemple de Python toohello Bonjour [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span><span class="sxs-lookup"><span data-stu-id="ecd73-262">toosubmit jobs from a Linux client, also refer toohello Python sample in hello [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="ecd73-263">Clusrun pour les nœuds Linux</span><span class="sxs-lookup"><span data-stu-id="ecd73-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="ecd73-264">Hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) outil peut être utilisé tooexecute les commandes des nœuds Linux via une invite de commandes ou d’un gestionnaire de Cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="ecd73-264">hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used tooexecute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="ecd73-265">Voici quelques exemples de base.</span><span class="sxs-lookup"><span data-stu-id="ecd73-265">Following are some basic examples.</span></span>

* <span data-ttu-id="ecd73-266">Afficher les noms d’utilisateur en cours sur tous les nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-266">Show current user names on all nodes in hello cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="ecd73-267">Installer hello **gdb** outil de débogage avec **yum** sur tous les nœuds hello linuxnodes groupe et redémarrez les nœuds hello après 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="ecd73-267">Install hello **gdb** debugger tool with **yum** on all nodes in hello linuxnodes group and then restart hello nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="ecd73-268">Créer un script shell afficher chaque nombre entre 1 et 10 pour une seconde sur chaque nœud de Linux dans le cluster de hello, exécuter et afficher la sortie à partir des nœuds de hello immédiatement.</span><span class="sxs-lookup"><span data-stu-id="ecd73-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in hello cluster, run it, and show output from hello nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="ecd73-269">Vous devrez peut-être toouse certains caractères d’échappement dans **clusrun** commandes.</span><span class="sxs-lookup"><span data-stu-id="ecd73-269">You might need toouse certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="ecd73-270">Comme illustré dans cet exemple, utilisez ^ un Bonjour de tooescape d’invite de commandes » > « symbole.</span><span class="sxs-lookup"><span data-stu-id="ecd73-270">As shown in this example, use ^ in a Command Prompt tooescape hello ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ecd73-271">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ecd73-271">Next steps</span></span>
* <span data-ttu-id="ecd73-272">Essayez la montée en puissance hello cluster tooa plus grand nombre de nœuds, ou une charge de travail Linux en cours d’exécution sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="ecd73-272">Try scaling up hello cluster tooa larger number of nodes, or try running a Linux workload on hello cluster.</span></span> <span data-ttu-id="ecd73-273">Pour trouver un exemple, consultez [Exécuter NAMD avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure](hpcpack-cluster-namd.md).</span><span class="sxs-lookup"><span data-stu-id="ecd73-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="ecd73-274">Essayez d’un cluster avec [prenant en charge RDMA, nécessitant de machines virtuelles](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun les charges de travail MPI.</span><span class="sxs-lookup"><span data-stu-id="ecd73-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI workloads.</span></span> <span data-ttu-id="ecd73-275">Pour trouver un exemple, consultez [Exécuter OpenFOAM avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure](hpcpack-cluster-openfoam.md).</span><span class="sxs-lookup"><span data-stu-id="ecd73-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="ecd73-276">Si vous êtes intéressé par utilisation des nœuds Linux dans un cluster de HPC Pack sur site, consultez hello [conseils TechNet](https://technet.microsoft.com/library/mt595803.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecd73-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see hello [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
