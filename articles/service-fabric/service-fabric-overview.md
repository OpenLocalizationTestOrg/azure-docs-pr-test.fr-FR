---
title: "aaaOverview de l’infrastructure de Service sur Azure | Documents Microsoft"
description: "Vue d’ensemble de l’infrastructure de Service, où les applications sont composées de nombreux microservices tooprovide échelle et résilience. Service Fabric est une plateforme de systèmes distribués utilisé toobuild évolutive, fiable et facile à gérer les applications de cloud de hello."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: masnider
ms.assetid: bbcc652a-a790-4bc4-926b-e8cd966587c0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: mfussell
ms.openlocfilehash: 427fcedf97e6b2aae42d240c63e9f85daed8d962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-service-fabric"></a>Vue d’ensemble d’Azure Service Fabric
Azure Service Fabric est une plateforme de systèmes distribués qui rend facile toopackage, déployer et gérer des conteneurs et microservices fiables et évolutives. Service Fabric résout également des défis de hello dans le développement et la gestion des applications natives de cloud. Les développeurs et administrateurs sont en mesure d’éviter les problèmes d’infrastructure complexes et peuvent se concentrer sur l’implémentation de charges de travail stratégiques et exigeantes, évolutives, fiables et faciles à gérer. L’infrastructure de service représente la plateforme de nouvelle génération hello pour la création et la gestion de ces entreprises, niveau 1, des applications de cloud à l’échelle en cours d’exécution dans des conteneurs.

Cette courte vidéo présente Service Fabric et les microservices : <center><a target="_blank" href="https://aka.ms/servicefabricvideo">  
<img src="./media/service-fabric-overview/OverviewVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="applications-composed-of-microservices"></a>Applications composées de microservices 
L’infrastructure de service vous permet de toobuild et gérer des applications fiables et évolutives composées de microservices que sur un pool de machines, exécutez à haute densité, qui est également appelée tooas un cluster. Il fournit un toobuild runtime léger et sophistiquées distribuée, évolutive, et sans état microservices en cours d’exécution dans des conteneurs. Il fournit également des tooprovision de fonctionnalités de gestion application complète, déployer, surveiller, mise à niveau/patch et supprimer des applications déployées, y compris des services.

Service Fabric alimente de nombreux services Microsoft aujourd’hui, notamment Azure SQL Database, Azure Cosmos DB, Cortana, Microsoft Power BI, Microsoft Intune, Azure Event Hubs, Azure IoT Hub, Dynamics 365, Skype Entreprise et de nombreux services Azure principaux.

Service Fabric est spécialement conçues toocreate natif services de cloud computing peuvent commencer petit, en fonction des besoins et augmenter l’échelle toomassive avec des centaines, voire des milliers d’ordinateurs.

Actuellement, les services Internet sont composés de microservices. Les microservices sont, par exemple, les passerelles de protocole, les profils utilisateur, les paniers d’achat, le traitement des stocks, les files d’attente et les caches. Service Fabric est une plateforme de microservices qui attribue à chaque microservice (ou conteneur) un nom unique pouvant être avec ou sans état.

Service Fabric fournit complète runtime et cycle de vie de gestion des fonctionnalités tooapplications qui sont composées de ces microservices. Il héberge microservices à l’intérieur des conteneurs qui sont déployés et activés sur le cluster Service Fabric de hello. Un déplacement de machines virtuelles toocontainers rend possible une augmentation de l’ordre de grandeur densité. De même, un autre ordre de grandeur dans densité devient possible lorsque vous déplacez de toomicroservices de conteneurs dans ces conteneurs. Par exemple, un cluster unique pour Azure SQL Database comprend des centaines d’ordinateurs exécutant des dizaines de milliers de conteneurs qui hébergent au total des centaines de milliers de bases de données. Chaque base de données est un microservice Service Fabric avec état. 

Pour plus d’informations sur l’approche de microservices hello, lisez [pourquoi une microservices approche toobuilding d’applications ?](service-fabric-overview-microservices.md)

## <a name="container-deployment-and-orchestration"></a>Orchestration et le déploiement de conteneurs
Service Fabric est [l’orchestrateur de conteneurs](service-fabric-cluster-resource-manager-introduction.md) de Microsoft permettant de déployer des microservices sur un cluster de machines. Microservices peuvent être développés dans nombreuses façons d’utiliser hello [Service Fabric, modèles de programmation](service-fabric-choose-framework.md), [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md), toodeploying [tout code de votre choix](service-fabric-deploy-existing-app.md). Important, vous pouvez combiner les services dans les processus et services dans des conteneurs hello même application. Si vous souhaitez simplement trop[déployer et gérer des conteneurs](service-fabric-containers-overview.md), Service Fabric est une solution idéale en tant qu’un orchestrateur de conteneur.

## <a name="any-os-any-cloud"></a>Tous les systèmes d’exploitation, tous les clouds
Service Fabric peut être exécuté partout. Vous pouvez créer des clusters pour Service Fabric dans de nombreux environnements, notamment Azure ou locaux, sous Windows Server ou sous Linux. Vous pouvez même créer des clusters sur d’autres clouds publics. En outre, l’environnement de développement de hello Bonjour SDK est **identiques** environnement de production toohello, avec aucun émulateur impliqués. En d’autres termes, ce qui s’exécute sur votre cluster de développement local déploie toohello des clusters dans d’autres environnements.

![Plateforme Service Fabric][Image1]

