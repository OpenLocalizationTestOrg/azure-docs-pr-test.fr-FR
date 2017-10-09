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
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a>Utiliser coordinateur de Oozie temporels avec Hadoop dans HDInsight toodefine workflows et coordonner les travaux
Dans cet article, vous allez apprendre comment toodefine le flux de travail et les coordinateurs et comment tootrigger hello travaux du coordinateur, en fonction de temps. Il est utile toogo via [Oozie d’utilisation avec HDInsight] [ hdinsight-use-oozie] avant de lire cet article. En outre tooOozie, vous pouvez également planifier des travaux à l’aide d’Azure Data Factory. toolearn Azure Data Factory, consultez [utilisez Pig et Hive avec Data Factory](../data-factory/data-factory-data-transformation-activities.md).

> [!NOTE]
> Cet article requiert un cluster HDInsight basé sur Windows. Pour plus d’informations sur l’utilisation de Oozie, y compris des travaux basés sur un cluster basé sur Linux, consultez [Oozie utilisation avec Hadoop toodefine et exécuter un flux de travail sur HDInsight de basés sur Linux](hdinsight-use-oozie-linux-mac.md)

## <a name="what-is-oozie"></a>Présentation d'Oozie
Apache Oozie est un système de workflow/coordination qui gère les tâches Hadoop. Il est intégré à la pile de Hadoop hello, et il prend en charge les travaux Hadoop pour Apache MapReduce Apache Pig, Apache Hive et Sqoop d’Apache. Il peut également être utilisé tooschedule les travaux système tooa spécifiques, tels que les programmes Java ou des scripts de shell.

Hello image suivante montre les flux de travail hello que vous allez implémenter :

![Diagramme du workflow][img-workflow-diagram]

flux de travail Hello contient deux actions :

1. Une action de la ruche exécute un Bonjour toocount du script HiveQL occurrences de chaque type de niveau de journal dans un fichier de journal log4j. Chaque journal log4j se compose d’une ligne de champs qui contient une [niveau de journal] champ tooshow hello type hello gravité et, par exemple :

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    Hello sortie du script Hive est similaire à :

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    Pour plus d’informations sur Hive, consultez l’article [Utilisation de Hive avec HDInsight][hdinsight-use-hive].
2. Une action Sqoop exporte hello HiveQL action tooa table de sortie dans une base de données SQL Azure. Pour plus d'informations sur Sqoop, consultez la rubrique [Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop].

> [!NOTE]
> Pour les versions Oozie prises en charge sur les clusters HDInsight, consultez [quelles sont les nouveautés dans les versions de cluster hello fournies par HDInsight ?] [hdinsight-versions].
>
>

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer de hello :

