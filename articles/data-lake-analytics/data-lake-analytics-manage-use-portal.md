---
title: "Gérer Azure Data Lake Analytics à l’aide du portail Azure | Microsoft Docs"
description: "Apprenez à gérer des comptes Data Lake Analytics, des sources de données, des utilisateurs et des travaux."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: e49d1a0e0ccc6567d0a6841817667717ff5dba76
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-the-azure-portal"></a><span data-ttu-id="13cfd-103">Gérer Azure Data Lake Analytics à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="13cfd-103">Manage Azure Data Lake Analytics by using the Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="13cfd-104">Apprenez à gérer des comptes Azure Data Lake Analytics, des sources de données de compte, des utilisateurs et des travaux à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="13cfd-104">Learn how to manage Azure Data Lake Analytics accounts, account data sources, users, and jobs by using the Azure portal.</span></span> <span data-ttu-id="13cfd-105">Pour afficher les rubriques de gestion sur l’utilisation d’autres outils, cliquez sur un onglet en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="13cfd-105">To see management topics about using other tools, click a tab at the top of the page.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a><span data-ttu-id="13cfd-106">Gérer les comptes Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="13cfd-106">Manage Data Lake Analytics accounts</span></span>

### <a name="create-an-account"></a><span data-ttu-id="13cfd-107">Créer un compte</span><span class="sxs-lookup"><span data-stu-id="13cfd-107">Create an account</span></span>

1. <span data-ttu-id="13cfd-108">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="13cfd-108">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="13cfd-109">Cliquez sur **Nouveau** > **Intelligence + analyse** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-109">Click **New** > **Intelligence + analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="13cfd-110">Sélectionnez des valeurs pour les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="13cfd-110">Select values for the following items:</span></span> 
   1. <span data-ttu-id="13cfd-111">**Nom** : nom du compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-111">**Name**: The name of the Data Lake Analytics account.</span></span>
   2. <span data-ttu-id="13cfd-112">**Abonnement** : abonnement Azure utilisé pour le compte.</span><span class="sxs-lookup"><span data-stu-id="13cfd-112">**Subscription**: The Azure subscription used for the account.</span></span>
   3. <span data-ttu-id="13cfd-113">**Groupe de ressources** : groupe de ressources Azure dans lequel créer le compte.</span><span class="sxs-lookup"><span data-stu-id="13cfd-113">**Resource Group**: The Azure resource group in which to create the account.</span></span> 
   4. <span data-ttu-id="13cfd-114">**Emplacement** : centre de données Azure pour le compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-114">**Location**: The Azure datacenter for the Data Lake Analytics account.</span></span> 
   5. <span data-ttu-id="13cfd-115">**Data Lake Store** : Store par défaut à utiliser pour le compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-115">**Data Lake Store**: The default store to be used for the Data Lake Analytics account.</span></span> <span data-ttu-id="13cfd-116">Le compte Azure Data Lake Store et le compte Data Lake Analytics doivent se trouver dans le même emplacement.</span><span class="sxs-lookup"><span data-stu-id="13cfd-116">The Azure Data Lake Store account and the Data Lake Analytics account must be in the same location.</span></span>
4. <span data-ttu-id="13cfd-117">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-117">Click **Create**.</span></span> 

### <a name="delete-a-data-lake-analytics-account"></a><span data-ttu-id="13cfd-118">Supprimer un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="13cfd-118">Delete a Data Lake Analytics account</span></span>

<span data-ttu-id="13cfd-119">Avant de supprimer un compte Data Lake Analytics, vous devez supprimer le compte Data Lake Store dépendant.</span><span class="sxs-lookup"><span data-stu-id="13cfd-119">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span></span>

1. <span data-ttu-id="13cfd-120">Dans le portail Azure, accédez à votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-120">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="13cfd-121">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-121">Click **Delete**.</span></span>
3. <span data-ttu-id="13cfd-122">Entez le nom du compte.</span><span class="sxs-lookup"><span data-stu-id="13cfd-122">Type the account name.</span></span>
4. <span data-ttu-id="13cfd-123">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-123">Click **Delete**.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a><span data-ttu-id="13cfd-124">Gérer les sources de données</span><span class="sxs-lookup"><span data-stu-id="13cfd-124">Manage data sources</span></span>

<span data-ttu-id="13cfd-125">Data Lake Analytics prend en charge les sources de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="13cfd-125">Data Lake Analytics supports the following data sources:</span></span>

* <span data-ttu-id="13cfd-126">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="13cfd-126">Data Lake Store</span></span>
* <span data-ttu-id="13cfd-127">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="13cfd-127">Azure Storage</span></span>

<span data-ttu-id="13cfd-128">Vous pouvez utiliser l’Explorateur de données pour parcourir les sources de données et effectuer des opérations de gestion des fichiers de base.</span><span class="sxs-lookup"><span data-stu-id="13cfd-128">You can use Data Explorer to browse data sources and perform basic file management operations.</span></span> 

### <a name="add-a-data-source"></a><span data-ttu-id="13cfd-129">Ajouter une source de données</span><span class="sxs-lookup"><span data-stu-id="13cfd-129">Add a data source</span></span>

