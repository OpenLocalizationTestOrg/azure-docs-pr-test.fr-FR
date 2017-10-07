---
title: "Considérations de performances et l’optimisation de la recherche aaaAzure | Documents Microsoft"
description: "Réglage des performances d’Azure Search et configuration d’une mise à l’échelle optimale"
services: search
documentationcenter: 
author: LiamCavanagh
manager: pablocas
editor: 
ms.assetid: 4d3cd864-29d2-4921-be0d-a3f1a819de46
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: 725149ba32773ab6b4c9d4b441424aba78db7c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-performance-and-optimization-considerations"></a>Considérations sur les performances et l’optimisation d’Azure Search
Une expérience de recherche est une clé toosuccess nombreux mobile et des applications web. Immobilier, à partir de catalogues de tooonline tooused voiture places de marché, une recherche rapide et résultats pertinents affectera expérience hello. Ce document est prévue toohelp découvrir les meilleures pratiques pour comment hello tooget parti d’Azure Search, en particulier pour des scénarios avancés avec sophistiqué configuration requise pour l’évolutivité, de prise en charge multilingue ou de classement personnalisé.  En outre, ce document détaille les mécanismes internes et décrit les approches qui fonctionnent efficacement dans les applications clientes réelles.

## <a name="performance-and-scale-tuning-for-search-services"></a>Réglage des performances et de la mise à l’échelle pour les services de recherche
Nous sommes tous les moteurs toosearch utilisés tels que Bing et Google et hello hautes performances qu’elles proposent.  Par conséquent, lorsque les clients utilisent la fonction de recherche de votre application mobile ou web, ils s’attendent à bénéficier des mêmes performances.  Lors de l’optimisation des performances de la recherche, une des approches de meilleures hello est toofocus sur la latence, ce qui est le temps hello toocomplete et retourner les résultats d’une requête est.  Lors de l’optimisation de la latence de recherche, il est important de noter les points suivants :

1. Choisir une latence sur la cible (ou la durée maximale) qu’une demande de recherche par défaut doit prendre toocomplete.
2. Créer et tester une charge de travail réelle par rapport à votre service de recherche avec un jeu de données réaliste de toomeasure ces taux de latence.
3. Démarrer avec un petit nombre de requêtes par seconde (QPS) et continuer le nombre de hello tooincrease exécutée dans un test de hello tant que requête hello latence inférieure hello défini par la latence sur la cible.  Il s’agit d’un toohelp banc d’essai important que prévoir l’échelle à mesure que votre application augmente l’utilisation.
4. Dans la mesure du possible, réutilisez les connexions HTTP.  Si vous utilisez hello Azure Search .NET SDK, cela signifie que vous devez réutiliser une instance ou [SearchIndexClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.searchindexclient) d’instance et si vous utilisez hello API REST, vous devez le réutiliser un client HTTP unique.

Lors de la création de ces charges de travail de test, il existe certaines caractéristiques de tookeep Azure Search à l’esprit :

1. Il est possible toopush autant les requêtes de recherche à la fois, que les ressources de hello disponibles dans votre service Azure Search seront saturé au point.  Dans ce cas, vous verrez les codes de réponse HTTP 503.  Pour cette raison, il est meilleure toostart avec différentes plages de recherche les demandes toosee hello différences dans le taux de latence que vous ajoutez plus de requêtes de recherche.
2. Le téléchargement de contenu tooAzure recherche aura un impact sur hello les performances globales et la latence de hello service Azure Search.  Si vous pensez que les données toosend tandis que les utilisateurs effectuant des recherches, il est important tootake cette charge de travail en compte dans vos tests.
3. Pas de chaque requête de recherche effectuera à hello même les niveaux de performance.  Par exemple, une recherche de document ou une suggestion de recherche s’exécutera plus rapidement qu’une requête comportant un nombre important de facettes et les filtres.  Il s’agit des meilleures tootake hello différentes requêtes souhaitées toosee en compte lors de la génération de vos tests.  
4. Variation de demandes de recherche est importante, car si vous exécutez en permanence hello les mêmes requêtes de recherche, mise en cache des données de performances toomake de début recherche mieux qu’il peut avec une requête plus disparates défini.