* **Un poste de travail sur lequel est installé Azure PowerShell**.

    > [!IMPORTANT]
    > La prise en charge de la gestion des ressources HDInsight par Azure PowerShell à l’aide d’Azure Service Manager est **déconseillée** ; elle sera supprimée le 1er janvier 2017. étapes de Hello dans ce document Utilisez hello nouvelles applets de commande HDInsight qui fonctionnent avec Azure Resource Manager.
    >
    > Suivez les étapes de hello dans [installer et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello dernière version d’Azure PowerShell. Si vous avez des scripts qui toobe besoin modifié toouse hello nouvelles applets de commande qui fonctionnent avec Azure Resource Manager, consultez [des outils de migration tooAzure développement basé sur le Gestionnaire de ressources pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) pour plus d’informations.

* **Un cluster HDInsight**. Pour plus d’informations sur la création d’un cluster HDInsight, consultez la rubrique ou [Création de clusters HDInsight][hdinsight-provision] ou [Prise en main de HDInsight][hdinsight-get-started]. Vous devez hello suivant toogo données didacticiel de hello :

    <table border = "1">
    <tr><th>Propriété du cluster</th><th>Nom de la variable Windows PowerShell</th><th>Valeur</th><th>Description</th></tr>
    <tr><td>Nom du cluster HDInsight</td><td>$clusterName</td><td></td><td>cluster de HDInsight Hello sur lequel vous allez exécuter ce didacticiel.</td></tr>
    <tr><td>Nom d'utilisateur du cluster HDInsight</td><td>$clusterUsername</td><td></td><td>nom d’utilisateur HDInsight cluster Hello. </td></tr>
    <tr><td>Mot de passe de l'utilisateur du cluster HDInsight </td><td>$clusterPassword</td><td></td><td>Hello HDInsight cluster mot de passe.</td></tr>
    <tr><td>Nom du compte de stockage Azure</td><td>$storageAccountName</td><td></td><td>Un cluster HDInsight des toohello disponibles du compte de stockage Azure. Pour ce didacticiel, utilisez le compte de stockage par défaut hello que vous avez spécifié au cours du processus de configuration du cluster hello.</td></tr>
    <tr><td>Nom du conteneur d'objets blob Azure</td><td>$containerName</td><td></td><td>Pour cet exemple, utilisez le conteneur de stockage d’objets Blob Azure hello est utilisé pour le système de fichiers de cluster hello par défaut HDInsight. Par défaut, elle a hello comme cluster HDInsight de hello du même nom.</td></tr>
    </table>
* **Une base de données SQL Azure**. Vous devez configurer une règle de pare-feu pour hello tooallow accès au serveur de base de données SQL à partir de votre station de travail. Pour obtenir des instructions sur la création d’une base de données SQL Azure et de configuration du pare-feu de hello, voir [prise en main de la base de données SQL Azure] [sqldatabase-get-started]. Cet article fournit un script Windows PowerShell pour créer la table de base de données SQL Azure hello dont vous avez besoin pour ce didacticiel.

    <table border = "1">
    <tr><th>Propriété de base de données SQL</th><th>Nom de la variable Windows PowerShell</th><th>Valeur</th><th>Description</th></tr>
    <tr><td>Nom du serveur de base de données SQL</td><td>$sqlDatabaseServer</td><td></td><td>Hello SQL de base de données serveur toowhich Sqoop exporte les données. </td></tr>
    <tr><td>Nom de connexion à la base de données SQL</td><td>$sqlDatabaseLogin</td><td></td><td>Nom de connexion à la base de données SQL.</td></tr>
    <tr><td>Mot de passe de connexion à la base de données SQL</td><td>$sqlDatabaseLoginPassword</td><td></td><td>Mot de passe de connexion à la base de données SQL.</td></tr>
    <tr><td>Nom de la base de données SQL</td><td>$sqlDatabaseName</td><td></td><td>toowhich de base de données SQL Azure Hello Sqoop exporte les données. </td></tr>
    </table>

  > [!NOTE]
  > Par défaut, une base de données SQL Azure autorise des connexions aux services Azure tels que Azure HDinsight. Si ce paramètre de pare-feu est désactivé, vous devez l’activer à partir de hello portail Azure. Pour obtenir des instructions sur la création d'une base de données SQL et la configuration des règles de pare-feu, consultez la rubrique [Création et configuration d'une base de données SQL][sqldatabase-get-started].

> [!NOTE]
> Valeurs hello remplir des tables de hello. Cela vous sera utile pour ce didacticiel.

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a>Définir le flux de travail Oozie et hello script HiveQL connexe
Les définitions des workflows Oozie sont écrites en hPDL (un langage de définition du processus XML). nom de fichier de flux de travail par défaut Hello est *workflow.xml*.  Vous enregistrer le fichier de flux de travail hello localement et déployez-le toohello HDInsight cluster à l’aide d’Azure PowerShell plus loin dans ce didacticiel.

Hello action Hive dans le flux de travail hello appelle un fichier de script HiveQL. Le fichier de script contient trois instructions HiveQL :

