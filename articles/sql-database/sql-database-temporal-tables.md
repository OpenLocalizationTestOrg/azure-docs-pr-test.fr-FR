---
title: "aaaGetting démarré avec des Tables temporelles dans la base de données SQL Azure | Documents Microsoft"
description: "Découvrez comment tooget main à l’aide des Tables temporelles dans la base de données SQL Azure."
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: c8c0f232-0751-4a7f-a36e-67a0b29fa1b8
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 01/10/2017
ms.author: bonova
ms.openlocfilehash: 54f394b51df07aa2f9bb299f207e692171d23479
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a><span data-ttu-id="29c79-103">Prise en main des tables temporelles dans Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="29c79-103">Getting Started with Temporal Tables in Azure SQL Database</span></span>
<span data-ttu-id="29c79-104">Tables temporelles sont une nouvelle fonctionnalité de programmabilité de la base de données SQL Azure qui vous permet de tootrack et analyser l’historique complet de hello des modifications dans vos données, sans avoir besoin de hello de codage personnalisé.</span><span class="sxs-lookup"><span data-stu-id="29c79-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you tootrack and analyze hello full history of changes in your data, without hello need for custom coding.</span></span> <span data-ttu-id="29c79-105">Tables temporelles conserver contexte tootime étroitement liés de données afin que les faits stockés peuvent être interprétées comme étant valides uniquement au sein de la période spécifique de hello.</span><span class="sxs-lookup"><span data-stu-id="29c79-105">Temporal Tables keep data closely related tootime context so that stored facts can be interpreted as valid only within hello specific period.</span></span> <span data-ttu-id="29c79-106">Cette propriété des tables temporelles permet une analyse efficace basée sur le temps et permet d’obtenir des informations à partir de l’évolution des données.</span><span class="sxs-lookup"><span data-stu-id="29c79-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span></span>

## <a name="temporal-scenario"></a><span data-ttu-id="29c79-107">Scénario temporel</span><span class="sxs-lookup"><span data-stu-id="29c79-107">Temporal Scenario</span></span>
<span data-ttu-id="29c79-108">Cet article explique hello étapes tooutilize Tables temporelles dans un scénario d’application.</span><span class="sxs-lookup"><span data-stu-id="29c79-108">This article illustrates hello steps tooutilize Temporal Tables in an application scenario.</span></span> <span data-ttu-id="29c79-109">Supposons que vous souhaitez tootrack l’activité des utilisateurs sur un site Web qui est en cours de développement à partir de zéro ou sur un site Web existant, que vous souhaitez tooextend avec analytique d’activité utilisateur.</span><span class="sxs-lookup"><span data-stu-id="29c79-109">Suppose that you want tootrack user activity on a new website that is being developed from scratch or on an existing website that you want tooextend with user activity analytics.</span></span> <span data-ttu-id="29c79-110">Dans cet exemple simplifié, nous supposons que plusieurs hello des pages web visités pendant une période de temps est un indicateur qui doit toobe capturées et analysées dans la base de données du site Web hello est hébergé sur la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="29c79-110">In this simplified example, we assume that hello number of visited web pages during a period of time is an indicator that needs toobe captured and monitored in hello website database that is hosted on Azure SQL Database.</span></span> <span data-ttu-id="29c79-111">objectif Hello d’analyse de l’historique hello d’activités des utilisateurs est le site Web de tooget entrées tooredesign et fournir la meilleure expérience pour les visiteurs de hello.</span><span class="sxs-lookup"><span data-stu-id="29c79-111">hello goal of hello historical analysis of user activity is tooget inputs tooredesign website and provide better experience for hello visitors.</span></span>

<span data-ttu-id="29c79-112">modèle de base de données Hello pour ce scénario est très simple : mesure d’activité utilisateur est représentée avec un champ d’entier unique, **PageVisited**et sont capturées en même temps que les informations de base sur le profil d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="29c79-112">hello database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on hello user profile.</span></span> <span data-ttu-id="29c79-113">En outre, pour l’analyse de l’heure, vous conservez une série de lignes pour chaque utilisateur, où chaque ligne représente le nombre de hello de pages consultée par un utilisateur particulier au sein d’une période spécifique.</span><span class="sxs-lookup"><span data-stu-id="29c79-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents hello number of pages a particular user visited within a specific period of time.</span></span>

![Schéma](./media/sql-database-temporal-tables/AzureTemporal1.png)

