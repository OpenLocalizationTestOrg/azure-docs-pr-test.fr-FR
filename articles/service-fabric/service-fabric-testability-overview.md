---
title: "vue d’ensemble du Service d’analyse aaaFault | Documents Microsoft"
description: "Cet article décrit hello erreur Analysis Service dans le Service Fabric pour induire des erreurs et l’exécution de scénarios de test par rapport à vos services."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: timlt
editor: vturecek
ms.assetid: 1f064276-293a-4989-a513-e0d0b9fdf703
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: anmola
ms.openlocfilehash: deac16ec830aa10d4e488e60691faa9ef2b6cd33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-fault-analysis-service"></a>Introduction toohello erreur Analysis Service
Hello erreur Analysis Services est conçu pour tester les services qui reposent sur Microsoft Azure Service Fabric. Avec hello erreur Analysis Service, vous pouvez induire des erreurs significatives et exécuter des scénarios de test complet sur vos applications. Ces erreurs et les scénarios de tester et valider hello de nombreux États et transitions subissent un service tout au long de sa durée de vie, tout de façon contrôlée, sécurisée et cohérente.

Actions sont hello des erreurs individuelles ciblant un service pour le tester. Un développeur de service peut utiliser en tant que blocs de construction toowrite compliquée scénarios. Par exemple :

* Redémarrer un toosimulate de nœud de n’importe quel nombre de situations où un ordinateur ou un ordinateur virtuel est redémarré.
* Déplacer un réplica de l’équilibrage de charge toosimulate service avec état, basculement ou de mise à niveau de l’application.
* Appelez la perte du quorum dans un service avec état de toocreate une situation où les opérations d’écriture ne peut pas continuer, car il n’existe pas suffisamment réplicas « sauvegarde » ou « secondaire » tooaccept de nouvelles données.
* Appelez la perte de données sur un service avec état de toocreate une situation dans laquelle tous les États en mémoire sont complètement supprimé.

Les scénarios sont des opérations complexes composées d’une ou plusieurs actions. Hello erreur Analysis Services fournit deux scénarios intégrés :

* Scénario de chaos
* Scénario de basculement

## <a name="testing-as-a-service"></a>Tests en tant que service
Hello erreur Analysis Service est un service de système de l’infrastructure de Service est démarré automatiquement avec un cluster Service Fabric. Ce service agit comme hôte hello pour l’injection d’erreurs, l’exécution de scénario de test et analyse de l’état. 

![Service d’analyse des erreurs][0]

Lorsqu’un scénario d’action ou de test de défaillance est lancé, une commande est envoyée toohello erreur Analysis Service toorun hello action ou test de scénario de panne. Hello erreur Analysis Service est avec état afin qu’il peut fiable exécuter les scénarios et les erreurs et validez les résultats. Par exemple, un scénario de test durée d’exécution longue peut être exécuté de façon fiable par hello erreur Analysis Service. Et parce que les tests sont en cours d’exécution à l’intérieur du cluster de hello, service de hello peut examiner état hello du cluster de hello et vos services tooprovide plus d’informations sur les échecs.

## <a name="testing-distributed-systems"></a>Test des systèmes distribués
Service Fabric rend la tâche hello d’écriture et de gestion des applications évolutives distribuées sensiblement plus faciles. Hello erreur Analysis Service rend le test d’une application distribuée de la même façon plus facile. Il existe trois principaux problèmes qui doivent toobe résolu lors du test :

1. Simulation/génération d’erreurs pouvant se produire dans des scénarios concrets : un des aspects importants de hello de Service Fabric est qu’elle permet à toorecover d’applications distribuées à partir de diverses défaillances. Toutefois, tootest qui hello application est en mesure de toorecover à partir de ces échecs, nous devons un toosimulate du mécanisme/générer ces défaillances réelles dans un environnement de test contrôlé.
2. Hello capacité toogenerate corrélées échecs : Basic de hello système, tels que les défaillances réseau et d’ordinateur, sont facilement tooproduce individuellement. Génération d’un nombre important de scénarios qui peuvent se produire dans Bonjour réel suite à des interactions hello des ces échecs est non trivial.
3. Expérience unifiée au sein de divers niveaux de développement et de déploiement : de nombreux systèmes d’injection d’erreurs peuvent générer différents types de défaillances. Toutefois, expérience hello dans tous ces éléments est médiocre lorsque le déplacement à partir des scénarios de développement d’une case, hello toorunning même dans les environnements de test volumineux, toousing les teste pour des tests en production.

Bien qu’il existe plusieurs mécanismes toosolve ces problèmes, un système qui identique à hello avec les garanties requises--tous les moyen hello à partir d’un environnement de développement d’une case, tootest dans les clusters de production--est manquant. Hello erreur Analysis Services permet aux développeurs d’applications hello se concentrer sur leur logique métier de test. Hello erreur Analysis Services fournit que toutes les fonctions hello requise interaction de hello tootest du service de hello avec un système distribué hello sous-jacent.

### <a name="simulatinggenerating-real-world-failure-scenarios"></a>Simulation/Génération de scénarios de défaillances réalistes
robustesse de hello tootest d’un système distribué contre les défaillances, nous devons un toogenerate d’échecs de mécanisme. En théorie, générer une défaillance comme un nœud vers le bas semble simple, qu'il démarre atteignez hello même jeu de problèmes de cohérence que toosolve est la tentative de l’infrastructure de Service. Par exemple, si nous voulons que tooshut arrêt d’un nœud, hello requis de flux de travail est suivant de hello :

