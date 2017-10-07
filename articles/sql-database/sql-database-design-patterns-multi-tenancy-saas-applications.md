---
title: "modèles d’aaaDesign pour les applications SaaS à plusieurs locataires et de la base de données SQL Azure | Documents Microsoft"
description: "Cet article décrit les exigences de hello et modèles d’architecture de données courantes des applications de base de données en cours d’exécution dans un environnement cloud besoin tooconsider hello différentes limites associées à ces modèles. Il explique également comment Azure SQL Database, avec ses outils et ses pools élastiques, permet de satisfaire ces exigences sans aucun compromis."
keywords: 
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 1dd20c6b-ddbb-40ef-ad34-609d398d008a
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-design
ms.date: 02/01/2017
ms.author: srinia
ms.openlocfilehash: a4b58935b08cb78792e65a675d680de708b709fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multi-tenant-saas-applications-and-azure-sql-database"></a>Modèles de conception pour les applications SaaS multilocataires et Azure SQL Database
Dans cet article, vous pouvez en savoir plus sur les exigences de hello et modèles d’architecture de données courantes des logiciels de l’architecture mutualisée comme une application de base de données de service (SaaS) qui s’exécutent dans un environnement de cloud. Elle explique également de facteurs hello vous devez tooconsider et hello compromis des modèles de conception différentes. Les pools élastiques et les outils élastiques dans Azure SQL Database peuvent vous aider à répondre à des besoins spécifiques sans compromettre d’autres objectifs.

Parfois, les développeurs prendre des décisions qui fonctionnent sur leur intérêt à long terme lorsqu’ils conçoivent des modèles d’architecture mutualisée pour les couches de données hello d’applications mutualisées. Initialement, au moins, un développeur peut percevoir facilité de développement et de réduire les coûts cloud service fournisseur comme la plus importante que l’extensibilité d’isolation ou hello client d’une application. Ce choix peut entraîner les problèmes de satisfaction toocustomer et une correction de cours coûteuse ultérieurement.

Une application mutualisée est une application hébergée dans un environnement cloud et hello même ensemble de services toohundreds plusieurs milliers de clients qui ne pas partager ou afficher les données de l’autre. Un exemple est une application SaaS qui fournit des tootenants de services dans un environnement hébergé dans le cloud.

## <a name="multi-tenant-applications"></a>Applications multilocataires
Dans les applications multilocataires, il est aisé de partitionner les données et la charge de travail. Vous pouvez partitionner données et la charge de travail, par exemple, le long des limites du client, car la plupart des requêtes se produisent dans les limites de hello d’un locataire. Cette propriété est inhérente dans les données de salutation et de la charge de travail hello et il privilégie les modèles d’application hello abordés dans cet article.

Les développeurs utilisent ce type d’application entre hello large éventail d’applications cloud, notamment :

* Les applications de base de données partenaire qui sont en cours a été transféré toohello cloud en tant qu’applications SaaS
* Applications SaaS créées pour le cloud hello de hello d’arrière-plan
* Les applications directes orientées client
* Les applications d’entreprise orientées employé

Applications SaaS qui sont conçues pour le cloud de hello et ceux dont les racines comme applications de base de données de partenaires sont généralement des applications mutualisées. Ces applications SaaS offrent une application spécialisée un locataires tootheir de service. Les clients peuvent accéder au service de l’application hello et avoir la propriété complète de données associées stockées dans le cadre de l’application hello. Mais bénéficiant de tootake de hello SaaS, les clients doive renoncer à contrôler leurs propres données. Ils font confiance hello SaaS service fournisseur tookeep leurs données sécurisées et isolées à partir des données d’autres clients. MYOB, SnelStart et Salesforce.com sont des exemples de ce type d’applications SaaS multilocataires. Chacune de ces applications peut être partitionnée selon les limites de client et les modèles de conception d’application hello prise en charge que les sujets abordés dans cet article.