<span data-ttu-id="29c79-115">Heureusement, vous n’avez pas besoin tooput tout effort dans votre application toomaintain ces informations d’activité.</span><span class="sxs-lookup"><span data-stu-id="29c79-115">Fortunately, you do not need tooput any effort in your app toomaintain this activity information.</span></span> <span data-ttu-id="29c79-116">Avec les Tables temporelles, ce processus est automatisé - ce qui vous donne une souplesse complète pendant la conception de site Web et plus toofocus de temps sur l’analyse de données hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="29c79-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time toofocus on hello data analysis itself.</span></span> <span data-ttu-id="29c79-117">Hello la seule chose que vous avez toodo est tooensure qui **WebSiteInfo** table est configurée en tant que [temporelles avec version système](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="29c79-117">hello only thing you have toodo is tooensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span></span> <span data-ttu-id="29c79-118">Hello étapes exactes tooutilize Tables temporelles dans ce scénario sont décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="29c79-118">hello exact steps tooutilize Temporal Tables in this scenario are described below.</span></span>

## <a name="step-1-configure-tables-as-temporal"></a><span data-ttu-id="29c79-119">Étape 1: Configurer les tables comme tables temporelles</span><span class="sxs-lookup"><span data-stu-id="29c79-119">Step 1: Configure tables as temporal</span></span>
<span data-ttu-id="29c79-120">Selon que vous commencez le développement d’une nouvelle application ou que vous mettez à niveau une application existante, vous créez des tables temporelles ou vous modifiez des tables existantes en ajoutant des attributs temporels.</span><span class="sxs-lookup"><span data-stu-id="29c79-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span></span> <span data-ttu-id="29c79-121">En général, votre scénario peut être une combinaison de ces deux options.</span><span class="sxs-lookup"><span data-stu-id="29c79-121">In general case, your scenario can be a mix of these two options.</span></span> <span data-ttu-id="29c79-122">Exécutez ces opérations à l’aide de [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) ou tout autre outil de développement Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="29c79-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29c79-123">Il est recommandé de toujours utiliser hello dernière version de Management Studio tooremain synchronisés avec les mises à jour tooMicrosoft Azure et base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="29c79-123">It is recommended that you always use hello latest version of Management Studio tooremain synchronized with updates tooMicrosoft Azure and SQL Database.</span></span> <span data-ttu-id="29c79-124">[Mettre à jour SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="29c79-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="create-new-table"></a><span data-ttu-id="29c79-125">Créer une table</span><span class="sxs-lookup"><span data-stu-id="29c79-125">Create new table</span></span>
<span data-ttu-id="29c79-126">Utilisez l’élément de menu contextuel « Nouvelle Table avec version système » dans l’éditeur de requête de l’Explorateur d’objets SSMS tooopen hello avec un script de modèle de table temporelle et ensuite utiliser le modèle de hello toopopulate « Spécifier les valeurs de paramètres de modèle « (Ctrl + Maj + M) :</span><span class="sxs-lookup"><span data-stu-id="29c79-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer tooopen hello query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) toopopulate hello template:</span></span>

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

<span data-ttu-id="29c79-128">Dans SSDT, a choisi le modèle de « Table temporelle (système par version) » lors de l’ajout du nouveau projet de base de données des éléments toohello.</span><span class="sxs-lookup"><span data-stu-id="29c79-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items toohello database project.</span></span> <span data-ttu-id="29c79-129">Que sont le Concepteur de tables ouverts et activer tooeasily vous spécifiez hello disposition de table :</span><span class="sxs-lookup"><span data-stu-id="29c79-129">That will open table designer and enable you tooeasily specify hello table layout:</span></span>

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

<span data-ttu-id="29c79-131">Vous pouvez également une instruction create temporal table en spécifiant les instructions Transact-SQL de hello directement, comme indiqué dans l’exemple hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="29c79-131">You can also a create temporal table by specifying hello Transact-SQL statements directly, as shown in hello example below.</span></span> <span data-ttu-id="29c79-132">Notez que hello éléments obligatoires de chaque table temporelle sont la définition de la période hello et clause SYSTEM_VERSIONING de hello avec une table d’utilisateur tooanother référence qui stocke les versions de ligne d’historique :</span><span class="sxs-lookup"><span data-stu-id="29c79-132">Note that hello mandatory elements of every temporal table are hello PERIOD definition and hello SYSTEM_VERSIONING clause with a reference tooanother user table that will store historical row versions:</span></span>

````
CREATE TABLE WebsiteUserInfo 
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED 
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL 
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
````

