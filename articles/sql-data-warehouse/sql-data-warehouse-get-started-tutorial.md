---
title: aaaAzure SQL Data Warehouse - commencer didacticiel | Documents Microsoft
description: "Ce didacticiel vous apprend comment tooprovision et charger les données dans l’entrepôt de données SQL Azure. Vous allez également principes hello sur la mise à l’échelle ou d’interruption et de paramétrage."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a>Prise en main de SQL Data Warehouse

Ce didacticiel montre comment tooprovision et charger les données dans l’entrepôt de données SQL Azure. Vous allez également principes hello sur la mise à l’échelle ou d’interruption et de paramétrage. Lorsque vous avez terminé, prêt tooquery et vous explorez votre entrepôt de données.

**Estimation du temps toocomplete :** il s’agit d’un didacticiel de bout en bout avec le code d’exemple qui prend environ 30 minutes toocomplete une fois que vous avez rempli les conditions préalables de hello. 

## <a name="prerequisites"></a>Composants requis

didacticiel de Hello suppose que vous êtes familiarisé avec les concepts de base de l’entrepôt de données SQL. Si vous avez besoin d’une introduction, consultez [En quoi consiste Azure SQL Data Warehouse ?](sql-data-warehouse-overview-what-is.md) 

### <a name="sign-up-for-microsoft-azure"></a>S'inscrire à Microsoft Azure
Si vous n’avez pas déjà un compte Microsoft Azure, vous devez toosign pour un toouse ce service. Si vous avez déjà un compte, vous pouvez ignorer cette étape. 

1. Naviguer entre les pages de compte toohello [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)
2. Créer un compte Azure gratuit, ou achetez-en un.
3. Suivez les instructions de hello

### <a name="install-appropriate-sql-client-drivers-and-tools"></a>Installer les pilotes du client SQL et les outils appropriés

La plupart des outils clients SQL peuvent se connecter tooSQL l’entrepôt de données à l’aide de JDBC, ODBC ou ADO.NET. En raison de toohello grand nombre de fonctionnalités de T-SQL qui prend en charge de l’entrepôt de données SQL, certaines applications clientes ne sont pas entièrement compatibles avec l’entrepôt de données SQL.

Si vous exécutez un système d’exploitation Windows, nous vous recommandons de recourir à [Visual Studio] ou à [SQL Server Management Studio].

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a>Créer un entrepôt de données SQL

SQL Data Warehouse est un type spécial de base de données conçu pour le traitement massivement parallèle. base de données Hello est distribuée sur plusieurs nœuds et traite les requêtes en parallèle. Entrepôt de données SQL a un nœud de contrôle qui orchestre les activités de tous les nœuds hello hello. nœuds Hello eux-mêmes utilisent toomanage de la base de données SQL à vos données.  

> [!NOTE]
> La création d’un entrepôt de données SQL Data Warehouse peut donner lieu à un nouveau service facturable.  Pour en savoir plus, voir [SQL Data Warehouse - Tarification](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).
>

### <a name="create-a-data-warehouse"></a>Créer un entrepôt de données

