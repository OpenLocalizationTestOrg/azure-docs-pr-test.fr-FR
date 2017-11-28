---
title: "Personnaliser des clusters HDInsight à l'aide d’actions de script - Azure | Documents Microsoft"
description: "Ajoutez des composants personnalisés à des clusters HDInsight basés sur Linux à l’aide des actions de script. Les actions de script sont des scripts Bash qui peuvent être utilisées pour personnaliser la configuration du cluster ou pour ajouter d’autres services et utilitaires comme Hue, Solr ou R."
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
ms.openlocfilehash: 0c5d00b6cb9f68a1a0e474f81c969eb1b5654c67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="d6863-104">Personnalisation de clusters HDInsight basés sur Linux à l'aide d'une action de script</span><span class="sxs-lookup"><span data-stu-id="d6863-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="d6863-105">HDInsight fournit une option de configuration intitulée **Action de script** , qui appelle des scripts personnalisés pouvant personnaliser le cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize the cluster.</span></span> <span data-ttu-id="d6863-106">Ces scripts sont utilisés pour installer des composants supplémentaires et modifier des paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="d6863-106">These scripts are used to install additional components and change configuration settings.</span></span> <span data-ttu-id="d6863-107">Les actions de script peuvent être utilisées pendant ou après la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6863-108">La possibilité d’utiliser les actions de script sur un cluster déjà en cours d’exécution est uniquement disponible pour les clusters HDInsight sous Linux.</span><span class="sxs-lookup"><span data-stu-id="d6863-108">The ability to use script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="d6863-109">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="d6863-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d6863-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d6863-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="d6863-111">Des actions de script peuvent également être publiées sur Azure Marketplace en tant qu’application HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6863-111">Script actions can also be published to the Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="d6863-112">Certains des exemples de ce document montrent comment vous pouvez installer une application HDInsight à l’aide de commandes d’action de script à partir de PowerShell et du Kit de développement logiciel (SDK) .NET.</span><span class="sxs-lookup"><span data-stu-id="d6863-112">Some of the examples in this document show how you can install an HDInsight application using script action commands from PowerShell and the .NET SDK.</span></span> <span data-ttu-id="d6863-113">Pour plus d’informations sur les applications HDInsight, consultez [Publier des applications HDInsight dans Azure Marketplace](hdinsight-apps-publish-applications.md).</span><span class="sxs-lookup"><span data-stu-id="d6863-113">For more information on HDInsight applications, see [Publish HDInsight applications into the Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="d6863-114">Autorisations</span><span class="sxs-lookup"><span data-stu-id="d6863-114">Permissions</span></span>

<span data-ttu-id="d6863-115">Si vous utilisez un cluster HDInsight joint à un domaine, deux autorisations Ambari sont requises lorsque vous utilisez des actions de script avec le cluster :</span><span class="sxs-lookup"><span data-stu-id="d6863-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with the cluster:</span></span>

* <span data-ttu-id="d6863-116">**AMBARI.RUN\_CUSTOM\_COMMAND** : le rôle Administrateur d’Ambari dispose de cette autorisation par défaut.</span><span class="sxs-lookup"><span data-stu-id="d6863-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: The Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="d6863-117">**CLUSTER.RUN\_CUSTOM\_COMMAND** : l’Administrateur de cluster HDInsight et l’Administrateur Ambari disposent de cette autorisation par défaut.</span><span class="sxs-lookup"><span data-stu-id="d6863-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both the HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="d6863-118">Pour plus d’informations sur l’utilisation des autorisations avec un cluster HDInsight joint à un domaine, consultez [Gestion des clusters HDInsight joints à un domaine](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="d6863-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="d6863-119">Contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="d6863-119">Access control</span></span>

<span data-ttu-id="d6863-120">Si vous n’êtes pas l’administrateur/le propriétaire de votre abonnement Azure, votre compte doit posséder au moins un accès **Contributeur** au groupe de ressources qui contient le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6863-120">If you are not the administrator/owner of your Azure subscription, your account must have at least **Contributor** access to the resource group that contains the HDInsight cluster.</span></span>

<span data-ttu-id="d6863-121">De plus, si vous créez un cluster HDInsight, une personne disposant d’au moins un accès **Collaborateur** à l’abonnement Azure doit avoir auparavant enregistré le fournisseur pour HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6863-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access to the Azure subscription must have previously registered the provider for HDInsight.</span></span> <span data-ttu-id="d6863-122">L’enregistrement du fournisseur se produit lorsqu’un utilisateur disposant d’un accès Contributeur à l’abonnement crée une ressource pour la première fois sur l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="d6863-122">Provider registration happens when a user with Contributor access to the subscription creates a resource for the first time on the subscription.</span></span> <span data-ttu-id="d6863-123">Vous pouvez également faire cela sans créer une ressource en [enregistrant un fournisseur à l’aide de REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6863-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="d6863-124">Pour plus d’informations sur le fonctionnement de la gestion des accès, consultez les documents suivants :</span><span class="sxs-lookup"><span data-stu-id="d6863-124">For more information on working with access management, see the following documents:</span></span>

* [<span data-ttu-id="d6863-125">Prise en main de la gestion des accès dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="d6863-125">Get started with access management in the Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="d6863-126">Utiliser les attributions de rôle pour gérer l’accès à vos ressources d’abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="d6863-126">Use role assignments to manage access to your Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="d6863-127">Comprendre les actions de script</span><span class="sxs-lookup"><span data-stu-id="d6863-127">Understanding Script Actions</span></span>

<span data-ttu-id="d6863-128">Une action de script est tout simplement un script Bash auquel vous apportez une URI et des paramètres.</span><span class="sxs-lookup"><span data-stu-id="d6863-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="d6863-129">Le script s’exécute sur les nœuds du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6863-129">The script runs on nodes in the HDInsight cluster.</span></span> <span data-ttu-id="d6863-130">Les éléments suivants constituent les caractéristiques et les fonctionnalités des actions de script.</span><span class="sxs-lookup"><span data-stu-id="d6863-130">The following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="d6863-131">Elles doivent être stockées sur un URI accessible à partir du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6863-131">Must be stored on a URI that is accessible from the HDInsight cluster.</span></span> <span data-ttu-id="d6863-132">Voici les emplacements de stockage possibles :</span><span class="sxs-lookup"><span data-stu-id="d6863-132">The following are possible storage locations:</span></span>

    * <span data-ttu-id="d6863-133">Un compte **Azure Data Lake Store** accessible via le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6863-133">An **Azure Data Lake Store** account that is accessible by the HDInsight cluster.</span></span> <span data-ttu-id="d6863-134">Pour plus d’informations sur l’utilisation d'Azure Data Lake Store avec HDInsight, voir [Créer un cluster HDInsight avec Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d6863-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="d6863-135">Lorsque vous utilisez un script stocké dans Data Lake Store, le format d’URI est `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span><span class="sxs-lookup"><span data-stu-id="d6863-135">When using a script stored in Data Lake Store, the URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="d6863-136">Le principal de service que HDInsight utilise pour accéder au Data Lake Store doit avoir accès en lecture au script.</span><span class="sxs-lookup"><span data-stu-id="d6863-136">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

    * <span data-ttu-id="d6863-137">Un blob est un **compte de stockage Azure** considéré comme compte de stockage principal ou supplémentaire pour le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6863-137">A blob in an **Azure Storage account** that is either the primary or additional storage account for the HDInsight cluster.</span></span> <span data-ttu-id="d6863-138">HDInsight peut accéder à ces deux types de comptes de stockage lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-138">HDInsight is granted access to both of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="d6863-139">Un service de partage de fichiers public, comme Azure Blob, GitHub, OneDrive, Dropbox, etc.</span><span class="sxs-lookup"><span data-stu-id="d6863-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="d6863-140">Par exemple les URI, consultez la section [Scripts d’actions de script exemples](#example-script-action-scripts).</span><span class="sxs-lookup"><span data-stu-id="d6863-140">For example URIs, see the [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="d6863-141">HDInsight prend uniquement en charge les comptes de stockage Azure à __usage général__.</span><span class="sxs-lookup"><span data-stu-id="d6863-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="d6863-142">Il ne prend actuellement pas en charge le type de compte __stockage Blob__.</span><span class="sxs-lookup"><span data-stu-id="d6863-142">It does not currently support the __Blob storage__ account type.</span></span>

* <span data-ttu-id="d6863-143">Ils peuvent être limités de manière à **s’exécuter sur certains types de nœuds uniquement**, par exemple des nœuds principaux ou des nœuds de travail (worker).</span><span class="sxs-lookup"><span data-stu-id="d6863-143">Can be restricted to **run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d6863-144">Lorsqu’il est utilisé avec HDInsight Premium, vous pouvez spécifier que le script doit être utilisé sur le nœud de périphérie.</span><span class="sxs-lookup"><span data-stu-id="d6863-144">When used with HDInsight Premium, you can specify that the script should be used on the edge node.</span></span>

* <span data-ttu-id="d6863-145">Son état peut être **persistant** ou **ad hoc**.</span><span class="sxs-lookup"><span data-stu-id="d6863-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="d6863-146">Des scripts **persistants** sont appliqués aux nœuds Worker ajoutés au cluster après l’exécution du script.</span><span class="sxs-lookup"><span data-stu-id="d6863-146">**Persisted** scripts are applied to worker nodes added to the cluster after the script runs.</span></span> <span data-ttu-id="d6863-147">Par exemple, lors de la mise à l’échelle du cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-147">For example, when scaling up the cluster.</span></span>

    <span data-ttu-id="d6863-148">Un script persistant peut également appliquer les modifications apportées à un autre type de nœud, tel qu’un nœud principal.</span><span class="sxs-lookup"><span data-stu-id="d6863-148">A persisted script might also apply changes to another node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d6863-149">Les actions de script persistantes doivent avoir un nom unique.</span><span class="sxs-lookup"><span data-stu-id="d6863-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="d6863-150">Les scripts**Ad hoc** ne sont pas conservés.</span><span class="sxs-lookup"><span data-stu-id="d6863-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="d6863-151">Ils ne sont pas appliqués à des nœuds worker ajoutés au cluster après l’exécution du script.</span><span class="sxs-lookup"><span data-stu-id="d6863-151">They are not applied to worker nodes added to the cluster after the script has ran.</span></span> <span data-ttu-id="d6863-152">Vous pouvez toutefois promouvoir un script ad hoc en script persistant ou abaisser un script persistant en script ad hoc.</span><span class="sxs-lookup"><span data-stu-id="d6863-152">You can subsequently promote an ad hoc script to a persisted script, or demote a persisted script to an ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d6863-153">Les actions de script utilisées lors de la création du cluster sont automatiquement rendues persistantes.</span><span class="sxs-lookup"><span data-stu-id="d6863-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="d6863-154">Les scripts qui échouent ne sont pas rendus persistants, même si vous précisez qu’ils doivent l’être.</span><span class="sxs-lookup"><span data-stu-id="d6863-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="d6863-155">Ils peuvent accepter les **paramètres** utilisés par le script lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="d6863-155">Can accept **parameters** that are used by the script during execution.</span></span>
* <span data-ttu-id="d6863-156">Ils sont exécutés avec des **privilèges au niveau de la racine** sur les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-156">Run with **root level privileges** on the cluster nodes.</span></span>
* <span data-ttu-id="d6863-157">Ils peuvent être utilisés par le biais du **portail Azure**, **d’Azure PowerShell**, de **l’interface de ligne de commande Azure (CLI)** ou du **Kit de développement logiciel (SDK) HDInsight .NET**</span><span class="sxs-lookup"><span data-stu-id="d6863-157">Can be used through the **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="d6863-158">Le cluster conserve un historique de tous les scripts ont été exécutés.</span><span class="sxs-lookup"><span data-stu-id="d6863-158">The cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="d6863-159">L’historique est utile lorsque vous devez rechercher l’ID d’un script pour promouvoir ou abaisser des opérations.</span><span class="sxs-lookup"><span data-stu-id="d6863-159">The history is useful when you need to find the ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6863-160">Il n’existe aucune méthode automatique pour annuler les modifications apportées par une action de script.</span><span class="sxs-lookup"><span data-stu-id="d6863-160">There is no automatic way to undo the changes made by a script action.</span></span> <span data-ttu-id="d6863-161">IL faut soit inverser les modifications manuellement, soit fournir un script qui les inverse.</span><span class="sxs-lookup"><span data-stu-id="d6863-161">Either manually reverse the changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-the-cluster-creation-process"></a><span data-ttu-id="d6863-162">Action de script dans le processus de création de cluster</span><span class="sxs-lookup"><span data-stu-id="d6863-162">Script Action in the cluster creation process</span></span>

<span data-ttu-id="d6863-163">Les actions de script utilisées lors de la création du cluster sont légèrement différentes des actions de script exécutées sur un cluster existant :</span><span class="sxs-lookup"><span data-stu-id="d6863-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="d6863-164">Le script est **automatiquement rendu persistant**.</span><span class="sxs-lookup"><span data-stu-id="d6863-164">The script is **automatically persisted**.</span></span>
* <span data-ttu-id="d6863-165">Un **échec** dans le script peut provoquer l’échec du processus de création du cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-165">A **failure** in the script can cause the cluster creation process to fail.</span></span>

<span data-ttu-id="d6863-166">Le diagramme suivant illustre le moment de l’exécution de l’action de script pendant le processus de création :</span><span class="sxs-lookup"><span data-stu-id="d6863-166">The following diagram illustrates when Script Action is executed during the creation process:</span></span>

<span data-ttu-id="d6863-167">![Personnalisation du cluster HDInsight et procédure de création d’un cluster][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="d6863-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="d6863-168">Le script est exécuté pendant la configuration de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6863-168">The script runs while HDInsight is being configured.</span></span> <span data-ttu-id="d6863-169">À ce stade, le script s’exécute en parallèle sur tous les nœuds spécifiés dans le cluster, et s’exécute avec des privilèges root complets sur les nœuds.</span><span class="sxs-lookup"><span data-stu-id="d6863-169">At this stage, the script runs in parallel on all the specified nodes in the cluster, and runs with root privileges on the nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="d6863-170">Étant donné que le script est exécuté avec des privilèges root sur les nœuds du cluster, vous pouvez effectuer des opérations comme arrêter et démarrer des services, notamment des services liés à Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d6863-170">Because the script runs with root level privilege on the cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="d6863-171">Si vous arrêtez les services, vous devez vous assurer que le service Ambari et d’autres services liés à Hadoop sont en cours d’exécution avant la fin de l’exécution du script.</span><span class="sxs-lookup"><span data-stu-id="d6863-171">If you stop services, you must ensure that the Ambari service and other Hadoop-related services are up and running before the script finishes running.</span></span> <span data-ttu-id="d6863-172">Ces services sont requis pour établir correctement l’intégrité et l’état du cluster pendant sa création.</span><span class="sxs-lookup"><span data-stu-id="d6863-172">These services are required to successfully determine the health and state of the cluster while it is being created.</span></span>


<span data-ttu-id="d6863-173">Lors de la création du cluster, vous pouvez utiliser plusieurs actions de script à la fois.</span><span class="sxs-lookup"><span data-stu-id="d6863-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="d6863-174">Ces scripts sont appelés dans l’ordre dans lequel ils ont été spécifiés.</span><span class="sxs-lookup"><span data-stu-id="d6863-174">These scripts are invoked in the order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6863-175">Les actions de script doivent se terminer dans les 60 minutes, faute de quoi elles expirent.</span><span class="sxs-lookup"><span data-stu-id="d6863-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="d6863-176">Lors de l’approvisionnement du cluster, le script est exécuté en même temps que les autres processus d’installation et de configuration.</span><span class="sxs-lookup"><span data-stu-id="d6863-176">During cluster provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="d6863-177">En raison de cette concurrence pour les ressources, par exemple au niveau du temps processeur ou de la bande passante, l’exécution du script risque de prendre plus de temps que dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="d6863-177">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>
>
> <span data-ttu-id="d6863-178">Pour réduire le temps nécessaire à l’exécution du script, évitez les tâches comme le téléchargement et la compilation d’applications à partir de la source.</span><span class="sxs-lookup"><span data-stu-id="d6863-178">To minimize the time it takes to run the script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="d6863-179">Précompilez des applications et stockez le fichier binaire dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d6863-179">Pre-compile applications and store the binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="d6863-180">Action de script sur un cluster en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="d6863-180">Script action on a running cluster</span></span>

<span data-ttu-id="d6863-181">Contrairement aux actions de script utilisées lors de la création d’un cluster, un échec dans un script exécuté sur un cluster déjà en cours d’exécution n’entraîne pas l’échec automatique du cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause the cluster to change to a failed state.</span></span> <span data-ttu-id="d6863-182">Une fois le script terminé, le cluster doit revenir à son état « en cours d’exécution ».</span><span class="sxs-lookup"><span data-stu-id="d6863-182">Once a script completes, the cluster should return to a "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6863-183">Bien que le cluster soit « en cours d’exécution », l’échec du script pourrait avoir endommagé des composants.</span><span class="sxs-lookup"><span data-stu-id="d6863-183">Even if the cluster has a 'running' state, the failed script may have broken things.</span></span> <span data-ttu-id="d6863-184">Par exemple, un script peut supprimer les fichiers requis par le cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-184">For example, a script could delete files needed by the cluster.</span></span>
>
> <span data-ttu-id="d6863-185">Les actions de scripts s’exécutent avec des privilèges root. Soyez donc sûr de comprendre ce que fait un script avant de l’appliquer à votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it to your cluster.</span></span>

<span data-ttu-id="d6863-186">Quand vous appliquez un script à un cluster, l’état du cluster pour un script réussi passe **d’En cours d’exécution** à **Accepté**, puis à **Configuration HDInsight**. Il finit ensuite par revenir à **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="d6863-186">When applying a script to a cluster, the cluster state changes to from **Running** to **Accepted**, then **HDInsight configuration**, and finally back to **Running** for successful scripts.</span></span> <span data-ttu-id="d6863-187">L’état du script est enregistré dans l’historique des actions de script et vous pouvez utiliser ces informations pour déterminer si le script a réussi ou échoué.</span><span class="sxs-lookup"><span data-stu-id="d6863-187">The script status is logged in the script action history, and you can use this information to determine whether the script succeeded or failed.</span></span> <span data-ttu-id="d6863-188">Par exemple, l’applet de commande PowerShell `Get-AzureRmHDInsightScriptActionHistory` peut être utilisée pour afficher l’état d’un script.</span><span class="sxs-lookup"><span data-stu-id="d6863-188">For example, the `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used to view the status of a script.</span></span> <span data-ttu-id="d6863-189">Cette commande renvoie des informations semblables au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="d6863-189">It returns information similar to the following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="d6863-190">Si vous avez modifié le mot de passe d’utilisateur (admin) du cluster après la création de ce dernier, les actions de script exécutées sur ce cluster risquent d’échouer.</span><span class="sxs-lookup"><span data-stu-id="d6863-190">If you have changed the cluster user (admin) password after the cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="d6863-191">Si des actions de script persistantes ciblent des nœuds worker, elles peuvent échouer quand vous mettez le cluster à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="d6863-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale the cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="d6863-192">Exemple de script d’action de script</span><span class="sxs-lookup"><span data-stu-id="d6863-192">Example Script Action scripts</span></span>

<span data-ttu-id="d6863-193">Des scripts d’action de script peuvent être utilisés par les utilitaires suivants :</span><span class="sxs-lookup"><span data-stu-id="d6863-193">Script Action scripts can be used through the following utilities:</span></span>

* <span data-ttu-id="d6863-194">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="d6863-194">Azure portal</span></span>
* <span data-ttu-id="d6863-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6863-195">Azure PowerShell</span></span>
* <span data-ttu-id="d6863-196">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="d6863-196">Azure CLI</span></span>
* <span data-ttu-id="d6863-197">Kit de développement logiciel (SDK) .NET de HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6863-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="d6863-198">HDInsight propose des scripts pour installer les composants suivants sur des clusters HDInsight :</span><span class="sxs-lookup"><span data-stu-id="d6863-198">HDInsight provides scripts to install the following components on HDInsight clusters:</span></span>

| <span data-ttu-id="d6863-199">Nom</span><span class="sxs-lookup"><span data-stu-id="d6863-199">Name</span></span> | <span data-ttu-id="d6863-200">Script</span><span class="sxs-lookup"><span data-stu-id="d6863-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="d6863-201">**Ajouter un compte Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="d6863-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="d6863-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. Consultez la page [Ajouter un stockage supplémentaire à un cluster HDInsight](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="d6863-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage to an HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="d6863-203">**Installez Hue.**</span><span class="sxs-lookup"><span data-stu-id="d6863-203">**Install Hue**</span></span> |<span data-ttu-id="d6863-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. Consultez [Installer et utiliser Hue sur les clusters HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d6863-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="d6863-205">**Installer Presto**</span><span class="sxs-lookup"><span data-stu-id="d6863-205">**Install Presto**</span></span> |<span data-ttu-id="d6863-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. Consultez la rubrique [Installer et utiliser Presto sur des clusters HDInsight](hdinsight-hadoop-install-presto.md).</span><span class="sxs-lookup"><span data-stu-id="d6863-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="d6863-207">**Installation de Solr**</span><span class="sxs-lookup"><span data-stu-id="d6863-207">**Install Solr**</span></span> |<span data-ttu-id="d6863-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. Consultez [Installer et utiliser Solr sur les clusters HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d6863-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="d6863-209">**Installation de Giraph**</span><span class="sxs-lookup"><span data-stu-id="d6863-209">**Install Giraph**</span></span> |<span data-ttu-id="d6863-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Consultez [Installer et utiliser Giraph sur les clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d6863-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="d6863-211">**Précharger les bibliothèques Hive**</span><span class="sxs-lookup"><span data-stu-id="d6863-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="d6863-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. Consultez [Ajouter des bibliothèques Hive sur des clusters HDInsight](hdinsight-hadoop-add-hive-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="d6863-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="d6863-213">**Installer ou mettre à jour Mono**</span><span class="sxs-lookup"><span data-stu-id="d6863-213">**Install or update Mono**</span></span> | <span data-ttu-id="d6863-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span><span class="sxs-lookup"><span data-stu-id="d6863-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="d6863-215">Consultez [Installer ou mettre à jour Mono sur HDInsight](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="d6863-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="d6863-216">Utiliser une action de script lors de la création du cluster</span><span class="sxs-lookup"><span data-stu-id="d6863-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="d6863-217">Cette section fournit des exemples sur les différentes façons d’utiliser des actions de script lors de la création d’un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6863-217">This section provides examples on the different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-azure-portal"></a><span data-ttu-id="d6863-218">Utiliser une action de script lors de la création d’un cluster à partir du portail Azure</span><span class="sxs-lookup"><span data-stu-id="d6863-218">Use a Script Action during cluster creation from the Azure portal</span></span>

1. <span data-ttu-id="d6863-219">Démarrez la création d'un cluster comme décrit dans [Création de clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="d6863-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="d6863-220">Arrêtez lorsque vous atteignez la section __Résumé du cluster__.</span><span class="sxs-lookup"><span data-stu-id="d6863-220">Stop when you reach the __Cluster summary__ section.</span></span>

2. <span data-ttu-id="d6863-221">Dans la section __Résumé du cluster__, sélectionnez le lien __modifier__ des__Paramètres avancés__.</span><span class="sxs-lookup"><span data-stu-id="d6863-221">From the __Cluster summary__ section, select the __edit__ link for __Advanced settings__.</span></span>

    ![Lien des Paramètres avancés](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="d6863-223">Dans la section __Paramètres avancés__, sélectionnez __Actions de script__.</span><span class="sxs-lookup"><span data-stu-id="d6863-223">From the __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="d6863-224">Dans la section __Actions de script__, sélectionnez __+ Soumettre nouveau__</span><span class="sxs-lookup"><span data-stu-id="d6863-224">From the __Script actions__ section, select __+ Submit new__</span></span>

    ![Soumettre une nouvelle action de script](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="d6863-226">Utilisez l’entrée __Sélectionner un script__ pour sélectionner un script prédéfini.</span><span class="sxs-lookup"><span data-stu-id="d6863-226">Use the __Select a script__ entry to select a pre-made script.</span></span> <span data-ttu-id="d6863-227">Pour utiliser un script personnalisé, sélectionnez __Personnaliser__, puis indiquez le __Nom__ et __URI de script Bash__ pour votre script.</span><span class="sxs-lookup"><span data-stu-id="d6863-227">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span></span>

    ![Ajouter un script sous la forme du script sélectionné](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="d6863-229">La table suivante décrit les éléments sous la forme :</span><span class="sxs-lookup"><span data-stu-id="d6863-229">The following table describes the elements on the form:</span></span>

    | <span data-ttu-id="d6863-230">Propriété</span><span class="sxs-lookup"><span data-stu-id="d6863-230">Property</span></span> | <span data-ttu-id="d6863-231">Valeur</span><span class="sxs-lookup"><span data-stu-id="d6863-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="d6863-232">Sélectionner un script</span><span class="sxs-lookup"><span data-stu-id="d6863-232">Select a script</span></span> | <span data-ttu-id="d6863-233">Pour utiliser votre propre script, sélectionnez __Personnalisé__.</span><span class="sxs-lookup"><span data-stu-id="d6863-233">To use your own script, select __Custom__.</span></span> <span data-ttu-id="d6863-234">Sinon, sélectionnez un des scripts fournis.</span><span class="sxs-lookup"><span data-stu-id="d6863-234">Otherwise, select one of the provided scripts.</span></span> |
    | <span data-ttu-id="d6863-235">Nom</span><span class="sxs-lookup"><span data-stu-id="d6863-235">Name</span></span> |<span data-ttu-id="d6863-236">Indiquez un nom pour l'action de script.</span><span class="sxs-lookup"><span data-stu-id="d6863-236">Specify a name for the script action.</span></span> |
    | <span data-ttu-id="d6863-237">URI de script bash</span><span class="sxs-lookup"><span data-stu-id="d6863-237">Bash script URI</span></span> |<span data-ttu-id="d6863-238">Spécifiez l'URI du script appelé pour personnaliser le cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-238">Specify the URI to the script that is invoked to customize the cluster.</span></span> |
    | <span data-ttu-id="d6863-239">Principal/Employé/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="d6863-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="d6863-240">Spécifiez les nœuds (**Head** ou **Worker** ou **ZooKeeper**) sur lesquels le script de personnalisation est exécuté.</span><span class="sxs-lookup"><span data-stu-id="d6863-240">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the customization script is run.</span></span> |
    | <span data-ttu-id="d6863-241">parameters</span><span class="sxs-lookup"><span data-stu-id="d6863-241">Parameters</span></span> |<span data-ttu-id="d6863-242">Spécifiez les paramètres, si le script le demande.</span><span class="sxs-lookup"><span data-stu-id="d6863-242">Specify the parameters, if required by the script.</span></span> |

    <span data-ttu-id="d6863-243">Utilisez l’entrée __Continuer cette action de script__ pour vous assurer que le script est appliqué aux nœuds lors de la mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="d6863-243">Use the __Persist this script action__ entry to ensure that the script is applied during scaling operations.</span></span>

5. <span data-ttu-id="d6863-244">Sélectionnez __Créer__ pour enregistrer le script.</span><span class="sxs-lookup"><span data-stu-id="d6863-244">Select __Create__ to save the script.</span></span> <span data-ttu-id="d6863-245">Vous pouvez ensuite utiliser __+ Soumettre nouveau__ pour ajouter un autre script.</span><span class="sxs-lookup"><span data-stu-id="d6863-245">You can then use __+ Submit new__ to add another script.</span></span>

    ![Plusieurs actions de script](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="d6863-247">Une fois l’ajout de scripts terminé, utilisez le bouton __Sélectionner__, puis le bouton __Suivant__ pour revenir à la section __Résumé du cluster__.</span><span class="sxs-lookup"><span data-stu-id="d6863-247">When you are done adding scripts, use the __Select__ button, and then the __Next__ button to return to the __Cluster summary__ section.</span></span>

3. <span data-ttu-id="d6863-248">Sur la page __Résumé du cluster__, sélectionnez __Créer__ pour créer le cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-248">To create the cluster, select __Create__ from the __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="d6863-249">Utilisez une action de Script à partir de modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d6863-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="d6863-250">Les exemples de cette section décrivent comment utiliser des actions de script avec les modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d6863-250">The examples in this section demonstrate how to use script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="d6863-251">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="d6863-251">Before you begin</span></span>

* <span data-ttu-id="d6863-252">Pour plus d’informations sur la configuration d’un poste de travail pour exécuter des applets de commande HDInsight Powershell, consultez la rubrique [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d6863-252">For information about configuring a workstation to run HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="d6863-253">Pour obtenir des instructions sur la création de modèles, consultez [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d6863-253">For instructions on how to create templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="d6863-254">Si vous n’avez pas déjà utilisé Azure PowerShell avec Resource Manager, consultez [Utilisation d’Azure PowerShell avec Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="d6863-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="d6863-255">Création de clusters à l’aide d’une action de script</span><span class="sxs-lookup"><span data-stu-id="d6863-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="d6863-256">Copiez le modèle suivant vers un emplacement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d6863-256">Copy the following template to a location on your computer.</span></span> <span data-ttu-id="d6863-257">Ce modèle installe Giraph sur les nœuds principaux, ainsi que des nœuds worker dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-257">This template installs Giraph on the headnodes and worker nodes in the cluster.</span></span> <span data-ttu-id="d6863-258">Vous pouvez également vérifier si le modèle JSON est valide.</span><span class="sxs-lookup"><span data-stu-id="d6863-258">You can also verify if the JSON template is valid.</span></span> <span data-ttu-id="d6863-259">Collez le contenu de votre modèle dans [JSONLint](http://jsonlint.com/), un outil de validation JSON en ligne.</span><span class="sxs-lookup"><span data-stu-id="d6863-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

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
2. <span data-ttu-id="d6863-260">Démarrer Azure PowerShell et se connecter à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="d6863-260">Start Azure PowerShell and Log in to your Azure account.</span></span> <span data-ttu-id="d6863-261">Une fois que vous avez entré vos informations d'identification, la commande retourne les informations relatives à votre compte.</span><span class="sxs-lookup"><span data-stu-id="d6863-261">After providing your credentials, the command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="d6863-262">Si vous avez plusieurs abonnements, fournissez l’ID d’abonnement que vous souhaitez utiliser pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="d6863-262">If you have multiple subscriptions, provide the subscription ID you wish to use for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="d6863-263">Vous pouvez utiliser `Get-AzureRmSubscription` pour obtenir la liste de tous les abonnements associés à votre compte, y compris l’ID d’abonnement de chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="d6863-263">You can use `Get-AzureRmSubscription` to get a list of all subscriptions associated with your account, which includes the subscription ID for each one.</span></span>

4. <span data-ttu-id="d6863-264">Si vous n’avez pas de groupe de ressources, créez-en un.</span><span class="sxs-lookup"><span data-stu-id="d6863-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="d6863-265">Indiquez le nom du groupe de ressources et l'emplacement dont vous avez besoin pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="d6863-265">Provide the name of the resource group and location that you need for your solution.</span></span> <span data-ttu-id="d6863-266">Un résumé du nouveau groupe de ressources est retourné.</span><span class="sxs-lookup"><span data-stu-id="d6863-266">A summary of the new resource group is returned.</span></span>

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

5. <span data-ttu-id="d6863-267">Pour créer un déploiement pour votre groupe de ressources, exécutez la commande **New-AzureRmResourceGroupDeployment** et indiquez les paramètres nécessaires.</span><span class="sxs-lookup"><span data-stu-id="d6863-267">To create a deployment for your resource group, run the **New-AzureRmResourceGroupDeployment** command and provide the necessary parameters.</span></span> <span data-ttu-id="d6863-268">Les paramètres comprennent les données suivantes :</span><span class="sxs-lookup"><span data-stu-id="d6863-268">The parameters include the following data:</span></span>

    * <span data-ttu-id="d6863-269">un nom pour votre déploiement ;</span><span class="sxs-lookup"><span data-stu-id="d6863-269">A name for your deployment</span></span>
    * <span data-ttu-id="d6863-270">le nom de votre groupe de ressources ;</span><span class="sxs-lookup"><span data-stu-id="d6863-270">The name of your resource group</span></span>
    * <span data-ttu-id="d6863-271">le chemin d’accès ou l’URL vers le modèle que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="d6863-271">The path or URL to the template you created.</span></span>

  <span data-ttu-id="d6863-272">Si votre modèle requiert n’importe quel paramètre, vous devez également transférer les paramètres.</span><span class="sxs-lookup"><span data-stu-id="d6863-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="d6863-273">Dans ce cas, l’action de script pour installer R sur le cluster ne nécessite pas de paramètres.</span><span class="sxs-lookup"><span data-stu-id="d6863-273">In this case, the script action to install R on the cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="d6863-274">Vous serez invité à fournir des valeurs pour les paramètres définis dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="d6863-274">You are prompted to provide values for the parameters defined in the template.</span></span>

1. <span data-ttu-id="d6863-275">Une fois le groupe de ressources déployé, un résumé du déploiement apparaît.</span><span class="sxs-lookup"><span data-stu-id="d6863-275">When the resource group has been deployed, a summary of the deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="d6863-276">Si votre déploiement échoue, vous pouvez utiliser les applets de commande suivants pour obtenir des informations sur les échecs.</span><span class="sxs-lookup"><span data-stu-id="d6863-276">If your deployment fails, you can use the following cmdlets to get information about the failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="d6863-277">Utiliser une action de script lors de la création du cluster à partir d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6863-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="d6863-278">Dans cette section, nous allons utiliser l'applet de commande [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) pour appeler des scripts avec une action de script pour personnaliser un cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-278">In this section, we use the [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet to invoke scripts by using Script Action to customize a cluster.</span></span> <span data-ttu-id="d6863-279">Avant de poursuivre, assurez-vous que vous avez installé et configuré Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6863-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="d6863-280">Pour plus d'informations sur la configuration d'un poste de travail pour exécuter des applets de commande HDInsight PowerShell, consultez la rubrique [Installation et configuration d'Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d6863-280">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="d6863-281">Le script suivant indique comment appliquer une action de script lors de la création d’un cluster à l’aide de PowerShell :</span><span class="sxs-lookup"><span data-stu-id="d6863-281">The following script demonstrates how to apply a script action when creating a cluster using PowerShell:</span></span>

<span data-ttu-id="d6863-282">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]</span><span class="sxs-lookup"><span data-stu-id="d6863-282">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]</span></span>

<span data-ttu-id="d6863-283">La création du cluster peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="d6863-283">It can take several minutes before the cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-hdinsight-net-sdk"></a><span data-ttu-id="d6863-284">Utiliser une action de script lors de la création du cluster à l’aide du Kit de développement logiciel (SDK) HDInsight .NET</span><span class="sxs-lookup"><span data-stu-id="d6863-284">Use a Script Action during cluster creation from the HDInsight .NET SDK</span></span>

<span data-ttu-id="d6863-285">Le Kit de développement logiciel (SDK) .NET HDInsight fournit des bibliothèques clientes qui facilitent l’utilisation d’HDInsight à partir d’une application .NET.</span><span class="sxs-lookup"><span data-stu-id="d6863-285">The HDInsight .NET SDK provides client libraries that makes it easier to work with HDInsight from a .NET application.</span></span> <span data-ttu-id="d6863-286">Pour obtenir un exemple de code, consultez [Créer des clusters basés sur Linux dans HDInsight à l’aide du Kit de développement logiciel (SDK) .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="d6863-286">For a code sample, see [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-to-a-running-cluster"></a><span data-ttu-id="d6863-287">Appliquer une action de script sur un cluster en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="d6863-287">Apply a Script Action to a running cluster</span></span>

<span data-ttu-id="d6863-288">Dans cette section, découvrez comment appliquer des actions de script à un cluster en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="d6863-288">In this section, learn how to apply script actions to a running cluster.</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-portal"></a><span data-ttu-id="d6863-289">Appliquer une action de script sur un cluster en cours d’exécution à partir du portail Azure</span><span class="sxs-lookup"><span data-stu-id="d6863-289">Apply a Script Action to a running cluster from the Azure portal</span></span>

1. <span data-ttu-id="d6863-290">Dans le [portail Azure](https://portal.azure.com), sélectionnez votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6863-290">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="d6863-291">Dans la vue d’ensemble du cluster HDInsight, sélectionnez la vignette **Actions de script**.</span><span class="sxs-lookup"><span data-stu-id="d6863-291">From the HDInsight cluster overview, select the **Script Actions** tile.</span></span>

    ![Vignette Actions de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="d6863-293">Vous pouvez également sélectionner **Tous les paramètres**, puis **Actions de script** dans la section Paramètres.</span><span class="sxs-lookup"><span data-stu-id="d6863-293">You can also select **All settings** and then select **Script Actions** from the Settings section.</span></span>

3. <span data-ttu-id="d6863-294">Dans le coin supérieur de la section Actions de script, sélectionnez **Soumettre nouveau**.</span><span class="sxs-lookup"><span data-stu-id="d6863-294">From the top of the Script Actions section, select **Submit new**.</span></span>

    ![Ajouter une action de script à un cluster en cours d’exécution](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="d6863-296">Utilisez l’entrée __Sélectionner un script__ pour sélectionner un script prédéfini.</span><span class="sxs-lookup"><span data-stu-id="d6863-296">Use the __Select a script__ entry to select a pre-made script.</span></span> <span data-ttu-id="d6863-297">Pour utiliser un script personnalisé, sélectionnez __Personnaliser__, puis indiquez le __Nom__ et __URI de script Bash__ pour votre script.</span><span class="sxs-lookup"><span data-stu-id="d6863-297">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span></span>

    ![Ajouter un script sous la forme du script sélectionné](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="d6863-299">La table suivante décrit les éléments sous la forme :</span><span class="sxs-lookup"><span data-stu-id="d6863-299">The following table describes the elements on the form:</span></span>

    | <span data-ttu-id="d6863-300">Propriété</span><span class="sxs-lookup"><span data-stu-id="d6863-300">Property</span></span> | <span data-ttu-id="d6863-301">Valeur</span><span class="sxs-lookup"><span data-stu-id="d6863-301">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="d6863-302">Sélectionner un script</span><span class="sxs-lookup"><span data-stu-id="d6863-302">Select a script</span></span> | <span data-ttu-id="d6863-303">Pour utiliser votre propre script, sélectionnez __Personnalisé__.</span><span class="sxs-lookup"><span data-stu-id="d6863-303">To use your own script, select __custom__.</span></span> <span data-ttu-id="d6863-304">Sinon, sélectionnez un script fourni.</span><span class="sxs-lookup"><span data-stu-id="d6863-304">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="d6863-305">Nom</span><span class="sxs-lookup"><span data-stu-id="d6863-305">Name</span></span> |<span data-ttu-id="d6863-306">Indiquez un nom pour l'action de script.</span><span class="sxs-lookup"><span data-stu-id="d6863-306">Specify a name for the script action.</span></span> |
    | <span data-ttu-id="d6863-307">URI de script bash</span><span class="sxs-lookup"><span data-stu-id="d6863-307">Bash script URI</span></span> |<span data-ttu-id="d6863-308">Spécifiez l'URI du script appelé pour personnaliser le cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-308">Specify the URI to the script that is invoked to customize the cluster.</span></span> |
    | <span data-ttu-id="d6863-309">Principal/Employé/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="d6863-309">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="d6863-310">Spécifiez les nœuds (**Head** ou **Worker** ou **ZooKeeper**) sur lesquels le script de personnalisation est exécuté.</span><span class="sxs-lookup"><span data-stu-id="d6863-310">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the customization script is run.</span></span> |
    | <span data-ttu-id="d6863-311">parameters</span><span class="sxs-lookup"><span data-stu-id="d6863-311">Parameters</span></span> |<span data-ttu-id="d6863-312">Spécifiez les paramètres, si le script le demande.</span><span class="sxs-lookup"><span data-stu-id="d6863-312">Specify the parameters, if required by the script.</span></span> |

    <span data-ttu-id="d6863-313">Utilisez l’entrée __Continuer cette action de script__ pour vous assurer que le script est appliqué aux nœuds lors de la mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="d6863-313">Use the __Persist this script action__ entry to make sure the script is applied during scaling operations.</span></span>

5. <span data-ttu-id="d6863-314">Pour finir, cliquez sur le bouton **Créer** afin d’appliquer le script au cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-314">Finally, use the **Create** button to apply the script to the cluster.</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-azure-powershell"></a><span data-ttu-id="d6863-315">Appliquer une action de script sur un cluster en cours d’exécution à partir d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6863-315">Apply a Script Action to a running cluster from Azure PowerShell</span></span>

<span data-ttu-id="d6863-316">Avant de poursuivre, assurez-vous que vous avez installé et configuré Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6863-316">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="d6863-317">Pour plus d'informations sur la configuration d'un poste de travail pour exécuter des applets de commande HDInsight PowerShell, consultez la rubrique [Installation et configuration d'Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d6863-317">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="d6863-318">L’exemple suivant décrit comment appliquer une action de script à un cluster en cours d'exécution :</span><span class="sxs-lookup"><span data-stu-id="d6863-318">The following example demonstrates how to apply a script action to a running cluster:</span></span>

<span data-ttu-id="d6863-319">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]</span><span class="sxs-lookup"><span data-stu-id="d6863-319">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]</span></span>

<span data-ttu-id="d6863-320">Une fois l’opération terminée, vous recevez des informations similaires au texte ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d6863-320">Once the operation completes, you receive information similar to the following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-cli"></a><span data-ttu-id="d6863-321">Appliquer une action de script sur un cluster en cours d’exécution à partir de l'interface de ligne de commande Azure (CLI)</span><span class="sxs-lookup"><span data-stu-id="d6863-321">Apply a Script Action to a running cluster from the Azure CLI</span></span>

<span data-ttu-id="d6863-322">Avant de poursuivre, assurez-vous que vous avez installé et configuré l'interface de ligne de commande Azure (CLI).</span><span class="sxs-lookup"><span data-stu-id="d6863-322">Before proceeding, make sure you have installed and configured the Azure CLI.</span></span> <span data-ttu-id="d6863-323">Pour plus d’informations, consultez la rubrique [Installation de l’interface de ligne de commande Azure (CLI)](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d6863-323">For more information, see [Install the Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="d6863-324">Pour passer en mode Azure Resource Manager, utilisez la commande suivante sur la ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="d6863-324">To switch to Azure Resource Manager mode, use the following command at the command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="d6863-325">Utilisez la commande suivante pour vous identifier auprès de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d6863-325">Use the following to authenticate to your Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="d6863-326">Utilisez la commande suivante pour appliquer une action de script à un cluster en cours d'exécution</span><span class="sxs-lookup"><span data-stu-id="d6863-326">Use the following command to apply a script action to a running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="d6863-327">Si vous omettez les paramètres de cette commande, vous êtes invité à les saisir.</span><span class="sxs-lookup"><span data-stu-id="d6863-327">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="d6863-328">Si le script que vous spécifiez avec `-u` accepte des paramètres, vous pouvez les spécifier à l’aide du paramètre `-p`.</span><span class="sxs-lookup"><span data-stu-id="d6863-328">If the script you specify with `-u` accepts parameters, you can specify them using the `-p` parameter.</span></span>

    <span data-ttu-id="d6863-329">Les types de nœud valides sont `headnode`, `workernode` et `zookeeper`.</span><span class="sxs-lookup"><span data-stu-id="d6863-329">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="d6863-330">Si le script doit être appliqué à plusieurs types de nœud, spécifiez ces types en les séparant par un « ; ».</span><span class="sxs-lookup"><span data-stu-id="d6863-330">If the script should be applied to multiple node types, specify the types separated by a ';'.</span></span> <span data-ttu-id="d6863-331">Par exemple : `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="d6863-331">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="d6863-332">Pour conserver le script, ajoutez le paramètre `--persistOnSuccess`.</span><span class="sxs-lookup"><span data-stu-id="d6863-332">To persist the script, add the `--persistOnSuccess`.</span></span> <span data-ttu-id="d6863-333">Vous pouvez également continuer le script à une date ultérieure à l’aide de `azure hdinsight script-action persisted set`.</span><span class="sxs-lookup"><span data-stu-id="d6863-333">You can also persist the script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="d6863-334">Une fois le travail terminé, vous obtenez un résultat similaire au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="d6863-334">Once the job completes, you receive output similar to the following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-to-a-running-cluster-using-rest-api"></a><span data-ttu-id="d6863-335">Appliquer une action de script sur un cluster en cours d’exécution à l’aide de l’API REST</span><span class="sxs-lookup"><span data-stu-id="d6863-335">Apply a Script Action to a running cluster using REST API</span></span>

<span data-ttu-id="d6863-336">Consultez [Exécuter des actions de script sur un cluster en cours d’exécution](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6863-336">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-hdinsight-net-sdk"></a><span data-ttu-id="d6863-337">Appliquer une action de script sur un cluster en cours d’exécution à partir du Kit de développement logiciel (SDK) HDInsight .NET</span><span class="sxs-lookup"><span data-stu-id="d6863-337">Apply a Script Action to a running cluster from the HDInsight .NET SDK</span></span>

<span data-ttu-id="d6863-338">Pour obtenir un exemple d’utilisation du Kit de développement logiciel (SDK) .NET pour appliquer des scripts à un cluster, consultez [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="d6863-338">For an example of using the .NET SDK to apply scripts to a cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="d6863-339">Afficher l’historique, promouvoir et abaisser des actions de script</span><span class="sxs-lookup"><span data-stu-id="d6863-339">View history, promote, and demote Script Actions</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="d6863-340">Utilisation du portail Azure</span><span class="sxs-lookup"><span data-stu-id="d6863-340">Using the Azure portal</span></span>

1. <span data-ttu-id="d6863-341">Dans le [portail Azure](https://portal.azure.com), sélectionnez votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6863-341">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="d6863-342">Dans la vue d’ensemble du cluster HDInsight, sélectionnez la vignette **Actions de script**.</span><span class="sxs-lookup"><span data-stu-id="d6863-342">From the HDInsight cluster overview, select the **Script Actions** tile.</span></span>

    ![Vignette Actions de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="d6863-344">Vous pouvez également sélectionner **Tous les paramètres**, puis **Actions de script** dans la section Paramètres.</span><span class="sxs-lookup"><span data-stu-id="d6863-344">You can also select **All settings** and then select **Script Actions** from the Settings section.</span></span>

4. <span data-ttu-id="d6863-345">Un historique des scripts pour ce cluster s’affiche dans la section Actions de script.</span><span class="sxs-lookup"><span data-stu-id="d6863-345">A history of scripts for this cluster is displayed on the Script Actions section.</span></span> <span data-ttu-id="d6863-346">Ces informations comprennent une liste de scripts persistants.</span><span class="sxs-lookup"><span data-stu-id="d6863-346">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="d6863-347">Dans la capture d’écran ci-dessous, vous pouvez voir que le script Solr a été exécuté sur ce cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-347">In the screenshot below, you can see that the Solr script has been ran on this cluster.</span></span> <span data-ttu-id="d6863-348">La capture d’écran n’affiche aucun script persistants.</span><span class="sxs-lookup"><span data-stu-id="d6863-348">The screenshot does not show any persisted scripts.</span></span>

    ![Section Actions de script](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="d6863-350">la sélection d’un script dans l’historique permet d’afficher sa section Propriétés.</span><span class="sxs-lookup"><span data-stu-id="d6863-350">Selecting a script from the history displays the Properties section for this script.</span></span> <span data-ttu-id="d6863-351">Dans le coin supérieur de l’écran, vous pouvez réexécuter le script ou le promouvoir.</span><span class="sxs-lookup"><span data-stu-id="d6863-351">From the top of the screen, you can rerun the script or promote it.</span></span>

    ![Propriétés des actions de script](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="d6863-353">Vous pouvez également utiliser le **…** situé sur le côté droit des entrées de la section Actions de script pour effectuer des actions.</span><span class="sxs-lookup"><span data-stu-id="d6863-353">You can also use the **...** to the right of entries on the Script Actions section to perform actions.</span></span>

    ![Utilisation de … des actions de script](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="d6863-355">Utilisation de Microsoft Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6863-355">Using Azure PowerShell</span></span>

| <span data-ttu-id="d6863-356">Utilisez...</span><span class="sxs-lookup"><span data-stu-id="d6863-356">Use the following...</span></span> | <span data-ttu-id="d6863-357">Pour...</span><span class="sxs-lookup"><span data-stu-id="d6863-357">To ...</span></span> |
| --- | --- |
| <span data-ttu-id="d6863-358">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="d6863-358">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="d6863-359">Récupérer des informations sur les actions de script persistantes</span><span class="sxs-lookup"><span data-stu-id="d6863-359">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="d6863-360">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="d6863-360">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="d6863-361">Récupérer l’historique des actions de script appliquées au cluster, ou les informations d’un script spécifique</span><span class="sxs-lookup"><span data-stu-id="d6863-361">Retrieve a history of script actions applied to the cluster, or details for a specific script</span></span> |
| <span data-ttu-id="d6863-362">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="d6863-362">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="d6863-363">Promouvoir une action de script ad hoc en action de script persistante</span><span class="sxs-lookup"><span data-stu-id="d6863-363">Promotes an ad hoc script action to a persisted script action</span></span> |
| <span data-ttu-id="d6863-364">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="d6863-364">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="d6863-365">Abaisser une action de script persistante en action ad hoc</span><span class="sxs-lookup"><span data-stu-id="d6863-365">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="d6863-366">L’utilisation de `Remove-AzureRmHDInsightPersistedScriptAction` n’annule pas les actions effectuées par un script.</span><span class="sxs-lookup"><span data-stu-id="d6863-366">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo the actions performed by a script.</span></span> <span data-ttu-id="d6863-367">Cette applet de commande supprime uniquement l’indicateur persistant.</span><span class="sxs-lookup"><span data-stu-id="d6863-367">This cmdlet only removes the persisted flag.</span></span>

<span data-ttu-id="d6863-368">L’exemple de script suivant illustre l’utilisation des applets de commande pour promouvoir, puis pour abaisser un script.</span><span class="sxs-lookup"><span data-stu-id="d6863-368">The following example script demonstrates using the cmdlets to promote, then demote a script.</span></span>

<span data-ttu-id="d6863-369">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]</span><span class="sxs-lookup"><span data-stu-id="d6863-369">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]</span></span>

### <a name="using-the-azure-cli"></a><span data-ttu-id="d6863-370">Utilisation de l’interface de ligne de commande Azure (CLI)</span><span class="sxs-lookup"><span data-stu-id="d6863-370">Using the Azure CLI</span></span>

| <span data-ttu-id="d6863-371">Utilisez...</span><span class="sxs-lookup"><span data-stu-id="d6863-371">Use the following...</span></span> | <span data-ttu-id="d6863-372">Pour...</span><span class="sxs-lookup"><span data-stu-id="d6863-372">To ...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="d6863-373">Récupérer une liste des actions de script persistantes</span><span class="sxs-lookup"><span data-stu-id="d6863-373">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="d6863-374">Récupérer des informations sur les actions de script persistantes</span><span class="sxs-lookup"><span data-stu-id="d6863-374">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="d6863-375">Récupérer l’historique des actions de script appliquées au cluster</span><span class="sxs-lookup"><span data-stu-id="d6863-375">Retrieve a history of script actions applied to the cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="d6863-376">Récupérer des informations sur une action de script spécifique</span><span class="sxs-lookup"><span data-stu-id="d6863-376">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="d6863-377">Promouvoir une action de script ad hoc en action de script persistante</span><span class="sxs-lookup"><span data-stu-id="d6863-377">Promotes an ad hoc script action to a persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="d6863-378">Abaisser une action de script persistante en action ad hoc</span><span class="sxs-lookup"><span data-stu-id="d6863-378">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="d6863-379">L’utilisation de `azure hdinsight script-action persisted delete` n’annule pas les actions effectuées par un script.</span><span class="sxs-lookup"><span data-stu-id="d6863-379">Using `azure hdinsight script-action persisted delete` does not undo the actions performed by a script.</span></span> <span data-ttu-id="d6863-380">Cette applet de commande supprime uniquement l’indicateur persistant.</span><span class="sxs-lookup"><span data-stu-id="d6863-380">This cmdlet only removes the persisted flag.</span></span>

### <a name="using-the-hdinsight-net-sdk"></a><span data-ttu-id="d6863-381">Utilisation du Kit de développement logiciel (SDK) HDInsight .NET</span><span class="sxs-lookup"><span data-stu-id="d6863-381">Using the HDInsight .NET SDK</span></span>

<span data-ttu-id="d6863-382">Pour obtenir un exemple d’utilisation du Kit de développement logiciel (SDK) .NET afin de récupérer l’historique des scripts d’un cluster, promouvoir ou abaisser des scripts, consultez [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="d6863-382">For an example of using the .NET SDK to retrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="d6863-383">Cet exemple montre également comment installer une application de HDInsight à l’aide du Kit de développement logiciel (SDK) .NET.</span><span class="sxs-lookup"><span data-stu-id="d6863-383">This example also demonstrates how to install an HDInsight application using the .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="d6863-384">Prise en charge des logiciels open source utilisés sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6863-384">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="d6863-385">Le service Microsoft Azure HDInsight utilise un écosystème de technologies open source formées autour de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d6863-385">The Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="d6863-386">Microsoft Azure fournit un niveau général de prise en charge pour les technologies open source.</span><span class="sxs-lookup"><span data-stu-id="d6863-386">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="d6863-387">Pour plus d’informations, consultez la section **Étendue de la prise en charge** du [site Web FAQ du support Azure](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="d6863-387">For more information, see the **Support Scope** section of the [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="d6863-388">Le service HDInsight fournit un niveau supplémentaire de prise en charge pour les composants intégrés.</span><span class="sxs-lookup"><span data-stu-id="d6863-388">The HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="d6863-389">Deux types de composant open source sont disponibles dans le service HDInsight :</span><span class="sxs-lookup"><span data-stu-id="d6863-389">There are two types of open-source components that are available in the HDInsight service:</span></span>

* <span data-ttu-id="d6863-390">**Composants intégrés** : ces composants sont préinstallés sur les clusters HDInsight et fournissent la fonctionnalité principale du cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-390">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span></span> <span data-ttu-id="d6863-391">Par exemple, YARN ResourceManager, le langage de requête Hive (HiveQL) et la bibliothèque Mahout appartiennent à cette catégorie.</span><span class="sxs-lookup"><span data-stu-id="d6863-391">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span></span> <span data-ttu-id="d6863-392">Une liste complète des composants de cluster est disponible sur la page [Nouveautés des versions de cluster Hadoop fournies par HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="d6863-392">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="d6863-393">**Composants personnalisés** : en tant qu’utilisateur du cluster, vous pouvez installer ou utiliser, dans votre charge de travail, tout composant qui est disponible dans la communauté ou que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="d6863-393">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="d6863-394">Les composants fournis avec le cluster HDInsight sont entièrement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d6863-394">Components provided with the HDInsight cluster are fully supported.</span></span> <span data-ttu-id="d6863-395">Le support Microsoft vous aide à isoler et à résoudre les problèmes liés à ces composants.</span><span class="sxs-lookup"><span data-stu-id="d6863-395">Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="d6863-396">Les composants personnalisés bénéficient d'un support commercialement raisonnable pour vous aider à résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="d6863-396">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="d6863-397">La prise en charge de Microsoft peut être en mesure de résoudre le problème, SINON vous pourrez avoir besoin d’associer les chaînes disponibles pour les technologies open source lorsqu’il est possible de recourir à une expertise reconnue concernant cette technologie.</span><span class="sxs-lookup"><span data-stu-id="d6863-397">Microsoft support may be able to resolve the issue OR they may ask you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="d6863-398">Vous pouvez, par exemple, utiliser de nombreux sites de communauté, comme le [forum MSDN sur HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). En outre, les projets Apache ont des sites de projet sur [http://apache.org](http://apache.org). Par exemple : [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="d6863-398">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="d6863-399">Le service HDInsight fournit plusieurs méthodes d’utilisation de ces composants personnalisés.</span><span class="sxs-lookup"><span data-stu-id="d6863-399">The HDInsight service provides several ways to use custom components.</span></span> <span data-ttu-id="d6863-400">Quel que soit le mode d’utilisation ou d’installation du composant sur le cluster, le même niveau de support s’applique.</span><span class="sxs-lookup"><span data-stu-id="d6863-400">The same level of support applies, regardless of how a component is used or installed on the cluster.</span></span> <span data-ttu-id="d6863-401">La liste suivante décrit les méthodes les plus courantes d’utilisation des composants personnalisés sur des clusters HDInsight :</span><span class="sxs-lookup"><span data-stu-id="d6863-401">The following list describes the most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="d6863-402">Envoi de travaux : il est possible d’envoyer des travaux Hadoop ou d’autres types de travaux au cluster qui exécute ou utilise des composants personnalisés.</span><span class="sxs-lookup"><span data-stu-id="d6863-402">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span></span>

2. <span data-ttu-id="d6863-403">Personnalisation de cluster : lors de la création du cluster, vous pouvez spécifier des paramètres supplémentaires et des composants personnalisés qui sont installés sur les nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-403">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on the cluster nodes.</span></span>

3. <span data-ttu-id="d6863-404">Exemples : pour des composants personnalisés fréquemment utilisés, il arrive que Microsoft et d’autres éditeurs proposent des exemples illustrant leur utilisation sur les clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6863-404">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span></span> <span data-ttu-id="d6863-405">Ces exemples sont fournis sans support.</span><span class="sxs-lookup"><span data-stu-id="d6863-405">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d6863-406">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="d6863-406">Troubleshooting</span></span>

<span data-ttu-id="d6863-407">Vous pouvez utiliser l’interface utilisateur web de Ambari pour afficher les informations consignées par des actions de script.</span><span class="sxs-lookup"><span data-stu-id="d6863-407">You can use Ambari web UI to view information logged by script actions.</span></span> <span data-ttu-id="d6863-408">Si le script échoue pendant la création du cluster, les journaux sont également disponibles dans le compte de stockage par défaut associé au cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-408">If the script fails during cluster creation, the logs are also available in the default storage account associated with the cluster.</span></span> <span data-ttu-id="d6863-409">Cette section fournit des informations sur la façon de récupérer les journaux à l'aide de ces deux options.</span><span class="sxs-lookup"><span data-stu-id="d6863-409">This section provides information on how to retrieve the logs using both these options.</span></span>

### <a name="using-the-ambari-web-ui"></a><span data-ttu-id="d6863-410">À l'aide de l'interface utilisateur Web d’Ambari</span><span class="sxs-lookup"><span data-stu-id="d6863-410">Using the Ambari Web UI</span></span>

1. <span data-ttu-id="d6863-411">Dans votre navigateur, accédez à https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="d6863-411">In your browser, navigate to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="d6863-412">Remplacez CLUSTERNAME par le nom de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6863-412">Replace CLUSTERNAME with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="d6863-413">Lorsque vous y êtes invité, saisissez le nom de compte (admin) et le mot de passe correspondant au cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-413">When prompted, enter the admin account name (admin) and password for the cluster.</span></span> <span data-ttu-id="d6863-414">Vous devrez peut-être saisir de nouveau les informations d’identification d’administrateur dans un formulaire Web.</span><span class="sxs-lookup"><span data-stu-id="d6863-414">You may have to reenter the admin credentials in a web form.</span></span>

2. <span data-ttu-id="d6863-415">Dans la barre située en haut de la page, sélectionnez l’entrée **ops** .</span><span class="sxs-lookup"><span data-stu-id="d6863-415">From the bar at the top of the page, select the **ops** entry.</span></span> <span data-ttu-id="d6863-416">Une liste des opérations en cours et précédentes effectuées sur le cluster via Ambari s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d6863-416">A list of current and previous operations performed on the cluster through Ambari is displayed.</span></span>

    ![Barre de l’interface utilisateur web Ambari avec ops sélectionné](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="d6863-418">Recherchez les entrées comportant **run\_customscriptaction** dans la colonne **Operations**.</span><span class="sxs-lookup"><span data-stu-id="d6863-418">Find the entries that have **run\_customscriptaction** in the **Operations** column.</span></span> <span data-ttu-id="d6863-419">Ces entrées sont créées lors de l’exécution des actions de script.</span><span class="sxs-lookup"><span data-stu-id="d6863-419">These entries are created when the Script Actions run.</span></span>

    ![Capture d’écran des opérations](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="d6863-421">Sélectionnez l’entrée run\customscriptaction et explorez les liens pour afficher les sorties STDOUT et STDERR.</span><span class="sxs-lookup"><span data-stu-id="d6863-421">To view the STDOUT and STDERR output, select the run\customscriptaction entry and drill down through the links.</span></span> <span data-ttu-id="d6863-422">Cette sortie est générée lorsque le script s’exécute et peut contenir des informations utiles.</span><span class="sxs-lookup"><span data-stu-id="d6863-422">This output is generated when the script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-the-default-storage-account"></a><span data-ttu-id="d6863-423">Accès aux journaux à partir du compte de stockage par défaut</span><span class="sxs-lookup"><span data-stu-id="d6863-423">Access logs from the default storage account</span></span>

<span data-ttu-id="d6863-424">Si la création du cluster échoue en raison d’une erreur d’action de script, vous pouvez accéder aux journaux à partir du compte de stockage de cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-424">If the cluster creation fails due to a script action error, the logs can be accessed from the cluster storage account.</span></span>

* <span data-ttu-id="d6863-425">Les journaux de stockage sont disponibles dans `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span><span class="sxs-lookup"><span data-stu-id="d6863-425">The storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![Capture d’écran des opérations](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="d6863-427">Sous ce répertoire, les journaux sont classés séparément selon les nœuds headnode, workernode et zookeeper.</span><span class="sxs-lookup"><span data-stu-id="d6863-427">Under this directory, the logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="d6863-428">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="d6863-428">Some examples are:</span></span>

    * <span data-ttu-id="d6863-429">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="d6863-429">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="d6863-430">**Nœud Worker** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="d6863-430">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="d6863-431">**Nœud Zookeeper** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="d6863-431">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="d6863-432">Toutes les valeurs stdout et stderr de l'hôte correspondant sont téléchargées vers le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="d6863-432">All stdout and stderr of the corresponding host is uploaded to the storage account.</span></span> <span data-ttu-id="d6863-433">Il existe un fichier **output-\*.txt** et un fichier **errors-\*.txt** pour chaque action de script.</span><span class="sxs-lookup"><span data-stu-id="d6863-433">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="d6863-434">Le fichier output-*.txt contient des informations sur l'URI du script que vous avez exécuté sur l'ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="d6863-434">The output-*.txt file contains information about the URI of the script that got run on the host.</span></span> <span data-ttu-id="d6863-435">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6863-435">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="d6863-436">Vous pouvez créer plusieurs fois un cluster d'action de script portant le même nom.</span><span class="sxs-lookup"><span data-stu-id="d6863-436">It's possible that you repeatedly create a script action cluster with the same name.</span></span> <span data-ttu-id="d6863-437">Dans ce cas, vous pouvez différencier les journaux correspondants selon le nom de dossier DATE.</span><span class="sxs-lookup"><span data-stu-id="d6863-437">In such case, you can distinguish the relevant logs based on the DATE folder name.</span></span> <span data-ttu-id="d6863-438">Par exemple, la structure de dossiers d’un cluster (mycluster) créé à différentes dates ressemble à aux entrées de journaux suivantes :</span><span class="sxs-lookup"><span data-stu-id="d6863-438">For example, the folder structure for a cluster (mycluster) created on different dates appears similar to the following log entries:</span></span>

    <span data-ttu-id="d6863-439">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="d6863-439">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="d6863-440">Si vous créez un cluster d'action de script avec le même nom le même jour, vous pouvez utiliser le préfixe unique pour identifier les fichiers journaux correspondants.</span><span class="sxs-lookup"><span data-stu-id="d6863-440">If you create a script action cluster with the same name on the same day, you can use the unique prefix to identify the relevant log files.</span></span>

* <span data-ttu-id="d6863-441">Si vous créez un cluster vers 0 h 00 (minuit), il est possible que les fichiers journaux s'étendent sur deux jours.</span><span class="sxs-lookup"><span data-stu-id="d6863-441">If you create a cluster near 12:00AM (midnight), it's possible that the log files span across two days.</span></span> <span data-ttu-id="d6863-442">Dans ce cas, vous voyez deux dossiers de dates différents pour le même cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-442">In such cases, you see two different date folders for the same cluster.</span></span>

* <span data-ttu-id="d6863-443">Le téléchargement des fichiers journaux vers le conteneur par défaut peut prendre jusqu'à 5 minutes, en particulier pour les clusters de grande taille.</span><span class="sxs-lookup"><span data-stu-id="d6863-443">Uploading log files to the default container can take up to 5 mins, especially for large clusters.</span></span> <span data-ttu-id="d6863-444">Par conséquent, si vous souhaitez accéder aux journaux, vous ne devez pas immédiatement supprimer le cluster en cas d'échec d'une action de script.</span><span class="sxs-lookup"><span data-stu-id="d6863-444">So, if you want to access the logs, you should not immediately delete the cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="d6863-445">Agent de surveillance Ambari</span><span class="sxs-lookup"><span data-stu-id="d6863-445">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="d6863-446">Ne modifiez pas le mot de passe pour l’agent de surveillance Ambari (hdinsightwatchdog) sur votre cluster HDInsight basé sur Linux.</span><span class="sxs-lookup"><span data-stu-id="d6863-446">Do not change the password for the Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d6863-447">La modification du mot de passe pour ce compte élimine la possibilité d’exécuter de nouvelles actions de script sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6863-447">Changing the password for this account breaks the ability to run new script actions on the HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="d6863-448">Impossible d’importer le nom BlobService</span><span class="sxs-lookup"><span data-stu-id="d6863-448">Can't import name BlobService</span></span>

<span data-ttu-id="d6863-449">__Symptômes__ : échec de l’action de script.</span><span class="sxs-lookup"><span data-stu-id="d6863-449">__Symptoms__: The script action fails.</span></span> <span data-ttu-id="d6863-450">Un texte semblable à l’erreur suivante s’affiche lorsque vous observez l’opération dans Ambari :</span><span class="sxs-lookup"><span data-stu-id="d6863-450">Text similar to the following error is displayed when you view the operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="d6863-451">__Cause__ : cette erreur se produit si vous mettez à niveau le client Python de stockage Azure qui est inclus dans le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6863-451">__Cause__: This error occurs if you upgrade the Python Azure Storage client that is included with the HDInsight cluster.</span></span> <span data-ttu-id="d6863-452">HDInsight attend le client de stockage Azure 0.20.0.</span><span class="sxs-lookup"><span data-stu-id="d6863-452">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="d6863-453">__Résolution__ : pour résoudre cette erreur, connectez-vous manuellement à chaque nœud de cluster à l’aide de `ssh` et utilisez la commande suivante pour réinstaller la version correcte du client de stockage :</span><span class="sxs-lookup"><span data-stu-id="d6863-453">__Resolution__: To resolve this error, manually connect to each cluster node using `ssh` and use the following command to reinstall the correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="d6863-454">Pour en savoir plus sur la connexion au cluster via SSH, voir [Utiliser SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d6863-454">For information on connecting to the cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="d6863-455">L’historique n’affiche pas les scripts utilisés lors de la création du cluster</span><span class="sxs-lookup"><span data-stu-id="d6863-455">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="d6863-456">Si votre cluster a été créé avant le 15 mars 2016, une entrée pourrait ne pas s’afficher dans l’historique des actions de script.</span><span class="sxs-lookup"><span data-stu-id="d6863-456">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="d6863-457">Toutefois, si vous redimensionnez le cluster après le 15 mars 2016, les scripts utilisés lors de la création du cluster sont affichés dans l’historique, car ils sont appliqués aux nouveaux nœuds du cluster dans le cadre de l’opération de redimensionnement.</span><span class="sxs-lookup"><span data-stu-id="d6863-457">If you resize the cluster after March 15, 2016, the scripts using during cluster creation appear in history as they are applied to new nodes in the cluster as part of the resize operation.</span></span>

<span data-ttu-id="d6863-458">Deux exceptions :</span><span class="sxs-lookup"><span data-stu-id="d6863-458">There are two exceptions:</span></span>

* <span data-ttu-id="d6863-459">Si votre cluster a été créé avant le 1er septembre 2015.</span><span class="sxs-lookup"><span data-stu-id="d6863-459">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="d6863-460">Il s’agit de la date à laquelle les actions de script ont été introduites.</span><span class="sxs-lookup"><span data-stu-id="d6863-460">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="d6863-461">Tout cluster créé avant cette date n’aurait pas pu utiliser les actions de script pour la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="d6863-461">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="d6863-462">Si vous avez utilisé plusieurs actions de script lors de la création du cluster et donné le même nom à plusieurs scripts, ou le même nom, le même URI, mais des paramètres différents pour plusieurs scripts.</span><span class="sxs-lookup"><span data-stu-id="d6863-462">If you used multiple Script Actions during cluster creation, and used the same name for multiple scripts, or the same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="d6863-463">Dans ce cas, vous recevez l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="d6863-463">In these cases, you receive the following error:</span></span>

    <span data-ttu-id="d6863-464">Aucune nouvelle action de script ne peut être exécutée sur ce cluster en raison d’un conflit de noms de script dans les scripts existants.</span><span class="sxs-lookup"><span data-stu-id="d6863-464">No new script actions can be ran on this cluster due to conflicting script names in existing scripts.</span></span> <span data-ttu-id="d6863-465">Les noms de script fournis au moment de la création du cluster doivent être uniques.</span><span class="sxs-lookup"><span data-stu-id="d6863-465">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="d6863-466">Les scripts existants sont exécutés lors du redimensionnement.</span><span class="sxs-lookup"><span data-stu-id="d6863-466">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6863-467">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d6863-467">Next steps</span></span>

* [<span data-ttu-id="d6863-468">Développer des scripts d’action de script pour HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6863-468">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="d6863-469">Installer et utiliser Solr sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6863-469">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="d6863-470">Installer et utiliser Giraph sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6863-470">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="d6863-471">Ajouter un stockage supplémentaire à un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6863-471">Add additional storage to an HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

<span data-ttu-id="d6863-472">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Procédure de création d’un cluster"</span><span class="sxs-lookup"><span data-stu-id="d6863-472">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Stages during cluster creation"</span></span>
