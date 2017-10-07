---
title: "aaaLearn la terminologie d’Azure Service Fabric | Documents Microsoft"
description: "Présentation de la terminologie de Service Fabric. Décrit les concepts de la terminologie et des termes utilisés dans le reste de hello de documentation de hello."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: chackdan;subramar
ms.assetid: 3a970679-e19e-43b3-9be8-71773f307c57
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/02/2017
ms.author: ryanwi
ms.openlocfilehash: 4781fc0527b8a58e534183249bc2759aded2730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-terminology-overview"></a>Présentation de la terminologie Service Fabric
Service Fabric est une plateforme de systèmes distribués qui rend facile toopackage, déployer et gérer des microservices fiables et évolutives. Cette rubrique Détails hello la terminologie utilisée par les termes du contrat de Service Fabric toounderstand hello utilisé dans la documentation de hello.

Hello concepts répertoriés dans cette section sont également abordées dans hello suivant vidéos de Microsoft Virtual Academy : <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">concepts fondamentaux</a>, <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965">les concepts de conception</a>, et <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">concepts de l’exécution</a>.

## <a name="infrastructure-concepts"></a>Concepts d’infrastructure
**Cluster**: groupe de machines virtuelles ou physiques connectées au réseau sur lequel vos microservices sont déployés et gérés.  Clusters peuvent évoluer toothousands d’ordinateurs.

**Nœud**: machine ou machine virtuelle faisant partie d’un cluster. Un nom (chaîne) est affecté à chaque nœud. Les nœuds présentent des caractéristiques, telles que des propriétés de placement. Chaque machine ou machine virtuelle a un service Windows à démarrage automatique, `FabricHost.exe`, qui commence à s’exécuter dès le démarrage, puis démarre deux exécutables : `Fabric.exe` et `FabricGateway.exe`. Ces deux exécutables constituent de nœud de hello. Pour les scénarios de test, vous pouvez héberger plusieurs nœuds sur une seule et même machine ou sur une seule et même machine virtuelle en exécutant plusieurs instances de `Fabric.exe` et `FabricGateway.exe`.

## <a name="application-concepts"></a>Concepts d’application
**Type d’application**: hello collection de tooa nom/version affectée au type de service. Défini dans un `ApplicationManifest.xml` file, incorporé dans un répertoire de package d’application, qui est ensuite copié magasin d’images du cluster toohello Service Fabric. Vous pouvez ensuite créer une application nommée à partir de ce type d’application au sein du cluster de hello.

Hello de lecture [modèle d’Application](service-fabric-application-model.md) article pour plus d’informations.

**Package d’application**: un répertoire de disque contenant du type d’application hello `ApplicationManifest.xml` fichier. Références hello packages de service pour chaque type de service qui compose le type d’application hello. fichiers Hello dans le répertoire de package d’application hello sont magasin d’images du cluster de l’ensemble fibre optique tooService copié. Par exemple, un package d’application pour un type d’application de messagerie peut contenir de package de service de file d’attente tooa références, un package de service de serveur frontal et un package de service de base de données.

**Nommé Application**: une fois un package d’application est un magasin d’images toohello copié, vous créez une instance de l’application hello au sein du cluster de hello en spécifiant le type d’application du package d’application hello (à l’aide de son nom/version). Un nom d’URI est affecté à chaque instance de type d’application, qui ressemble à ceci : `"fabric:/MyNamedApp"`. Dans un cluster, vous pouvez créer plusieurs applications nommées à partir d’un seul type d’application. Vous pouvez également en créer à partir de différents types d’application. Chaque application nommée est gérée, et sa version est gérée indépendamment.      

**Type de service**: hello nom/version affectée du service tooa packages de code, les packages de données et les packages de configuration. Défini dans un `ServiceManifest.xml` fichier, incorporé dans un répertoire de package de service et le répertoire du package service hello est ensuite référencé par un package d’application `ApplicationManifest.xml` fichier. Dans un cluster de hello, après avoir créé une application nommée, vous pouvez créer un service nommé parmi hello types de service du type d’application. Hello du type de service `ServiceManifest.xml` fichier décrit le service de hello.

Hello de lecture [modèle d’Application](service-fabric-application-model.md) article pour plus d’informations.

Il existe deux types de service :