1. <span data-ttu-id="13cfd-130">Dans le portail Azure, accédez à votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-130">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="13cfd-131">Cliquez sur **Sources de données**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-131">Click **Data Sources**.</span></span>
3. <span data-ttu-id="13cfd-132">Cliquez sur **Ajouter une source de données**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-132">Click **Add Data Source**.</span></span>
    
   * <span data-ttu-id="13cfd-133">Pour ajouter un compte Data Lake Store, vous avez besoin du nom du compte et de l’accès au compte pour pouvoir l’interroger.</span><span class="sxs-lookup"><span data-stu-id="13cfd-133">To add a Data Lake Store account, you need the account name and access to the account to be able to query it.</span></span>
   * <span data-ttu-id="13cfd-134">Pour ajouter du stockage Blob Azure, vous avez besoin du compte de stockage et de la clé du compte.</span><span class="sxs-lookup"><span data-stu-id="13cfd-134">To add Azure Blob storage, you need the storage account and the account key.</span></span> <span data-ttu-id="13cfd-135">Pour les trouver, accédez au compte de stockage dans le portail.</span><span class="sxs-lookup"><span data-stu-id="13cfd-135">To find them, go to the storage account in the portal.</span></span>

## <a name="set-up-firewall-rules"></a><span data-ttu-id="13cfd-136">Configurer des règles de pare-feu</span><span class="sxs-lookup"><span data-stu-id="13cfd-136">Set up firewall rules</span></span>

<span data-ttu-id="13cfd-137">Vous pouvez utiliser Data Lake Analytics pour mieux verrouiller l’accès à votre compte Data Lake Analytics au niveau du réseau.</span><span class="sxs-lookup"><span data-stu-id="13cfd-137">You can use Data Lake Analytics to further lock down access to your Data Lake Analytics account at the network level.</span></span> <span data-ttu-id="13cfd-138">Vous pouvez activer un pare-feu, spécifier une adresse IP ou définir une plage d’adresses IP pour vos clients approuvés.</span><span class="sxs-lookup"><span data-stu-id="13cfd-138">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="13cfd-139">Une fois ces mesures activées, seuls les clients possédant des adresses IP dans la plage définie peuvent se connecter au Store.</span><span class="sxs-lookup"><span data-stu-id="13cfd-139">After you enable these measures, only clients that have the IP addresses within the defined range can connect to the store.</span></span>

<span data-ttu-id="13cfd-140">Si d’autres services Azure, comme Azure Data Factory ou des machines virtuelles, se connectent au compte Data Lake Analytics, vérifiez que l’option **Autoriser les services Azure** est **activée**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-140">If other Azure services, like Azure Data Factory or VMs, connect to the Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span></span> 

### <a name="set-up-a-firewall-rule"></a><span data-ttu-id="13cfd-141">Configurer une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="13cfd-141">Set up a firewall rule</span></span>

1. <span data-ttu-id="13cfd-142">Dans le portail Azure, accédez à votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-142">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="13cfd-143">Dans le menu de gauche, cliquez sur **Pare-feu**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-143">On the menu on the left, click **Firewall**.</span></span>

## <a name="add-a-new-user"></a><span data-ttu-id="13cfd-144">Ajouter un nouvel utilisateur</span><span class="sxs-lookup"><span data-stu-id="13cfd-144">Add a new user</span></span>

<span data-ttu-id="13cfd-145">Vous pouvez utiliser **l’Assistant Ajout d’un utilisateur** pour configurer facilement de nouveaux utilisateurs Data Lake.</span><span class="sxs-lookup"><span data-stu-id="13cfd-145">You can use the **Add User Wizard** to easily provision new Data Lake users.</span></span>

1. <span data-ttu-id="13cfd-146">Dans le portail Azure, accédez à votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-146">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="13cfd-147">Sur la gauche, sous **Prise en main**, cliquez sur **Assistant Ajout d’un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-147">On the left, under **Getting Started**, click **Add User Wizard**.</span></span>
3. <span data-ttu-id="13cfd-148">Sélectionnez un utilisateur, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-148">Select a user, and then click **Select**.</span></span>
4. <span data-ttu-id="13cfd-149">Sélectionnez un rôle, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-149">Select a role, and then click **Select**.</span></span> <span data-ttu-id="13cfd-150">Pour configurer un nouveau développeur qui utilisera Azure Data Lake, sélectionnez le rôle **Développeur Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-150">To set up a new developer to use Azure Data Lake, select the **Data Lake Analytics Developer** role.</span></span>
5. <span data-ttu-id="13cfd-151">Sélectionnez les listes de contrôle d’accès (ACL) pour les bases de données U-SQL.</span><span class="sxs-lookup"><span data-stu-id="13cfd-151">Select the access control lists (ACLs) for the U-SQL databases.</span></span> <span data-ttu-id="13cfd-152">Lorsque vous êtes satisfait de vos choix, cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-152">When you're satisfied with your choices, click **Select**.</span></span>
6. <span data-ttu-id="13cfd-153">Sélectionnez les listes de contrôle d’accès pour les fichiers.</span><span class="sxs-lookup"><span data-stu-id="13cfd-153">Select the ACLs for files.</span></span> <span data-ttu-id="13cfd-154">Pour le Store par défaut, ne modifiez pas les listes de contrôle d’accès pour le dossier racine « / » et pour le dossier /system.</span><span class="sxs-lookup"><span data-stu-id="13cfd-154">For the default store, don't change the ACLs for the root folder "/" and for the /system folder.</span></span> <span data-ttu-id="13cfd-155">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-155">Click **Select**.</span></span>
7. <span data-ttu-id="13cfd-156">Passez en revue toutes vos sélections, puis cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-156">Review all your selected changes, and then click **Run**.</span></span>
8. <span data-ttu-id="13cfd-157">Une fois l’Assistant exécuté, cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-157">When the wizard is finished, click **Done**.</span></span>

