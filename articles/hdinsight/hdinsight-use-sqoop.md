---
title: aaaRun Apache Sqoop travaux Azure hdinsight (Hadoop) | Documents Microsoft
description: "Découvrez comment toouse Azure PowerShell à partir d’une station de travail de toorun Sqoop importer et exporter entre un cluster Hadoop et une base de données SQL Azure."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 2fdcc6b7-6ad5-4397-a30b-e7e389b66c7a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bdac507704937d77921c9c13d70aa2434c7e3be4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a>Utilisation de Sqoop avec Hadoop dans HDInsight
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Découvrez comment toouse Sqoop dans HDInsight tooimport et d’exportation entre le cluster HDInsight et de la base de données SQL Azure ou base de données SQL Server.

Bien que Hadoop est un choix naturel pour le traitement des données non structurées et semi-structurées, telles que les journaux et les fichiers, il peut également être un besoin de données tooprocess structurées stockées dans les bases de données relationnelles.

[Sqoop] [ sqoop-user-guide-1.4.4] est un outil conçu de tootransfer des données entre les clusters Hadoop et des bases de données relationnelles. Vous pouvez l’utiliser tooimport des données à partir d’un système de gestion de base de données relationnelle (SGBDR) telles que SQL Server, MySQL ou Oracle dans le système de fichiers DFS Hadoop hello (HDFS), transformer des données dans Hadoop MapReduce ou ruche hello et puis exporter les données hello dans un SGBDR. Dans ce didacticiel, vous allez utiliser une base de données SQL Server comme base de données relationnelle.

Pour les versions de Sqoop sont pris en charge sur les clusters HDInsight, consultez [quelles sont les nouveautés dans les versions de cluster hello fournies par HDInsight ?][hdinsight-versions]

## <a name="understand-hello-scenario"></a>Comprendre le scénario de hello

Le cluster HDInsight inclut des exemples de données. Vous utilisez hello suivant deux exemples :

* Un fichier journal log4j situé sous */example/data/sample.log*. Hello suivant les journaux est extraits à partir du fichier de hello :
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* Une table Hive nommée *hivesampletable*, lequel références hello le fichier de données situé à */hive/warehouse/hivesampletable*. table de Hello contient des données de l’appareil mobile. 
  
  | Champ | Type de données |
  | --- | --- |
  | clientid |string |
  | querytime |string |
  | market |string |
  | deviceplatform |string |
  | devicemake |string |
  | devicemodel |string |
  | state |string |
  | country |string |
  | querydwelltime |double |
  | sessionid |bigint |
  | sessionpagevieworder |bigint |

Tout d’abord, vous exportez *exemple.log* et *hivesampletable* base de données SQL Azure toohello ou tooSQL Server puis table hello d’importation qui contient les données des appareils mobiles hello sauvegarder tooHDInsight à l’aide de hello chemin d’accès suivant :

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a>Création du cluster et de la base de données SQL
Cette section vous montre comment toocreate un cluster, une base de données SQL et schémas de base de données SQL hello pour en cours d’exécution hello didacticiel à l’aide de hello portail Azure et un modèle Azure Resource Manager. modèle de Hello peut se trouver dans [modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/). modèle de gestionnaire de ressources Hello appelle un bacpac package toodeploy hello table schémas tooSQL de base de données.  package bacpac de Hello se trouve dans un conteneur d’objet blob public, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac. Si vous voulez toouse un conteneur privé pour les fichiers bacpac hello, utilisez hello valeurs dans le modèle de hello suivantes :
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

