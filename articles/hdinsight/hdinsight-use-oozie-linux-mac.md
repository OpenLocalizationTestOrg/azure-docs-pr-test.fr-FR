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
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a>Utilisez Oozie avec Hadoop toodefine et exécuter un workflow sur HDInsight de basés sur Linux

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

Découvrez comment toouse Oozie Apache avec Hadoop dans HDInsight. Apache Oozie est un système de workflow/coordination qui gère les tâches Hadoop. Oozie est intégré à la pile de Hadoop hello, et il prend en charge hello suivant de tâches :

* Apache MapReduce
* Apache Pig
* Apache Hive
* Apache Sqoop

Oozie peut également être utilisé tooschedule les travaux système tooa spécifiques, tels que les programmes Java ou des scripts de shell

> [!NOTE]
> Une autre option pour définir des flux de travail avec HDInsight consiste à utiliser Azure Data Factory. toolearn en savoir plus sur Azure Data Factory, consultez [utilisez Pig et Hive avec Data Factory][azure-data-factory-pig-hive].

> [!IMPORTANT]
> Oozie n’est pas activé sur HDInsight joint à un domaine.

## <a name="prerequisites"></a>Composants requis

* **Un cluster HDInsight**: consultez la page [Prise en main de HDInsight sur Linux](hdinsight-hadoop-linux-tutorial-get-started.md)

  > [!IMPORTANT]
  > étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="example-workflow"></a>Exemple de flux de travail

flux de travail Hello utilisé dans ce document contient deux actions. Les actions sont des définitions de tâches, telles que l’exécution de Hive, Sqoop, MapReduce ou un autre processus :

![Diagramme du workflow][img-workflow-diagram]

1. Une ruche action s’exécute un script HiveQL tooextract enregistrements à partir de hello **hivesampletable** inclus avec HDInsight. Chaque ligne de données décrit un accès depuis un appareil mobile spécifique. le format d’enregistrement Hello apparaît toohello similaire après le texte :

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    Hello script Hive utilisé dans ce document compte le nombre total de visites hello pour chaque plateforme (par exemple, Android ou iPhone) et stocke les nombres hello tooa nouvelle table de ruche.

    Pour plus d’informations sur Hive, consultez l’article [Utilisation de Hive avec HDInsight][hdinsight-use-hive].

2. Une action Sqoop exporte contenu hello de hello nouvelle table tooa table Hive dans une base de données SQL Azure. Pour plus d’informations sur Sqoop, consultez la rubrique [Utilisation de Hadoop Sqoop avec HDInsight][hdinsight-use-sqoop].

> [!NOTE]
> Pour les versions Oozie prises en charge sur les clusters HDInsight, consultez [quelles sont les nouveautés dans les versions de cluster Hadoop hello fournies par HDInsight][hdinsight-versions].

## <a name="create-hello-working-directory"></a>Créer le répertoire de travail hello

Oozie attend des ressources requises pour un travail toobe stockée Bonjour même répertoire. Cet exemple utilise **wasb:///tutorials/useoozie**. Utilisez hello suivant commande toocreate ce répertoire et le répertoire de données hello qui contient la nouvelle table Hive hello, créé par ce flux de travail :

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> Hello `-p` paramètre indique tous les répertoires dans hello toobe de chemin d’accès créé. Hello **données** répertoire est données toohold utilisé utilisées par hello **useooziewf.hql** script.

Également exécuter hello suivant de commande, ce qui garantit que Oozie peut emprunter l’identité de votre compte d’utilisateur lors de l’exécution de tâches Hive et Sqoop. Remplacez **USERNAME** par votre nom de connexion :

```
sudo adduser USERNAME users
```

> [!NOTE]
> Vous pouvez ignorer les erreurs de cet utilisateur hello est déjà membre de hello `users` groupe.

## <a name="add-a-database-driver"></a>Ajout d’un pilote de base de données

Étant donné que ce flux de travail utilise Sqoop tooexport tooSQL de données de base de données, vous devez fournir qu'une copie du pilote JDBC de hello utilisé tootalk tooSQL base de données. Utilisez hello suivant toocopy de commande de répertoire de travail toohello :

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

Si votre flux de travail utilisé les autres ressources, telles que fichier jar contenant une application MapReduce, vous devez tooadd également ces ressources.

## <a name="define-hello-hive-query"></a>Définir la requête Hive de hello