1. **Hello, l’instruction DROP TABLE** suppressions hello log4j ruche table si elle existe.
2. **Hello, l’instruction CREATE TABLE** crée une table externe de ruche log4j, qui désigne l’emplacement toohello du fichier de journal log4j hello.
3. **Hello d’emplacement du fichier de journal log4j hello**. séparateur de champs Hello est «, ». délimiteur de ligne Hello par défaut est « \n ». Une table externe Hive est fichier de données utilisé tooavoid hello en cours de suppression à partir de l’emplacement d’origine de hello, dans le cas du flux de travail toorun hello Oozie plusieurs fois.
4. **Hello insérer remplacer l’instruction** compte hello les occurrences de chaque type de niveau de journal à partir de hello log4j ruche table, et elle enregistre l’emplacement de stockage des objets Blob Azure hello sortie tooan.

> [!NOTE]
> Il existe un problème connu de chemin d'accès à Hive. Vous le rencontrez lors de l'envoi d'une tâche Oozie. Hello des instructions pour résoudre le problème de hello se trouvent sur hello TechNet Wiki : [HDInsight Hive erreur : Impossible de toorename][technetwiki-hive-error].

**fichier de script du HiveQL toodefine hello toobe appelée par le flux de travail hello**

1. Créez un fichier texte avec hello suivant contenu :

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    Il existe trois variables utilisées dans un script de hello :

   * ${hiveTableName}
   * ${hiveDataFolder}
   * ${hiveOutputFolder}

     le fichier de définition de flux de travail Hello (workflow.xml dans ce didacticiel) passe ces toothis valeurs HiveQL script en cours d’exécution.
2. Enregistrer le fichier hello sous **C:\Tutorials\UseOozie\useooziewf.hql** à l’aide de l’encodage ANSI (ASCII). (Utilisez le Bloc-notes si votre éditeur de texte ne dispose pas de cette option.) Ce fichier de script sera déployé toohello HDInsight cluster plus loin dans le didacticiel de hello.

**toodefine un flux de travail**

1. Créez un fichier texte avec hello suivant contenu :

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

    Il existe deux actions définies dans le flux de travail hello. est de démarrer Hello-tooaction *RunHiveScript*. Si l’action de hello exécute *OK*, est de l’action suivante de hello *RunSqoopExport*.

    Hello RunHiveScript a plusieurs variables. Vous allez passer les valeurs hello lorsque vous soumettez un travail de Oozie hello à partir de votre station de travail à l’aide d’Azure PowerShell.

    Variable de workflow

    <table border = "1">
    <tr><th>Variable de workflow</th><th>Description</th></tr>
    <tr><td>${jobTracker}</td><td>Spécifiez les URL de hello du suivi de travail Hadoop hello. Utilisez <strong>jobtrackerhost:9010</strong> sur les versions 3.0 et 2.0 de HDInsight.</td></tr>
    <tr><td>${nameNode}</td><td>Spécifiez les URL hello du nœud de nom hello Hadoop. Utilisez hello par défaut fichier système wasb : / / adresse, par exemple, <i>wasb : / /&lt;Nom_conteneur&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</td></tr>
    <tr><td>${queueName}</td><td>Spécifie le nom de file d’attente hello hello travail destinée au. Utilisez <strong>Default</strong>.</td></tr>
    </table>

    Variables de l'action Hive

    <table border = "1">
    <tr><th>Variable d'action Hive</th><th>Description</th></tr>
    <tr><td>${hiveDataFolder}</td><td>répertoire source Hello hello commande Hive Create Table.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>dossier de sortie Hello pour hello insérer remplacer l’instruction.</td></tr>
    <tr><td>${hiveTableName}</td><td>nom de Hello de table Hive hello qui fait référence à des fichiers de données log4j hello.</td></tr>
    </table>

    Variables d'action Sqoop

    <table border = "1">
    <tr><th>Variable d'action Sqoop</th><th>Description</th></tr>
    <tr><td>${sqlDatabaseConnectionString}</td><td>Chaîne de connexion à la base de données SQL.</td></tr>
    <tr><td>${sqlDatabaseTableName}</td><td>Hello SQL Azure table toowhere hello données est exportée.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>dossier de sortie Hello pour hello Hive insérer remplacer l’instruction. Il s’agit de hello même dossier pour l’exportation de Sqoop hello (export-dir).</td></tr>
    </table>

    Pour plus d’informations sur les flux de travail Oozie et à l’aide des actions de flux de travail hello, consultez [documentation Apache Oozie 4.0] [ apache-oozie-400] (pour la version 3.0 du cluster HDInsight) ou [Apache Oozie 3.3.2 documentation] [ apache-oozie-332] (pour la version 2.1 du cluster HDInsight).