Pour plus d’informations sur la création de clusters sur site, lisez [création d’un cluster sur Windows Server ou Linux](service-fabric-deploy-anywhere.md) ou pour créer un cluster de Azure [via le portail Azure de hello](service-fabric-cluster-creation-via-portal.md).

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Microservices avec et sans état pour Service Fabric
L’infrastructure de service vous permet de toobuild les applications qui se composent de microservices ou des conteneurs. Microservices sans état (par exemple, les passerelles de protocole et les serveurs proxy web) ne conservent pas un état mutable en dehors d’une demande et la réponse du service de hello. Les rôles de travail Azure Cloud Services sont un exemple de service sans état. Microservices avec état (par exemple, les comptes d’utilisateur, bases de données, périphériques, paniers d’achat et les files d’attente) conservent un état mutable, ne faisant pas autorité au-delà de la demande de hello et la réponse. Actuellement, les applications Internet sont constituées d’une combinaison de microservices avec et sans état. 

Une clé différentiation avec Service Fabric est son axées sur la création de services avec état, soit avec hello [des modèles de programmation intégrés ](service-fabric-choose-framework.md) ou avec les services avec état en conteneur. Hello [scénarios d’application](service-fabric-application-scenarios.md) décrivent des scénarios hello où les services avec état sont utilisés.


## <a name="application-lifecycle-management"></a>Gestion du cycle de vie des applications
Service Fabric prend en charge pour le cycle de vie complet hello et l’élément de configuration/CD des applications de cloud, y compris les conteneurs. Ce cycle de vie inclut développement via le déploiement, la gestion quotidienne et la désaffectation de tooeventual de maintenance.

Fonctionnalités de gestion du cycle de vie du service Fabric application permettent aux administrateurs d’application et de tooprovision de flux de travail simple et peu toouse informatique opérateurs, déploiement, le correctif et surveiller des applications. Ces flux de travail intégrés réduire considérablement la charge de hello pour les applications informatiques d’opérateurs tookeep disponibles en permanence.

La plupart des applications sont constituées d’une combinaison de microservices avec et sans état, de conteneurs et d’autres exécutables déployés ensemble. En ayant des types forts sur les applications hello, Service Fabric permet le déploiement de hello de plusieurs instances d’application. Chaque instance est gérée et mise à niveau indépendamment. Plus important encore, Service Fabric peut déployer des conteneurs ou n’importe quel exécutable et les rendre fiables. Par exemple, Service Fabric peut déployer .NET, ASP.NET Core, node.js, des conteneurs Windows, des conteneurs Linux, des machines virtuelles Java, des scripts, Angular ou littéralement n’importe quel élément qui compose votre application.

Service Fabric est intégré avec des outils de CI/CD tels que [Visual Studio Team Services](https://www.visualstudio.com/team-services/), [Jenkins](https://jenkins.io/index.html), et [Octopus Deploy](https://octopus.com/) et peut être utilisé avec n’importe quel autre outil de CI/CD populaire.

Pour plus d’informations sur la gestion du cycle de vie des applications, consultez [Cycle de vie des applications](service-fabric-application-lifecycle.md). Pour plus d’informations sur la façon toodeploy n’importe quel code, consultez [déployer un exécutable invité](service-fabric-deploy-existing-app.md).

## <a name="key-capabilities"></a>Fonctionnalités clés
Service Fabric vous permet d'effectuer les opérations suivantes :

* Déployer des centres de données tooAzure ou tooon locaux qui exécutent Windows ou Linux avec zéro modifications du code. Écrire une seule fois et cluster Service Fabric de tooany déployer n’importe où.
* Développer des applications évolutives qui sont composées de microservices à l’aide de n’importe quel code, les conteneurs ou les modèles de programmation de Service Fabric hello.
* Développer des microservices avec et sans état très fiables. Simplifier hello la conception de votre application à l’aide de microservices avec état. 
* Utilisez hello novel Reliable Actors modèle toocreate cloud objets de programmation avec état et le code autonomes.
* Déployer et orchestrer les conteneurs incluant des conteneurs Windows et Linux. Service Fabric est un orchestrateur de conteneurs avec état capable d’analyser et d’indexer automatiquement les données.
* Déployer des applications en quelques secondes, à haute densité et avec des centaines, voire des milliers d’applications ou de conteneurs par machine.
* Déployer différentes versions de la même application côte à côte et mettre à niveau de chaque application indépendamment de hello.
* Gérer le cycle de vie de hello de vos applications sans interruption de service, y compris les mises à niveau avec rupture et sans rupture.
* Montée en puissance parallèle ou mettre à l’échelle de nombre hello de nœuds dans un cluster. Lorsque vous mettez vos nœuds à l’échelle, vos applications sont automatiquement mises à l’échelle.
* Surveiller et diagnostiquer la santé de vos applications hello et définir des stratégies pour effectuer des réparations automatiques.
* Regardez équilibrage des ressources hello orchestrer redistribution hello des applications sur le cluster de hello. Service Fabric récupère les échecs et optimise distribution hello de charge en fonction des ressources disponibles.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Étapes suivantes
* Pour plus d'informations :
  * [Pourquoi un microservices approche toobuilding applications ?](service-fabric-overview-microservices.md)
  * [Vue d'ensemble de la terminologie](service-fabric-technical-overview.md)
* Configuration de votre [environnement de développement](service-fabric-get-started.md)  
* En savoir plus sur les [options de prise en charge de Service Fabric](service-fabric-support.md)

[Image1]: media/service-fabric-overview/Service-Fabric-Overview.png