* **Sans état :** utiliser un service sans état lorsqu’un état persistant du service hello est stocké dans un service de stockage externes tels que le stockage Azure, base de données SQL Azure ou base de données Azure Cosmos. Utiliser un service sans état lorsque le service de hello n’a pas de stockage persistant. Par exemple, un service de calculatrice où les valeurs sont transmises toohello service, un calcul est effectué à l’aide de ces valeurs et un résultat est retourné.
* **Avec état :** utiliser un service avec état lorsque vous souhaitez que l’infrastructure de Service toomanage état de votre service via ses Collections fiable ou la Reliable Actors modèles de programmation. Spécifiez le nombre de partitions vous souhaitez toospread votre état par (pour une évolutivité) lorsque la création d’un service nommé. Spécifiez également le nombre de fois tooreplicate votre état entre plusieurs nœuds (pour la fiabilité). Chaque service nommé possède un seul réplica principal et plusieurs réplicas secondaires. Vous modifiez l’état de votre service nommé en écrivant le réplica principal de toohello. Service Fabric réplique ensuite ce réplicas secondaires hello tooall état synchronisation votre état. Service Fabric détecte automatiquement un réplica principal échoue et promeut un réplica principal existant de tooa réplica secondaire. Service Fabric crée ensuite un nouveau réplica secondaire.  

**Package de service**: un répertoire de disque contenant le type de hello service `ServiceManifest.xml` fichier. Code de hello, les données statiques et les packages de configuration pour le type de service hello fait référence à ce fichier. fichiers de Hello dans le répertoire du package service hello sont référencés par du type d’application hello `ApplicationManifest.xml` fichier. Par exemple, un package de service peut faire référence toohello code, les données statiques et les packages de configuration qui composent un service de base de données.

**Nommé Service**: après avoir créé une application nommée, vous pouvez créer une instance de l’un de ses types de service de cluster de hello en spécifiant le type de service hello (à l’aide de son nom/version). Chaque instance du type de service reçoit un nom d’URI inclus dans l’étendue de l’URI de son application nommée. Par exemple, si vous créez un « MyDatabase » nommé service au sein d’un « MyNamedApp » nommée application, hello URI ressemble à : `"fabric:/MyNamedApp/MyDatabase"`. Dans une application nommée, vous pouvez créer plusieurs services nommés. Chaque service nommé peut posséder son propre schéma de partition et son propre nombre d’instances/réplicas.

**Package de code**: un répertoire de disque contenant des fichiers exécutables du type de service hello (en général, les fichiers DLL ou EXE). fichiers Hello dans le répertoire de package de code hello sont référencés par type de hello service `ServiceManifest.xml` fichier. Lorsqu’un service nommé est créé, package de code hello est copié toohello nœud ou hello toorun sélectionné de nœuds nommé service. Code de hello puis démarre l’exécution. Il existe deux types d’exécutable de code de package :

* **Les exécutables invité**: fichiers exécutables qui s’exécutent en tant que-se trouve sur un système de d’exploitation hôte hello (Windows ou Linux). Autrement dit, ces fichiers exécutables ne référence pas tooor du lien les fichiers de runtime de n’importe quel Service Fabric et par conséquent, n’utilisent pas les modèles de programmation de Service Fabric. Ces fichiers exécutables sont toouse Impossible de que certaines fonctionnalités de l’infrastructure de Service comme hello naming service pour la découverte de point de terminaison. Exécutables de l’invité ne peut pas rapporter l’instance de service spécifique tooeach charge métriques.
* **Exécutables d’hôte de service**: fichiers exécutables qui utilisent le Service Fabric, modèles de programmation en liant les fichiers exécutables de l’ensemble fibre optique tooService, activer les fonctionnalités de l’infrastructure de Service. Par exemple, une instance de service nommé peut inscrire les points de terminaison avec le service d’affectation de noms de Service Fabric et indiquer les mesures de chargement.      

**Package de données**: un répertoire de disque contenant les fichiers de données statiques en lecture seule de type hello service (généralement une vidéo, audio et les fichiers photo,). fichiers de Hello dans le répertoire du package hello données sont référencés par du type de service hello `ServiceManifest.xml` fichier. Lorsqu’un service nommé est créé, package de données hello est copié toohello nœud ou hello toorun sélectionné de nœuds nommé service.  code de Hello commence à s’exécuter et peut désormais accéder à des fichiers de données hello.

**Package de configuration**: un répertoire de disque contenant les statiques de type hello service, (en général, les fichiers de texte) des fichiers de configuration en lecture seule. les fichiers de Hello dans le répertoire de package de configuration hello sont référencés par type de hello service `ServiceManifest.xml` fichier. Lorsqu’un service nommé est créé, fichiers hello dans le package de configuration hello sont copié toohello une ou plusieurs hello toorun sélectionné de nœuds nommée service. Code de hello commence à s’exécuter, puis peut désormais accéder à des fichiers de configuration hello.

