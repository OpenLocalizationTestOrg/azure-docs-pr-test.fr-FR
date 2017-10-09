---
title: "niveaux d’aaaConsistency dans la base de données Azure Cosmos | Documents Microsoft"
description: "Base de données Azure Cosmos a cinq cohérence niveaux toohelp solde éventuelle latence, la disponibilité et la cohérence des compromis."
keywords: "cohérence éventuelle, azure cosmos db, azure, Microsoft Azure"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: cgronlun
documentationcenter: 
ms.assetid: 3fe51cfa-a889-4a4a-b320-16bf871fe74c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac399c229d0856cd811bc81568536e519af3300f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tunable-data-consistency-levels-in-azure-cosmos-db"></a>Niveaux de cohérence des données paramétrables dans Azure Cosmos DB
Base de données Azure Cosmos est conçu de hello d’arrière-plan avec une distribution globale à l’esprit pour chaque modèle de données. Il est conçu toooffer prévisibles à faible latence garanties, un SLA de disponibilité de 99,99 %, et plusieurs bien définis ont assoupli des modèles de cohérence. Pour le moment, Azure Cosmos DB prend en charge cinq niveaux de cohérence : Fort, Obsolescence limitée, Session, Préfixe cohérent et Éventuel. 

Outre les modèles de cohérence **fort** et **éventuel** souvent offerts par les bases de données distribuées, Azure Cosmos DB propose trois modèles de cohérence supplémentaires soigneusement codifiés et mis en œuvre, et dont l’utilité a été validée dans des conditions d’utilisation réelles. Il s’agit hello **délimitée péremption**, **session**, et **préfixe cohérent** niveaux de cohérence. Ces niveaux de cinq cohérence activer collectivement toomake bien motivée compromis entre la cohérence, la disponibilité et la latence. 

## <a name="distributed-databases-and-consistency"></a>Bases de données distribuées et cohérence
Les bases de données distribuées commerciales se répartissent en deux catégories : les bases de données qui n’offrent pas de choix de cohérence bien définis et démontrables et celles qui offrent deux possibilités de programmabilité extrêmes (cohérence éventuelle et forte). 

