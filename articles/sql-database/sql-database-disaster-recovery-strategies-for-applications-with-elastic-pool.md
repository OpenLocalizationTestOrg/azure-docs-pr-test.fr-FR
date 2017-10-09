---
title: "solutions de récupération d’urgence aaaDesign - base de données SQL Azure | Documents Microsoft"
description: "Découvrez comment toodesign votre solution de cloud de récupération d’urgence en choisissant le modèle de basculement droite hello."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 2db99057-0c79-4fb0-a7f1-d1c057ec787f
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 9d9eca7570c7a01c992d0b33d449721709b471c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-strategies-for-applications-using-sql-database-elastic-pools"></a>Stratégies de récupération d’urgence pour les applications utilisant les pools élastiques de bases de données SQL
Années hello, nous avons appris que les services de cloud computing ne sont pas sans poser de problèmes et incidents catastrophiques se produisent. Base de données SQL fournit plusieurs fonctionnalités tooprovide pour la continuité hello de votre application lorsque ces incidents se produisent. [Pools élastiques](sql-database-elastic-pool.md) et prend en charge les bases de données uniques hello même type de fonctionnalités de récupération d’urgence. Cet article décrit plusieurs stratégies de récupération d’urgence pour les pools élastiques qui tirent parti de ces fonctionnalités de continuité des activités de la base de données SQL.

Cet article utilise hello suivant le modèle d’application SaaS ISV canonique :

<i>Une application web moderne de nuage configure une base de données SQL pour chaque utilisateur final. Hello ISV a de nombreux clients et utilise plusieurs bases de données, appelées bases de données client. Étant donné que les bases de données clientes hello ont en général les modèles d’activités imprévisibles, hello ISV utilise un coût de base de données pool élastique toomake hello très prévisible sur de longues périodes. pool élastique de Hello simplifie également la gestion des performances hello lorsque l’activité des utilisateurs hello des pics se produisent. En outre application hello de toohello client bases de données utilise également plusieurs bases de données des profils utilisateur toomanage, sécurité, collecter etc. des modèles d’utilisation. Disponibilité des clients individuels de hello n’affecte pas la disponibilité de l’application hello dans son ensemble. Toutefois, hello et performances des bases de données de gestion est essentielles pour la fonction de l’application hello et si les bases de données de gestion hello sont l’ensemble de l’application hello hors connexion est hors connexion.</i>  

Cet article aborde les stratégies de récupération d’urgence qui couvrent un éventail de scénarios de coût démarrage sensibles applications tooones avec des exigences strictes de disponibilité.

## <a name="scenario-1-cost-sensitive-startup"></a>Scénario 1 Start-up soucieuse des coûts
<i>Ma jeune entreprise a un budget très serré.  Je veux toosimplify déploiement et gestion de l’application hello et je peux demander à un contrat SLA limité pour les clients individuels. Mais je veux application hello de tooensure comme un entier n’est jamais en mode hors connexion.</i>

spécification de simplicité toosatisfy hello déployer toutes les bases de données client dans un pool élastique Bonjour région Azure de votre choix et déployer des bases de données de gestion en tant que bases de données uniques géo-répliquées. Hello récupération d’urgence de clients, utilisez la géo-restauration, ce qui est fourni sans coût supplémentaire. disponibilité tooensure hello hello des bases de données de gestion, géo-répliquer les région tooanother à l’aide d’un groupe de basculement automatique (dans la version préliminaire) (étape 1). coût Hello de configuration de la récupération d’urgence hello dans ce scénario est égal toohello le coût total de bases de données secondaires hello. Cette configuration est illustrée dans le diagramme suivant de hello.

![La figure 1](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-1.png)

Si une panne se produit dans la région principale de hello, hello toobring d’étapes de récupération en ligne votre application sont illustrées par le diagramme suivant de hello.

* groupe de basculement Hello lance le basculement automatique d’une région de récupération d’urgence toohello hello gestion de base de données. application Hello est reconnectée automatiquement toohello nouveaux primaire et tous les nouveaux comptes et les bases de données clientes sont créés dans la région de récupération d’urgence hello. les clients existants de Hello voient leurs données temporairement indisponibles.
* Créer un pool élastique de hello avec hello même configuration que le pool d’origine de hello (2).
* Utiliser des copies de toocreate géo-restauration de bases de données clientes hello (3). Vous pouvez envisager de déclenchement des restaurations individuelles de hello par des connexions de l’utilisateur final hello ou utiliser certaines autres schéma spécifiques à l’application en priorité.


