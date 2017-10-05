---
title: Diagnostics et surveillance des performances Azure Service Fabric | Microsoft Docs
description: "Cet article décrit les fonctionnalités de surveillance des performances dans le runtime Reliable Service Remoting de Service Fabric, notamment les compteurs de performances émis par celui-ci."
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: suchiagicha
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: suchiagicha
ms.openlocfilehash: f54e157654fb15d2f7ff48ddc666c6c8803c75a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-service-remoting"></a>Diagnostics et surveillance des performances pour Reliable Service Remoting
Le runtime Reliable Service Remoting émet des [compteur de performances](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Ils fournissent des informations sur le fonctionnement du runtime Service Remoting et permettent de résoudre les problèmes et de surveiller les performances.


## <a name="performance-counters"></a>Compteurs de performances
Le runtime Reliable Service Remoting définit les catégories suivantes de compteur de performances :

| Catégorie | Description |
| --- | --- |
| Service Fabric Service |Compteurs spécifiques à Azure Service Fabric Service Remoting, par exemple, temps moyen nécessaire pour traiter la demande |
| Méthode de service Service Fabric |Compteurs spécifiques des méthodes implémentées par Service Fabric Remoting Service. Par exemple, la fréquence à laquelle une méthode de service est appelée |

Chacune des catégories précédentes possède un ou plusieurs compteurs.

L'application [Analyseur de performances Windows](https://technet.microsoft.com/library/cc749249.aspx) , disponible par défaut dans le système d'exploitation Windows, peut être utilisée pour collecter et afficher les données de compteur de performances. [Diagnostics Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) est une autre option pour collecter les données de compteur de performances et les télécharger dans les tables Azure.

### <a name="performance-counter-instance-names"></a>Noms d'instance de compteur de performances
Un cluster avec un grand nombre de services ou de partitions Service Remoting dispose d'un grand nombre d'instances de compteur de performances. Les noms d'instance de compteur de performances peuvent aider à identifier la partition et la méthode Service (le cas échéant) spécifiques associées à l'instance de compteur de performances.

#### <a name="service-fabric-service-category"></a>Catégorie de service Fabric Service
Pour la catégorie `Service Fabric Service`, les noms d'instance de compteur ont le format suivant :

`ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*ServiceFabricPartitionID* est la représentation sous forme de chaîne de l'ID de partition Service Fabric associée à l'instance de compteur de performances. L'ID de partition est un GUID et sa représentation sous forme de chaîne est générée à l'aide de la méthode [`Guid.ToString`](https://msdn.microsoft.com/library/97af8hh4.aspx) avec le spécificateur de format « D ».

*ServiceReplicaOrInstanceId* est la représentation sous forme de chaîne de l'ID du réplica/de l’instance Service Fabric associé(e) à l'instance de compteur de performances.

*ServiceRuntimeInternalID* est la représentation sous forme de chaîne d'un entier 64 bits généré par le runtime Fabric Service pour son usage interne. Il est inclus dans le nom de l'instance de compteur de performances pour garantir l'unicité et éviter tout conflit avec d'autres noms d'instance de compteur de performances. Les utilisateurs ne doivent pas tenter d'interpréter cette partie du nom de l'instance de compteur de performances.

Voici un exemple de nom d'instance de compteur pour un compteur appartenant à la catégorie `Service Fabric Service` :

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046_5008379932`

Dans l'exemple précédent, `2740af29-78aa-44bc-a20b-7e60fb783264` est la représentation sous forme de chaîne de l'ID de partition Service Fabric, `635650083799324046` est la représentation sous forme de chaîne de l'ID du réplica/de l’instance, et `5008379932` est l’ID 64 bits généré pour l'usage interne du runtime.

#### <a name="service-fabric-service-method-category"></a>Catégorie de méthode de service Service Fabric
Pour la catégorie `Service Fabric Service Method`, les noms d'instance de compteur ont le format suivant :

`MethodName_ServiceRuntimeMethodId_ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*MethodName* est le nom de la méthode de service associée à l'instance de compteur de performances. Le format du nom de méthode est déterminé selon une logique du runtime Fabric Service qui équilibre la lisibilité du nom avec des contraintes sur la longueur maximale des noms d'instance de compteur de performances sous Windows.

*ServiceRuntimeMethodId* est la représentation sous forme de chaîne d'un entier 32 bits généré par le runtime Fabric Service pour son usage interne. Il est inclus dans le nom de l'instance de compteur de performances pour garantir l'unicité et éviter tout conflit avec d'autres noms d'instance de compteur de performances. Les utilisateurs ne doivent pas tenter d'interpréter cette partie du nom de l'instance de compteur de performances.

*ServiceFabricPartitionID* est la représentation sous forme de chaîne de l'ID de partition Service Fabric associée à l'instance de compteur de performances. L'ID de partition est un GUID et sa représentation sous forme de chaîne est générée à l'aide de la méthode [`Guid.ToString`](https://msdn.microsoft.com/library/97af8hh4.aspx) avec le spécificateur de format « D ».

*ServiceReplicaOrInstanceId* est la représentation sous forme de chaîne de l'ID du réplica/de l’instance Service Fabric associé(e) à l'instance de compteur de performances.

*ServiceRuntimeInternalID* est la représentation sous forme de chaîne d'un entier 64 bits généré par le runtime Fabric Service pour son usage interne. Il est inclus dans le nom de l'instance de compteur de performances pour garantir l'unicité et éviter tout conflit avec d'autres noms d'instance de compteur de performances. Les utilisateurs ne doivent pas tenter d'interpréter cette partie du nom de l'instance de compteur de performances.

Voici un exemple de nom d'instance de compteur pour un compteur appartenant à la catégorie `Service Fabric Service Method` :

`ivoicemailboxservice.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486_5008380`

Dans l'exemple précédent, `ivoicemailboxservice.leavemessageasync` est le nom de la méthode, `2` est l'ID 32 bits généré pour l'usage interne du runtime, `89383d32-e57e-4a9b-a6ad-57c6792aa521` est la représentation sous forme de chaîne de l'ID de partition Service Fabric, `635650083804480486` est la représentation sous forme de chaîne de l'ID du réplica/de l’instance Service Fabric, et `5008380` est l'ID 64 bits généré pour l'usage interne du runtime.

## <a name="list-of-performance-counters"></a>Liste des compteurs de performances
### <a name="service-method-performance-counters"></a>Compteurs de performances de la méthode Service

Le runtime Reliable Service publie les compteurs de performances suivants liés à l'exécution des méthodes de service.

| Nom de la catégorie | Nom du compteur | Description |
| --- | --- | --- |
| Méthode de service Service Fabric |Appels/s |Nombre de fois où la méthode de service est appelée par seconde |
| Méthode de service Service Fabric |Moyenne en millisecondes par appel |Durée d'exécution de la méthode de service en millisecondes |
| Méthode de service Service Fabric |Exceptions levées/s |Nombre de fois où la méthode de service lève une exception par seconde |

### <a name="service-request-processing-performance-counters"></a>Compteurs de performances de traitement de la requête de service
Lorsqu'un client appelle une méthode via un objet proxy de service, un message de requête est envoyé via le réseau au service à distance. Le service traite le message de requête et renvoie une réponse au client. Le runtime Reliable Service Remoting publie les compteurs de performances suivants liés au traitement de la requête de service.

| Nom de la catégorie | Nom du compteur | Description |
| --- | --- | --- |
| Service Fabric Service |Nombre de requêtes en attente |Nombre de requêtes en cours de traitement dans le service |
| Service Fabric Service |Moyenne en millisecondes par requête |Durée (en millisecondes) nécessaire au service pour traiter une requête |
| Service Fabric Service |Moyenne en millisecondes pour la désérialisation de la requête |Durée (en millisecondes) nécessaire pour désérialiser le message de requête de service lorsqu'il est reçu au niveau du service |
| Service Fabric Service |Moyenne en millisecondes pour la sérialisation de la réponse |Durée (en millisecondes) nécessaire pour sérialiser le message de réponse de service au niveau du service avant l’envoi de la réponse au client |

## <a name="next-steps"></a>Étapes suivantes
* [Exemple de code](https://github.com/Azure/servicefabric-samples)
* [Fournisseurs EventSource dans PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