## <a name="manage-role-based-access-control"></a><span data-ttu-id="13cfd-158">Gérer le contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="13cfd-158">Manage Role-Based Access Control</span></span>

<span data-ttu-id="13cfd-159">Comme d’autres services Azure, vous pouvez utiliser le contrôle d’accès en fonction du rôle (RBAC) pour contrôler la façon dont les utilisateurs interagissent avec le service.</span><span class="sxs-lookup"><span data-stu-id="13cfd-159">Like other Azure services, you can use Role-Based Access Control (RBAC) to control how users interact with the service.</span></span>

<span data-ttu-id="13cfd-160">Les rôles RBAC standard ont les fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="13cfd-160">The standard RBAC roles have the following capabilities:</span></span>
* <span data-ttu-id="13cfd-161">**Propriétaire** : peut envoyer des travaux, surveiller des travaux, annuler des travaux de n’importe quel utilisateur et configurer le compte.</span><span class="sxs-lookup"><span data-stu-id="13cfd-161">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure the account.</span></span>
* <span data-ttu-id="13cfd-162">**Contributeur** : peut envoyer des travaux, surveiller des travaux, annuler des travaux de n’importe quel utilisateur et configurer le compte.</span><span class="sxs-lookup"><span data-stu-id="13cfd-162">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure the account.</span></span>
* <span data-ttu-id="13cfd-163">**Lecteur** : peut surveiller des travaux.</span><span class="sxs-lookup"><span data-stu-id="13cfd-163">**Reader**: Can monitor jobs.</span></span>

<span data-ttu-id="13cfd-164">Utilisez le rôle Développeur Data Lake Analytics pour permettre aux développeurs U-SQL d’utiliser le service Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-164">Use the Data Lake Analytics Developer role to enable U-SQL developers to use the Data Lake Analytics service.</span></span> <span data-ttu-id="13cfd-165">Vous pouvez utiliser le rôle Développeur Data Lake Analytics pour les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="13cfd-165">You can use the Data Lake Analytics Developer role to:</span></span>
* <span data-ttu-id="13cfd-166">Envoyer des travaux.</span><span class="sxs-lookup"><span data-stu-id="13cfd-166">Submit jobs.</span></span>
* <span data-ttu-id="13cfd-167">Surveiller l’état du travail et la progression des travaux soumis par les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="13cfd-167">Monitor job status and the progress of jobs submitted by any user.</span></span>
* <span data-ttu-id="13cfd-168">Afficher les scripts U-SQL à partir des travaux soumis par les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="13cfd-168">See the U-SQL scripts from jobs submitted by any user.</span></span>
* <span data-ttu-id="13cfd-169">Annuler uniquement vos propres travaux.</span><span class="sxs-lookup"><span data-stu-id="13cfd-169">Cancel only your own jobs.</span></span>

### <a name="add-users-or-security-groups-to-a-data-lake-analytics-account"></a><span data-ttu-id="13cfd-170">Ajouter des utilisateurs ou des groupes de sécurité à un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="13cfd-170">Add users or security groups to a Data Lake Analytics account</span></span>

1. <span data-ttu-id="13cfd-171">Dans le portail Azure, accédez à votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-171">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="13cfd-172">Cliquez sur **Contrôle d’accès (IAM)** > **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-172">Click **Access control (IAM)** > **Add**.</span></span>
3. <span data-ttu-id="13cfd-173">Sélectionnez un rôle</span><span class="sxs-lookup"><span data-stu-id="13cfd-173">Select a role.</span></span>
4. <span data-ttu-id="13cfd-174">Ajoutez un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="13cfd-174">Add a user.</span></span>
5. <span data-ttu-id="13cfd-175">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-175">Click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="13cfd-176">Si un utilisateur ou un groupe de sécurité doit envoyer des travaux, ils doivent également être autorisés sur le compte du Store.</span><span class="sxs-lookup"><span data-stu-id="13cfd-176">If a user or a security group needs to submit jobs, they also need permission on the store account.</span></span> <span data-ttu-id="13cfd-177">Pour plus d’informations, consultez [Sécuriser les données stockées dans Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span><span class="sxs-lookup"><span data-stu-id="13cfd-177">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span></span>
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a><span data-ttu-id="13cfd-178">Gestion des travaux</span><span class="sxs-lookup"><span data-stu-id="13cfd-178">Manage jobs</span></span>