À ce stade votre application est en ligne dans la région de récupération d’urgence hello, mais que certains clients délai lors de l’accès à leurs données.

![Figure 2](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-2.png)

Si la panne de hello était temporaire, il est possible de que cette région primaire hello est récupérée par Azure avant que toutes les restaurations de base de données hello soient terminées dans la région de hello récupération d’urgence. Dans ce cas, orchestrer le déplacement région principale hello application toohello précédent. processus de Hello prend les mesures de hello illustrés le diagramme suivant de hello.

* Annulez toutes les requêtes de géo-restauration en attente.   
* Basculer hello gestion des bases de données toohello région principale (5). Après la récupération de la région de hello, indistinctement ancien de hello est devenues automatiquement les bases de données secondaires. Les rôles sont à nouveau permutés. 
* Modifier connexion chaîne toopoint toohello arrière principal la région l’application hello. Maintenant tous les nouveaux comptes et les bases de données clientes sont créés dans la région principale de hello. Les données de certains clients existants sont temporairement indisponibles.   
* Définissez toutes les bases de données dans hello DR pool tooread uniquement tooensure qu'ils ne peuvent pas être modifiés dans la région de récupération d’urgence hello (6). 
* Pour chaque base de données Bonjour pool de récupération d’urgence qui a changé depuis la récupération de hello, renommer ou supprimer des bases de données correspondantes hello dans le pool principal d’hello (7). 
* Hello de copie mise à jour des bases de données à partir de hello pool principal de récupération d’urgence pool toohello (8). 
* Supprimer le pool de récupération d’urgence hello (9)

À ce stade votre application est en ligne dans la région principale de hello avec toutes les bases de données clientes disponibles dans le pool principal d’hello.

![Figure 3](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-3.png)

clé de Hello **bénéficier** de cette stratégie est faible coût en cours de la redondance de couche données. Sauvegardes sont effectuées automatiquement par hello service de base de données SQL avec aucune réécriture de l’application et sans coût supplémentaire.  Hello entraîne des coûts uniquement les bases de données élastiques hello sont restaurés. Hello **compromis** est que la récupération complète de hello de toutes les bases de données clientes prend beaucoup de temps. Hello durée dépend hello nombre total de restaurations vous lancer dans la récupération d’urgence de hello région et la taille globale de hello locataire des bases de données. Même si vous modifier la priorité sur d’autres restaurations de certains clients, vous sont en concurrence avec hello tous les autres restaurations lancées à partir de hello la même région comme service de hello détermine et limite toominimize hello l’impact global sur les bases de données clients hello existants. En outre, récupération hello de bases de données hello client ne peut pas démarrer tant que nouveau pool élastique hello dans la région de récupération d’urgence hello est créé.

## <a name="scenario-2-mature-application-with-tiered-service"></a>Scénario 2 Application arrivée à maturité avec un service sur plusieurs niveaux
<i>Je propose une application SaaS mature avec plusieurs offres de service et différents contrats SLA pour les clients qui utilisent une version d’évaluation gratuite ou une version payante. Pour les clients à l’essai hello, j’ai tooreduce hello coût autant que possible. Clients à l’essai peuvent prendre le temps d’arrêt, mais je veux tooreduce sa probabilité. Pourquoi les clients payants, les temps d’arrêt est un risque de vol. Donc de toomake assurer que les clients qui paient sont toujours en mesure de tooaccess leurs données.</i> 

toosupport ce scénario, distinct hello locataires de test à partir de payé locataires en les plaçant dans des pools élastiques distincts. les clients de version d’évaluation Hello ont eDTU inférieur par client et inférieure SLA avec un temps de récupération plus long. les clients qui paient Hello sont dans un pool avec eDTU plus élevée par le client et un contrat SLA plus élevé. tooguarantee hello plus faible temps de récupération, les bases de données des clients qui paient hello client sont répliquées. Cette configuration est illustrée dans le diagramme suivant de hello. 

![Figure 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-4.png)

Comme dans le scénario de première hello, bases de données de gestion hello ne sont assez actives une seule base de données géo-répliquées pour (1). Cela garantit des performances prévisibles hello pour l’abonnement du client, les mises à jour de profil et les autres opérations de gestion. région dans lesquels résidence indistinctement hello de bases de données de gestion hello Hello est la région primaire hello et région hello dans lesquels résident les bases de données secondaires hello de bases de données de gestion hello est la région de hello récupération d’urgence.

