---
title: "analyse des performances pour la base de données SQL Azure aaaQuery | Documents Microsoft"
description: "Analyse des performances des requêtes identifie hello consommation d’UC de la plupart des requêtes pour une base de données SQL Azure."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a>Query Performance Insight pour base de données SQL Azure
La gestion et de réglage des performances de hello de bases de données relationnelles sont une tâche complexe qui nécessite des compétences importantes et nécessite beaucoup de temps. Query Performance Insight vous permet de toospend moins de temps résolution des problèmes de performances de la base de données en fournissant les éléments suivants de hello :

* Une meilleure compréhension de la consommation des ressources des bases de données (DTU). 
* Hello premières requêtes par le nombre d’UC ou durée/de l’exécution, qui peuvent potentiellement être paramétrées pour améliorer les performances.
* Hello capacité toodrill vers le bas dans les détails de hello d’une requête, afficher son texte et son historique d’utilisation des ressources. 
* Des annotations de réglage des performances qui indiquent les actions effectuées par [SQL Azure Database Advisor](sql-database-advisor.md)  



## <a name="prerequisites"></a>Composants requis
* Query Performance Insight nécessite que le [magasin de requêtes](https://msdn.microsoft.com/library/dn817826.aspx) soit actif sur votre base de données. Si le magasin de requêtes n’est pas en cours d’exécution, le portail de hello vous invite tooturn sur.

## <a name="permissions"></a>Autorisations
suivant de Hello [contrôle d’accès basé sur le rôle](../active-directory/role-based-access-control-what-is.md) autorisations sont requise toouse Query Performance Insight : 

* **Lecteur**, **propriétaire**, **collaborateur**, **collaborateur de base de données SQL**, ou **SQL Server collaborateur** sont des autorisations tooview requis hello principales consommatrices de ressources des requêtes et des graphiques. 
* **Propriétaire**, **collaborateur**, **collaborateur de base de données SQL**, ou **SQL Server collaborateur** autorisations sont requises tooview texte de la requête.

## <a name="using-query-performance-insight"></a>Utilisation de Query Performance Insight
Query Performance Insight est facile toouse :

* Ouvrez [portail Azure](https://portal.azure.com/) et base de données de recherche que vous souhaitez tooexamine. 
  * Dans le menu de gauche, sous Support et dépannage, sélectionnez « Query Performance Insight ».
* Sur le premier onglet de hello, examinez la liste hello des principales requêtes consommatrices de ressources.
* Sélectionnez une requête individuelle de tooview ses détails.
* Ouvrez [SQL Azure Database Advisor](sql-database-advisor.md) , puis regardez si des recommandations sont disponibles.
* Utiliser des curseurs ou zoom toochange icônes observé intervalle.
  
    ![tableau de bord des performances](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> Quelques heures de données doit toobe capturée par le magasin de requêtes pour l’analyse des performances des requêtes de base de données SQL tooprovide. Si la base de données hello ne comporte aucune activité ou magasin de requêtes n’était pas actif pendant une période donnée, les graphiques de hello sera vides lors de l’affichage de cette période. Vous pouvez activer Query Store à tout moment s’il n’est pas en cours d’exécution.   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a>Consultez les requêtes principales consommatrices d’UC
Bonjour [portal](http://portal.azure.com) hello suivant :

1. Parcourir la base de données SQL tooa et cliquez sur **tous les paramètres** > **prise en charge + dépannage** > **analyse des performances de requête**. 
   
    ![Query Performance Insight][1]
   
    affichage des requêtes principales Hello s’ouvre et premières requêtes de consommation UC hello sont répertoriées.
2. Cliquez sur le graphique hello pour plus d’informations.<br>Hello ligne supérieure affiche % DTU global pour la base de données hello, tandis que les barres de hello affichent % processeur utilisé par les requêtes hello sélectionné pendant l’intervalle sélectionné de hello (par exemple, si **semaine** est sélectionné chaque barre représente un jour).
   
    ![principales requêtes][2]
   
    grille de bas Hello représente des informations agrégées pour les requêtes visible hello.
   
   * ID de requête : identificateur unique de la requête dans la base de données.
   * UC par requête pendant l’intervalle observable (dépend de la fonction d’agrégation).
   * Durée par requête (dépend de la fonction d’agrégation).
   * Nombre total d’exécutions pour une requête particulière.
     
     Activez ou désactivez des requêtes individuelles tooinclude ou les exclure de graphique de hello à l’aide de cases à cocher.
3. Si vos données devient obsolètes, cliquez sur hello **Actualiser** bouton.
4. Vous pouvez utiliser des curseurs et l’intervalle d’observation de zoom boutons toochange et examiner les pics : ![paramètres](./media/sql-database-query-performance/zoom.png)
5. Si vous souhaitez un affichage différent, vous pouvez également sélectionner l’onglet **Personnalisé** et définir :
   
   * la mesure (UC, Durée, Nombre d’exécutions) ;
   * l’intervalle de temps (Dernières 24 heures, Semaine dernière, Mois dernier) ; 
   * le nombre de requêtes ;
   * la fonction d’agrégation.
     
     ![Paramètres](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a>Affichage des détails d’une requête individuelle
Détails de la requête tooview :

1. Cliquez sur une requête dans la liste hello des premières requêtes.
   
    ![détails](./media/sql-database-query-performance/details.png)
2. affichage des détails Hello s’ouvre et nombre de consommation ou durée/de l’exécution de processeurs de requêtes hello est divisé au fil du temps.
3. Cliquez sur le graphique hello pour plus d’informations.
   
   * Graphique supérieure montre la ligne avec global % DTU de base de données, et les barres de hello sont % processeur consommé par la requête sélectionnée de hello.
   * Le deuxième graphique montre la durée totale par requête hello.
   * Graphique de bas indique le nombre total d’exécutions par requête sélectionnée de hello.
     
     ![détails de la requête][3]
4. Si vous le souhaitez, utiliser des curseurs, boutons de zoom ou cliquez sur **paramètres** toocustomize affichage des données de la requête ou toopick une période de temps différent.

## <a name="review-top-queries-per-duration"></a>Révision des requêtes principales par durée
Dans la mise à jour de la récente hello de Query Performance Insight, nous avons introduit deux nouvelles mesures qui peuvent vous aider à identifier les goulots d’étranglement potentiels : nombre de durée et de l’exécution.<br>

Requêtes longues ont hello plus grande pour plus de ressources de verrouillage, de bloquer d’autres utilisateurs et de limiter l’évolutivité. Ils sont également hello meilleurs éléments pour l’optimisation.<br>

tooidentify les longues requêtes :

1. Ouvrez l’onglet **Personnalisé** dans Query Performance Insight pour la base de données sélectionnée.
2. Modifier les mesures toobe **durée**
3. Sélectionner le nombre de requêtes et l’intervalle d’observation.
4. Sélectionnez la fonction d’agrégation.
   
   * **Somme** calcule le temps d’exécution total de toutes les requêtes pendant tout l’intervalle d’observation.
   * **Max** recherche le temps d’exécution maximum pendant l’intervalle d’observation.
   * **AVG** trouve durée moyenne d’exécution de toutes les exécutions de requête et vous montrent hello haut hors ces moyennes. 
     
     ![durée de la requête][4]

## <a name="review-top-queries-per-execution-count"></a>Révision des requêtes principales par nombre d’exécutions
Un nombre élevé d’exécutions peut ne pas affecter la base de données elle-même et l’utilisation de ressources peut être faible, mais l’application globale peut devenir lente.

Dans certains cas, le nombre d’exécutions très élevé peut entraîner des tooincrease du réseau les allers-retours. Les allers-retours affectent considérablement les performances. Elles sont une latence toonetwork sujet et latence du serveur toodownstream. 

Par exemple, de nombreux piloté par les données de sites Web accéder largement à base de hello pour chaque demande de l’utilisateur. Durant le regroupement de connexions permet, hello augmenté le trafic réseau et la charge de traitement sur le serveur de base de données hello peuvent nuire aux performances.  Conseils généraux sont tookeep round allers-retours tooan strict minimum.

tooidentify exécutées fréquemment des requêtes de requêtes (« bavardes ») :

1. Ouvrez l’onglet **Personnalisé** dans Query Performance Insight pour la base de données sélectionnée.
2. Modifier les mesures toobe **le nombre d’exécutions**
3. Sélectionner le nombre de requêtes et l’intervalle d’observation.
   
    ![nombre d’exécutions de la requête][5]

## <a name="understanding-performance-tuning-annotations"></a>Présentation des annotations de réglage des performances
Lors de l’exploration dans Query Performance Insight votre charge de travail, vous pouvez remarquer des icônes avec une ligne verticale sur le graphique de hello.<br>

Ces icônes sont des annotations. Elles représentent les performances qui affectent les actions effectuées par [SQL Azure Database Advisor](sql-database-advisor.md). Annotation de pointage, vous obtenez des informations de base sur l’action de hello :

![annotation de requête][6]

Si vous souhaitez tooknow plus ou appliquez les recommandations de l’Assistant, cliquez sur icône de hello. Les détails de l’action s’ouvrent. S’il s’agit d’une recommandation active, vous pouvez l’appliquer directement à l’aide de la commande.

![détails d’annotation de requête][7]

### <a name="multiple-annotations"></a>Annotations multiples.
Il est possible qu’en raison du niveau de zoom, fermer tooeach autres annotations seront obtenir réduites en une seule. Une icône spéciale s’affiche alors. Si vous cliquez dessus, un panneau s’ouvre, qui contient une liste d’annotations groupées.
Corrélation des requêtes et des actions de réglage des performances peut aider toobetter votre charge de travail. 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a>Optimisation de la configuration du magasin de requêtes hello pour Query Performance Insight
Pendant votre utilisation de Query Performance Insight, vous pouvez rencontrer hello suivant des messages du magasin de requêtes :

* « Le magasin de requête n’est pas correctement configuré dans cette base de données. Cliquez ici toolearn plus. »
* « Le magasin de requête n’est pas correctement configuré dans cette base de données. Cliquez ici les paramètres toochange. » 

Ces messages apparaissent généralement lorsque le magasin de requêtes n’est pas en mesure de toocollect de nouvelles données. 

Le premier cas se produit lorsque le magasin de requêtes est en mode Lecture seule et si les paramètres sont définis de façon optimale. Vous pouvez résoudre ce problème en augmentant la taille du magasin de requêtes ou en le nettoyant.

![bouton qds][8]

Le deuxième cas se produit lorsque le magasin de requêtes est désactivé ou si les paramètres ne sont pas définis de façon optimale. <br>Vous pouvez modifier hello de rétention et de Capture de stratégie et d’activer le magasin de requêtes en exécutant les commandes ci-dessous, ou directement à partir de portail :

![bouton qds][9]

### <a name="recommended-retention-and-capture-policy"></a>Stratégie de rétention et de capture recommandée
Il existe deux types de stratégies de rétention :

* Taille en fonction - si tooAUTO ensemble il sera nettoyer les données automatiquement vers la taille maximale est atteinte.
* Heure - par défaut, nous allons la définir too30 jours, ce qui signifie que, si le magasin de requêtes manquiez d’espace, elle supprimera interroger les informations datant de plus de 30 jours

La stratégie de capture peut avoir les valeurs suivantes :

* **Tout** : toutes les requêtes sont capturées.
* **Auto** : les requêtes peu fréquentes et les requêtes avec une durée de compilation et d’exécution insignifiante sont ignorées. Les seuils concernant le nombre d’exécutions, et la durée de compilation et d’exécution, sont déterminés en interne. Il s’agit d’option par défaut de hello.
* **Aucune** : le magasin de requêtes arrête la capture de nouvelles requêtes, mais les statistiques d’exécution pour les requêtes déjà capturées sont toujours collectées.

Nous vous recommandons de définir toutes les stratégies tooAUTO et nouvelle stratégie too30 jours :

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

Augmentez la taille du magasin de requêtes. Cela peut être exécutée par la connexion de base de données tooa et émetteur de la requête suivante :

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

Appliquer ces paramètres finalement rend le magasin de requêtes collecte les nouvelles requêtes, toutefois, si vous ne souhaitez pas toowait, vous pouvez désactiver le magasin de requêtes. 

> [!NOTE]
> Exécution de la requête suivante va supprimer toutes les informations actuelles dans le magasin de requêtes de hello. 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a>Résumé
Query Performance Insight vous aide à comprendre l’impact hello de votre charge de travail de requête et de sa relation toodatabase la consommation des ressources. Avec cette fonctionnalité, vous découvrez haut hello principales requêtes consommatrices et identifier facilement hello ceux toofix avant qu’ils deviennent un problème.

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des recommandations supplémentaires sur l’amélioration des performances hello de votre base de données SQL, cliquez sur [recommandations](sql-database-advisor.md) sur hello **Query Performance Insight** panneau.

![Performance Advisor](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