1. Enregistrer le fichier hello sous **C:\Tutorials\UseOozie\workflow.xml** à l’aide de l’encodage ANSI (ASCII). (Utilisez le Bloc-notes si votre éditeur de texte ne dispose pas de cette option.)

**coordinateur de toodefine**

1. Créez un fichier texte avec hello suivant contenu :

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    Il existe cinq variables utilisées dans le fichier de définition de hello :

   | Variable | Description |
   | --- | --- |
   | ${coordFrequency} |Heure de pause de la tâche. La fréquence est toujours exprimée en minutes. |
   | ${coordStart} |Heure de début de la tâche. |
   | ${coordEnd} |Heure de fin de la tâche. |
   | ${coordTimezone} |Oozie traite les tâches du coordinateur dans un fuseau horaire fixe sans passage à l’heure d’été (généralement représenté à l'aide de UTC). Ce fuseau horaire est appelé hello » Oozie traitement fuseau horaire. » |
   | ${wfPath} |chemin d’accès de Hello pour hello workflow.xml.  Si le nom de fichier de flux de travail hello n’est pas du nom de fichier hello par défaut (workflow.xml), vous devez la spécifier. |
2. Enregistrer le fichier hello sous **C:\Tutorials\UseOozie\coordinator.xml** à l’aide de l’encodage ANSI (ASCII) hello. (Utilisez le Bloc-notes si votre éditeur de texte ne dispose pas de cette option.)

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a>Déployer le projet de Oozie hello et préparer hello didacticiel
Vous allez exécuter une suivant hello de Azure PowerShell script tooperform :

* Hello de copie HiveQL stockage d’objets Blob de script (useoozie.hql) tooAzure, wasb:///tutorials/useoozie/useoozie.hql.
* Copiez workflow.xml toowasb:///tutorials/useoozie/workflow.xml.
* Copiez coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.
* Fichier de données de copie hello (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.
* Créer une table de base de données SQL Azure pour stocker les données d'exportation de Sqoop. nom de la table Hello est *log4jLogCount*.

**Présentation du stockage HDInsight**

HDInsight utilise le stockage d’objets blob Azure pour stocker les données. wasb : / / est l’implémentation Microsoft du système de fichiers hello distribués Hadoop (HDFS) dans le stockage d’objets Blob Azure. Pour plus d'informations, consultez la rubrique [Utilisation du stockage d'objets blob Azure avec HDInsight][hdinsight-storage].

Lorsque vous configurez un cluster HDInsight, un compte de stockage d’objets Blob Azure et un conteneur spécifique à partir de ce compte est désigné en tant que système de fichiers par défaut hello, comme dans HDFS. En outre toothis compte de stockage, vous pouvez ajouter plu les comptes de stockage à partir de hello même abonnement Azure ou à partir de différents abonnements Azure pendant hello processus de configuration. Pour plus d'instructions sur l’ajout des comptes de stockage supplémentaires, consultez la rubrique [Approvisionnement de clusters HDInsight][hdinsight-provision]. script de Azure PowerShell hello toosimplify utilisé dans ce didacticiel, tous les fichiers sont stockés dans le conteneur de système de fichiers par défaut hello de hello situé *useoozie/didacticiels/*. Par défaut, ce conteneur a hello même nom en tant que nom du cluster HDInsight hello.
syntaxe de Hello est :

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> Hello uniquement *wasb : / /* syntaxe est prise en charge dans la version 3.0 du cluster HDInsight. Hello plus anciens *asv : / /* syntaxe est prise en charge dans HDInsight 2.1 et 1.6 clusters, mais il n’est pas pris en charge dans les clusters HDInsight 3.0.
>
> Hello wasb : / / chemin d’accès est un chemin d’accès virtuel. Pour plus d'informations, consultez la rubrique [Utilisation du stockage d'objets blob Azure avec HDInsight][hdinsight-storage] .

Un fichier qui est stocké dans un conteneur de système de fichiers par défaut hello est accessible à partir de HDInsight à l’aide des hello suivant URI (j’utilise workflow.xml comme exemple) :

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

Si vous voulez tooaccess hello directement à partir de compte de stockage hello, nom d’objet blob hello pour le fichier de hello est :

    tutorials/useoozie/workflow.xml

**Présentation des tables interne et externe Hive**

Il existe quelques éléments, vous devez tooknow sur les tables internes et externes Hive :

* Hello commande CREATE TABLE crée une table interne, également appelé un tableau managé. fichier de données Hello doit se trouver dans le conteneur par défaut de hello.
* Hello commande CREATE TABLE déplace les données de salutation fichiertoohello/hive/entrepôt/<TableName> dossier dans le conteneur par défaut de hello.
* Hello les commandes CREATE EXTERNAL TABLE crée une table externe. fichier de données Hello peut être situé en dehors du conteneur par défaut de hello.
* Hello les commandes CREATE EXTERNAL TABLE ne déplace pas le fichier de données hello.
* Hello les commandes CREATE EXTERNAL TABLE n’autorise pas les sous-dossiers dans le dossier hello qui est spécifié dans la clause d’emplacement hello. C’est pourquoi hello pourquoi didacticiel de hello effectue une copie du fichier d’exemple.log hello.

Pour plus d’informations, consultez la rubrique [HDInsight : introduction aux tables interne et externe Hive][cindygross-hive-tables].

**didacticiel de hello tooprepare**

1. Hello ouvrir Windows PowerShell ISE (dans l’écran d’accueil de Windows 8 hello, tapez **PowerShell_ISE**, puis cliquez sur **Windows PowerShell ISE**. Pour plus d'informations, consultez la page [Démarrage de Windows PowerShell sur Windows 8 et Windows][powershell-start]).
2. Dans le volet inférieur de hello, exécutez hello suivant commande tooconnect tooyour abonnement Azure :

    ```powershell
    Add-AzureAccount
    ```

    Vous est demandée tooenter vos informations d’identification de compte Azure. Cette méthode d’ajout d’une connexion à un abonnement arrive à expiration, et après 12 heures, vous devez toorun hello applet de commande à nouveau.

   > [!NOTE]
   > Si vous avez plusieurs abonnements Azure et abonnement de hello par défaut n’est pas hello celui que vous souhaitez toouse, utilisez hello <strong>Select-AzureSubscription</strong> tooselect de l’applet de commande un abonnement.

3. Copier le script suivant dans le volet de script hello de hello, puis définir des variables de six premiers hello :

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

    Pour plus d’une description des variables de hello, consultez hello [conditions préalables](#prerequisites) section dans ce didacticiel.

4. Ajouter hello script toohello dans le volet de script hello suivant :

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

5. Cliquez sur **exécuter le Script** ou appuyez sur **F5** script de hello toorun. sortie de Hello sera semblable à :

    ![Sortie de la préparation du didacticiel][img-preparation-output]

## <a name="run-hello-oozie-project"></a>Exécutez hello Oozie projet
Azure PowerShell ne fournit actuellement aucune applet de commande pour la définition de tâches Oozie. Vous pouvez utiliser hello **Invoke-RestMethod** tooinvoke applet de commande Oozie des services web. API des services web Oozie Hello est une API de JSON HTTP REST. Pour plus d’informations sur les API des services web hello Oozie, consultez [documentation Apache Oozie 4.0] [ apache-oozie-400] (pour la version 3.0 du cluster HDInsight) ou [Apache Oozie 3.3.2 documentation] [ apache-oozie-332] (pour la version 2.1 du cluster HDInsight).

**toosubmit un travail Oozie**

1. Hello ouvrir Windows PowerShell ISE (dans l’écran d’accueil de Windows 8, tapez **PowerShell_ISE**, puis cliquez sur **Windows PowerShell ISE**. Pour plus d'informations, consultez la page [Démarrage de Windows PowerShell sur Windows 8 et Windows][powershell-start]).
2. Suit hello de copie de script dans le volet de script hello et puis ensemble hello variables tout d’abord quatorze (Toutefois, ignorer **$storageUri**).

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

    Pour plus d’une description des variables de hello, consultez hello [conditions préalables](#prerequisites) section dans ce didacticiel.

    $coordstart et $coordend sont à partir de flux de travail hello et l’heure de fin. toofind out hello heure UTC/GMT, rechercher « GMT » sur bing.com. Hello $coordFrequency est la fréquence à laquelle vous souhaitez toorun hello workflow des minutes.
3. Ajouter hello toohello script suivant. Cette partie définit la charge utile de hello Oozie :

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
   > fichier de charge utile de soumission principale différence par rapport toohello du flux de travail Hello est variable de hello **oozie.coord.application.path**. Lors de l'envoi d'une tâche de workflow, vous utilisez **oozie.wf.application.path** .

4. Ajouter hello toohello script suivant. Cette partie vérifie l’état du service web hello Oozie :

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

5. Ajouter hello toohello script suivant. Cette partie crée une tâche Oozie :

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
   > Lorsque vous soumettez une tâche de workflow, vous devez apporter d’un autre service appel toostart hello de tâche web après que hello travail est créé. Dans ce cas, les travaux du coordinateur hello est déclenchée par heure. Hello travail démarre automatiquement.

6. Ajouter hello toohello script suivant. Cette partie vérifie l’état du travail Oozie hello :

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

7. (Facultatif) Ajouter hello toohello script suivant.

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

8. Ajouter hello toohello script suivant :

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    Supprimez les signes # hello si vous souhaitez que les fonctions supplémentaires de toorun hello.
9. Si vous disposez du cluster HDInsight version 2.1, remplacez « https://$clusterName.azurehdinsight.net:443/oozie/v2/ » par « https://$clusterName.azurehdinsight.net:443/oozie/v1/ ». La version 2.1 du cluster HDInsight ne pas prend en charge la version 2 de hello web services.
10. Cliquez sur **exécuter le Script** ou appuyez sur **F5** script de hello toorun. sortie de Hello sera semblable à :

     ![Sortie du workflow exécuté par le didacticiel][img-runworkflow-output]
11. Se connecter tooyour données de base de données SQL toosee hello exportée.

**journal des erreurs de travail hello toocheck**

tootroubleshoot un flux de travail, fichier de journal hello Oozie trouverez C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log à partir du nœud principal de cluster hello. Pour plus d’informations sur le protocole RDP, consultez [clusters HDInsight d’administration à l’aide de hello portail Azure][hdinsight-admin-portal].

**didacticiel de hello toorerun**

flux de travail toorerun hello, vous devez effectuer hello tâches suivantes :

* Supprimer le fichier de sortie du script hello Hive.
* Suppression des données dans la table de log4jLogsCount hello hello.

Voici un exemple d'un script Windows PowerShell que vous pouvez utiliser :

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

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris comment toodefine Oozie d’un flux de travail et un coordinateur Oozie, et comment toorun Oozie coordinateur de projet à l’aide d’Azure PowerShell. toolearn, voir hello suivant des articles :

* [Prise en main de HDInsight][hdinsight-get-started]
* [Utilisation du stockage d’objets blob Azure avec HDInsight][hdinsight-storage]
* [Administration de HDInsight à l'aide d'Azure PowerShell][hdinsight-admin-powershell]
* [Télécharger des données tooHDInsight][hdinsight-upload-data]
* [Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop]
* [Utilisation de Hive avec HDInsight][hdinsight-use-hive]
* [Utilisation de Pig avec HDInsight][hdinsight-use-pig]
* [Développement de programmes MapReduce en Java pour HDInsight][hdinsight-develop-java-mapreduce]

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
