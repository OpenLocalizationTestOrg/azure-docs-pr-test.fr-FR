---
title: "aaaRun un Hadoop de la tâche à l’aide de la base de données Azure Cosmos et HDInsight | Documents Microsoft"
description: "Découvrez comment toorun un simple Hive, Pig et MapReduce de la tâche avec la base de données Azure Cosmos et Azure HDInsight."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="Azure Cosmos DB-HDInsight"></a>Exécuter un travail Apache Hive, Pig ou Hadoop avec Azure Cosmos DB et HDInsight
Ce didacticiel vous montre comment toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], et [Apache Hadoop] [ apache-hadoop] Travaux MapReduce sur Azure HDInsight avec connecteur Hadoop de Cosmos DB. Connecteur de Hadoop COSMOS DB permet tooact Cosmos DB comme une source et le récepteur de tâches Hive, Pig et MapReduce. Ce didacticiel utilise Cosmos DB en tant que source de données hello et de destination pour les travaux Hadoop.

À l’issue de ce didacticiel, vous serez hello en mesure de tooanswer suivant questions :

* Comment charger des données à partir de Cosmos DB à l’aide d’un travail Hive, Pig ou MapReduce ?
* Comment stocker des données dans Cosmos DB à l’aide d’un travail Hive, Pig ou MapReduce ?

Nous vous recommandons de mise en route en regardant hello suivant vidéo, où nous exécuter un travail Hive à l’aide de la base de données Cosmos et HDInsight.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

Revenez ensuite toothis article, où vous recevrez hello plus de détails sur l’exécution de travaux de l’analytique sur vos données de la base de données Cosmos.

> [!TIP]
> Ce didacticiel part du principe que vous avez déjà utilisé Apache Hadoop, Hive et/ou Pig. Si vous êtes de nouveau tooApache Hadoop, Hive et Pig, nous vous recommandons de consulter hello [Apache Hadoop documentation][apache-hadoop-doc]. Ce didacticiel suppose également que vous avez déjà utilisé Cosmos DB et que vous possédez un compte Cosmos DB. Si vous êtes tooCosmos nouvelle base de données ou vous n’avez pas un compte de base de données Cosmos, consultez notre [mise en route] [ getting-started] page.
>
>

N’avez pas temps toocomplete hello didacticiel et souhaitez uniquement tooget hello complète exemples PowerShell de scripts Hive, Pig et MapReduce ? Ce n’est pas un problème. Vous pouvez les obtenir [ici][hdinsight-samples]. téléchargement de Hello contient également les fichiers de hql, pig et java hello pour ces exemples.

## <a name="NewestVersion"></a>Version la plus récente
<table border='1'>
    <tr><th>Version du connecteur Hadoop</th>
        <td>1.2.0</td></tr>
    <tr><th>URI du script</th>
        <td>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</td></tr>
    <tr><th>Date de modification</th>
        <td>26/04/2016</td></tr>
    <tr><th>Versions de HDInsight prises en charge</th>
        <td>3.1, 3.2.</td></tr>
    <tr><th>Journal des modifications</th>
        <td>Mise à jour too1.6.0 de kit de développement Java Azure Cosmos DB</br>
            Prise en charge ajoutée pour les collections partitionnées en tant que source et récepteur</br>
        </td></tr>
</table>

## <a name="Prerequisites"></a>Configuration requise
Avant de suivre les instructions de hello dans ce didacticiel, assurez-vous que vous disposez des éléments suivants de hello :

* Un compte Cosmos DB, une base de données et une collection de documents. Pour plus d’informations, consultez la page [Getting Started with Cosmos DB (Prise en main de Cosmos DB)][getting-started]. Importer des exemples de données dans votre compte de base de données Cosmos avec hello [outil d’importation de base de données Cosmos][import-data].
* Débit. Les lectures et écritures à partir de HDInsight seront comptabilisées sur vos unités de demande allouées pour vos collections.
* Capacité pour une procédure stockée supplémentaire dans chaque collection de sortie. les procédures stockée de Hello sont utilisées pour le transfert de documents qui en résultent.
* Capacité d’un document qui en résulte hello hello Hive, Pig, MapReduce travaux ou.
* [*Facultatif*] Capacité pour une collection supplémentaire.

> [!WARNING]
> Dans l’ordre tooavoid hello la création d’une nouvelle collection au cours des travaux de hello, vous pouvez imprimer hello résultats toostdout, enregistrez le conteneur de hello sortie tooyour WASB ou spécifiez un regroupement existant déjà. Dans les cas de hello de spécification d’une collection existante, des documents seront créées à l’intérieur de la collection de hello et des documents déjà existants ne seront supprimés s’il existe un conflit dans *ID*. **connecteur de Hello remplace automatiquement les documents existants avec des conflits d’id**. Vous pouvez désactiver cette fonctionnalité en définissant hello upsert option toofalse. Si upsert a la valeur false et si un conflit se produit, la tâche Hadoop de hello échoue ; une erreur de conflit d’id de rapport.
>
>

