---
title: "flux de travail aaaUse Oozie de Hadoop dans HDInsight de basés sur Linux | Documents Microsoft"
description: "Utilisation de Hadoop Oozie dans HDInsight basé sur Linux. Découvrez comment toodefine Oozie d’un flux de travail et soumettre un travail Oozie."
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
ms.openlocfilehash: cb5682837543312621e3424b7a9341b5d2a00bf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="088be-104">Utilisez Oozie avec Hadoop toodefine et exécuter un workflow sur HDInsight de basés sur Linux</span><span class="sxs-lookup"><span data-stu-id="088be-104">Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="088be-105">Découvrez comment toouse Oozie Apache avec Hadoop dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="088be-105">Learn how toouse Apache Oozie with Hadoop on HDInsight.</span></span> <span data-ttu-id="088be-106">Apache Oozie est un système de workflow/coordination qui gère les tâches Hadoop.</span><span class="sxs-lookup"><span data-stu-id="088be-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="088be-107">Oozie est intégré à la pile de Hadoop hello, et il prend en charge hello suivant de tâches :</span><span class="sxs-lookup"><span data-stu-id="088be-107">Oozie is integrated with hello Hadoop stack, and it supports hello following jobs:</span></span>

* <span data-ttu-id="088be-108">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="088be-108">Apache MapReduce</span></span>
* <span data-ttu-id="088be-109">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="088be-109">Apache Pig</span></span>
* <span data-ttu-id="088be-110">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="088be-110">Apache Hive</span></span>
* <span data-ttu-id="088be-111">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="088be-111">Apache Sqoop</span></span>

