---
title: aaaAzure ServiceFabric diagnostics et surveillance | Documents Microsoft
description: "Cet article décrit les fonctionnalités de surveillance de performances hello dans hello ServiceRemoting fiable de l’infrastructure de Service runtime, tels que les compteurs de performance émis par celui-ci."
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
ms.openlocfilehash: 64db9a890bd59a1326e587d14b89c007b71a9059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-service-remoting"></a>Diagnostics et surveillance des performances pour Reliable Service Remoting
exécution de ServiceRemoting fiable Hello émet [les compteurs de performance](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Ces fournissent des informations sur le fonctionne de hello ServiceRemoting et aider à l’analyse des performances et le dépannage.


## <a name="performance-counters"></a>Compteurs de performances
Hello ServiceRemoting fiable runtime définit hello suivant des catégories de compteurs de performances :

| Catégorie | Description |
| --- | --- |
| Service Fabric Service |Compteurs spécifique tooAzure de communication à distance du Service Service Fabric, par exemple, le temps moyen nécessaire tooprocess demander |
| Méthode de service Service Fabric |Toomethods spécifique de compteurs implémentée par le Service de communication à distance l’ensemble fibre optique, par exemple, la fréquence à laquelle une méthode de service est appelée |

Chaque hello précédant les catégories a un ou plusieurs compteurs.

Hello [Analyseur de performances Windows](https://technet.microsoft.com/library/cc749249.aspx) application qui est disponible par défaut dans le système d’exploitation de Windows hello peut être utilisé toocollect et affichage de données compteur de performance. [Diagnostics Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) est une autre option pour la collecte de données de compteur de performances et de les télécharger tooAzure tables.

### <a name="performance-counter-instance-names"></a>Noms d'instance de compteur de performances
Un cluster avec un grand nombre de services ou de partitions Service Remoting dispose d'un grand nombre d'instances de compteur de performances. instance de compteur de performance Hello noms peuvent vous aider à identifier la partition spécifique de hello et la méthode de Service (le cas échéant) associée à cette instance de compteur de performances hello.

#### <a name="service-fabric-service-category"></a>Catégorie de service Fabric Service
Pour la catégorie de hello `Service Fabric Service`, noms d’instance de compteur de hello sont Bonjour suivant le format :

`ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*ServiceFabricPartitionID* est représentation de chaîne hello Hello ID de partition de Service Fabric qui hello l’instance de compteur de performance est associé. ID de partition Hello est un GUID, et sa représentation sous forme de chaîne est générée via hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) méthode avec le spécificateur de format « D ».

*ServiceReplicaOrInstanceId* est représentation de chaîne hello Hello ID de réplica/Instance Service Fabric hello l’instance de compteur de performance est associé.

*ServiceRuntimeInternalID* est la représentation sous forme de chaîne hello d’un entier 64 bits qui est généré par le runtime du Service de l’ensemble fibre optique hello pour son usage interne. Il est inclus dans l’instance de compteur de performance hello nom tooensure son unicité et éviter les conflits avec les autres noms d’instance des compteurs de performance. Les utilisateurs ne doivent pas essayer toointerpret cette partie du nom instance de compteur de performance hello.

Hello Voici un exemple d’un nom d’instance de compteur pour un compteur qui appartient toohello `Service Fabric Service` catégorie :

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046_5008379932`

Bonjour précédent exemple, `2740af29-78aa-44bc-a20b-7e60fb783264` est la représentation sous forme de chaîne hello d’ID de partition de Service Fabric hello, `635650083799324046` est la représentation sous forme de chaîne de réplica/InstanceId et `5008379932` hello 64 bits ID généré pour interne du runtime de hello à utiliser.

#### <a name="service-fabric-service-method-category"></a>Catégorie de méthode de service Service Fabric
Pour la catégorie de hello `Service Fabric Service Method`, noms d’instance de compteur de hello sont Bonjour suivant le format :

`MethodName_ServiceRuntimeMethodId_ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*MethodName* est le nom de hello de méthode de service hello hello l’instance de compteur de performance est associé. format Hello hello du nom de méthode est déterminée selon une logique dans le runtime Service Fabric hello qui équilibre la lisibilité hello du nom hello avec des contraintes sur la longueur maximale de hello de noms des instances de compteur performance hello sur Windows.

*ServiceRuntimeMethodId* est la représentation sous forme de chaîne hello d’un entier 32 bits qui est généré par le runtime du Service de l’ensemble fibre optique hello pour son usage interne. Il est inclus dans l’instance de compteur de performance hello nom tooensure son unicité et éviter les conflits avec les autres noms d’instance des compteurs de performance. Les utilisateurs ne doivent pas essayer toointerpret cette partie du nom instance de compteur de performance hello.

*ServiceFabricPartitionID* est représentation de chaîne hello Hello ID de partition de Service Fabric qui hello l’instance de compteur de performance est associé. ID de partition Hello est un GUID, et sa représentation sous forme de chaîne est générée via hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) méthode avec le spécificateur de format « D ».

*ServiceReplicaOrInstanceId* est représentation de chaîne hello Hello ID de réplica/Instance Service Fabric hello l’instance de compteur de performance est associé.

*ServiceRuntimeInternalID* est la représentation sous forme de chaîne hello d’un entier 64 bits qui est généré par le runtime du Service de l’ensemble fibre optique hello pour son usage interne. Il est inclus dans l’instance de compteur de performance hello nom tooensure son unicité et éviter les conflits avec les autres noms d’instance des compteurs de performance. Les utilisateurs ne doivent pas essayer toointerpret cette partie du nom instance de compteur de performance hello.

Hello Voici un exemple d’un nom d’instance de compteur pour un compteur qui appartient toohello `Service Fabric Service Method` catégorie :

`ivoicemailboxservice.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486_5008380`

Bonjour précédent exemple, `ivoicemailboxservice.leavemessageasync` est le nom de la méthode hello `2` est hello ID 32 bits généré pour interne du runtime de hello utiliser, `89383d32-e57e-4a9b-a6ad-57c6792aa521` est la représentation sous forme de chaîne hello d’ID de partition de Service Fabric hello,`635650083804480486` est hello chaîne représentation sous forme de hello ID de réplica/Instance Service Fabric et `5008380` est hello 64 bits ID est généré pour interne du runtime de hello utiliser.

## <a name="list-of-performance-counters"></a>Liste des compteurs de performances
### <a name="service-method-performance-counters"></a>Compteurs de performances de la méthode Service

exécution du Service fiable Hello publie hello suivant des compteurs de performances connexes toohello d’exécution des méthodes de service.

| Nom de la catégorie | Nom du compteur | Description |
| --- | --- | --- |
| Méthode de service Service Fabric |Appels/s |Nombre de fois que la méthode de service hello est appelé par seconde |
| Méthode de service Service Fabric |Moyenne en millisecondes par appel |Durée de la méthode de service tooexecute hello en millisecondes |
| Méthode de service Service Fabric |Exceptions levées/s |Nombre de fois que hello la méthode de service a levé une exception par seconde |

### <a name="service-request-processing-performance-counters"></a>Compteurs de performances de traitement de la requête de service
Lorsqu’un client appelle une méthode via un objet proxy de service, il renvoie un message de demande qui est envoyé sur le service d’accès distant toohello hello réseau. service de Hello traite le message de demande hello et envoie une réponse au client toohello précédent. Hello ServiceRemoting fiable runtime publie hello après le traitement de la demande des compteurs connexes tooservice performances.

| Nom de la catégorie | Nom du compteur | Description |
| --- | --- | --- |
| Service Fabric Service |Nombre de requêtes en attente |Nombre de demandes traitées dans le service hello |
| Service Fabric Service |Moyenne en millisecondes par requête |Durée (en millisecondes) de hello service tooprocess une demande |
| Service Fabric Service |Moyenne en millisecondes pour la désérialisation de la requête |Message de demande de service temps toodeserialize prises (en millisecondes) lorsqu’elle est reçue au niveau de service de hello |
| Service Fabric Service |Moyenne en millisecondes pour la sérialisation de la réponse |Message de réponse temps tooserialize prises (en millisecondes) hello service au service hello avant hello est envoyée toohello client |

## <a name="next-steps"></a>Étapes suivantes
* [Exemple de code](https://github.com/Azure/servicefabric-samples)
* [Fournisseurs EventSource dans PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
