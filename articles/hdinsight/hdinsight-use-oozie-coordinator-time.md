---
title: "Utilisation du coordinateur Hadoop Oozie basé sur le temps dans HDInsight | Microsoft Docs"
description: "Utilisez le coordinateur Hadoop Oozie basé sur le temps dans HDInsight, un service pour les données volumineuses. Découvrez comment définir des workflows et des coordinateurs Oozie, et envoyer des tâches."
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
ms.openlocfilehash: 600a70c74a16e2601a874f804ac2e8382c8bfa90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-to-define-workflows-and-coordinate-jobs"></a><span data-ttu-id="2a831-104">Utilisez le coordinateur Oozie basé sur le temps avec Hadoop dans HDInsight pour définir des workflows et coordonner des tâches</span><span class="sxs-lookup"><span data-stu-id="2a831-104">Use time-based Oozie coordinator with Hadoop in HDInsight to define workflows and coordinate jobs</span></span>
<span data-ttu-id="2a831-105">Dans cet article, vous découvrirez comment définir des workflows et des coordinateurs, et comment déclencher les tâches du coordinateur en fonction de l'heure.</span><span class="sxs-lookup"><span data-stu-id="2a831-105">In this article, you'll learn how to define workflows and coordinators, and how to trigger the coordinator jobs, based on time.</span></span> <span data-ttu-id="2a831-106">Il est utile de lire l’article [Utilisation d'Oozie avec HDInsight][hdinsight-use-oozie] avant cet article-ci.</span><span class="sxs-lookup"><span data-stu-id="2a831-106">It is helpful to go through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="2a831-107">En plus d’Oozie, vous pouvez utiliser Azure Data Factory pour programmer des tâches.</span><span class="sxs-lookup"><span data-stu-id="2a831-107">In addition to Oozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="2a831-108">Pour en savoir plus sur Azure Data Factory, consultez la rubrique [Utilisation de Pig et Hive avec Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="2a831-108">To learn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2a831-109">Cet article requiert un cluster HDInsight basé sur Windows.</span><span class="sxs-lookup"><span data-stu-id="2a831-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="2a831-110">Pour plus d’informations sur l’utilisation d’Oozie, notamment sur les travaux à durée définie sur un cluster basé sur Linux, consultez [Utiliser Oozie avec Hadoop pour définir et exécuter un flux de travail dans HDInsight basé sur Linux](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="2a831-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="2a831-111">Présentation d'Oozie</span><span class="sxs-lookup"><span data-stu-id="2a831-111">What is Oozie</span></span>
<span data-ttu-id="2a831-112">Apache Oozie est un système de workflow/coordination qui gère les tâches Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2a831-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="2a831-113">Il est intégré à la pile Hadoop et prend en charge les tâches Hadoop pour Apache MapReduce, Apache Pig, Apache Hive et Apache Sqoop.</span><span class="sxs-lookup"><span data-stu-id="2a831-113">It is integrated with the Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="2a831-114">Il peut également être utilisé pour planifier des tâches propres à un système comme des programmes Java ou des scripts shell.</span><span class="sxs-lookup"><span data-stu-id="2a831-114">It can also be used to schedule jobs that are specific to a system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="2a831-115">L’image suivante montre le workflow que vous allez implémenter :</span><span class="sxs-lookup"><span data-stu-id="2a831-115">The following image shows the workflow you will implement:</span></span>

![Diagramme du workflow][img-workflow-diagram]

<span data-ttu-id="2a831-117">Le workflow contient deux actions :</span><span class="sxs-lookup"><span data-stu-id="2a831-117">The workflow contains two actions:</span></span>

1. <span data-ttu-id="2a831-118">Une action Hive exécute un script HiveQL pour compter les occurrences de chaque type de niveau de journalisation dans un fichier journal log4j.</span><span class="sxs-lookup"><span data-stu-id="2a831-118">A Hive action runs a HiveQL script to count the occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="2a831-119">Chaque journal log4j est constitué d’une ligne de champs qui contient un champ [LOG LEVEL] pour indiquer le type et la gravité, par exemple :</span><span class="sxs-lookup"><span data-stu-id="2a831-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field to show the type and the severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="2a831-120">La sortie du script Hive doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="2a831-120">The Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="2a831-121">Pour plus d’informations sur Hive, consultez l’article [Utilisation de Hive avec HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="2a831-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="2a831-122">Une action Sqoop exporte la sortie de l'action HiveQL vers une table dans la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="2a831-122">A Sqoop action exports the HiveQL action output to a table in an Azure SQL database.</span></span> <span data-ttu-id="2a831-123">Pour plus d'informations sur Sqoop, consultez la rubrique [Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="2a831-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="2a831-124">Pour obtenir la liste des versions Oozie prises en charge sur les clusters HDInsight, consultez la rubrique [Nouveautés des versions de cluster fournies par HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="2a831-124">For supported Oozie versions on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="2a831-125">Prérequis</span><span class="sxs-lookup"><span data-stu-id="2a831-125">Prerequisites</span></span>
<span data-ttu-id="2a831-126">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2a831-126">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="2a831-127">**Un poste de travail sur lequel est installé Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="2a831-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2a831-128">La prise en charge de la gestion des ressources HDInsight par Azure PowerShell à l’aide d’Azure Service Manager est **déconseillée** ; elle sera supprimée le 1er janvier 2017.</span><span class="sxs-lookup"><span data-stu-id="2a831-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="2a831-129">Dans ce document, la procédure repose sur les nouvelles applets de commande HDInsight qui fonctionnent avec Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2a831-129">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="2a831-130">Suivez les étapes indiquées dans [Installation et de configuration d’Azure PowerShell](/powershell/azureps-cmdlets-docs) pour installer la dernière version d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2a831-130">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="2a831-131">Si vous devez modifier certains scripts pour utiliser les nouvelles applets de commande fonctionnant avec Azure Resource Manager, consultez [Migration vers les outils de développement Azure Resource Manager pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="2a831-131">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="2a831-132">**Un cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="2a831-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="2a831-133">Pour plus d’informations sur la création d’un cluster HDInsight, consultez la rubrique ou [Création de clusters HDInsight][hdinsight-provision] ou [Prise en main de HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="2a831-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="2a831-134">Vous aurez besoin des données suivantes pour suivre ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="2a831-134">You will need the following data to go through the tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2a831-135">Propriété du cluster</span><span class="sxs-lookup"><span data-stu-id="2a831-135">Cluster property</span></span></th><th><span data-ttu-id="2a831-136">Nom de la variable Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a831-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="2a831-137">Valeur</span><span class="sxs-lookup"><span data-stu-id="2a831-137">Value</span></span></th><th><span data-ttu-id="2a831-138">Description</span><span class="sxs-lookup"><span data-stu-id="2a831-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2a831-139">Nom du cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a831-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="2a831-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="2a831-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="2a831-141">Cluster HDInsight sur lequel vous exécutez ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2a831-141">The HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a831-142">Nom d'utilisateur du cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a831-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="2a831-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="2a831-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="2a831-144">Nom d'utilisateur de cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a831-144">The HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="2a831-145">Mot de passe de l'utilisateur du cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="2a831-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="2a831-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="2a831-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="2a831-147">Mot de passe de l'utilisateur du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a831-147">The HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a831-148">Nom du compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="2a831-148">Azure storage account name</span></span></td><td><span data-ttu-id="2a831-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="2a831-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="2a831-150">Il s'agit du compte de stockage Azure disponible sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a831-150">An Azure Storage account available to the HDInsight cluster.</span></span> <span data-ttu-id="2a831-151">Pour ce didacticiel, utilisez le compte de stockage par défaut que vous avez indiqué au cours du processus d'approvisionnement du cluster.</span><span class="sxs-lookup"><span data-stu-id="2a831-151">For this tutorial, use the default storage account that you specified during the cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a831-152">Nom du conteneur d'objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="2a831-152">Azure Blob container name</span></span></td><td><span data-ttu-id="2a831-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="2a831-153">$containerName</span></span></td><td></td><td><span data-ttu-id="2a831-154">Dans cet exemple, utilisez le conteneur de stockage d'objets blob Azure utilisé pour le système de fichiers de cluster HDInsight par défaut.</span><span class="sxs-lookup"><span data-stu-id="2a831-154">For this example, use the Azure Blob storage container that is used for the default HDInsight cluster file system.</span></span> <span data-ttu-id="2a831-155">Par défaut, il porte le même nom que le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a831-155">By default, it has the same name as the HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="2a831-156">
* **Une base de données SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="2a831-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="2a831-157">Vous devez configurer une règle de pare-feu pour que le serveur de base de données SQL autorise l'accès à partir de votre poste de travail.</span><span class="sxs-lookup"><span data-stu-id="2a831-157">You must configure a firewall rule for the SQL Database server to allow access from your workstation.</span></span> <span data-ttu-id="2a831-158">Pour des instructions sur la création d’une base de données SQL Azure et la configuration d’un pare-feu, consultez la rubrique [Prise en main de la base de données SQL Azure][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="2a831-158">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="2a831-159">Cet article inclut un script Windows PowerShell pour la création de la table de base de données SQL Azure dont vous avez besoin pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2a831-159">This article provides a Windows PowerShell script for creating the Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2a831-160">Propriété de base de données SQL</span><span class="sxs-lookup"><span data-stu-id="2a831-160">SQL database property</span></span></th><th><span data-ttu-id="2a831-161">Nom de la variable Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a831-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="2a831-162">Valeur</span><span class="sxs-lookup"><span data-stu-id="2a831-162">Value</span></span></th><th><span data-ttu-id="2a831-163">Description</span><span class="sxs-lookup"><span data-stu-id="2a831-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2a831-164">Nom du serveur de base de données SQL</span><span class="sxs-lookup"><span data-stu-id="2a831-164">SQL database server name</span></span></td><td><span data-ttu-id="2a831-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="2a831-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="2a831-166">Serveur de la base de données SQL vers lequel Sqoop exporte des données.</span><span class="sxs-lookup"><span data-stu-id="2a831-166">The SQL database server to which Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="2a831-167">Nom de connexion à la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="2a831-167">SQL database login name</span></span></td><td><span data-ttu-id="2a831-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="2a831-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="2a831-169">Nom de connexion à la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="2a831-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a831-170">Mot de passe de connexion à la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="2a831-170">SQL database login password</span></span></td><td><span data-ttu-id="2a831-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="2a831-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="2a831-172">Mot de passe de connexion à la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="2a831-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a831-173">Nom de la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="2a831-173">SQL database name</span></span></td><td><span data-ttu-id="2a831-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="2a831-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="2a831-175">Base de données SQL Azure vers laquelle Sqoop exporte des données.</span><span class="sxs-lookup"><span data-stu-id="2a831-175">The Azure SQL database to which Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="2a831-176">Par défaut, une base de données SQL Azure autorise des connexions aux services Azure tels que Azure HDinsight.</span><span class="sxs-lookup"><span data-stu-id="2a831-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="2a831-177">Si ce paramètre de pare-feu est désactivé, vous devez l’activer depuis le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2a831-177">If this firewall setting is disabled, you must enable it from the Azure Portal.</span></span> <span data-ttu-id="2a831-178">Pour obtenir des instructions sur la création d'une base de données SQL et la configuration des règles de pare-feu, consultez la rubrique [Création et configuration d'une base de données SQL][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="2a831-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="2a831-179">Remplissez les valeurs dans les tables.</span><span class="sxs-lookup"><span data-stu-id="2a831-179">Fill-in the values in the tables.</span></span> <span data-ttu-id="2a831-180">Cela vous sera utile pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2a831-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-the-related-hiveql-script"></a><span data-ttu-id="2a831-181">Définition du workflow Oozie et du script HiveQL lié</span><span class="sxs-lookup"><span data-stu-id="2a831-181">Define Oozie workflow and the related HiveQL script</span></span>
<span data-ttu-id="2a831-182">Les définitions des workflows Oozie sont écrites en hPDL (un langage de définition du processus XML).</span><span class="sxs-lookup"><span data-stu-id="2a831-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="2a831-183">Le nom du fichier de workflow par défaut est *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="2a831-183">The default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="2a831-184">Enregistrez le fichier de workflow en local et déployez-le ensuite sur le cluster HDInsight en utilisant Windows PowerShell plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2a831-184">You will save the workflow file locally, and then deploy it to the HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="2a831-185">L'action Hive dans le workflow appelle un fichier de script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="2a831-185">The Hive action in the workflow calls a HiveQL script file.</span></span> <span data-ttu-id="2a831-186">Le fichier de script contient trois instructions HiveQL :</span><span class="sxs-lookup"><span data-stu-id="2a831-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="2a831-187">**L'instruction DROP TABLE** supprime la table Hive log4j si elle existe.</span><span class="sxs-lookup"><span data-stu-id="2a831-187">**The DROP TABLE statement** deletes the log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="2a831-188">**L'instruction CREATE TABLE** crée une table externe Hive log4j pointant vers l'emplacement du fichier journal log4j.</span><span class="sxs-lookup"><span data-stu-id="2a831-188">**The CREATE TABLE statement** creates a log4j Hive external table, which points to the location of the log4j log file;</span></span>
3. <span data-ttu-id="2a831-189">**L'emplacement du fichier journal log4j**.</span><span class="sxs-lookup"><span data-stu-id="2a831-189">**The location of the log4j log file**.</span></span> <span data-ttu-id="2a831-190">Le séparateur de champ est « , ».</span><span class="sxs-lookup"><span data-stu-id="2a831-190">The field delimiter is ",".</span></span> <span data-ttu-id="2a831-191">Le séparateur de ligne par défaut est « \n ».</span><span class="sxs-lookup"><span data-stu-id="2a831-191">The default line delimiter is "\n".</span></span> <span data-ttu-id="2a831-192">La table externe Hive est utilisée pour éviter que le fichier de données soit supprimé de son emplacement d'origine au cas où vous souhaiteriez exécuter à plusieurs reprises le workflow Oozie.</span><span class="sxs-lookup"><span data-stu-id="2a831-192">A Hive external table is used to avoid the data file being removed from the original location, in case you want to run the Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="2a831-193">**L'instruction INSERT OVERWRITE** compte les occurrences de chaque type de niveau de journalisation à partir de la table Hive log4j et enregistre la sortie dans un emplacement de stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="2a831-193">**The INSERT OVERWRITE statement** counts the occurrences of each log-level type from the log4j Hive table, and it saves the output to an Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="2a831-194">Il existe un problème connu de chemin d'accès à Hive.</span><span class="sxs-lookup"><span data-stu-id="2a831-194">There is a known Hive path issue.</span></span> <span data-ttu-id="2a831-195">Vous le rencontrez lors de l'envoi d'une tâche Oozie.</span><span class="sxs-lookup"><span data-stu-id="2a831-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="2a831-196">Les instructions permettant d'y remédier sont disponibles dans le Wiki TechNet : [Erreur Hive HDInsight : impossible de renommer][technetwiki-hive-error].</span><span class="sxs-lookup"><span data-stu-id="2a831-196">The instructions for fixing the issue can be found on the TechNet Wiki: [HDInsight Hive error: Unable to rename][technetwiki-hive-error].</span></span>

<span data-ttu-id="2a831-197">**Définition du fichier de script HiveQL appelé par le workflow**</span><span class="sxs-lookup"><span data-stu-id="2a831-197">**To define the HiveQL script file to be called by the workflow**</span></span>

1. <span data-ttu-id="2a831-198">Créez un fichier texte avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="2a831-198">Create a text file with the following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="2a831-199">Voici les trois variables utilisées dans le script :</span><span class="sxs-lookup"><span data-stu-id="2a831-199">There are three variables used in the script:</span></span>

   * <span data-ttu-id="2a831-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="2a831-200">${hiveTableName}</span></span>
   * <span data-ttu-id="2a831-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="2a831-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="2a831-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="2a831-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="2a831-203">Le fichier de définition du workflow (workflow.xml dans ce didacticiel) transmet ces valeurs à ce script HiveQL au moment de l'exécution.</span><span class="sxs-lookup"><span data-stu-id="2a831-203">The workflow definition file (workflow.xml in this tutorial) will pass these values to this HiveQL script at run time.</span></span>
2. <span data-ttu-id="2a831-204">Enregistrez le fichier sous **C:\Tutorials\UseOozie\useooziewf.hql** en utilisant l’encodage ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="2a831-204">Save the file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="2a831-205">(Utilisez le Bloc-notes si votre éditeur de texte ne dispose pas de cette option.) Le fichier de script est déployé sur le cluster HDInsight plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2a831-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed to the HDInsight cluster later in the tutorial.</span></span>

<span data-ttu-id="2a831-206">**Définition d'un workflow**</span><span class="sxs-lookup"><span data-stu-id="2a831-206">**To define a workflow**</span></span>

1. <span data-ttu-id="2a831-207">Créez un fichier texte avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="2a831-207">Create a text file with the following content:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start to = "RunHiveScript"/>

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

    <span data-ttu-id="2a831-208">Voici les deux actions définies dans le workflow :</span><span class="sxs-lookup"><span data-stu-id="2a831-208">There are two actions defined in the workflow.</span></span> <span data-ttu-id="2a831-209">l'action de démarrage est *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="2a831-209">The start-to action is *RunHiveScript*.</span></span> <span data-ttu-id="2a831-210">Si cette action fonctionne *correctement*, l'action suivante est *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="2a831-210">If the action runs *OK*, the next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="2a831-211">RunHiveScript a plusieurs variables.</span><span class="sxs-lookup"><span data-stu-id="2a831-211">The RunHiveScript has several variables.</span></span> <span data-ttu-id="2a831-212">Vous transmettez ces valeurs lors de l'envoi de la tâche Oozie à partir de votre poste de travail en utilisant Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2a831-212">You will pass the values when you submit the Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="2a831-213">Variable de workflow</span><span class="sxs-lookup"><span data-stu-id="2a831-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2a831-214">Variable de workflow</span><span class="sxs-lookup"><span data-stu-id="2a831-214">Workflow variables</span></span></th><th><span data-ttu-id="2a831-215">Description</span><span class="sxs-lookup"><span data-stu-id="2a831-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2a831-216">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="2a831-216">${jobTracker}</span></span></td><td><span data-ttu-id="2a831-217">Spécifie l'URL du suivi des tâches Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2a831-217">Specify the URL of the Hadoop job tracker.</span></span> <span data-ttu-id="2a831-218">Utilisez <strong>jobtrackerhost:9010</strong> sur les versions 3.0 et 2.0 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a831-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a831-219">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="2a831-219">${nameNode}</span></span></td><td><span data-ttu-id="2a831-220">Spécifie l'URL du nœud de nom Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2a831-220">Specify the URL of the Hadoop name node.</span></span> <span data-ttu-id="2a831-221">Utilisez l’adresse wasb:// du système de fichiers par défaut, par exemple <i>wasb://&lt;nom_conteneur&gt;@&lt;nom_compte_de_stockage&gt;.blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="2a831-221">Use the default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a831-222">${queueName}</span><span class="sxs-lookup"><span data-stu-id="2a831-222">${queueName}</span></span></td><td><span data-ttu-id="2a831-223">Spécifie le nom de la file d’attente auquel est envoyée la tâche.</span><span class="sxs-lookup"><span data-stu-id="2a831-223">Specifies the queue name that the job will be submitted to.</span></span> <span data-ttu-id="2a831-224">Utilisez <strong>Default</strong>.</span><span class="sxs-lookup"><span data-stu-id="2a831-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="2a831-225">Variables de l'action Hive</span><span class="sxs-lookup"><span data-stu-id="2a831-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2a831-226">Variable d'action Hive</span><span class="sxs-lookup"><span data-stu-id="2a831-226">Hive action variable</span></span></th><th><span data-ttu-id="2a831-227">Description</span><span class="sxs-lookup"><span data-stu-id="2a831-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2a831-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="2a831-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="2a831-229">Répertoire source pour la commande Hive de création d'une table.</span><span class="sxs-lookup"><span data-stu-id="2a831-229">The source directory for the Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a831-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="2a831-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="2a831-231">Dossier de sortie pour l'instruction INSERT OVERWRITE.</span><span class="sxs-lookup"><span data-stu-id="2a831-231">The output folder for the INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a831-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="2a831-232">${hiveTableName}</span></span></td><td><span data-ttu-id="2a831-233">Nom de la table Hive référençant les fichiers de données log4j.</span><span class="sxs-lookup"><span data-stu-id="2a831-233">The name of the Hive table that references the log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="2a831-234">Variables d'action Sqoop</span><span class="sxs-lookup"><span data-stu-id="2a831-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="2a831-235">Variable d'action Sqoop</span><span class="sxs-lookup"><span data-stu-id="2a831-235">Sqoop action variable</span></span></th><th><span data-ttu-id="2a831-236">Description</span><span class="sxs-lookup"><span data-stu-id="2a831-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="2a831-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="2a831-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="2a831-238">Chaîne de connexion à la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="2a831-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a831-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="2a831-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="2a831-240">Table de la base de données SQL Azure vers laquelle les données sont exportées.</span><span class="sxs-lookup"><span data-stu-id="2a831-240">The Azure SQL database table to where the data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="2a831-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="2a831-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="2a831-242">Dossier de sortie pour l'instruction INSERT OVERWRITE de Hive.</span><span class="sxs-lookup"><span data-stu-id="2a831-242">The output folder for the Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="2a831-243">Il s'agit du même dossier pour Sqoop Export (export-dir).</span><span class="sxs-lookup"><span data-stu-id="2a831-243">This is the same folder for the Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="2a831-244">Pour plus d'informations sur le workflow Oozie et l'utilisation des actions de workflow, consultez la rubrique [Documentation sur Apache Oozie 4.0][apache-oozie-400] (pour la version 3.0 du cluster HDInsight) ou [Documentation sur Apache Oozie 3.3.2][apache-oozie-332] (pour la version 2.1 du cluster HDInsight).</span><span class="sxs-lookup"><span data-stu-id="2a831-244">For more information about Oozie workflow and using the workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="2a831-245">Enregistrez le fichier sous **C:\Tutorials\UseOozie\workflow.xml** en utilisant l'encodage ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="2a831-245">Save the file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="2a831-246">(Utilisez le Bloc-notes si votre éditeur de texte ne dispose pas de cette option.)</span><span class="sxs-lookup"><span data-stu-id="2a831-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="2a831-247">**Définition du coordinateur**</span><span class="sxs-lookup"><span data-stu-id="2a831-247">**To define coordinator**</span></span>

1. <span data-ttu-id="2a831-248">Créez un fichier texte avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="2a831-248">Create a text file with the following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="2a831-249">Ce fichier de définition comporte cinq variables :</span><span class="sxs-lookup"><span data-stu-id="2a831-249">There are five variables used in the definition file:</span></span>

   | <span data-ttu-id="2a831-250">Variable</span><span class="sxs-lookup"><span data-stu-id="2a831-250">Variable</span></span> | <span data-ttu-id="2a831-251">Description</span><span class="sxs-lookup"><span data-stu-id="2a831-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="2a831-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="2a831-252">${coordFrequency}</span></span> |<span data-ttu-id="2a831-253">Heure de pause de la tâche.</span><span class="sxs-lookup"><span data-stu-id="2a831-253">Job pause time.</span></span> <span data-ttu-id="2a831-254">La fréquence est toujours exprimée en minutes.</span><span class="sxs-lookup"><span data-stu-id="2a831-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="2a831-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="2a831-255">${coordStart}</span></span> |<span data-ttu-id="2a831-256">Heure de début de la tâche.</span><span class="sxs-lookup"><span data-stu-id="2a831-256">Job start time.</span></span> |
   | <span data-ttu-id="2a831-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="2a831-257">${coordEnd}</span></span> |<span data-ttu-id="2a831-258">Heure de fin de la tâche.</span><span class="sxs-lookup"><span data-stu-id="2a831-258">Job end time.</span></span> |
   | <span data-ttu-id="2a831-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="2a831-259">${coordTimezone}</span></span> |<span data-ttu-id="2a831-260">Oozie traite les tâches du coordinateur dans un fuseau horaire fixe sans passage à l’heure d’été (généralement représenté à l'aide de UTC).</span><span class="sxs-lookup"><span data-stu-id="2a831-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="2a831-261">Ce fuseau horaire est appelé le « fuseau horaire du traitement d’Oozie ».</span><span class="sxs-lookup"><span data-stu-id="2a831-261">This time zone is referred as the "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="2a831-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="2a831-262">${wfPath}</span></span> |<span data-ttu-id="2a831-263">Le chemin d'accès de workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="2a831-263">The path for the workflow.xml.</span></span>  <span data-ttu-id="2a831-264">Si le nom du fichier de workflow n'est pas celui par défaut (workflow.xml), vous devez le spécifier.</span><span class="sxs-lookup"><span data-stu-id="2a831-264">If the workflow file name is not the default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="2a831-265">Enregistrez le fichier sous **C:\Tutorials\UseOozie\coordinator.xml** en utilisant l'encodage ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="2a831-265">Save the file as **C:\Tutorials\UseOozie\coordinator.xml** by using the ANSI (ASCII) encoding.</span></span> <span data-ttu-id="2a831-266">(Utilisez le Bloc-notes si votre éditeur de texte ne dispose pas de cette option.)</span><span class="sxs-lookup"><span data-stu-id="2a831-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-the-oozie-project-and-prepare-the-tutorial"></a><span data-ttu-id="2a831-267">Déploiement du projet Oozie et préparation du didacticiel</span><span class="sxs-lookup"><span data-stu-id="2a831-267">Deploy the Oozie project and prepare the tutorial</span></span>
<span data-ttu-id="2a831-268">Exécutez un script Azure PowerShell pour effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2a831-268">You will run an Azure PowerShell script to perform the following:</span></span>

* <span data-ttu-id="2a831-269">Copie du script HiveQL (useoozie.hql) dans le stockage d’objets blob Azure, wasb:///tutorials/useoozie/useoozie.hql.</span><span class="sxs-lookup"><span data-stu-id="2a831-269">Copy the HiveQL script (useoozie.hql) to Azure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="2a831-270">Copie de workflow.xml dans wasb:///tutorials/useoozie/workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="2a831-270">Copy workflow.xml to wasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="2a831-271">Copie de coordinator.xml dans wasb:///tutorials/useoozie/coordinator.xml.</span><span class="sxs-lookup"><span data-stu-id="2a831-271">Copy coordinator.xml to wasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="2a831-272">Copie du fichier de données (/example/data/sample.log) dans wasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="2a831-272">Copy the data file (/example/data/sample.log) to wasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="2a831-273">Créer une table de base de données SQL Azure pour stocker les données d'exportation de Sqoop.</span><span class="sxs-lookup"><span data-stu-id="2a831-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="2a831-274">Le nom de la table est *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="2a831-274">The table name is *log4jLogCount*.</span></span>

<span data-ttu-id="2a831-275">**Présentation du stockage HDInsight**</span><span class="sxs-lookup"><span data-stu-id="2a831-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="2a831-276">HDInsight utilise le stockage d’objets blob Azure pour stocker les données.</span><span class="sxs-lookup"><span data-stu-id="2a831-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="2a831-277">wasb:// est l’implémentation Microsoft du système de fichiers distribués Hadoop (HDFS) dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="2a831-277">wasb:// is Microsoft's implementation of the Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="2a831-278">Pour plus d'informations, consultez la rubrique [Utilisation du stockage d'objets blob Azure avec HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="2a831-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="2a831-279">Lors de l'approvisionnement d'un cluster HDInsight, un compte Azure Storage et un conteneur spécifique de ce compte sont désignés en tant que système de fichiers par défaut, comme dans HDFS.</span><span class="sxs-lookup"><span data-stu-id="2a831-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as the default file system, like in HDFS.</span></span> <span data-ttu-id="2a831-280">En plus de ce compte de stockage, pendant le processus d’approvisionnement, vous pouvez ajouter des comptes de stockage supplémentaires à partir du même abonnement Azure ou à partir d’autres abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="2a831-280">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or from different Azure subscriptions during the provisioning process.</span></span> <span data-ttu-id="2a831-281">Pour plus d'instructions sur l’ajout des comptes de stockage supplémentaires, consultez la rubrique [Approvisionnement de clusters HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="2a831-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="2a831-282">Pour simplifier le script Azure PowerShell utilisé dans ce didacticiel, tous les fichiers sont stockés dans le conteneur de système de fichiers par défaut, à l'emplacement */tutorials/useoozie*.</span><span class="sxs-lookup"><span data-stu-id="2a831-282">To simplify the Azure PowerShell script used in this tutorial, all of the files are stored in the default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="2a831-283">Par défaut, ce conteneur porte le même nom que le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2a831-283">By default, this container has the same name as the HDInsight cluster name.</span></span>
<span data-ttu-id="2a831-284">La syntaxe est :</span><span class="sxs-lookup"><span data-stu-id="2a831-284">The syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="2a831-285">Seule la syntaxe *wasb://* est prise en charge dans le cluster HDInsight version 3.0.</span><span class="sxs-lookup"><span data-stu-id="2a831-285">Only the *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="2a831-286">L’ancienne syntaxe *asv://* est prise en charge dans les clusters HDInsight 2.1 et 1.6, mais elle n’est pas prise en charge dans les clusters HDInsight 3.0.</span><span class="sxs-lookup"><span data-stu-id="2a831-286">The older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="2a831-287">Le chemin d'accès wasb:// est un chemin d'accès virtuel.</span><span class="sxs-lookup"><span data-stu-id="2a831-287">The wasb:// path is a virtual path.</span></span> <span data-ttu-id="2a831-288">Pour plus d'informations, consultez la rubrique [Utilisation du stockage d'objets blob Azure avec HDInsight][hdinsight-storage] .</span><span class="sxs-lookup"><span data-stu-id="2a831-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="2a831-289">Vous pouvez accéder à un fichier stocké dans le conteneur du système de fichiers par défaut à partir de HDInsight en utilisant l'un des URI suivants (workflow.xml est utilisé comme exemple) :</span><span class="sxs-lookup"><span data-stu-id="2a831-289">A file that is stored in the default file system container can be accessed from HDInsight by using any of the following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="2a831-290">Pour accéder directement au fichier à partir du compte de stockage, le nom de l'objet blob du fichier est :</span><span class="sxs-lookup"><span data-stu-id="2a831-290">If you want to access the file directly from the storage account, the blob name for the file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="2a831-291">**Présentation des tables interne et externe Hive**</span><span class="sxs-lookup"><span data-stu-id="2a831-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="2a831-292">Voici quelques éléments à connaître sur les tables interne et externe Hive :</span><span class="sxs-lookup"><span data-stu-id="2a831-292">There are a few things you need to know about Hive internal and external tables:</span></span>

* <span data-ttu-id="2a831-293">La commande CREATE TABLE crée une table interne, également nommée table gérée.</span><span class="sxs-lookup"><span data-stu-id="2a831-293">The CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="2a831-294">Le fichier de données doit se trouver dans le conteneur par défaut.</span><span class="sxs-lookup"><span data-stu-id="2a831-294">The data file must be located in the default container.</span></span>
* <span data-ttu-id="2a831-295">La commande CREATE TABLE déplace le fichier de données vers le dossier /hive/warehouse/<TableName> dans le conteneur par défaut.</span><span class="sxs-lookup"><span data-stu-id="2a831-295">The CREATE TABLE command moves the data file to the /hive/warehouse/<TableName> folder in the default container.</span></span>
* <span data-ttu-id="2a831-296">La commande CREATE EXTERNAL TABLE permet de créer une table externe.</span><span class="sxs-lookup"><span data-stu-id="2a831-296">The CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="2a831-297">Le fichier de données peut se trouver à l'extérieur du conteneur par défaut.</span><span class="sxs-lookup"><span data-stu-id="2a831-297">The data file can be located outside the default container.</span></span>
* <span data-ttu-id="2a831-298">La commande CREATE EXTERNAL TABLE ne déplace pas le fichier de données.</span><span class="sxs-lookup"><span data-stu-id="2a831-298">The CREATE EXTERNAL TABLE command does not move the data file.</span></span>
* <span data-ttu-id="2a831-299">La commande CREATE EXTERNAL TABLE n'autorise aucun sous-dossier dans le dossier spécifié dans la clause LOCATION.</span><span class="sxs-lookup"><span data-stu-id="2a831-299">The CREATE EXTERNAL TABLE command doesn't allow any subfolders under the folder that is specified in the LOCATION clause.</span></span> <span data-ttu-id="2a831-300">C'est la raison pour laquelle le didacticiel réalise une copie du fichier sample.log.</span><span class="sxs-lookup"><span data-stu-id="2a831-300">This is the reason why the tutorial makes a copy of the sample.log file.</span></span>

<span data-ttu-id="2a831-301">Pour plus d’informations, consultez la rubrique [HDInsight : introduction aux tables interne et externe Hive][cindygross-hive-tables].</span><span class="sxs-lookup"><span data-stu-id="2a831-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="2a831-302">**Préparation du didacticiel**</span><span class="sxs-lookup"><span data-stu-id="2a831-302">**To prepare the tutorial**</span></span>

1. <span data-ttu-id="2a831-303">Ouvrez Windows PowerShell ISE (dans l'écran d'accueil Windows 8, tapez **PowerShell_ISE**, puis cliquez sur **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="2a831-303">Open the Windows PowerShell ISE (in the Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="2a831-304">Pour plus d'informations, consultez la page [Démarrage de Windows PowerShell sur Windows 8 et Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="2a831-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="2a831-305">Dans le volet inférieur, exécutez la commande suivante pour vous connecter à votre abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="2a831-305">In the bottom pane, run the following command to connect to your Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="2a831-306">Vous êtes invité à entrer les informations d'identification de votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="2a831-306">You will be prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="2a831-307">Cette méthode d'ajout de la connexion d'abonnement expire, et vous devez réexécuter l’applet de commande au bout de 12 heures.</span><span class="sxs-lookup"><span data-stu-id="2a831-307">This method of adding a subscription connection times out, and after 12 hours, you will have to run the cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2a831-308">Si vous disposez de plusieurs abonnements Azure et que vous ne souhaitez pas utiliser l’abonnement défini par défaut, utilisez l’applet de commande <strong>Select-AzureSubscription</strong> pour sélectionner un abonnement.</span><span class="sxs-lookup"><span data-stu-id="2a831-308">If you have multiple Azure subscriptions and the default subscription is not the one you want to use, use the <strong>Select-AzureSubscription</strong> cmdlet to select a subscription.</span></span>

3. <span data-ttu-id="2a831-309">Copiez le script suivant dans le volet de script, puis définissez les six premières variables :</span><span class="sxs-lookup"><span data-stu-id="2a831-309">Copy the following script into the script pane, and then set the first six variables:</span></span>

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

    # Oozie files for the tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing the Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use the long path here
    ```

    <span data-ttu-id="2a831-310">Pour plus d'informations sur les variables, consultez la section [Conditions préalables](#prerequisites) de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2a831-310">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="2a831-311">Ajoutez ce qui suit au script dans le volet de script :</span><span class="sxs-lookup"><span data-stu-id="2a831-311">Append the following to the script in the script pane:</span></span>

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
        Write-Host "Make a copy of the sample.log file ... " -ForegroundColor Green
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

        #Create the log4jLogsCount table
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

    # make a copy of example/data/sample.log to example/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="2a831-312">Cliquez sur **Exécuter le script** ou appuyez sur **F5** pour exécuter le script.</span><span class="sxs-lookup"><span data-stu-id="2a831-312">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="2a831-313">La sortie doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="2a831-313">The output will be similar to:</span></span>

    ![Sortie de la préparation du didacticiel][img-preparation-output]

## <a name="run-the-oozie-project"></a><span data-ttu-id="2a831-315">Exécution du projet Oozie</span><span class="sxs-lookup"><span data-stu-id="2a831-315">Run the Oozie project</span></span>
<span data-ttu-id="2a831-316">Azure PowerShell ne fournit actuellement aucune applet de commande pour la définition de tâches Oozie.</span><span class="sxs-lookup"><span data-stu-id="2a831-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="2a831-317">Vous pouvez utiliser l’applet de commande **Invoke-RestMethod** pour appeler les services web Oozie.</span><span class="sxs-lookup"><span data-stu-id="2a831-317">You can use the **Invoke-RestMethod** cmdlet to invoke Oozie web services.</span></span> <span data-ttu-id="2a831-318">L'API des services web Oozie est une API JSON REST HTTP.</span><span class="sxs-lookup"><span data-stu-id="2a831-318">The Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="2a831-319">Pour plus d'informations sur l'API des services web Oozie, consultez la page [Documentation sur Apache Oozie 4.0][apache-oozie-400] (pour la version 3.0 du cluster HDInsight) ou [Documentation sur Apache Oozie 3.3.2][apache-oozie-332] (pour la version 2.1 du cluster HDInsight).</span><span class="sxs-lookup"><span data-stu-id="2a831-319">For more information about the Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="2a831-320">**Envoi d'une tâche Oozie**</span><span class="sxs-lookup"><span data-stu-id="2a831-320">**To submit an Oozie job**</span></span>

1. <span data-ttu-id="2a831-321">Ouvrez Windows PowerShell ISE (dans l'écran d'accueil Windows 8, tapez **PowerShell_ISE**, puis cliquez sur **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="2a831-321">Open the Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="2a831-322">Pour plus d'informations, consultez la page [Démarrage de Windows PowerShell sur Windows 8 et Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="2a831-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="2a831-323">Copiez le script qui suit dans le volet de script et définissez les quatorze premières variables (sauf la variable **$storageUri**).</span><span class="sxs-lookup"><span data-stu-id="2a831-323">Copy the following script into the script pane, and then set the first fourteen variables (however, skip **$storageUri**).</span></span>

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

    $oozieWFPath="$storageUri/tutorials/useoozie"  # The default name is workflow.xml. And you don't need to specify the file name.
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

    <span data-ttu-id="2a831-324">Pour plus d'informations sur les variables, consultez la section [Conditions préalables](#prerequisites) de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2a831-324">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="2a831-325">$coordstart et $coordend représentent l'heure de début et de fin du workflow.</span><span class="sxs-lookup"><span data-stu-id="2a831-325">$coordstart and $coordend are the workflow starting and ending time.</span></span> <span data-ttu-id="2a831-326">Pour connaître l'heure UTC/GMT, recherchez « heure utc » sur bing.com. La valeur de $coordFrequency est la fréquence en minutes à laquelle vous voulez exécuter le workflow.</span><span class="sxs-lookup"><span data-stu-id="2a831-326">To find out the UTC/GMT time, search "utc time" on bing.com. The $coordFrequency is how often in minutes you want to run the workflow.</span></span>
3. <span data-ttu-id="2a831-327">Ajoutez ce qui suit au script :</span><span class="sxs-lookup"><span data-stu-id="2a831-327">Append the following to the script.</span></span> <span data-ttu-id="2a831-328">Cette partie définit la charge utile d'Oozie :</span><span class="sxs-lookup"><span data-stu-id="2a831-328">This part defines the Oozie payload:</span></span>

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
   > <span data-ttu-id="2a831-329">La principale différence avec le fichier de charge utile d'envoi du workflow est la variable **oozie.coord.application.path**.</span><span class="sxs-lookup"><span data-stu-id="2a831-329">The major difference compared to the workflow submission payload file is the variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="2a831-330">Lors de l'envoi d'une tâche de workflow, vous utilisez **oozie.wf.application.path** .</span><span class="sxs-lookup"><span data-stu-id="2a831-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="2a831-331">Ajoutez ce qui suit au script :</span><span class="sxs-lookup"><span data-stu-id="2a831-331">Append the following to the script.</span></span> <span data-ttu-id="2a831-332">Cette partie vérifie l'état du service Web Oozie :</span><span class="sxs-lookup"><span data-stu-id="2a831-332">This part checks the Oozie web service status:</span></span>

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
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check the server status and re-run the job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="2a831-333">Ajoutez ce qui suit au script :</span><span class="sxs-lookup"><span data-stu-id="2a831-333">Append the following to the script.</span></span> <span data-ttu-id="2a831-334">Cette partie crée une tâche Oozie :</span><span class="sxs-lookup"><span data-stu-id="2a831-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending the following Payload to the cluster:" -ForegroundColor Green
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
   > <span data-ttu-id="2a831-335">Lors de l'envoi d'une tâche de workflow, vous devez passer un autre appel de services web pour démarrer la tâche une fois qu'elle est créée.</span><span class="sxs-lookup"><span data-stu-id="2a831-335">When you submit a workflow job, you must make another web service call to start the job after the job is created.</span></span> <span data-ttu-id="2a831-336">Dans ce cas, la tâche du coordinateur est déclenchée par l'heure.</span><span class="sxs-lookup"><span data-stu-id="2a831-336">In this case, the coordinator job is triggered by time.</span></span> <span data-ttu-id="2a831-337">La tâche va démarrer automatiquement.</span><span class="sxs-lookup"><span data-stu-id="2a831-337">The job will start automatically.</span></span>

6. <span data-ttu-id="2a831-338">Ajoutez ce qui suit au script :</span><span class="sxs-lookup"><span data-stu-id="2a831-338">Append the following to the script.</span></span> <span data-ttu-id="2a831-339">Cette partie vérifie le statut de la tâche Oozie :</span><span class="sxs-lookup"><span data-stu-id="2a831-339">This part checks the Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until the job metadata is populated in the Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for the job to complete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for the job to complete..."
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

7. <span data-ttu-id="2a831-340">(Facultatif) Ajoutez ce qui suit au script :</span><span class="sxs-lookup"><span data-stu-id="2a831-340">(Optional) Append the following to the script.</span></span>

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
        Write-Host "Killing the Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for the 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="2a831-341">Ajoutez ce qui suit au script :</span><span class="sxs-lookup"><span data-stu-id="2a831-341">Append the following to the script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="2a831-342">Supprimez les signes # si vous souhaitez exécuter d'autres fonctions.</span><span class="sxs-lookup"><span data-stu-id="2a831-342">Remove the # signs if you want to run the additional functions.</span></span>
9. <span data-ttu-id="2a831-343">Si vous disposez du cluster HDInsight version 2.1, remplacez « https://$clusterName.azurehdinsight.net:443/oozie/v2/ » par « https://$clusterName.azurehdinsight.net:443/oozie/v1/ ».</span><span class="sxs-lookup"><span data-stu-id="2a831-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="2a831-344">Le cluster HDInsight version 2.1 ne prend pas en charge la version 2 des services Web.</span><span class="sxs-lookup"><span data-stu-id="2a831-344">HDInsight cluster version 2.1 does not supports version 2 of the web services.</span></span>
10. <span data-ttu-id="2a831-345">Cliquez sur **Exécuter le script** ou appuyez sur **F5** pour exécuter le script.</span><span class="sxs-lookup"><span data-stu-id="2a831-345">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="2a831-346">La sortie doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="2a831-346">The output will be similar to:</span></span>

     ![Sortie du workflow exécuté par le didacticiel][img-runworkflow-output]
11. <span data-ttu-id="2a831-348">Connectez-vous à votre base de données SQL pour voir les données exportées.</span><span class="sxs-lookup"><span data-stu-id="2a831-348">Connect to your SQL Database to see the exported data.</span></span>

<span data-ttu-id="2a831-349">**Vérification du journal des erreurs de la tâche**</span><span class="sxs-lookup"><span data-stu-id="2a831-349">**To check the job error log**</span></span>

<span data-ttu-id="2a831-350">Pour résoudre les problèmes d'un workflow, vous pouvez consulter le fichier journal Oozie dans C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log depuis le nœud principal du cluster.</span><span class="sxs-lookup"><span data-stu-id="2a831-350">To troubleshoot a workflow, the Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from the cluster headnode.</span></span> <span data-ttu-id="2a831-351">Pour plus d’informations sur le protocole RDP, consultez la rubrique [Administration de clusters HDInsight à l’aide du portail Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="2a831-351">For information on RDP, see [Administering HDInsight clusters using the Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="2a831-352">**Réexécution du didacticiel**</span><span class="sxs-lookup"><span data-stu-id="2a831-352">**To rerun the tutorial**</span></span>

<span data-ttu-id="2a831-353">Pour réexécuter le workflow, vous devez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2a831-353">To rerun the workflow, you must perform the following tasks:</span></span>

* <span data-ttu-id="2a831-354">Suppression du fichier de sortie du script Hive.</span><span class="sxs-lookup"><span data-stu-id="2a831-354">Delete the Hive script output file.</span></span>
* <span data-ttu-id="2a831-355">Suppression des données dans la table log4jLogsCount.</span><span class="sxs-lookup"><span data-stu-id="2a831-355">Delete the data in the log4jLogsCount table.</span></span>

<span data-ttu-id="2a831-356">Voici un exemple d'un script Windows PowerShell que vous pouvez utiliser :</span><span class="sxs-lookup"><span data-stu-id="2a831-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete the Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all the records from the log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="2a831-357">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2a831-357">Next steps</span></span>
<span data-ttu-id="2a831-358">Dans ce didacticiel, vous avez appris à définir un workflow Oozie et un coordinateur Oozie, et à exécuter une tâche de coordinateur Oozie en utilisant Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2a831-358">In this tutorial, you learned how to define an Oozie workflow and an Oozie coordinator, and how to run an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="2a831-359">Pour en savoir plus, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="2a831-359">To learn more, see the following articles:</span></span>

* <span data-ttu-id="2a831-360">[Prise en main de HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="2a831-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="2a831-361">[Utilisation du stockage d’objets blob Azure avec HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="2a831-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="2a831-362">[Administration de HDInsight à l'aide d'Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="2a831-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="2a831-363">[Téléchargement de données vers HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="2a831-363">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="2a831-364">[Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="2a831-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="2a831-365">[Utilisation de Hive avec HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="2a831-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="2a831-366">[Utilisation de Pig avec HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="2a831-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="2a831-367">[Développement de programmes MapReduce en Java pour HDInsight][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="2a831-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

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