<span data-ttu-id="088be-112">Oozie peut également être utilisé tooschedule les travaux système tooa spécifiques, tels que les programmes Java ou des scripts de shell</span><span class="sxs-lookup"><span data-stu-id="088be-112">Oozie can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="088be-113">Une autre option pour définir des flux de travail avec HDInsight consiste à utiliser Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="088be-113">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="088be-114">toolearn en savoir plus sur Azure Data Factory, consultez [utilisez Pig et Hive avec Data Factory][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="088be-114">toolearn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="088be-115">Oozie n’est pas activé sur HDInsight joint à un domaine.</span><span class="sxs-lookup"><span data-stu-id="088be-115">Oozie is not enabled on domain-joined HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="088be-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="088be-116">Prerequisites</span></span>

* <span data-ttu-id="088be-117">**Un cluster HDInsight**: consultez la page [Prise en main de HDInsight sur Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="088be-117">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="088be-118">étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux.</span><span class="sxs-lookup"><span data-stu-id="088be-118">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="088be-119">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="088be-119">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="088be-120">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="088be-120">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="example-workflow"></a><span data-ttu-id="088be-121">Exemple de flux de travail</span><span class="sxs-lookup"><span data-stu-id="088be-121">Example workflow</span></span>

<span data-ttu-id="088be-122">flux de travail Hello utilisé dans ce document contient deux actions.</span><span class="sxs-lookup"><span data-stu-id="088be-122">hello workflow used in this document contains two actions.</span></span> <span data-ttu-id="088be-123">Les actions sont des définitions de tâches, telles que l’exécution de Hive, Sqoop, MapReduce ou un autre processus :</span><span class="sxs-lookup"><span data-stu-id="088be-123">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![Diagramme du workflow][img-workflow-diagram]

1. <span data-ttu-id="088be-125">Une ruche action s’exécute un script HiveQL tooextract enregistrements à partir de hello **hivesampletable** inclus avec HDInsight.</span><span class="sxs-lookup"><span data-stu-id="088be-125">A Hive action runs a HiveQL script tooextract records from hello **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="088be-126">Chaque ligne de données décrit un accès depuis un appareil mobile spécifique.</span><span class="sxs-lookup"><span data-stu-id="088be-126">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="088be-127">le format d’enregistrement Hello apparaît toohello similaire après le texte :</span><span class="sxs-lookup"><span data-stu-id="088be-127">hello record format appears similar toohello following text:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="088be-128">Hello script Hive utilisé dans ce document compte le nombre total de visites hello pour chaque plateforme (par exemple, Android ou iPhone) et stocke les nombres hello tooa nouvelle table de ruche.</span><span class="sxs-lookup"><span data-stu-id="088be-128">hello Hive script used in this document counts hello total visits for each platform (such as Android or iPhone) and stores hello counts tooa new Hive table.</span></span>

    <span data-ttu-id="088be-129">Pour plus d’informations sur Hive, consultez l’article [Utilisation de Hive avec HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="088be-129">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="088be-130">Une action Sqoop exporte contenu hello de hello nouvelle table tooa table Hive dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="088be-130">A Sqoop action exports hello contents of hello new Hive table tooa table in an Azure SQL database.</span></span> <span data-ttu-id="088be-131">Pour plus d’informations sur Sqoop, consultez la rubrique [Utilisation de Hadoop Sqoop avec HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="088be-131">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="088be-132">Pour les versions Oozie prises en charge sur les clusters HDInsight, consultez [quelles sont les nouveautés dans les versions de cluster Hadoop hello fournies par HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="088be-132">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-hello-working-directory"></a><span data-ttu-id="088be-133">Créer le répertoire de travail hello</span><span class="sxs-lookup"><span data-stu-id="088be-133">Create hello working directory</span></span>

<span data-ttu-id="088be-134">Oozie attend des ressources requises pour un travail toobe stockée Bonjour même répertoire.</span><span class="sxs-lookup"><span data-stu-id="088be-134">Oozie expects resources required for a job toobe stored in hello same directory.</span></span> <span data-ttu-id="088be-135">Cet exemple utilise **wasb:///tutorials/useoozie**.</span><span class="sxs-lookup"><span data-stu-id="088be-135">This example uses **wasb:///tutorials/useoozie**.</span></span> <span data-ttu-id="088be-136">Utilisez hello suivant commande toocreate ce répertoire et le répertoire de données hello qui contient la nouvelle table Hive hello, créé par ce flux de travail :</span><span class="sxs-lookup"><span data-stu-id="088be-136">Use hello following command toocreate this directory, and hello data directory that holds hello new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="088be-137">Hello `-p` paramètre indique tous les répertoires dans hello toobe de chemin d’accès créé.</span><span class="sxs-lookup"><span data-stu-id="088be-137">hello `-p` parameter causes all directories in hello path toobe created.</span></span> <span data-ttu-id="088be-138">Hello **données** répertoire est données toohold utilisé utilisées par hello **useooziewf.hql** script.</span><span class="sxs-lookup"><span data-stu-id="088be-138">hello **data** directory is used toohold data used by hello **useooziewf.hql** script.</span></span>

<span data-ttu-id="088be-139">Également exécuter hello suivant de commande, ce qui garantit que Oozie peut emprunter l’identité de votre compte d’utilisateur lors de l’exécution de tâches Hive et Sqoop.</span><span class="sxs-lookup"><span data-stu-id="088be-139">Also run hello following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="088be-140">Remplacez **USERNAME** par votre nom de connexion :</span><span class="sxs-lookup"><span data-stu-id="088be-140">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

> [!NOTE]
> <span data-ttu-id="088be-141">Vous pouvez ignorer les erreurs de cet utilisateur hello est déjà membre de hello `users` groupe.</span><span class="sxs-lookup"><span data-stu-id="088be-141">You can ignore errors that hello user is already a member of hello `users` group.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="088be-142">Ajout d’un pilote de base de données</span><span class="sxs-lookup"><span data-stu-id="088be-142">Add a database driver</span></span>

<span data-ttu-id="088be-143">Étant donné que ce flux de travail utilise Sqoop tooexport tooSQL de données de base de données, vous devez fournir qu'une copie du pilote JDBC de hello utilisé tootalk tooSQL base de données.</span><span class="sxs-lookup"><span data-stu-id="088be-143">Since this workflow uses Sqoop tooexport data tooSQL Database, you must provide a copy of hello JDBC driver used tootalk tooSQL Database.</span></span> <span data-ttu-id="088be-144">Utilisez hello suivant toocopy de commande de répertoire de travail toohello :</span><span class="sxs-lookup"><span data-stu-id="088be-144">Use hello following command toocopy it toohello working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="088be-145">Si votre flux de travail utilisé les autres ressources, telles que fichier jar contenant une application MapReduce, vous devez tooadd également ces ressources.</span><span class="sxs-lookup"><span data-stu-id="088be-145">If your workflow used other resources, such as a jar containing a MapReduce application, you would need tooadd these resources as well.</span></span>

## <a name="define-hello-hive-query"></a><span data-ttu-id="088be-146">Définir la requête Hive de hello</span><span class="sxs-lookup"><span data-stu-id="088be-146">Define hello Hive query</span></span>

<span data-ttu-id="088be-147">Utilisez hello suivant les étapes toocreate un script HiveQL qui définit une requête, qui est utilisée dans un flux de travail Oozie plus loin dans ce document.</span><span class="sxs-lookup"><span data-stu-id="088be-147">Use hello following steps toocreate a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="088be-148">Connectez le cluster toohello à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="088be-148">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="088be-149">Bonjour commande suivante est un exemple d’utilisation hello `ssh` commande.</span><span class="sxs-lookup"><span data-stu-id="088be-149">hello following command is an example of using hello `ssh` command.</span></span> <span data-ttu-id="088be-150">Remplacez __nom d’utilisateur__ avec l’utilisateur SSH hello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-150">Replace __USERNAME__ with hello SSH user for hello cluster.</span></span> <span data-ttu-id="088be-151">Remplacez __CLUSTERNAME__ avec nom hello du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-151">Replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="088be-152">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="088be-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="088be-153">À partir de hello connexion SSH, utilisez hello suivant commande toocreate un fichier :</span><span class="sxs-lookup"><span data-stu-id="088be-153">From hello SSH connection, use hello following command toocreate a file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="088be-154">Une fois que l’éditeur de nano hello s’ouvre, utilisez hello suivant la requête en tant que contenu hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="088be-154">Once hello nano editor opens, use hello following query as hello contents of hello file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="088be-155">Il existe deux variables utilisées dans un script de hello :</span><span class="sxs-lookup"><span data-stu-id="088be-155">There are two variables used in hello script:</span></span>

    * <span data-ttu-id="088be-156">**${hiveTableName}**: contient le nom hello de hello toobe de table créé</span><span class="sxs-lookup"><span data-stu-id="088be-156">**${hiveTableName}**: contains hello name of hello table toobe created</span></span>

    * <span data-ttu-id="088be-157">**${hiveDataFolder}**: contient les fichiers de données hello emplacement toostore hello pour la table de hello</span><span class="sxs-lookup"><span data-stu-id="088be-157">**${hiveDataFolder}**: contains hello location toostore hello data files for hello table</span></span>

    <span data-ttu-id="088be-158">le fichier de définition de flux de travail Hello (workflow.xml dans ce didacticiel) passe ces toothis valeurs HiveQL script en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="088be-158">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time</span></span>

4. <span data-ttu-id="088be-159">éditeur de hello tooexit, appuyez sur Ctrl-X.</span><span class="sxs-lookup"><span data-stu-id="088be-159">tooexit hello editor, press Ctrl-X.</span></span> <span data-ttu-id="088be-160">Lorsque vous y êtes invité, sélectionnez **Y** toosave hello du fichier, puis utilisez **entrée** toouse hello **useooziewf.hql** nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="088be-160">When prompted, select **Y** toosave hello file, then use **Enter** toouse hello **useooziewf.hql** file name.</span></span>

5. <span data-ttu-id="088be-161">Suivant de hello utilisez commandes toocopy **useooziewf.hql** trop**wasb:///tutorials/useoozie/useooziewf.hql**:</span><span class="sxs-lookup"><span data-stu-id="088be-161">Use hello following commands toocopy **useooziewf.hql** too**wasb:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="088be-162">Ces commandes stockent hello **useooziewf.hql** fichier sur un stockage hello HDFS compatibles pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-162">These commands store hello **useooziewf.hql** file on hello HDFS-compatible storage for hello cluster.</span></span>

## <a name="define-hello-workflow"></a><span data-ttu-id="088be-163">Définir le flux de travail hello</span><span class="sxs-lookup"><span data-stu-id="088be-163">Define hello workflow</span></span>

<span data-ttu-id="088be-164">Les définitions des workflows Oozie sont écrites en hPDL (un langage de définition du processus XML).</span><span class="sxs-lookup"><span data-stu-id="088be-164">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="088be-165">Utilisez hello suivant du flux de travail suit toodefine hello :</span><span class="sxs-lookup"><span data-stu-id="088be-165">Use hello following steps toodefine hello workflow:</span></span>

1. <span data-ttu-id="088be-166">Utilisez hello suivant l’instruction toocreate et modifier un fichier :</span><span class="sxs-lookup"><span data-stu-id="088be-166">Use hello following statement toocreate and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="088be-167">Une fois que l’éditeur de nano hello s’ouvre, entrez hello XML suivant comme contenu du fichier hello :</span><span class="sxs-lookup"><span data-stu-id="088be-167">Once hello nano editor opens, enter hello following XML as hello file contents:</span></span>

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

    <span data-ttu-id="088be-168">Il existe deux actions définies dans le flux de travail hello :</span><span class="sxs-lookup"><span data-stu-id="088be-168">There are two actions defined in hello workflow:</span></span>

   * <span data-ttu-id="088be-169">**RunHiveScript**: cette action est l’action de démarrage hello et s’exécute hello **useooziewf.hql** script Hive</span><span class="sxs-lookup"><span data-stu-id="088be-169">**RunHiveScript**: This action is hello start action, and runs hello **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="088be-170">**RunSqoopExport**: cette action exporte les données de hello créées à partir de hello ruche script tooSQL Sqoop à l’aide de la base de données.</span><span class="sxs-lookup"><span data-stu-id="088be-170">**RunSqoopExport**: This action exports hello data created from hello Hive script tooSQL Database using Sqoop.</span></span> <span data-ttu-id="088be-171">Cette action s’exécute uniquement si hello **RunHiveScript** action a abouti.</span><span class="sxs-lookup"><span data-stu-id="088be-171">This action only runs if hello **RunHiveScript** action is successful.</span></span>

     <span data-ttu-id="088be-172">flux de travail Hello a plusieurs entrées, telles que `${jobTracker}`.</span><span class="sxs-lookup"><span data-stu-id="088be-172">hello workflow has several entries, such as `${jobTracker}`.</span></span> <span data-ttu-id="088be-173">Ces entrées sont remplacées par les valeurs que vous utilisez dans la définition de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="088be-173">These entries are replaced by values you use in hello job definition.</span></span> <span data-ttu-id="088be-174">définition de la tâche Hello est créée ultérieurement dans ce document.</span><span class="sxs-lookup"><span data-stu-id="088be-174">hello job definition is created later in this document.</span></span>

     <span data-ttu-id="088be-175">Hello de note également `<archive>sqljdbc4.jar</arcive>` entrée Bonjour Sqoop section.</span><span class="sxs-lookup"><span data-stu-id="088be-175">Also note hello `<archive>sqljdbc4.jar</arcive>` entry in hello Sqoop section.</span></span> <span data-ttu-id="088be-176">Cette entrée indique au Oozie toomake cette archive disponible pour Sqoop lors de l’exécution de cette action.</span><span class="sxs-lookup"><span data-stu-id="088be-176">This entry instructs Oozie toomake this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="088be-177">Utilisez Ctrl-X, puis **Y** et **entrée** fichier hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="088be-177">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

4. <span data-ttu-id="088be-178">Suivant de hello utilisez commande toocopy hello **workflow.xml** trop de fichiers**/tutorials/useoozie/workflow.xml**:</span><span class="sxs-lookup"><span data-stu-id="088be-178">Use hello following command toocopy hello **workflow.xml** file too**/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a><span data-ttu-id="088be-179">Créer la base de données hello</span><span class="sxs-lookup"><span data-stu-id="088be-179">Create hello database</span></span>

<span data-ttu-id="088be-180">toocreate une base de données SQL Azure, suivez les étapes de hello Bonjour [créer une base de données SQL](../sql-database/sql-database-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="088be-180">toocreate an Azure SQL Database, follow hello steps in hello [Create a SQL Database](../sql-database/sql-database-get-started.md) document.</span></span> <span data-ttu-id="088be-181">Lors de la création de la base de données hello, utilisez `oozietest` comme nom de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="088be-181">When creating hello database, use `oozietest` as hello database name.</span></span> <span data-ttu-id="088be-182">Notez également du nom de hello du serveur de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="088be-182">Also make a note of hello name of hello database server.</span></span>

### <a name="create-hello-table"></a><span data-ttu-id="088be-183">Créer la table de hello</span><span class="sxs-lookup"><span data-stu-id="088be-183">Create hello table</span></span>

> [!NOTE]
> <span data-ttu-id="088be-184">Il existe de nombreuses façons tooconnect tooSQL base de données toocreate une table.</span><span class="sxs-lookup"><span data-stu-id="088be-184">There are many ways tooconnect tooSQL Database toocreate a table.</span></span> <span data-ttu-id="088be-185">Hello suivant l’utilisation d’étapes [FreeTDS](http://www.freetds.org/) à partir du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-185">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="088be-186">Utilisez hello suivant de commande tooinstall FreeTDS de cluster HDInsight de hello :</span><span class="sxs-lookup"><span data-stu-id="088be-186">Use hello following command tooinstall FreeTDS on hello HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="088be-187">Une fois que FreeTDS a été installé, utilisez hello suivant du serveur de base de données SQL commandes tooconnect toohello que vous avez créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="088be-187">Once FreeTDS has been installed, use hello following command tooconnect toohello SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="088be-188">Vous recevez toohello similaire de sortie suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="088be-188">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. <span data-ttu-id="088be-189">À hello `1>` invite, entrez hello lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="088be-189">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="088be-190">Hello lorsque `GO` instruction est entrée, les instructions précédentes hello sont évaluées.</span><span class="sxs-lookup"><span data-stu-id="088be-190">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="088be-191">Ces instructions créent une table nommée **mobiledata** qui est utilisé par les flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="088be-191">These statements create a table named **mobiledata** that is used by hello workflow.</span></span>

    <span data-ttu-id="088be-192">Hello utilisation suivant tooverify qui hello table a été créé :</span><span class="sxs-lookup"><span data-stu-id="088be-192">Use hello following tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="088be-193">Vous consultez toohello similaire de sortie suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="088be-193">You see output similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="088be-194">Entrez `exit` à hello `1>` tooexit hello tsql utilitaire d’invite.</span><span class="sxs-lookup"><span data-stu-id="088be-194">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="create-hello-job-definition"></a><span data-ttu-id="088be-195">Créer la définition de la tâche hello</span><span class="sxs-lookup"><span data-stu-id="088be-195">Create hello job definition</span></span>

<span data-ttu-id="088be-196">définition de la tâche Hello décrit où toofind hello workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="088be-196">hello job definition describes where toofind hello workflow.xml.</span></span> <span data-ttu-id="088be-197">Il explique également où toofind autres fichiers utilisés par le flux de travail hello (par exemple, useooziewf.hql.) Il définit également les valeurs hello pour les propriétés utilisées dans le flux de travail hello et fichiers associés.</span><span class="sxs-lookup"><span data-stu-id="088be-197">It also describes where toofind other files used by hello workflow (such as useooziewf.hql.) It also defines hello values for properties used within hello workflow and associated files.</span></span>

1. <span data-ttu-id="088be-198">Utilisez hello commande tooget hello adresse complète du stockage par défaut de hello suivante.</span><span class="sxs-lookup"><span data-stu-id="088be-198">Use hello following command tooget hello full address of hello default storage.</span></span> <span data-ttu-id="088be-199">Cette adresse est utilisée dans le fichier de configuration hello dans un instant :</span><span class="sxs-lookup"><span data-stu-id="088be-199">This address is used in hello configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="088be-200">Cette commande retourne des informations similaires toohello est XML suivant :</span><span class="sxs-lookup"><span data-stu-id="088be-200">This command returns information similar toohello following XML:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="088be-201">Si le cluster HDInsight de hello utilise le stockage Azure en tant que stockage par défaut de hello, hello `<value>` le contenu d’éléments commence par `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="088be-201">If hello HDInsight cluster uses Azure Storage as hello default storage, hello `<value>` element contents begin with `wasb://`.</span></span> <span data-ttu-id="088be-202">En revanche, si Azure Data Lake Store est utilisé, il commence par `adl://`.</span><span class="sxs-lookup"><span data-stu-id="088be-202">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="088be-203">Enregistrer le contenu de hello hello `<value>` élément, tel qu’il est utilisé dans les étapes suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="088be-203">Save hello contents of hello `<value>` element, as it is used in hello next steps.</span></span>

2. <span data-ttu-id="088be-204">Utilisez hello suivant commande tooget nom de domaine complet du nœud principal de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="088be-204">Use hello following command tooget FQDN of hello cluster headnode.</span></span> <span data-ttu-id="088be-205">Ces informations sont utilisées pour hello adresse JobTracker pour le cluster de hello :</span><span class="sxs-lookup"><span data-stu-id="088be-205">This information is used for hello JobTracker address for hello cluster:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="088be-206">Cet exemple renvoie toohello similaire à informations suivant le texte :</span><span class="sxs-lookup"><span data-stu-id="088be-206">This returns information similar toohello following text:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="088be-207">Hello port utilisé pour hello JobTracker étant 8050, toouse d’adresse complète hello pour hello JobTracker est `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span><span class="sxs-lookup"><span data-stu-id="088be-207">hello port used for hello JobTracker is 8050, so hello full address toouse for hello JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="088be-208">Utilisez hello toocreate hello Oozie travail définition configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="088be-208">Use hello following toocreate hello Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="088be-209">Une fois que l’éditeur de nano hello s’ouvre, utilisez hello XML suivant comme contenu hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="088be-209">Once hello nano editor opens, use hello following XML as hello contents of hello file:</span></span>

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

   * <span data-ttu-id="088be-210">Remplacez toutes les instances de  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  avec la valeur hello reçu précédemment pour le stockage de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="088be-210">Replace all instances of **wasb://mycontainer@mystorageaccount.blob.core.windows.net** with hello value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="088be-211">Si le chemin d’accès hello est un `wasb` chemin d’accès, vous devez utiliser le chemin d’accès complet de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-211">If hello path is a `wasb` path, you must use hello full path.</span></span> <span data-ttu-id="088be-212">Ne le diminuez pas toojust `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="088be-212">Do not shorten it toojust `wasb:///`.</span></span>

   * <span data-ttu-id="088be-213">Remplacez **JOBTRACKERADDRESS** avec hello adresse JobTracker/ResourceManager reçu précédemment.</span><span class="sxs-lookup"><span data-stu-id="088be-213">Replace **JOBTRACKERADDRESS** with hello JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="088be-214">Remplacez **votrenom** avec votre nom de connexion pour le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-214">Replace **YourName** with your login name for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="088be-215">Remplacez **nom_serveur**, **adminLogin**, et **adminPassword** avec des informations de hello pour votre base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="088be-215">Replace **serverName**, **adminLogin**, and **adminPassword** with hello information for your Azure SQL Database.</span></span>

     <span data-ttu-id="088be-216">La plupart des informations hello dans ce fichier est toopopulate utilisé les valeurs hello utilisés dans les fichiers de hello workflow.xml ou ooziewf.hql (par exemple, ${nameNode}.)</span><span class="sxs-lookup"><span data-stu-id="088be-216">Most of hello information in this file is used toopopulate hello values used in hello workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="088be-217">Hello **oozie.wf.application.path** entrée définit où fichier workflow.xml toofind hello, qui contient le flux de travail hello exécuté par ce travail.</span><span class="sxs-lookup"><span data-stu-id="088be-217">hello **oozie.wf.application.path** entry defines where toofind hello workflow.xml file, which contains hello workflow ran by this job.</span></span>

5. <span data-ttu-id="088be-218">Utilisez Ctrl-X, puis **Y** et **entrée** fichier hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="088be-218">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

## <a name="submit-and-manage-hello-job"></a><span data-ttu-id="088be-219">Soumettre et de gérer le travail de hello</span><span class="sxs-lookup"><span data-stu-id="088be-219">Submit and manage hello job</span></span>

<span data-ttu-id="088be-220">Hello suit hello Oozie commande toosubmit et gérer des flux de travail Oozie sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-220">hello following steps use hello Oozie command toosubmit and manage Oozie workflows on hello cluster.</span></span> <span data-ttu-id="088be-221">Hello Oozie commande est une interface conviviale sur hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="088be-221">hello Oozie command is a friendly interface over hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="088be-222">Lorsque vous utilisez la commande de hello Oozie, vous devez utiliser hello nom de domaine complet pour le nœud principal de HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="088be-222">When using hello Oozie command, you must use hello FQDN for hello HDInsight headnode.</span></span> <span data-ttu-id="088be-223">Ce nom de domaine complet n’est accessible à partir du cluster de hello, ou si hello cluster se trouve sur un réseau virtuel Azure, à partir d’autres ordinateurs sur hello même réseau.</span><span class="sxs-lookup"><span data-stu-id="088be-223">This FQDN is only accessible from hello cluster, or if hello cluster is on an Azure Virtual Network, from other machines on hello same network.</span></span>


1. <span data-ttu-id="088be-224">Utilisez hello après tooobtain hello URL toohello Oozie service :</span><span class="sxs-lookup"><span data-stu-id="088be-224">Use hello following tooobtain hello URL toohello Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="088be-225">Cet exemple renvoie toohello similaires à des informations XML suivant :</span><span class="sxs-lookup"><span data-stu-id="088be-225">This returns information similar toohello following XML:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="088be-226">Hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` partie est toouse d’URL hello avec hello Oozie commande.</span><span class="sxs-lookup"><span data-stu-id="088be-226">hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is hello URL toouse with hello Oozie command.</span></span>

2. <span data-ttu-id="088be-227">Hello utilisation suivant toocreate une variable d’environnement pour l’URL de hello, donc vous n’avez pas tootype pour chaque commande :</span><span class="sxs-lookup"><span data-stu-id="088be-227">Use hello following toocreate an environment variable for hello URL, so you don't have tootype it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="088be-228">Remplacer les URL hello hello un reçu précédemment.</span><span class="sxs-lookup"><span data-stu-id="088be-228">Replace hello URL with hello one you received earlier.</span></span>
3. <span data-ttu-id="088be-229">Utilisez hello suivant le travail de hello toosubmit :</span><span class="sxs-lookup"><span data-stu-id="088be-229">Use hello following toosubmit hello job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="088be-230">Cette commande charge des informations sur les travaux hello de **job.xml** et la soumet tooOozie, mais ne s’exécute ne pas.</span><span class="sxs-lookup"><span data-stu-id="088be-230">This command loads hello job information from **job.xml** and submits it tooOozie, but does not run it.</span></span>

    <span data-ttu-id="088be-231">Une fois la commande hello terminée, elle doit retourner hello des ID de tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-231">Once hello command completes, it should return hello ID of hello job.</span></span> <span data-ttu-id="088be-232">Par exemple, `0000005-150622124850154-oozie-oozi-W`.</span><span class="sxs-lookup"><span data-stu-id="088be-232">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="088be-233">Cet ID est un travail de hello toomanage utilisé.</span><span class="sxs-lookup"><span data-stu-id="088be-233">This ID is used toomanage hello job.</span></span>

4. <span data-ttu-id="088be-234">Afficher l’état de hello du travail hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="088be-234">View hello status of hello job using hello following command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > <span data-ttu-id="088be-235">Remplacez `<JOBID>` par hello ID retourné à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-235">Replace `<JOBID>` with hello ID returned in hello previous step.</span></span>

    <span data-ttu-id="088be-236">Cet exemple renvoie toohello similaire à informations suivant le texte :</span><span class="sxs-lookup"><span data-stu-id="088be-236">This returns information similar toohello following text:</span></span>

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

    <span data-ttu-id="088be-237">Ce travail a le statut `PREP`,</span><span class="sxs-lookup"><span data-stu-id="088be-237">This job has a status of `PREP`.</span></span> <span data-ttu-id="088be-238">Cet état indique que le travail hello a été créé, mais n’a pas démarré.</span><span class="sxs-lookup"><span data-stu-id="088be-238">This status indicates that hello job was created, but not started.</span></span>

5. <span data-ttu-id="088be-239">Utilisez hello suivant le travail de commande toostart hello :</span><span class="sxs-lookup"><span data-stu-id="088be-239">Use hello following command toostart hello job:</span></span>

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > <span data-ttu-id="088be-240">Remplacez `<JOBID>` par hello ID retourné précédemment.</span><span class="sxs-lookup"><span data-stu-id="088be-240">Replace `<JOBID>` with hello ID returned previously.</span></span>

    <span data-ttu-id="088be-241">Si vous vérifiez l’état de hello après cette commande, il est en cours d’exécution, et informations sont retournées pour les actions de hello dans le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-241">If you check hello status after this command, it is in a running state, and information is returned for hello actions within hello job.</span></span>

6. <span data-ttu-id="088be-242">Une fois la tâche hello se termine correctement, vous pouvez vérifier que les données de salutation a été générées et exportés de table de base de données SQL toohello à l’aide de hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="088be-242">Once hello task completes successfully, you can verify that hello data was generated and exported toohello SQL Database table by using hello following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="088be-243">À hello `1>` invite, entrez hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="088be-243">At hello `1>` prompt, enter hello following query:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="088be-244">les informations de Hello retournées sont similaires toohello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="088be-244">hello information returned is similar toohello following text:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="088be-245">Pour plus d’informations sur hello Oozie commande, consultez [outil de ligne de commande Oozie](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span><span class="sxs-lookup"><span data-stu-id="088be-245">For more information on hello Oozie command, see [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="088be-246">API REST Oozie</span><span class="sxs-lookup"><span data-stu-id="088be-246">Oozie REST API</span></span>

<span data-ttu-id="088be-247">Hello Oozie REST API vous permet de toobuild vos propres outils qui fonctionnent avec Oozie.</span><span class="sxs-lookup"><span data-stu-id="088be-247">hello Oozie REST API allows you toobuild your own tools that work with Oozie.</span></span> <span data-ttu-id="088be-248">Hello Voici HDInsight des informations spécifiques sur l’utilisation de hello Oozie REST API :</span><span class="sxs-lookup"><span data-stu-id="088be-248">hello following are HDInsight specific information about using hello Oozie REST API:</span></span>

* <span data-ttu-id="088be-249">**URI**: hello API REST sont accessibles à partir de l’extérieur cluster hello à`https://CLUSTERNAME.azurehdinsight.net/oozie`</span><span class="sxs-lookup"><span data-stu-id="088be-249">**URI**: hello REST API can be accessed from outside hello cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="088be-250">**Authentification**: authentifier API toohello à l’aide du compte de cluster HTTP hello (administrateur) et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="088be-250">**Authentication**: Authenticate toohello API using hello cluster HTTP account (admin) and password.</span></span> <span data-ttu-id="088be-251">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="088be-251">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="088be-252">Pour plus d’informations sur l’utilisation de hello Oozie REST API, consultez [API des Services Web Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="088be-252">For more information on using hello Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="088be-253">Interface utilisateur web Oozie</span><span class="sxs-lookup"><span data-stu-id="088be-253">Oozie Web UI</span></span>

<span data-ttu-id="088be-254">Hello l’interface utilisateur Web de Oozie offre une vue basée sur le web état hello de Oozie travaux sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-254">hello Oozie Web UI provides a web-based view into hello status of Oozie jobs on hello cluster.</span></span> <span data-ttu-id="088be-255">interface utilisateur web de Hello permet hello tooview informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="088be-255">hello web UI allows you tooview hello following information:</span></span>

* <span data-ttu-id="088be-256">Statut de tâche</span><span class="sxs-lookup"><span data-stu-id="088be-256">Job status</span></span>
* <span data-ttu-id="088be-257">Définition du travail</span><span class="sxs-lookup"><span data-stu-id="088be-257">Job definition</span></span>
* <span data-ttu-id="088be-258">Configuration</span><span class="sxs-lookup"><span data-stu-id="088be-258">Configuration</span></span>
* <span data-ttu-id="088be-259">Un graphique des actions hello dans la tâche de hello</span><span class="sxs-lookup"><span data-stu-id="088be-259">A graph of hello actions in hello job</span></span>
* <span data-ttu-id="088be-260">Journaux hello travail</span><span class="sxs-lookup"><span data-stu-id="088be-260">Logs for hello job</span></span>

<span data-ttu-id="088be-261">Vous pouvez également afficher les détails pour les actions du travail.</span><span class="sxs-lookup"><span data-stu-id="088be-261">You can also view details for actions within a job.</span></span>

<span data-ttu-id="088be-262">tooaccess hello l’interface utilisateur Web de Oozie, utilisez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="088be-262">tooaccess hello Oozie Web UI, use hello following steps:</span></span>

1. <span data-ttu-id="088be-263">Créer un cluster de HDInsight de toohello tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="088be-263">Create an SSH tunnel toohello HDInsight cluster.</span></span> <span data-ttu-id="088be-264">Pour plus d’informations, consultez hello [utiliser SSH Tunneling hdinsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span><span class="sxs-lookup"><span data-stu-id="088be-264">For information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="088be-265">Une fois qu’un tunnel a été créé, ouvrez l’interface utilisateur web de Ambari hello dans votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="088be-265">Once a tunnel has been created, open hello Ambari web UI in your web browser.</span></span> <span data-ttu-id="088be-266">Hello URI pour le site de Ambari hello est **https://CLUSTERNAME.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="088be-266">hello URI for hello Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="088be-267">Remplacez **CLUSTERNAME** avec nom hello de votre cluster HDInsight de basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="088be-267">Replace **CLUSTERNAME** with hello name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="088be-268">Bonjour à gauche de la page de hello, sélectionnez **Oozie**, puis **liens rapides**et enfin **l’interface utilisateur Web de Oozie**.</span><span class="sxs-lookup"><span data-stu-id="088be-268">From hello left side of hello page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![image des menus de hello](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="088be-270">Bonjour toodisplaying de valeurs par défaut de l’interface utilisateur Web de Oozie tâches de Workflow en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="088be-270">hello Oozie Web UI defaults toodisplaying running Workflow Jobs.</span></span> <span data-ttu-id="088be-271">sélectionner de toutes les tâches de workflow, toosee **tous les travaux**.</span><span class="sxs-lookup"><span data-stu-id="088be-271">toosee all workflow jobs, select **All Jobs**.</span></span>

    ![Tous les travaux affichés](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="088be-273">Sélectionnez un travail tooview plus d’informations sur la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-273">Select a job tooview more information about hello job.</span></span>

    ![Job Info](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="088be-275">À partir de l’onglet informations du travail de hello, vous pouvez voir des informations sur les travaux de base et des actions individuelles hello dans le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-275">From hello Job Info tab, you can see basic job information and hello individual actions within hello job.</span></span> <span data-ttu-id="088be-276">À l’aide des onglets de hello haut hello, que vous pouvez afficher hello définition du travail, Configuration des tâches, hello d’accès journal des travaux ou afficher un dirigées acycliques graphique (DAG) du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-276">Using hello tabs at hello top you can view hello Job Definition, Job Configuration, access hello Job Log or view a Directed Acyclic Graph (DAG) of hello job.</span></span>

   * <span data-ttu-id="088be-277">**Journal des travaux**: hello sélectionnez **GetLogs** tooget tous les journaux hello travail ou pour utiliser hello **Entrez un filtre de recherche** champ toofilter journaux</span><span class="sxs-lookup"><span data-stu-id="088be-277">**Job Log**: Select hello **GetLogs** button tooget all logs for hello job, or use hello **Enter Search Filter** field toofilter logs</span></span>

       ![Journal du travail](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="088be-279">**JobDAG**: hello DAG est une représentation graphique des chemins d’accès de données hello effectuée par le biais du flux de travail hello</span><span class="sxs-lookup"><span data-stu-id="088be-279">**JobDAG**: hello DAG is a graphical overview of hello data paths taken through hello workflow</span></span>

       ![Graphique non cyclique dirigé du travail](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="088be-281">Sélectionner l’une des actions de hello dans hello **infos travail** onglet affiche des informations pour l’action de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-281">Selecting one of hello actions from hello **Job Info** tab brings up information for hello action.</span></span> <span data-ttu-id="088be-282">Par exemple, sélectionnez hello **RunHiveScript** action.</span><span class="sxs-lookup"><span data-stu-id="088be-282">For example, select hello **RunHiveScript** action.</span></span>

    ![Informations sur l’action](./media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="088be-284">Vous pouvez voir les détails pour hello action, comme un lien de toohello **URL de la Console**.</span><span class="sxs-lookup"><span data-stu-id="088be-284">You can see details for hello action, such as a link toohello **Console URL**.</span></span> <span data-ttu-id="088be-285">Ce lien peut renvoyer des informations de JobTracker tooview utilisé pour le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-285">This link can be used tooview JobTracker information for hello job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="088be-286">Planification des travaux</span><span class="sxs-lookup"><span data-stu-id="088be-286">Scheduling jobs</span></span>

<span data-ttu-id="088be-287">coordinateur de Hello vous permet de toospecify une fréquence d’occurrence, de début et de fin pour les travaux.</span><span class="sxs-lookup"><span data-stu-id="088be-287">hello coordinator allows you toospecify a start, end, and occurrence frequency for jobs.</span></span> <span data-ttu-id="088be-288">toodefine une planification de flux de travail hello, hello utilisation comme suit :</span><span class="sxs-lookup"><span data-stu-id="088be-288">toodefine a schedule for hello workflow, use hello following steps:</span></span>

1. <span data-ttu-id="088be-289">Hello utilisation suivant toocreate un fichier nommé **coordinator.xml**:</span><span class="sxs-lookup"><span data-stu-id="088be-289">Use hello following toocreate a file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="088be-290">Utilisez hello XML suivant comme contenu hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="088be-290">Use hello following XML as hello contents of hello file:</span></span>

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
    > <span data-ttu-id="088be-291">Hello `${...}` variables sont remplacées par les valeurs dans la définition de la tâche hello au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="088be-291">hello `${...}` variables are replaced by values in hello job definition at run-time.</span></span> <span data-ttu-id="088be-292">variables de Hello sont :</span><span class="sxs-lookup"><span data-stu-id="088be-292">hello variables are:</span></span>
    >
    > * <span data-ttu-id="088be-293">`${coordFrequency}`: Délai entre les instances de tâche de hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="088be-293">`${coordFrequency}`: Time between running instances of hello job.</span></span>
    > <span data-ttu-id="088be-294">** `${coordStart}`: heure de début du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-294">** `${coordStart}`: hello job start time.</span></span>
    > * <span data-ttu-id="088be-295">`${coordEnd}`: heure de fin de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="088be-295">`${coordEnd}`: hello job end time.</span></span>
    > * <span data-ttu-id="088be-296">`${coordTimezone}`: les travaux du coordinateur se trouvent dans un fuseau horaire fixe sans passage à l’heure d’été (généralement représenté par UTC).</span><span class="sxs-lookup"><span data-stu-id="088be-296">`${coordTimezone}`: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="088be-297">Ce fuseau horaire est appelé hello » Oozie traitement fuseau horaire. »</span><span class="sxs-lookup"><span data-stu-id="088be-297">This time zone is referred as hello "Oozie processing timezone."</span></span>
    > * <span data-ttu-id="088be-298">`${wfPath}`: hello workflow.xml toohello de chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="088be-298">`${wfPath}`: hello path toohello workflow.xml.</span></span>

2. <span data-ttu-id="088be-299">toosave hello, utilisez Ctrl-X, **Y**, et **entrée**.</span><span class="sxs-lookup"><span data-stu-id="088be-299">toosave hello file, use Ctrl-X, **Y**, and **Enter**.</span></span>

3. <span data-ttu-id="088be-300">Hello suivant commande toocopy hello toohello travail répertoire du fichier pour cette tâche, utilisez :</span><span class="sxs-lookup"><span data-stu-id="088be-300">Use hello following command toocopy hello file toohello working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="088be-301">Hello utilisation suivant toomodify hello **job.xml** fichier :</span><span class="sxs-lookup"><span data-stu-id="088be-301">Use hello following toomodify hello **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="088be-302">Rendre hello modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="088be-302">Make hello following changes:</span></span>

   * <span data-ttu-id="088be-303">fichier tooinstruct oozie toorun hello coordinator au lieu de flux de travail hello, modification `<name>oozie.wf.application.path</name>` trop`<name>oozie.coord.application.path</name>`.</span><span class="sxs-lookup"><span data-stu-id="088be-303">tooinstruct oozie toorun hello coordinator file instead of hello workflow, change `<name>oozie.wf.application.path</name>` too`<name>oozie.coord.application.path</name>`.</span></span>

   * <span data-ttu-id="088be-304">tooset hello `workflowPath` variable utilisée par le coordinateur de hello, ajouter hello XML suivant :</span><span class="sxs-lookup"><span data-stu-id="088be-304">tooset hello `workflowPath` variable used by hello coordinator, add hello following XML:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="088be-305">Remplacez hello `wasb://mycontainer@mystorageaccount.blob.core.windows` texte avec la valeur de hello utilisée dans d’autres entrées dans le fichier de job.xml hello.</span><span class="sxs-lookup"><span data-stu-id="088be-305">Replace hello `wasb://mycontainer@mystorageaccount.blob.core.windows` text with hello value used in other entries in hello job.xml file.</span></span>

   * <span data-ttu-id="088be-306">toodefine hello début, fin et la fréquence de coordinateur de hello, ajoutent hello XML suivant :</span><span class="sxs-lookup"><span data-stu-id="088be-306">toodefine hello start, end, and frequency for hello coordinator, add hello following XML:</span></span>

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

       <span data-ttu-id="088be-307">Ces valeurs définies hello début heure too12 : 00 PM sur 10 mai 2017, hello fin heure tooMay 12, 2017.</span><span class="sxs-lookup"><span data-stu-id="088be-307">These values set hello start time too12:00PM on May 10, 2017, hello end time tooMay 12, 2017.</span></span> <span data-ttu-id="088be-308">Intervalle Hello pour l’exécution de ce travail tous les jours.</span><span class="sxs-lookup"><span data-stu-id="088be-308">hello interval for running this job daily.</span></span> <span data-ttu-id="088be-309">fréquence de Hello est exprimée en minutes, par conséquent, 24 heures x 60 minutes = 1440 minutes.</span><span class="sxs-lookup"><span data-stu-id="088be-309">hello frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="088be-310">Enfin, hello timezone a la valeur tooUTC.</span><span class="sxs-lookup"><span data-stu-id="088be-310">Finally, hello timezone is set tooUTC.</span></span>

5. <span data-ttu-id="088be-311">Utilisez Ctrl-X, puis **Y** et **entrée** fichier hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="088be-311">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

6. <span data-ttu-id="088be-312">travail de hello toorun, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="088be-312">toorun hello job, use hello following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="088be-313">Cette commande envoie et démarre le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-313">This command submits and starts hello job.</span></span>

7. <span data-ttu-id="088be-314">Si vous visitez hello l’interface utilisateur Web de Oozie et sélectionnez hello **travaux du coordinateur** onglet, vous voyez toohello similaire à informations suivant image :</span><span class="sxs-lookup"><span data-stu-id="088be-314">If you visit hello Oozie Web UI and select hello **Coordinator Jobs** tab, you see information similar toohello following image:</span></span>

    ![Onglet Travaux du coordinateur](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="088be-316">Hello **matérialisation suivant** entrée contient hello prochaine hello s’exécute.</span><span class="sxs-lookup"><span data-stu-id="088be-316">hello **Next Materialization** entry contains hello next time that hello job runs.</span></span>

8. <span data-ttu-id="088be-317">Toohello similaire précédente tâche de workflow, sélection d’entrée de tâche hello dans l’interface utilisateur web de hello affiche des informations sur les travaux hello :</span><span class="sxs-lookup"><span data-stu-id="088be-317">Similar toohello earlier workflow job, selecting hello job entry in hello web UI displays information on hello job:</span></span>

    ![Informations sur les travaux du coordinateur](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > <span data-ttu-id="088be-319">Cette image montre uniquement réussies exécutions du travail de hello, pas les actions au sein du flux de travail hello planifiée.</span><span class="sxs-lookup"><span data-stu-id="088be-319">This image only shows successful runs of hello job, not individual actions within hello scheduled workflow.</span></span> <span data-ttu-id="088be-320">toosee qui, sélectionnez une des hello **Action** entrées.</span><span class="sxs-lookup"><span data-stu-id="088be-320">toosee that, select one of hello **Action** entries.</span></span>

    ![Informations sur l’action](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="088be-322">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="088be-322">Troubleshooting</span></span>

<span data-ttu-id="088be-323">Hello Oozie UI vous permet de tooview Oozie journaux.</span><span class="sxs-lookup"><span data-stu-id="088be-323">hello Oozie UI allows you tooview Oozie logs.</span></span> <span data-ttu-id="088be-324">Il contient également les journaux de tooJobTracker des liens pour les tâches MapReduce démarrés par le flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="088be-324">It also contains links tooJobTracker logs for MapReduce tasks started by hello workflow.</span></span> <span data-ttu-id="088be-325">modèle de Hello pour le dépannage doit être :</span><span class="sxs-lookup"><span data-stu-id="088be-325">hello pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="088be-326">Afficher le travail hello dans l’interface utilisateur Web de Oozie.</span><span class="sxs-lookup"><span data-stu-id="088be-326">View hello job in Oozie Web UI.</span></span>

2. <span data-ttu-id="088be-327">S’il existe une erreur ou un échec d’une action spécifique, sélectionnez hello action toosee si hello **Message d’erreur** champ fournit plus d’informations en cas d’échec hello.</span><span class="sxs-lookup"><span data-stu-id="088be-327">If there is an error or failure for a specific action, select hello action toosee if hello **Error Message** field provides more information on hello failure.</span></span>

3. <span data-ttu-id="088be-328">S’il est disponible, utilisez URL hello hello action tooview plus de détails (par exemple, les journaux JobTracker) pour l’action de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-328">If available, use hello URL from hello action tooview more details (such as JobTracker logs) for hello action.</span></span>

<span data-ttu-id="088be-329">Hello suivantes sont des erreurs spécifiques, vous pouvez rencontrer, et comment tooresolve les.</span><span class="sxs-lookup"><span data-stu-id="088be-329">hello following are specific errors you may encounter, and how tooresolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="088be-330">JA009 : Cannot initialize cluster (Impossible d'initialiser le cluster)</span><span class="sxs-lookup"><span data-stu-id="088be-330">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="088be-331">**Symptômes**: hello les changements d’état de tâche trop**SUSPENDED**.</span><span class="sxs-lookup"><span data-stu-id="088be-331">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="088be-332">Détails de tâche de hello indiquent l’état RunHiveScript hello **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="088be-332">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="088be-333">Sélection de l’action de hello affiche hello message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="088be-333">Selecting hello action displays hello following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="088be-334">**Cause**: hello adresses WASB utilisés Bonjour **job.xml** fichier ne contiennent pas de conteneur de stockage hello ou nom de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="088be-334">**Cause**: hello WASB addresses used in hello **job.xml** file do not contain hello storage container or storage account name.</span></span> <span data-ttu-id="088be-335">format d’adresse Hello WASB doit être `wasb://containername@storageaccountname.blob.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="088be-335">hello WASB address format must be `wasb://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="088be-336">**Résolution**: modifier les adresses hello WASB utilisés par le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-336">**Resolution**: Change hello WASB addresses used by hello job.</span></span>

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a><span data-ttu-id="088be-337">JA002 : Oozie n’est pas autorisée tooimpersonate &lt;utilisateur ></span><span class="sxs-lookup"><span data-stu-id="088be-337">JA002: Oozie is not allowed tooimpersonate &lt;USER></span></span>

<span data-ttu-id="088be-338">**Symptômes**: hello les changements d’état de tâche trop**SUSPENDED**.</span><span class="sxs-lookup"><span data-stu-id="088be-338">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="088be-339">Détails de tâche de hello indiquent l’état RunHiveScript hello **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="088be-339">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="088be-340">Action de hello cochant hello message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="088be-340">Selecting hello action shows hello following error message:</span></span>

    JA002: User: oozie is not allowed tooimpersonate <USER>

<span data-ttu-id="088be-341">**Cause**: paramètres d’autorisation actuels n’autorisent pas Oozie tooimpersonate hello de compte d’utilisateur spécifié.</span><span class="sxs-lookup"><span data-stu-id="088be-341">**Cause**: Current permission settings do not allow Oozie tooimpersonate hello specified user account.</span></span>

<span data-ttu-id="088be-342">**Résolution**: Oozie est autorisé aux utilisateurs de tooimpersonate Bonjour **utilisateurs** groupe.</span><span class="sxs-lookup"><span data-stu-id="088be-342">**Resolution**: Oozie is allowed tooimpersonate users in hello **users** group.</span></span> <span data-ttu-id="088be-343">Hello d’utilisation `groups USERNAME` groupes hello toosee hello du compte d’utilisateur est membre.</span><span class="sxs-lookup"><span data-stu-id="088be-343">Use hello `groups USERNAME` toosee hello groups that hello user account is a member of.</span></span> <span data-ttu-id="088be-344">Si l’utilisateur de hello n’est pas un membre de hello **utilisateurs** groupe, utilisez hello suivant du groupe de commandes tooadd hello utilisateur toohello :</span><span class="sxs-lookup"><span data-stu-id="088be-344">If hello user is not a member of hello **users** group, use hello following command tooadd hello user toohello group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="088be-345">Il peut prendre plusieurs minutes avant de HDInsight reconnaît que toohello groupe a été ajouté à cet utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="088be-345">It may take several minutes before HDInsight recognizes that hello user has been added toohello group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="088be-346">Launcher ERROR (Sqoop) (Erreur du lanceur, Sqoop)</span><span class="sxs-lookup"><span data-stu-id="088be-346">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="088be-347">**Symptômes**: hello les changements d’état de tâche trop**KILLED**.</span><span class="sxs-lookup"><span data-stu-id="088be-347">**Symptoms**: hello job status changes too**KILLED**.</span></span> <span data-ttu-id="088be-348">Détails de tâche de hello indiquent l’état RunSqoopExport hello **erreur**.</span><span class="sxs-lookup"><span data-stu-id="088be-348">Details for hello job show hello RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="088be-349">Action de hello cochant hello message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="088be-349">Selecting hello action shows hello following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="088be-350">**Cause**: Sqoop est impossible tooload hello pilote requis tooaccess hello base de données.</span><span class="sxs-lookup"><span data-stu-id="088be-350">**Cause**: Sqoop is unable tooload hello database driver required tooaccess hello database.</span></span>

<span data-ttu-id="088be-351">**Résolution**: lorsque vous utilisez Sqoop à partir d’un travail Oozie, vous devez inclure pilote de base de données hello avec hello autres ressources (par exemple hello workflow.xml) utilisés par le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="088be-351">**Resolution**: When using Sqoop from an Oozie job, you must include hello database driver with hello other resources (such as hello workflow.xml) used by hello job.</span></span> <span data-ttu-id="088be-352">Font également référence archive hello contenant le pilote de base de données hello de hello `<sqoop>...</sqoop>` section de hello workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="088be-352">Also Reference hello archive containing hello database driver from hello `<sqoop>...</sqoop>` section of hello workflow.xml.</span></span>

<span data-ttu-id="088be-353">Par exemple, pour la tâche hello dans ce document, vous utiliseriez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="088be-353">For example, for hello job in this document, you would use hello following steps:</span></span>

1. <span data-ttu-id="088be-354">Copie hello sqljdbc4.1.jar toohello /tutorials/useoozie répertoire du fichier :</span><span class="sxs-lookup"><span data-stu-id="088be-354">Copy hello sqljdbc4.1.jar file toohello /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="088be-355">Modifier le XML suivant sur une nouvelle ligne au-dessus de Bonjour workflow.xml tooadd Bonjour `</sqoop>`:</span><span class="sxs-lookup"><span data-stu-id="088be-355">Modify hello workflow.xml tooadd hello following XML on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="088be-356">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="088be-356">Next steps</span></span>

<span data-ttu-id="088be-357">Dans ce didacticiel, vous avez appris comment toodefine Oozie d’un flux de travail et comment toorun un travail Oozie.</span><span class="sxs-lookup"><span data-stu-id="088be-357">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job.</span></span> <span data-ttu-id="088be-358">toolearn en savoir plus sur l’utilisation de HDInsight, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="088be-358">toolearn more about working with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="088be-359">[Utilisation du coordinateur Oozie basé sur le temps avec HDInsight][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="088be-359">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="088be-360">[Importation de données pour les tâches Hadoop dans HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="088be-360">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="088be-361">[Utilisation de Sqoop avec Hadoop dans HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="088be-361">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="088be-362">[Utilisation de Hive avec Hadoop sur HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="088be-362">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="088be-363">[Utilisation de Pig avec Hadoop sur HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="088be-363">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="088be-364">[Développement de programmes MapReduce en Java pour HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="088be-364">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

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
