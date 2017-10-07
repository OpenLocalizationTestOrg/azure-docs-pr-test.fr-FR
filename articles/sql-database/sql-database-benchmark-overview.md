---
title: "vue d’ensemble du test d’évaluation de base de données SQL aaaAzure"
description: "Cette rubrique décrit hello référence de base de données SQL Azure utilisé pour mesurer les performances de hello de base de données SQL Azure."
services: sql-database
documentationcenter: na
author: jan-eng
manager: jhubbard
editor: monicar
ms.assetid: e26f8a66-2c12-49d7-8297-45b4d48a5c01
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/21/2016
ms.author: janeng
ms.openlocfilehash: 1024e9ada511935f911cb1345b4dc5508997c702
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-benchmark-overview"></a>Vue d’ensemble du test d’évaluation de la base de données SQL Azure
## <a name="overview"></a>Vue d'ensemble
La base de données SQL Microsoft Azure propose trois [niveaux de service](sql-database-service-tiers.md) associés à plusieurs niveaux de performance. Chaque niveau de performance fournit un augmentation ensemble de ressources, ou d’alimentation, conçu toodeliver plus en plus un débit plus élevé.

Il est important toobe tooquantify en mesure de la puissance croissante de hello de chaque niveau de performance se traduit par des performances de base de données améliorées. Microsoft a développé des toodo hello test d’évaluation de base de données SQL Azure (évaluation). test d’évaluation Hello effectue une combinaison d’opérations de base disponible dans toutes les charges de travail OLTP. Nous évaluons le débit hello obtenu de bases de données en cours d’exécution dans chaque niveau de performance.

Hello ressources et la puissance de chaque couche et les performances du niveau de service sont exprimés en termes de [unités de Transaction de base de données (Udbd)](sql-database-what-is-a-dtu.md). Les dtu permettent de capacité de relative hello toodescribe d’un niveau de performance en fonction de la mesure du processeur, mémoire, lire et écrire les taux offerts par chaque niveau de performance. Doubler la notation en DTU hello d’une base de données équivaut à puissance toodoubling hello. test d’évaluation Hello nous permet d’impact de hello tooassess sur les performances de base de données de la puissance offerte par chaque niveau de performances en exerçant les opérations de base de données, lors de la mise à l’échelle de taille de base de données, le nombre d’utilisateurs et de taux de transaction dans une proportion croissante de hello base de données de toohello toohello ressources fournies.

En exprimant le débit hello de niveau de service Basic de hello à l’aide de transactions par heure, niveau de service Standard hello à l’aide de transactions par minute et niveau de service Premium hello à l’aide de transactions par seconde, il rend plus facile tooquickly concernent hello chaque couche toohello d’exigences de service d’une application potentiel.

## <a name="correlating-benchmark-results-tooreal-world-database-performance"></a>Corrélation des performances de base de données de test d’évaluation des résultats tooreal world
Il est important toounderstand cette évaluation, comme tous les tests d’évaluation et d’indication n’est. Bonjour transaction taux atteints avec l’application de test d’évaluation hello ne sera pas hello mêmes que ceux qui peuvent être réalisées avec d’autres applications. test d’évaluation Hello comprend un ensemble de types s’exécutent sur un schéma contenant une plage de types de données et les tables de transaction différentes. Pendant les exercices de banc d’essai hello hello mêmes opérations de base qui sont des charges de travail courantes tooall OLTP, il ne représente pas une classe spécifique de la base de données ou d’une application. Hello banc d’essai hello vise tooprovide un performances relatives de toohello guide raisonnable d’une base de données attendue lors de la mise à l’échelle vers le haut ou vers le bas entre les niveaux de performance. En réalité, les bases de données varient en termes de taille et de complexité. Elles supportent diverses charges de travail et réagissent de différentes façons. Par exemple, une application gourmande en E/S peut atteindre rapidement les seuils d’E/S, de la même manière qu’une application gourmande en ressources processeur peut atteindre rapidement les limites processeur. Il n’existe aucune garantie qu’une base de données particulière évoluera de hello que même charger comme test d’évaluation hello constamment.

Hello banc d’essai et sa méthodologie sont décrits plus en détail ci-dessous.

