---
title: "basculement aaaRegional dans la base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez le fonctionnement du basculement manuel et automatique avec Azure Cosmos DB."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 446e2580-ff49-4485-8e53-ae34e08d997f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2fdc7b0e8958d129ab027e4b11193b12961ddae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-regional-failover-for-business-continuity-in-azure-cosmos-db"></a>Basculement régional automatique pour la continuité des activités dans Azure Cosmos DB
Base de données Azure Cosmos simplifie la distribution globale de hello des données en offrant entièrement géré, [des comptes de base de données de plusieurs régions](distribute-data-globally.md) qui fournissent les effacer compromis entre les performances, toutes avec correspondant, la disponibilité et la cohérence garanties. Les comptes de COSMOS DB offrent une haute disponibilité, des latences de ms chiffre unique, [niveaux de cohérence bien définis](consistency-levels.md), le basculement transparent régional avec hébergement multiple d’API et de débit de l’échelle tooelastically hello capacité et de stockage monde de hello. 

COSMOS DB prend en charge explicite et reposant sur des stratégies de basculement permettent de comportement de système de bout en bout toocontrol hello dans l’événement hello d’échecs. Dans cet article, nous allons répondre aux questions suivantes :

* Comment fonctionnent les basculements manuels dans Cosmos DB ?
* Comment fonctionnent les basculements automatiques dans Cosmos DB et que se passe-t-il lorsqu’un centre de données tombe en panne ?
* Comment utiliser les basculements manuels dans différentes architectures d’application ?

Vous pouvez également découvrir les basculements régionaux dans cette vidéo Azure Friday avec Scott Hanselman et Karthik Raman, responsable principal de l’ingénierie DocumentDB.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

## <a id="ConfigureMultiRegionApplications"></a>Configuration d'applications multi-régions
Avant d’étudier les modes de basculement, nous allons comment vous pouvez configurer un avantage de tootake d’application de la disponibilité de plusieurs région et qu’elles soient résistantes en face de hello basculements régional.

