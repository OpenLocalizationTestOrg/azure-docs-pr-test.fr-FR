---
title: "aaaSQL groupes de disponibilité de serveur - des Machines virtuelles Azure - didacticiel | Documents Microsoft"
description: "Ce didacticiel montre comment toocreate un SQL Server groupe de disponibilité AlwaysOn sur des Machines virtuelles Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="95a71-103">Configurer manuellement des groupes de disponibilité AlwaysOn dans une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="95a71-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="95a71-104">Ce didacticiel montre comment toocreate un SQL Server groupe de disponibilité AlwaysOn sur des Machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="95a71-104">This tutorial shows how toocreate a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="95a71-105">didacticiel complet de Hello crée un groupe de disponibilité avec un réplica de base de données sur deux serveurs SQL Server.</span><span class="sxs-lookup"><span data-stu-id="95a71-105">hello complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="95a71-106">**Durée estimée**: prend environ 30 minutes toocomplete une fois que les conditions préalables de hello sont remplies.</span><span class="sxs-lookup"><span data-stu-id="95a71-106">**Time estimate**: Takes about 30 minutes toocomplete once hello prerequisites are met.</span></span>

<span data-ttu-id="95a71-107">diagramme de Hello illustre ce que vous créez dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-107">hello diagram illustrates what you build in hello tutorial.</span></span>

![Groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="95a71-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="95a71-109">Prerequisites</span></span>

<span data-ttu-id="95a71-110">Hello est supposé qu'avoir une connaissance élémentaire de SQL Server groupes de disponibilité AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="95a71-110">hello tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="95a71-111">Pour plus d’informations, consultez [Vue d’ensemble des groupes de disponibilité AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span><span class="sxs-lookup"><span data-stu-id="95a71-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="95a71-112">Hello tableau suivant répertorie les conditions préalables de hello que vous avez besoin de toocomplete avant de commencer ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="95a71-112">hello following table lists hello prerequisites that you need toocomplete before starting this tutorial:</span></span>

|  |<span data-ttu-id="95a71-113">Prérequis</span><span class="sxs-lookup"><span data-stu-id="95a71-113">Requirement</span></span> |<span data-ttu-id="95a71-114">Description</span><span class="sxs-lookup"><span data-stu-id="95a71-114">Description</span></span> |
|----- |----- |----- |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="95a71-116">Deux serveurs SQL Server</span><span class="sxs-lookup"><span data-stu-id="95a71-116">Two SQL Servers</span></span> | <span data-ttu-id="95a71-117">- Dans un groupe à haute disponibilité Azure</span><span class="sxs-lookup"><span data-stu-id="95a71-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="95a71-118">- Dans un domaine</span><span class="sxs-lookup"><span data-stu-id="95a71-118">- In a single domain</span></span> <br/> <span data-ttu-id="95a71-119">- Avec la fonctionnalité de Clustering de basculement installée</span><span class="sxs-lookup"><span data-stu-id="95a71-119">- With Failover Clustering feature installed</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="95a71-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="95a71-121">Windows Server</span></span> | <span data-ttu-id="95a71-122">Partage de fichiers pour le témoin de cluster</span><span class="sxs-lookup"><span data-stu-id="95a71-122">File share for cluster witness</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="95a71-124">Compte du service SQL Server</span><span class="sxs-lookup"><span data-stu-id="95a71-124">SQL Server service account</span></span> | <span data-ttu-id="95a71-125">Compte du domaine</span><span class="sxs-lookup"><span data-stu-id="95a71-125">Domain account</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="95a71-127">Compte du service SQL Server Agent</span><span class="sxs-lookup"><span data-stu-id="95a71-127">SQL Server Agent service account</span></span> | <span data-ttu-id="95a71-128">Compte du domaine</span><span class="sxs-lookup"><span data-stu-id="95a71-128">Domain account</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="95a71-130">Ports du pare-feu ouverts</span><span class="sxs-lookup"><span data-stu-id="95a71-130">Firewall ports open</span></span> | <span data-ttu-id="95a71-131">- SQL Server : **1433** pour l’instance par défaut</span><span class="sxs-lookup"><span data-stu-id="95a71-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="95a71-132">- Point de terminaison de mise en miroir de bases de données : **5022** ou un port disponible</span><span class="sxs-lookup"><span data-stu-id="95a71-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="95a71-133">- Sonde d’équilibrage de charge Azure : **59999** ou un port disponible</span><span class="sxs-lookup"><span data-stu-id="95a71-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="95a71-135">Ajout de la fonctionnalité de Clustering de basculement</span><span class="sxs-lookup"><span data-stu-id="95a71-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="95a71-136">Fonctionnalité requise sur les deux serveurs SQL Server</span><span class="sxs-lookup"><span data-stu-id="95a71-136">Both SQL Servers require this feature</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="95a71-138">Compte du domaine d’installation</span><span class="sxs-lookup"><span data-stu-id="95a71-138">Installation domain account</span></span> | <span data-ttu-id="95a71-139">- Administrateur local sur chaque serveur SQL Server</span><span class="sxs-lookup"><span data-stu-id="95a71-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="95a71-140">- Membres du rôle de serveur fixe sysadmin pour chaque instance de SQL Server</span><span class="sxs-lookup"><span data-stu-id="95a71-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="95a71-141">Avant de commencer le didacticiel de hello, vous devez trop[remplir les conditions préalables pour la création de groupes de disponibilité AlwaysOn dans Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span><span class="sxs-lookup"><span data-stu-id="95a71-141">Before you begin hello tutorial, you need too[Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="95a71-142">Si ces conditions préalables ne sont déjà terminées, vous pouvez passer trop[création d’un Cluster](#CreateCluster).</span><span class="sxs-lookup"><span data-stu-id="95a71-142">If these prerequisites are completed already, you can jump too[Create Cluster](#CreateCluster).</span></span>


<span data-ttu-id="95a71-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Créer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="95a71-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## Create hello cluster</span></span>

<span data-ttu-id="95a71-144">Après avoir hello conditions préalables sont remplies, hello première étape consiste toocreate un Cluster de basculement Windows Server qui inclut deux serveurs de SQL et un serveur témoin.</span><span class="sxs-lookup"><span data-stu-id="95a71-144">After hello prerequisites are completed, hello first step is toocreate a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="95a71-145">RDP toohello première SQL Server à l’aide d’un compte de domaine qui est administrateur sur les serveurs SQL et le serveur témoin hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-145">RDP toohello first SQL Server using a domain account that is an administrator on both SQL Servers and hello witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="95a71-146">Si vous avez suivi hello [document configuration requise](virtual-machines-windows-portal-sql-availability-group-prereq.md), vous avez créé un compte appelé **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="95a71-146">If you followed hello [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="95a71-147">Utilisez ce compte.</span><span class="sxs-lookup"><span data-stu-id="95a71-147">Use this account.</span></span>

2. <span data-ttu-id="95a71-148">Bonjour **le Gestionnaire de serveur** tableau de bord, sélectionnez **outils**, puis cliquez sur **Gestionnaire du Cluster de basculement**.</span><span class="sxs-lookup"><span data-stu-id="95a71-148">In hello **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="95a71-149">Dans le volet gauche de hello, cliquez sur **Gestionnaire du Cluster de basculement**, puis cliquez sur **créer un Cluster**.</span><span class="sxs-lookup"><span data-stu-id="95a71-149">In hello left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="95a71-150">![Création d’un cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="95a71-150">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="95a71-151">Dans Assistant Création d’un Cluster de hello, créer un cluster à un nœud en parcourant les pages hello avec les paramètres de hello en hello tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="95a71-151">In hello Create Cluster Wizard, create a one-node cluster by stepping through hello pages with hello settings in hello following table:</span></span>

   | <span data-ttu-id="95a71-152">Page</span><span class="sxs-lookup"><span data-stu-id="95a71-152">Page</span></span> | <span data-ttu-id="95a71-153">Paramètres</span><span class="sxs-lookup"><span data-stu-id="95a71-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="95a71-154">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="95a71-154">Before You Begin</span></span> |<span data-ttu-id="95a71-155">Utilisation des valeurs par défaut</span><span class="sxs-lookup"><span data-stu-id="95a71-155">Use defaults</span></span> |
   | <span data-ttu-id="95a71-156">Sélection des serveurs</span><span class="sxs-lookup"><span data-stu-id="95a71-156">Select Servers</span></span> |<span data-ttu-id="95a71-157">Hello de type premier SQL Server nom de **nom du serveur** et cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="95a71-157">Type hello first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="95a71-158">Avertissement de validation</span><span class="sxs-lookup"><span data-stu-id="95a71-158">Validation Warning</span></span> |<span data-ttu-id="95a71-159">Sélectionnez **non. je ne nécessitent pas de prise en charge de Microsoft pour ce cluster et par conséquent ne voulez pas que la validation toorun hello teste. Lorsque vous cliquez sur Suivant, poursuivre la création de cluster de hello**.</span><span class="sxs-lookup"><span data-stu-id="95a71-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want toorun hello validation tests. When I click Next, continue Creating hello cluster**.</span></span> |
   | <span data-ttu-id="95a71-160">Point d’accès pour administration hello Cluster</span><span class="sxs-lookup"><span data-stu-id="95a71-160">Access Point for Administering hello Cluster</span></span> |<span data-ttu-id="95a71-161">Tapez un nom de cluster, par exemple **SQLAGCluster1** dans **Nom du cluster**.</span><span class="sxs-lookup"><span data-stu-id="95a71-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="95a71-162">Confirmation</span><span class="sxs-lookup"><span data-stu-id="95a71-162">Confirmation</span></span> |<span data-ttu-id="95a71-163">Utilisez les valeurs par défaut, sauf si vous utilisez des espaces de stockage.</span><span class="sxs-lookup"><span data-stu-id="95a71-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="95a71-164">Voir la Remarque hello sous ce tableau.</span><span class="sxs-lookup"><span data-stu-id="95a71-164">See hello note following this table.</span></span> |

### <a name="set-hello-cluster-ip-address"></a><span data-ttu-id="95a71-165">Définir l’adresse IP du cluster hello</span><span class="sxs-lookup"><span data-stu-id="95a71-165">Set hello cluster IP address</span></span>

1. <span data-ttu-id="95a71-166">Dans **Gestionnaire du Cluster de basculement**, faites défiler la liste trop**ressources principales du Cluster** et développez les détails du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-166">In **Failover Cluster Manager**, scroll down too**Cluster Core Resources** and expand hello cluster details.</span></span> <span data-ttu-id="95a71-167">Vous devez voir deux hello **nom** et hello **adresse IP** ressources Bonjour **n’a pas pu** état.</span><span class="sxs-lookup"><span data-stu-id="95a71-167">You should see both hello **Name** and hello **IP Address** resources in hello **Failed** state.</span></span> <span data-ttu-id="95a71-168">Hello ressource d’adresse IP ne peut pas être mises en ligne, car le cluster de hello est assigné hello même adresse IP en tant qu’ordinateur hello lui-même, par conséquent, il est une adresse en double.</span><span class="sxs-lookup"><span data-stu-id="95a71-168">hello IP address resource cannot be brought online because hello cluster is assigned hello same IP address as hello machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="95a71-169">Hello avec le bouton échoué **adresse IP** ressource, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="95a71-169">Right-click hello failed **IP Address** resource, and then click **Properties**.</span></span>

   ![Propriétés du cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="95a71-171">Sélectionnez **adresse IP statique** et spécifiez une adresse disponible à partir du sous-réseau dans lequel hello SQL Server est dans la zone de texte adresse hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-171">Select **Static IP Address** and specify an available address from subnet where hello SQL Server is in hello Address text box.</span></span> <span data-ttu-id="95a71-172">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="95a71-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="95a71-173">Bonjour **ressources principales du Cluster** , cliquez sur le nom de cluster et cliquez sur **mettre en ligne**.</span><span class="sxs-lookup"><span data-stu-id="95a71-173">In hello **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="95a71-174">Attendez que les deux ressources soient en ligne.</span><span class="sxs-lookup"><span data-stu-id="95a71-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="95a71-175">Lors de la ressource de nom de cluster hello est mis en ligne, il met à jour serveur du contrôleur de domaine hello avec un nouveau compte d’ordinateur Active Directory.</span><span class="sxs-lookup"><span data-stu-id="95a71-175">When hello cluster name resource comes online, it updates hello DC server with a new AD computer account.</span></span> <span data-ttu-id="95a71-176">Utilisez cette hello de toorun AD compte service de cluster du groupe de disponibilité plus tard.</span><span class="sxs-lookup"><span data-stu-id="95a71-176">Use this AD account toorun hello Availability Group clustered service later.</span></span>

### <span data-ttu-id="95a71-177"><a name="addNode"></a>Ajouter hello autres toocluster SQL Server</span><span class="sxs-lookup"><span data-stu-id="95a71-177"><a name="addNode"></a>Add hello other SQL Server toocluster</span></span>

<span data-ttu-id="95a71-178">Ajouter hello autre cluster toohello de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="95a71-178">Add hello other SQL Server toohello cluster.</span></span>

1. <span data-ttu-id="95a71-179">Dans l’arborescence du navigateur hello, cliquez sur le cluster de hello, sur **ajouter un nœud**.</span><span class="sxs-lookup"><span data-stu-id="95a71-179">In hello browser tree, right-click hello cluster and click **Add Node**.</span></span>

    ![Ajouter le nœud toohello Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="95a71-181">Bonjour **Assistant Ajout de nœud**, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="95a71-181">In hello **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="95a71-182">Bonjour **sélectionner des serveurs** , ajoutez hello du deuxième serveur SQL Server.</span><span class="sxs-lookup"><span data-stu-id="95a71-182">In hello **Select Servers** page, add hello second SQL Server.</span></span> <span data-ttu-id="95a71-183">Nom de serveur de type hello dans **nom du serveur** puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="95a71-183">Type hello server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="95a71-184">Une fois ces opérations effectuées, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="95a71-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="95a71-185">Bonjour **avertissement de Validation** , cliquez sur **non** (dans un scénario de production vous devez effectuer les tests de validation hello).</span><span class="sxs-lookup"><span data-stu-id="95a71-185">In hello **Validation Warning** page, click **No** (in a production scenario you should perform hello validation tests).</span></span> <span data-ttu-id="95a71-186">Cliquez ensuite sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="95a71-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="95a71-187">Bonjour **Confirmation** page si vous utilisez des espaces de stockage, hello désactivez case à cocher **ajouter tous les clusters de toohello totalité du stockage.**</span><span class="sxs-lookup"><span data-stu-id="95a71-187">In hello **Confirmation** page if you are using Storage Spaces, clear hello checkbox labeled **Add all eligible storage toohello cluster.**</span></span>

   ![Confirmation de l’ajout du nœud](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="95a71-189">Si vous utilisez des espaces de stockage et que vous ne désactivez pas **ajouter tous les totalité du stockage du cluster toohello**, Windows détache les disques virtuels hello pendant hello processus de clustering.</span><span class="sxs-lookup"><span data-stu-id="95a71-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage toohello cluster**, Windows detaches hello virtual disks during hello clustering process.</span></span> <span data-ttu-id="95a71-190">Par conséquent, ils n’apparaissent pas dans le Gestionnaire de disque ou de l’Explorateur, jusqu'à ce que les espaces de stockage hello sont supprimés du cluster de hello et rattachés à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="95a71-190">As a result, they do not appear in Disk Manager or Explorer until hello storage spaces are removed from hello cluster and reattached using PowerShell.</span></span> <span data-ttu-id="95a71-191">Les espaces de stockage regroupe plusieurs disques dans des pools toostorage.</span><span class="sxs-lookup"><span data-stu-id="95a71-191">Storage Spaces groups multiple disks in toostorage pools.</span></span> <span data-ttu-id="95a71-192">Pour plus d’informations, consultez la page [Espaces de stockage](https://technet.microsoft.com/library/hh831739).</span><span class="sxs-lookup"><span data-stu-id="95a71-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="95a71-193">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="95a71-193">Click **Next**.</span></span>

1. <span data-ttu-id="95a71-194">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="95a71-194">Click **Finish**.</span></span>

   <span data-ttu-id="95a71-195">Gestionnaire du Cluster de basculement indique que votre cluster a un nouveau nœud et il répertorie Bonjour **nœuds** conteneur.</span><span class="sxs-lookup"><span data-stu-id="95a71-195">Failover Cluster Manager shows that your cluster has a new node and lists it in hello **Nodes** container.</span></span>

10. <span data-ttu-id="95a71-196">Déconnecter la session de bureau à distance hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-196">Log out of hello remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="95a71-197">Ajouter un partage de fichiers de quorum de cluster</span><span class="sxs-lookup"><span data-stu-id="95a71-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="95a71-198">Dans cet exemple cluster de Windows hello utilise un toocreate de partage de fichier un quorum de cluster.</span><span class="sxs-lookup"><span data-stu-id="95a71-198">In this example hello Windows cluster uses a file share toocreate a cluster quorum.</span></span> <span data-ttu-id="95a71-199">Ce didacticiel utilise un quorum Nœud et partage de fichiers majoritaires.</span><span class="sxs-lookup"><span data-stu-id="95a71-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="95a71-200">Pour plus d’informations, consultez [Présentation des configurations de quorum dans un cluster de basculement](http://technet.microsoft.com/library/cc731739.aspx).</span><span class="sxs-lookup"><span data-stu-id="95a71-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="95a71-201">Connecter le serveur membre de témoin de partage de fichier toohello avec une session Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="95a71-201">Connect toohello file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="95a71-202">Dans **Gestionnaire de serveur**, cliquez sur **Outils**.</span><span class="sxs-lookup"><span data-stu-id="95a71-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="95a71-203">Ouvrez **Gestion de l’ordinateur**.</span><span class="sxs-lookup"><span data-stu-id="95a71-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="95a71-204">Cliquez sur **Dossiers partagés**.</span><span class="sxs-lookup"><span data-stu-id="95a71-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="95a71-205">Cliquez avec le bouton droit sur **Partages**, puis cliquez sur **Nouveau partage...**.</span><span class="sxs-lookup"><span data-stu-id="95a71-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Nouveau partage](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="95a71-207">Utilisez **créer un Assistant dossier partagé** toocreate un partage.</span><span class="sxs-lookup"><span data-stu-id="95a71-207">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="95a71-208">Sur **chemin d’accès du dossier**, cliquez sur **Parcourir** et localiser ou créer un chemin d’accès pour le dossier partagé de hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-208">On **Folder Path**, click **Browse** and locate or create a path for hello shared folder.</span></span> <span data-ttu-id="95a71-209">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="95a71-209">Click **Next**.</span></span>

1. <span data-ttu-id="95a71-210">Dans **nom, Description et paramètres** Vérifiez le nom de partage hello et chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="95a71-210">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="95a71-211">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="95a71-211">Click **Next**.</span></span>

1. <span data-ttu-id="95a71-212">Dans **Autorisations du dossier partagé**, sélectionnez **Personnaliser les autorisations**.</span><span class="sxs-lookup"><span data-stu-id="95a71-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="95a71-213">Cliquez sur **Personnalisé...**.</span><span class="sxs-lookup"><span data-stu-id="95a71-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="95a71-214">Dans **Personnaliser les autorisations**, cliquez sur **Ajouter...**.</span><span class="sxs-lookup"><span data-stu-id="95a71-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="95a71-215">Assurez-vous que ce cluster de hello toocreate hello compte utilisé dispose du contrôle total.</span><span class="sxs-lookup"><span data-stu-id="95a71-215">Make sure that hello account used toocreate hello cluster has full control.</span></span>

   ![Nouveau partage](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="95a71-217">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="95a71-217">Click **OK**.</span></span>

1. <span data-ttu-id="95a71-218">Dans **Autorisations du dossier partagé**, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="95a71-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="95a71-219">Cliquez à nouveau sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="95a71-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="95a71-220">Fermez la session sur le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="95a71-220">Log out of hello server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="95a71-221">Configurer le quorum du cluster</span><span class="sxs-lookup"><span data-stu-id="95a71-221">Configure cluster quorum</span></span>

<span data-ttu-id="95a71-222">Ensuite, définissez le quorum du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-222">Next, set hello cluster quorum.</span></span>

1. <span data-ttu-id="95a71-223">Se connecter toohello premier nœud du cluster avec le Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="95a71-223">Connect toohello first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="95a71-224">Dans **Gestionnaire du Cluster de basculement**, cliquez sur le cluster de hello, pointez trop**autres Actions**, puis cliquez sur **configurer les paramètres du Quorum du Cluster...** .</span><span class="sxs-lookup"><span data-stu-id="95a71-224">In **Failover Cluster Manager**, right-click hello cluster, point too**More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![Nouveau partage](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="95a71-226">Dans l’**Assistant Configuration de quorum du cluster**, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="95a71-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="95a71-227">Dans **sélectionner l’Option de Configuration de Quorum**, choisissez **sélectionner le témoin de quorum hello**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="95a71-227">In **Select Quorum Configuration Option**, choose **Select hello quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="95a71-228">Dans **Sélectionner le témoin de quorum**, cliquez sur **Configurer un témoin de partage de fichiers**.</span><span class="sxs-lookup"><span data-stu-id="95a71-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="95a71-229">Windows Server 2016 prend en charge un témoin cloud.</span><span class="sxs-lookup"><span data-stu-id="95a71-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="95a71-230">Si vous choisissez ce type de témoin, un témoin de partage de fichiers est inutile.</span><span class="sxs-lookup"><span data-stu-id="95a71-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="95a71-231">Pour plus d’informations, consultez [Déployer un témoin cloud pour un cluster de basculement](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="95a71-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="95a71-232">Ce didacticiel utilise un témoin de partage de fichiers, que les systèmes d’exploitation antérieurs prennent en charge.</span><span class="sxs-lookup"><span data-stu-id="95a71-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="95a71-233">Sur **témoin de partage de fichier de configuration**, chemin d’accès de type hello pour partage hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="95a71-233">On **Configure File Share Witness**, type hello path for hello share you created.</span></span> <span data-ttu-id="95a71-234">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="95a71-234">Click **Next**.</span></span>

1. <span data-ttu-id="95a71-235">Vérifiez les paramètres de hello sur **Confirmation**.</span><span class="sxs-lookup"><span data-stu-id="95a71-235">Verify hello settings on **Confirmation**.</span></span> <span data-ttu-id="95a71-236">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="95a71-236">Click **Next**.</span></span>

1. <span data-ttu-id="95a71-237">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="95a71-237">Click **Finish**.</span></span>

<span data-ttu-id="95a71-238">ressources principales du cluster Hello sont configurés avec un témoin de partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="95a71-238">hello cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="95a71-239">Activer les groupes de disponibilité</span><span class="sxs-lookup"><span data-stu-id="95a71-239">Enable Availability Groups</span></span>

<span data-ttu-id="95a71-240">Ensuite, activez hello **groupes de disponibilité AlwaysOn** fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="95a71-240">Next, enable hello **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="95a71-241">Effectuez ces étapes pour les deux serveurs SQL Server.</span><span class="sxs-lookup"><span data-stu-id="95a71-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="95a71-242">À partir de hello **Démarrer** écran, lancez **Gestionnaire de Configuration SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="95a71-242">From hello **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="95a71-243">Dans l’arborescence du navigateur hello, cliquez sur **SQL Server Services**, puis cliquez sur hello **SQL Server (MSSQLSERVER)** , puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="95a71-243">In hello browser tree, click **SQL Server Services**, then right-click hello **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="95a71-244">Cliquez sur hello **haute disponibilité AlwaysOn** , puis sélectionnez **activer les groupes de disponibilité AlwaysOn**, comme suit :</span><span class="sxs-lookup"><span data-stu-id="95a71-244">Click hello **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![Activation des groupes à haute disponibilité AlwaysOn](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="95a71-246">Cliquez sur **Apply**.</span><span class="sxs-lookup"><span data-stu-id="95a71-246">Click **Apply**.</span></span> <span data-ttu-id="95a71-247">Cliquez sur **OK** dans la boîte de dialogue contextuelle hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-247">Click **OK** in hello pop-up dialog.</span></span>

5. <span data-ttu-id="95a71-248">Redémarrez le service SQL Server de hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-248">Restart hello SQL Server service.</span></span>

<span data-ttu-id="95a71-249">Répétez ces étapes sur hello autre serveur SQL Server.</span><span class="sxs-lookup"><span data-stu-id="95a71-249">Repeat these steps on hello other SQL Server.</span></span>

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a><span data-ttu-id="95a71-250">Créer une base de données sur hello premier serveur SQL Server</span><span class="sxs-lookup"><span data-stu-id="95a71-250">Create a database on hello first SQL Server</span></span>

1. <span data-ttu-id="95a71-251">Lancement hello RDP fichier toohello première SQL Server avec un domaine de compte qui est membre de sysadmin de rôle de serveur fixe.</span><span class="sxs-lookup"><span data-stu-id="95a71-251">Launch hello RDP file toohello first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="95a71-252">Ouvrez SQL Server Management Studio et connectez-vous toohello premier serveur SQL Server.</span><span class="sxs-lookup"><span data-stu-id="95a71-252">Open SQL Server Management Studio and connect toohello first SQL Server.</span></span>
7. <span data-ttu-id="95a71-253">Dans l’**Explorateur d’objets**, cliquez avec le bouton droit sur **Bases de données**, puis cliquez sur **Nouvelle base de données**.</span><span class="sxs-lookup"><span data-stu-id="95a71-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="95a71-254">Dans **Nom de base de données**, saisissez **MyDB1**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="95a71-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <span data-ttu-id="95a71-255"><a name="backupshare"></a> Créer un partage de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="95a71-255"><a name="backupshare"></a> Create a backup share</span></span>

1. <span data-ttu-id="95a71-256">Sur hello première SQL Server dans **le Gestionnaire de serveur**, cliquez sur **outils**.</span><span class="sxs-lookup"><span data-stu-id="95a71-256">On hello first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="95a71-257">Ouvrez **Gestion de l’ordinateur**.</span><span class="sxs-lookup"><span data-stu-id="95a71-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="95a71-258">Cliquez sur **Dossiers partagés**.</span><span class="sxs-lookup"><span data-stu-id="95a71-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="95a71-259">Cliquez avec le bouton droit sur **Partages**, puis cliquez sur **Nouveau partage...**.</span><span class="sxs-lookup"><span data-stu-id="95a71-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Nouveau partage](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="95a71-261">Utilisez **créer un Assistant dossier partagé** toocreate un partage.</span><span class="sxs-lookup"><span data-stu-id="95a71-261">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="95a71-262">Sur **chemin d’accès du dossier**, cliquez sur **Parcourir** et localiser ou créer un chemin d’accès pour le dossier partagé sauvegarde de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-262">On **Folder Path**, click **Browse** and locate or create a path for hello database backup shared folder.</span></span> <span data-ttu-id="95a71-263">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="95a71-263">Click **Next**.</span></span>

1. <span data-ttu-id="95a71-264">Dans **nom, Description et paramètres** Vérifiez le nom de partage hello et chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="95a71-264">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="95a71-265">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="95a71-265">Click **Next**.</span></span>

1. <span data-ttu-id="95a71-266">Dans **Autorisations du dossier partagé**, sélectionnez **Personnaliser les autorisations**.</span><span class="sxs-lookup"><span data-stu-id="95a71-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="95a71-267">Cliquez sur **Personnalisé...**.</span><span class="sxs-lookup"><span data-stu-id="95a71-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="95a71-268">Dans **Personnaliser les autorisations**, cliquez sur **Ajouter...**.</span><span class="sxs-lookup"><span data-stu-id="95a71-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="95a71-269">Assurez-vous que contrôle total sur les comptes de service hello SQL Server et SQL Server Agent pour les deux serveurs.</span><span class="sxs-lookup"><span data-stu-id="95a71-269">Make sure that hello SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![Nouveau partage](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="95a71-271">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="95a71-271">Click **OK**.</span></span>

1. <span data-ttu-id="95a71-272">Dans **Autorisations du dossier partagé**, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="95a71-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="95a71-273">Cliquez à nouveau sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="95a71-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-hello-database"></a><span data-ttu-id="95a71-274">Effectuer une sauvegarde de base de données hello complète</span><span class="sxs-lookup"><span data-stu-id="95a71-274">Take a full backup of hello database</span></span>

<span data-ttu-id="95a71-275">Vous devez tooback hello nouvelle base de données tooinitialize hello journal dans la chaîne.</span><span class="sxs-lookup"><span data-stu-id="95a71-275">You need tooback up hello new database tooinitialize hello log chain.</span></span> <span data-ttu-id="95a71-276">Si vous ne prenez pas une sauvegarde de base de données hello, il ne peut pas être inclus dans un groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="95a71-276">If you do not take a backup of hello new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="95a71-277">Dans **l’Explorateur d’objets**, avec le bouton droit de la base de données hello, pointez trop**tâches...** , cliquez sur **Back Up**.</span><span class="sxs-lookup"><span data-stu-id="95a71-277">In **Object Explorer**, right-click hello database, point too**Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="95a71-278">Cliquez sur **OK** tootake un emplacement de sauvegarde par défaut toohello sauvegarde complète.</span><span class="sxs-lookup"><span data-stu-id="95a71-278">Click **OK** tootake a full backup toohello default backup location.</span></span>

## <a name="create-hello-availability-group"></a><span data-ttu-id="95a71-279">Créer le groupe de disponibilité de hello</span><span class="sxs-lookup"><span data-stu-id="95a71-279">Create hello Availability Group</span></span>
<span data-ttu-id="95a71-280">Vous êtes maintenant prêt tooconfigure étapes d’un groupe de disponibilité à l’aide de hello suivant :</span><span class="sxs-lookup"><span data-stu-id="95a71-280">You are now ready tooconfigure an Availability Group using hello following steps:</span></span>

* <span data-ttu-id="95a71-281">Créer une base de données sur hello premier serveur SQL Server.</span><span class="sxs-lookup"><span data-stu-id="95a71-281">Create a database on hello first SQL Server.</span></span>
* <span data-ttu-id="95a71-282">Effectuez une sauvegarde complète et une sauvegarde du journal des transactions de base de données hello</span><span class="sxs-lookup"><span data-stu-id="95a71-282">Take both a full backup and a transaction log backup of hello database</span></span>
* <span data-ttu-id="95a71-283">Hello de restauration complète et toohello de sauvegardes de journal deuxième SQL Server avec hello **NORECOVERY** option</span><span class="sxs-lookup"><span data-stu-id="95a71-283">Restore hello full and log backups toohello second SQL Server with hello **NORECOVERY** option</span></span>
* <span data-ttu-id="95a71-284">Créer le groupe de disponibilité de hello (**AG1**) avec validation synchrone, le basculement automatique et réplicas secondaires lisibles</span><span class="sxs-lookup"><span data-stu-id="95a71-284">Create hello Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-hello-availability-group"></a><span data-ttu-id="95a71-285">Créer le groupe de disponibilité de hello :</span><span class="sxs-lookup"><span data-stu-id="95a71-285">Create hello Availability Group:</span></span>

1. <span data-ttu-id="95a71-286">Sur la session Bureau à distance toohello premier serveur SQL Server.</span><span class="sxs-lookup"><span data-stu-id="95a71-286">On remote desktop session toohello first SQL Server.</span></span> <span data-ttu-id="95a71-287">Dans l’**Explorateur d’objets** dans SSMS, cliquez avec le bouton droit sur **Haute disponibilité AlwaysOn**, puis cliquez sur **Assistant Nouveau groupe de disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="95a71-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![Lancer l'Assistant Nouveau groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="95a71-289">Bonjour **Introduction** , cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="95a71-289">In hello **Introduction** page, click **Next**.</span></span> <span data-ttu-id="95a71-290">Bonjour **spécifier un nom de groupe de disponibilité** , tapez un nom pour hello groupe de disponibilité, par exemple **AG1**, dans **nom du groupe de disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="95a71-290">In hello **Specify Availability Group Name** page, type a name for hello Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="95a71-291">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="95a71-291">Click **Next**.</span></span>

    ![Assistant Nouveau groupe de disponibilité, spécifier le nom du groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="95a71-293">Bonjour **sélectionner les bases de données** page, sélectionnez votre base de données, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="95a71-293">In hello **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="95a71-294">base de données Hello remplit les conditions préalables de hello pour un groupe de disponibilité car vous avez effectué au moins une sauvegarde complète sur le réplica principal de hello prévue.</span><span class="sxs-lookup"><span data-stu-id="95a71-294">hello database meets hello prerequisites for an Availability Group because you have taken at least one full backup on hello intended primary replica.</span></span>

   ![Assistant Nouveau groupe de disponibilité, sélectionner les bases de données](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="95a71-296">Bonjour **spécifier les réplicas** , cliquez sur **ajouter un réplica**.</span><span class="sxs-lookup"><span data-stu-id="95a71-296">In hello **Specify Replicas** page, click **Add Replica**.</span></span>

   ![Assistant Nouveau groupe de disponibilité, spécifier les réplicas](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="95a71-298">Hello **connecter tooServer** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="95a71-298">hello **Connect tooServer** dialog pops up.</span></span> <span data-ttu-id="95a71-299">Nom du type hello du serveur de deuxième hello dans **nom du serveur**.</span><span class="sxs-lookup"><span data-stu-id="95a71-299">Type hello name of hello second server in **Server name**.</span></span> <span data-ttu-id="95a71-300">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="95a71-300">Click **Connect**.</span></span>

   <span data-ttu-id="95a71-301">Dans hello **spécifier les réplicas** page, vous devez maintenant voir hello second serveur répertorié dans **réplicas de disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="95a71-301">Back in hello **Specify Replicas** page, you should now see hello second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="95a71-302">Configurez les réplicas hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="95a71-302">Configure hello replicas as follows.</span></span>

   ![Assistant Nouveau groupe de disponibilité, spécifier les réplicas (Terminé)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="95a71-304">Cliquez sur **points de terminaison** toosee hello mise en miroir point de terminaison pour ce groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="95a71-304">Click **Endpoints** toosee hello database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="95a71-305">Hello d’utiliser le même port que vous avez utilisé lorsque vous définissez hello [règle de pare-feu pour les points de terminaison de mise en miroir de base de données](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="95a71-305">Use hello same port that you used when you set hello [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![Assistant Nouveau groupe de disponibilité, sélectionner la synchronisation initiale des données](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="95a71-307">Bonjour **sélectionner la synchronisation initiale des données** , sélectionnez **complète** et spécifiez un emplacement réseau partagé.</span><span class="sxs-lookup"><span data-stu-id="95a71-307">In hello **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="95a71-308">Pour l’emplacement de hello, utiliser hello [partage de sauvegarde que vous avez créé](#backupshare).</span><span class="sxs-lookup"><span data-stu-id="95a71-308">For hello location, use hello [backup share that you created](#backupshare).</span></span> <span data-ttu-id="95a71-309">Dans l’exemple hello qu’il a été, **\\\\\<premier SQL Server\>\Backup\**.</span><span class="sxs-lookup"><span data-stu-id="95a71-309">In hello example it was, **\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="95a71-310">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="95a71-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="95a71-311">Synchronisation complète effectue une sauvegarde complète de base de données hello hello première instance de SQL Server et il restaure toohello une deuxième instance.</span><span class="sxs-lookup"><span data-stu-id="95a71-311">Full synchronization takes a full backup of hello database on hello first instance of SQL Server and restores it toohello second instance.</span></span> <span data-ttu-id="95a71-312">Pour les bases de données volumineuses, une synchronisation complète n’est pas recommandée, car elle peut prendre longtemps.</span><span class="sxs-lookup"><span data-stu-id="95a71-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="95a71-313">Vous pouvez réduire ce délai en manuellement une sauvegarde de base de données hello et sa restauration avec `NO RECOVERY`.</span><span class="sxs-lookup"><span data-stu-id="95a71-313">You can reduce this time by manually taking a backup of hello database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="95a71-314">Si la base de données hello est déjà restaurée avec `NO RECOVERY` sur hello deuxième SQL Server avant de configurer le groupe de disponibilité de hello, choisissez **joindre uniquement**.</span><span class="sxs-lookup"><span data-stu-id="95a71-314">If hello database is already restored with `NO RECOVERY` on hello second SQL Server before configuring hello Availability Group, choose **Join only**.</span></span> <span data-ttu-id="95a71-315">Si vous souhaitez la sauvegarde de hello tootake après avoir configuré le groupe de disponibilité de hello, choisissez **ignorer la synchronisation initiale des données**.</span><span class="sxs-lookup"><span data-stu-id="95a71-315">If you want tootake hello backup after configuring hello Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![Assistant Nouveau groupe de disponibilité, sélectionner la synchronisation initiale des données](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="95a71-317">Bonjour **Validation** , cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="95a71-317">In hello **Validation** page, click **Next**.</span></span> <span data-ttu-id="95a71-318">Cette page doit être similaire toohello suivant l’image :</span><span class="sxs-lookup"><span data-stu-id="95a71-318">This page should look similar toohello following image:</span></span>

    ![Assistant Nouveau groupe de disponibilité, validation](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="95a71-320">Il est un avertissement pour la configuration de l’écouteur hello, car vous n’avez pas configuré un écouteur de groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="95a71-320">There is a warning for hello listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="95a71-321">Vous pouvez ignorer cet avertissement, car sur les machines virtuelles que vous créez les écouteur hello après la création d’équilibrage de charge Azure hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-321">You can ignore this warning because on Azure virtual machines you create hello listener after creating hello Azure load balancer.</span></span>

10. <span data-ttu-id="95a71-322">Bonjour **Résumé** , cliquez sur **Terminer**, puis patientez pendant que l’Assistant hello configure hello nouveau groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="95a71-322">In hello **Summary** page, click **Finish**, then wait while hello wizard configures hello new Availability Group.</span></span> <span data-ttu-id="95a71-323">Bonjour **progression** page, vous pouvez cliquer sur **plus de détails** tooview hello détaillées de progression.</span><span class="sxs-lookup"><span data-stu-id="95a71-323">In hello **Progress** page, you can click **More details** tooview hello detailed progress.</span></span> <span data-ttu-id="95a71-324">Une fois l’Assistant de hello est terminé, vérifiez que hello **résultats** tooverify page qui hello du groupe de disponibilité est créé avec succès.</span><span class="sxs-lookup"><span data-stu-id="95a71-324">Once hello wizard is finished, inspect hello **Results** page tooverify that hello Availability Group is successfully created.</span></span>

     ![Assistant Nouveau groupe de disponibilité, résultats](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="95a71-326">Cliquez sur **fermer** Assistant de hello tooexit.</span><span class="sxs-lookup"><span data-stu-id="95a71-326">Click **Close** tooexit hello wizard.</span></span>

### <a name="check-hello-availability-group"></a><span data-ttu-id="95a71-327">Hello de vérification de groupe de disponibilité</span><span class="sxs-lookup"><span data-stu-id="95a71-327">Check hello Availability Group</span></span>

1. <span data-ttu-id="95a71-328">Dans l’**Explorateur d’objets**, développez **Haute disponibilité AlwaysOn**, puis **Groupes de disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="95a71-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="95a71-329">Vous devez maintenant voir hello du nouveau groupe de disponibilité de ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="95a71-329">You should now see hello new Availability Group in this container.</span></span> <span data-ttu-id="95a71-330">Avec le bouton droit hello groupe de disponibilité, puis cliquez sur **afficher le tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="95a71-330">Right-click hello Availability Group and click **Show Dashboard**.</span></span>

   ![Afficher le tableau de bord de groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="95a71-332">Votre **tableau de bord AlwaysOn** doit ressembler toothis similaire.</span><span class="sxs-lookup"><span data-stu-id="95a71-332">Your **AlwaysOn Dashboard** should look similar toothis.</span></span>

   ![Tableau de bord de groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="95a71-334">Vous pouvez voir les réplicas hello, le mode de basculement hello de chaque état de synchronisation de réplica et hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-334">You can see hello replicas, hello failover mode of each replica and hello synchronization state.</span></span>

2. <span data-ttu-id="95a71-335">Dans le **Gestionnaire du cluster de basculement**, cliquez sur votre cluster.</span><span class="sxs-lookup"><span data-stu-id="95a71-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="95a71-336">Sélectionnez **Rôles**.</span><span class="sxs-lookup"><span data-stu-id="95a71-336">Select **Roles**.</span></span> <span data-ttu-id="95a71-337">nom de groupe de disponibilité de Hello utilisé est un rôle sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-337">hello Availability Group name you used is a role on hello cluster.</span></span> <span data-ttu-id="95a71-338">Ce groupe de disponibilité n’a pas une adresse IP pour les connexions clientes, car vous n’avez pas configuré d’écouteur.</span><span class="sxs-lookup"><span data-stu-id="95a71-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="95a71-339">Vous allez configurer le port d’écoute hello après avoir créé un équilibrage de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="95a71-339">You will configure hello listener after you create an Azure load balancer.</span></span>

   ![Groupe de disponibilité dans le Gestionnaire du cluster de basculement](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="95a71-341">N’essayez pas de toofail sur hello groupe de disponibilité à partir de hello Gestionnaire du Cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="95a71-341">Do not try toofail over hello Availability Group from hello Failover Cluster Manager.</span></span> <span data-ttu-id="95a71-342">Vous devez effectuer toutes les opérations de basculement à partir du **tableau de bord AlwaysOn** dans SSMS.</span><span class="sxs-lookup"><span data-stu-id="95a71-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="95a71-343">Pour plus d’informations, consultez [Restrictions d’utilisation hello Gestionnaire du Cluster de basculement avec des groupes de disponibilité](https://msdn.microsoft.com/library/ff929171.aspx).</span><span class="sxs-lookup"><span data-stu-id="95a71-343">For more information, see [Restrictions on Using hello Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="95a71-344">À ce stade, vous avez un groupe de disponibilité avec des réplicas sur les deux instances de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="95a71-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="95a71-345">Vous pouvez déplacer hello groupe de disponibilité entre des instances.</span><span class="sxs-lookup"><span data-stu-id="95a71-345">You can move hello Availability Group between instances.</span></span> <span data-ttu-id="95a71-346">Connexion impossible toohello groupe de disponibilité encore car vous ne disposez pas d’un écouteur.</span><span class="sxs-lookup"><span data-stu-id="95a71-346">You cannot connect toohello Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="95a71-347">Dans Azure virtual machines, port d’écoute hello requiert un équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="95a71-347">In Azure virtual machines, hello listener requires a load balancer.</span></span> <span data-ttu-id="95a71-348">étape suivante de Hello est un équilibreur de charge toocreate hello dans Azure.</span><span class="sxs-lookup"><span data-stu-id="95a71-348">hello next step is toocreate hello load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="95a71-349">Crée un équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="95a71-349">Create an Azure load balancer</span></span>

<span data-ttu-id="95a71-350">Sur les machines virtuelles Azure, un groupe de disponibilité SQL Serveur requiert un équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="95a71-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="95a71-351">équilibrage de charge Hello conserve adresse hello pour l’écouteur de groupe de disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-351">hello load balancer holds hello IP address for hello Availability Group listener.</span></span> <span data-ttu-id="95a71-352">Cette section résume comment toocreate hello l’équilibrage de charge Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="95a71-352">This section summarizes how toocreate hello load balancer in hello Azure portal.</span></span>

1. <span data-ttu-id="95a71-353">Bonjour portail Azure, accédez à toohello groupe de ressources où vos serveurs SQL sont et cliquez sur **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="95a71-353">In hello Azure portal, go toohello resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="95a71-354">Recherchez **Équilibrage de charge**.</span><span class="sxs-lookup"><span data-stu-id="95a71-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="95a71-355">Choisissez l’équilibrage de charge hello publié par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="95a71-355">Choose hello load balancer published by Microsoft.</span></span>

   ![Groupe de disponibilité dans le Gestionnaire du cluster de basculement](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="95a71-357">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="95a71-357">Click **Create**.</span></span>
3. <span data-ttu-id="95a71-358">Configurer hello suivant les paramètres d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-358">Configure hello following parameters for hello load balancer.</span></span>

   | <span data-ttu-id="95a71-359">Paramètre</span><span class="sxs-lookup"><span data-stu-id="95a71-359">Setting</span></span> | <span data-ttu-id="95a71-360">Champ</span><span class="sxs-lookup"><span data-stu-id="95a71-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="95a71-361">**Name**</span><span class="sxs-lookup"><span data-stu-id="95a71-361">**Name**</span></span> |<span data-ttu-id="95a71-362">Utiliser un nom pour l’équilibrage de charge hello, par exemple **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="95a71-362">Use a text name for hello load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="95a71-363">**Type**</span><span class="sxs-lookup"><span data-stu-id="95a71-363">**Type**</span></span> |<span data-ttu-id="95a71-364">Interne</span><span class="sxs-lookup"><span data-stu-id="95a71-364">Internal</span></span> |
   | <span data-ttu-id="95a71-365">**Réseau virtuel**</span><span class="sxs-lookup"><span data-stu-id="95a71-365">**Virtual network**</span></span> |<span data-ttu-id="95a71-366">Utiliser le nom hello Hello réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="95a71-366">Use hello name of hello Azure virtual network.</span></span> |
   | <span data-ttu-id="95a71-367">**Sous-réseau**</span><span class="sxs-lookup"><span data-stu-id="95a71-367">**Subnet**</span></span> |<span data-ttu-id="95a71-368">Utiliser le nom hello de sous-réseau hello hello d’ordinateur virtuel est dans.</span><span class="sxs-lookup"><span data-stu-id="95a71-368">Use hello name of hello subnet that hello virtual machine is in.</span></span>  |
   | <span data-ttu-id="95a71-369">**Affectation d’adresses IP**</span><span class="sxs-lookup"><span data-stu-id="95a71-369">**IP address assignment**</span></span> |<span data-ttu-id="95a71-370">Statique</span><span class="sxs-lookup"><span data-stu-id="95a71-370">Static</span></span> |
   | <span data-ttu-id="95a71-371">**Adresse IP**</span><span class="sxs-lookup"><span data-stu-id="95a71-371">**IP address**</span></span> |<span data-ttu-id="95a71-372">Utilisez une adresse disponible du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="95a71-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="95a71-373">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="95a71-373">**Subscription**</span></span> |<span data-ttu-id="95a71-374">Utilisez hello même abonnement que l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-374">Use hello same subscription as hello virtual machine.</span></span> |
   | <span data-ttu-id="95a71-375">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="95a71-375">**Location**</span></span> |<span data-ttu-id="95a71-376">Utilisez hello même emplacement que l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-376">Use hello same location as hello virtual machine.</span></span> |

   <span data-ttu-id="95a71-377">Hello panneau portail Azure doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="95a71-377">hello Azure portal blade should look like this:</span></span>

   ![Créer un équilibreur de charge](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="95a71-379">Cliquez sur **créer**, équilibrage de charge toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-379">Click **Create**, toocreate hello load balancer.</span></span>

<span data-ttu-id="95a71-380">équilibrage de charge tooconfigure hello, vous devez toocreate un pool principal, une sonde, ensemble hello équilibrage de charge et les règles.</span><span class="sxs-lookup"><span data-stu-id="95a71-380">tooconfigure hello load balancer, you need toocreate a backend pool, a probe, and set hello load balancing rules.</span></span> <span data-ttu-id="95a71-381">Procédez comme suit dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="95a71-381">Do these in hello Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="95a71-382">Ajouter le pool principal</span><span class="sxs-lookup"><span data-stu-id="95a71-382">Add backend pool</span></span>

1. <span data-ttu-id="95a71-383">Bonjour portail Azure, accédez à tooyour le groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="95a71-383">In hello Azure portal, go tooyour availability group.</span></span> <span data-ttu-id="95a71-384">Vous devrez peut-être l’équilibrage de charge toorefresh hello vue toosee hello nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="95a71-384">You might need toorefresh hello view toosee hello newly created load balancer.</span></span>

   ![Rechercher l’équilibrage de charge dans le groupe de ressources](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="95a71-386">Sur l’équilibrage de charge hello, cliquez sur **pools principaux**, puis cliquez sur **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="95a71-386">Click hello load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="95a71-387">Définissez le pool principal d’hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="95a71-387">Set hello backend pool as follows:</span></span>

   | <span data-ttu-id="95a71-388">Paramètre</span><span class="sxs-lookup"><span data-stu-id="95a71-388">Setting</span></span> | <span data-ttu-id="95a71-389">Description</span><span class="sxs-lookup"><span data-stu-id="95a71-389">Description</span></span> | <span data-ttu-id="95a71-390">Exemple</span><span class="sxs-lookup"><span data-stu-id="95a71-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="95a71-391">**Nom**</span><span class="sxs-lookup"><span data-stu-id="95a71-391">**Name**</span></span> | <span data-ttu-id="95a71-392">Tapez un nom.</span><span class="sxs-lookup"><span data-stu-id="95a71-392">Type a text name</span></span> | <span data-ttu-id="95a71-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="95a71-393">SQLLBBE</span></span>
   | <span data-ttu-id="95a71-394">**Associé à**</span><span class="sxs-lookup"><span data-stu-id="95a71-394">**Associated to**</span></span> | <span data-ttu-id="95a71-395">Choisir dans la liste</span><span class="sxs-lookup"><span data-stu-id="95a71-395">Pick from list</span></span> | <span data-ttu-id="95a71-396">Groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="95a71-396">Availability set</span></span>
   | <span data-ttu-id="95a71-397">**Groupe à haute disponibilité**</span><span class="sxs-lookup"><span data-stu-id="95a71-397">**Availability set**</span></span> | <span data-ttu-id="95a71-398">Utilisez un nom de groupe à haute disponibilité hello situés dans vos machines virtuelles SQL Server</span><span class="sxs-lookup"><span data-stu-id="95a71-398">Use a name of hello availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="95a71-399">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="95a71-399">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="95a71-400">**Machines virtuelles**</span><span class="sxs-lookup"><span data-stu-id="95a71-400">**Virtual machines**</span></span> |<span data-ttu-id="95a71-401">Hello deux noms de machine virtuelle Azure SQL Server</span><span class="sxs-lookup"><span data-stu-id="95a71-401">hello two Azure SQL Server VM names</span></span> | <span data-ttu-id="95a71-402">sqlserver-0, sqlserver-1</span><span class="sxs-lookup"><span data-stu-id="95a71-402">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="95a71-403">Nom de type hello pour le pool de back-end hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-403">Type hello name for hello back end pool.</span></span>

1. <span data-ttu-id="95a71-404">Cliquez sur **+ Ajouter une machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="95a71-404">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="95a71-405">Pour l’ensemble de disponibilité hello, choisissez hello haute disponibilité que hello sont des serveurs SQL Server dans.</span><span class="sxs-lookup"><span data-stu-id="95a71-405">For hello availability set, choose hello availability set that hello SQL Servers are in.</span></span>

1. <span data-ttu-id="95a71-406">Pour les ordinateurs virtuels, vous pouvez inclure les deux hello serveurs SQL Server.</span><span class="sxs-lookup"><span data-stu-id="95a71-406">For virtual machines, include both of hello SQL Servers.</span></span> <span data-ttu-id="95a71-407">N’incluez pas de serveur témoin de partage de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-407">Do not include hello file share witness server.</span></span>

1. <span data-ttu-id="95a71-408">Cliquez sur **OK** pool principal de toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-408">Click **OK** toocreate hello backend pool.</span></span>

### <a name="set-hello-probe"></a><span data-ttu-id="95a71-409">Sonde de hello ensemble</span><span class="sxs-lookup"><span data-stu-id="95a71-409">Set hello probe</span></span>

1. <span data-ttu-id="95a71-410">Sur l’équilibrage de charge hello, cliquez sur **sondes d’intégrité**, puis cliquez sur **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="95a71-410">Click hello load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="95a71-411">Définir la détection de l’intégrité de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="95a71-411">Set hello health probe as follows:</span></span>

   | <span data-ttu-id="95a71-412">Paramètre</span><span class="sxs-lookup"><span data-stu-id="95a71-412">Setting</span></span> | <span data-ttu-id="95a71-413">Description</span><span class="sxs-lookup"><span data-stu-id="95a71-413">Description</span></span> | <span data-ttu-id="95a71-414">Exemple</span><span class="sxs-lookup"><span data-stu-id="95a71-414">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="95a71-415">**Nom**</span><span class="sxs-lookup"><span data-stu-id="95a71-415">**Name**</span></span> | <span data-ttu-id="95a71-416">Texte</span><span class="sxs-lookup"><span data-stu-id="95a71-416">Text</span></span> | <span data-ttu-id="95a71-417">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="95a71-417">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="95a71-418">**Protocole**</span><span class="sxs-lookup"><span data-stu-id="95a71-418">**Protocol**</span></span> | <span data-ttu-id="95a71-419">Choisissez TCP.</span><span class="sxs-lookup"><span data-stu-id="95a71-419">Choose TCP</span></span> | <span data-ttu-id="95a71-420">TCP</span><span class="sxs-lookup"><span data-stu-id="95a71-420">TCP</span></span> |
   | <span data-ttu-id="95a71-421">**Port**</span><span class="sxs-lookup"><span data-stu-id="95a71-421">**Port**</span></span> | <span data-ttu-id="95a71-422">Tout port inutilisé.</span><span class="sxs-lookup"><span data-stu-id="95a71-422">Any unused port</span></span> | <span data-ttu-id="95a71-423">59999</span><span class="sxs-lookup"><span data-stu-id="95a71-423">59999</span></span> |
   | <span data-ttu-id="95a71-424">**Intervalle**</span><span class="sxs-lookup"><span data-stu-id="95a71-424">**Interval**</span></span>  | <span data-ttu-id="95a71-425">Durée Hello entre sonde tentatives en secondes</span><span class="sxs-lookup"><span data-stu-id="95a71-425">hello amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="95a71-426">5</span><span class="sxs-lookup"><span data-stu-id="95a71-426">5</span></span> |
   | <span data-ttu-id="95a71-427">**Seuil de défaillance sur le plan de l’intégrité**</span><span class="sxs-lookup"><span data-stu-id="95a71-427">**Unhealthy threshold**</span></span> | <span data-ttu-id="95a71-428">nombre d’échecs de sonde consécutifs devant se produire pour une toobe de machine virtuelle considéré comme non intègre de Hello</span><span class="sxs-lookup"><span data-stu-id="95a71-428">hello number of consecutive probe failures that must occur for a virtual machine toobe considered unhealthy</span></span>  | <span data-ttu-id="95a71-429">2</span><span class="sxs-lookup"><span data-stu-id="95a71-429">2</span></span> |

1. <span data-ttu-id="95a71-430">Cliquez sur **OK** sonde d’intégrité tooset hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-430">Click **OK** tooset hello health probe.</span></span>

### <a name="set-hello-load-balancing-rules"></a><span data-ttu-id="95a71-431">Définir des règles d’équilibrage de charge de hello</span><span class="sxs-lookup"><span data-stu-id="95a71-431">Set hello load balancing rules</span></span>

1. <span data-ttu-id="95a71-432">Sur l’équilibrage de charge hello, cliquez sur **règles d’équilibrage de charge**, puis cliquez sur **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="95a71-432">Click hello load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="95a71-433">Définissez comme suit les règles d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-433">Set hello load balancing rules as follows.</span></span>
   | <span data-ttu-id="95a71-434">Paramètre</span><span class="sxs-lookup"><span data-stu-id="95a71-434">Setting</span></span> | <span data-ttu-id="95a71-435">Description</span><span class="sxs-lookup"><span data-stu-id="95a71-435">Description</span></span> | <span data-ttu-id="95a71-436">Exemple</span><span class="sxs-lookup"><span data-stu-id="95a71-436">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="95a71-437">**Nom**</span><span class="sxs-lookup"><span data-stu-id="95a71-437">**Name**</span></span> | <span data-ttu-id="95a71-438">Texte</span><span class="sxs-lookup"><span data-stu-id="95a71-438">Text</span></span> | <span data-ttu-id="95a71-439">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="95a71-439">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="95a71-440">**Frontend IP address (Adresse IP frontale)**</span><span class="sxs-lookup"><span data-stu-id="95a71-440">**Frontend IP address**</span></span> | <span data-ttu-id="95a71-441">Choisissez une adresse.</span><span class="sxs-lookup"><span data-stu-id="95a71-441">Choose an address</span></span> |<span data-ttu-id="95a71-442">Utiliser une adresse hello que vous avez créé lorsque vous avez créé l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-442">Use hello address that you created when you created hello load balancer.</span></span> |
   | <span data-ttu-id="95a71-443">**Protocole**</span><span class="sxs-lookup"><span data-stu-id="95a71-443">**Protocol**</span></span> | <span data-ttu-id="95a71-444">Choisissez TCP.</span><span class="sxs-lookup"><span data-stu-id="95a71-444">Choose TCP</span></span> |<span data-ttu-id="95a71-445">TCP</span><span class="sxs-lookup"><span data-stu-id="95a71-445">TCP</span></span> |
   | <span data-ttu-id="95a71-446">**Port**</span><span class="sxs-lookup"><span data-stu-id="95a71-446">**Port**</span></span> | <span data-ttu-id="95a71-447">Utiliser le port de hello pour l’instance de SQL Server hello</span><span class="sxs-lookup"><span data-stu-id="95a71-447">Use hello port for hello SQL Server instance</span></span> | <span data-ttu-id="95a71-448">1433</span><span class="sxs-lookup"><span data-stu-id="95a71-448">1433</span></span> |
   | <span data-ttu-id="95a71-449">**Port principal**</span><span class="sxs-lookup"><span data-stu-id="95a71-449">**Backend Port**</span></span> | <span data-ttu-id="95a71-450">Ce champ est inutilisé lorsque l’option IP flottante est définie pour Retour au serveur direct.</span><span class="sxs-lookup"><span data-stu-id="95a71-450">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="95a71-451">1433</span><span class="sxs-lookup"><span data-stu-id="95a71-451">1433</span></span> |
   | <span data-ttu-id="95a71-452">**Sonde**</span><span class="sxs-lookup"><span data-stu-id="95a71-452">**Probe**</span></span> |<span data-ttu-id="95a71-453">nom Hello spécifié pour la sonde de hello</span><span class="sxs-lookup"><span data-stu-id="95a71-453">hello name you specified for hello probe</span></span> | <span data-ttu-id="95a71-454">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="95a71-454">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="95a71-455">**Persistance de session**</span><span class="sxs-lookup"><span data-stu-id="95a71-455">**Session Persistence**</span></span> | <span data-ttu-id="95a71-456">Liste déroulante</span><span class="sxs-lookup"><span data-stu-id="95a71-456">Drop down list</span></span> | <span data-ttu-id="95a71-457">**Aucun**</span><span class="sxs-lookup"><span data-stu-id="95a71-457">**None**</span></span> |
   | <span data-ttu-id="95a71-458">**Délai d’inactivité**</span><span class="sxs-lookup"><span data-stu-id="95a71-458">**Idle Timeout**</span></span> | <span data-ttu-id="95a71-459">Tookeep minutes d’ouvrir une connexion TCP</span><span class="sxs-lookup"><span data-stu-id="95a71-459">Minutes tookeep a TCP connection open</span></span> | <span data-ttu-id="95a71-460">4</span><span class="sxs-lookup"><span data-stu-id="95a71-460">4</span></span> |
   | <span data-ttu-id="95a71-461">**Adresse IP flottante (retour serveur direct)**</span><span class="sxs-lookup"><span data-stu-id="95a71-461">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="95a71-462">Activé</span><span class="sxs-lookup"><span data-stu-id="95a71-462">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="95a71-463">Le retour au serveur direct est configuré lors de la création.</span><span class="sxs-lookup"><span data-stu-id="95a71-463">Direct server return is set during creation.</span></span> <span data-ttu-id="95a71-464">Cette valeur n’est pas modifiable.</span><span class="sxs-lookup"><span data-stu-id="95a71-464">It cannot be changed.</span></span>

1. <span data-ttu-id="95a71-465">Cliquez sur **OK** tooset hello équilibrage de la charge des règles.</span><span class="sxs-lookup"><span data-stu-id="95a71-465">Click **OK** tooset hello load balancing rules.</span></span>

## <span data-ttu-id="95a71-466"><a name="configure-listener"></a>Configurer le port d’écoute hello</span><span class="sxs-lookup"><span data-stu-id="95a71-466"><a name="configure-listener"></a> Configure hello listener</span></span>

<span data-ttu-id="95a71-467">Hello suivant chose toodo est tooconfigure un écouteur de groupe de disponibilité sur un cluster de basculement hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-467">hello next thing toodo is tooconfigure an Availability Group listener on hello failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="95a71-468">Ce didacticiel montre comment la corriger toocreate un seul écouteur - avec une adresse IP ILB.</span><span class="sxs-lookup"><span data-stu-id="95a71-468">This tutorial shows how toocreate a single listener - with one ILB IP address.</span></span> <span data-ttu-id="95a71-469">un ou plusieurs écouteurs à l’aide d’une ou plusieurs adresses IP, reportez-vous à toocreate [écouteur de créer un groupe de disponibilité et équilibrage de charge | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="95a71-469">toocreate one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="95a71-470">Configurer le port d’écoute</span><span class="sxs-lookup"><span data-stu-id="95a71-470">Set listener port</span></span>

<span data-ttu-id="95a71-471">Dans SQL Server Management Studio, définissez le port d’écoute hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-471">In SQL Server Management Studio, set hello listener port.</span></span>

1. <span data-ttu-id="95a71-472">Lancez SQL Server Management Studio et connectez-vous toohello le réplica principal.</span><span class="sxs-lookup"><span data-stu-id="95a71-472">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="95a71-473">Accédez trop**haute disponibilité AlwaysOn** | **groupes de disponibilité** | **écouteurs de groupe de disponibilité**.</span><span class="sxs-lookup"><span data-stu-id="95a71-473">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="95a71-474">Vous devez maintenant voir le nom de l’écouteur hello que vous avez créé dans le Gestionnaire de Cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="95a71-474">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="95a71-475">Cliquez sur le nom d’écouteur hello et cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="95a71-475">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="95a71-476">Bonjour **Port** , spécifiez le numéro de port hello pour l’écouteur de groupe de disponibilité hello à l’aide de hello $EndpointPort utilisé précédemment (1433 était la valeur par défaut hello), puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="95a71-476">In hello **Port** box, specify hello port number for hello Availability Group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

<span data-ttu-id="95a71-477">Vous avez maintenant un groupe de disponibilité SQL Server dans des machines virtuelles Azure exécutées en mode Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="95a71-477">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-toolistener"></a><span data-ttu-id="95a71-478">Toolistener de connexion de test</span><span class="sxs-lookup"><span data-stu-id="95a71-478">Test connection toolistener</span></span>

<span data-ttu-id="95a71-479">connexion de hello tootest :</span><span class="sxs-lookup"><span data-stu-id="95a71-479">tootest hello connection:</span></span>

1. <span data-ttu-id="95a71-480">RDP tooa SQL Server qui se trouve dans hello virtuel même réseau, mais ne pas les réplicas hello propre.</span><span class="sxs-lookup"><span data-stu-id="95a71-480">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="95a71-481">Vous pouvez utiliser hello autre serveur SQL Server dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-481">You can use hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="95a71-482">Utilisez **sqlcmd** connexion de hello tootest utilitaire.</span><span class="sxs-lookup"><span data-stu-id="95a71-482">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="95a71-483">Par exemple, hello script suivant établit une **sqlcmd** réplica principal de connexion toohello via écouteur hello avec l’authentification Windows :</span><span class="sxs-lookup"><span data-stu-id="95a71-483">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>

    ```
    sqlcmd -S <listenerName> -E
    ```

    <span data-ttu-id="95a71-484">Si l’écouteur de hello utilise un port autre que hello par défaut du port (1433), spécifiez le port de hello dans la chaîne de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="95a71-484">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="95a71-485">Par exemple, hello commande sqlcmd suivante établit une connexion écouteur tooa sur le port 1435 :</span><span class="sxs-lookup"><span data-stu-id="95a71-485">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="95a71-486">Hello connexion de SQLCMD connecte automatiquement à instance toowhichever de SQL Server héberge hello le réplica principal.</span><span class="sxs-lookup"><span data-stu-id="95a71-486">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="95a71-487">Assurez-vous que port hello que vous spécifiez est ouvert sur le pare-feu hello des deux serveurs SQL.</span><span class="sxs-lookup"><span data-stu-id="95a71-487">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="95a71-488">Les deux serveurs requièrent une règle de trafic entrant pour hello le port TCP que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="95a71-488">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="95a71-489">Pour plus d’informations, consultez [Ajouter ou modifier une règle de pare-feu](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="95a71-489">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a><span data-ttu-id="95a71-490">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="95a71-490">Next steps</span></span>

- <span data-ttu-id="95a71-491">[Ajouter un équilibrage de charge de tooa d’adresse IP pour un deuxième groupe de disponibilité](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span><span class="sxs-lookup"><span data-stu-id="95a71-491">[Add an IP address tooa load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>
