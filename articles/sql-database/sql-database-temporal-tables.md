---
title: Prise en main des tables temporelles dans Azure SQL Database | Microsoft Docs
description: "Découvrez comment prendre en main les tables temporelles dans Azure SQL Database."
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
ms.openlocfilehash: d84db682089c65c2716d2d9bd92f7bc0ac47af27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a><span data-ttu-id="c0b3e-103">Prise en main des tables temporelles dans Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="c0b3e-103">Getting Started with Temporal Tables in Azure SQL Database</span></span>
<span data-ttu-id="c0b3e-104">Les tables temporelles sont une nouvelle fonctionnalité de programmabilité d’Azure SQL Database qui vous permet de suivre et d’analyser l’historique complet des modifications apportées à vos données, sans codage personnalisé.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you to track and analyze the full history of changes in your data, without the need for custom coding.</span></span> <span data-ttu-id="c0b3e-105">Les tables temporelles conservent les données étroitement liées au contexte temporel afin que les faits stockés puissent être interprétés comme étant valides uniquement dans une période spécifique.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-105">Temporal Tables keep data closely related to time context so that stored facts can be interpreted as valid only within the specific period.</span></span> <span data-ttu-id="c0b3e-106">Cette propriété des tables temporelles permet une analyse efficace basée sur le temps et permet d’obtenir des informations à partir de l’évolution des données.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span></span>

## <a name="temporal-scenario"></a><span data-ttu-id="c0b3e-107">Scénario temporel</span><span class="sxs-lookup"><span data-stu-id="c0b3e-107">Temporal Scenario</span></span>
<span data-ttu-id="c0b3e-108">Cet article illustre les étapes permettant d’utiliser les tables temporelles dans un scénario d’application.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-108">This article illustrates the steps to utilize Temporal Tables in an application scenario.</span></span> <span data-ttu-id="c0b3e-109">Supposons que vous voulez effectuer le suivi de l’activité utilisateur sur un nouveau site web en cours de développement ou sur un site web existant que vous voulez enrichir avec l’analyse de l’activité utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-109">Suppose that you want to track user activity on a new website that is being developed from scratch or on an existing website that you want to extend with user activity analytics.</span></span> <span data-ttu-id="c0b3e-110">Dans cet exemple simplifié, nous partons du principe que le nombre de pages web visitées pendant une période de temps est un indicateur qui doit être capturé et analysé dans la base de données du site web hébergée sur Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-110">In this simplified example, we assume that the number of visited web pages during a period of time is an indicator that needs to be captured and monitored in the website database that is hosted on Azure SQL Database.</span></span> <span data-ttu-id="c0b3e-111">L’objectif de l’analyse de l’historique de l’activité utilisateur est d’obtenir des informations pour redessiner le site web et fournir une meilleure expérience pour les visiteurs.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-111">The goal of the historical analysis of user activity is to get inputs to redesign website and provide better experience for the visitors.</span></span>

<span data-ttu-id="c0b3e-112">Le modèle de base de données pour ce scénario est très simple : la mesure de l’activité utilisateur est représentée par un champ d’entier unique, **PageVisited**, et est capturée en même temps que des informations de base sur le profil utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-112">The database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on the user profile.</span></span> <span data-ttu-id="c0b3e-113">En outre, pour l’analyse temporelle, vous conservez une série de lignes pour chaque utilisateur, où chaque ligne représente le nombre de pages visitées par un utilisateur particulier dans une période de temps spécifique.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents the number of pages a particular user visited within a specific period of time.</span></span>

![Schéma](./media/sql-database-temporal-tables/AzureTemporal1.png)

