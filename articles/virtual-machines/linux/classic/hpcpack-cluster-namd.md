---
title: NAMD avec Microsoft HPC Pack sur des machines virtuelles Linux | Microsoft Docs
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
ms.openlocfilehash: e31845f3d7aa08357b0e8a1b3b77d97302442ac3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a><span data-ttu-id="d663f-103">Exécution de NAMD avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="d663f-103">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>
<span data-ttu-id="d663f-104">Cet article vous montre comment exécuter une charge de travail HPC (calcul haute performance) Linux sur des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="d663f-104">This article shows you one way to run a Linux high-performance computing (HPC) workload on Azure virtual machines.</span></span> <span data-ttu-id="d663f-105">Vous allez découvrir comment configurer un cluster [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) sur Azure avec des nœuds de calcul Linux et exécuter une simulation [NAMD](http://www.ks.uiuc.edu/Research/namd/) pour calculer et visualiser la structure d’un système biomoléculaire étendu.</span><span class="sxs-lookup"><span data-stu-id="d663f-105">Here, you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster on Azure with Linux compute nodes and run a [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulation to calculate and visualize the structure of a large biomolecular system.</span></span>  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* <span data-ttu-id="d663f-106">**NAMD** (programme Nanoscale Molecular Dynamics) est un package de dynamique moléculaire parallèle, conçu pour la simulation hautes performances des systèmes biomoléculaires étendus contenant jusqu’à plusieurs millions d’atomes.</span><span class="sxs-lookup"><span data-stu-id="d663f-106">**NAMD** (for Nanoscale Molecular Dynamics program) is a parallel molecular dynamics package designed for high-performance simulation of large biomolecular systems containing up to millions of atoms.</span></span> <span data-ttu-id="d663f-107">Ces systèmes sont par exemple les virus, les structures de cellule et les grandes protéines.</span><span class="sxs-lookup"><span data-stu-id="d663f-107">Examples of these systems include viruses, cell structures, and large proteins.</span></span> <span data-ttu-id="d663f-108">NAMD s’adapte à des centaines de cœurs pour les simulations classiques et à plus de 500 000 cœurs pour les simulations les plus étendues.</span><span class="sxs-lookup"><span data-stu-id="d663f-108">NAMD scales to hundreds of cores for typical simulations and to more than 500,000 cores for the largest simulations.</span></span>
* <span data-ttu-id="d663f-109">**Microsoft HPC Pack** fournit des fonctionnalités permettant d’exécuter un éventail d’applications HPC à grande échelle et parallèles dans des clusters d’ordinateurs locaux ou de machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="d663f-109">**Microsoft HPC Pack** provides features to run large-scale HPC and parallel applications in clusters of on-premises computers or Azure virtual machines.</span></span> <span data-ttu-id="d663f-110">Développée à l’origine comme solution pour les charges de travail Windows HPC, HPC Pack prend désormais en charge l’exécution d’applications HPC Linux sur les machines virtuelles de nœuds de calcul Linux déployées dans un cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="d663f-110">Originally developed as a solution for Windows HPC workloads, HPC Pack now supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="d663f-111">Consultez la présentation [Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md) .</span><span class="sxs-lookup"><span data-stu-id="d663f-111">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction.</span></span>

<span data-ttu-id="d663f-112">Pour d’autres options d’exécution des charges de travail HPC Linux dans Azure, voir [Ressources techniques pour Batch et HPC (calcul haute performance)](../../../batch/batch-hpc-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="d663f-112">For other options to run Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/batch-hpc-solutions.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d663f-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d663f-113">Prerequisites</span></span>
* <span data-ttu-id="d663f-114">**Cluster HPC Pack avec nœuds de calcul Linux** : déployez un cluster HPC Pack avec des nœuds de calcul Linux dans Azure à l’aide d’un [modèle Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) ou d’un [script Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="d663f-114">**HPC Pack cluster with Linux compute nodes** - Deploy an HPC Pack cluster with Linux compute nodes on Azure using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="d663f-115">Consultez la configuration requise et la procédure pour chaque option sur la page [Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md) .</span><span class="sxs-lookup"><span data-stu-id="d663f-115">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for the prerequisites and steps for either option.</span></span> <span data-ttu-id="d663f-116">Si vous choisissez l’option de déploiement de script PowerShell, voir l’exemple de fichier de configuration dans les fichiers d’exemple à la fin de cet article.</span><span class="sxs-lookup"><span data-stu-id="d663f-116">If you choose the PowerShell script deployment option, see the sample configuration file in the sample files at the end of this article.</span></span> <span data-ttu-id="d663f-117">Ce fichier configure un cluster HPC Pack basé sur Azure comportant un nœud principal Windows Server 2012 R2 et quatre nœuds de calcul de grande taille CentOS 6.6.</span><span class="sxs-lookup"><span data-stu-id="d663f-117">This file configures an Azure-based HPC Pack cluster consisting of a Windows Server 2012 R2 head node and four size Large CentOS 6.6 compute nodes.</span></span> <span data-ttu-id="d663f-118">Personnalisez ce fichier comme il convient pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="d663f-118">Customize this file as needed for your environment.</span></span>
* <span data-ttu-id="d663f-119">**Logiciel NAMD et fichiers du didacticiel** : téléchargez le logiciel NAMD pour Linux à partir du site [NAMD](http://www.ks.uiuc.edu/Research/namd/) (inscription obligatoire).</span><span class="sxs-lookup"><span data-stu-id="d663f-119">**NAMD software and tutorial files** - Download NAMD software for Linux from the [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registration required).</span></span> <span data-ttu-id="d663f-120">Cet article est basé sur la version 2.10 de NAMD et utilise l’archive [Linux-x86_64 (Intel/AMD 64 bits avec Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310).</span><span class="sxs-lookup"><span data-stu-id="d663f-120">This article is based on NAMD version 2.10, and uses the [Linux-x86_64 (64-bit Intel/AMD with Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span></span> <span data-ttu-id="d663f-121">Téléchargez également les [fichiers du didacticiel NAMD](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span><span class="sxs-lookup"><span data-stu-id="d663f-121">Also download the [NAMD tutorial files](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span></span> <span data-ttu-id="d663f-122">Les fichiers ont l’extension .tar et vous devez utiliser un outil Windows pour les extraire sur le nœud principal du cluster.</span><span class="sxs-lookup"><span data-stu-id="d663f-122">The downloads are .tar files, and you need a Windows tool to extract the files on the cluster head node.</span></span> <span data-ttu-id="d663f-123">Pour extraire les fichiers, suivez les instructions données plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="d663f-123">To extract the files, follow the instructions later in this article.</span></span> 
* <span data-ttu-id="d663f-124">**VMD** (facultatif) : pour afficher les résultats de votre tâche NAMD, téléchargez et installez le programme de visualisation moléculaire [VMD](http://www.ks.uiuc.edu/Research/vmd/) sur un ordinateur de votre choix.</span><span class="sxs-lookup"><span data-stu-id="d663f-124">**VMD** (optional) - To see the results of your NAMD job, download and install the molecular visualization program [VMD](http://www.ks.uiuc.edu/Research/vmd/) on a computer of your choice.</span></span> <span data-ttu-id="d663f-125">La version actuelle est 1.9.2.</span><span class="sxs-lookup"><span data-stu-id="d663f-125">The current version is 1.9.2.</span></span> <span data-ttu-id="d663f-126">Consultez le site de téléchargement de VMD pour commencer.</span><span class="sxs-lookup"><span data-stu-id="d663f-126">See the VMD download site to get started.</span></span>  

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="d663f-127">Configuration de l’approbation mutuelle entre les nœuds de calcul</span><span class="sxs-lookup"><span data-stu-id="d663f-127">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="d663f-128">L’exécution d’une tâche de nœuds croisés sur plusieurs nœuds Linux requiert une approbation mutuelle entre les nœuds (par **rsh** ou **ssh**).</span><span class="sxs-lookup"><span data-stu-id="d663f-128">Running a cross-node job on multiple Linux nodes requires the nodes to trust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="d663f-129">Lorsque vous créez le cluster HPC Pack avec le script de déploiement IaaS Microsoft HPC Pack, le script définit automatiquement l’approbation mutuelle permanente pour le compte administrateur que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="d663f-129">When you create the HPC Pack cluster with the Microsoft HPC Pack IaaS deployment script, the script automatically sets up permanent mutual trust for the administrator account you specify.</span></span> <span data-ttu-id="d663f-130">Pour les utilisateurs non administrateurs que vous créez dans le domaine du cluster, vous devez configurer l’approbation mutuelle temporaire entre les nœuds lorsqu’une tâche leur est allouée.</span><span class="sxs-lookup"><span data-stu-id="d663f-130">For non-administrator users you create in the cluster's domain, you have to set up temporary mutual trust among the nodes when a job is allocated to them.</span></span> <span data-ttu-id="d663f-131">Puis, détruisez la relation une fois la tâche terminée.</span><span class="sxs-lookup"><span data-stu-id="d663f-131">Then, destroy the relationship after the job is complete.</span></span> <span data-ttu-id="d663f-132">Pour ce faire, pour chaque utilisateur, fournissez une paire de clés RSA au cluster que HPC Pack utilise pour établir la relation d’approbation.</span><span class="sxs-lookup"><span data-stu-id="d663f-132">To do this for each user, provide an RSA key pair to the cluster which HPC Pack uses to establish the trust relationship.</span></span> <span data-ttu-id="d663f-133">Instructions ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d663f-133">Instructions follow.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="d663f-134">Génération d’une paire de clés RSA</span><span class="sxs-lookup"><span data-stu-id="d663f-134">Generate an RSA key pair</span></span>
<span data-ttu-id="d663f-135">Générer une paire de clés RSA contenant une clé publique et une clé privée est facile : il vous suffit d’exécuter la commande Linux **ssh-keygen** .</span><span class="sxs-lookup"><span data-stu-id="d663f-135">It's easy to generate an RSA key pair, which contains a public key and a private key, by running the Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="d663f-136">Ouvrez une session sur un ordinateur Linux.</span><span class="sxs-lookup"><span data-stu-id="d663f-136">Log on to a Linux computer.</span></span>
2. <span data-ttu-id="d663f-137">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d663f-137">Run the following command:</span></span>
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="d663f-138">Appuyez sur **Entrée** pour utiliser les paramètres par défaut jusqu'à ce que la commande soit terminée.</span><span class="sxs-lookup"><span data-stu-id="d663f-138">Press **Enter** to use the default settings until the command is completed.</span></span> <span data-ttu-id="d663f-139">N'entrez pas de phrase secrète ici ; à l'invite de mot de passe, appuyez simplement sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="d663f-139">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Génération d’une paire de clés RSA][keygen]
3. <span data-ttu-id="d663f-141">Remplacez le répertoire par le répertoire ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="d663f-141">Change directory to the ~/.ssh directory.</span></span> <span data-ttu-id="d663f-142">La clé privée est stockée dans id_rsa et la clé publique dans id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="d663f-142">The private key is stored in id_rsa and the public key in id_rsa.pub.</span></span>
   
   ![Clés publiques et privées][keys]

### <a name="add-the-key-pair-to-the-hpc-pack-cluster"></a><span data-ttu-id="d663f-144">Ajout de la paire de clés au cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="d663f-144">Add the key pair to the HPC Pack cluster</span></span>
1. <span data-ttu-id="d663f-145">[Connectez-vous via le Bureau à distance](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) à la machine virtuelle du nœud principal en utilisant les informations d’identification du domaine que vous avez fournies au moment de déployer le cluster (par exemple, hpc\admin_cluster).</span><span class="sxs-lookup"><span data-stu-id="d663f-145">[Connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to the head node VM using the domain credentials you provided when you deployed the cluster (for example, hpc\clusteradmin).</span></span> <span data-ttu-id="d663f-146">Le cluster est géré à partir du nœud principal.</span><span class="sxs-lookup"><span data-stu-id="d663f-146">You manage the cluster from the head node.</span></span>
2. <span data-ttu-id="d663f-147">Utilisez les procédures standard Windows Server pour créer un compte d’utilisateur de domaine dans le domaine Active Directory du cluster.</span><span class="sxs-lookup"><span data-stu-id="d663f-147">Use standard Windows Server procedures to create a domain user account in the cluster's Active Directory domain.</span></span> <span data-ttu-id="d663f-148">Par exemple, utilisez l’outil Utilisateurs et ordinateurs Active Directory sur le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="d663f-148">For example, use the Active Directory User and Computers tool on the head node.</span></span> <span data-ttu-id="d663f-149">Les exemples de cet article supposent que vous créez un utilisateur de domaine nommé hpcuser dans le domaine hpclab (hpclab\hpcuser).</span><span class="sxs-lookup"><span data-stu-id="d663f-149">The examples in this article assume you create a domain user named hpcuser in the hpclab domain (hpclab\hpcuser).</span></span>
3. <span data-ttu-id="d663f-150">Ajoutez l’utilisateur de domaine au cluster HPC Pack en tant qu’utilisateur de cluster.</span><span class="sxs-lookup"><span data-stu-id="d663f-150">Add the domain user to the HPC Pack cluster as a cluster user.</span></span> <span data-ttu-id="d663f-151">Pour obtenir des instructions, consultez [Ajouter ou supprimer des utilisateurs du cluster](https://technet.microsoft.com/library/ff919330.aspx).</span><span class="sxs-lookup"><span data-stu-id="d663f-151">For instructions, see [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).</span></span>
4. <span data-ttu-id="d663f-152">Créez un fichier nommé C:\cred.xml et copiez-y les données de clé RSA.</span><span class="sxs-lookup"><span data-stu-id="d663f-152">Create a file named C:\cred.xml and copy the RSA key data into it.</span></span> <span data-ttu-id="d663f-153">Vous trouverez un exemple dans les exemples de fichiers à la fin de cet article.</span><span class="sxs-lookup"><span data-stu-id="d663f-153">You can find an example in the sample files at the end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy the contents of private key here</PrivateKey>
     <PublicKey>Copy the contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. <span data-ttu-id="d663f-154">Ouvrez une invite de commande et entrez la commande suivante pour définir les données d’informations d’identification du compte hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="d663f-154">Open a Command Prompt and enter the following command to set the credentials data for the hpclab\hpcuser account.</span></span> <span data-ttu-id="d663f-155">Utilisez le paramètre **extendeddata** pour transmettre le nom du fichier C:\cred.xml que vous avez créé pour les données de clé.</span><span class="sxs-lookup"><span data-stu-id="d663f-155">You use the **extendeddata** parameter to pass the name of the C:\cred.xml file you created for the key data.</span></span>
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="d663f-156">Cette commande se termine correctement sans sortie.</span><span class="sxs-lookup"><span data-stu-id="d663f-156">This command completes successfully without output.</span></span> <span data-ttu-id="d663f-157">Après avoir défini les informations d’identification pour les comptes d’utilisateurs dont vous avez besoin pour exécuter des tâches, stockez le fichier cred.xml à un emplacement sécurisé ou supprimez-le.</span><span class="sxs-lookup"><span data-stu-id="d663f-157">After setting the credentials for the user accounts you need to run jobs, store the cred.xml file in a secure location, or delete it.</span></span>
6. <span data-ttu-id="d663f-158">Si vous avez généré la paire de clés RSA sur l’un de vos nœuds Linux, pensez à supprimer les clés une fois que vous avez terminé de les utiliser.</span><span class="sxs-lookup"><span data-stu-id="d663f-158">If you generated the RSA key pair on one of your Linux nodes, remember to delete the keys after you finish using them.</span></span> <span data-ttu-id="d663f-159">HPC Pack ne configure pas l’approbation mutuelle s’il trouve des fichiers id_rsa ou id_rsa.pub existants.</span><span class="sxs-lookup"><span data-stu-id="d663f-159">HPC Pack does not set up mutual trust if it finds an existing id_rsa file or id_rsa.pub file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d663f-160">Nous déconseillons d’exécuter une tâche Linux en tant qu’administrateur de cluster sur un cluster partagé, car une tâche envoyée par un administrateur s’exécute sous le compte racine sur les nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="d663f-160">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under the root account on the Linux nodes.</span></span> <span data-ttu-id="d663f-161">Une tâche envoyée par un utilisateur non-administrateur s’exécute sous un compte utilisateur Linux local du même nom que l’utilisateur de la tâche.</span><span class="sxs-lookup"><span data-stu-id="d663f-161">A job submitted by a non-administrator user runs under a local Linux user account with the same name as the job user.</span></span> <span data-ttu-id="d663f-162">Dans ce cas, HPC Pack définit une approbation mutuelle pour cet utilisateur Linux sur tous les nœuds alloués à la tâche.</span><span class="sxs-lookup"><span data-stu-id="d663f-162">In this case, HPC Pack sets up mutual trust for this Linux user across all the nodes allocated to the job.</span></span> <span data-ttu-id="d663f-163">Vous pouvez configurer l’utilisateur Linux manuellement sur les nœuds Linux avant d’exécuter la tâche, ou bien HPC Pack crée automatiquement l’utilisateur lorsque la tâche est envoyée.</span><span class="sxs-lookup"><span data-stu-id="d663f-163">You can set up the Linux user manually on the Linux nodes before running the job, or HPC Pack creates the user automatically when the job is submitted.</span></span> <span data-ttu-id="d663f-164">Si HPC Pack crée l’utilisateur, il se charge de le supprimer une fois la tâche terminée.</span><span class="sxs-lookup"><span data-stu-id="d663f-164">If HPC Pack creates the user, HPC Pack deletes it after the job completes.</span></span> <span data-ttu-id="d663f-165">Pour réduire la menace de sécurité, les clés sont supprimées après l’achèvement de la tâche sur les nœuds.</span><span class="sxs-lookup"><span data-stu-id="d663f-165">To reduce security threat, the keys are removed after the job completes on the nodes.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="d663f-166">Configuration d’un partage de fichiers pour les nœuds Linux</span><span class="sxs-lookup"><span data-stu-id="d663f-166">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="d663f-167">À présent, configurez un partage de fichiers SMB et montez le dossier partagé sur tous les nœuds Linux pour leur permettre d’accéder aux fichiers NAMD avec un chemin d’accès commun.</span><span class="sxs-lookup"><span data-stu-id="d663f-167">Now set up an SMB file share, and mount the shared folder on all Linux nodes to allow the Linux nodes to access NAMD files with a common path.</span></span> <span data-ttu-id="d663f-168">Les étapes de montage d’un dossier partagé sur le nœud principal sont décrites ci-après.</span><span class="sxs-lookup"><span data-stu-id="d663f-168">Following are steps to mount a shared folder on the head node.</span></span> <span data-ttu-id="d663f-169">Un partage est recommandé pour les distributions comme CentOS 6.6 qui ne prennent pas en charge Azure File Service pour le moment.</span><span class="sxs-lookup"><span data-stu-id="d663f-169">A share is recommended for distributions such as CentOS 6.6 that currently don’t support the Azure File service.</span></span> <span data-ttu-id="d663f-170">Si vos nœuds Linux prennent en charge un partage de fichiers Azure, consultez [Utilisation du stockage de fichiers Azure avec Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d663f-170">If your Linux nodes support an Azure File share, see [How to use Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="d663f-171">Pour des options supplémentaires de partage des fichiers avec HPC Pack, consultez [Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="d663f-171">For additional file sharing options with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="d663f-172">Créez un dossier sur le nœud principal et partagez-le avec Tout le monde en définissant des privilèges de lecture/écriture.</span><span class="sxs-lookup"><span data-stu-id="d663f-172">Create a folder on the head node, and share it to Everyone by setting Read/Write privileges.</span></span> <span data-ttu-id="d663f-173">Dans cet exemple, \\\\CentOS66HN\Namd est le nom du dossier (où CentOS66HN est le nom d’hôte du nœud principal).</span><span class="sxs-lookup"><span data-stu-id="d663f-173">In this example, \\\\CentOS66HN\Namd is the name of the folder, where CentOS66HN is the host name of the head node.</span></span>
2. <span data-ttu-id="d663f-174">Créez un sous-dossier nommé namd2 dans le dossier partagé.</span><span class="sxs-lookup"><span data-stu-id="d663f-174">Create a subfolder named namd2 in the shared folder.</span></span> <span data-ttu-id="d663f-175">Créez un autre sous-dossier nommé namdsample dans namd2.</span><span class="sxs-lookup"><span data-stu-id="d663f-175">In namd2, create another subfolder named namdsample.</span></span>
3. <span data-ttu-id="d663f-176">Extrayez les fichiers NAMD dans le dossier en utilisant une version Windows de **tar** ou un autre utilitaire Windows qui fonctionne sur les archives .tar.</span><span class="sxs-lookup"><span data-stu-id="d663f-176">Extract the NAMD files in the folder by using a Windows version of **tar** or another Windows utility that operates on .tar archives.</span></span> 
   
   * <span data-ttu-id="d663f-177">Extrayez l’archive tar NAMD dans \\\\CentOS66HN\Namd\namd2.</span><span class="sxs-lookup"><span data-stu-id="d663f-177">Extract the NAMD tar archive to \\\\CentOS66HN\Namd\namd2.</span></span>
   * <span data-ttu-id="d663f-178">Extrayez les fichiers du didacticiel dans \\\\CentOS66HN\Namd\namd2\namdsample.</span><span class="sxs-lookup"><span data-stu-id="d663f-178">Extract the tutorial files under \\\\CentOS66HN\Namd\namd2\namdsample.</span></span>
4. <span data-ttu-id="d663f-179">Ouvrez une fenêtre Windows PowerShell et exécutez les commandes suivantes pour monter le dossier partagé sur les nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="d663f-179">Open a Windows PowerShell window and run the following commands to mount the shared folder on the Linux nodes.</span></span>
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="d663f-180">La première commande crée un dossier nommé /namd2 sur tous les nœuds dans le groupe LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="d663f-180">The first command creates a folder named /namd2 on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="d663f-181">La deuxième commande monte le dossier partagé //CentOS66HN/Namd/namd2 sur le dossier avec les bits dir_mode et file_mode définis sur 777.</span><span class="sxs-lookup"><span data-stu-id="d663f-181">The second command mounts the shared folder //CentOS66HN/Namd/namd2 onto the folder with dir_mode and file_mode bits set to 777.</span></span> <span data-ttu-id="d663f-182">Les valeurs *username* et *password* dans la commande doivent être les informations d’identification d’un utilisateur du nœud principal.</span><span class="sxs-lookup"><span data-stu-id="d663f-182">The *username* and *password* in the command should be the credentials of a user on the head node.</span></span>

> [!NOTE]
> <span data-ttu-id="d663f-183">Le symbole « \\` » dans la deuxième commande est un symbole de caractère d’échappement pour PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d663f-183">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="d663f-184">« \\`, » signifie que « , » (une virgule) fait partie de la commande.</span><span class="sxs-lookup"><span data-stu-id="d663f-184">“\\`,” means the “,” (comma character) is a part of the command.</span></span>
> 
> 

## <a name="create-a-bash-script-to-run-a-namd-job"></a><span data-ttu-id="d663f-185">Créer un script Bash pour exécuter une tâche NAMD</span><span class="sxs-lookup"><span data-stu-id="d663f-185">Create a Bash script to run a NAMD job</span></span>
<span data-ttu-id="d663f-186">Votre tâche NAMD requiert un fichier *nodelist* pour que **charmrun** détermine le nombre de nœuds à utiliser lors du démarrage des processus NAMD.</span><span class="sxs-lookup"><span data-stu-id="d663f-186">Your NAMD job needs a *nodelist* file for **charmrun** to determine the number of nodes to use when starting NAMD processes.</span></span> <span data-ttu-id="d663f-187">Vous utilisez un script Bash qui génère le fichier nodelist et exécute **charmrun** avec ce fichier.</span><span class="sxs-lookup"><span data-stu-id="d663f-187">You use a Bash script that generates the nodelist file and runs **charmrun** with this nodelist file.</span></span> <span data-ttu-id="d663f-188">Vous pouvez ensuite envoyer une tâche NAMD dans HPC Cluster Manager qui appelle ce script.</span><span class="sxs-lookup"><span data-stu-id="d663f-188">You can then submit a NAMD job in HPC Cluster Manager that calls this script.</span></span>

<span data-ttu-id="d663f-189">À l’aide de l’éditeur de texte de votre choix, créez un script Bash dans le dossier /namd2 contenant les fichiers du programme NAMD et nommez-le hpccharmrun.sh. Pour une démonstration rapide du concept, copiez l’exemple de script hpccharmrun.sh fourni à la fin de cet article et accédez à [Envoi d’une tâche NAMD](#submit-a-namd-job).</span><span class="sxs-lookup"><span data-stu-id="d663f-189">Using a text editor of your choice, create a Bash script in the /namd2 folder containing the NAMD program files and name it hpccharmrun.sh. For a quick proof of concept, copy the example hpccharmrun.sh script provided at the end of this article and go to [Submit a NAMD job](#submit-a-namd-job).</span></span>

> [!TIP]
> <span data-ttu-id="d663f-190">Enregistrez votre script en tant que fichier texte avec des fins de ligne Linux (LF uniquement, pas CR LF).</span><span class="sxs-lookup"><span data-stu-id="d663f-190">Save your script as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="d663f-191">Cela garantit qu’il s’exécute correctement sur les nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="d663f-191">This ensures that it runs properly on the Linux nodes.</span></span>
> 
> 

<span data-ttu-id="d663f-192">Voici les détails des actions du script Bash.</span><span class="sxs-lookup"><span data-stu-id="d663f-192">Following are details about what this bash script does.</span></span> 

1. <span data-ttu-id="d663f-193">Définir des variables.</span><span class="sxs-lookup"><span data-stu-id="d663f-193">Define some variables.</span></span>
   
   ```bash
   #!/bin/bash
   
   # The path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. <span data-ttu-id="d663f-194">Obtenir des informations de nœud dans les variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="d663f-194">Get node information from the environment variables.</span></span> <span data-ttu-id="d663f-195">$NODESCORES stocke une liste de mots de fractionnement à partir de $CCP_NODES_CORES.</span><span class="sxs-lookup"><span data-stu-id="d663f-195">$NODESCORES stores a list of split words from $CCP_NODES_CORES.</span></span> <span data-ttu-id="d663f-196">$COUNT représente la taille de $NODESCORES.</span><span class="sxs-lookup"><span data-stu-id="d663f-196">$COUNT is the size of $NODESCORES.</span></span>
   
   ```
   # Get node information from the environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   <span data-ttu-id="d663f-197">Le format de la variable $CCP_NODES_CORES est le suivant :</span><span class="sxs-lookup"><span data-stu-id="d663f-197">The format for the $CCP_NODES_CORES variable is as follows:</span></span>
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   <span data-ttu-id="d663f-198">Cette variable répertorie le nombre total de nœuds, les noms des nœuds et le nombre de cœurs sur chaque nœud qui sont alloués à la tâche.</span><span class="sxs-lookup"><span data-stu-id="d663f-198">This variable lists the total number of nodes, node names, and number of cores on each node that are allocated to the job.</span></span> <span data-ttu-id="d663f-199">Par exemple, si la tâche requiert 10 cœurs pour s’exécuter, la valeur de $CCP_NODES_CORES ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="d663f-199">For example, if the job needs 10 cores to run, the value of $CCP_NODES_CORES is similar to:</span></span>
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. <span data-ttu-id="d663f-200">Si la variable $CCP_NODES_CORES n’est pas définie, lancer **charmrun** directement.</span><span class="sxs-lookup"><span data-stu-id="d663f-200">If the $CCP_NODES_CORES variable is not set, start **charmrun** directly.</span></span> <span data-ttu-id="d663f-201">(Cela doit uniquement se produire lorsque vous exécutez ce script directement sur vos nœuds Linux.)</span><span class="sxs-lookup"><span data-stu-id="d663f-201">(This should only occur when you run this script directly on your Linux nodes.)</span></span>
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. <span data-ttu-id="d663f-202">Ou créer un fichier de liste de nœuds pour **charmrun**.</span><span class="sxs-lookup"><span data-stu-id="d663f-202">Or create a nodelist file for **charmrun**.</span></span>
   
   ```
   else
     # Create the nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write the head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into the nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. <span data-ttu-id="d663f-203">Exécuter **charmrun** avec le fichier de liste de nœuds, obtenir son état de retour et supprimer le fichier de liste de nœuds à la fin.</span><span class="sxs-lookup"><span data-stu-id="d663f-203">Run **charmrun** with the nodelist file, get its return status, and remove the nodelist file at the end.</span></span>
   
   <span data-ttu-id="d663f-204">${CCP_NUMCPUS} est une autre variable d’environnement définie par le nœud principal HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="d663f-204">${CCP_NUMCPUS} is another environment variable set by the HPC Pack head node.</span></span> <span data-ttu-id="d663f-205">Elle stocke le nombre total de cœurs alloués à cette tâche.</span><span class="sxs-lookup"><span data-stu-id="d663f-205">It stores the number of total cores allocated to this job.</span></span> <span data-ttu-id="d663f-206">Nous l’utilisons pour spécifier le nombre de processus pour charmrun.</span><span class="sxs-lookup"><span data-stu-id="d663f-206">We use it to specify the number of processes for charmrun.</span></span>
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. <span data-ttu-id="d663f-207">Quitter avec l'état de retour **charmrun** .</span><span class="sxs-lookup"><span data-stu-id="d663f-207">Exit with the **charmrun** return status.</span></span>
   
   ```
   exit ${RTNSTS}
   ```

<span data-ttu-id="d663f-208">Voici les informations contenues dans le fichier de liste de nœuds généré par le script :</span><span class="sxs-lookup"><span data-stu-id="d663f-208">Following is the information in the nodelist file, which the script generates:</span></span>

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

<span data-ttu-id="d663f-209">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d663f-209">For example:</span></span>

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a><span data-ttu-id="d663f-210">Envoi d’une tâche NAMD</span><span class="sxs-lookup"><span data-stu-id="d663f-210">Submit a NAMD job</span></span>
<span data-ttu-id="d663f-211">Vous êtes maintenant prêt à envoyer une tâche NAMD dans HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="d663f-211">Now you are ready to submit a NAMD job in HPC Cluster Manager.</span></span>

1. <span data-ttu-id="d663f-212">Connectez-vous à votre nœud principal de cluster et démarrez HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="d663f-212">Connect to your cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="d663f-213">Dans **Gestion des ressources**, assurez-vous que les nœuds de calcul Linux sont à l’état **En ligne**.</span><span class="sxs-lookup"><span data-stu-id="d663f-213">In **Resource Management**, ensure that the Linux compute nodes are in the **Online** state.</span></span> <span data-ttu-id="d663f-214">Si ce n’est pas le cas, sélectionnez-les et cliquez sur **Mettre en ligne**.</span><span class="sxs-lookup"><span data-stu-id="d663f-214">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="d663f-215">Dans **Gestion des tâches**, cliquez sur **Nouveau travail**.</span><span class="sxs-lookup"><span data-stu-id="d663f-215">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="d663f-216">Entrez un nom pour la tâche, par exemple *hpccharmrun*.</span><span class="sxs-lookup"><span data-stu-id="d663f-216">Enter a name for job such as *hpccharmrun*.</span></span>
   
   ![Nouvelle tâche HPC][namd_job]
5. <span data-ttu-id="d663f-218">Sur la page **Détails de la tâche**, sous **Ressources de la tâche**, sélectionnez le type de ressource **Nœud** et définissez la valeur **Minimum** sur 3.</span><span class="sxs-lookup"><span data-stu-id="d663f-218">On the **Job Details** page, under **Job Resources**, select the type of resource as **Node** and set the **Minimum** to 3.</span></span> <span data-ttu-id="d663f-219">, nous exécutons la tâche sur trois nœuds Linux et chaque nœud comporte quatre cœurs.</span><span class="sxs-lookup"><span data-stu-id="d663f-219">, we run the job on three Linux nodes and each node has four cores.</span></span>
   
   ![ressources de la tâche][job_resources]
6. <span data-ttu-id="d663f-221">Cliquez sur **Modifier des tâches** dans le volet de navigation gauche, puis sur **Ajouter** pour ajouter une tâche au travail.</span><span class="sxs-lookup"><span data-stu-id="d663f-221">Click **Edit Tasks** in the left navigation, and then click **Add** to add a task to the job.</span></span>    
7. <span data-ttu-id="d663f-222">Sur la page **Détails de la tâche et redirection d’E/S** , définissez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="d663f-222">On the **Task Details and I/O Redirection** page, set the following values:</span></span>
   
   * <span data-ttu-id="d663f-223">**Ligne de commande** -
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span><span class="sxs-lookup"><span data-stu-id="d663f-223">**Command line** -
`/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span></span>
     
     > [!TIP]
     > <span data-ttu-id="d663f-224">La ligne de commande précédente est une commande unique sans saut de ligne.</span><span class="sxs-lookup"><span data-stu-id="d663f-224">The preceding command line is a single command without line breaks.</span></span> <span data-ttu-id="d663f-225">Un retour à la ligne est appliqué pour qu’elle apparaisse sur plusieurs lignes sous **Ligne de commande**.</span><span class="sxs-lookup"><span data-stu-id="d663f-225">It wraps to appear on several lines under **Command line**.</span></span>
     > 
     > 
   * <span data-ttu-id="d663f-226">**Répertoire de travail** : /namd2</span><span class="sxs-lookup"><span data-stu-id="d663f-226">**Working directory** - /namd2</span></span>
   * <span data-ttu-id="d663f-227">**Minimum** : 3</span><span class="sxs-lookup"><span data-stu-id="d663f-227">**Minimum** - 3</span></span>
     
     ![Détails de la tâche][task_details]
     
     > [!NOTE]
     > <span data-ttu-id="d663f-229">Vous définissez le répertoire de travail ici car **charmrun** essaie de naviguer dans le même répertoire de travail sur chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="d663f-229">You set the working directory here because **charmrun** tries to navigate to the same working directory on each node.</span></span> <span data-ttu-id="d663f-230">Si le répertoire de travail n’est pas défini, HPC Pack démarre la commande dans un dossier nommé de façon aléatoire créé sur l’un des nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="d663f-230">If the working directory isn't set, HPC Pack starts the command in a randomly named folder created on one of the Linux nodes.</span></span> <span data-ttu-id="d663f-231">Cela provoque l’erreur suivante sur les autres nœuds : `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` Pour éviter ce problème, spécifiez un chemin d’accès du dossier accessible par tous les nœuds en tant que répertoire de travail.</span><span class="sxs-lookup"><span data-stu-id="d663f-231">This causes the following error on the other nodes: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` To avoid this problem, specify a folder path that can be accessed by all nodes as the working directory.</span></span>
     > 
     > 
8. <span data-ttu-id="d663f-232">Cliquez sur **OK**, puis sur **Envoyer** pour exécuter cette tâche.</span><span class="sxs-lookup"><span data-stu-id="d663f-232">Click **OK** and then click **Submit** to run this job.</span></span>
   
   <span data-ttu-id="d663f-233">Par défaut, HPC Pack envoie la tâche en tant que votre compte d’utilisateur connecté actuel.</span><span class="sxs-lookup"><span data-stu-id="d663f-233">By default, HPC Pack submits the job as your current logged-on user account.</span></span> <span data-ttu-id="d663f-234">Une boîte de dialogue peut vous inviter à entrer le nom d'utilisateur et le mot de passe après avoir cliqué sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="d663f-234">A dialog box might prompt you to enter the user name and password after you click **Submit**.</span></span>
   
   ![Informations d’identification de la tâche][creds]
   
   <span data-ttu-id="d663f-236">Dans certaines conditions, HPC Pack mémorise les informations utilisateur entrées auparavant et n’affiche plus cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d663f-236">Under some conditions, HPC Pack remembers the user information you input before and doesn't show this dialog box.</span></span> <span data-ttu-id="d663f-237">Pour que HPC Pack l’affiche de nouveau, entrez les informations suivantes à l’invite de commande, puis envoyez la tâche.</span><span class="sxs-lookup"><span data-stu-id="d663f-237">To make HPC Pack show it again, enter the following command at a Command Prompt and then submit the job.</span></span>
   
   ```command
   hpccred delcreds
   ```
9. <span data-ttu-id="d663f-238">La tâche nécessite plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="d663f-238">The job takes several minutes to finish.</span></span>
10. <span data-ttu-id="d663f-239">Vous trouverez le journal de la tâche sous \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log et les fichiers de sortie sous \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\..</span><span class="sxs-lookup"><span data-stu-id="d663f-239">Find the job log at \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log and the output files in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span></span>
11. <span data-ttu-id="d663f-240">Si vous le souhaitez, démarrez VMD pour afficher les résultats de votre tâche.</span><span class="sxs-lookup"><span data-stu-id="d663f-240">Optionally, start VMD to view your job results.</span></span> <span data-ttu-id="d663f-241">Les étapes permettant de visualiser les fichiers de sortie NAMD (dans le cas présent, une molécule protéique ubiquitine dans une sphère d’eau) dépassent le cadre de cet article.</span><span class="sxs-lookup"><span data-stu-id="d663f-241">The steps for visualizing the NAMD output files (in this case, a ubiquitin protein molecule in a water sphere) are beyond the scope of this article.</span></span> <span data-ttu-id="d663f-242">Voir [Didacticiel NAMD](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="d663f-242">See [NAMD Tutorial](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) for details.</span></span>
    
    ![Résultats de la tâche][vmd_view]

## <a name="sample-files"></a><span data-ttu-id="d663f-244">Exemple de fichiers</span><span class="sxs-lookup"><span data-stu-id="d663f-244">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="d663f-245">Exemple de fichier de configuration XML pour le déploiement de clusters par script PowerShell</span><span class="sxs-lookup"><span data-stu-id="d663f-245">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
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

### <a name="sample-credxml-file"></a><span data-ttu-id="d663f-246">Exemple de fichier cred.xml</span><span class="sxs-lookup"><span data-stu-id="d663f-246">Sample cred.xml file</span></span>
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

### <a name="sample-hpccharmrunsh-script"></a><span data-ttu-id="d663f-247">Exemple de script hpccharmrun.sh</span><span class="sxs-lookup"><span data-stu-id="d663f-247">Sample hpccharmrun.sh script</span></span>
```
#!/bin/bash

# The path of this script
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
    # If CCP_NODES_CORES is not found or is empty, just run the charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create the nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write the head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into the nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run the charmrun with nodelist arg
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
