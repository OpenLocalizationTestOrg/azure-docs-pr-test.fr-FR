---
title: aaaDifferences entre les Services de cloud computing et le Service Fabric | Documents Microsoft
description: "Une vue d’ensemble conceptuelle pour la migration d’applications à partir des Services de cloud computing tooService l’ensemble fibre optique."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 0b87b1d3-88ad-4658-a465-9f05a3376dee
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: bbc5ef4fe0fe1b0da55454cb6b766925030198fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-hello-differences-between-cloud-services-and-service-fabric-before-migrating-applications"></a>En savoir plus sur les différences de hello entre les Services de cloud computing et le Service Fabric avant de migrer les applications.
Microsoft Azure Service Fabric est la plate-forme d’application hello cloud de nouvelle génération pour les applications distribuées hautement évolutives et hautement fiables. Elle introduit de nombreuses nouvelles fonctionnalités d’empaquetage, de déploiement, de mise à niveau et de gestion des applications cloud distribuées. 

Il s’agit d’une application de toomigrating guide Introduction à partir des Services de cloud computing tooService l’ensemble fibre optique. Il se concentre essentiellement sur les différences d’architecture et de conception entre les services cloud et Service Fabric.

## <a name="applications-and-infrastructure"></a>Applications et infrastructure
Une différence fondamentale entre les Services de cloud computing et le Service Fabric est relation hello entre les machines virtuelles, les charges de travail et applications. Une charge de travail est défini en tant que code hello écrire tooperform une tâche spécifique ou de fournir un service.

* **Les services cloud visent à déployer des applications en tant que machines virtuelles.** code Hello que vous écrivez est l’instance de machine virtuelle tooa étroitement couplées, tel qu’un Web ou d’un rôle de travail. toodeploy une charge de travail dans les Services de cloud computing est toodeploy un ou plusieurs ordinateurs virtuels instances cette charge de travail d’exécution hello. Il n’existe pas de séparation entre les applications et les machines virtuelles, et par conséquent, les applications ne sont pas associées à une définition formelle. Une application peut être considérée comme un ensemble d’instances de rôle web ou de travail au sein d’un déploiement de services cloud ou comme un déploiement complet de services cloud. Dans cet exemple, une application est représentée comme un ensemble d’instances de rôle.

![Topologie et applications de service cloud][1]

* **Service Fabric est sur le déploiement applications tooexisting machines virtuelles ou des ordinateurs exécutant le Service Fabric sur Windows ou Linux.** services Hello que vous écrivez sont complètement dissociées de hello sous-jacent d’infrastructure, qui est abstrait par la plate-forme d’application hello Service Fabric, pour une application peut être déployée toomultiple environnements. Une charge de travail dans l’infrastructure de Service est appelé un « service », et un ou plusieurs services sont regroupées dans une application formellement défini qui s’exécute sur la plate-forme d’application Service Fabric hello. Plusieurs applications peuvent être déployé tooa les cluster Service Fabric unique.

![Topologie et applications Service Fabric][2]

Service Fabric correspond à une couche de plateforme d’application qui s’exécute sur Windows ou Linux, alors que les services cloud constituent un système de déploiement de machines virtuelles gérées par Azure avec des charges de travail jointes.
modèle d’application Service Fabric Hello présente plusieurs avantages :

* Temps de déploiement rapide. La création d’instances de machine virtuelle peut prendre beaucoup de temps. Dans l’infrastructure de Service, les machines virtuelles sont déployées uniquement une fois que tooform un cluster qui héberge hello plate-forme d’application Service Fabric. À ce stade, les packages d’applications peuvent être déployé toohello cluster très rapidement.
* Hébergement de haute densité. Dans les services cloud, une machine virtuelle de rôle de travail héberge une charge de travail. Dans l’infrastructure de Service, les applications sont distinctes de hello machines virtuelles qui s’exécutent, ce qui signifie que vous pouvez déployer un grand nombre d’applications tooa petit nombre de machines virtuelles, qui peuvent réduire les coûts globaux des déploiements plus importants.
* Hello Service Fabric plateforme peut exécuter n’importe où qui comporte des ordinateurs Windows Server ou Linux, qu’il s’agisse de Azure ou localement. plateforme de Hello fournit une couche d’abstraction sur l’infrastructure sous-jacente de hello permettant d’exécuter votre application sur différents environnements. 
* Gestion des applications distribuées. Service Fabric est une plateforme que non seulement les hôtes d’applications distribuées, mais aussi vous aide à gérer leur cycle de vie indépendamment hello hébergeant la machine virtuelle ou du cycle de vie de l’ordinateur.

## <a name="application-architecture"></a>Architecture de l'application
Hello architecture d’une application de Services de cloud computing inclut généralement plusieurs dépendances du service externe, telles que le Bus de Service Table Azure et stockage d’objets Blob, SQL, Redis et d’autres toomanage hello état et les données d’une application et la communication entre serveur Web Rôles de travail et dans un déploiement de Services de cloud computing. Voici un exemple d’application de services cloud complète :  

