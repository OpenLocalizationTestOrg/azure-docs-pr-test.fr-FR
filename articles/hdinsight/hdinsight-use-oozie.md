---
title: aaaUse Hadoop Oozie dans HDInsight | Documents Microsoft
description: "Utilisation de Hadoop Oozie dans HDInsight, un service pour les données volumineuses. Découvrez comment toodefine Oozie d’un flux de travail et soumettre un travail Oozie."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 870098f0-f416-4491-9719-78994bf4a369
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 12d0cf1a01838ab0f4e699c384ce2fb18f85cbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-in-hdinsight"></a><span data-ttu-id="65d79-104">Utilisez Oozie avec Hadoop toodefine et exécuter un workflow dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="65d79-104">Use Oozie with Hadoop toodefine and run a workflow in HDInsight</span></span>
[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="65d79-105">Découvrez comment toouse Apache Oozie toodefine un flux de travail et exécuter hello des flux de travail sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65d79-105">Learn how toouse Apache Oozie toodefine a workflow and run hello workflow on HDInsight.</span></span> <span data-ttu-id="65d79-106">toolearn sur coordinateur de Oozie hello, consultez [utiliser temporels coordinateur de Oozie Hadoop hdinsight][hdinsight-oozie-coordinator-time].</span><span class="sxs-lookup"><span data-stu-id="65d79-106">toolearn about hello Oozie coordinator, see [Use time-based Hadoop Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time].</span></span> <span data-ttu-id="65d79-107">toolearn Azure Data Factory, consultez [utilisez Pig et Hive avec Data Factory][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="65d79-107">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

<span data-ttu-id="65d79-108">Apache Oozie est un système de workflow/coordination qui gère les tâches Hadoop.</span><span class="sxs-lookup"><span data-stu-id="65d79-108">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="65d79-109">Il est intégré à la pile de Hadoop hello, et il prend en charge les travaux Hadoop pour Apache MapReduce Apache Pig, Apache Hive et Sqoop d’Apache.</span><span class="sxs-lookup"><span data-stu-id="65d79-109">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="65d79-110">Il peut également être utilisé tooschedule les travaux système tooa spécifiques, tels que les programmes Java ou des scripts de shell.</span><span class="sxs-lookup"><span data-stu-id="65d79-110">It can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts.</span></span>

<span data-ttu-id="65d79-111">flux de travail Hello que vous implémentez en suivant les instructions de hello dans ce didacticiel contient deux actions :</span><span class="sxs-lookup"><span data-stu-id="65d79-111">hello workflow you implement by following hello instructions in this tutorial contains two actions:</span></span>

![Diagramme du workflow][img-workflow-diagram]

1. <span data-ttu-id="65d79-113">Une action de la ruche exécute un Bonjour toocount du script HiveQL occurrences de chaque type de niveau de journal dans un fichier log4j.</span><span class="sxs-lookup"><span data-stu-id="65d79-113">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j file.</span></span> <span data-ttu-id="65d79-114">Chaque fichier log4j se compose d’une ligne de champs qui contient un champ [niveau de journal] indique le type de hello et niveau de gravité hello, par exemple :</span><span class="sxs-lookup"><span data-stu-id="65d79-114">Each log4j file consists of a line of fields that contains a [LOG LEVEL] field that shows hello type and hello severity, for example:</span></span>
   
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
   
    <span data-ttu-id="65d79-115">Hello sortie du script Hive est similaire à :</span><span class="sxs-lookup"><span data-stu-id="65d79-115">hello Hive script output is similar to:</span></span>
   
        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4
   
    <span data-ttu-id="65d79-116">Pour plus d’informations sur Hive, consultez l’article [Utilisation de Hive avec HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="65d79-116">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="65d79-117">Une action Sqoop exporte la table de tooa hello HiveQL sortie dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="65d79-117">A Sqoop action exports hello HiveQL output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="65d79-118">Pour plus d’informations sur Sqoop, consultez la rubrique [Utilisation de Hadoop Sqoop avec HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="65d79-118">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="65d79-119">Pour les versions Oozie prises en charge sur les clusters HDInsight, consultez [quelles sont les nouveautés dans les versions de cluster Hadoop hello fournies par HDInsight ?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="65d79-119">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="65d79-120">Composants requis</span><span class="sxs-lookup"><span data-stu-id="65d79-120">Prerequisites</span></span>
<span data-ttu-id="65d79-121">Avant de commencer ce didacticiel, vous devez disposer de hello élément suivant :</span><span class="sxs-lookup"><span data-stu-id="65d79-121">Before you begin this tutorial, you must have hello following item:</span></span>

* <span data-ttu-id="65d79-122">**Un poste de travail sur lequel est installé Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="65d79-122">**A workstation with Azure PowerShell**.</span></span> 
  

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]
  

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="65d79-123">Définir le flux de travail Oozie et hello script HiveQL connexe</span><span class="sxs-lookup"><span data-stu-id="65d79-123">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="65d79-124">Les définitions des workflows Oozie sont écrites en hPDL (un langage de définition du processus XML).</span><span class="sxs-lookup"><span data-stu-id="65d79-124">Oozie workflows definitions are written in hPDL (a XML Process Definition Language).</span></span> <span data-ttu-id="65d79-125">nom de fichier de flux de travail par défaut Hello est *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="65d79-125">hello default workflow file name is *workflow.xml*.</span></span> <span data-ttu-id="65d79-126">Hello Voici les fichiers de flux de travail hello que vous utilisez dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="65d79-126">hello following is hello workflow file you use in this tutorial.</span></span>

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

<span data-ttu-id="65d79-127">Il existe deux actions définies dans le flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="65d79-127">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="65d79-128">est de démarrer Hello-tooaction *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="65d79-128">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="65d79-129">Si l’action de hello s’exécute correctement, action suivante de hello est *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="65d79-129">If hello action runs successfully, hello next action is *RunSqoopExport*.</span></span>

<span data-ttu-id="65d79-130">Hello RunHiveScript a plusieurs variables.</span><span class="sxs-lookup"><span data-stu-id="65d79-130">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="65d79-131">Vous passez les valeurs hello lorsque vous soumettez un travail de Oozie hello à partir de votre station de travail à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65d79-131">You pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

<table border = "1">
<tr><th><span data-ttu-id="65d79-132">Variable de workflow</span><span class="sxs-lookup"><span data-stu-id="65d79-132">Workflow variables</span></span></th><th><span data-ttu-id="65d79-133">Description</span><span class="sxs-lookup"><span data-stu-id="65d79-133">Description</span></span></th></tr>
<tr><td><span data-ttu-id="65d79-134">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="65d79-134">${jobTracker}</span></span></td><td><span data-ttu-id="65d79-135">Spécifie l’URL hello de suivi de travail Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="65d79-135">Specifies hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="65d79-136">Utilisez <strong>jobtrackerhost:9010</strong> dans les versions 3.0 et 2.1 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65d79-136">Use <strong>jobtrackerhost:9010</strong> in HDInsight version 3.0 and 2.1.</span></span></td></tr>
<tr><td><span data-ttu-id="65d79-137">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="65d79-137">${nameNode}</span></span></td><td><span data-ttu-id="65d79-138">Spécifie l’URL hello du nœud de nom hello Hadoop.</span><span class="sxs-lookup"><span data-stu-id="65d79-138">Specifies hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="65d79-139">Utiliser adresse du système du fichier hello par défaut, par exemple, <i>wasb : / /&lt;Nom_conteneur&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="65d79-139">Use hello default file system address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
<tr><td><span data-ttu-id="65d79-140">${queueName}</span><span class="sxs-lookup"><span data-stu-id="65d79-140">${queueName}</span></span></td><td><span data-ttu-id="65d79-141">Spécifie le nom de file d’attente hello hello de travail est soumis à.</span><span class="sxs-lookup"><span data-stu-id="65d79-141">Specifies hello queue name that hello job is submitted to.</span></span> <span data-ttu-id="65d79-142">Hello d’utilisation <strong>par défaut</strong>.</span><span class="sxs-lookup"><span data-stu-id="65d79-142">Use hello <strong>default</strong>.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="65d79-143">Variable d'action Hive</span><span class="sxs-lookup"><span data-stu-id="65d79-143">Hive action variable</span></span></th><th><span data-ttu-id="65d79-144">Description</span><span class="sxs-lookup"><span data-stu-id="65d79-144">Description</span></span></th></tr>
<tr><td><span data-ttu-id="65d79-145">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="65d79-145">${hiveDataFolder}</span></span></td><td><span data-ttu-id="65d79-146">Spécifie le répertoire source hello hello commande Hive Create Table.</span><span class="sxs-lookup"><span data-stu-id="65d79-146">Specifies hello source directory for hello Hive Create Table command.</span></span></td></tr>
<tr><td><span data-ttu-id="65d79-147">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="65d79-147">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="65d79-148">Spécifie le dossier de sortie hello pour hello insérer remplacer l’instruction.</span><span class="sxs-lookup"><span data-stu-id="65d79-148">Specifies hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
<tr><td><span data-ttu-id="65d79-149">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="65d79-149">${hiveTableName}</span></span></td><td><span data-ttu-id="65d79-150">Spécifie le nom hello de table Hive hello qui fait référence à des fichiers de données log4j hello.</span><span class="sxs-lookup"><span data-stu-id="65d79-150">Specifies hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="65d79-151">Variable d'action Sqoop</span><span class="sxs-lookup"><span data-stu-id="65d79-151">Sqoop action variable</span></span></th><th><span data-ttu-id="65d79-152">Description</span><span class="sxs-lookup"><span data-stu-id="65d79-152">Description</span></span></th></tr>
<tr><td><span data-ttu-id="65d79-153">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="65d79-153">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="65d79-154">Spécifie la chaîne de connexion de base de données SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="65d79-154">Specifies hello Azure SQL database connection string.</span></span></td></tr>
<tr><td><span data-ttu-id="65d79-155">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="65d79-155">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="65d79-156">Spécifie la table de base de données SQL Azure hello où les données de salutation sont exportées vers.</span><span class="sxs-lookup"><span data-stu-id="65d79-156">Specifies hello Azure SQL database table where hello data is exported to.</span></span></td></tr>
<tr><td><span data-ttu-id="65d79-157">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="65d79-157">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="65d79-158">Spécifie le dossier de sortie hello pour hello Hive insérer remplacer l’instruction.</span><span class="sxs-lookup"><span data-stu-id="65d79-158">Specifies hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="65d79-159">Il s’agit de hello même dossier pour l’exportation de Sqoop hello (export-dir).</span><span class="sxs-lookup"><span data-stu-id="65d79-159">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
</table>

<span data-ttu-id="65d79-160">Pour plus d’informations sur le workflow Oozie et l’utilisation des actions de workflow, consultez la rubrique [Documentation sur Apache Oozie 4.0][apache-oozie-400] (pour la version 3.0 de HDInsight) ou [Documentation sur Apache Oozie 3.3.2][apache-oozie-332] (pour la version 2.1 de HDInsight).</span><span class="sxs-lookup"><span data-stu-id="65d79-160">For more information about Oozie workflow and using workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="65d79-161">Hello action Hive dans le flux de travail hello appelle un fichier de script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="65d79-161">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="65d79-162">Le fichier de script contient trois instructions HiveQL :</span><span class="sxs-lookup"><span data-stu-id="65d79-162">This script file contains three HiveQL statements:</span></span>

    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

1. <span data-ttu-id="65d79-163">**Hello, l’instruction DROP TABLE** suppressions hello log4j ruche table si elle existe.</span><span class="sxs-lookup"><span data-stu-id="65d79-163">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="65d79-164">**Hello, l’instruction CREATE TABLE** crée une table externe de ruche log4j qui pointe l’emplacement toohello du fichier de journal log4j hello.</span><span class="sxs-lookup"><span data-stu-id="65d79-164">**hello CREATE TABLE statement** creates a log4j Hive external table that points toohello location of hello log4j log file.</span></span> <span data-ttu-id="65d79-165">séparateur de champs Hello est «, ».</span><span class="sxs-lookup"><span data-stu-id="65d79-165">hello field delimiter is ",".</span></span> <span data-ttu-id="65d79-166">délimiteur de ligne Hello par défaut est « \n ».</span><span class="sxs-lookup"><span data-stu-id="65d79-166">hello default line delimiter is "\n".</span></span> <span data-ttu-id="65d79-167">Une table externe Hive est fichier de données utilisé tooavoid hello en cours de suppression hello emplacement d’origine si vous souhaitez des flux de travail toorun hello Oozie plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="65d79-167">A Hive external table is used tooavoid hello data file being removed from hello original location if you want toorun hello Oozie workflow multiple times.</span></span>
3. <span data-ttu-id="65d79-168">**Hello insérer remplacer l’instruction** compte hello les occurrences de chaque type de niveau de journal à partir de la table de Hive log4j hello et enregistre l’objet blob de hello sortie tooa dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="65d79-168">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and saves hello output tooa blob in Azure Storage.</span></span>

<span data-ttu-id="65d79-169">Il existe trois variables utilisées dans un script de hello :</span><span class="sxs-lookup"><span data-stu-id="65d79-169">There are three variables used in hello script:</span></span>

* <span data-ttu-id="65d79-170">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="65d79-170">${hiveTableName}</span></span>
* <span data-ttu-id="65d79-171">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="65d79-171">${hiveDataFolder}</span></span>
* <span data-ttu-id="65d79-172">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="65d79-172">${hiveOutputFolder}</span></span>

<span data-ttu-id="65d79-173">le fichier de définition de flux de travail Hello (workflow.xml dans ce didacticiel) passe ces toothis valeurs script HiveQL au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="65d79-173">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time.</span></span>

<span data-ttu-id="65d79-174">Fichier de flux de travail hello et fichier de HiveQL hello sont stockés dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="65d79-174">Both hello workflow file and hello HiveQL file are stored in a blob container.</span></span>  <span data-ttu-id="65d79-175">Hello script PowerShell que vous utilisez plus loin dans ce didacticiel copie les deux compte de stockage de fichiers toohello par défaut.</span><span class="sxs-lookup"><span data-stu-id="65d79-175">hello PowerShell script you use later in this tutorial copies both files toohello default Storage account.</span></span> 

## <a name="submit-oozie-jobs-using-powershell"></a><span data-ttu-id="65d79-176">Soumettre des tâches Oozie avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="65d79-176">Submit Oozie jobs using PowerShell</span></span>
<span data-ttu-id="65d79-177">Azure PowerShell ne fournit actuellement aucune applet de commande pour la définition de tâches Oozie.</span><span class="sxs-lookup"><span data-stu-id="65d79-177">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="65d79-178">Vous pouvez utiliser hello **Invoke-RestMethod** tooinvoke applet de commande Oozie des services web.</span><span class="sxs-lookup"><span data-stu-id="65d79-178">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="65d79-179">API des services web Oozie Hello est une API de JSON HTTP REST.</span><span class="sxs-lookup"><span data-stu-id="65d79-179">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="65d79-180">Pour plus d’informations sur les API des services web hello Oozie, consultez [documentation Apache Oozie 4.0] [ apache-oozie-400] (pour HDInsight version 3.0) ou [Apache Oozie 3.3.2 documentation] [ apache-oozie-332] (pour HDInsight version 2.1).</span><span class="sxs-lookup"><span data-stu-id="65d79-180">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="65d79-181">Hello script PowerShell dans cette section effectue hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="65d79-181">hello PowerShell script in this section performs hello following steps:</span></span>

1. <span data-ttu-id="65d79-182">Se connecter tooAzure.</span><span class="sxs-lookup"><span data-stu-id="65d79-182">Connect tooAzure.</span></span>
2. <span data-ttu-id="65d79-183">Création d’un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="65d79-183">Create an Azure resource group.</span></span> <span data-ttu-id="65d79-184">Pour plus d’informations, consultez [Utilisation d’Azure PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="65d79-184">For more information, see [Use Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>
3. <span data-ttu-id="65d79-185">Création d’un serveur Base de données SQL Azure, d’une base de données SQL Azure et de deux tables.</span><span class="sxs-lookup"><span data-stu-id="65d79-185">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> <span data-ttu-id="65d79-186">Ils sont utilisés par hello action Sqoop dans le flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="65d79-186">These are used by hello Sqoop action in hello workflow.</span></span>
   
    <span data-ttu-id="65d79-187">nom de la table Hello est *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="65d79-187">hello table name is *log4jLogCount*.</span></span>
4. <span data-ttu-id="65d79-188">Créer un toorun de cluster utilisé HDInsight Oozie travaux.</span><span class="sxs-lookup"><span data-stu-id="65d79-188">Create an HDInsight cluster used toorun Oozie jobs.</span></span>
   
    <span data-ttu-id="65d79-189">cluster de hello tooexamine, vous pouvez utiliser hello portail Azure ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65d79-189">tooexamine hello cluster, you can use hello Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="65d79-190">Copier le fichier de flux de travail oozie hello et hello HiveQL script toohello par défaut système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="65d79-190">Copy hello oozie workflow file and hello HiveQL script file toohello default file system.</span></span>
   
    <span data-ttu-id="65d79-191">Les deux fichiers sont stockés dans un conteneur d’objets blob public.</span><span class="sxs-lookup"><span data-stu-id="65d79-191">Both files are stored in a public Blob container.</span></span>
   
   * <span data-ttu-id="65d79-192">Copiez hello HiveQL script (useoozie.hql) tooAzure (wasb:///tutorials/useoozie/useoozie.hql) de stockage.</span><span class="sxs-lookup"><span data-stu-id="65d79-192">Copy hello HiveQL script (useoozie.hql) tooAzure Storage (wasb:///tutorials/useoozie/useoozie.hql).</span></span>
   * <span data-ttu-id="65d79-193">Copiez workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="65d79-193">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
   * <span data-ttu-id="65d79-194">Fichier de données de copie hello (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="65d79-194">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
6. <span data-ttu-id="65d79-195">Soumettez une tâche Oozie.</span><span class="sxs-lookup"><span data-stu-id="65d79-195">Submit an Oozie job.</span></span>
   
    <span data-ttu-id="65d79-196">résultats de la tâche de tooexamine hello OOzie, utilisez Visual Studio ou autres toohello de tooconnect outils base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="65d79-196">tooexamine hello OOzie job results, use Visual Studio or other tools tooconnect toohello Azure SQL Database.</span></span>

<span data-ttu-id="65d79-197">Voici le script de hello.</span><span class="sxs-lookup"><span data-stu-id="65d79-197">Here is hello script.</span></span>  <span data-ttu-id="65d79-198">Vous pouvez exécuter le script de hello à partir de Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="65d79-198">You can run hello script from Windows PowerShell ISE.</span></span> <span data-ttu-id="65d79-199">Vous ne devez tooconfigure hello 7 premiers variables.</span><span class="sxs-lookup"><span data-stu-id="65d79-199">You only need tooconfigure hello first 7 variables.</span></span>

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure subscription ID>"

    # SQL Database server login credentials used for creating and connecting
    $sqlDatabaseLogin = "<Enter SQL Database Login Name>"
    $sqlDatabasePassword = "<Enter SQL Database Login Password>"

    # HDInsight cluster HTTP user credential used for creating and connectin
    $httpUserName = "admin"  # hello default name is "admin"
    $httpPassword = "<Enter HDInsight Cluster HTTP User Password>"

    # Used for creating Azure service names
    $nameToken = "<Enter an Alias>"
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{
        Login-AzureRmAccount
        Select-AzureRmSubscription -SubscriptionId $subscriptionID
    }
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $sqlLoginCredentials = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $sqlLoginCredentials `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }
    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }
    #endregion

    #region - Create SQL database tables
    Write-Host "Creating hello log4jlogs table  ..." -ForegroundColor Green

    $sqlDatabaseTableName = "log4jLogsCount"
    $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
            [Level] [nvarchar](10) NOT NULL,
            [Total] float,
        CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
        (
        [Level] ASC
        )
        )"

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jCountTable
    $cmd.ExecuteNonQuery()

    $conn.close()
    #endregion

    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - copy Oozie workflow and HiveQL files

    Write-Host "Copy workflow definition and HiveQL script file ..." -ForegroundColor Green

    # Both files are stored in a public Blob
    $publicBlobContext = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "useooziewf.hql"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/useooziewf.hql" `
        -Force

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "workflow.xml"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/workflow.xml" `
        -Force

    #validate hello copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/workflow.xml

    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/useooziewf.hql

    #endregion

    #region - copy hello sample.log file

    Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green

    Start-CopyAzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -SrcContainer $defaultBlobContainerName `
        -SrcBlob "example/data/sample.log"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -destBlob "$destFolder/data/sample.log" 

    #validate hello copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/data/sample.log

    #endregion

    #region - submit Oozie job

    $storageUri="wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net"

    $oozieJobName = $namePrefix + "OozieJob"

    #Oozie WF variables
    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"

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
        <value>$httpUserName</value>
    </property>

    <property>
        <name>oozie.wf.application.path</name>
        <value>$oozieWFPath</value>
    </property>

    </configuration>
    "@

    Write-Host "Checking Oozie server status..." -ForegroundColor Green
    $clusterUriStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/admin/status"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $httpCredential -OutVariable $OozieServerStatus

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieServerSatus = $jsonResponse[0].("systemMode")
    Write-Host "Oozie server status is $oozieServerSatus."

    # create Oozie job
    Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
    Write-Host "`n--------`n$OoziePayload`n--------"
    $clusterUriCreateJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/jobs"
    $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $httpCredential -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName #-debug

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieJobId = $jsonResponse[0].("id")
    Write-Host "Oozie job id is $oozieJobId..."

    # start Oozie job
    Write-Host "Starting hello Oozie job $oozieJobId..." -ForegroundColor Green
    $clusterUriStartJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=start"
    $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $httpCredential | Format-Table -HideTableHeaders #-debug

    # get job status
    Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
    Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

    Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
    $clusterUriGetJobStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $JobStatus = $jsonResponse[0].("status")

    while($JobStatus -notmatch "SUCCEEDED|KILLED")
    {
        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")
        $jobStatus
    }

    Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!" -ForegroundColor Green

    #endregion


<span data-ttu-id="65d79-200">**didacticiel de la série de toore hello**</span><span class="sxs-lookup"><span data-stu-id="65d79-200">**toore-run hello tutorial**</span></span>

<span data-ttu-id="65d79-201">flux de travail-exécution toore hello, vous devez supprimer hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="65d79-201">toore-run hello workflow, you must delete hello following items:</span></span>

* <span data-ttu-id="65d79-202">Hello, fichier de sortie du script Hive</span><span class="sxs-lookup"><span data-stu-id="65d79-202">hello Hive script output file</span></span>
* <span data-ttu-id="65d79-203">données Hello dans la table de log4jLogsCount hello</span><span class="sxs-lookup"><span data-stu-id="65d79-203">hello data in hello log4jLogsCount table</span></span>

<span data-ttu-id="65d79-204">Voici un exemple d'un script PowerShell que vous pouvez utiliser :</span><span class="sxs-lookup"><span data-stu-id="65d79-204">Here is a sample PowerShell script that you can use:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"

    $defaultStorageAccountName = "<AzureStorageAccountName>"
    $defaultBlobContainerName = "<ContainerName>"

    #SQL database variables
    $sqlDatabaseServerName = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabasePassword = "<SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                -ResourceGroupName $resourceGroupName `
                                -Name $defaultStorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $defaultBlobContainerName

    Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = "delete from $sqlDatabaseTableName"
    $cmd.executenonquery()

    $conn.close()

## <a name="next-steps"></a><span data-ttu-id="65d79-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="65d79-205">Next steps</span></span>
<span data-ttu-id="65d79-206">Dans ce didacticiel, vous avez appris comment toodefine un Oozie comment toorun un Oozie de travail à l’aide de PowerShell et de flux de travail.</span><span class="sxs-lookup"><span data-stu-id="65d79-206">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job by using PowerShell.</span></span> <span data-ttu-id="65d79-207">toolearn, voir hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="65d79-207">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="65d79-208">[Utilisation du coordinateur Oozie basé sur le temps avec HDInsight][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="65d79-208">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="65d79-209">[Prise en main Hadoop avec ruche en cours d’utilisation de HDInsight tooanalyze combiné mobile][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="65d79-209">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="65d79-210">[Utilisation de Stockage Blob Azure avec HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="65d79-210">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="65d79-211">[Administration de HDInsight à l’aide de PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="65d79-211">[Administer HDInsight using PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="65d79-212">[Importation de données pour les tâches Hadoop dans HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="65d79-212">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="65d79-213">[Utilisation de Sqoop avec Hadoop dans HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="65d79-213">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="65d79-214">[Utilisation de Hive avec Hadoop sur HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="65d79-214">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="65d79-215">[Utilisation de Pig avec Hadoop sur HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="65d79-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="65d79-216">[Développement de programmes MapReduce en Java pour HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="65d79-216">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563



[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md


[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: ../sql-database-create-configure.md
[sqldatabase-get-started]: ../sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: https://technet.microsoft.com/en-us/library/ee176961.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.Preparation.Output1.png  
[img-runworkflow-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.RunWF.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