## <a name="benchmark-summary"></a>Résumé du test d’évaluation
Évaluation mesure les performances de hello une combinaison d’opérations de base de données qui se produisent plus fréquemment dans les charges de travail (OLTP) de traitement transactionnel en ligne. Bien que le test d’évaluation hello est conçu pour le cloud computing à l’esprit, schéma de base de données hello, remplissage des données et les transactions ont été conçu toobe largement représentative des éléments de base hello plus couramment utilisés dans les charges de travail OLTP.

## <a name="schema"></a>Schéma
schéma de Hello est conçue toohave suffisamment toosupport de variété et de complexité un large éventail d’opérations. test d’évaluation Hello s’exécute sur une base de données composé six tables. les tables Hello se répartissent en trois catégories : taille fixe, évolutives et croissante. Il existe deux tables de taille fixe, trois tables extensibles et une table évolutive. Les tables de taille fixe comportent un nombre constant de lignes. Les tables évolutives présentent une cardinalité proportionnelle toodatabase performances, mais ne change pas pendant le test d’évaluation hello. Hello augmente la table est dimensionnée comme une table de mise à l’échelle lors du chargement initial, mais passe cardinalité de hello cours hello banc d’essai hello en cours d’exécution que les lignes sont insérées et supprimées.

schéma Hello inclut une combinaison de types de données entier, numériques, de caractère et date/heure. schéma de Hello inclut des clés primaires et secondaires, mais pas de clés étrangères -, il n’existe pas de contraintes d’intégrité référentielle entre les tables.

Un programme de génération de données génère des données hello hello de base de données initiale. Les entiers et les données numériques sont générés à l’aide de différentes stratégies. Dans certains cas, les valeurs sont distribuées de façon aléatoire sur une plage. Dans d’autres cas, un ensemble de valeurs est permuté de façon aléatoire tooensure qu’une distribution spécifique est conservée. Champs de texte sont générés à partir d’une liste pondérée de mots tooproduce des données réalistes.

base de données Hello est dimensionnée en fonction d’un « facteur d’échelle ». facteur d’échelle Hello (abrégé en SF) détermine la cardinalité hello Hello tables évolutives et croissante. Comme décrit ci-dessous dans hello section utilisateurs et rythme, hello de base de données, le nombre d’utilisateurs et des performances maximales tous l’échelle en proportion tooeach autres.

## <a name="transactions"></a>Transactions
charge de travail Hello se compose de types de transactions neuf, comme indiqué dans le tableau hello ci-dessous. Chaque transaction est conçue toohighlight un ensemble particulier de caractéristiques dans le matériel de système et le moteur de base de données hello, avec un contraste élevé de hello autres transactions. Cette approche rend plus facile impact de hello tooassess des performances de toooverall différents composants. Par exemple, les transactions hello « Read Heavy » génère un nombre important d’opérations de lecture à partir du disque.

| Type de transaction | Description |
| --- | --- |
| Read Lite |SÉLECTION ; dans la mémoire ; lecture seule |
| Read Medium |SÉLECTION ; principalement dans la mémoire ; lecture seule |
| Read Heavy |SÉLECTION ; principalement hors de la mémoire ; lecture seule |
| Update Lite |MISE À JOUR ; dans la mémoire ; lecture-écriture |
| Update Heavy |MISE À JOUR ; principalement hors de la mémoire ; lecture-écriture |
| Insert Lite |INSERTION ; dans la mémoire ; lecture-écriture |
| Insert Heavy |INSERTION ; principalement hors de la mémoire ; lecture-écriture |
| Supprimer |SUPPRESSION ; combinaison de ressources dans la mémoire et hors de la mémoire ; lecture-écriture |
| CPU Heavy |SÉLECTION ; dans la mémoire ; charge UC relativement importante ; lecture seule |

## <a name="workload-mix"></a>Combinaison de charges de travail
Les transactions sont sélectionnées de manière aléatoire à partir d’une distribution pondérée avec hello suivant combinaison générale. Hello combinaison générale présente un ratio de lecture/écriture d’environ 2:1.

| Type de transaction | % de la combinaison |
| --- | --- |
| Read Lite |35 |
| Read Medium |20 |
| Read Heavy |5 |
| Update Lite |20 |
| Update Heavy |3 |
| Insert Lite |3 |
| Insert Heavy |2 |
| Supprimer |2 |
| CPU Heavy |10 |

