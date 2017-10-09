---
title: aaaSet une applications MPI de Linux RDMA cluster toorun | Documents Microsoft
description: "Créer un cluster de Linux de la taille des toouse H16r, H16mr, A8 ou A9 VMs les applications MPI toorun hello RDMA Azure réseau"
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
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a><span data-ttu-id="9b405-103">Configurer une application MPI de Linux RDMA cluster toorun</span><span class="sxs-lookup"><span data-stu-id="9b405-103">Set up a Linux RDMA cluster toorun MPI applications</span></span>
<span data-ttu-id="9b405-104">Découvrez comment tooset d’un RDMA Linux cluster dans Azure avec [tailles de machine virtuelle de calcul haute performance](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun les applications Interface MPI (Message Passing) parallèles.</span><span class="sxs-lookup"><span data-stu-id="9b405-104">Learn how tooset up a Linux RDMA cluster in Azure with [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun parallel Message Passing Interface (MPI) applications.</span></span> <span data-ttu-id="9b405-105">Cet article fournit des étapes tooprepare un toorun d’image Linux HPC Intel MPI sur un cluster.</span><span class="sxs-lookup"><span data-stu-id="9b405-105">This article provides steps tooprepare a Linux HPC image toorun Intel MPI on a cluster.</span></span> <span data-ttu-id="9b405-106">Après la préparation, vous déployez un cluster d’ordinateurs virtuels à l’aide de cette image et l’une des tailles de machine virtuelle de Azure prend en charge RDMA hello (actuellement H16r, H16mr, A8 ou A9).</span><span class="sxs-lookup"><span data-stu-id="9b405-106">After preparation, you deploy a cluster of VMs using this image and one of hello RDMA-capable Azure VM sizes (currently H16r, H16mr, A8, or A9).</span></span> <span data-ttu-id="9b405-107">Utilisez hello cluster toorun des applications MPI qui communiquent efficacement sur un réseau à faible latence, à débit élevé en fonction de la technologie direct à la mémoire à distance (RDMA) d’accès.</span><span class="sxs-lookup"><span data-stu-id="9b405-107">Use hello cluster toorun MPI applications that communicate efficiently over a low-latency, high-throughput network based on remote direct memory access (RDMA) technology.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b405-108">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager](../../../resource-manager-deployment-model.md) et classique.</span><span class="sxs-lookup"><span data-stu-id="9b405-108">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="9b405-109">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="9b405-110">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

## <a name="cluster-deployment-options"></a><span data-ttu-id="9b405-111">Options de déploiement de cluster</span><span class="sxs-lookup"><span data-stu-id="9b405-111">Cluster deployment options</span></span>
<span data-ttu-id="9b405-112">Voici les méthodes toocreate un cluster Linux RDMA avec ou sans un planificateur de travaux.</span><span class="sxs-lookup"><span data-stu-id="9b405-112">Following are methods you can use toocreate a Linux RDMA cluster with or without a job scheduler.</span></span>

* <span data-ttu-id="9b405-113">**Les scripts CLI Azure**: comme indiqué plus loin dans cet article, utilisez hello [interface de ligne de commande Azure](../../../cli-install-nodejs.md) déploiement de hello tooscript (CLI) d’un cluster d’ordinateurs virtuels prenant en charge RDMA.</span><span class="sxs-lookup"><span data-stu-id="9b405-113">**Azure CLI scripts**: As shown later in this article, use hello [Azure command-line interface](../../../cli-install-nodejs.md) (CLI) tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span> <span data-ttu-id="9b405-114">Hello CLI en mode de gestion de Service crée hello nœuds de cluster en série dans le modèle de déploiement classique de hello, afin de déployer plusieurs nœuds de calcul peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="9b405-114">hello CLI in Service Management mode creates hello cluster nodes serially in hello classic deployment model, so deploying many compute nodes might take several minutes.</span></span> <span data-ttu-id="9b405-115">tooenable hello connexion de réseau RDMA lorsque vous utilisez le modèle de déploiement classique de hello, déployez des machines virtuelles hello Bonjour même service cloud.</span><span class="sxs-lookup"><span data-stu-id="9b405-115">tooenable hello RDMA network connection when you use hello classic deployment model, deploy hello VMs in hello same cloud service.</span></span>
* <span data-ttu-id="9b405-116">**Les modèles de gestionnaire de ressources Azure**: vous pouvez également utiliser hello Gestionnaire de ressources du déploiement modèle toodeploy un cluster d’ordinateurs virtuels prenant en charge RDMA qui relie toohello RDMA.</span><span class="sxs-lookup"><span data-stu-id="9b405-116">**Azure Resource Manager templates**: You can also use hello Resource Manager deployment model toodeploy a cluster of RDMA-capable VMs that connects toohello RDMA network.</span></span> <span data-ttu-id="9b405-117">Vous pouvez [créer votre propre modèle](../../../resource-group-authoring-templates.md), ou vérifiez hello [modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/) pour les modèles fournis par Microsoft hello Communauté toodeploy hello solution ou souhaité.</span><span class="sxs-lookup"><span data-stu-id="9b405-117">You can [create your own template](../../../resource-group-authoring-templates.md), or check hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/) for templates contributed by Microsoft or hello community toodeploy hello solution you want.</span></span> <span data-ttu-id="9b405-118">Modèles du Gestionnaire de ressources peuvent fournir un moyen rapide et fiable de toodeploy un cluster Linux.</span><span class="sxs-lookup"><span data-stu-id="9b405-118">Resource Manager templates can provide a fast and reliable way toodeploy a Linux cluster.</span></span> <span data-ttu-id="9b405-119">tooenable hello connexion de réseau RDMA lorsque vous utilisez le modèle de déploiement du Gestionnaire de ressources hello, déployer des machines virtuelles de hello Bonjour même groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="9b405-119">tooenable hello RDMA network connection when you use hello Resource Manager deployment model, deploy hello VMs in hello same availability set.</span></span>
* <span data-ttu-id="9b405-120">**HPC Pack**: créer un cluster Microsoft HPC Pack dans Azure et ajouter des nœuds de calcul prenant en charge RDMA qui s’exécutent à un réseau RDMA hello de prise en charge Linux distribution tooaccess.</span><span class="sxs-lookup"><span data-stu-id="9b405-120">**HPC Pack**: Create a Microsoft HPC Pack cluster in Azure and add RDMA-capable compute nodes that run a supported Linux distribution tooaccess hello RDMA network.</span></span> <span data-ttu-id="9b405-121">Pour plus d’informations, consultez [Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="9b405-121">For more information, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="sample-deployment-steps-in-hello-classic-model"></a><span data-ttu-id="9b405-122">Étapes de l’exemple de déploiement dans le modèle classique de hello</span><span class="sxs-lookup"><span data-stu-id="9b405-122">Sample deployment steps in hello classic model</span></span>
<span data-ttu-id="9b405-123">Hello étapes suivantes montrent comment toouse hello CLI d’Azure toodeploy une machine virtuelle de SUSE Linux Enterprise Server 12 (SLES) SP1 HPC de hello Azure Marketplace, personnaliser et créer une image de machine virtuelle personnalisée.</span><span class="sxs-lookup"><span data-stu-id="9b405-123">hello following steps show how toouse hello Azure CLI toodeploy a SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM from hello Azure Marketplace, customize it, and create a custom VM image.</span></span> <span data-ttu-id="9b405-124">Ensuite, vous pouvez utiliser déploiement de hello tooscript hello image d’un cluster d’ordinateurs virtuels prenant en charge RDMA.</span><span class="sxs-lookup"><span data-stu-id="9b405-124">Then you can use hello image tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span>

> [!TIP]
> <span data-ttu-id="9b405-125">Utilisez similaire toodeploy comme un cluster d’ordinateurs virtuels prenant en charge RDMA basé sur des images HPC de base CentOS Bonjour Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="9b405-125">Use similar steps toodeploy a cluster of RDMA-capable VMs based on CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="9b405-126">Certaines étapes diffèrent légèrement, comme indiqué.</span><span class="sxs-lookup"><span data-stu-id="9b405-126">Some steps differ slightly, as noted.</span></span> 
>
>

### <a name="prerequisites"></a><span data-ttu-id="9b405-127">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9b405-127">Prerequisites</span></span>
* <span data-ttu-id="9b405-128">**Ordinateur client**: vous avez besoin d’un toocommunicate d’ordinateur client Mac, Linux ou Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="9b405-128">**Client computer**: You need a Mac, Linux, or Windows client computer toocommunicate with Azure.</span></span> <span data-ttu-id="9b405-129">Ces étapes supposent que vous utilisez un client Linux.</span><span class="sxs-lookup"><span data-stu-id="9b405-129">These steps assume you are using a Linux client.</span></span>
* <span data-ttu-id="9b405-130">**Abonnement Azure** : si vous n’en avez pas, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="9b405-130">**Azure subscription**: If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span> <span data-ttu-id="9b405-131">Pour les clusters de grande taille, envisagez de souscrire un abonnement de paiement à l’utilisation ou d’autres options d’achat.</span><span class="sxs-lookup"><span data-stu-id="9b405-131">For larger clusters, consider a pay-as-you-go subscription or other purchase options.</span></span>
* <span data-ttu-id="9b405-132">**Disponibilité de taille de machine virtuelle**: hello suivant des tailles d’instance est compatible RDMA : H16r, H16mr, A8 et A9.</span><span class="sxs-lookup"><span data-stu-id="9b405-132">**VM size availability**: hello following instance sizes are RDMA capable: H16r, H16mr, A8, and A9.</span></span> <span data-ttu-id="9b405-133">Pour connaître la disponibilité dans les différentes régions Azure, voir [Disponibilité des produits par région](https://azure.microsoft.com/regions/services/) .</span><span class="sxs-lookup"><span data-stu-id="9b405-133">Check [Products available by region](https://azure.microsoft.com/regions/services/) for availability in Azure regions.</span></span>
* <span data-ttu-id="9b405-134">**Quota de cœurs**: vous devrez peut-être le quota de hello tooincrease de cœurs toodeploy un cluster de machines virtuelles de calcul intensif.</span><span class="sxs-lookup"><span data-stu-id="9b405-134">**Cores quota**: You might need tooincrease hello quota of cores toodeploy a cluster of compute-intensive VMs.</span></span> <span data-ttu-id="9b405-135">Par exemple, vous devez au moins 128 cœurs si vous souhaitez toodeploy 8 machines virtuelles de A9 comme indiqué dans cet article.</span><span class="sxs-lookup"><span data-stu-id="9b405-135">For example, you need at least 128 cores if you want toodeploy 8 A9 VMs as shown in this article.</span></span> <span data-ttu-id="9b405-136">Votre abonnement peut également limiter hello nombre de cœurs, que vous pouvez déployer dans certaines familles de taille de machine virtuelle, y compris hello H-series.</span><span class="sxs-lookup"><span data-stu-id="9b405-136">Your subscription might also limit hello number of cores you can deploy in certain VM size families, including hello H-series.</span></span> <span data-ttu-id="9b405-137">un quota de toorequest augmenter, [ouvrir une demande de support client en ligne](../../../azure-supportability/how-to-create-azure-support-request.md) sans frais.</span><span class="sxs-lookup"><span data-stu-id="9b405-137">toorequest a quota increase, [open an online customer support request](../../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
* <span data-ttu-id="9b405-138">**CLI Azure**: [installer](../../../cli-install-nodejs.md) hello CLI d’Azure et [connecter tooyour abonnement Azure](../../../xplat-cli-connect.md) à partir de l’ordinateur client de hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-138">**Azure CLI**: [Install](../../../cli-install-nodejs.md) hello Azure CLI and [connect tooyour Azure subscription](../../../xplat-cli-connect.md) from hello client computer.</span></span>

### <a name="provision-an-sles-12-sp1-hpc-vm"></a><span data-ttu-id="9b405-139">Configurer une machine virtuelle SLES 12 SP1 HPC</span><span class="sxs-lookup"><span data-stu-id="9b405-139">Provision an SLES 12 SP1 HPC VM</span></span>
<span data-ttu-id="9b405-140">Une fois connectés tooAzure avec hello CLI d’Azure, exécutez `azure config list` tooconfirm qui hello sortie montre le mode de gestion de Service.</span><span class="sxs-lookup"><span data-stu-id="9b405-140">After signing in tooAzure with hello Azure CLI, run `azure config list` tooconfirm that hello output shows Service Management mode.</span></span> <span data-ttu-id="9b405-141">Si elle n’est pas le cas, définissez le mode hello en exécutant cette commande :</span><span class="sxs-lookup"><span data-stu-id="9b405-141">If it does not, set hello mode by running this command:</span></span>

    azure config mode asm


<span data-ttu-id="9b405-142">Tapez hello suivant toolist tous les abonnements hello vous toouse autorisé sont :</span><span class="sxs-lookup"><span data-stu-id="9b405-142">Type hello following toolist all hello subscriptions you are authorized toouse:</span></span>

    azure account list

<span data-ttu-id="9b405-143">abonnement actuel Hello est identifié avec `Current` défini trop`true`.</span><span class="sxs-lookup"><span data-stu-id="9b405-143">hello current active subscription is identified with `Current` set too`true`.</span></span> <span data-ttu-id="9b405-144">Si cet abonnement n’est pas hello celui que vous souhaitez toouse toocreate hello cluster, définissez les ID de l’abonnement approprié hello en tant qu’abonnement hello :</span><span class="sxs-lookup"><span data-stu-id="9b405-144">If this subscription isn't hello one you want toouse toocreate hello cluster, set hello appropriate subscription ID as hello active subscription:</span></span>

    azure account set <subscription-Id>

<span data-ttu-id="9b405-145">toosee hello disponibles publiquement images SLES 12 SP1 HPC dans Azure, exécutez une commande telle que hello suivant, en supposant que votre environnement de shell prend en charge **grep**:</span><span class="sxs-lookup"><span data-stu-id="9b405-145">toosee hello publicly available SLES 12 SP1 HPC images in Azure, run a command like hello following, assuming your shell environment supports **grep**:</span></span>

    azure vm image list | grep "suse.*hpc"

<span data-ttu-id="9b405-146">Configurer un ordinateur prenant en charge RDMA virtuel avec une image de SLES 12 SP1 HPC en exécutant une commande hello suivante :</span><span class="sxs-lookup"><span data-stu-id="9b405-146">Provision an RDMA-capable VM with a SLES 12 SP1 HPC image by running a command like hello following:</span></span>

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

<span data-ttu-id="9b405-147">Où :</span><span class="sxs-lookup"><span data-stu-id="9b405-147">Where:</span></span>

* <span data-ttu-id="9b405-148">taille de Hello (A9 dans cet exemple) est une des tailles de machine virtuelle hello prenant en charge RDMA.</span><span class="sxs-lookup"><span data-stu-id="9b405-148">hello size (A9 in this example) is one of hello RDMA-capable VM sizes.</span></span>
* <span data-ttu-id="9b405-149">numéro de port SSH externe Hello (22 dans cet exemple, qui est par défaut SSH de hello) est un numéro de port valide.</span><span class="sxs-lookup"><span data-stu-id="9b405-149">hello external SSH port number (22 in this example, which is hello SSH default) is any valid port number.</span></span> <span data-ttu-id="9b405-150">numéro de port SSH Hello interne a la valeur too22.</span><span class="sxs-lookup"><span data-stu-id="9b405-150">hello internal SSH port number is set too22.</span></span>
* <span data-ttu-id="9b405-151">Un nouveau service cloud est créé dans hello région Azure spécifiée par l’emplacement de hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-151">A new cloud service is created in hello Azure region specified by hello location.</span></span> <span data-ttu-id="9b405-152">Spécifiez un emplacement dans le machines virtuelles hello taille que vous choisissez est disponible.</span><span class="sxs-lookup"><span data-stu-id="9b405-152">Specify a location in which hello VM size you choose is available.</span></span>
* <span data-ttu-id="9b405-153">Pour un support de priorité SUSE (ce qui entraîne des frais supplémentaires), nom de l’image hello SLES 12 SP1 actuellement peut prendre l’une de ces deux options :</span><span class="sxs-lookup"><span data-stu-id="9b405-153">For SUSE priority support (which incurs additional charges), hello SLES 12 SP1 image name currently can be one of these two options:</span></span> 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a><span data-ttu-id="9b405-154">Personnaliser hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9b405-154">Customize hello VM</span></span>
<span data-ttu-id="9b405-155">Hello machine virtuelle après l’approvisionnement, SSH toohello machine virtuelle à l’aide de hello adresse IP externe de l’ordinateur virtuel (ou le nom DNS) et hello numéro de port externe que vous avez configuré et ensuite le personnaliser.</span><span class="sxs-lookup"><span data-stu-id="9b405-155">After hello VM finishes provisioning, SSH toohello VM by using hello VM's external IP address (or DNS name) and hello external port number you configured, and then customize it.</span></span> <span data-ttu-id="9b405-156">Pour plus d’informations de connexion, consultez [comment toolog sur l’ordinateur virtuel de tooa exécutant Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9b405-156">For connection details, see [How toolog on tooa virtual machine running Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9b405-157">Exécuter des commandes en tant qu’utilisateur hello que vous avez configurés sur hello machine virtuelle, sauf si l’accès à la racine est une étape de toocomplete requis.</span><span class="sxs-lookup"><span data-stu-id="9b405-157">Perform commands as hello user you configured on hello VM, unless root access is required toocomplete a step.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b405-158">Microsoft Azure ne fournit pas d’accès racine tooLinux VMs.</span><span class="sxs-lookup"><span data-stu-id="9b405-158">Microsoft Azure does not provide root access tooLinux VMs.</span></span> <span data-ttu-id="9b405-159">un accès administratif toogain lorsqu’il est connecté en tant qu’un utilisateur de toohello machine virtuelle, exécuter des commandes à l’aide de `sudo`.</span><span class="sxs-lookup"><span data-stu-id="9b405-159">toogain administrative access when connected as a user toohello VM, run commands by using `sudo`.</span></span>
>
>

* <span data-ttu-id="9b405-160">**Mises à jour** : installez les mises à jour à l’aide de zypper.</span><span class="sxs-lookup"><span data-stu-id="9b405-160">**Updates**: Install updates by using zypper.</span></span> <span data-ttu-id="9b405-161">Vous pourriez également des utilitaires NFS tooinstall.</span><span class="sxs-lookup"><span data-stu-id="9b405-161">You might also want tooinstall NFS utilities.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9b405-162">Dans une machine de HPC virtuelle SLES 12 SP1, nous vous recommandons de ne pas appliquer les mises à jour du noyau, ce qui peuvent entraîner des problèmes avec hello Linux RDMA pilotes.</span><span class="sxs-lookup"><span data-stu-id="9b405-162">In a SLES 12 SP1 HPC VM, we recommend that you don't apply kernel updates, which can cause issues with hello Linux RDMA drivers.</span></span>
  >
  >
* <span data-ttu-id="9b405-163">**Intel MPI**: installer hello d’Intel sur hello SLES 12 SP1 HPC virtuelle en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9b405-163">**Intel MPI**: Complete hello installation of Intel MPI on hello SLES 12 SP1 HPC VM by running hello following command:</span></span>

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* <span data-ttu-id="9b405-164">**Verrouiller la mémoire**: MPI codes toolock hello mémoire disponible pour RDMA, ajouter ou modifier des hello suivant les paramètres dans le fichier de /etc/security/limits.conf hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-164">**Lock memory**: For MPI codes toolock hello memory available for RDMA, add or change hello following settings in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="9b405-165">Vous devez tooedit d’accès racine de ce fichier.</span><span class="sxs-lookup"><span data-stu-id="9b405-165">You need root access tooedit this file.</span></span>

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > <span data-ttu-id="9b405-166">À des fins de test, vous pouvez également définir memlock toounlimited.</span><span class="sxs-lookup"><span data-stu-id="9b405-166">For testing purposes, you can also set memlock toounlimited.</span></span> <span data-ttu-id="9b405-167">Par exemple : `<User or group name>    hard    memlock unlimited`.</span><span class="sxs-lookup"><span data-stu-id="9b405-167">For example: `<User or group name>    hard    memlock unlimited`.</span></span> <span data-ttu-id="9b405-168">Pour plus d’informations, voir les [meilleures méthodes connues pour définir la taille de mémoire verrouillée](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span><span class="sxs-lookup"><span data-stu-id="9b405-168">For more information, see [Best known methods for setting locked memory size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span></span>
  >
  >
* <span data-ttu-id="9b405-169">**Clés SSH pour les machines virtuelles SLES**: générer SSH clés tooestablish confiance pour votre compte d’utilisateur entre hello nœuds hello SLES cluster de calcul lors de l’exécution des travaux MPI.</span><span class="sxs-lookup"><span data-stu-id="9b405-169">**SSH keys for SLES VMs**: Generate SSH keys tooestablish trust for your user account among hello compute nodes in hello SLES cluster when running MPI jobs.</span></span> <span data-ttu-id="9b405-170">Si vous avez déployé une machine virtuelle HPC basée sur CentOS, ne suivez pas cette étape.</span><span class="sxs-lookup"><span data-stu-id="9b405-170">If you deployed a CentOS-based HPC VM, don't follow this step.</span></span> <span data-ttu-id="9b405-171">Une fois que vous capturez l’image de hello et à déployez hello cluster, consultez les instructions plus loin dans cette tooset article passwordless SSH relation de confiance entre les nœuds de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-171">See instructions later in this article tooset up passwordless SSH trust among hello cluster nodes after you capture hello image and deploy hello cluster.</span></span>

    <span data-ttu-id="9b405-172">clés SSH toocreate, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="9b405-172">toocreate SSH keys, run hello following command.</span></span> <span data-ttu-id="9b405-173">Lorsque vous êtes invité pour l’entrée, sélectionnez **entrée** toogenerate les clés de hello dans l’emplacement par défaut de hello sans définir un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="9b405-173">When you are prompted for input, select **Enter** toogenerate hello keys in hello default location without setting a password.</span></span>

        ssh-keygen

    <span data-ttu-id="9b405-174">Ajouter le fichier d’authorized_keys hello toohello de clé publique pour les clés publiques connus.</span><span class="sxs-lookup"><span data-stu-id="9b405-174">Append hello public key toohello authorized_keys file for known public keys.</span></span>

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    <span data-ttu-id="9b405-175">Dans le répertoire de ~/.ssh hello, modifier ou créer le fichier de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-175">In hello ~/.ssh directory, edit or create hello config file.</span></span> <span data-ttu-id="9b405-176">Fournir plage d’adresses IP hello de réseau privé de hello que vous envisagez de toouse dans Azure (10.32.0.0/16 dans cet exemple) :</span><span class="sxs-lookup"><span data-stu-id="9b405-176">Provide hello IP address range of hello private network that you plan toouse in Azure (10.32.0.0/16 in this example):</span></span>

        host 10.32.0.*
        StrictHostKeyChecking no

    <span data-ttu-id="9b405-177">Vous pouvez également répertorier des adresse hello réseau privé de chaque machine virtuelle dans votre cluster comme suit :</span><span class="sxs-lookup"><span data-stu-id="9b405-177">Alternatively, list hello private network IP address of each VM in your cluster as follows:</span></span>

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > <span data-ttu-id="9b405-178">La configuration de `StrictHostKeyChecking no` peut créer un risque de sécurité potentiel si une adresse IP ou une plage d’adresses IP spécifiques ne sont pas spécifiées.</span><span class="sxs-lookup"><span data-stu-id="9b405-178">Configuring `StrictHostKeyChecking no` can create a potential security risk when a specific IP address or range is not specified.</span></span>
  >
  >
* <span data-ttu-id="9b405-179">**Applications**: installer des applications que vous avez besoin ou effectuez d’autres personnalisations avant de capturer l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-179">**Applications**: Install any applications you need or perform other customizations before you capture hello image.</span></span>

### <a name="capture-hello-image"></a><span data-ttu-id="9b405-180">Capturer l’image de hello</span><span class="sxs-lookup"><span data-stu-id="9b405-180">Capture hello image</span></span>
<span data-ttu-id="9b405-181">image de hello toocapture, exécutez d’abord hello suivant de commande de hello Linux VM.</span><span class="sxs-lookup"><span data-stu-id="9b405-181">toocapture hello image, first run hello following command on hello Linux VM.</span></span> <span data-ttu-id="9b405-182">Cette commande arrête hello machine virtuelle mais conserve les comptes d’utilisateur et les clés SSH que vous avez configurée.</span><span class="sxs-lookup"><span data-stu-id="9b405-182">This command deprovisions hello VM but maintains user accounts and SSH keys that you set up.</span></span>

```
sudo waagent -deprovision
```

<span data-ttu-id="9b405-183">À partir de votre ordinateur client, exécutez hello suivant l’image de hello de toocapture de commandes CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="9b405-183">From your client computer, run hello following Azure CLI commands toocapture hello image.</span></span> <span data-ttu-id="9b405-184">Pour plus d’informations, consultez [comment toocapture une machine virtuelle de Linux classique comme image](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="9b405-184">For more information, see [How toocapture a classic Linux virtual machine as an image](capture-image.md).</span></span>  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

<span data-ttu-id="9b405-185">Après avoir exécuté ces commandes, image de machine virtuelle hello est capturé pour votre utilisation et hello machine virtuelle est supprimé.</span><span class="sxs-lookup"><span data-stu-id="9b405-185">After you run these commands, hello VM image is captured for your use and hello VM is deleted.</span></span> <span data-ttu-id="9b405-186">Vous disposez à présent votre toodeploy prêt image personnalisée un cluster.</span><span class="sxs-lookup"><span data-stu-id="9b405-186">Now you have your custom image ready toodeploy a cluster.</span></span>

### <a name="deploy-a-cluster-with-hello-image"></a><span data-ttu-id="9b405-187">Déployer un cluster avec l’image de hello</span><span class="sxs-lookup"><span data-stu-id="9b405-187">Deploy a cluster with hello image</span></span>
<span data-ttu-id="9b405-188">Modifier hello script d’interpréteur de commandes avec les valeurs appropriées pour votre environnement suivant et exécutez-le à partir de votre ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="9b405-188">Modify hello following Bash script with appropriate values for your environment and run it from your client computer.</span></span> <span data-ttu-id="9b405-189">Étant donné que Azure déploie les machines virtuelles de hello en série dans le modèle de déploiement classique de hello, prend quelques minutes toodeploy hello huit machines virtuelles de A9 suggérés dans ce script.</span><span class="sxs-lookup"><span data-stu-id="9b405-189">Because Azure deploys hello VMs serially in hello classic deployment model, it takes a few minutes toodeploy hello eight A9 VMs suggested in this script.</span></span>

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a><span data-ttu-id="9b405-190">Considérations pour un cluster HPC CentOS</span><span class="sxs-lookup"><span data-stu-id="9b405-190">Considerations for a CentOS HPC cluster</span></span>
<span data-ttu-id="9b405-191">Si vous souhaitez tooset configuration d’un cluster basé sur l’une des images HPC de base CentOS hello Bonjour Azure Marketplace, au lieu de SLES 12 pour HPC, procédez hello général hello précédant la section.</span><span class="sxs-lookup"><span data-stu-id="9b405-191">If you want tooset up a cluster based on one of hello CentOS-based HPC images in hello Azure Marketplace instead of SLES 12 for HPC, follow hello general steps in hello preceding section.</span></span> <span data-ttu-id="9b405-192">Notez hello suivant différences lorsque vous configurez, configurez hello machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="9b405-192">Note hello following differences when you provision and configure hello VM:</span></span>

- <span data-ttu-id="9b405-193">Intel MPI est déjà installé sur une machine virtuelle approvisionnée à partir d’une image de HPC basée sur CentOS.</span><span class="sxs-lookup"><span data-stu-id="9b405-193">Intel MPI is already installed on a VM provisioned from a CentOS-based HPC image.</span></span>
- <span data-ttu-id="9b405-194">Verrouiller les paramètres de mémoire sont déjà ajoutés dans /etc/security/limits.conf fichier la machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-194">Lock memory settings are already added in hello VM's /etc/security/limits.conf file.</span></span>
- <span data-ttu-id="9b405-195">Ne pas générer les clés SSH sur hello machine virtuelle que vous configurez pour la capture.</span><span class="sxs-lookup"><span data-stu-id="9b405-195">Do not generate SSH keys on hello VM you provision for capture.</span></span> <span data-ttu-id="9b405-196">Au lieu de cela, nous vous recommandons de configurer l’authentification basée sur l’utilisateur après le déploiement de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-196">Instead, we recommend setting up user-based authentication after you deploy hello cluster.</span></span> <span data-ttu-id="9b405-197">Pour plus d’informations, consultez hello suivant la section.</span><span class="sxs-lookup"><span data-stu-id="9b405-197">For more information, see hello following section.</span></span>  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a><span data-ttu-id="9b405-198">Configurez passwordless approbation SSH sur le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="9b405-198">Set up passwordless SSH trust on hello cluster</span></span>
<span data-ttu-id="9b405-199">Sur un cluster HPC de base CentOS, il existe deux méthodes pour établir une approbation entre les nœuds de calcul hello : l’authentification basée sur l’hôte et l’authentification basée sur l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9b405-199">On a CentOS-based HPC cluster, there are two methods for establishing trust between hello compute nodes: host-based authentication and user-based authentication.</span></span> <span data-ttu-id="9b405-200">L’authentification basée sur l’hôte n’est pas décrite hello de cet article et doit généralement être effectuée via un script d’extension pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="9b405-200">Host-based authentication is outside of hello scope of this article and generally must be done through an extension script during deployment.</span></span> <span data-ttu-id="9b405-201">L’authentification basée sur l’utilisateur est pratique pour établir une approbation après le déploiement et requiert la génération de hello et le partage des clés SSH hello parmi les nœuds de calcul dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-201">User-based authentication is convenient for establishing trust after deployment and requires hello generation and sharing of SSH keys among hello compute nodes in hello cluster.</span></span> <span data-ttu-id="9b405-202">Cette méthode est communément appelée connexion SSH sans mot de passe. Elle est requise lors de l’exécution de travaux MPI.</span><span class="sxs-lookup"><span data-stu-id="9b405-202">This method is commonly known as passwordless SSH login and is required when running MPI jobs.</span></span>

<span data-ttu-id="9b405-203">Un exemple de script obtenue à partir de la Communauté de hello est disponible sur [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable l’authentification utilisateur simple sur un cluster HPC de base CentOS.</span><span class="sxs-lookup"><span data-stu-id="9b405-203">A sample script contributed from hello community is available on [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable easy user authentication on a CentOS-based HPC cluster.</span></span> <span data-ttu-id="9b405-204">Télécharger et utiliser ce script à l’aide de hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="9b405-204">Download and use this script by using hello following steps.</span></span> <span data-ttu-id="9b405-205">Vous pouvez également modifier ce script, ou utiliser n’importe quel autre méthode tooestablish passwordless SSH authentification entre les nœuds de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-205">You can also modify this script or use any other method tooestablish passwordless SSH authentication between hello cluster compute nodes.</span></span>

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

<span data-ttu-id="9b405-206">script de hello toorun, vous devez préfixe de hello tooknow pour vos adresses IP du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="9b405-206">toorun hello script, you need tooknow hello prefix for your subnet IP addresses.</span></span> <span data-ttu-id="9b405-207">Obtient le préfixe de hello en exécutant la commande suivante sur l’un des nœuds de cluster hello de hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-207">Get hello prefix by running hello following command on one of hello cluster nodes.</span></span> <span data-ttu-id="9b405-208">Votre sortie doit ressembler à 10.1.3.5 et préfixe de hello est la partie de hello 10.1.3.</span><span class="sxs-lookup"><span data-stu-id="9b405-208">Your output should look something like 10.1.3.5, and hello prefix is hello 10.1.3 portion.</span></span>

    ifconfig eth0 | grep -w inet | awk '{print $2}'

<span data-ttu-id="9b405-209">À présent exécuter script hello à l’aide de trois paramètres : hello utilisateur nom commun sur hello des nœuds de calcul, le mot de passe commun hello pour cet utilisateur hello sur les nœuds de calcul et du préfixe de sous-réseau de hello qui a été retourné à partir de la commande précédente hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-209">Now run hello script using three parameters: hello common user name on hello compute nodes, hello common password for that user on hello compute nodes, and hello subnet prefix that was returned from hello previous command.</span></span>

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

<span data-ttu-id="9b405-210">Ce script hello suivant :</span><span class="sxs-lookup"><span data-stu-id="9b405-210">This script does hello following:</span></span>

* <span data-ttu-id="9b405-211">Crée un répertoire sur le nœud d’hôte hello nommé .ssh, qui est requis pour la connexion passwordless.</span><span class="sxs-lookup"><span data-stu-id="9b405-211">Creates a directory on hello host node named .ssh, which is required for passwordless login.</span></span>
* <span data-ttu-id="9b405-212">Crée un fichier de configuration dans le répertoire .ssh hello qui indique la connexion de tooallow passwordless de connexion à partir de n’importe quel nœud dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-212">Creates a configuration file in hello .ssh directory that instructs passwordless login tooallow login from any node in hello cluster.</span></span>
* <span data-ttu-id="9b405-213">Crée des fichiers contenant les noms de nœud hello et les adresses IP de nœud de tous les nœuds hello dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-213">Creates files containing hello node names and node IP addresses for all hello nodes in hello cluster.</span></span> <span data-ttu-id="9b405-214">Ces fichiers sont conservés après l’exécution de script de hello pour référence ultérieure.</span><span class="sxs-lookup"><span data-stu-id="9b405-214">These files are left after hello script is run for later reference.</span></span>
* <span data-ttu-id="9b405-215">Crée une paire de clés privée et publique pour chaque nœud de cluster (y compris le nœud de l’hôte hello) et crée des entrées dans le fichier d’authorized_keys hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-215">Creates a private and public key pair for each cluster node (including hello host node) and creates entries in hello authorized_keys file.</span></span>

> [!WARNING]
> <span data-ttu-id="9b405-216">L’exécution de ce script peut créer un risque de sécurité potentiel.</span><span class="sxs-lookup"><span data-stu-id="9b405-216">Running this script can create a potential security risk.</span></span> <span data-ttu-id="9b405-217">Vérifiez que hello informations de clé publique ~/.ssh ne sont pas distribuées.</span><span class="sxs-lookup"><span data-stu-id="9b405-217">Ensure that hello public key information in ~/.ssh is not distributed.</span></span>
>
>

## <a name="configure-intel-mpi"></a><span data-ttu-id="9b405-218">Configurer Intel MPI</span><span class="sxs-lookup"><span data-stu-id="9b405-218">Configure Intel MPI</span></span>
<span data-ttu-id="9b405-219">toorun des applications MPI sur Azure Linux RDMA, vous devez tooconfigure certaine variables d’environnement spécifiques tooIntel MPI.</span><span class="sxs-lookup"><span data-stu-id="9b405-219">toorun MPI applications on Azure Linux RDMA, you need tooconfigure certain environment variables specific tooIntel MPI.</span></span> <span data-ttu-id="9b405-220">Voici un toorun de variables nécessaires exemple Bash script tooconfigure hello une application.</span><span class="sxs-lookup"><span data-stu-id="9b405-220">Here is a sample Bash script tooconfigure hello variables needed toorun an application.</span></span> <span data-ttu-id="9b405-221">Modifiez toompivars.sh de chemin d’accès hello en fonction des besoins de votre installation de Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="9b405-221">Change hello path toompivars.sh as needed for your installation of Intel MPI.</span></span>

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

<span data-ttu-id="9b405-222">format Hello du fichier d’hôte hello est comme suit.</span><span class="sxs-lookup"><span data-stu-id="9b405-222">hello format of hello host file is as follows.</span></span> <span data-ttu-id="9b405-223">Ajoutez une ligne pour chaque nœud de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="9b405-223">Add one line for each node in your cluster.</span></span> <span data-ttu-id="9b405-224">Spécifiez les adresses IP privées à partir du réseau virtuel de hello définie précédemment, pas les noms DNS.</span><span class="sxs-lookup"><span data-stu-id="9b405-224">Specify private IP addresses from hello virtual network defined earlier, not DNS names.</span></span> <span data-ttu-id="9b405-225">Par exemple, pour deux ordinateurs hôtes avec les adresses IP 10.32.0.1 et 10.32.0.2, fichier de hello contient suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="9b405-225">For example, for two hosts with IP addresses 10.32.0.1 and 10.32.0.2, hello file contains hello following:</span></span>

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a><span data-ttu-id="9b405-226">Exécuter MPI sur un cluster à deux nœuds de base</span><span class="sxs-lookup"><span data-stu-id="9b405-226">Run MPI on a basic two-node cluster</span></span>
<span data-ttu-id="9b405-227">Si vous n’avez pas déjà fait, définissez tout d’abord les environnement hello pour Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="9b405-227">If you haven't already done so, first set up hello environment for Intel MPI.</span></span>

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a><span data-ttu-id="9b405-228">Exécution d’une commande MPI</span><span class="sxs-lookup"><span data-stu-id="9b405-228">Run an MPI command</span></span>
<span data-ttu-id="9b405-229">Exécuter une commande MPI sur l’un des tooshow de nœuds de calcul hello MPI est correctement installé et peut communiquer au moins deux nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="9b405-229">Run an MPI command on one of hello compute nodes tooshow that MPI is installed properly and can communicate between at least two compute nodes.</span></span> <span data-ttu-id="9b405-230">suivant de Hello **mpirun** commande exécute hello **nom d’hôte** commande sur deux nœuds.</span><span class="sxs-lookup"><span data-stu-id="9b405-230">hello following **mpirun** command runs hello **hostname** command on two nodes.</span></span>

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
<span data-ttu-id="9b405-231">Votre sortie doit répertorier les noms de tous les nœuds hello que vous avez transmise en tant qu’entrée pour hello `-hosts`.</span><span class="sxs-lookup"><span data-stu-id="9b405-231">Your output should list hello names of all hello nodes that you passed as input for `-hosts`.</span></span> <span data-ttu-id="9b405-232">Par exemple, un **mpirun** commande avec deux nœuds retourne une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="9b405-232">For example, an **mpirun** command with two nodes returns output like hello following:</span></span>

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a><span data-ttu-id="9b405-233">Exécution d'un test d'évaluation MPI</span><span class="sxs-lookup"><span data-stu-id="9b405-233">Run an MPI benchmark</span></span>
<span data-ttu-id="9b405-234">Hello Intel MPI commande suivante exécute pingpong banc d’essai tooverify hello configuration et connexion toohello RDMA réseau du cluster.</span><span class="sxs-lookup"><span data-stu-id="9b405-234">hello following Intel MPI command runs a pingpong benchmark tooverify hello cluster configuration and connection toohello RDMA network.</span></span>

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

<span data-ttu-id="9b405-235">Sur un cluster opérationnel avec deux nœuds, vous devez voir la sortie suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="9b405-235">On a working cluster with two nodes, you should see output like hello following.</span></span> <span data-ttu-id="9b405-236">Sur le réseau RDMA Azure de hello, la latence ou inférieure à 3 microsecondes pour les formats de message des octets de too512 devrait.</span><span class="sxs-lookup"><span data-stu-id="9b405-236">On hello Azure RDMA network, expect latency at or below 3 microseconds for message sizes up too512 bytes.</span></span>

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
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

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
# List of Benchmarks toorun:
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



## <a name="next-steps"></a><span data-ttu-id="9b405-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9b405-237">Next steps</span></span>
* <span data-ttu-id="9b405-238">Déploiement et exécution de vos applications MPI Linux sur votre cluster Linux.</span><span class="sxs-lookup"><span data-stu-id="9b405-238">Deploy and run your Linux MPI applications on your Linux cluster.</span></span>
* <span data-ttu-id="9b405-239">Consultez hello [documentation de la bibliothèque de MPI Intel](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) pour obtenir des conseils sur Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="9b405-239">See hello [Intel MPI Library documentation](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) for guidance on Intel MPI.</span></span>
* <span data-ttu-id="9b405-240">Essayez une [modèle de démarrage rapide](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate un Lustre Intel cluster à l’aide d’une image basée sur CentOS HPC.</span><span class="sxs-lookup"><span data-stu-id="9b405-240">Try a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate an Intel Lustre cluster by using a CentOS-based HPC image.</span></span> <span data-ttu-id="9b405-241">Pour plus d’informations, consultez [Déploiement d’Intel Cloud Edition pour Lustre sur Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="9b405-241">For details, see [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span></span>
