---
title: aaaSQL ICF Server - Machines virtuelles Azure | Documents Microsoft
description: "Cet article explique comment toocreate sur des Machines virtuelles Azure de l’Instance Cluster de basculement SQL Server."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="dfcac-103">Configurer une instance de cluster de basculement SQL Server sur des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="dfcac-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="dfcac-104">Cet article explique comment toocreate un basculement SQL Server Cluster Instance (ICF) sur les machines virtuelles dans le modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="dfcac-104">This article explains how toocreate a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="dfcac-105">Cette solution utilise [Windows Server 2016 Datacenter edition espaces de stockage Direct \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) comme un logiciel réseau SAN virtuel qui synchronise le stockage hello (disques de données) entre les nœuds hello (machines virtuelles Azure) dans un Cluster Windows.</span><span class="sxs-lookup"><span data-stu-id="dfcac-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes hello storage (data disks) between hello nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="dfcac-106">La technologie Espaces de stockage direct (S2D) est une nouveauté dans Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="dfcac-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="dfcac-107">Hello diagramme suivant montre les solution complète hello sur des machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="dfcac-107">hello following diagram shows hello complete solution on Azure virtual machines:</span></span>

![Groupe de disponibilité](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="dfcac-109">Hello précédant le diagramme montre :</span><span class="sxs-lookup"><span data-stu-id="dfcac-109">hello preceding diagram shows:</span></span>

- <span data-ttu-id="dfcac-110">Deux machines virtuelles Azure dans un cluster de basculement Windows.</span><span class="sxs-lookup"><span data-stu-id="dfcac-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="dfcac-111">Lorsqu’une machine virtuelle se trouve dans un cluster de basculement, elle est également désignée comme *nœud* ou *nœuds* de cluster.</span><span class="sxs-lookup"><span data-stu-id="dfcac-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="dfcac-112">Chaque machine virtuelle possède au moins deux disques de données.</span><span class="sxs-lookup"><span data-stu-id="dfcac-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="dfcac-113">S2D synchronise les données de hello sur disque de données hello et présente le stockage hello synchronisé en tant qu’un pool de stockage.</span><span class="sxs-lookup"><span data-stu-id="dfcac-113">S2D synchronizes hello data on hello data disk and presents hello synchronized storage as a storage pool.</span></span>
- <span data-ttu-id="dfcac-114">pool de stockage Hello présente un cluster de basculement de cluster (CSV) de volume partagé toohello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-114">hello storage pool presents a cluster shared volume (CSV) toohello failover cluster.</span></span>
- <span data-ttu-id="dfcac-115">rôle de cluster SQL Server FCI Hello utilise hello CSV hello lecteurs de données.</span><span class="sxs-lookup"><span data-stu-id="dfcac-115">hello SQL Server FCI cluster role uses hello CSV for hello data drives.</span></span>
- <span data-ttu-id="dfcac-116">Une charge Azure équilibrage toohold hello adresse IP pour hello ICF de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dfcac-116">An Azure load balancer toohold hello IP address for hello SQL Server FCI.</span></span>
- <span data-ttu-id="dfcac-117">Haute disponibilité Azure conserve toutes les ressources hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-117">An Azure availability set holds all hello resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="dfcac-118">Toutes les ressources Azure sont dans le diagramme de hello sont Bonjour même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="dfcac-118">All Azure resources are in hello diagram are in hello same resource group.</span></span>

<span data-ttu-id="dfcac-119">Pour plus d’informations sur la technologie S2D, consultez [l’édition Espaces de stockage direct \(S2D\) de Windows Server 2016 Datacenter](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span><span class="sxs-lookup"><span data-stu-id="dfcac-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span>

<span data-ttu-id="dfcac-120">La technologie S2D prend en charge deux types d’architectures : convergée et hyper-convergée.</span><span class="sxs-lookup"><span data-stu-id="dfcac-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="dfcac-121">architecture de Hello dans ce document est Hyper-convergée.</span><span class="sxs-lookup"><span data-stu-id="dfcac-121">hello architecture in this document is hyper-converged.</span></span> <span data-ttu-id="dfcac-122">Un stockage de hello emplacements Hyper-convergée l’infrastructure sur hello serveurs mêmes application hello cluster hôte.</span><span class="sxs-lookup"><span data-stu-id="dfcac-122">A hyper-converged infrastructure places hello storage on hello same servers that host hello clustered application.</span></span> <span data-ttu-id="dfcac-123">Dans cette architecture, le stockage de hello est sur chaque nœud de l’instance de cluster de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dfcac-123">In this architecture, hello storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="dfcac-124">Exemple de modèle Azure</span><span class="sxs-lookup"><span data-stu-id="dfcac-124">Example Azure template</span></span>

<span data-ttu-id="dfcac-125">Vous pouvez créer l’ensemble de la solution hello dans Azure à partir d’un modèle.</span><span class="sxs-lookup"><span data-stu-id="dfcac-125">You can create hello entire solution in Azure from a template.</span></span> <span data-ttu-id="dfcac-126">Un exemple d’un modèle est disponible dans hello GitHub [modèles de démarrage rapide Azure](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span><span class="sxs-lookup"><span data-stu-id="dfcac-126">An example of a template is available in hello GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="dfcac-127">Cet exemple n’est pas conçu ni testé pour une charge de travail spécifique.</span><span class="sxs-lookup"><span data-stu-id="dfcac-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="dfcac-128">Vous pouvez exécuter hello modèle toocreate une instance de cluster SQL Server avec le domaine S2D tooyour connecté.</span><span class="sxs-lookup"><span data-stu-id="dfcac-128">You can run hello template toocreate a SQL Server FCI with S2D storage connected tooyour domain.</span></span> <span data-ttu-id="dfcac-129">Vous pouvez évaluer le modèle de hello et modifier en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="dfcac-129">You can evaluate hello template, and modify it for your purposes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dfcac-130">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="dfcac-130">Before you begin</span></span>

<span data-ttu-id="dfcac-131">Il existe plusieurs choses tooknow et remplit les fonctions dont vous avez besoin en place avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="dfcac-131">There are a few things you need tooknow and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-tooknow"></a><span data-ttu-id="dfcac-132">Quel tooknow</span><span class="sxs-lookup"><span data-stu-id="dfcac-132">What tooknow</span></span>
<span data-ttu-id="dfcac-133">Vous devez avoir une compréhension opérationnelle de hello suivant technologies :</span><span class="sxs-lookup"><span data-stu-id="dfcac-133">You should have an operational understanding of hello following technologies:</span></span>

- [<span data-ttu-id="dfcac-134">Technologies de cluster Windows</span><span class="sxs-lookup"><span data-stu-id="dfcac-134">Windows cluster technologies</span></span>](http://technet.microsoft.com/library/hh831579.aspx)
-  <span data-ttu-id="dfcac-135">[Instances de cluster de basculement SQL Server](http://msdn.microsoft.com/library/ms189134.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfcac-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span>

<span data-ttu-id="dfcac-136">En outre, doit avoir une compréhension générale de hello suivant technologies :</span><span class="sxs-lookup"><span data-stu-id="dfcac-136">Also, you should have a general understanding of hello following technologies:</span></span>

- [<span data-ttu-id="dfcac-137">Solution hyper-convergée utilisant les Espaces de stockage direct dans Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="dfcac-137">Hyper-converged solution using Storage Spaces Direct in Windows Server 2016</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [<span data-ttu-id="dfcac-138">Groupes de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="dfcac-138">Azure resource groups</span></span>](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a><span data-ttu-id="dfcac-139">Quel toohave</span><span class="sxs-lookup"><span data-stu-id="dfcac-139">What toohave</span></span>

<span data-ttu-id="dfcac-140">Avant de suivre les instructions de hello dans cet article, vous devez déjà avoir :</span><span class="sxs-lookup"><span data-stu-id="dfcac-140">Before following hello instructions in this article, you should already have:</span></span>

- <span data-ttu-id="dfcac-141">Un abonnement Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dfcac-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="dfcac-142">Un domaine Windows sur des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="dfcac-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="dfcac-143">Un compte avec des objets d’autorisation toocreate hello machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="dfcac-143">An account with permission toocreate objects in hello Azure virtual machine.</span></span>
- <span data-ttu-id="dfcac-144">Un réseau virtuel Azure et un sous-réseau avec un espace d’adressage IP pour hello suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="dfcac-144">An Azure virtual network and subnet with sufficient IP address space for hello following components:</span></span>
   - <span data-ttu-id="dfcac-145">Les deux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="dfcac-145">Both virtual machines.</span></span>
   - <span data-ttu-id="dfcac-146">adresse IP de cluster Hello basculement.</span><span class="sxs-lookup"><span data-stu-id="dfcac-146">hello failover cluster IP address.</span></span>
   - <span data-ttu-id="dfcac-147">Une adresse IP pour chaque instance de cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="dfcac-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="dfcac-148">DNS configuré sur le réseau Azure, pointant vers les contrôleurs de domaine toohello de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-148">DNS configured on hello Azure Network, pointing toohello domain controllers.</span></span>

<span data-ttu-id="dfcac-149">Une fois ces conditions préalables en place, vous pouvez passer à la création de votre cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="dfcac-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="dfcac-150">première étape de Hello est toocreate hello virtual machines.</span><span class="sxs-lookup"><span data-stu-id="dfcac-150">hello first step is toocreate hello virtual machines.</span></span>

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="dfcac-151">Étape 1 : Créer les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="dfcac-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="dfcac-152">Connectez-vous à toohello [portail Azure](http://portal.azure.com) avec votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="dfcac-152">Log in toohello [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="dfcac-153">[Créez un groupe à haute disponibilité Azure](../tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="dfcac-153">[Create an Azure availability set](../tutorial-availability-sets.md).</span></span>

   <span data-ttu-id="dfcac-154">disponibilité de Hello définis regroupe des machines virtuelles entre les domaines d’erreur et domaines de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="dfcac-154">hello availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="dfcac-155">Bonjour à haute disponibilité permet de s’assurer que votre application n’est pas affectée par des points uniques de panne, comme le commutateur de réseau hello ou unité d’alimentation de hello d’un rack de serveurs.</span><span class="sxs-lookup"><span data-stu-id="dfcac-155">hello availability set makes sure that your application is not affected by single points of failure, like hello network switch or hello power unit of a rack of servers.</span></span>

   <span data-ttu-id="dfcac-156">Si vous n'avez pas créé le groupe de ressources hello pour vos machines virtuelles, le faire lorsque vous créez un groupe à haute disponibilité Azure.</span><span class="sxs-lookup"><span data-stu-id="dfcac-156">If you have not created hello resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="dfcac-157">Si vous utilisez un ensemble de disponibilité hello hello toocreate portail Azure, procédez comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dfcac-157">If you're using hello Azure portal toocreate hello availability set, do hello following steps:</span></span>

   - <span data-ttu-id="dfcac-158">Bonjour portail Azure, cliquez sur  **+**  tooopen hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="dfcac-158">In hello Azure portal, click **+** tooopen hello Azure Marketplace.</span></span> <span data-ttu-id="dfcac-159">Recherchez **Groupe à haute disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="dfcac-160">Cliquez sur **Groupe à haute disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="dfcac-161">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-161">Click **Create**.</span></span>
   - <span data-ttu-id="dfcac-162">Sur hello **créer le groupe à haute disponibilité** panneau, hello du jeu de valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="dfcac-162">On hello **Create availability set** blade, set hello following values:</span></span>
      - <span data-ttu-id="dfcac-163">**Nom**: un nom pour le groupe à haute disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-163">**Name**: A name for hello availability set.</span></span>
      - <span data-ttu-id="dfcac-164">**Abonnement** : votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="dfcac-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="dfcac-165">**Groupe de ressources**: Si vous souhaitez toouse un groupe existant, cliquez sur **utiliser l’existante** et groupe hello select à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-165">**Resource group**: If you want toouse an existing group, click **Use existing** and select hello group from hello drop-down list.</span></span> <span data-ttu-id="dfcac-166">Sinon choisissez **créer un nouveau** et tapez un nom pour le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-166">Otherwise choose **Create New** and type a name for hello group.</span></span>
      - <span data-ttu-id="dfcac-167">**Emplacement**: définir l’emplacement de hello où vous prévoyez de toocreate vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="dfcac-167">**Location**: Set hello location where you plan toocreate your virtual machines.</span></span>
      - <span data-ttu-id="dfcac-168">**Domaines d’erreur**: hello par défaut (3).</span><span class="sxs-lookup"><span data-stu-id="dfcac-168">**Fault domains**: Use hello default (3).</span></span>
      - <span data-ttu-id="dfcac-169">**Mettre à jour des domaines**: hello par défaut (5).</span><span class="sxs-lookup"><span data-stu-id="dfcac-169">**Update domains**: Use hello default (5).</span></span>
   - <span data-ttu-id="dfcac-170">Cliquez sur **créer** toocreate hello à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="dfcac-170">Click **Create** toocreate hello availability set.</span></span>

1. <span data-ttu-id="dfcac-171">Créer des machines virtuelles de hello dans hello à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="dfcac-171">Create hello virtual machines in hello availability set.</span></span>

   <span data-ttu-id="dfcac-172">Configurez deux ordinateurs virtuels SQL Server à haute disponibilité Azure hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-172">Provision two SQL Server virtual machines in hello Azure availability set.</span></span> <span data-ttu-id="dfcac-173">Pour obtenir des instructions, consultez [configurer un ordinateur virtuel de SQL Server Bonjour Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="dfcac-173">For instructions, see [Provision a SQL Server virtual machine in hello Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

   <span data-ttu-id="dfcac-174">Placez les deux machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="dfcac-174">Place both virtual machines:</span></span>

   - <span data-ttu-id="dfcac-175">Bonjour le même groupe de ressources Azure votre groupe à haute disponibilité est dans.</span><span class="sxs-lookup"><span data-stu-id="dfcac-175">In hello same Azure resource group that your availability set is in.</span></span>
   - <span data-ttu-id="dfcac-176">Sur le même réseau que votre contrôleur de domaine de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-176">On hello same network as your domain controller.</span></span>
   - <span data-ttu-id="dfcac-177">Sur un sous-réseau avec un espace d’adressage IP suffisant pour les deux machines virtuelles et toutes les instances de cluster de basculement que vous pourriez utiliser sur ce cluster.</span><span class="sxs-lookup"><span data-stu-id="dfcac-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span>
   - <span data-ttu-id="dfcac-178">Dans le groupe à haute disponibilité Azure hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-178">In hello Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="dfcac-179">Vous ne pouvez pas définir ni modifier un groupe à haute disponibilité après la création d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dfcac-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="dfcac-180">Choisir une image de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="dfcac-180">Choose an image from hello Azure Marketplace.</span></span> <span data-ttu-id="dfcac-181">Vous pouvez utiliser un Marketplace image avec qui inclut Windows Server et SQL Server ou simplement hello Windows Server.</span><span class="sxs-lookup"><span data-stu-id="dfcac-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just hello Windows Server.</span></span> <span data-ttu-id="dfcac-182">Pour plus d’informations, consultez [Présentation de SQL Server sur les machines virtuelles Azure](../../virtual-machines-windows-sql-server-iaas-overview.md)</span><span class="sxs-lookup"><span data-stu-id="dfcac-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>

   <span data-ttu-id="dfcac-183">les images SQL Server officiels Hello Bonjour galerie Azure incluent une instance installée de SQL Server, ainsi que le logiciel d’installation de SQL Server de hello et la clé de requis de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-183">hello official SQL Server images in hello Azure Gallery include an installed SQL Server instance, plus hello SQL Server installation software, and hello required key.</span></span>

   <span data-ttu-id="dfcac-184">Choisissez l’image de droite hello selon toohow que vous souhaitez toopay de licence de SQL Server hello :</span><span class="sxs-lookup"><span data-stu-id="dfcac-184">Choose hello right image according toohow you want toopay for hello SQL Server license:</span></span>

   - <span data-ttu-id="dfcac-185">**Payer par le Gestionnaire de licences d’utilisation**: coût par minute de hello de ces images inclut hello licences de SQL Server :</span><span class="sxs-lookup"><span data-stu-id="dfcac-185">**Pay per usage licensing**: hello per-minute cost of these images includes hello SQL Server licensing:</span></span>
      - <span data-ttu-id="dfcac-186">**SQL Server 2016 Enterprise sur Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="dfcac-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="dfcac-187">**SQL Server 2016 Standard sur Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="dfcac-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="dfcac-188">**SQL Server 2016 Developer sur Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="dfcac-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>

   - <span data-ttu-id="dfcac-189">**BYOL (apportez votre propre licence)**</span><span class="sxs-lookup"><span data-stu-id="dfcac-189">**Bring-your-own-license (BYOL)**</span></span>

      - <span data-ttu-id="dfcac-190">**{BYOL} SQL Server 2016 Enterprise sur Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="dfcac-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="dfcac-191">**{BYOL} SQL Server 2016 Standard sur Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="dfcac-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="dfcac-192">Après avoir créé la machine virtuelle de hello, supprimer l’instance de SQL Server autonome préinstallées hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-192">After you create hello virtual machine, remove hello pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="dfcac-193">Vous allez utiliser hello préinstallées SQL Server Support toocreate hello ICF de SQL Server après avoir configuré le cluster de basculement hello et S2D.</span><span class="sxs-lookup"><span data-stu-id="dfcac-193">You will use hello pre-installed SQL Server media toocreate hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span>

   <span data-ttu-id="dfcac-194">Ou bien, vous pouvez utiliser images Azure Marketplace avec uniquement les systèmes d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-194">Alternatively, you can use Azure Marketplace images with just hello operating system.</span></span> <span data-ttu-id="dfcac-195">Choisissez un **Windows Server 2016 Datacenter** de l’image et installer hello ICF de SQL Server après avoir configuré le cluster de basculement hello et S2D.</span><span class="sxs-lookup"><span data-stu-id="dfcac-195">Choose a **Windows Server 2016 Datacenter** image and install hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span> <span data-ttu-id="dfcac-196">Cette image ne contient aucun support d’installation SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dfcac-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="dfcac-197">Placez le support d’installation hello dans un emplacement où vous pouvez exécuter l’installation de SQL Server hello pour chaque serveur.</span><span class="sxs-lookup"><span data-stu-id="dfcac-197">Place hello installation media in a location where you can run hello SQL Server installation for each server.</span></span>

1. <span data-ttu-id="dfcac-198">Une fois Azure crée vos machines virtuelles, connectez tooeach virtual machine à RDP.</span><span class="sxs-lookup"><span data-stu-id="dfcac-198">After Azure creates your virtual machines, connect tooeach virtual machine with RDP.</span></span>

   <span data-ttu-id="dfcac-199">Lorsque vous vous connectez premier ordinateur virtuel de tooa avec RDP, ordinateur de hello vous demande si vous tooallow cette toobe PC détectable sur le réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-199">When you first connect tooa virtual machine with RDP, hello computer asks if you want tooallow this PC toobe discoverable on hello network.</span></span> <span data-ttu-id="dfcac-200">Cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-200">Click **Yes**.</span></span>

1. <span data-ttu-id="dfcac-201">Si vous utilisez une des images de machine virtuelle SQL Server hello, supprimez l’instance de SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-201">If you are using one of hello SQL Server-based virtual machine images, remove hello SQL Server instance.</span></span>

   - <span data-ttu-id="dfcac-202">Dans **Programmes et fonctionnalités**, cliquez avec le bouton droit sur **Microsoft SQL Server 2016 (64 bits)** et sur **Désinstaller/modifier**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span>
   - <span data-ttu-id="dfcac-203">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-203">Click **Remove**.</span></span>
   - <span data-ttu-id="dfcac-204">Sélectionnez l’instance par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-204">Select hello default instance.</span></span>
   - <span data-ttu-id="dfcac-205">Supprimer toutes les fonctionnalités sous **Services Moteur de base de données**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="dfcac-206">Ne supprimez pas les **Fonctionnalités partagées**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="dfcac-207">Consultez hello illustration suivante :</span><span class="sxs-lookup"><span data-stu-id="dfcac-207">See hello following picture:</span></span>

      ![Supprimer des fonctionnalités](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="dfcac-209">Cliquez sur **Suivant**, puis sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-209">Click **Next**, and then click **Remove**.</span></span>

1. <span data-ttu-id="dfcac-210"><a name="ports"></a>Ouvrir les ports du pare-feu hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-210"><a name="ports"></a>Open hello firewall ports.</span></span>

   <span data-ttu-id="dfcac-211">Sur chaque ordinateur virtuel, ouvrez hello suivant des ports de hello le pare-feu Windows.</span><span class="sxs-lookup"><span data-stu-id="dfcac-211">On each virtual machine, open hello following ports on hello Windows Firewall.</span></span>

   | <span data-ttu-id="dfcac-212">Objectif</span><span class="sxs-lookup"><span data-stu-id="dfcac-212">Purpose</span></span> | <span data-ttu-id="dfcac-213">Port TCP</span><span class="sxs-lookup"><span data-stu-id="dfcac-213">TCP Port</span></span> | <span data-ttu-id="dfcac-214">Remarques</span><span class="sxs-lookup"><span data-stu-id="dfcac-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="dfcac-215">SQL Server</span><span class="sxs-lookup"><span data-stu-id="dfcac-215">SQL Server</span></span> | <span data-ttu-id="dfcac-216">1433</span><span class="sxs-lookup"><span data-stu-id="dfcac-216">1433</span></span> | <span data-ttu-id="dfcac-217">Port normal pour les instances par défaut de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dfcac-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="dfcac-218">Si vous avez utilisé une image à partir de la galerie de hello, ce port est ouvert automatiquement.</span><span class="sxs-lookup"><span data-stu-id="dfcac-218">If you used an image from hello gallery, this port is automatically opened.</span></span>
   | <span data-ttu-id="dfcac-219">Sonde d’intégrité</span><span class="sxs-lookup"><span data-stu-id="dfcac-219">Health probe</span></span> | <span data-ttu-id="dfcac-220">59999</span><span class="sxs-lookup"><span data-stu-id="dfcac-220">59999</span></span> | <span data-ttu-id="dfcac-221">Tout port TCP ouvert.</span><span class="sxs-lookup"><span data-stu-id="dfcac-221">Any open TCP port.</span></span> <span data-ttu-id="dfcac-222">Dans une étape ultérieure, configurer l’équilibrage de charge hello [sonde d’intégrité](#probe) et hello cluster toouse ce port.</span><span class="sxs-lookup"><span data-stu-id="dfcac-222">In a later step, configure hello load balancer [health probe](#probe) and hello cluster toouse this port.</span></span>  

1. <span data-ttu-id="dfcac-223">Ajouter la machine virtuelle de toohello stockage.</span><span class="sxs-lookup"><span data-stu-id="dfcac-223">Add storage toohello virtual machine.</span></span> <span data-ttu-id="dfcac-224">Pour plus d’informations, consultez [Ajouter du stockage](../../../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="dfcac-224">For detailed information, see [add storage](../../../storage/common/storage-premium-storage.md).</span></span>

   <span data-ttu-id="dfcac-225">Les deux machines virtuelles ont besoin d’au moins deux disques de données.</span><span class="sxs-lookup"><span data-stu-id="dfcac-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="dfcac-226">Attachez des disques bruts, et non des disques au format NTFS.</span><span class="sxs-lookup"><span data-stu-id="dfcac-226">Attach raw disks - not NTFS formatted disks.</span></span>
      >[!NOTE]
      ><span data-ttu-id="dfcac-227">Si vous attachez des disques au format NTFS, vous pouvez uniquement activer la technologie S2D sans vérification d’éligibilité de disque.</span><span class="sxs-lookup"><span data-stu-id="dfcac-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  

   <span data-ttu-id="dfcac-228">Attacher un minimum de deux Premium stockage (disques SSD) tooeach machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dfcac-228">Attach a minimum of two Premium Storage (SSD disks) tooeach VM.</span></span> <span data-ttu-id="dfcac-229">Nous vous recommandons d’utiliser au minimum des disques P30 (1 To).</span><span class="sxs-lookup"><span data-stu-id="dfcac-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="dfcac-230">Hôte de jeu de mise en cache trop**en lecture seule**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-230">Set host caching too**Read-only**.</span></span>

   <span data-ttu-id="dfcac-231">capacité de stockage Hello dans des environnements de production dépend de votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="dfcac-231">hello storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="dfcac-232">les valeurs Hello décrites dans cet article sont de démonstration et de test.</span><span class="sxs-lookup"><span data-stu-id="dfcac-232">hello values described in this article are for demonstration and testing.</span></span>

1. <span data-ttu-id="dfcac-233">[Ajouter un domaine existant de hello machines virtuelles tooyour](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="dfcac-233">[Add hello virtual machines tooyour pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="dfcac-234">Une fois hello virtuels sont créés et configurés, vous pouvez configurer le cluster de basculement hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-234">After hello virtual machines are created and configured, you can configure hello failover cluster.</span></span>

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a><span data-ttu-id="dfcac-235">Étape 2 : Configurer hello Cluster de basculement Windows avec S2D</span><span class="sxs-lookup"><span data-stu-id="dfcac-235">Step 2: Configure hello Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="dfcac-236">étape suivante de Hello est un cluster de basculement tooconfigure hello avec S2D.</span><span class="sxs-lookup"><span data-stu-id="dfcac-236">hello next step is tooconfigure hello failover cluster with S2D.</span></span> <span data-ttu-id="dfcac-237">Dans cette étape, vous ferez hello en suivant les étapes :</span><span class="sxs-lookup"><span data-stu-id="dfcac-237">In this step, you will do hello following substeps:</span></span>

1. <span data-ttu-id="dfcac-238">Ajouter la fonctionnalité Windows de Clustering de basculement</span><span class="sxs-lookup"><span data-stu-id="dfcac-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="dfcac-239">Validez le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="dfcac-239">Validate hello cluster</span></span>
1. <span data-ttu-id="dfcac-240">Créer le cluster de basculement hello</span><span class="sxs-lookup"><span data-stu-id="dfcac-240">Create hello failover cluster</span></span>
1. <span data-ttu-id="dfcac-241">Créer le témoin de cloud hello</span><span class="sxs-lookup"><span data-stu-id="dfcac-241">Create hello cloud witness</span></span>
1. <span data-ttu-id="dfcac-242">Ajouter du stockage</span><span class="sxs-lookup"><span data-stu-id="dfcac-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="dfcac-243">Ajouter la fonctionnalité Windows de Clustering de basculement</span><span class="sxs-lookup"><span data-stu-id="dfcac-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="dfcac-244">toobegin, connecter la première machine virtuelle de toohello avec RDP à l’aide d’un compte de domaine qui est membre du groupe Administrateurs locaux et possède des objets de toocreate autorisations dans Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dfcac-244">toobegin, connect toohello first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions toocreate objects in Active Directory.</span></span> <span data-ttu-id="dfcac-245">Utilisez ce compte pour rest hello de configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-245">Use this account for hello rest of hello configuration.</span></span>

1. <span data-ttu-id="dfcac-246">[Ajouter le Clustering de basculement d’ordinateur virtuel tooeach fonctionnalité](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="dfcac-246">[Add Failover Clustering feature tooeach virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

   <span data-ttu-id="dfcac-247">fonctionnalité de Clustering de basculement tooinstall à partir de l’interface utilisateur, de hello hello comme suit sur les deux ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="dfcac-247">tooinstall Failover Clustering feature from hello UI, do hello following steps on both virtual machines.</span></span>
   - <span data-ttu-id="dfcac-248">Dans le **Gestionnaire de serveur**, cliquez sur **Gérer**, puis sur **Ajouter des rôles et fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span>
   - <span data-ttu-id="dfcac-249">Dans **Assistant Ajouter des rôles et fonctionnalités**, cliquez sur **suivant** jusqu'à ce que vous atteigniez trop**sélectionner des fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-249">In **Add Roles and Features Wizard**, click **Next** until you get too**Select Features**.</span></span>
   - <span data-ttu-id="dfcac-250">Dans **Sélectionner les fonctionnalités**, cliquez sur **Clustering de basculement**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="dfcac-251">Inclure toutes les fonctionnalités requises et les outils de gestion hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-251">Include all required features and hello management tools.</span></span> <span data-ttu-id="dfcac-252">Cliquez sur **Ajouter des fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="dfcac-253">Cliquez sur **suivant** puis cliquez sur **Terminer** fonctionnalités de hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="dfcac-253">Click **Next** and then click **Finish** tooinstall hello features.</span></span>

   <span data-ttu-id="dfcac-254">tooinstall hello fonctionnalité Clustering avec basculement avec PowerShell, exécutez hello suivant de script à partir d’une session PowerShell d’administrateur sur l’un des ordinateurs virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-254">tooinstall hello Failover Clustering feature with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="dfcac-255">Pour référence, les étapes suivantes hello suivent les instructions de hello sous l’étape 3 de [solution Hyper convergé à l’aide des espaces de stockage Direct dans Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="dfcac-255">For reference, hello next steps follow hello instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span>

### <a name="validate-hello-cluster"></a><span data-ttu-id="dfcac-256">Validez le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="dfcac-256">Validate hello cluster</span></span>

<span data-ttu-id="dfcac-257">Ce guide fait référence tooinstructions sous [validez le cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span><span class="sxs-lookup"><span data-stu-id="dfcac-257">This guide refers tooinstructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="dfcac-258">Valider le cluster hello dans l’interface utilisateur de hello ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dfcac-258">Validate hello cluster in hello UI or with PowerShell.</span></span>

<span data-ttu-id="dfcac-259">cluster de hello toovalidate avec hello l’interface utilisateur, procédez comme hello suivant les étapes de l’une des machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-259">toovalidate hello cluster with hello UI, do hello following steps from one of hello virtual machines.</span></span>

1. <span data-ttu-id="dfcac-260">Dans le **Gestionnaire de serveur**, cliquez sur **Outils**, puis cliquez sur **Gestionnaire du cluster de basculement**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span>
1. <span data-ttu-id="dfcac-261">Dans le **Gestionnaire du cluster de basculement**, cliquez sur **Action**, puis cliquez sur **Valider la configuration...**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="dfcac-262">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-262">Click **Next**.</span></span>
1. <span data-ttu-id="dfcac-263">Sur **sélectionner des serveurs ou un Cluster**, nom du type hello de deux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="dfcac-263">On **Select Servers or a Cluster**, type hello name of both virtual machines.</span></span>
1. <span data-ttu-id="dfcac-264">Sous **Options de test**, choisissez **Exécuter uniquement les tests que je sélectionne**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="dfcac-265">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-265">Click **Next**.</span></span>
1. <span data-ttu-id="dfcac-266">Sous **Sélection du test**, incluez tous les tests sauf **Stockage**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="dfcac-267">Consultez hello illustration suivante :</span><span class="sxs-lookup"><span data-stu-id="dfcac-267">See hello following picture:</span></span>

   ![Valider les tests](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. <span data-ttu-id="dfcac-269">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-269">Click **Next**.</span></span>
1. <span data-ttu-id="dfcac-270">Sous **Confirmation**, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-270">On **Confirmation**, click **Next**.</span></span>

<span data-ttu-id="dfcac-271">Hello **Assistant Validation d’une Configuration** séries hello des tests de validation.</span><span class="sxs-lookup"><span data-stu-id="dfcac-271">hello **Validate a Configuration Wizard** runs hello validation tests.</span></span>

<span data-ttu-id="dfcac-272">cluster de hello toovalidate avec PowerShell, exécutez hello suivant de script à partir d’une session PowerShell d’administrateur sur l’un des ordinateurs virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-272">toovalidate hello cluster with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="dfcac-273">Une fois que vous validez le cluster de hello, créez le cluster de basculement de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-273">After you validate hello cluster, create hello failover cluster.</span></span>

### <a name="create-hello-failover-cluster"></a><span data-ttu-id="dfcac-274">Créer le cluster de basculement hello</span><span class="sxs-lookup"><span data-stu-id="dfcac-274">Create hello failover cluster</span></span>

<span data-ttu-id="dfcac-275">Ce guide fait référence trop[créer un cluster de basculement hello](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span><span class="sxs-lookup"><span data-stu-id="dfcac-275">This guide refers too[Create hello failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="dfcac-276">cluster de basculement toocreate hello, vous devez :</span><span class="sxs-lookup"><span data-stu-id="dfcac-276">toocreate hello failover cluster, you need:</span></span>
- <span data-ttu-id="dfcac-277">les noms d’ordinateurs virtuels hello deviennent Hello hello des nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="dfcac-277">hello names of hello virtual machines that become hello cluster nodes.</span></span>
- <span data-ttu-id="dfcac-278">Un nom pour le cluster de basculement hello</span><span class="sxs-lookup"><span data-stu-id="dfcac-278">A name for hello failover cluster</span></span>
- <span data-ttu-id="dfcac-279">Une adresse IP de cluster de basculement hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-279">An IP address for hello failover cluster.</span></span> <span data-ttu-id="dfcac-280">Vous pouvez utiliser une adresse IP qui n’est pas utilisée sur hello même réseau virtuel Azure et sous-réseau hello des nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="dfcac-280">You can use an IP address that is not used on hello same Azure virtual network and subnet as hello cluster nodes.</span></span>

<span data-ttu-id="dfcac-281">Hello suivant PowerShell crée un cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="dfcac-281">hello following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="dfcac-282">Mettre à jour le script hello avec des noms de nœuds de hello (noms d’ordinateur virtuel hello) hello et une adresse IP disponible à partir de hello réseau virtuel Azure :</span><span class="sxs-lookup"><span data-stu-id="dfcac-282">Update hello script with hello names of hello nodes (hello virtual machine names) and an available IP address from hello Azure VNET:</span></span>

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="dfcac-283">Créer un témoin cloud</span><span class="sxs-lookup"><span data-stu-id="dfcac-283">Create a cloud witness</span></span>

<span data-ttu-id="dfcac-284">Un témoin cloud est un nouveau type de témoin de quorum de cluster stocké dans un Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="dfcac-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="dfcac-285">Cela supprime la nécessité de hello d’un ordinateur de virtuel distinct qui héberge un témoin de partage.</span><span class="sxs-lookup"><span data-stu-id="dfcac-285">This removes hello need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="dfcac-286">[Créer un témoin de cloud pour le cluster de basculement hello](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="dfcac-286">[Create a cloud witness for hello failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span>

1. <span data-ttu-id="dfcac-287">Créez un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="dfcac-287">Create a blob container.</span></span>

1. <span data-ttu-id="dfcac-288">Enregistrer les clés d’accès hello et URL du conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-288">Save hello access keys and hello container URL.</span></span>

1. <span data-ttu-id="dfcac-289">Configurer le témoin de quorum de cluster hello basculement cluster.</span><span class="sxs-lookup"><span data-stu-id="dfcac-289">Configure hello failover cluster cluster quorum witness.</span></span> <span data-ttu-id="dfcac-290">Consultez [configurer le témoin de quorum hello dans l’interface utilisateur hello]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) dans l’interface utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-290">See, [Configure hello quorum witness in hello user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in hello UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="dfcac-291">Ajouter du stockage</span><span class="sxs-lookup"><span data-stu-id="dfcac-291">Add storage</span></span>

<span data-ttu-id="dfcac-292">les disques de Hello pour S2D doivent toobe vide et sans partitions ou d’autres données.</span><span class="sxs-lookup"><span data-stu-id="dfcac-292">hello disks for S2D need toobe empty and without partitions or other data.</span></span> <span data-ttu-id="dfcac-293">suivent des disques de tooclean [hello les étapes de ce guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span><span class="sxs-lookup"><span data-stu-id="dfcac-293">tooclean disks follow [hello steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>

1. <span data-ttu-id="dfcac-294">[Activez les Espaces de stockage direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="dfcac-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="dfcac-295">Hello suivant PowerShell permet d’espaces de stockage directs.</span><span class="sxs-lookup"><span data-stu-id="dfcac-295">hello following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="dfcac-296">Dans **Gestionnaire du Cluster de basculement**, vous pouvez maintenant voir le pool de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-296">In **Failover Cluster Manager**, you can now see hello storage pool.</span></span>

1. <span data-ttu-id="dfcac-297">[Créez un volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span><span class="sxs-lookup"><span data-stu-id="dfcac-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="dfcac-298">Une des fonctionnalités de hello de S2D est qu’il crée automatiquement un pool de stockage lorsque vous l’activez.</span><span class="sxs-lookup"><span data-stu-id="dfcac-298">One of hello features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="dfcac-299">Vous êtes maintenant prêt toocreate un volume.</span><span class="sxs-lookup"><span data-stu-id="dfcac-299">You are now ready toocreate a volume.</span></span> <span data-ttu-id="dfcac-300">applet de commande PowerShell de Hello `New-Volume` automatise le processus de création de volume hello, y compris la mise en forme, l’ajout de toohello cluster et la création d’un volume partagé de cluster (CSV).</span><span class="sxs-lookup"><span data-stu-id="dfcac-300">hello PowerShell commandlet `New-Volume` automates hello volume creation process, including formatting, adding toohello cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="dfcac-301">Bonjour à l’exemple suivant crée un 800 Go CSV.</span><span class="sxs-lookup"><span data-stu-id="dfcac-301">hello following example creates an 800 gigabyte (GB) CSV.</span></span>

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="dfcac-302">Une fois cette commande terminée, un volume de 800 Go est monté en tant que ressource du cluster.</span><span class="sxs-lookup"><span data-stu-id="dfcac-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="dfcac-303">volume de Hello est à `C:\ClusterStorage\Volume1\`.</span><span class="sxs-lookup"><span data-stu-id="dfcac-303">hello volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="dfcac-304">Hello suivant schéma montre un volume partagé de cluster avec S2D :</span><span class="sxs-lookup"><span data-stu-id="dfcac-304">hello following diagram shows a cluster shared volume with S2D:</span></span>

   ![VolumePartagéCluster](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="dfcac-306">Étape 3 : Tester le basculement du cluster de basculement</span><span class="sxs-lookup"><span data-stu-id="dfcac-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="dfcac-307">Dans le Gestionnaire de Cluster de basculement, vérifiez que vous pouvez déplacer toohello de ressource de stockage hello autre nœud de cluster.</span><span class="sxs-lookup"><span data-stu-id="dfcac-307">In Failover Cluster Manager, verify that you can move hello storage resource toohello other cluster node.</span></span> <span data-ttu-id="dfcac-308">Si vous pouvez vous connecter toohello basculement de cluster avec **Gestionnaire du Cluster de basculement** et déplacer le stockage hello d’un nœud toohello autres, vous êtes prêt tooconfigure hello FCI.</span><span class="sxs-lookup"><span data-stu-id="dfcac-308">If you can connect toohello failover cluster with **Failover Cluster Manager** and move hello storage from one node toohello other, you are ready tooconfigure hello FCI.</span></span>

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="dfcac-309">Étape 4 : Créer l’instance de cluster de basculement SQL Server</span><span class="sxs-lookup"><span data-stu-id="dfcac-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="dfcac-310">Une fois que vous avez configuré le cluster de basculement hello et tous les composants de cluster, y compris le stockage, vous pouvez créer hello ICF de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dfcac-310">After you have configured hello failover cluster and all cluster components including storage, you can create hello SQL Server FCI.</span></span>

1. <span data-ttu-id="dfcac-311">Connectez la première machine virtuelle de toohello à RDP.</span><span class="sxs-lookup"><span data-stu-id="dfcac-311">Connect toohello first virtual machine with RDP.</span></span>

1. <span data-ttu-id="dfcac-312">Dans **Gestionnaire du Cluster de basculement**, assurez-vous que toutes les ressources principales du cluster se trouvent sur le premier ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-312">In **Failover Cluster Manager**, make sure all cluster core resources are on hello first virtual machine.</span></span> <span data-ttu-id="dfcac-313">Si nécessaire, déplacez l’ordinateur virtuel de toothis toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="dfcac-313">If necessary, move all resources toothis virtual machine.</span></span>

1. <span data-ttu-id="dfcac-314">Recherchez le support d’installation hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-314">Locate hello installation media.</span></span> <span data-ttu-id="dfcac-315">Si la machine virtuelle de hello utilise l’une des images d’Azure Marketplace hello, support de hello est situé à `C:\SQLServer_<version number>_Full`.</span><span class="sxs-lookup"><span data-stu-id="dfcac-315">If hello virtual machine uses one of hello Azure Marketplace images, hello media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="dfcac-316">Cliquez sur **Setup**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-316">Click **Setup**.</span></span>

1. <span data-ttu-id="dfcac-317">Bonjour **centre d’Installation SQL Server**, cliquez sur **Installation**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-317">In hello **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="dfcac-318">Cliquez sur **Installation d’un nouveau cluster de basculement SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="dfcac-319">Suivez les instructions de hello Bonjour de tooinstall Assistant hello ICF de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dfcac-319">Follow hello instructions in hello wizard tooinstall hello SQL Server FCI.</span></span>

   <span data-ttu-id="dfcac-320">répertoires de données Hello FCI doivent toobe sur le stockage en cluster.</span><span class="sxs-lookup"><span data-stu-id="dfcac-320">hello FCI data directories need toobe on clustered storage.</span></span> <span data-ttu-id="dfcac-321">Avec S2D, il n’est pas un disque partagé, mais un volume tooa de point de montage sur chaque serveur.</span><span class="sxs-lookup"><span data-stu-id="dfcac-321">With S2D, it's not a shared disk, but a mount point tooa volume on each server.</span></span> <span data-ttu-id="dfcac-322">S2D synchronise volume hello entre les deux nœuds.</span><span class="sxs-lookup"><span data-stu-id="dfcac-322">S2D synchronizes hello volume between both nodes.</span></span> <span data-ttu-id="dfcac-323">volume de Hello est présentée toohello cluster comme un volume partagé de cluster.</span><span class="sxs-lookup"><span data-stu-id="dfcac-323">hello volume is presented toohello cluster as a cluster shared volume.</span></span> <span data-ttu-id="dfcac-324">Utilisez le point de montage de volume partagé de cluster hello pour les répertoires de données hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-324">Use hello CSV mount point for hello data directories.</span></span>

   ![RépertoiresDonnées](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="dfcac-326">Au terme de l’Assistant de hello, installe une instance de cluster SQL Server sur le premier nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-326">After you complete hello wizard, Setup will install a SQL Server FCI on hello first node.</span></span>

1. <span data-ttu-id="dfcac-327">Une fois que le programme d’installation installe correctement hello ICF sur le premier nœud de hello, connectez toohello second nœud à RDP.</span><span class="sxs-lookup"><span data-stu-id="dfcac-327">After Setup successfully installs hello FCI on hello first node, connect toohello second node with RDP.</span></span>

1. <span data-ttu-id="dfcac-328">Ouvrez hello **centre d’Installation SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-328">Open hello **SQL Server Installation Center**.</span></span> <span data-ttu-id="dfcac-329">Cliquez sur **Installation**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-329">Click **Installation**.</span></span>

1. <span data-ttu-id="dfcac-330">Cliquez sur **cluster de basculement SQL Server ajouter nœud tooa**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-330">Click **Add node tooa SQL Server failover cluster**.</span></span> <span data-ttu-id="dfcac-331">Suivez les instructions de hello de hello Assistant tooinstall SQL server, puis ajouter cette toohello serveur FCI.</span><span class="sxs-lookup"><span data-stu-id="dfcac-331">Follow hello instructions in hello wizard tooinstall SQL server and add this server toohello FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="dfcac-332">Si vous avez utilisé une image de la galerie Azure Marketplace avec SQL Server, outils de SQL Server ont été inclus avec l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with hello image.</span></span> <span data-ttu-id="dfcac-333">Si vous n’utilisez pas cette image, installez les outils de SQL Server hello séparément.</span><span class="sxs-lookup"><span data-stu-id="dfcac-333">If you did not use this image, install hello SQL Server tools separately.</span></span> <span data-ttu-id="dfcac-334">Consultez [Télécharger SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfcac-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="dfcac-335">Étape 5 : Créer un équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="dfcac-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="dfcac-336">Sur les machines virtuelles Azure, les clusters utilisent un toohold d’équilibrage de charge une adresse IP qui doit toobe sur un nœud de cluster à la fois.</span><span class="sxs-lookup"><span data-stu-id="dfcac-336">On Azure virtual machines, clusters use a load balancer toohold an IP address that needs toobe on one cluster node at a time.</span></span> <span data-ttu-id="dfcac-337">Dans cette solution, équilibrage de charge hello conserve adresse IP hello hello ICF de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dfcac-337">In this solution, hello load balancer holds hello IP address for hello SQL Server FCI.</span></span>

<span data-ttu-id="dfcac-338">[Créez et configurez un équilibrage de charge Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="dfcac-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="dfcac-339">Créer un équilibreur de charge hello Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="dfcac-339">Create hello load balancer in hello Azure portal</span></span>

<span data-ttu-id="dfcac-340">équilibrage de charge toocreate hello :</span><span class="sxs-lookup"><span data-stu-id="dfcac-340">toocreate hello load balancer:</span></span>

1. <span data-ttu-id="dfcac-341">Bonjour portail Azure, accédez à toohello groupe de ressources avec des machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-341">In hello Azure portal, go toohello Resource Group with hello virtual machines.</span></span>

1. <span data-ttu-id="dfcac-342">Cliquez sur **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-342">Click **+ Add**.</span></span> <span data-ttu-id="dfcac-343">Hello de recherche Marketplace pour **équilibrage de charge**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-343">Search hello Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="dfcac-344">Cliquez sur **Équilibrage de charge**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="dfcac-345">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-345">Click **Create**.</span></span>

1. <span data-ttu-id="dfcac-346">Configurer l’équilibrage de charge hello avec :</span><span class="sxs-lookup"><span data-stu-id="dfcac-346">Configure hello load balancer with:</span></span>

   - <span data-ttu-id="dfcac-347">**Nom**: un nom qui identifie l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-347">**Name**: A name that identifies hello load balancer.</span></span>
   - <span data-ttu-id="dfcac-348">**Type**: équilibrage de charge hello peut être public ou privé.</span><span class="sxs-lookup"><span data-stu-id="dfcac-348">**Type**: hello load balancer can be either public or private.</span></span> <span data-ttu-id="dfcac-349">Est accessible à partir d’un équilibreur de charge privé hello même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="dfcac-349">A private load balancer can be accessed from within hello same VNET.</span></span> <span data-ttu-id="dfcac-350">La plupart des applications Azure peut utiliser un équilibrage de charge privé.</span><span class="sxs-lookup"><span data-stu-id="dfcac-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="dfcac-351">Si votre application requiert un accès tooSQL Server directement via hello Internet, utilisez un équilibreur de charge public.</span><span class="sxs-lookup"><span data-stu-id="dfcac-351">If your application needs access tooSQL Server directly over hello Internet, use a public load balancer.</span></span>
   - <span data-ttu-id="dfcac-352">**Réseau virtuel**: hello même réseau que les machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-352">**Virtual Network**: hello same network as hello virtual machines.</span></span>
   - <span data-ttu-id="dfcac-353">**Sous-réseau**: hello même sous-réseau que les ordinateurs virtuels de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-353">**Subnet**: hello same subnet as hello virtual machines.</span></span>
   - <span data-ttu-id="dfcac-354">**Adresse IP privée**: hello la même adresse IP que vous avez affecté toohello SQL Server FCI réseau du cluster.</span><span class="sxs-lookup"><span data-stu-id="dfcac-354">**Private IP address**: hello same IP address that you assigned toohello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="dfcac-355">**Abonnement** : votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="dfcac-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="dfcac-356">**Groupe de ressources**: utilisez hello même groupe de ressources que vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="dfcac-356">**Resource Group**: Use hello same resource group as your virtual machines.</span></span>
   - <span data-ttu-id="dfcac-357">**Emplacement**: utilisez hello même emplacement que celui de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="dfcac-357">**Location**: Use hello same Azure location as your virtual machines.</span></span>
   <span data-ttu-id="dfcac-358">Consultez hello illustration suivante :</span><span class="sxs-lookup"><span data-stu-id="dfcac-358">See hello following picture:</span></span>

   ![CréerÉquilibrageCharge](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a><span data-ttu-id="dfcac-360">Configurer le pool principal d’équilibrage de charge hello</span><span class="sxs-lookup"><span data-stu-id="dfcac-360">Configure hello load balancer backend pool</span></span>

1. <span data-ttu-id="dfcac-361">Retourner toohello groupe de ressources Azure avec des machines virtuelles de hello et localiser un équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-361">Return toohello Azure Resource Group with hello virtual machines and locate hello new load balancer.</span></span> <span data-ttu-id="dfcac-362">Vous pouvez avoir toorefresh hello vue sur hello groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="dfcac-362">You may have toorefresh hello view on hello Resource Group.</span></span> <span data-ttu-id="dfcac-363">Cliquez sur le programme d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-363">Click hello load balancer.</span></span>

1. <span data-ttu-id="dfcac-364">Dans le panneau de programme d’équilibrage de charge hello, cliquez sur **pools principaux**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-364">On hello load balancer blade, click **Backend pools**.</span></span>

1. <span data-ttu-id="dfcac-365">Cliquez sur **+ ajouter** tooadd un pool principal.</span><span class="sxs-lookup"><span data-stu-id="dfcac-365">Click **+ Add** tooadd a backend pool.</span></span>

1. <span data-ttu-id="dfcac-366">Tapez un nom pour le pool principal d’hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-366">Type a name for hello backend pool.</span></span>

1. <span data-ttu-id="dfcac-367">Cliquez sur **Ajouter une machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="dfcac-368">Sur hello **choisir les machines virtuelles** panneau, cliquez sur **choisir un ensemble de disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-368">On hello **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="dfcac-369">Choisissez que vous avez placé virtuels hello SQL Server dans un ensemble de disponibilité de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-369">Choose hello availability set that you placed hello SQL Server virtual machines in.</span></span>

1. <span data-ttu-id="dfcac-370">Sur hello **choisir les machines virtuelles** panneau, cliquez sur **choisissez hello virtuels**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-370">On hello **Choose virtual machines** blade, click **Choose hello virtual machines**.</span></span>

   <span data-ttu-id="dfcac-371">Votre portail Azure doit ressembler à hello illustration suivante :</span><span class="sxs-lookup"><span data-stu-id="dfcac-371">Your Azure portal should look like hello following picture:</span></span>

   ![CréerPoolPrincipalÉquilibrageCharge](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="dfcac-373">Cliquez sur **sélectionnez** sur hello **choisir les machines virtuelles** panneau.</span><span class="sxs-lookup"><span data-stu-id="dfcac-373">Click **Select** on hello **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="dfcac-374">Cliquez sur **OK** deux fois.</span><span class="sxs-lookup"><span data-stu-id="dfcac-374">Click **OK** twice.</span></span>

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="dfcac-375">Configurer une sonde d’intégrité d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="dfcac-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="dfcac-376">Dans le panneau de programme d’équilibrage de charge hello, cliquez sur **sondes d’intégrité**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-376">On hello load balancer blade, click **Health probes**.</span></span>

1. <span data-ttu-id="dfcac-377">Cliquez sur **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-377">Click **+ Add**.</span></span>

1. <span data-ttu-id="dfcac-378">Sur hello **sonde d’intégrité ajouter** panneau, <a name="probe"> </a>définir les paramètres de sonde d’intégrité hello :</span><span class="sxs-lookup"><span data-stu-id="dfcac-378">On hello **Add health probe** blade, <a name="probe"></a>Set hello health probe parameters:</span></span>

   - <span data-ttu-id="dfcac-379">**Nom**: un nom pour la sonde d’intégrité hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-379">**Name**: A name for hello health probe.</span></span>
   - <span data-ttu-id="dfcac-380">**Protocole** : TCP.</span><span class="sxs-lookup"><span data-stu-id="dfcac-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="dfcac-381">**Port**: définissez tooan port TCP disponible.</span><span class="sxs-lookup"><span data-stu-id="dfcac-381">**Port**: Set tooan available TCP port.</span></span> <span data-ttu-id="dfcac-382">Ce port nécessite un port de pare-feu ouvert.</span><span class="sxs-lookup"><span data-stu-id="dfcac-382">This port requires an open firewall port.</span></span> <span data-ttu-id="dfcac-383">Hello d’utilisation [même port](#ports) vous définissez pour la sonde d’intégrité hello au pare-feu de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-383">Use hello [same port](#ports) you set for hello health probe at hello firewall.</span></span>
   - <span data-ttu-id="dfcac-384">**Intervalle** : 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="dfcac-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="dfcac-385">**Seuil de défaillance** : 2 défaillances consécutives.</span><span class="sxs-lookup"><span data-stu-id="dfcac-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="dfcac-386">Cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="dfcac-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="dfcac-387">Définir les règles d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="dfcac-387">Set load balancing rules</span></span>

1. <span data-ttu-id="dfcac-388">Dans le panneau de programme d’équilibrage de charge hello, cliquez sur **règles d’équilibrage de charge**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-388">On hello load balancer blade, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="dfcac-389">Cliquez sur **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="dfcac-390">Définir des paramètres de règles équilibrage hello charge :</span><span class="sxs-lookup"><span data-stu-id="dfcac-390">Set hello load balancing rules parameters:</span></span>

   - <span data-ttu-id="dfcac-391">**Nom**: un nom pour les règles d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-391">**Name**: A name for hello load balancing rules.</span></span>
   - <span data-ttu-id="dfcac-392">**Adresse IP de Frontend**: utiliser d’adresse IP de hello pour hello ressource réseau de clusters SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="dfcac-392">**Frontend IP address**: Use hello IP address for hello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="dfcac-393">**Port**: définie pour hello port TCP d’instance de cluster de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dfcac-393">**Port**: Set for hello SQL Server FCI TCP port.</span></span> <span data-ttu-id="dfcac-394">port d’instance Hello par défaut est 1433.</span><span class="sxs-lookup"><span data-stu-id="dfcac-394">hello default instance port is 1433.</span></span>
   - <span data-ttu-id="dfcac-395">**Port principal**: cette valeur utilise hello même port que hello **Port** valeur lorsque vous activez **IP flottante (retour direct du serveur)**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-395">**Backend port**: This value uses hello same port as hello **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="dfcac-396">**Pool principal**: nom du pool utilisez hello principal que vous avez configuré précédemment.</span><span class="sxs-lookup"><span data-stu-id="dfcac-396">**Backend pool**: Use hello backend pool name that you configured earlier.</span></span>
   - <span data-ttu-id="dfcac-397">**Sonde d’intégrité**: sonde d’intégrité de hello utilisation que vous avez configuré précédemment.</span><span class="sxs-lookup"><span data-stu-id="dfcac-397">**Health probe**: Use hello health probe that you configured earlier.</span></span>
   - <span data-ttu-id="dfcac-398">**Persistance de session** : aucune.</span><span class="sxs-lookup"><span data-stu-id="dfcac-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="dfcac-399">**Délai d’inactivité (minutes)** : 4.</span><span class="sxs-lookup"><span data-stu-id="dfcac-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="dfcac-400">**Adresse IP flottante (retour serveur direct)** : activée</span><span class="sxs-lookup"><span data-stu-id="dfcac-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="dfcac-401">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-401">Click **OK**.</span></span>

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="dfcac-402">Étape 6 : Configurer le cluster pour la sonde</span><span class="sxs-lookup"><span data-stu-id="dfcac-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="dfcac-403">Définissez le paramètre de port de sonde de cluster hello dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dfcac-403">Set hello cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="dfcac-404">tooset hello du paramètre de port de sonde de cluster, mettre à jour des variables dans le script suivant à partir de votre environnement de hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-404">tooset hello cluster probe port parameter, update variables in hello following script from your environment.</span></span>

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="dfcac-405">Étape 7 : Test du basculement FCI</span><span class="sxs-lookup"><span data-stu-id="dfcac-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="dfcac-406">Testez le basculement de hello la fonctionnalité cluster toovalidate FCI.</span><span class="sxs-lookup"><span data-stu-id="dfcac-406">Test failover of hello FCI toovalidate cluster functionality.</span></span> <span data-ttu-id="dfcac-407">Hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dfcac-407">Do hello following steps:</span></span>

1. <span data-ttu-id="dfcac-408">Se connecter tooone des nœuds de cluster de SQL Server FCI hello à RDP.</span><span class="sxs-lookup"><span data-stu-id="dfcac-408">Connect tooone of hello SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="dfcac-409">Ouvrez le **Gestionnaire du cluster de basculement**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="dfcac-410">Cliquez sur **Rôles**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-410">Click **Roles**.</span></span> <span data-ttu-id="dfcac-411">Notez le nœud qui possède le rôle de SQL Server FCI hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-411">Notice which node owns hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="dfcac-412">Cliquez sur le rôle de SQL Server FCI hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-412">Right-click hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="dfcac-413">Cliquez sur **Déplacer** et sur **Meilleur nœud possible**.</span><span class="sxs-lookup"><span data-stu-id="dfcac-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="dfcac-414">**Gestionnaire du Cluster de basculement** affiche hello rôle et ses ressources hors ligne.</span><span class="sxs-lookup"><span data-stu-id="dfcac-414">**Failover Cluster Manager** shows hello role and its resources go offline.</span></span> <span data-ttu-id="dfcac-415">Hello ressources ensuite déplacer et en ligne sur hello autre nœud.</span><span class="sxs-lookup"><span data-stu-id="dfcac-415">hello resources then move and come online on hello other node.</span></span>

### <a name="test-connectivity"></a><span data-ttu-id="dfcac-416">Tester la connectivité</span><span class="sxs-lookup"><span data-stu-id="dfcac-416">Test connectivity</span></span>

<span data-ttu-id="dfcac-417">connectivité tootest, journal de la machine virtuelle tooanother hello même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="dfcac-417">tootest connectivity, log in tooanother virtual machine in hello same virtual network.</span></span> <span data-ttu-id="dfcac-418">Ouvrez **SQL Server Management Studio** et nom d’instance de cluster de SQL Server toohello connect.</span><span class="sxs-lookup"><span data-stu-id="dfcac-418">Open **SQL Server Management Studio** and connect toohello SQL Server FCI name.</span></span>

>[!NOTE]
><span data-ttu-id="dfcac-419">Si nécessaire, vous pouvez [télécharger SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfcac-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="dfcac-420">Limites</span><span class="sxs-lookup"><span data-stu-id="dfcac-420">Limitations</span></span>
<span data-ttu-id="dfcac-421">Sur les machines virtuelles Azure, Microsoft Distributed Transaction Coordinator (DTC) n'est pas prise en charge sur les instances fci car hello port RPC n’est pas pris en charge par l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="dfcac-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because hello RPC port is not supported by hello load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="dfcac-422">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="dfcac-422">See Also</span></span>

[<span data-ttu-id="dfcac-423">Configurer S2D avec le Bureau à distance (Azure)</span><span class="sxs-lookup"><span data-stu-id="dfcac-423">Setup S2D with remote desktop (Azure)</span></span>](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

<span data-ttu-id="dfcac-424">[Solution hyper-convergée avec Espaces de stockage direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="dfcac-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

[<span data-ttu-id="dfcac-425">Vue d’ensemble de l’espace de stockage direct</span><span class="sxs-lookup"><span data-stu-id="dfcac-425">Storage Space Direct Overview</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[<span data-ttu-id="dfcac-426">Prise en charge de SQL Server pour S2D</span><span class="sxs-lookup"><span data-stu-id="dfcac-426">SQL Server support for S2D</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