1. L’authentification à hello [portail Azure](https://portal.azure.com).
2. Cliquez sur **Nouveau** > **Bases de données** > **SQL Data Warehouse**.

    ![Nouveau panneau](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png)![Choisir DW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)

3. Renseignez les détails relatifs au déploiement.

    **Nom de la base de données** : choisissez le nom de votre choix. Si vous avez plusieurs entrepôts de données, nous vous recommandons de vos noms d’incluent des détails tels que la région de hello, environnement, par exemple *mydw-westus-1-test*.

    **Abonnement** : votre abonnement Azure.

    **Groupe de ressources** : créez un groupe de ressources ou utilisez-en un existant.
    > [!NOTE]
    > Les groupes de ressources sont utiles pour administrer les ressources (définition de la portée du contrôle d’accès et déploiement basé sur des modèles, par exemple). Découvrez [ici](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) plus d’informations sur les groupes de ressources et meilleures pratiques Azure.

    **Source** : base de données vide.

    **Serveur**: serveur hello sélectionnez créé dans [conditions préalables].

    **Classement**: laissez le classement par défaut de hello SQL_Latin1_General_CP1_CI_AS.

    **Sélectionnez performance**: nous vous recommandons de commencer avec 400DWU standard de hello.

4. Choisissez **code confidentiel toodashboard** ![tooDashboard du code confidentiel](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)

5. Confortablement et attendez que votre toodeploy de l’entrepôt de données ! Il est normal pour cette tootake processus plusieurs minutes. portail de Hello vous avertit lorsque votre entrepôt de données est prêt toouse. 

## <a name="connect-toosql-data-warehouse"></a>Se connecter tooSQL l’entrepôt de données

Ce didacticiel utilise l’entrepôt de données SQL Server Management Studio (SSMS) tooconnect toohello. Vous pouvez vous connecter tooSQL l’entrepôt de données via ces connecteurs pris en charge : ADO.NET, JDBC, ODBC et PHP. N’oubliez pas que les fonctionnalités peuvent être limitées si les outils ne sont pas pris en charge par Microsoft.


### <a name="get-connection-information"></a>Obtenir des informations de connexion

tooconnect tooyour l’entrepôt de données, vous devez tooconnect via hello logique SQL server vous avez créé dans [conditions préalables].

1. Sélectionnez votre entrepôt de données à partir du tableau de bord hello ou la recherche de vos ressources.

    ![Tableau de bord SQL Data Warehouse](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. Rechercher le nom complet de hello pour hello logique SQL server.

    ![Sélection du nom du serveur](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. Ouvrez SSMS et utiliser objet explorer tooconnect toothis serveur utilisant hello informations d’identification administrateur serveur vous avez créé dans [conditions préalables]

    ![Connexion avec SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

Si tout se passe correctement, vous devez maintenant être connecté tooyour logique SQL server. Étant donné que vous connecté comme administrateur du serveur de hello, vous pouvez vous connecter tooany de base de données hébergée par serveur hello, y compris la base de données master hello. 

Compte d’administrateur qu’un seul serveur est et il a hello la plupart des privilèges d’un utilisateur. Veillez à ne pas tooallow trop d’utilisateurs dans votre mot de passe d’administrateur organisation tooknow hello. 

Vous pouvez également posséder un compte d’administrateur Azure Active Directory. Nous ne fournissent pas ici les détails hello. Si vous souhaitez toolearn plus en détail à l’aide de l’authentification Azure Active Directory, voir [d’authentification Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

Nous étudions maintenant la création d’utilisateurs et d’information de connexion supplémentaires.


## <a name="create-a-database-user"></a>Créer un utilisateur de base de données

Dans cette étape, vous créez un tooaccess de compte d’utilisateur votre entrepôt de données. Nous vous montrons également comment toogive ce toorun de capacité hello utilisateur interroge avec une grande quantité de mémoire et des ressources processeur.

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a>Remarques sur les classes de ressources pour allouer les ressources tooqueries

- tookeep vos données en sécurité, n’utilisez pas des requêtes hello server administration toorun sur vos bases de données de production. Il a hello de la plupart des privilèges d’un utilisateur et l’utiliser tooperform opérations sur les données utilisateur expose vos données à un risque. En outre, étant donné que l’administrateur du serveur hello vise tooperform les opérations de gestion, il exécute des opérations avec qu’une petite allocation de mémoire et des ressources processeur. 

- SQL Data Warehouse utilise des rôles de base de données prédéfinis, appelées classes de ressources, tooallocate différentes quantités de mémoire, les ressources du processeur et toousers des emplacements d’accès concurrentiel. Chaque utilisateur peut appartenir la classe de ressource de petite, moyenne, grande ou très grand tooa. Hello classe de ressource de l’utilisateur détermine hello ressources hello utilisateur toorun requêtes et opérations de chargement.

- Pour la compression des données optimale, hello est nécessaire tooload de grande taille ou des allocations de ressources très volumineux. Découvrez plus d’informations sur les classes de ressource [ici](./sql-data-warehouse-develop-concurrency.md#resource-classes) :

### <a name="create-an-account-that-can-control-a-database"></a>Créer un compte pouvant contrôler une base de données

Étant donné que vous êtes actuellement connecté comme administrateur du serveur de hello vous disposez des autorisations toocreate connexions et les utilisateurs.

1. À l’aide de SSMS ou d’un autre client de requête, ouvrez une nouvelle requête pour **master**.

    ![Nouvelle requête sur Master](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Nouvelle requête sur Master1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. Dans la fenêtre de requête hello, exécutez cette toocreate de commande T-SQL, une connexion nommée MedRCLogin et un utilisateur nommé LoadingUser. Cette connexion peut se connecter toohello logique SQL server.

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. Maintenant interrogation hello *base de données SQL Data Warehouse*, créez un utilisateur de base de données en fonction hello de connexion que vous avez créé tooaccess et effectuer des opérations sur la base de données hello.

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. Donnez à hello de base de données utilisateur contrôle autorisations toohello base de données appelée NYT. 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > Si le nom de votre base de données comporte des traits d’union, être toowrap que dans les crochets ! 
    >

### <a name="give-hello-user-medium-resource-allocations"></a>Donner des allocations de hello utilisateur moyenne des ressources

1. Exécutez cette toomake de commande T-SQL informatique, un membre de classe de ressource moyennes hello, qui est appelé mediumrc. 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > Cliquez sur [ici](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn plus d’informations sur les classes d’accès concurrentiel et de ressources ! 
    >

2. Connecter le serveur logique de toohello avec nouvelles informations d’identification de hello

    ![Connexion avec le nouveau compte de connexion](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a>Charger des données à partir d’objets Blob Microsoft Azure Storage

Vous êtes maintenant les données tooload prêt dans votre entrepôt de données. Cette étape vous montre comment les données de fichier cab tooload New York City taxi à partir d’un stockage Azure public blob. 

- Une méthode courante données tooload dans SQL Data Warehouse sont toofirst déplacer le stockage d’objets blob hello données tooAzure et puis son chargement dans votre entrepôt de données. toomake il toounderstand plus facilement comment tooload, nous disposons de New York taxi cab données déjà hébergées dans un objet blob de stockage Azure publique. 

- Pour référence ultérieure, toolearn comment tooget votre tooAzure de données d’objets blob de stockage ou tooload il directement à partir de votre source dans l’entrepôt de données SQL, consultez hello [vue d’ensemble de chargement](sql-data-warehouse-overview-load.md).


### <a name="define-external-data"></a>Définir des données externes

1. Créez une clé principale. Vous ne devez toocreate une clé principale une fois par base de données. 

    ```sql
    CREATE MASTER KEY;
    ```

2. Définir emplacement hello hello Azure blob qui contient les données de fichier cab taxi hello.  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. Définir des formats de fichier externe hello

    Hello ```CREATE EXTERNAL FILE FORMAT``` commande est utilisée toospecify le format des fichiers qui contiennent des données externes hello. Ils contiennent du texte séparé par un ou plusieurs caractères, appelés délimiteurs. À des fins de démonstration, les données de fichier cab taxi hello sont stockées à la fois des données et les données gzip compressées.

    Exécuter ces commandes T-SQL de toodefine deux formats : non compressés et compressé.

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  Créez un schéma pour le format de fichier externe. 

    ```sql
    CREATE SCHEMA ext;
    ```
5. Créer des tables externes hello. Ces tables référencent les données stockées dans le stockage d’objets blob Azure. Exécutez hello suivant toocreate de commandes T-SQL de plusieurs tables externes que toohello point tous les objets blob Azure nous défini précédemment dans notre source de données externe.

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-hello-data-from-azure-blob-storage"></a>Importer les données de salutation depuis le stockage blob Azure.

SQL Data Warehouse prend en charge une instruction clé appelée CREATE TABLE AS SELECT (CTAS). Cette instruction crée une nouvelle table basée sur les résultats d’une instruction select hello. Hello nouvelle table a hello les mêmes colonnes et types de données comme résultats hello Hello select (instruction).  Il s’agit d’une données tooimport de manière élégante à partir du stockage d’objets blob Azure dans SQL Data Warehouse.

1. Exécutez ce script tooimport vos données.

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. Affichez vos données à mesure qu’elles sont chargées.

   Vous chargez plusieurs gigaoctets de données et les compressez au sein d’index de cluster columnstore hautes performances. Exécutez hello suivant la requête qui utilise un état de hello gestion dynamique (DMV) de vues tooshow de charge de hello. Après le démarrage de la requête de hello, saisissez un café et une tasse SQL Data Warehouse Contrairement à certaines tâches.
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. Affichez toutes les requêtes du système.

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. Vous pouvez constater que vos données sont efficacement chargées dans votre entrepôt Azure SQL Data Warehouse.

    ![Affichage des données chargées](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a>Améliorer les performances des requêtes

Performances des requêtes de plusieurs façons tooimprove et performances haut débit tooachieve hello qui est de l’entrepôt de données SQL conçue tooprovide.  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a>Voir effet hello de mise à l’échelle sur les performances des requêtes 

Performances des requêtes tooimprove unidirectionnel sont tooscale ressources en modifiant le niveau de service hello DWU de votre entrepôt de données. Chaque niveau de service est plus onéreux, mais vous pouvez réduire la taille des ressources ou les mettre en pause à tout moment. 

Lors de cette étape, vous comparez les performances de deux paramètres DWU différents.

Tout d’abord, nous allons mettre à l’échelle de dimensionnement hello too100 DWU afin de nous pouvons obtenir une idée de la manière dont un nœud de calcul peut s’exécuter sur son propre vers le bas.

1. Toohello portail, sélectionnez votre entrepôt de données SQL.

2. Sélectionnez l’échelle dans le panneau de l’entrepôt de données SQL hello. 

    ![Mise à l’échelle de l’instance SQL Data Warehouse dans le portail](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. Performances hello barre too100 DWU à l’échelle et cliquez sur Enregistrer.

    ![Mise à l’échelle et enregistrement](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. Attendez que votre toofinish d’opération de mise à l’échelle.

    > [!NOTE]
    > Impossible d’exécuter des requêtes lors du changement d’échelle de hello. La mise à l’échelle **supprime** vos requêtes en cours d’exécution. Vous pourrez les redémarrer lorsque hello est terminée.
    >
    
5. Effectuer une opération d’analyse sur les données de voyage hello, en sélectionnant millions entrées de hello supérieur pour toutes les colonnes hello. Si vous êtes toomove hâtif sur rapidement, vous pouvez tooselect libre moins de lignes. Prenez note de hello temps toorun cette opération.

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. Mettre à l’échelle de votre entrepôt de données de sauvegarde too400 DWU. N’oubliez pas de chaque DWU 100 consiste à ajouter un autre tooyour de nœud de calcul Azure SQL Data Warehouse.

7. Réexécutez la requête de hello ! Vous devriez remarquer une différence importante. 

    > [!NOTE]
    > Requête de hello retourne une grande quantité de données, disponibilité de la bande passante hello d’ordinateur hello SSMS en cours d’exécution peut-être ne pas être un goulot d’étranglement. Cela peut vous empêcher de noter des améliorations des performances !

> [!NOTE]
> Étant donné que SQL Data Warehouse utilise le traitement massivement parallèle, Les requêtes qui analyse ou d’effectuer des fonctions analytiques sur des millions de lignes tirer hello véritable puissance de Azure SQL Data Warehouse.
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a>Voir l’effet hello des statistiques sur les performances des requêtes

1. Exécuter une requête que les jointures hello table Date avec la table de voyage hello

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    Cette requête prend un certain temps car SQL Data Warehouse contient des données de tooshuffle avant de pouvoir effectuer la jointure de hello. Jointures de données ne sont pas tooshuffle s’ils sont conçus toojoin données hello même façon, il est distribué. Il s’agit d’un thème plus spécifique. 

2. Les statistiques font la différence. 
3. Exécutez cette toocreate les statistiques instruction sur les colonnes de jointure hello.

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > Azure SQL Data Warehouse ne gère pas automatiquement les statistiques pour vous. Or, ces statistiques sont importantes pour déterminer les performances des requêtes. Il est donc fortement recommandé de créer et de mettre à jour les statistiques.
    > 
    > **Vous pouvez bénéficier hello plus en ayant des statistiques sur des colonnes impliquées dans les jointures, les colonnes utilisées dans hello où clause et colonnes trouvent dans GROUP BY.**
    >

3. Réexécutez hello requête à la configuration requise et observez les différences de performances. Pendant les différences de hello dans les performances des requêtes ne sera pas aussi radicales que l’évolution verticale, vous devez remarquer une accélération. 

## <a name="next-steps"></a>Étapes suivantes

Vous êtes maintenant prêt tooquery et Explorer. Découvrez nos meilleures pratiques et nos conseils !

Si vous avez terminé exploration jours hello, de rendre toopause que votre instance ! En production, vous pouvez être confronté économies considérables en suspendant et mise à l’échelle toomeet besoins de votre entreprise.

![Suspendre](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a>Documents utiles

[Gestion de la concurrence et des charges de travail][]

[Meilleures pratiques pour Azure SQL Data Warehouse][]

[surveillance des requêtes][]

[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][] (10 meilleures pratiques pour la création d’un entrepôt de données relationnelles à grande échelle)

[Migration tooAzure de données SQL Data Warehouse][]

[Gestion de la concurrence et des charges de travail]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Meilleures pratiques pour Azure SQL Data Warehouse]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[surveillance des requêtes]: sql-data-warehouse-manage-monitor.md
[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/ (10 meilleures pratiques pour la création d’un entrepôt de données relationnelles à grande échelle)
[Migration tooAzure de données SQL Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[conditions préalables]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
