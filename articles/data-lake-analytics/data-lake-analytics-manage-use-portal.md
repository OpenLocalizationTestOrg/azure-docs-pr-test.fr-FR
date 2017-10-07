---
title: "aaaManage Analytique de LAC de données Azure à l’aide de hello portail Azure | Documents Microsoft"
description: "Découvrez comment toomanage acounts Analytique lac de données, données sources, les utilisateurs et des travaux."
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
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a><span data-ttu-id="a2522-103">Gérer Analytique de LAC de données Azure à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="a2522-103">Manage Azure Data Lake Analytics by using hello Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="a2522-104">Découvrez comment des comptes toomanage Analytique de LAC de données Azure, des sources de données de compte, des utilisateurs et des travaux à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a2522-104">Learn how toomanage Azure Data Lake Analytics accounts, account data sources, users, and jobs by using hello Azure portal.</span></span> <span data-ttu-id="a2522-105">les rubriques de gestion toosee sur l’utilisation d’autres outils, cliquez sur un onglet en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-105">toosee management topics about using other tools, click a tab at hello top of hello page.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a><span data-ttu-id="a2522-106">Gérer les comptes Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a2522-106">Manage Data Lake Analytics accounts</span></span>

### <a name="create-an-account"></a><span data-ttu-id="a2522-107">Créer un compte</span><span class="sxs-lookup"><span data-stu-id="a2522-107">Create an account</span></span>

1. <span data-ttu-id="a2522-108">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a2522-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a2522-109">Cliquez sur **Nouveau** > **Intelligence + analyse** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="a2522-109">Click **New** > **Intelligence + analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="a2522-110">Sélectionnez les valeurs de hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a2522-110">Select values for hello following items:</span></span> 
   1. <span data-ttu-id="a2522-111">**Nom**: nom hello Hello compte d’Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="a2522-111">**Name**: hello name of hello Data Lake Analytics account.</span></span>
   2. <span data-ttu-id="a2522-112">**Abonnement**: hello abonnement Azure utilisé pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-112">**Subscription**: hello Azure subscription used for hello account.</span></span>
   3. <span data-ttu-id="a2522-113">**Groupe de ressources**: groupe de ressources Azure hello dans quel compte de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="a2522-113">**Resource Group**: hello Azure resource group in which toocreate hello account.</span></span> 
   4. <span data-ttu-id="a2522-114">**Emplacement**: hello du centre de données Azure pour compte Analytique lac de données de hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-114">**Location**: hello Azure datacenter for hello Data Lake Analytics account.</span></span> 
   5. <span data-ttu-id="a2522-115">**Data Lake Store**: hello toobe de magasin par défaut utilisé pour hello Analytique lac de données compte.</span><span class="sxs-lookup"><span data-stu-id="a2522-115">**Data Lake Store**: hello default store toobe used for hello Data Lake Analytics account.</span></span> <span data-ttu-id="a2522-116">compte d’Azure Data Lake Store Hello et hello Analytique lac de données compte doit être dans hello même emplacement.</span><span class="sxs-lookup"><span data-stu-id="a2522-116">hello Azure Data Lake Store account and hello Data Lake Analytics account must be in hello same location.</span></span>
4. <span data-ttu-id="a2522-117">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="a2522-117">Click **Create**.</span></span> 

### <a name="delete-a-data-lake-analytics-account"></a><span data-ttu-id="a2522-118">Supprimer un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a2522-118">Delete a Data Lake Analytics account</span></span>

<span data-ttu-id="a2522-119">Avant de supprimer un compte Data Lake Analytics, vous devez supprimer le compte Data Lake Store dépendant.</span><span class="sxs-lookup"><span data-stu-id="a2522-119">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span></span>

1. <span data-ttu-id="a2522-120">Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.</span><span class="sxs-lookup"><span data-stu-id="a2522-120">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="a2522-121">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="a2522-121">Click **Delete**.</span></span>
3. <span data-ttu-id="a2522-122">Nom du compte type hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-122">Type hello account name.</span></span>
4. <span data-ttu-id="a2522-123">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="a2522-123">Click **Delete**.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a><span data-ttu-id="a2522-124">Gérer les sources de données</span><span class="sxs-lookup"><span data-stu-id="a2522-124">Manage data sources</span></span>

<span data-ttu-id="a2522-125">Analytique de LAC de données prend en charge hello les sources de données suivantes :</span><span class="sxs-lookup"><span data-stu-id="a2522-125">Data Lake Analytics supports hello following data sources:</span></span>

* <span data-ttu-id="a2522-126">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a2522-126">Data Lake Store</span></span>
* <span data-ttu-id="a2522-127">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a2522-127">Azure Storage</span></span>

<span data-ttu-id="a2522-128">Vous pouvez utiliser des sources de données toobrowse Explorateur de données et effectuer des opérations de gestion de fichiers de base.</span><span class="sxs-lookup"><span data-stu-id="a2522-128">You can use Data Explorer toobrowse data sources and perform basic file management operations.</span></span> 