<span data-ttu-id="29c79-133">Lorsque vous créez la table temporelle avec version système, hello accompagnant la table d’historique hello configuration par défaut est automatiquement créé.</span><span class="sxs-lookup"><span data-stu-id="29c79-133">When you create system-versioned temporal table, hello accompanying history table with hello default configuration is automatically created.</span></span> <span data-ttu-id="29c79-134">table d’historique par défaut Hello contient un index B-tree de cluster sur les colonnes de période hello (début, fin) avec la compression de page activée.</span><span class="sxs-lookup"><span data-stu-id="29c79-134">hello default history table contains a clustered B-tree index on hello period columns (end, start) with page compression enabled.</span></span> <span data-ttu-id="29c79-135">Cette configuration est optimale pour la majorité de hello des scénarios dans lesquels les tables temporelles sont utilisés, en particulier pour [l’audit des données](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="29c79-135">This configuration is optimal for hello majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span></span> 

<span data-ttu-id="29c79-136">Dans ce cas particulier, nous visent tooperform temporels tendances sur un historique de données plus long et de jeux de données plus grande, choix du stockage pour la table d’historique hello hello est un index cluster columnstore.</span><span class="sxs-lookup"><span data-stu-id="29c79-136">In this particular case, we aim tooperform time-based trend analysis over a longer data history and with bigger data sets, so hello storage choice for hello history table is a clustered columnstore index.</span></span> <span data-ttu-id="29c79-137">L’index cluster columnstore fournit une très bonne compression et des performances optimales pour les requêtes analytiques.</span><span class="sxs-lookup"><span data-stu-id="29c79-137">A clustered columnstore provides very good compression and performance for analytical queries.</span></span> <span data-ttu-id="29c79-138">Fournissent des Tables temporel vous hello index tooconfigure de flexibilité sur les tables actuelles et temporelles hello totalement indépendants.</span><span class="sxs-lookup"><span data-stu-id="29c79-138">Temporal Tables give you hello flexibility tooconfigure indexes on hello current and temporal tables completely independently.</span></span> 

> [!NOTE]
> <span data-ttu-id="29c79-139">Index ColumnStore sont uniquement disponibles dans le niveau de service premium hello.</span><span class="sxs-lookup"><span data-stu-id="29c79-139">Columnstore indexes are only available in hello premium service tier.</span></span>
>

<span data-ttu-id="29c79-140">Hello script suivant montre comment les index par défaut sur la table d’historique peut être modifiées toohello clusterisé columnstore :</span><span class="sxs-lookup"><span data-stu-id="29c79-140">hello following script shows how default index on history table can be changed toohello clustered columnstore:</span></span>

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

<span data-ttu-id="29c79-141">Tables temporelles sont représentés dans hello l’Explorateur d’objets avec une icône spécifique de hello pour faciliter l’identification, tandis que sa table d’historique est affiché comme un nœud enfant.</span><span class="sxs-lookup"><span data-stu-id="29c79-141">Temporal Tables are represented in hello Object Explorer with hello specific icon for easier identification, while its history table is displayed as a child node.</span></span>

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a><span data-ttu-id="29c79-143">ALTER tootemporal de table existant</span><span class="sxs-lookup"><span data-stu-id="29c79-143">Alter existing table tootemporal</span></span>
<span data-ttu-id="29c79-144">Nous allons couvrir les scénarios alternatifs hello dans le hello WebsiteUserInfo table existe déjà, mais n’était pas tookeep conçu un historique des modifications.</span><span class="sxs-lookup"><span data-stu-id="29c79-144">Let’s cover hello alternative scenario in which hello WebsiteUserInfo table already exists, but was not designed tookeep a history of changes.</span></span> <span data-ttu-id="29c79-145">Dans ce cas, vous pouvez étendre toobecome table hello existant temporelle, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="29c79-145">In this case, you can simply extend hello existing table toobecome temporal, as shown in hello following example:</span></span>

````
ALTER TABLE WebsiteUserInfo 
ADD 
    ValidFrom datetime2 (0) GENERATED ALWAYS AS ROW START HIDDEN  
        constraint DF_ValidFrom DEFAULT DATEADD(SECOND, -1, SYSUTCDATETIME())
    , ValidTo datetime2 (0)  GENERATED ALWAYS AS ROW END HIDDEN   
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo); 

ALTER TABLE WebsiteUserInfo  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