### <a name="submit-a-job"></a><span data-ttu-id="13cfd-179">Soumettre un travail</span><span class="sxs-lookup"><span data-stu-id="13cfd-179">Submit a job</span></span>

1. <span data-ttu-id="13cfd-180">Dans le portail Azure, accédez à votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-180">In the Azure portal, go to your Data Lake Analytics account.</span></span>

2. <span data-ttu-id="13cfd-181">Cliquez sur **Nouveau travail**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-181">Click **New Job**.</span></span> <span data-ttu-id="13cfd-182">Pour chaque travail, configurez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="13cfd-182">For each job,  configure:</span></span>

    1. <span data-ttu-id="13cfd-183">**Nom du travail** : nom du travail.</span><span class="sxs-lookup"><span data-stu-id="13cfd-183">**Job Name**: The name of the job.</span></span>
    2. <span data-ttu-id="13cfd-184">**Priorité** : les nombres inférieurs ont une priorité supérieure.</span><span class="sxs-lookup"><span data-stu-id="13cfd-184">**Priority**: Lower numbers have higher priority.</span></span> <span data-ttu-id="13cfd-185">Si deux travaux sont en file d’attente, celui dont la valeur de la priorité est la plus faible s’exécute en premier.</span><span class="sxs-lookup"><span data-stu-id="13cfd-185">If two jobs are queued, the one with lower priority value runs first.</span></span>
    3. <span data-ttu-id="13cfd-186">**Parallélisme** : nombre maximal de processus de calcul à réserver pour ce travail.</span><span class="sxs-lookup"><span data-stu-id="13cfd-186">**Parallelism**: The maximum number of compute processes to reserve for this job.</span></span>

3. <span data-ttu-id="13cfd-187">Cliquez sur **Envoyer le travail**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-187">Click **Submit Job**.</span></span>

### <a name="monitor-jobs"></a><span data-ttu-id="13cfd-188">Surveiller des travaux</span><span class="sxs-lookup"><span data-stu-id="13cfd-188">Monitor jobs</span></span>

1. <span data-ttu-id="13cfd-189">Dans le portail Azure, accédez à votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-189">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="13cfd-190">Cliquez sur **Afficher tous les travaux**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-190">Click **View All Jobs**.</span></span> <span data-ttu-id="13cfd-191">Une liste de tous les travaux actifs et récemment terminés dans le compte s’affiche.</span><span class="sxs-lookup"><span data-stu-id="13cfd-191">A list of all the active and recently finished jobs in the account is shown.</span></span>
3. <span data-ttu-id="13cfd-192">Le cas échéant, cliquez sur **Filtrer** pour rechercher les travaux par **Intervalle de temps**, **Nom du travail** et **Auteur**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-192">Optionally, click **Filter** to help you find the jobs by **Time Range**, **Job Name**, and **Author** values.</span></span> 

### <a name="monitoring-pipeline-jobs"></a><span data-ttu-id="13cfd-193">Surveillance des tâches de pipeline</span><span class="sxs-lookup"><span data-stu-id="13cfd-193">Monitoring pipeline jobs</span></span>
<span data-ttu-id="13cfd-194">Les tâches qui font partie d’un pipeline fonctionnent ensemble, généralement séquentiellement, pour réaliser un scénario spécifique.</span><span class="sxs-lookup"><span data-stu-id="13cfd-194">Jobs that are part of a pipeline work together, usually sequentially, to accomplish a specific scenario.</span></span> <span data-ttu-id="13cfd-195">Par exemple, vous pouvez avoir un pipeline qui nettoie, extrait, transforme, regroupe l’utilisation des informations du client.</span><span class="sxs-lookup"><span data-stu-id="13cfd-195">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span></span> <span data-ttu-id="13cfd-196">Les tâches de pipeline sont identifiées à l’aide de la propriété « Pipeline » lorsque la tâche a été soumise.</span><span class="sxs-lookup"><span data-stu-id="13cfd-196">Pipeline jobs are identified using the "Pipeline" property when the job was submitted.</span></span> <span data-ttu-id="13cfd-197">Les tâches planifiées à l’aide du fichier de définition d’application V2 auront automatiquement cette propriété remplie.</span><span class="sxs-lookup"><span data-stu-id="13cfd-197">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span> 

<span data-ttu-id="13cfd-198">Pour afficher une liste des tâches U-SQL qui font partie de pipelines :</span><span class="sxs-lookup"><span data-stu-id="13cfd-198">To view a list of U-SQL jobs that are part of pipelines:</span></span> 

1. <span data-ttu-id="13cfd-199">Dans le portail Azure, accédez à vos comptes Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-199">In the Azure portal, go to your Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="13cfd-200">Cliquez sur **Informations sur les tâches**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-200">Click **Job Insights**.</span></span> <span data-ttu-id="13cfd-201">L’onglet « Toutes les tâches » s’affiche par défaut avec la liste des tâches en cours d’exécution, en file d’attente et terminées.</span><span class="sxs-lookup"><span data-stu-id="13cfd-201">The "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="13cfd-202">Cliquez sur l’onglet **Tâches de pipeline**. Une liste des tâches de pipeline s’affiche, ainsi que des statistiques agrégées pour chaque pipeline.</span><span class="sxs-lookup"><span data-stu-id="13cfd-202">Click the **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span></span>

