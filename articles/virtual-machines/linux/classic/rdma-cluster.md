---
title: "Configuration d’un cluster Linux RDMA pour exécuter des applications MPI | Microsoft Docs"
description: "Créer un cluster Linux de machines virtuelles de taille H16r, H16mr, A8 ou A9 afin d’utiliser le réseau RDMA Azure pour exécuter des applications MPI"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 4b2ceb64b1737918458f6d5c692fc2bfbc0f12ed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-a-linux-rdma-cluster-to-run-mpi-applications"></a><span data-ttu-id="045b1-103">Configuration d’un cluster Linux RDMA pour exécuter des applications MPI</span><span class="sxs-lookup"><span data-stu-id="045b1-103">Set up a Linux RDMA cluster to run MPI applications</span></span>
<span data-ttu-id="045b1-104">Découvrez comment configurer un cluster RDMA Linux dans Azure avec des [tailles de machines virtuelles de calcul haute performance](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour exécuter des applications MPI (Message Passing Interface) parallèles.</span><span class="sxs-lookup"><span data-stu-id="045b1-104">Learn how to set up a Linux RDMA cluster in Azure with [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to run parallel Message Passing Interface (MPI) applications.</span></span> <span data-ttu-id="045b1-105">Cet article explique comment préparer une image Linux HPC pour exécuter Intel MPI sur un cluster.</span><span class="sxs-lookup"><span data-stu-id="045b1-105">This article provides steps to prepare a Linux HPC image to run Intel MPI on a cluster.</span></span> <span data-ttu-id="045b1-106">Après la préparation, vous déployez un cluster de machines virtuelles à l’aide de cette image et d’une des tailles de machine virtuelle Azure prenant en charge RDMA (actuellement H16r, H16mr, A8 ou A9).</span><span class="sxs-lookup"><span data-stu-id="045b1-106">After preparation, you deploy a cluster of VMs using this image and one of the RDMA-capable Azure VM sizes (currently H16r, H16mr, A8, or A9).</span></span> <span data-ttu-id="045b1-107">Utilisez le cluster pour exécuter des applications MPI communiquant efficacement avec un réseau haut débit basé sur la technologie d’accès direct à la mémoire à distance (RDMA) à faible latence.</span><span class="sxs-lookup"><span data-stu-id="045b1-107">Use the cluster to run MPI applications that communicate efficiently over a low-latency, high-throughput network based on remote direct memory access (RDMA) technology.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="045b1-108">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager](../../../resource-manager-deployment-model.md) et classique.</span><span class="sxs-lookup"><span data-stu-id="045b1-108">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="045b1-109">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="045b1-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="045b1-110">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="045b1-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

## <a name="cluster-deployment-options"></a><span data-ttu-id="045b1-111">Options de déploiement de cluster</span><span class="sxs-lookup"><span data-stu-id="045b1-111">Cluster deployment options</span></span>
<span data-ttu-id="045b1-112">Voici des méthodes que vous pouvez utiliser pour créer un cluster Linux RDMA avec ou sans planificateur de tâches.</span><span class="sxs-lookup"><span data-stu-id="045b1-112">Following are methods you can use to create a Linux RDMA cluster with or without a job scheduler.</span></span>

* <span data-ttu-id="045b1-113">**Scripts de l’interface de ligne de commande Azure** : comme indiqué plus loin dans cet article, utilisez la [CLI Azure](../../../cli-install-nodejs.md) pour créer un script de déploiement d’un cluster de machines virtuelles prenant en charge RDMA.</span><span class="sxs-lookup"><span data-stu-id="045b1-113">**Azure CLI scripts**: As shown later in this article, use the [Azure command-line interface](../../../cli-install-nodejs.md) (CLI) to script the deployment of a cluster of RDMA-capable VMs.</span></span> <span data-ttu-id="045b1-114">La CLI en mode Service Management crée les nœuds de cluster en série dans le modèle de déploiement classique. Le déploiement d’un grand nombre de nœuds de calcul peut donc prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="045b1-114">The CLI in Service Management mode creates the cluster nodes serially in the classic deployment model, so deploying many compute nodes might take several minutes.</span></span> <span data-ttu-id="045b1-115">Pour activer la connexion réseau RDMA lorsque vous utilisez le modèle de déploiement classique, déployez les machines virtuelles dans le même service cloud.</span><span class="sxs-lookup"><span data-stu-id="045b1-115">To enable the RDMA network connection when you use the classic deployment model, deploy the VMs in the same cloud service.</span></span>
* <span data-ttu-id="045b1-116">**Modèles Azure Resource Manager** : vous pouvez aussi utiliser le modèle de déploiement Resource Manager pour déployer un cluster de machines virtuelles prenant en charge RDMA, qui se connecte au réseau RDMA.</span><span class="sxs-lookup"><span data-stu-id="045b1-116">**Azure Resource Manager templates**: You can also use the Resource Manager deployment model to deploy a cluster of RDMA-capable VMs that connects to the RDMA network.</span></span> <span data-ttu-id="045b1-117">Vous pouvez [créer votre propre modèle](../../../resource-group-authoring-templates.md) ou consulter la page [Modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/) pour trouver des modèles fournis par Microsoft ou la communauté, pour déployer la solution de votre choix.</span><span class="sxs-lookup"><span data-stu-id="045b1-117">You can [create your own template](../../../resource-group-authoring-templates.md), or check the [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/) for templates contributed by Microsoft or the community to deploy the solution you want.</span></span> <span data-ttu-id="045b1-118">Les modèles Resource Manager peuvent fournir un moyen rapide et fiable pour déployer un cluster Linux.</span><span class="sxs-lookup"><span data-stu-id="045b1-118">Resource Manager templates can provide a fast and reliable way to deploy a Linux cluster.</span></span> <span data-ttu-id="045b1-119">Pour activer la connexion réseau RDMA lorsque vous utilisez le modèle de déploiement Resource Manager, déployez les machines virtuelles dans le même groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="045b1-119">To enable the RDMA network connection when you use the Resource Manager deployment model, deploy the VMs in the same availability set.</span></span>
* <span data-ttu-id="045b1-120">**HPC Pack** : créez un cluster Microsoft HPC Pack dans Azure, et ajoutez des nœuds de calcul prenant en charge RDMA, qui exécutent des distributions Linux prises en charge pour accéder au réseau RDMA.</span><span class="sxs-lookup"><span data-stu-id="045b1-120">**HPC Pack**: Create a Microsoft HPC Pack cluster in Azure and add RDMA-capable compute nodes that run a supported Linux distribution to access the RDMA network.</span></span> <span data-ttu-id="045b1-121">Pour plus d’informations, consultez [Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="045b1-121">For more information, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="sample-deployment-steps-in-the-classic-model"></a><span data-ttu-id="045b1-122">Exemple d’étapes de déploiement dans le modèle classique</span><span class="sxs-lookup"><span data-stu-id="045b1-122">Sample deployment steps in the classic model</span></span>
<span data-ttu-id="045b1-123">Les étapes suivantes montrent comment utiliser la CLI Azure pour déployer une machine virtuelle HPC SUSE Linux Enterprise Server (SLES) 12 SP1 à partir de la Place de marché Azure, la personnaliser, et créer une image de machine virtuelle personnalisée.</span><span class="sxs-lookup"><span data-stu-id="045b1-123">The following steps show how to use the Azure CLI to deploy a SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM from the Azure Marketplace, customize it, and create a custom VM image.</span></span> <span data-ttu-id="045b1-124">Vous pouvez ensuite utiliser l’image pour créer un script de déploiement d’un cluster de machines virtuelles prenant en charge RDMA.</span><span class="sxs-lookup"><span data-stu-id="045b1-124">Then you can use the image to script the deployment of a cluster of RDMA-capable VMs.</span></span>

> [!TIP]
> <span data-ttu-id="045b1-125">Utilisez une procédure similaire pour déployer un cluster de machines virtuelles prenant en charge RDMA sur des images HPC basées sur CentOS dans la Place de marché Azure.</span><span class="sxs-lookup"><span data-stu-id="045b1-125">Use similar steps to deploy a cluster of RDMA-capable VMs based on CentOS-based HPC images in the Azure Marketplace.</span></span> <span data-ttu-id="045b1-126">Certaines étapes diffèrent légèrement, comme indiqué.</span><span class="sxs-lookup"><span data-stu-id="045b1-126">Some steps differ slightly, as noted.</span></span> 
>
>

### <a name="prerequisites"></a><span data-ttu-id="045b1-127">Composants requis</span><span class="sxs-lookup"><span data-stu-id="045b1-127">Prerequisites</span></span>
* <span data-ttu-id="045b1-128">**Ordinateur client** : vous avez besoin d’un ordinateur client Mac, Linux ou Windows pour communiquer avec Azure.</span><span class="sxs-lookup"><span data-stu-id="045b1-128">**Client computer**: You need a Mac, Linux, or Windows client computer to communicate with Azure.</span></span> <span data-ttu-id="045b1-129">Ces étapes supposent que vous utilisez un client Linux.</span><span class="sxs-lookup"><span data-stu-id="045b1-129">These steps assume you are using a Linux client.</span></span>
* <span data-ttu-id="045b1-130">**Abonnement Azure** : si vous n’en avez pas, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="045b1-130">**Azure subscription**: If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span> <span data-ttu-id="045b1-131">Pour les clusters de grande taille, envisagez de souscrire un abonnement de paiement à l’utilisation ou d’autres options d’achat.</span><span class="sxs-lookup"><span data-stu-id="045b1-131">For larger clusters, consider a pay-as-you-go subscription or other purchase options.</span></span>
* <span data-ttu-id="045b1-132">**Disponibilité de taille de machine virtuelle** : les tailles d’instance prenant en charge RDMA sont les suivantes : H16r, H16mr, A8 et A9.</span><span class="sxs-lookup"><span data-stu-id="045b1-132">**VM size availability**: The following instance sizes are RDMA capable: H16r, H16mr, A8, and A9.</span></span> <span data-ttu-id="045b1-133">Pour connaître la disponibilité dans les différentes régions Azure, voir [Disponibilité des produits par région](https://azure.microsoft.com/regions/services/) .</span><span class="sxs-lookup"><span data-stu-id="045b1-133">Check [Products available by region](https://azure.microsoft.com/regions/services/) for availability in Azure regions.</span></span>
* <span data-ttu-id="045b1-134">**Quota de cœurs** : il se peut que vous deviez augmenter le quota de cœurs pour déployer un cluster de machines virtuelles nécessitant beaucoup de ressources système.</span><span class="sxs-lookup"><span data-stu-id="045b1-134">**Cores quota**: You might need to increase the quota of cores to deploy a cluster of compute-intensive VMs.</span></span> <span data-ttu-id="045b1-135">Par exemple, vous devez avoir au moins 128 cœurs si vous souhaitez déployer 8 machines virtuelles A9, comme indiqué dans cet article.</span><span class="sxs-lookup"><span data-stu-id="045b1-135">For example, you need at least 128 cores if you want to deploy 8 A9 VMs as shown in this article.</span></span> <span data-ttu-id="045b1-136">Votre abonnement peut également limiter le nombre de cœurs, que vous pouvez déployer dans certaines familles de taille de machine virtuelle, dont la série H.</span><span class="sxs-lookup"><span data-stu-id="045b1-136">Your subscription might also limit the number of cores you can deploy in certain VM size families, including the H-series.</span></span> <span data-ttu-id="045b1-137">Pour demander une augmentation de quota, [ouvrez une demande de service clientèle en ligne](../../../azure-supportability/how-to-create-azure-support-request.md) gratuitement.</span><span class="sxs-lookup"><span data-stu-id="045b1-137">To request a quota increase, [open an online customer support request](../../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
* <span data-ttu-id="045b1-138">**CLI Azure** : [installez](../../../cli-install-nodejs.md) la CLI Azure et [connectez-vous à votre abonnement Azure](../../../xplat-cli-connect.md) sur l’ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="045b1-138">**Azure CLI**: [Install](../../../cli-install-nodejs.md) the Azure CLI and [connect to your Azure subscription](../../../xplat-cli-connect.md) from the client computer.</span></span>

### <a name="provision-an-sles-12-sp1-hpc-vm"></a><span data-ttu-id="045b1-139">Configurer une machine virtuelle SLES 12 SP1 HPC</span><span class="sxs-lookup"><span data-stu-id="045b1-139">Provision an SLES 12 SP1 HPC VM</span></span>
<span data-ttu-id="045b1-140">Après la connexion à Azure avec la CLI Azure, exécutez la commande `azure config list` pour confirmer que la sortie affiche le mode Service Management.</span><span class="sxs-lookup"><span data-stu-id="045b1-140">After signing in to Azure with the Azure CLI, run `azure config list` to confirm that the output shows Service Management mode.</span></span> <span data-ttu-id="045b1-141">Si ce n’est pas le cas, définissez le mode en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="045b1-141">If it does not, set the mode by running this command:</span></span>

    azure config mode asm


<span data-ttu-id="045b1-142">Tapez la commande suivante pour répertorier tous les abonnements que vous êtes autorisé à utiliser :</span><span class="sxs-lookup"><span data-stu-id="045b1-142">Type the following to list all the subscriptions you are authorized to use:</span></span>

    azure account list

<span data-ttu-id="045b1-143">L’abonnement actif actuel est identifié par `Current` avec la valeur `true`.</span><span class="sxs-lookup"><span data-stu-id="045b1-143">The current active subscription is identified with `Current` set to `true`.</span></span> <span data-ttu-id="045b1-144">S’il ne s’agit pas de l’abonnement que vous souhaitez utiliser pour créer le cluster, définissez l’ID d’abonnement approprié comme abonnement actif :</span><span class="sxs-lookup"><span data-stu-id="045b1-144">If this subscription isn't the one you want to use to create the cluster, set the appropriate subscription ID as the active subscription:</span></span>

    azure account set <subscription-Id>

<span data-ttu-id="045b1-145">Pour afficher les images de SLES 12 SP1 HPC publiquement disponibles dans Azure, exécutez une commande comme celle qui suit, si votre environnement d’interpréteur de commandes prend en charge **grep** :</span><span class="sxs-lookup"><span data-stu-id="045b1-145">To see the publicly available SLES 12 SP1 HPC images in Azure, run a command like the following, assuming your shell environment supports **grep**:</span></span>

    azure vm image list | grep "suse.*hpc"

<span data-ttu-id="045b1-146">Configurez une machine virtuelle prenant en charge RDMA avec une image de SLES 12 SP1 HPC en exécutant une commande comme la suivante :</span><span class="sxs-lookup"><span data-stu-id="045b1-146">Provision an RDMA-capable VM with a SLES 12 SP1 HPC image by running a command like the following:</span></span>

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

<span data-ttu-id="045b1-147">Où :</span><span class="sxs-lookup"><span data-stu-id="045b1-147">Where:</span></span>

* <span data-ttu-id="045b1-148">La taille (A9 dans cet exemple) est l’une des tailles de machine virtuelle prenant en charge RDMA.</span><span class="sxs-lookup"><span data-stu-id="045b1-148">The size (A9 in this example) is one of the RDMA-capable VM sizes.</span></span>
* <span data-ttu-id="045b1-149">Le numéro de port SSH externe (22 dans cet exemple, qui est le SHH par défaut) est un numéro de port valide.</span><span class="sxs-lookup"><span data-stu-id="045b1-149">The external SSH port number (22 in this example, which is the SSH default) is any valid port number.</span></span> <span data-ttu-id="045b1-150">Le numéro de port interne SSH est défini sur 22.</span><span class="sxs-lookup"><span data-stu-id="045b1-150">The internal SSH port number is set to 22.</span></span>
* <span data-ttu-id="045b1-151">Un service cloud est créé dans la région Azure spécifiée par l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="045b1-151">A new cloud service is created in the Azure region specified by the location.</span></span> <span data-ttu-id="045b1-152">Spécifiez un emplacement dans lequel la taille de machine virtuelle que vous choisissez est disponible.</span><span class="sxs-lookup"><span data-stu-id="045b1-152">Specify a location in which the VM size you choose is available.</span></span>
* <span data-ttu-id="045b1-153">Pour la prise en charge de la priorité SUSE (des frais supplémentaires s’appliquent), le nom de l’image de SLES 12 SP1 peut actuellement être conforme à une de ces deux options :</span><span class="sxs-lookup"><span data-stu-id="045b1-153">For SUSE priority support (which incurs additional charges), the SLES 12 SP1 image name currently can be one of these two options:</span></span> 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-the-vm"></a><span data-ttu-id="045b1-154">Personnalisation de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="045b1-154">Customize the VM</span></span>
<span data-ttu-id="045b1-155">Après l’approvisionnement de la machine virtuelle, utilisez SSH pour vous connecter à la machine virtuelle à l’aide de l’adresse IP externe de la machine virtuelle (ou du nom DNS) et du numéro de port externe configuré et personnalisez-la.</span><span class="sxs-lookup"><span data-stu-id="045b1-155">After the VM finishes provisioning, SSH to the VM by using the VM's external IP address (or DNS name) and the external port number you configured, and then customize it.</span></span> <span data-ttu-id="045b1-156">Pour plus d’informations sur la connexion, consultez [Connexion à une machine virtuelle exécutant Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="045b1-156">For connection details, see [How to log on to a virtual machine running Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="045b1-157">Exécutez les commandes comme l’utilisateur que vous avez configuré sur la machine virtuelle, à moins qu’un accès racine soit nécessaire pour accomplir une étape.</span><span class="sxs-lookup"><span data-stu-id="045b1-157">Perform commands as the user you configured on the VM, unless root access is required to complete a step.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="045b1-158">Microsoft Azure ne fournit pas d'accès racine aux machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="045b1-158">Microsoft Azure does not provide root access to Linux VMs.</span></span> <span data-ttu-id="045b1-159">Pour obtenir un accès administratif lorsque vous êtes connecté en tant qu’utilisateur à la machine virtuelle, exécutez les commandes avec `sudo`.</span><span class="sxs-lookup"><span data-stu-id="045b1-159">To gain administrative access when connected as a user to the VM, run commands by using `sudo`.</span></span>
>
>

* <span data-ttu-id="045b1-160">**Mises à jour** : installez les mises à jour à l’aide de zypper.</span><span class="sxs-lookup"><span data-stu-id="045b1-160">**Updates**: Install updates by using zypper.</span></span> <span data-ttu-id="045b1-161">Vous pouvez également installer les utilitaires NFS.</span><span class="sxs-lookup"><span data-stu-id="045b1-161">You might also want to install NFS utilities.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="045b1-162">Dans une machine virtuelle SLES 12 SP1 HPC, nous vous recommandons de ne pas appliquer les mises à jour du noyau, qui peuvent provoquer des problèmes avec les pilotes RDMA Linux.</span><span class="sxs-lookup"><span data-stu-id="045b1-162">In a SLES 12 SP1 HPC VM, we recommend that you don't apply kernel updates, which can cause issues with the Linux RDMA drivers.</span></span>
  >
  >
* <span data-ttu-id="045b1-163">**Intel MPI** : terminez l’installation d’Intel MPI sur la machine virtuelle SLES 12 SP1 HPC en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="045b1-163">**Intel MPI**: Complete the installation of Intel MPI on the SLES 12 SP1 HPC VM by running the following command:</span></span>

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* <span data-ttu-id="045b1-164">**Verrouiller la mémoire** : pour que les codes MPI verrouillent la mémoire disponible pour RDMA, ajoutez ou modifiez les paramètres suivants dans le fichier /etc/security/limits.conf.</span><span class="sxs-lookup"><span data-stu-id="045b1-164">**Lock memory**: For MPI codes to lock the memory available for RDMA, add or change the following settings in the /etc/security/limits.conf file.</span></span> <span data-ttu-id="045b1-165">Un accès racine est requis pour modifier ce fichier.</span><span class="sxs-lookup"><span data-stu-id="045b1-165">You need root access to edit this file.</span></span>

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > <span data-ttu-id="045b1-166">À des fins de test, vous pouvez également définir memlock comme illimité.</span><span class="sxs-lookup"><span data-stu-id="045b1-166">For testing purposes, you can also set memlock to unlimited.</span></span> <span data-ttu-id="045b1-167">Par exemple : `<User or group name>    hard    memlock unlimited`.</span><span class="sxs-lookup"><span data-stu-id="045b1-167">For example: `<User or group name>    hard    memlock unlimited`.</span></span> <span data-ttu-id="045b1-168">Pour plus d’informations, voir les [meilleures méthodes connues pour définir la taille de mémoire verrouillée](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span><span class="sxs-lookup"><span data-stu-id="045b1-168">For more information, see [Best known methods for setting locked memory size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span></span>
  >
  >
* <span data-ttu-id="045b1-169">**Clés SSH pour machines virtuelles SLES** : générez des clés SSH pour établir l’approbation de votre compte utilisateur parmi les nœuds de calcul du cluster SLES lors de l’exécution de travaux MPI.</span><span class="sxs-lookup"><span data-stu-id="045b1-169">**SSH keys for SLES VMs**: Generate SSH keys to establish trust for your user account among the compute nodes in the SLES cluster when running MPI jobs.</span></span> <span data-ttu-id="045b1-170">Si vous avez déployé une machine virtuelle HPC basée sur CentOS, ne suivez pas cette étape.</span><span class="sxs-lookup"><span data-stu-id="045b1-170">If you deployed a CentOS-based HPC VM, don't follow this step.</span></span> <span data-ttu-id="045b1-171">Consultez les instructions de la suite de cet article pour définir une confiance SSH sans mot de passe entre les nœuds du cluster une fois que vous avez capturé l’image et déployé le cluster.</span><span class="sxs-lookup"><span data-stu-id="045b1-171">See instructions later in this article to set up passwordless SSH trust among the cluster nodes after you capture the image and deploy the cluster.</span></span>

    <span data-ttu-id="045b1-172">Pour créer des clés SSH, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="045b1-172">To create SSH keys, run the following command.</span></span> <span data-ttu-id="045b1-173">Lorsque vous y êtes invité, appuyez sur **Entrée** pour générer les clés dans l’emplacement par défaut sans définir de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="045b1-173">When you are prompted for input, select **Enter** to generate the keys in the default location without setting a password.</span></span>

        ssh-keygen

    <span data-ttu-id="045b1-174">Ajoutez la clé publique au fichier authorized_keys pour les clés publiques connues.</span><span class="sxs-lookup"><span data-stu-id="045b1-174">Append the public key to the authorized_keys file for known public keys.</span></span>

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    <span data-ttu-id="045b1-175">Dans l’annuaire ~/.ssh, modifiez ou créez le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="045b1-175">In the ~/.ssh directory, edit or create the config file.</span></span> <span data-ttu-id="045b1-176">Fournissez la plage d’adresses IP du réseau privé que vous prévoyez d’utiliser dans Azure (10.32.0.0/16 dans cet exemple) :</span><span class="sxs-lookup"><span data-stu-id="045b1-176">Provide the IP address range of the private network that you plan to use in Azure (10.32.0.0/16 in this example):</span></span>

        host 10.32.0.*
        StrictHostKeyChecking no

    <span data-ttu-id="045b1-177">Vous pouvez également répertorier l'adresse IP du réseau privé de chaque machine virtuelle dans votre cluster comme suit :</span><span class="sxs-lookup"><span data-stu-id="045b1-177">Alternatively, list the private network IP address of each VM in your cluster as follows:</span></span>

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > <span data-ttu-id="045b1-178">La configuration de `StrictHostKeyChecking no` peut créer un risque de sécurité potentiel si une adresse IP ou une plage d’adresses IP spécifiques ne sont pas spécifiées.</span><span class="sxs-lookup"><span data-stu-id="045b1-178">Configuring `StrictHostKeyChecking no` can create a potential security risk when a specific IP address or range is not specified.</span></span>
  >
  >
* <span data-ttu-id="045b1-179">**Applications** : installez les applications dont vous avez besoin ou effectuez d’autres personnalisations avant de capturer l’image.</span><span class="sxs-lookup"><span data-stu-id="045b1-179">**Applications**: Install any applications you need or perform other customizations before you capture the image.</span></span>

### <a name="capture-the-image"></a><span data-ttu-id="045b1-180">capture de l’image</span><span class="sxs-lookup"><span data-stu-id="045b1-180">Capture the image</span></span>
<span data-ttu-id="045b1-181">Pour capturer l’image, exécutez d’abord la commande suivante sur la machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="045b1-181">To capture the image, first run the following command on the Linux VM.</span></span> <span data-ttu-id="045b1-182">Cette commande désaffecte la machine virtuelle, mais conserve les comptes utilisateurs et les clés SSH que vous avez configurés.</span><span class="sxs-lookup"><span data-stu-id="045b1-182">This command deprovisions the VM but maintains user accounts and SSH keys that you set up.</span></span>

```
sudo waagent -deprovision
```

<span data-ttu-id="045b1-183">Depuis votre ordinateur client, exécutez les commandes CLI Azure suivantes pour capturer l’image.</span><span class="sxs-lookup"><span data-stu-id="045b1-183">From your client computer, run the following Azure CLI commands to capture the image.</span></span> <span data-ttu-id="045b1-184">Pour plus d’informations, consultez la page [Capture d’une machine virtuelle Linux classique en tant qu’image](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="045b1-184">For more information, see [How to capture a classic Linux virtual machine as an image](capture-image.md).</span></span>  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

<span data-ttu-id="045b1-185">Après avoir exécuté ces commandes, l'image de machine virtuelle est capturée pour que vous puissiez l'utiliser et la machine virtuelle est supprimée.</span><span class="sxs-lookup"><span data-stu-id="045b1-185">After you run these commands, the VM image is captured for your use and the VM is deleted.</span></span> <span data-ttu-id="045b1-186">Vous disposez maintenant d’une image personnalisée prête à être déployée sur un cluster.</span><span class="sxs-lookup"><span data-stu-id="045b1-186">Now you have your custom image ready to deploy a cluster.</span></span>

### <a name="deploy-a-cluster-with-the-image"></a><span data-ttu-id="045b1-187">Déploiement d’un cluster avec l'image</span><span class="sxs-lookup"><span data-stu-id="045b1-187">Deploy a cluster with the image</span></span>
<span data-ttu-id="045b1-188">Modifiez le script Bash suivant avec les valeurs appropriées pour votre environnement et exécutez-le à partir de votre ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="045b1-188">Modify the following Bash script with appropriate values for your environment and run it from your client computer.</span></span> <span data-ttu-id="045b1-189">Dans la mesure où Azure déploie les machines virtuelles en série dans le modèle de déploiement Service Management, quelques minutes sont nécessaires pour déployer les huit machines virtuelles A9 suggérées dans ce script.</span><span class="sxs-lookup"><span data-stu-id="045b1-189">Because Azure deploys the VMs serially in the classic deployment model, it takes a few minutes to deploy the eight A9 VMs suggested in this script.</span></span>

```
#!/bin/bash -x
# Script to create a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where the VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All the compute-intensive instances need to be in the same cloud service for Linux RDMA to work across InfiniBand.
# Note: The current maximum number of VMs in a cloud service is 50. If you need to provision more than 50 VMs in the same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want to turn off external ports and use only internal ports to communicate between compute nodes via port 22, don’t use this option. Since port numbers up to 10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 to cluster18. Specify your captured image in <image-name>. Specify the username and password you used when creating the SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment to provision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a><span data-ttu-id="045b1-190">Considérations pour un cluster HPC CentOS</span><span class="sxs-lookup"><span data-stu-id="045b1-190">Considerations for a CentOS HPC cluster</span></span>
<span data-ttu-id="045b1-191">Si vous souhaitez configurer un cluster basé sur l’une des images HPC basées sur CentOS dans Azure Marketplace au lieu de SLES 12 pour HPC, suivez les étapes générales de la section précédente.</span><span class="sxs-lookup"><span data-stu-id="045b1-191">If you want to set up a cluster based on one of the CentOS-based HPC images in the Azure Marketplace instead of SLES 12 for HPC, follow the general steps in the preceding section.</span></span> <span data-ttu-id="045b1-192">Notez les différences suivantes lorsque vous approvisionnez et configurez la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="045b1-192">Note the following differences when you provision and configure the VM:</span></span>

- <span data-ttu-id="045b1-193">Intel MPI est déjà installé sur une machine virtuelle approvisionnée à partir d’une image de HPC basée sur CentOS.</span><span class="sxs-lookup"><span data-stu-id="045b1-193">Intel MPI is already installed on a VM provisioned from a CentOS-based HPC image.</span></span>
- <span data-ttu-id="045b1-194">Les paramètres de verrouillage de mémoire sont déjà ajoutés dans le fichier /etc/security/limits.conf de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="045b1-194">Lock memory settings are already added in the VM's /etc/security/limits.conf file.</span></span>
- <span data-ttu-id="045b1-195">Ne générez pas de clés SSH sur la machine virtuelle que vous approvisionnez pour la capture.</span><span class="sxs-lookup"><span data-stu-id="045b1-195">Do not generate SSH keys on the VM you provision for capture.</span></span> <span data-ttu-id="045b1-196">Au lieu de cela, nous vous recommandons de configurer une authentification basée sur l’utilisateur après le déploiement du cluster.</span><span class="sxs-lookup"><span data-stu-id="045b1-196">Instead, we recommend setting up user-based authentication after you deploy the cluster.</span></span> <span data-ttu-id="045b1-197">Pour plus d’informations, consultez la section suivante :</span><span class="sxs-lookup"><span data-stu-id="045b1-197">For more information, see the following section.</span></span>  

### <a name="set-up-passwordless-ssh-trust-on-the-cluster"></a><span data-ttu-id="045b1-198">Configurer une approbation SSH sans mot de passe sur le cluster</span><span class="sxs-lookup"><span data-stu-id="045b1-198">Set up passwordless SSH trust on the cluster</span></span>
<span data-ttu-id="045b1-199">Sur un cluster HPC basé sur CentOS, deux méthodes permettent d’établir une approbation entre les nœuds de calcul : l’authentification basée sur l’hôte et l’authentification basée sur l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="045b1-199">On a CentOS-based HPC cluster, there are two methods for establishing trust between the compute nodes: host-based authentication and user-based authentication.</span></span> <span data-ttu-id="045b1-200">L’authentification basée sur l’hôte n’est pas expliquée dans cet article. Elle doit généralement être configurée à l’aide d’un script d’extension pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="045b1-200">Host-based authentication is outside of the scope of this article and generally must be done through an extension script during deployment.</span></span> <span data-ttu-id="045b1-201">L’authentification basée sur l’utilisateur est pratique pour établir une confiance après le déploiement, et nécessite la génération et le partage de clés SSH entre les nœuds de calcul dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="045b1-201">User-based authentication is convenient for establishing trust after deployment and requires the generation and sharing of SSH keys among the compute nodes in the cluster.</span></span> <span data-ttu-id="045b1-202">Cette méthode est communément appelée connexion SSH sans mot de passe. Elle est requise lors de l’exécution de travaux MPI.</span><span class="sxs-lookup"><span data-stu-id="045b1-202">This method is commonly known as passwordless SSH login and is required when running MPI jobs.</span></span>

<span data-ttu-id="045b1-203">Un exemple de script fourni par la communauté est disponible sur [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) pour permettre une authentification utilisateur simple sur un cluster HPC basé sur CentOS.</span><span class="sxs-lookup"><span data-stu-id="045b1-203">A sample script contributed from the community is available on [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) to enable easy user authentication on a CentOS-based HPC cluster.</span></span> <span data-ttu-id="045b1-204">Vous pouvez télécharger et utiliser ce script en procédant comme suit.</span><span class="sxs-lookup"><span data-stu-id="045b1-204">Download and use this script by using the following steps.</span></span> <span data-ttu-id="045b1-205">Vous pouvez également modifier ce script ou utiliser toute autre méthode permettant d’établir une authentification SSH sans mot de passe entre les nœuds de calcul du cluster.</span><span class="sxs-lookup"><span data-stu-id="045b1-205">You can also modify this script or use any other method to establish passwordless SSH authentication between the cluster compute nodes.</span></span>

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

<span data-ttu-id="045b1-206">Pour exécuter le script, vous devez connaître le préfixe des adresses IP de votre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="045b1-206">To run the script, you need to know the prefix for your subnet IP addresses.</span></span> <span data-ttu-id="045b1-207">Vous pouvez obtenir ces informations en exécutant la commande suivante sur l’un des nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="045b1-207">Get the prefix by running the following command on one of the cluster nodes.</span></span> <span data-ttu-id="045b1-208">Votre résultat doit ressembler à 10.1.3.5, et le préfixe est 10.1.3.</span><span class="sxs-lookup"><span data-stu-id="045b1-208">Your output should look something like 10.1.3.5, and the prefix is the 10.1.3 portion.</span></span>

    ifconfig eth0 | grep -w inet | awk '{print $2}'

<span data-ttu-id="045b1-209">Ensuite, exécutez le script à l’aide de trois paramètres : le nom d’utilisateur courant utilisé sur les nœuds de calcul, le mot de passe pour cet utilisateur sur les nœuds de calcul et le préfixe de sous-réseau renvoyé par la commande précédente.</span><span class="sxs-lookup"><span data-stu-id="045b1-209">Now run the script using three parameters: the common user name on the compute nodes, the common password for that user on the compute nodes, and the subnet prefix that was returned from the previous command.</span></span>

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

<span data-ttu-id="045b1-210">Ce script effectue les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="045b1-210">This script does the following:</span></span>

* <span data-ttu-id="045b1-211">Crée sur le nœud hôte un répertoire nommé .ssh, qui est requis pour la connexion sans mot de passe.</span><span class="sxs-lookup"><span data-stu-id="045b1-211">Creates a directory on the host node named .ssh, which is required for passwordless login.</span></span>
* <span data-ttu-id="045b1-212">Crée un fichier de configuration dans le répertoire .ssh, qui indique à la méthode de connexion sans mot de passe d’autoriser la connexion à partir de n’importe quel nœud du cluster.</span><span class="sxs-lookup"><span data-stu-id="045b1-212">Creates a configuration file in the .ssh directory that instructs passwordless login to allow login from any node in the cluster.</span></span>
* <span data-ttu-id="045b1-213">Crée des fichiers contenant les noms et adresses IP de chacun des nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="045b1-213">Creates files containing the node names and node IP addresses for all the nodes in the cluster.</span></span> <span data-ttu-id="045b1-214">Ces fichiers sont conservés après l’exécution du script à des fins de référence ultérieure.</span><span class="sxs-lookup"><span data-stu-id="045b1-214">These files are left after the script is run for later reference.</span></span>
* <span data-ttu-id="045b1-215">Crée une paire de clés privée et publique pour chaque nœud du cluster, (y compris le nœud hôte), et crée des entrées dans le fichier authorized_keys.</span><span class="sxs-lookup"><span data-stu-id="045b1-215">Creates a private and public key pair for each cluster node (including the host node) and creates entries in the authorized_keys file.</span></span>

> [!WARNING]
> <span data-ttu-id="045b1-216">L’exécution de ce script peut créer un risque de sécurité potentiel.</span><span class="sxs-lookup"><span data-stu-id="045b1-216">Running this script can create a potential security risk.</span></span> <span data-ttu-id="045b1-217">Assurez-vous que les informations de clé publique dans ~/.ssh ne sont pas distribuées.</span><span class="sxs-lookup"><span data-stu-id="045b1-217">Ensure that the public key information in ~/.ssh is not distributed.</span></span>
>
>

## <a name="configure-intel-mpi"></a><span data-ttu-id="045b1-218">Configurer Intel MPI</span><span class="sxs-lookup"><span data-stu-id="045b1-218">Configure Intel MPI</span></span>
<span data-ttu-id="045b1-219">Pour exécuter des applications MPI sur RDMA Azure Linux, vous devez configurer certaines variables d'environnement spécifiques à Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="045b1-219">To run MPI applications on Azure Linux RDMA, you need to configure certain environment variables specific to Intel MPI.</span></span> <span data-ttu-id="045b1-220">Voici un exemple de script bash pour configurer les variables nécessaires à l’exécution d’une application.</span><span class="sxs-lookup"><span data-stu-id="045b1-220">Here is a sample Bash script to configure the variables needed to run an application.</span></span> <span data-ttu-id="045b1-221">Modifiez le chemin d’accès à mpivars.sh selon les besoins de votre installation d’Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="045b1-221">Change the path to mpivars.sh as needed for your installation of Intel MPI.</span></span>

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting the variable to shm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line to run the job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path to the application exe> <arguments specific to the application>

#end
```

<span data-ttu-id="045b1-222">Le format du fichier hôte est le suivant.</span><span class="sxs-lookup"><span data-stu-id="045b1-222">The format of the host file is as follows.</span></span> <span data-ttu-id="045b1-223">Ajoutez une ligne pour chaque nœud de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="045b1-223">Add one line for each node in your cluster.</span></span> <span data-ttu-id="045b1-224">Spécifiez des adresses IP privées à partir du réseau virtuel défini précédemment, pas des noms DNS.</span><span class="sxs-lookup"><span data-stu-id="045b1-224">Specify private IP addresses from the virtual network defined earlier, not DNS names.</span></span> <span data-ttu-id="045b1-225">Par exemple, pour deux hôtes avec les adresses IP 10.32.0.1 et 10.32.0.2, le fichier contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="045b1-225">For example, for two hosts with IP addresses 10.32.0.1 and 10.32.0.2, the file contains the following:</span></span>

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a><span data-ttu-id="045b1-226">Exécuter MPI sur un cluster à deux nœuds de base</span><span class="sxs-lookup"><span data-stu-id="045b1-226">Run MPI on a basic two-node cluster</span></span>
<span data-ttu-id="045b1-227">Si ce n'est pas déjà fait, commencez par configurer l'environnement pour Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="045b1-227">If you haven't already done so, first set up the environment for Intel MPI.</span></span>

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a><span data-ttu-id="045b1-228">Exécution d’une commande MPI</span><span class="sxs-lookup"><span data-stu-id="045b1-228">Run an MPI command</span></span>
<span data-ttu-id="045b1-229">Exécutez une commande MPI sur l’un des nœuds de calcul pour montrer que MPI est installé correctement et peut communiquer entre au moins deux nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="045b1-229">Run an MPI command on one of the compute nodes to show that MPI is installed properly and can communicate between at least two compute nodes.</span></span> <span data-ttu-id="045b1-230">La commande **mpirun** suivante exécute la commande **hostname** sur deux nœuds.</span><span class="sxs-lookup"><span data-stu-id="045b1-230">The following **mpirun** command runs the **hostname** command on two nodes.</span></span>

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
<span data-ttu-id="045b1-231">Votre sortie doit répertorier les noms de tous les nœuds que vous avez transmis comme entrée pour `-hosts`.</span><span class="sxs-lookup"><span data-stu-id="045b1-231">Your output should list the names of all the nodes that you passed as input for `-hosts`.</span></span> <span data-ttu-id="045b1-232">Par exemple, une commande **mpirun** avec deux nœuds renvoie un résultat comme le suivant :</span><span class="sxs-lookup"><span data-stu-id="045b1-232">For example, an **mpirun** command with two nodes returns output like the following:</span></span>

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a><span data-ttu-id="045b1-233">Exécution d'un test d'évaluation MPI</span><span class="sxs-lookup"><span data-stu-id="045b1-233">Run an MPI benchmark</span></span>
<span data-ttu-id="045b1-234">La commande Intel MPI suivante vérifie la configuration du cluster et sa connexion au réseau RDMA à l’aide d’un banc d’essai pingpong.</span><span class="sxs-lookup"><span data-stu-id="045b1-234">The following Intel MPI command runs a pingpong benchmark to verify the cluster configuration and connection to the RDMA network.</span></span>

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

<span data-ttu-id="045b1-235">Sur un cluster opérationnel à deux nœuds, vous devez voir une sortie comme ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="045b1-235">On a working cluster with two nodes, you should see output like the following.</span></span> <span data-ttu-id="045b1-236">Sur le réseau RDMA Azure, vous devez vous attendre à une latence égale ou inférieure à 3 microsecondes pour les tailles de messages jusqu’à 512 octets.</span><span class="sxs-lookup"><span data-stu-id="045b1-236">On the Azure RDMA network, expect latency at or below 3 microseconds for message sizes up to 512 bytes.</span></span>

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# the number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected to be exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through the flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks to run:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a><span data-ttu-id="045b1-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="045b1-237">Next steps</span></span>
* <span data-ttu-id="045b1-238">Déploiement et exécution de vos applications MPI Linux sur votre cluster Linux.</span><span class="sxs-lookup"><span data-stu-id="045b1-238">Deploy and run your Linux MPI applications on your Linux cluster.</span></span>
* <span data-ttu-id="045b1-239">Consultez la [documentation de la bibliothèque Intel MPI](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) pour obtenir des conseils sur Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="045b1-239">See the [Intel MPI Library documentation](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) for guidance on Intel MPI.</span></span>
* <span data-ttu-id="045b1-240">Essayez un [modèle de démarrage rapide](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) pour créer un cluster Intel Lustre en utilisant une image HPC basée sur CentOS.</span><span class="sxs-lookup"><span data-stu-id="045b1-240">Try a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) to create an Intel Lustre cluster by using a CentOS-based HPC image.</span></span> <span data-ttu-id="045b1-241">Pour plus d’informations, consultez [Déploiement d’Intel Cloud Edition pour Lustre sur Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="045b1-241">For details, see [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span></span>