* Tout d’abord, déployez votre application multi-régions
* l’accès à faible latence tooensure à partir de chaque région de votre application est déployée, configurer hello correspondant [liste régions préféré](https://msdn.microsoft.com/library/microsoft.azure.documents.client.connectionpolicy.preferredlocations.aspx#P:Microsoft.Azure.Documents.Client.ConnectionPolicy.PreferredLocations) pour chaque région via l’une des hello pris en charge les kits de développement logiciel.

Hello suivant extrait de code montre comment tooinitialize une application de plusieurs région. Ici, hello compte de base de données Azure Cosmos `contoso.documents.azure.com` est configuré avec deux régions - Ouest des États-Unis et Europe du Nord. 

* application Hello est déployée dans la région ouest des États-Unis hello (à l’aide de Services d’application Azure par exemple) 
* Configuré avec `West US` en tant que première région préférée hello pour une latence faible lit
* Configuré avec `North Europe` en tant que la région préférée deuxième hello (pour une haute disponibilité lors des défaillances régionales)

Bonjour API DocumentDB, cette configuration ressemble hello suivant extrait de code :

```cs
ConnectionPolicy usConnectionPolicy = new ConnectionPolicy 
{ 
    ConnectionMode = ConnectionMode.Direct,
    ConnectionProtocol = Protocol.Tcp
};

usConnectionPolicy.PreferredLocations.Add(LocationNames.WestUS);
usConnectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

DocumentClient usClient = new DocumentClient(
    new Uri("https://contosodb.documents.azure.com"),
    "memf7qfF89n6KL9vcb7rIQl6tfgZsRt5gY5dh3BIjesarJanYIcg2Edn9uPOUIVwgkAugOb2zUdCR2h0PTtMrA==",
    usConnectionPolicy);
```

application Hello est également déployée dans la région Europe du Nord hello avec ordre hello préféré régions inversées. Autrement dit, la région Europe du Nord hello est spécifiée en premier pour les lectures de faible latence. Ensuite, la région ouest des États-Unis hello est spécifiée en tant que la région préférée deuxième hello pour la haute disponibilité lors des défaillances régionales.

Hello architecture diagramme suivant illustre un déploiement d’application de plusieurs régions où Cosmos DB et l’application hello sont toobe configurée disponible dans quatre régions géographiques de Azure.  

![Déploiement d’une application distribuée dans le monde entier avec Azure Cosmos DB](./media/regional-failover/app-deployment.png)

À présent, voyons comment hello Cosmos DB service gère les défaillances régionales via les basculements automatiques. 

## <a id="AutomaticFailovers"></a>Basculements automatiques
Dans hello rares cas d’une panne régionale Azure ou une panne du centre de données, Cosmos DB déclenche automatiquement des basculements de tous les comptes Cosmos DB avec sa présence dans la région de hello affectée. 

**Que se passe-t-il si une région de lecture connaît une panne ?**

Comptes COSMOS DB avec une zone de lecture de l’une des régions de hello affecté sont automatiquement déconnectés de la région de leur écriture et marqués hors connexion. Hello kits de développement logiciel Cosmos DB implémentent un protocole de découverte régionale qui leur permet de tooautomatically détecter une région n’est disponible et la redirection de lire des appels toohello suivante région disponibles dans la liste de la région préférée hello. Si aucune des régions hello Bonjour préféré liste région n’est disponible, les appels revient automatiquement zone d’écriture en cours toohello. Aucun changement est nécessaire dans votre code d’application toohandle des basculements de régional. Pendant ce processus, des garanties de cohérence continuent toobe honorée par base de données Cosmos.

![Défaillances de la région de lecture dans Azure Cosmos DB](./media/regional-failover/read-region-failures.png)

Une fois la région de hello affectée récupère à partir de la panne de hello, tous les comptes de Cosmos DB hello affectée dans la région de hello sont récupérés automatiquement par le service de hello. Comptes COSMOS DB ayant une région de lecture dans la région de hello affectée ensuite automatiquement une synchronisation avec la zone d’écriture en cours et activer en ligne. Kits de développement logiciel Hello Cosmos DB découvrir disponibilité hello de nouvelle région de hello et évaluer si la région de hello doit être sélectionnée en tant que région actuelle lecture hello en fonction de liste de la région préférée hello configuré par l’application hello. Les lectures sont redirigés toohello de région récupérée sans requérir de modifications tooyour application code.

**Que se passe-t-il si une région d'écriture connaît une panne ?**

Si la région affectée de hello est hello région en cours écriture pour un compte de base de données Cosmos donné, puis la région de hello est automatiquement marquée comme étant hors connexion. Ensuite, une autre région est promue comme hello écrire région chaque compte Cosmos DB concerné. Vous pouvez contrôler entièrement l’ordre de sélection de région de hello pour vos comptes de base de données Cosmos via hello portail Azure ou [par programme](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_FailoverPriorityChange). 

![Priorités de basculement pour Azure Cosmos DB](./media/regional-failover/failover-priorities.png)

Pendant les basculements automatiques, Cosmos DB choisit automatiquement la zone d’écriture suivante hello pour une base de données donnée Cosmos compte selon hello spécifié ordre de priorité. 

![Défaillances de la région d’écriture dans Azure Cosmos DB](./media/regional-failover/write-region-failures.png)

Une fois la région de hello affectée récupère à partir de la panne de hello, tous les comptes de Cosmos DB hello affectée dans la région de hello sont récupérés automatiquement par le service de hello. 

* Comptes COSMOS DB avec leur région d’écriture précédente dans la région de hello affectée resteront en mode hors connexion avec la disponibilité en lecture, même après la récupération hello de région de hello. 
* Vous pouvez interroger cette toocompute région des écritures non répliquées panne hello en comparant avec des données hello disponibles dans la zone d’écriture en cours hello. Selon les besoins de hello de votre application, vous pouvez effectuer une résolution de fusion et de conflit et écrire le jeu final de hello de zone d’écriture en cours modifications toohello précédent. 
* Une fois que vous avez terminé la fusion des modifications, vous pouvez remettre région de hello affecté en ligne en supprimant et en readding compte de base de données Cosmos tooyour hello région. Une fois la région de hello est à nouveau ajoutée, vous pouvez le configurer comme région d’écriture hello en effectuant un basculement manuel via hello portail Azure ou [par programme](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate).

## <a id="ManualFailovers"></a>Basculements manuels

En outre d’écrire tooautomatic basculements, hello actuel région d’un compte de base de données Cosmos donné peut être modifiée manuellement dynamiquement tooone des régions de lecture existant hello. Les basculements manuels peuvent être lancées via hello portail Azure ou [par programme](https://docs.microsoft.com/rest/api/documentdbresourceprovider/databaseaccounts#DatabaseAccounts_CreateOrUpdate). 

Assurez-vous de basculements manuels **aucune perte de données** et **zéro disponibilité** perte et normalement l’état d’écriture de transfert des hello ancien écrivent toohello de région nouveau pour hello spécifié un compte de base de données Cosmos. Comme dans les basculements automatiques, hello Cosmos DB SDK automatiquement handles écrire région change pendant les basculements manuels et garantit que les appels sont automatiquement redirigé toohello nouvelle écriture zone. Aucune modification de code ou de configuration n’est requises dans votre application toomanage les basculements. 

![Basculements manuels dans Azure Cosmos DB](./media/regional-failover/manual-failovers.png)

Certains des scénarios courants de hello où le basculement manuel peut être utile sont :

**Suivre le modèle d’horloge hello**: si vos applications ont des modèles de trafic prévisible selon hello heure hello, vous pouvez changer régulièrement hello écriture état toohello plus actifs région géographique en fonction de l’heure du jour de hello.

**Mise à jour de service**: Certain déploiement d’application distribuée globalement peut impliquer la redirection de la région toodifferent le trafic via le Gestionnaire de trafic pendant leur mise à jour de service planifiée. Ce déploiement de l’application maintenant pouvez utiliser le basculement manuel tookeep hello écriture état toohello région où il y aura le trafic active de toobe au cours de la fenêtre de mise à jour de service hello.

**Simulations de continuité d’activité et de récupération d’urgence (Business Continuity and Disaster Recovery, BCDR) et Haute disponibilité et récupération d’urgence (High Availability and Disaster Recovery, HADR)** : la plupart des applications d’entreprise incluent des tests de continuité d’activité dans le cadre de leurs processus de développement et de mise sur le marché. BCDR et HADR test est souvent une étape importante dans les certifications de conformité et garantissant la disponibilité en cas de hello de pannes de courant régionales. Vous pouvez tester la disponibilité BCDR hello de vos applications qui utilisent des Cosmos DB pour le stockage en déclencher un basculement manuel de votre compte de base de données Cosmos et/ou en ajoutant et en supprimant une région dynamiquement.

Dans cet article, nous avons vu comment du travail de basculements manuel et automatique dans la base de données Cosmos et comment vous pouvez configurer votre toobe Cosmos DB comptes et les applications disponible. À l’aide de prise en charge de Cosmos DB global de réplication, vous pouvez améliorer la latence de bout en bout et vous assurer qu’ils sont hautement disponibles même en cas de hello d’échecs de la région. 

## <a id="NextSteps"></a>Étapes suivantes
* Découvrez-en plus sur la manière dont Cosmos DB prend en charge la [distribution mondiale](distribute-data-globally.md)
* Découvrez-en plus sur [la cohérence globale avec Azure Cosmos DB](consistency-levels.md)
* Développez en mode multirégion à l’aide de l’[API DocumentDB](../cosmos-db/tutorial-global-distribution-documentdb.md) d’Azure Cosmos DB
* Découvrez comment toobuild [architectures d’enregistreur de plusieurs régions](multi-region-writers.md) avec Azure DocumentDB