![Architecture des services cloud][9]

Applications de service Fabric peuvent également choisir toouse hello mêmes services externes dans une application complète. Cet exemple montre l’architecture des Services de Cloud hello la plus simple de migration à partir des Services de cloud computing tooService Fabric est déploiement de Services de cloud computing de hello uniquement tooreplace avec une application de Service Fabric, en conservant hello architecture globale hello identiques. Hello Web et rôles de travail peuvent être tooService porté a généré l’infrastructure des services sans état avec des modifications minimales du code.

![Architecture Service Fabric après une migration simple][10]

À ce stade, le système de hello doit continuer toowork hello même qu’avant. En tirant profit des fonctionnalités avec état de Service Fabric, les magasins d’état externe peuvent être internalisés sous forme de services avec état le cas échéant. Cela est plus complexe qu’une simple migration de rôles Web et Worker tooService sans état services de Fabric, car il nécessite l’écriture des services personnalisés qui fournissent l’application tooyour de fonctionnalités équivalentes des services externes hello comme avant. Hello les avantages suivants : 

* Suppression des dépendances externes 
* Unification de déploiement de hello, la gestion et les modèles de mise à niveau. 

Voici un exemple d’architecture résultant de l’internalisation de ces services :

![Architecture Service Fabric après une migration complète][11]

## <a name="communication-and-workflow"></a>Communication et workflow
La plupart des applications de service cloud sont constituées de plusieurs niveaux. De même, une application Service Fabric se compose de plusieurs services (généralement de nombreux services). La communication directe et la communication via un stockage durable externe constituent deux modèles de communication courants.

### <a name="direct-communication"></a>Communication directe
Avec la communication directe, les niveaux peuvent communiquer directement par le biais du point de terminaison exposé par chacun d’entre eux. Dans les environnements sans état comme Services de cloud computing, cette sélection d’une instance d’un rôle de machine virtuelle, soit au hasard des moyens ou alternée toobalance charge et connexion tooits point de terminaison directement.

![Communication directe des services cloud][5]

 La communication directe est un modèle de communication courant dans Service Fabric. Hello principale différence entre l’infrastructure de Service et les Services de cloud computing est que, dans les Services de cloud computing, vous vous connectez tooa machine virtuelle, tandis que dans l’infrastructure de Service vous connectez tooa service. Cette distinction est importante pour plusieurs raisons :

* Services dans l’infrastructure de Service ne sont pas des machines virtuelles toohello liée qui les hébergent ; Services peut déplacer dans un cluster de hello et en fait, attendu toomove autour pour diverses raisons : ressource d’équilibrage, le basculement, mises à niveau de l’application et l’infrastructure et les contraintes de placement ou de la charge. Cela signifie que l’adresse d’une instance de service peut changer à tout moment. 
* Une machine virtuelle dans Service Fabric peut héberger plusieurs services, chacun avec des points de terminaison uniques.

L’infrastructure de service fournit un mécanisme de découverte de service, appelé hello Service d’affectation de noms, qui peut être utilisé tooresolve les adresses de point de terminaison des services. 

![Communication directe Service Fabric][6]

### <a name="queues"></a>Files d’attente
Un mécanisme de communication commun entre les couches dans les environnements sans état tels que les Services de cloud computing est toouse un toodurably de file d’attente de stockage externe stocker les tâches de travail à partir d’une couche tooanother. Un scénario courant consiste à un niveau web qui envoie des travaux tooan file d’attente Azure ou le Bus de Service où les instances de rôle de travail peuvent dequeue et traiter les travaux hello.

![Communication par file d’attente des services cloud][7]

Hello même modèle de communication peut être utilisé dans l’infrastructure de Service. Cela peut être utile lorsque vous migrez un tooService d’application Services de cloud computing existant l’ensemble fibre optique. 

![Communication directe Service Fabric][8]

## <a name="next-steps"></a>Étapes suivantes
Hello la plus simple de migration à partir de tooService de Services de cloud computing Fabric est tooreplace uniquement hello déploiement des Services de Cloud avec une application de Service Fabric, en conservant hello architecture globale de votre application à peu près hello identiques. Bonjour à l’article suivant fournit un guide toohelp convertir un tooa Web ou rôle de travail de service sans état de l’infrastructure de Service.

* [Migration simple : convertir un tooa Web ou rôle de travail de service sans état du Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md)

<!--Image references-->
[1]: ./media/service-fabric-cloud-services-migration-differences/topology-cloud-services.png
[2]: ./media/service-fabric-cloud-services-migration-differences/topology-service-fabric.png
[5]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-direct.png
[6]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-direct.png
[7]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-queues.png
[8]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-queues.png
[9]: ./media/service-fabric-cloud-services-migration-differences/cloud-services-architecture.png
[10]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-simple.png
[11]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-full.png
