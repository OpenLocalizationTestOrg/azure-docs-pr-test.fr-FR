---
title: "aaaApplication scénarios et conception | Documents Microsoft"
description: "Vue d'ensemble des catégories d'applications cloud dans Service Fabric. Traite de la conception d’applications à l’aide de services avec ou sans état"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3a8ca6ea-b8e9-4bc3-9e20-262437d2528e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 7/02/2017
ms.author: mfussell
ms.openlocfilehash: e36d5b2d21a6a1e3e85c9b21190072616e4921e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-scenarios"></a>Scénarios d'applications Service Fabric
Azure Service Fabric offre une plateforme fiable et flexible qui vous permet de toowrite et exécutez de nombreux types de services et applications d’entreprise. Ces applications et les microservices peuvent être sans état ou avec état, et sont équilibrée sur les ressources entre les machines virtuelles toomaximize efficacité. l’architecture unique de l’infrastructure de Service Hello vous permet de tooperform près d’analyse en temps réel, le calcul en mémoire, les transactions parallèles et dans vos applications de traitement des événements. Vous pouvez facilement augmenter ou réduire l’échelle de vos applications (vraiment dehors ou dedans), en fonction de vos besoins en ressources.

plateforme de Service Fabric Hello dans Azure est idéal pour hello suivant des catégories d’applications :

