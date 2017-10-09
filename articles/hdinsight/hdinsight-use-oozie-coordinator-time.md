---
title: coordinateur de Hadoop Oozie aaaUse temporels dans HDInsight | Documents Microsoft
description: "Utilisez le coordinateur Hadoop Oozie basé sur le temps dans HDInsight, un service pour les données volumineuses. Découvrez comment toodefine Oozie coordinateurs et les flux de travail et envoyer des travaux."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a><span data-ttu-id="9ad0c-104">Utiliser coordinateur de Oozie temporels avec Hadoop dans HDInsight toodefine workflows et coordonner les travaux</span><span class="sxs-lookup"><span data-stu-id="9ad0c-104">Use time-based Oozie coordinator with Hadoop in HDInsight toodefine workflows and coordinate jobs</span></span>
<span data-ttu-id="9ad0c-105">Dans cet article, vous allez apprendre comment toodefine le flux de travail et les coordinateurs et comment tootrigger hello travaux du coordinateur, en fonction de temps.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-105">In this article, you'll learn how toodefine workflows and coordinators, and how tootrigger hello coordinator jobs, based on time.</span></span> <span data-ttu-id="9ad0c-106">Il est utile toogo via [Oozie d’utilisation avec HDInsight] [ hdinsight-use-oozie] avant de lire cet article.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-106">It is helpful toogo through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="9ad0c-107">En outre tooOozie, vous pouvez également planifier des travaux à l’aide d’Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-107">In addition tooOozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="9ad0c-108">toolearn Azure Data Factory, consultez [utilisez Pig et Hive avec Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="9ad0c-108">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9ad0c-109">Cet article requiert un cluster HDInsight basé sur Windows.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="9ad0c-110">Pour plus d’informations sur l’utilisation de Oozie, y compris des travaux basés sur un cluster basé sur Linux, consultez [Oozie utilisation avec Hadoop toodefine et exécuter un flux de travail sur HDInsight de basés sur Linux](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="9ad0c-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="9ad0c-111">Présentation d'Oozie</span><span class="sxs-lookup"><span data-stu-id="9ad0c-111">What is Oozie</span></span>
<span data-ttu-id="9ad0c-112">Apache Oozie est un système de workflow/coordination qui gère les tâches Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="9ad0c-113">Il est intégré à la pile de Hadoop hello, et il prend en charge les travaux Hadoop pour Apache MapReduce Apache Pig, Apache Hive et Sqoop d’Apache.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-113">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="9ad0c-114">Il peut également être utilisé tooschedule les travaux système tooa spécifiques, tels que les programmes Java ou des scripts de shell.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-114">It can also be used tooschedule jobs that are specific tooa system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="9ad0c-115">Hello image suivante montre les flux de travail hello que vous allez implémenter :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-115">hello following image shows hello workflow you will implement:</span></span>

![Diagramme du workflow][img-workflow-diagram]

<span data-ttu-id="9ad0c-117">flux de travail Hello contient deux actions :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-117">hello workflow contains two actions:</span></span>

1. <span data-ttu-id="9ad0c-118">Une action de la ruche exécute un Bonjour toocount du script HiveQL occurrences de chaque type de niveau de journal dans un fichier de journal log4j.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-118">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="9ad0c-119">Chaque journal log4j se compose d’une ligne de champs qui contient une [niveau de journal] champ tooshow hello type hello gravité et, par exemple :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field tooshow hello type and hello severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="9ad0c-120">Hello sortie du script Hive est similaire à :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-120">hello Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="9ad0c-121">Pour plus d’informations sur Hive, consultez l’article [Utilisation de Hive avec HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="9ad0c-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="9ad0c-122">Une action Sqoop exporte hello HiveQL action tooa table de sortie dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-122">A Sqoop action exports hello HiveQL action output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="9ad0c-123">Pour plus d'informations sur Sqoop, consultez la rubrique [Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="9ad0c-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="9ad0c-124">Pour les versions Oozie prises en charge sur les clusters HDInsight, consultez [quelles sont les nouveautés dans les versions de cluster hello fournies par HDInsight ?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="9ad0c-124">For supported Oozie versions on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="9ad0c-125">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9ad0c-125">Prerequisites</span></span>
<span data-ttu-id="9ad0c-126">Avant de commencer ce didacticiel, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-126">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="9ad0c-127">**Un poste de travail sur lequel est installé Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9ad0c-128">La prise en charge de la gestion des ressources HDInsight par Azure PowerShell à l’aide d’Azure Service Manager est **déconseillée** ; elle sera supprimée le 1er janvier 2017.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="9ad0c-129">étapes de Hello dans ce document Utilisez hello nouvelles applets de commande HDInsight qui fonctionnent avec Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-129">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="9ad0c-130">Suivez les étapes de hello dans [installer et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello dernière version d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-130">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="9ad0c-131">Si vous avez des scripts qui toobe besoin modifié toouse hello nouvelles applets de commande qui fonctionnent avec Azure Resource Manager, consultez [des outils de migration tooAzure développement basé sur le Gestionnaire de ressources pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-131">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="9ad0c-132">**Un cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="9ad0c-133">Pour plus d’informations sur la création d’un cluster HDInsight, consultez la rubrique ou [Création de clusters HDInsight][hdinsight-provision] ou [Prise en main de HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="9ad0c-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="9ad0c-134">Vous devez hello suivant toogo données didacticiel de hello :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-134">You will need hello following data toogo through hello tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="9ad0c-135">Propriété du cluster</span><span class="sxs-lookup"><span data-stu-id="9ad0c-135">Cluster property</span></span></th><th><span data-ttu-id="9ad0c-136">Nom de la variable Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ad0c-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="9ad0c-137">Valeur</span><span class="sxs-lookup"><span data-stu-id="9ad0c-137">Value</span></span></th><th><span data-ttu-id="9ad0c-138">Description</span><span class="sxs-lookup"><span data-stu-id="9ad0c-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="9ad0c-139">Nom du cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="9ad0c-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="9ad0c-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="9ad0c-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="9ad0c-141">cluster de HDInsight Hello sur lequel vous allez exécuter ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-141">hello HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="9ad0c-142">Nom d'utilisateur du cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="9ad0c-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="9ad0c-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="9ad0c-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="9ad0c-144">nom d’utilisateur HDInsight cluster Hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-144">hello HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="9ad0c-145">Mot de passe de l'utilisateur du cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="9ad0c-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="9ad0c-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="9ad0c-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="9ad0c-147">Hello HDInsight cluster mot de passe.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-147">hello HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="9ad0c-148">Nom du compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="9ad0c-148">Azure storage account name</span></span></td><td><span data-ttu-id="9ad0c-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="9ad0c-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="9ad0c-150">Un cluster HDInsight des toohello disponibles du compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-150">An Azure Storage account available toohello HDInsight cluster.</span></span> <span data-ttu-id="9ad0c-151">Pour ce didacticiel, utilisez le compte de stockage par défaut hello que vous avez spécifié au cours du processus de configuration du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-151">For this tutorial, use hello default storage account that you specified during hello cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="9ad0c-152">Nom du conteneur d'objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="9ad0c-152">Azure Blob container name</span></span></td><td><span data-ttu-id="9ad0c-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="9ad0c-153">$containerName</span></span></td><td></td><td><span data-ttu-id="9ad0c-154">Pour cet exemple, utilisez le conteneur de stockage d’objets Blob Azure hello est utilisé pour le système de fichiers de cluster hello par défaut HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-154">For this example, use hello Azure Blob storage container that is used for hello default HDInsight cluster file system.</span></span> <span data-ttu-id="9ad0c-155">Par défaut, elle a hello comme cluster HDInsight de hello du même nom.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-155">By default, it has hello same name as hello HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="9ad0c-156">
* **Une base de données SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="9ad0c-157">Vous devez configurer une règle de pare-feu pour hello tooallow accès au serveur de base de données SQL à partir de votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-157">You must configure a firewall rule for hello SQL Database server tooallow access from your workstation.</span></span> <span data-ttu-id="9ad0c-158">Pour obtenir des instructions sur la création d’une base de données SQL Azure et de configuration du pare-feu de hello, voir [prise en main de la base de données SQL Azure] [sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="9ad0c-158">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="9ad0c-159">Cet article fournit un script Windows PowerShell pour créer la table de base de données SQL Azure hello dont vous avez besoin pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-159">This article provides a Windows PowerShell script for creating hello Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="9ad0c-160">Propriété de base de données SQL</span><span class="sxs-lookup"><span data-stu-id="9ad0c-160">SQL database property</span></span></th><th><span data-ttu-id="9ad0c-161">Nom de la variable Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ad0c-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="9ad0c-162">Valeur</span><span class="sxs-lookup"><span data-stu-id="9ad0c-162">Value</span></span></th><th><span data-ttu-id="9ad0c-163">Description</span><span class="sxs-lookup"><span data-stu-id="9ad0c-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="9ad0c-164">Nom du serveur de base de données SQL</span><span class="sxs-lookup"><span data-stu-id="9ad0c-164">SQL database server name</span></span></td><td><span data-ttu-id="9ad0c-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="9ad0c-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="9ad0c-166">Hello SQL de base de données serveur toowhich Sqoop exporte les données.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-166">hello SQL database server toowhich Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="9ad0c-167">Nom de connexion à la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="9ad0c-167">SQL database login name</span></span></td><td><span data-ttu-id="9ad0c-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="9ad0c-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="9ad0c-169">Nom de connexion à la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="9ad0c-170">Mot de passe de connexion à la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="9ad0c-170">SQL database login password</span></span></td><td><span data-ttu-id="9ad0c-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="9ad0c-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="9ad0c-172">Mot de passe de connexion à la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="9ad0c-173">Nom de la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="9ad0c-173">SQL database name</span></span></td><td><span data-ttu-id="9ad0c-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="9ad0c-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="9ad0c-175">toowhich de base de données SQL Azure Hello Sqoop exporte les données.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-175">hello Azure SQL database toowhich Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="9ad0c-176">Par défaut, une base de données SQL Azure autorise des connexions aux services Azure tels que Azure HDinsight.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="9ad0c-177">Si ce paramètre de pare-feu est désactivé, vous devez l’activer à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-177">If this firewall setting is disabled, you must enable it from hello Azure Portal.</span></span> <span data-ttu-id="9ad0c-178">Pour obtenir des instructions sur la création d'une base de données SQL et la configuration des règles de pare-feu, consultez la rubrique [Création et configuration d'une base de données SQL][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="9ad0c-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="9ad0c-179">Valeurs hello remplir des tables de hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-179">Fill-in hello values in hello tables.</span></span> <span data-ttu-id="9ad0c-180">Cela vous sera utile pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="9ad0c-181">Définir le flux de travail Oozie et hello script HiveQL connexe</span><span class="sxs-lookup"><span data-stu-id="9ad0c-181">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="9ad0c-182">Les définitions des workflows Oozie sont écrites en hPDL (un langage de définition du processus XML).</span><span class="sxs-lookup"><span data-stu-id="9ad0c-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="9ad0c-183">nom de fichier de flux de travail par défaut Hello est *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-183">hello default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="9ad0c-184">Vous enregistrer le fichier de flux de travail hello localement et déployez-le toohello HDInsight cluster à l’aide d’Azure PowerShell plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-184">You will save hello workflow file locally, and then deploy it toohello HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="9ad0c-185">Hello action Hive dans le flux de travail hello appelle un fichier de script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-185">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="9ad0c-186">Le fichier de script contient trois instructions HiveQL :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="9ad0c-187">**Hello, l’instruction DROP TABLE** suppressions hello log4j ruche table si elle existe.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-187">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="9ad0c-188">**Hello, l’instruction CREATE TABLE** crée une table externe de ruche log4j, qui désigne l’emplacement toohello du fichier de journal log4j hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-188">**hello CREATE TABLE statement** creates a log4j Hive external table, which points toohello location of hello log4j log file;</span></span>
3. <span data-ttu-id="9ad0c-189">**Hello d’emplacement du fichier de journal log4j hello**.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-189">**hello location of hello log4j log file**.</span></span> <span data-ttu-id="9ad0c-190">séparateur de champs Hello est «, ».</span><span class="sxs-lookup"><span data-stu-id="9ad0c-190">hello field delimiter is ",".</span></span> <span data-ttu-id="9ad0c-191">délimiteur de ligne Hello par défaut est « \n ».</span><span class="sxs-lookup"><span data-stu-id="9ad0c-191">hello default line delimiter is "\n".</span></span> <span data-ttu-id="9ad0c-192">Une table externe Hive est fichier de données utilisé tooavoid hello en cours de suppression à partir de l’emplacement d’origine de hello, dans le cas du flux de travail toorun hello Oozie plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-192">A Hive external table is used tooavoid hello data file being removed from hello original location, in case you want toorun hello Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="9ad0c-193">**Hello insérer remplacer l’instruction** compte hello les occurrences de chaque type de niveau de journal à partir de hello log4j ruche table, et elle enregistre l’emplacement de stockage des objets Blob Azure hello sortie tooan.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-193">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and it saves hello output tooan Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="9ad0c-194">Il existe un problème connu de chemin d'accès à Hive.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-194">There is a known Hive path issue.</span></span> <span data-ttu-id="9ad0c-195">Vous le rencontrez lors de l'envoi d'une tâche Oozie.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="9ad0c-196">Hello des instructions pour résoudre le problème de hello se trouvent sur hello TechNet Wiki : [HDInsight Hive erreur : Impossible de toorename][technetwiki-hive-error].</span><span class="sxs-lookup"><span data-stu-id="9ad0c-196">hello instructions for fixing hello issue can be found on hello TechNet Wiki: [HDInsight Hive error: Unable toorename][technetwiki-hive-error].</span></span>

<span data-ttu-id="9ad0c-197">**fichier de script du HiveQL toodefine hello toobe appelée par le flux de travail hello**</span><span class="sxs-lookup"><span data-stu-id="9ad0c-197">**toodefine hello HiveQL script file toobe called by hello workflow**</span></span>

1. <span data-ttu-id="9ad0c-198">Créez un fichier texte avec hello suivant contenu :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-198">Create a text file with hello following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="9ad0c-199">Il existe trois variables utilisées dans un script de hello :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-199">There are three variables used in hello script:</span></span>

   * <span data-ttu-id="9ad0c-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="9ad0c-200">${hiveTableName}</span></span>
   * <span data-ttu-id="9ad0c-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="9ad0c-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="9ad0c-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="9ad0c-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="9ad0c-203">le fichier de définition de flux de travail Hello (workflow.xml dans ce didacticiel) passe ces toothis valeurs HiveQL script en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-203">hello workflow definition file (workflow.xml in this tutorial) will pass these values toothis HiveQL script at run time.</span></span>
2. <span data-ttu-id="9ad0c-204">Enregistrer le fichier hello sous **C:\Tutorials\UseOozie\useooziewf.hql** à l’aide de l’encodage ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="9ad0c-204">Save hello file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="9ad0c-205">(Utilisez le Bloc-notes si votre éditeur de texte ne dispose pas de cette option.) Ce fichier de script sera déployé toohello HDInsight cluster plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed toohello HDInsight cluster later in hello tutorial.</span></span>

<span data-ttu-id="9ad0c-206">**toodefine un flux de travail**</span><span class="sxs-lookup"><span data-stu-id="9ad0c-206">**toodefine a workflow**</span></span>

1. <span data-ttu-id="9ad0c-207">Créez un fichier texte avec hello suivant contenu :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-207">Create a text file with hello following content:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>

        <action name="RunHiveScript">
            <hive xmlns="uri:oozie:hive-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.job.queue.name</name>
                        <value>${queueName}</value>
                    </property>
                </configuration>
                <script>${hiveScript}</script>
                <param>hiveTableName=${hiveTableName}</param>
                <param>hiveDataFolder=${hiveDataFolder}</param>
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
            </hive>
            <ok to="RunSqoopExport"/>
            <error to="fail"/>
        </action>

        <action name="RunSqoopExport">
            <sqoop xmlns="uri:oozie:sqoop-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.compress.map.output</name>
                        <value>true</value>
                    </property>
                </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>
    ```

    <span data-ttu-id="9ad0c-208">Il existe deux actions définies dans le flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-208">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="9ad0c-209">est de démarrer Hello-tooaction *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-209">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="9ad0c-210">Si l’action de hello exécute *OK*, est de l’action suivante de hello *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-210">If hello action runs *OK*, hello next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="9ad0c-211">Hello RunHiveScript a plusieurs variables.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-211">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="9ad0c-212">Vous allez passer les valeurs hello lorsque vous soumettez un travail de Oozie hello à partir de votre station de travail à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-212">You will pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="9ad0c-213">Variable de workflow</span><span class="sxs-lookup"><span data-stu-id="9ad0c-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="9ad0c-214">Variable de workflow</span><span class="sxs-lookup"><span data-stu-id="9ad0c-214">Workflow variables</span></span></th><th><span data-ttu-id="9ad0c-215">Description</span><span class="sxs-lookup"><span data-stu-id="9ad0c-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="9ad0c-216">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="9ad0c-216">${jobTracker}</span></span></td><td><span data-ttu-id="9ad0c-217">Spécifiez les URL de hello du suivi de travail Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-217">Specify hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="9ad0c-218">Utilisez <strong>jobtrackerhost:9010</strong> sur les versions 3.0 et 2.0 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="9ad0c-219">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="9ad0c-219">${nameNode}</span></span></td><td><span data-ttu-id="9ad0c-220">Spécifiez les URL hello du nœud de nom hello Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-220">Specify hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="9ad0c-221">Utilisez hello par défaut fichier système wasb : / / adresse, par exemple, <i>wasb : / /&lt;Nom_conteneur&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-221">Use hello default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="9ad0c-222">${queueName}</span><span class="sxs-lookup"><span data-stu-id="9ad0c-222">${queueName}</span></span></td><td><span data-ttu-id="9ad0c-223">Spécifie le nom de file d’attente hello hello travail destinée au.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-223">Specifies hello queue name that hello job will be submitted to.</span></span> <span data-ttu-id="9ad0c-224">Utilisez <strong>Default</strong>.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="9ad0c-225">Variables de l'action Hive</span><span class="sxs-lookup"><span data-stu-id="9ad0c-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="9ad0c-226">Variable d'action Hive</span><span class="sxs-lookup"><span data-stu-id="9ad0c-226">Hive action variable</span></span></th><th><span data-ttu-id="9ad0c-227">Description</span><span class="sxs-lookup"><span data-stu-id="9ad0c-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="9ad0c-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="9ad0c-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="9ad0c-229">répertoire source Hello hello commande Hive Create Table.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-229">hello source directory for hello Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="9ad0c-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="9ad0c-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="9ad0c-231">dossier de sortie Hello pour hello insérer remplacer l’instruction.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-231">hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="9ad0c-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="9ad0c-232">${hiveTableName}</span></span></td><td><span data-ttu-id="9ad0c-233">nom de Hello de table Hive hello qui fait référence à des fichiers de données log4j hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-233">hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="9ad0c-234">Variables d'action Sqoop</span><span class="sxs-lookup"><span data-stu-id="9ad0c-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="9ad0c-235">Variable d'action Sqoop</span><span class="sxs-lookup"><span data-stu-id="9ad0c-235">Sqoop action variable</span></span></th><th><span data-ttu-id="9ad0c-236">Description</span><span class="sxs-lookup"><span data-stu-id="9ad0c-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="9ad0c-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="9ad0c-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="9ad0c-238">Chaîne de connexion à la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="9ad0c-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="9ad0c-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="9ad0c-240">Hello SQL Azure table toowhere hello données est exportée.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-240">hello Azure SQL database table toowhere hello data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="9ad0c-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="9ad0c-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="9ad0c-242">dossier de sortie Hello pour hello Hive insérer remplacer l’instruction.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-242">hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="9ad0c-243">Il s’agit de hello même dossier pour l’exportation de Sqoop hello (export-dir).</span><span class="sxs-lookup"><span data-stu-id="9ad0c-243">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="9ad0c-244">Pour plus d’informations sur les flux de travail Oozie et à l’aide des actions de flux de travail hello, consultez [documentation Apache Oozie 4.0] [ apache-oozie-400] (pour la version 3.0 du cluster HDInsight) ou [Apache Oozie 3.3.2 documentation] [ apache-oozie-332] (pour la version 2.1 du cluster HDInsight).</span><span class="sxs-lookup"><span data-stu-id="9ad0c-244">For more information about Oozie workflow and using hello workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="9ad0c-245">Enregistrer le fichier hello sous **C:\Tutorials\UseOozie\workflow.xml** à l’aide de l’encodage ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="9ad0c-245">Save hello file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="9ad0c-246">(Utilisez le Bloc-notes si votre éditeur de texte ne dispose pas de cette option.)</span><span class="sxs-lookup"><span data-stu-id="9ad0c-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="9ad0c-247">**coordinateur de toodefine**</span><span class="sxs-lookup"><span data-stu-id="9ad0c-247">**toodefine coordinator**</span></span>

1. <span data-ttu-id="9ad0c-248">Créez un fichier texte avec hello suivant contenu :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-248">Create a text file with hello following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="9ad0c-249">Il existe cinq variables utilisées dans le fichier de définition de hello :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-249">There are five variables used in hello definition file:</span></span>

   | <span data-ttu-id="9ad0c-250">Variable</span><span class="sxs-lookup"><span data-stu-id="9ad0c-250">Variable</span></span> | <span data-ttu-id="9ad0c-251">Description</span><span class="sxs-lookup"><span data-stu-id="9ad0c-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="9ad0c-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="9ad0c-252">${coordFrequency}</span></span> |<span data-ttu-id="9ad0c-253">Heure de pause de la tâche.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-253">Job pause time.</span></span> <span data-ttu-id="9ad0c-254">La fréquence est toujours exprimée en minutes.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="9ad0c-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="9ad0c-255">${coordStart}</span></span> |<span data-ttu-id="9ad0c-256">Heure de début de la tâche.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-256">Job start time.</span></span> |
   | <span data-ttu-id="9ad0c-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="9ad0c-257">${coordEnd}</span></span> |<span data-ttu-id="9ad0c-258">Heure de fin de la tâche.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-258">Job end time.</span></span> |
   | <span data-ttu-id="9ad0c-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="9ad0c-259">${coordTimezone}</span></span> |<span data-ttu-id="9ad0c-260">Oozie traite les tâches du coordinateur dans un fuseau horaire fixe sans passage à l’heure d’été (généralement représenté à l'aide de UTC).</span><span class="sxs-lookup"><span data-stu-id="9ad0c-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="9ad0c-261">Ce fuseau horaire est appelé hello » Oozie traitement fuseau horaire. »</span><span class="sxs-lookup"><span data-stu-id="9ad0c-261">This time zone is referred as hello "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="9ad0c-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="9ad0c-262">${wfPath}</span></span> |<span data-ttu-id="9ad0c-263">chemin d’accès de Hello pour hello workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-263">hello path for hello workflow.xml.</span></span>  <span data-ttu-id="9ad0c-264">Si le nom de fichier de flux de travail hello n’est pas du nom de fichier hello par défaut (workflow.xml), vous devez la spécifier.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-264">If hello workflow file name is not hello default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="9ad0c-265">Enregistrer le fichier hello sous **C:\Tutorials\UseOozie\coordinator.xml** à l’aide de l’encodage ANSI (ASCII) hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-265">Save hello file as **C:\Tutorials\UseOozie\coordinator.xml** by using hello ANSI (ASCII) encoding.</span></span> <span data-ttu-id="9ad0c-266">(Utilisez le Bloc-notes si votre éditeur de texte ne dispose pas de cette option.)</span><span class="sxs-lookup"><span data-stu-id="9ad0c-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a><span data-ttu-id="9ad0c-267">Déployer le projet de Oozie hello et préparer hello didacticiel</span><span class="sxs-lookup"><span data-stu-id="9ad0c-267">Deploy hello Oozie project and prepare hello tutorial</span></span>
<span data-ttu-id="9ad0c-268">Vous allez exécuter une suivant hello de Azure PowerShell script tooperform :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-268">You will run an Azure PowerShell script tooperform hello following:</span></span>

* <span data-ttu-id="9ad0c-269">Hello de copie HiveQL stockage d’objets Blob de script (useoozie.hql) tooAzure, wasb:///tutorials/useoozie/useoozie.hql.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-269">Copy hello HiveQL script (useoozie.hql) tooAzure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="9ad0c-270">Copiez workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-270">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="9ad0c-271">Copiez coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-271">Copy coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="9ad0c-272">Fichier de données de copie hello (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-272">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="9ad0c-273">Créer une table de base de données SQL Azure pour stocker les données d'exportation de Sqoop.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="9ad0c-274">nom de la table Hello est *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-274">hello table name is *log4jLogCount*.</span></span>

<span data-ttu-id="9ad0c-275">**Présentation du stockage HDInsight**</span><span class="sxs-lookup"><span data-stu-id="9ad0c-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="9ad0c-276">HDInsight utilise le stockage d’objets blob Azure pour stocker les données.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="9ad0c-277">wasb : / / est l’implémentation Microsoft du système de fichiers hello distribués Hadoop (HDFS) dans le stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-277">wasb:// is Microsoft's implementation of hello Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="9ad0c-278">Pour plus d'informations, consultez la rubrique [Utilisation du stockage d'objets blob Azure avec HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="9ad0c-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="9ad0c-279">Lorsque vous configurez un cluster HDInsight, un compte de stockage d’objets Blob Azure et un conteneur spécifique à partir de ce compte est désigné en tant que système de fichiers par défaut hello, comme dans HDFS.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as hello default file system, like in HDFS.</span></span> <span data-ttu-id="9ad0c-280">En outre toothis compte de stockage, vous pouvez ajouter plu les comptes de stockage à partir de hello même abonnement Azure ou à partir de différents abonnements Azure pendant hello processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-280">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or from different Azure subscriptions during hello provisioning process.</span></span> <span data-ttu-id="9ad0c-281">Pour plus d'instructions sur l’ajout des comptes de stockage supplémentaires, consultez la rubrique [Approvisionnement de clusters HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="9ad0c-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="9ad0c-282">script de Azure PowerShell hello toosimplify utilisé dans ce didacticiel, tous les fichiers sont stockés dans le conteneur de système de fichiers par défaut hello de hello situé *useoozie/didacticiels/*.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-282">toosimplify hello Azure PowerShell script used in this tutorial, all of hello files are stored in hello default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="9ad0c-283">Par défaut, ce conteneur a hello même nom en tant que nom du cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-283">By default, this container has hello same name as hello HDInsight cluster name.</span></span>
<span data-ttu-id="9ad0c-284">syntaxe de Hello est :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-284">hello syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="9ad0c-285">Hello uniquement *wasb : / /* syntaxe est prise en charge dans la version 3.0 du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-285">Only hello *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="9ad0c-286">Hello plus anciens *asv : / /* syntaxe est prise en charge dans HDInsight 2.1 et 1.6 clusters, mais il n’est pas pris en charge dans les clusters HDInsight 3.0.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-286">hello older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="9ad0c-287">Hello wasb : / / chemin d’accès est un chemin d’accès virtuel.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-287">hello wasb:// path is a virtual path.</span></span> <span data-ttu-id="9ad0c-288">Pour plus d'informations, consultez la rubrique [Utilisation du stockage d'objets blob Azure avec HDInsight][hdinsight-storage] .</span><span class="sxs-lookup"><span data-stu-id="9ad0c-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="9ad0c-289">Un fichier qui est stocké dans un conteneur de système de fichiers par défaut hello est accessible à partir de HDInsight à l’aide des hello suivant URI (j’utilise workflow.xml comme exemple) :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-289">A file that is stored in hello default file system container can be accessed from HDInsight by using any of hello following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="9ad0c-290">Si vous voulez tooaccess hello directement à partir de compte de stockage hello, nom d’objet blob hello pour le fichier de hello est :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-290">If you want tooaccess hello file directly from hello storage account, hello blob name for hello file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="9ad0c-291">**Présentation des tables interne et externe Hive**</span><span class="sxs-lookup"><span data-stu-id="9ad0c-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="9ad0c-292">Il existe quelques éléments, vous devez tooknow sur les tables internes et externes Hive :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-292">There are a few things you need tooknow about Hive internal and external tables:</span></span>

* <span data-ttu-id="9ad0c-293">Hello commande CREATE TABLE crée une table interne, également appelé un tableau managé.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-293">hello CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="9ad0c-294">fichier de données Hello doit se trouver dans le conteneur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-294">hello data file must be located in hello default container.</span></span>
* <span data-ttu-id="9ad0c-295">Hello commande CREATE TABLE déplace les données de salutation fichiertoohello/hive/entrepôt/<TableName> dossier dans le conteneur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-295">hello CREATE TABLE command moves hello data file toohello /hive/warehouse/<TableName> folder in hello default container.</span></span>
* <span data-ttu-id="9ad0c-296">Hello les commandes CREATE EXTERNAL TABLE crée une table externe.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-296">hello CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="9ad0c-297">fichier de données Hello peut être situé en dehors du conteneur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-297">hello data file can be located outside hello default container.</span></span>
* <span data-ttu-id="9ad0c-298">Hello les commandes CREATE EXTERNAL TABLE ne déplace pas le fichier de données hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-298">hello CREATE EXTERNAL TABLE command does not move hello data file.</span></span>
* <span data-ttu-id="9ad0c-299">Hello les commandes CREATE EXTERNAL TABLE n’autorise pas les sous-dossiers dans le dossier hello qui est spécifié dans la clause d’emplacement hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-299">hello CREATE EXTERNAL TABLE command doesn't allow any subfolders under hello folder that is specified in hello LOCATION clause.</span></span> <span data-ttu-id="9ad0c-300">C’est pourquoi hello pourquoi didacticiel de hello effectue une copie du fichier d’exemple.log hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-300">This is hello reason why hello tutorial makes a copy of hello sample.log file.</span></span>

<span data-ttu-id="9ad0c-301">Pour plus d’informations, consultez la rubrique [HDInsight : introduction aux tables interne et externe Hive][cindygross-hive-tables].</span><span class="sxs-lookup"><span data-stu-id="9ad0c-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="9ad0c-302">**didacticiel de hello tooprepare**</span><span class="sxs-lookup"><span data-stu-id="9ad0c-302">**tooprepare hello tutorial**</span></span>

1. <span data-ttu-id="9ad0c-303">Hello ouvrir Windows PowerShell ISE (dans l’écran d’accueil de Windows 8 hello, tapez **PowerShell_ISE**, puis cliquez sur **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-303">Open hello Windows PowerShell ISE (in hello Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="9ad0c-304">Pour plus d'informations, consultez la page [Démarrage de Windows PowerShell sur Windows 8 et Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="9ad0c-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="9ad0c-305">Dans le volet inférieur de hello, exécutez hello suivant commande tooconnect tooyour abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-305">In hello bottom pane, run hello following command tooconnect tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="9ad0c-306">Vous est demandée tooenter vos informations d’identification de compte Azure.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-306">You will be prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="9ad0c-307">Cette méthode d’ajout d’une connexion à un abonnement arrive à expiration, et après 12 heures, vous devez toorun hello applet de commande à nouveau.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-307">This method of adding a subscription connection times out, and after 12 hours, you will have toorun hello cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9ad0c-308">Si vous avez plusieurs abonnements Azure et abonnement de hello par défaut n’est pas hello celui que vous souhaitez toouse, utilisez hello <strong>Select-AzureSubscription</strong> tooselect de l’applet de commande un abonnement.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-308">If you have multiple Azure subscriptions and hello default subscription is not hello one you want toouse, use hello <strong>Select-AzureSubscription</strong> cmdlet tooselect a subscription.</span></span>

3. <span data-ttu-id="9ad0c-309">Copier le script suivant dans le volet de script hello de hello, puis définir des variables de six premiers hello :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-309">Copy hello following script into hello script pane, and then set hello first six variables:</span></span>

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    <span data-ttu-id="9ad0c-310">Pour plus d’une description des variables de hello, consultez hello [conditions préalables](#prerequisites) section dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-310">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="9ad0c-311">Ajouter hello script toohello dans le volet de script hello suivant :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-311">Append hello following toohello script in hello script pane:</span></span>

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create hello log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="9ad0c-312">Cliquez sur **exécuter le Script** ou appuyez sur **F5** script de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-312">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="9ad0c-313">sortie de Hello sera semblable à :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-313">hello output will be similar to:</span></span>

    ![Sortie de la préparation du didacticiel][img-preparation-output]

## <a name="run-hello-oozie-project"></a><span data-ttu-id="9ad0c-315">Exécutez hello Oozie projet</span><span class="sxs-lookup"><span data-stu-id="9ad0c-315">Run hello Oozie project</span></span>
<span data-ttu-id="9ad0c-316">Azure PowerShell ne fournit actuellement aucune applet de commande pour la définition de tâches Oozie.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="9ad0c-317">Vous pouvez utiliser hello **Invoke-RestMethod** tooinvoke applet de commande Oozie des services web.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-317">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="9ad0c-318">API des services web Oozie Hello est une API de JSON HTTP REST.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-318">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="9ad0c-319">Pour plus d’informations sur les API des services web hello Oozie, consultez [documentation Apache Oozie 4.0] [ apache-oozie-400] (pour la version 3.0 du cluster HDInsight) ou [Apache Oozie 3.3.2 documentation] [ apache-oozie-332] (pour la version 2.1 du cluster HDInsight).</span><span class="sxs-lookup"><span data-stu-id="9ad0c-319">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="9ad0c-320">**toosubmit un travail Oozie**</span><span class="sxs-lookup"><span data-stu-id="9ad0c-320">**toosubmit an Oozie job**</span></span>

1. <span data-ttu-id="9ad0c-321">Hello ouvrir Windows PowerShell ISE (dans l’écran d’accueil de Windows 8, tapez **PowerShell_ISE**, puis cliquez sur **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-321">Open hello Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="9ad0c-322">Pour plus d'informations, consultez la page [Démarrage de Windows PowerShell sur Windows 8 et Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="9ad0c-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="9ad0c-323">Suit hello de copie de script dans le volet de script hello et puis ensemble hello variables tout d’abord quatorze (Toutefois, ignorer **$storageUri**).</span><span class="sxs-lookup"><span data-stu-id="9ad0c-323">Copy hello following script into hello script pane, and then set hello first fourteen variables (however, skip **$storageUri**).</span></span>

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    <span data-ttu-id="9ad0c-324">Pour plus d’une description des variables de hello, consultez hello [conditions préalables](#prerequisites) section dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-324">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="9ad0c-325">$coordstart et $coordend sont à partir de flux de travail hello et l’heure de fin.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-325">$coordstart and $coordend are hello workflow starting and ending time.</span></span> <span data-ttu-id="9ad0c-326">toofind out hello heure UTC/GMT, rechercher « GMT » sur bing.com. Hello $coordFrequency est la fréquence à laquelle vous souhaitez toorun hello workflow des minutes.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-326">toofind out hello UTC/GMT time, search "utc time" on bing.com. hello $coordFrequency is how often in minutes you want toorun hello workflow.</span></span>
3. <span data-ttu-id="9ad0c-327">Ajouter hello toohello script suivant.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-327">Append hello following toohello script.</span></span> <span data-ttu-id="9ad0c-328">Cette partie définit la charge utile de hello Oozie :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-328">This part defines hello Oozie payload:</span></span>

    ```powershell
    #OoziePayload used for Oozie web service submission
    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
            <name>nameNode</name>
            <value>$storageUrI</value>
        </property>

        <property>
            <name>jobTracker</name>
            <value>jobtrackerhost:9010</value>
        </property>

        <property>
            <name>queueName</name>
            <value>default</value>
        </property>

        <property>
            <name>oozie.use.system.libpath</name>
            <value>true</value>
        </property>

        <property>
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
        </property>

        <property>
            <name>hiveScript</name>
            <value>$hiveScript</value>
        </property>

        <property>
            <name>hiveTableName</name>
            <value>$hiveTableName</value>
        </property>

        <property>
            <name>hiveDataFolder</name>
            <value>$hiveDataFolder</value>
        </property>

        <property>
            <name>hiveOutputFolder</name>
            <value>$hiveOutputFolder</value>
        </property>

        <property>
            <name>sqlDatabaseConnectionString</name>
            <value>&quot;$sqlDatabaseConnectionString&quot;</value>
        </property>

        <property>
            <name>sqlDatabaseTableName</name>
            <value>$SQLDatabaseTableName</value>
        </property>

        <property>
            <name>user.name</name>
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > <span data-ttu-id="9ad0c-329">fichier de charge utile de soumission principale différence par rapport toohello du flux de travail Hello est variable de hello **oozie.coord.application.path**.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-329">hello major difference compared toohello workflow submission payload file is hello variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="9ad0c-330">Lors de l'envoi d'une tâche de workflow, vous utilisez **oozie.wf.application.path** .</span><span class="sxs-lookup"><span data-stu-id="9ad0c-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="9ad0c-331">Ajouter hello toohello script suivant.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-331">Append hello following toohello script.</span></span> <span data-ttu-id="9ad0c-332">Cette partie vérifie l’état du service web hello Oozie :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-332">This part checks hello Oozie web service status:</span></span>

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="9ad0c-333">Ajouter hello toohello script suivant.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-333">Append hello following toohello script.</span></span> <span data-ttu-id="9ad0c-334">Cette partie crée une tâche Oozie :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="9ad0c-335">Lorsque vous soumettez une tâche de workflow, vous devez apporter d’un autre service appel toostart hello de tâche web après que hello travail est créé.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-335">When you submit a workflow job, you must make another web service call toostart hello job after hello job is created.</span></span> <span data-ttu-id="9ad0c-336">Dans ce cas, les travaux du coordinateur hello est déclenchée par heure.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-336">In this case, hello coordinator job is triggered by time.</span></span> <span data-ttu-id="9ad0c-337">Hello travail démarre automatiquement.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-337">hello job will start automatically.</span></span>

6. <span data-ttu-id="9ad0c-338">Ajouter hello toohello script suivant.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-338">Append hello following toohello script.</span></span> <span data-ttu-id="9ad0c-339">Cette partie vérifie l’état du travail Oozie hello :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-339">This part checks hello Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. <span data-ttu-id="9ad0c-340">(Facultatif) Ajouter hello toohello script suivant.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-340">(Optional) Append hello following toohello script.</span></span>

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="9ad0c-341">Ajouter hello toohello script suivant :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-341">Append hello following toohello script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="9ad0c-342">Supprimez les signes # hello si vous souhaitez que les fonctions supplémentaires de toorun hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-342">Remove hello # signs if you want toorun hello additional functions.</span></span>
9. <span data-ttu-id="9ad0c-343">Si vous disposez du cluster HDInsight version 2.1, remplacez « https://$clusterName.azurehdinsight.net:443/oozie/v2/ » par « https://$clusterName.azurehdinsight.net:443/oozie/v1/ ».</span><span class="sxs-lookup"><span data-stu-id="9ad0c-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="9ad0c-344">La version 2.1 du cluster HDInsight ne pas prend en charge la version 2 de hello web services.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-344">HDInsight cluster version 2.1 does not supports version 2 of hello web services.</span></span>
10. <span data-ttu-id="9ad0c-345">Cliquez sur **exécuter le Script** ou appuyez sur **F5** script de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-345">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="9ad0c-346">sortie de Hello sera semblable à :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-346">hello output will be similar to:</span></span>

     ![Sortie du workflow exécuté par le didacticiel][img-runworkflow-output]
11. <span data-ttu-id="9ad0c-348">Se connecter tooyour données de base de données SQL toosee hello exportée.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-348">Connect tooyour SQL Database toosee hello exported data.</span></span>

<span data-ttu-id="9ad0c-349">**journal des erreurs de travail hello toocheck**</span><span class="sxs-lookup"><span data-stu-id="9ad0c-349">**toocheck hello job error log**</span></span>

<span data-ttu-id="9ad0c-350">tootroubleshoot un flux de travail, fichier de journal hello Oozie trouverez C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log à partir du nœud principal de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-350">tootroubleshoot a workflow, hello Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from hello cluster headnode.</span></span> <span data-ttu-id="9ad0c-351">Pour plus d’informations sur le protocole RDP, consultez [clusters HDInsight d’administration à l’aide de hello portail Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="9ad0c-351">For information on RDP, see [Administering HDInsight clusters using hello Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="9ad0c-352">**didacticiel de hello toorerun**</span><span class="sxs-lookup"><span data-stu-id="9ad0c-352">**toorerun hello tutorial**</span></span>

<span data-ttu-id="9ad0c-353">flux de travail toorerun hello, vous devez effectuer hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-353">toorerun hello workflow, you must perform hello following tasks:</span></span>

* <span data-ttu-id="9ad0c-354">Supprimer le fichier de sortie du script hello Hive.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-354">Delete hello Hive script output file.</span></span>
* <span data-ttu-id="9ad0c-355">Suppression des données dans la table de log4jLogsCount hello hello.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-355">Delete hello data in hello log4jLogsCount table.</span></span>

<span data-ttu-id="9ad0c-356">Voici un exemple d'un script Windows PowerShell que vous pouvez utiliser :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="9ad0c-357">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9ad0c-357">Next steps</span></span>
<span data-ttu-id="9ad0c-358">Dans ce didacticiel, vous avez appris comment toodefine Oozie d’un flux de travail et un coordinateur Oozie, et comment toorun Oozie coordinateur de projet à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ad0c-358">In this tutorial, you learned how toodefine an Oozie workflow and an Oozie coordinator, and how toorun an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="9ad0c-359">toolearn, voir hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="9ad0c-359">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="9ad0c-360">[Prise en main de HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="9ad0c-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="9ad0c-361">[Utilisation du stockage d’objets blob Azure avec HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="9ad0c-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="9ad0c-362">[Administration de HDInsight à l'aide d'Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="9ad0c-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="9ad0c-363">[Télécharger des données tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="9ad0c-363">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="9ad0c-364">[Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="9ad0c-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="9ad0c-365">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="9ad0c-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="9ad0c-366">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="9ad0c-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="9ad0c-367">[Développement de programmes MapReduce en Java pour HDInsight][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="9ad0c-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
