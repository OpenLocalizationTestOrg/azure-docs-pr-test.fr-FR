---
title: "données de retard de vol aaaAnalyze avec Hadoop dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment toouse un Windows PowerShell script toocreate un cluster HDInsight, exécuter un travail Hive, exécuter un travail Sqoop et supprimer hello cluster."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a>Analyse des données sur les retards de vol avec Hive dans HDInsight
Hive permet d’exécuter des tâches Hadoop MapReduce via un langage de création de scripts semblable à SQL, nommé *[HiveQL][hadoop-hiveql]*, qui peut être appliqué à la synthèse, à l’envoi de requêtes et à l’analyse d’importants volumes de données.

> [!IMPORTANT]
> Hello étapes décrites dans ce document nécessitent un cluster HDInsight de basés sur Windows. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Pour les étapes fonctionnant avec un cluster basé sur Linux, consultez la rubrique [Analyse des données sur les retards de vol avec Hive dans HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).

Un des principaux avantages de hello d’Azure HDInsight est séparation hello de calcul et de stockage de données. HDInsight utilise le stockage d’objets blob Azure pour stocker les données. Une tâche classique comprend trois parties :

1. **Le stockage des données dans un stockage d’objets blob Azure.**  Par exemple, les données météorologiques, les données de capteur, les journaux web et, en l’occurrence, les données liées aux retards de vol, sont enregistrés dans un stockage d’objets blob Azure.
2. **L’exécution des tâches.** Lorsqu’il est données hello tooprocess du temps, vous exécutez un script Windows PowerShell (ou une application cliente) toocreate un cluster HDInsight, exécuter des travaux et supprimer le cluster de hello. travaux Hello enregistrer les données de sortie tooAzure stockage d’objets Blob. les données de sortie Hello sont conservées même après la suppression de cluster de hello. De cette façon, vous ne payez que ce que vous avez consommé.
3. **Récupérer la sortie de hello du stockage d’objets Blob Azure**, ou dans ce didacticiel, exporter la base de données SQL Azure hello données tooan.

Hello diagramme suivant illustre le scénario de hello et structure hello de ce didacticiel :

![HDI.FlightDelays.flow][img-hdi-flightdelays-flow]

Notez que les nombres hello dans le diagramme de hello correspondent toohello les titres de section. **M** représente le processus principal hello. **A** représente le contenu dans l’annexe de hello hello.

partie principale de Hello du didacticiel de hello vous montre des tâches de toouse un Windows PowerShell script tooperform hello suivant :

* Créez un cluster HDInsight.
* Exécuter un travail Hive sur des retards de hello cluster toocalculate moyenne dans les aéroports. données de retard de vol Hello sont stockées dans un compte de stockage d’objets Blob Azure.
* Exécuter un Sqoop travail tooexport hello ruche travail sortie tooan SQL Azure de base de données.
* Supprimer le cluster HDInsight de hello.

Dans les annexes hello, vous trouverez des instructions de hello pour télécharger des données de retard de vol, création/chargement d’une chaîne de requête Hive et préparation de la base de données SQL Azure hello pour le travail de Sqoop hello.

> [!NOTE]
> étapes de Hello dans ce document sont des clusters HDInsight tooWindows spécifiques. Pour les étapes fonctionnant avec un cluster basé sur Linux, consultez la rubrique [Analyse des données sur les retards de vol avec Hive dans HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).

