---
title: "bases de données à grande échelle cloud aaaManaging | Documents Microsoft"
description: "Illustre le service de travail de base de données élastique hello"
metakeywords: azure sql database elastic databases
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 6fa47cf2-1162-4534-a206-6e2d95b78580
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: b6d330cd712421b8cba781e835830772e6e5b77e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-scaled-out-cloud-databases"></a>Gestion des bases de données cloud avec montée en charge
bases de données partitionnée toomanage à grande échelle, hello **des travaux de base de données élastique** fonctionnalité active (version préliminaire) tooreliably vous exécutez un script Transact-SQL (T-SQL) dans un groupe de bases de données, y compris :

* une collection personnalisée des bases de données (voir ci-après)
* toutes les bases de données dans un [pool élastique](sql-database-elastic-pool.md)
* un ensemble de partitions (créé à l’aide d’une [bibliothèque client de base de données élastique](sql-database-elastic-database-client-library.md)). 

## <a name="documentation"></a>Documentation
* [Installer les composants de travail de base de données élastique hello](sql-database-elastic-jobs-service-installation.md). 
* [Prise en main des tâches de base de données élastique](sql-database-elastic-jobs-getting-started.md).
* [Créer et gérer des tâches avec PowerShell](sql-database-elastic-jobs-powershell.md).
* [Créer et gérer des bases de données SQL Azure avec montée en charge](sql-database-elastic-jobs-getting-started.md)

**Les travaux de base de données élastiques** est actuellement un Service hébergé par le client de Cloud Azure qui permet l’exécution de hello d’ad hoc et tâches administratives planifiées, appelées **travaux**. Des travaux, vous pouvez facilement et gérez de manière fiable des grands groupes de bases de données SQL Azure en exécutant les opérations d’administration de tooperform de scripts Transact-SQL. 

![Service de tâche de base de données élastique][1]

## <a name="why-use-jobs"></a>Pourquoi utiliser les tâches ?
**Gérer**

Effectuer facilement des modifications de schéma, la gestion des informations d’identification, les mises à jour de données de référence, la collecte des données de performances ou la collecte télémétrique du locataire (client).

**Rapports**

Agréger des données à partir d’une collection de bases de données SQL Azure dans un tableau de destination unique.

**Réduction de la surcharge**

En règle générale, vous devez connecter tooeach de base de données de façon indépendante aux instructions de commande toorun Transact-SQL ou effectuer d’autres tâches d’administration. Un travail gère la tâche hello de la journalisation dans la base de données tooeach dans le groupe cible de hello. Vous également définissez, gérez et conserver toobe de scripts Transact-SQL exécutée sur un groupe de bases de données SQL Azure.

**Gestion des comptes**

Les travaux exécutés hello script et journal hello l’état de l’exécution pour chaque base de données. De plus, une nouvelle tentative est lancée automatiquement en cas d’échec.

**Flexibilité**

Définir des groupes personnalisés de bases de données SQL Azure, ainsi que des planifications pour l'exécution d’une tâche.

> [!NOTE]
> Bonjour portail Azure, un jeu réduit de fonctionnalités limité tooSQL Azure élastique pools n’est disponible. Utilisez hello PowerShell APIs tooaccess hello ensemble de fonctionnalités en cours.
> 
> 

## <a name="applications"></a>Applications
* Réaliser des tâches administratives, par exemple le déploiement d'un nouveau schéma.
* Mettre à jour les informations données-produits de référence sur toutes les bases de données. Ou planifier des mises à jour automatiques tous les jours ouvrables, après les heures de travail.
* Reconstruire les performances des requêtes tooimprove index. Hello reconstruction peut être configuré tooexecute sur une collection de bases de données sur une base périodique, comme pendant les heures creuses.
* Collecter les résultats de la requête à partir d'un ensemble de bases de données dans une table centrale sur une base continue. Les requêtes de performances peuvent être exécutées en permanence et configuré tootrigger des tâches supplémentaires toobe est exécutée.
* Exécuter des requêtes de traitement des données plus en cours d’exécution sur un grand ensemble de bases de données, par exemple hello collection de télémétrie de client. Les résultats sont rassemblés dans une table de destination unique pour une analyse ultérieure.