## <a name="step-2-run-your-workload-regularly"></a><span data-ttu-id="29c79-146">Étape 2 : Exécuter votre charge de travail de façon régulière</span><span class="sxs-lookup"><span data-stu-id="29c79-146">Step 2: Run your workload regularly</span></span>
<span data-ttu-id="29c79-147">Hello principal avantage des Tables temporelles est ne pas besoin de toochange ou d’ajuster votre site Web dans n’importe quel moyen tooperform le suivi.</span><span class="sxs-lookup"><span data-stu-id="29c79-147">hello main advantage of Temporal Tables is that you do not need toochange or adjust your website in any way tooperform change tracking.</span></span> <span data-ttu-id="29c79-148">Une fois créées, les tables temporelles conservent en toute transparence les versions précédentes des lignes chaque fois que vous effectuez des modifications sur vos données.</span><span class="sxs-lookup"><span data-stu-id="29c79-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span></span> 

<span data-ttu-id="29c79-149">Dans l’ordre tooleverage suivi des modifications automatique pour ce scénario particulier, nous allons simplement mettre à jour colonne **PagesVisited** chaque fois que lorsque l’utilisateur met fin à sa session sur le site Web de hello :</span><span class="sxs-lookup"><span data-stu-id="29c79-149">In order tooleverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on hello website:</span></span>

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

<span data-ttu-id="29c79-150">Il est important de toonotice qui hello requête mise à jour n’a pas besoin tooknow hello heure exacte à laquelle s’est produite lors de l’opération réelle de hello, ni comment les données d’historique seront conservées pour une analyse future.</span><span class="sxs-lookup"><span data-stu-id="29c79-150">It is important toonotice that hello update query doesn’t need tooknow hello exact time when hello actual operation occurred nor how historical data will be preserved for future analysis.</span></span> <span data-ttu-id="29c79-151">Les deux aspects sont gérées automatiquement par hello de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="29c79-151">Both aspects are automatically handled by hello Azure SQL Database.</span></span> <span data-ttu-id="29c79-152">Hello diagramme suivant illustre comment les données d’historique sont générées sur chaque mise à jour.</span><span class="sxs-lookup"><span data-stu-id="29c79-152">hello following diagram illustrates how history data is being generated on every update.</span></span>

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a><span data-ttu-id="29c79-154">Étape 3: Analyser les données historiques</span><span class="sxs-lookup"><span data-stu-id="29c79-154">Step 3: Perform historical data analysis</span></span>
<span data-ttu-id="29c79-155">Une fois que la gestion de version des tables temporelles par le système est activée, il vous suffit d’une seule requête pour analyser les données historiques.</span><span class="sxs-lookup"><span data-stu-id="29c79-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span></span> <span data-ttu-id="29c79-156">Dans cet article, nous allons sera fournir quelques exemples de scénarios courants analyse - toolearn tous les détails, Explorer différentes options introduites par Bonjour [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span><span class="sxs-lookup"><span data-stu-id="29c79-156">In this article, we will provide a few examples that address common analysis scenarios - toolearn all details, explore various options introduced with hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span></span>

<span data-ttu-id="29c79-157">toosee hello top 10 utilisateurs classés par nombre de hello de pages web visitées à partir d’une heure, exécutez cette requête :</span><span class="sxs-lookup"><span data-stu-id="29c79-157">toosee hello top 10 users ordered by hello number of visited web pages as of an hour ago, run this query:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

<span data-ttu-id="29c79-158">Vous pouvez facilement modifier cette requête tooanalyze hello visites un jour il y a un mois d’avance ou à tout moment dans hello précédente vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="29c79-158">You can easily modify this query tooanalyze hello site visits as of a day ago, a month ago or at any point in hello past you wish.</span></span>

<span data-ttu-id="29c79-159">analyse de statistiques de base de tooperform pour hello jour précédent, utilisez hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="29c79-159">tooperform basic statistical analysis for hello previous day, use hello following example:</span></span>

````
DECLARE @twoDaysAgo datetime2 = DATEADD(DAY, -2, SYSUTCDATETIME());
DECLARE @aDayAgo datetime2 = DATEADD(DAY, -1, SYSUTCDATETIME());

SELECT UserID, SUM (PagesVisited) as TotalVisitedPages, AVG (PagesVisited) as AverageVisitedPages,
MAX (PagesVisited) AS MaxVisitedPages, MIN (PagesVisited) AS MinVisitedPages,
STDEV (PagesVisited) as StDevViistedPages
FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME BETWEEN @twoDaysAgo AND @aDayAgo
GROUP BY UserId
````

<span data-ttu-id="29c79-160">toosearch pour les activités d’un utilisateur spécifique, dans un laps de temps, utilisez hello CONTAINED IN clause :</span><span class="sxs-lookup"><span data-stu-id="29c79-160">toosearch for activities of a specific user, within a period of time, use hello CONTAINED IN clause:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