### <a name="add-a-data-source"></a><span data-ttu-id="a2522-129">Ajouter une source de données</span><span class="sxs-lookup"><span data-stu-id="a2522-129">Add a data source</span></span>

1. <span data-ttu-id="a2522-130">Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.</span><span class="sxs-lookup"><span data-stu-id="a2522-130">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="a2522-131">Cliquez sur **Sources de données**.</span><span class="sxs-lookup"><span data-stu-id="a2522-131">Click **Data Sources**.</span></span>
3. <span data-ttu-id="a2522-132">Cliquez sur **Ajouter une source de données**.</span><span class="sxs-lookup"><span data-stu-id="a2522-132">Click **Add Data Source**.</span></span>
    
   * <span data-ttu-id="a2522-133">tooadd un compte Data Lake Store, vous devez compte hello toohello d’accès et le nom de compte tooquery en mesure de toobe il.</span><span class="sxs-lookup"><span data-stu-id="a2522-133">tooadd a Data Lake Store account, you need hello account name and access toohello account toobe able tooquery it.</span></span>
   * <span data-ttu-id="a2522-134">tooadd stockage d’objets Blob Azure, vous devez compte de stockage hello et clé de compte hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-134">tooadd Azure Blob storage, you need hello storage account and hello account key.</span></span> <span data-ttu-id="a2522-135">toofind compte de stockage toohello leur, allez dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-135">toofind them, go toohello storage account in hello portal.</span></span>

## <a name="set-up-firewall-rules"></a><span data-ttu-id="a2522-136">Configurer des règles de pare-feu</span><span class="sxs-lookup"><span data-stu-id="a2522-136">Set up firewall rules</span></span>

<span data-ttu-id="a2522-137">Vous pouvez utiliser les données Lake Analytique toofurther verrouiller accès tooyour compte d’Analytique lac de données au niveau du réseau hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-137">You can use Data Lake Analytics toofurther lock down access tooyour Data Lake Analytics account at hello network level.</span></span> <span data-ttu-id="a2522-138">Vous pouvez activer un pare-feu, spécifier une adresse IP ou définir une plage d’adresses IP pour vos clients approuvés.</span><span class="sxs-lookup"><span data-stu-id="a2522-138">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="a2522-139">Une fois que ces mesures, seuls les clients qui ont des adresses IP de hello plage hello défini peuvent se connecter toohello magasin.</span><span class="sxs-lookup"><span data-stu-id="a2522-139">After you enable these measures, only clients that have hello IP addresses within hello defined range can connect toohello store.</span></span>

<span data-ttu-id="a2522-140">Si d’autres services Azure, comme Azure Data Factory ou des machines virtuelles, vous connecter compte Analytique lac de données de toohello, assurez-vous que **autoriser les Services Azure** est activé **sur**.</span><span class="sxs-lookup"><span data-stu-id="a2522-140">If other Azure services, like Azure Data Factory or VMs, connect toohello Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span></span> 

### <a name="set-up-a-firewall-rule"></a><span data-ttu-id="a2522-141">Configurer une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="a2522-141">Set up a firewall rule</span></span>

1. <span data-ttu-id="a2522-142">Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.</span><span class="sxs-lookup"><span data-stu-id="a2522-142">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="a2522-143">Dans le menu hello hello gauche, cliquez sur **pare-feu**.</span><span class="sxs-lookup"><span data-stu-id="a2522-143">On hello menu on hello left, click **Firewall**.</span></span>

## <a name="add-a-new-user"></a><span data-ttu-id="a2522-144">Ajouter un nouvel utilisateur</span><span class="sxs-lookup"><span data-stu-id="a2522-144">Add a new user</span></span>

<span data-ttu-id="a2522-145">Vous pouvez utiliser hello **Assistant Ajout d’utilisateur** tooeasily configurer de nouveaux utilisateurs lac de données.</span><span class="sxs-lookup"><span data-stu-id="a2522-145">You can use hello **Add User Wizard** tooeasily provision new Data Lake users.</span></span>

