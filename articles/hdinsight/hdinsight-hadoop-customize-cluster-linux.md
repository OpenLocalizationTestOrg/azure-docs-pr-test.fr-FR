---
title: "aaaCustomize des clusters HDInsight à l’aide des actions de script - Azure | Documents Microsoft"
description: "Ajouter des composants personnalisés en fonction de tooLinux de HDInsight des clusters à l’aide des Actions de Script. Actions de script sont des scripts Bash qui peuvent être la configuration de cluster utilisé toocustomize hello ou ajouter des services supplémentaires et des utilitaires de teinte, de Solr ou R."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="7ea15-104">Personnalisation de clusters HDInsight basés sur Linux à l'aide d'une action de script</span><span class="sxs-lookup"><span data-stu-id="7ea15-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="7ea15-105">HDInsight fournit une option de configuration appelée **Action de Script** qui appelle des scripts personnalisés qui personnalisent le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize hello cluster.</span></span> <span data-ttu-id="7ea15-106">Ces scripts sont utilisé tooinstall des composants supplémentaires et modifier les paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="7ea15-106">These scripts are used tooinstall additional components and change configuration settings.</span></span> <span data-ttu-id="7ea15-107">Les actions de script peuvent être utilisées pendant ou après la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="7ea15-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ea15-108">actions de script toouse Hello capacité sur un cluster déjà en cours d’exécution est uniquement disponible pour les clusters HDInsight de basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="7ea15-108">hello ability toouse script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="7ea15-109">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7ea15-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7ea15-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="7ea15-111">Actions de script peuvent également être publiée toohello Azure Marketplace en tant qu’une application HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ea15-111">Script actions can also be published toohello Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="7ea15-112">Certains des exemples hello dans ce document montrent comment vous pouvez installer une application de HDInsight à l’aide des commandes d’action de script à partir de PowerShell et hello du SDK .NET.</span><span class="sxs-lookup"><span data-stu-id="7ea15-112">Some of hello examples in this document show how you can install an HDInsight application using script action commands from PowerShell and hello .NET SDK.</span></span> <span data-ttu-id="7ea15-113">Pour plus d’informations sur les applications de HDInsight, consultez [HDInsight de publier des applications dans Azure Marketplace de hello](hdinsight-apps-publish-applications.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-113">For more information on HDInsight applications, see [Publish HDInsight applications into hello Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="7ea15-114">Autorisations</span><span class="sxs-lookup"><span data-stu-id="7ea15-114">Permissions</span></span>

<span data-ttu-id="7ea15-115">Si vous utilisez un cluster HDInsight à un domaine, il existe deux autorisations Ambari qui sont requises lors de l’utilisation des actions de script avec le cluster de hello :</span><span class="sxs-lookup"><span data-stu-id="7ea15-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with hello cluster:</span></span>

* <span data-ttu-id="7ea15-116">**AMBARI. Exécutez\_personnalisé\_commande**: rôle d’administrateur de Ambari hello possède cette autorisation par défaut.</span><span class="sxs-lookup"><span data-stu-id="7ea15-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: hello Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="7ea15-117">**METTRE EN CLUSTER. Exécutez\_personnalisé\_commande**: les deux hello administrateur de Cluster HDInsight et Ambari administrateur ont cette autorisation par défaut.</span><span class="sxs-lookup"><span data-stu-id="7ea15-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both hello HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="7ea15-118">Pour plus d’informations sur l’utilisation des autorisations avec un cluster HDInsight joint à un domaine, consultez [Gestion des clusters HDInsight joints à un domaine](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="7ea15-119">Contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="7ea15-119">Access control</span></span>

<span data-ttu-id="7ea15-120">Si vous n’êtes pas administrateur de hello/propriétaire de votre abonnement Azure, votre compte doit posséder au moins **collaborateur** groupe de ressources toohello accès qui contient le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-120">If you are not hello administrator/owner of your Azure subscription, your account must have at least **Contributor** access toohello resource group that contains hello HDInsight cluster.</span></span>

<span data-ttu-id="7ea15-121">En outre, si vous créez un cluster HDInsight, une personne disposant au moins **collaborateur** accès toohello abonnement Azure doit avoir inscrite précédemment fournisseur hello pour HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ea15-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access toohello Azure subscription must have previously registered hello provider for HDInsight.</span></span> <span data-ttu-id="7ea15-122">Inscription du fournisseur qui se produit quand un utilisateur avec un abonnement de collaborateur accès toohello crée une ressource pour hello première fois sur l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-122">Provider registration happens when a user with Contributor access toohello subscription creates a resource for hello first time on hello subscription.</span></span> <span data-ttu-id="7ea15-123">Vous pouvez également faire cela sans créer une ressource en [enregistrant un fournisseur à l’aide de REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ea15-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="7ea15-124">Pour plus d’informations sur l’utilisation de la gestion de l’accès, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="7ea15-124">For more information on working with access management, see hello following documents:</span></span>

* [<span data-ttu-id="7ea15-125">Prise en main Bonjour Azure portail de gestion de l’accès</span><span class="sxs-lookup"><span data-stu-id="7ea15-125">Get started with access management in hello Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="7ea15-126">Utiliser les ressources de rôle affectations toomanage accès tooyour abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="7ea15-126">Use role assignments toomanage access tooyour Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="7ea15-127">Comprendre les actions de script</span><span class="sxs-lookup"><span data-stu-id="7ea15-127">Understanding Script Actions</span></span>

<span data-ttu-id="7ea15-128">Une action de script est tout simplement un script Bash auquel vous apportez une URI et des paramètres.</span><span class="sxs-lookup"><span data-stu-id="7ea15-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="7ea15-129">script de Hello s’exécute sur les nœuds de cluster de HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-129">hello script runs on nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="7ea15-130">Hello Voici les caractéristiques et fonctionnalités des actions de script.</span><span class="sxs-lookup"><span data-stu-id="7ea15-130">hello following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="7ea15-131">Doit être stocké sur un URI qui est accessible à partir du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-131">Must be stored on a URI that is accessible from hello HDInsight cluster.</span></span> <span data-ttu-id="7ea15-132">Hello Voici les emplacements de stockage possibles :</span><span class="sxs-lookup"><span data-stu-id="7ea15-132">hello following are possible storage locations:</span></span>

    * <span data-ttu-id="7ea15-133">Un **Azure Data Lake Store** compte qui est accessible par le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-133">An **Azure Data Lake Store** account that is accessible by hello HDInsight cluster.</span></span> <span data-ttu-id="7ea15-134">Pour plus d’informations sur l’utilisation d'Azure Data Lake Store avec HDInsight, voir [Créer un cluster HDInsight avec Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="7ea15-135">Lorsque vous utilisez un script stocké dans Data Lake Store, le format d’URI hello est `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span><span class="sxs-lookup"><span data-stu-id="7ea15-135">When using a script stored in Data Lake Store, hello URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="7ea15-136">Hello service principal HDInsight utilise tooaccess Data Lake Store doit avoir accès en lecture toohello script.</span><span class="sxs-lookup"><span data-stu-id="7ea15-136">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

    * <span data-ttu-id="7ea15-137">Un objet blob dans un **compte de stockage Azure** qui est un compte de stockage primaire ou une autre de hello pour le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-137">A blob in an **Azure Storage account** that is either hello primary or additional storage account for hello HDInsight cluster.</span></span> <span data-ttu-id="7ea15-138">HDInsight est accordé tooboth d’accès de ces types de comptes de stockage pendant la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="7ea15-138">HDInsight is granted access tooboth of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="7ea15-139">Un service de partage de fichiers public, comme Azure Blob, GitHub, OneDrive, Dropbox, etc.</span><span class="sxs-lookup"><span data-stu-id="7ea15-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="7ea15-140">Par exemple les URI, consultez hello [scripts d’action de script exemple](#example-script-action-scripts) section.</span><span class="sxs-lookup"><span data-stu-id="7ea15-140">For example URIs, see hello [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="7ea15-141">HDInsight prend uniquement en charge les comptes de stockage Azure à __usage général__.</span><span class="sxs-lookup"><span data-stu-id="7ea15-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="7ea15-142">Il ne prend pas en charge hello __stockage d’objets Blob__ type de compte.</span><span class="sxs-lookup"><span data-stu-id="7ea15-142">It does not currently support hello __Blob storage__ account type.</span></span>

* <span data-ttu-id="7ea15-143">Peut être restreinte trop**s’exécutent sur les seuls certains types de nœud**, pour les nœuds principaux d’un exemple ou les nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="7ea15-143">Can be restricted too**run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="7ea15-144">Lorsqu’il est utilisé avec HDInsight Premium, vous pouvez spécifier que le script de hello doit être utilisé sur le nœud de périmètre hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-144">When used with HDInsight Premium, you can specify that hello script should be used on hello edge node.</span></span>

* <span data-ttu-id="7ea15-145">Son état peut être **persistant** ou **ad hoc**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="7ea15-146">**Persistante** scripts sont cluster de toohello ajouté nœuds tooworker appliqué après exécution du script hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-146">**Persisted** scripts are applied tooworker nodes added toohello cluster after hello script runs.</span></span> <span data-ttu-id="7ea15-147">Par exemple, lors de la mise à l’échelle d’un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-147">For example, when scaling up hello cluster.</span></span>

    <span data-ttu-id="7ea15-148">Un script persistant peut également appliquer les modifications tooanother nœud type, tel qu’un nœud principal.</span><span class="sxs-lookup"><span data-stu-id="7ea15-148">A persisted script might also apply changes tooanother node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7ea15-149">Les actions de script persistantes doivent avoir un nom unique.</span><span class="sxs-lookup"><span data-stu-id="7ea15-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="7ea15-150">Les scripts**Ad hoc** ne sont pas conservés.</span><span class="sxs-lookup"><span data-stu-id="7ea15-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="7ea15-151">Ils ne sont pas cluster de toohello ajouté nœuds tooworker appliquées après l’exécution de script de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-151">They are not applied tooworker nodes added toohello cluster after hello script has ran.</span></span> <span data-ttu-id="7ea15-152">Par la suite, vous pouvez promouvoir un tooa script ad hoc persistant de script, ou rétrograder un script ad hoc tooan de script persistantes.</span><span class="sxs-lookup"><span data-stu-id="7ea15-152">You can subsequently promote an ad hoc script tooa persisted script, or demote a persisted script tooan ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7ea15-153">Les actions de script utilisées lors de la création du cluster sont automatiquement rendues persistantes.</span><span class="sxs-lookup"><span data-stu-id="7ea15-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="7ea15-154">Les scripts qui échouent ne sont pas rendus persistants, même si vous précisez qu’ils doivent l’être.</span><span class="sxs-lookup"><span data-stu-id="7ea15-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="7ea15-155">Peut accepter **paramètres** qui sont utilisés par le script de hello lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="7ea15-155">Can accept **parameters** that are used by hello script during execution.</span></span>
* <span data-ttu-id="7ea15-156">Exécuter avec **racine des privilèges de niveau** sur les nœuds de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-156">Run with **root level privileges** on hello cluster nodes.</span></span>
* <span data-ttu-id="7ea15-157">Peut être utilisé par le biais hello **portail Azure**, **Azure PowerShell**, **CLI d’Azure**, ou **HDInsight .NET SDK**</span><span class="sxs-lookup"><span data-stu-id="7ea15-157">Can be used through hello **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="7ea15-158">cluster de Hello conserve un historique de tous les scripts ont été exécutés.</span><span class="sxs-lookup"><span data-stu-id="7ea15-158">hello cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="7ea15-159">historique de Hello est utile lorsque vous avez besoin d’ID de hello toofind d’un script pour les opérations de promotion ou la rétrogradation.</span><span class="sxs-lookup"><span data-stu-id="7ea15-159">hello history is useful when you need toofind hello ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ea15-160">Il n’existe aucun tooundo de façon automatique hello les modifications apportées par une action de script.</span><span class="sxs-lookup"><span data-stu-id="7ea15-160">There is no automatic way tooundo hello changes made by a script action.</span></span> <span data-ttu-id="7ea15-161">Hello annuler manuellement ou fournir un script qui les inverse.</span><span class="sxs-lookup"><span data-stu-id="7ea15-161">Either manually reverse hello changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="7ea15-162">Action de script dans le processus de création de cluster hello</span><span class="sxs-lookup"><span data-stu-id="7ea15-162">Script Action in hello cluster creation process</span></span>

<span data-ttu-id="7ea15-163">Les actions de script utilisées lors de la création du cluster sont légèrement différentes des actions de script exécutées sur un cluster existant :</span><span class="sxs-lookup"><span data-stu-id="7ea15-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="7ea15-164">script de Hello est **automatiquement persistantes**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-164">hello script is **automatically persisted**.</span></span>
* <span data-ttu-id="7ea15-165">A **échec** Bonjour script peut entraîner des toofail de processus de création de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-165">A **failure** in hello script can cause hello cluster creation process toofail.</span></span>

<span data-ttu-id="7ea15-166">Hello diagramme ci-dessous illustre lors de l’Action de Script est exécutée pendant le processus de création de hello :</span><span class="sxs-lookup"><span data-stu-id="7ea15-166">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="7ea15-167">![Personnalisation du cluster HDInsight et procédure de création d’un cluster][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="7ea15-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="7ea15-168">script de Hello s’exécute pendant la configuration de HDInsight est en cours.</span><span class="sxs-lookup"><span data-stu-id="7ea15-168">hello script runs while HDInsight is being configured.</span></span> <span data-ttu-id="7ea15-169">À ce stade, hello s’exécute le script en parallèle sur tous les hello nœuds spécifiés dans le cluster de hello et s’exécute avec des privilèges racine sur les nœuds hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-169">At this stage, hello script runs in parallel on all hello specified nodes in hello cluster, and runs with root privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="7ea15-170">Étant donné que le script de hello s’exécute avec des privilèges de niveau racine sur les nœuds de cluster hello, vous pouvez effectuer des opérations telles que l’arrêt et démarrage des services, y compris les services liés à Hadoop.</span><span class="sxs-lookup"><span data-stu-id="7ea15-170">Because hello script runs with root level privilege on hello cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="7ea15-171">Si vous arrêtez les services, vous devez vous assurer que service de Ambari hello et autres services Hadoop sont en cours d’exécution avant la fin de script de hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="7ea15-171">If you stop services, you must ensure that hello Ambari service and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="7ea15-172">Ces services sont requis toosuccessfully déterminer l’intégrité de hello et l’état du cluster de hello lors de sa création.</span><span class="sxs-lookup"><span data-stu-id="7ea15-172">These services are required toosuccessfully determine hello health and state of hello cluster while it is being created.</span></span>


<span data-ttu-id="7ea15-173">Lors de la création du cluster, vous pouvez utiliser plusieurs actions de script à la fois.</span><span class="sxs-lookup"><span data-stu-id="7ea15-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="7ea15-174">Ces scripts sont appelés dans l’ordre de hello dans lequel elles ont été spécifiées.</span><span class="sxs-lookup"><span data-stu-id="7ea15-174">These scripts are invoked in hello order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ea15-175">Les actions de script doivent se terminer dans les 60 minutes, faute de quoi elles expirent.</span><span class="sxs-lookup"><span data-stu-id="7ea15-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="7ea15-176">Lors de la configuration de cluster, script de hello s’exécute en même temps que d’autres processus d’installation et la configuration.</span><span class="sxs-lookup"><span data-stu-id="7ea15-176">During cluster provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="7ea15-177">Concurrence pour les ressources, telles que la bande passante du réseau ou de temps processeur peut entraîner hello script tootake plu toofinish qu’il ne le fait dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="7ea15-177">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>
>
> <span data-ttu-id="7ea15-178">toominimize hello fois qu’il prend toorun hello script, évitez de tâches, telles que le téléchargement et la compilation d’applications à partir de la source.</span><span class="sxs-lookup"><span data-stu-id="7ea15-178">toominimize hello time it takes toorun hello script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="7ea15-179">Précompiler des applications et stocker les binaires hello dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-179">Pre-compile applications and store hello binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="7ea15-180">Action de script sur un cluster en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="7ea15-180">Script action on a running cluster</span></span>

<span data-ttu-id="7ea15-181">Contrairement aux actions utilisées lors de la création du cluster, une défaillance dans un script exécutées sur un cluster déjà en cours d’exécution de script ne provoque pas automatiquement l’état hello cluster toochange tooa a échoué.</span><span class="sxs-lookup"><span data-stu-id="7ea15-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause hello cluster toochange tooa failed state.</span></span> <span data-ttu-id="7ea15-182">Une fois qu’un script s’achève, cluster de hello doit retourner tooa « running » l’état.</span><span class="sxs-lookup"><span data-stu-id="7ea15-182">Once a script completes, hello cluster should return tooa "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ea15-183">Même si le cluster de hello a un état « en cours d’exécution », hello script ayant échoué peut-être rompu choses.</span><span class="sxs-lookup"><span data-stu-id="7ea15-183">Even if hello cluster has a 'running' state, hello failed script may have broken things.</span></span> <span data-ttu-id="7ea15-184">Par exemple, un script peut supprimer les fichiers requis par le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-184">For example, a script could delete files needed by hello cluster.</span></span>
>
> <span data-ttu-id="7ea15-185">Les actions de scripts s’exécutent avec des privilèges racine, donc vous devez vous assurer que vous comprenez ce que fait par un script avant de l’appliquer tooyour cluster.</span><span class="sxs-lookup"><span data-stu-id="7ea15-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it tooyour cluster.</span></span>

<span data-ttu-id="7ea15-186">Lorsque vous appliquez un cluster tooa de script, état du cluster hello change toofrom **en cours d’exécution** trop**accepté**, puis **configuration HDInsight**et enfin trop**En cours d’exécution** pour les scripts réussies.</span><span class="sxs-lookup"><span data-stu-id="7ea15-186">When applying a script tooa cluster, hello cluster state changes toofrom **Running** too**Accepted**, then **HDInsight configuration**, and finally back too**Running** for successful scripts.</span></span> <span data-ttu-id="7ea15-187">statut du script Hello est enregistré dans l’historique des actions de script hello, et vous pouvez utiliser cette toodetermine informations si le script de hello a réussi ou échoué.</span><span class="sxs-lookup"><span data-stu-id="7ea15-187">hello script status is logged in hello script action history, and you can use this information toodetermine whether hello script succeeded or failed.</span></span> <span data-ttu-id="7ea15-188">Par exemple, hello `Get-AzureRmHDInsightScriptActionHistory` applet de commande PowerShell peut être l’état de hello tooview utilisé d’un script.</span><span class="sxs-lookup"><span data-stu-id="7ea15-188">For example, hello `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used tooview hello status of a script.</span></span> <span data-ttu-id="7ea15-189">Il retourne toohello similaire à informations suivant le texte :</span><span class="sxs-lookup"><span data-stu-id="7ea15-189">It returns information similar toohello following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="7ea15-190">Si vous avez modifié le mot de passe utilisateur (admin) hello cluster après la création de cluster de hello, actions exécutées sur ce cluster peut échouer.</span><span class="sxs-lookup"><span data-stu-id="7ea15-190">If you have changed hello cluster user (admin) password after hello cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="7ea15-191">Si vous disposez de toutes les actions de script persistantes que de nœuds de travail cible, ces scripts peuvent échouer lorsque vous mettez à l’échelle de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale hello cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="7ea15-192">Exemple de script d’action de script</span><span class="sxs-lookup"><span data-stu-id="7ea15-192">Example Script Action scripts</span></span>

<span data-ttu-id="7ea15-193">Scripts d’Action de script peuvent être utilisés par le biais hello suivant utilitaires :</span><span class="sxs-lookup"><span data-stu-id="7ea15-193">Script Action scripts can be used through hello following utilities:</span></span>

* <span data-ttu-id="7ea15-194">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="7ea15-194">Azure portal</span></span>
* <span data-ttu-id="7ea15-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ea15-195">Azure PowerShell</span></span>
* <span data-ttu-id="7ea15-196">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="7ea15-196">Azure CLI</span></span>
* <span data-ttu-id="7ea15-197">Kit de développement logiciel (SDK) .NET de HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ea15-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="7ea15-198">HDInsight fournit hello tooinstall de scripts suivant des composants de clusters HDInsight :</span><span class="sxs-lookup"><span data-stu-id="7ea15-198">HDInsight provides scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="7ea15-199">Nom</span><span class="sxs-lookup"><span data-stu-id="7ea15-199">Name</span></span> | <span data-ttu-id="7ea15-200">Script</span><span class="sxs-lookup"><span data-stu-id="7ea15-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="7ea15-201">**Ajouter un compte Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="7ea15-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="7ea15-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. Consultez [ajouter un stockage supplémentaire tooan HDInsight cluster](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage tooan HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="7ea15-203">**Installez Hue.**</span><span class="sxs-lookup"><span data-stu-id="7ea15-203">**Install Hue**</span></span> |<span data-ttu-id="7ea15-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. Consultez [Installer et utiliser Hue sur les clusters HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="7ea15-205">**Installer Presto**</span><span class="sxs-lookup"><span data-stu-id="7ea15-205">**Install Presto**</span></span> |<span data-ttu-id="7ea15-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. Consultez la rubrique [Installer et utiliser Presto sur des clusters HDInsight](hdinsight-hadoop-install-presto.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="7ea15-207">**Installation de Solr**</span><span class="sxs-lookup"><span data-stu-id="7ea15-207">**Install Solr**</span></span> |<span data-ttu-id="7ea15-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. Consultez [Installer et utiliser Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="7ea15-209">**Installation de Giraph**</span><span class="sxs-lookup"><span data-stu-id="7ea15-209">**Install Giraph**</span></span> |<span data-ttu-id="7ea15-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Consultez [Installer et utiliser Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="7ea15-211">**Précharger les bibliothèques Hive**</span><span class="sxs-lookup"><span data-stu-id="7ea15-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="7ea15-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. Consultez [Ajouter des bibliothèques Hive sur des clusters HDInsight](hdinsight-hadoop-add-hive-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="7ea15-213">**Installer ou mettre à jour Mono**</span><span class="sxs-lookup"><span data-stu-id="7ea15-213">**Install or update Mono**</span></span> | <span data-ttu-id="7ea15-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span><span class="sxs-lookup"><span data-stu-id="7ea15-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="7ea15-215">Consultez [Installer ou mettre à jour Mono sur HDInsight](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="7ea15-216">Utiliser une action de script lors de la création du cluster</span><span class="sxs-lookup"><span data-stu-id="7ea15-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="7ea15-217">Cette section fournit des exemples sur hello différentes utilisations des actions de script lors de la création d’un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ea15-217">This section provides examples on hello different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a><span data-ttu-id="7ea15-218">Utiliser une Action de Script lors de la création du cluster à partir de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7ea15-218">Use a Script Action during cluster creation from hello Azure portal</span></span>

1. <span data-ttu-id="7ea15-219">Démarrez la création d'un cluster comme décrit dans [Création de clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="7ea15-220">Arrêtez quand vous atteignez hello __résumé du Cluster__ section.</span><span class="sxs-lookup"><span data-stu-id="7ea15-220">Stop when you reach hello __Cluster summary__ section.</span></span>

2. <span data-ttu-id="7ea15-221">À partir de hello __résumé du Cluster__ section, sélectionnez hello __modifier__ de liens pour __paramètres avancés__.</span><span class="sxs-lookup"><span data-stu-id="7ea15-221">From hello __Cluster summary__ section, select hello __edit__ link for __Advanced settings__.</span></span>

    ![Lien des Paramètres avancés](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="7ea15-223">À partir de hello __paramètres avancés__ section, sélectionnez __actions de Script__.</span><span class="sxs-lookup"><span data-stu-id="7ea15-223">From hello __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="7ea15-224">À partir de hello __actions de Script__ section, sélectionnez __+ soumettre à nouveau__</span><span class="sxs-lookup"><span data-stu-id="7ea15-224">From hello __Script actions__ section, select __+ Submit new__</span></span>

    ![Soumettre une nouvelle action de script](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="7ea15-226">Hello d’utilisation __sélectionner un script__ entrée tooselect un script existant.</span><span class="sxs-lookup"><span data-stu-id="7ea15-226">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="7ea15-227">toouse un script personnalisé, sélectionnez __personnalisé__ , puis indiquez hello __nom__ et __Bash URI de script__ pour votre script.</span><span class="sxs-lookup"><span data-stu-id="7ea15-227">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Ajouter un script hello sélectionnez sous forme de script](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="7ea15-229">Hello tableau suivant décrit les éléments de hello sur le formulaire de hello :</span><span class="sxs-lookup"><span data-stu-id="7ea15-229">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="7ea15-230">Propriété</span><span class="sxs-lookup"><span data-stu-id="7ea15-230">Property</span></span> | <span data-ttu-id="7ea15-231">Valeur</span><span class="sxs-lookup"><span data-stu-id="7ea15-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="7ea15-232">Sélectionner un script</span><span class="sxs-lookup"><span data-stu-id="7ea15-232">Select a script</span></span> | <span data-ttu-id="7ea15-233">toouse votre propre script, sélectionnez __personnalisé__.</span><span class="sxs-lookup"><span data-stu-id="7ea15-233">toouse your own script, select __Custom__.</span></span> <span data-ttu-id="7ea15-234">Sinon, sélectionnez un des scripts de hello fourni.</span><span class="sxs-lookup"><span data-stu-id="7ea15-234">Otherwise, select one of hello provided scripts.</span></span> |
    | <span data-ttu-id="7ea15-235">Nom</span><span class="sxs-lookup"><span data-stu-id="7ea15-235">Name</span></span> |<span data-ttu-id="7ea15-236">Spécifiez un nom pour l’action de script hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-236">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="7ea15-237">URI de script bash</span><span class="sxs-lookup"><span data-stu-id="7ea15-237">Bash script URI</span></span> |<span data-ttu-id="7ea15-238">Spécifiez hello URI toohello script qui est appelée toocustomize hello cluster.</span><span class="sxs-lookup"><span data-stu-id="7ea15-238">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="7ea15-239">Principal/Employé/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="7ea15-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="7ea15-240">Spécifier les nœuds hello (**Head**, **travail**, ou **soigneur**) sur la personnalisation hello script est exécuté.</span><span class="sxs-lookup"><span data-stu-id="7ea15-240">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="7ea15-241">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7ea15-241">Parameters</span></span> |<span data-ttu-id="7ea15-242">Spécifiez des paramètres de hello, si requis par le script de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-242">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="7ea15-243">Hello d’utilisation __conserver cette action de script__ tooensure d’entrée qui hello script est appliqué pendant les opérations de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="7ea15-243">Use hello __Persist this script action__ entry tooensure that hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="7ea15-244">Sélectionnez __créer__ script de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="7ea15-244">Select __Create__ toosave hello script.</span></span> <span data-ttu-id="7ea15-245">Vous pouvez ensuite utiliser __+ soumettre de nouvelles__ tooadd un autre script.</span><span class="sxs-lookup"><span data-stu-id="7ea15-245">You can then use __+ Submit new__ tooadd another script.</span></span>

    ![Plusieurs actions de script](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="7ea15-247">Lorsque vous avez terminé l’ajout de scripts, utilisez hello __sélectionnez__ bouton et puis hello __suivant__ bouton tooreturn toohello __résumé du Cluster__ section.</span><span class="sxs-lookup"><span data-stu-id="7ea15-247">When you are done adding scripts, use hello __Select__ button, and then hello __Next__ button tooreturn toohello __Cluster summary__ section.</span></span>

3. <span data-ttu-id="7ea15-248">cluster de hello toocreate, sélectionnez __créer__ de hello __résumé du Cluster__ sélection.</span><span class="sxs-lookup"><span data-stu-id="7ea15-248">toocreate hello cluster, select __Create__ from hello __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="7ea15-249">Utilisez une action de Script à partir de modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7ea15-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="7ea15-250">exemples de Hello dans cette section montrent comment toouse script actions avec les modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7ea15-250">hello examples in this section demonstrate how toouse script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="7ea15-251">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="7ea15-251">Before you begin</span></span>

* <span data-ttu-id="7ea15-252">Pour plus d’informations sur la configuration d’une station de travail de toorun applets de commande HDInsight Powershell, consultez [installer et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7ea15-252">For information about configuring a workstation toorun HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="7ea15-253">Pour obtenir des instructions sur la façon de toocreate modèles, consultez [les modèles de programmation Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-253">For instructions on how toocreate templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="7ea15-254">Si vous n’avez pas déjà utilisé Azure PowerShell avec Resource Manager, consultez [Utilisation d’Azure PowerShell avec Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="7ea15-255">Création de clusters à l’aide d’une action de script</span><span class="sxs-lookup"><span data-stu-id="7ea15-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="7ea15-256">Copiez hello suivant l’emplacement du modèle tooa sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7ea15-256">Copy hello following template tooa location on your computer.</span></span> <span data-ttu-id="7ea15-257">Ce modèle installe Giraph sur les nœuds de hello headnodes et de travail dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-257">This template installs Giraph on hello headnodes and worker nodes in hello cluster.</span></span> <span data-ttu-id="7ea15-258">Vous pouvez également vérifier si le modèle de hello JSON est valide.</span><span class="sxs-lookup"><span data-stu-id="7ea15-258">You can also verify if hello JSON template is valid.</span></span> <span data-ttu-id="7ea15-259">Collez le contenu de votre modèle dans [JSONLint](http://jsonlint.com/), un outil de validation JSON en ligne.</span><span class="sxs-lookup"><span data-stu-id="7ea15-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. <span data-ttu-id="7ea15-260">Démarrer PowerShell d’Azure et connectez-vous tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-260">Start Azure PowerShell and Log in tooyour Azure account.</span></span> <span data-ttu-id="7ea15-261">Après avoir entré vos informations d’identification, commande hello retourne des informations relatives à votre compte.</span><span class="sxs-lookup"><span data-stu-id="7ea15-261">After providing your credentials, hello command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="7ea15-262">Si vous avez plusieurs abonnements, indiquez l’ID d’abonnement hello vous souhaitez toouse pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="7ea15-262">If you have multiple subscriptions, provide hello subscription ID you wish toouse for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="7ea15-263">Vous pouvez utiliser `Get-AzureRmSubscription` tooget une liste de tous les abonnements associés à votre compte, ce qui inclut l’ID d’abonnement hello pour chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="7ea15-263">You can use `Get-AzureRmSubscription` tooget a list of all subscriptions associated with your account, which includes hello subscription ID for each one.</span></span>

4. <span data-ttu-id="7ea15-264">Si vous n’avez pas de groupe de ressources, créez-en un.</span><span class="sxs-lookup"><span data-stu-id="7ea15-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="7ea15-265">Fournir le nom hello du groupe de ressources hello et l’emplacement que vous avez besoin pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="7ea15-265">Provide hello name of hello resource group and location that you need for your solution.</span></span> <span data-ttu-id="7ea15-266">Un résumé du nouveau groupe de ressources hello est retourné.</span><span class="sxs-lookup"><span data-stu-id="7ea15-266">A summary of hello new resource group is returned.</span></span>

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. <span data-ttu-id="7ea15-267">toocreate de déploiement de votre groupe de ressources, exécutez hello **New-AzureRmResourceGroupDeployment** de commandes et de fournir les paramètres nécessaires hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-267">toocreate a deployment for your resource group, run hello **New-AzureRmResourceGroupDeployment** command and provide hello necessary parameters.</span></span> <span data-ttu-id="7ea15-268">les paramètres de Hello incluent hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="7ea15-268">hello parameters include hello following data:</span></span>

    * <span data-ttu-id="7ea15-269">un nom pour votre déploiement ;</span><span class="sxs-lookup"><span data-stu-id="7ea15-269">A name for your deployment</span></span>
    * <span data-ttu-id="7ea15-270">nom de Hello de votre groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="7ea15-270">hello name of your resource group</span></span>
    * <span data-ttu-id="7ea15-271">chemin d’accès Hello ou modèle d’URL toohello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="7ea15-271">hello path or URL toohello template you created.</span></span>

  <span data-ttu-id="7ea15-272">Si votre modèle requiert n’importe quel paramètre, vous devez également transférer les paramètres.</span><span class="sxs-lookup"><span data-stu-id="7ea15-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="7ea15-273">Dans ce cas, hello script action tooinstall R sur le cluster de hello ne nécessite pas de paramètres de.</span><span class="sxs-lookup"><span data-stu-id="7ea15-273">In this case, hello script action tooinstall R on hello cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="7ea15-274">Vous n’êtes tooprovide invité à des valeurs pour les paramètres de hello définis dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-274">You are prompted tooprovide values for hello parameters defined in hello template.</span></span>

1. <span data-ttu-id="7ea15-275">Lorsque le groupe de ressources hello a été déployé, un résumé du déploiement de hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7ea15-275">When hello resource group has been deployed, a summary of hello deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="7ea15-276">Si votre déploiement échoue, vous pouvez utiliser hello suivant d’applets de commande tooget plus d’informations sur les échecs de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-276">If your deployment fails, you can use hello following cmdlets tooget information about hello failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="7ea15-277">Utiliser une action de script lors de la création du cluster à partir d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ea15-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="7ea15-278">Dans cette section, nous utilisons hello [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) scripts de tooinvoke d’applet de commande en utilisant l’Action de Script toocustomize un cluster.</span><span class="sxs-lookup"><span data-stu-id="7ea15-278">In this section, we use hello [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts by using Script Action toocustomize a cluster.</span></span> <span data-ttu-id="7ea15-279">Avant de poursuivre, assurez-vous que vous avez installé et configuré Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ea15-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="7ea15-280">Pour plus d’informations sur la configuration d’une station de travail de toorun applets de commande HDInsight PowerShell, consultez [installer et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7ea15-280">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="7ea15-281">Hello de script suivant montre comment tooapply une action de script lors de la création d’un cluster à l’aide de PowerShell :</span><span class="sxs-lookup"><span data-stu-id="7ea15-281">hello following script demonstrates how tooapply a script action when creating a cluster using PowerShell:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

<span data-ttu-id="7ea15-282">Il peut prendre plusieurs minutes avant que le cluster de hello est créé.</span><span class="sxs-lookup"><span data-stu-id="7ea15-282">It can take several minutes before hello cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="7ea15-283">Utiliser une Action de Script lors de la création du cluster à partir de hello HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7ea15-283">Use a Script Action during cluster creation from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="7ea15-284">Hello HDInsight .NET SDK fournit des bibliothèques clientes qui rend plus facile toowork avec HDInsight à partir d’une application .NET.</span><span class="sxs-lookup"><span data-stu-id="7ea15-284">hello HDInsight .NET SDK provides client libraries that makes it easier toowork with HDInsight from a .NET application.</span></span> <span data-ttu-id="7ea15-285">Pour un exemple de code, consultez [basés sur Linux de créer des clusters HDInsight à l’aide hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="7ea15-285">For a code sample, see [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-tooa-running-cluster"></a><span data-ttu-id="7ea15-286">Appliquer un tooa d’Action de Script en cours d’exécution cluster</span><span class="sxs-lookup"><span data-stu-id="7ea15-286">Apply a Script Action tooa running cluster</span></span>

<span data-ttu-id="7ea15-287">Dans cette section, découvrez comment tooapply script tooa actions cluster en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="7ea15-287">In this section, learn how tooapply script actions tooa running cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a><span data-ttu-id="7ea15-288">Appliquer un tooa d’Action de Script en cours d’exécution cluster à partir de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7ea15-288">Apply a Script Action tooa running cluster from hello Azure portal</span></span>

1. <span data-ttu-id="7ea15-289">À partir de hello [portail Azure](https://portal.azure.com), sélectionnez votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ea15-289">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="7ea15-290">Dans la vue d’ensemble du cluster HDInsight hello, sélectionnez hello **Actions de Script** vignette.</span><span class="sxs-lookup"><span data-stu-id="7ea15-290">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Vignette Actions de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="7ea15-292">Vous pouvez également sélectionner **tous les paramètres** , puis sélectionnez **Actions de Script** de hello section de paramètres.</span><span class="sxs-lookup"><span data-stu-id="7ea15-292">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

3. <span data-ttu-id="7ea15-293">À partir du haut hello Hello section Actions de Script, sélectionnez **envoyer nouveau**.</span><span class="sxs-lookup"><span data-stu-id="7ea15-293">From hello top of hello Script Actions section, select **Submit new**.</span></span>

    ![Ajouter un tooa script cluster en cours d’exécution](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="7ea15-295">Hello d’utilisation __sélectionner un script__ entrée tooselect un script existant.</span><span class="sxs-lookup"><span data-stu-id="7ea15-295">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="7ea15-296">toouse un script personnalisé, sélectionnez __personnalisé__ , puis indiquez hello __nom__ et __Bash URI de script__ pour votre script.</span><span class="sxs-lookup"><span data-stu-id="7ea15-296">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Ajouter un script hello sélectionnez sous forme de script](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="7ea15-298">Hello tableau suivant décrit les éléments de hello sur le formulaire de hello :</span><span class="sxs-lookup"><span data-stu-id="7ea15-298">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="7ea15-299">Propriété</span><span class="sxs-lookup"><span data-stu-id="7ea15-299">Property</span></span> | <span data-ttu-id="7ea15-300">Valeur</span><span class="sxs-lookup"><span data-stu-id="7ea15-300">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="7ea15-301">Sélectionner un script</span><span class="sxs-lookup"><span data-stu-id="7ea15-301">Select a script</span></span> | <span data-ttu-id="7ea15-302">toouse votre propre script, sélectionnez __personnalisé__.</span><span class="sxs-lookup"><span data-stu-id="7ea15-302">toouse your own script, select __custom__.</span></span> <span data-ttu-id="7ea15-303">Sinon, sélectionnez un script fourni.</span><span class="sxs-lookup"><span data-stu-id="7ea15-303">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="7ea15-304">Nom</span><span class="sxs-lookup"><span data-stu-id="7ea15-304">Name</span></span> |<span data-ttu-id="7ea15-305">Spécifiez un nom pour l’action de script hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-305">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="7ea15-306">URI de script bash</span><span class="sxs-lookup"><span data-stu-id="7ea15-306">Bash script URI</span></span> |<span data-ttu-id="7ea15-307">Spécifiez hello URI toohello script qui est appelée toocustomize hello cluster.</span><span class="sxs-lookup"><span data-stu-id="7ea15-307">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="7ea15-308">Principal/Employé/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="7ea15-308">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="7ea15-309">Spécifier les nœuds hello (**Head**, **travail**, ou **soigneur**) sur la personnalisation hello script est exécuté.</span><span class="sxs-lookup"><span data-stu-id="7ea15-309">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="7ea15-310">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7ea15-310">Parameters</span></span> |<span data-ttu-id="7ea15-311">Spécifiez des paramètres de hello, si requis par le script de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-311">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="7ea15-312">Hello d’utilisation __conserver cette action de script__ script d’entrée toomake vraiment hello est appliqué pendant les opérations de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="7ea15-312">Use hello __Persist this script action__ entry toomake sure hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="7ea15-313">Enfin, utilisez hello **créer** le cluster toohello script bouton tooapply hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-313">Finally, use hello **Create** button tooapply hello script toohello cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a><span data-ttu-id="7ea15-314">Appliquer un tooa d’Action de Script en cours d’exécution cluster à partir d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ea15-314">Apply a Script Action tooa running cluster from Azure PowerShell</span></span>

<span data-ttu-id="7ea15-315">Avant de poursuivre, assurez-vous que vous avez installé et configuré Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ea15-315">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="7ea15-316">Pour plus d’informations sur la configuration d’une station de travail de toorun applets de commande HDInsight PowerShell, consultez [installer et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7ea15-316">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="7ea15-317">Hello exemple suivant montre comment tooapply un cluster en cours d’exécution de script action tooa :</span><span class="sxs-lookup"><span data-stu-id="7ea15-317">hello following example demonstrates how tooapply a script action tooa running cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

<span data-ttu-id="7ea15-318">Une fois que hello terminée, vous recevez toohello similaire à informations suivant le texte :</span><span class="sxs-lookup"><span data-stu-id="7ea15-318">Once hello operation completes, you receive information similar toohello following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a><span data-ttu-id="7ea15-319">Appliquer un tooa d’Action de Script en cours d’exécution cluster à partir de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="7ea15-319">Apply a Script Action tooa running cluster from hello Azure CLI</span></span>

<span data-ttu-id="7ea15-320">Avant de continuer, assurez-vous que vous avez installé et configuré hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-320">Before proceeding, make sure you have installed and configured hello Azure CLI.</span></span> <span data-ttu-id="7ea15-321">Pour plus d’informations, consultez [installation Bonjour Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-321">For more information, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="7ea15-322">tooswitch tooAzure mode du Gestionnaire de ressources, utilisez hello commande à la ligne de commande hello suivante :</span><span class="sxs-lookup"><span data-stu-id="7ea15-322">tooswitch tooAzure Resource Manager mode, use hello following command at hello command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="7ea15-323">Utilisez hello suivant tooauthenticate tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea15-323">Use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="7ea15-324">Utilisez hello suivant commande tooapply un tooa d’action de script en cours d’exécution cluster</span><span class="sxs-lookup"><span data-stu-id="7ea15-324">Use hello following command tooapply a script action tooa running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="7ea15-325">Si vous omettez les paramètres de cette commande, vous êtes invité à les saisir.</span><span class="sxs-lookup"><span data-stu-id="7ea15-325">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="7ea15-326">Si hello script que vous spécifiez avec `-u` accepte des paramètres, vous pouvez spécifier les à l’aide de hello `-p` paramètre.</span><span class="sxs-lookup"><span data-stu-id="7ea15-326">If hello script you specify with `-u` accepts parameters, you can specify them using hello `-p` parameter.</span></span>

    <span data-ttu-id="7ea15-327">Les types de nœud valides sont `headnode`, `workernode` et `zookeeper`.</span><span class="sxs-lookup"><span data-stu-id="7ea15-327">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="7ea15-328">Si le script de hello doit être appliqué toomultiple les types de nœuds, spécifiez les types de hello séparés par un ';'.</span><span class="sxs-lookup"><span data-stu-id="7ea15-328">If hello script should be applied toomultiple node types, specify hello types separated by a ';'.</span></span> <span data-ttu-id="7ea15-329">Par exemple, `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="7ea15-329">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="7ea15-330">toopersist hello script, ajoutez hello `--persistOnSuccess`.</span><span class="sxs-lookup"><span data-stu-id="7ea15-330">toopersist hello script, add hello `--persistOnSuccess`.</span></span> <span data-ttu-id="7ea15-331">Vous pouvez également rendre persistantes les script hello ultérieurement à l’aide de `azure hdinsight script-action persisted set`.</span><span class="sxs-lookup"><span data-stu-id="7ea15-331">You can also persist hello script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="7ea15-332">Une fois que hello est terminée, vous recevez toohello similaire de sortie suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="7ea15-332">Once hello job completes, you receive output similar toohello following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a><span data-ttu-id="7ea15-333">Appliquer un tooa d’Action de Script en cours d’exécution à l’aide des API REST de cluster</span><span class="sxs-lookup"><span data-stu-id="7ea15-333">Apply a Script Action tooa running cluster using REST API</span></span>

<span data-ttu-id="7ea15-334">Consultez [Exécuter des actions de script sur un cluster en cours d’exécution](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ea15-334">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="7ea15-335">Appliquer un tooa d’Action de Script en cours d’exécution cluster à partir de hello HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7ea15-335">Apply a Script Action tooa running cluster from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="7ea15-336">Pour obtenir un exemple d’utilisation de cluster de tooa hello .NET SDK tooapply des scripts, consultez [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="7ea15-336">For an example of using hello .NET SDK tooapply scripts tooa cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="7ea15-337">Afficher l’historique, promouvoir et abaisser des actions de script</span><span class="sxs-lookup"><span data-stu-id="7ea15-337">View history, promote, and demote Script Actions</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="7ea15-338">À l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7ea15-338">Using hello Azure portal</span></span>

1. <span data-ttu-id="7ea15-339">À partir de hello [portail Azure](https://portal.azure.com), sélectionnez votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ea15-339">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="7ea15-340">Dans la vue d’ensemble du cluster HDInsight hello, sélectionnez hello **Actions de Script** vignette.</span><span class="sxs-lookup"><span data-stu-id="7ea15-340">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Vignette Actions de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="7ea15-342">Vous pouvez également sélectionner **tous les paramètres** , puis sélectionnez **Actions de Script** de hello section de paramètres.</span><span class="sxs-lookup"><span data-stu-id="7ea15-342">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

4. <span data-ttu-id="7ea15-343">Un historique des scripts pour ce cluster s’affiche sur hello section Actions de Script.</span><span class="sxs-lookup"><span data-stu-id="7ea15-343">A history of scripts for this cluster is displayed on hello Script Actions section.</span></span> <span data-ttu-id="7ea15-344">Ces informations comprennent une liste de scripts persistants.</span><span class="sxs-lookup"><span data-stu-id="7ea15-344">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="7ea15-345">Dans la capture d’écran de hello ci-dessous, vous pouvez voir que hello Solr script a été exécuté sur ce cluster.</span><span class="sxs-lookup"><span data-stu-id="7ea15-345">In hello screenshot below, you can see that hello Solr script has been ran on this cluster.</span></span> <span data-ttu-id="7ea15-346">capture d’écran de Hello n’affiche pas tous les scripts persistantes.</span><span class="sxs-lookup"><span data-stu-id="7ea15-346">hello screenshot does not show any persisted scripts.</span></span>

    ![Section Actions de script](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="7ea15-348">Sélection d’un script à partir de l’historique de hello affiche la section des propriétés hello pour ce script.</span><span class="sxs-lookup"><span data-stu-id="7ea15-348">Selecting a script from hello history displays hello Properties section for this script.</span></span> <span data-ttu-id="7ea15-349">À partir du haut hello d’écran hello, vous pouvez réexécuter le script de hello ou promouvoir en tant que.</span><span class="sxs-lookup"><span data-stu-id="7ea15-349">From hello top of hello screen, you can rerun hello script or promote it.</span></span>

    ![Propriétés des actions de script](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="7ea15-351">Vous pouvez également utiliser hello **...**  toohello à droite des entrées sur les actions de tooperform section hello Actions de Script.</span><span class="sxs-lookup"><span data-stu-id="7ea15-351">You can also use hello **...** toohello right of entries on hello Script Actions section tooperform actions.</span></span>

    ![Utilisation de … des actions de script](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="7ea15-353">Utilisation de Microsoft Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ea15-353">Using Azure PowerShell</span></span>

| <span data-ttu-id="7ea15-354">Utilisez les éléments suivants de hello...</span><span class="sxs-lookup"><span data-stu-id="7ea15-354">Use hello following...</span></span> | <span data-ttu-id="7ea15-355">trop...</span><span class="sxs-lookup"><span data-stu-id="7ea15-355">too...</span></span> |
| --- | --- |
| <span data-ttu-id="7ea15-356">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="7ea15-356">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="7ea15-357">Récupérer des informations sur les actions de script persistantes</span><span class="sxs-lookup"><span data-stu-id="7ea15-357">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="7ea15-358">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="7ea15-358">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="7ea15-359">Récupérer un historique de script actions appliquées toohello cluster ou les détails d’un script spécifique</span><span class="sxs-lookup"><span data-stu-id="7ea15-359">Retrieve a history of script actions applied toohello cluster, or details for a specific script</span></span> |
| <span data-ttu-id="7ea15-360">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="7ea15-360">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="7ea15-361">Promeut un ad hoc tooa d’action de script persistantes action de script</span><span class="sxs-lookup"><span data-stu-id="7ea15-361">Promotes an ad hoc script action tooa persisted script action</span></span> |
| <span data-ttu-id="7ea15-362">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="7ea15-362">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="7ea15-363">Rétrograde une action ad hoc de script persistantes action tooan</span><span class="sxs-lookup"><span data-stu-id="7ea15-363">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="7ea15-364">À l’aide de `Remove-AzureRmHDInsightPersistedScriptAction` n’annule pas les actions hello effectuées par un script.</span><span class="sxs-lookup"><span data-stu-id="7ea15-364">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="7ea15-365">Cette applet de commande supprime uniquement l’indicateur de rendu persistant hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-365">This cmdlet only removes hello persisted flag.</span></span>

<span data-ttu-id="7ea15-366">Hello, exemple de script suivant illustre l’utilisation de toopromote d’applets de commande hello, puis rétrograder un script.</span><span class="sxs-lookup"><span data-stu-id="7ea15-366">hello following example script demonstrates using hello cmdlets toopromote, then demote a script.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a><span data-ttu-id="7ea15-367">À l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="7ea15-367">Using hello Azure CLI</span></span>

| <span data-ttu-id="7ea15-368">Utilisez les éléments suivants de hello...</span><span class="sxs-lookup"><span data-stu-id="7ea15-368">Use hello following...</span></span> | <span data-ttu-id="7ea15-369">trop...</span><span class="sxs-lookup"><span data-stu-id="7ea15-369">too...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="7ea15-370">Récupérer une liste des actions de script persistantes</span><span class="sxs-lookup"><span data-stu-id="7ea15-370">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="7ea15-371">Récupérer des informations sur les actions de script persistantes</span><span class="sxs-lookup"><span data-stu-id="7ea15-371">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="7ea15-372">Récupérer un historique de script actions appliquées toohello cluster</span><span class="sxs-lookup"><span data-stu-id="7ea15-372">Retrieve a history of script actions applied toohello cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="7ea15-373">Récupérer des informations sur une action de script spécifique</span><span class="sxs-lookup"><span data-stu-id="7ea15-373">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="7ea15-374">Promeut un ad hoc tooa d’action de script persistantes action de script</span><span class="sxs-lookup"><span data-stu-id="7ea15-374">Promotes an ad hoc script action tooa persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="7ea15-375">Rétrograde une action ad hoc de script persistantes action tooan</span><span class="sxs-lookup"><span data-stu-id="7ea15-375">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="7ea15-376">À l’aide de `azure hdinsight script-action persisted delete` n’annule pas les actions hello effectuées par un script.</span><span class="sxs-lookup"><span data-stu-id="7ea15-376">Using `azure hdinsight script-action persisted delete` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="7ea15-377">Cette applet de commande supprime uniquement l’indicateur de rendu persistant hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-377">This cmdlet only removes hello persisted flag.</span></span>

### <a name="using-hello-hdinsight-net-sdk"></a><span data-ttu-id="7ea15-378">À l’aide de hello HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7ea15-378">Using hello HDInsight .NET SDK</span></span>

<span data-ttu-id="7ea15-379">Pour obtenir un exemple d’utilisation de l’historique de script tooretrieve hello .NET SDK à partir d’un cluster, vous devez promouvoir ou rétrograder des scripts, consultez [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="7ea15-379">For an example of using hello .NET SDK tooretrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="7ea15-380">Cet exemple montre également comment une application de HDInsight à l’aide de tooinstall hello du SDK .NET.</span><span class="sxs-lookup"><span data-stu-id="7ea15-380">This example also demonstrates how tooinstall an HDInsight application using hello .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="7ea15-381">Prise en charge des logiciels open source utilisés sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ea15-381">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="7ea15-382">Hello service Microsoft Azure HDInsight utilise un écosystème de technologies open source sur Hadoop.</span><span class="sxs-lookup"><span data-stu-id="7ea15-382">hello Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="7ea15-383">Microsoft Azure fournit un niveau général de prise en charge pour les technologies open source.</span><span class="sxs-lookup"><span data-stu-id="7ea15-383">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="7ea15-384">Pour plus d’informations, consultez hello **prise en charge étendue** section Hello [Azure prise en charge du site Web](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="7ea15-384">For more information, see hello **Support Scope** section of hello [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="7ea15-385">Hello service HDInsight fournit un niveau supplémentaire de prise en charge pour les composants intégrés.</span><span class="sxs-lookup"><span data-stu-id="7ea15-385">hello HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="7ea15-386">Il existe deux types de composants open source qui sont disponibles dans hello service HDInsight :</span><span class="sxs-lookup"><span data-stu-id="7ea15-386">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="7ea15-387">**Les composants intégrés** -ces composants sont déjà installés sur les clusters HDInsight et fournir des fonctionnalités principales du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-387">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="7ea15-388">Par exemple, fils ResourceManager, langage de requête Hive hello (HiveQL) et la bibliothèque de Mahout hello appartiennent toothis catégorie.</span><span class="sxs-lookup"><span data-stu-id="7ea15-388">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="7ea15-389">Une liste complète des composants de cluster est disponible dans [quelles sont les nouveautés dans les versions de cluster Hadoop hello fournies par HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-389">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="7ea15-390">**Les composants personnalisés** -vous, en tant qu’utilisateur de cluster de hello, pourrez installer ou utiliser dans votre charge de travail n’importe quel composant disponible dans la Communauté de hello ou créée par vous.</span><span class="sxs-lookup"><span data-stu-id="7ea15-390">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="7ea15-391">Composants fournis avec le cluster HDInsight de hello sont entièrement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7ea15-391">Components provided with hello HDInsight cluster are fully supported.</span></span> <span data-ttu-id="7ea15-392">Support technique de Microsoft vous aide à tooisolate et résoudre les problèmes connexes toothese composants.</span><span class="sxs-lookup"><span data-stu-id="7ea15-392">Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="7ea15-393">Les composants personnalisés de réception efforcera toohelp vous toofurther hello de dépannage.</span><span class="sxs-lookup"><span data-stu-id="7ea15-393">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="7ea15-394">Prise en charge Microsoft soit en mesure de tooresolve hello ou elles peuvent demander tooengage les canaux disponibles pour les technologies open source hello où se trouve une grande expérience pour laquelle la technologie.</span><span class="sxs-lookup"><span data-stu-id="7ea15-394">Microsoft support may be able tooresolve hello issue OR they may ask you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="7ea15-395">Vous pouvez, par exemple, utiliser de nombreux sites de communauté, comme le [forum MSDN sur HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). En outre, les projets Apache ont des sites de projet sur [http://apache.org](http://apache.org). Par exemple : [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="7ea15-395">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="7ea15-396">Hello service HDInsight propose plusieurs manières toouse des composants personnalisés.</span><span class="sxs-lookup"><span data-stu-id="7ea15-396">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="7ea15-397">Bonjour s’applique même au niveau de prise en charge, quelle que soit la façon dont un composant est utilisé ou installé sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-397">hello same level of support applies, regardless of how a component is used or installed on hello cluster.</span></span> <span data-ttu-id="7ea15-398">Hello liste suivante décrit les méthodes les plus courantes hello que les composants personnalisés peuvent être utilisés sur les clusters HDInsight :</span><span class="sxs-lookup"><span data-stu-id="7ea15-398">hello following list describes hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="7ea15-399">Envoi de travaux - Hadoop ou autres types de tâches qui s’exécutent, ou utilisent des composants personnalisés peut être soumis toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="7ea15-399">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>

2. <span data-ttu-id="7ea15-400">Personnalisation de cluster - lors de la création du cluster, vous pouvez spécifier des paramètres supplémentaires et des composants personnalisés qui sont installés sur les nœuds de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-400">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on hello cluster nodes.</span></span>

3. <span data-ttu-id="7ea15-401">Exemples - pour les composants personnalisés populaires, Microsoft et d’autres peuvent fournir des exemples de la façon dont ces composants peuvent être utilisés sur des clusters HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-401">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="7ea15-402">Ces exemples sont fournis sans support.</span><span class="sxs-lookup"><span data-stu-id="7ea15-402">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7ea15-403">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="7ea15-403">Troubleshooting</span></span>

<span data-ttu-id="7ea15-404">Vous pouvez utiliser Ambari web UI tooview les informations enregistrées par les actions de script.</span><span class="sxs-lookup"><span data-stu-id="7ea15-404">You can use Ambari web UI tooview information logged by script actions.</span></span> <span data-ttu-id="7ea15-405">Si le script de hello échoue pendant la création du cluster, hello journaux sont également disponibles dans le compte de stockage par défaut hello associé hello cluster.</span><span class="sxs-lookup"><span data-stu-id="7ea15-405">If hello script fails during cluster creation, hello logs are also available in hello default storage account associated with hello cluster.</span></span> <span data-ttu-id="7ea15-406">Cette section fournit des informations sur la façon dont tooretrieve hello connecte à l’aide de ces deux options.</span><span class="sxs-lookup"><span data-stu-id="7ea15-406">This section provides information on how tooretrieve hello logs using both these options.</span></span>

### <a name="using-hello-ambari-web-ui"></a><span data-ttu-id="7ea15-407">À l’aide de hello Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="7ea15-407">Using hello Ambari Web UI</span></span>

1. <span data-ttu-id="7ea15-408">Dans votre navigateur, accédez à toohttps://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="7ea15-408">In your browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="7ea15-409">Remplacez CLUSTERNAME par nom hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ea15-409">Replace CLUSTERNAME with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="7ea15-410">Lorsque vous y êtes invité, entrez le nom du compte administrateur hello (admin) et le mot de passe pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-410">When prompted, enter hello admin account name (admin) and password for hello cluster.</span></span> <span data-ttu-id="7ea15-411">Vous pouvez avoir des informations d’identification d’administrateur de hello tooreenter dans un formulaire web.</span><span class="sxs-lookup"><span data-stu-id="7ea15-411">You may have tooreenter hello admin credentials in a web form.</span></span>

2. <span data-ttu-id="7ea15-412">Dans la barre de hello en hello haut hello, sélectionnez hello **ops** entrée.</span><span class="sxs-lookup"><span data-stu-id="7ea15-412">From hello bar at hello top of hello page, select hello **ops** entry.</span></span> <span data-ttu-id="7ea15-413">Une liste des opérations actuelles et précédentes effectuées sur le cluster de hello via Ambari s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7ea15-413">A list of current and previous operations performed on hello cluster through Ambari is displayed.</span></span>

    ![Barre de l’interface utilisateur web Ambari avec ops sélectionné](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="7ea15-415">Rechercher des entrées hello ayant **exécuter\_customscriptaction** Bonjour **Operations** colonne.</span><span class="sxs-lookup"><span data-stu-id="7ea15-415">Find hello entries that have **run\_customscriptaction** in hello **Operations** column.</span></span> <span data-ttu-id="7ea15-416">Ces entrées sont créées lorsque vous exécutez des Actions de Script hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-416">These entries are created when hello Script Actions run.</span></span>

    ![Capture d’écran des opérations](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="7ea15-418">tooview hello STDOUT et la sortie STDERR, sélectionnez hello run\customscriptaction entrée et Explorer les liens de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-418">tooview hello STDOUT and STDERR output, select hello run\customscriptaction entry and drill down through hello links.</span></span> <span data-ttu-id="7ea15-419">Cette sortie est générée lorsque hello script s’exécute et peut contenir des informations utiles.</span><span class="sxs-lookup"><span data-stu-id="7ea15-419">This output is generated when hello script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-hello-default-storage-account"></a><span data-ttu-id="7ea15-420">Journaux d’accès de compte de stockage par défaut hello</span><span class="sxs-lookup"><span data-stu-id="7ea15-420">Access logs from hello default storage account</span></span>

<span data-ttu-id="7ea15-421">Si la création du cluster hello échoue en raison de l’erreur de script d’action de tooa, hello journaux accessibles à partir du compte de stockage de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-421">If hello cluster creation fails due tooa script action error, hello logs can be accessed from hello cluster storage account.</span></span>

* <span data-ttu-id="7ea15-422">Hello journaux de stockage sont disponibles dans `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span><span class="sxs-lookup"><span data-stu-id="7ea15-422">hello storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![Capture d’écran des opérations](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="7ea15-424">Sous ce répertoire, les journaux de hello sont organisés séparément pour le nœud principal et les nœuds soigneur workernode.</span><span class="sxs-lookup"><span data-stu-id="7ea15-424">Under this directory, hello logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="7ea15-425">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="7ea15-425">Some examples are:</span></span>

    * <span data-ttu-id="7ea15-426">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="7ea15-426">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="7ea15-427">**Nœud Worker** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="7ea15-427">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="7ea15-428">**Nœud Zookeeper** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="7ea15-428">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="7ea15-429">Tous les stdout et stderr d’hôte correspondant de hello est téléchargés du compte de stockage toohello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-429">All stdout and stderr of hello corresponding host is uploaded toohello storage account.</span></span> <span data-ttu-id="7ea15-430">Il existe un fichier **output-\*.txt** et un fichier **errors-\*.txt** pour chaque action de script.</span><span class="sxs-lookup"><span data-stu-id="7ea15-430">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="7ea15-431">fichier de sortie-*.txt Hello contient des informations sur hello URI de script de hello qui a été exécuté sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-431">hello output-*.txt file contains information about hello URI of hello script that got run on hello host.</span></span> <span data-ttu-id="7ea15-432">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="7ea15-432">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="7ea15-433">Il est possible que vous créez un cluster d’action de script à plusieurs reprises avec hello même nom.</span><span class="sxs-lookup"><span data-stu-id="7ea15-433">It's possible that you repeatedly create a script action cluster with hello same name.</span></span> <span data-ttu-id="7ea15-434">Dans ce cas, vous pouvez distinguer les journaux appropriés hello basés sur le nom du dossier DATE hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-434">In such case, you can distinguish hello relevant logs based on hello DATE folder name.</span></span> <span data-ttu-id="7ea15-435">Par exemple, structure de dossiers de hello pour un cluster (mycluster) créé à des dates différentes apparaît similaire toohello suivant des entrées de journal :</span><span class="sxs-lookup"><span data-stu-id="7ea15-435">For example, hello folder structure for a cluster (mycluster) created on different dates appears similar toohello following log entries:</span></span>

    <span data-ttu-id="7ea15-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04``\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="7ea15-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="7ea15-437">Si vous créez un cluster d’action de script avec hello même nom sur hello même jour, vous pouvez utiliser des fichiers journaux pertinents de hello préfixe unique tooidentify hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-437">If you create a script action cluster with hello same name on hello same day, you can use hello unique prefix tooidentify hello relevant log files.</span></span>

* <span data-ttu-id="7ea15-438">Si vous créez un cluster près de 12:00 (minuit), il est possible que les fichiers journaux hello s’étendre sur deux jours.</span><span class="sxs-lookup"><span data-stu-id="7ea15-438">If you create a cluster near 12:00AM (midnight), it's possible that hello log files span across two days.</span></span> <span data-ttu-id="7ea15-439">Dans ce cas, vous voyez deux dossiers de date différents pour hello même cluster.</span><span class="sxs-lookup"><span data-stu-id="7ea15-439">In such cases, you see two different date folders for hello same cluster.</span></span>

* <span data-ttu-id="7ea15-440">Conteneur par défaut de téléchargement journal fichiers toohello peut prendre jusqu'à minutes too5, en particulier pour les clusters de grande taille.</span><span class="sxs-lookup"><span data-stu-id="7ea15-440">Uploading log files toohello default container can take up too5 mins, especially for large clusters.</span></span> <span data-ttu-id="7ea15-441">Par conséquent, si vous souhaitez que les journaux tooaccess hello, vous ne devez pas immédiatement supprimer hello cluster si une action de script échoue.</span><span class="sxs-lookup"><span data-stu-id="7ea15-441">So, if you want tooaccess hello logs, you should not immediately delete hello cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="7ea15-442">Agent de surveillance Ambari</span><span class="sxs-lookup"><span data-stu-id="7ea15-442">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="7ea15-443">Ne modifiez pas le mot de passe hello hello Ambari surveillance (hdinsightwatchdog) sur votre cluster HDInsight de basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="7ea15-443">Do not change hello password for hello Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="7ea15-444">Un mot de passe de modification hello pour ce compte interrompt les actions de script nouveau hello capacité toorun sur cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-444">Changing hello password for this account breaks hello ability toorun new script actions on hello HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="7ea15-445">Impossible d’importer le nom BlobService</span><span class="sxs-lookup"><span data-stu-id="7ea15-445">Can't import name BlobService</span></span>

<span data-ttu-id="7ea15-446">__Symptômes__: hello action de script échoue.</span><span class="sxs-lookup"><span data-stu-id="7ea15-446">__Symptoms__: hello script action fails.</span></span> <span data-ttu-id="7ea15-447">Texte similaire toohello est l’erreur suivante s’affiche lorsque vous affichez les opération hello dans Ambari :</span><span class="sxs-lookup"><span data-stu-id="7ea15-447">Text similar toohello following error is displayed when you view hello operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="7ea15-448">__Cause__: cette erreur se produit si vous mettez à niveau le client de stockage Azure de Python hello qui est inclus dans le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="7ea15-448">__Cause__: This error occurs if you upgrade hello Python Azure Storage client that is included with hello HDInsight cluster.</span></span> <span data-ttu-id="7ea15-449">HDInsight attend le client de stockage Azure 0.20.0.</span><span class="sxs-lookup"><span data-stu-id="7ea15-449">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="7ea15-450">__Résolution__: tooresolve cette erreur, vous connecter manuellement à l’aide de nœud de cluster tooeach `ssh` et utilisez hello suivant la version du client de stockage correct commande tooreinstall hello :</span><span class="sxs-lookup"><span data-stu-id="7ea15-450">__Resolution__: tooresolve this error, manually connect tooeach cluster node using `ssh` and use hello following command tooreinstall hello correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="7ea15-451">Pour plus d’informations sur la connexion de cluster toohello avec SSH, consultez [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7ea15-451">For information on connecting toohello cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="7ea15-452">L’historique n’affiche pas les scripts utilisés lors de la création du cluster</span><span class="sxs-lookup"><span data-stu-id="7ea15-452">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="7ea15-453">Si votre cluster a été créé avant le 15 mars 2016, une entrée pourrait ne pas s’afficher dans l’historique des actions de script.</span><span class="sxs-lookup"><span data-stu-id="7ea15-453">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="7ea15-454">Si vous redimensionnez un cluster de hello après le 15 mars 2016, les scripts hello à l’aide lors de la création de cluster s’affiche dans l’historique lorsqu’ils sont appliqués toonew des nœuds dans le cluster hello dans le cadre de hello redimensionnement l’opération.</span><span class="sxs-lookup"><span data-stu-id="7ea15-454">If you resize hello cluster after March 15, 2016, hello scripts using during cluster creation appear in history as they are applied toonew nodes in hello cluster as part of hello resize operation.</span></span>

<span data-ttu-id="7ea15-455">Deux exceptions :</span><span class="sxs-lookup"><span data-stu-id="7ea15-455">There are two exceptions:</span></span>

* <span data-ttu-id="7ea15-456">Si votre cluster a été créé avant le 1er septembre 2015.</span><span class="sxs-lookup"><span data-stu-id="7ea15-456">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="7ea15-457">Il s’agit de la date à laquelle les actions de script ont été introduites.</span><span class="sxs-lookup"><span data-stu-id="7ea15-457">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="7ea15-458">Tout cluster créé avant cette date n’aurait pas pu utiliser les actions de script pour la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="7ea15-458">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="7ea15-459">Si vous avez utilisé plusieurs Actions de Script lors de la création du cluster et utilisé hello même nom pour plusieurs scripts ou hello même nom, même URI, mais des paramètres différents pour plusieurs scripts.</span><span class="sxs-lookup"><span data-stu-id="7ea15-459">If you used multiple Script Actions during cluster creation, and used hello same name for multiple scripts, or hello same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="7ea15-460">Dans ce cas, vous recevez hello l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="7ea15-460">In these cases, you receive hello following error:</span></span>

    <span data-ttu-id="7ea15-461">Aucun nouveau script, les actions peuvent être n’exécutés sur ce cluster en raison de noms de script tooconflicting dans les scripts existants.</span><span class="sxs-lookup"><span data-stu-id="7ea15-461">No new script actions can be ran on this cluster due tooconflicting script names in existing scripts.</span></span> <span data-ttu-id="7ea15-462">Les noms de script fournis au moment de la création du cluster doivent être uniques.</span><span class="sxs-lookup"><span data-stu-id="7ea15-462">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="7ea15-463">Les scripts existants sont exécutés lors du redimensionnement.</span><span class="sxs-lookup"><span data-stu-id="7ea15-463">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ea15-464">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7ea15-464">Next steps</span></span>

* [<span data-ttu-id="7ea15-465">Développer des scripts d’action de script pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ea15-465">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="7ea15-466">Installer et utiliser Solr sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ea15-466">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="7ea15-467">Installer et utiliser Giraph sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ea15-467">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="7ea15-468">Ajouter un cluster de stockage supplémentaire tooan HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ea15-468">Add additional storage tooan HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Procédure de création d’un cluster"
