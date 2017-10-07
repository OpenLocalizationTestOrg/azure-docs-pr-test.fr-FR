---
title: "aaaWhat sont les pools élastiques ? Gérer plusieurs bases de données SQL - Azure | Microsoft Docs"
description: "Gérez et mettez à l’échelle plusieurs bases de données SQL (des centaines et des milliers) avec des pools élastiques. Un prix unique pour des ressources que vous pouvez distribuer là où vous en avez besoin."
keywords: "plusieurs bases de données, ressources des bases de données, performances des bases de données"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: b46e7fdc-2238-4b3b-a944-8ab36c5bdb8e
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 07/31/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 2098d7817ebe1277b5c131421f23c00803ec78f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-pools-help-you-manage-and-scale-multiple-sql-databases"></a>Les pools élastiques vous aident à gérer et à mettre à l’échelle plusieurs bases de données SQL

Les pools élastiques SQL Database représentent une solution simple et rentable de gestion et de mise à l’échelle de plusieurs bases de données qui ont des demandes d’utilisation variables et imprévisibles. Hello et bases de données dans un pool élastique sur un seul serveur de base de données SQL Azure partagent un nombre défini de ressources ([unités de Transaction de base de données élastique](sql-database-what-is-a-dtu.md) (Edtu)) à un prix fixe. Les pools élastiques dans la base de données SQL Azure activer SaaS développeurs toooptimize hello prix des performances pour un groupe de bases de données dans un budget prescrit tout en offrant l’élasticité de performances pour chaque base de données.   

> [!NOTE]
> Les pools élastiques sont mis à la disposition générale dans toutes les régions Azure, à l’exception de l’Inde de l’Ouest, où ils sont actuellement en version préliminaire.  Les pools élastiques seront en disposition générale dès que possible dans cette région.
>

## <a name="what-are-sql-elastic-pools"></a>Que sont les pools élastiques SQL ? 

Les développeurs SaaS créent des applications qui reposent sur des couches de données à grande échelle composées de plusieurs bases de données. Un modèle d’application commun est tooprovision une base de données pour chaque client. Mais différents clients ont souvent des modèles d’utilisation imprévisibles et variables, et il est difficile de toopredict besoins en ressources hello de chaque utilisateur de base de données individuels. Vous disposez généralement de deux options : 

- Sur-approvisionner les ressources en fonction de l’utilisation maximale et payer trop, ou
- Toosave disposition incomplète de coût, à des frais de hello de performances et la satisfaction client pendant les heures de pointe. 

Pools élastiques résolvent ce problème en vous assurant que les bases de données d’obtenir les ressources de performances hello que dont ils ont besoin lorsqu’ils en ont besoin. Ils représentent un mécanisme simple d’allocation de ressources avec un budget prévisible. toolearn savoir plus sur les modèles de conception pour les applications SaaS à l’aide de pools élastiques, consultez [des modèles de conception pour les Applications SaaS mutualisée avec la base de données SQL Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Elastic-databases-helps-SaaS-developers-tame-explosive-growth/player]
>

Pools élastiques activer hello développeur toopurchase [unités de Transaction de base de données élastique](sql-database-what-is-a-dtu.md) (Edtu) pour un pool partagé par plusieurs bases de données tooaccommodate imprévisible des périodes d’utilisation par les bases de données individuelles. spécification d’eDTU Hello pour un pool est déterminée par l’utilisation d’agrégation hello de ses bases de données. nombre de Hello d’Edtu toohello disponible pool est contrôlé par budget de développeur hello. développeur de Hello ajoute simplement pool toohello de bases de données, définit le minimum de hello et Edtu maximale pour les bases de données hello et définit ensuite eDTU hello du pool hello en fonction de leur budget. Un développeur peut utiliser des pools de leur service à partir d’une entreprise bien établie tooa de démarrage adaptée à la croissance tooseamlessly mise à l’échelle croissante.

Dans un pool de hello, bases de données individuelles sont fournies hello flexibilité tooauto à l’échelle dans le jeu de paramètres. Sous une charge importante, une base de données peut consommer plus à la demande de toomeet Edtu. Les bases de données soumises à des charges légères en consomment moins, tandis que celles qui ne sont soumises à aucune charge n’en consomment pas du tout. Configuration des ressources pour le pool entier de hello plutôt que pour les bases de données uniques simplifie vos tâches de gestion. Ainsi, vous avez un budget prévisible pour le pool de hello. Edtu supplémentaires peut être ajoutées tooan pool existant sans interruption de la base de données, sauf que les bases de données hello doivent toobe déplacé hello tooprovide supplémentaire des ressources pour la réservation eDTU hello de calcul. De même, si les eDTU supplémentaires ne sont plus nécessaires, ils peuvent être supprimés à partir d’un pool existant à tout moment. Et vous pouvez ajouter ou soustraire pool toohello de bases de données. Si une base de données finit par sous-utiliser les ressources, retirez-la.

