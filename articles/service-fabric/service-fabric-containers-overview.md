---
title: "aaaOverview de l’infrastructure de Service et de conteneurs | Documents Microsoft"
description: "Une vue d’ensemble de l’infrastructure de Service et hello utiliser des applications de conteneurs toodeploy microservice. Cet article fournit un aperçu de comment les conteneurs peuvent être utilisés et hello des fonctionnalités disponibles dans l’infrastructure de Service."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: c98b3fcb-c992-4dd9-b67d-2598a9bf8aab
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: fce94c4b476351c90f23f706aab8bc17319cce22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-and-containers"></a>Service Fabric et conteneurs
> [!NOTE]
> Cette fonctionnalité est en préversion pour Linux.  Déploiement de cluster du Service Fabric tooa dans Windows 10 n’est pas prise en charge des conteneurs encore (prochainement). 
>   

## <a name="introduction"></a>Introduction
Azure Service Fabric est un [orchestrateur](service-fabric-cluster-resource-manager-introduction.md) de services sur un cluster de machines. Il profite des nombreuses années d’expérience de Microsoft en matière d’utilisation et d’optimisation de services à très grande échelle. Les services peuvent être développés de nombreuses façons, à l’aide de hello [Service Fabric, modèles de programmation](service-fabric-choose-framework.md) toodeploying [invité exécutables](service-fabric-deploy-existing-app.md). Par défaut, Service Fabric déploie et active ces services en tant que processus. Processus fournissent l’activation de la plus rapide de hello et utilisation de densité la plus élevée des ressources hello dans un cluster. Service Fabric peut également déployer des services dans les images de conteneur. Important, vous pouvez combiner des services dans les processus et services dans des conteneurs hello même application. 

## <a name="containers-and-service-fabric-roadmap"></a>Feuille de route des conteneurs et de Service Fabric
Dans les versions à venir, de nombreuses améliorations sont planifiées concernant l’orchestration des conteneurs avec Service Fabric. Les améliorations comprennent des fonctionnalités pour une meilleure mise en réseau avec la prise en charge des réseaux virtuels au sein d’une application, des fonctionnalités de sécurité, des diagnostics améliorés et une prise en charge des outils. L’infrastructure de service vous permet d’applications toocreate mélange des conteneurs empaquetés avec le code existant (par exemple, les applications IIS MVC) avec les services développés à l’aide de modèles de programmation de Service Fabric hello.  Vous pouvez exécuter plusieurs de ces applications sur un seul cluster. 

## <a name="what-are-containers"></a>Qu’est-ce qu’un conteneur ?
Les conteneurs sont encapsulées, déployables individuellement composants qui s’exécutent en tant qu’instances isolées sur hello même avantage tootake de noyau de virtualisation qui fournit d’un système d’exploitation. Par conséquent, chaque application et ses bibliothèques runtime, les dépendances et système exécutent à l’intérieur d’un conteneur en mode du conteneur isolé toohello un accès privé complet de constructions de système d’exploitation. En même temps que la portabilité, ce degré d’isolement des ressources et de sécurité est principal avantage de hello pour l’utilisation de conteneurs avec l’infrastructure de Service, qui exécute les services dans le processus.

Les conteneurs sont une technologie de virtualisation qui virtualise hello le système d’exploitation sous-jacent à partir d’applications. Conteneurs de fournissent un environnement immuable toorun d’applications avec différents degrés d’isolation. Les conteneurs s’exécutent directement sur le noyau de hello et ont une vue isolée hello du système de fichiers et d’autres ressources. Ordinateurs comparés toovirtual, conteneurs ont hello suivant avantages :

* **Petite**: conteneurs utilisent un seul espace et la couche de versions et mises à jour tooincrease l’efficacité du stockage.
* **Fast**: conteneurs n’ont pas tooboot un système d’exploitation, afin qu’ils peuvent démarrer beaucoup plus rapidement, généralement en secondes.
* **Portabilité**: une image d’application en conteneur peut être porté toorun dans le cloud hello, en local, dans les machines virtuelles, ou directement sur les ordinateurs physiques.
* **Gouvernance des ressources**: un conteneur peut limiter les ressources physiques hello qu’elle peut consommer sur son ordinateur hôte.

## <a name="container-types"></a>Types de conteneur
L’infrastructure de service prend en charge les conteneurs Linux et Windows et prend également en charge le mode d’isolation Hyper-V sur hello ce dernier. 

### <a name="docker-containers-on-linux"></a>Conteneurs Docker sur Linux
Docker fournit les principales API toocreate et gérer des conteneurs sur les conteneurs de noyau Linux. Hub d’ancrage est un référentiel central de toostore et récupérer des images de conteneur.
Pour obtenir un didacticiel, consultez [déployer un tooService de conteneur Docker Fabric](service-fabric-get-started-containers-linux.md).

### <a name="windows-server-containers"></a>Conteneurs Windows Server
Windows Server 2016 fournit deux types de conteneurs qui diffèrent au niveau de hello d’isolation fourni. Conteneurs Windows Server et Docker sont similaires, car les deux ont l’espace de noms et le fichier d’isolation mais partage hello noyau du système avec l’hôte hello sur que s’exécutent. Sur Linux, cette isolation est généralement fournie par `cgroups` et `namespaces`. Les conteneurs Windows Server se comportent de la même manière.

