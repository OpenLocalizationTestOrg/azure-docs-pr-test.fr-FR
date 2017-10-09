---
title: "aaaModeling l’architecture mutualisée dans Azure Search | Documents Microsoft"
description: "Découvrez les modèles de conception courants pour les applications SaaS mutualisées lors de l’utilisation de Recherche Azure."
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 72e9696a-553b-47dc-9e05-a82db0ebf094
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/26/2016
ms.author: ashmaka
ms.openlocfilehash: dd46cda772d32566b9aaa18d407f12fdf178bd43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multitenant-saas-applications-and-azure-search"></a>Modèles de conception pour les applications SaaS mutualisées et Recherche Azure
Une application multi-locataire est celle qui fournit hello services et des fonctionnalités tooany autant de clients qui ne peuvent pas voir ou partager des données hello de n’importe quel autre client. Ce document aborde les stratégies d’isolation de client pour les applications mutualisées conçues avec Recherche Azure.

## <a name="azure-search-concepts"></a>Concepts de Recherche Azure
Comme solution de recherche en tant que service, Azure Search permet la recherche riches de développeurs tooadd rencontre tooapplications sans gérer n’importe quelle infrastructure ou de devenir un expert dans la recherche. Les données sont téléchargées toohello service et stockées dans le cloud de hello. À l’aide de simples demandes toohello API Azure Search, hello puis modifiées et des données recherchées. Vous trouverez une vue d’ensemble du service de hello dans [cet article](http://aka.ms/whatisazsearch). Avant d’aborder les modèles de conception, il est important toounderstand certains concepts dans Azure Search.

### <a name="search-services-indexes-fields-and-documents"></a>Rechercher des services, des index, des champs et des documents
Lorsque vous utilisez Azure Search, un s’abonne tooa *service de recherche*. Comme les données sont téléchargée tooAzure recherche, il est stocké dans un *index* au sein du service de recherche hello. Un seul service peut contenir plusieurs index. toouse hello concepts familiers de bases de données, service de recherche hello peut être comparés de tooa index hello au sein d’un service peuvent être comparés de tootables au sein d’une base de données.

Chaque index au sein d’un service de recherche possède son propre schéma, qui est défini par un certain nombre de *champs*personnalisables. Données sont ajoutées index Azure Search de tooan sous forme de hello de personne *documents*. Chaque document doit être téléchargé tooa un index particulier et doit tenir schéma de cet index. Lors de la recherche des données à l’aide d’Azure Search, les requêtes de recherche en texte intégral hello sont émis par rapport à un index particulier.  toocompare toothose de ces concepts de base de données, les champs peuvent être comparés de toocolumns dans une table et les documents peuvent être comparés de toorows.

### <a name="scalability"></a>Extensibilité
N’importe quel service Azure Search Bonjour Standard [tarification](https://azure.microsoft.com/pricing/details/search/) peut évoluer en deux dimensions : stockage et disponibilité.

* *Partitions* peut être ajouté de stockage de hello tooincrease d’un service de recherche.
* *Réplicas* peuvent être ajoutées tooa service tooincrease hello un débit de demandes capable de gérer un service de recherche.

Ajout et suppression de partitions et réplicas sur permettra capacité hello de hello recherche service toogrow avec la quantité de hello de données et le trafic de demandes d’application hello. Dans commande pour un tooachieve de service de recherche une lecture [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), elle nécessite deux réplicas. Dans commande pour un service tooachieve en lecture-écriture [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), il requiert trois réplicas.

### <a name="service-and-index-limits-in-azure-search"></a>Limites du service et de l’index dans Recherche Azure
Il existe quelques différents [niveaux tarifaires](https://azure.microsoft.com/pricing/details/search/) dans Azure Search, chacun des niveaux de hello dispose de différents [limites et quotas](search-limits-quotas-capacity.md). Certaines de ces limites sont à hello au niveau du service, certaines sont au niveau d’index hello et certaines sont au niveau de partition hello.

|  | De base | Standard1 | Standard2 | Standard3 | Standard3 HD |
| --- | --- | --- | --- | --- | --- |
| Nombre maximal de réplicas par service |3 |12 |12 |12 |12 |
| Nombre maximal de partitions par service |1 |12 |12 |12 |1 |
| Nombre maximal d’unités de recherche (réplicas*partitions) par service |3 |36 |36 |36 |36 (3 partitions max.) |
| Nombre maximal de documents par service |1 million |180 millions |720 millions |1,4 milliard |600 millions |
| Stockage maximal par service |2 Go |300 Go |1,2 To |2,4 To |600 Go |
| Nombre maximal de documents par partition |1 million |15 millions |60 millions |120 millions |200 millions |
| Stockage maximal par partition |2 Go |25 Go |100 Go |200 Go |200 Go |
| Nombre maximal d’index par service |5 |50 |200 |200 |3000 (1 000 index max. par partition) |

#### <a name="s3-high-density"></a>Haute densité S3
Dans le niveau de tarification d’Azure Search S3, il est une option pour le mode haute densité (HD) hello spécifiquement conçu pour les scénarios multi-locataires. Dans de nombreux cas, il est nécessaire toosupport un grand nombre de clients plus petits sous un avantages de hello tooachieve service unique de simplicité et une meilleure rentabilité.

S3 HD permet hello de nombreux petits index toobe empaquetés sous gestion hello d’un service de recherche par commercial tooscale de capacité hello des index sur des partitions hello capacité toohost plusieurs index dans un seul service.

Concrètement, un service de S3 peut avoir entre 1 et 200 index ensemble susceptible d’héberger des milliards documents de too1.4. Un disque dur S3 sur hello autre part permettrait aux index individuels tooonly monter too1 millions de documents, mais il peut gérer des index too1000 par partition (haut too3000 par service) avec un nombre de documents total de 200 millions par partition (les too600 millions par service).

## <a name="considerations-for-multitenant-applications"></a>Considérations relatives aux applications mutualisées
Applications mutualisées doivent distribuer efficacement les ressources entre les locataires hello tout en conservant un niveau de confidentialité entre hello différents clients. Il existe quelques considérations lors de la conception d’architecture hello pour une telle application :

* *Isolation des locataires :* les développeurs d’applications doivent tootake mesures tooensure qu’aucune clients ont non autorisé ou indésirables d’accéder aux données de toohello d’autres clients. Au-delà de la perspective hello de confidentialité des données, stratégies d’isolation de client requièrent une gestion efficace des ressources partagées et la protection bruyantes voisins.
* *Coût des ressources cloud :* comme pour toute autre application, les solutions logicielles doivent rester compétitives au niveau du coût en tant que composant d’une application mutualisée.
* *Facilité d’opérations :* lors du développement d’une architecture mutualisée, hello impact sur les opérations de l’application hello et la complexité est un facteur important. La Recherche Azure bénéficie d’un [Contrat de niveau de service de 99,9 %](https://azure.microsoft.com/support/legal/sla/search/v1_0/).
* *Encombrement global :* applications mutualisées peuvent nécessiter que les locataires serve tooeffectively qui sont réparties entre les globe hello.
* *Évolutivité :* les développeurs d’applications doivent tooconsider leur rapprochement entre maintenir un niveau suffisamment faible de la complexité des applications et de conception hello application tooscale avec le nombre de clients et hello la taille des données de clients et charge de travail.

Azure Search offre quelques limites qui peuvent être des données et la charge de travail clients tooisolate utilisé.

## <a name="modeling-multitenancy-with-azure-search"></a>Modélisation d’une architecture mutualisée avec Recherche Azure
Dans les cas de hello d’un scénario multi-locataire, développeur de l’application hello consomme un ou plusieurs services de recherche et diviser les locataires des clients entre les services, les index ou les deux. Recherche Azure offre quelques modèles courants pour la modélisation d’un scénario mutualisé :

1. *Index par client :* chaque client a son propre index dans un service de recherche qui est partagé avec d’autres clients.
2. *Service par client :* chaque client possède son propre service Recherche Azure dédié, pour un niveau de séparation maximal entre les données et la charge de travail.
3. *Combinaison des deux :* les clients les plus volumineux et actifs se voient attribuer des services dédiés, tandis que les clients plus petits se voient attribuer des index individuels au sein de services partagés.

## <a name="1-index-per-tenant"></a>1. Index par client
![Une image de modèle d’index pour chaque locataire hello](./media/search-modeling-multitenant-saas-applications/azure-search-index-per-tenant.png)

Dans un modèle d’index par client, plusieurs clients occupent un seul service Recherche Azure où chaque client a son propre index.

Les clients bénéficient de l’isolation des données, car toutes les requêtes de recherche et les opérations sur les documents sont émises au niveau de l’index dans Recherche Azure. Dans la couche d’application hello, il est reconnaissance du besoin hello toodirect hello index appropriés de différents clients trafic toohello tout en gérant des ressources au niveau de service hello sur tous les locataires.

Un attribut de clé du modèle d’index pour chaque locataire hello consiste hello hello application developer toooversubscribe hello la capacité d’un service de recherche entre les clients de l’application hello. Si les locataires hello ont une distribution inégale de la charge de travail, combinaison optimale de hello de clients peuvent être distribués sur un service de recherche d’index tooaccommodate un nombre de hautement les locataires actives, beaucoup de ressources lors du traitement d’une longue file de simultanément clients moins actifs. trouver un compromis Hello est impossibilité hello hello modèle toohandle situations où chaque client est simultanément très actif.

modèle d’index pour chaque locataire Hello servant de base de hello un modèle de coût de la variable, où un service Azure Search entier est acheté initial et rempli par la suite avec les clients. Cela permet à toobe capacité inutilisée désigné pour les versions d’évaluation et les comptes gratuits.

Pour les applications avec un encombrement global, modèle d’index pour chaque locataire hello ne peut pas être hello plus efficace. Si les clients d’une application sont répartis entre les globe hello, un service distinct peut être nécessaire pour chaque zone peut dupliquer les coûts sur chacun d’eux.

Azure Search permet de montée en puissance hello des index individuels de hello et nombre total de hello de toogrow d’index. Si une tarification approprié niveau choisie, les partitions et réplicas peuvent être ajoutés au service de recherche toohello lorsqu’un index individuel au sein du service de hello devient trop importante en termes de stockage ou le trafic réseau.

Si le nombre total de hello d’index devient trop volumineux pour un seul service, un autre service a toobe configuré tooaccommodate hello de nouveaux clients. Si les index toobe déplacée entre les services de recherche lors de l’ajout de nouveaux services, les données de salutation à partir de l’index de hello ont toobe copié manuellement à partir d’un seul index toohello autres que Azure Search n’autorise pas un toobe index déplacé.

## <a name="2-service-per-tenant"></a>2. Service par client
![Une image de modèle de service pour chaque locataire hello](./media/search-modeling-multitenant-saas-applications/azure-search-service-per-tenant.png)

Dans une architecture de service par client, chaque client possède son propre service de recherche.

Dans ce modèle, application hello atteint le niveau maximal de hello d’isolation pour ses clients. Chaque service bénéficie d’un débit et d’un stockage dédiés pour gérer les requêtes de recherche, ainsi que des clés d’API distinctes.

Pour les applications, où chaque client a un grand encombrement ou charge de travail hello a peu de variabilité de client tootenant, hello par client de service modèle est un choix efficace ressources ne sont pas partagées entre les charges de travail différents clients.

Un service par le modèle de client également propose hello d’un modèle de coût fixe et prévisible. N’existe aucun investissements dans un service de recherche jusqu'à ce qu’il existe un toofill client, toutefois hello coût par client est supérieur à un modèle d’index pour chaque locataire.

modèle de service pour chaque locataire Hello est un choix efficace pour les applications avec un encombrement global. Dans les clients distribués géographiquement, il est facile toohave service de chaque client dans la région appropriée hello.

difficultés de Hello dans ce modèle de mise à l’échelle se présentent lorsque les locataires individuels prévoit leur service. Azure Search ne prend pas en charge la mise à niveau hello tarification d’un service de recherche, pour toutes les données aurait toobe copié manuellement tooa nouveau service.

## <a name="3-mixing-both-models"></a>3. Combinaison des deux modèles
Un autre modèle pour la modélisation mutualisée est de combiner les stratégies d’index par client et de service par client.

En combinant les modèles de hello deux, les clients plus grand d’une application peuvent occupent services dédiés hello long fin de moins de clients actifs, plus petits peut occuper un index dans un service partagé. Ce modèle garantit que les clients plus grande hello ont des performances élevées à partir du service de hello tout en aidant tooprotect hello plus petits clients à partir de n’importe quel voisin bruyant.

Cependant, l’implémentation de cette stratégie repose sur la capacité à prévoir quels clients nécessiteront un service dédié au lieu d’un index dans un service partagé. La complexité des applications augmente avec hello besoin toomanage les deux de ces modèles de l’architecture mutualisées.

## <a name="achieving-even-finer-granularity"></a>Atteindre une granularité encore plus fine
Hello ci-dessus scénarios multi-locataires toomodel modèles conception dans Azure Search supposent une étendue uniforme, où chaque client est un ensemble de l’instance d’une application. Toutefois, les applications peuvent parfois gérer plusieurs étendues plus petites.

Si les modèles par client de service et les index de chaque locataire ne sont pas des étendues suffisamment petites, il est possible toomodel un tooachieve index un degré de davantage de granularité.

toohave un index unique se comportent différemment pour les points de terminaison clients différents, un champ peut être ajouté tooan des index qui désigne une certaine valeur pour chaque client possible. Chaque fois qu’un client appelle Azure Search tooquery ou modifier un index, le code hello à partir de l’application cliente de hello spécifie la valeur appropriée de hello pour ce champ à l’aide de la recherche d’Azure [filtre](https://msdn.microsoft.com/library/azure/dn798921.aspx) fonctionnalité au moment de la requête.

Cette méthode peut être utilisé tooachieve les fonctionnalités des comptes d’utilisateurs distincts, les niveaux d’autorisation distinct et les applications même complètement distinctes.

> [!NOTE]
> Hello approche décrite ci-dessus tooconfigure un index unique de tooserve plusieurs locataires affecte hello pertinence pour les résultats de recherche. Les scores de pertinence de recherche sont calculées dans une étendue au niveau de l’index, pas une portée au niveau du client, pour les données de tous les clients sont intégrées dans les statistiques sous-jacentes de scores de pertinence hello tels que la fréquence du terme.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Azure Search est un vaste choix pour de nombreuses applications [en savoir plus sur les fonctionnalités du service hello robuste](http://aka.ms/whatisazsearch). Lorsque l’évaluation hello différents modèles pour les applications multi-locataires de conception, envisagez de hello [différents niveaux de tarification](https://azure.microsoft.com/pricing/details/search/) et hello respectif [limites de service](search-limits-quotas-capacity.md) toobest adapter toofit d’Azure Search des charges de travail et les architectures de toutes tailles.

Des questions sur Azure Search et scénarios multi-locataires peuvent être dirigées tooazuresearch_contact@microsoft.com.