### <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer des éléments suivants de hello :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Un poste de travail sur lequel est installé Azure PowerShell**.

    > [!IMPORTANT]
    > La prise en charge de la gestion des ressources HDInsight par Azure PowerShell à l’aide d’Azure Service Manager est **déconseillée** ; elle a été supprimée le 1er janvier 2017. étapes de Hello dans ce document Utilisez hello nouvelles applets de commande HDInsight qui fonctionnent avec Azure Resource Manager.
    >
    > Suivez les étapes de hello dans [installer et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello dernière version d’Azure PowerShell. Si vous avez des scripts qui toobe besoin modifié toouse hello nouvelles applets de commande qui fonctionnent avec Azure Resource Manager, consultez [des outils de migration tooAzure développement basé sur le Gestionnaire de ressources pour les clusters HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) pour plus d’informations.

**Fichiers utilisés dans ce didacticiel**

Ce didacticiel utilise hello sur performances compagnie aérienne de données de vol de [recherche et Administration de la technologie novatrice, Bureau de statistiques de transport ou RITA][rita-website].
Une copie de hello données a été téléchargé tooan conteneur de stockage d’objets Blob Azure avec l’autorisation d’accès Public Blob hello.
Une partie de votre script PowerShell copie des données de hello de hello blob publics conteneur toohello par défaut conteneur d’objets blob de votre cluster. Hello HiveQL script est également copié toohello même conteneur d’objets Blob.
Si vous souhaitez toolearn comment tooget/téléchargement hello données tooyour propriétaire de compte de stockage, et comment toocreate/téléchargement hello HiveQL script de fichier, consultez [annexe A](#appendix-a) et [annexe B](#appendix-b).

Hello tableau suivant répertorie les fichiers hello utilisés dans ce didacticiel :

<table border="1">
<tr><th>Fichiers</th><th>Description</th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td>fichier de script HiveQL Hello utilisé par hello tâche Hive. Ce script a été téléchargé tooan compte de stockage d’objets Blob Azure avec un accès public hello. <a href="#appendix-b">Annexe B</a> contient des instructions sur la préparation et le téléchargement de ce compte de stockage de fichier tooyour propre objets Blob Azure.</td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td>Données d’entrée pour le travail de ruche hello. les données de salutation a été téléchargé tooan compte de stockage d’objets Blob Azure avec un accès public hello. <a href="#appendix-a">Annexe A</a> contient des instructions sur l’obtention de données de hello et le téléchargement de compte de stockage Azure Blob propre hello données tooyour.</td></tr>
<tr><td>\tutorials\flightdelays\output</td><td>chemin de sortie Hello pour le travail de ruche hello. conteneur par défaut de Hello est utilisé pour stocker les données de sortie hello.</td></tr>
<tr><td>\tutorials\flightdelays\jobstatus</td><td>Hello ruche travail état dossier conteneur par défaut de hello.</td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a>Création d’un cluster et exécution de tâches Hive/Sqoop
Hadoop MapReduce correspond au traitement par lots. Hello plus rentable toorun un travail Hive est toocreate un cluster pour la tâche de hello et supprimer le travail de hello après la tâche de hello. Hello script suivant couvre les processus hello.
Pour plus d’informations sur la création d’un cluster HDInsight et l’exécution de tâches Hive, consultez les rubriques [Création de clusters Hadoop dans HDInsight][hdinsight-provision] et [Utilisation de Hive avec HDInsight][hdinsight-use-hive].

**requêtes Hive toorun hello par Azure PowerShell**

1. Créer une table de base de données et hello SQL Azure pour la sortie de tâche hello Sqoop à l’aide d’instructions hello dans [annexe C](#appendix-c).
2. Ouvrez Windows PowerShell ISE et exécutez hello script suivant :

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

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
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit hello Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. Connexion de base de données SQL tooyour et consultez les retards de vol moyenne par ville dans la table de AvgDelays hello :

    ![HDI.FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <a id="appendix-a"></a>Annexe A - téléchargement flight delay données tooAzure stockage d’objets Blob
Téléchargement du fichier de données hello et les fichiers de script de HiveQL hello (consultez [annexe B](#appendix-b)) requiert une planification. Hello est toostore des fichiers de données hello et fichier de HiveQL hello avant de créer un cluster HDInsight et de travail de ruche hello en cours d’exécution. Deux options s'offrent à vous :

* **Utilisez hello même compte de stockage Azure qui servira par cluster HDInsight de hello en tant que système de fichiers par défaut hello.** Étant donné que le cluster HDInsight de hello aura hello compte clé d’accès, vous n’avez pas besoin toomake des modifications supplémentaires.
* **Utilisez un compte de stockage Azure différent de hello système de fichiers HDInsight cluster par défaut.** Si c’est le cas de hello, vous devez modifier la partie de la création de hello Hello Windows PowerShell script trouvé dans [cluster HDInsight de créer et tâches d’exécution Hive/Sqoop](#runjob) toolink hello compte de stockage comme un compte de stockage supplémentaire. Pour plus d’informations, consultez la rubrique [Création de clusters Hadoop dans HDInsight][hdinsight-provision]. cluster HDInsight de Hello sait ensuite la clé d’accès hello hello compte de stockage.

> [!NOTE]
> Bonjour le chemin d’accès de stockage Blob pour hello fichier de données est codé en dur dans le fichier de script HiveQL hello. Vous devez le mettre à jour en conséquence.

**données de vol hello toodownload**

1. Parcourir trop[recherche et l’Administration de technologie novatrice, Bureau de statistiques de transport][rita-website].
2. Sur la page de hello, sélectionnez hello valeurs suivantes :

    <table border="1">
    <tr><th>Nom</th><th>Valeur</th></tr>
    <tr><td>Filtre année</td><td>2013 </td></tr>
    <tr><td>Filtre période</td><td>Janvier</td></tr>
    <tr><td>Champs</td><td>*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (effacez tous les autres champs)</td></tr>
    </table>
3. Cliquez sur **Télécharger**.
4. Décompressez hello fichier toohello **C:\Tutorials\FlightDelay\2013Data** dossier. Chaque fichier correspond à un fichier CSV d’environ 60 Go.
5. Renommer hello fichier toohello du mois hello qu’il contient des données. Par exemple, fichier hello contenant hello janvier données serait nommé *January.csv*.
6. Répétez le toodownload les étapes 2 et 5 un fichier pour chaque hello 12 mois dans 2013. Vous devez au minimum un didacticiel de hello toorun fichier.

**tooupload hello flight delay données tooAzure stockage d’objets Blob**

1. Préparer les paramètres hello :

    <table border="1">
    <tr><th>Nom de la variable</th><th>Remarques</th></tr>
    <tr><td>$storageAccountName</td><td>compte de stockage Azure où vous souhaitez que les données hello tooupload de Hello.</td></tr>
    <tr><td>$blobContainerName</td><td>conteneur d’objets Blob Hello où vous souhaitez que les données hello tooupload.</td></tr>
    </table>
2. Ouvrez Azure PowerShell ISE.
3. Collez hello script suivant dans le volet de script hello :

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. Appuyez sur **F5** script de hello toorun.

Si vous choisissez toouse une autre méthode de téléchargement des fichiers de hello, assurez-vous que le chemin d’accès du fichier hello est didacticiels/flightdelay/données. syntaxe Hello pour accéder aux fichiers de hello est :

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

Hello chemin didacticiels/flightdelay/données est un dossier virtuel de hello que vous avez créé lorsque vous avez téléchargé les fichiers hello. Assurez-vous qu'il existe 12 fichiers, un par mois.

> [!NOTE]
> Vous devez mettre à jour hello ruche requête tooread à partir de l’emplacement du nouveau hello.
>
> Vous devez configurer hello conteneur accès autorisation toobe public ou lier toohello de compte de stockage hello cluster HDInsight. Sinon, chaîne de requête Hive hello ne sera pas en mesure de tooaccess des fichiers de données hello.

- - -

## <a id="appendix-b"></a>Annexe B - Création et téléchargement d’un script HiveQL
À l’aide d’Azure PowerShell, vous pouvez exécuter plusieurs instructions HiveQL une à une heure ou package hello HiveQL instruction dans un fichier de script. Cette section vous montre comment toocreate un script HiveQL hello de chargement de script et tooAzure stockage d’objets Blob à l’aide d’Azure PowerShell. Ruche requiert hello HiveQL scripts toobe stockée dans le stockage Blob Azure.

Hello script HiveQL effectuera suivant de hello :

1. **Supprimer la table de delays_raw hello**, au cas où la table hello existe déjà.
2. **Créer une table Hive externe hello delays_raw** pointant d’emplacement de stockage d’objets Blob toohello avec les fichiers de retard de vol hello. Cette requête spécifie les champs délimités par « , » et les lignes se terminant par « \n ». Cela pose un problème lorsque les valeurs de champ contiennent des virgules, car la ruche ne peut pas différencier une virgule est un délimiteur de champ et un qui fait partie d’une valeur de champ (qui est le cas de hello dans les valeurs de champ pour l’origine\_Ville\_nom et DEST\_ Ville\_nom). tooaddress, hello requête crée les colonnes TEMP données toohold sont incorrectement divisées en colonnes.
3. **Supprimer la table de retards hello**, au cas où la table hello existe déjà.
4. **Créer la table de retards hello**. Il est utile tooclean les données de hello avant tout traitement supplémentaire. Cette requête crée une nouvelle table, *retards*, à partir de la table de delays_raw hello. Notez que les colonnes TEMP hello (comme indiqué précédemment) ne sont pas copiés et ce hello **sous-chaîne** fonction est guillemets tooremove utilisés à partir des données de hello.
5. **Calcul résultats hello hello météo moyenne délai et les groupes par nom de ville.** Il produira également de stockage de tooBlob résultats hello. Notez cette requête hello supprimera les apostrophes à partir des données de hello et exclut les lignes où la valeur hello pour **weather_delay** a la valeur null. Ces mesures sont nécessaires, car Sqoop, qui est utilisé ultérieurement dans ce didacticiel, ne gère pas correctement ces valeurs par défaut.

Pour obtenir une liste complète des commandes de HiveQL hello, consultez [Hive Data Definition Language][hadoop-hiveql]. Chaque commande HiveQL doit se terminer par un point virgule.

**toocreate un fichier de script HiveQL**

1. Préparer les paramètres hello :

    <table border="1">
    <tr><th>Nom de la variable</th><th>Remarques</th></tr>
    <tr><td>$storageAccountName</td><td>Hello compte de stockage Azure où vous souhaitez que tooupload hello script HiveQL.</td></tr>
    <tr><td>$blobContainerName</td><td>conteneur d’objets Blob Hello où vous souhaitez que tooupload hello script HiveQL.</td></tr>
    </table>
2. Ouvrez Azure PowerShell ISE.
3. Copiez et collez le script suivant dans le volet de script hello de hello :

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    Voici les variables hello utilisées dans le script de hello :

   * **$hqlLocalFileName** -hello script enregistre fichier de script HiveQL hello localement avant de le télécharger tooBlob stockage. Il s’agit de nom de fichier hello. la valeur par défaut Hello est <u>C:\tutorials\flightdelay\flightdelays.hql</u>.
   * **$hqlBlobName** -hello HiveQL script blob nom du fichier utilisé dans hello le stockage Blob Azure. valeur par défaut de Hello est tutorials/flightdelay/flightdelays.hql. Étant donné que hello fichier sera écrit directement tooAzure stockage d’objets Blob, il n’est pas un « / » au début de hello du nom d’objet blob hello. Si vous voulez tooaccess hello depuis le stockage Blob, vous devez tooadd « / » au début de hello hello du nom de fichier.
   * **$srcDataFolder** et **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"

- - -
## <a id="appendix-c"></a>Annexe C - préparer une base de données SQL Azure hello sortie de travail Sqoop
**base de données SQL tooprepare hello (fusionne avec hello Sqoop script)**

1. Préparer les paramètres hello :

    <table border="1">
    <tr><th>Nom de la variable</th><th>Remarques</th></tr>
    <tr><td>$sqlDatabaseServerName</td><td>nom de Hello du serveur de base de données SQL Azure hello. Entrez rien toocreate un nouveau serveur.</td></tr>
    <tr><td>$sqlDatabaseUsername</td><td>nom de connexion Hello pour le serveur de base de données SQL Azure hello. Si $sqlDatabaseServerName est un serveur existant, connexion de hello et le mot de passe sont tooauthenticate utilisé avec le serveur de hello. Sinon, elles sont utilisée toocreate un nouveau serveur.</td></tr>
    <tr><td>$sqlDatabasePassword</td><td>Hello mot de passe pour le serveur de base de données SQL Azure hello.</td></tr>
    <tr><td>$sqlDatabaseLocation</td><td>Cette valeur est uniquement utilisée lors de la création d’un nouveau serveur de base de données Azure.</td></tr>
    <tr><td>$sqlDatabaseName</td><td>base de données SQL Hello utilisé table de AvgDelays toocreate hello pour le travail de Sqoop hello. Si vous laissez cette valeur vide, une base de données intitulée HDISqoop est créée. nom de la table Hello pour hello sortie de travail Sqoop est AvgDelays. </td></tr>
    </table>
2. Ouvrez Azure PowerShell ISE.
3. Copiez et collez le script suivant dans le volet de script hello de hello :

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > Hello script utilise un service de transfert (REST) état representational, http://bot.whatismyipaddress.com, tooretrieve votre adresse IP externe. adresse IP de Hello est utilisé pour la création d’une règle de pare-feu pour votre serveur de base de données SQL.

    Voici quelques-unes des variables utilisées dans le script de hello :

   * **$ipAddressRestService** -valeur par défaut de hello est http://bot.whatismyipaddress.com. Il s’agit d’un service REST d’adresse IP publique permettant d’obtenir votre adresse IP externe. Vous pouvez utiliser d'autres services si vous voulez. adresse IP externe Hello récupérée via le service de hello sera utilisé toocreate une règle de pare-feu pour votre serveur de base de données SQL Azure, afin que vous pouvez accéder de la base de données hello à partir de votre station de travail (en utilisant un script Windows PowerShell).
   * **$fireWallRuleName** -il s’agit d’un nom de hello hello de règle de pare-feu pour le serveur de base de données SQL Azure hello. le nom par défaut Hello est <u>FlightDelay</u>. Vous pouvez le renommer si vous voulez.
   * **$sqlDatabaseMaxSizeGB** - Cette valeur est uniquement utilisée lors de la création d’un nouveau serveur de base de données SQL Azure. valeur par défaut de Hello est de 10 Go. Une capacité de 10 Go est suffisante pour ce didacticiel.
   * **$sqlDatabaseName** - Cette valeur est uniquement utilisée lors de la création d’une nouvelle base de données SQL Azure. valeur par défaut de Hello est HDISqoop. Si vous renommez, vous devez mettre à jour en conséquence hello Sqoop de script Windows PowerShell.
4. Appuyez sur **F5** script de hello toorun.
5. Valider la sortie du script hello. Assurez-vous que le script de hello s’est correctement exécutée.

## <a id="nextsteps"></a> Étapes suivantes
Présent que vous savez comment tooupload un tooAzure fichier stockage d’objets Blob, comment toopopulate une ruche de table à l’aide de données hello du stockage d’objets Blob Azure, comment toorun Hive requêtes et comment toouse données tooexport de Sqoop à partir de la base de données SQL Azure de tooan HDFS. toolearn, voir hello suivant des articles :

* [Prise en main de HDInsight][hdinsight-get-started]
* [Utilisation de Hive avec HDInsight][hdinsight-use-hive]
* [Utilisation d’Oozie avec HDInsight][hdinsight-use-oozie]
* [Utilisation de Sqoop avec HDInsight][hdinsight-use-sqoop]
* [Utilisation de Pig avec HDInsight][hdinsight-use-pig]
* [Développement de programmes MapReduce en Java pour HDInsight][hdinsight-develop-mapreduce]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
