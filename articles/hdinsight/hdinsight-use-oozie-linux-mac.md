---
title: "Utilisation des workflows Hadoop Oozie dans HDInsight basé sur Linux | Microsoft Docs"
description: "Utilisation de Hadoop Oozie dans HDInsight basé sur Linux. Découvrez comment définir un workflow Oozie et envoyer une tâche Oozie."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d7603471-5076-43d1-8b9a-dbc4e366ce5d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: e3206078e451aefe02689bfb61ce22a20dd0fa70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-oozie-with-hadoop-to-define-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="52c41-104">Utilisation d’Oozie avec Hadoop pour définir et exécuter un flux de travail dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="52c41-104">Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="52c41-105">Découvrez comment utiliser Apache Oozie avec Hadoop sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="52c41-105">Learn how to use Apache Oozie with Hadoop on HDInsight.</span></span> <span data-ttu-id="52c41-106">Apache Oozie est un système de workflow/coordination qui gère les tâches Hadoop.</span><span class="sxs-lookup"><span data-stu-id="52c41-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="52c41-107">Oozie est intégré dans la pile Hadoop et prend en charge les travaux suivants :</span><span class="sxs-lookup"><span data-stu-id="52c41-107">Oozie is integrated with the Hadoop stack, and it supports the following jobs:</span></span>

* <span data-ttu-id="52c41-108">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="52c41-108">Apache MapReduce</span></span>
* <span data-ttu-id="52c41-109">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="52c41-109">Apache Pig</span></span>
* <span data-ttu-id="52c41-110">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="52c41-110">Apache Hive</span></span>
* <span data-ttu-id="52c41-111">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="52c41-111">Apache Sqoop</span></span>