Hello bases de données des clients qui paient client ont des bases de données actives Bonjour « payant « pool configuré dans la région principale de hello. Configurer un pool secondaire avec le même nom dans la région de hello récupération d’urgence de hello. Chaque client est toohello de géo-répliquées de pool secondaire (2). Cela permet une récupération rapide de toutes les bases de données client à l’aide de la fonctionnalité de basculement. 

Si une panne se produit dans la région principale de hello, hello toobring d’étapes de récupération en ligne votre application sont illustrées dans le diagramme suivant de hello :

![Figure 5](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-5.png)

* Basculer immédiatement la région de récupération d’urgence toohello hello gestion des bases de données (3).
* Modifier connexion chaîne toopoint toohello récupération d’urgence la région l’application hello. Maintenant tous les nouveaux comptes et les bases de données clientes sont créés dans la région de récupération d’urgence hello. les clients existants de version d’évaluation Hello voient leurs données temporairement indisponibles.
* Basculer hello payé de pool de toohello de bases de données du locataire dans tooimmediately de région de récupération d’urgence hello restaurer leur disponibilité (4). Basculement de hello étant une modification du niveau de métadonnées rapide, envisagez une optimisation où hello les basculements individuels sont déclenchés à la demande par des connexions de l’utilisateur final hello. 
* Si la taille d’eDTU de pool secondaire était inférieure à hello principal, car les bases de données secondaires hello uniquement requis hello capacité tooprocess hello modification enregistre pendant qu’ils ont des bases de données secondaires, augmentez immédiatement la capacité du pool hello maintenant tooaccommodate hello complète charge de travail de tous les locataires (5). 
* Créer nouveau pool élastique d’hello avec hello même nom et même hello configuration dans la région de hello récupération d’urgence pour les bases de données clients hello d’évaluation (6). 
* Une fois le pool de clients hello d’évaluation est créé, utilisez bases de données géo-restauration toorestore hello client d’évaluation individuelle dans un nouveau pool d’hello (7). Envisagez de déclencher les restaurations individuelles hello par des connexions de l’utilisateur final hello ou utiliser certaines autres schéma spécifiques à l’application en priorité.

À ce stade votre application est en ligne dans la région de récupération d’urgence hello. Tous les clients qui paient ont accès aux données tootheir tandis que les clients à l’essai hello subissent délai lors de l’accès à leurs données.

Lorsque la région principale de hello est récupérée par Azure *après* vous avez restauré application hello chez hello récupération d’urgence, vous pouvez continuer à exécuter des application hello dans cette région ou vous pouvez décider de région principale de toofail toohello précédent. Si la région primaire hello est récupérée *avant* hello basculement terminée, envisagez de restauration immédiatement. la restauration automatique Hello prend les mesures de hello illustrés dans le diagramme suivant de hello : 

![Figure 6](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-6.png)

* Annulez toutes les requêtes de géo-restauration en attente.   
* Basculer les bases de données de gestion hello (8). Après la récupération de la région de hello, hello ancien serveur principal devient automatiquement hello secondaire. Maintenant il devient hello principal à nouveau.  
* Basculer hello payé des bases de données client (9). De même, après la récupération de la région de hello, indistinctement ancien de hello deviennent automatiquement les bases de données secondaires hello. Ils sont désormais à nouveau indistinctement de hello. 
* Hello du jeu de restauration des bases de données d’évaluation qui ont été modifiés dans la région de récupération d’urgence hello tooread uniquement (10).
* Pour chaque base de données de pool de récupération d’urgence de clients à l’essai hello qui a changé depuis la récupération de hello, renommer ou supprimer la base de données correspondante hello dans le pool principal de clients à l’essai hello (11). 
* Hello de copie mise à jour des bases de données à partir de hello pool principal de récupération d’urgence pool toohello (12). 
* Supprimer le pool de récupération d’urgence hello (13) 

> [!NOTE]
> l’opération de basculement Hello est asynchrone. temps de récupération hello toominimize qu'il est important que vous exécutez commande de basculement hello client bases de données par lots de moins de 20 bases de données. 
> 
> 

clé de Hello **bénéficier** de cette stratégie est qu’elle fournit des SLA de la plus élevée hello pour hello clients payants. Elle garantit également que les nouvelles versions d’essai hello sont débloquées dès que le pool de récupération d’urgence d’évaluation hello est créé. Hello **compromis** est que ce programme d’installation augmente le coût de hello total de bases de données clientes hello par coût hello du pool de récupération d’urgence secondaire hello pour payer des clients. En outre, si le pool de hello secondaire a une taille différente, les clients qui paient hello performances inférieur après le basculement jusqu'à ce que hello mise à niveau du pool dans la région de hello récupération d’urgence est terminée. 