<span data-ttu-id="c0b3e-115">Heureusement, vous n’avez pas besoin d’intervenir sur votre application pour gérer les informations de cette activité.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-115">Fortunately, you do not need to put any effort in your app to maintain this activity information.</span></span> <span data-ttu-id="c0b3e-116">Avec les tables temporelles, ce processus est automatisé : ce qui vous donne une grande souplesse pour concevoir le site web et davantage de temps pour vous concentrer sur l’analyse des données.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time to focus on the data analysis itself.</span></span> <span data-ttu-id="c0b3e-117">La seule chose que vous avez à faire est de garantir que la table **WebSiteInfo** est configurée en tant que table [temporelle avec versions gérées par le système](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="c0b3e-117">The only thing you have to do is to ensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span></span> <span data-ttu-id="c0b3e-118">Les étapes à suivre pour utiliser les tables temporelles dans ce scénario sont décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-118">The exact steps to utilize Temporal Tables in this scenario are described below.</span></span>

## <a name="step-1-configure-tables-as-temporal"></a><span data-ttu-id="c0b3e-119">Étape 1: Configurer les tables comme tables temporelles</span><span class="sxs-lookup"><span data-stu-id="c0b3e-119">Step 1: Configure tables as temporal</span></span>
<span data-ttu-id="c0b3e-120">Selon que vous commencez le développement d’une nouvelle application ou que vous mettez à niveau une application existante, vous créez des tables temporelles ou vous modifiez des tables existantes en ajoutant des attributs temporels.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span></span> <span data-ttu-id="c0b3e-121">En général, votre scénario peut être une combinaison de ces deux options.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-121">In general case, your scenario can be a mix of these two options.</span></span> <span data-ttu-id="c0b3e-122">Exécutez ces opérations à l’aide de [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) ou tout autre outil de développement Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0b3e-123">Nous vous recommandons d’utiliser systématiquement la dernière version de Management Studio afin de rester en cohérence avec les mises à jour de Microsoft Azure et Base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-123">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span></span> <span data-ttu-id="c0b3e-124">[Mettre à jour SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0b3e-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="create-new-table"></a><span data-ttu-id="c0b3e-125">Créer une table</span><span class="sxs-lookup"><span data-stu-id="c0b3e-125">Create new table</span></span>
<span data-ttu-id="c0b3e-126">Utilisez l’élément de menu contextuel Nouvelle table avec version système dans l’Explorateur d’objets SSMS pour ouvrir l’éditeur de requête avec un script de modèle de table temporelle, puis utilisez « Spécifier les valeurs des paramètres du modèle » (Ctrl+Maj+M) pour remplir le modèle :</span><span class="sxs-lookup"><span data-stu-id="c0b3e-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer to open the query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) to populate the template:</span></span>

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

<span data-ttu-id="c0b3e-128">Dans SSDT, choisissez le modèle « Table temporelle (Système par version) » quand vous ajoutez de nouveaux éléments au projet de base de données.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items to the database project.</span></span> <span data-ttu-id="c0b3e-129">Cette opération ouvre le concepteur de tables et vous permet de spécifier facilement la disposition de la table :</span><span class="sxs-lookup"><span data-stu-id="c0b3e-129">That will open table designer and enable you to easily specify the table layout:</span></span>

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

<span data-ttu-id="c0b3e-131">Vous pouvez également créer une table temporelle en spécifiant les instructions Transact-SQL directement, comme indiqué dans l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-131">You can also a create temporal table by specifying the Transact-SQL statements directly, as shown in the example below.</span></span> <span data-ttu-id="c0b3e-132">Notez que les éléments obligatoires de chaque table temporelle sont la définition de PERIOD et la clause SYSTEM_VERSIONING avec une référence à une autre table utilisateur qui stocke les versions de ligne historiques :</span><span class="sxs-lookup"><span data-stu-id="c0b3e-132">Note that the mandatory elements of every temporal table are the PERIOD definition and the SYSTEM_VERSIONING clause with a reference to another user table that will store historical row versions:</span></span>

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

