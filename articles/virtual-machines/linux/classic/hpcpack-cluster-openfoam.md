---
title: aaaRun OpenFOAM avec HPC Pack sur les machines virtuelles Linux | Documents Microsoft
description: "Déployer un cluster Microsoft HPC Pack sur Azure et exécuter un travail OpenFOAM sur plusieurs nœuds de calcul RDMA."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="8c9c9-103">Exécuter OpenFoam avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure</span><span class="sxs-lookup"><span data-stu-id="8c9c9-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="8c9c9-104">Cet article vous montre une façon toorun OpenFoam dans des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-104">This article shows you one way toorun OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="8c9c9-105">Ici, vous déployez un cluster Microsoft HPC Pack avec des nœuds de calcul Linux sur Azure, et exécutez une tâche [OpenFoam](http://openfoam.com/) avec Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="8c9c9-106">Vous pouvez utiliser des machines virtuelles de Azure prend en charge RDMA pour les nœuds de calcul hello, afin que les nœuds de calcul hello communiquent sur le réseau RDMA Azure de hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-106">You can use RDMA-capable Azure VMs for hello compute nodes, so that hello compute nodes communicate over hello Azure RDMA network.</span></span> <span data-ttu-id="8c9c9-107">Autres toorun options OpenFoam dans Azure sont entièrement configuré commerciales images disponibles dans hello Marketplace, tels que de UberCloud [2.3 OpenFoam CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)et en exécutant sur [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span><span class="sxs-lookup"><span data-stu-id="8c9c9-107">Other options toorun OpenFoam in Azure include fully configured commercial images available in hello Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="8c9c9-108">OpenFOAM (acronyme d’Open Field Operation and Manipulation) est un logiciel open source de calcul de mécanique des fluides numérique largement utilisé en ingénierie et en sciences, tant au sein d’organisations commerciales que d’instituts universitaires.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="8c9c9-109">Il comprend des outils de maillage, notamment snappyHexMesh, un meilleur parallélisé pour les géométries de CAO complexes et de pré et post-traitement.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="8c9c9-110">Presque tous les processus s’exécutent en parallèle, l’activation des utilisateurs tootake pleinement parti du matériel informatique à leur disposition.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-110">Almost all processes run in parallel, enabling users tootake full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="8c9c9-111">Microsoft HPC Pack fournit des fonctionnalités toorun HPC à grande échelle et des applications parallèles, y compris des applications MPI sur des clusters de machines virtuelles Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-111">Microsoft HPC Pack provides features toorun large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="8c9c9-112">HPC Pack prend également en charge l’exécution d’applications Linux HPC sur les machines virtuelles de nœuds de calcul Linux déployées dans un cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="8c9c9-113">Consultez [prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md) pour une présentation toousing Linux de calcul des nœuds avec HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction toousing Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="8c9c9-114">Cet article explique comment toorun une charge de travail Linux MPI avec HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-114">This article illustrates how toorun a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="8c9c9-115">Il suppose que vous êtes familiarisé avec l’administration du système Linux et l’exécution de charges de travail MPI sur des clusters Linux.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="8c9c9-116">Si vous utilisez des versions de MPI et OpenFOAM différent de ceux indiqués dans cet article de hello, vous pouvez avoir toomodify certaines étapes d’installation et de configuration.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-116">If you use versions of MPI and OpenFOAM different from hello ones shown in this article, you might have toomodify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="8c9c9-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8c9c9-117">Prerequisites</span></span>
* <span data-ttu-id="8c9c9-118">**Cluster HPC Pack avec nœuds de calcul Linux prenant en charge RDMA** : déployez un cluster HPC Pack avec des nœuds de calcul Linux de taille A8, A9, H16r ou H16rm à l’aide d’un [modèle Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) ou d’un [script Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="8c9c9-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="8c9c9-119">Consultez [prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md) pour les conditions préalables de hello et étapes dans les deux cas.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="8c9c9-120">Si vous choisissez hello option de déploiement de script PowerShell, consultez le fichier de configuration d’exemple hello dans les fichiers d’exemple hello à fin hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-120">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="8c9c9-121">Utilisez ce cluster de HPC Pack configuration toodeploy basé sur un Azure consistant en un nœud principal de taille A8 Windows Server 2012 R2 et les nœuds de calcul de taille de 2 A8 SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-121">Use this configuration toodeploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="8c9c9-122">Remplacez les valeurs appropriées pour les noms de vos abonnement et service.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="8c9c9-123">**Autres informations tooknow**</span><span class="sxs-lookup"><span data-stu-id="8c9c9-123">**Additional things tooknow**</span></span>
  
  * <span data-ttu-id="8c9c9-124">Pour connaître les conditions préalables à la mise en réseau RDMA Linux dans Azure, consultez [Tailles de machines virtuelles de calcul haute performance](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8c9c9-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="8c9c9-125">Si vous utilisez hello option de déploiement de script Powershell, déployer tous les nœuds de calcul Linux hello au sein de la connexion de réseau d’un cloud service toouse hello RDMA.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-125">If you use hello Powershell script deployment option, deploy all hello Linux compute nodes within one cloud service toouse hello RDMA network connection.</span></span>
  * <span data-ttu-id="8c9c9-126">Après le déploiement de nœuds de Linux hello, connectez-vous à SSH tooperform les tâches d’administration supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-126">After deploying hello Linux nodes, connect by SSH tooperform any additional administrative tasks.</span></span> <span data-ttu-id="8c9c9-127">Trouver les détails de la connexion SSH hello pour chaque VM Linux Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-127">Find hello SSH connection details for each Linux VM in hello Azure portal.</span></span>  
* <span data-ttu-id="8c9c9-128">**Intel MPI** -toorun OpenFOAM SLES 12 HPC sur les nœuds de calcul dans Azure, vous devez tooinstall hello Intel MPI bibliothèque 5 runtime hello [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span><span class="sxs-lookup"><span data-stu-id="8c9c9-128">**Intel MPI** - toorun OpenFOAM on SLES 12 HPC compute nodes in Azure, you need tooinstall hello Intel MPI Library 5 runtime from hello [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="8c9c9-129">(Intel MPI 5 est préinstallé sur des images HPC basées sur CentOS.)  Si nécessaire, vous devez ensuite installer Intel MPI sur vos nœuds de calcul Linux.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="8c9c9-130">tooprepare pour cette étape, après avoir inscrit avec Intel, procédez comme lien hello hello confirmation par courrier électronique toohello connexes des pages web.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-130">tooprepare for this step, after you register with Intel, follow hello link in hello confirmation email toohello related web page.</span></span> <span data-ttu-id="8c9c9-131">Ensuite, hello de copie télécharger le lien pour la version appropriée de hello d’Intel sur le fichier .tgz hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-131">Then, copy hello download link for hello .tgz file for hello appropriate version of Intel MPI.</span></span> <span data-ttu-id="8c9c9-132">Cet article est basé sur Intel MPI version 5.0.3.048.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="8c9c9-133">**Pack de Source OpenFOAM** -télécharger le logiciel de OpenFOAM Source Pack hello pour Linux à partir de hello [site OpenFOAM Foundation](http://openfoam.org/download/2-3-1-source/).</span><span class="sxs-lookup"><span data-stu-id="8c9c9-133">**OpenFOAM Source Pack** - Download hello OpenFOAM Source Pack software for Linux from hello [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="8c9c9-134">Cet article est basé sur la version du Pack Source 2.3.1, disponible en téléchargement en tant que OpenFOAM 2.3.1.tgz.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="8c9c9-135">Suivez les instructions de hello plus loin dans cet article de toounpack et OpenFOAM se compiler sur les nœuds de calcul Linux hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-135">Follow hello instructions later in this article toounpack and compile OpenFOAM on hello Linux compute nodes.</span></span>
* <span data-ttu-id="8c9c9-136">**EnSight** (facultatif) : résultats de hello toosee de votre simulation OpenFOAM, télécharger et installer hello [EnSight](https://www.ceisoftware.com/download/) programme de visualisation et d’analyse.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-136">**EnSight** (optional) - toosee hello results of your OpenFOAM simulation, download and install hello [EnSight](https://www.ceisoftware.com/download/) visualization and analysis program.</span></span> <span data-ttu-id="8c9c9-137">Informations de licence et de téléchargement sont sur le site de EnSight hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-137">Licensing and download information are at hello EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="8c9c9-138">Configuration de l’approbation mutuelle entre les nœuds de calcul</span><span class="sxs-lookup"><span data-stu-id="8c9c9-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="8c9c9-139">L’exécution d’une tâche entre nœuds sur plusieurs nœuds Linux requiert hello nœuds tootrust eux (par **rsh** ou **ssh**).</span><span class="sxs-lookup"><span data-stu-id="8c9c9-139">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="8c9c9-140">Lorsque vous créez un cluster HPC Pack de hello avec hello script de déploiement Microsoft HPC Pack IaaS, script de hello configure automatiquement permanente confiance mutuelle pour le compte administrateur hello que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-140">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="8c9c9-141">Pour les utilisateurs non-administrateurs que vous créez dans le domaine de ce cluster hello, vous avez tooset temporaire approbation mutuelle entre les nœuds de hello quand un travail est alloué toothem et détruire la relation de hello après que hello tâche est terminée.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-141">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem, and destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="8c9c9-142">approbation tooestablish pour chaque utilisateur, fournissez un cluster de toohello de paire de clés RSA HPC Pack utilise pour la relation d’approbation hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-142">tooestablish trust for each user, provide an RSA key pair toohello cluster that HPC Pack uses for hello trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="8c9c9-143">Génération d’une paire de clés RSA</span><span class="sxs-lookup"><span data-stu-id="8c9c9-143">Generate an RSA key pair</span></span>
<span data-ttu-id="8c9c9-144">Il est facile toogenerate une paire de clés RSA, qui contient une clé publique et une clé privée, en exécutant hello Linux **ssh-keygen** commande.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-144">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="8c9c9-145">Ouvrez une session tooa ordinateur Linux.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-145">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="8c9c9-146">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8c9c9-146">Run hello following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="8c9c9-147">Appuyez sur **entrée** toouse hello paramètres jusqu'à ce que la commande hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-147">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="8c9c9-148">N'entrez pas de phrase secrète ici ; à l'invite de mot de passe, appuyez simplement sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Génération d’une paire de clés RSA][keygen]
3. <span data-ttu-id="8c9c9-150">Modification toohello ~/.ssh répertoire.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-150">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="8c9c9-151">clé privée de Hello est stockée dans la clé publique id_rsa et hello dans id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-151">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![Clés publiques et privées][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="8c9c9-153">Ajouter un cluster de HPC Pack toohello hello paire de clés</span><span class="sxs-lookup"><span data-stu-id="8c9c9-153">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="8c9c9-154">Rendre un nœud de tête du tooyour de connexion Bureau à distance avec votre compte d’administrateur de HPC Pack (compte d’administrateur hello configuré lors de l’exécution du script de déploiement hello).</span><span class="sxs-lookup"><span data-stu-id="8c9c9-154">Make a Remote Desktop connection tooyour head node with your HPC Pack administrator account (hello administrator account you set up when you ran hello deployment script).</span></span>
2. <span data-ttu-id="8c9c9-155">Utilisez toocreate de procédures standard Windows Server un compte d’utilisateur de domaine dans le domaine d’Active Directory du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-155">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="8c9c9-156">Par exemple, utiliser hello utilisateur Active Directory et outil d’ordinateurs sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-156">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="8c9c9-157">les exemples de Hello dans cet article supposent que vous créez un utilisateur de domaine nommé hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-157">hello examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="8c9c9-158">Créez un fichier nommé C:\cred.xml et copier hello RSA clé des données dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-158">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="8c9c9-159">Un exemple de fichier cred.xml est à la fin de hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-159">A sample cred.xml file is at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="8c9c9-160">Ouvrez une invite de commandes et entrez hello tooset hello données hello hpclab\hpcuser compte les informations d’identification de commande suivante.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-160">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="8c9c9-161">Vous utilisez hello **extendeddata** toopass de paramètre hello nom de fichier C:\cred.xml que vous avez créé pour les données de clé hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-161">You use hello **extendeddata** parameter toopass hello name of C:\cred.xml file you created for hello key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="8c9c9-162">Cette commande se termine correctement sans sortie.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-162">This command completes successfully without output.</span></span> <span data-ttu-id="8c9c9-163">Après avoir défini les informations d’identification hello pour les comptes d’utilisateur hello que vous devez toorun travaux, stockez le fichier de cred.xml de hello dans un emplacement sécurisé ou supprimez-le.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-163">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="8c9c9-164">Si vous avez généré hello paire de clés RSA sur l’un de vos nœuds de Linux, n’oubliez pas les clés hello toodelete après avoir terminé leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-164">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="8c9c9-165">HPC Pack recherche un fichier id_rsa ou id_rsa.pub existant. Il ne configure pas d’approbation mutuelle.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c9c9-166">Nous ne recommandons l’exécution d’un travail de Linux en tant qu’un administrateur de cluster sur un cluster partagé, car une tâche envoyée par un administrateur s’exécute sous un compte de racine hello des nœuds de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="8c9c9-167">Toutefois, une tâche envoyée par un utilisateur non administrateur s’exécute sous un compte d’utilisateur local Linux avec hello même nom en tant qu’utilisateur de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-167">However, a job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="8c9c9-168">Dans ce cas, HPC Pack définit confiance mutuelle pour cet utilisateur Linux sur les nœuds hello allouées toohello travail.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-168">In this case, HPC Pack sets up mutual trust for this Linux user across hello nodes allocated toohello job.</span></span> <span data-ttu-id="8c9c9-169">Vous pouvez configurer des utilisateurs de Linux hello manuellement sur les nœuds de Linux hello avant d’exécuter le travail de hello ou HPC Pack crée automatiquement les utilisateur hello lorsque le travail de hello est envoyé.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-169">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="8c9c9-170">Si HPC Pack crée un utilisateur de hello, HPC Pack supprime une fois hello travail terminé.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-170">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="8c9c9-171">menaces de sécurité tooreduce, HPC Pack supprime les clés de hello après l’achèvement du travail.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-171">tooreduce security threats, HPC Pack removes hello keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="8c9c9-172">Configuration d’un partage de fichiers pour les nœuds Linux</span><span class="sxs-lookup"><span data-stu-id="8c9c9-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="8c9c9-173">Maintenant configurer un partage SMB standard sur un dossier sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-173">Now set up a standard SMB share on a folder on hello head node.</span></span> <span data-ttu-id="8c9c9-174">tooallow hello Linux nœuds tooaccess fichiers d’application avec un chemin d’accès commun, montage hello dossier partagé sur les nœuds de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-174">tooallow hello Linux nodes tooaccess application files with a common path, mount hello shared folder on hello Linux nodes.</span></span> <span data-ttu-id="8c9c9-175">Si vous le souhaitez, vous pouvez utiliser une autre option de partage de fichier telle que le partage de fichiers Azure (recommandé dans de nombreux scénarios) ou un partage NFS.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="8c9c9-176">Consultez le fichier hello partager des informations et des instructions détaillées dans [prise en main des nœuds de calcul Linux dans un Cluster HPC Pack dans Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="8c9c9-176">See hello file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="8c9c9-177">Créez un dossier sur le nœud principal de hello et partagez-le tooEveryone en définissant des privilèges de lecture/écriture.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-177">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="8c9c9-178">Par exemple, partager C:\OpenFOAM sur le nœud principal de hello en tant que \\ \\SUSE12RDMA-HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-178">For example, share C:\OpenFOAM on hello head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="8c9c9-179">Ici, *SUSE12RDMA-HN* est le nom d’hôte hello de nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-179">Here, *SUSE12RDMA-HN* is hello host name of hello head node.</span></span>
2. <span data-ttu-id="8c9c9-180">Ouvrez une fenêtre Windows PowerShell et exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="8c9c9-180">Open a Windows PowerShell window and run hello following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="8c9c9-181">Hello première commande crée un dossier nommé /openfoam sur tous les nœuds dans le groupe de LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-181">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="8c9c9-182">commande deuxième Hello monte hello partagé dossier //SUSE12RDMA-HN/OpenFOAM des nœuds de Linux hello avec dir_mode et file_mode too777 d’ensemble de bits.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-182">hello second command mounts hello shared folder //SUSE12RDMA-HN/OpenFOAM on hello Linux nodes with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="8c9c9-183">Hello *nom d’utilisateur* et *mot de passe* Bonjour commande doit-elle être des informations d’identification de hello d’un utilisateur sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-183">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="8c9c9-184">Hello »\\`« symbole dans la deuxième commande de hello est un symbole d’échappement pour PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-184">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="8c9c9-185">«\\`, « signifie hello », » (virgule) est une partie de la commande hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-185">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="8c9c9-186">Installer MPI et OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="8c9c9-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="8c9c9-187">toorun OpenFOAM comme un travail MPI sur le réseau de hello RDMA, vous devez toocompile OpenFOAM avec les bibliothèques Intel MPI hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-187">toorun OpenFOAM as an MPI job on hello RDMA network, you need toocompile OpenFOAM with hello Intel MPI libraries.</span></span> 

<span data-ttu-id="8c9c9-188">Tout d’abord, exécuter plusieurs **clusrun** des commandes telles que les bibliothèques Intel MPI tooinstall (le cas échéant) et OpenFOAM sur vos nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-188">First, run several **clusrun** commands tooinstall Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="8c9c9-189">Partage de nœud principal Utilisez hello configuré précédemment fichiers d’installation hello tooshare entre les nœuds de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-189">Use hello head node share configured previously tooshare hello installation files among hello Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c9c9-190">Ces étapes d’installation et de compilation sont des exemples.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="8c9c9-191">Vous devez avoir quelques connaissances de Linux système administration tooensure que les bibliothèques et les compilateurs dépendants sont installés correctement.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-191">You need some knowledge of Linux system administration tooensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="8c9c9-192">Vous devrez peut-être toomodify certaines variables d’environnement ou d’autres paramètres pour les versions de Intel MPI et OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-192">You might need toomodify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="8c9c9-193">Pour plus de détails, voir [Guide d’installation de la bibliothèque Intel MPI pour Linux](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) et [Installation du pack source d’OpenFOAM](http://openfoam.org/download/2-3-1-source/) pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="8c9c9-194">Installer Intel MPI</span><span class="sxs-lookup"><span data-stu-id="8c9c9-194">Install Intel MPI</span></span>
<span data-ttu-id="8c9c9-195">Enregistrer package d’installation téléchargé hello pour Intel MPI (l_mpi_p_5.0.3.048.tgz dans cet exemple) dans C:\OpenFoam sur le nœud principal de hello afin que les nœuds de Linux hello peuvent accéder à ce fichier à partir de /openfoam.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-195">Save hello downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="8c9c9-196">Puis exécutez **clusrun** bibliothèque d’Intel MPI tooinstall sur tous les nœuds de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-196">Then run **clusrun** tooinstall Intel MPI library on all hello Linux nodes.</span></span>

1. <span data-ttu-id="8c9c9-197">Voici de Hello commandes package d’installation copie hello, extrayez-le trop/opt/intel sur chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-197">hello following commands copy hello installation package and extract it too/opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="8c9c9-198">tooinstall Intel MPI bibliothèque utilisez en mode silencieux, un fichier silent.cfg.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-198">tooinstall Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="8c9c9-199">Vous trouverez un exemple Bonjour exemples de fichiers à la fin de hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-199">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="8c9c9-200">Place ce fichier dans hello partagé /openfoam du dossier.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-200">Place this file in hello shared folder /openfoam.</span></span> <span data-ttu-id="8c9c9-201">Pour plus d’informations sur le fichier de silent.cfg hello, consultez [Intel MPI Library for Linux Installation Guide - Installation sans assistance](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span><span class="sxs-lookup"><span data-stu-id="8c9c9-201">For details about hello silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="8c9c9-202">Assurez-vous que vous enregistrez votre fichier .cfg silencieux en tant que fichier texte avec des fins de ligne Linux (LF uniquement, et non CR LF).</span><span class="sxs-lookup"><span data-stu-id="8c9c9-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="8c9c9-203">Cette étape permet de s’assurer qu’elle s’exécute correctement sur les nœuds de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-203">This step ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="8c9c9-204">Installez la bibliothèque MPI Intel en mode silencieux.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="8c9c9-205">Configuration de MPI</span><span class="sxs-lookup"><span data-stu-id="8c9c9-205">Configure MPI</span></span>
<span data-ttu-id="8c9c9-206">Pour le test, vous devez ajouter hello suivant des lignes toohello /etc/security/limits.conf sur chacun des nœuds de Linux hello :</span><span class="sxs-lookup"><span data-stu-id="8c9c9-206">For testing, you should add hello following lines toohello /etc/security/limits.conf on each of hello Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="8c9c9-207">Redémarrez les nœuds de Linux hello une fois que vous mettez à jour le fichier de limits.conf hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-207">Restart hello Linux nodes after you update hello limits.conf file.</span></span> <span data-ttu-id="8c9c9-208">Par exemple, utilisez hello qui suit **clusrun** commande :</span><span class="sxs-lookup"><span data-stu-id="8c9c9-208">For example, use hello following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="8c9c9-209">Après avoir redémarré, vérifiez que ce dossier partagé hello est monté en tant que /openfoam.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-209">After restarting, ensure that hello shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="8c9c9-210">Compiler et installer OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="8c9c9-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="8c9c9-211">Enregistrez le package d’installation téléchargé hello pour hello tooC:\OpenFoam de OpenFOAM Source Pack (OpenFOAM 2.3.1.tgz dans cet exemple) sur le nœud principal de hello afin que les nœuds de Linux hello peuvent accéder à ce fichier à partir de /openfoam.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-211">Save hello downloaded installation package for hello OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) tooC:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="8c9c9-212">Puis exécutez **clusrun** commandes toocompile OpenFOAM sur tous les hello des nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-212">Then run **clusrun** commands toocompile OpenFOAM on all hello Linux nodes.</span></span>

1. <span data-ttu-id="8c9c9-213">Créer un dossier /opt/OpenFOAM sur chaque nœud de Linux, copier hello source package toothis le dossier et il l’extraire.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-213">Create a folder /opt/OpenFOAM on each Linux node, copy hello source package toothis folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="8c9c9-214">toocompile OpenFOAM avec hello Intel MPI bibliothèque, définissez tout d’abord certaines variables d’environnement pour Intel MPI et OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-214">toocompile OpenFOAM with hello Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="8c9c9-215">Utiliser un script d’interpréteur de commandes appelé settings.sh tooset hello variables.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-215">Use a bash script called settings.sh tooset hello variables.</span></span> <span data-ttu-id="8c9c9-216">Vous trouverez un exemple Bonjour exemples de fichiers à la fin de hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-216">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="8c9c9-217">Place ce fichier (à des fins de ligne Linux) Bonjour partagé /openfoam du dossier.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-217">Place this file (saved with Linux line endings) in hello shared folder /openfoam.</span></span> <span data-ttu-id="8c9c9-218">Ce fichier contient également des paramètres pour hello MPI OpenFOAM composants d’exécution et que vous utilisez ultérieure toorun un travail OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-218">This file also contains settings for hello MPI and OpenFOAM runtimes that you use later toorun an OpenFOAM job.</span></span>
3. <span data-ttu-id="8c9c9-219">Installer des packages dépendants nécessités toocompile OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-219">Install dependent packages needed toocompile OpenFOAM.</span></span> <span data-ttu-id="8c9c9-220">En fonction de votre distribution Linux, vous devrez tout d’abord tooadd un référentiel.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-220">Depending on your Linux distribution, you might first need tooadd a repository.</span></span> <span data-ttu-id="8c9c9-221">Exécutez **clusrun** commandes similaires toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="8c9c9-221">Run **clusrun** commands similar toohello following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="8c9c9-222">Si nécessaire, hello toorun SSH tooeach Linux nœud commandes tooconfirm qu’ils s’exécutent correctement.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-222">If necessary, SSH tooeach Linux node toorun hello commands tooconfirm that they run properly.</span></span>
4. <span data-ttu-id="8c9c9-223">Exécutez hello suivant commande toocompile OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-223">Run hello following command toocompile OpenFOAM.</span></span> <span data-ttu-id="8c9c9-224">processus de compilation Hello prend quelques toocomplete de temps et génère une grande quantité de sortie toostandard informations du journal, par conséquent, utilisez hello **/ entrelacées** option de sortie de hello toodisplay entrelacée.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-224">hello compilation process takes some time toocomplete and generates a large amount of log information toostandard output, so use hello **/interleaved** option toodisplay hello output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="8c9c9-225">Hello »\\`« symbole dans la commande hello est un symbole d’échappement pour PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-225">hello “\\`” symbol in hello command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="8c9c9-226">«\\`& » signifie hello « & » fait partie de la commande hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-226">“\\`&” means hello “&” is a part of hello command.</span></span>
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a><span data-ttu-id="8c9c9-227">Préparer toorun une tâche de OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="8c9c9-227">Prepare toorun an OpenFOAM job</span></span>
<span data-ttu-id="8c9c9-228">Maintenant get prêt toorun un travail MPI appelée sloshingTank3D, qui est un des exemples de OpenFoam hello, sur les deux nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-228">Now get ready toorun an MPI job called sloshingTank3D, which is one of hello OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-hello-runtime-environment"></a><span data-ttu-id="8c9c9-229">Configurer l’environnement d’exécution hello</span><span class="sxs-lookup"><span data-stu-id="8c9c9-229">Set up hello runtime environment</span></span>
<span data-ttu-id="8c9c9-230">tooset des environnements d’exécution hello pour MPI et OpenFOAM des nœuds de Linux hello, exécutez hello suivant de commande dans une fenêtre Windows PowerShell sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-230">tooset up hello runtime environments for MPI and OpenFOAM on hello Linux nodes, run hello following command in a Windows PowerShell window on hello head node.</span></span> <span data-ttu-id="8c9c9-231">(Cette commande est valide pour SUSE Linux uniquement.)</span><span class="sxs-lookup"><span data-stu-id="8c9c9-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="8c9c9-232">Préparer l’exemple de données</span><span class="sxs-lookup"><span data-stu-id="8c9c9-232">Prepare sample data</span></span>
<span data-ttu-id="8c9c9-233">Partage de nœud principal Utilisez hello configurées précédemment tooshare des fichiers entre les nœuds de Linux hello (montés en tant que /openfoam).</span><span class="sxs-lookup"><span data-stu-id="8c9c9-233">Use hello head node share you configured previously tooshare files among hello Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="8c9c9-234">Nœuds de calcul tooone SSH de votre Linux.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-234">SSH tooone of your Linux compute nodes.</span></span>
2. <span data-ttu-id="8c9c9-235">Exécutez hello suivant tooset de commande d’environnement d’exécution hello OpenFOAM si vous n’avez pas déjà fait.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-235">Run hello following command tooset up hello OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="8c9c9-236">Copier le dossier partagé du toohello exemple sloshingTank3D hello et accédez tooit.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-236">Copy hello sloshingTank3D sample toohello shared folder and navigate tooit.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="8c9c9-237">Lorsque vous utilisez les paramètres par défaut de hello de cet exemple, il peut prendre des dizaines de minutes toorun, vous pouvez donc toomodify certains toomake paramètres il s’exécuter plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-237">When you use hello default parameters of this sample, it can take tens of minutes toorun, so you might want toomodify some parameters toomake it run faster.</span></span> <span data-ttu-id="8c9c9-238">Un choix simple est toomodify hello temps étape variables deltaT et writeInterval dans le fichier du système/controlDict hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-238">One simple choice is toomodify hello time step variables deltaT and writeInterval in hello system/controlDict file.</span></span> <span data-ttu-id="8c9c9-239">Ce fichier stocke toutes les données d’entrée relatives contrôle toohello de temps et de la lecture et l’écriture des données de la solution.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-239">This file stores all input data relating toohello control of time and reading and writing solution data.</span></span> <span data-ttu-id="8c9c9-240">Par exemple, vous pouvez modifier la valeur hello deltaT de 0,05 too0.5 et valeur hello writeInterval de 0,05 too0.5.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-240">For example, you could change hello value of deltaT from 0.05 too0.5 and hello value of writeInterval from 0.05 too0.5.</span></span>
   
   ![Modifier les variables d’étape][step_variables]
5. <span data-ttu-id="8c9c9-242">Spécifiez les valeurs souhaitées pour les variables de hello dans le fichier du système/decomposeParDict hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-242">Specify desired values for hello variables in hello system/decomposeParDict file.</span></span> <span data-ttu-id="8c9c9-243">Cet exemple utilise deux nœuds Linux chaque avec 8 cœurs, définissez donc numberOfSubdomains too16 et n de hierarchicalCoeffs too(1 1 16), ce qui signifie qu’exécuter OpenFOAM en parallèle avec les 16 processus.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains too16 and n of hierarchicalCoeffs too(1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="8c9c9-244">Pour plus d’informations, consultez [Guide de l’utilisateur OpenFOAM : 3.4 Exécution d’applications en parallèle](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span><span class="sxs-lookup"><span data-stu-id="8c9c9-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![Décomposer les processus][decompose]
6. <span data-ttu-id="8c9c9-246">Exécutez hello suivant les commandes à partir de hello sloshingTank3D Active tooprepare hello exemples de données.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-246">Run hello following commands from hello sloshingTank3D directory tooprepare hello sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="8c9c9-247">Sur le nœud principal de hello, vous devez voir des fichiers de données exemple hello sont copiés dans C:\OpenFoam\sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-247">On hello head node, you should see hello sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="8c9c9-248">(C:\OpenFoam est dossier partagé de hello sur le nœud principal de hello).</span><span class="sxs-lookup"><span data-stu-id="8c9c9-248">(C:\OpenFoam is hello shared folder on hello head node.)</span></span>
   
   ![Fichiers de données sur le nœud principal de hello][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="8c9c9-250">Fichier hôte pour mpirun</span><span class="sxs-lookup"><span data-stu-id="8c9c9-250">Host file for mpirun</span></span>
<span data-ttu-id="8c9c9-251">Dans cette étape, vous créez un fichier d’hôte (il s’agit d’une liste de nœuds de calcul) qui hello **mpirun** commande utilise.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-251">In this step, you create a host file (a list of compute nodes) which hello **mpirun** command uses.</span></span>

1. <span data-ttu-id="8c9c9-252">Sur l’un des nœuds de Linux hello, créez un fichier nommé fichier hôte sous /openfoam, donc ce fichier peut être atteint à /openfoam/hostfile sur tous les nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-252">On one of hello Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="8c9c9-253">Écrivez vos noms de nœud Linux dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="8c9c9-254">Dans cet exemple, les fichiers hello contient hello nom :</span><span class="sxs-lookup"><span data-stu-id="8c9c9-254">In this example, hello file contains hello following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="8c9c9-255">Vous pouvez également créer ce fichier à C:\OpenFoam\hostfile sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-255">You can also create this file at C:\OpenFoam\hostfile on hello head node.</span></span> <span data-ttu-id="8c9c9-256">Si vous optez pour cette solution, enregistrez le fichier au format texte avec des fins de lignes Linux (LF uniquement, pas CR LF).</span><span class="sxs-lookup"><span data-stu-id="8c9c9-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="8c9c9-257">Cela garantit qu’elle s’exécute correctement sur les nœuds de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-257">This ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="8c9c9-258">**Wrapper de script d’interpréteur de commandes**</span><span class="sxs-lookup"><span data-stu-id="8c9c9-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="8c9c9-259">Si vous disposez de nombreux nœuds Linux et vous souhaitez que votre toorun de travail uniquement sur certaines d'entre elles, il n’est pas un toouse conseillé de fichiers, un hôte fixe, car vous ne connaissez pas les nœuds qui seront allouées tooyour travail.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-259">If you have many Linux nodes and you want your job toorun on only some of them, it’s not a good idea toouse a fixed host file, because you don’t know which nodes will be allocated tooyour job.</span></span> <span data-ttu-id="8c9c9-260">Dans ce cas, écrire un wrapper un interpréteur de commandes de script pour **mpirun** toocreate hello automatiquement les fichiers de l’ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-260">In this case, write a bash script wrapper for **mpirun** toocreate hello host file automatically.</span></span> <span data-ttu-id="8c9c9-261">Vous pouvez trouver un wrapper de script exemple un interpréteur de commandes appelé hpcimpirun.sh à fin hello de cet article et l’enregistrer en tant que /openfoam/hpcimpirun.sh. Cet exemple de script hello suivant :</span><span class="sxs-lookup"><span data-stu-id="8c9c9-261">You can find an example bash script wrapper called hpcimpirun.sh at hello end of this article, and save it as /openfoam/hpcimpirun.sh. This example script does hello following:</span></span>
   
   1. <span data-ttu-id="8c9c9-262">Définit les variables d’environnement hello pour **mpirun**et certains travail MPI addition commande paramètres toorun hello via réseau RDMA de hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-262">Sets up hello environment variables for **mpirun**, and some addition command parameters toorun hello MPI job through hello RDMA network.</span></span> <span data-ttu-id="8c9c9-263">Dans ce cas, il définit hello suivant variables :</span><span class="sxs-lookup"><span data-stu-id="8c9c9-263">In this case, it sets hello following variables:</span></span>
      
      * <span data-ttu-id="8c9c9-264">I_MPI_FABRICS=shm:dapl</span><span class="sxs-lookup"><span data-stu-id="8c9c9-264">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="8c9c9-265">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span><span class="sxs-lookup"><span data-stu-id="8c9c9-265">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="8c9c9-266">I_MPI_DYNAMIC_CONNECTION=0</span><span class="sxs-lookup"><span data-stu-id="8c9c9-266">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="8c9c9-267">Crée un fichier d’hôte en fonction de toohello $ variable d’environnement CCP_NODES_CORES, qui est définie par le nœud principal HPC de hello lors de la tâche de hello est activé.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-267">Creates a host file according toohello environment variable $CCP_NODES_CORES, which is set by hello HPC head node when hello job is activated.</span></span>
      
      <span data-ttu-id="8c9c9-268">format Hello $CCP_NODES_CORES suit ce modèle :</span><span class="sxs-lookup"><span data-stu-id="8c9c9-268">hello format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="8c9c9-269">où</span><span class="sxs-lookup"><span data-stu-id="8c9c9-269">where</span></span>
      
      * <span data-ttu-id="8c9c9-270">`<Number of nodes>`-nombre de hello de nœuds allouée toothis travail.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-270">`<Number of nodes>` - hello number of nodes allocated toothis job.</span></span>  
      * <span data-ttu-id="8c9c9-271">`<Name of node_n_...>`-nom hello de chaque nœud allouée toothis travail.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-271">`<Name of node_n_...>` - hello name of each node allocated toothis job.</span></span>
      * <span data-ttu-id="8c9c9-272">`<Cores of node_n_...>`-hello du nombre de cœurs sur le travail de hello nœud toothis alloué.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-272">`<Cores of node_n_...>` - hello number of cores on hello node allocated toothis job.</span></span>
      
      <span data-ttu-id="8c9c9-273">Par exemple, si le travail de hello a besoin de deux nœuds toorun, $CCP_NODES_CORES est similaire à</span><span class="sxs-lookup"><span data-stu-id="8c9c9-273">For example, if hello job needs two nodes toorun, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="8c9c9-274">Hello d’appels **mpirun** commande et ajoute la ligne de commande de deux paramètres toohello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-274">Calls hello **mpirun** command and appends two parameters toohello command line.</span></span>
      
      * <span data-ttu-id="8c9c9-275">`--hostfile <hostfilepath>: <hostfilepath>`-chemin d’accès de hello du script de hello du fichier hôte hello crée</span><span class="sxs-lookup"><span data-stu-id="8c9c9-275">`--hostfile <hostfilepath>: <hostfilepath>` - hello path of hello host file hello script creates</span></span>
      * <span data-ttu-id="8c9c9-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-une variable d’environnement définie par hello nœud principal HPC Pack, qui stocke le nombre de hello de cœurs total alloué toothis travail.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by hello HPC Pack head node, which stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="8c9c9-277">Dans ce cas, il spécifie le nombre de hello de processus pour **mpirun**.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-277">In this case, it specifies hello number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="8c9c9-278">Envoi d’un travail OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="8c9c9-278">Submit an OpenFOAM job</span></span>
<span data-ttu-id="8c9c9-279">Maintenant, vous pouvez envoyer un travail dans HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-279">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="8c9c9-280">Vous devez toopass hello script hpcimpirun.sh dans les lignes de commande hello pour certaines des tâches hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-280">You need toopass hello script hpcimpirun.sh in hello command lines for some of hello job tasks.</span></span>

1. <span data-ttu-id="8c9c9-281">Se connecter tooyour nœud principal du cluster et démarrez le Gestionnaire du Cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-281">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="8c9c9-282">**Dans la gestion des ressources**, assurez-vous que les nœuds de calcul Linux hello sont Bonjour **Online** état.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-282">**In Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="8c9c9-283">Si ce n’est pas le cas, sélectionnez-les et cliquez sur **Mettre en ligne**.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-283">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="8c9c9-284">Dans **Gestion des tâches**, cliquez sur **Nouveau travail**.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-284">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="8c9c9-285">Entrez un nom pour le travail, par exemple *sloshingTank3D*.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-285">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![Détails du travail][job_details]
5. <span data-ttu-id="8c9c9-287">Dans **ressources de projet**, choisissez de type hello de ressource en tant que « Nœud » et définir hello Minimum too2.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-287">In **Job resources**, choose hello type of resource as “Node” and set hello Minimum too2.</span></span> <span data-ttu-id="8c9c9-288">Cette configuration s’exécute le travail de hello sur deux nœuds de Linux, chacun d’eux a huit cœurs dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-288">This configuration runs hello job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![ressources de la tâche][job_resources]
6. <span data-ttu-id="8c9c9-290">Cliquez sur **modifier des tâches** dans hello du volet de navigation gauche, puis cliquez sur **ajouter** tooadd un travail de toohello de tâches.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-290">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span> <span data-ttu-id="8c9c9-291">Ajouter quatre travail toohello de tâches avec hello suivant des lignes de commande et les paramètres.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-291">Add four tasks toohello job with hello following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8c9c9-292">En cours d’exécution `source /openfoam/settings.sh` configure hello OpenFOAM et MPI environnements d’exécution, si bien que chacun des hello tâches suivantes l’appelle avant hello OpenFOAM commande.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-292">Running `source /openfoam/settings.sh` sets up hello OpenFOAM and MPI runtime environments, so each of hello following tasks calls it before hello OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="8c9c9-293">**Tâche 1**.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-293">**Task 1**.</span></span> <span data-ttu-id="8c9c9-294">Exécutez **decomposePar** toogenerate des fichiers de données pour exécuter **interDyMFoam** en parallèle.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-294">Run **decomposePar** toogenerate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="8c9c9-295">Affecter une tâche toohello de nœud</span><span class="sxs-lookup"><span data-stu-id="8c9c9-295">Assign one node toohello task</span></span>
     * <span data-ttu-id="8c9c9-296">**Ligne de commande** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="8c9c9-296">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="8c9c9-297">**Répertoire de travail** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="8c9c9-297">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="8c9c9-298">Consultez hello figure suivante.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-298">See hello following figure.</span></span> <span data-ttu-id="8c9c9-299">Vous configurez les tâches restantes hello de la même façon.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-299">You configure hello remaining tasks similarly.</span></span>
     
     ![Détails de la tâche 1][task_details1]
   * <span data-ttu-id="8c9c9-301">**Tâche 2**.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-301">**Task 2**.</span></span> <span data-ttu-id="8c9c9-302">Exécutez **interDyMFoam** dans toocompute parallèle hello exemple.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-302">Run **interDyMFoam** in parallel toocompute hello sample.</span></span>
     
     * <span data-ttu-id="8c9c9-303">Affecter des tâches de toohello deux nœuds</span><span class="sxs-lookup"><span data-stu-id="8c9c9-303">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="8c9c9-304">**Ligne de commande** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="8c9c9-304">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="8c9c9-305">**Répertoire de travail** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="8c9c9-305">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="8c9c9-306">**Tâche 3**.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-306">**Task 3**.</span></span> <span data-ttu-id="8c9c9-307">Exécutez **reconstructPar** toomerge hello définit des répertoires de temps à partir de chaque répertoire processor_N_ en un seul ensemble.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-307">Run **reconstructPar** toomerge hello sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="8c9c9-308">Affecter une tâche toohello de nœud</span><span class="sxs-lookup"><span data-stu-id="8c9c9-308">Assign one node toohello task</span></span>
     * <span data-ttu-id="8c9c9-309">**Ligne de commande** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="8c9c9-309">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="8c9c9-310">**Répertoire de travail** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="8c9c9-310">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="8c9c9-311">**Tâche 4**.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-311">**Task 4**.</span></span> <span data-ttu-id="8c9c9-312">Exécutez **foamToEnsight** dans tooconvert parallèle fichiers de résultats OpenFOAM hello dans EnSight mettre en forme et hello EnSight fichiers dans un répertoire nommé Ensight dans le répertoire de cas hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-312">Run **foamToEnsight** in parallel tooconvert hello OpenFOAM result files into EnSight format and place hello EnSight files in a directory named Ensight in hello case directory.</span></span>
     
     * <span data-ttu-id="8c9c9-313">Affecter des tâches de toohello deux nœuds</span><span class="sxs-lookup"><span data-stu-id="8c9c9-313">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="8c9c9-314">**Ligne de commande** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="8c9c9-314">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="8c9c9-315">**Répertoire de travail** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="8c9c9-315">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="8c9c9-316">Ajouter des tâches de toothese de dépendances dans l’ordre croissant de l’ordre des tâches.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-316">Add dependencies toothese tasks in ascending task order.</span></span>
   
   ![Dépendances de la tâche][task_dependencies]
8. <span data-ttu-id="8c9c9-318">Cliquez sur **Submit** toorun ce travail.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-318">Click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="8c9c9-319">Par défaut, HPC Pack soumet le travail hello que votre compte d’utilisateur connecté actuel.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-319">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="8c9c9-320">Après avoir cliqué sur **envoyer**, vous pouvez voir une boîte de dialogue vous invitant à nom d’utilisateur tooenter hello et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-320">After you click **Submit**, you might see a dialog box prompting you tooenter hello user name and password.</span></span>
   
   ![Informations d’identification de la tâche][creds]
   
   <span data-ttu-id="8c9c9-322">Sous certaines conditions, HPC Pack mémorise les informations d’utilisateur hello d’entrée avant et de ne plus afficher cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-322">Under some conditions, HPC Pack remembers hello user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="8c9c9-323">toomake HPC Pack afficher à nouveau, entrez hello commande à l’invite de commande suivante et l’envoi de la tâche de hello puis.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-323">toomake HPC Pack show it again, enter hello following command at a Command prompt and then submit hello job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="8c9c9-324">travail de Hello prend de dizaines de minutes tooseveral heures en fonction des paramètres toohello que vous avez défini pour l’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-324">hello job takes from tens of minutes tooseveral hours according toohello parameters you have set for hello sample.</span></span> <span data-ttu-id="8c9c9-325">Dans la carte thermique hello, vous voyez travail hello en cours d’exécution sur les nœuds de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-325">In hello heat map, you see hello job running on hello Linux nodes.</span></span> 
   
   ![Carte thermique][heat_map]
   
   <span data-ttu-id="8c9c9-327">Sur chaque nœud, huit processus sont démarrés.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-327">On each node, eight processes are started.</span></span>
   
   ![Processus Linux][linux_processes]
10. <span data-ttu-id="8c9c9-329">Lors de la fin du travail de hello, trouver les résultats de la tâche hello dans les dossiers C:\OpenFoam\sloshingTank3D et des fichiers journaux hello C:\OpenFoam.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-329">When hello job finishes, find hello job results in folders under C:\OpenFoam\sloshingTank3D, and hello log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="8c9c9-330">Afficher les résultats dans EnSight</span><span class="sxs-lookup"><span data-stu-id="8c9c9-330">View results in EnSight</span></span>
<span data-ttu-id="8c9c9-331">Vous pouvez également utiliser [EnSight](https://www.ceisoftware.com/) toovisualize et analyser les résultats hello du travail de OpenFOAM hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-331">Optionally use [EnSight](https://www.ceisoftware.com/) toovisualize and analyze hello results of hello OpenFOAM job.</span></span> <span data-ttu-id="8c9c9-332">Pour plus d’informations sur la visualisation et l’animation dans EnSight, consultez le [guide vidéo](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span><span class="sxs-lookup"><span data-stu-id="8c9c9-332">For more about visualization and animation in EnSight, see this [video guide](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span></span>

1. <span data-ttu-id="8c9c9-333">Après avoir installé EnSight sur le nœud principal de hello, démarrez-le.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-333">After you install EnSight on hello head node, start it.</span></span>
2. <span data-ttu-id="8c9c9-334">Ouvrez C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-334">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="8c9c9-335">Vous voyez un réservoir dans l’Observateur hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-335">You see a tank in hello viewer.</span></span>
   
   ![Réservoir dans EnSight][tank]
3. <span data-ttu-id="8c9c9-337">Créer un **Isosurface** de **internalMesh**, puis choisissez la variable de hello **alpha_water**.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-337">Create an **Isosurface** from **internalMesh**, and then choose hello variable **alpha_water**.</span></span>
   
   ![Créer une isosurface][isosurface]
4. <span data-ttu-id="8c9c9-339">Définir la couleur de hello pour **Isosurface_part** créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-339">Set hello color for **Isosurface_part** created in hello previous step.</span></span> <span data-ttu-id="8c9c9-340">Par exemple, définissez-le toowater bleu.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-340">For example, set it toowater blue.</span></span>
   
   ![Modifier la couleur de l’isosurface][isosurface_color]
5. <span data-ttu-id="8c9c9-342">Créer un **Iso-volume** de **murs** en sélectionnant **murs** Bonjour **parties** volet et cliquez sur hello **Isosurfaces**  bouton dans la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-342">Create an **Iso-volume** from **walls** by selecting **walls** in hello **Parts** panel and click hello **Isosurfaces** button in hello toolbar.</span></span>
6. <span data-ttu-id="8c9c9-343">Dans la boîte de dialogue hello, sélectionnez **Type** en tant que **Isovolume** et définissez hello Min. de **Isovolume plage** too0.5.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-343">In hello dialog box, select **Type** as **Isovolume** and set hello Min of **Isovolume range** too0.5.</span></span> <span data-ttu-id="8c9c9-344">toocreate hello isovolume, cliquez sur **créer avec les parties sélectionnées**.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-344">toocreate hello isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="8c9c9-345">Définir la couleur de hello pour **Iso_volume_part** créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-345">Set hello color for **Iso_volume_part** created in hello previous step.</span></span> <span data-ttu-id="8c9c9-346">Par exemple, définissez-le toodeep eau bleu.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-346">For example, set it toodeep water blue.</span></span>
8. <span data-ttu-id="8c9c9-347">Définir la couleur de hello pour **murs**.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-347">Set hello color for **walls**.</span></span> <span data-ttu-id="8c9c9-348">Par exemple, définissez-le tootransparent blanc.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-348">For example, set it tootransparent white.</span></span>
9. <span data-ttu-id="8c9c9-349">Maintenant, cliquez sur **lire** toosee les résultats de hello de simulation de hello.</span><span class="sxs-lookup"><span data-stu-id="8c9c9-349">Now click **Play** toosee hello results of hello simulation.</span></span>
   
    ![Résultat du réservoir][tank_result]

## <a name="sample-files"></a><span data-ttu-id="8c9c9-351">Exemple de fichiers</span><span class="sxs-lookup"><span data-stu-id="8c9c9-351">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="8c9c9-352">Exemple de fichier de configuration XML pour le déploiement de clusters par script PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c9c9-352">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

### <a name="sample-credxml-file"></a><span data-ttu-id="8c9c9-353">Exemple de fichier cred.xml</span><span class="sxs-lookup"><span data-stu-id="8c9c9-353">Sample cred.xml file</span></span>
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```
### <a name="sample-silentcfg-file-tooinstall-mpi"></a><span data-ttu-id="8c9c9-354">Exemple silent.cfg fichier tooinstall MPI</span><span class="sxs-lookup"><span data-stu-id="8c9c9-354">Sample silent.cfg file tooinstall MPI</span></span>
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="8c9c9-355">Exemple de script settings.sh</span><span class="sxs-lookup"><span data-stu-id="8c9c9-355">Sample settings.sh script</span></span>
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="8c9c9-356">Exemple de script hpcimpirun.sh</span><span class="sxs-lookup"><span data-stu-id="8c9c9-356">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