## <a name="users-and-pacing"></a>Utilisateurs et rythme
charge de travail de test d’évaluation Hello est pilotée par un outil qui envoie des transactions sur un ensemble de comportement hello toosimulate des connexions d’un nombre d’utilisateurs simultanés. Bien que toutes les transactions et les connexions de hello sont machine généré, par souci de simplicité constitue les connexions toothese comme « utilisateurs ». Bien que chaque utilisateur fonctionne indépendamment de tous les autres utilisateurs, tous les utilisateurs effectuent hello même cycle d’étapes ci-dessous :

1. Établir une connexion à la base de données.
2. Répéter jusqu'à tooexit signalé :
   * Sélection d’une transaction de façon aléatoire (à partir d’une distribution pondérée)
   * Effectuer une transaction de hello sélectionné et du temps de réponse de mesure hello.
   * Délai d’attente
3. Fermez la connexion de base de données hello.
4. Quitter.

Hello rythme (à l’étape 2c) est sélectionné au hasard, mais avec une distribution qui possède une moyenne de 1 seconde. Chaque utilisateur peut donc, en moyenne, générer au maximum une transaction par seconde.

## <a name="scaling-rules"></a>Règles de mise à l’échelle
nombre de Hello d’utilisateurs est déterminé par la taille de base de données hello (en unités de facteur d’échelle). On compte un seul utilisateur pour cinq unités de facteur d’échelle. En raison de hello rythme, un utilisateur peut générer au maximum une transaction par seconde, en moyenne.

Par exemple, une base de données utilisant un facteur d’échelle de 500 (SF = 500) comportera 100 utilisateurs et pourra atteindre un taux maximum de 100 TPS. toodrive un taux TPS supérieur requiert davantage d’utilisateurs et une plus grande base de données.

tableau Hello ci-dessous montre nombre hello d’utilisateurs soutenus en fait pour chaque niveau de performances et de la couche de service.

| Niveau de service (niveau de performance) | Utilisateurs | Taille de la base de données |
| --- | --- | --- |
| De base |5 |720 Mo |
| Standard (S0) |10 |1 Go |
| Standard (S1) |20 |2,1 Go |
| Standard (S2) |50 |7,1 Go |
| Premium (P1) |100 |14 Go |
| Premium (P2) |200 |28 Go |
| Premium (P6/P3) |800 |114 Go |

## <a name="measurement-duration"></a>Durée de la mesure
Pour être reconnu valide, un test d’évaluation doit s’effectuer sur une durée de mesure constante d’au moins une heure.

## <a name="metrics"></a>Mesures
mesures clés de Hello banc d’essai hello sont débit et temps de réponse.

* Le débit est la mesure essentielle des performances de hello banc d’essai hello. Il est exprimé en transactions par unité de temps et tient compte de tous les types de transactions.
* Le temps de réponse permet de mesurer la prévisibilité des performances. contrainte de temps de réponse Hello varie en fonction de la classe de service, les classes de service ayant un temps de réponse plus strictes requis, comme indiqué ci-dessous.

| Classe de service | Mesure du débit | Temps de réponse requis |
| --- | --- | --- |
| Premium |Transactions par seconde |95e centile à 0,5 seconde |
| Standard |Transactions par minute |90e centile à 1 seconde |
| De base |Transactions par heure |80e centile à 2 secondes |

## <a name="conclusion"></a>Conclusion
Hello référence de base de données SQL Azure mesure les performances de relatif hello de base de données SQL Azure s’exécutant sur ensemble hello de niveaux de service disponibles et les niveaux de performance. banc d’essai Hello effectue une combinaison d’opérations de base de données qui se produisent plus fréquemment dans les charges de travail (OLTP) de traitement transactionnel en ligne. En mesurant les performances réelles, banc d’essai hello fournit un bilan plus significatif de l’impact de hello sur le débit du changement de niveau de performance hello qu’il est possible en indiquant seulement les ressources hello offertes par chaque niveau tels que la vitesse du processeur, la taille de la mémoire et e/s . Bonjour future, nous continuer tooevolve hello banc d’essai toobroaden son étendue et développez données hello fournies.

## <a name="resources"></a>Ressources
[Introduction tooSQL de base de données](sql-database-technical-overview.md)

[Niveaux de service et niveaux de performances](sql-database-service-tiers.md)

[Guide des performances pour les bases de données uniques](sql-database-performance-guidance.md)