### <a name="monitoring-recurring-jobs"></a><span data-ttu-id="13cfd-203">Surveillance des tâches récurrentes</span><span class="sxs-lookup"><span data-stu-id="13cfd-203">Monitoring recurring jobs</span></span>
<span data-ttu-id="13cfd-204">Une tâche récurrente a la même logique métier, mais utilise les données d’entrée différente chaque fois qu’elle est exécutée.</span><span class="sxs-lookup"><span data-stu-id="13cfd-204">A recurring job is one that has the same business logic but uses different input data every time it runs.</span></span> <span data-ttu-id="13cfd-205">Dans l’idéal, les tâches récurrentes doivent toujours réussir et ont une exécution relativement stable ; La surveillance de ces comportements permet de garantir que la tâche est intègre.</span><span class="sxs-lookup"><span data-stu-id="13cfd-205">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure the job is healthy.</span></span> <span data-ttu-id="13cfd-206">Les tâches récurrentes sont identifiées à l’aide de la propriété « Récurrence ».</span><span class="sxs-lookup"><span data-stu-id="13cfd-206">Recurring jobs are identified using the "Recurrence" property.</span></span> <span data-ttu-id="13cfd-207">Les tâches planifiées à l’aide du fichier de définition d’application V2 auront automatiquement cette propriété remplie.</span><span class="sxs-lookup"><span data-stu-id="13cfd-207">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span>

<span data-ttu-id="13cfd-208">Pour afficher une liste des tâches U-SQL récurrentes :</span><span class="sxs-lookup"><span data-stu-id="13cfd-208">To view a list of U-SQL jobs that are recurring:</span></span> 

1. <span data-ttu-id="13cfd-209">Dans le portail Azure, accédez à vos comptes Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-209">In the Azure portal, go to your Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="13cfd-210">Cliquez sur **Informations sur les tâches**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-210">Click **Job Insights**.</span></span> <span data-ttu-id="13cfd-211">L’onglet « Toutes les tâches » s’affiche par défaut avec la liste des tâches en cours d’exécution, en file d’attente et terminées.</span><span class="sxs-lookup"><span data-stu-id="13cfd-211">The "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="13cfd-212">Cliquez sur l’onglet **Tâches récurrentes**. Une liste des tâches récurrentes s’affiche, ainsi que des statistiques agrégées pour chaque tâche récurrente.</span><span class="sxs-lookup"><span data-stu-id="13cfd-212">Click the **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span></span>

## <a name="manage-policies"></a><span data-ttu-id="13cfd-213">Gérer les stratégies</span><span class="sxs-lookup"><span data-stu-id="13cfd-213">Manage policies</span></span>

### <a name="account-level-policies"></a><span data-ttu-id="13cfd-214">Stratégies au niveau du compte</span><span class="sxs-lookup"><span data-stu-id="13cfd-214">Account-level policies</span></span>

<span data-ttu-id="13cfd-215">Ces stratégies s’appliquent à tous les travaux dans un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-215">These policies apply to all jobs in a Data Lake Analytics account.</span></span>

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a><span data-ttu-id="13cfd-216">Nombre maximal d’unités Analytics dans un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="13cfd-216">Maximum number of AUs in a Data Lake Analytics account</span></span>
<span data-ttu-id="13cfd-217">Une stratégie contrôle le nombre total d’unités Analytics que votre compte Data Lake Analytics peut utiliser.</span><span class="sxs-lookup"><span data-stu-id="13cfd-217">A policy controls the total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span></span> <span data-ttu-id="13cfd-218">Par défaut, la valeur est définie sur 250.</span><span class="sxs-lookup"><span data-stu-id="13cfd-218">By default, the value is set to 250.</span></span> <span data-ttu-id="13cfd-219">Par exemple, si cette valeur est définie sur 250 unités Analytics, vous pouvez avoir un travail qui s’exécute avec 250 unités Analytics assignées ou 10 travaux exécutant chacun 25 unités Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-219">For example, if this value is set to 250 AUs, you can have one job running with 250 AUs assigned to it, or 10 jobs running with 25 AUs each.</span></span> <span data-ttu-id="13cfd-220">Les travaux supplémentaires qui sont envoyés sont placés en file d’attente jusqu'à ce que les travaux en cours d’exécution soient terminés.</span><span class="sxs-lookup"><span data-stu-id="13cfd-220">Additional jobs that are submitted are queued until the running jobs are finished.</span></span> <span data-ttu-id="13cfd-221">Lorsque les travaux en cours d’exécution sont terminés, des unités Analytics sont libérées pour l’exécution des travaux dans la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="13cfd-221">When running jobs are finished, AUs are freed up for the queued jobs to run.</span></span>

<span data-ttu-id="13cfd-222">Pour modifier le nombre d’unités Analytics pour votre compte Data Lake Analytics :</span><span class="sxs-lookup"><span data-stu-id="13cfd-222">To change the number of AUs for your Data Lake Analytics account:</span></span>