Les applications qui fournissent un service direct toocustomers ou le tooemployees au sein d’une organisation (souvent désignée tooas utilisateurs, plutôt que les clients) sont une autre catégorie sur un spectre d’application mutualisée hello. Les clients s’abonner toohello service et ne possèdent pas de données hello hello du fournisseur de services de collecte et de stockage. Fournisseurs de services ont moins strictes exigences tookeep isolées de l’autre au-delà des réglementations imposées par le gouvernement la confidentialité des données de leurs clients. Les fournisseurs de contenus multimédias comme Netflix, Spotify et Xbox LIVE sont des exemples de ce type d’applications multilocataires orientées client. Il existe d’autres exemples d’applications facilement configurables en partition comme les applications Internet orientées client ou les applications IoT (Internet des objets), dans lesquelles chaque client ou appareil peut servir de partition. Les limites de partition peuvent séparer les utilisateurs et les appareils.

Le partitionnement des applications n’est pas toujours simple pour une propriété unique (locataire, client, utilisateur, appareil, etc.). Une application ERP complexe, par exemple, traite des produits, des commandes et des clients. Elle suit généralement un schéma complexe avec des milliers de tables hautement interconnectées.

Aucune stratégie de partition unique puisse appliquer des tables de tooall et fonctionnent sur les charges de travail d’une application. Cet article se concentre sur les applications multilocataires comportant des charges de travail et des données facilement configurables en partition.

## <a name="multi-tenant-application-design-trade-offs"></a>Compromis de conception des applications multilocataires
modèle de conception de Hello un développeur d’application mutualisée choisit généralement est basé sur un facteur important de hello suivant facteurs :

* **Isolation des locataires**. développeur de Hello doit tooensure qu’aucun client ne comporte des données de clients tooother contre un accès. spécification d’isolation Hello étend tooother propriétés, telles qu’offrant une protection à partir de voisins bruyantes, qui est en mesure de toorestore les données d’un locataire et mettre en œuvre les personnalisations spécifiques du client.
* **Coût des ressources du cloud**. Une application SaaS doit toobe économique. Un développeur d’application mutualisée peut choisir toooptimize pour réduire le coût en cours d’utilisation hello des ressources du cloud, tels que le stockage et les coûts de calcul.
* **Convivialité DevOps**. Un développeur d’application mutualisée requiert une protection d’isolation tooincorporate, mettre à jour et surveiller l’intégrité de hello un schéma de base de données et les applications et résoudre les problèmes de client. La complexité de développement d’applications et l’opération traduit directement tooincreased coût et défis avec la satisfaction client.
* **Extensibilité**. Hello capacité tooincrementally ajouter plus de clients et de capacité pour les clients qui ont besoin qu’il est impératif tooa opération SaaS.

Chacun de ces facteurs a compromis comparées tooanother. cloud plus économique Hello peuvent ne pas offrir l’expérience de développement hello plus pratique de l’offre. Il est important pour un développeur toomake informés de choix de ces options et leurs compromis pendant le processus de conception d’application hello.

Un modèle de développement courants est toopack plusieurs locataires dans une ou plusieurs bases de données. avantages de Hello de cette approche sont un coût inférieur comme vous payez pour certaines bases de données et la simplicité de relatif hello de travailler avec un nombre limité de bases de données. Toutefois, au fil du temps, un développeur d’applications multilocataires SaaS réalisera que ce choix présente des inconvénients substantiels pour l’isolation des locataires et la scalabilité. Si l’isolation des locataires devient importante, effort supplémentaire est tooprotect requis des données du locataire dans le stockage partagé à partir de tout accès non autorisé ou bruyants voisins. Cet effort supplémentaire peut augmenter considérablement les efforts de développement et les coûts de maintenance de l’isolation. De même, si l’ajout des locataires est requis, ce modèle de conception requiert généralement des données du locataire expertise tooredistribute entre la couche données de hello d’échelle tooproperly bases de données d’une application.  

