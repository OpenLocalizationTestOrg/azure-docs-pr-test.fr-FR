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
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a>Prise en main des tables temporelles dans Azure SQL Database
Tables temporelles sont une nouvelle fonctionnalité de programmabilité de la base de données SQL Azure qui vous permet de tootrack et analyser l’historique complet de hello des modifications dans vos données, sans avoir besoin de hello de codage personnalisé. Tables temporelles conserver contexte tootime étroitement liés de données afin que les faits stockés peuvent être interprétées comme étant valides uniquement au sein de la période spécifique de hello. Cette propriété des tables temporelles permet une analyse efficace basée sur le temps et permet d’obtenir des informations à partir de l’évolution des données.

## <a name="temporal-scenario"></a>Scénario temporel
Cet article explique hello étapes tooutilize Tables temporelles dans un scénario d’application. Supposons que vous souhaitez tootrack l’activité des utilisateurs sur un site Web qui est en cours de développement à partir de zéro ou sur un site Web existant, que vous souhaitez tooextend avec analytique d’activité utilisateur. Dans cet exemple simplifié, nous supposons que plusieurs hello des pages web visités pendant une période de temps est un indicateur qui doit toobe capturées et analysées dans la base de données du site Web hello est hébergé sur la base de données SQL Azure. objectif Hello d’analyse de l’historique hello d’activités des utilisateurs est le site Web de tooget entrées tooredesign et fournir la meilleure expérience pour les visiteurs de hello.

modèle de base de données Hello pour ce scénario est très simple : mesure d’activité utilisateur est représentée avec un champ d’entier unique, **PageVisited**et sont capturées en même temps que les informations de base sur le profil d’utilisateur hello. En outre, pour l’analyse de l’heure, vous conservez une série de lignes pour chaque utilisateur, où chaque ligne représente le nombre de hello de pages consultée par un utilisateur particulier au sein d’une période spécifique.

![Schéma](./media/sql-database-temporal-tables/AzureTemporal1.png)

Heureusement, vous n’avez pas besoin tooput tout effort dans votre application toomaintain ces informations d’activité. Avec les Tables temporelles, ce processus est automatisé - ce qui vous donne une souplesse complète pendant la conception de site Web et plus toofocus de temps sur l’analyse de données hello lui-même. Hello la seule chose que vous avez toodo est tooensure qui **WebSiteInfo** table est configurée en tant que [temporelles avec version système](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0). Hello étapes exactes tooutilize Tables temporelles dans ce scénario sont décrites ci-dessous.

## <a name="step-1-configure-tables-as-temporal"></a>Étape 1: Configurer les tables comme tables temporelles
Selon que vous commencez le développement d’une nouvelle application ou que vous mettez à niveau une application existante, vous créez des tables temporelles ou vous modifiez des tables existantes en ajoutant des attributs temporels. En général, votre scénario peut être une combinaison de ces deux options. Exécutez ces opérations à l’aide de [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) ou tout autre outil de développement Transact-SQL.

