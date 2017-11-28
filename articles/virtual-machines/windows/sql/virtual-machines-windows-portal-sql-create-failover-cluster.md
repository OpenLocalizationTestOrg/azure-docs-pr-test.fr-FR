---
title: Instance de cluster de basculement (FCI) SQL Server - Machines virtuelles Azure | Microsoft Docs
description: "Cet article explique comment créer une instance de cluster de basculement SQL Server sur des machines virtuelles Azure."
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
ms.openlocfilehash: 439353b7d22fb7376049ea8e1433a8d5840d3e0f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="6a7ab-103">Configurer une instance de cluster de basculement SQL Server sur des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="6a7ab-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="6a7ab-104">Cet article explique comment créer une instance de cluster de basculement (FCI) SQL Server sur des machines virtuelles Azure dans le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-104">This article explains how to create a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="6a7ab-105">Cette solution utilise [l’édition Espaces de stockage direct \(S2D\) de Windows Server 2016 Datacenter](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) en tant que réseau SAN virtuel basé sur logiciel qui synchronise le stockage (disques de données) entre les nœuds (machines virtuelles Azure) dans un cluster Windows.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes the storage (data disks) between the nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="6a7ab-106">La technologie Espaces de stockage direct (S2D) est une nouveauté dans Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="6a7ab-107">Le schéma suivant illustre la solution complète sur les machines virtuelles Azure :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-107">The following diagram shows the complete solution on Azure virtual machines:</span></span>