## <a name="ProvisionHDInsight"></a>Étape 1 : créer un cluster HDInsight
Ce didacticiel utilise Action de Script à partir de toocustomize du portail Azure hello votre cluster HDInsight. Dans ce didacticiel, nous utiliserons toocreate du portail Azure hello votre cluster HDInsight. Pour obtenir des instructions sur la façon dont les applets de commande PowerShell toouse ou hello HDInsight .NET SDK, extraire les [HDInsight de personnaliser des clusters à l’aide de Script Action] [ hdinsight-custom-provision] l’article.

1. Connectez-vous à toohello [Azure Portal][azure-portal].
2. Cliquez sur **+ nouveau** sur haut hello Hello barre de navigation gauche, recherchez **HDInsight** dans la barre de recherche supérieure hello sur le nouveau panneau de hello.
3. **HDInsight** publié par **Microsoft** s’affiche en haut de hello des résultats de hello. Cliquez dessus, puis cliquez sur **Créer**.
4. Sur le nouveau HDInsight Cluster de hello créer panneau, entrez votre **nom de Cluster** et sélectionnez hello **abonnement** vous souhaitez tooprovision cette ressource sous.

    <table border='1'>
        <tr><td>Nom du cluster</td><td>Cluster de nom hello.<br/>
Le nom DNS doit commencer et finir par un caractère alphanumérique et peut contenir des traits d’union.<br/>
champ de Hello doit être une chaîne comprise entre 3 et 63 caractères.</td></tr>
        <tr><td>Nom d'abonnement</td>
            <td>Si vous avez plusieurs abonnements Azure, sélectionnez l’abonnement hello qui hébergera votre cluster HDInsight. </td></tr>
    </table>
5.Cliquez sur **sélectionner le Type de Cluster** et hello ensemble suivant de propriétés toohello des valeurs spécifiées.

    <table border='1'>
        <tr><td>Type de cluster</td><td><strong>Hadoop</strong></td></tr>
        <tr><td>Niveau de cluster</td><td><strong>Standard</strong></td></tr>
        <tr><td>Système d'exploitation</td><td><strong>Windows</strong></td></tr>
        <tr><td>Version</td><td>version la plus récente</td></tr>
    </table>

    Maintenant, cliquez sur **SÉLECTIONNER**.

    ![Fournir des détails du cluster initial Hadoop HDInsight][image-customprovision-page1]
6. Cliquez sur **informations d’identification** tooset votre connexion et les informations d’identification de l’accès à distance. Choisissez le **nom de connexion au cluster** et le **mot de passe de connexion au cluster**.

    Si vous souhaitez tooremote dans votre cluster, sélectionnez *Oui* bas hello du Panneau de hello et fournir un nom d’utilisateur et un mot de passe.
7. Cliquez sur **Source de données** tooset accéder à votre emplacement principal pour les données. Choisissez hello **méthode de sélection** et spécifiez un compte de stockage déjà existant ou créez-en un.
8. On hello même panneau, spécifiez un **conteneur par défaut** et un **emplacement**. Et cliquez sur **SÉLECTIONNER**.

   > [!NOTE]
   > Sélectionnez une région du compte de base de données Cosmos pour de meilleures performances de tooyour fermer emplacement
   >
   >
9. Cliquez sur **tarification** tooselect hello nombre et le type de nœuds. Vous pouvez conserver configuration par défaut de hello et nombre de hello mise à l’échelle de nœuds Worker ultérieurement.
10. Cliquez sur **Configuration facultative**, puis **Actions de Script** Bonjour facultatif Panneau de Configuration.

     Dans Actions de Script, entrez hello suivant informations toocustomize votre cluster HDInsight.

     <table border='1'>
         <tr><th>Propriété</th><th>Valeur</th></tr>
         <tr><td>Nom</td>
             <td>Spécifiez un nom pour l’action de script hello.</td></tr>
         <tr><td>URI du script</td>
             <td>Spécifiez hello URI toohello script qui est appelée toocustomize hello cluster.</br></br>
