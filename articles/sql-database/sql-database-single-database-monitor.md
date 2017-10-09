---
title: "aaaMonitoring des performances de base de données dans la base de données SQL Azure | Documents Microsoft"
description: "En savoir plus sur les options de hello pour l’analyse de votre base de données avec Azure tools et des vues de gestion dynamique."
keywords: "analyse de base de données, performances des bases de données du cloud"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: a2e47475-c955-4a8d-a65c-cbef9a6d9b9f
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: b13771183d4ccf37f58e2fc518b9b14de38212dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-database-performance-in-azure-sql-database"></a>Analyse des performances d’une base de données dans une base de données SQL Azure
Analyse des performances hello d’une base de données SQL Azure démarre avec l’analyse de niveau de toohello relatif d’utilisation de ressources de hello des performances de base de données choisie. Analyse vous permet de déterminer si votre base de données a une capacité excédentaire ou rencontre des problèmes, car les ressources sont surexploités et ensuite décider s’il s’agit de niveau de performance de temps tooadjust hello et [niveau de service](sql-database-service-tiers.md) de votre base de données. Vous pouvez surveiller votre base de données à l’aide des outils graphiques Bonjour [portail Azure](https://portal.azure.com) ou à l’aide de SQL [vues de gestion dynamique](https://msdn.microsoft.com/library/ms188754.aspx).

## <a name="monitor-databases-using-hello-azure-portal"></a>Surveiller les bases de données à l’aide de hello portail Azure
Bonjour [portail Azure](https://portal.azure.com/), vous pouvez surveiller le taux d’utilisation de base de données unique en sélectionnant votre base de données en cliquant sur hello **analyse** graphique. Ceci fait apparaître un **métrique** fenêtre que vous pouvez modifier en cliquant sur hello **modifier le graphique** bouton. Ajoutez hello suivant des métriques :

* Pourcentage UC
* Pourcentage DTU
* Pourcentage E/S des données
* Pourcentage de la taille de la base de données

Une fois que vous avez ajouté ces métriques, vous pouvez continuer tooview dans hello **analyse** graphique avec plus de détails sur hello **métrique** fenêtre. Toutes les métriques de quatre affichent hello utilisation moyenne du pourcentage relatif toohello **DTU** de votre base de données. Consultez hello [niveaux de service](sql-database-service-tiers.md) article pour plus d’informations sur les dtu.

![Surveillance des niveaux de service des performances de la base de données.](./media/sql-database-service-tiers/sqldb_service_tier_monitoring.png)

Vous pouvez également configurer des alertes sur des métriques de performances hello. Cliquez sur hello **ajouter une alerte** bouton Bonjour **métrique** fenêtre. Suivez hello Assistant tooconfigure votre alerte. Vous avez hello option tooalert si les métriques hello dépassent un certain seuil ou si la métrique de hello tombe en dessous d’un certain seuil.

Par exemple, si vous pensez que la charge de travail hello sur toogrow de votre base de données, vous pouvez choisir tooconfigure une alerte par courrier électronique chaque fois que votre base de données atteint 80 % d’une des métriques de performances hello. Vous pouvez utiliser cela comme un toofigure avertissement précoce out lorsque vous disposez tooswitch toohello niveau de performance supérieur.

les mesures de performances Hello peuvent également vous aider à déterminer si vous êtes le niveau de performances inférieur en mesure de toodowngrade tooa. Supposons que vous utilisez une base de données Standard S2 et tous les afficher de métriques de performances qui hello en moyenne de base de données n’utilise pas plus de 10 % à un moment donné. Il est probable que cette base de données hello fonctionne bien en Standard S1. Toutefois, tenez compte des charges de travail qui connaissent des pics ou fluctuent avant d’apporter des tooa-niveau de performance inférieur hello décision toomove.

## <a name="monitor-databases-using-dmvs"></a>Analyser des bases de données à l’aide des vues de gestion dynamique
Hello mêmes métriques qui sont exposées dans le portail de hello sont également disponibles via des vues système : [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) Bonjour logique **master** base de données de votre serveur, et [sys.dm_db_ des statistiques des ressources](https://msdn.microsoft.com/library/dn800981.aspx) dans la base de données utilisateur hello. Utilisez **sys.resource_stats** si vous avez besoin toomonitor moins de données granulaires sur une période plus longue. Utilisez **sys.dm_db_resource_stats** si vous avez besoin de toomonitor données plus granulaires sur un plus petit intervalle de temps. Pour en savoir plus, consultez [Guide des performances de base de données SQL Azure](sql-database-single-database-monitor.md#monitor-resource-use).

> [!NOTE]
> **sys.dm_db_resource_stats** retourne un résultat vide quand elle est utilisée dans les éditions de base de données Web et Business, qui sont supprimées.
>
>

### <a name="monitor-resource-use"></a>Surveiller l’utilisation des ressources

Vous pouvez surveiller l’utilisation des ressources à l’aide de [SQL Database Query Performance Insight](sql-database-query-performance.md) et du [magasin de requêtes](https://msdn.microsoft.com/library/dn817826.aspx).

Vous pouvez également surveiller l’utilisation à l’aide de ces deux vues :

* [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)
* [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx)

#### <a name="sysdmdbresourcestats"></a>sys.dm_db_resource_stats
Vous pouvez utiliser hello [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) vue dans chaque base de données SQL. Hello **sys.dm_db_resource_stats** affiche le niveau de service récentes ressource utilisez données toohello relatif. Les pourcentages moyens d’UC, d’E/S des données, d’écritures du journal et de mémoire sont enregistrés toutes les 15 secondes et conservés pendant une heure.

Étant donné que cette vue fournit un aperçu plus granulaire de l’utilisation des ressources, utilisez d’abord **sys.dm_db_resource_stats** pour n’importe quelle analyse d’état actuel ou pour la résolution des problèmes. Par exemple, cette requête affiche la moyenne de hello et maximale de ressources utilisent pour la base de données actuelle hello sur hello dernière heure :

    SELECT  
        AVG(avg_cpu_percent) AS 'Average CPU use in percent',
        MAX(avg_cpu_percent) AS 'Maximum CPU use in percent',
        AVG(avg_data_io_percent) AS 'Average data I/O in percent',
        MAX(avg_data_io_percent) AS 'Maximum data I/O in percent',
        AVG(avg_log_write_percent) AS 'Average log write use in percent',
        MAX(avg_log_write_percent) AS 'Maximum log write use in percent',
        AVG(avg_memory_usage_percent) AS 'Average memory use in percent',
        MAX(avg_memory_usage_percent) AS 'Maximum memory use in percent'
    FROM sys.dm_db_resource_stats;  

Pour les autres requêtes, consultez les exemples de hello dans [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx).

#### <a name="sysresourcestats"></a>sys.resource_stats
Hello [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) vue Bonjour **master** base de données comporte des informations supplémentaires qui peuvent vous aider à surveiller les performances de hello de votre base de données SQL à son niveau de performances et de la couche de service spécifique . les données de salutation sont collectées toutes les 5 minutes et sont conservées pendant environ 35 jours. Cette vue est utile pour une analyse historique de plus long terme sur l’utilisation des ressources par votre base de données SQL.

Hello graphique suivant illustre hello utilisation des ressources du processeur pour une base de données Premium avec hello niveau de performance P2 pour chaque heure de la semaine. Ce graphique commence un lundi, affiche 5 journées de travail et affiche alors un week-end, cas moins importante sur l’application hello.

![Utilisation des ressources de base de données SQL](./media/sql-database-performance-guidance/sql_db_resource_utilization.png)

À partir des données de hello, cette base de données possède actuellement un pic de charge de l’UC simplement plus de 50 % processeur utiliser le niveau de performance relatif toohello P2 (MIDI le mardi). Si l’UC est hello un facteur dominant dans le profil de ressource de l’application hello, vous pouvez décider que P2 est hello droit tooguarantee de niveau de performances qui hello toujours les charges de travail correspond à. Si vous prévoyez une toogrow d’application au fil du temps, il est un toohave conseillé une mémoire tampon de ressources supplémentaire afin que l’application hello n’atteint jamais la limite du niveau de performance hello. Si vous augmentez le niveau de performance hello, vous pouvez éviter les erreurs visible par les clients qui peuvent se produire lorsqu’une base de données n’a suffisamment tooprocess les demandes d’alimentation efficacement, en particulier dans les environnements sensibles au temps de latence. Un exemple est une base de données qui prend en charge une application qui peint les pages Web en fonction des résultats hello d’appels de base de données.

Autres types d’applications peuvent interpréter hello même graphique différemment. Par exemple, si une application tente de données sur les salaires tooprocess chaque jour et a hello même graphique, ce type de modèle de « traitement par lot » peut faire correctement à un niveau de performance P1. Hello niveau de performance P1 a 100 dtu too200 de dtu par rapport au niveau de performance P2 de hello. Hello niveau de performance P1 offre des performances de hello moitié de hello niveau de performance P2. Par conséquent, 50 % d’utilisation de l’UC au niveau P2 correspond à 100 % d’utilisation de l’UC au niveau de performance P1. Si l’application hello n’a pas de délais d’attente, il peut concerner pas si un travail prend 2 heures ou 2,5 heures toofinish, si elle obtient fait aujourd'hui. Une application de cette catégorie peut probablement utiliser un niveau de performances P1. Vous pouvez tirer parti des faits hello qu’il n’y a des périodes au cours de la journée hello lorsque l’utilisation des ressources est moindre, afin que toute « période de pointe » peut déborder sur dans une des creux de hello plus tard dans la journée de hello. Hello niveau de performance P1 peut être approprié pour ce type d’application (et économies) tant que les travaux hello peuvent terminer à temps chaque jour.

Azure SQL Database consommées informations sur les ressources pour chaque base de données active Bonjour **sys.resource_stats** vue Hello **master** dans chaque serveur de base de données. données Hello dans la table de hello sont agrégées à des intervalles de 5 minutes. Avec les niveaux de service des basique, Standard et Premium d’hello, hello données peut prendre plus de 5 minutes tooappear dans la table de hello, par conséquent, ces données sont plus pratique pour l’analyse historique au lieu d’analyse de la proximité en temps réel. Hello de requête **sys.resource_stats** vue toosee hello historique récent d’une base de données et les toovalidate si réservation de hello choisis remis hello performances si nécessaire.

> [!NOTE]
> Vous devez être connecté toohello **master** base de données de votre logique tooquery de serveur de base de données SQL **sys.resource_stats** Bonjour exemple suivant.
> 
> 

Cet exemple vous montre comment les données hello dans cette vue sont exposées :

    SELECT TOP 10 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![vue de catalogue sys.resource_stats Hello](./media/sql-database-performance-guidance/sys_resource_stats.png)

Hello suivant montre différentes manières que vous pouvez utiliser hello **sys.resource_stats** catalogue vue tooget plus d’informations sur l’utilisation des ressources dans votre base de données SQL :

1. toolook à hello au-delà de ressource de la semaine utilisent pour userdb1 de base de données hello, vous pouvez exécuter cette requête :
   
        SELECT *
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND
              start_time > DATEADD(day, -7, GETDATE())
        ORDER BY start_time DESC;
2. tooevaluate degré de niveau de performance hello le mieux à votre charge de travail, vous avez besoin de toodrill vers le bas dans chaque aspect de métriques de ressources hello : UC, lectures, écritures, nombre de threads de travail et nombre de sessions. Voici un révisée à l’aide de la requête **sys.resource_stats** tooreport hello valeurs moyennes et maximales de ces métriques de ressource :
   
        SELECT
            avg(avg_cpu_percent) AS 'Average CPU use in percent',
            max(avg_cpu_percent) AS 'Maximum CPU use in percent',
            avg(avg_data_io_percent) AS 'Average physical data I/O use in percent',
            max(avg_data_io_percent) AS 'Maximum physical data I/O use in percent',
            avg(avg_log_write_percent) AS 'Average log write use in percent',
            max(avg_log_write_percent) AS 'Maximum log write use in percent',
            avg(max_session_percent) AS 'Average % of sessions',
            max(max_session_percent) AS 'Maximum % of sessions',
            avg(max_worker_percent) AS 'Average % of workers',
            max(max_worker_percent) AS 'Maximum % of workers'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
3. Avec ces informations sur les valeurs moyennes et maximales hello de chaque métrique de ressource, vous pouvez évaluer le degré votre charge de travail s’adapte à niveau de performance hello choisi. En règle générale, les valeurs moyennes de **sys.resource_stats** vous donner un toouse bonne ligne de base par rapport à la taille cible hello. Elles doivent constituer votre principale jauge de mesure. Pour obtenir un exemple, vous utilisez peut-être niveau de service Standard hello avec niveau de performance S2. moyenne de Hello utiliser des pourcentages pour les lectures d’e/s et UC écritures sont au-dessous de 40 %, nombre moyen de hello de threads de travail est inférieur à 50 et nombre moyen de hello de sessions est inférieur à 200. Hello niveau de performance S1 soit adéquat pour votre charge de travail. Il est facile toosee si votre base de données tient dans le processus de travail hello et les limites de session. toosee indique si une base de données s’adapte à un niveau inférieur à ce qui concerne les tooCPU, les lectures et écritures, divisez le nombre DTU de hello du niveau de performance inférieur hello en hello valeur DTU du niveau de performance actuel, puis multiplier le résultat de hello par 100 :
   
    **S1 DTU / S2 DTU * 100 = 20 / 50 * 100 = 40**
   
    résultat de Hello est la différence de performances relatives de hello entre deux niveaux de performance hello en pourcentage. Si cette quantité ne dépasse pas votre utilisation des ressources, votre charge de travail peut-être s’ajuster à niveau de performance inférieur hello. Toutefois, vous devez toolook à toutes les plages de valeurs d’utilisation de ressources et déterminez, en pourcentage, la fréquence à laquelle votre charge de travail de base de données tiendrait au niveau de performance inférieur hello. Hello requête suivante génère hello ajuster le pourcentage par dimension de ressource, en fonction de seuil hello de 40 pour cent que nous avons calculé dans cet exemple :
   
        SELECT
            (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log Write Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical Data IO Fit Percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    Selon votre objectif de niveau de service (SLO) de base de données, vous pouvez décider si votre charge de travail s’adapte à niveau de performance inférieur hello. Si votre charge de travail de base de données SLO est 99,9 % et hello requête précédente retourne les valeurs supérieures à 99,9 % pour tous les trois dimensions de ressources, votre charge de travail susceptible de correspond au niveau de performance inférieur hello.
   
    Recherche hello ajuster le pourcentage vous donne également un aperçu de si vous devez déplacer les toomeet au niveau suivant supérieur performances de toohello vos objectifs du contrat. Par exemple, userdb1 indique hello suivant l’utilisation du processeur pour hello semaine dernière :
   
   | Pourcentage moyen d’UC | Pourcentage maximum d’UC |
   | --- | --- |
   | 24,5 |100,00 |
   
    Hello moyenne du processeur est environ un quart de limite hello du niveau de performance hello, qui serait rentrent dans le niveau de performance hello de base de données hello. Toutefois, valeur maximale de hello montre que cette base de données hello atteint la limite de hello du niveau de performance hello. Avez-vous besoin de toomove toohello niveau de performance supérieur ? Examiner le nombre de fois où votre charge de travail atteint 100 pour cent et comparez-le charge de travail de base de données tooyour objectifs du contrat.
   
        SELECT
        (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log write fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical data I/O fit percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    Si cette requête retourne une valeur inférieure à 99,9 % pour une des dimensions de ressources hello trois, envisagez soit mobile toohello niveau de performance supérieur ou utiliser le paramétrage d’application techniques tooreduce hello charge sur la base de données SQL hello.
4. Cet exercice tient également compte de votre charge de travail prévue augmentation hello futures.

Pour les pools élastiques, vous pouvez surveiller les bases de données individuelles dans le pool de hello avec les techniques de hello décrites dans cette section. Mais vous pouvez également surveiller pool hello dans sa globalité. Pour plus d’informations, consultez l’article [Surveiller et gérer un pool élastique](sql-database-elastic-pool-manage-portal.md).


### <a name="maximum-concurrent-requests"></a>Nombre maximal de requêtes simultanées
nombre de hello toosee de demandes simultanées, exécutez cette requête Transact-SQL sur votre base de données SQL :

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R

la charge de travail hello tooanalyze d’une base de données SQL Server sur site, modifiez cette toofilter de requête sur la base de données spécifique hello souhaité tooanalyze. Par exemple, si vous avez une base de données locale nommée MyDatabase, cette requête Transact-SQL renvoie le nombre hello de demandes simultanées dans cette base de données :

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R
    INNER JOIN sys.databases D ON D.database_id = R.database_id
    AND D.name = 'MyDatabase'

Il s’agit simplement d’un instantané à un point unique dans le temps. tooget une meilleure compréhension de votre charge de travail et les exigences de demandes simultanées, vous devez toocollect nombreux échantillons au fil du temps.

### <a name="maximum-concurrent-logins"></a>Nombre maximal de connexions simultanées
Vous pouvez analyser vos modèles utilisateur et application tooget une idée de la fréquence de hello de connexions. Vous pouvez également exécuter des charges réelles dans toomake d’un environnement test sûr que vous rencontrez pas cela ou autres limites sur que les sujets abordés dans cet article. Il n’existe aucune requête ou vue de gestion dynamique qui peut vous indiquer le nombre de connexions simultanées ou un historique dédié.

Si plusieurs clients utilisent hello même chaîne de connexion, hello service s’authentifie à chaque connexion. Si 10 utilisateurs à se connectent simultanément tooa de base de données à l’aide de hello le même nom d’utilisateur et mot de passe, il n’y a 10 connexions simultanées. Cette limite s’applique uniquement toohello durée d’ouverture de session hello et d’authentification. Si les utilisateurs de hello 10 même vous connecter toohello de base de données séquentiellement, nombre de hello de connexions simultanées ne serait jamais supérieure à 1.

> [!NOTE]
> Actuellement, cette limite ne s’applique pas toodatabases dans les pools élastiques.
> 
> 

### <a name="maximum-sessions"></a>Nombre maximal de sessions
nombre de hello toosee de sessions actives en cours, exécutez cette requête Transact-SQL sur votre base de données SQL :

    SELECT COUNT(*) AS [Sessions]
    FROM sys.dm_exec_connections

Si vous analysez une charge de travail de SQL Server sur site, modifiez toofocus de requête hello sur une base de données spécifique. Cette requête permet de déterminer les besoins possibles d’une session de base de données hello si vous envisagez de déplacer tooAzure base de données SQL.

    SELECT COUNT(*)  AS [Sessions]
    FROM sys.dm_exec_connections C
    INNER JOIN sys.dm_exec_sessions S ON (S.session_id = C.session_id)
    INNER JOIN sys.databases D ON (D.database_id = S.database_id)
    WHERE D.name = 'MyDatabase'

Là encore, ces requêtes renvoient un nombre à un point dans le temps. Si vous regroupez plusieurs échantillons au fil du temps, vous aurez hello meilleure connaissance de votre session utiliser.

Pour l’analyse de la base de données SQL, vous pouvez obtenir des statistiques d’historique sur les sessions en interrogeant hello [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) affichage et examen hello **active_session_count** colonne. 