1. <span data-ttu-id="13cfd-223">Dans le portail Azure, accédez à votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-223">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="13cfd-224">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-224">Click **Properties**.</span></span>
3. <span data-ttu-id="13cfd-225">Sous **Nombre maximale d’unités Analytics**, déplacez le curseur pour sélectionner une valeur ou entrez la valeur dans la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="13cfd-225">Under **Maximum AUs**, move the slider to select a value, or enter the value in the text box.</span></span> 
4. <span data-ttu-id="13cfd-226">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-226">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="13cfd-227">Si vous avez besoin de plus d’unités Analytics que la valeur par défaut (250), cliquez sur **Aide + support** dans le portail pour envoyer une demande de support.</span><span class="sxs-lookup"><span data-stu-id="13cfd-227">If you need more than the default (250) AUs, in the portal, click **Help+Support** to submit a support request.</span></span> <span data-ttu-id="13cfd-228">Il est possible d’augmenter le nombre d’unités Analytics disponibles dans votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-228">The number of AUs available in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a><span data-ttu-id="13cfd-229">Nombre maximal de travaux pouvant s’exécuter simultanément</span><span class="sxs-lookup"><span data-stu-id="13cfd-229">Maximum number of jobs that can run simultaneously</span></span>
<span data-ttu-id="13cfd-230">Une stratégie contrôle le nombre de travaux qui peuvent s’exécuter simultanément.</span><span class="sxs-lookup"><span data-stu-id="13cfd-230">A policy controls how many jobs can run at the same time.</span></span> <span data-ttu-id="13cfd-231">Par défaut, cette valeur est définie sur 20.</span><span class="sxs-lookup"><span data-stu-id="13cfd-231">By default, this value is set to 20.</span></span> <span data-ttu-id="13cfd-232">Si des unités Analytics sont disponibles dans votre Data Lake Analytics, de nouveaux travaux sont planifiés pour s’exécuter immédiatement jusqu’à ce que le nombre total de travaux en cours d’exécution atteigne la valeur de cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="13cfd-232">If your Data Lake Analytics has AUs available, new jobs are scheduled to run immediately until the total number of running jobs reaches the value of this policy.</span></span> <span data-ttu-id="13cfd-233">Lorsque vous atteignez le nombre maximal de travaux pouvant s’exécuter simultanément, les travaux suivants sont placés en file d’attente par ordre de priorité jusqu’à ce qu’un ou plusieurs des travaux en cours d’exécution se termine (selon la disponibilité des unités Analytics).</span><span class="sxs-lookup"><span data-stu-id="13cfd-233">When you reach the maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span></span>

<span data-ttu-id="13cfd-234">Pour modifier le nombre maximal de travaux pouvant s’exécuter simultanément :</span><span class="sxs-lookup"><span data-stu-id="13cfd-234">To change the number of jobs that can run simultaneously:</span></span>

1. <span data-ttu-id="13cfd-235">Dans le portail Azure, accédez à votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-235">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="13cfd-236">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-236">Click **Properties**.</span></span>
3. <span data-ttu-id="13cfd-237">Sous **Nombre maximal de travaux en cours d’exécution**, déplacez le curseur pour sélectionner une valeur ou entrez la valeur dans la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="13cfd-237">Under **Maximum Number of Running Jobs**, move the slider to select a value, or enter the value in the text box.</span></span> 
4. <span data-ttu-id="13cfd-238">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-238">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="13cfd-239">Si vous avez besoin d’exécuter plus de travaux que la valeur par défaut (20), cliquez sur **Aide + support** dans le portail pour envoyer une demande de support.</span><span class="sxs-lookup"><span data-stu-id="13cfd-239">If you need to run more than the default (20) number of jobs, in the portal, click **Help+Support** to submit a support request.</span></span> <span data-ttu-id="13cfd-240">Il est possible d’augmenter le nombre de travaux pouvant s’exécuter simultanément dans votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-240">The number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="how-long-to-keep-job-metadata-and-resources"></a><span data-ttu-id="13cfd-241">Durée de conservation des métadonnées et des ressources d’un travail</span><span class="sxs-lookup"><span data-stu-id="13cfd-241">How long to keep job metadata and resources</span></span> 
<span data-ttu-id="13cfd-242">Lorsque vos utilisateurs exécutent des travaux U-SQL, le service Data Lake Analytics conserve tous les fichiers associés.</span><span class="sxs-lookup"><span data-stu-id="13cfd-242">When your users run U-SQL jobs, the Data Lake Analytics service retains all related files.</span></span> <span data-ttu-id="13cfd-243">Les fichiers associés incluent le script U-SQL, les fichiers DLL référencés dans le script U-SQL, les ressources compilées et les statistiques.</span><span class="sxs-lookup"><span data-stu-id="13cfd-243">Related files include the U-SQL script, the DLL files referenced in the U-SQL script, compiled resources, and statistics.</span></span> <span data-ttu-id="13cfd-244">Les fichiers se trouvent dans le dossier /system/ du compte de stockage Azure Data Lake par défaut.</span><span class="sxs-lookup"><span data-stu-id="13cfd-244">The files are in the /system/ folder of the default Azure Data Lake Storage account.</span></span> <span data-ttu-id="13cfd-245">Cette stratégie contrôle la durée pendant laquelle ces ressources sont stockées avant d’être automatiquement supprimées (la valeur par défaut est de 30 jours).</span><span class="sxs-lookup"><span data-stu-id="13cfd-245">This policy controls how long these resources are stored before they are automatically deleted (the default is 30 days).</span></span> <span data-ttu-id="13cfd-246">Vous pouvez utiliser ces fichiers pour le débogage et pour régler les performances des travaux que vous exécuterez à nouveau à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="13cfd-246">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in the future.</span></span>