Isolation des locataires souvent est une condition fondamentale dans les applications SaaS mutualisées prenant en charge toobusinesses et des organisations. Un développeur peut se laisser tenter par les avantages apparents liés à la simplicité et au coût, au lieu de privilégier l’isolation des locataires et l’évolutivité. Ce compromis peut s’avérer complexe et coûteux comme service de hello se développe et des conditions d’isolation locataire deviennent plus importantes et gérée au niveau de la couche d’application hello. Toutefois, dans les applications mutualisées qui fournissent un toocustomers service directe pour les consommateurs, isolation des locataires peut être une priorité inférieure à l’optimisation pour le coût des ressources de cloud.

## <a name="multi-tenant-data-models"></a>Modèles de données multilocataires
Les pratiques de conception courantes pour placer les données des locataires suivent trois modèles distincts illustrés dans la Figure 1.

![modèles de données d’applications multilocataires](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-multi-tenant-data-models.png)

Figure 1 : Pratiques de conception courantes pour les modèles de données multilocataires

* **Base de données par locataire**. Chaque locataire a sa propre base de données. Toutes les données spécifiques du client est confiné toohello de base de données et isolé des autres locataires et leurs données.
* **Base de données partagée partitionnée**. Plusieurs locataires partagent l’une des différentes bases de données. Un ensemble distinct de clients est affecté tooeach de base de données à l’aide d’une stratégie de partitionnement telles que le hachage, la plage ou le partitionnement de la liste. Cette stratégie de distribution de données est souvent désignée tooas partitionnement.
* **Base de données partagée unique**. Une base de données unique et parfois volumineuse contient des données permettant d’éviter toute ambiguïté à propos des locataires dans une colonne d’ID de locataire.

> [!NOTE]
> Un développeur d’applications peut choisir tooplace de plusieurs clients dans les schémas de base de données différent et utilisez hello schéma nom toodisambiguate hello de plusieurs clients. Nous déconseillons cette approche, car elle nécessite généralement utiliser hello SQL dynamique, et il ne peut pas être efficace dans la mise en cache du plan. Dans le reste de hello de cet article, nous concentrer sur approche de table hello partagé pour cette catégorie d’application mutualisée.
> 
> 

## <a name="popular-multi-tenant-data-models"></a>Modèles de données multilocataires courants
Il est important tooevaluate hello différents types de modèles de données de l’architecture mutualisée en termes de hello application conception compromis que nous avons déjà identifié. Ces facteurs aident caractérisent hello trois courants mutualisée des modèles décrits précédemment et leur utilisation de base de données, comme indiqué dans la Figure 2.

* **Isolement**. degré de Hello d’isolation entre les clients peut être une mesure de la quantité isolation des locataires permet d’obtenir un modèle de données.
* **Coût des ressources du cloud**. quantité Hello de partage de ressources entre les clients peut optimiser le coût des ressources de cloud. Une ressource peut être définie comme le coût de stockage et de calcul de hello.
* **Coût DevOps**. facilité Hello du développement d’applications, de déploiement et de facilité de gestion réduit le coût de fonctionnement global SaaS.  

Dans la Figure 2, axe de hello Y affiche au niveau d’isolation des locataires du hello. axe de Hello X montre niveau hello de partage des ressources. gris de Hello, flèche diagonale milieu de hello indique la direction hello des coûts DevOps, tendance tooincrease ou diminuer.

![Modèles courants de conception d’applications multilocataires](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-popular-application-patterns.png)

Figure 2 : Modèles de données multilocataires courants

Hello quadrant inférieur droit dans la Figure 2 montre un modèle d’application qui utilise une base de données unique potentiellement volumineux, partagée et hello partagé table (ou un schéma distinct) approche. Il est recommandé pour la ressource de partage, car tous les locataires utilisent hello mêmes ressources (processeur, mémoire, entrée/sortie) dans une base de données de la base de données. Cependant, l’isolation des locataires est limitée. Vous devrez peut-être tootake des étapes supplémentaires tooprotect aux clients de l’autre au niveau de la couche d’application hello. Ces étapes supplémentaires peuvent augmenter considérablement le coût de DevOps hello de développement et la gestion d’application hello. L’évolutivité est limitée par la montée en puissance hello du matériel hello qui héberge la base de données hello.

