---
title: aaaSet de HPC Pack hybride de cluster dans Azure | Documents Microsoft
description: "Découvrez comment toouse Microsoft HPC Pack et Azure tooset jusqu'à un petit, hybride haute performance computing (HPC) cluster"
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a><span data-ttu-id="9b2da-103">Configuration d’un cluster de calcul haute performance (HPC) hybride avec Microsoft HPC Pack et les nœuds de calcul Azure à la demande</span><span class="sxs-lookup"><span data-stu-id="9b2da-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span></span>
<span data-ttu-id="9b2da-104">Utilisez Microsoft HPC Pack 2012 R2 et Azure tooset d’un petite, hybride informatiques hautes performances cluster (HPC).</span><span class="sxs-lookup"><span data-stu-id="9b2da-104">Use Microsoft HPC Pack 2012 R2 and Azure tooset up a small, hybrid high performance computing (HPC) cluster.</span></span> <span data-ttu-id="9b2da-105">cluster Hello illustré dans cet article se compose d’un nœud principal de HPC Pack sur site et certains nœuds que vous déployez à la demande dans Azure cloud service de calcul.</span><span class="sxs-lookup"><span data-stu-id="9b2da-105">hello cluster shown in this article consists of an on-premises HPC Pack head node and some compute nodes you deploy on-demand in an Azure cloud service.</span></span> <span data-ttu-id="9b2da-106">Vous pouvez ensuite exécuter des travaux de calcul sur un cluster hybride de hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-106">You can then run compute jobs on hello hybrid cluster.</span></span>

![Cluster HPC hybride][Overview] 

<span data-ttu-id="9b2da-108">Ce didacticiel illustre une approche, parfois appelé cluster « rafale toohello cloud », applications de calcul intensif toorun toouse évolutive, à la demande des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2da-108">This tutorial shows one approach, sometimes called cluster "burst toohello cloud," toouse scalable, on-demand Azure resources toorun compute-intensive applications.</span></span>