<span data-ttu-id="13cfd-247">Pour modifier la durée de conservation des métadonnées et des ressources d’un travail :</span><span class="sxs-lookup"><span data-stu-id="13cfd-247">To change how long to keep job metadata and resources:</span></span>

1. <span data-ttu-id="13cfd-248">Dans le portail Azure, accédez à votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-248">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="13cfd-249">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-249">Click **Properties**.</span></span>
3. <span data-ttu-id="13cfd-250">Sous **Jours de rétention des requêtes de tâche**, déplacez le curseur pour sélectionner une valeur ou entrez la valeur dans la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="13cfd-250">Under **Days to Retain Job Queries**, move the slider to select a value, or enter the value in the text box.</span></span>  
4. <span data-ttu-id="13cfd-251">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-251">Click **Save**.</span></span>

### <a name="job-level-policies"></a><span data-ttu-id="13cfd-252">Stratégies au niveau du travail</span><span class="sxs-lookup"><span data-stu-id="13cfd-252">Job-level policies</span></span>
<span data-ttu-id="13cfd-253">Avec les stratégies au niveau du travail, vous pouvez contrôler les unités Analytics maximales et la priorité maximale que les utilisateurs individuels (ou les membres de groupes de sécurité spécifiques) peuvent définir sur les travaux qu’ils soumettent.</span><span class="sxs-lookup"><span data-stu-id="13cfd-253">With job-level policies, you can control the maximum AUs and the maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span></span> <span data-ttu-id="13cfd-254">Cela vous permet de contrôler les coûts générés par les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="13cfd-254">This lets you control the costs incurred by users.</span></span> <span data-ttu-id="13cfd-255">Cela vous permet également de contrôler l’effet que les travaux planifiés peuvent avoir sur des travaux de production à priorité élevée qui s’exécutent dans le même compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-255">It also lets you control the effect that scheduled jobs might have on high-priority production jobs that are running in the same Data Lake Analytics account.</span></span>

<span data-ttu-id="13cfd-256">Data Lake Analytics inclut deux stratégies que vous pouvez définir au niveau du travail :</span><span class="sxs-lookup"><span data-stu-id="13cfd-256">Data Lake Analytics has two policies that you can set at the job level:</span></span>

* <span data-ttu-id="13cfd-257">**Limite d’unités Analytics par travail** : les utilisateurs peuvent uniquement soumettre des travaux dont le nombre maximal d’unités Analytics est inférieur ou égal à cette valeur.</span><span class="sxs-lookup"><span data-stu-id="13cfd-257">**AU limit per job**: Users can only submit jobs that have up to this number of AUs.</span></span> <span data-ttu-id="13cfd-258">Par défaut, cette limite est identique à la limite maximale d’unités Analytics du compte.</span><span class="sxs-lookup"><span data-stu-id="13cfd-258">By default, this limit is the same as the maximum AU limit for the account.</span></span>
* <span data-ttu-id="13cfd-259">**Priorité** : les utilisateurs peuvent uniquement soumettre les travaux dont la priorité est inférieure ou égale à cette valeur.</span><span class="sxs-lookup"><span data-stu-id="13cfd-259">**Priority**: Users can only submit jobs that have a priority lower than or equal to this value.</span></span> <span data-ttu-id="13cfd-260">Notez qu’un nombre plus élevé signifie une priorité plus faible.</span><span class="sxs-lookup"><span data-stu-id="13cfd-260">Note that a higher number means a lower priority.</span></span> <span data-ttu-id="13cfd-261">Par défaut, elle est définie sur 1, qui est la priorité la plus élevée.</span><span class="sxs-lookup"><span data-stu-id="13cfd-261">By default, this is set to 1, which is the highest possible priority.</span></span>

<span data-ttu-id="13cfd-262">Chaque compte contient une stratégie par défaut.</span><span class="sxs-lookup"><span data-stu-id="13cfd-262">There is a default policy set on every account.</span></span> <span data-ttu-id="13cfd-263">La stratégie par défaut s’applique à tous les utilisateurs du compte.</span><span class="sxs-lookup"><span data-stu-id="13cfd-263">The default policy applies to all users of the account.</span></span> <span data-ttu-id="13cfd-264">Vous pouvez définir des stratégies supplémentaires pour des utilisateurs et des groupes spécifiques.</span><span class="sxs-lookup"><span data-stu-id="13cfd-264">You can set additional policies for specific users and groups.</span></span> 