quadrant inférieur gauche de Hello dans la Figure 2 illustre plusieurs clients partitionnées entre plusieurs bases de données (en général, un matériel différent échelle unités). Chaque base de données héberge un sous-ensemble de clients, qui résout le problème d’évolutivité hello d’autres modèles. Si plus de capacité est requise pour les clients de plus, vous pouvez facilement placer les locataires hello sur les nouvelles bases de données alloués des unités d’échelle toonew matériel. Toutefois, la quantité hello de partage des ressources est réduite. Seule locataires placée sur hello même unités d’échelle partagent des ressources. Cette approche fournit une isolation de tootenant peu d’amélioration du produit, car de nombreux clients sont toujours colocalisés sans automatiquement protégée contre les actions des autres. L’application reste très complexe.

quadrant supérieur gauche de Hello dans la Figure 2 est l’approche de tiers de hello. Il place les données de chaque locataire dans sa propre base de données. Cette approche présente de bonnes propriétés d’isolation des locataires, mais elle limite le partage des ressources lorsque chaque base de données a ses propres ressources dédiées. Il s’agit d’une bonne approche si tous les locataires ont des charges de travail prévisibles. Si les charges de travail client sont moins prévisibles, fournisseur de hello ne peut pas optimiser le partage des ressources. L’imprévisibilité est courante pour les applications SaaS. fournisseur de Hello devez soit surconfigurer toomeet demandes ou des ressources inférieure. Ces actions se traduisent soit par une augmentation des coûts, soit par une diminution de la satisfaction des locataires. Un degré plus élevé de ressource de partage entre les clients devient toomake souhaitable la solution hello plus économique. Nombre croissant de hello des bases de données augmente DevOps coût toodeploy également et mettre à jour d’application hello. Malgré ces problèmes, cette méthode fournit une isolation de hello meilleure et plus facile pour les clients.

Ces facteurs d’influence également un client choisit de modèle de conception de hello :

* **Propriété des données des locataires**. Une application dans laquelle les clients conservent la propriété de leurs propres données favorise modèle hello d’une base de données par client.
* **Mettant à l’échelle**. Une application qui cible des centaines de milliers ou des millions de clients favorise les approches de partage des bases de données comme le partitionnement. Les exigences d’isolation peuvent encore poser des problèmes.
* **Modèle de valeur et d’entreprise**. Si le chiffre d’affaires par locataire d’une application est faible (moins d’un dollar), les exigences d’isolation deviennent moins critiques et il est plus logique de recourir à des bases de données partagées. Si le chiffre d’affaires par locataire est de quelques dollars ou plus, il est préférable d’utiliser un modèle de base de données par locataire. Cela peut contribuer à réduire les coûts de développement.

Étant donné hello conception compromis indiqués dans la Figure 2, un modèle d’architecture mutualisé idéal doit les propriétés d’isolation tooincorporate bon client avec optimale des ressources de partage entre les clients. Ce modèle tient dans catégorie hello décrit quadrant du coin supérieur droit hello de la Figure 2.

## <a name="multi-tenancy-support-in-azure-sql-database"></a>Prise en charge des modèles multilocataires dans Azure SQL Database
Azure SQL Database prend en charge tous les modèles d’applications multilocataires décrits dans la Figure 2. Avec les pools élastiques, prend également en charge le modèle d’application qui combine la bonne ressource partage et avantages d’isolation hello de base de données par client hello approchent (voir quadrant du coin supérieur droit hello dans la Figure 3). Outils de base de données élastique et des fonctions dans la base de données SQL aider à réduire hello coût toodevelop et d’utiliser une application qui possède de nombreuses bases de données (affichées dans la zone hello ombré dans la Figure 3). Ces outils peuvent vous aider à créer et gérer des applications qui utilisent un des modèles de bases de données multiples hello.