<span data-ttu-id="9b2da-109">Ce didacticiel ne requiert pas d'expérience préalable avec les clusters de calcul ou HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="9b2da-109">This tutorial assumes no prior experience with compute clusters or HPC Pack.</span></span> <span data-ttu-id="9b2da-110">Il est prévu toohelp uniquement, vous déployez un cluster de calcul hybride rapidement à des fins de démonstration.</span><span class="sxs-lookup"><span data-stu-id="9b2da-110">It is intended only toohelp you deploy a hybrid compute cluster quickly for demonstration purposes.</span></span> <span data-ttu-id="9b2da-111">Pour considérations et toodeploy étapes de cluster HPC Pack hybride à plus grande échelle dans un environnement de production, ou toouse HPC Pack 2016, consultez hello [conseils détaillés](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="9b2da-111">For considerations and steps toodeploy a hybrid HPC Pack cluster at greater scale in a production environment, or toouse HPC Pack 2016, see hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span> <span data-ttu-id="9b2da-112">Pour d’autres scénarios avec HPC Pack, notamment le déploiement automatisé de clusters dans des machines virtuelles Azure, consultez [Options pour créer et gérer un cluster de calcul haute performance dans Azure avec Microsoft HPC Pack](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9b2da-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b2da-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9b2da-113">Prerequisites</span></span>
* <span data-ttu-id="9b2da-114">**Abonnement Azure** : si vous n’en avez pas, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/free/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="9b2da-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>
* <span data-ttu-id="9b2da-115">**Un ordinateur local exécutant Windows Server 2012 R2 ou Windows Server 2012** -utiliser cet ordinateur en tant que nœud principal de hello de cluster HPC de hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - Use this computer as hello head node of hello HPC cluster.</span></span> <span data-ttu-id="9b2da-116">Si vous n'utilisez pas déjà Windows Server, vous pouvez télécharger et installer une [version d'évaluation](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span><span class="sxs-lookup"><span data-stu-id="9b2da-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span></span>
  
  * <span data-ttu-id="9b2da-117">ordinateur de Hello doit être domaine d’Active Directory tooan jointes.</span><span class="sxs-lookup"><span data-stu-id="9b2da-117">hello computer must be joined tooan Active Directory domain.</span></span> <span data-ttu-id="9b2da-118">À des fins de test, vous pouvez configurer l’ordinateur du nœud principal hello comme contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="9b2da-118">For test purposes, you can configure hello head node computer as a domain controller.</span></span> <span data-ttu-id="9b2da-119">tooadd hello du rôle de serveur Services de domaine Active Directory et promouvoir l’ordinateur du nœud principal hello comme contrôleur de domaine, consultez la documentation de hello pour Windows Server.</span><span class="sxs-lookup"><span data-stu-id="9b2da-119">tooadd hello Active Directory Domain Services server role and promote hello head node computer as a domain controller, see hello documentation for Windows Server.</span></span>
  * <span data-ttu-id="9b2da-120">toosupport HPC Pack, le système d’exploitation de hello doit être installé dans un de ces langues : anglais, japonais et chinois (simplifié).</span><span class="sxs-lookup"><span data-stu-id="9b2da-120">toosupport HPC Pack, hello operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span></span>
  * <span data-ttu-id="9b2da-121">Vérifiez que les mises à jour importantes et critiques sont installées.</span><span class="sxs-lookup"><span data-stu-id="9b2da-121">Verify that important and critical updates are installed.</span></span>
* <span data-ttu-id="9b2da-122">**HPC Pack 2012 R2** - [télécharger](http://go.microsoft.com/fwlink/p/?linkid=328024) package d’installation hello pour la version la plus récente hello sans frais et copie hello fichiers toohello ordinateur du nœud principal.</span><span class="sxs-lookup"><span data-stu-id="9b2da-122">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) hello installation package for hello latest version free of charge and copy hello files toohello head node computer.</span></span> <span data-ttu-id="9b2da-123">Choisissez les fichiers d’installation Bonjour même langue que celle de votre installation de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="9b2da-123">Choose installation files in hello same language as your installation of Windows Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="9b2da-124">Si vous souhaitez toouse HPC Pack 2016, au lieu de HPC Pack 2012 R2, une configuration supplémentaire est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9b2da-124">If you want toouse HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span></span> <span data-ttu-id="9b2da-125">Consultez hello [conseils détaillés](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="9b2da-125">See hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
    > 
* <span data-ttu-id="9b2da-126">**Compte de domaine** -ce compte doit être configuré avec des autorisations d’administrateur locales sur hello tooinstall de nœud principal HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="9b2da-126">**Domain account** - This account must be configured with local Administrator permissions on hello head node tooinstall HPC Pack.</span></span>
* <span data-ttu-id="9b2da-127">**Connectivité TCP sur le port 443** de tooAzure de nœud principal hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-127">**TCP connectivity on port 443** from hello head node tooAzure.</span></span>

## <a name="install-hpc-pack-on-hello-head-node"></a><span data-ttu-id="9b2da-128">Installez le Pack HPC sur le nœud principal de hello</span><span class="sxs-lookup"><span data-stu-id="9b2da-128">Install HPC Pack on hello head node</span></span>
<span data-ttu-id="9b2da-129">Vous devez tout d'abord installer Microsoft HPC Pack sur votre ordinateur local qui exécute Windows Server</span><span class="sxs-lookup"><span data-stu-id="9b2da-129">You first install Microsoft HPC Pack on your on-premises computer running Windows Server.</span></span> <span data-ttu-id="9b2da-130">Cet ordinateur devient hello nœud de tête hello cluster.</span><span class="sxs-lookup"><span data-stu-id="9b2da-130">This computer becomes hello head node of hello cluster.</span></span>

1. <span data-ttu-id="9b2da-131">Ouvrez une session sur le nœud principal de toohello à l’aide d’un compte de domaine qui dispose des autorisations d’administrateur locales.</span><span class="sxs-lookup"><span data-stu-id="9b2da-131">Log on toohello head node by using a domain account that has local Administrator permissions.</span></span>

2. <span data-ttu-id="9b2da-132">Démarrez hello Assistant d’Installation de HPC Pack en exécutant Setup.exe à partir de fichiers d’installation de HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-132">Start hello HPC Pack Installation Wizard by running Setup.exe from hello HPC Pack installation files.</span></span>

3. <span data-ttu-id="9b2da-133">Sur hello **le programme d’installation de HPC Pack 2012 R2** , cliquez sur **nouvelle installation ou ajoutez l’installation existante de nouvelles fonctionnalités tooan**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-133">On hello **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features tooan existing installation**.</span></span>

    ![Configuration de HPC Pack 2012][install_hpc1]

4. <span data-ttu-id="9b2da-135">Sur hello **page contrat utilisateur de logiciels Microsoft**, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-135">On hello **Microsoft Software User Agreement page**, click **Next**.</span></span>

5. <span data-ttu-id="9b2da-136">Sur hello **sélectionner le Type d’Installation** , cliquez sur **créer un cluster HPC en créant un nœud principal**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-136">On hello **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span></span>

6. <span data-ttu-id="9b2da-137">Assistant de Hello exécute plusieurs tests avant l’installation.</span><span class="sxs-lookup"><span data-stu-id="9b2da-137">hello wizard runs several pre-installation tests.</span></span> <span data-ttu-id="9b2da-138">Cliquez sur **suivant** sur hello **règles d’Installation** page si tous les tests réussissent.</span><span class="sxs-lookup"><span data-stu-id="9b2da-138">Click **Next** on hello **Installation Rules** page if all tests pass.</span></span> <span data-ttu-id="9b2da-139">Sinon, passez en revue les informations hello fournies et apportez les modifications nécessaires dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="9b2da-139">Otherwise, review hello information provided and make any necessary changes in your environment.</span></span> <span data-ttu-id="9b2da-140">Puis exécutez à nouveau les tests hello ou si nécessaire démarrer hello Assistant Installation à nouveau.</span><span class="sxs-lookup"><span data-stu-id="9b2da-140">Then run hello tests again or if necessary start hello Installation Wizard again.</span></span>
7. <span data-ttu-id="9b2da-141">Sur hello **Configuration de base de données HPC** , vérifiez que **le nœud principal** est activée pour toutes les bases de données HPC, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-141">On hello **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span></span> 

    ![Configuration de base de données][install_hpc4]

8. <span data-ttu-id="9b2da-143">Acceptez les sélections par défaut sur les pages restantes de hello d’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-143">Accept default selections on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="9b2da-144">Sur hello **installer les composants nécessaires** , cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-144">On hello **Install Required Components** page, click **Install**.</span></span>
   
    ![Installer][install_hpc6]

9. <span data-ttu-id="9b2da-146">Après l’installation de hello, décochez la case **démarrer HPC Cluster Manager** puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-146">After hello installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span></span> <span data-ttu-id="9b2da-147">(Vous pourrez démarrer HPC Cluster Manager à une étape ultérieure.)</span><span class="sxs-lookup"><span data-stu-id="9b2da-147">(You start HPC Cluster Manager in a later step.)</span></span>
   
    ![Terminer][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a><span data-ttu-id="9b2da-149">Préparer hello abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="9b2da-149">Prepare hello Azure subscription</span></span>
<span data-ttu-id="9b2da-150">Effectuer hello comme suit dans hello [portail Azure](https://portal.azure.com) avec votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2da-150">Perform hello following steps in hello [Azure portal](https://portal.azure.com) with your Azure subscription.</span></span> <span data-ttu-id="9b2da-151">Après avoir effectué ces étapes, vous pouvez déployer des nœuds Azure à partir du nœud principal local hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-151">After completing these steps, you can deploy Azure nodes from hello on-premises head node.</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="9b2da-152">Notez votre ID d’abonnement Azure. Il vous sera utile par la suite.</span><span class="sxs-lookup"><span data-stu-id="9b2da-152">Also make a note of your Azure subscription ID, which you need later.</span></span> <span data-ttu-id="9b2da-153">Trouver l’ID de hello dans **abonnements** dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-153">Find hello ID in **Subscriptions** in hello portal.</span></span>
  > 

### <a name="upload-hello-default-management-certificate"></a><span data-ttu-id="9b2da-154">Télécharger le certificat de gestion par défaut hello</span><span class="sxs-lookup"><span data-stu-id="9b2da-154">Upload hello default management certificate</span></span>
<span data-ttu-id="9b2da-155">HPC Pack installe un certificat auto-signé sur le nœud principal hello, appelé certificat de gestion par défaut Microsoft HPC Azure hello, que vous pouvez télécharger en tant qu’un certificat de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2da-155">HPC Pack installs a self-signed certificate on hello head node, called hello Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span></span> <span data-ttu-id="9b2da-156">Ce certificat est fourni pour le test et les déploiements de preuve de concept toosecure hello relier hello du nœud principal et Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2da-156">This certificate is provided for testing and proof-of-concept deployments toosecure hello connection between hello head node and Azure.</span></span>

1. <span data-ttu-id="9b2da-157">À partir de l’ordinateur du nœud principal hello, connectez-vous toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9b2da-157">From hello head node computer, sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="9b2da-158">Cliquez sur **Abonnements** > *nom_de_votre_abonnement*.</span><span class="sxs-lookup"><span data-stu-id="9b2da-158">Click **Subscriptions** > *your_subscription_name*.</span></span>

3. <span data-ttu-id="9b2da-159">Cliquez sur **Certificats de gestion** > **Télécharger**.4.</span><span class="sxs-lookup"><span data-stu-id="9b2da-159">Click **Management certificates** > **Upload**.4.</span></span> <span data-ttu-id="9b2da-160">Rechercher sur le nœud principal de hello pour hello fichier C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span><span class="sxs-lookup"><span data-stu-id="9b2da-160">Browse on hello head node for hello file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span></span> <span data-ttu-id="9b2da-161">Cliquez ensuite sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-161">Then, click **Upload**.</span></span>

   
<span data-ttu-id="9b2da-162">Hello **gestion de Azure HPC par défaut** certificat apparaît dans la liste hello des certificats de gestion.</span><span class="sxs-lookup"><span data-stu-id="9b2da-162">hello **Default HPC Azure Management** certificate appears in hello list of management certificates.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="9b2da-163">Création d'un service cloud Azure</span><span class="sxs-lookup"><span data-stu-id="9b2da-163">Create an Azure cloud service</span></span>
> [!NOTE]
> <span data-ttu-id="9b2da-164">Pour de meilleures performances, créer un compte de stockage de hello (dans une étape ultérieure) et de service de cloud computing hello Bonjour même région géographique.</span><span class="sxs-lookup"><span data-stu-id="9b2da-164">For best performance, create hello cloud service and hello storage account (in a later step) in hello same geographic region.</span></span>
> 
> 

1. <span data-ttu-id="9b2da-165">Dans le portail de hello, cliquez sur **(classiques) de services de cloud computing** > **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-165">In hello portal, click **Cloud services (classic)** > **+Add**.</span></span>

2.  <span data-ttu-id="9b2da-166">Tapez un nom DNS pour le service de hello, choisissez un groupe de ressources et un emplacement, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-166">Type a DNS name for hello service, choose a resource group and a location, and then click **Create**.</span></span>


### <a name="create-an-azure-storage-account"></a><span data-ttu-id="9b2da-167">Création d'un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="9b2da-167">Create an Azure storage account</span></span>
1. <span data-ttu-id="9b2da-168">Dans le portail de hello, cliquez sur **comptes de stockage (classiques)** > **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-168">In hello portal, click **Storage accounts (classic)** > **+Add**.</span></span>

2. <span data-ttu-id="9b2da-169">Tapez un nom pour le compte de hello et sélectionnez hello **classique** modèle de déploiement.</span><span class="sxs-lookup"><span data-stu-id="9b2da-169">Type a name for hello account, and select hello **Classic** deployment model.</span></span>

3. <span data-ttu-id="9b2da-170">Sélectionnez un groupe de ressources et un emplacement, et conservez les valeurs par défaut des autres paramètres.</span><span class="sxs-lookup"><span data-stu-id="9b2da-170">Choose a resource group and a location, and leave other settings at default values.</span></span> <span data-ttu-id="9b2da-171">Cliquez ensuite sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-171">Then click **Create**.</span></span>

## <a name="configure-hello-head-node"></a><span data-ttu-id="9b2da-172">Configurer le nœud principal de hello</span><span class="sxs-lookup"><span data-stu-id="9b2da-172">Configure hello head node</span></span>
<span data-ttu-id="9b2da-173">toouse toodeploy de HPC Cluster Manager nœuds Azure et les travaux de toosubmit, d’abord effectuer certaines étapes de configuration de cluster nécessaires.</span><span class="sxs-lookup"><span data-stu-id="9b2da-173">toouse HPC Cluster Manager toodeploy Azure nodes and toosubmit jobs, first perform some required cluster configuration steps.</span></span>

1. <span data-ttu-id="9b2da-174">Sur le nœud principal de hello, démarrez HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="9b2da-174">On hello head node, start HPC Cluster Manager.</span></span> <span data-ttu-id="9b2da-175">Si hello **sélectionner le nœud principal** boîte de dialogue s’affiche, cliquez sur **ordinateur Local**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-175">If hello **Select Head Node** dialog box appears, click **Local Computer**.</span></span> <span data-ttu-id="9b2da-176">Hello **liste des tâches de déploiement** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="9b2da-176">hello **Deployment To-do List** appears.</span></span>

2. <span data-ttu-id="9b2da-177">Sous **Tâches de déploiement requises**, cliquez sur **Configurer votre réseau**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-177">Under **Required deployment tasks**, click **Configure your network**.</span></span>
   
    ![Configurer le réseau][config_hpc2]

3. <span data-ttu-id="9b2da-179">Dans l’Assistant Configuration du réseau de hello, sélectionnez **tous les nœuds sur un réseau d’entreprise** (topologie 5).</span><span class="sxs-lookup"><span data-stu-id="9b2da-179">In hello Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span></span> <span data-ttu-id="9b2da-180">Cette configuration de réseau est hello plus simple à des fins de démonstration.</span><span class="sxs-lookup"><span data-stu-id="9b2da-180">This network configuration is hello simplest for demonstration purposes.</span></span>
   
    ![Topologie 5][config_hpc3]
   
4. <span data-ttu-id="9b2da-182">Cliquez sur **suivant** tooaccept les valeurs par défaut sur hello restant des pages d’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-182">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="9b2da-183">Ensuite, sous hello **révision** , cliquez sur **configurer** configuration du réseau toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-183">Then, on hello **Review** tab, click **Configure** toocomplete hello network configuration.</span></span>

5. <span data-ttu-id="9b2da-184">Bonjour **liste des tâches de déploiement**, cliquez sur **fournissent des informations d’identification de l’installation**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-184">In hello **Deployment To-do List**, click **Provide installation credentials**.</span></span>

6. <span data-ttu-id="9b2da-185">Bonjour **informations d’identification de l’Installation** boîte de dialogue, les informations d’identification de type hello du compte de domaine hello que vous avez utilisé tooinstall HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="9b2da-185">In hello **Installation Credentials** dialog box, type hello credentials of hello domain account that you used tooinstall HPC Pack.</span></span> <span data-ttu-id="9b2da-186">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-186">Then click **OK**.</span></span> 
   
    ![Installation Credentials][config_hpc6]
   
7. <span data-ttu-id="9b2da-188">Bonjour **liste des tâches de déploiement**, cliquez sur **configurer hello d’affectation de noms des nouveaux nœuds**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-188">In hello **Deployment To-do List**, click **Configure hello naming of new nodes**.</span></span>

8. <span data-ttu-id="9b2da-189">Bonjour **spécifier une série de noms de nœud** boîte de dialogue zone, accepter d’affectation de noms série et cliquez sur la valeur par défaut hello **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-189">In hello **Specify Node Naming Series** dialog box, accept hello default naming series and click **OK**.</span></span> <span data-ttu-id="9b2da-190">Effectuez cette étape, même si hello nœuds Azure, que vous ajoutez dans ce didacticiel sont nommées automatiquement.</span><span class="sxs-lookup"><span data-stu-id="9b2da-190">Complete this step even though hello Azure nodes you add in this tutorial are named automatically.</span></span>
   
    ![Noms de nœuds][config_hpc8]
   
9. <span data-ttu-id="9b2da-192">Bonjour **liste des tâches de déploiement**, cliquez sur **créer un modèle de nœud**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-192">In hello **Deployment To-do List**, click **Create a node template**.</span></span> <span data-ttu-id="9b2da-193">Plus loin dans le didacticiel de hello, vous utilisez cluster toohello de hello nœud modèle tooadd nœuds Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2da-193">Later in hello tutorial, you use hello node template tooadd Azure nodes toohello cluster.</span></span>

10. <span data-ttu-id="9b2da-194">Dans hello Assistant modèle de nœud, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="9b2da-194">In hello Create Node Template Wizard, do hello following:</span></span>
    
    <span data-ttu-id="9b2da-195">a.</span><span class="sxs-lookup"><span data-stu-id="9b2da-195">a.</span></span> <span data-ttu-id="9b2da-196">Sur hello **choisir le Type de modèle de nœud** , cliquez sur **modèle de nœud Windows Azure**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-196">On hello **Choose Node Template Type** page, click **Windows Azure node template**, and then click **Next**.</span></span>
    
    ![Modèle de nœud][config_hpc10]
    
    <span data-ttu-id="9b2da-198">b.</span><span class="sxs-lookup"><span data-stu-id="9b2da-198">b.</span></span> <span data-ttu-id="9b2da-199">Cliquez sur **suivant** nom de modèle par défaut tooaccept hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-199">Click **Next** tooaccept hello default template name.</span></span>
    
    <span data-ttu-id="9b2da-200">c.</span><span class="sxs-lookup"><span data-stu-id="9b2da-200">c.</span></span> <span data-ttu-id="9b2da-201">Sur hello **fournissent des informations d’abonnement** , entrez votre ID d’abonnement Azure (disponible dans les informations de votre compte Azure).</span><span class="sxs-lookup"><span data-stu-id="9b2da-201">On hello **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span></span> <span data-ttu-id="9b2da-202">Puis, sous **Certificat de gestion**, recherchez **Gestion Azure Microsoft HPC par défaut**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-202">Then, in **Management certificate**, browse for **Default Microsoft HPC Azure Management.**</span></span> <span data-ttu-id="9b2da-203">Cliquez ensuite sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-203">Then click **Next**.</span></span>
    
    ![Modèle de nœud][config_hpc12]
    
    <span data-ttu-id="9b2da-205">d.</span><span class="sxs-lookup"><span data-stu-id="9b2da-205">d.</span></span> <span data-ttu-id="9b2da-206">Sur hello **fournissent des informations de Service** page, le service cloud sélectionnez hello et compte de stockage hello que vous avez créé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="9b2da-206">On hello **Provide Service Information** page, select hello cloud service and hello storage account that you created in a previous step.</span></span> <span data-ttu-id="9b2da-207">Cliquez ensuite sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-207">Then click **Next**.</span></span>
    
    ![Modèle de nœud][config_hpc13]
    
    <span data-ttu-id="9b2da-209">e.</span><span class="sxs-lookup"><span data-stu-id="9b2da-209">e.</span></span> <span data-ttu-id="9b2da-210">Cliquez sur **suivant** tooaccept les valeurs par défaut sur hello restant des pages d’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-210">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="9b2da-211">Ensuite, sous hello **révision** , cliquez sur **créer** modèle de nœud toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-211">Then, on hello **Review** tab, click **Create** toocreate hello node template.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="9b2da-212">Par défaut, modèle de nœud Azure hello inclut des paramètres pour toostart (disposition) et les nœuds de hello arrêter manuellement, à l’aide de HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="9b2da-212">By default, hello Azure node template includes settings for you toostart (provision) and stop hello nodes manually, using HPC Cluster Manager.</span></span> <span data-ttu-id="9b2da-213">Vous pouvez éventuellement configurer un toostart de planification et d’arrêter hello automatiquement des nœuds Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2da-213">You can optionally configure a schedule toostart and stop hello Azure nodes automatically.</span></span>
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a><span data-ttu-id="9b2da-214">Ajouter des nœuds Azure toohello cluster</span><span class="sxs-lookup"><span data-stu-id="9b2da-214">Add Azure nodes toohello cluster</span></span>
<span data-ttu-id="9b2da-215">Maintenant utiliser le cluster de toohello hello nœud modèle tooadd nœuds Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2da-215">Now use hello node template tooadd Azure nodes toohello cluster.</span></span> <span data-ttu-id="9b2da-216">Ajout de cluster de toohello nœuds hello stocke ses informations de configuration afin que vous puissiez démarrer (approvisionner) les à tout moment dans le service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-216">Adding hello nodes toohello cluster stores their configuration information so that you can start (provision) them at any time in hello cloud service.</span></span> <span data-ttu-id="9b2da-217">Votre abonnement obtient uniquement facturé pour les nœuds Azure une fois que les instances de hello sont en cours d’exécution dans le service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-217">Your subscription only gets charged for Azure nodes after hello instances are running in hello cloud service.</span></span>

<span data-ttu-id="9b2da-218">Suivez ces étapes tooadd deux petits nœuds.</span><span class="sxs-lookup"><span data-stu-id="9b2da-218">Follow these steps tooadd two Small nodes.</span></span>

1. <span data-ttu-id="9b2da-219">Dans HPC Cluster Manager, cliquez sur **Gestion des nœuds** (ou **Gestion des ressources** dans les versions actuelles de HPC Pack) > **Ajouter un nœud**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-219">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack) > **Add Node**.</span></span>
   
    ![Add Node][add_node1]

2. <span data-ttu-id="9b2da-221">Dans hello Assistant Ajout de nœud, sur hello **sélectionner la méthode de déploiement** , cliquez sur **nœuds ajouter Windows Azure**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-221">In hello Add Node Wizard, on hello **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span></span>
   
    ![Ajouter un nœud Azure][add_node1_1]

3. <span data-ttu-id="9b2da-223">Sur hello **spécifier de nouveaux nœuds** page, le modèle de nœud Azure hello sélectionnez vous avez créé précédemment (appelée par défaut **par défaut AzureNode modèle**).</span><span class="sxs-lookup"><span data-stu-id="9b2da-223">On hello **Specify New Nodes** page, select hello Azure node template you created previously (called by default **Default AzureNode Template**).</span></span> <span data-ttu-id="9b2da-224">Spécifiez ensuite **2** nœuds de taille **Petite**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-224">Then specify **2** nodes of size **Small**, and then click **Next**.</span></span>
   
    ![Spécifier les nœuds][add_node2]
   
4. <span data-ttu-id="9b2da-226">Sur hello **fin hello Assistant Ajout de nœud** , cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-226">On hello **Completing hello Add Node Wizard** page, click **Finish**.</span></span>
    
     <span data-ttu-id="9b2da-227">Deux nœuds Azure, nommés **AzureCN-0001** et **AzureCN-0002**, sont désormais affichés dans HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="9b2da-227">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span></span> <span data-ttu-id="9b2da-228">Les deux sont Bonjour **Not-Deployed** état.</span><span class="sxs-lookup"><span data-stu-id="9b2da-228">Both are in hello **Not-Deployed** state.</span></span>
   
    ![Nœuds ajoutés][add_node3]

## <a name="start-hello-azure-nodes"></a><span data-ttu-id="9b2da-230">Démarrer hello des nœuds Azure</span><span class="sxs-lookup"><span data-stu-id="9b2da-230">Start hello Azure nodes</span></span>
<span data-ttu-id="9b2da-231">Lorsque vous souhaitez que les ressources du cluster de hello toouse dans Azure, utilisez HPC Cluster Manager toostart (disposition) hello des nœuds Azure et les mettent en ligne.</span><span class="sxs-lookup"><span data-stu-id="9b2da-231">When you want toouse hello cluster resources in Azure, use HPC Cluster Manager toostart (provision) hello Azure nodes and bring them online.</span></span>

1. <span data-ttu-id="9b2da-232">Dans HPC Cluster Manager, cliquez sur **la gestion des nœuds** (appelé **gestion des ressources** dans les versions actuelles de HPC Pack), et sélectionnez hello nœuds Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2da-232">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack), and select hello Azure nodes.</span></span>

2. <span data-ttu-id="9b2da-233">Cliquez sur **Démarrer**, puis sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-233">Click **Start**, and then click **OK**.</span></span>
   
   ![Démarrer les nœuds][add_node4]
   
    <span data-ttu-id="9b2da-235">les nœuds Hello transition toohello **Provisioning** état.</span><span class="sxs-lookup"><span data-stu-id="9b2da-235">hello nodes transition toohello **Provisioning** state.</span></span> <span data-ttu-id="9b2da-236">Hello vue hello tootrack de journal progression de provisionnement de configuration.</span><span class="sxs-lookup"><span data-stu-id="9b2da-236">View hello provisioning log tootrack hello provisioning progress.</span></span>
   
    ![Nœuds d'approvisionnement][add_node6]

3. <span data-ttu-id="9b2da-238">Après quelques minutes, hello nœuds Azure terminer l’approvisionnement et sont Bonjour **hors connexion** état.</span><span class="sxs-lookup"><span data-stu-id="9b2da-238">After a few minutes, hello Azure nodes finish provisioning and are in hello **Offline** state.</span></span> <span data-ttu-id="9b2da-239">Dans cet état, les instances de rôle hello sont en cours d’exécution mais ne peut pas accepter encore les travaux de cluster.</span><span class="sxs-lookup"><span data-stu-id="9b2da-239">In this state, hello role instances are running but cannot yet accept cluster jobs.</span></span>

4. <span data-ttu-id="9b2da-240">tooconfirm qui hello des instances de rôle sont en cours d’exécution, Bonjour portail Azure, cliquez sur **Services Cloud (classiques)** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="9b2da-240">tooconfirm that hello role instances are running, in hello Azure portal, click **Cloud Services (classic)** > *your_cloud_service_name*.</span></span>
   
   <span data-ttu-id="9b2da-241">Vous devez voir deux **HpcWorkerRole** instances (nœuds) en cours d’exécution dans le service hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-241">You should see two **HpcWorkerRole** instances (nodes) running in hello service.</span></span> <span data-ttu-id="9b2da-242">HPC Pack déploie automatiquement deux **HpcProxy** instances de communication de toohandle (taille moyenne) entre le nœud principal de hello et Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2da-242">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) toohandle communication between hello head node and Azure.</span></span>

   ![Instances en cours d'exécution][view_instances1]

5. <span data-ttu-id="9b2da-244">toorun en ligne des nœuds Azure hello toobring de travaux, les nœuds sélectionnez hello, avec le bouton droit, puis cliquez sur cluster **mettre en ligne**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-244">toobring hello Azure nodes online toorun cluster jobs, select hello nodes, right-click, and then click **Bring Online**.</span></span>
   
    ![Nœuds hors ligne][add_node7]
   
    <span data-ttu-id="9b2da-246">HPC Cluster Manager indique que les nœuds de hello sont Bonjour **Online** état.</span><span class="sxs-lookup"><span data-stu-id="9b2da-246">HPC Cluster Manager indicates that hello nodes are in hello **Online** state.</span></span>

## <a name="run-a-command-across-hello-cluster"></a><span data-ttu-id="9b2da-247">Exécuter une commande sur le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="9b2da-247">Run a command across hello cluster</span></span>
<span data-ttu-id="9b2da-248">installation de hello toocheck, utilisez hello HPC Pack **clusrun** commande toorun une commande ou une application sur un ou plusieurs nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="9b2da-248">toocheck hello installation, use hello HPC Pack **clusrun** command toorun a command or application on one or more cluster nodes.</span></span> <span data-ttu-id="9b2da-249">À titre d’exemple, utilisez **clusrun** configuration d’IP tooget hello de hello nœuds Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2da-249">As a simple example, use **clusrun** tooget hello IP configuration of hello Azure nodes.</span></span>

1. <span data-ttu-id="9b2da-250">Sur le nœud principal de hello, ouvrez une invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="9b2da-250">On hello head node, open a command prompt as an administrator.</span></span>

2. <span data-ttu-id="9b2da-251">Tapez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9b2da-251">Type hello following command:</span></span>
   
    `clusrun /nodes:azurecn* ipconfig`

3. <span data-ttu-id="9b2da-252">Si vous y êtes invité, entrez votre mot de passe administrateur de cluster.</span><span class="sxs-lookup"><span data-stu-id="9b2da-252">If prompted, enter your cluster administrator password.</span></span> <span data-ttu-id="9b2da-253">Vous devez voir similaire toohello suivant de sortie de commande.</span><span class="sxs-lookup"><span data-stu-id="9b2da-253">You should see command output similar toohello following.</span></span>
   
    ![clusrun][clusrun1]

## <a name="run-a-test-job"></a><span data-ttu-id="9b2da-255">Exécution d'une tâche de test</span><span class="sxs-lookup"><span data-stu-id="9b2da-255">Run a test job</span></span>
<span data-ttu-id="9b2da-256">Maintenant soumettre un travail de test qui s’exécute sur un cluster hybride de hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-256">Now submit a test job that runs on hello hybrid cluster.</span></span> <span data-ttu-id="9b2da-257">Cet exemple est une simple tâche de « balayage paramétrique » (un type de calcul intrinsèquement parallèle).</span><span class="sxs-lookup"><span data-stu-id="9b2da-257">This example is a simple parametric sweep job (a type of intrinsically parallel computation).</span></span> <span data-ttu-id="9b2da-258">Cet exemple exécute des tâches subordonnées qui ajoutent une tooitself entier à l’aide de hello **set /a** commande.</span><span class="sxs-lookup"><span data-stu-id="9b2da-258">This example runs subtasks that add an integer tooitself by using hello **set /a** command.</span></span> <span data-ttu-id="9b2da-259">Tous les nœuds hello cluster de hello contribuent toofinishing les tâches subordonnées hello pour les entiers de 1 too100.</span><span class="sxs-lookup"><span data-stu-id="9b2da-259">All hello nodes in hello cluster contribute toofinishing hello subtasks for integers from 1 too100.</span></span>

1. <span data-ttu-id="9b2da-260">Dans HPC Cluster Manager, cliquez sur **Gestion des tâches** > **Nouvelle tâche de balayage paramétrique**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-260">In HPC Cluster Manager, click **Job Management** > **New Parametric Sweep Job**.</span></span>
   
    ![Nouvelle tâche][test_job1]

2. <span data-ttu-id="9b2da-262">Bonjour **nouveau travail de balayage paramétrique** boîte de dialogue **ligne de commande**, type `set /a *+*` (ligne de commande hello par défaut qui s’affiche par écrasement).</span><span class="sxs-lookup"><span data-stu-id="9b2da-262">In hello **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting hello default command line that appears).</span></span> <span data-ttu-id="9b2da-263">Conservez les valeurs par défaut pour hello restant de paramètres, puis cliquez sur **Submit** tâche hello de toosubmit.</span><span class="sxs-lookup"><span data-stu-id="9b2da-263">Leave default values for hello remaining settings, and then click **Submit** toosubmit hello job.</span></span>
   
    ![Balayage paramétrique][param_sweep1]

3. <span data-ttu-id="9b2da-265">Lorsque le travail hello est terminé, double-cliquez sur hello **Mes tâches balayage** travail.</span><span class="sxs-lookup"><span data-stu-id="9b2da-265">When hello job is finished, double-click hello **My Sweep Task** job.</span></span>

4. <span data-ttu-id="9b2da-266">Cliquez sur **afficher les tâches**, puis cliquez sur une sortie de hello calculé sous-tâche tooview cette tâche subordonnée.</span><span class="sxs-lookup"><span data-stu-id="9b2da-266">Click **View Tasks**, and then click a subtask tooview hello calculated output of that subtask.</span></span>
   
    ![Résultats de la tâche][view_job361]

5. <span data-ttu-id="9b2da-268">toosee quel nœud effectué le calcul de hello pour cette tâche subordonnée, cliquez sur **alloué des nœuds**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-268">toosee which node performed hello calculation for that subtask, click **Allocated Nodes**.</span></span> <span data-ttu-id="9b2da-269">(votre cluster peut indiquer un nom de nœud différent).</span><span class="sxs-lookup"><span data-stu-id="9b2da-269">(Your cluster might show a different node name.)</span></span>
   
    ![Résultats de la tâche][view_job362]

## <a name="stop-hello-azure-nodes"></a><span data-ttu-id="9b2da-271">Arrêter hello des nœuds Azure</span><span class="sxs-lookup"><span data-stu-id="9b2da-271">Stop hello Azure nodes</span></span>
<span data-ttu-id="9b2da-272">Une fois que vous essayez de cluster de hello, arrêtez compte tooyour de hello nœuds Azure tooavoid les coûts inutiles.</span><span class="sxs-lookup"><span data-stu-id="9b2da-272">After you try out hello cluster, stop hello Azure nodes tooavoid unnecessary charges tooyour account.</span></span> <span data-ttu-id="9b2da-273">Cette étape arrête le service de cloud computing hello et supprime des instances de rôle Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-273">This step stops hello cloud service and removes hello Azure role instances.</span></span>

1. <span data-ttu-id="9b2da-274">Dans HPC Cluster Manager, sous **Gestion des nœuds** (ou **Gestion des ressources** dans les versions antérieures de HPC Pack), sélectionnez les deux nœuds Azure.</span><span class="sxs-lookup"><span data-stu-id="9b2da-274">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in previous versions of HPC Pack), select both Azure nodes.</span></span> <span data-ttu-id="9b2da-275">Cliquez ensuite sur **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-275">Then, click **Stop**.</span></span>
   
    ![Arrêter les nœuds][stop_node1]

2. <span data-ttu-id="9b2da-277">Bonjour **nœuds arrêter Windows Azure** boîte de dialogue, cliquez sur **arrêter**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-277">In hello **Stop Windows Azure nodes** dialog box, click **Stop**.</span></span> 
   
3. <span data-ttu-id="9b2da-278">les nœuds Hello transition toohello **arrêt** état.</span><span class="sxs-lookup"><span data-stu-id="9b2da-278">hello nodes transition toohello **Stopping** state.</span></span> <span data-ttu-id="9b2da-279">Après quelques minutes, HPC Cluster Manager indique que les nœuds hello **Not-Deployed**.</span><span class="sxs-lookup"><span data-stu-id="9b2da-279">After a few minutes, HPC Cluster Manager shows that hello nodes are **Not-Deployed**.</span></span>
   
    ![Nœuds non déployés][stop_node4]

4. <span data-ttu-id="9b2da-281">tooconfirm les instances de rôle hello sont n’est plus en cours d’exécution dans Azure, dans hello portail, Azure, sur **(classiques) de services de cloud computing** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="9b2da-281">tooconfirm that hello role instances are no longer running in Azure, in hello Azure portal, click **Cloud services (classic)** > *your_cloud_service_name*.</span></span> <span data-ttu-id="9b2da-282">Aucune instance n’est déployés dans un environnement de production hello.</span><span class="sxs-lookup"><span data-stu-id="9b2da-282">No instances are deployed in hello production environment.</span></span> 
   
    <span data-ttu-id="9b2da-283">Didacticiel de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="9b2da-283">This completes hello tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b2da-284">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9b2da-284">Next steps</span></span>
* <span data-ttu-id="9b2da-285">Explorer la documentation hello pour [HPC Pack](https://technet.microsoft.com/library/cc514029).</span><span class="sxs-lookup"><span data-stu-id="9b2da-285">Explore hello documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span></span>
* <span data-ttu-id="9b2da-286">tooset d’un déploiement de cluster HPC Pack à une échelle supérieure, hybride voir [croître tooAzure des Instances de rôle de travail avec Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="9b2da-286">tooset up a hybrid HPC Pack cluster deployment at greater scale, see [Burst tooAzure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
* <span data-ttu-id="9b2da-287">Pour les autres façons toocreate un cluster HPC Pack dans Azure, y compris à l’aide de modèles Azure Resource Manager, consultez [options de cluster HPC avec Microsoft HPC Pack dans Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9b2da-287">For other ways toocreate an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