Si vous préférez le cluster de hello toocreate toouse Azure PowerShell et hello de base de données SQL, consultez [annexe A](#appendix-a---a-powershell-sample).

1. Cliquez sur hello suivant image tooopen un modèle de gestionnaire de ressources Bonjour portail Azure.         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. Entrez hello propriétés suivantes :

    - **Abonnement** : indiquez votre abonnement Azure.
    - **Groupe de ressources** : créez un groupe de ressources Azure ou sélectionnez un groupe de ressources existant.  Un groupe de ressources est destiné à la gestion.  C’est un conteneur d’objets.
    - **Emplacement** : sélectionnez une région.
    - **ClusterName**: entrez un nom pour le cluster Hadoop de hello.
    - **Nom de connexion et mot de passe de cluster**: nom de connexion hello par défaut est Admin.
    - **Nom d’utilisateur et mot de passe SSH**.
    - **Nom et mot de passe de connexion au serveur de base de données SQL**.
    - **_artifacts emplacement**: utiliser la valeur par défaut de hello sauf si vous souhaitez toouse votre propre fichier à DOS dans un emplacement différent.
    - **_artifacts Location Sas Token** (Jeton SAP d’emplacement _artifacts) : laissez ce champ vide.
    - **Nom du fichier Bacpac**: utiliser la valeur par défaut de hello sauf si vous souhaitez toouse votre propre fichier à DOS.
     
     Hello valeurs suivantes est codés en dur dans la section des variables hello :
     
     | Nom du compte de stockage par défaut | <CluterName>store |
     | --- | --- |
     | Nom du serveur de base de données SQL Azure. |<ClusterName>dbserver |
     | Nom de la base de données SQL Azure |<ClusterName>db |
     
     Veuillez noter ces valeurs.  Vous avez besoin plus tard dans le didacticiel de hello.

3. Cliquez sur **OK** toosave les paramètres hello.

4. à partir de hello **les déploiement personnalisé** panneau, cliquez sur **groupe de ressources** déroulante zone, puis cliquez sur **nouveau** toocreate un groupe de ressources. groupe de ressources Hello est un conteneur qui regroupe le cluster de hello, compte de stockage dépendant de hello et autres ressources liées.

5.Cliquez sur **Conditions juridiques**, puis cliquez sur **Créer**.

6.Cliquez sur **Créer**. Une nouvelle vignette intitulée Envoi du déploiement pour Déploiement de modèle s’affiche. Cela prend environ le cluster de hello toocreate environ 20 minutes et la base de données SQL.

Si vous choisissez la base de données SQL Azure toouse ou Microsoft SQL Server

* **Base de données SQL Azure**: vous devez configurer une règle de pare-feu pour hello accès au tooallow du serveur de base de données SQL Azure à partir de votre station de travail. Pour obtenir des instructions sur la création d’une base de données SQL Azure et de configuration du pare-feu de hello, consultez [prise en main de la base de données SQL Azure][sqldatabase-get-started]. 
  
  > [!NOTE]
  > Par défaut, une base de données SQL Azure autorise des connexions aux services Azure tels qu’Azure HDinsight. Si ce paramètre de pare-feu est désactivé, vous devez tooenable à partir de hello portail Azure. Pour obtenir des instructions sur la création d’une base de données SQL Azure et la configuration des règles de pare-feu, consultez la rubrique [Création et configuration d’une base de données SQL][sqldatabase-create-configue].
  > 
  > 
* **SQL Server**: Si votre cluster HDInsight se trouve sur hello même réseau virtuel dans Azure en tant que SQL Server, vous pouvez utiliser les étapes de hello dans cet article tooimport et exportation de données tooa de données SQL Server.
  
  > [!NOTE]
  > HDInsight prend en charge uniquement les réseaux virtuels basés sur l'emplacement et ne fonctionne pas pour le moment avec des réseaux virtuels basés sur des groupes d'affinités.
  > 
  > 
  
  * toocreate et configurer un réseau virtuel, consultez [créer un réseau virtuel à l’aide de hello Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    
    * Lorsque vous utilisez SQL Server dans votre centre de données, vous devez configurer le réseau virtuel hello *site-à-site* ou *point-to-site*.
      
      > [!NOTE]
      > Pour **point-to-site** des réseaux virtuels, SQL Server doivent exécuter hello VPN client application de configuration, qui est disponible à partir de hello **tableau de bord** de votre configuration de réseau virtuel Azure.
      > 
      > 
    * Lorsque vous utilisez SQL Server sur une machine virtuelle Azure, toute configuration de réseau virtuel peut être utilisée si la machine virtuelle de hello hébergeant SQL Server est un membre de hello même réseau virtuel que HDInsight.
  * toocreate un cluster HDInsight sur un réseau virtuel, consultez [Hadoop de créer des clusters dans HDInsight à l’aide des options personnalisées](hdinsight-hadoop-provision-linux-clusters.md)
    
    > [!NOTE]
    > SQL Server doit également autoriser l'authentification. Vous devez utiliser un serveur SQL Server hello toocomplete de connexion les étapes de cet article.
    > 
    > 

## <a name="run-sqoop-jobs"></a>Exécuter des tâches Sqoop
HDInsight peut exécuter des tâches Sqoop à l’aide de différentes méthodes. Utilisez hello suivant toodecide table quelle méthode vous consiste, puis suivez le lien hello pour une procédure pas à pas.

| **Utilisez-le** si vous souhaitez... | ... un interpréteur de commandes **interactif** | ... un traitement par **lots** | ...avec ce **système d’exploitation cluster** | ...depuis ce **système d’exploitation cluster** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-use-sqoop-mac-linux.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X ou Windows |
| [Kit de développement logiciel (SDK) .NET pour Hadoop](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |✔ |Linux ou Windows |Windows (pour l’instant) |
| [Azure PowerShell](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |✔ |Linux ou Windows |Windows |

## <a name="limitations"></a>Limites
* L’exportation en bloc - basés sur Linux avec un HDInsight, hello Sqoop connecteur utilisé tooexport données tooMicrosoft SQL Server ou base de données SQL Azure ne prend actuellement pas en charge les insertions en bloc.
* Le traitement par lot - Hdinsight basés sur Linux, lorsque vous utilisez hello `-batch` commutateur lorsque vous effectuez des insertions, Sqoop effectue plusieurs insertions au lieu de traitement par lot des opérations d’insertion hello.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris comment toouse Sqoop. toolearn, voir :

* [Utilisation de Hive avec HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig avec HDInsight](hdinsight-use-pig.md)
* [Utilisation d’Oozie avec HDInsight][hdinsight-use-oozie] : utilisez l’action Sqoop dans un workflow Oozie.
* [Analyser des données de retard de vol avec HDInsight][hdinsight-analyze-flight-data]: utiliser la ruche de vol de tooanalyze retarder des données et ensuite utiliser la base de données Sqoop tooexport données tooan SQL Azure.
* [Télécharger des données tooHDInsight][hdinsight-upload-data]: trouver d’autres méthodes pour le téléchargement des données tooHDInsight/Azure Blob storage.

## <a name="appendix-a---a-powershell-sample"></a>Annexe A - Exemple PowerShell
exemple de PowerShell Hello exécute hello comme suit :

1. Se connecter tooAzure.
2. Création d’un groupe de ressources Azure. Pour en savoir plus, voir [Utilisation d’Azure PowerShell avec le Gestionnaire de ressources Azure](../powershell-azure-resource-manager.md)
3. Création d’un serveur Base de données SQL Azure, d’une base de données SQL Azure et de deux tables. 
   
    Si vous utilisez SQL Server au lieu de cela, utilisez hello instructions toocreate hello tables suivantes :
   
        CREATE TABLE [dbo].[log4jlogs](
         [t1] [nvarchar](50),
         [t2] [nvarchar](50),
         [t3] [nvarchar](50),
         [t4] [nvarchar](50),
         [t5] [nvarchar](50),
         [t6] [nvarchar](50),
         [t7] [nvarchar](50))
   
        CREATE TABLE [dbo].[mobiledata](
         [clientid] [nvarchar](50),
         [querytime] [nvarchar](50),
         [market] [nvarchar](50),
         [deviceplatform] [nvarchar](50),
         [devicemake] [nvarchar](50),
         [devicemodel] [nvarchar](50),
         [state] [nvarchar](50),
         [country] [nvarchar](50),
         [querydwelltime] [float],
         [sessionid] [bigint],
         [sessionpagevieworder][bigint])
   
    tables et la base de données de hello plus simple façon tooexamine hello est toouse Visual Studio. serveur de base de données Hello et la base de données hello peuvent être examinées à l’aide de hello portail Azure.
4. Créez un cluster HDInsight.
   
    cluster de hello tooexamine, vous pouvez utiliser hello portail Azure ou Azure PowerShell.
5. Prétraiter le fichier de données source hello.
   
    Dans ce didacticiel, vous exportez un fichier de journal log4j (un fichier délimité) et une base de données SQL Azure de tooan table Hive. Hello fichier délimité est appelé */example/data/sample.log*. Plus haut dans le didacticiel de hello, vous avez vu quelques exemples des journaux de log4j. Dans le fichier journal de hello, il existe des lignes vides et certains toothese similaires de lignes :
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    Cela convient pour obtenir des exemples qui utilisent ces données, mais nous devons supprimer ces exceptions avant de pouvoir importer dans la base de données SQL Azure hello ou SQL Server. Exportation de Sqoop échoue s’il existe une chaîne vide ou une ligne comportant moins les éléments que nombre hello des champs définis dans la table de base de données SQL Azure hello. table de log4jlogs Hello comporte des champs de type chaîne 7.
   
    Cette procédure crée un nouveau fichier sur le cluster de hello : tutorials/usesqoop/data/sample.log. fichier de données modifiées tooexamine hello, vous pouvez utiliser hello portail Azure, un outil Explorateur de stockage Azure ou Azure PowerShell. [Prise en main HDInsight] [ hdinsight-get-started] possède un code d’exemple pour l’utilisation d’Azure PowerShell toodownload un fichier et afficher le contenu du fichier hello.
6. Exporter une base de données SQL Azure de données fichier toohello.
   
    fichier de source de Hello est tutorials/usesqoop/data/sample.log. table Hello où les données de salutation sont exporté toois appelé log4jlogs.
   
   > [!NOTE]
   > Autres que les informations de chaîne de connexion, les étapes hello dans cette section doivent fonctionner pour une base de données SQL Azure ou SQL Server. Ces étapes ont été testés à l’aide de hello configuration suivante :
   > 
   > * **Configuration de point-to-site de réseau virtuel Azure**: un réseau virtuel connecté hello HDInsight cluster tooa SQL Server dans un centre de données privé. Consultez [configurer un VPN de Point-to-Site dans le portail de gestion de hello](../vpn-gateway/vpn-gateway-point-to-site-create.md) pour plus d’informations.
   > * **Azure HDInsight 3.1**: pour plus d’informations sur la création d’un cluster sur un réseau virtuel, consultez la rubrique [Création de clusters Hadoop dans HDInsight à l’aide d’options personnalisées](hdinsight-hadoop-provision-linux-clusters.md) .
   > * **SQL Server 2014**: configurés de manière sécurisée l’authentification tooallow et en cours d’exécution hello VPN client configuration package tooconnect toohello des réseaux virtuels.
   > 
   > 
7. Exporter une base de données SQL Azure de toohello table Hive.
8. Importez le cluster HDInsight toohello hello mobiledata table.
   
    fichier de données modifiées tooexamine hello, vous pouvez utiliser hello portail Azure, un outil Explorateur de stockage Azure ou Azure PowerShell.  [Prise en main HDInsight] [ hdinsight-get-started] possède un code d’exemple sur l’utilisation d’Azure PowerShell toodownload un fichier et afficher le contenu du fichier hello.

### <a name="hello-powershell-sample"></a>Hello, exemple PowerShell
    # Prepare an Azure SQL database toobe used by hello Sqoop tutorial

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure Subscription ID>"

    $sqlDatabaseLogin = "<Enter a SQL Database Login name>" #SQL Database server login
    $sqlDatabasePassword = "<Enter a Password>"

    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<Enter a Password>"

    # used for creating Azure service names
    $nameToken = "<Enter an alias>" 
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

    # Used for creating tables and clustered indexes
    $cmdCreateLog4jTable = "CREATE TABLE [dbo].[log4jlogs](
        [t1] [nvarchar](50),
        [t2] [nvarchar](50),
        [t3] [nvarchar](50),
        [t4] [nvarchar](50),
        [t5] [nvarchar](50),
        [t6] [nvarchar](50),
        [t7] [nvarchar](50))"

    $cmdCreateLog4jClusteredIndex = "CREATE CLUSTERED INDEX log4jlogs_clustered_index on log4jlogs(t1)"

    $cmdCreateMobileTable = " CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder][bigint])"

    $cmdCreateMobileDataClusteredIndex = "CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)"

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
    catch{Login-AzureRmAccount}
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
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $credential `
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
    Write-Host "`nCreating an Azure SQL database ..." -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region - Create tables
    Write-Host "Creating hello log4jlogs table and hello mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create hello mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
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

    #region - pre-process hello source file

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from hello cluster toohello SQL database

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    $tableName_log4j = "log4jlogs"

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $exportDir_log4j = "/tutorials/usesqoop/data"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose
    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput

    #endregion

    #region - export a Hive table

    $tableName_mobile = "mobiledata"
    $exportDir_mobile = "/hive/warehouse/hivesampletable"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_mobile --export-dir $exportDir_mobile --fields-terminated-by \t -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion

    #region - import a database

    $targetDir_mobile = "/tutorials/usesqoop/importeddata/"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "import --connect $connectionString --table $tableName_mobile --target-dir $targetDir_mobile --fields-terminated-by \t --lines-terminated-by \n -m 1"

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion



[azure-management-portal]: https://portal.azure.com/

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database/sql-database-get-started.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