Hello les développeurs d’applications charges ancien avec minutia de protocoles de leur réplication et attend les compromis difficile de toomake entre la cohérence, la disponibilité, la latence et débit. Hello ce dernier met un toochoose pression un des deux extrêmes de hello. En dépit d’abondance hello de recherche et de propositions pour les modèles de cohérence plus de 50, hello Communauté de base de données distribuée n’a pas été en mesure de toocommercialize des niveaux de cohérence au-delà de la cohérence forte et éventuelle. Permet de COSMOS DB toochoose développeurs entre cinq modèles de cohérence bien définis dans spectre de cohérence hello – fort, délimitée péremption, [session](http://dl.acm.org/citation.cfm?id=383631), préfixe cohérent et finale. 

![Base de données Cosmos Azure offre plusieurs bien définie toochoose de modèles de cohérence (souple) à partir de](./media/consistency-levels/five-consistency-levels.png)

Hello tableau suivant illustre les garanties particulières hello que fournit chaque niveau de cohérence.
 
**Niveaux de cohérence et garanties**

| Niveau de cohérence | Garanties |
| --- | --- |
| Remarque | Linéarisabilité |
| Obsolescence limitée | Préfixe cohérent. Retard des lectures par rapport aux écritures par k préfixes ou un intervalle t |
| session   | Préfixe cohérent. Lectures unitones, écritures unitones, lecture de vos écritures, l’écriture suit les lectures |
| Préfixe cohérent | Mises à jour retournées sont un préfixe de toutes les mises à jour hello, sans interruption |
| Eventual (Éventuel)  | Lectures en désordre |

Configurer le niveau de cohérence hello par défaut sur votre compte de base de données Cosmos (et remplacer ultérieurement cohérence hello sur une requête de lecture spécifique). En interne, niveau de cohérence hello par défaut s’applique toodata dans les groupes de partition hello qui peuvent être réparties entre les régions. Environ 73 % de nos clients utilisent la cohérence de session et 20 % y préfèrent l’obsolescence limitée. Nous observons qu’environ 3 % de nos clients expérimentent initialement différents niveaux de cohérence avant de choisir une cohérence spécifique pour leur application. Nous observons également que seuls 2 % de nos clients modifient les niveaux de cohérence sur demande. 

Dans DB Cosmos, les lectures au niveaux de cohérence session, préfixe cohérent et cohérence éventuelle sont deux fois meilleur marché que les lectures aux niveaux de cohérence fort ou obsolescence limitée. Cosmos DB offre des SLA à 99,99 % exhaustifs de pointe, incluant des garanties de cohérence en plus de la disponibilité, du débit et de la latence. Nous utilisons un [vérificateur de linearizability](http://dl.acm.org/citation.cfm?id=1806634), qui fonctionne en continu via la télémétrie de notre service et ouvertement signale toute tooyou de violations de la cohérence. Pour délimité péremption, nous analyse et rapports des violations a duré et les limites de t. Pour toutes les cinq niveaux de cohérence souple, nous avons également signaler hello [métrique de l’obsolescence limitée PROBABILISTE](http://dl.acm.org/citation.cfm?id=2212359) tooyou directement.  

## <a name="scope-of-consistency"></a>Portée de la cohérence
granularité de Hello de cohérence a une demande d’utilisateur unique tooa étendue. Une demande d’écriture peut correspondent tooan insert, replace, la fusionner ou supprimer la transaction. Comme les écritures, une transaction de lecture/la requête est également demande d’utilisateur unique tooa étendue. utilisateur de Hello peut-être toopaginate requis sur un grand jeu de résultats, le fractionnement des partitions multiples, mais chaque lecture transaction étendue tooa une seule page et pris en charge à partir d’une partition unique.

## <a name="consistency-levels"></a>Niveaux de cohérence
Vous pouvez configurer un niveau de cohérence par défaut sur votre compte de base de données qui s’applique tooall collections (et les bases de données) sous votre compte de base de données Cosmos. Par défaut, toutes les lectures et les requêtes exécutées sur hello ressources définies par l’utilisateur utilisent le niveau de cohérence par défaut hello spécifié sur le compte de base de données hello. Vous pouvez assouplir le niveau de cohérence hello d’une requête de lecture/spécifique demande à l’aide de chacune des hello API prises en charge. Il existe cinq types de niveaux de cohérence pris en charge par le protocole de réplication de base de données Azure Cosmos hello offrant un compromis clair entre des garanties de cohérence spécifiques et les performances, comme décrit dans cette section.

**Remarque**: 

* Cohérence forte offre un [linearizability](https://aphyr.com/posts/313-strong-consistency-models) garantie avec hello lit la version la plus récente hello tooreturn garantie d’un élément. 
* Cohérence forte garantit qu’une écriture est visible uniquement après sa validation durable par le quorum majoritaire de hello de réplicas. Une écriture est validée soit synchrone durablement par hello principal et quorum hello de bases de données secondaires, ou elle est abandonnée. Une lecture est toujours acceptée par une majorité hello lire le quorum, un client ne peut jamais voir une écriture partielle ou non validée et est toujours garanti tooread hello dernier accusé de réception écriture. 
* Comptes Cosmos DB Azure qui sont la cohérence forte toouse configuré ne peut pas associer plusieurs régions Azure avec leur compte de base de données Azure Cosmos. 
* Hello le coût d’une opération de lecture (en termes de [unités de requête](request-units.md) consommée) à forte cohérence est supérieure à la session et éventuelle, mais même hello comme obsolescence limitée.

**Obsolescence limitée**: 

* Cohérence de l’obsolescence limitée garantit que les lectures hello risque de souffrir écritures au maximum *K* versions ou des préfixes d’un élément ou *t* intervalle de temps. 
* Par conséquent, lorsque choix délimitée péremption, hello « péremption » peut être configurée de deux manières : nombre de versions *K* d’élément hello par lequel hello lectures rester derrière les écritures hello et intervalle de temps hello *t* 
* Délimitée péremption offres total global de la commande à l’exception de hello « fenêtre péremption. » Hello monotone lire garanties existe dans une région à l’intérieur et à l’extérieur de hello « fenêtre péremption. » 
* La cohérence Obsolescence limitée fournit une meilleure garantie de cohérence que le niveau Session ou Éventuel. Pour les applications distribuées globalement, nous vous recommandons de qu'utiliser obsolescence limitée pour les scénarios où vous aimeriez toohave forte cohérence mais également la disponibilité de 99,99 % et une faible latence. 
* Les comptes Azure Cosmos DB configurés avec une cohérence de type obsolescence limitée peuvent associer n’importe quel nombre de régions Azure avec leur compte. 
* Hello le coût d’une opération de lecture (en termes de RUs consommée) avec obsolescence limitée est supérieure à la session et la cohérence éventuelle, mais même hello en tant que la cohérence forte.

**Session**: 

* Contrairement aux modèles de la cohérence globale hello offertes par les niveaux de cohérence de péremption fort et limité, la cohérence de session est étendue tooa session du client. 
* La cohérence Session est idéale pour tous les scénarios dans lesquels une session utilisateur ou d’appareil est impliquée, car elle garantit des lectures unitones, des écritures unitones et des garanties de lecture de vos propres écritures. 
* Fournit une cohérence prévisible pour une session et débit de lecture maximale tout en offrant des lectures et écritures de latence la plus faible hello. 
* Les comptes Azure Cosmos DB configurés avec une cohérence de type session peuvent associer n’importe quel nombre de régions Azure avec leur compte. 
* Hello du coût d’une opération de lecture (en termes de RUs consommée) avec une session de niveau de cohérence est inférieur à péremption fort et limitée, mais la cohérence éventuelle de plus de

<a id="consistent-prefix"></a>
**Préfixe cohérent** : 

* Préfixe cohérente garantit qu’en l’absence d’autres écritures, les réplicas hello au sein du groupe de hello convergent. 
* Le niveau de cohérence préfixe cohérent garantit que les lectures ne voient jamais d’écritures dans le désordre. Si les écritures ont été effectuées dans l’ordre de hello `A, B, C`, puis un client voit soit `A`, `A,B`, ou `A,B,C`, mais jamais en désordre comme `A,C` ou `B,A,C`.
* Les comptes Azure Cosmos DB configurés avec une cohérence de type préfixe cohérent peuvent associer n’importe quel nombre de régions Azure avec leur compte. 

**Eventual (Éventuel)**: 

* Cohérence éventuelle garantit qu’en l’absence d’autres écritures, les réplicas hello au sein du groupe de hello convergent. 
* Cohérence éventuelle est hello plus faible cohérence où un client peut obtenir les valeurs hello qui sont antérieurs au hello ceux qu’il avait auparavant.
* Cohérence éventuelle fournit une cohérence de lecture hello plus faible, mais offre hello latence la plus faible pour les lectures et écritures.
* Les comptes Azure Cosmos DB configurés avec une cohérence éventuelle peuvent associer n’importe quel nombre de régions Azure avec leur compte. 
* Hello le coût d’une opération de lecture (en termes de RUs consommée) au niveau de cohérence éventuelle de hello est hello plus petit de tous les niveaux de cohérence de base de données Azure Cosmos hello.

## <a name="configuring-hello-default-consistency-level"></a>Configuration du niveau de cohérence hello par défaut
1. Bonjour [portail Azure](https://portal.azure.com/)hello Jumpbar, cliquez sur dans **base de données Azure Cosmos**.
2. Bonjour **base de données Azure Cosmos** panneau, sélectionnez hello de base de données compte toomodify.
3. Dans le panneau de compte hello, cliquez sur **par défaut de la cohérence**.
4. Bonjour **cohérence par défaut** panneau, niveau de cohérence hello sélectionnez Nouveau, cliquez sur **enregistrer**.
   
    ![Capture d’écran en mettant en surbrillance icône des paramètres hello et l’entrée de cohérence par défaut](./media/consistency-levels/database-consistency-level-1.png)

## <a name="consistency-levels-for-queries"></a>Niveaux de cohérence des requêtes
Par défaut, pour les ressources définies par l’utilisateur, au niveau de cohérence hello pour les requêtes est hello même niveau de cohérence hello pour des lectures. Par défaut, les index hello est mis à jour synchrone chaque insert, remplacer ou supprimer d’un conteneur de base de données Cosmos toohello élément. Cela permet les requêtes hello toohonor hello même niveau de cohérence que celui du point de lectures. Lors de la base de données Azure Cosmos est optimisé en écriture et prend en charge des volumes maintenus d’écritures, maintenance d’index synchrones et traiter les requêtes de cohérence, vous pouvez configurer certaine tooupdate collections leur index tardivement. Indexation différée davantage améliore les performances d’écriture hello et est idéale pour les scénarios d’ingestion en bloc lorsqu’une charge de travail est principalement lectures.  

| Mode d'indexation | Lectures | Requêtes |
| --- | --- | --- |
| Cohérence (par défaut) |Choisir parmi Fort, Obsolescence limitée, Session, Préfixe cohérent et Éventuel |Choisir parmi Fort, Obsolescence limitée, Session et Éventuel |
| Différé |Choisir parmi Fort, Obsolescence limitée, Session, Préfixe cohérent et Éventuel |Eventual (Éventuel) |
| Aucun |Choisir parmi Fort, Obsolescence limitée, Session, Préfixe cohérent et Éventuel |Non applicable |

Comme avec les demandes de lecture, vous pouvez réduire le niveau de cohérence hello d’une demande de requête spécifique dans chaque API.

## <a name="next-steps"></a>Étapes suivantes
Si vous souhaitez que toodo plus lors de la lecture sur les niveaux de cohérence et compromis, nous vous recommandons de hello suivant des ressources :

* Doug Terry. La cohérence des données répliquées expliquée par le baseball (vidéo).   
  [https://www.youtube.com/watch?v=gluIh8zd26I](https://www.youtube.com/watch?v=gluIh8zd26I)
* Doug Terry. La cohérence des données répliquées basée sur l’exemple du baseball.   
  [http://research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.pdf](http://research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.pdf)
* Doug Terry. Le niveau Par session garantit des données répliquées peu cohérentes.   
  [http://dl.acm.org/citation.cfm?id=383631](http://dl.acm.org/citation.cfm?id=383631)
* Daniel Abadi. La cohérence des compromis en termes de conception de systèmes de base de données distribué moderne : extrémité de fin n'est qu’une partie d’un récit hello ».   
  [http://computer.org/csdl/mags/co/2012/02/mco2012020037-abs.html](http://computer.org/csdl/mags/co/2012/02/mco2012020037-abs.html)
* Peter Bailis, Shivaram Venkataraman, Michael J. Franklin, Joseph M. Hellerstein, Ion Stoica. Probabilités en fonction de l'obsolescence (PBS) pour les quorums partiels pratiques   
  [http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf)
* Werner Vogels. Niveau de cohérence Éventuel repensé.    
  [http://allthingsdistributed.com/2008/12/eventually_consistent.html](http://allthingsdistributed.com/2008/12/eventually_consistent.html)
* Moni Naor, Avishai laine, hello charge, la capacité et disponibilité de Quorum systèmes, Journal SIAM Computing, v.27 n.2, p.423-447, avril 1998.
  [http://epubs.siam.org/doi/abs/10.1137/S0097539795281232](http://epubs.siam.org/doi/abs/10.1137/S0097539795281232)
* Sebastian Burckhardt, Chris Dern, Macanal Musuvathi, Roy Tan, gamme : un linearizability complet et automatique vérificateur, procédure de conférence de ACM SIGPLAN 2010 hello sur la programmation de langage conception et implémentation, 05-10 juin 2010, Toronto, Ontario, Canada [doi > 10.1145/1806596.1806634] [http://dl.acm.org/citation.cfm?id=1806634](http://dl.acm.org/citation.cfm?id=1806634)
* Peter Bailis, Shivaram Venkataraman, Michael J. Franklin, Joseph M. Hellerstein, Ion Stoica, Probabilistically délimitée péremption pour pratiques quorums partielles, une procédure de hello VLDB dotation, v.5 n.8, p.776-787, avril 2012 [http:// DL.ACM.org/citation.cfm?ID=2212359](http://dl.acm.org/citation.cfm?id=2212359)