![Groupe de disponibilité](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="6a7ab-109">Le schéma précédent illustre :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-109">The preceding diagram shows:</span></span>

- <span data-ttu-id="6a7ab-110">Deux machines virtuelles Azure dans un cluster de basculement Windows.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="6a7ab-111">Lorsqu’une machine virtuelle se trouve dans un cluster de basculement, elle est également désignée comme *nœud* ou *nœuds* de cluster.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="6a7ab-112">Chaque machine virtuelle possède au moins deux disques de données.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="6a7ab-113">La technologie S2D synchronise les données sur le disque de données et présente le stockage synchronisé en tant que pool de stockage.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-113">S2D synchronizes the data on the data disk and presents the synchronized storage as a storage pool.</span></span>
- <span data-ttu-id="6a7ab-114">Le pool de stockage présente un volume partagé de cluster au cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-114">The storage pool presents a cluster shared volume (CSV) to the failover cluster.</span></span>
- <span data-ttu-id="6a7ab-115">Le rôle du cluster de l’instance de cluster de basculement SQL Server utilise le volume partagé de cluster pour les lecteurs de données.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-115">The SQL Server FCI cluster role uses the CSV for the data drives.</span></span>
- <span data-ttu-id="6a7ab-116">Un équilibrage de charge Azure pour contenir l’adresse IP de l’instance de cluster de basculement SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-116">An Azure load balancer to hold the IP address for the SQL Server FCI.</span></span>
- <span data-ttu-id="6a7ab-117">Un groupe à haute disponibilité Azure contient toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-117">An Azure availability set holds all the resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="6a7ab-118">Toutes les ressources Azure dans le schéma se trouvent dans le même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-118">All Azure resources are in the diagram are in the same resource group.</span></span>

<span data-ttu-id="6a7ab-119">Pour plus d’informations sur la technologie S2D, consultez [l’édition Espaces de stockage direct \(S2D\) de Windows Server 2016 Datacenter](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span>

<span data-ttu-id="6a7ab-120">La technologie S2D prend en charge deux types d’architectures : convergée et hyper-convergée.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="6a7ab-121">L’architecture dans ce document est hyper-convergée.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-121">The architecture in this document is hyper-converged.</span></span> <span data-ttu-id="6a7ab-122">Une infrastructure hyper-convergée place le stockage sur les mêmes serveurs que ceux qui hébergent l’application en cluster.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-122">A hyper-converged infrastructure places the storage on the same servers that host the clustered application.</span></span> <span data-ttu-id="6a7ab-123">Dans cette architecture, le stockage se trouve sur chaque nœud de l’instance de cluster de basculement SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-123">In this architecture, the storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="6a7ab-124">Exemple de modèle Azure</span><span class="sxs-lookup"><span data-stu-id="6a7ab-124">Example Azure template</span></span>

<span data-ttu-id="6a7ab-125">Vous pouvez créer la solution complète dans Azure à partir d’un modèle.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-125">You can create the entire solution in Azure from a template.</span></span> <span data-ttu-id="6a7ab-126">Un exemple de modèle est disponible dans les [Modèles de démarrage rapide Azure](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-126">An example of a template is available in the GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="6a7ab-127">Cet exemple n’est pas conçu ni testé pour une charge de travail spécifique.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="6a7ab-128">Vous pouvez exécuter le modèle pour créer une instance de cluster de basculement SQL Server avec le stockage S2D connecté à votre domaine.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-128">You can run the template to create a SQL Server FCI with S2D storage connected to your domain.</span></span> <span data-ttu-id="6a7ab-129">Vous pouvez évaluer le modèle et le modifier selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-129">You can evaluate the template, and modify it for your purposes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6a7ab-130">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="6a7ab-130">Before you begin</span></span>

<span data-ttu-id="6a7ab-131">Il existe quelques éléments que vous devez connaître et deux choses que vous devez mettre en place avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-131">There are a few things you need to know and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-to-know"></a><span data-ttu-id="6a7ab-132">Éléments à connaître</span><span class="sxs-lookup"><span data-stu-id="6a7ab-132">What to know</span></span>
<span data-ttu-id="6a7ab-133">Vous devez avoir une compréhension opérationnelle des technologies suivantes :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-133">You should have an operational understanding of the following technologies:</span></span>

- [<span data-ttu-id="6a7ab-134">Technologies de cluster Windows</span><span class="sxs-lookup"><span data-stu-id="6a7ab-134">Windows cluster technologies</span></span>](http://technet.microsoft.com/library/hh831579.aspx)
-  <span data-ttu-id="6a7ab-135">[Instances de cluster de basculement SQL Server](http://msdn.microsoft.com/library/ms189134.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span>

<span data-ttu-id="6a7ab-136">Vous devez également avoir une compréhension générale des technologies suivantes :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-136">Also, you should have a general understanding of the following technologies:</span></span>

- [<span data-ttu-id="6a7ab-137">Solution hyper-convergée utilisant les Espaces de stockage direct dans Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="6a7ab-137">Hyper-converged solution using Storage Spaces Direct in Windows Server 2016</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [<span data-ttu-id="6a7ab-138">Groupes de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="6a7ab-138">Azure resource groups</span></span>](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-to-have"></a><span data-ttu-id="6a7ab-139">Éléments à mettre en place</span><span class="sxs-lookup"><span data-stu-id="6a7ab-139">What to have</span></span>

<span data-ttu-id="6a7ab-140">Avant de suivre les instructions de cet article, vérifiez que vous disposez déjà des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-140">Before following the instructions in this article, you should already have:</span></span>

- <span data-ttu-id="6a7ab-141">Un abonnement Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="6a7ab-142">Un domaine Windows sur des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="6a7ab-143">Un compte autorisé à créer des objets sur la machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-143">An account with permission to create objects in the Azure virtual machine.</span></span>
- <span data-ttu-id="6a7ab-144">Un réseau virtuel et un sous-réseau Azure avec suffisamment d’espace d’adressage IP pour les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-144">An Azure virtual network and subnet with sufficient IP address space for the following components:</span></span>
   - <span data-ttu-id="6a7ab-145">Les deux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-145">Both virtual machines.</span></span>
   - <span data-ttu-id="6a7ab-146">L’adresse IP du cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-146">The failover cluster IP address.</span></span>
   - <span data-ttu-id="6a7ab-147">Une adresse IP pour chaque instance de cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="6a7ab-148">Un DNS configuré sur le réseau Azure, pointant vers les contrôleurs de domaine.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-148">DNS configured on the Azure Network, pointing to the domain controllers.</span></span>

<span data-ttu-id="6a7ab-149">Une fois ces conditions préalables en place, vous pouvez passer à la création de votre cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="6a7ab-150">La première étape consiste à créer les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-150">The first step is to create the virtual machines.</span></span>

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="6a7ab-151">Étape 1 : Créer les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="6a7ab-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="6a7ab-152">Connectez-vous au [portail Azure](http://portal.azure.com) avec votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-152">Log in to the [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="6a7ab-153">[Créez un groupe à haute disponibilité Azure](../tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-153">[Create an Azure availability set](../tutorial-availability-sets.md).</span></span>

   <span data-ttu-id="6a7ab-154">Le groupe à haute disponibilité regroupe les machines virtuelles entre les domaines d’erreur et les domaines de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-154">The availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="6a7ab-155">Le groupe à haute disponibilité garantit que votre application n’est pas affectée par les points de défaillance uniques, comme le commutateur réseau ou l’unité d’alimentation d’un rack de serveurs.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-155">The availability set makes sure that your application is not affected by single points of failure, like the network switch or the power unit of a rack of servers.</span></span>

   <span data-ttu-id="6a7ab-156">Si vous n’avez pas créé le groupe de ressources pour vos machines virtuelles, faites-le lorsque vous créez un groupe à haute disponibilité Azure.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-156">If you have not created the resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="6a7ab-157">Si vous utilisez le portail Azure pour créer le groupe à haute disponibilité, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-157">If you're using the Azure portal to create the availability set, do the following steps:</span></span>

   - <span data-ttu-id="6a7ab-158">Dans le portail Azure, cliquez sur **+** pour ouvrir Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-158">In the Azure portal, click **+** to open the Azure Marketplace.</span></span> <span data-ttu-id="6a7ab-159">Recherchez **Groupe à haute disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="6a7ab-160">Cliquez sur **Groupe à haute disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="6a7ab-161">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-161">Click **Create**.</span></span>
   - <span data-ttu-id="6a7ab-162">Dans le panneau **Créer un groupe à haute disponibilité**, définissez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-162">On the **Create availability set** blade, set the following values:</span></span>
      - <span data-ttu-id="6a7ab-163">**Nom** : nom du groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-163">**Name**: A name for the availability set.</span></span>
      - <span data-ttu-id="6a7ab-164">**Abonnement** : votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="6a7ab-165">**Groupe de ressources** : si vous souhaitez utiliser un groupe existant, cliquez sur **Use existing** (Utiliser le groupe existant) et sélectionnez le groupe dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-165">**Resource group**: If you want to use an existing group, click **Use existing** and select the group from the drop-down list.</span></span> <span data-ttu-id="6a7ab-166">Sinon, choisissez **Créer** et entrez un nom pour le groupe.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-166">Otherwise choose **Create New** and type a name for the group.</span></span>
      - <span data-ttu-id="6a7ab-167">**Emplacement** : définissez l’emplacement où vous souhaitez créer vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-167">**Location**: Set the location where you plan to create your virtual machines.</span></span>
      - <span data-ttu-id="6a7ab-168">**Domaines d’erreur** : utilisez la valeur par défaut (3).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-168">**Fault domains**: Use the default (3).</span></span>
      - <span data-ttu-id="6a7ab-169">**Domaines de mise à jour** : utilisez la valeur par défaut (5).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-169">**Update domains**: Use the default (5).</span></span>
   - <span data-ttu-id="6a7ab-170">Cliquez sur **Créer** pour créer le groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-170">Click **Create** to create the availability set.</span></span>

1. <span data-ttu-id="6a7ab-171">Créez les machines virtuelles dans le groupe à haute disponibilité sélectionné.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-171">Create the virtual machines in the availability set.</span></span>

   <span data-ttu-id="6a7ab-172">Configurez deux machines virtuelles SQL Server dans le groupe à haute disponibilité Azure.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-172">Provision two SQL Server virtual machines in the Azure availability set.</span></span> <span data-ttu-id="6a7ab-173">Pour obtenir des instructions, consultez [Approvisionnement d’une machine virtuelle SQL Server dans le portail Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-173">For instructions, see [Provision a SQL Server virtual machine in the Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

   <span data-ttu-id="6a7ab-174">Placez les deux machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-174">Place both virtual machines:</span></span>

   - <span data-ttu-id="6a7ab-175">Dans le même groupe de ressources Azure que celui où se trouve le groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-175">In the same Azure resource group that your availability set is in.</span></span>
   - <span data-ttu-id="6a7ab-176">Sur le même réseau que votre contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-176">On the same network as your domain controller.</span></span>
   - <span data-ttu-id="6a7ab-177">Sur un sous-réseau avec un espace d’adressage IP suffisant pour les deux machines virtuelles et toutes les instances de cluster de basculement que vous pourriez utiliser sur ce cluster.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span>
   - <span data-ttu-id="6a7ab-178">Dans le groupe à haute disponibilité Azure.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-178">In the Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="6a7ab-179">Vous ne pouvez pas définir ni modifier un groupe à haute disponibilité après la création d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="6a7ab-180">Choisissez une image dans Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-180">Choose an image from the Azure Marketplace.</span></span> <span data-ttu-id="6a7ab-181">Vous pouvez utiliser une image Marketplace qui inclut Windows Server et SQL Server, ou uniquement Windows Server.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just the Windows Server.</span></span> <span data-ttu-id="6a7ab-182">Pour plus d’informations, consultez [Présentation de SQL Server sur les machines virtuelles Azure](../../virtual-machines-windows-sql-server-iaas-overview.md)</span><span class="sxs-lookup"><span data-stu-id="6a7ab-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>

   <span data-ttu-id="6a7ab-183">Les images SQL Server officielles dans la galerie Azure incluent une instance SQL Server installée, ainsi que le logiciel d’installation SQL Server et la clé requise.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-183">The official SQL Server images in the Azure Gallery include an installed SQL Server instance, plus the SQL Server installation software, and the required key.</span></span>

   <span data-ttu-id="6a7ab-184">Choisissez l’image appropriée en fonction de la façon dont vous souhaitez payer pour la licence SQL Server :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-184">Choose the right image according to how you want to pay for the SQL Server license:</span></span>

   - <span data-ttu-id="6a7ab-185">**Licences avec paiement à l’utilisation** : le coût par minute de ces images inclut l’attribution de licences SQL Server :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-185">**Pay per usage licensing**: The per-minute cost of these images includes the SQL Server licensing:</span></span>
      - <span data-ttu-id="6a7ab-186">**SQL Server 2016 Enterprise sur Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="6a7ab-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="6a7ab-187">**SQL Server 2016 Standard sur Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="6a7ab-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="6a7ab-188">**SQL Server 2016 Developer sur Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="6a7ab-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>

   - <span data-ttu-id="6a7ab-189">**BYOL (apportez votre propre licence)**</span><span class="sxs-lookup"><span data-stu-id="6a7ab-189">**Bring-your-own-license (BYOL)**</span></span>

      - <span data-ttu-id="6a7ab-190">**{BYOL} SQL Server 2016 Enterprise sur Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="6a7ab-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="6a7ab-191">**{BYOL} SQL Server 2016 Standard sur Windows Server Datacenter 2016**</span><span class="sxs-lookup"><span data-stu-id="6a7ab-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="6a7ab-192">Après avoir créé la machine virtuelle, supprimez l’instance SQL Server autonome préinstallée.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-192">After you create the virtual machine, remove the pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="6a7ab-193">Vous utiliserez le support SQL Server préinstallé pour créer l’instance de cluster de basculement SQL Server après avoir configuré le cluster de basculement et les espaces de stockage direct.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-193">You will use the pre-installed SQL Server media to create the SQL Server FCI after you configure the failover cluster and S2D.</span></span>

   <span data-ttu-id="6a7ab-194">Vous pouvez également utiliser des images Azure Marketplace avec le système d’exploitation seulement.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-194">Alternatively, you can use Azure Marketplace images with just the operating system.</span></span> <span data-ttu-id="6a7ab-195">Choisissez une image **Windows Server 2016 Datacenter** et installez l’instance de cluster de basculement SQL Server après avoir configuré le cluster de basculement et les espaces de stockage direct.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-195">Choose a **Windows Server 2016 Datacenter** image and install the SQL Server FCI after you configure the failover cluster and S2D.</span></span> <span data-ttu-id="6a7ab-196">Cette image ne contient aucun support d’installation SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="6a7ab-197">Placez le support d’installation dans un emplacement où vous pouvez exécuter l’installation de SQL Server pour chaque serveur.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-197">Place the installation media in a location where you can run the SQL Server installation for each server.</span></span>

1. <span data-ttu-id="6a7ab-198">Une fois que vos machines virtuelles ont été créées par Azure, connectez-vous à chaque machine virtuelle en utilisant le protocole RDP.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-198">After Azure creates your virtual machines, connect to each virtual machine with RDP.</span></span>

   <span data-ttu-id="6a7ab-199">Lors de votre première connexion à une machine virtuelle avec le protocole RDP, l’ordinateur vous demande si vous souhaitez autoriser que cet ordinateur soit détecté sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-199">When you first connect to a virtual machine with RDP, the computer asks if you want to allow this PC to be discoverable on the network.</span></span> <span data-ttu-id="6a7ab-200">Cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-200">Click **Yes**.</span></span>

1. <span data-ttu-id="6a7ab-201">Si vous utilisez l’une des images de machine virtuelle basée sur SQL Server, supprimez l’instance SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-201">If you are using one of the SQL Server-based virtual machine images, remove the SQL Server instance.</span></span>

   - <span data-ttu-id="6a7ab-202">Dans **Programmes et fonctionnalités**, cliquez avec le bouton droit sur **Microsoft SQL Server 2016 (64 bits)** et sur **Désinstaller/modifier**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span>
   - <span data-ttu-id="6a7ab-203">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-203">Click **Remove**.</span></span>
   - <span data-ttu-id="6a7ab-204">Sélectionnez l’instance par défaut.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-204">Select the default instance.</span></span>
   - <span data-ttu-id="6a7ab-205">Supprimer toutes les fonctionnalités sous **Services Moteur de base de données**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="6a7ab-206">Ne supprimez pas les **Fonctionnalités partagées**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="6a7ab-207">Consultez l’illustration suivante :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-207">See the following picture:</span></span>

      ![Supprimer des fonctionnalités](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="6a7ab-209">Cliquez sur **Suivant**, puis sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-209">Click **Next**, and then click **Remove**.</span></span>

1. <span data-ttu-id="6a7ab-210"><a name="ports"></a>Ouvrez les ports du pare-feu.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-210"><a name="ports"></a>Open the firewall ports.</span></span>

   <span data-ttu-id="6a7ab-211">Sur chaque machine virtuelle, ouvrez les ports suivants du pare-feu Windows.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-211">On each virtual machine, open the following ports on the Windows Firewall.</span></span>

   | <span data-ttu-id="6a7ab-212">Objectif</span><span class="sxs-lookup"><span data-stu-id="6a7ab-212">Purpose</span></span> | <span data-ttu-id="6a7ab-213">Port TCP</span><span class="sxs-lookup"><span data-stu-id="6a7ab-213">TCP Port</span></span> | <span data-ttu-id="6a7ab-214">Remarques</span><span class="sxs-lookup"><span data-stu-id="6a7ab-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="6a7ab-215">SQL Server</span><span class="sxs-lookup"><span data-stu-id="6a7ab-215">SQL Server</span></span> | <span data-ttu-id="6a7ab-216">1433</span><span class="sxs-lookup"><span data-stu-id="6a7ab-216">1433</span></span> | <span data-ttu-id="6a7ab-217">Port normal pour les instances par défaut de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="6a7ab-218">Si vous avez utilisé une image de la galerie, ce port s’ouvre automatiquement.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-218">If you used an image from the gallery, this port is automatically opened.</span></span>
   | <span data-ttu-id="6a7ab-219">Sonde d’intégrité</span><span class="sxs-lookup"><span data-stu-id="6a7ab-219">Health probe</span></span> | <span data-ttu-id="6a7ab-220">59999</span><span class="sxs-lookup"><span data-stu-id="6a7ab-220">59999</span></span> | <span data-ttu-id="6a7ab-221">Tout port TCP ouvert.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-221">Any open TCP port.</span></span> <span data-ttu-id="6a7ab-222">Dans une étape ultérieure, configurez la [sonde d’intégrité](#probe) de l’équilibrage de charge et le cluster pour qu’ils utilisent ce port.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-222">In a later step, configure the load balancer [health probe](#probe) and the cluster to use this port.</span></span>  

1. <span data-ttu-id="6a7ab-223">Ajoutez du stockage à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-223">Add storage to the virtual machine.</span></span> <span data-ttu-id="6a7ab-224">Pour plus d’informations, consultez [Ajouter du stockage](../../../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-224">For detailed information, see [add storage](../../../storage/common/storage-premium-storage.md).</span></span>

   <span data-ttu-id="6a7ab-225">Les deux machines virtuelles ont besoin d’au moins deux disques de données.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="6a7ab-226">Attachez des disques bruts, et non des disques au format NTFS.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-226">Attach raw disks - not NTFS formatted disks.</span></span>
      >[!NOTE]
      ><span data-ttu-id="6a7ab-227">Si vous attachez des disques au format NTFS, vous pouvez uniquement activer la technologie S2D sans vérification d’éligibilité de disque.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  

   <span data-ttu-id="6a7ab-228">Attachez au moins deux instances de stockage Premium (disques SSD) à chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-228">Attach a minimum of two Premium Storage (SSD disks) to each VM.</span></span> <span data-ttu-id="6a7ab-229">Nous vous recommandons d’utiliser au minimum des disques P30 (1 To).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="6a7ab-230">Définissez la mise en cache de l’hôte sur **Lecture seule**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-230">Set host caching to **Read-only**.</span></span>

   <span data-ttu-id="6a7ab-231">La capacité de stockage que vous utilisez dans des environnements de production dépend de votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-231">The storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="6a7ab-232">Les valeurs décrites dans cet article sont à des fins de démonstration et de test.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-232">The values described in this article are for demonstration and testing.</span></span>

1. <span data-ttu-id="6a7ab-233">[Ajoutez les machines virtuelles à votre domaine préexistant](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-233">[Add the virtual machines to your pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="6a7ab-234">Une fois les machines virtuelles créées et configurées, vous pouvez configurer le cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-234">After the virtual machines are created and configured, you can configure the failover cluster.</span></span>

## <a name="step-2-configure-the-windows-failover-cluster-with-s2d"></a><span data-ttu-id="6a7ab-235">Étape 2 : Configurer le cluster de basculement Windows avec la technologie S2D</span><span class="sxs-lookup"><span data-stu-id="6a7ab-235">Step 2: Configure the Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="6a7ab-236">L’étape suivante consiste à configurer le cluster de basculement avec la technologie S2D.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-236">The next step is to configure the failover cluster with S2D.</span></span> <span data-ttu-id="6a7ab-237">Dans cette étape, vous allez exécuter les sous-étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-237">In this step, you will do the following substeps:</span></span>

1. <span data-ttu-id="6a7ab-238">Ajouter la fonctionnalité Windows de Clustering de basculement</span><span class="sxs-lookup"><span data-stu-id="6a7ab-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="6a7ab-239">Valider le cluster</span><span class="sxs-lookup"><span data-stu-id="6a7ab-239">Validate the cluster</span></span>
1. <span data-ttu-id="6a7ab-240">Créer le cluster de basculement</span><span class="sxs-lookup"><span data-stu-id="6a7ab-240">Create the failover cluster</span></span>
1. <span data-ttu-id="6a7ab-241">Créer le témoin cloud</span><span class="sxs-lookup"><span data-stu-id="6a7ab-241">Create the cloud witness</span></span>
1. <span data-ttu-id="6a7ab-242">Ajouter du stockage</span><span class="sxs-lookup"><span data-stu-id="6a7ab-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="6a7ab-243">Ajouter la fonctionnalité Windows de Clustering de basculement</span><span class="sxs-lookup"><span data-stu-id="6a7ab-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="6a7ab-244">Pour commencer, connectez-vous à la première machine virtuelle avec RDP à l’aide d’un compte de domaine qui est membre du groupe Administrateurs locaux et qui dispose des autorisations pour créer des objets dans Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-244">To begin, connect to the first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions to create objects in Active Directory.</span></span> <span data-ttu-id="6a7ab-245">Utilisez ce compte pour le reste de la configuration.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-245">Use this account for the rest of the configuration.</span></span>

1. <span data-ttu-id="6a7ab-246">[Ajoutez la fonctionnalité de Clustering de basculement à chaque machine virtuelle](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-246">[Add Failover Clustering feature to each virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

   <span data-ttu-id="6a7ab-247">Pour installer la fonctionnalité de Clustering de basculement à partir de l’interface utilisateur, exécutez les étapes suivantes sur les deux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-247">To install Failover Clustering feature from the UI, do the following steps on both virtual machines.</span></span>
   - <span data-ttu-id="6a7ab-248">Dans le **Gestionnaire de serveur**, cliquez sur **Gérer**, puis sur **Ajouter des rôles et fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span>
   - <span data-ttu-id="6a7ab-249">Dans **l’Assistant Ajout de rôles et de fonctionnalités**, cliquez sur **Suivant** jusqu’à ce que vous atteigniez la page **Sélectionner les fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-249">In **Add Roles and Features Wizard**, click **Next** until you get to **Select Features**.</span></span>
   - <span data-ttu-id="6a7ab-250">Dans **Sélectionner les fonctionnalités**, cliquez sur **Clustering de basculement**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="6a7ab-251">Incluez toutes les fonctionnalités et les outils de gestion requis.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-251">Include all required features and the management tools.</span></span> <span data-ttu-id="6a7ab-252">Cliquez sur **Ajouter des fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="6a7ab-253">Cliquez sur **Suivant**, puis sur **Terminer** pour installer les fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-253">Click **Next** and then click **Finish** to install the features.</span></span>

   <span data-ttu-id="6a7ab-254">Pour installer la fonctionnalité Clustering de basculement avec PowerShell, exécutez le script suivant à partir d’une session PowerShell d’administrateur sur l’une des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-254">To install the Failover Clustering feature with PowerShell, run the following script from an administrator PowerShell session on one of the virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="6a7ab-255">À titre de référence, les étapes suivantes respectent les instructions de l’Étape 3 sous [Solution hyper-convergée utilisant les Espaces de stockage direct dans Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-255">For reference, the next steps follow the instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span>

### <a name="validate-the-cluster"></a><span data-ttu-id="6a7ab-256">Valider le cluster</span><span class="sxs-lookup"><span data-stu-id="6a7ab-256">Validate the cluster</span></span>

<span data-ttu-id="6a7ab-257">Ce guide fait référence aux instructions sous [Valider le cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-257">This guide refers to instructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="6a7ab-258">Validez le cluster dans l’interface utilisateur ou avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-258">Validate the cluster in the UI or with PowerShell.</span></span>

<span data-ttu-id="6a7ab-259">Pour valider le cluster avec l’interface utilisateur, effectuez les étapes suivantes à partir d’une des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-259">To validate the cluster with the UI, do the following steps from one of the virtual machines.</span></span>

1. <span data-ttu-id="6a7ab-260">Dans le **Gestionnaire de serveur**, cliquez sur **Outils**, puis cliquez sur **Gestionnaire du cluster de basculement**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span>
1. <span data-ttu-id="6a7ab-261">Dans le **Gestionnaire du cluster de basculement**, cliquez sur **Action**, puis cliquez sur **Valider la configuration...**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="6a7ab-262">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-262">Click **Next**.</span></span>
1. <span data-ttu-id="6a7ab-263">Sous **Sélectionner des serveurs ou un cluster**, entrez le nom des deux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-263">On **Select Servers or a Cluster**, type the name of both virtual machines.</span></span>
1. <span data-ttu-id="6a7ab-264">Sous **Options de test**, choisissez **Exécuter uniquement les tests que je sélectionne**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="6a7ab-265">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-265">Click **Next**.</span></span>
1. <span data-ttu-id="6a7ab-266">Sous **Sélection du test**, incluez tous les tests sauf **Stockage**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="6a7ab-267">Consultez l’illustration suivante :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-267">See the following picture:</span></span>

   ![Valider les tests](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. <span data-ttu-id="6a7ab-269">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-269">Click **Next**.</span></span>
1. <span data-ttu-id="6a7ab-270">Sous **Confirmation**, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-270">On **Confirmation**, click **Next**.</span></span>

<span data-ttu-id="6a7ab-271">**L’Assistant Validation d’une configuration** exécute les tests de validation.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-271">The **Validate a Configuration Wizard** runs the validation tests.</span></span>

<span data-ttu-id="6a7ab-272">Pour valider le cluster avec PowerShell, exécutez le script suivant à partir d’une session PowerShell d’administrateur sur l’une des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-272">To validate the cluster with PowerShell, run the following script from an administrator PowerShell session on one of the virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="6a7ab-273">Après avoir validé le cluster, créez le cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-273">After you validate the cluster, create the failover cluster.</span></span>

### <a name="create-the-failover-cluster"></a><span data-ttu-id="6a7ab-274">Créer le cluster de basculement</span><span class="sxs-lookup"><span data-stu-id="6a7ab-274">Create the failover cluster</span></span>

<span data-ttu-id="6a7ab-275">Ce guide fait référence à la section [Créer le cluster de basculement](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-275">This guide refers to [Create the failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="6a7ab-276">Pour créer le cluster de basculement, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-276">To create the failover cluster, you need:</span></span>
- <span data-ttu-id="6a7ab-277">Les noms des machines virtuelles qui deviennent les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-277">The names of the virtual machines that become the cluster nodes.</span></span>
- <span data-ttu-id="6a7ab-278">Un nom pour le cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-278">A name for the failover cluster</span></span>
- <span data-ttu-id="6a7ab-279">Une adresse IP pour le cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-279">An IP address for the failover cluster.</span></span> <span data-ttu-id="6a7ab-280">Vous pouvez spécifier une adresse IP qui n’est pas utilisée sur le même réseau virtuel et sous-réseau Azure que les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-280">You can use an IP address that is not used on the same Azure virtual network and subnet as the cluster nodes.</span></span>

<span data-ttu-id="6a7ab-281">Le script PowerShell suivant crée un cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-281">The following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="6a7ab-282">Mettez à jour le script avec les noms des nœuds (les noms des machines virtuelles) et une adresse IP disponible à partir du réseau virtuel Azure :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-282">Update the script with the names of the nodes (the virtual machine names) and an available IP address from the Azure VNET:</span></span>

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="6a7ab-283">Créer un témoin cloud</span><span class="sxs-lookup"><span data-stu-id="6a7ab-283">Create a cloud witness</span></span>

<span data-ttu-id="6a7ab-284">Un témoin cloud est un nouveau type de témoin de quorum de cluster stocké dans un Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="6a7ab-285">Cela supprime la nécessité de disposer d’une machine virtuelle distincte qui héberge un partage de fichiers du témoin.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-285">This removes the need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="6a7ab-286">[Créez un témoin cloud pour le cluster de basculement](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-286">[Create a cloud witness for the failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span>

1. <span data-ttu-id="6a7ab-287">Créez un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-287">Create a blob container.</span></span>

1. <span data-ttu-id="6a7ab-288">Enregistrez les clés d’accès et l’URL du conteneur.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-288">Save the access keys and the container URL.</span></span>

1. <span data-ttu-id="6a7ab-289">Configurez le témoin de quorum du cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-289">Configure the failover cluster cluster quorum witness.</span></span> <span data-ttu-id="6a7ab-290">Consultez [Configurer le témoin de quorum dans l’interface utilisateur].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-290">See, [Configure the quorum witness in the user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in the UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="6a7ab-291">Ajouter du stockage</span><span class="sxs-lookup"><span data-stu-id="6a7ab-291">Add storage</span></span>

<span data-ttu-id="6a7ab-292">Les disques pour la technologie S2D doivent être vides et sans partitions ou autres données.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-292">The disks for S2D need to be empty and without partitions or other data.</span></span> <span data-ttu-id="6a7ab-293">Pour nettoyer les disques, suivez [les étapes décrites dans ce guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-293">To clean disks follow [the steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>

1. <span data-ttu-id="6a7ab-294">[Activez les Espaces de stockage direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="6a7ab-295">Le script PowerShell suivant active les espaces de stockage direct.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-295">The following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="6a7ab-296">Dans le **Gestionnaire du cluster de basculement**, vous pouvez maintenant voir le pool de stockage.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-296">In **Failover Cluster Manager**, you can now see the storage pool.</span></span>

1. <span data-ttu-id="6a7ab-297">[Créez un volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="6a7ab-298">L’une des fonctionnalités de la technologie S2D est qu’elle crée automatiquement un pool de stockage lorsque vous l’activez.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-298">One of the features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="6a7ab-299">Vous êtes maintenant prêt à créer un volume.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-299">You are now ready to create a volume.</span></span> <span data-ttu-id="6a7ab-300">L’applet de commande PowerShell `New-Volume` automatise le processus de création de volume, notamment la mise en forme, l’ajout au cluster et la création d’un volume partagé de cluster (CSV).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-300">The PowerShell commandlet `New-Volume` automates the volume creation process, including formatting, adding to the cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="6a7ab-301">L’exemple suivant crée un volume partagé de cluster de 800 gigaoctets.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-301">The following example creates an 800 gigabyte (GB) CSV.</span></span>

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="6a7ab-302">Une fois cette commande terminée, un volume de 800 Go est monté en tant que ressource du cluster.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="6a7ab-303">Le volume se trouve sous `C:\ClusterStorage\Volume1\`.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-303">The volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="6a7ab-304">Le schéma suivant illustre un volume partagé de cluster avec la technologie S2D :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-304">The following diagram shows a cluster shared volume with S2D:</span></span>

   ![VolumePartagéCluster](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="6a7ab-306">Étape 3 : Tester le basculement du cluster de basculement</span><span class="sxs-lookup"><span data-stu-id="6a7ab-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="6a7ab-307">Dans le Gestionnaire du cluster de basculement, vérifiez que vous pouvez déplacer la ressource de stockage vers l’autre nœud du cluster.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-307">In Failover Cluster Manager, verify that you can move the storage resource to the other cluster node.</span></span> <span data-ttu-id="6a7ab-308">Si vous pouvez vous connecter au cluster de basculement avec le **Gestionnaire du cluster de basculement** et déplacer le stockage d’un nœud à l’autre, vous êtes prêt à configurer l’instance de cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-308">If you can connect to the failover cluster with **Failover Cluster Manager** and move the storage from one node to the other, you are ready to configure the FCI.</span></span>

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="6a7ab-309">Étape 4 : Créer l’instance de cluster de basculement SQL Server</span><span class="sxs-lookup"><span data-stu-id="6a7ab-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="6a7ab-310">Après avoir configuré le cluster de basculement et tous les composants du cluster, notamment le stockage, vous pouvez créer l’instance de cluster de basculement SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-310">After you have configured the failover cluster and all cluster components including storage, you can create the SQL Server FCI.</span></span>

1. <span data-ttu-id="6a7ab-311">Connectez-vous à la première machine virtuelle avec RDP.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-311">Connect to the first virtual machine with RDP.</span></span>

1. <span data-ttu-id="6a7ab-312">Dans le **Gestionnaire du cluster de basculement**, vérifiez que toutes les ressources principales du cluster se trouvent sur la première machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-312">In **Failover Cluster Manager**, make sure all cluster core resources are on the first virtual machine.</span></span> <span data-ttu-id="6a7ab-313">Si nécessaire, déplacez toutes les ressources vers cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-313">If necessary, move all resources to this virtual machine.</span></span>

1. <span data-ttu-id="6a7ab-314">Recherchez le support d’installation.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-314">Locate the installation media.</span></span> <span data-ttu-id="6a7ab-315">Si la machine virtuelle utilise l’une des images Azure Marketplace, le support se situe sous `C:\SQLServer_<version number>_Full`.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-315">If the virtual machine uses one of the Azure Marketplace images, the media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="6a7ab-316">Cliquez sur **Setup**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-316">Click **Setup**.</span></span>

1. <span data-ttu-id="6a7ab-317">Dans le **Centre d’installation SQL Server**, cliquez sur **Installation**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-317">In the **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="6a7ab-318">Cliquez sur **Installation d’un nouveau cluster de basculement SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="6a7ab-319">Suivez les instructions de l’Assistant pour installer l’instance de cluster de basculement SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-319">Follow the instructions in the wizard to install the SQL Server FCI.</span></span>

   <span data-ttu-id="6a7ab-320">Les répertoires de données de l’instance de cluster de basculement doivent se trouver sur le stockage en cluster.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-320">The FCI data directories need to be on clustered storage.</span></span> <span data-ttu-id="6a7ab-321">Avec la technologie S2D, il ne s’agit pas d’un disque partagé, mais d’un point de montage vers un volume sur chaque serveur.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-321">With S2D, it's not a shared disk, but a mount point to a volume on each server.</span></span> <span data-ttu-id="6a7ab-322">La technologie S2D synchronise le volume entre les deux nœuds.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-322">S2D synchronizes the volume between both nodes.</span></span> <span data-ttu-id="6a7ab-323">Le volume est présenté au cluster en tant que volume partagé de cluster.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-323">The volume is presented to the cluster as a cluster shared volume.</span></span> <span data-ttu-id="6a7ab-324">Utilisez le point de montage du volume partagé de cluster pour les répertoires de données.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-324">Use the CSV mount point for the data directories.</span></span>

   ![RépertoiresDonnées](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="6a7ab-326">Une fois l’Assistant terminé, le programme d’installation installe une instance de cluster de basculement SQL Server sur le premier nœud.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-326">After you complete the wizard, Setup will install a SQL Server FCI on the first node.</span></span>

1. <span data-ttu-id="6a7ab-327">Une fois que le programme d’installation a correctement installé l’instance de cluster de basculement sur le premier nœud, connectez-vous au second nœud avec RDP.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-327">After Setup successfully installs the FCI on the first node, connect to the second node with RDP.</span></span>

1. <span data-ttu-id="6a7ab-328">Ouvrez le **Centre d’installation SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-328">Open the **SQL Server Installation Center**.</span></span> <span data-ttu-id="6a7ab-329">Cliquez sur **Installation**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-329">Click **Installation**.</span></span>

1. <span data-ttu-id="6a7ab-330">Cliquez sur **Ajouter un nœud à un cluster de basculement SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-330">Click **Add node to a SQL Server failover cluster**.</span></span> <span data-ttu-id="6a7ab-331">Suivez les instructions de l’Assistant pour installer SQL Server et ajouter ce serveur à l’instance de cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-331">Follow the instructions in the wizard to install SQL server and add this server to the FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="6a7ab-332">Si vous avez utilisé une image de la galerie Azure Marketplace avec SQL Server, les outils SQL Server ont été inclus avec l’image.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with the image.</span></span> <span data-ttu-id="6a7ab-333">Si vous n’avez pas utilisé cette image, installez les outils SQL Server séparément.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-333">If you did not use this image, install the SQL Server tools separately.</span></span> <span data-ttu-id="6a7ab-334">Consultez [Télécharger SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="6a7ab-335">Étape 5 : Créer un équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="6a7ab-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="6a7ab-336">Sur les machines virtuelles Azure, les clusters utilisent un équilibrage de charge pour conserver une adresse IP qui doit se trouver sur un nœud de cluster à la fois.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-336">On Azure virtual machines, clusters use a load balancer to hold an IP address that needs to be on one cluster node at a time.</span></span> <span data-ttu-id="6a7ab-337">Dans cette solution, l’équilibrage de charge contient l’adresse IP de l’instance de cluster de basculement SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-337">In this solution, the load balancer holds the IP address for the SQL Server FCI.</span></span>

<span data-ttu-id="6a7ab-338">[Créez et configurez un équilibrage de charge Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-the-load-balancer-in-the-azure-portal"></a><span data-ttu-id="6a7ab-339">Créer l’équilibrage de charge dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="6a7ab-339">Create the load balancer in the Azure portal</span></span>

<span data-ttu-id="6a7ab-340">Pour créer l’équilibrage de charge :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-340">To create the load balancer:</span></span>

1. <span data-ttu-id="6a7ab-341">Dans le portail Azure, accédez au groupe de ressources contenant les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-341">In the Azure portal, go to the Resource Group with the virtual machines.</span></span>

1. <span data-ttu-id="6a7ab-342">Cliquez sur **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-342">Click **+ Add**.</span></span> <span data-ttu-id="6a7ab-343">Recherchez **Équilibrage de charge** dans Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-343">Search the Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="6a7ab-344">Cliquez sur **Équilibrage de charge**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="6a7ab-345">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-345">Click **Create**.</span></span>

1. <span data-ttu-id="6a7ab-346">Configurez l’équilibrage de charge avec :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-346">Configure the load balancer with:</span></span>

   - <span data-ttu-id="6a7ab-347">**Nom** : nom qui identifie l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-347">**Name**: A name that identifies the load balancer.</span></span>
   - <span data-ttu-id="6a7ab-348">**Type** : l’équilibrage de charge peut être public ou privé.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-348">**Type**: The load balancer can be either public or private.</span></span> <span data-ttu-id="6a7ab-349">Un équilibrage de charge privé est accessible à partir du même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-349">A private load balancer can be accessed from within the same VNET.</span></span> <span data-ttu-id="6a7ab-350">La plupart des applications Azure peut utiliser un équilibrage de charge privé.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="6a7ab-351">Si votre application doit accéder à SQL Server directement via Internet, utilisez un équilibrage de charge public.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-351">If your application needs access to SQL Server directly over the Internet, use a public load balancer.</span></span>
   - <span data-ttu-id="6a7ab-352">**Réseau virtuel** : le même réseau que les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-352">**Virtual Network**: The same network as the virtual machines.</span></span>
   - <span data-ttu-id="6a7ab-353">**Sous-réseau** : le même sous-réseau que les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-353">**Subnet**: The same subnet as the virtual machines.</span></span>
   - <span data-ttu-id="6a7ab-354">**Adresse IP privée** : la même adresse IP que celle attribuée à la ressource réseau de cluster FCI SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-354">**Private IP address**: The same IP address that you assigned to the SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="6a7ab-355">**Abonnement** : votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="6a7ab-356">**Groupe de ressources** : utilisez le même groupe de ressources que celui de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-356">**Resource Group**: Use the same resource group as your virtual machines.</span></span>
   - <span data-ttu-id="6a7ab-357">**Emplacement** : utilisez le même emplacement Azure que celui de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-357">**Location**: Use the same Azure location as your virtual machines.</span></span>
   <span data-ttu-id="6a7ab-358">Consultez l’illustration suivante :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-358">See the following picture:</span></span>

   ![CréerÉquilibrageCharge](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-the-load-balancer-backend-pool"></a><span data-ttu-id="6a7ab-360">Configurer le pool principal de l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="6a7ab-360">Configure the load balancer backend pool</span></span>

1. <span data-ttu-id="6a7ab-361">Revenez au groupe de ressources Azure contenant les machines virtuelles et recherchez le nouvel équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-361">Return to the Azure Resource Group with the virtual machines and locate the new load balancer.</span></span> <span data-ttu-id="6a7ab-362">Vous devrez peut-être actualiser l’affichage du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-362">You may have to refresh the view on the Resource Group.</span></span> <span data-ttu-id="6a7ab-363">Cliquez sur l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-363">Click the load balancer.</span></span>

1. <span data-ttu-id="6a7ab-364">Dans le panneau de l’équilibrage de charge, cliquez sur **Pools principaux**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-364">On the load balancer blade, click **Backend pools**.</span></span>

1. <span data-ttu-id="6a7ab-365">Cliquez sur **+ Ajouter** pour ajouter un pool principal.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-365">Click **+ Add** to add a backend pool.</span></span>

1. <span data-ttu-id="6a7ab-366">Entez un nom pour le pool principal.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-366">Type a name for the backend pool.</span></span>

1. <span data-ttu-id="6a7ab-367">Cliquez sur **Ajouter une machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="6a7ab-368">Dans le panneau **Choisir des machines virtuelles**, cliquez sur **Choisir un groupe à haute disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-368">On the **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="6a7ab-369">Choisissez le groupe à haute disponibilité dans lequel vous avez placé les machines virtuelles SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-369">Choose the availability set that you placed the SQL Server virtual machines in.</span></span>

1. <span data-ttu-id="6a7ab-370">Dans le panneau **Choisir des machines virtuelles**, cliquez sur **Choisir les machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-370">On the **Choose virtual machines** blade, click **Choose the virtual machines**.</span></span>

   <span data-ttu-id="6a7ab-371">Votre portail Azure doit ressembler à l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-371">Your Azure portal should look like the following picture:</span></span>

   ![CréerPoolPrincipalÉquilibrageCharge](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="6a7ab-373">Cliquez sur **Sélectionner** dans le panneau **Choisir des machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-373">Click **Select** on the **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="6a7ab-374">Cliquez sur **OK** deux fois.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-374">Click **OK** twice.</span></span>

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="6a7ab-375">Configurer une sonde d’intégrité d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="6a7ab-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="6a7ab-376">Dans le panneau de l’équilibrage de charge, cliquez sur **Sondes d’intégrité**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-376">On the load balancer blade, click **Health probes**.</span></span>

1. <span data-ttu-id="6a7ab-377">Cliquez sur **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-377">Click **+ Add**.</span></span>

1. <span data-ttu-id="6a7ab-378">Dans le panneau **Ajouter une sonde d’intégrité**, <a name="probe"></a>définissez les paramètres de la sonde d’intégrité :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-378">On the **Add health probe** blade, <a name="probe"></a>Set the health probe parameters:</span></span>

   - <span data-ttu-id="6a7ab-379">**Nom** : nom de la sonde d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-379">**Name**: A name for the health probe.</span></span>
   - <span data-ttu-id="6a7ab-380">**Protocole** : TCP.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="6a7ab-381">**Port** : défini sur un port TCP disponible.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-381">**Port**: Set to an available TCP port.</span></span> <span data-ttu-id="6a7ab-382">Ce port nécessite un port de pare-feu ouvert.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-382">This port requires an open firewall port.</span></span> <span data-ttu-id="6a7ab-383">Utilisez le [même port](#ports) que celui défini pour la sonde d’intégrité au niveau du pare-feu.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-383">Use the [same port](#ports) you set for the health probe at the firewall.</span></span>
   - <span data-ttu-id="6a7ab-384">**Intervalle** : 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="6a7ab-385">**Seuil de défaillance** : 2 défaillances consécutives.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="6a7ab-386">Cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="6a7ab-387">Définir les règles d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="6a7ab-387">Set load balancing rules</span></span>

1. <span data-ttu-id="6a7ab-388">Dans le panneau de l’équilibrage de charge, cliquez sur **Règles d’équilibrage de charge**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-388">On the load balancer blade, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="6a7ab-389">Cliquez sur **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="6a7ab-390">Configurez les paramètres d’équilibrage de charge :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-390">Set the load balancing rules parameters:</span></span>

   - <span data-ttu-id="6a7ab-391">**Nom** : nom des règles d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-391">**Name**: A name for the load balancing rules.</span></span>
   - <span data-ttu-id="6a7ab-392">**Adresse IP frontale** : utilisez l’adresse IP de la ressource réseau de cluster FCI SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-392">**Frontend IP address**: Use the IP address for the SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="6a7ab-393">**Port** : défini pour le port TCP FCI SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-393">**Port**: Set for the SQL Server FCI TCP port.</span></span> <span data-ttu-id="6a7ab-394">Le port d’instance par défaut est 1433.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-394">The default instance port is 1433.</span></span>
   - <span data-ttu-id="6a7ab-395">**Port principal** : cette valeur utilise le même port que la valeur **Port** lorsque vous activez **Adresse IP flottante (retour serveur direct)**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-395">**Backend port**: This value uses the same port as the **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="6a7ab-396">**Pool principal** : utilisez le nom du pool principal que vous avez configuré précédemment.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-396">**Backend pool**: Use the backend pool name that you configured earlier.</span></span>
   - <span data-ttu-id="6a7ab-397">**Sonde d’intégrité** : utilisez la sonde d’intégrité que vous avez configurée précédemment.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-397">**Health probe**: Use the health probe that you configured earlier.</span></span>
   - <span data-ttu-id="6a7ab-398">**Persistance de session** : aucune.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="6a7ab-399">**Délai d’inactivité (minutes)** : 4.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="6a7ab-400">**Adresse IP flottante (retour serveur direct)** : activée</span><span class="sxs-lookup"><span data-stu-id="6a7ab-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="6a7ab-401">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-401">Click **OK**.</span></span>

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="6a7ab-402">Étape 6 : Configurer le cluster pour la sonde</span><span class="sxs-lookup"><span data-stu-id="6a7ab-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="6a7ab-403">Définissez le paramètre de port de sonde de cluster dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-403">Set the cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="6a7ab-404">Pour définir le paramètre de port de sonde de cluster, mettez à jour les variables dans le script suivant à partir de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-404">To set the cluster probe port parameter, update variables in the following script from your environment.</span></span>

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name).
   $IPResourceName = "IP Address Resource Name" # the IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # the IP Address of the Internal Load Balancer (ILB). This is the static IP address for the load balancer you configured in the Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="6a7ab-405">Étape 7 : Test du basculement FCI</span><span class="sxs-lookup"><span data-stu-id="6a7ab-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="6a7ab-406">Testez le basculement de l’instance de cluster de basculement pour valider le fonctionnement du cluster.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-406">Test failover of the FCI to validate cluster functionality.</span></span> <span data-ttu-id="6a7ab-407">Effectuez également les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="6a7ab-407">Do the following steps:</span></span>

1. <span data-ttu-id="6a7ab-408">Connectez-vous à l’un des nœuds de cluster FCI SQL Server avec RDP.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-408">Connect to one of the SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="6a7ab-409">Ouvrez le **Gestionnaire du cluster de basculement**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="6a7ab-410">Cliquez sur **Rôles**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-410">Click **Roles**.</span></span> <span data-ttu-id="6a7ab-411">Notez le nœud qui possède le rôle de l’instance de cluster de basculement SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-411">Notice which node owns the SQL Server FCI role.</span></span>

1. <span data-ttu-id="6a7ab-412">Cliquez avec le bouton droit sur le rôle de l’instance de cluster de basculement SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-412">Right-click the SQL Server FCI role.</span></span>

1. <span data-ttu-id="6a7ab-413">Cliquez sur **Déplacer** et sur **Meilleur nœud possible**.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="6a7ab-414">Le **Gestionnaire du cluster de basculement** présente le rôle et ses ressources hors connexion.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-414">**Failover Cluster Manager** shows the role and its resources go offline.</span></span> <span data-ttu-id="6a7ab-415">Ensuite, les ressources sont déplacées et mises en ligne sur l’autre nœud.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-415">The resources then move and come online on the other node.</span></span>

### <a name="test-connectivity"></a><span data-ttu-id="6a7ab-416">Tester la connectivité</span><span class="sxs-lookup"><span data-stu-id="6a7ab-416">Test connectivity</span></span>

<span data-ttu-id="6a7ab-417">Pour tester la connectivité, connectez-vous à une autre machine virtuelle sur le même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-417">To test connectivity, log in to another virtual machine in the same virtual network.</span></span> <span data-ttu-id="6a7ab-418">Ouvrez **SQL Server Management Studio** et connectez-vous au nom FCI SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-418">Open **SQL Server Management Studio** and connect to the SQL Server FCI name.</span></span>

>[!NOTE]
><span data-ttu-id="6a7ab-419">Si nécessaire, vous pouvez [télécharger SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="6a7ab-420">Limitations</span><span class="sxs-lookup"><span data-stu-id="6a7ab-420">Limitations</span></span>
<span data-ttu-id="6a7ab-421">Sur les machines virtuelles Azure, Microsoft Distributed Transaction Coordinator (DTC) n’est pas pris en charge sur les instances de cluster de basculement car le port RPC n’est pas pris en charge par l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="6a7ab-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because the RPC port is not supported by the load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="6a7ab-422">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6a7ab-422">See Also</span></span>

[<span data-ttu-id="6a7ab-423">Configurer S2D avec le Bureau à distance (Azure)</span><span class="sxs-lookup"><span data-stu-id="6a7ab-423">Setup S2D with remote desktop (Azure)</span></span>](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

<span data-ttu-id="6a7ab-424">[Solution hyper-convergée avec Espaces de stockage direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="6a7ab-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

[<span data-ttu-id="6a7ab-425">Vue d’ensemble de l’espace de stockage direct</span><span class="sxs-lookup"><span data-stu-id="6a7ab-425">Storage Space Direct Overview</span></span>](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[<span data-ttu-id="6a7ab-426">Prise en charge de SQL Server pour S2D</span><span class="sxs-lookup"><span data-stu-id="6a7ab-426">SQL Server support for S2D</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