Conteneurs Windows Hyper-V fournissent plus d’isolation et la sécurité, car chaque conteneur ne partage pas le noyau du système d’exploitation hello avec d’autres conteneurs ou avec l’hôte de hello. Grâce à ce niveau élevé d’isolation à des fins de sécurité, les conteneurs Hyper-V ciblent les scénarios de multilocation hostiles.
Pour obtenir un didacticiel, consultez [déployer un tooService de conteneur Windows Fabric](service-fabric-get-started-containers.md).

Hello figure ci-dessous montre hello différents types de virtualisation et niveaux d’isolement disponibles dans le système d’exploitation de hello.
![Plateforme Service Fabric][Image1]

## <a name="scenarios-for-using-containers"></a>Scénarios d’utilisation des conteneurs
Voici des exemples pour lesquels le conteneur est un bon choix :

* **IIS de courbes d’élévation et MAJ**: Si vous disposez [ASP.NET MVC](https://www.asp.net/mvc) applications que vous souhaitez toocontinue toouse, placez-les dans un conteneur au lieu de les faire migrer tooASP.NET Core. Ces applications ASP.NET MVC dépendent des services Internet (IIS, Internet Information Services). Vous pouvez empaqueter ces applications dans les images de conteneur à partir de hello précréés image IIS et les déployer avec Service Fabric. Consultez [Images de conteneur sur Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/quick_start/quick_start_images) pour savoir comment les images toocreate IIS.
* **Mélange de conteneurs et de microservices Service Fabric** : utilisez une image de conteneur existante pour une partie de votre application. Par exemple, vous pouvez utiliser hello [conteneur NGINX](https://hub.docker.com/_/nginx/) hello web frontal de vos applications et services avec état pour hello plus intensif principal calcul.
* **Réduire l’impact des services de « voisin bruyant »**: vous pouvez utiliser la possibilité de gouvernance des ressources hello des ressources de hello toorestrict conteneurs utilisé par un service sur un ordinateur hôte. Si les services peuvent consommer beaucoup de ressources et affecter les performances de hello d’autres (par exemple, une opération longue et de requête similaire), envisagez de placer ces services dans les conteneurs qui ont la gouvernance des ressources.

## <a name="service-fabric-support-for-containers"></a>Prise en charge des conteneurs par Service Fabric
Actuellement, Service Fabric prend en charge le déploiement de conteneurs Docker sur Linux et de conteneurs Windows Server sur Windows Server 2016. Il prend également en charge le mode d’isolation Hyper-V. 

Bonjour Service Fabric [modèle d’application](service-fabric-application-model.md), un conteneur représente un hôte d’application dans le service de plusieurs réplicas sont placés. Service Fabric peut exécuter n’importe quel conteneur, et scénario de hello est similaire toohello [scénario d’exécutable invité](service-fabric-deploy-existing-app.md), où vous empaquetez une application existante à l’intérieur d’un conteneur. Ce scénario est hello-cas d’usage courant pour les conteneurs, et exécution d’une application écrite à l’aide de n’importe quel langage ou des infrastructures, mais ne pas à l’aide de modèles de programmation de l’infrastructure de Service intégrés hello sont des exemples.

En outre, vous pouvez également exécuter des services Service Fabric à l’intérieur de conteneurs. Prise en charge pour les services de l’infrastructure de Service en cours d’exécution à l’intérieur des conteneurs est limité actuellement, mais toobe améliorée dans les versions à venir.

* **Les services sans état fiables dans des conteneurs**: services fiable sans état à l’aide des Services fiables hello modèles de programmation sont uniquement pris en charge sous Linux. La prise en charge des services sans état dans les conteneurs Windows est planifiée pour une version à venir.
* **Les services avec état dans des conteneurs**: ces services utilisent hello Reliable Actors ou des Services fiables modèle de programmation. La prise en charge de l’exécution des services avec état dans les conteneurs sera ajoutée dans une version à venir.

Service Fabric dispose de plusieurs fonctionnalités de gestion des conteneurs, qui vous aident à créer des applications composées de microservices mis en conteneur. Service Fabric offre hello suivant de fonctionnalités pour les services en conteneur :

* Activation et déploiement d’images de conteneur
* Gouvernance des ressources.
* Authentification de référentiels.
* Mappage de port toohost port du conteneur.
* Découverte et communication entre des conteneurs.
* Capacité tooconfigure et définir des variables d’environnement.

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris ce qu’était un conteneur. Vous savez désormais que Service Fabric est un orchestrateur de conteneurs et qu’il fournit des fonctionnalités de prise en charge des conteneurs. Comme prochaine étape, nous passe en revue quelques exemples d’hello fonctionnalités tooshow vous comment toouse les.

[Déployer un tooService de conteneur Windows Fabric sur Windows Server 2016](service-fabric-get-started-containers.md)

[Déployer un tooService de conteneur Docker Fabric sur Linux](service-fabric-get-started-containers-linux.md)

[Image1]: media/service-fabric-containers/Service-Fabric-Types-of-Isolation.png