![Modèles dans Azure SQL Database](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-patterns-sqldb.png)

Figure 3 : Modèles d’applications multilocataires dans Azure SQL Database

## <a name="database-per-tenant-model-with-elastic-pools-and-tools"></a>Modèle de base de données par locataire avec outils et pools élastiques
Les pools élastiques dans la base de données SQL combinent isolation des locataires avec le partage de ressources entre l’approche de la base de données pour chaque locataire client bases de données toobetter prise en charge hello. SQL Database est une solution de couche de données pour les fournisseurs SaaS qui créent des applications multilocataires. charge Hello de partage de ressources entre les locataires passe à partir de la couche de service de base de données hello application couche toohello. complexité Hello de la gestion et l’interrogation de bases de données à l’échelle est simplifiée grâce à des travaux élastiques, requête élastique, transactions élastiques et bibliothèque cliente de base de données élastique hello.

| Exigences de l’application | Fonctionnalités de Base de données SQL |
| --- | --- |
| Isolation des locataires et partage des ressources |[Pools élastiques](sql-database-elastic-pool.md): allouez un pool de ressources de base de données SQL et de partager des ressources de hello dans différentes bases de données. En outre, des bases de données peuvent dessiner autant de ressources à partir du pool de hello en tant que les pics de demandes de capacité tooaccommodate nécessaires toochanges échéance dans les charges de travail clientes. pool élastique de Hello lui-même peut être monté en haut ou vers le bas en fonction des besoins. Pools élastiques fournissent également la facilité de gestion et de surveillance et de résolution des problèmes au niveau du pool hello. |
| Simplicité des opérations de développement entre bases de données |[Pools élastiques](sql-database-elastic-pool.md): comme indiqué ci-dessus. |
| | [Requête élastique](sql-database-elastic-query-horizontal-partitioning.md): permet d’interroger des bases de données pour la création de rapports ou l’analyse entre locataires. |
| | [Travaux élastique](sql-database-elastic-jobs-overview.md): Package et déployer de manière fiable des opérations de maintenance de base de données ou bases de données toomultiple de modifications de schéma de base de données. |
| | [Transactions élastiques](sql-database-elastic-transactions-overview.md): processus modifie les bases de données tooseveral de manière atomique et isolée. Les transactions élastiques sont nécessaire lorsque des applications ont besoin de garanties « tout ou rien » sur plusieurs opérations de base de données. |
| | [Bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md): gérer les distributions de données et de mappage toodatabases les locataires. |

## <a name="shared-models"></a>Modèles partagés
Comme indiqué précédemment, pour la plupart des fournisseurs SaaS une approche de modèle partagé peut engendrer des problèmes d’isolation des locataires, mais aussi compliquer le développement et la maintenance des applications. Toutefois, pour les applications mutualisées qui fournissent un service directement du locataire tooconsumers, aux exigences d’isolation peut-être pas comme prioritaires comme en réduisant les coûts. Elles peuvent être toopack en mesure des locataires dans une ou plusieurs bases de données à un coût de tooreduce haute densité. Les modèles de base de données partagée qui utilisent une base de données unique ou plusieurs bases de données partitionnées peuvent améliorer le partage des ressources et faire baisser les coûts globaux. Base de données SQL Azure fournit des fonctionnalités qui aident les clients génération d’isolation pour améliorer la sécurité et de gestion à grande échelle dans la couche de données hello.