> [!NOTE]
> <span data-ttu-id="13cfd-265">Les stratégies au niveau du compte et les stratégies au niveau du travail s’appliquent simultanément.</span><span class="sxs-lookup"><span data-stu-id="13cfd-265">Account-level policies and job-level policies apply simultaneously.</span></span>
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a><span data-ttu-id="13cfd-266">Ajouter une stratégie pour un utilisateur ou un groupe spécifique</span><span class="sxs-lookup"><span data-stu-id="13cfd-266">Add a policy for a specific user or group</span></span>

1. <span data-ttu-id="13cfd-267">Dans le portail Azure, accédez à votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-267">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="13cfd-268">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-268">Click **Properties**.</span></span>
3. <span data-ttu-id="13cfd-269">Sous **Limites d’envoi de tâches**, cliquez sur le bouton **Ajouter une stratégie**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-269">Under **Job Submission Limits**, click the **Add Policy** button.</span></span> <span data-ttu-id="13cfd-270">Puis, sélectionnez ou saisissez les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="13cfd-270">Then, select or enter the following settings:</span></span>
    1. <span data-ttu-id="13cfd-271">**Nom de la stratégie de calcul** : entrez un nom de stratégie, pour vous rappeler de l’objectif de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="13cfd-271">**Compute Policy Name**: Enter a policy name, to remind you of the purpose of the policy.</span></span>
    2. <span data-ttu-id="13cfd-272">**Sélectionner un utilisateur ou un groupe** : sélectionnez l’utilisateur ou le groupe auquel la stratégie s’applique.</span><span class="sxs-lookup"><span data-stu-id="13cfd-272">**Select User or Group**: Select the user or group this policy applies to.</span></span>
    3. <span data-ttu-id="13cfd-273">**Définir la limite d’unités Analytics du travail** : définissez la limite d’unités Analytics qui s’applique à l’utilisateur ou au groupe sélectionné.</span><span class="sxs-lookup"><span data-stu-id="13cfd-273">**Set the Job AU Limit**: Set the AU limit that applies to the selected user or group.</span></span>
    4. <span data-ttu-id="13cfd-274">**Définir la limite de priorité** : définissez la limite de priorité qui s’applique à l’utilisateur ou au groupe sélectionné.</span><span class="sxs-lookup"><span data-stu-id="13cfd-274">**Set the Priority Limit**: Set the priority limit that applies to the selected user or group.</span></span>

4. <span data-ttu-id="13cfd-275">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-275">Click **Ok**.</span></span>

5. <span data-ttu-id="13cfd-276">La nouvelle stratégie est répertoriée dans la table des stratégies **Par défaut**, sous **Limites d’envoi de tâches**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-276">The new policy is listed in the **Default** policy table, under **Job Submission Limits**.</span></span> 

#### <a name="delete-or-edit-an-existing-policy"></a><span data-ttu-id="13cfd-277">Supprimer ou modifier une stratégie existante</span><span class="sxs-lookup"><span data-stu-id="13cfd-277">Delete or edit an existing policy</span></span>

1. <span data-ttu-id="13cfd-278">Dans le portail Azure, accédez à votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="13cfd-278">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="13cfd-279">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-279">Click **Properties**.</span></span>
3. <span data-ttu-id="13cfd-280">Sous **Limites d’envoi de tâches**, recherchez la stratégie que vous souhaitez modifier.</span><span class="sxs-lookup"><span data-stu-id="13cfd-280">Under **Job Submission Limits**, find the policy you want to edit.</span></span>
4.  <span data-ttu-id="13cfd-281">Pour voir les options **Supprimer** et **Modifier**, dans la colonne la plus à droite de la table, cliquez sur **...**.</span><span class="sxs-lookup"><span data-stu-id="13cfd-281">To see the **Delete** and **Edit** options, in the rightmost column of the table, click **...**.</span></span>

### <a name="additional-resources-for-job-policies"></a><span data-ttu-id="13cfd-282">Ressources supplémentaires relatives aux stratégies de travail</span><span class="sxs-lookup"><span data-stu-id="13cfd-282">Additional resources for job policies</span></span>
* [<span data-ttu-id="13cfd-283">Post de blog Vue d’ensemble de la stratégie</span><span class="sxs-lookup"><span data-stu-id="13cfd-283">Policy overview blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [<span data-ttu-id="13cfd-284">Post de blog Stratégies au niveau du compte</span><span class="sxs-lookup"><span data-stu-id="13cfd-284">Account-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [<span data-ttu-id="13cfd-285">Post de blog Stratégies au niveau du travail</span><span class="sxs-lookup"><span data-stu-id="13cfd-285">Job-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a><span data-ttu-id="13cfd-286">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="13cfd-286">Next steps</span></span>

* [<span data-ttu-id="13cfd-287">Présentation d’Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="13cfd-287">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="13cfd-288">Prise en main de Data Lake Analytics à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="13cfd-288">Get started with Data Lake Analytics by using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="13cfd-289">Gestion d’Azure Data Lake Analytics à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="13cfd-289">Manage Azure Data Lake Analytics by using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)