Entrez : </br> <strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</td></tr>
         <tr><td>Nœud principal</td>
             <td>Cliquez sur toorun de case à cocher Bonjour Bonjour script PowerShell sur le nœud principal hello.</br></br>
             <strong>Activez cette case à cocher</strong>.</td></tr>
         <tr><td>Worker</td>
             <td>Cliquez sur hello case à cocher toorun hello PowerShell script sur le nœud de travail hello.</br></br>
             <strong>Activez cette case à cocher</strong>.</td></tr>
         <tr><td>Zookeeper</td>
             <td>Cliquez sur le script hello case à cocher toorun hello PowerShell sur hello soigneur.</br></br>
             <strong>Inutile</strong>.
             </td></tr>
         <tr><td>Paramètres</td>
             <td>Spécifiez des paramètres de hello, si requis par le script de hello.</br></br>
             <strong>Aucun paramètre requis</strong>.</td></tr>
     </table>
11. Créez un **Groupe de ressources** ou utilisez un groupe de votre abonnement Azure.
12. Examinez à présent **code confidentiel toodashboard** tootrack son déploiement et un clic **créer**!

## <a name="InstallCmdlets"></a>Étape 2 : installer et configurer Azure PowerShell
1. Installez Azure PowerShell. Vous trouverez des instructions [ici][powershell-install-configure].

   > [!NOTE]
   > Pour les requêtes Hive, vous pouvez également utiliser l'éditeur Hive en ligne de HDInsight. toodo, inscrivez-vous dans toohello [Azure Portal][azure-portal], cliquez sur **HDInsight** tooview de volet de gauche hello sur une liste de vos clusters HDInsight. Cliquez sur le cluster hello vous souhaitez que les requêtes Hive toorun sur, puis cliquez sur **Console de requête**.
   >
   >
2. Ouvrez hello environnement d’écriture de scripts intégré Azure PowerShell :

   * Sur un ordinateur exécutant Windows 8 ou Windows Server 2012 ou version ultérieure, vous pouvez utiliser intégrées de hello recherche. À partir de l’écran d’accueil hello, tapez **powershell ise** et cliquez sur **entrée**.
   * Sur un ordinateur exécutant une version antérieure à Windows 8 ou Windows Server 2012, utilisez le menu Démarrer de hello. À partir du menu Démarrer de hello, tapez **invite de commandes** dans la zone de recherche hello, puis, dans la liste hello des résultats, cliquez sur **invite de commandes**. Bonjour invite de commandes, tapez **powershell_ise** et cliquez sur **entrée**.
3. Ajoutez votre compte Azure.

   1. Dans le volet de la Console de hello, tapez **Add-AzureAccount** et cliquez sur **entrée**.
   2. Tapez hello adresse de messagerie associée à votre abonnement Azure et cliquez sur **continuer**.
   3. Tapez un mot de passe hello pour votre abonnement Azure.
   4. Cliquez sur **Se connecter**.
4. Hello suivant schéma identifie les parties importantes de hello de votre environnement de script Azure PowerShell.

    ![Diagramme d’Azure PowerShell][azure-powershell-diagram]

## <a name="RunHive"></a>Étape 3 : exécuter un travail Hive à l’aide de Cosmos DB et HDInsight
> [!IMPORTANT]
> Toutes les variables indiquées par < > doivent être renseignées à l’aide de vos paramètres de configuration.
>
>