<span data-ttu-id="52c41-112">Oozie peut également être utilisé pour planifier des travaux propres à un système, comme des programmes Java ou des scripts de l’interpréteur de commandes</span><span class="sxs-lookup"><span data-stu-id="52c41-112">Oozie can also be used to schedule jobs that are specific to a system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="52c41-113">Une autre option pour définir des flux de travail avec HDInsight consiste à utiliser Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="52c41-113">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="52c41-114">Pour en savoir plus sur Azure Data Factory, consultez la page [Utilisation de Pig et Hive avec Data Factory][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="52c41-114">To learn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52c41-115">Oozie n’est pas activé sur HDInsight joint à un domaine.</span><span class="sxs-lookup"><span data-stu-id="52c41-115">Oozie is not enabled on domain-joined HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52c41-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="52c41-116">Prerequisites</span></span>

* <span data-ttu-id="52c41-117">**Un cluster HDInsight**: consultez la page [Prise en main de HDInsight sur Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="52c41-117">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="52c41-118">Les étapes décrites dans ce document nécessitent un cluster HDInsight utilisant Linux.</span><span class="sxs-lookup"><span data-stu-id="52c41-118">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="52c41-119">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="52c41-119">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="52c41-120">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="52c41-120">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="example-workflow"></a><span data-ttu-id="52c41-121">Exemple de flux de travail</span><span class="sxs-lookup"><span data-stu-id="52c41-121">Example workflow</span></span>

<span data-ttu-id="52c41-122">Le workflow utilisé dans ce document comporte deux actions.</span><span class="sxs-lookup"><span data-stu-id="52c41-122">The workflow used in this document contains two actions.</span></span> <span data-ttu-id="52c41-123">Les actions sont des définitions de tâches, telles que l’exécution de Hive, Sqoop, MapReduce ou un autre processus :</span><span class="sxs-lookup"><span data-stu-id="52c41-123">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![Diagramme du workflow][img-workflow-diagram]

1. <span data-ttu-id="52c41-125">Une action Hive exécute un script HiveQL pour extraire des enregistrements à partir de la table **hivesampletable** incluse avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="52c41-125">A Hive action runs a HiveQL script to extract records from the **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="52c41-126">Chaque ligne de données décrit un accès depuis un appareil mobile spécifique.</span><span class="sxs-lookup"><span data-stu-id="52c41-126">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="52c41-127">Le format d’enregistrement ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="52c41-127">The record format appears similar to the following text:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="52c41-128">Le script Hive utilisé dans ce document comptabilise le nombre total d’accès pour chaque plateforme (par exemple, Android ou iPhone) et stocke les nombres dans une nouvelle table Hive.</span><span class="sxs-lookup"><span data-stu-id="52c41-128">The Hive script used in this document counts the total visits for each platform (such as Android or iPhone) and stores the counts to a new Hive table.</span></span>

    <span data-ttu-id="52c41-129">Pour plus d’informations sur Hive, consultez l’article [Utilisation de Hive avec HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="52c41-129">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="52c41-130">Une action Sqoop exporte le contenu de la nouvelle table Hive vers une table dans la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="52c41-130">A Sqoop action exports the contents of the new Hive table to a table in an Azure SQL database.</span></span> <span data-ttu-id="52c41-131">Pour plus d’informations sur Sqoop, consultez la rubrique [Utilisation de Hadoop Sqoop avec HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="52c41-131">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="52c41-132">Pour obtenir la liste des versions Oozie prises en charge sur les clusters HDInsight, voir [Nouveautés des versions de cluster Hadoop fournies par HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="52c41-132">For supported Oozie versions on HDInsight clusters, see [What's new in the Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-the-working-directory"></a><span data-ttu-id="52c41-133">Création du répertoire de travail</span><span class="sxs-lookup"><span data-stu-id="52c41-133">Create the working directory</span></span>

<span data-ttu-id="52c41-134">Oozie s’attend à ce que les ressources requises pour un travail soient stockées dans le même répertoire.</span><span class="sxs-lookup"><span data-stu-id="52c41-134">Oozie expects resources required for a job to be stored in the same directory.</span></span> <span data-ttu-id="52c41-135">Cet exemple utilise **wasb:///tutorials/useoozie**.</span><span class="sxs-lookup"><span data-stu-id="52c41-135">This example uses **wasb:///tutorials/useoozie**.</span></span> <span data-ttu-id="52c41-136">Utilisez la commande suivante pour créer ce répertoire et le répertoire de données qui contient la nouvelle table Hive créée par ce workflow :</span><span class="sxs-lookup"><span data-stu-id="52c41-136">Use the following command to create this directory, and the data directory that holds the new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="52c41-137">Le paramètre `-p` a provoqué la création de tous les répertoires dans le chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="52c41-137">The `-p` parameter causes all directories in the path to be created.</span></span> <span data-ttu-id="52c41-138">Le répertoire **data** est utilisé pour contenir les données utilisées par le script **useooziewf.hql**.</span><span class="sxs-lookup"><span data-stu-id="52c41-138">The **data** directory is used to hold data used by the **useooziewf.hql** script.</span></span>

<span data-ttu-id="52c41-139">Exécutez également la commande suivante, qui garantit que Oozie peut emprunter l’identité de votre compte d'utilisateur lors de l’exécution de travaux Hive et Sqoop.</span><span class="sxs-lookup"><span data-stu-id="52c41-139">Also run the following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="52c41-140">Remplacez **USERNAME** par votre nom de connexion :</span><span class="sxs-lookup"><span data-stu-id="52c41-140">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

> [!NOTE]
> <span data-ttu-id="52c41-141">Vous pouvez ignorer les erreurs indiquant que l’utilisateur est déjà membre du groupe `users`.</span><span class="sxs-lookup"><span data-stu-id="52c41-141">You can ignore errors that the user is already a member of the `users` group.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="52c41-142">Ajout d’un pilote de base de données</span><span class="sxs-lookup"><span data-stu-id="52c41-142">Add a database driver</span></span>

<span data-ttu-id="52c41-143">Étant donné que ce flux de travail utilise Sqoop pour exporter des données vers la base de données SQL, vous devez fournir une copie du pilote JDBC utilisé pour communiquer avec la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="52c41-143">Since this workflow uses Sqoop to export data to SQL Database, you must provide a copy of the JDBC driver used to talk to SQL Database.</span></span> <span data-ttu-id="52c41-144">Pour le copier dans le répertoire de travail, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52c41-144">Use the following command to copy it to the working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="52c41-145">Si votre flux de travail utilisait d’autres ressources, par exemple un fichier jar contenant une application MapReduce, vous devez également les ajouter.</span><span class="sxs-lookup"><span data-stu-id="52c41-145">If your workflow used other resources, such as a jar containing a MapReduce application, you would need to add these resources as well.</span></span>

## <a name="define-the-hive-query"></a><span data-ttu-id="52c41-146">Définition de la requête Hive</span><span class="sxs-lookup"><span data-stu-id="52c41-146">Define the Hive query</span></span>

<span data-ttu-id="52c41-147">Utilisez les étapes suivantes pour créer un script HiveQL qui définit une requête qui est utilisée dans un workflow Oozie plus loin dans ce document.</span><span class="sxs-lookup"><span data-stu-id="52c41-147">Use the following steps to create a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="52c41-148">Connectez-vous au cluster à l'aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="52c41-148">Connect to the cluster using SSH.</span></span> <span data-ttu-id="52c41-149">La commande suivante est un exemple d’utilisation de la commande `ssh`.</span><span class="sxs-lookup"><span data-stu-id="52c41-149">The following command is an example of using the `ssh` command.</span></span> <span data-ttu-id="52c41-150">Remplacez __USERNAME__ par l’utilisateur SSH pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="52c41-150">Replace __USERNAME__ with the SSH user for the cluster.</span></span> <span data-ttu-id="52c41-151">Remplacez __CLUSTERNAME__ par le nom du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="52c41-151">Replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="52c41-152">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="52c41-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="52c41-153">À partir de la connexion SSH, utilisez la commande suivante pour créer un fichier :</span><span class="sxs-lookup"><span data-stu-id="52c41-153">From the SSH connection, use the following command to create a file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="52c41-154">Une fois que l’éditeur nano est ouvert, utilisez la requête suivante comme contenu du fichier :</span><span class="sxs-lookup"><span data-stu-id="52c41-154">Once the nano editor opens, use the following query as the contents of the file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="52c41-155">Deux variables sont utilisées dans le script :</span><span class="sxs-lookup"><span data-stu-id="52c41-155">There are two variables used in the script:</span></span>

    * <span data-ttu-id="52c41-156">**${hiveTableName}** : contient le nom de la table à créer.</span><span class="sxs-lookup"><span data-stu-id="52c41-156">**${hiveTableName}**: contains the name of the table to be created</span></span>

    * <span data-ttu-id="52c41-157">**${hiveDataFolder}** : contient l’emplacement où stocker les fichiers de données pour la table.</span><span class="sxs-lookup"><span data-stu-id="52c41-157">**${hiveDataFolder}**: contains the location to store the data files for the table</span></span>

    <span data-ttu-id="52c41-158">Le fichier de définition du workflow (workflow.xml dans ce didacticiel) transmet ces valeurs à ce script HiveQL au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="52c41-158">The workflow definition file (workflow.xml in this tutorial) passes these values to this HiveQL script at run time</span></span>

4. <span data-ttu-id="52c41-159">Appuyez sur Ctrl+X pour quitter l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="52c41-159">To exit the editor, press Ctrl-X.</span></span> <span data-ttu-id="52c41-160">Lorsque vous y êtes invité, sélectionnez **Y** pour enregistrer le fichier, puis sélectionnez **Entrée** pour utiliser le nom de fichier **useooziewf.hql**.</span><span class="sxs-lookup"><span data-stu-id="52c41-160">When prompted, select **Y** to save the file, then use **Enter** to use the **useooziewf.hql** file name.</span></span>

5. <span data-ttu-id="52c41-161">Utilisez les commandes suivantes pour copier **useooziewf.hql** vers **wasb:///tutorials/useoozie/useooziewf.hql** :</span><span class="sxs-lookup"><span data-stu-id="52c41-161">Use the following commands to copy **useooziewf.hql** to **wasb:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="52c41-162">Ces commandes stockent le fichier **useooziewf.hql** sur le stockage compatible avec HDFS pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="52c41-162">These commands store the **useooziewf.hql** file on the HDFS-compatible storage for the cluster.</span></span>

## <a name="define-the-workflow"></a><span data-ttu-id="52c41-163">Définition du flux de travail</span><span class="sxs-lookup"><span data-stu-id="52c41-163">Define the workflow</span></span>

<span data-ttu-id="52c41-164">Les définitions des workflows Oozie sont écrites en hPDL (un langage de définition du processus XML).</span><span class="sxs-lookup"><span data-stu-id="52c41-164">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="52c41-165">Pour définir le flux de travail, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="52c41-165">Use the following steps to define the workflow:</span></span>

1. <span data-ttu-id="52c41-166">Pour créer et modifier un fichier, utilisez l’instruction suivante :</span><span class="sxs-lookup"><span data-stu-id="52c41-166">Use the following statement to create and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="52c41-167">Une fois que l’éditeur nano est ouvert, saisissez le code XML suivant comme contenu du fichier :</span><span class="sxs-lookup"><span data-stu-id="52c41-167">Once the nano editor opens, enter the following XML as the file contents:</span></span>

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
            <arg>${hiveDataFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\t"</arg>
            <archive>sqljdbc41.jar</archive>
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

    <span data-ttu-id="52c41-168">Deux actions sont définies dans le flux de travail :</span><span class="sxs-lookup"><span data-stu-id="52c41-168">There are two actions defined in the workflow:</span></span>

   * <span data-ttu-id="52c41-169">**RunHiveScript** : il s’agit de l’action de départ, qui exécute le script Hive **useooziewf.hql**</span><span class="sxs-lookup"><span data-stu-id="52c41-169">**RunHiveScript**: This action is the start action, and runs the **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="52c41-170">**RunSqoopExport** : cette action exporte les données créées à partir du script Hive vers la base de données SQL à l’aide de Sqoop.</span><span class="sxs-lookup"><span data-stu-id="52c41-170">**RunSqoopExport**: This action exports the data created from the Hive script to SQL Database using Sqoop.</span></span> <span data-ttu-id="52c41-171">Elle n’est exécutée que si l’action **RunHiveScript** a abouti.</span><span class="sxs-lookup"><span data-stu-id="52c41-171">This action only runs if the **RunHiveScript** action is successful.</span></span>

     <span data-ttu-id="52c41-172">Le workflow a plusieurs entrées, telle que `${jobTracker}`.</span><span class="sxs-lookup"><span data-stu-id="52c41-172">The workflow has several entries, such as `${jobTracker}`.</span></span> <span data-ttu-id="52c41-173">Ces entrées sont remplacées par les valeurs que vous utilisez dans la définition du travail.</span><span class="sxs-lookup"><span data-stu-id="52c41-173">These entries are replaced by values you use in the job definition.</span></span> <span data-ttu-id="52c41-174">La définition du travail est créée ultérieurement dans ce document.</span><span class="sxs-lookup"><span data-stu-id="52c41-174">The job definition is created later in this document.</span></span>

     <span data-ttu-id="52c41-175">Notez également l’entrée `<archive>sqljdbc4.jar</arcive>` dans la section Sqoop.</span><span class="sxs-lookup"><span data-stu-id="52c41-175">Also note the `<archive>sqljdbc4.jar</arcive>` entry in the Sqoop section.</span></span> <span data-ttu-id="52c41-176">Celle-ci indique à Oozie de rendre cette archive disponible pour Sqoop lors de l’exécution de cette action.</span><span class="sxs-lookup"><span data-stu-id="52c41-176">This entry instructs Oozie to make this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="52c41-177">Utilisez Ctrl-X, puis **Y** et **Entrée** pour enregistrer le fichier.</span><span class="sxs-lookup"><span data-stu-id="52c41-177">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

4. <span data-ttu-id="52c41-178">Utilisez la commande suivante pour copier le fichier **workflow.xml** vers **/tutorials/useoozie/workflow.xml** :</span><span class="sxs-lookup"><span data-stu-id="52c41-178">Use the following command to copy the **workflow.xml** file to **/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-the-database"></a><span data-ttu-id="52c41-179">Création de la base de données</span><span class="sxs-lookup"><span data-stu-id="52c41-179">Create the database</span></span>

<span data-ttu-id="52c41-180">Suivez les étapes du document [Création d’une base de données SQL](../sql-database/sql-database-get-started.md) afin de créer une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="52c41-180">To create an Azure SQL Database, follow the steps in the [Create a SQL Database](../sql-database/sql-database-get-started.md) document.</span></span> <span data-ttu-id="52c41-181">Lorsque vous créez la base de données, utilisez `oozietest` comme nom de base de données.</span><span class="sxs-lookup"><span data-stu-id="52c41-181">When creating the database, use `oozietest` as the database name.</span></span> <span data-ttu-id="52c41-182">Prenez également note du nom du serveur de base de données.</span><span class="sxs-lookup"><span data-stu-id="52c41-182">Also make a note of the name of the database server.</span></span>

### <a name="create-the-table"></a><span data-ttu-id="52c41-183">Créer la table</span><span class="sxs-lookup"><span data-stu-id="52c41-183">Create the table</span></span>

> [!NOTE]
> <span data-ttu-id="52c41-184">Il existe de nombreuses façons de se connecter à la base de données SQL pour créer une table.</span><span class="sxs-lookup"><span data-stu-id="52c41-184">There are many ways to connect to SQL Database to create a table.</span></span> <span data-ttu-id="52c41-185">Les étapes suivantes utilisent [FreeTDS](http://www.freetds.org/) à partir du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="52c41-185">The following steps use [FreeTDS](http://www.freetds.org/) from the HDInsight cluster.</span></span>


1. <span data-ttu-id="52c41-186">Utilisez la commande suivante pour installer FreeTDS sur le cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="52c41-186">Use the following command to install FreeTDS on the HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="52c41-187">Une fois FreeTDS installé, utilisez la commande suivante pour vous connecter au serveur de base de données SQL créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="52c41-187">Once FreeTDS has been installed, use the following command to connect to the SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="52c41-188">Le résultat ressemble au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="52c41-188">You receive output similar to the following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set to oozietest
        1>

3. <span data-ttu-id="52c41-189">À l’invite de commandes `1>` , entrez les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="52c41-189">At the `1>` prompt, enter the following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="52c41-190">Une fois l’instruction `GO` entrée, les instructions précédentes sont évaluées.</span><span class="sxs-lookup"><span data-stu-id="52c41-190">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="52c41-191">Ces instructions créent une table nommée **mobiledata** qui est utilisé par le workflow.</span><span class="sxs-lookup"><span data-stu-id="52c41-191">These statements create a table named **mobiledata** that is used by the workflow.</span></span>

    <span data-ttu-id="52c41-192">Vérifiez que la table a été créée à l’aide des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="52c41-192">Use the following to verify that the table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="52c41-193">Le résultat est similaire au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="52c41-193">You see output similar to the following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="52c41-194">Pour quitter l’utilitaire psql, entrez `exit` at the `1>` .</span><span class="sxs-lookup"><span data-stu-id="52c41-194">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="create-the-job-definition"></a><span data-ttu-id="52c41-195">Création de la définition de travail</span><span class="sxs-lookup"><span data-stu-id="52c41-195">Create the job definition</span></span>

<span data-ttu-id="52c41-196">La définition du travail indique où se trouve le fichier workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="52c41-196">The job definition describes where to find the workflow.xml.</span></span> <span data-ttu-id="52c41-197">Elle indique également où se trouvent les autres fichiers utilisés par le workflow (par exemple, useooziewf.hql). Elle définit également les valeurs des propriétés utilisées dans le flux de travail et les fichiers associés.</span><span class="sxs-lookup"><span data-stu-id="52c41-197">It also describes where to find other files used by the workflow (such as useooziewf.hql.) It also defines the values for properties used within the workflow and associated files.</span></span>

1. <span data-ttu-id="52c41-198">Utilisez la commande suivante pour obtenir l’adresse complète du stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="52c41-198">Use the following command to get the full address of the default storage.</span></span> <span data-ttu-id="52c41-199">Nous nous en servirons dans le fichier de configuration dans un moment :</span><span class="sxs-lookup"><span data-stu-id="52c41-199">This address is used in the configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="52c41-200">Cette commande renvoie des informations similaires au code XML suivant :</span><span class="sxs-lookup"><span data-stu-id="52c41-200">This command returns information similar to the following XML:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="52c41-201">Si le cluster HDInsight utilise le stockage Azure comme stockage par défaut, le contenu de l’élément `<value>` commence par `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="52c41-201">If the HDInsight cluster uses Azure Storage as the default storage, the `<value>` element contents begin with `wasb://`.</span></span> <span data-ttu-id="52c41-202">En revanche, si Azure Data Lake Store est utilisé, il commence par `adl://`.</span><span class="sxs-lookup"><span data-stu-id="52c41-202">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="52c41-203">Enregistrez le contenu de l’élément `<value>`, tel qu’il est utilisé dans les prochaines étapes.</span><span class="sxs-lookup"><span data-stu-id="52c41-203">Save the contents of the `<value>` element, as it is used in the next steps.</span></span>

2. <span data-ttu-id="52c41-204">Utilisez la commande suivante pour obtenir le nom de domaine complet du nœud principal du cluster.</span><span class="sxs-lookup"><span data-stu-id="52c41-204">Use the following command to get FQDN of the cluster headnode.</span></span> <span data-ttu-id="52c41-205">Il est utilisé comme adresse JobTracker pour le cluster :</span><span class="sxs-lookup"><span data-stu-id="52c41-205">This information is used for the JobTracker address for the cluster:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="52c41-206">Cette commande renvoie des informations semblables au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="52c41-206">This returns information similar to the following text:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="52c41-207">Le port utilisé pour JobTracker est 8050. Ainsi, l’adresse complète à utiliser pour JobTracker est la suivante : `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span><span class="sxs-lookup"><span data-stu-id="52c41-207">The port used for the JobTracker is 8050, so the full address to use for the JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="52c41-208">Utilisez la commande suivante pour créer la configuration de définition de travail Oozie :</span><span class="sxs-lookup"><span data-stu-id="52c41-208">Use the following to create the Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="52c41-209">Une fois que l’éditeur nano est ouvert, utilisez le code XML suivant comme contenu du fichier :</span><span class="sxs-lookup"><span data-stu-id="52c41-209">Once the nano editor opens, use the following XML as the contents of the file:</span></span>

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
        <name>nameNode</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
        </property>

        <property>
        <name>jobTracker</name>
        <value>JOBTRACKERADDRESS</value>
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
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/useooziewf.hql</value>
        </property>

        <property>
        <name>hiveTableName</name>
        <value>mobilecount</value>
        </property>

        <property>
        <name>hiveDataFolder</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/data</value>
        </property>

        <property>
        <name>sqlDatabaseConnectionString</name>
        <value>"jdbc:sqlserver://serverName.database.windows.net;user=adminLogin;password=adminPassword;database=oozietest"</value>
        </property>

        <property>
        <name>sqlDatabaseTableName</name>
        <value>mobiledata</value>
        </property>

        <property>
        <name>user.name</name>
        <value>YourName</value>
        </property>

        <property>
        <name>oozie.wf.application.path</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
    </configuration>
    ```

   * <span data-ttu-id="52c41-210">Remplacez toutes les instances de **wasb://mycontainer@mystorageaccount.blob.core.windows.net** par la valeur que vous avez reçue précédemment pour le stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="52c41-210">Replace all instances of **wasb://mycontainer@mystorageaccount.blob.core.windows.net** with the value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="52c41-211">Si le chemin d’accès est un chemin `wasb`, vous devez utiliser le chemin d’accès complet.</span><span class="sxs-lookup"><span data-stu-id="52c41-211">If the path is a `wasb` path, you must use the full path.</span></span> <span data-ttu-id="52c41-212">Ne le limitez pas simplement à `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="52c41-212">Do not shorten it to just `wasb:///`.</span></span>

   * <span data-ttu-id="52c41-213">Remplacez **JOBTRACKERADDRESS** par l’adresse de JobTracker/ResourceManager reçue précédemment.</span><span class="sxs-lookup"><span data-stu-id="52c41-213">Replace **JOBTRACKERADDRESS** with the JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="52c41-214">Remplacez **YourName** par votre nom de connexion pour le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="52c41-214">Replace **YourName** with your login name for the HDInsight cluster.</span></span>
   * <span data-ttu-id="52c41-215">Remplacez **serverName**, **adminLogin** et **adminPassword** par les informations de votre Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="52c41-215">Replace **serverName**, **adminLogin**, and **adminPassword** with the information for your Azure SQL Database.</span></span>

     <span data-ttu-id="52c41-216">La plupart des informations de ce fichier sont utilisées pour remplir les valeurs utilisées dans les fichiers workflow.xml ou ooziewf.hql (comme ${nameNode}).</span><span class="sxs-lookup"><span data-stu-id="52c41-216">Most of the information in this file is used to populate the values used in the workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="52c41-217">L’entrée **oozie.wf.application.path** définit l’emplacement du fichier workflow.xml, qui contient le flux de travail exécuté par ce travail.</span><span class="sxs-lookup"><span data-stu-id="52c41-217">The **oozie.wf.application.path** entry defines where to find the workflow.xml file, which contains the workflow ran by this job.</span></span>

5. <span data-ttu-id="52c41-218">Utilisez Ctrl-X, puis **Y** et **Entrée** pour enregistrer le fichier.</span><span class="sxs-lookup"><span data-stu-id="52c41-218">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

## <a name="submit-and-manage-the-job"></a><span data-ttu-id="52c41-219">Soumission et gestion du travail</span><span class="sxs-lookup"><span data-stu-id="52c41-219">Submit and manage the job</span></span>

<span data-ttu-id="52c41-220">Les étapes suivantes utilisent la commande Oozie pour soumettre et gérer des flux de travail Oozie sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="52c41-220">The following steps use the Oozie command to submit and manage Oozie workflows on the cluster.</span></span> <span data-ttu-id="52c41-221">La commande Oozie est une interface conviviale sur l’ [API REST Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="52c41-221">The Oozie command is a friendly interface over the [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52c41-222">Lorsque vous utilisez la commande Oozie, vous devez utiliser le nom de domaine complet pour le nœud principal HDInsight.</span><span class="sxs-lookup"><span data-stu-id="52c41-222">When using the Oozie command, you must use the FQDN for the HDInsight headnode.</span></span> <span data-ttu-id="52c41-223">Ce nom de domaine complet est uniquement accessible à partir du cluster, ou, si le cluster se trouve sur un réseau virtuel Azure, à partir des autres ordinateurs sur le même réseau.</span><span class="sxs-lookup"><span data-stu-id="52c41-223">This FQDN is only accessible from the cluster, or if the cluster is on an Azure Virtual Network, from other machines on the same network.</span></span>


1. <span data-ttu-id="52c41-224">Utilisez la commande suivante pour obtenir l’URL du service Oozie :</span><span class="sxs-lookup"><span data-stu-id="52c41-224">Use the following to obtain the URL to the Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="52c41-225">Cette commande renvoie des informations semblables au code XML suivant :</span><span class="sxs-lookup"><span data-stu-id="52c41-225">This returns information similar to the following XML:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="52c41-226">La partie `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` correspond à l’URL à utiliser avec la commande Oozie.</span><span class="sxs-lookup"><span data-stu-id="52c41-226">The `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is the URL to use with the Oozie command.</span></span>

2. <span data-ttu-id="52c41-227">Pour créer une variable d’environnement pour l’URL de manière à ne pas être obligé de la taper pour chaque commande :</span><span class="sxs-lookup"><span data-stu-id="52c41-227">Use the following to create an environment variable for the URL, so you don't have to type it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="52c41-228">Remplacez l’URL par celle reçue précédemment.</span><span class="sxs-lookup"><span data-stu-id="52c41-228">Replace the URL with the one you received earlier.</span></span>
3. <span data-ttu-id="52c41-229">Pour envoyer le travail, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52c41-229">Use the following to submit the job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="52c41-230">Cette commande charge les informations du travail à partir de **job.xml** et les envoie à Oozie, mais n’exécute pas le travail.</span><span class="sxs-lookup"><span data-stu-id="52c41-230">This command loads the job information from **job.xml** and submits it to Oozie, but does not run it.</span></span>

    <span data-ttu-id="52c41-231">Une fois la commande terminée, elle retourne normalement l’ID du travail.</span><span class="sxs-lookup"><span data-stu-id="52c41-231">Once the command completes, it should return the ID of the job.</span></span> <span data-ttu-id="52c41-232">Par exemple, `0000005-150622124850154-oozie-oozi-W`.</span><span class="sxs-lookup"><span data-stu-id="52c41-232">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="52c41-233">Cet ID est utilisé pour gérer le travail.</span><span class="sxs-lookup"><span data-stu-id="52c41-233">This ID is used to manage the job.</span></span>

4. <span data-ttu-id="52c41-234">Affichez l’état du travail à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52c41-234">View the status of the job using the following command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > <span data-ttu-id="52c41-235">Remplacez `<JOBID>` par l’ID renvoyé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="52c41-235">Replace `<JOBID>` with the ID returned in the previous step.</span></span>

    <span data-ttu-id="52c41-236">Cette commande renvoie des informations semblables au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="52c41-236">This returns information similar to the following text:</span></span>

    ```
    Job ID : 0000005-150622124850154-oozie-oozi-W
    ------------------------------------------------------------------------------------------------------------------------------------
    Workflow Name : useooziewf
    App Path      : wasb:///tutorials/useoozie
    Status        : PREP
    Run           : 0
    User          : USERNAME
    Group         : -
    Created       : 2015-06-22 15:06 GMT
    Started       : -
    Last Modified : 2015-06-22 15:06 GMT
    Ended         : -
    CoordAction ID: -
    ------------------------------------------------------------------------------------------------------------------------------------
    ```

    <span data-ttu-id="52c41-237">Ce travail a le statut `PREP`,</span><span class="sxs-lookup"><span data-stu-id="52c41-237">This job has a status of `PREP`.</span></span> <span data-ttu-id="52c41-238">Cet état indique que le travail a été créé, mais qu’il n’a pas commencé.</span><span class="sxs-lookup"><span data-stu-id="52c41-238">This status indicates that the job was created, but not started.</span></span>

5. <span data-ttu-id="52c41-239">Utilisez la commande suivante pour démarrer le travail :</span><span class="sxs-lookup"><span data-stu-id="52c41-239">Use the following command to start the job:</span></span>

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > <span data-ttu-id="52c41-240">Remplacez `<JOBID>` par l’ID renvoyé précédemment.</span><span class="sxs-lookup"><span data-stu-id="52c41-240">Replace `<JOBID>` with the ID returned previously.</span></span>

    <span data-ttu-id="52c41-241">Si vous vérifiez l’état après cette commande, il sera en cours d’exécution et des informations pour les actions au sein du travail seront retournées.</span><span class="sxs-lookup"><span data-stu-id="52c41-241">If you check the status after this command, it is in a running state, and information is returned for the actions within the job.</span></span>

6. <span data-ttu-id="52c41-242">Une fois le travail terminé correctement, vous pouvez vérifier que les données ont été générées et exportées vers la table de base de données SQL en utilisant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="52c41-242">Once the task completes successfully, you can verify that the data was generated and exported to the SQL Database table by using the following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="52c41-243">À l’invite de commandes `1>` , entrez la requête suivante :</span><span class="sxs-lookup"><span data-stu-id="52c41-243">At the `1>` prompt, enter the following query:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="52c41-244">Les informations renvoyées sont semblables à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="52c41-244">The information returned is similar to the following text:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="52c41-245">Pour plus d’informations sur la commande Oozie, consultez la page [Outil en ligne de commande Oozie](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span><span class="sxs-lookup"><span data-stu-id="52c41-245">For more information on the Oozie command, see [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="52c41-246">API REST Oozie</span><span class="sxs-lookup"><span data-stu-id="52c41-246">Oozie REST API</span></span>

<span data-ttu-id="52c41-247">L’API REST Oozie vous permet de créer vos propres outils fonctionnant avec Oozie.</span><span class="sxs-lookup"><span data-stu-id="52c41-247">The Oozie REST API allows you to build your own tools that work with Oozie.</span></span> <span data-ttu-id="52c41-248">Les informations suivantes sont des informations spécifiques de HDInsight sur l’utilisation de l’API REST Oozie :</span><span class="sxs-lookup"><span data-stu-id="52c41-248">The following are HDInsight specific information about using the Oozie REST API:</span></span>

* <span data-ttu-id="52c41-249">**URI** : l’API REST est accessible depuis l’extérieur du cluster à l’adresse `https://CLUSTERNAME.azurehdinsight.net/oozie`</span><span class="sxs-lookup"><span data-stu-id="52c41-249">**URI**: The REST API can be accessed from outside the cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="52c41-250">**Authentification** : authentifiez-vous à l’API en utilisant le compte HTTP (admin) et le mot de passe du cluster.</span><span class="sxs-lookup"><span data-stu-id="52c41-250">**Authentication**: Authenticate to the API using the cluster HTTP account (admin) and password.</span></span> <span data-ttu-id="52c41-251">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="52c41-251">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="52c41-252">Pour plus d'informations sur l’utilisation de l’API REST Oozie, consultez la page [API des services web Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="52c41-252">For more information on using the Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="52c41-253">Interface utilisateur web Oozie</span><span class="sxs-lookup"><span data-stu-id="52c41-253">Oozie Web UI</span></span>

<span data-ttu-id="52c41-254">L’interface utilisateur web Oozie fournit une vue web de l’état des travaux Oozie sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="52c41-254">The Oozie Web UI provides a web-based view into the status of Oozie jobs on the cluster.</span></span> <span data-ttu-id="52c41-255">L’interface utilisateur web vous permet d’afficher les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="52c41-255">The web UI allows you to view the following information:</span></span>

* <span data-ttu-id="52c41-256">Statut de tâche</span><span class="sxs-lookup"><span data-stu-id="52c41-256">Job status</span></span>
* <span data-ttu-id="52c41-257">Définition du travail</span><span class="sxs-lookup"><span data-stu-id="52c41-257">Job definition</span></span>
* <span data-ttu-id="52c41-258">Configuration</span><span class="sxs-lookup"><span data-stu-id="52c41-258">Configuration</span></span>
* <span data-ttu-id="52c41-259">Un graphique des actions exécutées sur le travail</span><span class="sxs-lookup"><span data-stu-id="52c41-259">A graph of the actions in the job</span></span>
* <span data-ttu-id="52c41-260">Les journaux du travail</span><span class="sxs-lookup"><span data-stu-id="52c41-260">Logs for the job</span></span>

<span data-ttu-id="52c41-261">Vous pouvez également afficher les détails pour les actions du travail.</span><span class="sxs-lookup"><span data-stu-id="52c41-261">You can also view details for actions within a job.</span></span>

<span data-ttu-id="52c41-262">Pour accéder à l'interface utilisateur web Oozie, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="52c41-262">To access the Oozie Web UI, use the following steps:</span></span>

1. <span data-ttu-id="52c41-263">Créez un tunnel SSH vers le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="52c41-263">Create an SSH tunnel to the HDInsight cluster.</span></span> <span data-ttu-id="52c41-264">Pour plus d’informations, consultez le document [Utilisation du tunnel SSH avec HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="52c41-264">For information, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="52c41-265">Une fois qu’un tunnel a été créé, ouvrez l’interface utilisateur web Ambari dans votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="52c41-265">Once a tunnel has been created, open the Ambari web UI in your web browser.</span></span> <span data-ttu-id="52c41-266">L’URI du site Ambari est **https://CLUSTERNAME.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="52c41-266">The URI for the Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="52c41-267">Remplacez **CLUSTERNAME** par le nom de votre cluster HDInsight basé sur Linux.</span><span class="sxs-lookup"><span data-stu-id="52c41-267">Replace **CLUSTERNAME** with the name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="52c41-268">Sur le côté gauche de la page, sélectionnez **Oozie**, puis **Liens rapides**, et enfin **Interface utilisateur web Oozie**.</span><span class="sxs-lookup"><span data-stu-id="52c41-268">From the left side of the page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![image des menus](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="52c41-270">L’interface utilisateur web Oozie affiche par défaut les travaux du flux de travail en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="52c41-270">The Oozie Web UI defaults to displaying running Workflow Jobs.</span></span> <span data-ttu-id="52c41-271">Pour voir tous les travaux du flux de travail, sélectionnez **Tous les travaux**.</span><span class="sxs-lookup"><span data-stu-id="52c41-271">To see all workflow jobs, select **All Jobs**.</span></span>

    ![Tous les travaux affichés](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="52c41-273">Sélectionnez un travail pour afficher plus d’informations sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="52c41-273">Select a job to view more information about the job.</span></span>

    ![Job Info](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="52c41-275">Sous l’onglet Job Info, vous pouvez voir les informations de base sur le travail, ainsi que les actions individuelles au sein du travail.</span><span class="sxs-lookup"><span data-stu-id="52c41-275">From the Job Info tab, you can see basic job information and the individual actions within the job.</span></span> <span data-ttu-id="52c41-276">Les onglets visibles en haut de la page vous permettent d’afficher la définition du travail et la configuration du travail, d’accéder au journal du travail ou d’afficher un graphique non cyclique dirigé du travail.</span><span class="sxs-lookup"><span data-stu-id="52c41-276">Using the tabs at the top you can view the Job Definition, Job Configuration, access the Job Log or view a Directed Acyclic Graph (DAG) of the job.</span></span>

   * <span data-ttu-id="52c41-277">**Job Log** : cliquez sur le bouton **GetLogs** pour obtenir tous les journaux du travail, ou utilisez le champ **Enter Search Filter** pour filtrer les journaux.</span><span class="sxs-lookup"><span data-stu-id="52c41-277">**Job Log**: Select the **GetLogs** button to get all logs for the job, or use the **Enter Search Filter** field to filter logs</span></span>

       ![Journal du travail](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="52c41-279">**JobDAG**: le graphique non cyclique dirigé est une représentation graphique des chemins de données utilisés à travers le flux de travail.</span><span class="sxs-lookup"><span data-stu-id="52c41-279">**JobDAG**: The DAG is a graphical overview of the data paths taken through the workflow</span></span>

       ![Graphique non cyclique dirigé du travail](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="52c41-281">Lorsque vous sélectionnez l’une des actions sous l’onglet **Infos travail**, des informations sur l’action s’affichent.</span><span class="sxs-lookup"><span data-stu-id="52c41-281">Selecting one of the actions from the **Job Info** tab brings up information for the action.</span></span> <span data-ttu-id="52c41-282">Par exemple, sélectionnez l’action **RunHiveScript** .</span><span class="sxs-lookup"><span data-stu-id="52c41-282">For example, select the **RunHiveScript** action.</span></span>

    ![Informations sur l’action](./media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="52c41-284">Vous pouvez voir les détails de l’action, notamment un lien vers **l’URL de la console**</span><span class="sxs-lookup"><span data-stu-id="52c41-284">You can see details for the action, such as a link to the **Console URL**.</span></span> <span data-ttu-id="52c41-285">qui peut être utilisé pour afficher les informations de JobTracker pour le travail.</span><span class="sxs-lookup"><span data-stu-id="52c41-285">This link can be used to view JobTracker information for the job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="52c41-286">Planification des travaux</span><span class="sxs-lookup"><span data-stu-id="52c41-286">Scheduling jobs</span></span>

<span data-ttu-id="52c41-287">Le coordinateur vous permet de spécifier le début, la fin et la fréquence d’occurrence des travaux.</span><span class="sxs-lookup"><span data-stu-id="52c41-287">The coordinator allows you to specify a start, end, and occurrence frequency for jobs.</span></span> <span data-ttu-id="52c41-288">Pour définir une planification pour le flux de travail, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="52c41-288">To define a schedule for the workflow, use the following steps:</span></span>

1. <span data-ttu-id="52c41-289">Utilisez la commande suivante pour créer un fichier nommé **coordinator.xml** :</span><span class="sxs-lookup"><span data-stu-id="52c41-289">Use the following to create a file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="52c41-290">Utilisez le code XML suivant comme contenu du fichier :</span><span class="sxs-lookup"><span data-stu-id="52c41-290">Use the following XML as the contents of the file:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
        <workflow>
            <app-path>${workflowPath}</app-path>
        </workflow>
        </action>
    </coordinator-app>
    ```

    > [!NOTE]
    > <span data-ttu-id="52c41-291">Les variables `${...}` sont remplacées par des valeurs dans la définition du travail lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="52c41-291">The `${...}` variables are replaced by values in the job definition at run-time.</span></span> <span data-ttu-id="52c41-292">Les variables sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="52c41-292">The variables are:</span></span>
    >
    > * <span data-ttu-id="52c41-293">`${coordFrequency}` : délai entre les instances du travail en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="52c41-293">`${coordFrequency}`: Time between running instances of the job.</span></span>
    > <span data-ttu-id="52c41-294">** `${coordStart}` : heure de début du travail.</span><span class="sxs-lookup"><span data-stu-id="52c41-294">** `${coordStart}`: The job start time.</span></span>
    > * <span data-ttu-id="52c41-295">`${coordEnd}` : heure de fin du travail.</span><span class="sxs-lookup"><span data-stu-id="52c41-295">`${coordEnd}`: The job end time.</span></span>
    > * <span data-ttu-id="52c41-296">`${coordTimezone}`: les travaux du coordinateur se trouvent dans un fuseau horaire fixe sans passage à l’heure d’été (généralement représenté par UTC).</span><span class="sxs-lookup"><span data-stu-id="52c41-296">`${coordTimezone}`: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="52c41-297">Ce fuseau horaire est appelé le « fuseau horaire du traitement d’Oozie ».</span><span class="sxs-lookup"><span data-stu-id="52c41-297">This time zone is referred as the "Oozie processing timezone."</span></span>
    > * <span data-ttu-id="52c41-298">`${wfPath}` : chemin d’accès au fichier workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="52c41-298">`${wfPath}`: The path to the workflow.xml.</span></span>

2. <span data-ttu-id="52c41-299">Sélectionnez Ctrl+X, **Y**, puis **Entrée** pour enregistrer le fichier.</span><span class="sxs-lookup"><span data-stu-id="52c41-299">To save the file, use Ctrl-X, **Y**, and **Enter**.</span></span>

3. <span data-ttu-id="52c41-300">Pour le copier dans le répertoire de travail pour ce travail, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52c41-300">Use the following command to copy the file to the working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="52c41-301">Utilisez la commande suivante pour modifier le fichier **job.xml** :</span><span class="sxs-lookup"><span data-stu-id="52c41-301">Use the following to modify the **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="52c41-302">Effectuez les modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="52c41-302">Make the following changes:</span></span>

   * <span data-ttu-id="52c41-303">Pour ordonner à Oozie d’exécuter le fichier coordinateur au lieu du fichier de workflow, remplacez `<name>oozie.wf.application.path</name>` par `<name>oozie.coord.application.path</name>`.</span><span class="sxs-lookup"><span data-stu-id="52c41-303">To instruct oozie to run the coordinator file instead of the workflow, change `<name>oozie.wf.application.path</name>` to `<name>oozie.coord.application.path</name>`.</span></span>

   * <span data-ttu-id="52c41-304">Pour définir la variable `workflowPath` utilisée par le coordinateur, ajoutez le code XML suivant :</span><span class="sxs-lookup"><span data-stu-id="52c41-304">To set the `workflowPath` variable used by the coordinator, add the following XML:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="52c41-305">Remplacez le texte `wasb://mycontainer@mystorageaccount.blob.core.windows` par la valeur utilisée dans les autres entrées du fichier job.xml.</span><span class="sxs-lookup"><span data-stu-id="52c41-305">Replace the `wasb://mycontainer@mystorageaccount.blob.core.windows` text with the value used in other entries in the job.xml file.</span></span>

   * <span data-ttu-id="52c41-306">Pour définir le début, la fin et la fréquence correspondant au coordinateur, ajoutez le code XML suivant :</span><span class="sxs-lookup"><span data-stu-id="52c41-306">To define the start, end, and frequency for the coordinator, add the following XML:</span></span>

        ```xml
        <property>
            <name>coordStart</name>
            <value>2017-05-10T12:00Z</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>2017-05-12T12:00Z</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>1440</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>UTC</value>
        </property>
        ```

       <span data-ttu-id="52c41-307">Ces valeurs définissent l’heure de début sur 12 h 00 le 10 mai 2017 et la fin sur le 12 mai 2017.</span><span class="sxs-lookup"><span data-stu-id="52c41-307">These values set the start time to 12:00PM on May 10, 2017, the end time to May 12, 2017.</span></span> <span data-ttu-id="52c41-308">L’intervalle d’exécution de ce travail est quotidien.</span><span class="sxs-lookup"><span data-stu-id="52c41-308">The interval for running this job daily.</span></span> <span data-ttu-id="52c41-309">La fréquence est exprimée en minutes, par conséquent, 24 heures x 60 minutes = 1 440 minutes.</span><span class="sxs-lookup"><span data-stu-id="52c41-309">The frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="52c41-310">Enfin, le fuseau horaire est défini au format UTC.</span><span class="sxs-lookup"><span data-stu-id="52c41-310">Finally, the timezone is set to UTC.</span></span>

5. <span data-ttu-id="52c41-311">Utilisez Ctrl-X, puis **Y** et **Entrée** pour enregistrer le fichier.</span><span class="sxs-lookup"><span data-stu-id="52c41-311">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

6. <span data-ttu-id="52c41-312">Utilisez la commande suivante pour exécuter le travail :</span><span class="sxs-lookup"><span data-stu-id="52c41-312">To run the job, use the following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="52c41-313">Cette commande envoie et démarre le travail.</span><span class="sxs-lookup"><span data-stu-id="52c41-313">This command submits and starts the job.</span></span>

7. <span data-ttu-id="52c41-314">Si vous accédez à l’interface utilisateur web Oozie et sélectionnez l’onglet **Travaux du coordinateur**, vous obtenez des informations semblables à l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="52c41-314">If you visit the Oozie Web UI and select the **Coordinator Jobs** tab, you see information similar to the following image:</span></span>

    ![Onglet Travaux du coordinateur](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="52c41-316">L’entrée **Next Materialization** (Matérialisation suivante) indique l’heure de la prochaine exécution du travail.</span><span class="sxs-lookup"><span data-stu-id="52c41-316">The **Next Materialization** entry contains the next time that the job runs.</span></span>

8. <span data-ttu-id="52c41-317">De même que pour le workflow précédent, lorsque vous sélectionnez l’entrée du travail dans l’interface utilisateur web, des informations sur le travail s’affichent :</span><span class="sxs-lookup"><span data-stu-id="52c41-317">Similar to the earlier workflow job, selecting the job entry in the web UI displays information on the job:</span></span>

    ![Informations sur les travaux du coordinateur](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > <span data-ttu-id="52c41-319">L’image affiche uniquement les exécutions réussies du travail, et non les actions individuelles dans le workflow planifié.</span><span class="sxs-lookup"><span data-stu-id="52c41-319">This image only shows successful runs of the job, not individual actions within the scheduled workflow.</span></span> <span data-ttu-id="52c41-320">Pour voir ces dernières, sélectionnez l’une des entrées **Action** .</span><span class="sxs-lookup"><span data-stu-id="52c41-320">To see that, select one of the **Action** entries.</span></span>

    ![Informations sur l’action](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="52c41-322">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="52c41-322">Troubleshooting</span></span>

<span data-ttu-id="52c41-323">L’interface utilisateur Oozie vous permet d’afficher les journaux Oozie.</span><span class="sxs-lookup"><span data-stu-id="52c41-323">The Oozie UI allows you to view Oozie logs.</span></span> <span data-ttu-id="52c41-324">Elle contient également des liens vers les journaux JobTracker pour les tâches MapReduce démarrées par le workflow.</span><span class="sxs-lookup"><span data-stu-id="52c41-324">It also contains links to JobTracker logs for MapReduce tasks started by the workflow.</span></span> <span data-ttu-id="52c41-325">Le modèle pour la résolution des problèmes doit être le suivant :</span><span class="sxs-lookup"><span data-stu-id="52c41-325">The pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="52c41-326">Afficher le travail dans l’interface utilisateur web Oozie.</span><span class="sxs-lookup"><span data-stu-id="52c41-326">View the job in Oozie Web UI.</span></span>

2. <span data-ttu-id="52c41-327">En cas d’erreur ou d’échec d’une action spécifique, sélectionnez l’action pour voir si le champ **Message d’erreur** fournit plus d’informations sur l’échec.</span><span class="sxs-lookup"><span data-stu-id="52c41-327">If there is an error or failure for a specific action, select the action to see if the **Error Message** field provides more information on the failure.</span></span>

3. <span data-ttu-id="52c41-328">Si elle est disponible, utilisez l’URL de l’action pour afficher des détails supplémentaires (tels que les journaux JobTracker) pour l’action.</span><span class="sxs-lookup"><span data-stu-id="52c41-328">If available, use the URL from the action to view more details (such as JobTracker logs) for the action.</span></span>

<span data-ttu-id="52c41-329">Voici des erreurs spécifiques que vous pouvez rencontrer avec une description de la marche à suivre pour les résoudre.</span><span class="sxs-lookup"><span data-stu-id="52c41-329">The following are specific errors you may encounter, and how to resolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="52c41-330">JA009 : Cannot initialize cluster (Impossible d'initialiser le cluster)</span><span class="sxs-lookup"><span data-stu-id="52c41-330">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="52c41-331">**Symptômes** : l’état du travail devient **SUSPENDED**.</span><span class="sxs-lookup"><span data-stu-id="52c41-331">**Symptoms**: The job status changes to **SUSPENDED**.</span></span> <span data-ttu-id="52c41-332">Dans les détails du travail, **START_MANUAL** est affiché pour l’état de RunHiveScript.</span><span class="sxs-lookup"><span data-stu-id="52c41-332">Details for the job show the RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="52c41-333">Lorsque vous sélectionnez l’action, le message d’erreur suivant apparaît :</span><span class="sxs-lookup"><span data-stu-id="52c41-333">Selecting the action displays the following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="52c41-334">**Cause** : les adresses WASB utilisées dans le fichier **job.xml** ne contiennent pas le conteneur de stockage ou le nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="52c41-334">**Cause**: The WASB addresses used in the **job.xml** file do not contain the storage container or storage account name.</span></span> <span data-ttu-id="52c41-335">Le format d’adresse WASB doit être `wasb://containername@storageaccountname.blob.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="52c41-335">The WASB address format must be `wasb://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="52c41-336">**Résolution**: modifiez les adresses WASB utilisées par le travail.</span><span class="sxs-lookup"><span data-stu-id="52c41-336">**Resolution**: Change the WASB addresses used by the job.</span></span>

### <a name="ja002-oozie-is-not-allowed-to-impersonate-ltuser"></a><span data-ttu-id="52c41-337">JA002 : Oozie is not allowed to impersonate &lt;USER> (Oozie ne peut pas emprunter l’identité USER>)</span><span class="sxs-lookup"><span data-stu-id="52c41-337">JA002: Oozie is not allowed to impersonate &lt;USER></span></span>

<span data-ttu-id="52c41-338">**Symptômes** : l’état du travail devient **SUSPENDED**.</span><span class="sxs-lookup"><span data-stu-id="52c41-338">**Symptoms**: The job status changes to **SUSPENDED**.</span></span> <span data-ttu-id="52c41-339">Dans les détails du travail, **START_MANUAL** est affiché pour l’état de RunHiveScript.</span><span class="sxs-lookup"><span data-stu-id="52c41-339">Details for the job show the RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="52c41-340">Lorsque vous sélectionnez l’action, le message d’erreur suivant apparaît :</span><span class="sxs-lookup"><span data-stu-id="52c41-340">Selecting the action shows the following error message:</span></span>

    JA002: User: oozie is not allowed to impersonate <USER>

<span data-ttu-id="52c41-341">**Cause**: les paramètres d’autorisation actuels ne permettent pas à Oozie d’emprunter l’identité du compte d’utilisateur spécifié.</span><span class="sxs-lookup"><span data-stu-id="52c41-341">**Cause**: Current permission settings do not allow Oozie to impersonate the specified user account.</span></span>

<span data-ttu-id="52c41-342">**Résolution** : Oozie est autorisé à emprunter l’identité des utilisateurs dans le groupe **users**.</span><span class="sxs-lookup"><span data-stu-id="52c41-342">**Resolution**: Oozie is allowed to impersonate users in the **users** group.</span></span> <span data-ttu-id="52c41-343">Utilisez le `groups USERNAME` pour voir les groupes dont le compte d’utilisateur est membre.</span><span class="sxs-lookup"><span data-stu-id="52c41-343">Use the `groups USERNAME` to see the groups that the user account is a member of.</span></span> <span data-ttu-id="52c41-344">Si l’utilisateur n’est pas membre du groupe **users** , utilisez la commande suivante pour ajouter l’utilisateur au groupe :</span><span class="sxs-lookup"><span data-stu-id="52c41-344">If the user is not a member of the **users** group, use the following command to add the user to the group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="52c41-345">Il peut se passer plusieurs minutes avant que HDInsight reconnaisse que l'utilisateur a été ajouté au groupe.</span><span class="sxs-lookup"><span data-stu-id="52c41-345">It may take several minutes before HDInsight recognizes that the user has been added to the group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="52c41-346">Launcher ERROR (Sqoop) (Erreur du lanceur, Sqoop)</span><span class="sxs-lookup"><span data-stu-id="52c41-346">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="52c41-347">**Symptômes** : l’état du travail devient **KILLED**.</span><span class="sxs-lookup"><span data-stu-id="52c41-347">**Symptoms**: The job status changes to **KILLED**.</span></span> <span data-ttu-id="52c41-348">Les détails du travail affichent **ERROR** pour l’état de RunSqoopExport.</span><span class="sxs-lookup"><span data-stu-id="52c41-348">Details for the job show the RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="52c41-349">Lorsque vous sélectionnez l’action, le message d’erreur suivant apparaît :</span><span class="sxs-lookup"><span data-stu-id="52c41-349">Selecting the action shows the following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="52c41-350">**Cause**: Sqoop ne peut pas charger le pilote de base de données requis pour accéder à la base de données.</span><span class="sxs-lookup"><span data-stu-id="52c41-350">**Cause**: Sqoop is unable to load the database driver required to access the database.</span></span>

<span data-ttu-id="52c41-351">**Résolution** : lors de l’utilisation de Sqoop à partir d’un travail Oozie, vous devez inclure le pilote de base de données avec les autres ressources (telles que workflow.xml) utilisées par le travail.</span><span class="sxs-lookup"><span data-stu-id="52c41-351">**Resolution**: When using Sqoop from an Oozie job, you must include the database driver with the other resources (such as the workflow.xml) used by the job.</span></span> <span data-ttu-id="52c41-352">Vous devez également référencer l’archive contenant le pilote de base de données à partir de la section `<sqoop>...</sqoop>` de workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="52c41-352">Also Reference the archive containing the database driver from the `<sqoop>...</sqoop>` section of the workflow.xml.</span></span>

<span data-ttu-id="52c41-353">Par exemple, pour le travail de ce document, vous utiliseriez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="52c41-353">For example, for the job in this document, you would use the following steps:</span></span>

1. <span data-ttu-id="52c41-354">Copier le fichier sqljdbc4.1.jar dans le répertoire /tutorials/useoozie :</span><span class="sxs-lookup"><span data-stu-id="52c41-354">Copy the sqljdbc4.1.jar file to the /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="52c41-355">Modifier le fichier workflow.xml pour ajouter le code XML suivant sur une nouvelle ligne au-dessus de `</sqoop>` :</span><span class="sxs-lookup"><span data-stu-id="52c41-355">Modify the workflow.xml to add the following XML on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="52c41-356">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="52c41-356">Next steps</span></span>

<span data-ttu-id="52c41-357">Dans ce didacticiel, vous avez appris comment définir un flux de travail Oozie et comment exécuter un travail Oozie.</span><span class="sxs-lookup"><span data-stu-id="52c41-357">In this tutorial, you learned how to define an Oozie workflow and how to run an Oozie job.</span></span> <span data-ttu-id="52c41-358">Pour en savoir plus sur l’utilisation de HDInsight, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="52c41-358">To learn more about working with HDInsight, see the following articles:</span></span>

* <span data-ttu-id="52c41-359">[Utilisation du coordinateur Oozie basé sur le temps avec HDInsight][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="52c41-359">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="52c41-360">[Importation de données pour les tâches Hadoop dans HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="52c41-360">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="52c41-361">[Utilisation de Sqoop avec Hadoop dans HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="52c41-361">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="52c41-362">[Utilisation de Hive avec Hadoop sur HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="52c41-362">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="52c41-363">[Utilisation de Pig avec Hadoop sur HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="52c41-363">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="52c41-364">[Développement de programmes MapReduce en Java pour HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="52c41-364">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563
[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started]: hdinsight-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started-emulator]: hdinsight-get-started-emulator.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: sql-database-create-configure.md
[sqldatabase-get-started]: sql-database-get-started.md

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
