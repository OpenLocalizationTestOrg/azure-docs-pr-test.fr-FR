---
title: "données aaaDistribute globalement avec la base de données Azure Cosmos | Documents Microsoft"
description: "Apprenez-en plus sur la géoréplication à l’échelle de la planète, le basculement et la récupération des données à l’aide de bases de données mondiales à partir d’Azure Cosmos DB, un service de base de données multimodèle distribué mondialement."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: ba5ad0cc-aa1f-4f40-aee9-3364af070725
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/14/2017
ms.author: arramac
ms.openlocfilehash: b50e8433dc7e70c54d68c4c2f99954a13f4951f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodistribute-data-globally-with-azure-cosmos-db"></a>Comment les données toodistribute globalement avec la base de données Azure Cosmos
Avec plus de 30 régions géographiques, Azure est partout et continue de s’étendre. Avec sa présence dans le monde entier, une des fonctions hello différencié Qu'azure offre aux développeurs de tooits est hello toobuild de capacité, déployer et gérer facilement des applications distribuées globalement. 

[Azure Cosmos DB](../cosmos-db/introduction.md) est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale pour les applications stratégiques. Base de données Azure Cosmos assure la distribution globale clé en main, [mise à l’échelle élastique de débit et de stockage](../cosmos-db/partition-data.md) des latences de milliseconde dans le monde entier, à un chiffre à 99e centile de hello, [cinq niveaux de cohérence bien définis ](consistency-levels.md)et la garantie de haute disponibilité, bénéficient toutes [pointe SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Base de données Azure Cosmos [automatiquement les données d’index](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sans avoir toodeal avec la gestion de schéma et d’index. Il est multi-modèle et prend en charge les modèles de données en colonnes, documents, graphiques et clé-valeur. Comme un service cloud réunit, base de données Azure Cosmos est soigneusement conçu avec une architecture mutualisée et globale distribution à partir de hello d’arrière-plan.

**Collection Azure Cosmos DB unique, partitionnée et distribuée dans plusieurs régions Azure**

![Collection Azure Cosmos DB partitionnée et distribuée dans trois régions](./media/distribute-data-globally/global-apps.png)

Comme nous l’avons appris lors de la création Azure Cosmos DB, l’ajout de la distribution globale ne peut pas venir après coup. Cette fonction ne peut pas être « rajoutée » sur un système de base de données à un seul site. les fonctions Hello offertes par une base de données distribué internationalement s’étendre au-delà que des sinistres traditionnel récupération (Geo-DR) proposé par les bases de données de site « unique ». Les bases de données à un seul site offrant la fonctionnalité de récupération d’urgence géographique sont un sous-ensemble strict des bases de données mondialement distribuées. 

Avec la distribution globale clé en main de Azure Cosmos DB, développeurs n’ont pas toobuild leur propres la structure de la réplication en utilisant un modèle de Lambda hello (par exemple, [AWS DynamoDB réplication](https://github.com/awslabs/dynamodb-cross-region-library/blob/master/README.md)) sur le journal de base de données hello ou par vous « écritures doubles » dans plusieurs régions. Nous ne vous recommandons de ces approches, car il est impossible tooensure ces approches est correct et fournir les contrats SLA audio. 

Dans cet article, nous fournissons une vue d’ensemble des fonctionnalités de distribution mondiale d’Azure Cosmos DB. Nous expliquons également tooproviding d’approche unique Azure Cosmos DB SLA complète. 

## <a id="EnableGlobalDistribution"></a>Activation de la distribution mondiale clé en main
Base de données Cosmos Azure fournit des éléments suivants de hello tooenable de fonctionnalités tooeasily vous écrire des applications à l’échelle planète. Ces fonctionnalités sont disponibles via la ressource du hello Cosmos base de données Azure fournisseur [API REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/) , ainsi que de hello portail Azure.

### <a id="RegionalPresence"></a>Omniprésence régionale 
Azure étend constamment sa présence géographique en ajoutant de [nouvelles régions](https://azure.microsoft.com/regions/) en ligne. Azure Cosmos DB est disponible par défaut dans toutes les nouvelles régions Azure. Ainsi, vous tooassociate une région géographique avec votre compte de base de données de base de données Azure Cosmos dès que Azure ouvre la nouvelle région de hello entreprise.

**Azure Cosmos DB est disponible par défaut dans toutes les régions Azure**

![Azure Cosmos DB est disponible par défaut dans toutes les régions Azure](./media/distribute-data-globally/azure-regions.png)

### <a id="UnlimitedRegionsPerAccount"></a>Associer un nombre illimité de régions à votre compte de base de données Azure Cosmos DB
Base de données Cosmos Azure vous permet de tooassociate compte de base de données n’importe quel nombre de régions Azure avec votre base de données Azure Cosmos. En dehors des restrictions de délimitation géographique (par exemple, en Chine, Allemagne), il n’existe aucune limitation sur le nombre de hello des régions qui peuvent être associés à votre compte de base de données de base de données Azure Cosmos. Hello figure suivante montre un toospan configuré de compte de base de données entre les régions Azure 25.  

**Un compte de base de données Azure Cosmos DB d’un locataire couvrant 25 régions Azure**

![Compte de base de données Azure Cosmos DB couvrant 25 régions Azure](./media/distribute-data-globally/spanning-regions.png)

### <a id="PolicyBasedGeoFencing"></a>Délimitations géographiques basées sur des stratégies
Base de données Azure Cosmos est conçue toohave basée sur des stratégies des fonctionnalités de délimitation géographique. Délimitation géographique est un composant important de tooensure restrictions de gouvernance et de conformité des données et peut empêcher l’association d’une région spécifique à votre compte. Exemples de délimitation géographique inclure (mais ne sont pas limitées à), l’étendue de régions de toohello distribution globale dans un cloud souverain (par exemple, en Chine et en Allemagne), ou dans une limite de taxation gouvernement (par exemple, Australie). stratégies de Hello sont contrôlées à l’aide de métadonnées hello de votre abonnement Azure.

### <a id="DynamicallyAddRegions"></a>Ajouter et supprimer des régions dynamiquement
Base de données Azure Cosmos vous permet de tooadd (associer) ou supprimer (Dissocier) compte de base de données des régions tooyour à tout moment (consultez [figure précédente](#UnlimitedRegionsPerAccount)). En vertu de la réplication des données sur plusieurs partitions en parallèle, base de données Azure Cosmos garantit que lorsqu’une nouvelle zone est en ligne, base de données Azure Cosmos est disponible dans les 30 minutes n’importe où dans le monde hello pour les too100 to. 

### <a id="FailoverPriorities"></a>Priorités de basculement
toocontrol la séquence exacte des basculements régionaux lors d’une panne régionale multiples, base de données Azure Cosmos vous permet de régions de toovarious tooassociate hello priorité associées au compte de base de données hello (voir la figure suivante de hello). Base de données Azure Cosmos garantit que la séquence de basculement automatique de hello se produit dans l’ordre de priorité hello spécifié. Pour plus d’informations sur les basculements régionaux, consultez [Basculements régionaux automatiques pour la continuité des activités dans Azure Cosmos DB](regional-failover.md).

**Un client de base de données Azure Cosmos pouvez configurer l’ordre de priorité de basculement hello (volet droit) pour les régions associées à un compte de base de données**

![Configuration des priorités de basculement avec Azure Cosmos DB](./media/distribute-data-globally/failover-priorities.png)

### <a id="OfflineRegions"></a>Déconnecter une région dynamiquement
Base de données Cosmos Azure vous permet de tootake votre base de données hors connexion de compte dans une région spécifique et remettre en ligne ultérieurement. Régions marquées hors connexion ne participent pas activement la réplication et ne font pas partie de la séquence de basculement hello. Cela vous permet de hello toofreeze dernière connue image bonne base de données dans un des hello lire régions avant tooyour application de mises à niveau propagées potentiellement dangereux.

### <a id="ConsistencyLevels"></a>Plusieurs modèles de cohérence bien définis pour les bases de données mondialement répliquées
Azure Cosmos DB expose [plusieurs niveaux de cohérence bien définis](consistency-levels.md) pris en charge par des contrats SLA. Vous pouvez choisir un modèle de cohérence spécifiques (de liste disponibles de hello des options) en fonction de la charge de travail/scénarios de hello. 

### <a id="TunableConsistency"></a>Cohérence ajustable pour les bases de données répliquées mondialement
Base de données Azure Cosmos vous permet de tooprogrammatically override et assouplir les choix de la cohérence hello par défaut sur une base de chaque demande, lors de l’exécution. 

### <a id="DynamicallyConfigurableReadWriteRegions"></a>Régions de lecture et d’écriture configurables de manière dynamique
Base de données Azure Cosmos vous permet de régions de hello tooconfigure (associées de la base de données hello) pour « lecture », « écriture » ou « en lecture/écriture » des régions. 

### <a id="ElasticallyScaleThroughput"></a>Mise à l’échelle flexible du débit à travers les régions Azure
Vous pouvez mettre à l’échelle une collection Azure Cosmos DB de manière flexible en configurant le débit par programme. débit de Hello est appliqué tooall des régions hello est distribué dans le regroupement de hello.

### <a id="GeoLocalReadsAndWrites"></a>Lectures et écritures géo-locales
Hello des principaux avantages d’une base de données distribué internationalement donnée toooffer à faible latence accès toohello n’importe où dans Bonjour. Azure Cosmos DB offre des garanties de latence faible à 99,99 % pour diverses opérations de base de données. Elle garantit que toutes les lectures sont routés toohello région lecture local le plus proche. tooserve une demande de lecture, dans laquelle est émise hello lire la région hello quorum toohello local est utilisé ; Hello va de même toohello écritures. Une écriture est reconnue uniquement après qu’une majorité des réplicas de validation durablement écriture de hello localement sans être contrôlé sur les réplicas distants tooacknowledge hello écritures. Autres termes, le protocole de réplication hello de base de données Azure Cosmos fonctionne sous hypothèse hello hello en lecture et d’écriture des quorums sont toujours toohello local lire et écrivent des régions, respectivement, dans la requête hello est émise.

### <a id="ManualFailover"></a>Initier manuellement le basculement régional
Base de données Cosmos Azure vous permet le basculement de hello tootrigger Hello de toovalidate de compte de base de données hello *fin tooend* propriétés de la disponibilité de hello ensemble de l’application (au-delà de la base de données hello). Étant donné que les deux hello sécurité et sont garanti que les propriétés de l’activité d’élection de détection et la suite de la défaillance hello, base de données Azure Cosmos garantit *zéro perte de données* pour une opération exécutée par le client un basculement manuel.

### <a id="AutomaticFailover"></a>Basculement automatique
Azure Cosmos DB prend en charge le basculement automatique en cas d’une ou de plusieurs pannes régionales. Lors d’un basculement régional, Azure Cosmos DB gère la latence de lecture, la disponibilité, la cohérence et les contrats SLA de débit. Azure Cosmos DB fournit une limite supérieure de durée de hello d’un toocomplete d’opération de basculement automatique. Il s’agit fenêtre hello potentiel de perte de données pendant une panne régionale de hello.

### <a id="GranularFailover"></a>Conçu pour différentes granularités de basculement
Actuellement hello automatique et des fonctionnalités de basculement manuel sont exposées au niveau de granularité hello du compte de base de données hello. Notez que, en interne les DB Cosmos Azure est conçue toooffer *automatique* basculement au niveau de granularité plus fine d’une base de données, collection ou même une partition (d’une collection qui possède une plage de clés). 

### <a id="MultiHomingAPIs"></a>API multihébergement dans Azure Cosmos DB
Base de données Cosmos Azure vous permet de toointeract à l’aide de la base de données hello logique (indépendant de la région) ou des points de terminaison physiques (spécifique à la région). À l’aide de points de terminaison logiques permet de s’assurer qu’application hello peut en toute transparence multirésident en cas de basculement. Hello des points de terminaison de ce dernier, physiques, fournir un contrôle affiné toohello application tooredirect lit et écrit des régions de toospecific.

Vous trouverez plus d’informations sur comment tooconfigure de lire les préférences pour hello [API DocumentDB](../cosmos-db/tutorial-global-distribution-documentdb.md), [API Graph](../cosmos-db/tutorial-global-distribution-graph.md), [Table API](../cosmos-db/tutorial-global-distribution-table.md), et [MongoDB API](../cosmos-db/tutorial-global-distribution-mongodb.md)dans respectives liés aux articles.

### <a id="TransparentSchemaMigration"></a>Schéma de base de données et migration d’index transparents et cohérents 
Azure Cosmos DB est entièrement [sans schéma](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf). conception unique de Hello de son moteur de base de données lui permet de tooautomatically et toutes les données hello il résultants sans index secondaire de votre schéma ou de façon synchrone d’index. Ainsi, vous tooiterate votre application distribuée globalement rapidement sans préoccuper de la migration de schéma et d’index de base de données ou à coordonner les déploiements à plusieurs phases application des modifications de schéma. Base de données Azure Cosmos garantit que les stratégies de tooindexing modifications vous avez explicitement faites n’entraîne pas dans une dégradation des performances ou de disponibilité.  

### <a id="ComprehensiveSLAs"></a>Contrats de niveau de service complets (au-delà de la simple haute disponibilité)
Comme un service de base de données distribuée globalement, base de données Azure Cosmos offre SLA bien défini de **perte de données**, **disponibilité**, **latence à P99**, **débit**  et **cohérence** de base de données hello dans son ensemble, quel que soit le nombre de hello de zones associés hello de base de données.  

## <a id="LatencyGuarantees"></a>Garanties de latence
Hello des principaux avantages d’un service de base de données distribués internationalement comme base de données Azure Cosmos donnée toooffer à faible latence accès tooyour n’importe où dans Bonjour. Azure Cosmos DB offre une latence faible garantie à 99,99 % pour diverses opérations de base de données. protocole de réplication Hello qui utilise la base de données Azure Cosmos garantit que hello des opérations de base de données (dans l’idéal, lit et écrit) sont toujours effectuées dans toothat local de région hello du client de hello. latence Hello pour que SLA d’Azure Cosmos DB inclut P99 les lectures, écritures indexées (synchrone) et des requêtes pour différentes tailles de demande et de réponse. Hello de garanties de latence pour les écritures incluent les validations de quorum majoritaire durable dans le centre de données local hello.

### <a id="LatencyAndConsistency"></a>Relation de latence avec la cohérence 
Pour une service distribué globalement toooffer fort la cohérence dans une installation distribuée globalement, il doit toosynchronously hello réplique écritures synchrones effectuer entre régions lectures – la vitesse de clair et hello déterminent de fiabilité de réseau étendu hello que la cohérence forte entraîne des latences élevées et faible disponibilité des opérations de base de données. Par conséquent, dans toooffer ordre garanti que les temps de latence basses au P99 et à la disponibilité de 99,99, service de hello doit utiliser la réplication asynchrone. Cette à leur tour nécessite que le service de hello doit également offrir [choix de cohérence bien définis et souple](consistency-levels.md) – plus faible que fort (toooffer faible latence et la disponibilité des garanties) et dans l’idéal, plus puissant que cohérence « éventuelle » () toooffer un modèle de programmation intuitif).

Base de données Azure Cosmos garantit qu’une opération de lecture n’est pas requis toocontact réplicas sur plusieurs régions toodeliver hello spécifiques au niveau garantie de cohérence. De même, elle garantit qu’une opération d’écriture ne pas bloquée alors que les données de salutation sont en cours de réplication toutes les régions hello (autrement dit, les écritures sont répliquées de manière asynchrone entre les régions). Dans le cas de comptes de base de données multirégions, plusieurs niveaux de cohérence flexibles sont disponibles. 

### <a id="LatencyAndAvailability"></a>Relation de la latence avec la disponibilité 
La latence et disponibilité sont sociaux hello hello même pièce. Nous aborderons la latence d’opération hello dans un état stable et de disponibilité, en face de hello d’échecs. Point de vue application hello, une opération de base de données en cours d’exécution lente est indiscernable à partir d’une base de données n’est pas disponible. 

une latence élevée d’indisponibilité, base de données Azure Cosmos toodistinguish fournit une limite supérieure absolue sur la latence de diverses opérations de base de données. Si l’opération de base de données hello dure plus longtemps que hello limite supérieure toocomplete, base de données Azure Cosmos renvoie une erreur de délai d’attente. Hello contrat SLA de disponibilité de base de données Azure Cosmos garantit que délais d’attente hello sont compté dans le contrat SLA de disponibilité hello. 

### <a id="LatencyAndThroughput"></a>Relation de latence avec le débit
Azure Cosmos DB ne vous fait pas choisir entre la latence et le débit. Elle respecte le contrat SLA de hello pour les deux une latence au P99 et fournir un débit hello que vous avez configurés. 

## <a id="ConsistencyGuarantees"></a>Garanties de cohérence
Lors de hello [modèle de cohérence forte](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) est hello gold standard de programmabilité, il est fourni au prix de forte de hello d’une latence élevée (dans un état stable) et une perte de disponibilité (en face de hello d’échecs). 

Azure Cosmos DB offre une tooreason tooyou modèle programmation bien défini sur la cohérence de données répliquées. Dans commande tooenable vous toobuild multirésident applications, les modèles de cohérence hello exposées par la base de données Azure Cosmos sont indépendantes de la région toobe conçue et ne dépendant pas de la région de hello d’où hello lectures et écritures sont pris en charge. 

Contrat SLA de la cohérence de DB Cosmos Azure garantit que 100 % des demandes de lecture répondra garantie de cohérence hello pour le niveau de cohérence hello demandé par vous (hello par défaut niveau de cohérence sur le compte de base de données hello ou valeur hello substituée à la demande de hello ). Une demande de lecture est considéré comme toohave remplie hello cohérence SLA si toutes les garanties de cohérence hello associées au niveau de cohérence hello sont satisfaites. Hello tableau suivant répertorie les garanties de cohérence hello correspondant aux niveaux de cohérence toospecific offertes par la base de données Azure Cosmos.

**Garanties de cohérence associées à un niveau de cohérence donné dans Azure Cosmos DB**

<table>
    <tr>
        <td><strong>Niveau de cohérence</strong></td>
        <td><strong>Caractéristiques de la cohérence</strong></td>
        <td><strong>CONTRAT SLA</strong></td>
    </tr>
    <tr>
        <td rowspan="3">session</td>
        <td>Lecture de votre propre écriture</td>
        <td>100 %</td>
    </tr>
    <tr>
        <td>Lecture unitone</td>
        <td>100 %</td>
    </tr>
    <tr>
        <td>Préfixe cohérent</td>
        <td>100 %</td>
    </tr>
    <tr>
        <td rowspan="3">Bounded staleness (En fonction de l'obsolescence)</td>
        <td>Lecture unitone (au sein d’une région)</td>
        <td>100 %</td>
    </tr>
    <tr>
        <td>Préfixe cohérent</td>
        <td>100 %</td>
    </tr>
    <tr>
        <td>Obsolescence limitée &lt; K, T</td>
        <td>100 %</td>
    </tr>
    <tr>
        <td>Préfixe cohérent</td>
        <td>Préfixe cohérent</td>
        <td>100 %</td>
    </tr>
    <tr>
        <td>Remarque</td>
        <td>Linéarisable</td>
        <td>100 %</td>
    </tr>
</table>

### <a id="ConsistencyAndAvailability"></a>Relation de la cohérence avec la disponibilité
Hello [résultat de l’impossibilité](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf) Hello [théorème de CAP](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf) prouve qu’il est en effet empêche tooremain de système de hello disponible et offre de cohérence linearizable en face de hello d’échecs. service de base de données Hello doit choisir toobe CP ou l’Asie-Pacifique - systèmes de CP renoncer disponibilité en faveur de la cohérence linearizable tandis que les systèmes hello PA renoncer [linearizable cohérence](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) en faveur de la disponibilité. Base de données Azure Cosmos viole jamais hello demandée au niveau de cohérence, ce qui le rend formellement un système CP. Toutefois, dans la pratique la cohérence n’est pas une proposition tout ou rien : il existe plusieurs modèles de cohérence bien définis dans spectre de cohérence hello entre cohérence linearizable et éventuelle. Dans la base de données Azure Cosmos, nous avons tenté tooidentify plusieurs hello ont assoupli des modèles de cohérence avec la mise en application du monde réel et un modèle de programmation intuitif. Base de données Azure Cosmos navigue compromis lors de la disponibilité de la cohérence hello en offrant 99,99 SLA de disponibilité avec [plusieurs ont assoupli des niveaux de cohérence encore bien défini](consistency-levels.md). 

### <a id="ConsistencyAndAvailability"></a>Relation de la cohérence avec la latence
Une variation plus complète du CAP a été proposée par le professeur Daniel Abadi ; elle est appelée [PACELC](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf), qui constitue également un compromis en termes de latence et de cohérence dans un état stable. Il indique que dans un état stable, système de base de données hello doit choisir entre la cohérence et la latence. Avec plusieurs modèles de cohérence souple (pris en charge par la réplication asynchrone et local lecture, écriture quorums), base de données Azure Cosmos garantit que toutes les lectures et écritures sont toohello local lecture et écrivent respectivement les régions.  Cela permet à faible latence toooffer de base de données Azure Cosmos garantit au sein de la région de hello pour les niveaux de cohérence hello.  

### <a id="ConsistencyAndThroughput"></a>Relation de la cohérence avec le débit
Étant donné que l’implémentation hello d’un modèle de cohérence spécifique dépend des choix hello d’un [type de quorum](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf), débit de hello varie en fonction des choix hello de cohérence. Par exemple, dans la base de données Azure Cosmos, hello débit avec des lectures fortement cohérents est toothat environ la moitié de lectures cohérentes. 
 
**Relation de la capacité de lecture pour un niveau de cohérence spécifique dans Azure Cosmos DB**

![Relation entre cohérence et débit](./media/distribute-data-globally/consistency-and-throughput.png)

## <a id="ThroughputGuarantees"></a>Garanties de débit 
Base de données Cosmos Azure vous permet de tooscale débit (comme, stockage), configurées sur différentes régions, en fonction de la demande de hello. 

**Une collection Azure Cosmos DB unique, partitionnée (sur trois partitions) et distribuée dans trois régions Azure**

![Collections distribuées et partitionnées d’Azure Cosmos DB](../cosmos-db/media/introduction/azure-cosmos-db-global-distribution.png)

Une collection Azure Cosmos DB est distribuée dans deux dimensions : au sein d’une région, puis entre les régions. Voici comment procéder : 

* Dans une région unique, une collection Azure Cosmos DB est mise à l’échelle en termes de partitions de ressources. Chaque partition de ressources gère un ensemble de clés et est fortement cohérente et hautement disponible en vertu de la réplication de machines d’état parmi un jeu de réplicas. Azure Cosmos DB est un système de gouverneur de ressources entièrement où une partition de ressource est responsable de sa part de débit pour budget hello de tooit des ressources allouées de système de remise. Hello mise à l’échelle d’une collection de base de données Azure Cosmos est complètement transparent : base de données Azure Cosmos gère les partitions de ressource hello et fractionne et fusionne en fonction des besoins. 
* Chaque partition de ressource hello est ensuite distribué dans plusieurs régions. Partitions de ressources propriétaire hello même jeu de clés dans différentes régions formulaire partition ensemble (consultez [figure précédente](#ThroughputGuarantees)).  Partitions de ressources au sein d’un jeu de partitions sont coordonnées à l’aide de la réplication de machine d’état entre hello plusieurs régions. Selon le niveau de cohérence hello configuré, les partitions de ressources hello au sein d’un jeu de partitions sont configurées dynamiquement à l’aide de différentes topologies (par exemple, en étoile, cascade, arborescence, etc.). 

En vertu d’une gestion des partitions très réactif, l’équilibrage de charge et gouvernance des ressources strict, base de données Azure Cosmos vous permet un débit de montée en puissance tooelastically dans plusieurs régions Azure sur une collection de base de données Azure Cosmos. Changement de débit sur une collection est une opération du runtime dans la base de données Azure Cosmos - comme avec d’autres opérations de base de données que base de données Azure Cosmos garantit hello absolue supérieure sur la latence pour votre débit hello toochange des demandes. Par exemple, hello figure suivante montre la collection d’un client avec un débit approvisionné de façon élastique (comprise entre 1M - 10M demandes/s entre deux régions) basé sur la demande de hello.
 
**Collection d’un client dont le débit est configuré en toute flexibilité (1 à 10 millions de demandes/s)**

![Débit configuré en toute flexibilité d’Azure Cosmos DB](./media/distribute-data-globally/elastic-throughput.png)

### <a id="ThroughputAndConsistency"></a>Relation du débit avec la cohérence 
Identique à la[Relation de la cohérence avec le débit](#ConsistencyAndThroughput).

### <a id="ThroughputAndAvailability"></a>Relation du débit avec la disponibilité
Base de données Azure Cosmos se poursuit toomaintain sa disponibilité hello modifications apportées toohello débit. Base de données Azure Cosmos gère de façon transparente les partitions (par exemple, fractionnement, fusion, les opérations de clonage) et s’assure que les opérations hello n’altèrent pas la performance ou disponibilité, tandis que l’application hello configurées augmente ou diminue le débit. 

## <a id="AvailabilityGuarantees"></a>Garanties de disponibilité
Azure Cosmos DB offre une disponibilité de 99,99 % SLA pour chacun des hello les opérations de plan de données et le contrôle. Comme indiqué précédemment, les garanties de disponibilité d’Azure Cosmos DB incluent une limite supérieure absolue de la latence pour toutes les opérations de données et de plan de contrôle. les garanties de disponibilité Hello sont permanent et ne changent pas avec le nombre de hello de régions ou de la distance entre les régions géographique. Les garanties de disponibilité s’appliquent au basculement manuel et automatique. Base de données Azure Cosmos offre transparent API d’hébergement multiple qui garantissent que votre application peut fonctionner sur des points de terminaison logiques et qu’il peut acheminer en toute transparence nouvelle zone de toohello hello demandes en cas de basculement. Autres termes, votre application ne doit pas toobe redéployé lors du basculement régional et la disponibilité de hello SLA sont conservées.

### <a id="AvailabilityAndConsistency"></a>Relation de la disponibilité avec la cohérence, la latence et le débit
La relation de la disponibilité avec la cohérence, la latence et le débit est décrite dans [Relation de la cohérence avec la disponibilité](#ConsistencyAndAvailability), [Relation de la latence avec la disponibilité](#LatencyAndAvailability) et [Relation du débit avec la disponibilité](#ThroughputAndAvailability). 

## <a id="GuaranteesAgainstDataLoss"></a>Garanties et comportement du système en cas de « perte de données »
Dans Azure Cosmos DB, chaque partition (d’une collection) est rendue hautement disponible par un certain nombre de réplicas, répartis entre 10 à 20 domaines d’erreur au moins. Toutes les écritures sont de façon synchrone et durablement validées par le quorum majoritaire de réplicas avant qu’ils sont reconnus toohello client. La réplication asynchrone est appliquée de manière coordonnée entre les partitions réparties dans plusieurs régions. Azure Cosmos DB garantit qu’il n’y a aucune perte de données en cas de basculement manuel initié par un locataire. Pendant le basculement automatique, base de données Azure Cosmos garantit une limite supérieure de hello configuré délimitée d’intervalle de péremption sur la fenêtre de perte de données hello dans le cadre de son contrat SLA.

## <a id="CustomerFacingSLAMetrics"></a>Mesures de contrat de niveau de service orientées client
Base de données Azure Cosmos expose en toute transparence les mesures de débit, latence, la cohérence et la disponibilité hello. Ces mesures sont accessibles par programme et via hello portail Azure (voir la figure suivante). Vous pouvez également définir des alertes sur différents seuils à l’aide d’Azure Application Insights.
 
**Métriques de cohérence, la latence, débit et disponibilité sont disponibles en toute transparence tooeach client**

![Mesures du contrat SLA visible par le client d’Azure Cosmos DB](./media/distribute-data-globally/customer-slas.png)

## <a id="Next Steps"></a>Étapes suivantes
* tooimplement de réplication global sur votre compte de base de données Azure Cosmos à l’aide de hello Azure portail, consultez [comment la réplication d’à l’aide globale de la base de données tooperform base de données Azure Cosmos hello portail Azure](tutorial-global-distribution-documentdb.md).
* toolearn sur la tooimplement des architectures multimaître avec la base de données Azure Cosmos, consultez [des architectures de base de données master multiples avec la base de données Azure Cosmos](multi-region-writers.md).
* toolearn en savoir plus sur les basculements automatiques et manuels de travail dans la base de données Azure Cosmos, voir [basculements régionaux dans la base de données Azure Cosmos](regional-failover.md).

## <a id="References"></a>Références
1. Eric Brewer. [Towards Robust Distributed Systems](https://people.eecs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf) (Vers des systèmes distribués robustes)
2. Eric Brewer. [Extrémité de fin douze années plus tard – comment les règles de hello ont changé](http://informatik.unibas.ch/fileadmin/Lectures/HS2012/CS341/workshops/reportsAndSlides/PresentationKevinUrban.pdf)
3. Gilbert, Lynch. - [Brewer&amp;#39;s Conjecture and Feasibility of Consistent, Available, Partition Tolerant Web Services](http://www.glassbeam.com/sites/all/themes/glassbeam/images/blog/10.1.1.67.6951.pdf) (Conjecture et faisabilité de services web cohérents, disponibles et tolérant le partitionnement)
4. Daniel Abadi. [Consistency Tradeoffs in Modern Distributed Database Systems Design](http://cs-www.cs.yale.edu/homes/dna/papers/abadi-pacelc.pdf) (Compromis en termes de cohérence dans la conception des systèmes de base de données distribués modernes)
5. Martin Kleppmann. [Please stop calling databases CP or AP](https://martin.kleppmann.com/2015/05/11/please-stop-calling-databases-cp-or-ap.html) (Arrêtez d’appeler les bases de données CP ou AP)
6. Peter Bailis et al. [Probabilistic Bounded Staleness (PBS) for Practical Partial Quorums](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf) (Probabilités en fonction de l’obsolescence limitée (PBS) pour les quorums partiels pratiques)
7. Naor and Wool. [Load, Capacity and Availability in Quorum Systems](http://www.cs.utexas.edu/~lorenzo/corsi/cs395t/04S/notes/naor98load.pdf) (Charge, capacité et disponibilité dans les systèmes de quorum)
8. Herlihy and Wing. [Lineralizability: A correctness condition for concurrent objects](http://cs.brown.edu/~mph/HerlihyW90/p463-herlihy.pdf) (Linéarisabilité : Une condition d’exactitude pour les objets simultanés)
9. [SLA pour Azure Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db/)
