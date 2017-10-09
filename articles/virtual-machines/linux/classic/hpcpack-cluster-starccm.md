---
title: "aaaRun en étoile-CCM + avec HPC Pack sur les machines virtuelles Linux | Documents Microsoft"
description: "Déployer un cluster Microsoft HPC Pack sur Azure et exécuter un travail Star-CCM+ sur plusieurs nœuds de calcul Linux d’un réseau RDMA."
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="da0cf-103">Exécuter Star-CCM+ avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure</span><span class="sxs-lookup"><span data-stu-id="da0cf-103">Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="da0cf-104">Cet article explique comment toodeploy un Microsoft HPC Pack cluster sur Azure, exécutez un [CD-adapco STAR-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) travail sur plusieurs nœuds de calcul Linux qui sont interconnectés avec InfiniBand.</span><span class="sxs-lookup"><span data-stu-id="da0cf-104">This article shows you how toodeploy a Microsoft HPC Pack cluster on Azure and run a [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) job on multiple Linux compute nodes that are interconnected with InfiniBand.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="da0cf-105">Microsoft HPC Pack fournit des fonctionnalités toorun divers HPC à grande échelle et des applications parallèles, y compris des applications MPI sur des clusters de machines virtuelles Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="da0cf-105">Microsoft HPC Pack provides features toorun a variety of large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="da0cf-106">HPC Pack prend également en charge l’exécution d’applications Linux HPC sur les machines virtuelles de nœuds de calcul Linux déployées dans un cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="da0cf-106">HPC Pack also supports running Linux HPC applications on Linux compute-node VMs that are deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="da0cf-107">Pour une présentation de toousing Linux nœuds avec HPC Pack, consultez [prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="da0cf-107">For an introduction toousing Linux compute nodes with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="set-up-an-hpc-pack-cluster"></a><span data-ttu-id="da0cf-108">Configurer un cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="da0cf-108">Set up an HPC Pack cluster</span></span>
<span data-ttu-id="da0cf-109">Télécharger les scripts de déploiement IaaS de HPC Pack hello de hello [centre de téléchargement](https://www.microsoft.com/en-us/download/details.aspx?id=44949) et extrayez-les localement.</span><span class="sxs-lookup"><span data-stu-id="da0cf-109">Download hello HPC Pack IaaS deployment scripts from hello [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=44949) and extract them locally.</span></span>

<span data-ttu-id="da0cf-110">Azure PowerShell doit être installé et configuré.</span><span class="sxs-lookup"><span data-stu-id="da0cf-110">Azure PowerShell is a prerequisite.</span></span> <span data-ttu-id="da0cf-111">Si PowerShell n’est pas configuré sur votre ordinateur local, consultez l’article de hello [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="da0cf-111">If PowerShell is not configured on your local machine, please read hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="da0cf-112">Au moment de hello de rédaction de cet article, les images Linux hello hello Azure Marketplace (qui contient les pilotes InfiniBand hello pour Azure) sont pour SLES 12, CentOS 6.5 et CentOS 7.1.</span><span class="sxs-lookup"><span data-stu-id="da0cf-112">At hello time of this writing, hello Linux images from hello Azure Marketplace (which contains hello InfiniBand drivers for Azure) are for SLES 12, CentOS 6.5, and CentOS 7.1.</span></span> <span data-ttu-id="da0cf-113">Cet article est basé sur l’utilisation de hello de SLES 12.</span><span class="sxs-lookup"><span data-stu-id="da0cf-113">This article is based on hello usage of SLES 12.</span></span> <span data-ttu-id="da0cf-114">nom de hello tooretrieve de toutes les images Linux qui prennent en charge HPC Bonjour Marketplace, vous pouvez exécuter hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="da0cf-114">tooretrieve hello name of all Linux images that support HPC in hello Marketplace, you can run hello following PowerShell command:</span></span>

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

<span data-ttu-id="da0cf-115">le résultat de Hello affiche emplacement hello dans lequel ces images sont disponibles et nom de l’image de hello (**ImageName**) toobe utilisé dans le modèle de déploiement hello plus tard.</span><span class="sxs-lookup"><span data-stu-id="da0cf-115">hello output lists hello location in which these images are available and hello image name (**ImageName**) toobe used in hello deployment template later.</span></span>

<span data-ttu-id="da0cf-116">Avant de déployer les clusters hello, vous avez toobuild un fichier de modèle de déploiement de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="da0cf-116">Before you deploy hello cluster, you have toobuild an HPC Pack deployment template file.</span></span> <span data-ttu-id="da0cf-117">Étant donné que nous avons ciblez un petit cluster, nœud de tête hello sera contrôleur de domaine hello et héberger la base de données SQL locale.</span><span class="sxs-lookup"><span data-stu-id="da0cf-117">Because we're targeting a small cluster, hello head node will be hello domain controller and host a local SQL database.</span></span>

<span data-ttu-id="da0cf-118">Hello modèle suivant sera déployer ce type d’un nœud principal, créez un fichier XML nommé **MyCluster.xml**et remplacez les valeurs hello de **SubscriptionId**, **StorageAccount**,  **Emplacement**, **VMName**, et **ServiceName** avec les vôtres.</span><span class="sxs-lookup"><span data-stu-id="da0cf-118">hello following template will deploy such a head node, create an XML file named **MyCluster.xml**, and replace hello values of **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, and **ServiceName** with yours.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

<span data-ttu-id="da0cf-119">Démarrer la création du nœud principal et hello en exécutant la commande PowerShell de hello dans une invite de commandes avec élévation de privilèges :</span><span class="sxs-lookup"><span data-stu-id="da0cf-119">Start hello head-node creation by running hello PowerShell command in an elevated command prompt:</span></span>

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

<span data-ttu-id="da0cf-120">Après 20 minutes too30, du nœud principal hello devrait être prêt.</span><span class="sxs-lookup"><span data-stu-id="da0cf-120">After 20 too30 minutes, hello head node should be ready.</span></span> <span data-ttu-id="da0cf-121">Vous pouvez vous connecter tooit hello portail Azure en cliquant sur hello **Connect** icône de l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="da0cf-121">You can connect tooit from hello Azure portal by clicking hello **Connect** icon of hello virtual machine.</span></span>

<span data-ttu-id="da0cf-122">Vous pouvez éventuellement avoir redirecteur DNS de hello toofix.</span><span class="sxs-lookup"><span data-stu-id="da0cf-122">You might eventually have toofix hello DNS forwarder.</span></span> <span data-ttu-id="da0cf-123">toodo, démarrez le Gestionnaire DNS.</span><span class="sxs-lookup"><span data-stu-id="da0cf-123">toodo so, start DNS Manager.</span></span>

1. <span data-ttu-id="da0cf-124">Nom du serveur hello avec le bouton droit dans le Gestionnaire de DNS, sélectionnez **propriétés**, puis cliquez sur hello **redirecteurs** onglet.</span><span class="sxs-lookup"><span data-stu-id="da0cf-124">Right-click hello server name in DNS Manager, select **Properties**, and then click hello **Forwarders** tab.</span></span>
2. <span data-ttu-id="da0cf-125">Cliquez sur hello **modifier** bouton tooremove tous les redirecteurs, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="da0cf-125">Click hello **Edit** button tooremove any forwarders, and then click **OK**.</span></span>
3. <span data-ttu-id="da0cf-126">Vérifiez que hello **utiliser les indications de racine si aucune des redirecteurs ne sont disponibles** case à cocher est sélectionnée, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="da0cf-126">Make sure that hello **Use root hints if no forwarders are available** check box is selected, and then click **OK**.</span></span>

## <a name="set-up-linux-compute-nodes"></a><span data-ttu-id="da0cf-127">Créer les nœuds de calcul Linux</span><span class="sxs-lookup"><span data-stu-id="da0cf-127">Set up Linux compute nodes</span></span>
<span data-ttu-id="da0cf-128">Vous déployez des nœuds de calcul hello Linux à l’aide de hello même modèle de déploiement que vous avez utilisé le nœud principal de toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="da0cf-128">You deploy hello Linux compute nodes by using hello same deployment template that you used toocreate hello head node.</span></span>

<span data-ttu-id="da0cf-129">Copier le fichier hello **MyCluster.xml** depuis votre nœud principal de toohello ordinateur local et mise à jour hello **NodeCount** balise avec un nombre de hello de nœuds que vous souhaitez toodeploy (< = 20).</span><span class="sxs-lookup"><span data-stu-id="da0cf-129">Copy hello file **MyCluster.xml** from your local machine toohello head node, and update hello **NodeCount** tag with hello number of nodes that you want toodeploy (<=20).</span></span> <span data-ttu-id="da0cf-130">Être prudent toohave assez de cœurs disponibles dans votre quota de Azure, car chaque instance A9 consommera 16 cœurs dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="da0cf-130">Be careful toohave enough available cores in your Azure quota, because each A9 instance will consume 16 cores in your subscription.</span></span> <span data-ttu-id="da0cf-131">Vous pouvez utiliser des instances de A8 (8 cœurs) au lieu de A9 si vous souhaitez toouse davantage d’ordinateurs virtuels dans hello même budget.</span><span class="sxs-lookup"><span data-stu-id="da0cf-131">You can use A8 instances (8 cores) instead of A9 if you want toouse more VMs in hello same budget.</span></span>

<span data-ttu-id="da0cf-132">Sur le nœud principal de hello, copiez les scripts de déploiement IaaS de HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="da0cf-132">On hello head node, copy hello HPC Pack IaaS deployment scripts.</span></span>

<span data-ttu-id="da0cf-133">Exécutez hello suivant les commandes Azure PowerShell dans une invite de commandes avec élévation de privilèges :</span><span class="sxs-lookup"><span data-stu-id="da0cf-133">Run hello following Azure PowerShell commands in an elevated command prompt:</span></span>

1. <span data-ttu-id="da0cf-134">Exécutez **Add-AzureAccount** tooconnect tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="da0cf-134">Run **Add-AzureAccount** tooconnect tooyour Azure subscription.</span></span>
2. <span data-ttu-id="da0cf-135">Si vous avez plusieurs abonnements, exécutez **Get-AzureSubscription** toolist les.</span><span class="sxs-lookup"><span data-stu-id="da0cf-135">If you have multiple subscriptions, run **Get-AzureSubscription** toolist them.</span></span>
3. <span data-ttu-id="da0cf-136">Définir un abonnement par défaut en exécutant hello **Select-AzureSubscription - SubscriptionName xxxx-par défaut** commande.</span><span class="sxs-lookup"><span data-stu-id="da0cf-136">Set a default subscription by running hello **Select-AzureSubscription -SubscriptionName xxxx -Default** command.</span></span>
4. <span data-ttu-id="da0cf-137">Exécutez **.\New-HPCIaaSCluster.ps1 - ConfigFile MyCluster.xml** toostart déploiement de nœuds de calcul Linux.</span><span class="sxs-lookup"><span data-stu-id="da0cf-137">Run **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** toostart deploying Linux compute nodes.</span></span>
   
   ![Déploiement d’un nœud principal en action][hndeploy]

<span data-ttu-id="da0cf-139">Ouvrez l’outil de gestionnaire du Cluster HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="da0cf-139">Open hello HPC Pack Cluster Manager tool.</span></span> <span data-ttu-id="da0cf-140">Après quelques minutes, des nœuds de calcul Linux apparaîtront régulièrement dans la liste.</span><span class="sxs-lookup"><span data-stu-id="da0cf-140">After few minutes, Linux compute nodes will regularly appear in list of cluster compute nodes.</span></span> <span data-ttu-id="da0cf-141">Avec le mode de déploiement classique de hello, les machines virtuelles IaaS sont créés de façon séquentielle.</span><span class="sxs-lookup"><span data-stu-id="da0cf-141">With hello classic deployment mode, IaaS VMs are created sequentially.</span></span> <span data-ttu-id="da0cf-142">Par conséquent, si le nombre de hello de nœuds est important, obtention tous déployé peut prendre beaucoup de temps.</span><span class="sxs-lookup"><span data-stu-id="da0cf-142">So if hello number of nodes is important, getting them all deployed can take a significant amount of time.</span></span>

![Nœuds Linux dans le Gestionnaire de cluster de HPC Pack][clustermanager]

<span data-ttu-id="da0cf-144">Maintenant que tous les nœuds sont en cours d’exécution dans un cluster de hello, il existe une infrastructure supplémentaire paramètres toomake.</span><span class="sxs-lookup"><span data-stu-id="da0cf-144">Now that all nodes are up and running in hello cluster, there are additional infrastructure settings toomake.</span></span>

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a><span data-ttu-id="da0cf-145">Configurer un partage Azure File pour les nœuds Windows et Linux</span><span class="sxs-lookup"><span data-stu-id="da0cf-145">Set up an Azure File share for Windows and Linux nodes</span></span>
<span data-ttu-id="da0cf-146">Vous pouvez utiliser des scripts de toostore hello Azure File service, les packages d’applications et fichiers de données.</span><span class="sxs-lookup"><span data-stu-id="da0cf-146">You can use hello Azure File service toostore scripts, application packages, and data files.</span></span> <span data-ttu-id="da0cf-147">Azure File fournit des fonctionnalités CIFS en plus d’un stockage d’objets blob Azure comme magasin persistant.</span><span class="sxs-lookup"><span data-stu-id="da0cf-147">Azure File provides CIFS capabilities on top of Azure Blob storage as a persistent store.</span></span> <span data-ttu-id="da0cf-148">N’oubliez pas que cela n’est pas solution plus évolutive de hello, mais il est hello celle la plus simple et ne nécessite pas dédié de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="da0cf-148">Be aware that this is not hello most scalable solution, but it is hello simplest one and doesn’t require dedicated VMs.</span></span>

<span data-ttu-id="da0cf-149">Créer un partage de fichiers Azure en suivant les instructions de hello dans l’article de hello [prise en main avec un stockage de fichier Azure sur Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="da0cf-149">Create an Azure File share by following hello instructions in hello article [Get started with Azure File storage on Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="da0cf-150">Conservez votre compte de stockage en tant que nom hello **saname**, nom de partage de fichiers hello en tant que **nom_partage**et la clé de compte de stockage hello en tant que **sakey**.</span><span class="sxs-lookup"><span data-stu-id="da0cf-150">Keep hello name of your storage account as **saname**, hello file share name as **sharename**, and hello storage account key as **sakey**.</span></span>

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a><span data-ttu-id="da0cf-151">Partage de fichiers Azure hello de montage sur le nœud principal de hello</span><span class="sxs-lookup"><span data-stu-id="da0cf-151">Mount hello Azure File share on hello head node</span></span>
<span data-ttu-id="da0cf-152">Ouvrez une invite de commandes avec élévation de privilèges et exécutez hello suit les informations d’identification de commande toostore hello dans le coffre hello ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="da0cf-152">Open an elevated command prompt and run hello following command toostore hello credentials in hello local machine vault:</span></span>

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

<span data-ttu-id="da0cf-153">Ensuite, toomount hello Azure partage de fichiers, exécutez :</span><span class="sxs-lookup"><span data-stu-id="da0cf-153">Then, toomount hello Azure File share, run:</span></span>

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a><span data-ttu-id="da0cf-154">Monter le partage de fichiers Azure hello sur les nœuds de calcul Linux</span><span class="sxs-lookup"><span data-stu-id="da0cf-154">Mount hello Azure File share on Linux compute nodes</span></span>
<span data-ttu-id="da0cf-155">Un outil utile qui est fourni avec HPC Pack est outil de clusrun hello.</span><span class="sxs-lookup"><span data-stu-id="da0cf-155">One useful tool that comes with HPC Pack is hello clusrun tool.</span></span> <span data-ttu-id="da0cf-156">Vous pouvez utiliser cette hello toorun d’outil de ligne de commande même commande simultanément sur un ensemble de nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="da0cf-156">You can use this command-line tool toorun hello same command simultaneously on a set of compute nodes.</span></span> <span data-ttu-id="da0cf-157">Dans notre cas, il utilise le partage de fichiers Azure hello toomount et rendre persistant toosurvive redémarrages.</span><span class="sxs-lookup"><span data-stu-id="da0cf-157">In our case, it's used toomount hello Azure File share and persist it toosurvive reboots.</span></span>
<span data-ttu-id="da0cf-158">Dans une invite de commandes avec élévation de privilèges sur le nœud principal de hello, exécutez hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="da0cf-158">In an elevated command prompt on hello head node, run hello following commands.</span></span>

<span data-ttu-id="da0cf-159">répertoire de montage toocreate hello :</span><span class="sxs-lookup"><span data-stu-id="da0cf-159">toocreate hello mount directory:</span></span>

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

<span data-ttu-id="da0cf-160">hello toomount partage de fichiers Azure :</span><span class="sxs-lookup"><span data-stu-id="da0cf-160">toomount hello Azure File share:</span></span>

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

<span data-ttu-id="da0cf-161">partage de montage toopersist hello :</span><span class="sxs-lookup"><span data-stu-id="da0cf-161">toopersist hello mount share:</span></span>

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a><span data-ttu-id="da0cf-162">Installer STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="da0cf-162">Install STAR-CCM+</span></span>
<span data-ttu-id="da0cf-163">Les instances A8 et A9 de machine virtuelle Azure prennent en charge InfiniBand et les fonctionnalités RDMA.</span><span class="sxs-lookup"><span data-stu-id="da0cf-163">Azure VM instances A8 and A9 provide InfiniBand support and RDMA capabilities.</span></span> <span data-ttu-id="da0cf-164">les pilotes de noyau Hello qui permettent ces fonctionnalités sont disponibles pour Windows Server 2012 R2, SUSE 12, CentOS 6.5 et images CentOS 7.1 Bonjour Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="da0cf-164">hello kernel drivers that enable those capabilities are available for Windows Server 2012 R2, SUSE 12, CentOS 6.5, and CentOS 7.1 images in hello Azure Marketplace.</span></span> <span data-ttu-id="da0cf-165">Microsoft MPI et Intel MPI (version 5.x) sont hello deux MPI bibliothèques qui prennent en charge les pilotes compris dans Azure.</span><span class="sxs-lookup"><span data-stu-id="da0cf-165">Microsoft MPI and Intel MPI (release 5.x) are hello two MPI libraries that support those drivers in Azure.</span></span>

<span data-ttu-id="da0cf-166">CD-adapco STAR-CCM+ 11.x et version ultérieure est fourni avec Intel MPI version 5.x et prend donc en charge InfiniBand pour Azure.</span><span class="sxs-lookup"><span data-stu-id="da0cf-166">CD-adapco STAR-CCM+ release 11.x and later is bundled with Intel MPI version 5.x, so InfiniBand support for Azure is included.</span></span>

<span data-ttu-id="da0cf-167">Obtenir hello Linux64 étoile-package CCM + à partir de hello [CD-adapco portal](https://steve.cd-adapco.com).</span><span class="sxs-lookup"><span data-stu-id="da0cf-167">Get hello Linux64 STAR-CCM+ package from hello [CD-adapco portal](https://steve.cd-adapco.com).</span></span> <span data-ttu-id="da0cf-168">Dans notre cas, nous avons utilisé la version 11.02.010 en précision mixte.</span><span class="sxs-lookup"><span data-stu-id="da0cf-168">In our case, we used version 11.02.010 in mixed precision.</span></span>

<span data-ttu-id="da0cf-169">Sur le nœud principal hello, Bonjour **/hpcdata** fichier Azure partage, créez un script shell intitulé **setupstarccm.sh** avec hello suivant le contenu.</span><span class="sxs-lookup"><span data-stu-id="da0cf-169">On hello head node, in hello **/hpcdata** Azure File share, create a shell script named **setupstarccm.sh** with hello following content.</span></span> <span data-ttu-id="da0cf-170">Ce script est exécuté sur chaque tooset de nœud de calcul des ÉTOILES-CCM + localement.</span><span class="sxs-lookup"><span data-stu-id="da0cf-170">This script will be run on each compute node tooset up STAR-CCM+ locally.</span></span>

#### <a name="sample-setupstarcmsh-script"></a><span data-ttu-id="da0cf-171">Exemple de script setupstarcm.sh</span><span class="sxs-lookup"><span data-stu-id="da0cf-171">Sample setupstarcm.sh script</span></span>
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
<span data-ttu-id="da0cf-172">Maintenant, tooset d’étoile-CCM + sur tous vos Linux nœuds de calcul, ouvrez une invite de commandes avec élévation de privilèges et exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="da0cf-172">Now, tooset up STAR-CCM+ on all your Linux compute nodes, open an elevated command prompt and run hello following command:</span></span>

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

<span data-ttu-id="da0cf-173">Pendant l’exécution de la commande hello, vous pouvez surveiller l’utilisation du processeur hello à l’aide de carte thermique hello du Gestionnaire du Cluster.</span><span class="sxs-lookup"><span data-stu-id="da0cf-173">While hello command is running, you can monitor hello CPU usage by using hello heat map of Cluster Manager.</span></span> <span data-ttu-id="da0cf-174">Après quelques minutes, tous les nœuds devraient être correctement installés.</span><span class="sxs-lookup"><span data-stu-id="da0cf-174">After few minutes, all nodes should be correctly set up.</span></span>

## <a name="run-star-ccm-jobs"></a><span data-ttu-id="da0cf-175">Exécuter des travaux STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="da0cf-175">Run STAR-CCM+ jobs</span></span>
<span data-ttu-id="da0cf-176">HPC Pack est utilisé pour ses fonctionnalités de planificateur de tâche dans l’ordre toorun étoile-CCM + travaux.</span><span class="sxs-lookup"><span data-stu-id="da0cf-176">HPC Pack is used for its job scheduler capabilities in order toorun STAR-CCM+ jobs.</span></span> <span data-ttu-id="da0cf-177">toodo par conséquent, nous devons hello prise en charge de scripts certains travaux de hello toostart utilisés et exécutées en étoile-CCM +.</span><span class="sxs-lookup"><span data-stu-id="da0cf-177">toodo so, we need hello support of a few scripts that are used toostart hello job and run STAR-CCM+.</span></span> <span data-ttu-id="da0cf-178">les données d’entrée Hello sont conservées sur le partage de fichiers Azure hello premier par souci de simplicité.</span><span class="sxs-lookup"><span data-stu-id="da0cf-178">hello input data is kept on hello Azure File share first for simplicity.</span></span>

<span data-ttu-id="da0cf-179">Hello PowerShell script suivant est utilisé tooqueue une étoile-travail CCM +.</span><span class="sxs-lookup"><span data-stu-id="da0cf-179">hello following PowerShell script is used tooqueue a STAR-CCM+ job.</span></span> <span data-ttu-id="da0cf-180">Il tient compte de trois arguments :</span><span class="sxs-lookup"><span data-stu-id="da0cf-180">It takes three arguments:</span></span>

* <span data-ttu-id="da0cf-181">nom du modèle Hello</span><span class="sxs-lookup"><span data-stu-id="da0cf-181">hello model name</span></span>
* <span data-ttu-id="da0cf-182">nombre de Hello de toobe de nœuds utilisé</span><span class="sxs-lookup"><span data-stu-id="da0cf-182">hello number of nodes toobe used</span></span>
* <span data-ttu-id="da0cf-183">nombre de Hello de cœurs sur chaque toobe nœud utilisé</span><span class="sxs-lookup"><span data-stu-id="da0cf-183">hello number of cores on each node toobe used</span></span>

<span data-ttu-id="da0cf-184">Étant donné qu’étoile-CCM + peuvent remplir la bande passante de mémoire hello, ses généralement une meilleure toouse moins noyaux par les nœuds de calcul et ajouter de nouveaux nœuds.</span><span class="sxs-lookup"><span data-stu-id="da0cf-184">Because STAR-CCM+ can fill hello memory bandwidth, it's usually better toouse fewer cores per compute nodes and add new nodes.</span></span> <span data-ttu-id="da0cf-185">nombre exact de Hello de cœurs par nœud dépend de la famille de processeurs hello et la vitesse d’interconnexion hello.</span><span class="sxs-lookup"><span data-stu-id="da0cf-185">hello exact number of cores per node will depend on hello processor family and hello interconnect speed.</span></span>

<span data-ttu-id="da0cf-186">les nœuds de Hello sont allouées exclusivement pour le travail de hello et ne peut pas être partagés avec d’autres tâches.</span><span class="sxs-lookup"><span data-stu-id="da0cf-186">hello nodes are allocated exclusively for hello job and can’t be shared with other jobs.</span></span> <span data-ttu-id="da0cf-187">travail de Hello n’est pas démarré directement comme un travail MPI.</span><span class="sxs-lookup"><span data-stu-id="da0cf-187">hello job is not started as an MPI job directly.</span></span> <span data-ttu-id="da0cf-188">Hello **runstarccm.sh** script shell démarrera Lanceur MPI hello.</span><span class="sxs-lookup"><span data-stu-id="da0cf-188">hello **runstarccm.sh** shell script will start hello MPI launcher.</span></span>

<span data-ttu-id="da0cf-189">Hello d’entrée de modèle et hello **runstarccm.sh** script sont stockés dans hello **/hpcdata** partage a été précédemment chargé.</span><span class="sxs-lookup"><span data-stu-id="da0cf-189">hello input model and hello **runstarccm.sh** script are stored in hello **/hpcdata** share that was previously mounted.</span></span>

<span data-ttu-id="da0cf-190">Les fichiers journaux sont nommés avec l’ID de tâche hello et sont stockées dans hello **/hpcdata partage**, ainsi que de hello étoile-CCM + fichiers de sortie.</span><span class="sxs-lookup"><span data-stu-id="da0cf-190">Log files are named with hello job ID and are stored in hello **/hpcdata share**, along with hello STAR-CCM+ output files.</span></span>

#### <a name="sample-submitstarccmjobps1-script"></a><span data-ttu-id="da0cf-191">Exemple de script SubmitStarccmJob.ps1</span><span class="sxs-lookup"><span data-stu-id="da0cf-191">Sample SubmitStarccmJob.ps1 script</span></span>
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
<span data-ttu-id="da0cf-192">Remplacez le **runner.java** par le lanceur de modèle Java STAR-CCM+ de votre choix et votre code de journalisation.</span><span class="sxs-lookup"><span data-stu-id="da0cf-192">Replace **runner.java** with your preferred STAR-CCM+ Java model launcher and logging code.</span></span>

#### <a name="sample-runstarccmsh-script"></a><span data-ttu-id="da0cf-193">Exemple de script runstarccm.sh</span><span class="sxs-lookup"><span data-stu-id="da0cf-193">Sample runstarccm.sh script</span></span>
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

<span data-ttu-id="da0cf-194">Dans notre test, nous avons utilisé un jeton de licence Power-On-Demand,</span><span class="sxs-lookup"><span data-stu-id="da0cf-194">In our test, we used a Power-On-Demand license token.</span></span> <span data-ttu-id="da0cf-195">Pour ce jeton, vous avez tooset hello **$CDLMD_LICENSE_FILE** variable d’environnement trop **1999@flex.cd-adapco.com**  et la clé hello Bonjour **- podkey** option de ligne de commande hello .</span><span class="sxs-lookup"><span data-stu-id="da0cf-195">For that token, you have tooset hello **$CDLMD_LICENSE_FILE** environment variable too**1999@flex.cd-adapco.com** and hello key in hello **-podkey** option of hello command line.</span></span>

<span data-ttu-id="da0cf-196">Après une initialisation, le script de hello extrait--hello **$CCP_NODES_CORES** variables d’environnement HPC Pack définir--hello liste de toobuild nœuds un fichier d’hôte qui hello Lanceur de MPI utilise.</span><span class="sxs-lookup"><span data-stu-id="da0cf-196">After some initialization, hello script extracts--from hello **$CCP_NODES_CORES** environment variables that HPC Pack set--hello list of nodes toobuild a hostfile that hello MPI launcher uses.</span></span> <span data-ttu-id="da0cf-197">Ce fichier d’hôte doit contenir une liste de hello des noms de nœud de calcul qui sont utilisés pour la tâche hello, un nom par ligne.</span><span class="sxs-lookup"><span data-stu-id="da0cf-197">This hostfile will contain hello list of compute node names that are used for hello job, one name per line.</span></span>

<span data-ttu-id="da0cf-198">format Hello de **$CCP_NODES_CORES** suit ce modèle :</span><span class="sxs-lookup"><span data-stu-id="da0cf-198">hello format of **$CCP_NODES_CORES** follows this pattern:</span></span>

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

<span data-ttu-id="da0cf-199">Où :</span><span class="sxs-lookup"><span data-stu-id="da0cf-199">Where:</span></span>

* <span data-ttu-id="da0cf-200">`<Number of nodes>`est nombre hello de nœuds allouée toothis travail.</span><span class="sxs-lookup"><span data-stu-id="da0cf-200">`<Number of nodes>` is hello number of nodes allocated toothis job.</span></span>
* <span data-ttu-id="da0cf-201">`<Name of node_n_...>`est le nom hello de chaque nœud allouée toothis travail.</span><span class="sxs-lookup"><span data-stu-id="da0cf-201">`<Name of node_n_...>` is hello name of each node allocated toothis job.</span></span>
* <span data-ttu-id="da0cf-202">`<Cores of node_n_...>`est nombre hello de cœurs sur le nœud hello allouée toothis travail.</span><span class="sxs-lookup"><span data-stu-id="da0cf-202">`<Cores of node_n_...>` is hello number of cores on hello node allocated toothis job.</span></span>

<span data-ttu-id="da0cf-203">Hello du nombre de cœurs (**$NBCORES**) est également calculée hello en fonction de nombre de nœuds (**$NBNODES**) et le nombre de hello de cœurs par nœud (fourni comme paramètre **$NBCORESPERNODE**).</span><span class="sxs-lookup"><span data-stu-id="da0cf-203">hello number of cores (**$NBCORES**) is also calculated based on hello number of nodes (**$NBNODES**) and hello number of cores per node (provided as parameter **$NBCORESPERNODE**).</span></span>

<span data-ttu-id="da0cf-204">Pour les options de MPI hello, hello ceux qui sont utilisés avec MPI Intel sur Azure sont :</span><span class="sxs-lookup"><span data-stu-id="da0cf-204">For hello MPI options, hello ones that are used with Intel MPI on Azure are:</span></span>

* <span data-ttu-id="da0cf-205">`-mpi intel`toospecify Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="da0cf-205">`-mpi intel` toospecify Intel MPI.</span></span>
* <span data-ttu-id="da0cf-206">`-fabric UDAPL`verbes toouse InfiniBand de Azure.</span><span class="sxs-lookup"><span data-stu-id="da0cf-206">`-fabric UDAPL` toouse Azure InfiniBand verbs.</span></span>
* <span data-ttu-id="da0cf-207">`-cpubind bandwidth,v`la bande passante toooptimize pour MPI avec étoile-CCM +.</span><span class="sxs-lookup"><span data-stu-id="da0cf-207">`-cpubind bandwidth,v` toooptimize bandwidth for MPI with STAR-CCM+.</span></span>
* <span data-ttu-id="da0cf-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`toomake Intel MPI fonctionnent avec Azure InfiniBand et tooset hello nécessaire le nombre de cœurs par nœud.</span><span class="sxs-lookup"><span data-stu-id="da0cf-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` toomake Intel MPI work with Azure InfiniBand, and tooset hello required number of cores per node.</span></span>
* <span data-ttu-id="da0cf-209">`-batch`toostart en étoile-CCM + en mode batch sans interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="da0cf-209">`-batch` toostart STAR-CCM+ in batch mode with no UI.</span></span>

<span data-ttu-id="da0cf-210">Enfin, toostart un travail, assurez-vous que vos nœuds sont en cours d’exécution et en ligne dans le Gestionnaire du Cluster.</span><span class="sxs-lookup"><span data-stu-id="da0cf-210">Finally, toostart a job, make sure that your nodes are up and running and are online in Cluster Manager.</span></span> <span data-ttu-id="da0cf-211">Puis, dans une invite de commandes PowerShell, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="da0cf-211">Then from a PowerShell command prompt, run this:</span></span>

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a><span data-ttu-id="da0cf-212">Arrêter les nœuds</span><span class="sxs-lookup"><span data-stu-id="da0cf-212">Stop nodes</span></span>
<span data-ttu-id="da0cf-213">Une fois que vous avez terminé avec vos tests, vous pouvez utiliser hello suivant HPC Pack PowerShell commandes toostop et démarrer les nœuds :</span><span class="sxs-lookup"><span data-stu-id="da0cf-213">Later on, after you're done with your tests, you can use hello following HPC Pack PowerShell commands toostop and start nodes:</span></span>

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a><span data-ttu-id="da0cf-214">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="da0cf-214">Next steps</span></span>
<span data-ttu-id="da0cf-215">Essayez d’exécuter d’autres charges de travail Linux,</span><span class="sxs-lookup"><span data-stu-id="da0cf-215">Try running other Linux workloads.</span></span> <span data-ttu-id="da0cf-216">par exemple :</span><span class="sxs-lookup"><span data-stu-id="da0cf-216">For example, see:</span></span>

* [<span data-ttu-id="da0cf-217">Exécution de NAMD avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="da0cf-217">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
* [<span data-ttu-id="da0cf-218">Exécuter OpenFOAM avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure</span><span class="sxs-lookup"><span data-stu-id="da0cf-218">Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
