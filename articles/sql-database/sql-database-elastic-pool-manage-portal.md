---
title: "Portail Azure : Créer et gérer un pool élastique SQL Database | Microsoft Docs"
description: "Découvrez comment toouse hello portail Azure et toomanage intelligence intégrée de la base de données SQL, analyse et redimensionner un performances de base de données évolutive pool élastique toooptimize et gérer les coûts."
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a>Créer et gérer un pool élastique hello portail Azure
Cette rubrique vous montre comment toocreate et gérer évolutive [pools élastiques](sql-database-elastic-pool.md) avec hello portail Azure. Vous pouvez également créer et gérer un pool élastique Azure [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello API REST, ou [c#](sql-database-elastic-pool-manage-csharp.md). Vous pouvez également créer et déplacer des bases de données vers et depuis des pools élastiques à l’aide de [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

## <a name="create-an-elastic-pool"></a>Créer un pool élastique 

Vous pouvez créer un pool élastique de deux façons. Vous pouvez le faire à partir de zéro si vous savez que le programme d’installation de hello pool que vous voulez, ou commencer par la recommandation du service de hello. Base de données SQL a une intelligence intégrée qui recommande une configuration de pool élastique, s’il est plus économique en fonction de hello au-delà de télémétrie d’utilisation pour vos bases de données.

Vous pouvez créer plusieurs pools sur un serveur, mais vous ne pouvez ajouter des bases de données à partir de différents serveurs dans hello même pool. 

> [!NOTE]
> Les pools élastiques sont mis à la disposition générale dans toutes les régions Azure, à l’exception de l’Inde de l’Ouest, où ils sont actuellement en version préliminaire.  Les pools élastiques seront en disposition générale dès que possible dans cette région.
>

### <a name="step-1-create-an-elastic-pool"></a>Étape 1 : Créer un pool élastique

Création d’un pool élastique d’un existant **server** panneau dans le portail de hello est hello plus simple façon toomove bases de données existantes dans un pool élastique.

> [!NOTE]
> Vous pouvez également créer un pool élastique en recherchant **pool élastique SQL** Bonjour **Marketplace** ou en cliquant sur **+ ajouter** Bonjour **pools élastiques de SQL**parcourir le panneau. Vous êtes en mesure de toospecify un serveur nouveau ou existant à ce pool de mise en service de flux de travail.
>
>

1. Bonjour [portail Azure](http://portal.azure.com/), cliquez sur **davantage de services**  **>**  **serveurs SQL**, puis cliquez sur serveur hello contenant hello bases de données pool élastique de tooadd tooan.
2. Cliquez sur **Nouveau pool**.

    ![Ajouter le serveur de tooa pool](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    **OU**

    Vous pouvez voir un message indiquant qu’il est recommandé de pools élastiques pour serveur de hello. Cliquez sur hello de toosee message hello recommandé en fonction de la télémétrie d’utilisation de base de données historiques, puis sur hello couche toosee plus de détails et personnaliser le pool de hello. Consultez [comprendre les recommandations de pool](#understand-elastic-pool-recommendations) plus loin dans cette rubrique pour la recommandation de hello est effectuée.

    ![pool recommandé](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. Hello **pool élastique** panneau s’affiche, qui est de spécifier les paramètres de hello pour le pool. Si vous avez cliqué sur **nouveau pool** à l’étape précédente de hello, hello niveau tarifaire est **Standard** par défaut et aucune base de données est sélectionnée. Vous pouvez créer un pool vide, ou spécifier un ensemble de bases de données existantes à partir de cette toomove serveur dans le pool de hello. Si vous créez un pool recommandé, hello recommandé de tarification, les paramètres de performances et la liste des bases de données sont préremplies, mais vous pouvez toujours modifier les.

    ![Configurer un pool élastique](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. Spécifiez un nom pour le pool élastique de hello, ou laissez-le comme valeur par défaut hello.

### <a name="step-2-choose-a-pricing-tier"></a>Étape 2 : sélectionner un niveau tarifaire

Hello niveau de tarification du pool détermine hello fonctionnalités ELASTIQUES toohello disponibles dans le pool de hello et hello le nombre maximal d’Edtu (eDTU MAX) et de base de données de stockage (Go) disponible tooeach. Pour plus d’informations, voir Niveaux de service.

Cliquez sur le niveau de tarification hello toochange de pool de hello **niveau tarifaire**, cliquez sur hello tarification de votre choix, puis cliquez sur **sélectionnez**.

> [!IMPORTANT]
> Une fois que vous choisissez hello tarification et valider vos modifications en cliquant sur **OK** dans la dernière étape de hello, vous ne serez pas hello toochange en mesure de tarification du pool de hello. toochange hello niveau tarifaire pour un pool élastique existant, créez un pool élastique dans le niveau de tarification souhaité hello et migrez hello bases de données toothis nouveau pool.
>

![Sélectionner un niveau de tarification](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a>Étape 3 : Configurer le pool de hello

Après avoir hello niveau tarifaire, cliquez sur Configurer pool lorsque vous ajoutez des bases de données, Edtu de pool de jeu et du stockage (pool Go), où vous avez défini des Edtu de hello min et max pour ELASTIQUES de hello dans le pool de hello.

1. Cliquez sur **Configurer le pool**
2. Sélectionnez hello bases de données tooadd toohello pool. Cette étape est facultative lors de la création du pool de hello. Bases de données peuvent être ajoutés qu’après que hello pool a été créé.
    tooadd de bases de données, cliquez sur **Add database**, cliquez sur les bases de données hello que vous souhaitez tooadd, puis cliquez sur hello **sélectionnez** bouton.

    ![Ajouter des bases de données](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    Si les bases de données hello avec lequel vous travaillez ont suffisamment de télémétrie d’utilisation historiques, hello **estimée des eDTU et l’utilisation de Go** graphique et hello **réel eDTU utilisation** toohelp de mise à jour de graphique à barres vous vérifiez la configuration décisions. En outre, les service hello peut donner un toohelp de message de recommandation vous redimensionner hello pool. Voir [Recommandations dynamiques](#understand-elastic-pool-recommendations).

3. Utilisez les contrôles de hello dans hello **configurer le pool** tooexplore paramètres de page et de configurer le pool. Pour plus d’informations sur les limites de chaque niveau de service, consultez l’article décrivant les [limites des pools élastiques](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools). Pour obtenir des conseils détaillés sur le dimensionnement approprié d’un pool, consultez l’article fournissant des [considérations sur les prix et performances pour un pool élastique](sql-database-elastic-pool.md). Pour plus d’informations sur les paramètres du pool, consultez [Propriétés du pool élastique](sql-database-elastic-pool.md#database-properties-for-pooled-databases).

    ![Configurer un pool élastique](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. Cliquez sur **sélectionnez** Bonjour **configurer un Pool** panneau après modification des paramètres.
5. Cliquez sur **OK** pool de hello toocreate.

## <a name="understand-elastic-pool-recommendations"></a>Comprendre les recommandations relatives au pool élastique

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

## <a name="manage-and-monitor-an-elastic-pool"></a>Gérer et surveiller un pool élastique

Vous pouvez utiliser hello toomonitor portail Azure et gérer un pool élastique et hello bases de données hello pool. À partir du portail de hello, vous pouvez surveiller l’utilisation de hello un pool élastique et bases de données hello dans ce pool. Vous pouvez également effectuer un ensemble de modifications pool élastique de tooyour et envoyer toutes les modifications apportées à hello même temps. Ces modifications incluent l’ajout ou la suppression de bases de données, ainsi que le changement des paramètres du pool élastique ou des bases de données.

Hello graphique suivant montre un pool élastique exemple. affichage de Hello inclut :

*  Graphiques de surveillance de l’utilisation des ressources de pool élastique de hello et bases de données hello contenus dans le pool de hello.
*  Hello **configurer** pool bouton toomake modifie le pool élastique de toohello.
*  Hello **créer la base de données** bouton qui crée une base de données et l’ajoute toohello pool élastique en cours.
*  Des tâches élastiques, qui vous aident à gérer un grand nombre de bases de données en exécutant des scripts Transact SQL sur toutes les bases de données d’une liste.

![Affichage du pool][2]

Vous pouvez accéder tooa pool particulier toosee son utilisation des ressources. Par défaut, le pool de hello est l’utilisation de stockage et d’eDTU tooshow configuré pour hello dernière heure. graphique de Hello peut être configuré tooshow différentes métriques sur différentes périodes.

1. Sélectionnez un toowork pool élastique avec.
2. Sous **Surveillance du pool élastique**, vous trouverez un graphique intitulé **Utilisation des ressources**. Cliquez sur le graphique de hello.

    ![Surveillance du pool élastique][3]

    Hello **métrique** panneau s’ouvre, affichant une vue détaillée de hello spécifié métriques sur la fenêtre de temps spécifié hello.   

    ![Volet Metric][9]

### <a name="toocustomize-hello-chart-display"></a>affichage du graphique hello toocustomize

Vous pouvez modifier les graphique hello et hello métriques toodisplay autres métriques telles que le pourcentage du processeur, pourcentage de données e/s et pourcentage d’e/s de journal utilisé.

1. Dans le panneau de métrique hello, cliquez sur **modifier**.

    ![Cliquez sur Modifier][6]

2. Bonjour **modifier le graphique** panneau, sélectionnez une plage de temps (heure, l’heure actuelle, ou semaine), ou cliquez sur **personnalisé** tooselect toute plage de dates hello deux dernières semaines. Sélectionner le type de graphique hello (barre ou ligne), puis sélectionnez hello ressources toomonitor.

   > [!Note]
   > Seul graphique des métriques avec hello même unité de mesure peut être affichée dans hello en hello même temps. Par exemple, si vous sélectionnez « pourcentage d’eDTU » puis vous pouvez uniquement sélectionner d’autres mesures avec pourcentage en tant qu’unité hello.
   >

    ![Cliquez sur Modifier](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. Cliquez ensuite sur **OK**.

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>Gérer et surveiller des bases de données dans un pool élastique

Il est également possible de surveiller des bases de données individuelles pour identifier des problèmes potentiels.

1. Sous **Surveillance de la base de données élastique**, vous trouverez un graphique qui affiche les métriques de cinq bases de données. Par défaut, hello graphique affiche hello 5 bases de données dans le pool de hello par utilisation moyenne eDTU Bonjour dernière heure. Cliquez sur le graphique de hello.

    ![Surveillance du pool élastique][4]

2. Hello **l’utilisation des ressources de base de données** panneau s’affiche. Cela fournit une vue détaillée de l’utilisation de base de données hello dans le pool de hello. À l’aide de la grille hello dans la partie inférieure de hello du Panneau de hello, vous pouvez sélectionner des bases de données dans hello pool toodisplay son utilisation dans le graphique de hello (des bases de données too5). Vous pouvez également personnaliser la fenêtre hello métriques et l’heure affichée dans le graphique de hello en cliquant sur **modifier le graphique**.

    ![Panneau Database Resource Utilization (Utilisation des ressources des bases de données)][8]

### <a name="toocustomize-hello-view"></a>affichage de hello toocustomize

1. Bonjour **l’utilisation des ressources de base de données** panneau, cliquez sur **modifier le graphique**.

    ![Cliquez sur Modifier le graphique](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. Bonjour **modifier** panneau du graphique, sélectionnez une plage de temps (après les heures ou dernières 24 heures) ou cliquez sur **personnalisé** tooselect un autre jour Bonjour au-delà de 2 semaines toodisplay.

    ![Cliquez sur Personnalisé](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. Cliquez sur hello **comparer les bases de données par** tooselect de liste déroulante un toouse métrique différents lors de la comparaison des bases de données.

    ![Modifier le graphique de hello](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>toomonitor de bases de données tooselect

Dans la liste base de données hello hello **l’utilisation des ressources de base de données** panneau, vous pouvez trouver des bases de données particulières en consultant les pages hello dans la liste de hello ou en tapant dans nom hello d’une base de données. Utilisez hello case à cocher tooselect hello base de données.

![Recherchez des bases de données toomonitor][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a>Ajouter une ressource de pool élastique tooan alerte

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

## <a name="move-a-database-into-an-elastic-pool"></a>Déplacer une base de données dans un pool élastique

Vous pouvez ajouter ou supprimer des bases de données dans un pool existant. bases de données Hello peuvent être dans d’autres pools. Toutefois, vous pouvez uniquement ajouter des bases de données qui sont sur hello même serveur logique.

1. Dans le panneau hello pour le pool de hello, sous **des bases de données élastiques** cliquez sur **configurer pool**.

    ![Cliquez sur Configurer le pool][1]

2. Bonjour **configurer pool** panneau, cliquez sur **ajouter toopool**.

    ![Cliquez sur Ajouter toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. Bonjour **ajouter des bases de données** panneau, base de données Sélectionnez hello ou pool de bases de données tooadd toohello. Puis cliquez sur **Sélectionner**.

    ![Sélectionnez les bases de données tooadd](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    Hello **configurer pool** panneau maintenant listes hello de base de données sélectionnée toobe ajouté, avec son état défini trop**en attente**.

    ![Ajouts de pool en attente](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. Bonjour **Panneau de pool configurer**, cliquez sur **enregistrer**.

    ![Cliquez sur Enregistrer.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a>Déplacer une base de données hors d’un pool élastique

1. Bonjour **configurer pool** panneau, base de données Sélectionnez hello ou tooremove de bases de données.

    ![liste des bases de données](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. Cliquez sur **Supprimer du pool**.

    ![liste des bases de données](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    Hello **configurer pool** panneau maintenant listes hello de base de données sélectionnée toobe supprimée avec son état défini trop**en attente**.

    ![Afficher l’aperçu d’ajout et de suppression de base de données](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. Bonjour **Panneau de pool configurer**, cliquez sur **enregistrer**.

    ![Cliquez sur Enregistrer.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a>Modifier les paramètres de performances d'un pool élastique

Lorsque vous analysez l’utilisation des ressources d’un pool élastique hello, vous pouvez constater que quelques ajustements sont nécessaires. Peut-être pool de hello doit être modifiée dans les limites de performances ou le stockage hello. Éventuellement, vous souhaitez que les paramètres de base de données toochange hello dans le pool de hello. Vous pouvez modifier le programme d’installation de hello du pool hello à n’importe quel moment tooget hello meilleur compromis entre les performances et le coût. Pour plus d’informations, consultez l’article [Quand utiliser un pool élastique ?](sql-database-elastic-pool.md).

toochange hello Edtu limites ou de stockage par pool et Edtu par base de données :

1. Ouvrez hello **configurer pool** panneau.

    Sous **les paramètres de pool élastique**, utilisez les deux paramètres de pool de curseur toochange hello.

    ![Utilisation des ressources du pool élastique](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. Lorsque le paramètre de hello change, hello affiche hello mensuel coût estimé de modifications de hello.

    ![Mise à jour d’un pool élastique et nouveau coût mensuel](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a>Latence des opérations du pool élastique
* La modification d’Edtu de min hello par base de données ou max Edtu par base de données généralement se termine dans 5 minutes ou moins.
* Modification des Edtu hello par pool dépend hello total de l’espace utilisé par toutes les bases de données dans le pool de hello. Ce processus prend en moyenne 90 minutes au maximum, pour chaque tranche de 100 Go. Par exemple, si hello l’espace total utilisé par toutes les bases de données dans le pool de hello est 200 Go, puis hello attendu de latence de modification hello eDTU du pool par pool est de 3 heures au maximum.

## <a name="next-steps"></a>Étapes suivantes

- toounderstand quelles un pool élastique, consultez [pool élastique de base de données SQL](sql-database-elastic-pool.md).
- Pour obtenir de l’aide sur l’utilisation des pools élastiques, consultez [Considérations sur les prix et performances pour les pools élastiques](sql-database-elastic-pool.md).
- scripts de toorun Transact-SQL de travaux élastique toouse par rapport à n’importe quel nombre de bases de données dans le pool de hello, voir [vue d’ensemble de travaux élastique](sql-database-elastic-jobs-overview.md).
- tooquery sur n’importe quel nombre de bases de données dans le pool de hello, consultez [vue d’ensemble de la requête élastique](sql-database-elastic-query-overview.md).
- Pour les transactions de n’importe quel nombre de bases de données dans le pool de hello, consultez [transactions élastiques](sql-database-elastic-transactions-overview.md).


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