Utilisez hello suivant les étapes toocreate un script HiveQL qui définit une requête, qui est utilisée dans un flux de travail Oozie plus loin dans ce document.

1. Connectez le cluster toohello à l’aide de SSH. Bonjour commande suivante est un exemple d’utilisation hello `ssh` commande. Remplacez __nom d’utilisateur__ avec l’utilisateur SSH hello pour le cluster de hello. Remplacez __CLUSTERNAME__ avec nom hello du cluster HDInsight de hello.

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. À partir de hello connexion SSH, utilisez hello suivant commande toocreate un fichier :

    ```
    nano useooziewf.hql
    ```

3. Une fois que l’éditeur de nano hello s’ouvre, utilisez hello suivant la requête en tant que contenu hello du fichier de hello :

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    Il existe deux variables utilisées dans un script de hello :

    * **${hiveTableName}**: contient le nom hello de hello toobe de table créé

    * **${hiveDataFolder}**: contient les fichiers de données hello emplacement toostore hello pour la table de hello

    le fichier de définition de flux de travail Hello (workflow.xml dans ce didacticiel) passe ces toothis valeurs HiveQL script en cours d’exécution

4. éditeur de hello tooexit, appuyez sur Ctrl-X. Lorsque vous y êtes invité, sélectionnez **Y** toosave hello du fichier, puis utilisez **entrée** toouse hello **useooziewf.hql** nom de fichier.

5. Suivant de hello utilisez commandes toocopy **useooziewf.hql** trop**wasb:///tutorials/useoozie/useooziewf.hql**:

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    Ces commandes stockent hello **useooziewf.hql** fichier sur un stockage hello HDFS compatibles pour le cluster de hello.

## <a name="define-hello-workflow"></a>Définir le flux de travail hello

Les définitions des workflows Oozie sont écrites en hPDL (un langage de définition du processus XML). Utilisez hello suivant du flux de travail suit toodefine hello :

1. Utilisez hello suivant l’instruction toocreate et modifier un fichier :

    ```
    nano workflow.xml
    ```

2. Une fois que l’éditeur de nano hello s’ouvre, entrez hello XML suivant comme contenu du fichier hello :

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

    Il existe deux actions définies dans le flux de travail hello :

   * **RunHiveScript**: cette action est l’action de démarrage hello et s’exécute hello **useooziewf.hql** script Hive

   * **RunSqoopExport**: cette action exporte les données de hello créées à partir de hello ruche script tooSQL Sqoop à l’aide de la base de données. Cette action s’exécute uniquement si hello **RunHiveScript** action a abouti.

     flux de travail Hello a plusieurs entrées, telles que `${jobTracker}`. Ces entrées sont remplacées par les valeurs que vous utilisez dans la définition de la tâche hello. définition de la tâche Hello est créée ultérieurement dans ce document.

     Hello de note également `<archive>sqljdbc4.jar</arcive>` entrée Bonjour Sqoop section. Cette entrée indique au Oozie toomake cette archive disponible pour Sqoop lors de l’exécution de cette action.

3. Utilisez Ctrl-X, puis **Y** et **entrée** fichier hello de toosave.

4. Suivant de hello utilisez commande toocopy hello **workflow.xml** trop de fichiers**/tutorials/useoozie/workflow.xml**:

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a>Créer la base de données hello

toocreate une base de données SQL Azure, suivez les étapes de hello Bonjour [créer une base de données SQL](../sql-database/sql-database-get-started.md) document. Lors de la création de la base de données hello, utilisez `oozietest` comme nom de base de données hello. Notez également du nom de hello du serveur de base de données hello.

### <a name="create-hello-table"></a>Créer la table de hello