## <a name="scenario-3-geographically-distributed-application-with-tiered-service"></a>Scénario 3 Application dispersée géographiquement avec un service sur plusieurs niveaux
<i>Je propose une application SaaS mature avec des offres de service sur plusieurs niveaux. Je souhaitez toooffer un toomy SLA très agressif payé clients et réduire les risques de hello d’impact sur les cas de panne, car même brève interruption peut entraîner le mécontentement du client. Il est essentiel que hello payer les clients permettre toujours accéder à leurs données. les essais Hello sont gratuits et un contrat SLA n’est pas proposé pendant la période d’évaluation de hello.</i> 

toosupport ce scénario, utilisent les pools élastiques distinct trois. Configurer deux pools de taille égale avec haute Edtu par base de données dans deux hello toocontain de différentes régions payant bases de données clientes clients. pool de tiers Hello contenant les clients de la version d’évaluation de hello peut inférieur Edtu par base de données et être configuré dans un des deux régions de hello.

tooguarantee hello plus faible temps de récupération pendant les pannes, les bases de données des clients qui paient hello client sont répliquées avec 50 % de bases de données primaires hello dans chacune des régions de hello deux. De même, chaque région a 50 % de bases de données secondaires hello. De cette manière, si une région est hors connexion, seuls 50 % des hello payé des bases de données de clients sont affectés et toofail sur. Hello autres bases de données restent intacts. Cette configuration est illustrée dans hello suivant schéma :

![Figure 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-7.png)

Comme dans les scénarios précédents hello, bases de données de gestion hello sont très actifs ainsi les configurer comme unique géo-répliquées bases de données (1). Cela garantit des performances prévisibles hello d’abonnement du client hello, de mises à jour de profil et d’autres opérations de gestion. Région A est la région principale de hello pour les bases de données de gestion hello et région de hello B est utilisée pour la récupération des bases de données de gestion hello.

bases de données des clients qui paient Hello client sont également répliquées, mais avec des couleurs primaires et secondaires fractionnée entre région A et B (2). De cette manière, hello client bases de données primaires affectés par la panne de hello peuvent basculer toohello autre région et deviennent disponibles. Hello autres la moitié des bases de données clientes hello ne soient pas affectés du tout. 

le diagramme suivant Hello montre hello récupération étapes tootake si une panne se produit dans la région A.

![Figure 5](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-8.png)

* Basculer immédiatement tooregion de bases de données de gestion hello B (3).
* Modifier connexion chaîne toopoint toohello gestion des bases de données l’application hello dans la région B. Modifiez hello gestion des bases de données toomake que hello nouveaux comptes et les bases de données clientes sont créés dans la région B et bases de données client hello figurent il en tant que barre d’outils. les clients existants de version d’évaluation Hello voient leurs données temporairement indisponibles.
* Basculer hello payé toopool de bases de données du locataire 2 dans la région B tooimmediately restaurer leur disponibilité (4). Basculement de hello étant une modification du niveau de métadonnées rapide, vous pouvez envisager une optimisation où hello les basculements individuels sont déclenchés à la demande par des connexions de l’utilisateur final hello. 
* Depuis maintenant pool 2 contient uniquement les bases de données primaires, hello la charge de travail totale dans hello pool augmente et immédiatement augmenter sa taille eDTU (5). 
* Créer nouveau pool élastique d’hello avec hello même nom et même hello configuration dans la région B hello pour les bases de données clients hello d’évaluation (6). 
* Une fois le pool de hello est créé de base de données d’utilisation géo-restauration toorestore hello client d’évaluation individuelle dans le pool hello (7). Vous pouvez envisager de déclenchement des restaurations individuelles de hello par des connexions de l’utilisateur final hello ou utiliser certaines autres schéma spécifiques à l’application en priorité.

> [!NOTE]
> l’opération de basculement Hello est asynchrone. temps de récupération toominimize hello, il est important que vous exécutez commande de basculement hello client bases de données par lots de moins de 20 bases de données. 
> 

À ce stade votre application est en ligne dans la région B. Tous les clients qui paient ont accès aux données tootheir tandis que les clients à l’essai hello subissent délai lors de l’accès à leurs données.