> [!NOTE]
> [Test de charge Visual Studio](https://www.visualstudio.com/docs/test/performance-testing/run-performance-tests-app-before-release) est un tooperform très bonne façon votre test d’évaluation teste car elle vous permet les demandes tooexecute HTTP que vous avez besoin pour l’exécution de requêtes sur Azure Search et Active la parallélisation des requêtes.
> 
> 

## <a name="scaling-azure-search-for-high-query-rates-and-throttled-requests"></a>Mise à l’échelle d’Azure Search pour obtenir des taux de requêtes élevés et des requêtes limitées
Lorsque vous recevez trop de demandes d’accélérée ou dépassez votre taux de latence cible à partir d’une charge accrue de requête, vous pouvez consulter le taux de latence toodecrease de deux manières :

1. **Augmentation des réplicas :** un réplica est comme une copie de vos données, ce qui permet à Azure Search tooload équilibrer les demandes sur hello plusieurs copies.  Tous les équilibrage de charge et la réplication des données entre des réplicas est gérée par Azure Search, et vous pouvez modifier le nombre de hello de réplicas allouée pour votre service à tout moment.  Vous pouvez allouer des réplicas too12 dans un service de recherche Standard et 3 dans un service de recherche de base. Les réplicas peuvent être ajusté à partir de hello [portail Azure](search-create-service-portal.md) ou [PowerShell](search-manage-powershell.md).
2. **Augmenter le niveau de recherche :** la Recherche Azure est fournie avec un certain [nombre de niveaux](https://azure.microsoft.com/pricing/details/search/) et chacun de ces niveaux offre différents niveaux de performances.  Dans certains cas, vous avez peut-être nombreuses requêtes ce niveau hello que vous êtes sur ne peut pas fournir les vitesses de transmission suffisamment faible latence, même lorsque les réplicas sont surexploités.  Dans ce cas, vous souhaiterez tooconsider tirant parti de niveaux de recherche supérieure hello comme niveau d’Azure Search S3 hello qui convient pour les scénarios avec un grand nombre de documents et les charges de travail très élevé de requête.

## <a name="scaling-azure-search-for-slow-individual-queries"></a>Mise à l’échelle d’Azure Search pour des requêtes individuelles lentes
Une autre raison pourquoi les taux de latence peuvent être lents est à partir d’une seule requête prend trop de temps toocomplete.  Dans ce cas, l’ajout de réplicas n’améliorera pas les taux de latence.  Il existe alors deux options possibles :

1. **Augmenter les partitions** Une partition est un mécanisme permettant de répartir vos données sur des ressources supplémentaires.  Pour cette raison, lorsque vous ajoutez une deuxième partition, vos données sont divisées en deux.  Une troisième partition divise votre index en trois, etc.  Cela a également effet hello que dans certains cas, les requêtes lentes seront exécutera plus rapidement en raison de la parallélisation toohello de calcul.  Il existe quelques exemples dans lesquels cette parallélisation fonctionne très bien avec des requêtes affichant une faible sélectivité.  Il s’agit de requêtes qui correspondent au nombre de documents ou lorsque des facettes doit tooprovide compte sur un grand nombre de documents.  Dans la mesure où il existe qu'un grand nombre de calculs nécessaires pertinence de hello tooscore de documents de hello toocount hello numéros ou des documents, l’ajout de partitions supplémentaires peuvent aider à tooprovide des calculs supplémentaires.  
   
   Il peut y avoir un maximum de 12 partitions dans le service de recherche Standard et 1 partition dans le service de recherche de base hello.  Les partitions peuvent être ajustés à partir de hello [portail Azure](search-create-service-portal.md) ou [PowerShell](search-manage-powershell.md).
2. **Champs de cardinalité élevée de limitation :** un champ de cardinalité élevée consiste en un facetable filtrable champ qui a un nombre important de valeurs uniques et par conséquent, adopte un grand nombre de ressources toocompute résultats.   Par exemple, la définition d’un champ de Description ou un ID de produit comme filterable/facetable créerait une cardinalité élevée, car la plupart des valeurs hello à partir du document toodocument est unique. Dans la mesure du possible, limiter le nombre de hello de champs de cardinalité élevée.
3. **Niveau de recherche d’augmentation :** remontant tooa plus élevé de niveau d’Azure Search peut être des performances de tooimprove un autre moyen de requêtes lentes.  Chaque niveau supérieur propose également un processeur plus rapide et plus de mémoire, ce qui peut avoir un impact positif sur les performances des requêtes.

## <a name="scaling-for-availability"></a>Mise à l’échelle pour la disponibilité
Les réplicas permettent non seulement de réduire la latence des requêtes mais ils peuvent également offrir une plus grande disponibilité.  Avec un seul réplica, attendez-vous à des temps morts périodiques d’échéance tooserver redémarrages après les mises à jour logicielles ou d’autres événements de maintenance qui seront produit.  Par conséquent, il est important tooconsider si votre application requiert une haute disponibilité des recherches (requêtes) ainsi que les écritures (événements d’indexation).  Azure Search offre des options de contrat SLA sur tous les hello services de recherche avec hello suivant d’attributs :

* 2 réplicas pour la haute disponibilité des charges de travail en lecture seule (requêtes)
* 3 réplicas (ou plus) pour la haute disponibilité des charges de travail en lecture-écriture (requêtes et indexation)

Pour plus d’informations, visitez hello [contrat de niveau de Service de recherche Azure](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

Étant donné que les réplicas sont des copies de vos données, ayant plusieurs réplicas permet de redémarrages d’ordinateur Azure Search toodo et toobe toocontinue exécutée sur des requêtes de maintenance par rapport à un réplica à un moment tout en autorisant hello autres réplicas.  Pour cette raison, vous devez également tooconsider comment ce temps mort peut affecter les requêtes hello qui maintenant ont toobe exécutée sur une seule copie de moins de données de hello.

## <a name="scaling-geo-distributed-workloads-and-provide-geo-redundancy"></a>Mise à l’échelle de charges de travail géo-distribuées et géo-redondance
Pour les charges de travail géo-distribué, vous constaterez que les utilisateurs trouve loin d’être de centre de données hello héberge votre service Azure Search ont des taux de latence plus élevées.  Pour cette raison, il est souvent important toohave recherche plusieurs services dans des régions qui se trouvent dans les utilisateurs de toothese proximité plus proche.  Azure Search ne fournit pas actuellement une méthode automatisée des index de recherche de Azure géo-réplication entre les régions, mais il existe quelques techniques qui peuvent être utilisés que peuvent rendre cette tooimplement simple de processus et à gérer. Ils sont présentés dans hello sections suivantes.

l’objectif d’un ensemble de géo-distribué de services de recherche Hello est toohave deux ou plusieurs index disponibles dans deux ou plusieurs régions où un utilisateur sera routé service Azure Search toohello qui fournit la latence la plus faible de hello comme dans cet exemple :

   ![Tableau croisé des services par région][1]

### <a name="keeping-data-in-sync-across-multiple-azure-search-services"></a>Synchronisation des données entre plusieurs services Azure Search
Il existe deux options pour conserver vos services de recherche distribuée synchronisés qui consistent à l’aide de hello [Azure Search Indexer](search-indexer-overview.md) ou hello API de Push (également appelée tooas hello [API REST Azure Search](https://docs.microsoft.com/rest/api/searchservice/)).  

### <a name="azure-search-indexers"></a>Indexeurs Azure Search
Si vous utilisez hello indexeur de recherche Azure, vous importez déjà des modifications de données à partir d’une banque de données centrale telles que la base de données SQL Azure ou base de données Azure Cosmos. Lorsque vous créez une nouvelle recherche le Service, vous simplement également créer un nouvel indexeur de recherche Azure pour ce service qui toothis points même magasin de données. De cette façon, chaque fois que les nouvelles modifications entrent en magasin de données hello, elles seront indexés par hello plusieurs indexeurs.  

Voici à quoi ressemblerait une telle architecture.

   ![Source de données unique avec indexeur distribué et combinaisons de service][2]

### <a name="push-api"></a>API push
Si vous utilisez l’API de Push Azure Search hello trop[mettre à jour le contenu de votre index Azure Search](https://docs.microsoft.com/rest/api/searchservice/update-index), vous pouvez synchroniser vos différents services de recherche en envoyant des services de recherche de modifications tooall chaque fois qu’une mise à jour est requise.  Ce faisant, il est important toomake que toohandle cas où un service de recherche de tooone de mise à jour échoue et un ou plusieurs des mises à jour réussissent.

## <a name="leveraging-azure-traffic-manager"></a>Utilisation d’Azure Traffic Manager
[Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) vous permet de tooroute demandes toomultiple géo-localisés des sites Web qui sont sauvegardés puis par plusieurs Services de recherche Azure.  Un avantage de hello Traffic Manager est qu’il peut détecter tooensure Azure Search qu’il est disponible et acheminer des services de recherche tooalternate les utilisateurs dans l’événement hello du temps d’arrêt.  En outre, si vous routez les demandes de recherche via les Sites Web Azure, Azure Traffic Manager vous permet de cas de solde tooload où le site Web de hello est haut, mais pas Azure Search.  Voici un exemple d’architecture hello qui tire parti de Traffic Manager.

   ![Tableau croisé des services par région, avec Traffic Manager central][3]

## <a name="monitoring-performance"></a>Analyse des performances
Azure Search offre hello capacité tooanalyze et analysent hello les performances de votre service via [recherche le trafic Analytique (STA)](search-traffic-analytics.md). Via STA, vous pouvez éventuellement enregistrer les opérations de recherche individuelles hello ainsi que compte de stockage Azure tooan des mesures agrégées qui peut être traitée pour l’analyse ou de visualisation dans Power BI.  À l’aide de mesures STA, vous pouvez afficher les statistiques de performances comme le nombre moyen de requêtes ou les temps de réponse.  Enregistrement de l’opération hello permet en outre, toodrill dans les détails des opérations de recherche spécifique.

STA est un outil précieux toounderstand latence des taux à partir de ce point de vue Azure Search.  Étant donné que les métriques de performances de requête hello connectés sont basés sur le temps de hello toobe entièrement traité dans Azure Search (à partir de hello temps toowhen demandé, il est diffusée) d’une requête est, vous êtes en mesure de toouse ce toodetermine si les problèmes de latence sont de hello service Azure Search côté ou en dehors de hello service, par exemple une latence du réseau.  

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur hello tarification niveaux et les limites de services pour chacune d’elles, consultez [Service limites dans Azure Search](search-limits-quotas-capacity.md).

Visitez [planification de la capacité](search-capacity-planning.md) toolearn plus d’informations sur les combinaisons de partition et le réplica.

Pour plus d’extraction sur les performances et toosee des démonstrations de comment tooimplement hello optimisations présentées dans cet article, regardez hello suivant vidéo :

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<!--Image references-->
[1]: ./media/search-performance-optimization/geo-redundancy.png
[2]: ./media/search-performance-optimization/scale-indexers.png
[3]: ./media/search-performance-optimization/geo-search-traffic-mgr.png