Vous pouvez créer et gérer un pool élastique, à l’aide de hello [portail Azure](sql-database-elastic-pool-manage-portal.md), [PowerShell](sql-database-elastic-pool-manage-powershell.md), [Transact-SQL](sql-database-elastic-pool-manage-tsql.md), [c#](sql-database-elastic-pool-manage-csharp.md), et l’API REST de hello. 

## <a name="when-should-you-consider-a-sql-database-elastic-pool"></a>Quand devez-vous envisager d’utiliser un pool élastique SQL Database ?

Les pools sont idéaux dans le cas de nombreuses bases de données avec des modèles d’utilisation spécifiques. Pour une base de données indiquée, ce modèle se caractérise par une faible utilisation moyenne avec des pics d'utilisation relativement rares.

Hello plusieurs bases de données vous pouvez ajouter hello de pool tooa supérieur que deviennent d’épargne. Selon votre modèle d’utilisation de l’application, il est économies toosee possibles avec un minimum de deux bases de données S3.  

vous aident à comprendre les sections suivantes de Hello comment tooassess si votre regroupement spécifique des bases de données peut tirer parti dans un pool. Hello exemples utilisent les pools Standard mais hello mêmes principes s’appliquent également tooBasic et pools de Premium.

### <a name="assessing-database-utilization-patterns"></a>Évaluation des modèles d'utilisation de base de données

Hello figure suivante montre un exemple de base de données qui prend beaucoup de temps pour inactif, mais également régulièrement des pics se produisent avec l’activité. Il s’agit d’un modèle d’utilisation particulièrement adapté à un pool :

   ![une base de données unique adaptée à un pool](./media/sql-database-elastic-pool/one-database.png)

Pourquoi illustré délai de cinq minutes, pics DB1 des too90 Udbd, mais son utilisation moyenne totale est inférieure à cinq dtu. Un niveau de performance est de S3 requis toorun cette charge de travail dans une base de données, mais cela laisse la plupart des ressources de hello inutilisé pendant les périodes de faible activité.

Un pool autorise ces toobe dtu inutilisés partagés entre plusieurs bases de données et réduit ainsi le coût de nécessaires et global de la dtu hello.

S’appuyant sur l’exemple précédent de hello, supposons qu’il existe des bases de données supplémentaires avec des modèles d’utilisation similaires en tant que DB1. Hello deux figures ci-dessous hello l’utilisation des quatre bases de données et 20 bases de données sont organisées en couches sur hello même graphique nature de non-chevauchement tooillustrate hello de leur utilisation dans le temps :

   ![quatre bases de données avec un modèle d’utilisation adapté à un pool](./media/sql-database-elastic-pool/four-databases.png)

  ![vingt bases de données avec un modèle d’utilisation adapté à un pool](./media/sql-database-elastic-pool/twenty-databases.png)

utilisation de DTU d’agrégation Hello sur toutes les bases de données de 20 est illustrée par la ligne hello noir Bonjour précédant figure. Cela montre que l’utilisation de DTU d’agrégation hello jamais dépasse 100 dtu et indique que 20 bases de données hello peuvent partager des 100 Edtu pendant cette période. Cela entraîne une réduction de 20 x en dtu et un 13 x prix baisse tooplacing chaque des bases de données hello en S3 des niveaux de performances pour les bases de données uniques.

Cet exemple est idéal pour hello suivant raisons :

* Il existe de grandes différences entre les pics d’utilisation et l'utilisation moyenne par base de données.  
* pics d’utilisation Hello pour chaque base de données se produit à différents moments dans le temps.
* Les eDTU sont partagées entre plusieurs bases de données.

prix Hello d’un pool est une fonction d’Edtu de pool hello. Alors que le prix unitaire hello eDTU pour un pool est 1,5 fois supérieure à UnitPrice hello DTU pour une base de données, **Edtu de pool peut être partagé par plusieurs bases de données et moins Edtu total est nécessaires**. Ces différences de tarification et de partage eDTU constituent hello de potentiel d’économies de prix hello qui peuvent fournir des pools.  

Hello suivants règles générales liées toodatabase nombre et la base de données utilisation de l’aide tooensure offrant un pool réduit le coût par rapport toousing les niveaux de performance pour les bases de données uniques.

### <a name="minimum-number-of-databases"></a>Nombre minimal de bases de données

Si somme hello Hello dtu des niveaux de performance pour les bases de données uniques est plus de 1,5 x Edtu hello nécessaire pour le pool de hello, un pool élastique est plus rentable. Pour plus d’informations sur les tailles disponibles, consultez l’article [Limites relatives aux eDTU et au stockage pour les pools et bases de données élastiques](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

***Exemple***<br>
Au moins deux bases de données S3 ou des bases de données S0 au moins 15 sont nécessaires pour un toobe de pool 100 eDTU plus économiques que l’utilisation des niveaux de performances pour les bases de données uniques.

### <a name="maximum-number-of-concurrently-peaking-databases"></a>Nombre maximal de bases de données connaissant un pic simultané

En partageant des Edtu, pas toutes les bases de données dans un pool peuvent utiliser simultanément les Edtu de limite toohello disponible lors de l’utilisation des niveaux de performances pour les bases de données uniques. Hello des bases de données moins pic simultanément, hello eDTU du pool hello inférieur peut être ensemble et hello que plus économique hello pool devient. En général, pas plus que 2/3 (ou 67 %) des bases de données hello dans le pool de hello doivent monter simultanément tootheir eDTU limitent.

***Exemple***<br>
coûts tooreduce pour trois bases de données S3 dans un pool eDTU 200, au plus deux de ces bases de données simultanément pics peuvent dans leur utilisation. Sinon, si plus de deux de ces quatre bases de données S3 monter simultanément, pool de hello aurait toomore toobe taille de 200 Edtu. Si le pool de hello est redimensionné toomore à 200 Edtu, plusieurs bases de données S3 devez toobe ajouté coûts de tookeep toohello pool inférieurs à des niveaux de performance des bases de données uniques.

Notez que cet exemple ne tient pas compte de l’utilisation des autres bases de données dans le pool de hello. Si toutes les bases de données ont une utilisation à un moment donné dans le temps, puis inférieure à 2/3 (ou 67 %) des bases de données hello pics peuvent simultanément.

### <a name="dtu-utilization-per-database"></a>Utilisation de DTU par base de données
Une grande différence entre les heures de pointe de hello et utilisation moyenne d’une base de données indique de longues périodes de faible utilisation et de courtes périodes d’utilisation intensive. Ce modèle d'utilisation est idéal pour partager des ressources entre les bases de données. Une base de données doit être envisagée pour un pool quand son pic d’utilisation est environ 1,5 fois supérieur à son utilisation moyenne.

***Exemple***<br>
Une base de données S3 pics too100 dtu et utilise en moyenne de 67 dtu ou inférieure est un bon candidat pour le partage des Edtu dans un pool. Vous pouvez également une base de données S1 pics too20 dtu et utilise en moyenne de 13 dtu ou inférieure est un bon candidat pour un pool.

## <a name="how-do-i-choose-hello-correct-pool-size"></a>Comment choisir la taille du pool approprié hello ?

taille de meilleures de Hello pour un pool varie selon les Edtu d’agrégation hello et ressources de stockage nécessaires pour toutes les bases de données dans le pool de hello. Cela implique de déterminer hello plus grand des éléments suivants de hello :

* Dtu maximales utilisées par toutes les bases de données dans le pool de hello.
* Octets de stockage maximale utilisées par toutes les bases de données dans le pool de hello.

Pour plus d’informations sur les tailles disponibles, consultez l’article [Limites relatives aux eDTU et au stockage pour les pools et bases de données élastiques](#what-are-the-resource-limits-for-elastic-pools).

Base de données SQL prend la valeur hello historiques l’utilisation des ressources de bases de données dans un serveur de base de données SQL existant automatiquement et recommande la configuration du pool approprié hello Bonjour portail Azure. Dans les recommandations toohello addition, une expérience intégrée estime l’utilisation des eDTU hello pour un groupe de bases de données sur le serveur de hello personnalisé. Ainsi, vous toodo une analyse « what-if » par l’ajout du pool toohello de bases de données et suppression d’analyse de l’utilisation des ressources tooget et dimensionnement des conseils avant de valider vos modifications de manière interactive. Pour afficher une procédure, consultez [Surveiller, gérer et dimensionner un pool élastique](sql-database-elastic-pool-manage-portal.md).

Dans les cas où vous ne pouvez pas utiliser les outils, suivant hello pas à pas peut vous aider à estimer si un pool est plus économique que les bases de données uniques :

1. Estimer Edtu hello nécessaire pour le pool de hello comme suit :

   MAX(<*nombre total de bases de données* X *utilisation DTU moyenne par base de données*>,<br>
   <*Nombre de bases de données connaissant un pic simultané* X *utilisation DTU maximale par base de données*)
2. Estimez l’espace de stockage hello nécessaire pour le pool de hello en ajoutant le nombre de hello d’octets nécessaires pour toutes les bases de données hello dans le pool de hello. Déterminent ensuite la taille du pool eDTU hello qui fournit cette quantité de stockage. Pour connaître les limites de stockage du pool en fonction de la taille du pool d’eDTU, consultez l’article [Limites relatives aux eDTU et au stockage pour les pools et bases de données élastiques](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).
3. Prendre hello plus grand de hello eDTU estimations de l’étape 1 et l’étape 2.
4. Consultez hello [page de tarification de la base de données SQL](https://azure.microsoft.com/pricing/details/sql-database/) et rechercher de pool d’eDTU hello plus petite taille est supérieure à estimation hello depuis l’étape 3.
5. Comparer les prix de pool de hello du prix de toohello étape 5 de l’utilisation des niveaux de performance appropriés hello pour les bases de données uniques.

### <a name="changing-elastic-pool-resources"></a>Modification des ressources de pool élastique

Vous pouvez augmenter ou diminuer le pool élastique hello ressources tooan disponibles selon les besoins en ressources.

* La modification d’Edtu de min hello par base de données ou max Edtu par base de données généralement se termine dans 5 minutes ou moins.
* Modification des Edtu hello par pool dépend hello total de l’espace utilisé par toutes les bases de données dans le pool de hello. Ce processus prend en moyenne 90 minutes au maximum, pour chaque tranche de 100 Go. Par exemple, si hello l’espace total utilisé par toutes les bases de données dans le pool de hello est 200 Go, puis hello attendu de latence de modification hello eDTU du pool par pool est de 3 heures au maximum.

## <a name="what-are-hello-resource-limits-for-elastic-pools"></a>Quelles sont les limites des ressources hello pour les pools élastiques ?

Hello les tableaux suivants décrire les limites des ressources hello de pools élastiques.  Notez que les limites des ressources hello de bases de données individuelles dans les pools élastiques ne sont généralement hello même que pour les bases de données uniques en dehors des pools en fonction de dtu et le niveau de service hello.  Par exemple, travailleurs simultanées max de hello pour une base de données S2 est 120 threads de travail.  Par conséquent, hello max simultanées traitements pour une base de données dans un pool Standard est également une 120 workers si hello max DTU par base de données dans le pool de hello est 50 dtu (qui est équivalent tooS2).

[!INCLUDE [SQL DB service tiers table for elastic pools](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Si tous les dtu d’un pool élastique sont utilisés, chaque base de données dans le pool de hello reçoit une quantité égale de requêtes tooprocess de ressources.  Hello service de base de données SQL fournit équité entre bases de données en s’assurant qu’égales tranches de temps de calcul du partage des ressources. Respect de partage des ressources de pool élastique sont en outre tooany quantité de ressources garanties tooeach de base de données lorsque hello nombre minimal de DTU par base de données a une valeur non nulle de tooa.

### <a name="database-properties-for-pooled-databases"></a>Propriétés de base de données pour les bases de données mises en pool

Hello tableau suivant décrit les propriétés de hello pour les bases de données mis en pool.

| Propriété | Description |
|:--- |:--- |
| Nombre maximal d’eDTU par base de données |nombre maximal de Hello des Edtu qui utilisent une base de données dans le pool de hello, si disponibles basées sur l’utilisation par d’autres bases de données dans le pool de hello.  Le nombre maximal d’eDTU par base de données n’est pas une garantie concernant l’octroi des ressources pour une base de données.  Ce paramètre est un paramètre global qui s’applique tooall des bases de données dans le pool de hello. Définir max Edtu par base de données toohandle suffisamment élevée des pics d’utilisation de base de données. Une certaine de sollicitation excessive est attendue, car le pool de hello suppose généralement des modèles d’utilisation de sauvegardes à chaud et à froid pour bases de données où toutes les bases de données ne sont pas commencé simultanément. Par exemple, supposons que hello utilisation maximale par base de données est 20 Edtu et seulement 20 % de hello 100 bases de données hello pool sont utilisation maximale de hello même temps.  Si eDTU hello max par base de données too20 Edtu, il est pool de hello tooovercommit raisonnable par 5 fois et d’Edtu de hello ensemble par pool too400. |
| Nombre minimal d’eDTU par base de données |nombre minimal de Hello d’edtu qu’une base de données dans le pool de hello est assuré.  Ce paramètre est un paramètre global qui s’applique tooall des bases de données dans le pool de hello. Hello des eDTU minimale par base de données peut être définie too0 et il est également hello valeur par défaut. Cette propriété a la valeur tooanywhere entre 0 et hello utilisation moyenne eDTU par base de données. produit Hello du nombre de hello de bases de données dans le pool de hello et d’Edtu de min hello par base de données ne peut pas dépasser Edtu hello par pool.  Par exemple, si un pool a 20 bases de données et hello nombre minimal d’eDTU par base de données définie too10 Edtu, Edtu hello par pool doit être au moins aussi grande que 200 Edtu. |
| Espace de stockage de données maximal par base de données |Hello maximale de stockage pour une base de données dans un pool. Mis en pool de bases de données partagent du stockage du pool, stockage de base de données est limitée toohello plus petit de stockage du pool restant et de stockage maximale par base de données. Espace de stockage max. par base de données fait référence toohello la taille maximale des fichiers de données hello et n’inclut pas d’espace de hello utilisé par les fichiers journaux. |
|||

## <a name="using-other-sql-database-features-with-elastic-pools"></a>Utilisation d’autres fonctionnalités SQL Database avec des pools élastiques

### <a name="elastic-jobs-and-elastic-pools"></a>Travaux élastiques et pools élastiques

Un pool simplifie les tâches de gestion grâce à l’exécution des scripts dans des **[tâches élastiques](sql-database-elastic-jobs-overview.md)**. Un travail élastique élimine pratiquement le caractère fastidieux d’un nombre élevé de bases de données. toobegin, consultez [prise en main de travaux élastique](sql-database-elastic-jobs-getting-started.md).

Pour en savoir plus sur les autres outils de base de données permettant d’utiliser plusieurs bases de données, consultez l’article [Montée en charge avec la base de données SQL Azure](sql-database-elastic-scale-introduction.md).

### <a name="business-continuity-options-for-databases-in-an-elastic-pool"></a>Options de continuité de l’activité pour les bases de données d’un pool élastique
Mis en pool de bases de données généralement prise en charge hello même [les fonctionnalités de continuité d’activité](sql-database-business-continuity.md) qui sont des bases de données toosingle disponibles.

- **Point de restauration dans le temps**: Point de restauration de temps utilise les sauvegardes de base de données automatique toorecover une base de données dans un point spécifique de pool tooa dans le temps. Voir [Limite de restauration dans le temps](sql-database-recovery-using-backups.md#point-in-time-restore)

- **Géo-restauration**: géo-restauration fournit l’option de récupération par défaut hello lorsqu’une base de données n’est pas disponible en raison d’un incident dans la région de hello où la base de données hello est hébergé. Consultez [restaurer une base de données SQL Azure ou le basculement de tooa secondaire](sql-database-disaster-recovery.md)

- [Géoréplication active](sql-database-geo-replication-overview.md) : pour les applications qui ont des exigences de récupération plus agressives que ce qu’offre la géorestauration, configurez la **géoréplication active**.

## <a name="manage-sql-database-elastic-pools-using-hello-azure-portal"></a>Gérer les pools élastiques de base de données SQL à l’aide de hello portail Azure

### <a name="creating-a-new-sql-database-elastic-pool-using-hello-azure-portal"></a>Créer un nouveau pool élastique de base de données SQL à l’aide de hello portail Azure

Il existe deux façons de que créer un pool élastique Bonjour portail Azure. Vous pouvez le faire à partir de zéro si vous savez que le programme d’installation de hello pool que vous voulez, ou commencer par la recommandation du service de hello. Base de données SQL a une intelligence intégrée qui recommande une configuration de pool élastique, s’il est plus économique en fonction de hello au-delà de télémétrie d’utilisation pour vos bases de données. 

Création d’un pool élastique d’un existant **server** panneau dans le portail de hello est hello plus simple façon toomove bases de données existantes dans un pool élastique. Vous pouvez également créer un pool élastique en recherchant **pool élastique SQL** Bonjour **Marketplace** ou en cliquant sur **+ ajouter** Bonjour **pools élastiques de SQL**parcourir le panneau. Vous êtes en mesure de toospecify un serveur nouveau ou existant à ce pool de mise en service de flux de travail.

> [!NOTE]
> Vous pouvez créer plusieurs pools sur un serveur, mais vous ne pouvez ajouter des bases de données à partir de différents serveurs dans hello même pool.
>  

Hello niveau de tarification du pool détermine hello fonctionnalités ELASTIQUES toohello disponibles dans le pool de hello et hello le nombre maximal d’Edtu (eDTU MAX) et de base de données de stockage (Go) disponible tooeach. Pour plus d’informations, voir [Niveaux de service](#edtu-and-storage-limits-for-elastic-pools).

Cliquez sur le niveau de tarification hello toochange de pool de hello **niveau tarifaire**, cliquez sur hello tarification de votre choix, puis cliquez sur **sélectionnez**.

> [!IMPORTANT]
> Une fois que vous choisissez hello tarification et valider vos modifications en cliquant sur **OK** dans la dernière étape de hello, vous ne serez pas hello toochange en mesure de tarification du pool de hello. toochange hello niveau tarifaire pour un pool élastique existant, créez un pool élastique dans le niveau de tarification souhaité hello et migrez hello bases de données toothis nouveau pool.
>

Si les bases de données hello avec lequel vous travaillez ont suffisamment de télémétrie d’utilisation historiques, hello **estimée des eDTU et l’utilisation de Go** graphique et hello **réel eDTU utilisation** toohelp de mise à jour de graphique à barres vous vérifiez la configuration décisions. En outre, les service hello peut donner un toohelp de message de recommandation vous redimensionner hello pool.

Hello service de base de données SQL évalue l’historique d’utilisation et recommande un ou plusieurs pools lorsqu’il est plus économique que l’utilisation de bases de données uniques. Chaque recommandation est configurée avec un sous-ensemble unique de bases de données du serveur hello ajuster le pool de hello.

![pool recommandé](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

recommandation de pool Hello comprend :

- Un niveau de tarification pour le pool hello (Basic, Standard, Premium ou Premium RS)
- Valeur **eDTU du pool** appropriée (également appelée eDTU max par pool)
- Hello **eDTU MAX** et **eDTU Min** par base de données
- liste Hello des bases de données recommandés pour le pool de hello

> [!IMPORTANT]
> service de Hello prend hello 30 derniers jours de données de télémétrie en compte lorsque vous recommander des pools. Pour une base de données toobe considéré comme un candidat pour un pool élastique, il doit exister au moins 7 jours. Les bases de données qui figurent déjà dans un pool élastique ne sont pas considérées comme candidates pour les recommandations de pool élastique.
>

Hello évalue les besoins en ressources et rentabilité de déplacement hello unique bases de données dans chaque niveau de service dans des pools de hello même couche. Par exemple, toutes les bases de données Standard d’un serveur sont évaluées pour leur compatibilité avec un pool élastique Standard. Cela signifie que le service de hello ne fait pas de recommandations entre les couches tels que le déplacement d’une base de données Standard dans un pool Premium.

Après avoir ajouté un pool toohello de bases de données, les recommandations sont générées dynamiquement selon hello historique de l’utilisation des bases de données hello que vous avez sélectionné. Ces recommandations sont affichées dans hello eDTU et graphique d’utilisation Go et une bannière de recommandation haut hello hello **configurer pool** panneau. Ces recommandations sont tooassist prévue dans la création d’un pool élastique optimisé pour vos bases de données spécifiques.

![Recommandations dynamiques](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

### <a name="manage-and-monitor-an-elastic-pool"></a>Gérer et surveiller un pool élastique

Bonjour portail Azure, vous pouvez surveiller l’utilisation de hello un pool élastique et bases de données hello dans ce pool. Vous pouvez également effectuer un ensemble de modifications pool élastique de tooyour et envoyer toutes les modifications apportées à hello même temps. Ces modifications incluent l’ajout ou la suppression de bases de données, ainsi que le changement des paramètres du pool élastique ou des bases de données.

Hello graphique suivant montre un pool élastique exemple. affichage de Hello inclut :

*  Graphiques de surveillance de l’utilisation des ressources de pool élastique de hello et bases de données hello contenus dans le pool de hello.
*  Hello **configurer** pool bouton toomake modifie le pool élastique de toohello.
*  Hello **créer la base de données** bouton qui crée une base de données et l’ajoute toohello pool élastique en cours.
*  Des tâches élastiques, qui vous aident à gérer un grand nombre de bases de données en exécutant des scripts Transact SQL sur toutes les bases de données d’une liste.

![Affichage du pool](./media/sql-database-elastic-pool-manage-portal/basic.png)

Vous pouvez accéder tooa pool particulier toosee son utilisation des ressources. Par défaut, le pool de hello est l’utilisation de stockage et d’eDTU tooshow configuré pour hello dernière heure. graphique de Hello peut être configuré tooshow différentes métriques sur différentes périodes. Cliquez sur hello **l’utilisation des ressources** graphique sous **analyse du pool élastique** tooshow une vue détaillée de hello spécifié métriques sur la fenêtre de temps spécifié hello.

![Surveillance du pool élastique](./media/sql-database-elastic-pool-manage-portal/basic-2.png)

![Volet Metric](./media/sql-database-elastic-pool-manage-portal/metric.png)

### <a name="toocustomize-hello-chart-display"></a>affichage du graphique hello toocustomize

Vous pouvez modifier les graphique hello et hello métriques toodisplay autres métriques telles que le pourcentage du processeur, pourcentage de données e/s et pourcentage d’e/s de journal utilisé.

![Cliquez sur Modifier](./media/sql-database-elastic-pool-manage-portal/edit-metric.png)

Sur hello **modifier le graphique** formulaire, vous pouvez sélectionner une plage de temps (heure, l’heure actuelle, ou semaine), ou cliquez sur **personnalisé** tooselect toute plage de dates hello deux dernières semaines. Vous pouvez choisir entre une barre ou un graphique en courbes, puis sélectionnez hello ressources toomonitor.

> [!Note]
> Seul graphique des métriques avec hello même unité de mesure peut être affichée dans hello en hello même temps. Par exemple, si vous sélectionnez « pourcentage d’eDTU » puis vous pouvez uniquement sélectionner d’autres mesures avec pourcentage en tant qu’unité hello.
>

[Cliquez sur Modifier](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

### <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>Gérer et surveiller des bases de données dans un pool élastique

Il est également possible de surveiller des bases de données individuelles pour identifier des problèmes potentiels. Sous **Surveillance de la base de données élastique**, vous trouverez un graphique qui affiche les métriques de cinq bases de données. Par défaut, hello graphique affiche hello 5 bases de données dans le pool de hello par utilisation moyenne eDTU Bonjour dernière heure. 

![Surveillance du pool élastique](./media/sql-database-elastic-pool-manage-portal/basic-3.png)

Cliquez sur hello **utilisation des eDTU pour les bases de données pour la dernière heure de hello** sous **analyse de la base de données élastique**. Cette opération ouvre **l’utilisation des ressources de base de données** et fournit une vue détaillée de l’utilisation de base de données hello dans le pool de hello. À l’aide de la grille hello dans la partie inférieure de hello du Panneau de hello, vous pouvez sélectionner des bases de données dans hello pool toodisplay son utilisation dans le graphique de hello (des bases de données too5). Vous pouvez également personnaliser la fenêtre hello métriques et l’heure affichée dans le graphique de hello en cliquant sur **modifier le graphique**.

![Panneau Database Resource Utilization (Utilisation des ressources des bases de données)](./media/sql-database-elastic-pool-manage-portal/db-utilization.png)

### <a name="toocustomize-hello-view"></a>affichage de hello toocustomize

Vous pouvez modifier le graphique de hello tooselect une plage de temps (après les heures ou dernières 24 heures), ou cliquez sur **personnalisé** tooselect un autre jour Bonjour au-delà de 2 semaines toodisplay.

![Cliquez sur Modifier le graphique](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

![Cliquez sur Personnalisé](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

Vous pouvez également cliquer sur hello **comparer les bases de données par** tooselect de liste déroulante un toouse métrique différents lors de la comparaison des bases de données.

![Modifier le graphique de hello](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>toomonitor de bases de données tooselect

Dans la liste base de données hello hello **l’utilisation des ressources de base de données** panneau, vous pouvez trouver des bases de données particulières en consultant les pages hello dans la liste de hello ou en tapant dans nom hello d’une base de données. Utilisez hello case à cocher tooselect hello base de données.

![Recherchez des bases de données toomonitor](./media/sql-database-elastic-pool-manage-portal/select-dbs.png)


### <a name="add-an-alert-tooan-elastic-pool-resource"></a>Ajouter une ressource de pool élastique tooan alerte

Vous pouvez ajouter des règles tooan élastique pool d’envoyer un courrier électronique toopeople alerte chaînes tooURL points de terminaison ou lorsque le pool élastique de hello atteint un seuil d’utilisation que vous avez configurée.

**tooadd une ressource tooany alerte :**

1. Cliquez sur hello **l’utilisation des ressources** hello de tooopen graphique **métrique** panneau, cliquez sur **ajouter une alerte**, puis remplissez les informations de hello Bonjour **ajouter une alerte règle** blade (**ressource** est configuré automatiquement de pool de hello toobe avec lequel vous travaillez).
2. Tapez un **nom** et **Description** qui identifie les tooyou alerte hello et les destinataires de hello.
3. Choisissez un **métrique** que vous souhaitez tooalert à partir de la liste de hello.

    graphique de Hello affiche dynamiquement l’utilisation des ressources pour cette métrique toohelp que vous choisissez un seuil.

4. Choisissez une **condition** (supérieur à, inférieur à, etc.) et un **seuil**.
5. Choisissez un **période** de temps qui hello métrique règle doit être satisfaite avant de déclencheurs d’alerte hello.
6. Cliquez sur **OK**.

Pour plus d'informations, voir [Créer des alertes SQL Database dans le portail Azure](sql-database-insights-alerts-portal.md).

### <a name="move-a-database-into-an-elastic-pool"></a>Déplacer une base de données dans un pool élastique

Vous pouvez ajouter ou supprimer des bases de données dans un pool existant. bases de données Hello peuvent être dans d’autres pools. Toutefois, vous pouvez uniquement ajouter des bases de données qui sont sur hello même serveur logique.

 ![Cliquez sur Configurer le pool](./media/sql-database-elastic-pool-manage-portal/configure-pool.png)

![Cliquez sur Ajouter toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)

![Sélectionnez les bases de données tooadd](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

![Ajouts de pool en attente](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

![Cliquez sur Enregistrer.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="move-a-database-out-of-an-elastic-pool"></a>Déplacer une base de données hors d’un pool élastique

![liste des bases de données](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

![liste des bases de données](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

![Afficher l’aperçu d’ajout et de suppression de base de données](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

![Cliquez sur Enregistrer.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="change-performance-settings-of-an-elastic-pool"></a>Modifier les paramètres de performances d'un pool élastique

Lorsque vous analysez l’utilisation des ressources d’un pool élastique hello, vous pouvez constater que quelques ajustements sont nécessaires. Peut-être pool de hello doit être modifiée dans les limites de performances ou le stockage hello. Éventuellement, vous souhaitez que les paramètres de base de données toochange hello dans le pool de hello. Vous pouvez modifier le programme d’installation de hello du pool hello à n’importe quel moment tooget hello meilleur compromis entre les performances et le coût. Pour plus d’informations, consultez l’article [Quand utiliser un pool élastique ?](sql-database-elastic-pool.md).

toochange hello Edtu limites ou de stockage par pool et Edtu par base de données :

![Utilisation des ressources du pool élastique](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

![Mise à jour d’un pool élastique et nouveau coût mensuel](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="manage-sql-database-elastic-pools-using-powershell"></a>Gérer des pools élastiques SQL Database à l’aide de PowerShell

toocreate et de gérer les pools élastiques de base de données SQL Azure PowerShell, utilisez hello suivant d’applets de commande PowerShell. Si vous avez besoin de tooinstall ou mise à niveau de PowerShell, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps). toocreate et gérer des bases de données, les serveurs et les règles de pare-feu, consultez [créer et gérer les serveurs de base de données SQL Azure et les bases de données à l’aide de PowerShell](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-powershell). 

> [!TIP]
> Pour plus d’exemples de scripts PowerShell, consultez [créer des pools élastiques et déplacer les bases de données entre les pools et hors d’un pool à l’aide de PowerShell](scripts/sql-database-move-database-between-pools-powershell.md) et [toomonitor d’utiliser PowerShell et l’échelle un élastique SQL pool dans la base de données SQL Azure](scripts/sql-database-monitor-and-scale-pool-powershell.md).
>

| Applet de commande | Description |
| --- | --- |
|[New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool)|Crée un pool de bases de données élastique sur un serveur SQL logique.|
|[Get-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/get-azurermsqlelasticpool)|Obtient les pools élastiques et leurs valeurs de propriété sur un serveur SQL logique.|
|[Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool)|Modifie les propriétés d’un pool de bases de données élastique sur un serveur SQL logique.|
|[Remove-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/remove-azurermsqlelasticpool)|Supprime un pool de bases de données élastique sur un serveur SQL logique.|
|[Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity)|Obtient l’état hello d’opérations sur un pool élastique sur un serveur SQL logique.|
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Crée une base de données dans un pool existant ou en tant que base de données seule. |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Obtient une ou plusieurs bases de données.|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Définit les propriétés d’une base de données, ou déplace une base de données existante dans un pool élastique, en dehors de celui-ci ou entre des pools élastiques.|
|[Remove-AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase)|Supprime une base de données.|

> [!TIP]
> La création de plusieurs bases de données dans un pool élastique peut prendre un temps quand terminé à l’aide du portail de hello ou des applets de commande PowerShell créer uniquement une seule base de données à la fois. Création de tooautomate dans un pool élastique, consultez [CreateOrUpdateElasticPoolAndPopulate](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).
>

## <a name="manage-sql-database-elastic-pools-using-hello-azure-cli"></a>Gérer les pools élastiques de base de données SQL à l’aide de hello CLI d’Azure

toocreate et gérer les pools élastiques de base de données SQL avec hello [CLI d’Azure](/cli/azure/overview), utilisez hello suivante [base de données SQL Azure CLI](/cli/azure/sql/db) commandes. Hello d’utilisation [Cloud Shell](/azure/cloud-shell/overview) toorun hello CLI dans votre navigateur, ou [installer](/cli/azure/install-azure-cli) sur Windows, Linux ou macOS. 

> [!TIP]
> Pour plus d’exemples de scripts CLI d’Azure, consultez [toomove de CLI d’utiliser une base de données SQL Azure dans un pool élastique SQL](scripts/sql-database-move-database-between-pools-cli.md) et [CLI d’Azure utilisation tooscale un pool élastique SQL dans la base de données SQL Azure](scripts/sql-database-scale-pool-cli.md).
>

| Applet de commande | Description |
| --- | --- |
|[az sql elastic-pool create](/cli/azure/sql/elastic-pool#create)|Crée un pool élastique.|
|[az sql elastic-pool list](/cli/azure/sql/elastic-pool#list)|Renvoie une liste de pools élastiques dans un serveur.|
|[az sql elastic-pool list-dbs](/cli/azure/sql/elastic-pool#list-dbs)|Renvoie une liste des bases de données dans un pool élastique.|
|[az sql elastic-pool list-editions](/cli/azure/sql/elastic-pool#list-editions)|Inclut également les paramètres DTU de pool, les limites de stockage et les paramètres par base de données disponibles. Dans les commentaires de tooreduce de commande, les limites de stockage supplémentaire et par base de données des paramètres sont masqués par défaut.|
|[az sql elastic-pool update](/cli/azure/sql/elastic-pool#update)|Met à jour un pool élastique.|
|[az sql elastic-pool delete](/cli/azure/sql/elastic-pool#delete)|Supprime le pool élastique de hello.|

## <a name="manage-sql-database-elastic-pools-using-transact-sql"></a>Gérer des pools élastiques SQL Database à l’aide de Transact-SQL

toocreate et déplacement des bases de données dans les pools élastiques existants ou tooreturn d’informations sur un pool élastique de base de données SQL avec Transact-SQL, utilisez hello suivant de commandes T-SQL. Vous pouvez émettre ces commandes à l’aide du portail Azure, de hello [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), ou tout autre programme qui peut se connecter le serveur de base de données SQL Azure tooan et passer Transact-SQL commandes. toocreate et gérer des bases de données, les serveurs et les règles de pare-feu, consultez [créer et gérer les serveurs de base de données SQL Azure et les bases de données à l’aide de Transact-SQL](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-transact-sql).

> [!IMPORTANT]
> Vous ne pouvez pas créer, mettre à jour ou supprimer un pool élastique SQL Database à l’aide de Transact-SQL. Vous pouvez ajouter ou supprimer des bases de données à partir d’un pool élastique, et vous pouvez utiliser des vues de gestion dynamique tooreturn informations sur les pools élastiques existants.
>

| Commande | Description |
| --- | --- |
|[CREATE DATABASE (Azure SQL Database)](/sql/t-sql/statements/create-database-azure-sql-database)|Crée une base de données dans un pool existant ou en tant que base de données seule. Vous devez être connecté toohello base de données master toocreate une base de données.|
| [ALTER DATABASE (Azure SQL Database)](/sql/t-sql/statements/alter-database-azure-sql-database) |Déplace une base de données dans un pool élastique, en dehors de celui-ci ou entre des pools élastiques.|
|[DROP DATABASE (Transact-SQL)](/sql/t-sql/statements/drop-database-transact-sql)|Supprime une base de données.|
|[sys.elastic_pool_resource_stats (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-elastic-pool-resource-stats-azure-sql-database)|Retourne les statistiques d’utilisation de ressources pour tous les pools de bases de données élastiques hello dans un serveur logique. Pour chaque pool de bases de données élastique, il existe une ligne pour chaque fenêtre de création de rapports de 15 secondes (quatre lignes par minute). Cela inclut l’utilisation du processeur, e/s, journal, la consommation du stockage et demande/sessions simultanées par toutes les bases de données dans le pool de hello.|
|[sys.database_service_objectives (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Retourne hello edition (niveau de service), objectif de service (niveau de tarification) et nom du pool élastique, le cas échéant, pour une base de données SQL Azure ou d’un entrepôt de données SQL Azure. Si une session toohello la base de données master sur un serveur de base de données SQL Azure, retourne des informations sur toutes les bases de données. Pour l’entrepôt de données SQL Azure, vous devez être connecté toohello de base de données master.|

## <a name="manage-sql-database-elastic-pools-using-hello-rest-api"></a>Gérer les pools élastiques de base de données SQL à l’aide des API REST de hello

toocreate et gérer les pools élastiques de base de données SQL à l’aide de hello API REST, consultez [API REST de Azure SQL Database](/rest/api/sql/).

## <a name="next-steps"></a>Étapes suivantes

* Vous pouvez aussi regarder la vidéo [Formation vidéo Microsoft Virtual Academy sur les fonctions de bases de données élastiques dans Azure SQL Database](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554)
* toolearn savoir plus sur les modèles de conception pour les applications SaaS à l’aide de pools élastiques, consultez [des modèles de conception pour les Applications SaaS mutualisée avec la base de données SQL Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).
* Pour obtenir un didacticiel SaaS à l’aide de pools élastiques, consultez [Introduction toohello application Wingtip SaaS](sql-database-wtp-overview.md).