1. Hello ensemble suivant de variables dans votre volet de PowerShell Script.

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p>Commençons à construire votre chaîne de requête. Nous allons écrire une requête Hive qui Récupère tous les documents générés par le système horodateurs (DTS) et des identificateurs uniques (_rid) à partir d’une collection de base de données Azure Cosmos, comptabilise tous les documents par minute de hello et stocke ensuite les résultats de hello dans une nouvelle collection de base de données Azure Cosmos.</p>

    <p>Commençons par créer une table Hive à partir de notre collection Azure Cosmos DB. Ajouter hello suivant extrait de code toohello volet de PowerShell Script <strong>après</strong> extrait de code hello de #1. Veillez à qu'inclure hello facultatif DocumentDB.query paramètre t trim nos documents toojust _ts et le _rid.</p>

   > [!NOTE]
   > **L’attribution du nom DocumentDB.inputCollections n’était pas une erreur.** Oui, nous autorisons l'ajout de plusieurs collections en tant qu'entrée : </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. Ensuite, nous allons créer une table Hive pour la collection de sortie hello. propriétés de document de sortie Hello sera hello mois, jour, heure, minute et nombre total de hello d’occurrences.

   > [!NOTE]
   > **Une fois encore, l’attribution du nom DocumentDB.outputCollections n’était pas une erreur.** Oui, nous autorisons l'ajout de plusieurs collections en tant que sortie : </br>
   > '*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*' </br> noms de collection Hello sont séparés sans espaces, à l’aide uniquement une virgule. </br></br>
   > Les documents seront distribués en tourniquet (round robin), sur plusieurs collections. Un lot de documents est stocké dans une collection, puis un deuxième lot de documents est stocké dans la collection suivante de hello et ainsi de suite.
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. Enfin, nous allons tally hello des documents par mois, jour, heure et minute et insérer les résultats de hello en hello sortie table Hive.

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. Ajoutez hello suivant extrait de code de script toocreate une définition de tâche Hive à partir de la requête précédente de hello.

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    Vous pouvez également utiliser hello - fichier basculer toospecify un fichier de script HiveQL sur HDFS.
4. Ajouter hello suivant l’heure de début d’extrait de code toosave hello et envoi de la tâche de ruche hello.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. Ajoutez hello suivant toowait pour hello ruche travail toocomplete.

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. Ajouter hello suivant tooprint hello standard sortie et hello démarrez heures et de fin.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. **Exécutez** votre nouveau script ! **Cliquez sur** vert de hello bouton d’exécution.
8. Vérifier les résultats de hello. L’authentification à hello [Azure Portal][azure-portal].

   1. Cliquez sur <strong>Parcourir</strong> sur le panneau de gauche hello. </br>
   2. Cliquez sur <strong>tout</strong> en haut à droite de hello du Panneau de navigation hello. </br>
   3. Recherchez les <strong>comptes Azure Cosmos DB</strong>, puis cliquez sur ces derniers. </br>
   4. Ensuite, recherchez votre <strong>compte de base de données Azure Cosmos</strong>, puis <strong>base de données de base de données Azure Cosmos</strong> et votre <strong>Azure Cosmos DB Collection</strong> associée hello collection de sortie spécifiée dans votre requête Hive.</br>
   5. Pour finir, cliquez sur <strong>Explorateur de documents</strong> sous <strong>Outils de développement</strong>.</br></p>

   Vous verrez des résultats de votre requête Hive hello.

   ![Résultats de la requête Hive][image-hive-query-results]

## <a name="RunPig"></a>Étape 4 : exécuter un travail Pig à l’aide de Cosmos DB et HDInsight
> [!IMPORTANT]
> Toutes les variables indiquées par < > doivent être renseignées à l’aide de vos paramètres de configuration.
>
>

1. Hello ensemble suivant de variables dans votre volet de PowerShell Script.

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p>Commençons à construire votre chaîne de requête. Nous allons écrire une requête Pig qui Récupère tous les documents générés par le système horodateurs (DTS) et des identificateurs uniques (_rid) à partir d’une collection de base de données Azure Cosmos, comptabilise tous les documents par minute de hello et stocke ensuite les résultats de hello dans une nouvelle collection de base de données Azure Cosmos.</p>
    <p>Chargez d’abord des documents Cosmos DB dans HDInsight. Ajouter hello suivant extrait de code toohello volet de PowerShell Script <strong>après</strong> extrait de code hello de #1. Assurez-vous que tooadd un DocumentDB requête tootrim DocumentDB facultatif du paramètre de requête toohello nos documents toojust _ts et le _rid.</p>

   > [!NOTE]
   > Oui, nous autorisons l'ajout de plusieurs collections en tant qu'entrée : </br>
   > '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</br> noms de collection Hello sont séparés sans espaces, à l’aide uniquement une virgule. </b>
   >
   >

    Les documents seront distribués en tourniquet (round robin), sur plusieurs collections. Un lot de documents est stocké dans une collection, puis un deuxième lot de documents est stocké dans la collection suivante de hello et ainsi de suite.

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. Ensuite, nous allons calculer les documents hello en hello mois, jour, heure, minute et nombre total de hello d’occurrences.

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. Enfin, nous allons stocker les résultats de hello dans notre nouvelle collection de sortie.

   > [!NOTE]
   > Oui, nous autorisons l'ajout de plusieurs collections en tant que sortie : </br>
   > '\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</br> noms de collection Hello sont séparés sans espaces, à l’aide uniquement une virgule.</br>
   > Documents va être distribué de tourniquet (Round Robin) entre hello plusieurs collections. Un lot de documents est stocké dans une collection, puis un deuxième lot de documents est stocké dans la collection suivante de hello et ainsi de suite.
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. Ajoutez hello suivant extrait de code de script toocreate une définition de tâche Pig à partir de la requête précédente de hello.

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    Vous pouvez également utiliser hello - fichier basculer toospecify un fichier de script Pig sur HDFS.
6. Ajouter hello suivant l’heure de début d’extrait de code toosave hello et envoi de la tâche de Pig hello.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. Ajoutez hello suivant toowait pour toocomplete de travail Pig hello.

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. Ajouter hello suivant tooprint hello standard sortie et hello démarrez heures et de fin.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. **Exécutez** votre nouveau script ! **Cliquez sur** vert de hello bouton d’exécution.
10. Vérifier les résultats de hello. L’authentification à hello [Azure Portal][azure-portal].

    1. Cliquez sur <strong>Parcourir</strong> sur le panneau de gauche hello. </br>
    2. Cliquez sur <strong>tout</strong> en haut à droite de hello du Panneau de navigation hello. </br>
    3. Recherchez les <strong>comptes Azure Cosmos DB</strong>, puis cliquez sur ces derniers. </br>
    4. Ensuite, recherchez votre <strong>compte de base de données Azure Cosmos</strong>, puis <strong>base de données de base de données Azure Cosmos</strong> et votre <strong>Azure Cosmos DB Collection</strong> associée hello collection de sortie spécifiée dans votre requête Pig.</br>
    5. Pour finir, cliquez sur <strong>Explorateur de documents</strong> sous <strong>Outils de développement</strong>.</br></p>

    Vous verrez des résultats de votre requête Pig hello.

    ![Résultats de la requête Pig][image-pig-query-results]

