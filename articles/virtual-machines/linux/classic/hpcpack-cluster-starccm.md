---
title: "Exécuter Star-CCM+ avec HPC Pack sur des machines virtuelles Linux | Microsoft Docs"
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
ms.openlocfilehash: b45fcfb981287035da02fda62eaf5f9436ec2379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="9b38d-103">Exécuter Star-CCM+ avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure</span><span class="sxs-lookup"><span data-stu-id="9b38d-103">Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="9b38d-104">Cet article vous explique comment déployer un cluster Microsoft HPC Pack sur Azure et exécuter un travail [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) sur plusieurs nœuds de calcul Linux interconnectés avec InfiniBand.</span><span class="sxs-lookup"><span data-stu-id="9b38d-104">This article shows you how to deploy a Microsoft HPC Pack cluster on Azure and run a [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) job on multiple Linux compute nodes that are interconnected with InfiniBand.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="9b38d-105">Microsoft HPC Pack fournit des fonctionnalités permettant d’exécuter un éventail d’applications HPC à grande échelle et parallèles, y compris des applications MPI, sur des clusters de machines virtuelles Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9b38d-105">Microsoft HPC Pack provides features to run a variety of large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="9b38d-106">HPC Pack prend également en charge l’exécution d’applications Linux HPC sur les machines virtuelles de nœuds de calcul Linux déployées dans un cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="9b38d-106">HPC Pack also supports running Linux HPC applications on Linux compute-node VMs that are deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="9b38d-107">Pour une présentation de l’utilisation des nœuds de calcul Linux avec HPC Pack, consultez l’article [Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="9b38d-107">For an introduction to using Linux compute nodes with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="set-up-an-hpc-pack-cluster"></a><span data-ttu-id="9b38d-108">Configurer un cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="9b38d-108">Set up an HPC Pack cluster</span></span>
<span data-ttu-id="9b38d-109">Téléchargez les scripts de déploiement IaaS de HPC Pack à partir du [Centre de téléchargement](https://www.microsoft.com/en-us/download/details.aspx?id=44949) et extrayez-les localement.</span><span class="sxs-lookup"><span data-stu-id="9b38d-109">Download the HPC Pack IaaS deployment scripts from the [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=44949) and extract them locally.</span></span>

<span data-ttu-id="9b38d-110">Azure PowerShell doit être installé et configuré.</span><span class="sxs-lookup"><span data-stu-id="9b38d-110">Azure PowerShell is a prerequisite.</span></span> <span data-ttu-id="9b38d-111">Si le logiciel PowerShell n’est pas configuré sur votre ordinateur local, consultez l’article [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9b38d-111">If PowerShell is not configured on your local machine, please read the article [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="9b38d-112">Lors de la rédaction de cet article, les images Linux d’Azure Marketplace (qui contient les pilotes InfiniBand pour Azure) correspondent à SLES 12, CentOS 6.5 et CentOS 7.1.</span><span class="sxs-lookup"><span data-stu-id="9b38d-112">At the time of this writing, the Linux images from the Azure Marketplace (which contains the InfiniBand drivers for Azure) are for SLES 12, CentOS 6.5, and CentOS 7.1.</span></span> <span data-ttu-id="9b38d-113">Cet article utilise SLES 12.</span><span class="sxs-lookup"><span data-stu-id="9b38d-113">This article is based on the usage of SLES 12.</span></span> <span data-ttu-id="9b38d-114">Pour récupérer le nom de toutes les images Linux prenant en charge HPC dans le Marketplace, exécutez la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="9b38d-114">To retrieve the name of all Linux images that support HPC in the Marketplace, you can run the following PowerShell command:</span></span>

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

<span data-ttu-id="9b38d-115">La sortie indique l’emplacement où ces images sont disponibles et le nom d’image (**ImageName**) à utiliser ultérieurement dans le modèle de déploiement.</span><span class="sxs-lookup"><span data-stu-id="9b38d-115">The output lists the location in which these images are available and the image name (**ImageName**) to be used in the deployment template later.</span></span>

<span data-ttu-id="9b38d-116">Avant de déployer le cluster, vous devez générer un fichier modèle de déploiement de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="9b38d-116">Before you deploy the cluster, you have to build an HPC Pack deployment template file.</span></span> <span data-ttu-id="9b38d-117">Comme notre cluster cible est de taille modeste, le nœud principal est le contrôleur de domaine et héberge une base de données SQL locale.</span><span class="sxs-lookup"><span data-stu-id="9b38d-117">Because we're targeting a small cluster, the head node will be the domain controller and host a local SQL database.</span></span>

<span data-ttu-id="9b38d-118">Le modèle ci-dessous déploie un nœud principal, crée le fichier XML **MyCluster.xml** et remplace les valeurs de **SubscriptionId**, **StorageAccount**, **Location**, **VMName** et **ServiceName** par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="9b38d-118">The following template will deploy such a head node, create an XML file named **MyCluster.xml**, and replace the values of **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, and **ServiceName** with yours.</span></span>

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

<span data-ttu-id="9b38d-119">Lancez la création du nœud principal en exécutant la commande PowerShell dans une invite de commandes avec élévation de privilèges :</span><span class="sxs-lookup"><span data-stu-id="9b38d-119">Start the head-node creation by running the PowerShell command in an elevated command prompt:</span></span>

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

<span data-ttu-id="9b38d-120">Le nœud principal devrait être prêt au bout de 20 à 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="9b38d-120">After 20 to 30 minutes, the head node should be ready.</span></span> <span data-ttu-id="9b38d-121">Vous pouvez vous y connecter à partir du portail Azure en cliquant sur l’icône **Connecter** de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9b38d-121">You can connect to it from the Azure portal by clicking the **Connect** icon of the virtual machine.</span></span>

<span data-ttu-id="9b38d-122">Vous devrez peut-être corriger le redirecteur DNS.</span><span class="sxs-lookup"><span data-stu-id="9b38d-122">You might eventually have to fix the DNS forwarder.</span></span> <span data-ttu-id="9b38d-123">Pour ce faire, démarrez le Gestionnaire DNS.</span><span class="sxs-lookup"><span data-stu-id="9b38d-123">To do so, start DNS Manager.</span></span>

1. <span data-ttu-id="9b38d-124">Cliquez avec le bouton droit sur le nom du serveur dans le Gestionnaire DNS, sélectionnez **Propriétés**, puis cliquez sur l’onglet **Redirecteurs**.</span><span class="sxs-lookup"><span data-stu-id="9b38d-124">Right-click the server name in DNS Manager, select **Properties**, and then click the **Forwarders** tab.</span></span>
2. <span data-ttu-id="9b38d-125">Cliquez sur le bouton **Modifier** pour supprimer tous les redirecteurs, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b38d-125">Click the **Edit** button to remove any forwarders, and then click **OK**.</span></span>
3. <span data-ttu-id="9b38d-126">Vérifiez que la case **Utiliser les indications de racine si aucun redirecteur n’est disponible** est cochée et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b38d-126">Make sure that the **Use root hints if no forwarders are available** check box is selected, and then click **OK**.</span></span>

## <a name="set-up-linux-compute-nodes"></a><span data-ttu-id="9b38d-127">Créer les nœuds de calcul Linux</span><span class="sxs-lookup"><span data-stu-id="9b38d-127">Set up Linux compute nodes</span></span>
<span data-ttu-id="9b38d-128">Pour déployer les nœuds de calcul Linux, utilisez le même modèle de déploiement que vous avez utilisé pour créer le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="9b38d-128">You deploy the Linux compute nodes by using the same deployment template that you used to create the head node.</span></span>

<span data-ttu-id="9b38d-129">Copiez le fichier **MyCluster.xml** de votre ordinateur local vers le nœud principal et modifiez la balise **NodeCount** en fonction du nombre de nœuds à déployer (<= 20).</span><span class="sxs-lookup"><span data-stu-id="9b38d-129">Copy the file **MyCluster.xml** from your local machine to the head node, and update the **NodeCount** tag with the number of nodes that you want to deploy (<=20).</span></span> <span data-ttu-id="9b38d-130">Veillez à avoir un nombre suffisant de cœurs dans votre quota Azure, car chaque instance A9 consomme 16 cœurs dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="9b38d-130">Be careful to have enough available cores in your Azure quota, because each A9 instance will consume 16 cores in your subscription.</span></span> <span data-ttu-id="9b38d-131">Vous pouvez utiliser des instances A8 (8 cœurs) au lieu d’instances A9, si vous souhaitez utiliser davantage de machines virtuelles avec le même budget.</span><span class="sxs-lookup"><span data-stu-id="9b38d-131">You can use A8 instances (8 cores) instead of A9 if you want to use more VMs in the same budget.</span></span>

<span data-ttu-id="9b38d-132">Sur le nœud principal, copiez les scripts de déploiement IaaS de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="9b38d-132">On the head node, copy the HPC Pack IaaS deployment scripts.</span></span>

<span data-ttu-id="9b38d-133">Exécutez les commandes Azure PowerShell suivantes dans une invite de commandes avec élévation de privilèges :</span><span class="sxs-lookup"><span data-stu-id="9b38d-133">Run the following Azure PowerShell commands in an elevated command prompt:</span></span>

1. <span data-ttu-id="9b38d-134">Exécutez **Add-AzureAccount** pour vous connecter à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="9b38d-134">Run **Add-AzureAccount** to connect to your Azure subscription.</span></span>
2. <span data-ttu-id="9b38d-135">Si vous avez plusieurs abonnements, exécutez **Get-AzureSubscription** pour les afficher.</span><span class="sxs-lookup"><span data-stu-id="9b38d-135">If you have multiple subscriptions, run **Get-AzureSubscription** to list them.</span></span>
3. <span data-ttu-id="9b38d-136">Définissez l’abonnement par défaut en exécutant la commande **Select-AzureSubscription -SubscriptionName xxxx-Default** .</span><span class="sxs-lookup"><span data-stu-id="9b38d-136">Set a default subscription by running the **Select-AzureSubscription -SubscriptionName xxxx -Default** command.</span></span>
4. <span data-ttu-id="9b38d-137">Exécutez **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** pour commencer à déployer les nœuds de calcul Linux.</span><span class="sxs-lookup"><span data-stu-id="9b38d-137">Run **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** to start deploying Linux compute nodes.</span></span>
   
   ![Déploiement d’un nœud principal en action][hndeploy]

<span data-ttu-id="9b38d-139">Ouvrez le Gestionnaire de cluster de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="9b38d-139">Open the HPC Pack Cluster Manager tool.</span></span> <span data-ttu-id="9b38d-140">Après quelques minutes, des nœuds de calcul Linux apparaîtront régulièrement dans la liste.</span><span class="sxs-lookup"><span data-stu-id="9b38d-140">After few minutes, Linux compute nodes will regularly appear in list of cluster compute nodes.</span></span> <span data-ttu-id="9b38d-141">En mode de déploiement classique, les machines virtuelles IaaS sont créées de manière séquentielle.</span><span class="sxs-lookup"><span data-stu-id="9b38d-141">With the classic deployment mode, IaaS VMs are created sequentially.</span></span> <span data-ttu-id="9b38d-142">Par conséquent, si le nombre de nœuds est important, le déploiement de l’ensemble des nœuds peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="9b38d-142">So if the number of nodes is important, getting them all deployed can take a significant amount of time.</span></span>

![Nœuds Linux dans le Gestionnaire de cluster de HPC Pack][clustermanager]

<span data-ttu-id="9b38d-144">Maintenant que tous les nœuds sont opérationnels dans le cluster, il reste quelques opérations de configuration de l’infrastructure à effectuer.</span><span class="sxs-lookup"><span data-stu-id="9b38d-144">Now that all nodes are up and running in the cluster, there are additional infrastructure settings to make.</span></span>

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a><span data-ttu-id="9b38d-145">Configurer un partage Azure File pour les nœuds Windows et Linux</span><span class="sxs-lookup"><span data-stu-id="9b38d-145">Set up an Azure File share for Windows and Linux nodes</span></span>
<span data-ttu-id="9b38d-146">Vous pouvez utiliser le service Azure File pour stocker les scripts, les packages d’applications et les fichiers de données.</span><span class="sxs-lookup"><span data-stu-id="9b38d-146">You can use the Azure File service to store scripts, application packages, and data files.</span></span> <span data-ttu-id="9b38d-147">Azure File fournit des fonctionnalités CIFS en plus d’un stockage d’objets blob Azure comme magasin persistant.</span><span class="sxs-lookup"><span data-stu-id="9b38d-147">Azure File provides CIFS capabilities on top of Azure Blob storage as a persistent store.</span></span> <span data-ttu-id="9b38d-148">Sachez que ce n’est pas la solution la plus évolutive, mais c’est la plus simple et elle ne nécessite aucune machine virtuelle dédiée.</span><span class="sxs-lookup"><span data-stu-id="9b38d-148">Be aware that this is not the most scalable solution, but it is the simplest one and doesn’t require dedicated VMs.</span></span>

<span data-ttu-id="9b38d-149">Créez un partage Azure File en suivant les instructions fournies dans l’article [Prise en main d’Azure File Storage sur Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="9b38d-149">Create an Azure File share by following the instructions in the article [Get started with Azure File storage on Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="9b38d-150">Conservez le nom de votre compte de stockage **saname**, le nom du partage de fichiers **sharename** et la clé du compte de stockage **sakey**.</span><span class="sxs-lookup"><span data-stu-id="9b38d-150">Keep the name of your storage account as **saname**, the file share name as **sharename**, and the storage account key as **sakey**.</span></span>

### <a name="mount-the-azure-file-share-on-the-head-node"></a><span data-ttu-id="9b38d-151">Montage du partage Azure File sur le nœud principal</span><span class="sxs-lookup"><span data-stu-id="9b38d-151">Mount the Azure File share on the head node</span></span>
<span data-ttu-id="9b38d-152">Ouvrez une invite de commandes avec élévation de privilèges et exécutez la commande suivante pour stocker les informations d’identification dans le coffre de l’ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="9b38d-152">Open an elevated command prompt and run the following command to store the credentials in the local machine vault:</span></span>

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

<span data-ttu-id="9b38d-153">Puis, pour monter le partage Azure File, exécutez :</span><span class="sxs-lookup"><span data-stu-id="9b38d-153">Then, to mount the Azure File share, run:</span></span>

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-the-azure-file-share-on-linux-compute-nodes"></a><span data-ttu-id="9b38d-154">Montage du partage Azure File sur les nœuds de calcul Linux</span><span class="sxs-lookup"><span data-stu-id="9b38d-154">Mount the Azure File share on Linux compute nodes</span></span>
<span data-ttu-id="9b38d-155">L’utilitaire clusrun, fourni avec HPC Pack, est particulièrement utile.</span><span class="sxs-lookup"><span data-stu-id="9b38d-155">One useful tool that comes with HPC Pack is the clusrun tool.</span></span> <span data-ttu-id="9b38d-156">Cet outil de ligne de commande vous permet d’exécuter la même commande simultanément sur plusieurs nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="9b38d-156">You can use this command-line tool to run the same command simultaneously on a set of compute nodes.</span></span> <span data-ttu-id="9b38d-157">Dans notre cas, il est utilisé pour monter le partage Azure File et le rendre persistant aux redémarrages.</span><span class="sxs-lookup"><span data-stu-id="9b38d-157">In our case, it's used to mount the Azure File share and persist it to survive reboots.</span></span>
<span data-ttu-id="9b38d-158">Exécutez les commandes suivantes dans une invite de commandes avec élévation de privilèges sur le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="9b38d-158">In an elevated command prompt on the head node, run the following commands.</span></span>

<span data-ttu-id="9b38d-159">Pour créer le répertoire du point de montage :</span><span class="sxs-lookup"><span data-stu-id="9b38d-159">To create the mount directory:</span></span>

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

<span data-ttu-id="9b38d-160">Pour monter le partage Azure File :</span><span class="sxs-lookup"><span data-stu-id="9b38d-160">To mount the Azure File share:</span></span>

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

<span data-ttu-id="9b38d-161">Pour rendre le partage permanent :</span><span class="sxs-lookup"><span data-stu-id="9b38d-161">To persist the mount share:</span></span>

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a><span data-ttu-id="9b38d-162">Installer STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="9b38d-162">Install STAR-CCM+</span></span>
<span data-ttu-id="9b38d-163">Les instances A8 et A9 de machine virtuelle Azure prennent en charge InfiniBand et les fonctionnalités RDMA.</span><span class="sxs-lookup"><span data-stu-id="9b38d-163">Azure VM instances A8 and A9 provide InfiniBand support and RDMA capabilities.</span></span> <span data-ttu-id="9b38d-164">Les pilotes de noyau qui mettent en œuvre ces fonctionnalités sont disponibles pour les images Windows Server 2012 R2, SUSE 12, CentOS 6.5 et CentOS 7.1 dans Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="9b38d-164">The kernel drivers that enable those capabilities are available for Windows Server 2012 R2, SUSE 12, CentOS 6.5, and CentOS 7.1 images in the Azure Marketplace.</span></span> <span data-ttu-id="9b38d-165">Microsoft MPI et Intel MPI (version 5.x) sont les deux bibliothèques MPI qui prennent en charge ces pilotes dans Azure.</span><span class="sxs-lookup"><span data-stu-id="9b38d-165">Microsoft MPI and Intel MPI (release 5.x) are the two MPI libraries that support those drivers in Azure.</span></span>

<span data-ttu-id="9b38d-166">CD-adapco STAR-CCM+ 11.x et version ultérieure est fourni avec Intel MPI version 5.x et prend donc en charge InfiniBand pour Azure.</span><span class="sxs-lookup"><span data-stu-id="9b38d-166">CD-adapco STAR-CCM+ release 11.x and later is bundled with Intel MPI version 5.x, so InfiniBand support for Azure is included.</span></span>

<span data-ttu-id="9b38d-167">Récupérez le package Linux64 STAR-CCM+ sur le [portail CD-adapco](https://steve.cd-adapco.com).</span><span class="sxs-lookup"><span data-stu-id="9b38d-167">Get the Linux64 STAR-CCM+ package from the [CD-adapco portal](https://steve.cd-adapco.com).</span></span> <span data-ttu-id="9b38d-168">Dans notre cas, nous avons utilisé la version 11.02.010 en précision mixte.</span><span class="sxs-lookup"><span data-stu-id="9b38d-168">In our case, we used version 11.02.010 in mixed precision.</span></span>

<span data-ttu-id="9b38d-169">Sur le nœud principal, dans le partage Azure File **/hpcdata**, créez un script shell intitulé **setupstarccm.sh** avec le contenu suivant.</span><span class="sxs-lookup"><span data-stu-id="9b38d-169">On the head node, in the **/hpcdata** Azure File share, create a shell script named **setupstarccm.sh** with the following content.</span></span> <span data-ttu-id="9b38d-170">Ce script s’exécutera sur chaque nœud de calcul pour configurer STAR-CCM+ localement.</span><span class="sxs-lookup"><span data-stu-id="9b38d-170">This script will be run on each compute node to set up STAR-CCM+ locally.</span></span>

#### <a name="sample-setupstarcmsh-script"></a><span data-ttu-id="9b38d-171">Exemple de script setupstarcm.sh</span><span class="sxs-lookup"><span data-stu-id="9b38d-171">Sample setupstarcm.sh script</span></span>
```
    #!/bin/bash
    # setupstarcm.sh to set up STAR-CCM+ locally

    # Create the CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy the STAR-CCM package from the file share to the local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract the package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without the FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
<span data-ttu-id="9b38d-172">Maintenant, pour installer Star-CCM+ sur tous vos nœuds de calcul Linux, ouvrez une invite de commandes avec élévation de privilèges et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9b38d-172">Now, to set up STAR-CCM+ on all your Linux compute nodes, open an elevated command prompt and run the following command:</span></span>

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

<span data-ttu-id="9b38d-173">Pendant l’exécution de la commande, vous pouvez surveiller l’utilisation du processeur à l’aide de la carte thermique du Gestionnaire de cluster.</span><span class="sxs-lookup"><span data-stu-id="9b38d-173">While the command is running, you can monitor the CPU usage by using the heat map of Cluster Manager.</span></span> <span data-ttu-id="9b38d-174">Après quelques minutes, tous les nœuds devraient être correctement installés.</span><span class="sxs-lookup"><span data-stu-id="9b38d-174">After few minutes, all nodes should be correctly set up.</span></span>

## <a name="run-star-ccm-jobs"></a><span data-ttu-id="9b38d-175">Exécuter des travaux STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="9b38d-175">Run STAR-CCM+ jobs</span></span>
<span data-ttu-id="9b38d-176">HPC Pack est utilisé pour ses fonctionnalités de planificateur afin d’exécuter des travaux Star-CCM+.</span><span class="sxs-lookup"><span data-stu-id="9b38d-176">HPC Pack is used for its job scheduler capabilities in order to run STAR-CCM+ jobs.</span></span> <span data-ttu-id="9b38d-177">Pour ce faire, nous avons besoin de prendre en charge les quelques scripts utilisés pour démarrer le travail et exécuter Star-CCM+.</span><span class="sxs-lookup"><span data-stu-id="9b38d-177">To do so, we need the support of a few scripts that are used to start the job and run STAR-CCM+.</span></span> <span data-ttu-id="9b38d-178">Pour plus de simplicité, les données d’entrée sont d’abord conservées sur le partage Azure File.</span><span class="sxs-lookup"><span data-stu-id="9b38d-178">The input data is kept on the Azure File share first for simplicity.</span></span>

<span data-ttu-id="9b38d-179">Le script PowerShell suivant est utilisé pour mettre en attente un travail Star-CCM+.</span><span class="sxs-lookup"><span data-stu-id="9b38d-179">The following PowerShell script is used to queue a STAR-CCM+ job.</span></span> <span data-ttu-id="9b38d-180">Il tient compte de trois arguments :</span><span class="sxs-lookup"><span data-stu-id="9b38d-180">It takes three arguments:</span></span>

* <span data-ttu-id="9b38d-181">Le nom du modèle</span><span class="sxs-lookup"><span data-stu-id="9b38d-181">The model name</span></span>
* <span data-ttu-id="9b38d-182">Le nombre de nœuds à utiliser</span><span class="sxs-lookup"><span data-stu-id="9b38d-182">The number of nodes to be used</span></span>
* <span data-ttu-id="9b38d-183">Le nombre de cœurs sur chaque nœud à utiliser</span><span class="sxs-lookup"><span data-stu-id="9b38d-183">The number of cores on each node to be used</span></span>

<span data-ttu-id="9b38d-184">Comme Star-CCM+ peut saturer la bande passante de mémoire, il vaut mieux utiliser moins de cœurs par nœud de calcul et ajouter de nouveaux nœuds.</span><span class="sxs-lookup"><span data-stu-id="9b38d-184">Because STAR-CCM+ can fill the memory bandwidth, it's usually better to use fewer cores per compute nodes and add new nodes.</span></span> <span data-ttu-id="9b38d-185">Le nombre exact de cœurs par nœud dépend de la gamme de processeurs et de la vitesse d’interconnexion.</span><span class="sxs-lookup"><span data-stu-id="9b38d-185">The exact number of cores per node will depend on the processor family and the interconnect speed.</span></span>

<span data-ttu-id="9b38d-186">Les nœuds sont alloués exclusivement au travail et ne peuvent pas être partagés avec d’autres travaux.</span><span class="sxs-lookup"><span data-stu-id="9b38d-186">The nodes are allocated exclusively for the job and can’t be shared with other jobs.</span></span> <span data-ttu-id="9b38d-187">Le travail n’est pas directement démarré comme un travail MPI.</span><span class="sxs-lookup"><span data-stu-id="9b38d-187">The job is not started as an MPI job directly.</span></span> <span data-ttu-id="9b38d-188">Le script shell **runstarccm.sh** permet de démarrer le lanceur MPI.</span><span class="sxs-lookup"><span data-stu-id="9b38d-188">The **runstarccm.sh** shell script will start the MPI launcher.</span></span>

<span data-ttu-id="9b38d-189">Le modèle d’entrée et le script **runstarccm.sh** sont stockés dans le partage **/hpcdata** précédemment monté.</span><span class="sxs-lookup"><span data-stu-id="9b38d-189">The input model and the **runstarccm.sh** script are stored in the **/hpcdata** share that was previously mounted.</span></span>

<span data-ttu-id="9b38d-190">Les fichiers journaux sont nommés d’après l’ID du travail et stockés dans le **partage /hpcdata**avec les fichiers de sortie STAR-CCM+.</span><span class="sxs-lookup"><span data-stu-id="9b38d-190">Log files are named with the job ID and are stored in the **/hpcdata share**, along with the STAR-CCM+ output files.</span></span>

#### <a name="sample-submitstarccmjobps1-script"></a><span data-ttu-id="9b38d-191">Exemple de script SubmitStarccmJob.ps1</span><span class="sxs-lookup"><span data-stu-id="9b38d-191">Sample SubmitStarccmJob.ps1 script</span></span>
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us the job ID that's used to identify the name of the uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit the job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
<span data-ttu-id="9b38d-192">Remplacez le **runner.java** par le lanceur de modèle Java STAR-CCM+ de votre choix et votre code de journalisation.</span><span class="sxs-lookup"><span data-stu-id="9b38d-192">Replace **runner.java** with your preferred STAR-CCM+ Java model launcher and logging code.</span></span>

#### <a name="sample-runstarccmsh-script"></a><span data-ttu-id="9b38d-193">Exemple de script runstarccm.sh</span><span class="sxs-lookup"><span data-stu-id="9b38d-193">Sample runstarccm.sh script</span></span>
```
    #!/bin/bash
    echo "start"
    # The path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set the mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create the hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into the hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with the hostfile argument
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

<span data-ttu-id="9b38d-194">Dans notre test, nous avons utilisé un jeton de licence Power-On-Demand,</span><span class="sxs-lookup"><span data-stu-id="9b38d-194">In our test, we used a Power-On-Demand license token.</span></span> <span data-ttu-id="9b38d-195">dont vous devez définir la variable d’environnement **$CDLMD_LICENSE_FILE** sur **1999@flex.cd-adapco.com** et la clé dans l’option **-podkey** de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="9b38d-195">For that token, you have to set the **$CDLMD_LICENSE_FILE** environment variable to **1999@flex.cd-adapco.com** and the key in the **-podkey** option of the command line.</span></span>

<span data-ttu-id="9b38d-196">Après une phase d’initialisation, le script extrait, à partir des variables d’environnement **$CCP_NODES_CORES** définies par HPC Pack, la liste des nœuds permettant de générer un fichier d’hôte utilisé par le lanceur MPI.</span><span class="sxs-lookup"><span data-stu-id="9b38d-196">After some initialization, the script extracts--from the **$CCP_NODES_CORES** environment variables that HPC Pack set--the list of nodes to build a hostfile that the MPI launcher uses.</span></span> <span data-ttu-id="9b38d-197">Ce fichier d’hôte contient la liste des noms de nœuds de calcul utilisés pour le travail (un nom par ligne).</span><span class="sxs-lookup"><span data-stu-id="9b38d-197">This hostfile will contain the list of compute node names that are used for the job, one name per line.</span></span>

<span data-ttu-id="9b38d-198">Le format de **$CCP_NODES_CORES** suit ce modèle :</span><span class="sxs-lookup"><span data-stu-id="9b38d-198">The format of **$CCP_NODES_CORES** follows this pattern:</span></span>

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

<span data-ttu-id="9b38d-199">Où :</span><span class="sxs-lookup"><span data-stu-id="9b38d-199">Where:</span></span>

* <span data-ttu-id="9b38d-200">`<Number of nodes>` est le nombre de nœuds affectés à ce travail.</span><span class="sxs-lookup"><span data-stu-id="9b38d-200">`<Number of nodes>` is the number of nodes allocated to this job.</span></span>
* <span data-ttu-id="9b38d-201">`<Name of node_n_...>` est le nom de chaque nœud affecté à ce travail.</span><span class="sxs-lookup"><span data-stu-id="9b38d-201">`<Name of node_n_...>` is the name of each node allocated to this job.</span></span>
* <span data-ttu-id="9b38d-202">`<Cores of node_n_...>` est le nombre de cœurs présents sur le nœud affecté à ce travail.</span><span class="sxs-lookup"><span data-stu-id="9b38d-202">`<Cores of node_n_...>` is the number of cores on the node allocated to this job.</span></span>

<span data-ttu-id="9b38d-203">Le nombre de cœurs (**$NBCORES**) est également calculé en fonction du nombre de nœuds (**$NBNODES**) et du nombre de cœurs par nœud (fourni comme paramètre **$NBCORESPERNODE**).</span><span class="sxs-lookup"><span data-stu-id="9b38d-203">The number of cores (**$NBCORES**) is also calculated based on the number of nodes (**$NBNODES**) and the number of cores per node (provided as parameter **$NBCORESPERNODE**).</span></span>

<span data-ttu-id="9b38d-204">Les options MPI utilisées avec Intel MPI dans Azure sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="9b38d-204">For the MPI options, the ones that are used with Intel MPI on Azure are:</span></span>

* <span data-ttu-id="9b38d-205">`-mpi intel` pour définir Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="9b38d-205">`-mpi intel` to specify Intel MPI.</span></span>
* <span data-ttu-id="9b38d-206">`-fabric UDAPL` pour utiliser des verbes Azure InfiniBand.</span><span class="sxs-lookup"><span data-stu-id="9b38d-206">`-fabric UDAPL` to use Azure InfiniBand verbs.</span></span>
* <span data-ttu-id="9b38d-207">`-cpubind bandwidth,v` pour optimiser la bande passante pour MPI avec STAR-CCM+.</span><span class="sxs-lookup"><span data-stu-id="9b38d-207">`-cpubind bandwidth,v` to optimize bandwidth for MPI with STAR-CCM+.</span></span>
* <span data-ttu-id="9b38d-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` pour faire fonctionner Intel MPI avec Azure InfiniBand et pour définir le nombre de cœurs par nœud requis.</span><span class="sxs-lookup"><span data-stu-id="9b38d-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` to make Intel MPI work with Azure InfiniBand, and to set the required number of cores per node.</span></span>
* <span data-ttu-id="9b38d-209">`-batch` pour démarrer STAR-CCM+ en mode batch sans interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9b38d-209">`-batch` to start STAR-CCM+ in batch mode with no UI.</span></span>

<span data-ttu-id="9b38d-210">Enfin, pour démarrer un travail, vérifiez que vos nœuds sont opérationnels et en ligne dans le Gestionnaire de cluster.</span><span class="sxs-lookup"><span data-stu-id="9b38d-210">Finally, to start a job, make sure that your nodes are up and running and are online in Cluster Manager.</span></span> <span data-ttu-id="9b38d-211">Puis, dans une invite de commandes PowerShell, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9b38d-211">Then from a PowerShell command prompt, run this:</span></span>

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a><span data-ttu-id="9b38d-212">Arrêter les nœuds</span><span class="sxs-lookup"><span data-stu-id="9b38d-212">Stop nodes</span></span>
<span data-ttu-id="9b38d-213">Ensuite, une fois vos tests terminés, vous pouvez utiliser les commandes PowerShell HPC Pack suivantes pour arrêter et démarrer des nœuds :</span><span class="sxs-lookup"><span data-stu-id="9b38d-213">Later on, after you're done with your tests, you can use the following HPC Pack PowerShell commands to stop and start nodes:</span></span>

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a><span data-ttu-id="9b38d-214">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9b38d-214">Next steps</span></span>
<span data-ttu-id="9b38d-215">Essayez d’exécuter d’autres charges de travail Linux,</span><span class="sxs-lookup"><span data-stu-id="9b38d-215">Try running other Linux workloads.</span></span> <span data-ttu-id="9b38d-216">par exemple :</span><span class="sxs-lookup"><span data-stu-id="9b38d-216">For example, see:</span></span>

* [<span data-ttu-id="9b38d-217">Exécution de NAMD avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="9b38d-217">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
* [<span data-ttu-id="9b38d-218">Exécuter OpenFOAM avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure</span><span class="sxs-lookup"><span data-stu-id="9b38d-218">Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