1. À partir du client de hello, émettre une demande d’arrêt du nœud.
2. Envoyer le nœud approprié de hello demande toohello.
   
    a. Si le nœud de hello n’est trouvé, il doit échouer.
   
    b. Si le nœud de hello est trouvée, elle doit retourner uniquement si le nœud de hello est arrêté.

Échec de hello tooverify à partir d’une perspective de test, les tests hello doit tooknow que lorsque cet échec ne soit induit, Échec de hello réellement se produire. garantie de Hello offre de Service Fabric est que des nœuds hello seront arrêtera ou était déjà arrêté lors de la commande hello atteint le nœud de hello. Dans les deux cas hello test doit être raison toocorrectly en mesure sur l’état de hello et réussissent ou échouent correctement dans sa validation. Un système est implémenté en dehors de hello de toodo Service Fabric que même jeu d’échecs a accès au que réseau sont nombreuses, le matériel et les problèmes de logiciel, ce qui empêcheraient de fournir des garanties précédents hello. En présence de hello des problèmes hello indiqué précédemment, le Service Fabric reconfigurer hello cluster état toowork des problèmes de hello et par conséquent hello erreur Analysis Service aura toujours hello toogive en mesure de droite la valeur de garanties.

### <a name="generating-required-events-and-scenarios"></a>Génération des événements et scénarios requis
Simulation d’un échec réel constamment est difficile toostart avec, hello capacité toogenerate corrélée échecs est encore davantage. Par exemple, une perte de données se produit dans un service rendues persistantes avec état lorsque hello suivant les choses se produire :

1. Uniquement un quorum d’écriture des réplicas de hello sont en retard sur la réplication. Tous les réplicas secondaires hello être en décalage hello principal.
2. quorum d’écriture Hello tombe en panne en raison de réplicas hello en panne (en raison de package de code tooa ou nœud en panne).
3. quorum d’écriture Hello ne peut pas revenir données hello pour les réplicas de hello étant perdues (échéance toodisk endommagée ou réinitialisation de l’ordinateur).

Ces échecs corrélés se produisent dans le monde réel de hello, mais pas aussi souvent que les échecs. tootest de capacité Hello pour ces scénarios avant qu’ils se produisent en production est critique. Encore plus important est hello capacité toosimulate ces scénarios avec des charges de travail dans des circonstances contrôlées (intercepteur hello du jour hello avec les ingénieurs de pont). Qui est beaucoup plu qu’il se produire pour hello première en production à 02:00.

### <a name="unified-experience-across-different-environments"></a>Expérience unifiée au sein d’environnements différents
pratique de Hello traditionnellement toocreate trois types différents d’expériences, l’autre pour l’environnement de développement hello, un pour les tests et un pour la production. modèle de Hello était :

1. Dans l’environnement de développement hello, produire des transitions d’état qui permettent des tests unitaires de méthodes individuelles.
2. Dans l’environnement de test hello, produire des tests de bout en bout tooallow échecs qui vérifient les différents scénarios d’échec.
3. Conservez hello production environnement dénué tooprevent tout non naturelle échecs et la tooensure qu’il y a toofailure de réponse humaine extrêmement rapide.

Dans l’infrastructure de Service, par le biais hello erreur Analysis Service, nous proposons en conséquence tooturn cela autour et utilisez hello même méthodologie de tooproduction d’environnement de développement. Il existe deux façons tooachieve cela :

1. échecs de tooinduce contrôlée, utilisez hello erreur Analysis Service API à partir d’un environnement d’une case tooproduction de façon hello tous les clusters.
2. toogive hello une peste qui provoque des échecs automatique d’induction automatique d’échecs, utilisez hello erreur Analysis Service toogenerate du cluster. Contrôle taux hello d’échecs via la configuration active hello même service toobe testé différemment dans différents environnements.

Avec Service Fabric, même si échelle hello d’échecs est différent dans différents environnements de hello, les mécanismes réels hello serait identiques. Ainsi, pour beaucoup plus rapide au déploiement de code pipeline et hello capacité tootest hello services sous des charges réelles.

## <a name="using-hello-fault-analysis-service"></a>À l’aide de hello erreur Analysis Service
**C#**

Fonctionnalités de Service d’analyse de pannes sont dans l’espace de noms hello System.Fabric Bonjour package NuGet de Microsoft.ServiceFabric. fonctionnalités de Service d’analyse de pannes toouse hello, inclure package nuget de hello en tant que référence dans votre projet.

**PowerShell**

toouse PowerShell, vous devez installer hello SDK de l’infrastructure de Service. Après avoir hello que SDK est installé, hello ServiceFabric PowerShell module est automatiquement chargé pour vous toouse.

## <a name="next-steps"></a>Étapes suivantes
toocreate réellement l’échelle du cloud services, il est critique tooensure, avant et après le déploiement, que les services peuvent résister aux défaillances du monde réel. Dans le monde de services hello aujourd'hui, hello capacité tooinnovate rapidement et déplacez le code tooproduction rapidement est très importante. Hello erreur Analysis Services permet de toodo les développeurs de service précisément qui.

Commencer à tester vos applications et services à l’aide intégrée de hello [les scénarios de test](service-fabric-testability-scenarios.md), ou créer vos propres scénarios de test à l’aide de hello [actions d’erreur](service-fabric-testability-actions.md) fournie par hello erreur Analysis Service.

<!--Image references-->
[0]: ./media/service-fabric-testability-overview/faultanalysisservice.png