## <a name="RunMapReduce"></a>Étape 5 : exécuter une tâche MapReduce à l’aide d’Azure Cosmos DB et HDInsight
1. Hello ensemble suivant de variables dans votre volet de PowerShell Script.

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. Nous allons exécuter une tâche MapReduce qui comptabilise le nombre de hello d’occurrences de chaque propriété de Document à partir de votre collection de base de données Azure Cosmos. Ajoutez cet extrait de script **après** extrait de code hello ci-dessus.

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > TallyProperties-v01.jar est fourni avec une installation personnalisée de hello Cosmos DB Hadoop connecteur hello.
   >
   >
3. Ajoutez hello suivant la tâche de commande toosubmit hello MapReduce.

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    En outre toohello définition de la tâche MapReduce, vous fournissez également nom du cluster HDInsight hello où vous souhaitez tâche MapReduce de hello toorun et les informations d’identification hello. Hello Start-AzureHDInsightJob est un appel asynchrone. toocheck hello hello travail achevé, utilisez hello *Wait-AzureHDInsightJob* applet de commande.
4. Ajoutez hello suivant de commande toocheck des erreurs avec la tâche de MapReduce hello en cours d’exécution.

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. **Exécutez** votre nouveau script ! **Cliquez sur** vert de hello bouton d’exécution.
6. Vérifier les résultats de hello. L’authentification à hello [Azure Portal][azure-portal].

   1. Cliquez sur <strong>Parcourir</strong> sur le panneau de gauche hello.
   2. Cliquez sur <strong>tout</strong> en haut à droite de hello du Panneau de navigation hello.
   3. Recherchez les <strong>comptes Azure Cosmos DB</strong>, puis cliquez sur ces derniers.
   4. Ensuite, recherchez votre <strong>compte de base de données Azure Cosmos</strong>, puis <strong>base de données de base de données Azure Cosmos</strong> et votre <strong>Azure Cosmos DB Collection</strong> associée hello collection de sortie spécifiée dans votre tâche MapReduce.
   5. Pour finir, cliquez sur <strong>Explorateur de documents</strong> sous <strong>Outils de développement</strong>.

      Vous verrez des résultats de votre tâche MapReduce hello.

      ![Résultats de la requête MapReduce][image-mapreduce-query-results]

## <a name="NextSteps"></a>Étapes suivantes
Félicitations ! Vous venez d’exécuter vos premiers travaux Hive, Pig et MapReduce à l’aide d’Azure Cosmos DB et HDInsight.

Le code source de notre connecteur Hadoop est disponible gratuitement. Si vous êtes intéressé, vous pouvez apporter votre contribution sur [GitHub][github].

toolearn, voir hello suivant des articles :

* [Développement d’une application Java avec DocumentDB][documentdb-java-application]
* [Développement de programmes MapReduce en Java pour Hadoop dans HDInsight][hdinsight-develop-deploy-java-mapreduce]
* [Prise en main Hadoop avec ruche en cours d’utilisation de HDInsight tooanalyze combiné mobile][hdinsight-get-started]
* [Utilisation de MapReduce avec HDInsight][hdinsight-use-mapreduce]
* [Utilisation de Hive avec HDInsight][hdinsight-use-hive]
* [Utilisation de Pig avec HDInsight][hdinsight-use-pig]
* [Personnaliser des clusters HDInsight à l'aide d'une action de script][hdinsight-hadoop-customize-cluster]

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
