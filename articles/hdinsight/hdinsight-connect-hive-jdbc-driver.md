---
title: aaaQuery ruche via le pilote JDBC de hello - Azure HDInsight | Documents Microsoft
description: "Utiliser le pilote JDBC hello à partir d’un tooHadoop de requêtes Java application toosubmit Hive dans HDInsight. Se connecter par programmation et hello non SQL client."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 93178da3b8d497faa4c788e91dba89c4e45d3fff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a>Une requête Hive via le pilote JDBC de hello dans HDInsight

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Découvrez comment le pilote JDBC toouse hello un toosubmit d’application Java ruche interroge tooHadoop dans Azure HDInsight. informations Hello dans ce document montre comment tooconnect par programmation et à partir de hello HIPPOCAMPIQUES SQL client.

Pour plus d’informations sur hello Hive une Interface de JDBC, consultez [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).

## <a name="prerequisites"></a>Composants requis

* Un cluster Hadoop sur HDInsight. Les clusters basés tant sur Linux que sur Windows fonctionnent.

  > [!IMPORTANT]
  > Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, reportez-vous à la rubrique [Déclassement de HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [SQuirreL SQL](http://squirrel-sql.sourceforge.net/). SQuirreL est une application cliente JDBC.

* Hello [Kit de développement Java (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou une version ultérieure.

* [Apache Maven](https://maven.apache.org). Maven est un projet de build système pour les projets Java qui est utilisé par le projet hello associé à cet article.

## <a name="jdbc-connection-string"></a>Chaîne de connexion JDBC

Cluster de HDInsight de tooan de connexions JDBC sur Azure sont effectuées sur 443 et le trafic de hello est sécurisé à l’aide de SSL. passerelle publique Hello qui les clusters hello se situent derrière redirige hello trafic toohello port qui écoute réellement HiveServer2. Hello Voici un exemple de chaîne de connexion :

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

Remplacez `CLUSTERNAME` par nom de hello de votre cluster HDInsight.

## <a name="authentication"></a>Authentification

Lorsque vous établissez la connexion de hello, vous devez utiliser hello HDInsight cluster admin nom et mot de passe tooauthenticate toohello cluster la passerelle. Lors de la connexion à partir de clients JDBC, tel que non SQL, vous devez entrer le nom de l’administrateur hello et le mot de passe dans les paramètres client.

À partir d’une application Java, vous devez utiliser un mot de passe et nom de hello lors de l’établissement d’une connexion. Par exemple, hello code Java suivant ouvre une nouvelle connexion à l’aide de la chaîne de connexion hello, nom d’administrateur et un mot de passe :

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a>Connexion avec un client SQuirreL SQL

Non SQL est un client JDBC qui peut être utilisés tooremotely exécuter des requêtes Hive avec votre cluster HDInsight. Hello étapes suivantes supposent que vous avez déjà installé non SQL.

1. Copier les pilotes JDBC de la ruche hello à partir de votre cluster HDInsight.

    * Pour **HDInsight de basés sur Linux**, les fichiers jar toodownload hello requis les étapes suivantes de hello d’utilisation.

        1. Créez un répertoire qui contient les fichiers hello. Par exemple, `mkdir hivedriver`.

        2. À partir d’une ligne de commande suivant de hello utilisez commandes fichiers hello toocopy cluster HDInsight de hello :

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            Remplacez `USERNAME` avec le nom du compte d’utilisateur hello SSH pour le cluster de hello. Remplacez `CLUSTERNAME` avec le nom du cluster HDInsight hello.

    * Pour **HDInsight de basés sur Windows**, les fichiers jar toodownload hello les étapes suivantes de hello d’utilisation.

        1. À partir de hello portail Azure, sélectionnez votre cluster HDInsight, puis hello **Bureau à distance** icône.

            ![Icône Bureau à distance](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. Dans Panneau de bureau à distance hello, utilisez hello **Connect** cluster de toohello tooconnect de bouton. Si hello Bureau à distance n’est pas activé, utilisez hello formulaire tooprovide un nom d’utilisateur et mot de passe, puis sélectionnez **activer** tooenable Bureau à distance pour un cluster de hello.

            ![Panneau Bureau à distance](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            Lorsque vous sélectionnez le bouton **Se connecter**, un fichier .rdp est téléchargé. Utilisez ce client Bureau à distance de fichier toolaunch hello. Lorsque vous y êtes invité, utilisez le nom d’utilisateur hello et le mot de que passe pour l’accès Bureau à distance.

        3. Une fois connecté, copiez hello fichiers suivants à partir de l’ordinateur local du tooyour session Bureau à distance hello. Placez-les dans un répertoire local nommé `hivedriver`.

            * C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar

            > [!NOTE]
            > version de Hello nombres inclus dans les chemins d’accès hello et noms de fichiers peut être différente pour votre cluster.

        4. Déconnecter la session de bureau à distance hello lorsque vous avez terminé la copie des fichiers de hello.

2. Démarrer l’application de hello non SQL. De gauche hello de fenêtre hello, sélectionnez **pilotes**.

    ![Onglet pilotes hello gauche de la fenêtre hello](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. Parmi les icônes hello haut hello hello **pilotes** boîte de dialogue, sélectionnez hello  **+**  icône toocreate un pilote.

    ![Icônes des pilotes](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. Dans la boîte de dialogue Ajouter un pilote hello, ajoutez hello informations suivantes :

    * **Nom** : Hive
    * **Exemple d’URL** : `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`
    * **Chemin de classe supplémentaire**: utilisez hello ajouter bouton tooadd hello jar des fichiers téléchargés précédemment
    * **Nom de la classe** : org.apache.hive.jdbc.HiveDriver

   ![boîte de dialogue ajouter un pilote](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   Cliquez sur **OK** toosave ces paramètres.

5. Sur la gauche hello de fenêtre de hello non SQL, sélectionnez **alias**. Puis cliquez sur hello  **+**  icône toocreate un alias de connexion.

    ![ajouter un nouvel alias](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. Valeurs suivantes de hello d’utilisation pour hello **ajouter un Alias** boîte de dialogue.

    * **Nom** : Hive sur HDInsight

    * **Pilote**: utilisez Bonjour déroulante tooselect Bonjour **Hive** pilote

    * **URL** : jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

        Remplacez **CLUSTERNAME** avec nom hello de votre cluster HDInsight.

    * **Nom d’utilisateur**: nom de compte de connexion de cluster hello pour votre cluster HDInsight. valeur par défaut Hello est `admin`.

    * **Mot de passe**: mot de passe hello hello cluster compte de connexion.

 ![boîte de dialogue ajouter un alias](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    Hello d’utilisation **Test** tooverify bouton qui hello le fonctionnement de la connexion. Lorsque **se connecter à : Hive dans HDInsight** boîte de dialogue s’affiche, sélectionnez **Connect** test de hello tooperform. Si hello réussit, vous voyez un **connexion réussie** boîte de dialogue.

    connexion de hello toosave utiliser alias, hello **Ok** bouton bas hello hello **ajouter un Alias** boîte de dialogue.

7. À partir de hello **se connecter à** liste déroulante en haut de hello non SQL, sélectionnez **Hive dans HDInsight**. Lorsque vous y êtes invité, sélectionnez **Connexion**.

    ![boîte de dialogue connexion](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. Une fois connecté, entrez hello ci-dessous de requête dans la boîte de dialogue requête hello SQL, puis sélectionnez hello **exécuter** icône. zone de résultats Hello doit afficher les résultats de hello de requête de hello.

        select * from hivesampletable limit 10;

    ![boîte de dialogue requête sql, incluant les résultats](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a>Connexion à partir d’un exemple d’application Java

Un exemple d’utilisation d’un tooquery de client Java Hive dans HDInsight est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc). Suivez les instructions de hello dans hello référentiel toobuild et exécuter l’exemple hello.

## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a>Une erreur inattendue s’est produite lors de le tooopen une connexion SQL

**Symptômes**: lors de la connexion de cluster HDInsight tooan version 3.3 ou 3.4, vous pouvez recevoir une erreur s’est produite lors d’une erreur inattendue. trace de la pile pour cette erreur Hello commence par hello lignes suivantes :

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

**Cause**: cette erreur est due à une incompatibilité de version hello de hello commons-codec.jar fichier non et hello requise par les composants de la ruche de JDBC hello.

**Résolution**: toofix étapes de cette erreur, hello utilisation suivant :

1. Téléchargez le fichier jar hello commons-codec à partir de votre cluster HDInsight.

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. Quitter non et passez toohello répertoire où non est installé sur votre système. Dans le répertoire non hello sous hello `lib` active, remplacer hello existant commons-codec.jar avec hello une téléchargé à partir du cluster HDInsight de hello.

3. Redémarrez SQuirreL. Erreur de Hello ne devrait plus apparaître lors de la connexion tooHive sur HDInsight.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris comment toowork JDBC toouse avec Hive, hello utilisation suivant lie tooexplore autres toowork manières avec Azure HDInsight.

* [Télécharger des données tooHDInsight](hdinsight-upload-data.md)
* [Utilisation de Hive avec HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig avec HDInsight](hdinsight-use-pig.md)
* [Utilisation des tâches MapReduce avec HDInsight](hdinsight-use-mapreduce.md)