> [!IMPORTANT]
> Il est recommandé de toujours utiliser hello dernière version de Management Studio tooremain synchronisés avec les mises à jour tooMicrosoft Azure et base de données SQL. [Mettre à jour SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

### <a name="create-new-table"></a>Créer une table
Utilisez l’élément de menu contextuel « Nouvelle Table avec version système » dans l’éditeur de requête de l’Explorateur d’objets SSMS tooopen hello avec un script de modèle de table temporelle et ensuite utiliser le modèle de hello toopopulate « Spécifier les valeurs de paramètres de modèle « (Ctrl + Maj + M) :

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

Dans SSDT, a choisi le modèle de « Table temporelle (système par version) » lors de l’ajout du nouveau projet de base de données des éléments toohello. Que sont le Concepteur de tables ouverts et activer tooeasily vous spécifiez hello disposition de table :

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

Vous pouvez également une instruction create temporal table en spécifiant les instructions Transact-SQL de hello directement, comme indiqué dans l’exemple hello ci-dessous. Notez que hello éléments obligatoires de chaque table temporelle sont la définition de la période hello et clause SYSTEM_VERSIONING de hello avec une table d’utilisateur tooanother référence qui stocke les versions de ligne d’historique :

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

Lorsque vous créez la table temporelle avec version système, hello accompagnant la table d’historique hello configuration par défaut est automatiquement créé. table d’historique par défaut Hello contient un index B-tree de cluster sur les colonnes de période hello (début, fin) avec la compression de page activée. Cette configuration est optimale pour la majorité de hello des scénarios dans lesquels les tables temporelles sont utilisés, en particulier pour [l’audit des données](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0). 

Dans ce cas particulier, nous visent tooperform temporels tendances sur un historique de données plus long et de jeux de données plus grande, choix du stockage pour la table d’historique hello hello est un index cluster columnstore. L’index cluster columnstore fournit une très bonne compression et des performances optimales pour les requêtes analytiques. Fournissent des Tables temporel vous hello index tooconfigure de flexibilité sur les tables actuelles et temporelles hello totalement indépendants. 

> [!NOTE]
> Index ColumnStore sont uniquement disponibles dans le niveau de service premium hello.
>

Hello script suivant montre comment les index par défaut sur la table d’historique peut être modifiées toohello clusterisé columnstore :

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

Tables temporelles sont représentés dans hello l’Explorateur d’objets avec une icône spécifique de hello pour faciliter l’identification, tandis que sa table d’historique est affiché comme un nœud enfant.

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a>ALTER tootemporal de table existant
Nous allons couvrir les scénarios alternatifs hello dans le hello WebsiteUserInfo table existe déjà, mais n’était pas tookeep conçu un historique des modifications. Dans ce cas, vous pouvez étendre toobecome table hello existant temporelle, comme indiqué dans hello l’exemple suivant :

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

## <a name="step-2-run-your-workload-regularly"></a>Étape 2 : Exécuter votre charge de travail de façon régulière
Hello principal avantage des Tables temporelles est ne pas besoin de toochange ou d’ajuster votre site Web dans n’importe quel moyen tooperform le suivi. Une fois créées, les tables temporelles conservent en toute transparence les versions précédentes des lignes chaque fois que vous effectuez des modifications sur vos données. 

Dans l’ordre tooleverage suivi des modifications automatique pour ce scénario particulier, nous allons simplement mettre à jour colonne **PagesVisited** chaque fois que lorsque l’utilisateur met fin à sa session sur le site Web de hello :

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

Il est important de toonotice qui hello requête mise à jour n’a pas besoin tooknow hello heure exacte à laquelle s’est produite lors de l’opération réelle de hello, ni comment les données d’historique seront conservées pour une analyse future. Les deux aspects sont gérées automatiquement par hello de base de données SQL Azure. Hello diagramme suivant illustre comment les données d’historique sont générées sur chaque mise à jour.

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a>Étape 3: Analyser les données historiques
Une fois que la gestion de version des tables temporelles par le système est activée, il vous suffit d’une seule requête pour analyser les données historiques. Dans cet article, nous allons sera fournir quelques exemples de scénarios courants analyse - toolearn tous les détails, Explorer différentes options introduites par Bonjour [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.

toosee hello top 10 utilisateurs classés par nombre de hello de pages web visitées à partir d’une heure, exécutez cette requête :

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

Vous pouvez facilement modifier cette requête tooanalyze hello visites un jour il y a un mois d’avance ou à tout moment dans hello précédente vous le souhaitez.

analyse de statistiques de base de tooperform pour hello jour précédent, utilisez hello l’exemple suivant :

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

toosearch pour les activités d’un utilisateur spécifique, dans un laps de temps, utilisez hello CONTAINED IN clause :

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

La visualisation graphique est particulièrement pratique pour les requêtes temporelles, car vous pouvez afficher les tendances et les modèles d’utilisation de façon intuitive très facilement :

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a>Évolution du schéma de table
En règle générale, vous devez schéma de table temporelle toochange hello pendant que vous faites le développement d’applications. Pour ce faire, il suffit d’exécuter les instructions ALTER TABLE régulières et base de données SQL Azure seront propagées correctement la table d’historique des modifications toohello. Hello script suivant montre comment vous pouvez ajouter des attributs supplémentaires pour le suivi :

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

De même, vous pouvez modifier la définition de colonne pendant que votre charge de travail est active :

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

Enfin, vous pouvez supprimer une colonne dont vous n’avez plus besoin.

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

Vous pouvez également utiliser plus tard [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange temporelle schéma de table pendant que vous êtes connecté toohello la base de données (mode en ligne) ou en tant que partie du projet de base de données hello (mode hors connexion).

## <a name="controlling-retention-of-historical-data"></a>Contrôle de la rétention des données historiques
Avec des tables temporelles avec version gérée par le système de table d’historique hello peut augmenter de taille de base de données hello plus de tables normales. Une table d’historique volumineuse et qui ne cesse de croître peut devenir un problème en raison des coûts de stockage toopure ainsi qu’imposant des performances sur l’interrogation temporelle. Par conséquent, le développement d’une stratégie de rétention de données pour la gestion des données dans la table d’historique hello est un aspect important de la planification et la gestion du cycle de vie hello de chaque table temporelle. Avec la base de données SQL Azure, vous avez hello méthodes pour la gestion des données d’historique dans la table temporelle hello suivantes :

* [Partitionnement de tables](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [Script de nettoyage personnalisé](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les tables temporelles, consultez la [documentation MSDN](https://msdn.microsoft.com/library/dn935015.aspx).
Visitez Channel 9 toohear un [réussite implémentation temporelle de client réel](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) et Espion un [live démonstration temporelle](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

