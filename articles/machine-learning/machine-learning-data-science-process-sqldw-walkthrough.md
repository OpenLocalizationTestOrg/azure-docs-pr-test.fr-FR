---
title: "Hello processus de science des données équipe en action : à l’aide de l’entrepôt de données SQL | Documents Microsoft"
description: "Processus d’analyse avancé et technologie en action"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a>Hello processus de science des données équipe en action : à l’aide de l’entrepôt de données SQL
Dans ce didacticiel, nous vous guide dans la génération et le déploiement d’un modèle d’apprentissage automatique à l’aide de l’entrepôt de données SQL (SQL DW) pour un jeu de données disponible publiquement--hello [NYC Taxi allers-retours](http://www.andresmh.com/nyctaxitrips/) jeu de données. modèle de classification binaire Hello construit prédit ou non une info-bulle est payée pour un voyage, et les modèles de classification multiclasse et de régression sont également traités qui prédisent la distribution de hello pour les quantités de conseil hello payées.

procédure de Hello suit hello [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) flux de travail. Nous allons montrer comment toosetup un environnement de science des données, comment tooload hello des données dans l’entrepôt de données SQL et comment utiliser l’entrepôt de données SQL ou une toomodel de fonctionnalités notebooks bloc-notes tooexplore hello données et d’ingénierie à rebours. Ensuite, nous montrons comment toobuild et déployer un modèle avec Azure Machine Learning.

## <a name="dataset"></a>jeu de données Hello NYC Taxi allers-retours
Hello les données NYC Taxi voyage se compose d’environ 20 Go de fichiers CSV compressées (Go ~ 48 non compressé), l’enregistrement de plus de 173 millions hello et des boucles tarifs payé pour chaque sortie. Chaque enregistrement de voyage inclut les emplacements de collecte et de remise de hello et de, présentées de façon anonyme hack numéro de licence (du pilote), hello nombre de medallion (id unique de taxi). les données de salutation couvre toutes les boucles dans l’année hello 2013 et sont fournies dans hello suivant deux jeux de données pour chaque mois :

1. Hello **trip_data.csv** fichier contient les détails de voyage, telles que le nombre de personnes, points de collecte et cette chute, durée de voyage, longueur de voyage. Voici quelques exemples d’enregistrements :
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Hello **trip_fare.csv** fichier contient les détails des prix hello payé pour chaque sortie, comme type de paiement, montant de frais, surcharge et taxes, conseils et péage et montant total de hello payé. Voici quelques exemples d’enregistrements :
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Hello **clé unique** utilisé toojoin voyage\_données et voyage\_tarif est composé de hello suivant trois champs :

* medallion (médaillon),
* hack\_license (licence de taxi) et
* pickup\_datetime (date et heure d’embarquement).

## <a name="mltasks"></a>Traiter trois types de tâches de prédiction
Nous formuler à trois problèmes de prédiction selon hello *Conseil\_quantité* tooillustrate trois des types de tâches de modélisation :

1. **Classification binaire**: toopredict ou non un Conseil a été payé un voyage, c'est-à-dire un *Conseil\_quantité* qui est supérieur à $0 est un exemple positif, tandis qu’un *Conseil\_quantité* $ 0 est un exemple négatif.
2. **Classification multiclasse**: plage de hello toopredict d’info-bulle payé pour le voyage de hello. Nous allons diviser hello *Conseil\_quantité* dans les cinq conteneurs ou les classes :
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **Tâche de régression**: toopredict hello d’info-bulle montant d’un voyage.  

## <a name="setup"></a>Configuration d’environnement de science des données Azure hello pour analytique avancée
tooset de votre environnement pour la science des données Azure, procédez comme suit.

**Créez votre propre compte de stockage d’objets blob Azure**

* Lorsque vous configurez votre propre stockage d’objets blob Azure, choisissez un emplacement géographique pour le stockage d’objets blob Azure dans ou aussi près que possible trop**Amérique du Sud**, c'est-à-dire où est stockée les données NYC Taxi de hello. Hello données seront copiées à l’aide de AzCopy à partir du conteneur tooa conteneur de stockage d’objets blob publics hello dans votre propre compte de stockage. Hello rapprocher votre stockage d’objets blob Azure est tooSouth du centre des États-Unis, hello plus rapidement cette tâche (étape 4) se terminera.
* compte de votre propre stockage Azure toocreate hello suivez la procédure décrite à [comptes de stockage sur Azure](../storage/common/storage-create-storage-account.md). Être sûr de notes toomake sur les valeurs hello pour les informations d’identification de compte de stockage suivantes qu’ils sont reviendrez plus loin dans cette procédure pas à pas.
  
  * **Nom du compte de stockage**
  * **Clé du compte de stockage**
  * **Nom du conteneur** (sur lequel vous voulez hello toobe de données stockée dans hello stockage d’objets blob Azure)

**Approvisionnez votre instance Azure SQL DW.**
Suivre la documentation hello à [créer un entrepôt de données SQL](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision une instance de SQL Data Warehouse. Assurez-vous que vous notations sur hello suit les informations d’identification de l’entrepôt de données SQL qui seront utilisées dans les étapes ultérieures.

* **Nom du serveur** : <server Name>.database.windows.net
* **Nom SQL DW (base de données)**
* **Nom d’utilisateur**
* **Mot de passe**

**Installez Visual Studio et SQL Server Data Tools.** Pour connaître les instructions à suivre, consultez l’article [Installer Visual Studio 2015 et/ou SSDT pour SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).

**Se connecter tooyour entrepôt de données SQL Azure avec Visual Studio.** Pour obtenir des instructions, consultez les étapes 1 et 2 de [connecter tooAzure SQL Data Warehouse avec Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).

> [!NOTE]
> Exécution hello requête SQL sur la base de données hello que vous avez créé dans votre entrepôt de données SQL suivante (se connecter rubrique, au lieu de la requête de hello fournie à l’étape 3 de hello) trop**créer une clé principale**.
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

**Créez un espace de travail Azure Machine Learning dans votre abonnement Azure.** Pour connaître les instructions à suivre, consultez l’article [Création d’un espace de travail Azure Machine Learning](machine-learning-create-workspace.md).

## <a name="getdata"></a>Charger des données de hello dans l’entrepôt de données SQL
Ouvrez une console de commandes Windows PowerShell. Exécutez hello toodownload hello exemple fichiers de script SQL que nous partagent avec vous sur le répertoire local GitHub tooa que vous spécifiez avec le paramètre hello de commandes PowerShell *- DestDir*. Vous pouvez modifier la valeur hello du paramètre *- DestDir* tooany les répertoire local. Si *- DestDir* n’existe pas, il sera créé par hello script PowerShell.

> [!NOTE]
> Vous devrez peut-être trop**exécuter en tant qu’administrateur** lors de l’exécution hello suite du script PowerShell si votre *DestDir* tooit toocreate ou toowrite du privilège administrateur a besoin de répertoire.
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

Après l’exécution réussie, votre répertoire de travail actuel change également*- DestDir*. Vous devez pouvoir écran toosee comme ci-dessous :

![][19]

Dans votre *- DestDir*, exécutez hello script PowerShell en mode administrateur suivant :

    ./SQLDW_Data_Import.ps1

Lorsque hello script PowerShell s’exécute pour hello première fois, vous devez tooinput d’informations hello à partir de votre entrepôt de données SQL Azure et votre compte de stockage d’objets blob Azure. À l’issue de ce script PowerShell en cours d’exécution pour hello première fois, les informations d’identification hello vous entrée auront été écrites le fichier de configuration tooa SQLDW.conf dans le répertoire de travail présent hello. Hello futures l’exécution de ce fichier de script PowerShell a hello option tooread nécessaires tous les paramètres à partir de ce fichier de configuration. Si vous devez toochange certains paramètres, vous pouvez choisir tooinput paramètres hello sur l’écran hello à l’invite en supprimant ce fichier de configuration et de saisie de valeurs de paramètres hello à l’invite ou des valeurs de paramètre toochange hello en modifiant le fichier de SQLDW.conf hello dans votre *- DestDir* active.

> [!NOTE]
> Commande tooavoid schéma nom est en conflit avec ceux qui existent déjà dans votre entrepôt de données SQL Azure, lors de la lecture des paramètres directement à partir de fichiers de SQLDW.conf hello, un nombre aléatoire à 3 chiffres est ajouté toohello nom du schéma à partir du fichier de SQLDW.conf hello comme nom de schéma par défaut hello pour chaque exécution. Hello script PowerShell peut vous inviter à entrer un nom de schéma : nom de hello peut être spécifiée à la discrétion de l’utilisateur.
> 
> 

Cela **script PowerShell** fichier termine hello tâches suivantes :

* **Télécharge et installe AzCopy**, si AzCopy n’est pas déjà installé.
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* **Copie du compte de stockage de données tooyour blob privé** à partir de l’objet blob public de hello avec AzCopy
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* **Charge les données à l’aide de Polybase (en exécutant LoadDataToSQLDW.sql) tooyour Azure SQL DW** à partir de votre compte de stockage d’objets blob privé avec hello suivant les commandes.
  
  * Créer un schéma
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * Créer un fichier d’informations d’identification de niveau base de données
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * Créer une source de données externe pour un objet blob de stockage Azure
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * Créer un format de fichier externe pour un fichier csv. Données ne sont pas compressées et champs sont séparés par une barre verticale hello.
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * Créer des tables externes pour les prix et les courses correspondant au jeu de données NYC Taxi dans le stockage d’objets blob Azure.
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - Charger des données à partir des tables externes tooSQL de stockage d’objets blob Azure Data Warehouse

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - Créer un exemple de table de données (NYCTaxi_Sample) et insérez des données tooit à partir de la sélection des requêtes SQL portant sur les tables de voyage et tarif hello. (Certaines étapes de cette procédure pas à pas doit toouse cette table d’exemple).

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

emplacement géographique de Hello de vos comptes de stockage affecte le temps de chargement.

> [!NOTE]
> En fonction de l’emplacement géographique de hello de votre compte de stockage d’objets blob privé, hello les processus de copie des données à partir d’un compte de stockage privé tooyour objet blob public peuvent prend environ 15 minutes ou même plus, hello de processus et de chargement des données à partir de votre compte de stockage tooyour entrepôt de données SQL Azure peut prendre 20 minutes ou plus.  
> 
> 

Vous devez toodecide que faire si vous avez une source en double et les fichiers de destination.

> [!NOTE]
> Si toobe de fichiers .csv hello provenant de compte de stockage blob privé hello blob publics stockage tooyour déjà existe dans votre compte de stockage d’objets blob privé, AzCopy vous demande si vous souhaitez toooverwrite les. Si vous ne souhaitez pas toooverwrite leur, d’entrée  **n**  lorsque vous y êtes invité. Si vous souhaitez toooverwrite **tous les** , entrée **un** lorsque vous y êtes invité. Vous pouvez également entrer **y** toooverwrite .csv fichiers individuellement.
> 
> 

![Diagramme n°21][21]

Vous pouvez utiliser vos propres données. Si les données de votre ordinateur local dans votre application de la vie réelle, vous pouvez toujours utiliser AzCopy tooupload local données tooyour privé Azure stockage d’objets blob. Vous ne devez toochange hello **Source** emplacement, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, Bonjour commande AzCopy d’hello PowerShell script fichier toohello répertoire local qui contient vos données.

> [!TIP]
> Si vos données sont déjà dans votre stockage d’objets blob Azure privé dans votre application de la vie réelle, vous pouvez ignorer hello AzCopy étape Bonjour script PowerShell et le télécharger directement hello tooAzure de données SQL DW. Vous devrez supplémentaires modifie de hello script tootailor format toohello de vos données.
> 
> 

Ce script Powershell se connecte également Bonjour informations de l’entrepôt de données SQL Azure dans hello exploration exemple des fichiers de données SQLDW_Explorations.sql, SQLDW_Explorations.ipynb et SQLDW_Explorations_Scripts.py afin que ces trois fichiers sont prêt toobe essayé instantanément une fois hello script PowerShell est terminée.

À l’issue d’une exécution réussie, un écran semblable à ce qui suit s’affiche :

![][20]

## <a name="dbexplore"></a>Exploration des données et conception de fonctionnalités dans Azure SQL Data Warehouse
Dans cette section, nous effectuons une exploration des données et une génération de caractéristiques en exécutant des requêtes SQL directement dans Azure SQL DW à l’aide de **Visual Studio Data Tools**. Toutes les requêtes SQL utilisées dans cette section se trouvent dans le script d’exemple hello nommé *SQLDW_Explorations.sql*. Ce fichier a déjà été téléchargé tooyour répertoire local par le script PowerShell de hello. Vous pouvez également le récupérer à partir de [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql), Mais, au fichier hello dans GitHub n’a pas d’informations d’entrepôt de données SQL Azure hello branchées.

Se connecter tooyour entrepôt de données SQL Azure à l’aide de Visual Studio avec le nom de connexion SQL DW hello et le mot de passe et ouvrez hello **l’Explorateur d’objets SQL** base de données tooconfirm hello et les tables qui ont été importés. Récupérer hello *SQLDW_Explorations.sql* fichier.

> [!NOTE]
> tooopen un éditeur de requête Parallel Data Warehouse (PDW), utilisez hello **nouvelle requête** commande alors que votre PDW est sélectionné dans hello **l’Explorateur d’objets SQL**. éditeur de requête SQL standard Hello n’est pas pris en charge par PDW.
> 
> 

Voici le type hello de données exploration et la fonctionnalité des tâches de génération effectuée dans cette section :

* Explorer les distributions de données de quelques champs portant sur différentes périodes.
* Analyser la qualité des données des champs de longitude et de latitude hello.
* Générer des étiquettes de classification binaire et multiclasse selon hello **Conseil\_quantité**.
* Générer des fonctionnalités et calculer/comparer les distances des trajets.
* Joindre hello deux tables et extraire un échantillon aléatoire qui sera utilisé toobuild modèles.

### <a name="data-import-verification"></a>Vérification de l’importation des données
Ces requêtes fournissent une vérification rapide du nombre de hello de lignes et colonnes Bonjour importer des tables remplis précédemment à l’aide de parallèle en bloc de Polybase,

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

**Sortie :** vous devez obtenir 173 179 759 lignes et 14 colonnes.

### <a name="exploration-trip-distribution-by-medallion"></a>Exploration : distribution des courses par médaillon
Cet exemple de requête identifie des medallions hello (numéros taxi) qui s’est terminée de plus de 100 allers-retours au sein d’une période de temps. requête de Hello tireront parti d’accès à la table hello partitionnée, car il est conditionnée par le schéma de partition hello de **collecte\_datetime**. Interrogation du jeu de données complet hello rendent également utiliser de table partitionnée de hello et/ou d’analyse d’index.

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

**Sortie :** hello de requêtes doit retourner une table avec des lignes en spécifiant le medallions hello 13,369 (taxi) et de hello nombre de voyage s’est terminée par ces derniers en 2013. Hello dernière colonne contient les nombre hello de hello allers-retours s’est terminée.

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Exploration : distribution des courses par médaillon et par licence de taxi
Cet exemple identifie le medallions hello (numéros taxi) et hack_license des chiffres (pilotes) qui s’est terminée plus de 100 boucles dans un laps de temps spécifié.

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

**Sortie :** requête de hello doit retourner une table avec des 13,369 lignes spécifiant hello 13,369 voiture/pilote ID qui ont été effectuées plus que 100 allers-retours dans 2013. Hello dernière colonne contient les nombre hello de hello allers-retours s’est terminée.

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Évaluation de la qualité des données : Vérifier les enregistrements indiquant une longitude et/ou une latitude incorrectes
Cet exemple examine si un des champs de longitude et/ou latitude hello contenir une valeur non valide (les degrés en radians doivent être comprise entre -90 et 90), ou avoir (0, 0) coordonnées.

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

**Sortie :** requête de hello retourne 837,467 boucles qui ont des champs de longitude ou de latitude non valides.

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Exploration : Distribution des courses avec et sans pourboire
Cet exemple recherche le nombre de hello d’allers-retours qui ont été déposés contre le nombre de hello qui ont été déposés pas dans un laps de temps spécifié (ou dans hello jeu de données complet si couvrant an hello comme il est défini ici). Cette distribution reflète hello étiquette binaire distribution toobe utilisée ultérieurement pour la modélisation de classification binaire.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

**Sortie :** hello requête doit suivant de retour hello Conseil fréquences pour l’année hello incliné 2013 : 90,447,622 et 82,264,709 a n’est pas.

### <a name="exploration-tip-classrange-distribution"></a>Exploration : Distribution des classes/fourchettes de pourboires
Cet exemple calcule la distribution hello des plages de Conseil dans un délai donné période (ou dans hello jeu de données complet si couvrant an hello). Il s’agit de distribution hello des classes d’étiquette hello qui sera utilisée ultérieurement pour la modélisation de classification multiclasse.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

**Output:**

| tip_class | tip_freq |
| --- | --- |
| 1 |82230915 |
| 2 |6198803 |
| 3 |1932223 |
| 0 |82264625 |
| 4 |85765 |

### <a name="exploration-compute-and-compare-trip-distance"></a>Exploration : Calculer et comparer les distances des courses
L’exemple suivant convertit la longitude de collecte et de remise hello et latitude tooSQL geography pointe, calcule la distance de voyage hello à l’aide de la différence de points SQL geography et retourne un échantillon aléatoire de résultats hello pour la comparaison. exemple de Hello limite les résultats de hello toovalid coordonne uniquement à l’aide de la requête d’évaluation de la qualité des données d’hello évoqué précédemment.

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a>Conception de fonctionnalités à l’aide de fonctions SQL
Les fonctions SQL peuvent parfois s’avérer efficaces pour la conception des fonctionnalités. Dans cette procédure pas à pas, nous avons défini une SQL fonction toocalculate hello distance directe entre les emplacements de collecte et de cette chute de hello. Vous pouvez exécuter hello suivant des scripts SQL dans **outils de données Visual Studio**.

Voici le script SQL hello qui définit la fonction de distance hello.

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

Voici un exemple toocall cette fonctionnalités toogenerate de fonction dans votre requête SQL :

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

**Sortie :** cette requête génère une table (avec des 2,803,538 lignes) avec la collecte et cette chute de latitude et de dirigent les distances en miles longitudes et hello correspondant. Voici les résultats de hello pour les 3 premiers lignes :

|  | pickup_latitude | pickup_longitude | dropoff_latitude | dropoff_longitude | DirectDistance |
| --- | --- | --- | --- | --- | --- |
| 1 |40,731804 |-74,001083 |40,736622 |-73,988953 |0,7169601222 |
| 2 |40,715794 |-74,010635 |40,725338 |-74,00399 |0,7448343721 |
| 3 |40.761456 |-73.999886 |40.766544 |-73.988228 |0,7037227967 |

### <a name="prepare-data-for-model-building"></a>Préparer les données pour la création de modèles
hello de jointures de requête suivant de Hello **nyctaxi\_voyage** et **nyctaxi\_tarif** des tables, génère une étiquette de classification binaire **incliné**, un étiquette de classification multiclasse **Conseil\_classe**et extrait un échantillon de jeu de données joint hello complète. échantillonnage de Hello est effectuée par la récupération d’un sous-ensemble des allers-retours hello selon l’heure de collecte.  Cette requête peut être copiée, puis collée directement dans hello [Azure Machine Learning Studio](https://studio.azureml.net) [importer des données] [ import-data] module pour l’ingestion de données directement à partir de l’instance de base de données SQL hello dans Azure. requête de Hello exclut les enregistrements avec incorrect (0, 0) coordonnées.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

Lorsque vous êtes prêt tooproceed tooAzure Machine Learning, vous pouvez :  

1. Enregistrer hello final SQL requête tooextract et exemple hello données et copier-coller hello requête directement dans un [importer des données] [ import-data] module dans Azure Machine Learning, ou
2. Conserver hello échantillonnée et données ingénieries que vous prévoyez toouse pour un nouvel entrepôt de données SQL de création de modèles de table et utilisent la nouvelle table de hello Bonjour [importer des données] [ import-data] module dans Azure Machine Learning. Hello script PowerShell à l’étape précédente a fait cela pour vous. Vous pouvez lire directement à partir de cette table dans le module d’importation de données hello.

## <a name="ipnb"></a>Exploration des données et conception de fonctionnalités dans IPython Notebook
Dans cette section, nous allons effectuer l’exploration de données et de génération de fonctionnalité à l’aide de deux Python et des requêtes SQL sur hello SQL DW créé précédemment. Un bloc-notes de notebooks exemple nommé **SQLDW_Explorations.ipynb** et un fichier de script Python **SQLDW_Explorations_Scripts.py** ont été téléchargés tooyour les répertoire local. Ils sont également disponibles sur [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW). Ces deux fichiers sont identiques dans les scripts Python. fichier de script Python Hello est fourni tooyou au cas où vous ne disposez pas d’un serveur de notebooks bloc-notes. Ces deux exemples de fichier Python sont conçus sous **Python 2.7**.

Hello les informations d’entrepôt de données SQL Azure nécessaires dans l’exemple hello notebooks bloc-notes et hello Python ordinateur local de script fichier tooyour téléchargé a été branché par script PowerShell de hello précédemment. Elles peuvent être exécutées sans aucune modification.

Si vous avez déjà configuré un espace de travail AzureML, vous pouvez directement télécharger l’exemple hello service de AzureML notebooks bloc-notes toohello notebooks portable et commencer à l’exécuter. Voici hello étapes tooupload tooAzureML service des notebooks bloc-notes :

1. Ouvrez une session dans l’espace de travail tooyour AzureML et cliquez sur « Studio » en haut de hello, cliquez sur « Ordinateurs portables » sur le côté gauche de hello de page web de hello.
   
    ![Diagramme n°22][22]
2. Cliquez sur « Nouveau » dans le coin inférieur gauche de hello de hello web page, puis sélectionnez « Python 2 ». Ensuite, un ordinateur portable toohello de nom et cliquez sur hello coche toocreate hello vierge notebooks bloc-notes.
   
    ![Diagramme n°23][23]
3. Cliquez sur symboles de « Notebook » hello sur le coin supérieur gauche de hello Hello notebooks bloc-notes.
   
    ![Diagramme n°24][24]
4. Faites glisser et déposez hello exemple notebooks bloc-notes toohello **arborescence** page de votre service de AzureML notebooks bloc-notes, puis cliquez sur **télécharger**. Ensuite, l’exemple hello notebooks bloc-notes sera téléchargé toohello service de AzureML notebooks bloc-notes.
   
    ![Diagramme n°25][25]

Bonjour toorun de commande exemple notebooks bloc-notes ou hello du fichier de script Python, hello Python packages suivants sont nécessaires. Si vous utilisez le service de AzureML notebooks bloc-notes hello, ces packages ont été préinstallés.

    - pandas
    - numpy
    - matplotlib
    - pyodbc
    - PyTables

Hello séquence recommandée lors de la génération des solutions analytiques avancées sur AzureML avec des données volumineuses est suivant de hello :

* Lire dans un petit échantillon de données de salutation dans une trame de données en mémoire.
* Effectuer des visualisations et à l’aide des explorations hello données échantillonnées.
* Faites l’expérience de l’ingénierie de fonctionnalité à l’aide de hello exemples de données.
* Pour l’exploration de données plus volumineuse, l’ingénierie de fonctionnalité et de manipulation de données utiliser Python tooissue SQL requêtes directement sur hello SQL DW.
* Décidez hello exemple taille toobe approprié pour la construction d’un modèle Azure Machine Learning.

Hello trouverez ci-dessous quelques exemples ingénierie de fonctionnalité, l’exploration de données et visualisation des données. Vous trouverez plus d’explorations de données dans l’exemple hello notebooks bloc-notes et fichier de script Python exemple hello.

### <a name="initialize-database-credentials"></a>Initialiser les informations d’identification de la base de données
Initialiser vos paramètres de connexion de base de données Bonjour suivant variables :

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a>Créer une connexion à la base de données
Voici la chaîne de connexion hello qui crée la base de données toohello hello connexion.

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Afficher le nombre de lignes et de colonnes de la table <nyctaxi_trip>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Nombre total de lignes = 173 179 759  
* Nombre total de colonnes = 14

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a>Afficher le nombre de lignes et de colonnes de la table <nyctaxi_fare>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Nombre total de lignes = 173 179 759  
* Nombre total de colonnes = 11

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a>Lecture dans un échantillon de données de petite taille à partir de hello de base de données de l’entrepôt de données SQL
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

Table d’exemple hello temps tooread est 14.096495 secondes.  
Nombre de lignes et de colonnes récupérées = (1000, 21)

### <a name="descriptive-statistics"></a>Statistiques descriptives
Vous êtes maintenant données hello échantillonnée de tooexplore prêt. Nous allons commencer par envisager des statistiques descriptives pour hello **voyage\_distance** (ou tous les autres champs que vous choisissez toospecify).

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a>Visualisation : Exemple de diagramme à surfaces
Ensuite, nous allons examiner les surfaces hello pour hello voyage distance toovisualize hello quantiles.

    df1.boxplot(column='trip_distance',return_type='dict')

![Diagramme #1][1]

### <a name="visualization-distribution-plot-example"></a>Visualisation : Exemple de diagramme de distribution
Les tracés visualiser la distribution de hello et un histogramme pour hello échantillonnées distances de voyage.

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Diagramme #2][2]

### <a name="visualization-bar-and-line-plots"></a>Visualisation : Diagrammes en bâtons et linéaires
Dans cet exemple, nous bin distance de voyage hello dans cinq compartiments et visualiser hello placement des résultats.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

Nous pouvons tracer hello au-dessus de distribution d’emplacement dans une barre ou ligne de traçage avec :

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Diagramme #3][3]

and

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Diagramme #4][4]

### <a name="visualization-scatterplot-examples"></a>Visualisation : Exemples de nuage de points
Nous allons montrer nuage entre **voyage\_temps\_dans\_secondes** et **voyage\_distance** toosee s’il existe une corrélation

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Diagramme #6][6]

De même, nous pouvons vérifier relation hello entre **taux\_code** et **voyage\_distance**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Diagramme #8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a>Exploration des données échantillonnées à l’aide de requêtes SQL dans IPython Notebook
Dans cette section, nous explorons les distributions de données à l’aide de données hello échantillonnée qui sont conservées dans hello nouvelle table créée précédemment. Notez que des explorations similaire peuvent être effectuées à l’aide de tables d’origine de hello.

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a>Exploration : Nombre de rapports de lignes et colonnes Bonjour échantillonnées table
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a>Exploration : Distribution avec et sans pourboire
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a>Exploration : Distribution des classes de pourboires
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a>Exploration : Tracer la distribution de conseil hello par classe
    tip_class_dist['tip_freq'].plot(kind='bar')

![Diagramme n°26][26]

#### <a name="exploration-daily-distribution-of-trips"></a>Exploration : distribution quotidienne des courses
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Exploration : distribution des courses par médaillon
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a>Exploration : Distribution des courses par médaillon et par licence de taxi
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a>Exploration : Distribution des durées de course
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a>Exploration : Distribution des distances de course
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a>Exploration : Distribution des types de paiement
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Vérifiez la forme finale de la table de fonctionnalités hello de hello
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <a name="mlmodel"></a>Créer des modèles dans Azure Machine Learning
Vous voilà prêt tooproceed toomodel génération et déploiement de modèle dans [Azure Machine Learning](https://studio.azureml.net). les données de salutation sont prêt toobe utilisé dans un des problèmes de prédiction hello identifiées précédemment, à savoir :

1. **Classification binaire**: toopredict ou non un Conseil a été payé un voyage.
2. **Classification multiclasse**: plage de hello toopredict d’info-bulle payé, en fonction de toohello classes précédemment définies.
3. **Tâche de régression**: toopredict hello d’info-bulle montant d’un voyage.  

toobegin hello exercice de modélisation, connectez-vous à tooyour **Azure Machine Learning** espace de travail. Si vous n’avez pas encore créé d’espace de travail d’apprentissage automatique, consultez l’article [Créer un espace de travail Azure Machine Learning](machine-learning-create-workspace.md).

1. tooget main d’Azure Machine Learning, consultez [Nouveautés d’Azure Machine Learning Studio ?](machine-learning-what-is-ml-studio.md)
2. Connectez-vous trop[Azure Machine Learning Studio](https://studio.azureml.net).
3. page d’accueil Studio Hello fournit une mine d’informations, des vidéos, didacticiels, des liens toohello référence des Modules et autres ressources. Pour plus d’informations sur Azure Machine Learning, consultez hello [centre de Documentation Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).

Une expérience de formation standard se compose de hello comme suit :

1. Création d’une expérience à l’aide du bouton **+NOUVEAU** .
2. Permet d’obtenir des données de hello dans Azure ML.
3. Prétraiter, transformer et manipuler des données de hello en fonction des besoins.
4. Génération des fonctionnalités requises.
5. Fractionner les données de hello en jeux de données d’apprentissage/validation/test (ou avoir des jeux de données distincts pour chaque).
6. Sélectionnez un ou plusieurs algorithmes d’apprentissage en fonction de hello toosolve de problème d’apprentissage. Exemples : classification binaire, classification multiclasse, régression.
7. L’apprentissage d’un ou plusieurs modèles à l’aide du jeu de données d’apprentissage hello.
8. Un score de jeu de données de validation hello à l’aide de modèles formés de hello.
9. Évaluer hello ou les modèles toocompute hello mesures pour hello problème d’apprentissage.
10. Réglage de l’ou les modèles hello et sélectionnez hello meilleur modèle toodeploy.

Dans cet exercice, nous avons déjà exploré et conçu données hello SQL Data Warehouse et décidé sur tooingest de taille d’échantillon hello dans Azure ML. Voici hello procédure toobuild une ou plusieurs des modèles de prévision hello :

1. Obtenir des données de hello dans Azure ML à l’aide de hello [importer des données] [ import-data] module, disponible dans hello **données d’entrée et sortie** section. Pour plus d’informations, consultez hello [importer des données] [ import-data] page de référence de module.
   
    ![Importer les données Azure ML][17]
2. Sélectionnez **base de données SQL Azure** comme hello **source de données** Bonjour **propriétés** Panneau de configuration.
3. Entrez le nom DNS de base de données hello Bonjour **nom du serveur de base de données** champ. Format : `tcp:<your_virtual_machine_DNS_name>,1433`
4. Entrez hello **nom de la base de données** dans le champ correspondant de hello.
5. Entrez hello *nom d’utilisateur SQL* Bonjour **le nom de compte d’utilisateur Server**et hello *mot de passe* Bonjour **mot de passe utilisateur Server**.
6. Vérifiez hello **accepter n’importe quel certificat du serveur** option.
7. Bonjour **requête de base de données** modifier la zone de texte, collez la requête hello extrait hello nécessaire (y compris les champs calculés tels que des étiquettes de hello) des champs de base de données et le bas exemples de taille d’échantillon hello données toohello souhaité.

Un exemple d’une expérience de classification binaire la lecture des données directement à partir de la base de données SQL Data Warehouse hello est dans la figure ci-dessous hello (n’oubliez pas de la table de hello tooreplace les noms nyctaxi_trip et nyctaxi_fare par schéma de hello hello et nom des noms de table utilisé dans votre procédure pas à pas). Vous pouvez créer des expériences similaires pour les problèmes de classification multiclasse et de régression.

![Formation Azure Machine Learning][10]

> [!IMPORTANT]
> Bonjour, extraction de données de modélisation et de l’échantillonnage des exemples de requêtes fournis dans les sections précédentes, **toutes les étiquettes pour les exercices de modélisation hello trois sont inclus dans la requête de hello**. Une étape importante (obligatoire) dans chacun des exercices de modélisation de hello est trop**exclure** hello étiquettes inutiles pour hello autres deux problèmes, ainsi que tout autre **cible fuites**. Par exemple, lors de l’utilisation de classification binaire, utilisez les étiquette hello **incliné** et exclure les champs hello **Conseil\_classe**, **Conseil\_quantité**, et **total\_quantité**. Hello dernier paiement des fuites de cible, car elles impliquent l’info-bulle hello.
> 
> tooexclude toutes les colonnes inutiles ou les fuites de cible, vous pouvez utiliser hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module ou hello [modifier les métadonnées] [ edit-metadata]. Pour plus d’informations, consultez les pages de référence [Sélectionner des colonnes dans le jeu de données][select-columns] et [Modifier les métadonnées][edit-metadata].
> 
> 

## <a name="mldeploy"></a>Déployer des modèles dans Azure Machine Learning
Lorsque votre modèle est prêt, vous pouvez la déployer facilement en tant qu’un service web directement à partir de l’expérience de hello. Pour plus d’informations sur le déploiement de services web Azure Machine Learning, consultez [Déployer un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

toodeploy un nouveau service web, vous devez :

1. créer une expérience de notation ;
2. Déployer un service web de hello.

toocreate une expérience d’un score d’un **terminé** expérience d’apprentissage, cliquez sur **créer une expérience de score** dans la barre d’action hello inférieur.

![Notation Azure][18]

Azure Machine Learning tentera toocreate expérience de score basée sur les composants hello d’expérience de formation hello. Il va notamment :

1. Enregistrer le modèle formé de hello et supprimer des modules de formation du modèle hello.
2. Identifier un opérateur logique **port d’entrée** toorepresent hello attendue de schéma de données d’entrée.
3. Identifier un opérateur logique **port de sortie** schéma de sortie de service toorepresent hello web attendu.

Lors de la création de hello expérience de score, examiner et rendre l’ajuster en fonction des besoins. Un ajustement standard est tooreplace hello jeu de données d’entrée et/ou de la requête avec l’une qui exclut les champs d’étiquette, car il ne sera pas disponibles lorsque le service de hello est appelé. Il est également qu'une taille de hello tooreduce bonnes pratiques de hello d’entrée tooa de jeu de données et/ou des requêtes peu d’enregistrements, juste assez schéma d’entrée de tooindicate hello. Pour le port de sortie hello, il est commun tooexclude entrées tous les champs et uniquement inclure hello **Scored Labels** et **des probabilités notées** Bonjour de sortie à l’aide de hello [sélectionner les colonnes dans le jeu de données ] [ select-columns] module.

Un exemple d’expérience de score est fourni dans la figure ci-dessous hello. Quand vous êtes prêt toodeploy, cliquez sur hello **publier le SERVICE WEB** bouton dans la barre d’action hello inférieur.

![Publication Azure Machine Learning][11]

## <a name="summary"></a>Résumé
toorecap ce que nous avons effectué dans ce didacticiel de la procédure pas à pas, vous avez créé un environnement de science des données Azure, travaillé avec un jeu de données publique volumineux, il guidant hello processus d’équipe données scientifiques, tous les moyen hello de formation de toomodel d’acquisition de données, puis toohello le déploiement d’un service web Azure Machine Learning.

### <a name="license-information"></a>Informations de licence
Cet exemple de procédure et accompagne des scripts et des notebooks notebook(s) sont partagées par Microsoft sous licence du MIT hello. Vérifiez fichier hello le répertoire hello hello exemple de code sur GitHub pour plus d’informations.

## <a name="references"></a>Références
•    [Page de téléchargement des jeux de données NYC Taxi Trips par Andrés Monroy (en anglais)](http://www.andresmh.com/nyctaxitrips/)  
•    [Page de partage des données relatives aux courses en taxi new-yorkais par Chris Whong (en anglais)](http://chriswhong.com/open-data/foil_nyc_taxi/)   
•    [Page de recherche et de statistiques de la Commission des services de taxis et de limousines de la ville de New York (en anglais)](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