* **Services hautement disponibles**: les services Service Fabric assurent un basculement rapide en créant plusieurs réplicas de services secondaires. Si un nœud, un processus ou un service individuel tombe en panne en raison de la défaillance ou toohardware, un des réplicas secondaires de hello est promue tooa le réplica principal avec une perte minimale de service.
* **Des services évolutifs**: les services individuels peuvent être partitionnées, permettant ainsi toobe état monté en charge sur le cluster de hello. En outre, les services individuels peuvent être créés et supprimés volée hello. Services peuvent être rapidement et facilement monté en charge à partir de quelques instances sur quelques toothousands de nœuds d’instances sur un grand nombre de nœuds et évoluer de nouveau, selon vos besoins en ressources. Vous pouvez utiliser l’infrastructure de Service toobuild ces services et gérer leur cycle de vie complet.
* **Calcul sur les données non statique**: l’infrastructure de Service vous permet de toobuild données d’entrée/sortie et applications de calcul intensif avec état. L’infrastructure de service permet de colocalisation hello de traitement (calcul) et les données dans les applications. Normalement, lorsque votre application nécessite un accès toodata, il est une latence réseau associée à un niveau de cache ou le stockage de données externes. Avec Service Fabric avec état, cette latence est éliminée, ce qui permet des lectures et écritures performantes. Imaginez, par exemple, une application qui effectue des sélections de recommandation en temps quasi-réel pour des clients, avec un délai d’aller-retour de moins de 100 millisecondes. caractéristiques de latence et les performances de Hello des services de l’infrastructure de Service (où le calcul de la sélection de la recommandation hello est colocalisé avec les données de salutation et des règles) qui fournit une expérience réactive toohello utilisateur par rapport à l’implémentation standard de hello modèle d’avoir toofetch hello les données nécessaires à partir du stockage à distance.  
* **Applications interactives basées sur les sessions** : Service Fabric est utile si vos applications, telles que les jeux en ligne ou la messagerie instantanée, ont besoin d’effectuer des opérations de lecture et d’écriture avec une faible latence. L’infrastructure de service permet de vous toobuild ces applications avec état interactives sans avoir toocreate un magasin distinct ou le cache, en fonction des besoins pour les applications sans état. (cela augmente la latence et entraîne des problèmes de cohérence).
* **Analytique de données et de flux de travail**: hello rapides lectures et écritures de l’infrastructure de Service des applications qui doivent traiter de manière fiable les événements ou les flux de données. L’infrastructure de service permet également d’applications qui décrivent des pipelines de traitement, où les résultats doivent être fiables et passé sur toohello prochaine étape de traitement sans perte. Ceci s’applique en particulier aux systèmes transactionnels et financiers, qui imposent une garantie de calcul et de cohérence des données.
* **Collecte de données, le traitement et IoT**: étant donné que le Service Fabric gère à grande échelle et a une latence faible via ses services avec état, il est idéal pour le traitement des données sur des millions d’appareils où se trouvent les données hello pour appareil de hello et de calcul de hello colocalisés.
Plusieurs clients ont établi des systèmes IoT avec Service Fabric notamment [BMW](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/24/service-fabric-customer-profile-bmw-technology-corporation/), [Schneider Electric](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/05/service-fabric-customer-profile-schneider-electric/) et [Mesh Systems](https://blogs.msdn.microsoft.com/azureservicefabric/2016/06/20/service-fabric-customer-profile-mesh-systems/).

## <a name="application-design-case-studies"></a>Études de cas de conception d’applications
Un nombre d’études de cas illustrant comment le Service Fabric est utilisé toodesign applications est publié sur hello [blog de l’équipe Service Fabric](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/) et hello [site de solutions microservices](https://azure.microsoft.com/solutions/microservice-applications/).

## <a name="design-applications-composed-of-stateless-and-stateful-microservices"></a>Conception d’applications composées de microservices avec et sans état
La création d’applications avec des rôles de travail Azure Cloud Service est un exemple de service sans état. En revanche, avec état microservices conservent leur état faisant autorité au-delà de la demande de hello et la réponse. Cela fournit une haute disponibilité et la cohérence d’état hello via des API simples qui fournissent des garanties transactionnelles soutenus par la réplication. Les services avec état du service Fabric democratize haute disponibilité, sa mise en tooall des types d’applications, pas seulement les bases de données et les autres banques de données. Il s’agit d’une évolution naturelle. Les applications ont déjà déplacés d’à l’aide de bases de données relationnelles uniquement pour les bases de données haute disponibilité tooNoSQL. Maintenant les applications de hello eux-mêmes peuvent avoir leur état « actif » et les données gérées au sein de celles-ci pour des gains de performances supplémentaires sans sacrifier la fiabilité, la cohérence ou disponibilité.

Lors de la génération d’applications composé de microservices, vous devez en général une combinaison d’applications web sans état (ASP.NET, Node.js, etc.) appel sur les services de couche intermédiaire d’entreprise et sans état, tous déployés dans hello même cluster Service Fabric à l’aide des commandes de déploiement de Service Fabric hello. Tenir compte tooscale, la fiabilité et des ressources d’utilisation, ce qui améliore considérablement la souplesse dans la gestion du cycle de vie de développement et de chacun de ces services dépend.

Avec état microservices simplifier des conceptions d’application, car ils supprimer besoin hello pour les files d’attente supplémentaires hello et caches qui ont été traditionnellement tooaddress requis hello des exigences de disponibilité et la latence des applications purement sans état. Étant donné que les services avec état sont naturellement hautement disponible et faible latence, cela signifie qu’il n’y a moins toomanage déplacement de parties dans votre application dans son ensemble. diagrammes de Hello ci-dessous illustrent les différences de conception d’une application qui est sans état et l’autre qui est avec état hello. En tirant parti de hello [des Services fiables](service-fabric-reliable-services-introduction.md) et [Reliable Actors](service-fabric-reliable-actors-introduction.md) modèles de programmation, les services avec état réduire la complexité des applications tout en assurant un débit élevé et une faible latence.

## <a name="an-application-built-using-stateless-services"></a>Application créée à l'aide de services sans état
![Application utilisant un service sans état][Image1]

## <a name="an-application-built-using-stateful-services"></a>Application créée à l'aide de services avec état
![Application utilisant un service sans état][Image2]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Étapes suivantes

* Écouter trop[études de cas client](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=qDJnf86yC_5206218965
)
* Lire les [études de cas clients](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/)
* En savoir plus sur les [modèles et scénarios](service-fabric-patterns-and-scenarios.md)

* Prise en main la création de services et sans état avec hello Service Fabric [des services fiables](service-fabric-reliable-services-quick-start.md) et [acteurs fiables](service-fabric-reliable-actors-get-started.md) modèles de programmation.
* Voir aussi hello rubriques suivantes :
  * [En savoir plus sur les microservices](service-fabric-overview-microservices.md)
  * [Définition et gestion de l’état du service](service-fabric-concepts-state.md)
  * [Disponibilité des services Service Fabric](service-fabric-availability-services.md)
  * [Mise à l’échelle des applications Service Fabric](service-fabric-concepts-scalability.md)
  * [Partitionnement des services Service Fabric](service-fabric-concepts-partitioning.md)

[Image1]: media/service-fabric-application-scenarios/AppwithStatelessServices.jpg
[Image2]: media/service-fabric-application-scenarios/AppwithStatefulServices.jpg
