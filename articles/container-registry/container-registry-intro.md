---
title: aaaPrivate registres de conteneur Docker dans Azure | Documents Microsoft
description: "Introduction toohello service de Registre de conteneur Azure, en fournissant des registres Docker privés, gérés sur le cloud."
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: ee2b652b-fb7c-455b-8275-b8d4d08ffeb3
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f6edcf0bf947b7770ee0a4e4a5cfbf4ef8b7392a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooprivate-docker-container-registries"></a>Registres de conteneur Docker introduction tooprivate


Registre de conteneur Azure est managé [Registre de Docker](https://docs.docker.com/registry/) service selon hello 2.0 de Registre Docker open source. Créer et tenir à jour le conteneur Azure registres toostore et gérer votre privé [conteneur Docker](https://www.docker.com/what-docker) images. Utiliser des registres de conteneur dans Azure avec votre développement de conteneur existantes et les pipelines de déploiement et dessiner sur corps hello d’expertise de communauté Docker.

Pour plus d’informations sur Docker et les conteneurs, voir :

* [Guide d'utilisation Docker](https://docs.docker.com/engine/userguide/)




## <a name="use-cases"></a>Cas d'utilisation
Extraire les images à partir d’un conteneur Azure cibles de déploiement toovarious de Registre :

* Des **systèmes d’orchestration évolutifs** qui gèrent des applications en conteneur sur des clusters d’hôtes, y compris du [contrôleur de domaine/système d’exploitation](https://docs.mesosphere.com/), [Docker Swarm](https://docs.docker.com/swarm/) et [Kubernetes](http://kubernetes.io/docs/).
* Des **services Azure** qui prennent en charge la création et l’exécution des applications à grande échelle, y compris [Container Service](../container-service/index.yml), [App Service](/app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/) et d’autres services.

Les développeurs peuvent pousser également tooa Registre de conteneur dans le cadre d’un flux de travail de développement de conteneur. Par exemple, ciblez un registre de conteneur à partir d’un outil de développement et d’intégration continu comme [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) ou [Jenkins](https://jenkins.io/).





## <a name="key-concepts"></a>Concepts clés
* **Registre** : créez au moins un registre de conteneur dans votre abonnement Azure. Chaque registre est soutenu par un Azure standard [compte de stockage](../storage/common/storage-introduction.md) Bonjour même emplacement. Tirer parti du stockage local, fermeture de réseau de vos images de conteneur en créant un Registre Bonjour même emplacement que celui de vos déploiements. Un nom qualifié complet du Registre présente sous forme de hello `myregistry.azurecr.io`.

  Vous [contrôler l’accès](container-registry-authentication.md) tooa Registre de conteneur à l’aide d’une sauvegarde d’Azure Active Directory [principal du service](../active-directory/active-directory-application-objects.md) ou un compte d’administrateur fourni. Exécution hello standard `docker login` tooauthenticate de commande avec un Registre.

* **Registre géré** : niveau qui offre des fonctionnalités supplémentaires pour les registres dans trois références SKU, De base, Standard et Premium. images de Hello dans ces références (SKU) sont stockées dans des comptes de stockage géré par hello service registres du conteneur Azure, ce qui améliore la fiabilité et active de nouvelles fonctionnalités. Ces fonctionnalités comprennent l’intégration des webhooks, l’authentification des référentiels auprès d’Azure Active Directory et la prise en charge de la fonctionnalité de suppression. Les utilisateurs ont toochoose d’option hello entre les registres managés ou toocreate un Registre soutenu par leurs propres comptes de stockage lors de la création de registres.

* **Référentiel** : un registre contient un ou plusieurs référentiels, qui sont des groupes d’images de conteneur. Azure Container Registry prend en charge les espaces de noms de référentiel à plusieurs niveaux. Cette fonctionnalité permet de vous toogroup collections d’application spécifique d’images tooa connexes, ou une collection de développement de toospecific d’applications ou les équipes d’exploitation. Par exemple :

  * `myregistry.azurecr.io/aspnetcore:1.0.1` représente une image de l’entreprise.
  * `myregistry.azurecr.io/warrantydept/dotnet-build`représente une image utilisée toobuild les applications .NET, partagées à travers le service de garantie de hello
  * `myregistry.azrecr.io/warrantydept/customersubmissions/web`représente une image web, regroupée dans une application de soumissions client hello, détenue par le service de garantie de hello

* **Image** : stockée dans un référentiel, chaque image est une capture instantanée en lecture seule d’un conteneur Docker. Les registres de conteneur Azure peuvent inclure des images de Windows et Linux. Vous contrôlez les noms d’images pour tous les déploiements de votre conteneur. Standard d’utilisation [commandes Docker](https://docs.docker.com/engine/reference/commandline/) toopush des images dans un référentiel, ou une image à partir d’un référentiel par extraction de données.

* **Conteneur** : un conteneur définit une application logicielle et ses dépendances encapsulées dans un système de fichiers complet, y compris le code, l’exécution, les outils système et les bibliothèques. Exécutez des conteneurs Docker basés sur des images Windows ou Linux que vous extrayez à partir d’un registre de conteneur. Les conteneurs en cours d’exécution sur un seul ordinateur partagent noyau du système d’exploitation hello. Conteneurs docker sont entièrement portables tooall principales versions de Linux, Mac et Windows.




## <a name="next-steps"></a>Étapes suivantes
* [Créer un Registre de conteneur à l’aide de hello portail Azure](container-registry-get-started-portal.md)
* [Créer un Registre de conteneur à l’aide de hello CLI d’Azure](container-registry-get-started-azure-cli.md)
* [Push de votre première image à l’aide de hello Docker CLI](container-registry-get-started-docker-cli.md)
* toobuild une intégration continue et flux de travail de déploiement à l’aide de Visual Studio Team Services, Service de conteneur Azure et Registre de conteneur Azure, consultez [ce didacticiel](../container-service/dcos-swarm/container-service-docker-swarm-setup-ci-cd.md).
* Si vous souhaitez tooset vos propres Docker privé du Registre dans Azure (sans le point de terminaison public), consultez [déployer votre propre privée Docker Registre sur Azure](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md).
