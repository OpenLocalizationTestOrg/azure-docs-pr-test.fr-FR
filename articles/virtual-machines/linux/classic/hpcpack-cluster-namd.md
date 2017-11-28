---
title: aaaNAMD avec Microsoft HPC Pack sur les machines virtuelles Linux | Documents Microsoft
description: "Déployer un cluster Microsoft HPC Pack sur Azure et exécuter une simulation NAMD avec charmrun sur plusieurs nœuds de calcul Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a><span data-ttu-id="ccada-103">Exécution de NAMD avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="ccada-103">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>
<span data-ttu-id="ccada-104">Cet article explique monodirectionnelle toorun une charge de travail informatique de hautes performances (HPC) Linux sur les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="ccada-104">This article shows you one way toorun a Linux high-performance computing (HPC) workload on Azure virtual machines.</span></span> <span data-ttu-id="ccada-105">Ici, vous configurez un [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) de cluster avec les nœuds de calcul Linux sur Azure et exécuter un [NAMD](http://www.ks.uiuc.edu/Research/namd/) toocalculate de simulation et de visualiser la structure hello d’un système BIOMOLÉCULAIRE volumineux.</span><span class="sxs-lookup"><span data-stu-id="ccada-105">Here, you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster on Azure with Linux compute nodes and run a [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulation toocalculate and visualize hello structure of a large biomolecular system.</span></span>  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* <span data-ttu-id="ccada-106">**NAMD** (pour le programme de Dynamics moléculaire d’a) est un package parallèle dynamics moléculaire conçu pour la simulation de hautes performances des systèmes de BIOMOLÉCULAIRE volumineux contenant des toomillions des atomes.</span><span class="sxs-lookup"><span data-stu-id="ccada-106">**NAMD** (for Nanoscale Molecular Dynamics program) is a parallel molecular dynamics package designed for high-performance simulation of large biomolecular systems containing up toomillions of atoms.</span></span> <span data-ttu-id="ccada-107">Ces systèmes sont par exemple les virus, les structures de cellule et les grandes protéines.</span><span class="sxs-lookup"><span data-stu-id="ccada-107">Examples of these systems include viruses, cell structures, and large proteins.</span></span> <span data-ttu-id="ccada-108">NAMD ajuste toohundreds de cœurs pour les simulations classiques et toomore à 500 000 cœurs pour les simulations de plus grande hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-108">NAMD scales toohundreds of cores for typical simulations and toomore than 500,000 cores for hello largest simulations.</span></span>
* <span data-ttu-id="ccada-109">**Microsoft HPC Pack** fournit les fonctionnalités toorun HPC à grande échelle et des applications parallèles dans les clusters d’ordinateurs locaux ou des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="ccada-109">**Microsoft HPC Pack** provides features toorun large-scale HPC and parallel applications in clusters of on-premises computers or Azure virtual machines.</span></span> <span data-ttu-id="ccada-110">Développée à l’origine comme solution pour les charges de travail Windows HPC, HPC Pack prend désormais en charge l’exécution d’applications HPC Linux sur les machines virtuelles de nœuds de calcul Linux déployées dans un cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="ccada-110">Originally developed as a solution for Windows HPC workloads, HPC Pack now supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="ccada-111">Consultez la présentation [Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md) .</span><span class="sxs-lookup"><span data-stu-id="ccada-111">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction.</span></span>

<span data-ttu-id="ccada-112">Pour les autres options de toorun Linux HPC les charges de travail dans Azure, consultez [ressources techniques pour le traitement et l’informatique hautes performances](../../../batch/batch-hpc-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="ccada-112">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/batch-hpc-solutions.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccada-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ccada-113">Prerequisites</span></span>
* <span data-ttu-id="ccada-114">**Cluster HPC Pack avec nœuds de calcul Linux** : déployez un cluster HPC Pack avec des nœuds de calcul Linux dans Azure à l’aide d’un [modèle Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) ou d’un [script Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="ccada-114">**HPC Pack cluster with Linux compute nodes** - Deploy an HPC Pack cluster with Linux compute nodes on Azure using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="ccada-115">Consultez [prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md) pour les conditions préalables de hello et étapes dans les deux cas.</span><span class="sxs-lookup"><span data-stu-id="ccada-115">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="ccada-116">Si vous choisissez hello option de déploiement de script PowerShell, consultez le fichier de configuration d’exemple hello dans les fichiers d’exemple hello à fin hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="ccada-116">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="ccada-117">Ce fichier configure un cluster HPC Pack basé sur Azure comportant un nœud principal Windows Server 2012 R2 et quatre nœuds de calcul de grande taille CentOS 6.6.</span><span class="sxs-lookup"><span data-stu-id="ccada-117">This file configures an Azure-based HPC Pack cluster consisting of a Windows Server 2012 R2 head node and four size Large CentOS 6.6 compute nodes.</span></span> <span data-ttu-id="ccada-118">Personnalisez ce fichier comme il convient pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="ccada-118">Customize this file as needed for your environment.</span></span>
* <span data-ttu-id="ccada-119">**Fichiers de logiciel et didacticiel NAMD** -logiciel NAMD de téléchargement pour Linux à partir de hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (inscription requise).</span><span class="sxs-lookup"><span data-stu-id="ccada-119">**NAMD software and tutorial files** - Download NAMD software for Linux from hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registration required).</span></span> <span data-ttu-id="ccada-120">Cet article est basé sur la version 2.10 de NAMD et utilise hello [Linux-x86_64 (64 bits Intel/AMD avec Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span><span class="sxs-lookup"><span data-stu-id="ccada-120">This article is based on NAMD version 2.10, and uses hello [Linux-x86_64 (64-bit Intel/AMD with Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span></span> <span data-ttu-id="ccada-121">Téléchargez également hello [de fichiers de didacticiel NAMD](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span><span class="sxs-lookup"><span data-stu-id="ccada-121">Also download hello [NAMD tutorial files](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span></span> <span data-ttu-id="ccada-122">Hello téléchargements sont les fichiers .tar, et vous avez besoin d’un Windows outil tooextract hello les fichiers sur le nœud principal du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-122">hello downloads are .tar files, and you need a Windows tool tooextract hello files on hello cluster head node.</span></span> <span data-ttu-id="ccada-123">fichiers de hello tooextract, suivez les instructions de hello plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="ccada-123">tooextract hello files, follow hello instructions later in this article.</span></span> 
* <span data-ttu-id="ccada-124">**VMD** (facultatif) - toosee les résultats de hello de votre travail NAMD, télécharger et installer le programme de visualisation moléculaire hello [VMD](http://www.ks.uiuc.edu/Research/vmd/) sur un ordinateur de votre choix.</span><span class="sxs-lookup"><span data-stu-id="ccada-124">**VMD** (optional) - toosee hello results of your NAMD job, download and install hello molecular visualization program [VMD](http://www.ks.uiuc.edu/Research/vmd/) on a computer of your choice.</span></span> <span data-ttu-id="ccada-125">version actuelle de Hello est 1.9.2.</span><span class="sxs-lookup"><span data-stu-id="ccada-125">hello current version is 1.9.2.</span></span> <span data-ttu-id="ccada-126">Consultez hello VDM télécharger tooget de site a démarré.</span><span class="sxs-lookup"><span data-stu-id="ccada-126">See hello VMD download site tooget started.</span></span>  

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="ccada-127">Configuration de l’approbation mutuelle entre les nœuds de calcul</span><span class="sxs-lookup"><span data-stu-id="ccada-127">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="ccada-128">L’exécution d’une tâche entre nœuds sur plusieurs nœuds Linux requiert hello nœuds tootrust eux (par **rsh** ou **ssh**).</span><span class="sxs-lookup"><span data-stu-id="ccada-128">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="ccada-129">Lorsque vous créez un cluster HPC Pack de hello avec hello script de déploiement Microsoft HPC Pack IaaS, script de hello configure automatiquement permanente confiance mutuelle pour le compte administrateur hello que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="ccada-129">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="ccada-130">Pour les utilisateurs non-administrateurs que vous créez dans le domaine de ce cluster hello, vous avez tooset temporaire approbation mutuelle entre les nœuds de hello lorsqu’un travail est alloué toothem.</span><span class="sxs-lookup"><span data-stu-id="ccada-130">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem.</span></span> <span data-ttu-id="ccada-131">Ensuite, détruisez relation de hello hello tâche est terminée.</span><span class="sxs-lookup"><span data-stu-id="ccada-131">Then, destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="ccada-132">toodo cela pour chaque utilisateur, de fournir un cluster toohello de paire de clés RSA les HPC Pack utilise la relation d’approbation tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-132">toodo this for each user, provide an RSA key pair toohello cluster which HPC Pack uses tooestablish hello trust relationship.</span></span> <span data-ttu-id="ccada-133">Instructions ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ccada-133">Instructions follow.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="ccada-134">Génération d’une paire de clés RSA</span><span class="sxs-lookup"><span data-stu-id="ccada-134">Generate an RSA key pair</span></span>
<span data-ttu-id="ccada-135">Il est facile toogenerate une paire de clés RSA, qui contient une clé publique et une clé privée, en exécutant hello Linux **ssh-keygen** commande.</span><span class="sxs-lookup"><span data-stu-id="ccada-135">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="ccada-136">Ouvrez une session tooa ordinateur Linux.</span><span class="sxs-lookup"><span data-stu-id="ccada-136">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="ccada-137">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ccada-137">Run hello following command:</span></span>
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="ccada-138">Appuyez sur **entrée** toouse hello paramètres jusqu'à ce que la commande hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="ccada-138">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="ccada-139">N'entrez pas de phrase secrète ici ; à l'invite de mot de passe, appuyez simplement sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="ccada-139">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Génération d’une paire de clés RSA][keygen]
3. <span data-ttu-id="ccada-141">Modification toohello ~/.ssh répertoire.</span><span class="sxs-lookup"><span data-stu-id="ccada-141">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="ccada-142">clé privée de Hello est stockée dans la clé publique id_rsa et hello dans id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="ccada-142">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![Clés publiques et privées][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="ccada-144">Ajouter un cluster de HPC Pack toohello hello paire de clés</span><span class="sxs-lookup"><span data-stu-id="ccada-144">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="ccada-145">[Connexion Bureau à distance](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) à l’aide de machine virtuelle de nœud principal toohello hello des informations d’identification de domaine vous avez fourni lorsque vous avez déployé le cluster hello (par exemple, hpc\clusteradmin).</span><span class="sxs-lookup"><span data-stu-id="ccada-145">[Connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, hpc\clusteradmin).</span></span> <span data-ttu-id="ccada-146">Vous gérez un cluster de hello à partir du nœud principal hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-146">You manage hello cluster from hello head node.</span></span>
2. <span data-ttu-id="ccada-147">Utilisez toocreate de procédures standard Windows Server un compte d’utilisateur de domaine dans le domaine d’Active Directory du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-147">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="ccada-148">Par exemple, utiliser hello utilisateur Active Directory et outil d’ordinateurs sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-148">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="ccada-149">les exemples de Hello dans cet article supposent que vous créez un utilisateur de domaine nommé hpcuser dans le domaine de hpclab hello (hpclab\hpcuser).</span><span class="sxs-lookup"><span data-stu-id="ccada-149">hello examples in this article assume you create a domain user named hpcuser in hello hpclab domain (hpclab\hpcuser).</span></span>
3. <span data-ttu-id="ccada-150">Ajoutez le cluster HPC Pack toohello hello domaine utilisateur en tant qu’un utilisateur de cluster.</span><span class="sxs-lookup"><span data-stu-id="ccada-150">Add hello domain user toohello HPC Pack cluster as a cluster user.</span></span> <span data-ttu-id="ccada-151">Pour obtenir des instructions, consultez [Ajouter ou supprimer des utilisateurs du cluster](https://technet.microsoft.com/library/ff919330.aspx).</span><span class="sxs-lookup"><span data-stu-id="ccada-151">For instructions, see [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).</span></span>
4. <span data-ttu-id="ccada-152">Créez un fichier nommé C:\cred.xml et copier hello RSA clé des données dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="ccada-152">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="ccada-153">Vous trouverez un exemple Bonjour exemples de fichiers à la fin de hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="ccada-153">You can find an example in hello sample files at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. <span data-ttu-id="ccada-154">Ouvrez une invite de commandes et entrez hello tooset hello données hello hpclab\hpcuser compte les informations d’identification de commande suivante.</span><span class="sxs-lookup"><span data-stu-id="ccada-154">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="ccada-155">Vous utilisez hello **extendeddata** toopass de paramètre hello nom du fichier de C:\cred.xml hello vous avez créé pour les données de clé hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-155">You use hello **extendeddata** parameter toopass hello name of hello C:\cred.xml file you created for hello key data.</span></span>
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="ccada-156">Cette commande se termine correctement sans sortie.</span><span class="sxs-lookup"><span data-stu-id="ccada-156">This command completes successfully without output.</span></span> <span data-ttu-id="ccada-157">Après avoir défini les informations d’identification hello pour les comptes d’utilisateur hello que vous devez toorun travaux, stockez le fichier de cred.xml de hello dans un emplacement sécurisé ou supprimez-le.</span><span class="sxs-lookup"><span data-stu-id="ccada-157">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
6. <span data-ttu-id="ccada-158">Si vous avez généré hello paire de clés RSA sur l’un de vos nœuds de Linux, n’oubliez pas les clés hello toodelete après avoir terminé leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="ccada-158">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="ccada-159">HPC Pack ne configure pas l’approbation mutuelle s’il trouve des fichiers id_rsa ou id_rsa.pub existants.</span><span class="sxs-lookup"><span data-stu-id="ccada-159">HPC Pack does not set up mutual trust if it finds an existing id_rsa file or id_rsa.pub file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ccada-160">Nous ne recommandons l’exécution d’un travail de Linux en tant qu’un administrateur de cluster sur un cluster partagé, car une tâche envoyée par un administrateur s’exécute sous un compte de racine hello des nœuds de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-160">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="ccada-161">Une tâche envoyée par un utilisateur non administrateur s’exécute sous un compte d’utilisateur local Linux avec hello même nom en tant qu’utilisateur de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-161">A job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="ccada-162">Dans ce cas, HPC Pack définit confiance mutuelle pour cet utilisateur Linux sur tous les nœuds hello allouées toohello travail.</span><span class="sxs-lookup"><span data-stu-id="ccada-162">In this case, HPC Pack sets up mutual trust for this Linux user across all hello nodes allocated toohello job.</span></span> <span data-ttu-id="ccada-163">Vous pouvez configurer des utilisateurs de Linux hello manuellement sur les nœuds de Linux hello avant d’exécuter le travail de hello ou HPC Pack crée automatiquement les utilisateur hello lorsque le travail de hello est envoyé.</span><span class="sxs-lookup"><span data-stu-id="ccada-163">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="ccada-164">Si HPC Pack crée un utilisateur de hello, HPC Pack supprime une fois hello travail terminé.</span><span class="sxs-lookup"><span data-stu-id="ccada-164">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="ccada-165">tooreduce menace pour la sécurité, hello clés sont supprimées après la fin de la tâche de hello sur les nœuds hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-165">tooreduce security threat, hello keys are removed after hello job completes on hello nodes.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="ccada-166">Configuration d’un partage de fichiers pour les nœuds Linux</span><span class="sxs-lookup"><span data-stu-id="ccada-166">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="ccada-167">Maintenant configurer un partage de fichiers SMB et monter le dossier partagé de hello sur tous les nœuds tooallow hello Linux nœuds tooaccess NAMD fichiers Linux avec un chemin d’accès commun.</span><span class="sxs-lookup"><span data-stu-id="ccada-167">Now set up an SMB file share, and mount hello shared folder on all Linux nodes tooallow hello Linux nodes tooaccess NAMD files with a common path.</span></span> <span data-ttu-id="ccada-168">Voici les étapes toomount un dossier partagé sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-168">Following are steps toomount a shared folder on hello head node.</span></span> <span data-ttu-id="ccada-169">Un partage est recommandé pour les distributions tels que CentOS 6.6 actuellement ne prend en charge les services de fichiers Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-169">A share is recommended for distributions such as CentOS 6.6 that currently don’t support hello Azure File service.</span></span> <span data-ttu-id="ccada-170">Si vos nœuds Linux prend en charge un partage de fichiers Azure, consultez [comment toouse stockage Azure files avec Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ccada-170">If your Linux nodes support an Azure File share, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="ccada-171">Pour des options supplémentaires de partage des fichiers avec HPC Pack, consultez [Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ccada-171">For additional file sharing options with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="ccada-172">Créez un dossier sur le nœud principal de hello et partagez-le tooEveryone en définissant des privilèges de lecture/écriture.</span><span class="sxs-lookup"><span data-stu-id="ccada-172">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="ccada-173">Dans cet exemple, \\ \\CentOS66HN\Namd est le nom hello du dossier hello, où CentOS66HN est le nom d’hôte hello de nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-173">In this example, \\\\CentOS66HN\Namd is hello name of hello folder, where CentOS66HN is hello host name of hello head node.</span></span>
2. <span data-ttu-id="ccada-174">Créer un sous-dossier nommé namd2 dans le dossier partagé de hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-174">Create a subfolder named namd2 in hello shared folder.</span></span> <span data-ttu-id="ccada-175">Créez un autre sous-dossier nommé namdsample dans namd2.</span><span class="sxs-lookup"><span data-stu-id="ccada-175">In namd2, create another subfolder named namdsample.</span></span>
3. <span data-ttu-id="ccada-176">Extraire hello NAMD fichiers hello dossier à l’aide d’une version Windows de **tar** ou un autre utilitaire de Windows qui fonctionne sur les archives .tar.</span><span class="sxs-lookup"><span data-stu-id="ccada-176">Extract hello NAMD files in hello folder by using a Windows version of **tar** or another Windows utility that operates on .tar archives.</span></span> 
   
   * <span data-ttu-id="ccada-177">Extraire archive tar NAMD hello trop\\\\CentOS66HN\Namd\namd2.</span><span class="sxs-lookup"><span data-stu-id="ccada-177">Extract hello NAMD tar archive too\\\\CentOS66HN\Namd\namd2.</span></span>
   * <span data-ttu-id="ccada-178">Extraire les fichiers du didacticiel hello sous \\ \\CentOS66HN\Namd\namd2\namdsample.</span><span class="sxs-lookup"><span data-stu-id="ccada-178">Extract hello tutorial files under \\\\CentOS66HN\Namd\namd2\namdsample.</span></span>
4. <span data-ttu-id="ccada-179">Ouvrez une fenêtre Windows PowerShell et exécutez hello suivant les commandes toomount hello dossier partagé sur les nœuds de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-179">Open a Windows PowerShell window and run hello following commands toomount hello shared folder on hello Linux nodes.</span></span>
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="ccada-180">Hello première commande crée un dossier nommé /namd2 sur tous les nœuds dans le groupe de LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-180">hello first command creates a folder named /namd2 on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="ccada-181">commande deuxième Hello monte hello partagé dossier //CentOS66HN/Namd/namd2 sur le dossier hello avec dir_mode et file_mode too777 d’ensemble de bits.</span><span class="sxs-lookup"><span data-stu-id="ccada-181">hello second command mounts hello shared folder //CentOS66HN/Namd/namd2 onto hello folder with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="ccada-182">Hello *nom d’utilisateur* et *mot de passe* Bonjour commande doit-elle être des informations d’identification de hello d’un utilisateur sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-182">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="ccada-183">Hello »\\`« symbole dans la deuxième commande de hello est un symbole d’échappement pour PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ccada-183">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="ccada-184">«\\`, « signifie hello », » (virgule) est une partie de la commande hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-184">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a><span data-ttu-id="ccada-185">Créer un toorun de script Bash un travail NAMD</span><span class="sxs-lookup"><span data-stu-id="ccada-185">Create a Bash script toorun a NAMD job</span></span>
<span data-ttu-id="ccada-186">Votre travail NAMD un *nodelist* de fichiers pour **charmrun** toodetermine hello quantité, nœuds toouse lors du démarrage du processus NAMD.</span><span class="sxs-lookup"><span data-stu-id="ccada-186">Your NAMD job needs a *nodelist* file for **charmrun** toodetermine hello number of nodes toouse when starting NAMD processes.</span></span> <span data-ttu-id="ccada-187">Vous utilisez un script d’interpréteur de commandes qui génère le fichier de liste de nœuds hello et exécute **charmrun** avec ce fichier de liste de nœuds.</span><span class="sxs-lookup"><span data-stu-id="ccada-187">You use a Bash script that generates hello nodelist file and runs **charmrun** with this nodelist file.</span></span> <span data-ttu-id="ccada-188">Vous pouvez ensuite envoyer une tâche NAMD dans HPC Cluster Manager qui appelle ce script.</span><span class="sxs-lookup"><span data-stu-id="ccada-188">You can then submit a NAMD job in HPC Cluster Manager that calls this script.</span></span>

<span data-ttu-id="ccada-189">À l’aide d’un éditeur de texte de votre choix, créez un script d’interpréteur de commandes dans le dossier de /namd2 hello contenant les fichiers de programme NAMD hello et nommez-le hpccharmrun.sh. Pour obtenir une rapide preuve de concept, copiez hello exemple hpccharmrun.sh de script fourni à fin hello de cet article, puis accédez trop[soumettre un travail NAMD](#submit-a-namd-job).</span><span class="sxs-lookup"><span data-stu-id="ccada-189">Using a text editor of your choice, create a Bash script in hello /namd2 folder containing hello NAMD program files and name it hpccharmrun.sh. For a quick proof of concept, copy hello example hpccharmrun.sh script provided at hello end of this article and go too[Submit a NAMD job](#submit-a-namd-job).</span></span>

> [!TIP]
> <span data-ttu-id="ccada-190">Enregistrez votre script en tant que fichier texte avec des fins de ligne Linux (LF uniquement, pas CR LF).</span><span class="sxs-lookup"><span data-stu-id="ccada-190">Save your script as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="ccada-191">Cela garantit qu’elle s’exécute correctement sur les nœuds de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-191">This ensures that it runs properly on hello Linux nodes.</span></span>
> 
> 

<span data-ttu-id="ccada-192">Voici les détails des actions du script Bash.</span><span class="sxs-lookup"><span data-stu-id="ccada-192">Following are details about what this bash script does.</span></span> 

1. <span data-ttu-id="ccada-193">Définir des variables.</span><span class="sxs-lookup"><span data-stu-id="ccada-193">Define some variables.</span></span>
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. <span data-ttu-id="ccada-194">Obtenir des informations sur les nœuds à partir de variables d’environnement hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-194">Get node information from hello environment variables.</span></span> <span data-ttu-id="ccada-195">$NODESCORES stocke une liste de mots de fractionnement à partir de $CCP_NODES_CORES.</span><span class="sxs-lookup"><span data-stu-id="ccada-195">$NODESCORES stores a list of split words from $CCP_NODES_CORES.</span></span> <span data-ttu-id="ccada-196">$COUNT n’hello taille $NODESCORES.</span><span class="sxs-lookup"><span data-stu-id="ccada-196">$COUNT is hello size of $NODESCORES.</span></span>
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   <span data-ttu-id="ccada-197">format Hello pour la variable CCP_NODES_CORES $ hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="ccada-197">hello format for hello $CCP_NODES_CORES variable is as follows:</span></span>
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   <span data-ttu-id="ccada-198">Cette variable répertorie le nombre total de hello de nœuds, les noms de nœud et nombre de cœurs sur chaque nœud qui sont alloués toohello travail.</span><span class="sxs-lookup"><span data-stu-id="ccada-198">This variable lists hello total number of nodes, node names, and number of cores on each node that are allocated toohello job.</span></span> <span data-ttu-id="ccada-199">Par exemple, si le travail de hello doit 10 cœurs toorun, valeur hello $CCP_NODES_CORES est similaire à :</span><span class="sxs-lookup"><span data-stu-id="ccada-199">For example, if hello job needs 10 cores toorun, hello value of $CCP_NODES_CORES is similar to:</span></span>
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. <span data-ttu-id="ccada-200">Si la variable CCP_NODES_CORES $ hello n’est pas définie, démarrez **charmrun** directement.</span><span class="sxs-lookup"><span data-stu-id="ccada-200">If hello $CCP_NODES_CORES variable is not set, start **charmrun** directly.</span></span> <span data-ttu-id="ccada-201">(Cela doit uniquement se produire lorsque vous exécutez ce script directement sur vos nœuds Linux.)</span><span class="sxs-lookup"><span data-stu-id="ccada-201">(This should only occur when you run this script directly on your Linux nodes.)</span></span>
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. <span data-ttu-id="ccada-202">Ou créer un fichier de liste de nœuds pour **charmrun**.</span><span class="sxs-lookup"><span data-stu-id="ccada-202">Or create a nodelist file for **charmrun**.</span></span>
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. <span data-ttu-id="ccada-203">Exécutez **charmrun** avec le fichier de liste de nœuds hello, obtenir son état de retour et supprimer le fichier de liste de nœuds hello à fin de hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-203">Run **charmrun** with hello nodelist file, get its return status, and remove hello nodelist file at hello end.</span></span>
   
   <span data-ttu-id="ccada-204">${CCP_NUMCPUS} est une autre variable d’environnement définie par le nœud principal HPC Pack de hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-204">${CCP_NUMCPUS} is another environment variable set by hello HPC Pack head node.</span></span> <span data-ttu-id="ccada-205">Il stocke le nombre hello de cœurs total alloué toothis travail.</span><span class="sxs-lookup"><span data-stu-id="ccada-205">It stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="ccada-206">Nous utiliserons pas toospecify hello sur différents processus à charmrun.</span><span class="sxs-lookup"><span data-stu-id="ccada-206">We use it toospecify hello number of processes for charmrun.</span></span>
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. <span data-ttu-id="ccada-207">Sortie avec hello **charmrun** état de retour.</span><span class="sxs-lookup"><span data-stu-id="ccada-207">Exit with hello **charmrun** return status.</span></span>
   
   ```
   exit ${RTNSTS}
   ```

<span data-ttu-id="ccada-208">Voici quelques informations hello dans fichier de liste de nœuds hello, le script de hello génère :</span><span class="sxs-lookup"><span data-stu-id="ccada-208">Following is hello information in hello nodelist file, which hello script generates:</span></span>

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

<span data-ttu-id="ccada-209">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="ccada-209">For example:</span></span>

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a><span data-ttu-id="ccada-210">Envoi d’une tâche NAMD</span><span class="sxs-lookup"><span data-stu-id="ccada-210">Submit a NAMD job</span></span>
<span data-ttu-id="ccada-211">Vous êtes maintenant prêt toosubmit un travail NAMD dans HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="ccada-211">Now you are ready toosubmit a NAMD job in HPC Cluster Manager.</span></span>

1. <span data-ttu-id="ccada-212">Se connecter tooyour nœud principal du cluster et démarrez le Gestionnaire du Cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="ccada-212">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="ccada-213">Dans **gestion des ressources**, assurez-vous que les nœuds de calcul Linux hello sont Bonjour **Online** état.</span><span class="sxs-lookup"><span data-stu-id="ccada-213">In **Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="ccada-214">Si ce n’est pas le cas, sélectionnez-les et cliquez sur **Mettre en ligne**.</span><span class="sxs-lookup"><span data-stu-id="ccada-214">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="ccada-215">Dans **Gestion des tâches**, cliquez sur **Nouveau travail**.</span><span class="sxs-lookup"><span data-stu-id="ccada-215">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="ccada-216">Entrez un nom pour la tâche, par exemple *hpccharmrun*.</span><span class="sxs-lookup"><span data-stu-id="ccada-216">Enter a name for job such as *hpccharmrun*.</span></span>
   
   ![Nouvelle tâche HPC][namd_job]
5. <span data-ttu-id="ccada-218">Sur hello **détails de la tâche** sous **des ressources de travail**, sélectionner le type de hello de ressource en tant que **nœud** et ensemble hello **Minimum** too3.</span><span class="sxs-lookup"><span data-stu-id="ccada-218">On hello **Job Details** page, under **Job Resources**, select hello type of resource as **Node** and set hello **Minimum** too3.</span></span> <span data-ttu-id="ccada-219">, nous exécutons les travaux hello sur trois nœuds Linux, et chaque nœud possède quatre cœurs.</span><span class="sxs-lookup"><span data-stu-id="ccada-219">, we run hello job on three Linux nodes and each node has four cores.</span></span>
   
   ![ressources de la tâche][job_resources]
6. <span data-ttu-id="ccada-221">Cliquez sur **modifier des tâches** dans hello du volet de navigation gauche, puis cliquez sur **ajouter** tooadd un travail de toohello de tâches.</span><span class="sxs-lookup"><span data-stu-id="ccada-221">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span>    
7. <span data-ttu-id="ccada-222">Sur hello **détails de la tâche et la Redirection des e/s** page hello du jeu de valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="ccada-222">On hello **Task Details and I/O Redirection** page, set hello following values:</span></span>
   
   * <span data-ttu-id="ccada-223">**Ligne de commande**-
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span><span class="sxs-lookup"><span data-stu-id="ccada-223">**Command line** -
`/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span></span>
     
     > [!TIP]
     > <span data-ttu-id="ccada-224">Hello ligne de commande précédente est une commande unique sans saut de ligne.</span><span class="sxs-lookup"><span data-stu-id="ccada-224">hello preceding command line is a single command without line breaks.</span></span> <span data-ttu-id="ccada-225">Elle encapsule tooappear sur plusieurs lignes sous **ligne de commande**.</span><span class="sxs-lookup"><span data-stu-id="ccada-225">It wraps tooappear on several lines under **Command line**.</span></span>
     > 
     > 
   * <span data-ttu-id="ccada-226">**Répertoire de travail** : /namd2</span><span class="sxs-lookup"><span data-stu-id="ccada-226">**Working directory** - /namd2</span></span>
   * <span data-ttu-id="ccada-227">**Minimum** : 3</span><span class="sxs-lookup"><span data-stu-id="ccada-227">**Minimum** - 3</span></span>
     
     ![Détails de la tâche][task_details]
     
     > [!NOTE]
     > <span data-ttu-id="ccada-229">Vous définissez répertoire de travail hello ici car **charmrun** tente toonavigate toohello même répertoire de travail sur chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="ccada-229">You set hello working directory here because **charmrun** tries toonavigate toohello same working directory on each node.</span></span> <span data-ttu-id="ccada-230">Si le répertoire de travail hello n’est pas défini, HPC Pack démarre la commande hello dans un dossier nommé de façon aléatoire créé sur l’un des nœuds de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-230">If hello working directory isn't set, HPC Pack starts hello command in a randomly named folder created on one of hello Linux nodes.</span></span> <span data-ttu-id="ccada-231">Cela provoque des autres nœuds hello l’erreur suivante sur hello : `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid ce problème, spécifiez un chemin d’accès du dossier qui est accessible par tous les nœuds en tant que répertoire de travail hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-231">This causes hello following error on hello other nodes: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid this problem, specify a folder path that can be accessed by all nodes as hello working directory.</span></span>
     > 
     > 
8. <span data-ttu-id="ccada-232">Cliquez sur **OK** puis cliquez sur **Submit** toorun ce travail.</span><span class="sxs-lookup"><span data-stu-id="ccada-232">Click **OK** and then click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="ccada-233">Par défaut, HPC Pack soumet le travail hello que votre compte d’utilisateur connecté actuel.</span><span class="sxs-lookup"><span data-stu-id="ccada-233">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="ccada-234">Une boîte de dialogue peut vous demander nom d’utilisateur tooenter hello et le mot de passe après avoir cliqué sur **Submit**.</span><span class="sxs-lookup"><span data-stu-id="ccada-234">A dialog box might prompt you tooenter hello user name and password after you click **Submit**.</span></span>
   
   ![Informations d’identification de la tâche][creds]
   
   <span data-ttu-id="ccada-236">Sous certaines conditions, HPC Pack mémorise les informations d’utilisateur hello d’entrée avant et de ne plus afficher cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ccada-236">Under some conditions, HPC Pack remembers hello user information you input before and doesn't show this dialog box.</span></span> <span data-ttu-id="ccada-237">toomake HPC Pack afficher à nouveau, entrez hello commande à l’invite de commande suivante et l’envoi de la tâche de hello puis.</span><span class="sxs-lookup"><span data-stu-id="ccada-237">toomake HPC Pack show it again, enter hello following command at a Command Prompt and then submit hello job.</span></span>
   
   ```command
   hpccred delcreds
   ```
9. <span data-ttu-id="ccada-238">travail de Hello prend plusieurs minutes toofinish.</span><span class="sxs-lookup"><span data-stu-id="ccada-238">hello job takes several minutes toofinish.</span></span>
10. <span data-ttu-id="ccada-239">Rechercher le journal des travaux hello à \\ <headnodeName>\Namd\namd2\namd2_hpccharmrun.log et hello dans les fichiers de sortie \\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span><span class="sxs-lookup"><span data-stu-id="ccada-239">Find hello job log at \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log and hello output files in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span></span>
11. <span data-ttu-id="ccada-240">Vous pouvez également démarrer VDM tooview vos résultats de la tâche.</span><span class="sxs-lookup"><span data-stu-id="ccada-240">Optionally, start VMD tooview your job results.</span></span> <span data-ttu-id="ccada-241">étapes de Hello pour visualiser des fichiers de sortie hello NAMD (dans ce cas, une molecule de PROTEINE UBIQUITINE dans une sphère d’eau) sont abordée dans cet article hello.</span><span class="sxs-lookup"><span data-stu-id="ccada-241">hello steps for visualizing hello NAMD output files (in this case, a ubiquitin protein molecule in a water sphere) are beyond hello scope of this article.</span></span> <span data-ttu-id="ccada-242">Voir [Didacticiel NAMD](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="ccada-242">See [NAMD Tutorial](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) for details.</span></span>
    
    ![Résultats de la tâche][vmd_view]

## <a name="sample-files"></a><span data-ttu-id="ccada-244">Exemple de fichiers</span><span class="sxs-lookup"><span data-stu-id="ccada-244">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="ccada-245">Exemple de fichier de configuration XML pour le déploiement de clusters par script PowerShell</span><span class="sxs-lookup"><span data-stu-id="ccada-245">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>    
```

### <a name="sample-credxml-file"></a><span data-ttu-id="ccada-246">Exemple de fichier cred.xml</span><span class="sxs-lookup"><span data-stu-id="ccada-246">Sample cred.xml file</span></span>
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

### <a name="sample-hpccharmrunsh-script"></a><span data-ttu-id="ccada-247">Exemple de script hpccharmrun.sh</span><span class="sxs-lookup"><span data-stu-id="ccada-247">Sample hpccharmrun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