| Exigences de l’application | Fonctionnalités de Base de données SQL |
| --- | --- |
| Fonctionnalités d’isolation pour la sécurité |[Sécurité au niveau des lignes](https://msdn.microsoft.com/library/dn765131.aspx) |
| [Schéma de base de données](https://msdn.microsoft.com/library/dd207005.aspx) | |
| Simplicité des opérations de développement entre bases de données |[Requête élastique](sql-database-elastic-query-horizontal-partitioning.md) |
| | [Tâches élastiques](sql-database-elastic-jobs-overview.md) |
| | [Transactions élastiques](sql-database-elastic-transactions-overview.md) |
| | [Bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md) |
| | [Fractionnement et fusion de base de données élastique](sql-database-elastic-scale-overview-split-and-merge.md) |

## <a name="summary"></a>Résumé
Les exigences en matière d’isolation des locataires sont importantes pour la plupart des applications multilocataires SaaS. isolation de Hello meilleure option tooprovide utilise largement vers l’approche de base de données pour chaque locataire hello. Hello deux autres approches nécessitent l’investissement dans les couches application complexe qui requièrent le développement et les dons personnel tooprovide d’isolation, ce qui augmente considérablement les coûts et les risques. Si aux exigences d’isolation ne sont pas prises en compte pour tôt dans le développement du service hello, il peut être encore plus coûteux dans les modèles de deux premières hello de rattrapage les. Hello principaux inconvénients associés au modèle de base de données pour chaque locataire hello sont les coûts des ressources cloud tooincreased connexes en raison de tooreduced de partage et la maintenance et la gestion des nombreuses bases de données. Les développeurs d’applications SaaS sont souvent bien embêtés de devoir faire ces compromis.

Bien que les compromis des barrières avec la plupart des fournisseurs de services cloud de base de données, base de données SQL Azure élimine les barrières de hello avec son pool élastique et ses fonctionnalités de base de données élastique. Les développeurs de SaaS peuvent combiner les caractéristiques d’isolation hello d’un modèle de base de données pour chaque locataire et optimiser les ressources de partage et hello possibilités de nombreuses bases de données à l’aide de pools élastiques et les outils associés.

Pour les fournisseurs d’applications multilocataires qui n’affichent aucune exigence en termes d’isolation des locataires et peuvent regrouper les locataires dans une base de données à haute densité, les modèles de données partagées offrent la possibilité d’améliorer le partage des ressources et de réduire le coût total. Les outils de bases de données élastiques Azure SQL Database, les bibliothèques de partitionnement et les fonctionnalités de sécurité aident les fournisseurs SaaS à créer et à gérer des applications multilocataires.

## <a name="next-steps"></a>Étapes suivantes
[Prise en main des outils de base de données élastique](sql-database-elastic-scale-get-started.md) avec un exemple d’application qui illustre la bibliothèque cliente de hello.

Créez un [tableau de bord personnalisé de pool élastique pour SaaS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools-custom-dashboard) avec un exemple d’application qui utilise des pools élastiques pour fournir une solution de base de données économique et évolutive.

Utilisez les outils de base de données SQL Azure hello trop[migrer tooscale de bases de données existant à](sql-database-elastic-convert-to-use-elastic-tools.md).

un pool élastique à l’aide de toocreate hello Azure portail, consultez [créer un pool élastique](sql-database-elastic-pool-manage-portal.md).  

Découvrez comment trop[surveiller et gérer un pool élastique](sql-database-elastic-pool-manage-portal.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Déployer et explorer une application multilocataire qui utilise Azure SQL Database - Wingtip SaaS](sql-database-saas-tutorial.md)
* [Qu’est-ce qu’un pool élastique Azure ?](sql-database-elastic-pool.md)
* [Montée en charge avec Azure SQL Database](sql-database-elastic-scale-introduction.md)
* [applications multilocataires avec des outils de bases de données élastiques et la sécurité au niveau des lignes](sql-database-elastic-tools-multi-tenant-row-level-security.md)
* [Authentification dans des applications multilocataires à l’aide d’Azure Active Directory et d’OpenID Connect](../guidance/guidance-multitenant-identity-authenticate.md)
* [Application Tailspin Surveys](../guidance/guidance-multitenant-identity-tailspin.md)


## <a name="questions-and-feature-requests"></a>Questions et demandes de fonctionnalités

Pour toute question, nous trouver Bonjour [Forum sur la base de données SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted). Ajout d’une demande de fonctionnalité Bonjour [forum de commentaires de la base de données SQL](https://feedback.azure.com/forums/217321-sql-database/).