## <a name="elastic-database-jobs-end-to-end"></a>Travaux de base de données élastique : de bout en bout
1. Installer hello **des travaux de base de données élastique** composants. Pour en savoir plus, consultez [Installation des tâches de bases de données élastiques](sql-database-elastic-jobs-service-installation.md). Cas d’échec de l’installation de hello, voir [comment toouninstall](sql-database-elastic-jobs-uninstall.md).
2. Utilisez hello PowerShell APIs tooaccess plus de fonctionnalités, par exemple créer des collections personnalisées de la base de données, ajout de planifications et/ou la collecte des jeux de résultats. Utilisez hello portail installation simple et/contrôle de la création de travaux limitée tooexecution par rapport à un **pool élastique**. 
3. Créer des informations d’identification chiffrées pour l’exécution du travail et [ajouter hello utilisateur (ou rôle) tooeach base de données dans le groupe de hello](sql-database-security-overview.md).
4. Créer un script T-SQL qui peut être exécuté sur chaque base de données dans le groupe de hello idempotent. 
5. Suivez ces travaux de toocreate étapes à l’aide de hello portail Azure : [création et la gestion des travaux de base de données élastique](sql-database-elastic-jobs-create-and-manage.md). 
6. Ou utilisez des scripts PowerShell : [Création et gestion des travaux de base de données SQL élastiques à l’aide de PowerShell (version préliminaire)](sql-database-elastic-jobs-powershell.md).

