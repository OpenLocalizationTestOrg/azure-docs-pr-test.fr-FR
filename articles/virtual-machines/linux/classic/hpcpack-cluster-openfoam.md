---
title: "Exécuter OpenFOAM avec HPC Pack sur des machines virtuelles Linux | Microsoft Docs"
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
ms.openlocfilehash: ef124a8983fa112d499252460bff9ed2fcccc02b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="482b1-103">Exécuter OpenFoam avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure</span><span class="sxs-lookup"><span data-stu-id="482b1-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="482b1-104">Cet article vous montre une méthode d’exécution d’OpenFoam dans des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="482b1-104">This article shows you one way to run OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="482b1-105">Ici, vous déployez un cluster Microsoft HPC Pack avec des nœuds de calcul Linux sur Azure, et exécutez une tâche [OpenFoam](http://openfoam.com/) avec Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="482b1-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="482b1-106">Vous pouvez utiliser des machines virtuelles Azure prenant en charge RDMA pour les nœuds de calcul, de sorte que ceux-ci communiquent sur le réseau RDMA Azure.</span><span class="sxs-lookup"><span data-stu-id="482b1-106">You can use RDMA-capable Azure VMs for the compute nodes, so that the compute nodes communicate over the Azure RDMA network.</span></span> <span data-ttu-id="482b1-107">Les autres options d’exécution d’OpenFoam dans Azure incluent des images commerciales entièrement configurées disponibles sur le Marketplace, notamment [OpenFoam 2.3 sur CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/) d’UberCloud, et l’exécution sur [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span><span class="sxs-lookup"><span data-stu-id="482b1-107">Other options to run OpenFoam in Azure include fully configured commercial images available in the Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="482b1-108">OpenFOAM (acronyme d’Open Field Operation and Manipulation) est un logiciel open source de calcul de mécanique des fluides numérique largement utilisé en ingénierie et en sciences, tant au sein d’organisations commerciales que d’instituts universitaires.</span><span class="sxs-lookup"><span data-stu-id="482b1-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="482b1-109">Il comprend des outils de maillage, notamment snappyHexMesh, un meilleur parallélisé pour les géométries de CAO complexes et de pré et post-traitement.</span><span class="sxs-lookup"><span data-stu-id="482b1-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="482b1-110">Presque tous les processus s’exécutent en parallèle, permettant aux utilisateurs de tirer le meilleur parti du matériel informatique à leur disposition.</span><span class="sxs-lookup"><span data-stu-id="482b1-110">Almost all processes run in parallel, enabling users to take full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="482b1-111">Microsoft HPC Pack fournit des fonctionnalités permettant d’exécuter un éventail d’applications HPC à grande échelle et parallèles, dont des applications MPI, sur des clusters de machines virtuelles Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="482b1-111">Microsoft HPC Pack provides features to run large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="482b1-112">HPC Pack prend également en charge l’exécution d’applications Linux HPC sur les machines virtuelles de nœuds de calcul Linux déployées dans un cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="482b1-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="482b1-113">Voir [Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md) pour une présentation de l’utilisation des nœuds de calcul Linux avec HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="482b1-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction to using Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="482b1-114">Cet article explique comment exécuter une charge de travail Linux MPI avec HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="482b1-114">This article illustrates how to run a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="482b1-115">Il suppose que vous êtes familiarisé avec l’administration du système Linux et l’exécution de charges de travail MPI sur des clusters Linux.</span><span class="sxs-lookup"><span data-stu-id="482b1-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="482b1-116">Si vous utilisez des versions MPI et OpenFOAM différentes de celles indiquées dans cet article, vous devrez peut-être adapter certaines étapes d’installation et de configuration.</span><span class="sxs-lookup"><span data-stu-id="482b1-116">If you use versions of MPI and OpenFOAM different from the ones shown in this article, you might have to modify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="482b1-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="482b1-117">Prerequisites</span></span>
* <span data-ttu-id="482b1-118">**Cluster HPC Pack avec nœuds de calcul Linux prenant en charge RDMA** : déployez un cluster HPC Pack avec des nœuds de calcul Linux de taille A8, A9, H16r ou H16rm à l’aide d’un [modèle Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) ou d’un [script Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="482b1-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="482b1-119">Consultez la configuration requise et la procédure pour chaque option sur la page [Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md) .</span><span class="sxs-lookup"><span data-stu-id="482b1-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for the prerequisites and steps for either option.</span></span> <span data-ttu-id="482b1-120">Si vous choisissez l’option de déploiement de script PowerShell, voir l’exemple de fichier de configuration dans les fichiers d’exemple à la fin de cet article.</span><span class="sxs-lookup"><span data-stu-id="482b1-120">If you choose the PowerShell script deployment option, see the sample configuration file in the sample files at the end of this article.</span></span> <span data-ttu-id="482b1-121">Utilisez cette configuration pour déployer un cluster HPC Pack basé sur Azure, composé d’un nœud principal Windows Server 2012 R2 de taille A8, et de 2 nœuds de calcul SUSE Linux Enterprise Server 12 de taille A8.</span><span class="sxs-lookup"><span data-stu-id="482b1-121">Use this configuration to deploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="482b1-122">Remplacez les valeurs appropriées pour les noms de vos abonnement et service.</span><span class="sxs-lookup"><span data-stu-id="482b1-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="482b1-123">**Autres informations à connaître**</span><span class="sxs-lookup"><span data-stu-id="482b1-123">**Additional things to know**</span></span>
  
  * <span data-ttu-id="482b1-124">Pour connaître les conditions préalables à la mise en réseau RDMA Linux dans Azure, consultez [Tailles de machines virtuelles de calcul haute performance](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="482b1-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="482b1-125">Si vous utilisez l’option de déploiement de script Powershell, déployez tous les nœuds de calcul Linux au sein d’un service cloud pour utiliser la connexion réseau RDMA.</span><span class="sxs-lookup"><span data-stu-id="482b1-125">If you use the Powershell script deployment option, deploy all the Linux compute nodes within one cloud service to use the RDMA network connection.</span></span>
  * <span data-ttu-id="482b1-126">Après avoir déployé les nœuds Linux, connectez-vous à SSH pour effectuer toutes tâches administratives supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="482b1-126">After deploying the Linux nodes, connect by SSH to perform any additional administrative tasks.</span></span> <span data-ttu-id="482b1-127">Recherchez les détails de connexion SSH pour chaque machine virtuelle Linux dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="482b1-127">Find the SSH connection details for each Linux VM in the Azure portal.</span></span>  
* <span data-ttu-id="482b1-128">**Intel MPI** : pour exécuter OpenFOAM sur des nœuds de calcul SLES 12 HPC dans Azure, vous devez installer le runtime Intel MPI Library 5 que vous trouverez sur le [site Intel.com](https://software.intel.com/en-us/intel-mpi-library/).</span><span class="sxs-lookup"><span data-stu-id="482b1-128">**Intel MPI** - To run OpenFOAM on SLES 12 HPC compute nodes in Azure, you need to install the Intel MPI Library 5 runtime from the [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="482b1-129">(Intel MPI 5 est préinstallé sur des images HPC basées sur CentOS.)  Si nécessaire, vous devez ensuite installer Intel MPI sur vos nœuds de calcul Linux.</span><span class="sxs-lookup"><span data-stu-id="482b1-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="482b1-130">Pour préparer cette étape, après votre inscription auprès d’Intel, suivez le lien vers la page web associée, figurant dans le message de confirmation.</span><span class="sxs-lookup"><span data-stu-id="482b1-130">To prepare for this step, after you register with Intel, follow the link in the confirmation email to the related web page.</span></span> <span data-ttu-id="482b1-131">Ensuite, copiez le lien de téléchargement du fichier .tgz pour la version appropriée d’Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="482b1-131">Then, copy the download link for the .tgz file for the appropriate version of Intel MPI.</span></span> <span data-ttu-id="482b1-132">Cet article est basé sur Intel MPI version 5.0.3.048.</span><span class="sxs-lookup"><span data-stu-id="482b1-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="482b1-133">**OpenFOAM Source Pack** : téléchargez le logiciel OpenFOAM Source Pack pour Linux à partir du [site d’OpenFOAM Foundation](http://openfoam.org/download/2-3-1-source/).</span><span class="sxs-lookup"><span data-stu-id="482b1-133">**OpenFOAM Source Pack** - Download the OpenFOAM Source Pack software for Linux from the [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="482b1-134">Cet article est basé sur la version du Pack Source 2.3.1, disponible en téléchargement en tant que OpenFOAM 2.3.1.tgz.</span><span class="sxs-lookup"><span data-stu-id="482b1-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="482b1-135">Suivez les instructions présentes plus loin dans cet article pour décompresser et compiler OpenFOAM sur les nœuds de calcul Linux.</span><span class="sxs-lookup"><span data-stu-id="482b1-135">Follow the instructions later in this article to unpack and compile OpenFOAM on the Linux compute nodes.</span></span>
* <span data-ttu-id="482b1-136">**EnSight** (facultatif) : pour afficher les résultats de votre simulation OpenFOAM, téléchargez et installez le programme de visualisation et d’analyse [EnSight](https://www.ceisoftware.com/download/) .</span><span class="sxs-lookup"><span data-stu-id="482b1-136">**EnSight** (optional) - To see the results of your OpenFOAM simulation, download and install the [EnSight](https://www.ceisoftware.com/download/) visualization and analysis program.</span></span> <span data-ttu-id="482b1-137">Les informations de licence et de téléchargement se trouvent sur le site EnSight.</span><span class="sxs-lookup"><span data-stu-id="482b1-137">Licensing and download information are at the EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="482b1-138">Configuration de l’approbation mutuelle entre les nœuds de calcul</span><span class="sxs-lookup"><span data-stu-id="482b1-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="482b1-139">L’exécution d’une tâche de nœuds croisés sur plusieurs nœuds Linux requiert une approbation mutuelle entre les nœuds (par **rsh** ou **ssh**).</span><span class="sxs-lookup"><span data-stu-id="482b1-139">Running a cross-node job on multiple Linux nodes requires the nodes to trust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="482b1-140">Lorsque vous créez le cluster HPC Pack avec le script de déploiement IaaS Microsoft HPC Pack, le script définit automatiquement l’approbation mutuelle permanente pour le compte administrateur que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="482b1-140">When you create the HPC Pack cluster with the Microsoft HPC Pack IaaS deployment script, the script automatically sets up permanent mutual trust for the administrator account you specify.</span></span> <span data-ttu-id="482b1-141">Pour les utilisateurs non administrateurs que vous créez dans le domaine du cluster, vous devez configurer l’approbation mutuelle temporaire entre les nœuds lorsqu’une tâche leur est allouée, puis détruire la relation une fois la tâche terminée.</span><span class="sxs-lookup"><span data-stu-id="482b1-141">For non-administrator users you create in the cluster's domain, you have to set up temporary mutual trust among the nodes when a job is allocated to them, and destroy the relationship after the job is complete.</span></span> <span data-ttu-id="482b1-142">Pour établir l’approbation, pour chaque utilisateur, fournissez une paire de clés RSA au cluster que HPC Pack utilise pour la relation d’approbation.</span><span class="sxs-lookup"><span data-stu-id="482b1-142">To establish trust for each user, provide an RSA key pair to the cluster that HPC Pack uses for the trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="482b1-143">Génération d’une paire de clés RSA</span><span class="sxs-lookup"><span data-stu-id="482b1-143">Generate an RSA key pair</span></span>
<span data-ttu-id="482b1-144">Générer une paire de clés RSA contenant une clé publique et une clé privée est facile : il vous suffit d’exécuter la commande Linux **ssh-keygen** .</span><span class="sxs-lookup"><span data-stu-id="482b1-144">It's easy to generate an RSA key pair, which contains a public key and a private key, by running the Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="482b1-145">Ouvrez une session sur un ordinateur Linux.</span><span class="sxs-lookup"><span data-stu-id="482b1-145">Log on to a Linux computer.</span></span>
2. <span data-ttu-id="482b1-146">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="482b1-146">Run the following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="482b1-147">Appuyez sur **Entrée** pour utiliser les paramètres par défaut jusqu'à ce que la commande soit terminée.</span><span class="sxs-lookup"><span data-stu-id="482b1-147">Press **Enter** to use the default settings until the command is completed.</span></span> <span data-ttu-id="482b1-148">N'entrez pas de phrase secrète ici ; à l'invite de mot de passe, appuyez simplement sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="482b1-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Génération d’une paire de clés RSA][keygen]
3. <span data-ttu-id="482b1-150">Remplacez le répertoire par le répertoire ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="482b1-150">Change directory to the ~/.ssh directory.</span></span> <span data-ttu-id="482b1-151">La clé privée est stockée dans id_rsa et la clé publique dans id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="482b1-151">The private key is stored in id_rsa and the public key in id_rsa.pub.</span></span>
   
   ![Clés publiques et privées][keys]

### <a name="add-the-key-pair-to-the-hpc-pack-cluster"></a><span data-ttu-id="482b1-153">Ajout de la paire de clés au cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="482b1-153">Add the key pair to the HPC Pack cluster</span></span>
1. <span data-ttu-id="482b1-154">Effectuez une connexion Bureau à distance à votre nœud principal avec votre compte administrateur HPC Pack (le compte administrateur que vous avez configuré lorsque vous avez exécuté le script de déploiement).</span><span class="sxs-lookup"><span data-stu-id="482b1-154">Make a Remote Desktop connection to your head node with your HPC Pack administrator account (the administrator account you set up when you ran the deployment script).</span></span>
2. <span data-ttu-id="482b1-155">Utilisez les procédures standard Windows Server pour créer un compte d’utilisateur de domaine dans le domaine Active Directory du cluster.</span><span class="sxs-lookup"><span data-stu-id="482b1-155">Use standard Windows Server procedures to create a domain user account in the cluster's Active Directory domain.</span></span> <span data-ttu-id="482b1-156">Par exemple, utilisez l’outil Utilisateurs et ordinateurs Active Directory sur le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="482b1-156">For example, use the Active Directory User and Computers tool on the head node.</span></span> <span data-ttu-id="482b1-157">Les exemples de cet article supposent que vous créez un utilisateur de domaine nommé hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="482b1-157">The examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="482b1-158">Créez un fichier nommé C:\cred.xml et copiez-y les données de clé RSA.</span><span class="sxs-lookup"><span data-stu-id="482b1-158">Create a file named C:\cred.xml and copy the RSA key data into it.</span></span> <span data-ttu-id="482b1-159">Un exemple de fichier cred.xml figure à la fin de cet article.</span><span class="sxs-lookup"><span data-stu-id="482b1-159">A sample cred.xml file is at the end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy the contents of private key here</PrivateKey>
     <PublicKey>Copy the contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="482b1-160">Ouvrez une invite de commande et entrez la commande suivante pour définir les données d’informations d’identification du compte hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="482b1-160">Open a Command Prompt and enter the following command to set the credentials data for the hpclab\hpcuser account.</span></span> <span data-ttu-id="482b1-161">Utilisez le paramètre **extendeddata** pour transmettre le nom du fichier C:\cred.xml que vous avez créé pour les données de clé.</span><span class="sxs-lookup"><span data-stu-id="482b1-161">You use the **extendeddata** parameter to pass the name of C:\cred.xml file you created for the key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="482b1-162">Cette commande se termine correctement sans sortie.</span><span class="sxs-lookup"><span data-stu-id="482b1-162">This command completes successfully without output.</span></span> <span data-ttu-id="482b1-163">Après avoir défini les informations d’identification pour les comptes d’utilisateurs dont vous avez besoin pour exécuter des tâches, stockez le fichier cred.xml à un emplacement sécurisé ou supprimez-le.</span><span class="sxs-lookup"><span data-stu-id="482b1-163">After setting the credentials for the user accounts you need to run jobs, store the cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="482b1-164">Si vous avez généré la paire de clés RSA sur l’un de vos nœuds Linux, pensez à supprimer les clés une fois que vous avez terminé de les utiliser.</span><span class="sxs-lookup"><span data-stu-id="482b1-164">If you generated the RSA key pair on one of your Linux nodes, remember to delete the keys after you finish using them.</span></span> <span data-ttu-id="482b1-165">HPC Pack recherche un fichier id_rsa ou id_rsa.pub existant. Il ne configure pas d’approbation mutuelle.</span><span class="sxs-lookup"><span data-stu-id="482b1-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="482b1-166">Nous déconseillons d’exécuter une tâche Linux en tant qu’administrateur de cluster sur un cluster partagé, car une tâche envoyée par un administrateur s’exécute sous le compte racine sur les nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="482b1-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under the root account on the Linux nodes.</span></span> <span data-ttu-id="482b1-167">Toutefois, une tâche envoyée par un utilisateur non-administrateur s’exécute sous un compte utilisateur Linux local du même nom que l’utilisateur de la tâche.</span><span class="sxs-lookup"><span data-stu-id="482b1-167">However, a job submitted by a non-administrator user runs under a local Linux user account with the same name as the job user.</span></span> <span data-ttu-id="482b1-168">Dans ce cas, HPC Pack définit une approbation mutuelle pour cet utilisateur Linux sur les nœuds alloués à la tâche.</span><span class="sxs-lookup"><span data-stu-id="482b1-168">In this case, HPC Pack sets up mutual trust for this Linux user across the nodes allocated to the job.</span></span> <span data-ttu-id="482b1-169">Vous pouvez configurer l’utilisateur Linux manuellement sur les nœuds Linux avant d’exécuter la tâche, ou bien HPC Pack crée automatiquement l’utilisateur lorsque la tâche est envoyée.</span><span class="sxs-lookup"><span data-stu-id="482b1-169">You can set up the Linux user manually on the Linux nodes before running the job, or HPC Pack creates the user automatically when the job is submitted.</span></span> <span data-ttu-id="482b1-170">Si HPC Pack crée l’utilisateur, il se charge de le supprimer une fois la tâche terminée.</span><span class="sxs-lookup"><span data-stu-id="482b1-170">If HPC Pack creates the user, HPC Pack deletes it after the job completes.</span></span> <span data-ttu-id="482b1-171">Pour réduire les menaces de sécurité, HPC Pack supprime les clés une fois la tâche accomplie.</span><span class="sxs-lookup"><span data-stu-id="482b1-171">To reduce security threats, HPC Pack removes the keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="482b1-172">Configuration d’un partage de fichiers pour les nœuds Linux</span><span class="sxs-lookup"><span data-stu-id="482b1-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="482b1-173">À présent, configurez un partage SMB standard sur un dossier du nœud principal.</span><span class="sxs-lookup"><span data-stu-id="482b1-173">Now set up a standard SMB share on a folder on the head node.</span></span> <span data-ttu-id="482b1-174">Pour autoriser les nœuds Linux à accéder aux fichiers d’application avec un chemin d’accès commun, montez le dossier partagé sur les nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="482b1-174">To allow the Linux nodes to access application files with a common path, mount the shared folder on the Linux nodes.</span></span> <span data-ttu-id="482b1-175">Si vous le souhaitez, vous pouvez utiliser une autre option de partage de fichier telle que le partage de fichiers Azure (recommandé dans de nombreux scénarios) ou un partage NFS.</span><span class="sxs-lookup"><span data-stu-id="482b1-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="482b1-176">Consultez les étapes détaillées et les informations de partage de fichiers dans la section [Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="482b1-176">See the file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="482b1-177">Créez un dossier sur le nœud principal et partagez-le avec Tout le monde en définissant des privilèges de lecture/écriture.</span><span class="sxs-lookup"><span data-stu-id="482b1-177">Create a folder on the head node, and share it to Everyone by setting Read/Write privileges.</span></span> <span data-ttu-id="482b1-178">Par exemple, partagez D:\OpenFOAM sur le nœud principal en tant que \\\\SUSE12RDMA-HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="482b1-178">For example, share C:\OpenFOAM on the head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="482b1-179">Ici, *SUSE12RDMA-HN* est le nom d’hôte du nœud principal.</span><span class="sxs-lookup"><span data-stu-id="482b1-179">Here, *SUSE12RDMA-HN* is the host name of the head node.</span></span>
2. <span data-ttu-id="482b1-180">Ouvrez une fenêtre Windows PowerShell, puis exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="482b1-180">Open a Windows PowerShell window and run the following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="482b1-181">La première commande crée un dossier nommé /openfoam sur tous les nœuds du groupe LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="482b1-181">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="482b1-182">La deuxième commande monte le dossier partagé //SUSE12RDMA-HN/OpenFOAM sur les nœuds avec les bits dir_mode et file_mode définis sur 777.</span><span class="sxs-lookup"><span data-stu-id="482b1-182">The second command mounts the shared folder //SUSE12RDMA-HN/OpenFOAM on the Linux nodes with dir_mode and file_mode bits set to 777.</span></span> <span data-ttu-id="482b1-183">Les valeurs *username* et *password* dans la commande doivent être les informations d’identification d’un utilisateur du nœud principal.</span><span class="sxs-lookup"><span data-stu-id="482b1-183">The *username* and *password* in the command should be the credentials of a user on the head node.</span></span>

> [!NOTE]
> <span data-ttu-id="482b1-184">Le symbole « \\` » dans la deuxième commande est un symbole de caractère d’échappement pour PowerShell.</span><span class="sxs-lookup"><span data-stu-id="482b1-184">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="482b1-185">« \\`, » signifie que « , » (une virgule) fait partie de la commande.</span><span class="sxs-lookup"><span data-stu-id="482b1-185">“\\`,” means the “,” (comma character) is a part of the command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="482b1-186">Installer MPI et OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="482b1-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="482b1-187">Pour exécuter OpenFOAM en tant que travail MPI sur le réseau RDMA, vous devez compiler OpenFOAM avec les bibliothèques Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="482b1-187">To run OpenFOAM as an MPI job on the RDMA network, you need to compile OpenFOAM with the Intel MPI libraries.</span></span> 

<span data-ttu-id="482b1-188">Tout d’abord, exécutez quelques commandes **clusrun** pour installer (le cas échéant) les bibliothèques Intel MPI et OpenFOAM sur vos nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="482b1-188">First, run several **clusrun** commands to install Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="482b1-189">Utiliser le partage de nœud principal configuré précédemment pour partager les fichiers d’installation sur les nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="482b1-189">Use the head node share configured previously to share the installation files among the Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="482b1-190">Ces étapes d’installation et de compilation sont des exemples.</span><span class="sxs-lookup"><span data-stu-id="482b1-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="482b1-191">Pour vous assurer que les bibliothèques et les compilateurs dépendants sont correctement installés, vous devez disposer de connaissances en administration du système Linux.</span><span class="sxs-lookup"><span data-stu-id="482b1-191">You need some knowledge of Linux system administration to ensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="482b1-192">Vous devrez peut-être modifier certaines variables d’environnement ou d’autres paramètres pour vos versions d’Intel MPI et OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="482b1-192">You might need to modify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="482b1-193">Pour plus de détails, voir [Guide d’installation de la bibliothèque Intel MPI pour Linux](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) et [Installation du pack source d’OpenFOAM](http://openfoam.org/download/2-3-1-source/) pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="482b1-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="482b1-194">Installer Intel MPI</span><span class="sxs-lookup"><span data-stu-id="482b1-194">Install Intel MPI</span></span>
<span data-ttu-id="482b1-195">Enregistrez le package d’installation téléchargé pour Intel MPI (l_mpi_p_5.0.3.048.tgz dans cet exemple) dans C:\OpenFoam sur le nœud principal afin que les nœuds Linux puissent accéder à ce fichier à partir de /openfoam.</span><span class="sxs-lookup"><span data-stu-id="482b1-195">Save the downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="482b1-196">Exécutez ensuite **clusrun** pour installer la bibliothèque Intel MPI sur tous les nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="482b1-196">Then run **clusrun** to install Intel MPI library on all the Linux nodes.</span></span>

1. <span data-ttu-id="482b1-197">Les commandes suivantes copient le package d’installation et l’extraient dans le répertoire /opt/intel de chacun des nœuds.</span><span class="sxs-lookup"><span data-stu-id="482b1-197">The following commands copy the installation package and extract it to /opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="482b1-198">Pour installer la bibliothèque Intel MPI en mode silencieux, utilisez un fichier silent.cfg.</span><span class="sxs-lookup"><span data-stu-id="482b1-198">To install Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="482b1-199">Vous trouverez un exemple dans les exemples de fichiers à la fin de cet article.</span><span class="sxs-lookup"><span data-stu-id="482b1-199">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="482b1-200">Placez ce fichier dans le dossier partagé /openfoam.</span><span class="sxs-lookup"><span data-stu-id="482b1-200">Place this file in the shared folder /openfoam.</span></span> <span data-ttu-id="482b1-201">Pour plus de détails sur le fichier silent.cfg, consultez le [Guide d’installation de la bibliothèque MPI Intel pour Linux - Installation silencieuse](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span><span class="sxs-lookup"><span data-stu-id="482b1-201">For details about the silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="482b1-202">Assurez-vous que vous enregistrez votre fichier .cfg silencieux en tant que fichier texte avec des fins de ligne Linux (LF uniquement, et non CR LF).</span><span class="sxs-lookup"><span data-stu-id="482b1-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="482b1-203">Cette étape garantit une exécution correcte sur les nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="482b1-203">This step ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="482b1-204">Installez la bibliothèque MPI Intel en mode silencieux.</span><span class="sxs-lookup"><span data-stu-id="482b1-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="482b1-205">Configuration de MPI</span><span class="sxs-lookup"><span data-stu-id="482b1-205">Configure MPI</span></span>
<span data-ttu-id="482b1-206">Pour le test, vous devez ajouter les lignes suivantes à /etc/security/limits.conf dans chaque nœud Linux :</span><span class="sxs-lookup"><span data-stu-id="482b1-206">For testing, you should add the following lines to the /etc/security/limits.conf on each of the Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="482b1-207">Redémarrez les nœuds Linux une fois la mise à jour du fichier limits.conf terminée.</span><span class="sxs-lookup"><span data-stu-id="482b1-207">Restart the Linux nodes after you update the limits.conf file.</span></span> <span data-ttu-id="482b1-208">Par exemple, utilisez la commande **clusrun** suivante :</span><span class="sxs-lookup"><span data-stu-id="482b1-208">For example, use the following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="482b1-209">Après le redémarrage, assurez-vous que le dossier partagé est monté en tant que /openfoam.</span><span class="sxs-lookup"><span data-stu-id="482b1-209">After restarting, ensure that the shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="482b1-210">Compiler et installer OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="482b1-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="482b1-211">Enregistrez le package d’installation téléchargé pour le pack source OpenFOAM (OpenFOAM-2.3.1.tgz dans cet exemple) sur C:\OpenFoam sur le nœud principal afin que les nœuds Linux puissent accéder à ce fichier depuis /openfoam.</span><span class="sxs-lookup"><span data-stu-id="482b1-211">Save the downloaded installation package for the OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) to C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="482b1-212">Exécutez ensuite les commandes **clusrun** pour compiler OpenFOAM sur tous les nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="482b1-212">Then run **clusrun** commands to compile OpenFOAM on all the Linux nodes.</span></span>

1. <span data-ttu-id="482b1-213">Créer un dossier /opt/OpenFOAM sur chaque nœud Linux, copiez le package source dans ce dossier et extrayez-le ici.</span><span class="sxs-lookup"><span data-stu-id="482b1-213">Create a folder /opt/OpenFOAM on each Linux node, copy the source package to this folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="482b1-214">Pour compiler OpenFOAM avec la bibliothèque MPI Intel, commencez par configurer certaines variables d’environnement à la fois pour Intel MPI et OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="482b1-214">To compile OpenFOAM with the Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="482b1-215">Pour définir les variables, utilisez un script bash nommé settings.sh.</span><span class="sxs-lookup"><span data-stu-id="482b1-215">Use a bash script called settings.sh to set the variables.</span></span> <span data-ttu-id="482b1-216">Vous trouverez un exemple dans les exemples de fichiers à la fin de cet article.</span><span class="sxs-lookup"><span data-stu-id="482b1-216">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="482b1-217">Placez ce fichier (enregistré avec des fins de ligne Linux) dans le dossier partagé /openfoam.</span><span class="sxs-lookup"><span data-stu-id="482b1-217">Place this file (saved with Linux line endings) in the shared folder /openfoam.</span></span> <span data-ttu-id="482b1-218">Ce fichier contient également des paramètres pour les runtimes MPI et OpenFOAM que vous utiliserez par la suite afin d’exécuter un travail OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="482b1-218">This file also contains settings for the MPI and OpenFOAM runtimes that you use later to run an OpenFOAM job.</span></span>
3. <span data-ttu-id="482b1-219">Installez des packages dépendants nécessaires pour compiler OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="482b1-219">Install dependent packages needed to compile OpenFOAM.</span></span> <span data-ttu-id="482b1-220">En fonction de votre distribution Linux, vous aurez peut-être besoin d’ajouter un référentiel.</span><span class="sxs-lookup"><span data-stu-id="482b1-220">Depending on your Linux distribution, you might first need to add a repository.</span></span> <span data-ttu-id="482b1-221">Exécutez des commandes **clusrun** similaires à la suivante :</span><span class="sxs-lookup"><span data-stu-id="482b1-221">Run **clusrun** commands similar to the following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="482b1-222">Si nécessaire, exécutez une commande SSH sur chaque nœud Linux pour exécuter les commandes afin de vérifier qu’ils fonctionnent correctement.</span><span class="sxs-lookup"><span data-stu-id="482b1-222">If necessary, SSH to each Linux node to run the commands to confirm that they run properly.</span></span>
4. <span data-ttu-id="482b1-223">Exécutez la commande suivante pour compiler OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="482b1-223">Run the following command to compile OpenFOAM.</span></span> <span data-ttu-id="482b1-224">Le processus de compilation prend un certain temps et génère une grande quantité d’informations de journalisation dans la sortie standard. Nous recommandons donc d’utiliser l’option **/interleaved** pour afficher la sortie entrelacée.</span><span class="sxs-lookup"><span data-stu-id="482b1-224">The compilation process takes some time to complete and generates a large amount of log information to standard output, so use the **/interleaved** option to display the output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="482b1-225">Le symbole « \\` » dans la commande est un symbole de caractère d’échappement pour PowerShell.</span><span class="sxs-lookup"><span data-stu-id="482b1-225">The “\\`” symbol in the command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="482b1-226">«\\`& » signifie que « & » fait partie de la commande.</span><span class="sxs-lookup"><span data-stu-id="482b1-226">“\\`&” means the “&” is a part of the command.</span></span>
   > 
   > 

## <a name="prepare-to-run-an-openfoam-job"></a><span data-ttu-id="482b1-227">Préparer l’exécution d’un travail OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="482b1-227">Prepare to run an OpenFOAM job</span></span>
<span data-ttu-id="482b1-228">Préparez-vous maintenant à exécuter une tâche MPI nommée sloshingTank3D (l’un des exemples OpenFoam) sur deux nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="482b1-228">Now get ready to run an MPI job called sloshingTank3D, which is one of the OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-the-runtime-environment"></a><span data-ttu-id="482b1-229">Configurer l’environnement runtime</span><span class="sxs-lookup"><span data-stu-id="482b1-229">Set up the runtime environment</span></span>
<span data-ttu-id="482b1-230">Pour configurer les environnements d’exécution pour MPI et OpenFOAM sur les nœuds Linux, exécutez la commande suivante dans une fenêtre Windows PowerShell sur le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="482b1-230">To set up the runtime environments for MPI and OpenFOAM on the Linux nodes, run the following command in a Windows PowerShell window on the head node.</span></span> <span data-ttu-id="482b1-231">(Cette commande est valide pour SUSE Linux uniquement.)</span><span class="sxs-lookup"><span data-stu-id="482b1-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="482b1-232">Préparer l’exemple de données</span><span class="sxs-lookup"><span data-stu-id="482b1-232">Prepare sample data</span></span>
<span data-ttu-id="482b1-233">Utilisez le partage de nœud principal configuré précédemment pour partager les fichiers d’installation sur les nœuds Linux (monté en tant que /openfoam).</span><span class="sxs-lookup"><span data-stu-id="482b1-233">Use the head node share you configured previously to share files among the Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="482b1-234">Exécutez une commande SSH sur l’un des nœuds de calcul Linux.</span><span class="sxs-lookup"><span data-stu-id="482b1-234">SSH to one of your Linux compute nodes.</span></span>
2. <span data-ttu-id="482b1-235">Exécutez la commande suivante pour configurer l’environnement d’exécution OpenFOAM, si vous ne l’avez pas déjà fait.</span><span class="sxs-lookup"><span data-stu-id="482b1-235">Run the following command to set up the OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="482b1-236">Copiez l’exemple sloshingTank3D dans le dossier partagé et accédez à ce dernier.</span><span class="sxs-lookup"><span data-stu-id="482b1-236">Copy the sloshingTank3D sample to the shared folder and navigate to it.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="482b1-237">Lorsque vous utilisez les paramètres par défaut de cet exemple, l’exécution de l’opération peut prendre des dizaines de minutes. Il se peut donc que vous vouliez modifier certains paramètres pour accélérer le processus.</span><span class="sxs-lookup"><span data-stu-id="482b1-237">When you use the default parameters of this sample, it can take tens of minutes to run, so you might want to modify some parameters to make it run faster.</span></span> <span data-ttu-id="482b1-238">Un choix simple consiste à modifier les variables d’étape de temps deltaT et writeInterval dans le fichier system/controlDict.</span><span class="sxs-lookup"><span data-stu-id="482b1-238">One simple choice is to modify the time step variables deltaT and writeInterval in the system/controlDict file.</span></span> <span data-ttu-id="482b1-239">Ce fichier stocke toutes les données d’entrée relatives au contrôle du temps, ainsi qu’à la lecture et à l’écriture des données de la solution.</span><span class="sxs-lookup"><span data-stu-id="482b1-239">This file stores all input data relating to the control of time and reading and writing solution data.</span></span> <span data-ttu-id="482b1-240">Par exemple, vous pouvez faire passer la valeur deltaT de 0,05 à 0,5 et la valeur writeInterval de 0,05 à 0,5.</span><span class="sxs-lookup"><span data-stu-id="482b1-240">For example, you could change the value of deltaT from 0.05 to 0.5 and the value of writeInterval from 0.05 to 0.5.</span></span>
   
   ![Modifier les variables d’étape][step_variables]
5. <span data-ttu-id="482b1-242">Spécifiez les valeurs souhaitées pour les variables dans le fichier system/decomposeParDict.</span><span class="sxs-lookup"><span data-stu-id="482b1-242">Specify desired values for the variables in the system/decomposeParDict file.</span></span> <span data-ttu-id="482b1-243">Dans cet exemple, deux nœuds Linux de 8 cœurs chacun sont utilisés. Définissez donc la valeur numberOfSubdomains sur 16, et le n de hierarchicalCoeffs sur (1 1 16), ce qui signifie qu’OpenFOAM doit s’exécuter en parallèle avec 16 processus.</span><span class="sxs-lookup"><span data-stu-id="482b1-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains to 16 and n of hierarchicalCoeffs to (1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="482b1-244">Pour plus d’informations, consultez [Guide de l’utilisateur OpenFOAM : 3.4 Exécution d’applications en parallèle](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span><span class="sxs-lookup"><span data-stu-id="482b1-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![Décomposer les processus][decompose]
6. <span data-ttu-id="482b1-246">Exécutez les commandes suivantes à partir du répertoire sloshingTank3D pour préparer les exemples de données.</span><span class="sxs-lookup"><span data-stu-id="482b1-246">Run the following commands from the sloshingTank3D directory to prepare the sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="482b1-247">Sur le nœud principal, vous devez voir que les exemples de fichiers de données sont copiés dans C:\OpenFoam\sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="482b1-247">On the head node, you should see the sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="482b1-248">(C:\OpenFoam est le dossier partagé sur le nœud principal.)</span><span class="sxs-lookup"><span data-stu-id="482b1-248">(C:\OpenFoam is the shared folder on the head node.)</span></span>
   
   ![Fichiers de données sur le nœud principal][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="482b1-250">Fichier hôte pour mpirun</span><span class="sxs-lookup"><span data-stu-id="482b1-250">Host file for mpirun</span></span>
<span data-ttu-id="482b1-251">Au cours de cette étape, vous créez un fichier hôte (une liste de nœuds de calcul) que la commande **mpirun** utilise.</span><span class="sxs-lookup"><span data-stu-id="482b1-251">In this step, you create a host file (a list of compute nodes) which the **mpirun** command uses.</span></span>

1. <span data-ttu-id="482b1-252">Sur l’un des nœuds Linux, créez un fichier nommé hostfile sous /openfoam, afin que ce fichier soit accessible dans /openfoam/hostfile sur tous les nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="482b1-252">On one of the Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="482b1-253">Écrivez vos noms de nœud Linux dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="482b1-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="482b1-254">Dans cet exemple, le fichier contient les noms suivants :</span><span class="sxs-lookup"><span data-stu-id="482b1-254">In this example, the file contains the following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="482b1-255">Vous pouvez également créer ce fichier dans C:\OpenFoam\hostfile sur le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="482b1-255">You can also create this file at C:\OpenFoam\hostfile on the head node.</span></span> <span data-ttu-id="482b1-256">Si vous optez pour cette solution, enregistrez le fichier au format texte avec des fins de lignes Linux (LF uniquement, pas CR LF).</span><span class="sxs-lookup"><span data-stu-id="482b1-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="482b1-257">Cela garantit qu’il s’exécute correctement sur les nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="482b1-257">This ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="482b1-258">**Wrapper de script d’interpréteur de commandes**</span><span class="sxs-lookup"><span data-stu-id="482b1-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="482b1-259">Si vous disposez de plusieurs nœuds Linux et voulez que votre tâche s’exécute uniquement sur certains d’entre eux, nous vous recommandons d’utiliser un fichier hôte fixe, car vous ignorez les nœuds qui seront alloués à votre tâche.</span><span class="sxs-lookup"><span data-stu-id="482b1-259">If you have many Linux nodes and you want your job to run on only some of them, it’s not a good idea to use a fixed host file, because you don’t know which nodes will be allocated to your job.</span></span> <span data-ttu-id="482b1-260">Dans ce cas, écrivez un wrapper de script Bash pour **mpirun** afin de créer le fichier hôte automatiquement.</span><span class="sxs-lookup"><span data-stu-id="482b1-260">In this case, write a bash script wrapper for **mpirun** to create the host file automatically.</span></span> <span data-ttu-id="482b1-261">Vous pouvez trouver un exemple de wrapper de script bash nommé hpcimpirun.sh à la fin de cet article, et l’enregistrer en tant que /openfoam/hpcimpirun.sh.</span><span class="sxs-lookup"><span data-stu-id="482b1-261">You can find an example bash script wrapper called hpcimpirun.sh at the end of this article, and save it as /openfoam/hpcimpirun.sh.</span></span> <span data-ttu-id="482b1-262">L’exemple de script effectue les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="482b1-262">This example script does the following:</span></span>
   
   1. <span data-ttu-id="482b1-263">Configure les variables d’environnement pour **mpirun**, et certains paramètres de commande supplémentaires pour exécuter le travail MPI via le réseau RDMA.</span><span class="sxs-lookup"><span data-stu-id="482b1-263">Sets up the environment variables for **mpirun**, and some addition command parameters to run the MPI job through the RDMA network.</span></span> <span data-ttu-id="482b1-264">Dans ce cas, il définit les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="482b1-264">In this case, it sets the following variables:</span></span>
      
      * <span data-ttu-id="482b1-265">I_MPI_FABRICS=shm:dapl</span><span class="sxs-lookup"><span data-stu-id="482b1-265">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="482b1-266">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span><span class="sxs-lookup"><span data-stu-id="482b1-266">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="482b1-267">I_MPI_DYNAMIC_CONNECTION=0</span><span class="sxs-lookup"><span data-stu-id="482b1-267">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="482b1-268">Crée un fichier d’hôte en fonction de la variable d’environnement $CCP_NODES_CORES définie par le nœud principal HPC lorsque le travail est activé.</span><span class="sxs-lookup"><span data-stu-id="482b1-268">Creates a host file according to the environment variable $CCP_NODES_CORES, which is set by the HPC head node when the job is activated.</span></span>
      
      <span data-ttu-id="482b1-269">Le format de $CCP_NODES_CORES suit ce modèle :</span><span class="sxs-lookup"><span data-stu-id="482b1-269">The format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="482b1-270">où</span><span class="sxs-lookup"><span data-stu-id="482b1-270">where</span></span>
      
      * <span data-ttu-id="482b1-271">`<Number of nodes>` : nombre de nœuds affectés à ce travail.</span><span class="sxs-lookup"><span data-stu-id="482b1-271">`<Number of nodes>` - the number of nodes allocated to this job.</span></span>  
      * <span data-ttu-id="482b1-272">`<Name of node_n_...>` : nom de chaque nœud affecté à ce travail.</span><span class="sxs-lookup"><span data-stu-id="482b1-272">`<Name of node_n_...>` - the name of each node allocated to this job.</span></span>
      * <span data-ttu-id="482b1-273">`<Cores of node_n_...>` : nombre de cœurs présents sur le nœud affecté à ce travail.</span><span class="sxs-lookup"><span data-stu-id="482b1-273">`<Cores of node_n_...>` - the number of cores on the node allocated to this job.</span></span>
      
      <span data-ttu-id="482b1-274">Par exemple, si l’exécution de la tâche requiert deux nœuds, la valeur de $CCP_NODES_CORES se présente comme suit</span><span class="sxs-lookup"><span data-stu-id="482b1-274">For example, if the job needs two nodes to run, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="482b1-275">Appelle la commande **mpirun** , et ajoute deux paramètres à la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="482b1-275">Calls the **mpirun** command and appends two parameters to the command line.</span></span>
      
      * <span data-ttu-id="482b1-276">`--hostfile <hostfilepath>: <hostfilepath>` : le chemin d’accès du fichier hôte que le script crée</span><span class="sxs-lookup"><span data-stu-id="482b1-276">`--hostfile <hostfilepath>: <hostfilepath>` - the path of the host file the script creates</span></span>
      * <span data-ttu-id="482b1-277">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` : une variable d’environnement définie par le nœud principal HPC Pack, qui stocke le nombre total de cœurs affectés à ce travail.</span><span class="sxs-lookup"><span data-stu-id="482b1-277">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by the HPC Pack head node, which stores the number of total cores allocated to this job.</span></span> <span data-ttu-id="482b1-278">Dans ce cas, elle spécifie le nombre de processus pour **mpirun**.</span><span class="sxs-lookup"><span data-stu-id="482b1-278">In this case, it specifies the number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="482b1-279">Envoi d’un travail OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="482b1-279">Submit an OpenFOAM job</span></span>
<span data-ttu-id="482b1-280">Maintenant, vous pouvez envoyer un travail dans HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="482b1-280">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="482b1-281">Vous devez transférer le script hpcimpirun.sh dans les lignes de commande pour certaines des tâches du travail.</span><span class="sxs-lookup"><span data-stu-id="482b1-281">You need to pass the script hpcimpirun.sh in the command lines for some of the job tasks.</span></span>

1. <span data-ttu-id="482b1-282">Connectez-vous à votre nœud principal de cluster et démarrez HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="482b1-282">Connect to your cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="482b1-283">Dans **Gestion des ressources**, assurez-vous que les nœuds de calcul Linux sont à l’état **En ligne**.</span><span class="sxs-lookup"><span data-stu-id="482b1-283">**In Resource Management**, ensure that the Linux compute nodes are in the **Online** state.</span></span> <span data-ttu-id="482b1-284">Si ce n’est pas le cas, sélectionnez-les et cliquez sur **Mettre en ligne**.</span><span class="sxs-lookup"><span data-stu-id="482b1-284">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="482b1-285">Dans **Gestion des tâches**, cliquez sur **Nouveau travail**.</span><span class="sxs-lookup"><span data-stu-id="482b1-285">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="482b1-286">Entrez un nom pour le travail, par exemple *sloshingTank3D*.</span><span class="sxs-lookup"><span data-stu-id="482b1-286">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![Détails du travail][job_details]
5. <span data-ttu-id="482b1-288">Dans les **ressources de la tâche**, sélectionnez le type de ressource en tant que « Nœud » et définissez la valeur minimale sur 2.</span><span class="sxs-lookup"><span data-stu-id="482b1-288">In **Job resources**, choose the type of resource as “Node” and set the Minimum to 2.</span></span> <span data-ttu-id="482b1-289">Cette configuration exécute la tâche sur deux nœuds Linux, chacun d’eux comportant huit cœurs dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="482b1-289">This configuration runs the job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![ressources de la tâche][job_resources]
6. <span data-ttu-id="482b1-291">Cliquez sur **Modifier des tâches** dans le volet de navigation gauche, puis sur **Ajouter** pour ajouter une tâche au travail.</span><span class="sxs-lookup"><span data-stu-id="482b1-291">Click **Edit Tasks** in the left navigation, and then click **Add** to add a task to the job.</span></span> <span data-ttu-id="482b1-292">Ajoutez quatre tâches au travail avec les lignes de commande et les paramètres suivants.</span><span class="sxs-lookup"><span data-stu-id="482b1-292">Add four tasks to the job with the following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="482b1-293">L’exécution de  `source /openfoam/settings.sh` configure les environnements d’exécution OpenFOAM et MPI pour que chacune des tâches suivantes l’appelle avant la commande OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="482b1-293">Running `source /openfoam/settings.sh` sets up the OpenFOAM and MPI runtime environments, so each of the following tasks calls it before the OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="482b1-294">**Tâche 1**.</span><span class="sxs-lookup"><span data-stu-id="482b1-294">**Task 1**.</span></span> <span data-ttu-id="482b1-295">Exécutez **decomposePar** pour générer des fichiers de données pour l’exécution de **interDyMFoam** en parallèle.</span><span class="sxs-lookup"><span data-stu-id="482b1-295">Run **decomposePar** to generate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="482b1-296">Affecter un nœud à la tâche</span><span class="sxs-lookup"><span data-stu-id="482b1-296">Assign one node to the task</span></span>
     * <span data-ttu-id="482b1-297">**Ligne de commande** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="482b1-297">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="482b1-298">**Répertoire de travail** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="482b1-298">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="482b1-299">Voir la figure suivante.</span><span class="sxs-lookup"><span data-stu-id="482b1-299">See the following figure.</span></span> <span data-ttu-id="482b1-300">Vous configurez les tâches restantes de la même manière.</span><span class="sxs-lookup"><span data-stu-id="482b1-300">You configure the remaining tasks similarly.</span></span>
     
     ![Détails de la tâche 1][task_details1]
   * <span data-ttu-id="482b1-302">**Tâche 2**.</span><span class="sxs-lookup"><span data-stu-id="482b1-302">**Task 2**.</span></span> <span data-ttu-id="482b1-303">Exécutez **interDyMFoam** en parallèle pour calculer l’exemple.</span><span class="sxs-lookup"><span data-stu-id="482b1-303">Run **interDyMFoam** in parallel to compute the sample.</span></span>
     
     * <span data-ttu-id="482b1-304">Affectez deux nœuds à la tâche</span><span class="sxs-lookup"><span data-stu-id="482b1-304">Assign two nodes to the task</span></span>
     * <span data-ttu-id="482b1-305">**Ligne de commande** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="482b1-305">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="482b1-306">**Répertoire de travail** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="482b1-306">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="482b1-307">**Tâche 3**.</span><span class="sxs-lookup"><span data-stu-id="482b1-307">**Task 3**.</span></span> <span data-ttu-id="482b1-308">Exécutez la commande **reconstructPar** pour fusionner les jeux de répertoires temporels à partir de chaque répertoire processor_N en un seul jeu.</span><span class="sxs-lookup"><span data-stu-id="482b1-308">Run **reconstructPar** to merge the sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="482b1-309">Affecter un nœud à la tâche</span><span class="sxs-lookup"><span data-stu-id="482b1-309">Assign one node to the task</span></span>
     * <span data-ttu-id="482b1-310">**Ligne de commande** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="482b1-310">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="482b1-311">**Répertoire de travail** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="482b1-311">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="482b1-312">**Tâche 4**.</span><span class="sxs-lookup"><span data-stu-id="482b1-312">**Task 4**.</span></span> <span data-ttu-id="482b1-313">Exécutez **foamToEnsight** en parallèle pour convertir les fichiers de résultats OpenFOAM au format EnSight et placez les fichiers EnSight dans un répertoire nommé Ensight dans le répertoire du cas.</span><span class="sxs-lookup"><span data-stu-id="482b1-313">Run **foamToEnsight** in parallel to convert the OpenFOAM result files into EnSight format and place the EnSight files in a directory named Ensight in the case directory.</span></span>
     
     * <span data-ttu-id="482b1-314">Affectez deux nœuds à la tâche</span><span class="sxs-lookup"><span data-stu-id="482b1-314">Assign two nodes to the task</span></span>
     * <span data-ttu-id="482b1-315">**Ligne de commande** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="482b1-315">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="482b1-316">**Répertoire de travail** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="482b1-316">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="482b1-317">Ajoutez des dépendances à ces tâches dans l’ordre croissant des tâches.</span><span class="sxs-lookup"><span data-stu-id="482b1-317">Add dependencies to these tasks in ascending task order.</span></span>
   
   ![Dépendances de la tâche][task_dependencies]
8. <span data-ttu-id="482b1-319">Cliquez sur **Envoyer** pour exécuter ce travail.</span><span class="sxs-lookup"><span data-stu-id="482b1-319">Click **Submit** to run this job.</span></span>
   
   <span data-ttu-id="482b1-320">Par défaut, HPC Pack envoie la tâche en tant que votre compte d’utilisateur connecté actuel.</span><span class="sxs-lookup"><span data-stu-id="482b1-320">By default, HPC Pack submits the job as your current logged-on user account.</span></span> <span data-ttu-id="482b1-321">Une fois que vous avez cliqué sur **Envoyer**, une boîte de dialogue peut vous inviter à entrer le nom d’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="482b1-321">After you click **Submit**, you might see a dialog box prompting you to enter the user name and password.</span></span>
   
   ![Informations d’identification de la tâche][creds]
   
   <span data-ttu-id="482b1-323">Dans certaines conditions, HPC Pack mémorise les informations utilisateur entrées auparavant et n’affiche plus cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="482b1-323">Under some conditions, HPC Pack remembers the user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="482b1-324">Pour que HPC Pack l’affiche de nouveau, entrez les informations suivantes à l’invite de commande, puis envoyez le travail.</span><span class="sxs-lookup"><span data-stu-id="482b1-324">To make HPC Pack show it again, enter the following command at a Command prompt and then submit the job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="482b1-325">Ce travail prend de quelques dizaines de minutes à plusieurs heures en fonction des paramètres que vous avez définis pour l’exemple.</span><span class="sxs-lookup"><span data-stu-id="482b1-325">The job takes from tens of minutes to several hours according to the parameters you have set for the sample.</span></span> <span data-ttu-id="482b1-326">Sur la carte thermique, vous voyez le travail s’exécutant sur les nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="482b1-326">In the heat map, you see the job running on the Linux nodes.</span></span> 
   
   ![Carte thermique][heat_map]
   
   <span data-ttu-id="482b1-328">Sur chaque nœud, huit processus sont démarrés.</span><span class="sxs-lookup"><span data-stu-id="482b1-328">On each node, eight processes are started.</span></span>
   
   ![Processus Linux][linux_processes]
10. <span data-ttu-id="482b1-330">Lorsque le travail se termine, recherchez les résultats du travail dans les dossiers sous C:\OpenFoam\sloshingTank3D et les fichiers journaux dans C:\OpenFoam.</span><span class="sxs-lookup"><span data-stu-id="482b1-330">When the job finishes, find the job results in folders under C:\OpenFoam\sloshingTank3D, and the log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="482b1-331">Afficher les résultats dans EnSight</span><span class="sxs-lookup"><span data-stu-id="482b1-331">View results in EnSight</span></span>
<span data-ttu-id="482b1-332">Vous pouvez également utiliser [EnSight](https://www.ceisoftware.com/) pour visualiser et analyser les résultats du travail OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="482b1-332">Optionally use [EnSight](https://www.ceisoftware.com/) to visualize and analyze the results of the OpenFOAM job.</span></span> <span data-ttu-id="482b1-333">Pour plus d’informations sur la visualisation et l’animation dans EnSight, consultez le [guide vidéo](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span><span class="sxs-lookup"><span data-stu-id="482b1-333">For more about visualization and animation in EnSight, see this [video guide](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span></span>

1. <span data-ttu-id="482b1-334">Après avoir installé EnSight sur le nœud principal, démarrez le service.</span><span class="sxs-lookup"><span data-stu-id="482b1-334">After you install EnSight on the head node, start it.</span></span>
2. <span data-ttu-id="482b1-335">Ouvrez C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span><span class="sxs-lookup"><span data-stu-id="482b1-335">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="482b1-336">Vous verrez une citerne dans la visionneuse.</span><span class="sxs-lookup"><span data-stu-id="482b1-336">You see a tank in the viewer.</span></span>
   
   ![Réservoir dans EnSight][tank]
3. <span data-ttu-id="482b1-338">Créez une **Isosurface** à partir de **internalMesh**, puis choisissez la variable **alpha_water**.</span><span class="sxs-lookup"><span data-stu-id="482b1-338">Create an **Isosurface** from **internalMesh**, and then choose the variable **alpha_water**.</span></span>
   
   ![Créer une isosurface][isosurface]
4. <span data-ttu-id="482b1-340">Définissez la couleur de l’élément **Isosurface_part** créé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="482b1-340">Set the color for **Isosurface_part** created in the previous step.</span></span> <span data-ttu-id="482b1-341">Par exemple, définissez la sur bleu océan.</span><span class="sxs-lookup"><span data-stu-id="482b1-341">For example, set it to water blue.</span></span>
   
   ![Modifier la couleur de l’isosurface][isosurface_color]
5. <span data-ttu-id="482b1-343">Créez un **Isovolume** à partir des **parois** en sélectionnant **parois** dans le panneau **Pièces**, puis cliquez sur le bouton **Isosurfaces** dans la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="482b1-343">Create an **Iso-volume** from **walls** by selecting **walls** in the **Parts** panel and click the **Isosurfaces** button in the toolbar.</span></span>
6. <span data-ttu-id="482b1-344">Dans la boîte de dialogue, sélectionnez **Type** en tant qu’**Isovolume** et définissez la **plage Isovolume** minimale sur 0,5.</span><span class="sxs-lookup"><span data-stu-id="482b1-344">In the dialog box, select **Type** as **Isovolume** and set the Min of **Isovolume range** to 0.5.</span></span> <span data-ttu-id="482b1-345">Pour créer l’isovolume, cliquez sur **Créer avec des pièces sélectionnées**.</span><span class="sxs-lookup"><span data-stu-id="482b1-345">To create the isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="482b1-346">Définissez la couleur de l’élément **Iso_volume_part** créé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="482b1-346">Set the color for **Iso_volume_part** created in the previous step.</span></span> <span data-ttu-id="482b1-347">Par exemple, définissez sur bleu profond.</span><span class="sxs-lookup"><span data-stu-id="482b1-347">For example, set it to deep water blue.</span></span>
8. <span data-ttu-id="482b1-348">Définissez la couleur des **parois**.</span><span class="sxs-lookup"><span data-stu-id="482b1-348">Set the color for **walls**.</span></span> <span data-ttu-id="482b1-349">Par exemple, définissez-le sur blanc transparent.</span><span class="sxs-lookup"><span data-stu-id="482b1-349">For example, set it to transparent white.</span></span>
9. <span data-ttu-id="482b1-350">Cliquez maintenant sur **Lire** pour afficher les résultats de la simulation.</span><span class="sxs-lookup"><span data-stu-id="482b1-350">Now click **Play** to see the results of the simulation.</span></span>
   
    ![Résultat du réservoir][tank_result]

## <a name="sample-files"></a><span data-ttu-id="482b1-352">Exemple de fichiers</span><span class="sxs-lookup"><span data-stu-id="482b1-352">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="482b1-353">Exemple de fichier de configuration XML pour le déploiement de clusters par script PowerShell</span><span class="sxs-lookup"><span data-stu-id="482b1-353">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
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

### <a name="sample-credxml-file"></a><span data-ttu-id="482b1-354">Exemple de fichier cred.xml</span><span class="sxs-lookup"><span data-stu-id="482b1-354">Sample cred.xml file</span></span>
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
### <a name="sample-silentcfg-file-to-install-mpi"></a><span data-ttu-id="482b1-355">Exemple de fichier silent.cfg pour installer MPI</span><span class="sxs-lookup"><span data-stu-id="482b1-355">Sample silent.cfg file to install MPI</span></span>
```
# Patterns used to check silent configuration file
#
# anythingpat - any string
# filepat     - the file location pattern (/file/location/to/license.lic)
# lspat       - the license server address pattern (0123@hostname)
# snpat       - the serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components to install, valid values are: {ALL, DEFAULTS, anythingpat}
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

# Path to the cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes to enable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes to update ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="482b1-356">Exemple de script settings.sh</span><span class="sxs-lookup"><span data-stu-id="482b1-356">Sample settings.sh script</span></span>
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


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="482b1-357">Exemple de script hpcimpirun.sh</span><span class="sxs-lookup"><span data-stu-id="482b1-357">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# The path of this script
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
    # CCP_NODES_CORES is not found or is empty, just run the mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create the hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into the hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run the mpirun with hostfile arg
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