**Conteneurs** : par défaut, Service Fabric déploie et active ces services en tant que processus. Service Fabric peut également déployer des services dans les images de conteneur. Les conteneurs sont une technologie de virtualisation qui virtualise hello le système d’exploitation sous-jacent à partir d’applications. Une application et ses bibliothèques runtime, les dépendances et système exécutent à l’intérieur d’un conteneur avec l’affichage du conteneur isolé toohello un accès privé complet de constructions de système d’exploitation. Service Fabric prend en charge les conteneurs Docker sur Linux et les conteneurs Windows Server.  Pour plus d’informations, consultez [Service Fabric et conteneurs](service-fabric-containers-overview.md).

**Schéma de partition** : lors de la création d’un service nommé, vous indiquez un schéma de partition. Services de grandes quantités de l’état de fractionnement les données de hello sur plusieurs partitions, qui répartit l’état de hello entre les nœuds du cluster hello. Cela permet de tooscale d’état de votre service nommé. Dans une partition, les services nommés sans état ont des instances tandis que les services nommés avec état ont des réplicas. En règle générale, les services nommés sans état ne possèdent qu’une partition, car ils sont dépourvus d’état interne. fournissent des instances de partition Hello pour la disponibilité ; Si une instance échoue, autres continuent toooperate normalement et ensuite le Service Fabric créera une nouvelle instance. Avec état nommé services conservent leur état au sein de réplicas et chaque partition possède son propre jeu de réplicas avec tous les États de hello est synchronisé. Un réplica doit échouer, le Service Fabric génère un nouveau réplica à partir des réplicas existants hello.

Hello de lecture [des services fiables Partition Service Fabric](service-fabric-concepts-partitioning.md) article pour plus d’informations.

## <a name="system-services"></a>Services système
Il existe des services système qui sont créés dans chaque cluster et qui fournissent des fonctionnalités de plateforme hello de Service Fabric.

**Service de noms**: cluster de chaque Service Fabric est un service d’affectation de noms, qui résout l’emplacement de tooa de noms de service dans un cluster de hello. Gérer les noms de service hello et des propriétés, tooan similaire internet Service DNS (Domain Name) pour le cluster de hello. Les clients communiquent en toute sécurité avec n’importe quel nœud dans le cluster hello à l’aide de hello Naming Service tooresolve un nom de service et son emplacement.  Les applications se déplacer au sein du cluster hello par exemple en raison de toofailures, l’équilibrage des ressources ou hello redimensionnement du cluster de hello. Vous pouvez développer des services et les clients qui résoudre l’emplacement réseau actuel de hello. Les clients obtenir l’adresse IP de machine réelles hello et le port sur lequel il est en cours d’exécution.

Lecture [communiquer avec les services](service-fabric-connect-and-communicate-with-services.md) pour plus d’informations sur la communication client et le service hello API qui fonctionnent avec hello Naming service.

**Service de magasin d’images**: chaque cluster Service Fabric a un service de magasin d’images où sont conservés les packages d’application avec version déployés. Copier un toohello de package d’application magasin d’images, puis enregistrez type d’application hello contenu dans ce package d’application. Après la configuration de type hello de l’application, vous créez une application nommée à partir de celui-ci. Vous pouvez annuler l’inscription de hello le service banque d’Image d’un type d’application après la suppression de toutes ses applications nommées.

Lecture [comprendre le paramètre de ImageStoreConnectionString hello](service-fabric-image-store-connection-string.md) pour plus d’informations sur hello service du magasin d’images.

Hello de lecture [déployer une application](service-fabric-deploy-remove-applications.md) article pour plus d’informations sur le déploiement du service d’applications toohello Image store.

## <a name="built-in-programming-models"></a>Modèles de programmation intégrés
Modèles de programmation .NET Framework sont disponibles pour vous, les services de l’infrastructure de Service toobuild :

**Services fiables**: les services une API toobuild et sans état. Les services avec état stockent leur état dans Collections fiables (par exemple, un dictionnaire ou une file d’attente). Vous obtenez également tooplug dans différentes piles de communication tels que les API Web et Windows Communication Foundation (WCF).

**Reliable Actors**: un toobuild et sans état objets d’API via virtuel modèle de programmation intervenant hello. Ce modèle peut être utile si vous avez un grand nombre d’unités indépendantes d’état/de calcul. Ce modèle utilise un modèle de thread tour, il est meilleur code tooavoid qui appelle tooother acteurs ou les services dans la mesure où un acteur individuel ne peut pas traiter les autres demandes entrantes jusqu'à ce que toutes ses demandes sortantes s’est terminé.

Hello de lecture [choisir un modèle de programmation de votre service](service-fabric-choose-framework.md) article pour plus d’informations.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Étapes suivantes
toolearn plus d’informations sur l’infrastructure de Service :

* [Vue d'ensemble de Service Fabric](service-fabric-overview.md)
* [Pourquoi un microservices approche toobuilding applications ?](service-fabric-overview-microservices.md)
* [Scénarios d’application](service-fabric-application-scenarios.md)