Lors de la récupération de la région A vous devez toodecide si vous souhaitez toouse région B pour les clients à l’essai ou pool de clients à l’essai de la restauration automatique toousing hello dans la région A. Un critère pu être hello du client d’évaluation de bases de données modifiées depuis la récupération de hello. Quelle que soit cette décision, vous devez toore équilibrer les locataires de hello payé entre deux pools. Hello le diagramme suivant montre les processus hello cas d’échouent des bases de données client d’évaluation hello a de tooregion précédent.  

![Figure 6](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-9.png)

* Annuler le pool tootrial récupération d’urgence de demandes toutes les géo-restauration en attente.   
* Basculer la base de données de gestion hello (8). Après la récupération de la région de hello, ancien serveur principal de hello est automatiquement devenu hello secondaire. Maintenant il devient hello principal à nouveau.  
* Sélectionnez les bases de données client payant échouent précédent toopool 1 et initier basculement tootheir secondaires (9). Après la récupération de la région de hello, toutes les bases de données dans le pool 1 sont automatiquement les bases de données secondaires. Désormais, 50 % d’entre elles redeviennent des bases de données primaires. 
* Réduire la taille hello des 2 toohello d’origine eDTU (10).
* Jeu de tous les restauré les bases de données d’évaluation dans la région de hello B tooread uniquement (11).
* Pour chaque base de données hello d’évaluation DR pool a changé depuis la récupération de hello, renommez ou supprimez des base de données correspondante hello dans le pool principal d’évaluation hello (12). 
* Hello de copie mise à jour des bases de données à partir de hello pool principal de récupération d’urgence pool toohello (13). 
* Supprimer le pool de récupération d’urgence hello (14) 

clé de Hello **avantages** de cette stratégie sont :

* Il prend en charge les SLA plus agressif hello hello clients payants, car elle garantit qu’une panne ne peut pas avoir une incidence sur plus de 50 % de bases de données clientes hello. 
* Elle garantit que les nouvelles versions d’essai hello sont débloquées dès que le cheminement de hello DR pool est créé lors de la récupération de hello. 
* Il permet une utilisation plus efficace de la capacité du pool hello à 50 % des bases de données secondaires dans le pool 1 et 2 de pool est garantie toobe moins actives de bases de données primaires hello.

Hello principal **compromis** sont :

* les opérations CRUD Hello par rapport aux bases de données de gestion hello ont une latence plus faible pour hello utilisateurs finaux tooregion A que pour les utilisateurs finaux de hello tooregion B comme elles sont exécutées sur principal hello de bases de données de gestion hello.
* Elle nécessite une conception plus complexe de base de données de gestion hello. Par exemple, chaque enregistrement de client est une balise d’emplacement qui doit toobe modifié pendant le basculement et la restauration automatique.  
* Hello clients payants peut rencontrer des performances inférieures à la normale jusqu'à ce que hello mise à niveau du pool dans la région B est terminée. 

## <a name="summary"></a>Résumé
Cet article se concentre sur les stratégies de récupération d’urgence hello pour le niveau de base de données hello utilisé par une application mutualisée de SaaS ISV. choix de la stratégie Hello est basée sur les besoins hello d’application hello, telles que le mode d’entreprise hello, hello SLA vous toooffer tooyour clients, etc. de contrainte de budget. Description de chacun stratégie contours hello avantages et compromis afin de vous pourriez prendre une décision informée. De plus, votre propre application inclut probablement d’autres composants Azure. Vous passez en revue leur aide de la continuité des activités et Orchestrez récupération hello de niveau de base de données hello avec eux. toolearn savoir plus sur la gestion de la récupération des applications de base de données dans Azure, consultez trop[conception de solutions de cloud de récupération d’urgence](sql-database-designing-cloud-solutions-for-disaster-recovery.md).  

## <a name="next-steps"></a>Étapes suivantes
* toolearn sur les sauvegardes de base de données SQL Azure automatisée, consultez [base de données SQL des sauvegardes automatisées](sql-database-automated-backups.md).
* Pour une vue d’ensemble de la continuité des activités et des scénarios, consultez [Vue d’ensemble de la continuité des activités](sql-database-business-continuity.md).
* toolearn sur l’utilisation des sauvegardes automatisées pour la récupération, consultez [restaurer une base de données à partir de sauvegardes de hello initiées par le service](sql-database-recovery-using-backups.md).
* toolearn sur les options de récupération plus rapides, consultez [géo-réplication active](sql-database-geo-replication-overview.md).
* toolearn sur l’utilisation des sauvegardes automatisées pour l’archivage, consultez [copie de base de données](sql-database-copy.md).