## <a name="idempotent-scripts"></a>Scripts idempotents
les scripts Hello doivent être [idempotent](https://en.wikipedia.org/wiki/Idempotence). En termes simples, « idempotent » signifie que si le script de hello réussit, et il est exécuté à nouveau, hello même résultat se produit. Un script peut échouer en raison de problèmes de réseau tootransient. Dans ce cas, le travail de hello réessaiera automatiquement script hello en cours d’exécution un nombre prédéfini de fois avant desisting. Un script idempotent a hello même résultat même si a été correctement exécuté deux fois. 

Une solution simple est tootest existence hello d’un objet avant sa création.  

    IF NOT EXIST (some_object)
    -- Create hello object 
    -- If it exists, drop hello object before recreating it.

De même, un script doit être en mesure de tooexecute correctement en testant logiquement et contrecarrer toutes les conditions de recherche.

## <a name="failures-and-logs"></a>Échecs et journaux
Si un script échoue après plusieurs tentatives, le travail de hello consigne hello erreur et continue. Après la fin d’un travail (c'est-à-dire une exécution sur toutes les bases de données dans le groupe de hello), vous pouvez vérifier sa liste de tentatives ayant échoué. les journaux Hello fournissent des détails toodebug des scripts est défectueux. 

## <a name="group-types-and-creation"></a>Types de groupe et création
Il existe deux types de groupes : 

1. Ensemble de partitions
2. Groupes personnalisés

Groupes d’ensembles de partitions sont créés à l’aide de hello [outils de base de données élastique](sql-database-elastic-scale-introduction.md). Lorsque vous créez un groupe de jeu de partitions, bases de données sont ajoutées ou supprimées automatiquement à partir du groupe de hello. Par exemple, une nouvelle partition sera automatiquement dans le groupe de hello lorsque vous l’ajoutez carte de partitions toohello. Un travail peut ensuite être exécuté sur le groupe de hello.

Les groupes personnalisés, on hello d’autre part, sont définies de façon rigide. Vous devez explicitement ajouter ou supprimer des bases de données à partir de groupes personnalisés. Si une base de données dans le groupe de hello est supprimée, les travaux hello va tenter de script hello toorun entraîne un échec éventuel de la base de données hello. Les groupes créés à l’aide de hello portail Azure en sont des groupes personnalisés. 

## <a name="components-and-pricing"></a>Composants et tarification
Hello suivants composants fonctionnent ensemble toocreate un service Cloud Azure qui permet l’exécution d’ad-hoc des tâches d’administration. Hello composants sont installés et configurés automatiquement pendant l’installation, dans votre abonnement. Vous pouvez identifier les services hello comme elles ont hello même généré automatiquement nom. nom de Hello est unique et se compose d’un préfixe « edj hello » suivi de 21 caractères générés de manière aléatoire.

* **Le Service Cloud Azure**: travaux de base de données élastique (version préliminaire) sont fournies sous la forme d’un Cloud de Azure hébergé par le client l’exécution du service tooperform de hello les tâches demandées. À partir du portail de hello, service de hello est déployé et hébergé dans votre abonnement Microsoft Azure. service de valeur par défaut déployé Hello s’exécute avec au minimum deux rôles de travail pour la haute disponibilité hello. taille par défaut de Hello de chaque rôle de travail (ElasticDatabaseJobWorker) s’exécute sur une instance A0. Pour la tarification, voir [Tarification des services cloud](https://azure.microsoft.com/pricing/details/cloud-services/). 
* **Base de données SQL Azure**: service de hello utilise une base de données SQL Azure appelé hello **base de données contrôle** toostore toutes les métadonnées de tâche hello. niveau de service par défaut Hello est un S0. Pour en savoir plus, voir [Tarification - SQL Database](https://azure.microsoft.com/pricing/details/sql-database/).
* **Azure Service Bus**: un Bus des services Azure est pour la coordination de travail hello en hello Azure Cloud Service. Voir [Tarification de Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).
* **Le stockage Azure**: compte d’un stockage Azure est utilisé toostore diagnostic sortie de journalisation dans l’événement de hello un problème nécessite un débogage supplémentaire (consultez [activation des Diagnostics dans Azure Cloud Services et Machines virtuelles](../cloud-services/cloud-services-dotnet-diagnostics.md)). Pour la tarification, voir [Tarification Azure Storage](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-elastic-database-jobs-work"></a>Fonctionnement des tâches de bases de données élastiques
1. Une base de données SQL Azure est conçue comme une **base de données de contrôle** qui stocke toutes les métadonnées et les données d’état.
2. base de données de contrôle Hello est accessible par hello **de la tâche service** toolaunch et suivre le tooexecute de travaux.
3. Deux rôles qui communiquent avec la base de données de contrôle hello : 
   * Contrôleur : Détermine les tâches qui requièrent hello tooperform de tâches demandées du travail et nouvelles tentatives des travaux ayant échoué en créant de nouvelles tâches.
   * Exécution de la tâche travail : Exécute les tâches hello.

### <a name="job-task-types"></a>Types de tâches de travail
Il existe plusieurs types de tâches qui effectuent l'exécution des tâches :

* ShardMapRefresh : Requêtes hello toodetermine de carte de partitions toutes les bases de données hello utilisés en tant que partitions
* ScriptSplit : Script de hello fractionnements entre les instructions 'GO' en lots
* ExpandJob : crée des tâches enfants pour chaque base de données à partir d'une tâche qui cible un groupe de bases de données
* ScriptExecution : exécute un script sur une base de données spécifique à l'aide des informations d'identification définies
* Dacpac : S’applique à un DACPAC tooa base de données spécifique à l’aide des informations d’identification spécifiques

## <a name="end-to-end-job-execution-work-flow"></a>Flux de travail de l'exécution de tâche de bout en bout
1. Utilisez hello portail ou hello API PowerShell, un travail est inséré à hello **base de données de contrôle**. travail de Hello demande l’exécution d’un script Transact-SQL par rapport à un groupe de bases de données à l’aide des informations d’identification spécifiques.
2. contrôleur de Hello identifie la nouvelle tâche de hello. Tâches de travail sont créés et exécuté le script de hello toosplit et bases de données du groupe toorefresh hello. Enfin, un nouveau travail est créé et exécuté la tâche de hello tooexpand et créer des travaux, où chaque tâche enfant est spécifié tooexecute hello script Transact-SQL sur une base de données individuel dans le groupe de hello nouvel enfant.
3. contrôleur de Hello identifie hello créé des tâches enfants. Pour chaque tâche, le contrôleur de hello crée et déclenche un script hello de travail tâche tooexecute par rapport à une base de données. 
4. Une fois que toutes les tâches terminées, le contrôleur de hello met à jour l’état de tooa terminé de travaux de hello. 
   À tout moment pendant l’exécution du travail, hello API PowerShell peut être utilisé tooview hello l’état actuel de l’exécution du travail. Toutes les heures retourné par hello APIs PowerShell sont représentés au format UTC. Si vous le souhaitez, une demande d’annulation peut être toostop initiée par un travail. 

## <a name="next-steps"></a>Étapes suivantes
[Installer les composants de hello](sql-database-elastic-jobs-service-installation.md), puis [créer et ajouter un journal de base de données tooeach groupe hello des bases de données](sql-database-manage-logins.md). toofurther comprendre la gestion et création de tâche, consultez [créer et gérer des travaux de base de données élastique](sql-database-elastic-jobs-create-and-manage.md). Consultez également [Prise en main des tâches de base de données élastique](sql-database-elastic-jobs-getting-started.md).

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-overview/elastic-jobs.png
<!--anchors-->