<span data-ttu-id="c0b3e-133">Quand vous créez une table temporelle avec versions gérées par le système, la table d’historique associée avec la configuration par défaut est automatiquement créée.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-133">When you create system-versioned temporal table, the accompanying history table with the default configuration is automatically created.</span></span> <span data-ttu-id="c0b3e-134">La table d’historique par défaut contient un index cluster arbre B (B-tree) sur les colonnes de période (début, fin) pour lequel la compression de page est activée.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-134">The default history table contains a clustered B-tree index on the period columns (end, start) with page compression enabled.</span></span> <span data-ttu-id="c0b3e-135">Cette configuration est optimale pour la plupart des scénarios dans lesquels les tables temporelles sont utilisées, en particulier pour l’ [audit des données](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="c0b3e-135">This configuration is optimal for the majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span></span> 

<span data-ttu-id="c0b3e-136">Dans ce cas particulier, nous voulons effectuer une analyse temporelle des tendances sur un historique de données plus long et avec des jeux de données plus volumineux, le choix du stockage pour la table d’historique est donc un index cluster columnstore.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-136">In this particular case, we aim to perform time-based trend analysis over a longer data history and with bigger data sets, so the storage choice for the history table is a clustered columnstore index.</span></span> <span data-ttu-id="c0b3e-137">L’index cluster columnstore fournit une très bonne compression et des performances optimales pour les requêtes analytiques.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-137">A clustered columnstore provides very good compression and performance for analytical queries.</span></span> <span data-ttu-id="c0b3e-138">Les tables temporelles vous donnent la possibilité de configurer complètement indépendamment des index sur les tables actuelles et temporelles.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-138">Temporal Tables give you the flexibility to configure indexes on the current and temporal tables completely independently.</span></span> 

> [!NOTE]
> <span data-ttu-id="c0b3e-139">Les index columnstore sont uniquement disponibles au niveau de service Premium.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-139">Columnstore indexes are only available in the premium service tier.</span></span>
>

<span data-ttu-id="c0b3e-140">Le script suivant montre comment l’index par défaut sur la table d’historique peut être modifié en index cluster columnstore :</span><span class="sxs-lookup"><span data-stu-id="c0b3e-140">The following script shows how default index on history table can be changed to the clustered columnstore:</span></span>

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

<span data-ttu-id="c0b3e-141">Les tables temporelles sont représentées dans l’Explorateur d’objets avec une icône spécifique pour faciliter l’identification, tandis que la table d’historique s’affiche comme un nœud enfant.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-141">Temporal Tables are represented in the Object Explorer with the specific icon for easier identification, while its history table is displayed as a child node.</span></span>

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-to-temporal"></a><span data-ttu-id="c0b3e-143">Transformer une table existante en table temporelle</span><span class="sxs-lookup"><span data-stu-id="c0b3e-143">Alter existing table to temporal</span></span>
<span data-ttu-id="c0b3e-144">Examinons l’autre scénario dans lequel la table WebsiteUserInfo existe déjà, mais n’a pas été conçue pour conserver un historique des modifications.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-144">Let’s cover the alternative scenario in which the WebsiteUserInfo table already exists, but was not designed to keep a history of changes.</span></span> <span data-ttu-id="c0b3e-145">Dans ce cas, vous pouvez simplement étendre la table existante pour qu’elle devienne temporelle, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c0b3e-145">In this case, you can simply extend the existing table to become temporal, as shown in the following example:</span></span>

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

## <a name="step-2-run-your-workload-regularly"></a><span data-ttu-id="c0b3e-146">Étape 2 : Exécuter votre charge de travail de façon régulière</span><span class="sxs-lookup"><span data-stu-id="c0b3e-146">Step 2: Run your workload regularly</span></span>
<span data-ttu-id="c0b3e-147">Le principal avantage des tables temporelles est que vous n’avez pas besoin de modifier ou d’ajuster votre site web de quelque façon que ce soit pour effectuer le suivi des modifications.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-147">The main advantage of Temporal Tables is that you do not need to change or adjust your website in any way to perform change tracking.</span></span> <span data-ttu-id="c0b3e-148">Une fois créées, les tables temporelles conservent en toute transparence les versions précédentes des lignes chaque fois que vous effectuez des modifications sur vos données.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span></span> 

<span data-ttu-id="c0b3e-149">Pour tirer parti du suivi automatique des modifications dans ce scénario particulier, nous allons simplement mettre à jour la colonne **PagesVisited** chaque fois qu’un utilisateur met fin à sa session sur le site web :</span><span class="sxs-lookup"><span data-stu-id="c0b3e-149">In order to leverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on the website:</span></span>

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

<span data-ttu-id="c0b3e-150">Notez que la requête de mise à jour n’a pas besoin de connaître l’heure exacte à laquelle s’est produit l’opération réelle ni comment les données historiques sont conservées pour une future analyse.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-150">It is important to notice that the update query doesn’t need to know the exact time when the actual operation occurred nor how historical data will be preserved for future analysis.</span></span> <span data-ttu-id="c0b3e-151">Ces deux aspects sont gérés automatiquement par Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-151">Both aspects are automatically handled by the Azure SQL Database.</span></span> <span data-ttu-id="c0b3e-152">Le diagramme suivant illustre la façon dont les données d’historique sont générées à chaque mise à jour.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-152">The following diagram illustrates how history data is being generated on every update.</span></span>

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a><span data-ttu-id="c0b3e-154">Étape 3: Analyser les données historiques</span><span class="sxs-lookup"><span data-stu-id="c0b3e-154">Step 3: Perform historical data analysis</span></span>
<span data-ttu-id="c0b3e-155">Une fois que la gestion de version des tables temporelles par le système est activée, il vous suffit d’une seule requête pour analyser les données historiques.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span></span> <span data-ttu-id="c0b3e-156">Dans cet article, nous fournissons des exemples de scénarios d’analyse courants. Pour connaître tous les détails, explorez les diverses options introduites avec la clause [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="c0b3e-156">In this article, we will provide a few examples that address common analysis scenarios - to learn all details, explore various options introduced with the [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span></span>

<span data-ttu-id="c0b3e-157">Pour afficher les 10 principaux utilisateurs classés par nombre de pages web visitées durant la dernière heure, exécutez cette requête :</span><span class="sxs-lookup"><span data-stu-id="c0b3e-157">To see the top 10 users ordered by the number of visited web pages as of an hour ago, run this query:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

<span data-ttu-id="c0b3e-158">Vous pouvez facilement modifier cette requête pour analyser les visites du site au cours du dernier jour, du dernier mois ou à n’importe quel moment dans le passé.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-158">You can easily modify this query to analyze the site visits as of a day ago, a month ago or at any point in the past you wish.</span></span>

<span data-ttu-id="c0b3e-159">Pour effectuer l’analyse statistique de base du jour précédent, utilisez l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c0b3e-159">To perform basic statistical analysis for the previous day, use the following example:</span></span>

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

<span data-ttu-id="c0b3e-160">Pour rechercher les activités d’un utilisateur spécifique dans une période de temps, utilisez la clause CONTAINED IN :</span><span class="sxs-lookup"><span data-stu-id="c0b3e-160">To search for activities of a specific user, within a period of time, use the CONTAINED IN clause:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

<span data-ttu-id="c0b3e-161">La visualisation graphique est particulièrement pratique pour les requêtes temporelles, car vous pouvez afficher les tendances et les modèles d’utilisation de façon intuitive très facilement :</span><span class="sxs-lookup"><span data-stu-id="c0b3e-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span></span>

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a><span data-ttu-id="c0b3e-163">Évolution du schéma de table</span><span class="sxs-lookup"><span data-stu-id="c0b3e-163">Evolving table schema</span></span>
<span data-ttu-id="c0b3e-164">En règle générale, vous devez modifier le schéma de table temporelle pendant le développement d’applications.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-164">Typically, you will need to change the temporal table schema while you are doing app development.</span></span> <span data-ttu-id="c0b3e-165">Pour ce faire, exécutez simplement des instructions ALTER TABLE standard et Azure SQL Database propage les modifications de manière appropriée dans la table d’historique.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes to the history table.</span></span> <span data-ttu-id="c0b3e-166">Le script suivant montre comment ajouter un attribut supplémentaire pour le suivi :</span><span class="sxs-lookup"><span data-stu-id="c0b3e-166">The following script shows how you can add additional attribute for tracking:</span></span>

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

<span data-ttu-id="c0b3e-167">De même, vous pouvez modifier la définition de colonne pendant que votre charge de travail est active :</span><span class="sxs-lookup"><span data-stu-id="c0b3e-167">Similarly, you can change column definition while your workload is active:</span></span>

````
/*Increase the length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

<span data-ttu-id="c0b3e-168">Enfin, vous pouvez supprimer une colonne dont vous n’avez plus besoin.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-168">Finally, you can remove a column that you do not need anymore.</span></span>

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

<span data-ttu-id="c0b3e-169">Vous pouvez également utiliser la dernière version de [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) pour modifier un schéma de table temporelle quand vous êtes connecté à la base de données (mode en ligne) ou dans le cadre du projet de base de données (mode hors connexion).</span><span class="sxs-lookup"><span data-stu-id="c0b3e-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) to change temporal table schema while you are connected to the database (online mode) or as part of the database project (offline mode).</span></span>

## <a name="controlling-retention-of-historical-data"></a><span data-ttu-id="c0b3e-170">Contrôle de la rétention des données historiques</span><span class="sxs-lookup"><span data-stu-id="c0b3e-170">Controlling retention of historical data</span></span>
<span data-ttu-id="c0b3e-171">Avec les tables temporelles avec versions gérées par le système, la table d’historique peut augmenter la taille de la base de données davantage que les tables normales.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-171">With system-versioned temporal tables, the history table may increase the database size more than regular tables.</span></span> <span data-ttu-id="c0b3e-172">Une table d’historique volumineuse qui continue à croître peut devenir un problème non seulement en raison des coûts de stockage, mais aussi parce qu’elle a un impact négatif sur les performances de l’interrogation temporelle.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-172">A large and ever-growing history table can become an issue both due to pure storage costs as well as imposing a performance tax on temporal querying.</span></span> <span data-ttu-id="c0b3e-173">Par conséquent, le développement d’une stratégie de rétention des données pour gérer les données dans la table d’historique est un aspect important de la planification et de la gestion du cycle de vie de chaque table temporelle.</span><span class="sxs-lookup"><span data-stu-id="c0b3e-173">Hence, developing a data retention policy for managing data in the history table is an important aspect of planning and managing the lifecycle of every temporal table.</span></span> <span data-ttu-id="c0b3e-174">Avec Azure SQL Database, vous bénéficiez des approches suivantes pour gérer les données historiques dans la table temporelle :</span><span class="sxs-lookup"><span data-stu-id="c0b3e-174">With Azure SQL Database, you have the following approaches for managing historical data in the temporal table:</span></span>

* [<span data-ttu-id="c0b3e-175">Partitionnement de tables</span><span class="sxs-lookup"><span data-stu-id="c0b3e-175">Table Partitioning</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [<span data-ttu-id="c0b3e-176">Script de nettoyage personnalisé</span><span class="sxs-lookup"><span data-stu-id="c0b3e-176">Custom Cleanup Script</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a><span data-ttu-id="c0b3e-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c0b3e-177">Next steps</span></span>
<span data-ttu-id="c0b3e-178">Pour plus d’informations sur les tables temporelles, consultez la [documentation MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0b3e-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>
<span data-ttu-id="c0b3e-179">Visitez Channel 9 pour écouter le [témoignage d’un client sur l’implémentation temporelle](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) et regardez une [démonstration de table temporelle en direct](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="c0b3e-179">Visit Channel 9 to hear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