<span data-ttu-id="29c79-161">La visualisation graphique est particulièrement pratique pour les requêtes temporelles, car vous pouvez afficher les tendances et les modèles d’utilisation de façon intuitive très facilement :</span><span class="sxs-lookup"><span data-stu-id="29c79-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span></span>

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a><span data-ttu-id="29c79-163">Évolution du schéma de table</span><span class="sxs-lookup"><span data-stu-id="29c79-163">Evolving table schema</span></span>
<span data-ttu-id="29c79-164">En règle générale, vous devez schéma de table temporelle toochange hello pendant que vous faites le développement d’applications.</span><span class="sxs-lookup"><span data-stu-id="29c79-164">Typically, you will need toochange hello temporal table schema while you are doing app development.</span></span> <span data-ttu-id="29c79-165">Pour ce faire, il suffit d’exécuter les instructions ALTER TABLE régulières et base de données SQL Azure seront propagées correctement la table d’historique des modifications toohello.</span><span class="sxs-lookup"><span data-stu-id="29c79-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes toohello history table.</span></span> <span data-ttu-id="29c79-166">Hello script suivant montre comment vous pouvez ajouter des attributs supplémentaires pour le suivi :</span><span class="sxs-lookup"><span data-stu-id="29c79-166">hello following script shows how you can add additional attribute for tracking:</span></span>

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

<span data-ttu-id="29c79-167">De même, vous pouvez modifier la définition de colonne pendant que votre charge de travail est active :</span><span class="sxs-lookup"><span data-stu-id="29c79-167">Similarly, you can change column definition while your workload is active:</span></span>

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

<span data-ttu-id="29c79-168">Enfin, vous pouvez supprimer une colonne dont vous n’avez plus besoin.</span><span class="sxs-lookup"><span data-stu-id="29c79-168">Finally, you can remove a column that you do not need anymore.</span></span>

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

<span data-ttu-id="29c79-169">Vous pouvez également utiliser plus tard [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange temporelle schéma de table pendant que vous êtes connecté toohello la base de données (mode en ligne) ou en tant que partie du projet de base de données hello (mode hors connexion).</span><span class="sxs-lookup"><span data-stu-id="29c79-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange temporal table schema while you are connected toohello database (online mode) or as part of hello database project (offline mode).</span></span>

## <a name="controlling-retention-of-historical-data"></a><span data-ttu-id="29c79-170">Contrôle de la rétention des données historiques</span><span class="sxs-lookup"><span data-stu-id="29c79-170">Controlling retention of historical data</span></span>
<span data-ttu-id="29c79-171">Avec des tables temporelles avec version gérée par le système de table d’historique hello peut augmenter de taille de base de données hello plus de tables normales.</span><span class="sxs-lookup"><span data-stu-id="29c79-171">With system-versioned temporal tables, hello history table may increase hello database size more than regular tables.</span></span> <span data-ttu-id="29c79-172">Une table d’historique volumineuse et qui ne cesse de croître peut devenir un problème en raison des coûts de stockage toopure ainsi qu’imposant des performances sur l’interrogation temporelle.</span><span class="sxs-lookup"><span data-stu-id="29c79-172">A large and ever-growing history table can become an issue both due toopure storage costs as well as imposing a performance tax on temporal querying.</span></span> <span data-ttu-id="29c79-173">Par conséquent, le développement d’une stratégie de rétention de données pour la gestion des données dans la table d’historique hello est un aspect important de la planification et la gestion du cycle de vie hello de chaque table temporelle.</span><span class="sxs-lookup"><span data-stu-id="29c79-173">Hence, developing a data retention policy for managing data in hello history table is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="29c79-174">Avec la base de données SQL Azure, vous avez hello méthodes pour la gestion des données d’historique dans la table temporelle hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="29c79-174">With Azure SQL Database, you have hello following approaches for managing historical data in hello temporal table:</span></span>

* [<span data-ttu-id="29c79-175">Partitionnement de tables</span><span class="sxs-lookup"><span data-stu-id="29c79-175">Table Partitioning</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [<span data-ttu-id="29c79-176">Script de nettoyage personnalisé</span><span class="sxs-lookup"><span data-stu-id="29c79-176">Custom Cleanup Script</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a><span data-ttu-id="29c79-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29c79-177">Next steps</span></span>
<span data-ttu-id="29c79-178">Pour plus d’informations sur les tables temporelles, consultez la [documentation MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="29c79-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>
<span data-ttu-id="29c79-179">Visitez Channel 9 toohear un [réussite implémentation temporelle de client réel](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) et Espion un [live démonstration temporelle](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="29c79-179">Visit Channel 9 toohear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