> [!NOTE]
> Il existe de nombreuses façons tooconnect tooSQL base de données toocreate une table. Hello suivant l’utilisation d’étapes [FreeTDS](http://www.freetds.org/) à partir du cluster HDInsight de hello.


1. Utilisez hello suivant de commande tooinstall FreeTDS de cluster HDInsight de hello :

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. Une fois que FreeTDS a été installé, utilisez hello suivant du serveur de base de données SQL commandes tooconnect toohello que vous avez créé précédemment :

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    Vous recevez toohello similaire de sortie suivant du texte :

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. À hello `1>` invite, entrez hello lignes suivantes :

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    Hello lorsque `GO` instruction est entrée, les instructions précédentes hello sont évaluées. Ces instructions créent une table nommée **mobiledata** qui est utilisé par les flux de travail hello.

    Hello utilisation suivant tooverify qui hello table a été créé :

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    Vous consultez toohello similaire de sortie suivant du texte :

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. Entrez `exit` à hello `1>` tooexit hello tsql utilitaire d’invite.

## <a name="create-hello-job-definition"></a>Créer la définition de la tâche hello

définition de la tâche Hello décrit où toofind hello workflow.xml. Il explique également où toofind autres fichiers utilisés par le flux de travail hello (par exemple, useooziewf.hql.) Il définit également les valeurs hello pour les propriétés utilisées dans le flux de travail hello et fichiers associés.

1. Utilisez hello commande tooget hello adresse complète du stockage par défaut de hello suivante. Cette adresse est utilisée dans le fichier de configuration hello dans un instant :

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    Cette commande retourne des informations similaires toohello est XML suivant :

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > Si le cluster HDInsight de hello utilise le stockage Azure en tant que stockage par défaut de hello, hello `<value>` le contenu d’éléments commence par `wasb://`. En revanche, si Azure Data Lake Store est utilisé, il commence par `adl://`.

    Enregistrer le contenu de hello hello `<value>` élément, tel qu’il est utilisé dans les étapes suivantes hello.

2. Utilisez hello suivant commande tooget nom de domaine complet du nœud principal de cluster hello. Ces informations sont utilisées pour hello adresse JobTracker pour le cluster de hello :

    ```
    hostname -f
    ```

    Cet exemple renvoie toohello similaire à informations suivant le texte :

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    Hello port utilisé pour hello JobTracker étant 8050, toouse d’adresse complète hello pour hello JobTracker est `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.

3. Utilisez hello toocreate hello Oozie travail définition configuration suivante :

    ```
    nano job.xml
    ```

4. Une fois que l’éditeur de nano hello s’ouvre, utilisez hello XML suivant comme contenu hello du fichier de hello :

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

   * Remplacez toutes les instances de  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  avec la valeur hello reçu précédemment pour le stockage de la valeur par défaut.

     > [!WARNING]
     > Si le chemin d’accès hello est un `wasb` chemin d’accès, vous devez utiliser le chemin d’accès complet de hello. Ne le diminuez pas toojust `wasb:///`.

   * Remplacez **JOBTRACKERADDRESS** avec hello adresse JobTracker/ResourceManager reçu précédemment.
   * Remplacez **votrenom** avec votre nom de connexion pour le cluster HDInsight de hello.
   * Remplacez **nom_serveur**, **adminLogin**, et **adminPassword** avec des informations de hello pour votre base de données SQL Azure.

     La plupart des informations hello dans ce fichier est toopopulate utilisé les valeurs hello utilisés dans les fichiers de hello workflow.xml ou ooziewf.hql (par exemple, ${nameNode}.)

     > [!NOTE]
     > Hello **oozie.wf.application.path** entrée définit où fichier workflow.xml toofind hello, qui contient le flux de travail hello exécuté par ce travail.

5. Utilisez Ctrl-X, puis **Y** et **entrée** fichier hello de toosave.

## <a name="submit-and-manage-hello-job"></a>Soumettre et de gérer le travail de hello

Hello suit hello Oozie commande toosubmit et gérer des flux de travail Oozie sur le cluster de hello. Hello Oozie commande est une interface conviviale sur hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

> [!IMPORTANT]
> Lorsque vous utilisez la commande de hello Oozie, vous devez utiliser hello nom de domaine complet pour le nœud principal de HDInsight hello. Ce nom de domaine complet n’est accessible à partir du cluster de hello, ou si hello cluster se trouve sur un réseau virtuel Azure, à partir d’autres ordinateurs sur hello même réseau.


1. Utilisez hello après tooobtain hello URL toohello Oozie service :

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    Cet exemple renvoie toohello similaires à des informations XML suivant :

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    Hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` partie est toouse d’URL hello avec hello Oozie commande.

2. Hello utilisation suivant toocreate une variable d’environnement pour l’URL de hello, donc vous n’avez pas tootype pour chaque commande :

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    Remplacer les URL hello hello un reçu précédemment.
3. Utilisez hello suivant le travail de hello toosubmit :

    ```
    oozie job -config job.xml -submit
    ```

    Cette commande charge des informations sur les travaux hello de **job.xml** et la soumet tooOozie, mais ne s’exécute ne pas.

    Une fois la commande hello terminée, elle doit retourner hello des ID de tâche de hello. Par exemple, `0000005-150622124850154-oozie-oozi-W`. Cet ID est un travail de hello toomanage utilisé.

4. Afficher l’état de hello du travail hello à l’aide de hello de commande suivante :

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > Remplacez `<JOBID>` par hello ID retourné à l’étape précédente de hello.

    Cet exemple renvoie toohello similaire à informations suivant le texte :

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

    Ce travail a le statut `PREP`, Cet état indique que le travail hello a été créé, mais n’a pas démarré.

5. Utilisez hello suivant le travail de commande toostart hello :

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > Remplacez `<JOBID>` par hello ID retourné précédemment.

    Si vous vérifiez l’état de hello après cette commande, il est en cours d’exécution, et informations sont retournées pour les actions de hello dans le travail de hello.

6. Une fois la tâche hello se termine correctement, vous pouvez vérifier que les données de salutation a été générées et exportés de table de base de données SQL toohello à l’aide de hello suivant de commandes :

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    À hello `1>` invite, entrez hello suivant la requête :

    ```
    SELECT * FROM mobiledata
    GO
    ```

    les informations de Hello retournées sont similaires toohello suivant du texte :

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

Pour plus d’informations sur hello Oozie commande, consultez [outil de ligne de commande Oozie](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).

## <a name="oozie-rest-api"></a>API REST Oozie

Hello Oozie REST API vous permet de toobuild vos propres outils qui fonctionnent avec Oozie. Hello Voici HDInsight des informations spécifiques sur l’utilisation de hello Oozie REST API :

* **URI**: hello API REST sont accessibles à partir de l’extérieur cluster hello à`https://CLUSTERNAME.azurehdinsight.net/oozie`

* **Authentification**: authentifier API toohello à l’aide du compte de cluster HTTP hello (administrateur) et le mot de passe. Par exemple :

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

Pour plus d’informations sur l’utilisation de hello Oozie REST API, consultez [API des Services Web Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

## <a name="oozie-web-ui"></a>Interface utilisateur web Oozie

Hello l’interface utilisateur Web de Oozie offre une vue basée sur le web état hello de Oozie travaux sur le cluster de hello. interface utilisateur web de Hello permet hello tooview informations suivantes :

* Statut de tâche
* Définition du travail
* Configuration
* Un graphique des actions hello dans la tâche de hello
* Journaux hello travail

Vous pouvez également afficher les détails pour les actions du travail.

tooaccess hello l’interface utilisateur Web de Oozie, utilisez hello comme suit :

1. Créer un cluster de HDInsight de toohello tunnel SSH. Pour plus d’informations, consultez hello [utiliser SSH Tunneling hdinsight](hdinsight-linux-ambari-ssh-tunnel.md) document.

2. Une fois qu’un tunnel a été créé, ouvrez l’interface utilisateur web de Ambari hello dans votre navigateur web. Hello URI pour le site de Ambari hello est **https://CLUSTERNAME.azurehdinsight.net**. Remplacez **CLUSTERNAME** avec nom hello de votre cluster HDInsight de basés sur Linux.

3. Bonjour à gauche de la page de hello, sélectionnez **Oozie**, puis **liens rapides**et enfin **l’interface utilisateur Web de Oozie**.

    ![image des menus de hello](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. Bonjour toodisplaying de valeurs par défaut de l’interface utilisateur Web de Oozie tâches de Workflow en cours d’exécution. sélectionner de toutes les tâches de workflow, toosee **tous les travaux**.

    ![Tous les travaux affichés](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. Sélectionnez un travail tooview plus d’informations sur la tâche de hello.

    ![Job Info](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. À partir de l’onglet informations du travail de hello, vous pouvez voir des informations sur les travaux de base et des actions individuelles hello dans le travail de hello. À l’aide des onglets de hello haut hello, que vous pouvez afficher hello définition du travail, Configuration des tâches, hello d’accès journal des travaux ou afficher un dirigées acycliques graphique (DAG) du travail de hello.

   * **Journal des travaux**: hello sélectionnez **GetLogs** tooget tous les journaux hello travail ou pour utiliser hello **Entrez un filtre de recherche** champ toofilter journaux

       ![Journal du travail](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * **JobDAG**: hello DAG est une représentation graphique des chemins d’accès de données hello effectuée par le biais du flux de travail hello

       ![Graphique non cyclique dirigé du travail](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. Sélectionner l’une des actions de hello dans hello **infos travail** onglet affiche des informations pour l’action de hello. Par exemple, sélectionnez hello **RunHiveScript** action.

    ![Informations sur l’action](./media/hdinsight-use-oozie-linux-mac/action.png)

8. Vous pouvez voir les détails pour hello action, comme un lien de toohello **URL de la Console**. Ce lien peut renvoyer des informations de JobTracker tooview utilisé pour le travail de hello.

## <a name="scheduling-jobs"></a>Planification des travaux

coordinateur de Hello vous permet de toospecify une fréquence d’occurrence, de début et de fin pour les travaux. toodefine une planification de flux de travail hello, hello utilisation comme suit :

1. Hello utilisation suivant toocreate un fichier nommé **coordinator.xml**:

    ```
    nano coordinator.xml
    ```

    Utilisez hello XML suivant comme contenu hello du fichier de hello :

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
    > Hello `${...}` variables sont remplacées par les valeurs dans la définition de la tâche hello au moment de l’exécution. variables de Hello sont :
    >
    > * `${coordFrequency}`: Délai entre les instances de tâche de hello en cours d’exécution.
    > ** `${coordStart}`: heure de début du travail de hello.
    > * `${coordEnd}`: heure de fin de tâche hello.
    > * `${coordTimezone}`: les travaux du coordinateur se trouvent dans un fuseau horaire fixe sans passage à l’heure d’été (généralement représenté par UTC). Ce fuseau horaire est appelé hello » Oozie traitement fuseau horaire. »
    > * `${wfPath}`: hello workflow.xml toohello de chemin d’accès.

2. toosave hello, utilisez Ctrl-X, **Y**, et **entrée**.

3. Hello suivant commande toocopy hello toohello travail répertoire du fichier pour cette tâche, utilisez :

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. Hello utilisation suivant toomodify hello **job.xml** fichier :

    ```
    nano job.xml
    ```

    Rendre hello modifications suivantes :

   * fichier tooinstruct oozie toorun hello coordinator au lieu de flux de travail hello, modification `<name>oozie.wf.application.path</name>` trop`<name>oozie.coord.application.path</name>`.

   * tooset hello `workflowPath` variable utilisée par le coordinateur de hello, ajouter hello XML suivant :

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       Remplacez hello `wasb://mycontainer@mystorageaccount.blob.core.windows` texte avec la valeur de hello utilisée dans d’autres entrées dans le fichier de job.xml hello.

   * toodefine hello début, fin et la fréquence de coordinateur de hello, ajoutent hello XML suivant :

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

       Ces valeurs définies hello début heure too12 : 00 PM sur 10 mai 2017, hello fin heure tooMay 12, 2017. Intervalle Hello pour l’exécution de ce travail tous les jours. fréquence de Hello est exprimée en minutes, par conséquent, 24 heures x 60 minutes = 1440 minutes. Enfin, hello timezone a la valeur tooUTC.

5. Utilisez Ctrl-X, puis **Y** et **entrée** fichier hello de toosave.

6. travail de hello toorun, hello utilisez commande suivante :

    ```
    oozie job -config job.xml -run
    ```

    Cette commande envoie et démarre le travail de hello.

7. Si vous visitez hello l’interface utilisateur Web de Oozie et sélectionnez hello **travaux du coordinateur** onglet, vous voyez toohello similaire à informations suivant image :

    ![Onglet Travaux du coordinateur](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    Hello **matérialisation suivant** entrée contient hello prochaine hello s’exécute.

8. Toohello similaire précédente tâche de workflow, sélection d’entrée de tâche hello dans l’interface utilisateur web de hello affiche des informations sur les travaux hello :

    ![Informations sur les travaux du coordinateur](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > Cette image montre uniquement réussies exécutions du travail de hello, pas les actions au sein du flux de travail hello planifiée. toosee qui, sélectionnez une des hello **Action** entrées.

    ![Informations sur l’action](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a>Résolution des problèmes

Hello Oozie UI vous permet de tooview Oozie journaux. Il contient également les journaux de tooJobTracker des liens pour les tâches MapReduce démarrés par le flux de travail hello. modèle de Hello pour le dépannage doit être :

1. Afficher le travail hello dans l’interface utilisateur Web de Oozie.

2. S’il existe une erreur ou un échec d’une action spécifique, sélectionnez hello action toosee si hello **Message d’erreur** champ fournit plus d’informations en cas d’échec hello.

3. S’il est disponible, utilisez URL hello hello action tooview plus de détails (par exemple, les journaux JobTracker) pour l’action de hello.

Hello suivantes sont des erreurs spécifiques, vous pouvez rencontrer, et comment tooresolve les.

### <a name="ja009-cannot-initialize-cluster"></a>JA009 : Cannot initialize cluster (Impossible d'initialiser le cluster)

**Symptômes**: hello les changements d’état de tâche trop**SUSPENDED**. Détails de tâche de hello indiquent l’état RunHiveScript hello **START_MANUAL**. Sélection de l’action de hello affiche hello message d’erreur suivant :

    JA009: Cannot initialize Cluster. Please check your configuration for map

**Cause**: hello adresses WASB utilisés Bonjour **job.xml** fichier ne contiennent pas de conteneur de stockage hello ou nom de compte de stockage. format d’adresse Hello WASB doit être `wasb://containername@storageaccountname.blob.core.windows.net`.

**Résolution**: modifier les adresses hello WASB utilisés par le travail de hello.

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a>JA002 : Oozie n’est pas autorisée tooimpersonate &lt;utilisateur >

**Symptômes**: hello les changements d’état de tâche trop**SUSPENDED**. Détails de tâche de hello indiquent l’état RunHiveScript hello **START_MANUAL**. Action de hello cochant hello message d’erreur suivant :

    JA002: User: oozie is not allowed tooimpersonate <USER>

**Cause**: paramètres d’autorisation actuels n’autorisent pas Oozie tooimpersonate hello de compte d’utilisateur spécifié.

**Résolution**: Oozie est autorisé aux utilisateurs de tooimpersonate Bonjour **utilisateurs** groupe. Hello d’utilisation `groups USERNAME` groupes hello toosee hello du compte d’utilisateur est membre. Si l’utilisateur de hello n’est pas un membre de hello **utilisateurs** groupe, utilisez hello suivant du groupe de commandes tooadd hello utilisateur toohello :

    sudo adduser USERNAME users

> [!NOTE]
> Il peut prendre plusieurs minutes avant de HDInsight reconnaît que toohello groupe a été ajouté à cet utilisateur hello.

### <a name="launcher-error-sqoop"></a>Launcher ERROR (Sqoop) (Erreur du lanceur, Sqoop)

**Symptômes**: hello les changements d’état de tâche trop**KILLED**. Détails de tâche de hello indiquent l’état RunSqoopExport hello **erreur**. Action de hello cochant hello message d’erreur suivant :

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

**Cause**: Sqoop est impossible tooload hello pilote requis tooaccess hello base de données.

**Résolution**: lorsque vous utilisez Sqoop à partir d’un travail Oozie, vous devez inclure pilote de base de données hello avec hello autres ressources (par exemple hello workflow.xml) utilisés par le travail de hello. Font également référence archive hello contenant le pilote de base de données hello de hello `<sqoop>...</sqoop>` section de hello workflow.xml.

Par exemple, pour la tâche hello dans ce document, vous utiliseriez hello comme suit :

1. Copie hello sqljdbc4.1.jar toohello /tutorials/useoozie répertoire du fichier :

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. Modifier le XML suivant sur une nouvelle ligne au-dessus de Bonjour workflow.xml tooadd Bonjour `</sqoop>`:

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris comment toodefine Oozie d’un flux de travail et comment toorun un travail Oozie. toolearn en savoir plus sur l’utilisation de HDInsight, consultez hello suivant des articles :

* [Utilisation du coordinateur Oozie basé sur le temps avec HDInsight][hdinsight-oozie-coordinator-time]
* [Importation de données pour les tâches Hadoop dans HDInsight][hdinsight-upload-data]
* [Utilisation de Sqoop avec Hadoop dans HDInsight][hdinsight-use-sqoop]
* [Utilisation de Hive avec Hadoop sur HDInsight][hdinsight-use-hive]
* [Utilisation de Pig avec Hadoop sur HDInsight][hdinsight-use-pig]
* [Développement de programmes MapReduce en Java pour HDInsight][hdinsight-develop-mapreduce]

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