1. <span data-ttu-id="a2522-146">Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.</span><span class="sxs-lookup"><span data-stu-id="a2522-146">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="a2522-147">Sur hello de gauche, sous **mise en route**, cliquez sur **Assistant Ajout d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="a2522-147">On hello left, under **Getting Started**, click **Add User Wizard**.</span></span>
3. <span data-ttu-id="a2522-148">Sélectionnez un utilisateur, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a2522-148">Select a user, and then click **Select**.</span></span>
4. <span data-ttu-id="a2522-149">Sélectionnez un rôle, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a2522-149">Select a role, and then click **Select**.</span></span> <span data-ttu-id="a2522-150">tooset d’un nouveau toouse de développeur Azure Data Lake, sélectionnez hello **données Lake Analytique développeur** rôle.</span><span class="sxs-lookup"><span data-stu-id="a2522-150">tooset up a new developer toouse Azure Data Lake, select hello **Data Lake Analytics Developer** role.</span></span>
5. <span data-ttu-id="a2522-151">Sélectionnez les listes de contrôle d’accès hello (ACL) pour les bases de données hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a2522-151">Select hello access control lists (ACLs) for hello U-SQL databases.</span></span> <span data-ttu-id="a2522-152">Lorsque vous êtes satisfait de vos choix, cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="a2522-152">When you're satisfied with your choices, click **Select**.</span></span>
6. <span data-ttu-id="a2522-153">Sélectionnez les ACL hello pour les fichiers.</span><span class="sxs-lookup"><span data-stu-id="a2522-153">Select hello ACLs for files.</span></span> <span data-ttu-id="a2522-154">Hello banque par défaut, ne modifiez pas les ACL hello pour le dossier racine de hello « / » et pour hello/System dossier.</span><span class="sxs-lookup"><span data-stu-id="a2522-154">For hello default store, don't change hello ACLs for hello root folder "/" and for hello /system folder.</span></span> <span data-ttu-id="a2522-155">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="a2522-155">Click **Select**.</span></span>
7. <span data-ttu-id="a2522-156">Passez en revue toutes vos sélections, puis cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="a2522-156">Review all your selected changes, and then click **Run**.</span></span>
8. <span data-ttu-id="a2522-157">Hello Assistant terminé, cliquez sur **fait**.</span><span class="sxs-lookup"><span data-stu-id="a2522-157">When hello wizard is finished, click **Done**.</span></span>

## <a name="manage-role-based-access-control"></a><span data-ttu-id="a2522-158">Gérer le contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="a2522-158">Manage Role-Based Access Control</span></span>

<span data-ttu-id="a2522-159">Comme d’autres services Azure, vous pouvez utiliser toocontrol de contrôle d’accès en fonction du rôle (RBAC) comment les utilisateurs interagissent avec le service de hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-159">Like other Azure services, you can use Role-Based Access Control (RBAC) toocontrol how users interact with hello service.</span></span>

<span data-ttu-id="a2522-160">les rôles RBAC standards Hello ont hello suivant de fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="a2522-160">hello standard RBAC roles have hello following capabilities:</span></span>
* <span data-ttu-id="a2522-161">**Propriétaire**: peut envoyer des travaux, surveillez les travaux, annuler les travaux à partir de n’importe quel utilisateur et configurer le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-161">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="a2522-162">**Collaborateur**: peut envoyer des travaux, surveillez les travaux, annuler les travaux à partir de n’importe quel utilisateur et configurer le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-162">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="a2522-163">**Lecteur** : peut surveiller des travaux.</span><span class="sxs-lookup"><span data-stu-id="a2522-163">**Reader**: Can monitor jobs.</span></span>

<span data-ttu-id="a2522-164">Utilisez hello données Lake Analytique développeur rôle tooenable U-SQL développeurs toouse hello Analytique lac de données service.</span><span class="sxs-lookup"><span data-stu-id="a2522-164">Use hello Data Lake Analytics Developer role tooenable U-SQL developers toouse hello Data Lake Analytics service.</span></span> <span data-ttu-id="a2522-165">Vous pouvez utiliser le rôle de développeur du lac de données Analytique hello pour :</span><span class="sxs-lookup"><span data-stu-id="a2522-165">You can use hello Data Lake Analytics Developer role to:</span></span>
* <span data-ttu-id="a2522-166">Envoyer des travaux.</span><span class="sxs-lookup"><span data-stu-id="a2522-166">Submit jobs.</span></span>
* <span data-ttu-id="a2522-167">Surveiller la progression de statut et hello travail soumis par n’importe quel utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a2522-167">Monitor job status and hello progress of jobs submitted by any user.</span></span>
* <span data-ttu-id="a2522-168">Consultez hello U-SQL de scripts de travaux soumis par les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a2522-168">See hello U-SQL scripts from jobs submitted by any user.</span></span>
* <span data-ttu-id="a2522-169">Annuler uniquement vos propres travaux.</span><span class="sxs-lookup"><span data-stu-id="a2522-169">Cancel only your own jobs.</span></span>

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a><span data-ttu-id="a2522-170">Ajouter des utilisateurs ou des groupes de sécurité tooa compte d’Analytique lac de données</span><span class="sxs-lookup"><span data-stu-id="a2522-170">Add users or security groups tooa Data Lake Analytics account</span></span>

