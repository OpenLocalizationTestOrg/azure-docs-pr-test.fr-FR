---
title: "étapes de création de projet l’ensemble fibre optique aaaService suivants | Documents Microsoft"
description: "Cet article contient des liens les ensemble de tooa principales tâches de développement pour Service Fabric"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a>Votre application Service Fabric et étapes suivantes
Votre application Azure Service Fabric a été créée. Cet article décrit la composition hello de votre projet et quelques astuces potentiels.

## <a name="your-application"></a>Votre application.
Chaque nouvelle application inclut un projet d'application. Il peut y avoir un ou deux projets supplémentaires, en fonction de type hello du service choisi.

### <a name="hello-application-project"></a>projet d’application Hello
projet d’application Hello comprend :

* Un ensemble de services de toohello de références qui composent votre application.
* Trois profils (1-nœud Local, 5 nœuds locaux et Cloud) que vous pouvez utiliser pour travailler avec différents environnements--comme point de terminaison de préférences tooa connexes cluster et si tooperform mise à niveau des déploiements par défaut, les préférences de toomaintain de publication.
* Fichiers de paramètres application trois (identique à ci-dessus) que vous pouvez utiliser des configurations d’application spécifique à un environnement toomaintain, telles que nombre de hello de toocreate de partitions pour un service.
* Un script de déploiement que vous pouvez utiliser toodeploy votre application à partir de la ligne de commande hello ou en tant que partie d’un pipeline d’intégration et de déploiement continu automatisé.
* manifeste d’application Hello, qui décrit l’application hello. Vous pouvez trouver hello manifeste sous le dossier de ApplicationPackageRoot hello.

### <a name="stateless-service"></a>Service sans état
Lorsque vous ajoutez un nouveau service sans état, Visual Studio ajoute une solution de tooyour de projet de service qui inclut un type issu de `StatelessService`. service de Hello incrémente une variable locale dans un compteur.

### <a name="stateful-service"></a>Service avec état
Lorsque vous ajoutez un nouveau service avec état, Visual Studio ajoute une solution de tooyour de projet de service qui inclut un type issu de `StatefulService`. Hello service incrémente un compteur dans son `RunAsync` (méthode) et stocke le résultat de hello dans un `ReliableDictionary`.

### <a name="actor-service"></a>Service d’acteur
Lorsque vous ajoutez un nouveau acteur fiable, Visual Studio ajoute la solution de tooyour deux projets : un projet de l’acteur et un projet d’interface.

projet d’acteur Hello fournit des méthodes pour le paramètre et l’obtention de valeur hello d’un compteur qui est rendue persistante fiable au sein de l’état de hello acteur. Hello projet d’interface fournit une interface que les autres services peut utiliser l’acteur de hello tooinvoke.

### <a name="stateless-web-api"></a>API web sans état
projet d’API Web sans état Hello fournit un de base que vous pouvez utiliser tooopen clients tooexternal de votre application de service web. Pour plus d’informations sur la structure de projet de hello, consultez [services API Web du Service Fabric avec OWIN auto-hébergement](service-fabric-reliable-services-communication-webapi.md).


### <a name="aspnet-core"></a>ASP.NET Core
Hello Service Fabric SDK fournit hello même jeu de modèles ASP.NET Core qui sont disponibles pour la version autonome des projets ASP.NET Core : vide, [API Web][aspnet-webapi], et [l’Application Web][aspnet-webapp].

### <a name="guest-executables-and-guest-containers"></a>Exécutables invités et conteneurs d’invités

Un Service Fabric 'invité' est un service qui n’est pas généré avec les modèles de programmation de la plate-forme hello. Vous pouvez empaqueter les fichiers binaires de hello pour un invité soit [directement dans le package d’application hello](service-fabric-deploy-existing-app.md) ou [via une image de conteneur](service-fabric-deploy-container.md). Dans les deux cas, Visual Studio crée hello artefacts nécessaires Bonjour **ApplicationPackageRoot** dossier du projet d’application hello. Visual Studio ne crée pas un nouveau projet de service, car le code hello existe déjà un autre emplacement. Si vous souhaitez que toomanage votre invité projets en même temps que le projet d’application Service Fabric hello, vous pouvez les ajouter toohello même solution Visual Studio.

## <a name="next-steps"></a>Étapes suivantes
### <a name="create-an-azure-cluster"></a>Création d’un cluster Azure
Hello Service Fabric SDK fournit un cluster local pour le développement et de test. toocreate un cluster dans Azure, consultez [configuration d’un cluster Service Fabric à partir de hello portail Azure][create-cluster-in-portal].

### <a name="publish-your-application-tooazure"></a>Publier votre application tooAzure
Vous pouvez publier votre application directement à partir de Visual Studio tooan cluster Azure. toolearn, voir [tooAzure de votre application de publication][publish-app-to-azure].

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a>Utiliser Service Fabric Explorer toovisualize votre cluster
Service Fabric Explorer offre un moyen simple de toovisualize votre cluster, y compris les applications déployées et la disposition physique. toolearn, voir [visualiser votre cluster à l’aide du Service Fabric Explorer][visualize-with-sfx].

### <a name="version-and-upgrade-your-services"></a>Contrôle de la version et mise à niveau de vos services
Service Fabric permet une gestion de version indépendante et la mise à niveau de services indépendants dans une application. toolearn, voir [le contrôle de version et la mise à niveau vos services][app-upgrade-tutorial].

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a>Configuration de l’intégration continue avec Visual Studio Team Services
toolearn comment vous pouvez configurer un processus d’intégration continue pour votre application de Service Fabric, consultez [configurer l’intégration continue avec Visual Studio Team Services][ci-with-vso].

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