1. <span data-ttu-id="a2522-171">Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.</span><span class="sxs-lookup"><span data-stu-id="a2522-171">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="a2522-172">Cliquez sur **Contrôle d’accès (IAM)** > **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a2522-172">Click **Access control (IAM)** > **Add**.</span></span>
3. <span data-ttu-id="a2522-173">Sélectionnez un rôle</span><span class="sxs-lookup"><span data-stu-id="a2522-173">Select a role.</span></span>
4. <span data-ttu-id="a2522-174">Ajoutez un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a2522-174">Add a user.</span></span>
5. <span data-ttu-id="a2522-175">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a2522-175">Click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="a2522-176">Si un utilisateur ou un groupe de sécurité doit toosubmit travaux, ils doivent également l’autorisation sur le compte du magasin hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-176">If a user or a security group needs toosubmit jobs, they also need permission on hello store account.</span></span> <span data-ttu-id="a2522-177">Pour plus d’informations, consultez [Sécuriser les données stockées dans Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span><span class="sxs-lookup"><span data-stu-id="a2522-177">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span></span>
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a><span data-ttu-id="a2522-178">Gestion des travaux</span><span class="sxs-lookup"><span data-stu-id="a2522-178">Manage jobs</span></span>

### <a name="submit-a-job"></a><span data-ttu-id="a2522-179">Soumettre un travail</span><span class="sxs-lookup"><span data-stu-id="a2522-179">Submit a job</span></span>

1. <span data-ttu-id="a2522-180">Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.</span><span class="sxs-lookup"><span data-stu-id="a2522-180">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>

2. <span data-ttu-id="a2522-181">Cliquez sur **Nouveau travail**.</span><span class="sxs-lookup"><span data-stu-id="a2522-181">Click **New Job**.</span></span> <span data-ttu-id="a2522-182">Pour chaque travail, configurez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a2522-182">For each job,  configure:</span></span>

    1. <span data-ttu-id="a2522-183">**Nom de la tâche**: nom hello du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-183">**Job Name**: hello name of hello job.</span></span>
    2. <span data-ttu-id="a2522-184">**Priorité** : les nombres inférieurs ont une priorité supérieure.</span><span class="sxs-lookup"><span data-stu-id="a2522-184">**Priority**: Lower numbers have higher priority.</span></span> <span data-ttu-id="a2522-185">Si deux travaux est en attente, hello une valeur de priorité inférieure s’exécute en premier.</span><span class="sxs-lookup"><span data-stu-id="a2522-185">If two jobs are queued, hello one with lower priority value runs first.</span></span>
    3. <span data-ttu-id="a2522-186">**Parallélisme**: nombre maximal de hello de compute traite tooreserve pour ce travail.</span><span class="sxs-lookup"><span data-stu-id="a2522-186">**Parallelism**: hello maximum number of compute processes tooreserve for this job.</span></span>

3. <span data-ttu-id="a2522-187">Cliquez sur **Envoyer le travail**.</span><span class="sxs-lookup"><span data-stu-id="a2522-187">Click **Submit Job**.</span></span>

### <a name="monitor-jobs"></a><span data-ttu-id="a2522-188">Surveiller des travaux</span><span class="sxs-lookup"><span data-stu-id="a2522-188">Monitor jobs</span></span>

1. <span data-ttu-id="a2522-189">Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.</span><span class="sxs-lookup"><span data-stu-id="a2522-189">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="a2522-190">Cliquez sur **Afficher tous les travaux**.</span><span class="sxs-lookup"><span data-stu-id="a2522-190">Click **View All Jobs**.</span></span> <span data-ttu-id="a2522-191">Une liste de tous les travaux actifs et récemment terminé hello dans le compte de hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a2522-191">A list of all hello active and recently finished jobs in hello account is shown.</span></span>
3. <span data-ttu-id="a2522-192">Si vous le souhaitez, cliquez sur **filtre** toohelp vous recherchez les travaux de hello par **période**, **nom de la tâche**, et **auteur** valeurs.</span><span class="sxs-lookup"><span data-stu-id="a2522-192">Optionally, click **Filter** toohelp you find hello jobs by **Time Range**, **Job Name**, and **Author** values.</span></span> 

### <a name="monitoring-pipeline-jobs"></a><span data-ttu-id="a2522-193">Surveillance des tâches de pipeline</span><span class="sxs-lookup"><span data-stu-id="a2522-193">Monitoring pipeline jobs</span></span>
<span data-ttu-id="a2522-194">Les travaux qui font partie d’un pipeline fonctionnent ensemble, généralement séquentiellement, tooaccomplish un scénario spécifique.</span><span class="sxs-lookup"><span data-stu-id="a2522-194">Jobs that are part of a pipeline work together, usually sequentially, tooaccomplish a specific scenario.</span></span> <span data-ttu-id="a2522-195">Par exemple, vous pouvez avoir un pipeline qui nettoie, extrait, transforme, regroupe l’utilisation des informations du client.</span><span class="sxs-lookup"><span data-stu-id="a2522-195">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span></span> <span data-ttu-id="a2522-196">Travaux de pipeline est identifiés à l’aide de la propriété « Pipeline » de hello lors de la soumission de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-196">Pipeline jobs are identified using hello "Pipeline" property when hello job was submitted.</span></span> <span data-ttu-id="a2522-197">Les tâches planifiées à l’aide du fichier de définition d’application V2 auront automatiquement cette propriété remplie.</span><span class="sxs-lookup"><span data-stu-id="a2522-197">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span> 

<span data-ttu-id="a2522-198">tooview une liste des tâches U-SQL qui font partie de pipelines :</span><span class="sxs-lookup"><span data-stu-id="a2522-198">tooview a list of U-SQL jobs that are part of pipelines:</span></span> 

1. <span data-ttu-id="a2522-199">Bonjour portail Azure, accédez à des comptes tooyour Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="a2522-199">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="a2522-200">Cliquez sur **Informations sur les tâches**.</span><span class="sxs-lookup"><span data-stu-id="a2522-200">Click **Job Insights**.</span></span> <span data-ttu-id="a2522-201">Bonjour qu'onglet « Toutes les tâches » prendra par défaut, qui contient la liste en cours d’exécution, en file d’attente et fin des tâches.</span><span class="sxs-lookup"><span data-stu-id="a2522-201">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="a2522-202">Cliquez sur hello **Pipeline travaux** onglet. Une liste des tâches de pipeline s’affiche, ainsi que des statistiques agrégées pour chaque pipeline.</span><span class="sxs-lookup"><span data-stu-id="a2522-202">Click hello **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span></span>

### <a name="monitoring-recurring-jobs"></a><span data-ttu-id="a2522-203">Surveillance des tâches récurrentes</span><span class="sxs-lookup"><span data-stu-id="a2522-203">Monitoring recurring jobs</span></span>
<span data-ttu-id="a2522-204">Un abonnement est un travail qui a hello même logique métier mais utilise les données d’entrée différente chaque fois qu’il exécute.</span><span class="sxs-lookup"><span data-stu-id="a2522-204">A recurring job is one that has hello same business logic but uses different input data every time it runs.</span></span> <span data-ttu-id="a2522-205">Dans l’idéal, tâches périodiques doivent toujours réussir et ont relativement stable exécution ; Ces comportements d’analyse afin de garantir le travail de hello est intègre.</span><span class="sxs-lookup"><span data-stu-id="a2522-205">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure hello job is healthy.</span></span> <span data-ttu-id="a2522-206">Tâches périodiques sont identifiés à l’aide de la propriété « Recurrence » de hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-206">Recurring jobs are identified using hello "Recurrence" property.</span></span> <span data-ttu-id="a2522-207">Les tâches planifiées à l’aide du fichier de définition d’application V2 auront automatiquement cette propriété remplie.</span><span class="sxs-lookup"><span data-stu-id="a2522-207">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span>

<span data-ttu-id="a2522-208">tooview une liste des tâches U-SQL qui sont récurrents :</span><span class="sxs-lookup"><span data-stu-id="a2522-208">tooview a list of U-SQL jobs that are recurring:</span></span> 

1. <span data-ttu-id="a2522-209">Bonjour portail Azure, accédez à des comptes tooyour Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="a2522-209">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="a2522-210">Cliquez sur **Informations sur les tâches**.</span><span class="sxs-lookup"><span data-stu-id="a2522-210">Click **Job Insights**.</span></span> <span data-ttu-id="a2522-211">Bonjour qu'onglet « Toutes les tâches » prendra par défaut, qui contient la liste en cours d’exécution, en file d’attente et fin des tâches.</span><span class="sxs-lookup"><span data-stu-id="a2522-211">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="a2522-212">Cliquez sur hello **périodique des travaux** onglet. Une liste des tâches récurrentes s’affiche, ainsi que des statistiques agrégées pour chaque tâche récurrente.</span><span class="sxs-lookup"><span data-stu-id="a2522-212">Click hello **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span></span>

## <a name="manage-policies"></a><span data-ttu-id="a2522-213">Gérer les stratégies</span><span class="sxs-lookup"><span data-stu-id="a2522-213">Manage policies</span></span>

### <a name="account-level-policies"></a><span data-ttu-id="a2522-214">Stratégies au niveau du compte</span><span class="sxs-lookup"><span data-stu-id="a2522-214">Account-level policies</span></span>

<span data-ttu-id="a2522-215">Ces stratégies s’appliquent à des travaux de tooall dans un compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="a2522-215">These policies apply tooall jobs in a Data Lake Analytics account.</span></span>

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a><span data-ttu-id="a2522-216">Nombre maximal d’unités Analytics dans un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a2522-216">Maximum number of AUs in a Data Lake Analytics account</span></span>
<span data-ttu-id="a2522-217">Une stratégie de contrôle le nombre total de hello d’Analytique unités (AUs), votre compte Analytique lac de données peut utiliser.</span><span class="sxs-lookup"><span data-stu-id="a2522-217">A policy controls hello total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span></span> <span data-ttu-id="a2522-218">Par défaut, hello est la valeur too250.</span><span class="sxs-lookup"><span data-stu-id="a2522-218">By default, hello value is set too250.</span></span> <span data-ttu-id="a2522-219">Par exemple, si cette valeur est définie à too250 AUs, vous pouvez avoir une tâche est exécutée avec 250 AUs affectés tooit ou 10 travaux en cours d’exécution avec 25 AUs chaque.</span><span class="sxs-lookup"><span data-stu-id="a2522-219">For example, if this value is set too250 AUs, you can have one job running with 250 AUs assigned tooit, or 10 jobs running with 25 AUs each.</span></span> <span data-ttu-id="a2522-220">Tâches supplémentaires qui sont envoyées sont en file d’attente jusqu'à ce que les travaux en cours d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-220">Additional jobs that are submitted are queued until hello running jobs are finished.</span></span> <span data-ttu-id="a2522-221">Lorsque des travaux en cours d’exécution sont terminées, AUs sont libérer hello en file d’attente des travaux toorun.</span><span class="sxs-lookup"><span data-stu-id="a2522-221">When running jobs are finished, AUs are freed up for hello queued jobs toorun.</span></span>

<span data-ttu-id="a2522-222">nombre de hello toochange de AUs pour votre compte Analytique lac de données :</span><span class="sxs-lookup"><span data-stu-id="a2522-222">toochange hello number of AUs for your Data Lake Analytics account:</span></span>

1. <span data-ttu-id="a2522-223">Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.</span><span class="sxs-lookup"><span data-stu-id="a2522-223">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="a2522-224">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="a2522-224">Click **Properties**.</span></span>
3. <span data-ttu-id="a2522-225">Sous **AUs maximale**, déplacer hello curseur tooselect une valeur ou entrez la valeur de hello dans la zone de texte hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-225">Under **Maximum AUs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="a2522-226">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a2522-226">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="a2522-227">Si vous avez besoin de plus de hello par défaut (250) AUs, dans le portail hello, cliquez sur **aide + Support** toosubmit une demande de support.</span><span class="sxs-lookup"><span data-stu-id="a2522-227">If you need more than hello default (250) AUs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="a2522-228">nombre de Hello de AUs disponibles dans votre compte Analytique lac de données peut être augmenté.</span><span class="sxs-lookup"><span data-stu-id="a2522-228">hello number of AUs available in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a><span data-ttu-id="a2522-229">Nombre maximal de travaux pouvant s’exécuter simultanément</span><span class="sxs-lookup"><span data-stu-id="a2522-229">Maximum number of jobs that can run simultaneously</span></span>
<span data-ttu-id="a2522-230">Une stratégie de contrôle le nombre de travaux peut exécuter à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="a2522-230">A policy controls how many jobs can run at hello same time.</span></span> <span data-ttu-id="a2522-231">Par défaut, cette valeur est définie à too20.</span><span class="sxs-lookup"><span data-stu-id="a2522-231">By default, this value is set too20.</span></span> <span data-ttu-id="a2522-232">Si votre Analytique lac de données a AUs disponibles, nouvelles tâches sont planifiée toorun immédiatement tant que le nombre total de hello de travaux en cours d’exécution atteint la valeur hello de cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="a2522-232">If your Data Lake Analytics has AUs available, new jobs are scheduled toorun immediately until hello total number of running jobs reaches hello value of this policy.</span></span> <span data-ttu-id="a2522-233">Lorsque vous atteignez le nombre maximal de hello de tâches pouvant être exécutés simultanément, les tâches suivantes sont en attente dans l’ordre de priorité jusqu'à ce que la fin d’une ou plusieurs tâches en cours d’exécution (selon la disponibilité de l’Australie).</span><span class="sxs-lookup"><span data-stu-id="a2522-233">When you reach hello maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span></span>

<span data-ttu-id="a2522-234">nombre de hello toochange de tâches qui peuvent s’exécuter simultanément :</span><span class="sxs-lookup"><span data-stu-id="a2522-234">toochange hello number of jobs that can run simultaneously:</span></span>

1. <span data-ttu-id="a2522-235">Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.</span><span class="sxs-lookup"><span data-stu-id="a2522-235">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="a2522-236">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="a2522-236">Click **Properties**.</span></span>
3. <span data-ttu-id="a2522-237">Sous **nombre maximal de travaux d’en cours d’exécution**, déplacer hello curseur tooselect une valeur ou entrez la valeur de hello dans la zone de texte hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-237">Under **Maximum Number of Running Jobs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="a2522-238">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a2522-238">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="a2522-239">Si vous avez besoin de toorun plus que hello par défaut (20) nombre de travaux, dans le portail de hello, cliquez sur **aide + Support** toosubmit une demande de support.</span><span class="sxs-lookup"><span data-stu-id="a2522-239">If you need toorun more than hello default (20) number of jobs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="a2522-240">nombre de Hello de travaux pouvant s’exécuter simultanément dans votre compte Analytique lac de données peut être augmenté.</span><span class="sxs-lookup"><span data-stu-id="a2522-240">hello number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a><span data-ttu-id="a2522-241">La durée pendant laquelle les métadonnées de tâche tookeep et ressources</span><span class="sxs-lookup"><span data-stu-id="a2522-241">How long tookeep job metadata and resources</span></span> 
<span data-ttu-id="a2522-242">Lorsque les utilisateurs exécutent des travaux U-SQL, hello service de données Lake Analytique conserve tous les fichiers associés.</span><span class="sxs-lookup"><span data-stu-id="a2522-242">When your users run U-SQL jobs, hello Data Lake Analytics service retains all related files.</span></span> <span data-ttu-id="a2522-243">Les fichiers associés incluent un script de hello U-SQL, les fichiers DLL hello référencés dans le script de hello U-SQL, les ressources compilées et les statistiques.</span><span class="sxs-lookup"><span data-stu-id="a2522-243">Related files include hello U-SQL script, hello DLL files referenced in hello U-SQL script, compiled resources, and statistics.</span></span> <span data-ttu-id="a2522-244">les fichiers de Hello sont dans le dossier de /system/ hello du compte de stockage de LAC de données Azure hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="a2522-244">hello files are in hello /system/ folder of hello default Azure Data Lake Storage account.</span></span> <span data-ttu-id="a2522-245">Cette stratégie contrôle la durée pendant laquelle ces ressources sont stockées avant d’être automatiquement supprimés (valeur par défaut hello est de 30 jours).</span><span class="sxs-lookup"><span data-stu-id="a2522-245">This policy controls how long these resources are stored before they are automatically deleted (hello default is 30 days).</span></span> <span data-ttu-id="a2522-246">Vous pouvez utiliser ces fichiers pour le débogage et pour régler les performances des tâches que vous devez réexécuter Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="a2522-246">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in hello future.</span></span>

<span data-ttu-id="a2522-247">toochange la durée pendant laquelle les métadonnées de tâche tookeep et ressources :</span><span class="sxs-lookup"><span data-stu-id="a2522-247">toochange how long tookeep job metadata and resources:</span></span>

1. <span data-ttu-id="a2522-248">Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.</span><span class="sxs-lookup"><span data-stu-id="a2522-248">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="a2522-249">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="a2522-249">Click **Properties**.</span></span>
3. <span data-ttu-id="a2522-250">Sous **jours tooRetain travail interroge**, déplacer hello curseur tooselect une valeur ou entrez la valeur de hello dans la zone de texte hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-250">Under **Days tooRetain Job Queries**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span>  
4. <span data-ttu-id="a2522-251">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a2522-251">Click **Save**.</span></span>

### <a name="job-level-policies"></a><span data-ttu-id="a2522-252">Stratégies au niveau du travail</span><span class="sxs-lookup"><span data-stu-id="a2522-252">Job-level policies</span></span>
<span data-ttu-id="a2522-253">Avec les stratégies au niveau du projet, vous pouvez contrôler hello AUs maximales et hello priorité maximale que des utilisateurs individuels (ou les membres de groupes de sécurité spécifiques) peuvent définir sur les tâches qu’ils ont envoyés.</span><span class="sxs-lookup"><span data-stu-id="a2522-253">With job-level policies, you can control hello maximum AUs and hello maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span></span> <span data-ttu-id="a2522-254">Cette permet de contrôler les coûts de hello induites par les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a2522-254">This lets you control hello costs incurred by users.</span></span> <span data-ttu-id="a2522-255">Il vous permet également d’effet hello que les tâches planifiées peut-être avoir sur haute priorité des tâches de production qui sont exécutent dans hello même compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="a2522-255">It also lets you control hello effect that scheduled jobs might have on high-priority production jobs that are running in hello same Data Lake Analytics account.</span></span>

<span data-ttu-id="a2522-256">Analytique de LAC de données a deux stratégies que vous pouvez définir au niveau du travail hello :</span><span class="sxs-lookup"><span data-stu-id="a2522-256">Data Lake Analytics has two policies that you can set at hello job level:</span></span>

* <span data-ttu-id="a2522-257">**Limite de l’Australie par travail**: les utilisateurs peuvent envoyer uniquement les tâches qui ont des nombre toothis de l’Australie.</span><span class="sxs-lookup"><span data-stu-id="a2522-257">**AU limit per job**: Users can only submit jobs that have up toothis number of AUs.</span></span> <span data-ttu-id="a2522-258">Par défaut, cette limite est hello identique hello AU nombre maximal de compte de hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-258">By default, this limit is hello same as hello maximum AU limit for hello account.</span></span>
* <span data-ttu-id="a2522-259">**Priorité**: les utilisateurs peuvent envoyer uniquement les tâches qui ont une valeur toothis inférieur ou égal à priorité.</span><span class="sxs-lookup"><span data-stu-id="a2522-259">**Priority**: Users can only submit jobs that have a priority lower than or equal toothis value.</span></span> <span data-ttu-id="a2522-260">Notez qu’un nombre plus élevé signifie une priorité plus faible.</span><span class="sxs-lookup"><span data-stu-id="a2522-260">Note that a higher number means a lower priority.</span></span> <span data-ttu-id="a2522-261">Par défaut, il a la valeur too1, qui est la priorité la plus élevée hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-261">By default, this is set too1, which is hello highest possible priority.</span></span>

<span data-ttu-id="a2522-262">Chaque compte contient une stratégie par défaut.</span><span class="sxs-lookup"><span data-stu-id="a2522-262">There is a default policy set on every account.</span></span> <span data-ttu-id="a2522-263">stratégie par défaut de Hello s’applique aux utilisateurs de tooall du compte de hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-263">hello default policy applies tooall users of hello account.</span></span> <span data-ttu-id="a2522-264">Vous pouvez définir des stratégies supplémentaires pour des utilisateurs et des groupes spécifiques.</span><span class="sxs-lookup"><span data-stu-id="a2522-264">You can set additional policies for specific users and groups.</span></span> 

> [!NOTE]
> <span data-ttu-id="a2522-265">Les stratégies au niveau du compte et les stratégies au niveau du travail s’appliquent simultanément.</span><span class="sxs-lookup"><span data-stu-id="a2522-265">Account-level policies and job-level policies apply simultaneously.</span></span>
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a><span data-ttu-id="a2522-266">Ajouter une stratégie pour un utilisateur ou un groupe spécifique</span><span class="sxs-lookup"><span data-stu-id="a2522-266">Add a policy for a specific user or group</span></span>

1. <span data-ttu-id="a2522-267">Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.</span><span class="sxs-lookup"><span data-stu-id="a2522-267">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="a2522-268">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="a2522-268">Click **Properties**.</span></span>
3. <span data-ttu-id="a2522-269">Sous **limite de tâches de présentation**, cliquez sur hello **ajouter une stratégie** bouton.</span><span class="sxs-lookup"><span data-stu-id="a2522-269">Under **Job Submission Limits**, click hello **Add Policy** button.</span></span> <span data-ttu-id="a2522-270">Ensuite, sélectionnez ou entrez hello suivant les paramètres :</span><span class="sxs-lookup"><span data-stu-id="a2522-270">Then, select or enter hello following settings:</span></span>
    1. <span data-ttu-id="a2522-271">**Nom de la stratégie de calcul**: entrez un nom de la stratégie tooremind vous objectif hello de stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="a2522-271">**Compute Policy Name**: Enter a policy name, tooremind you of hello purpose of hello policy.</span></span>
    2. <span data-ttu-id="a2522-272">**Sélectionnez l’utilisateur ou le groupe**: sélectionnez hello utilisateur ou un groupe s’applique cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="a2522-272">**Select User or Group**: Select hello user or group this policy applies to.</span></span>
    3. <span data-ttu-id="a2522-273">**Définir hello limite de tâche de l’Australie**: définir la limite de hello AU qui s’applique toohello sélectionné utilisateur ou groupe.</span><span class="sxs-lookup"><span data-stu-id="a2522-273">**Set hello Job AU Limit**: Set hello AU limit that applies toohello selected user or group.</span></span>
    4. <span data-ttu-id="a2522-274">**Définir hello limite de priorité**: définir la limite de priorité hello qui s’applique toohello sélectionné utilisateur ou groupe.</span><span class="sxs-lookup"><span data-stu-id="a2522-274">**Set hello Priority Limit**: Set hello priority limit that applies toohello selected user or group.</span></span>

4. <span data-ttu-id="a2522-275">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a2522-275">Click **Ok**.</span></span>

5. <span data-ttu-id="a2522-276">nouvelle stratégie de Hello est répertoriée dans hello **par défaut** stratégie de table, sous **limites de soumission de travail**.</span><span class="sxs-lookup"><span data-stu-id="a2522-276">hello new policy is listed in hello **Default** policy table, under **Job Submission Limits**.</span></span> 

#### <a name="delete-or-edit-an-existing-policy"></a><span data-ttu-id="a2522-277">Supprimer ou modifier une stratégie existante</span><span class="sxs-lookup"><span data-stu-id="a2522-277">Delete or edit an existing policy</span></span>

1. <span data-ttu-id="a2522-278">Bonjour portail Azure, accédez à compte Analytique lac de données de tooyour.</span><span class="sxs-lookup"><span data-stu-id="a2522-278">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="a2522-279">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="a2522-279">Click **Properties**.</span></span>
3. <span data-ttu-id="a2522-280">Sous **limite de tâches de présentation**, rechercher hello stratégie tooedit.</span><span class="sxs-lookup"><span data-stu-id="a2522-280">Under **Job Submission Limits**, find hello policy you want tooedit.</span></span>
4.  <span data-ttu-id="a2522-281">toosee hello **supprimer** et **modifier** options, dans la colonne de droite hello de table de hello, cliquez sur **...** .</span><span class="sxs-lookup"><span data-stu-id="a2522-281">toosee hello **Delete** and **Edit** options, in hello rightmost column of hello table, click **...**.</span></span>

### <a name="additional-resources-for-job-policies"></a><span data-ttu-id="a2522-282">Ressources supplémentaires relatives aux stratégies de travail</span><span class="sxs-lookup"><span data-stu-id="a2522-282">Additional resources for job policies</span></span>
* [<span data-ttu-id="a2522-283">Post de blog Vue d’ensemble de la stratégie</span><span class="sxs-lookup"><span data-stu-id="a2522-283">Policy overview blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [<span data-ttu-id="a2522-284">Post de blog Stratégies au niveau du compte</span><span class="sxs-lookup"><span data-stu-id="a2522-284">Account-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [<span data-ttu-id="a2522-285">Post de blog Stratégies au niveau du travail</span><span class="sxs-lookup"><span data-stu-id="a2522-285">Job-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a><span data-ttu-id="a2522-286">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a2522-286">Next steps</span></span>

* [<span data-ttu-id="a2522-287">Présentation d’Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a2522-287">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="a2522-288">Prise en main Analytique lac de données à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="a2522-288">Get started with Data Lake Analytics by using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="a2522-289">Gestion d’Azure Data Lake Analytics à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2522-289">Manage Azure Data Lake Analytics by using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)

