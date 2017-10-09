---
title: "aaaLearn plus d’informations sur Azure Service Fabric | Documents Microsoft"
description: "En savoir plus sur les concepts fondamentaux de hello et les principales zones de Azure Service Fabric. Fournit une vue d’ensemble étendu de l’infrastructure de Service et comment toocreate microservices."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/14/2017
ms.author: ryanwi
ms.openlocfilehash: 7fe8de777755be11635912613bb5b970e3fe3ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="so-you-want-toolearn-about-service-fabric"></a>Par conséquent, vous souhaitez toolearn sur l’infrastructure de Service ?
Azure Service Fabric est une plateforme de systèmes distribués qui rend facile toopackage, déployer et gérer des microservices fiables et évolutives.  Service Fabric a une grande surface d’exposition, toutefois, et il existe beaucoup de toolearn.  Cet article fournit une synthèse de l’infrastructure de Service et décrit les concepts fondamentaux de hello, modèles de programmation, cycle de vie d’application, de test, des clusters et contrôle d’intégrité. Hello de lecture [vue d’ensemble](service-fabric-overview.md) et [quelles sont les microservices ?](service-fabric-overview-microservices.md) pour obtenir une présentation et comment l’infrastructure de Service peut être utilisé toocreate microservices. Cet article ne contient pas une liste complète de contenu, mais pointe toooverview et l’obtention des articles démarrées pour chaque zone d’infrastructure de Service. 

## <a name="core-concepts"></a>Principaux concepts
[Terminologie de service Fabric](service-fabric-technical-overview.md), [modèle d’Application](service-fabric-application-model.md), et [prise en charge des modèles de programmation](service-fabric-choose-framework.md) fournissent davantage de concepts et des descriptions, mais vous trouverez ici des notions de base hello.

<table><tr><th>Principaux concepts</th><th>Au moment du design</th><th>En cours d’exécution</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/CoreConceptsVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965"><img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">
<img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td></tr>
</table>

### <a name="design-time-application-type-service-type-application-package-and-manifest-service-package-and-manifest"></a>Au moment du design : type d’application, type de service, package et manifeste d’application, package et manifeste de service
Un type d’application est hello nom/version affectée au regroupement tooa des types de services. Cela est défini dans un fichier *ApplicationManifest.xml* qui est incorporé dans un répertoire de package d’application. Hello package d’application est ensuite copié magasin d’images du cluster toohello Service Fabric. Vous pouvez ensuite créer une application nommée à partir de ce type d’application, puis s’exécute au sein du cluster de hello. 

Un type de service est affecté à la hello nom/version du service tooa packages de code, les packages de données et les packages de configuration. Cela est défini dans un fichier ApplicationManifest.xml qui est incorporé dans un répertoire de package d’application. Hello répertoire de package de service est ensuite référencé par un package d’application *ApplicationManifest.xml* fichier. Dans un cluster de hello, après avoir créé une application nommée, vous pouvez créer un service nommé parmi hello types de service du type d’application. Un type de service est décrit par son fichier *ServiceManifest.xml*. type de service Hello est composé de paramètres de configuration de service code exécutable, qui sont chargés au moment de l’exécution, et les données statiques qui sont consommées par le service de hello.

![Types d’application service Fabric et types de service][cluster-imagestore-apptypes]

package d’application Hello est un répertoire de disque contenant du type d’application hello *ApplicationManifest.xml* fichier, qui fait référence à des packages de service hello pour chaque type de service qui compose le type d’application hello. Par exemple, un package d’application pour un type d’application de messagerie peut contenir de package de service de file d’attente tooa références, un package de service de serveur frontal et un package de service de base de données. fichiers Hello dans le répertoire de package d’application hello sont magasin d’images de cluster copiés toohello Service Fabric. 

Un package de service est un répertoire de disque contenant le type de hello service *ServiceManifest.xml* fichier, qui fait référence à code de hello, les données statiques et les packages de configuration pour le type de service hello. fichiers de Hello dans le répertoire du package service hello sont référencés par du type d’application hello *ApplicationManifest.xml* fichier. Par exemple, un package de service peut faire référence toohello code, les données statiques et les packages de configuration qui composent un service de base de données.

### <a name="run-time-clusters-and-nodes-named-applications-named-services-partitions-and-replicas"></a>En cours d’exécution : clusters et nœuds, applications nommées, services nommés, partitions et réplicas
Un [cluster Service Fabric](service-fabric-deploy-anywhere.md) est un groupe de machines virtuelles ou physiques connectées au réseau, sur lequel vos microservices sont déployés et gérés. Clusters peuvent évoluer toothousands d’ordinateurs.

Une machine ou une machine virtuelle appartenant à un cluster est appelée « nœud ». Un nom (chaîne) est affecté à chaque nœud. Les nœuds présentent des caractéristiques, telles que des propriétés de placement. Chaque machine ou machine virtuelle a un service Windows à démarrage automatique, `FabricHost.exe`, qui commence à s’exécuter dès le démarrage, puis démarre deux exécutables : `Fabric.exe` et `FabricGateway.exe`. Ces deux exécutables constituent de nœud de hello. Pour développer des scénarios de test, vous pouvez héberger plusieurs nœuds sur une seule et même machine ou machine virtuelle en exécutant plusieurs instances de `Fabric.exe` et de `FabricGateway.exe`.

Une application nommée est un ensemble de services nommés qui exécute une ou plusieurs fonctions. Un service exécute une fonction complète et autonome (il peut démarrer et s'exécuter indépendamment des autres services) et est composé de code, d’une configuration et de données. Après qu’un package d’application est un magasin d’images toohello copiés, créez une instance d’application hello au sein du cluster de hello en spécifiant le type d’application du package d’application hello (à l’aide de son nom/version). Chaque instance de type d’application se voit affecter un nom d’URI ressemblant à ceci : *fabric:/MonApplicationNommée*. Dans un cluster, vous pouvez créer plusieurs applications nommées à partir d’un seul type d’application. Vous pouvez également en créer à partir de différents types d’application. Chaque application nommée est gérée, et sa version est gérée indépendamment.

Après avoir créé une application nommée, vous pouvez créer une instance de l’un de ses types de service (un service nommé) au sein du cluster de hello en spécifiant le type de service hello (à l’aide de son nom/version). Chaque instance du type de service reçoit un nom d’URI inclus dans l’étendue de l’URI de son application nommée. Par exemple, si vous créez un « MyDatabase » nommé service au sein d’un « MyNamedApp » nommée application, hello URI ressemble à : *fabric : / MyNamedApp/MyDatabase*. Dans une application nommée, vous pouvez créer un ou plusieurs services nommés. Chaque service nommé peut posséder son propre schéma de partition et son propre nombre d’instances/réplicas. 

Il existe deux types de services : sans état et avec état. Les services sans état sont stockés à l’état persistant dans un service de stockage externe tel que Stockage Azure, Azure SQL Database ou Azure Cosmos DB. Utiliser un service sans état lorsque le service de hello n’a pas de stockage persistant. Un service avec état utilise Service Fabric toomanage état de votre service via ses Collections fiable ou la Reliable Actors modèles de programmation. 

Lors de la création d’un service nommé, vous indiquez un schéma de partition. Services de grandes quantités de l’état de fractionnement les données de hello sur plusieurs partitions. Chaque partition est une partie de l’état du service de hello, qui est réparti entre les nœuds du cluster hello hello responsable. Dans une partition, les services nommés sans état ont des instances tandis que les services nommés avec état ont des réplicas. En règle générale, les services nommés sans état ne possèdent qu’une partition, car ils sont dépourvus d’état interne. Les services nommés avec état conservent leur état dans les réplicas, et chaque partition possède son propre jeu de réplicas. Opérations de lecture et d’écriture sont effectuées dans un réplica (appelé hello principal). Toostate de modifications à partir de l’écriture d’opérations sont répliquées toomultiple autres réplicas (appelés secondaires actifs). 

Hello diagramme suivant montre relation hello entre les applications et les instances de service, les partitions et les réplicas.

![Partitions et réplicas au sein d'un service][cluster-application-instances]

### <a name="partitioning-scaling-and-availability"></a>Partitionnement, mise à l’échelle et disponibilité
[Partitionnement](service-fabric-concepts-partitioning.md) n’est pas unique tooService l’ensemble fibre optique. Le partitionnement des données constitue une forme bien connue de partitionnement. Les services avec état avec de grandes quantités de l’état de fractionnement les données de hello sur plusieurs partitions. Chaque partition est une partie de l’état du service de hello hello responsable. 

réplicas Hello de chaque partition sont répartis entre les nœuds du cluster hello, qui permet d’état de votre service nommé trop[échelle](service-fabric-concepts-scalability.md). Comme les données de salutation besoins augmentent, la croissance des partitions et Service Fabric rééquilibrage des partitions entre les nœuds toomake une utilisation efficace des ressources matérielles. Si vous ajoutez le nouveau cluster toohello de nœuds, Service Fabric rééquilibrer les réplicas de partition hello sur nombre hello augmentée de nœuds. Améliorent les performances de l’application global et réduit les conflits d’accès toomemory. Si les nœuds hello dans un cluster de hello ne sont pas utilisés efficacement, vous pouvez réduire le nombre de hello de nœuds de cluster de hello. Service Fabric rééquilibre à nouveau les réplicas de partition hello sur nombre hello diminué de nœuds toomake améliore l’utilisation du matériel hello sur chaque nœud.

Dans une partition, les services nommés sans état ont des instances tandis que les services nommés avec état ont des réplicas. En règle générale, les services nommés sans état ne possèdent qu’une partition, car ils sont dépourvus d’état interne. pour fournissent des instances de partition Hello [disponibilité](service-fabric-availability-services.md). Si une instance échoue, autres continuent toooperate normalement et le Service Fabric crée ensuite une nouvelle instance. Les services nommés avec état conservent leur état dans les réplicas, et chaque partition possède son propre jeu de réplicas. Opérations de lecture et d’écriture sont effectuées dans un réplica (appelé hello principal). Toostate de modifications à partir de l’écriture d’opérations sont répliquées toomultiple autres réplicas (appelés secondaires actifs). Un réplica doit échouer, le Service Fabric génère un nouveau réplica à partir des réplicas existants hello.

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Microservices avec et sans état pour Service Fabric
L’infrastructure de service vous permet de toobuild les applications qui se composent de microservices ou des conteneurs. Microservices sans état (par exemple, les passerelles de protocole et les serveurs proxy web) ne conservent pas un état mutable en dehors d’une demande et la réponse du service de hello. Les rôles de travail Azure Cloud Services sont un exemple de service sans état. Microservices avec état (par exemple, les comptes d’utilisateur, bases de données, périphériques, paniers d’achat et les files d’attente) conservent un état mutable, ne faisant pas autorité au-delà de la demande de hello et la réponse. Actuellement, les applications Internet sont constituées d’une combinaison de microservices avec et sans état. 

Une clé différentiation avec Service Fabric est son axées sur la création de services avec état, soit avec hello [générées dans les modèles de programmation ](service-fabric-choose-framework.md) ou avec les services avec état en conteneur. Hello [scénarios d’application](service-fabric-application-scenarios.md) décrivent des scénarios hello où les services avec état sont utilisés.

Pourquoi vous avez microservices avec état, ainsi que ceux qui sont sans état ? deux principales raisons Hello sont :

* Vous pouvez générer à débit élevé, à faible latence, le traitement transactionnel en ligne à tolérance de pannes (OLTP) des services en conservant le code et fermez toutes les données sur hello le même ordinateur. Quelques exemples : vitrines interactives, recherche, systèmes Internet des objets (IoT), systèmes commerciaux, systèmes de détection des fraudes et de traitement des cartes de crédit et gestion des enregistrements personnels.
* Vous pouvez simplifier la conception d’applications. Microservices avec état supprimer la nécessité de hello pour les files d’attente supplémentaires et caches qui sont traditionnellement exigences tooaddress hello disponibilité et la latence d’une application purement sans état. Les services avec état sont naturellement haute disponibilité et à faible latence, ce qui réduit le nombre de hello de déplacement toomanage parties dans votre application dans son ensemble.

## <a name="supported-programming-models"></a>Modèles de programmation pris en charge
Service Fabric offre plusieurs façons toowrite et gérer vos services. Services peuvent utiliser hello Service Fabric API tootake pleinement parti des fonctionnalités de plateforme hello et les infrastructures d’application. Les services peuvent être n’importe quel programme exécutable compilé, écrit dans n’importe quel langage et hébergé sur un cluster Service Fabric. Pour plus d’informations, consultez [Vue d’ensemble des modèles de programmation Service Fabric](service-fabric-choose-framework.md).

### <a name="containers"></a>Conteneurs
Par défaut, Service Fabric déploie et active les services en tant que processus. Service Fabric permet également de déployer les services dans des [conteneurs](service-fabric-containers-overview.md). Important, vous pouvez combiner des services dans les processus et services dans des conteneurs hello même application. Service Fabric prend en charge le déploiement de conteneurs Linux et de conteneurs Windows sur Windows Server 2016. Vous pouvez déployer des applications, des services sans état ou des services avec état dans des conteneurs. 

### <a name="reliable-services"></a>Services fiables (Reliable Services)
[Services fiables](service-fabric-reliable-services-introduction.md) est une infrastructure léger pour l’écriture de services qui s’intègrent avec la plateforme de Service Fabric hello et tirer parti de l’ensemble hello des fonctionnalités de plateforme. Services fiables peuvent être sans état (similaire toomost service plateformes, telles que les serveurs web ou des rôles de travail dans Azure Cloud Services), où l’état est persistant dans une solution externe, telles que la base de données Azure ou le stockage de Table Azure. Services fiables peuvent également être avec état, où l’état est persistant directement dans le service hello lui-même à l’aide de Collections fiable. L’état est [hautement disponible](service-fabric-availability-services.md) grâce à la réplication et distribué grâce au [partitionnement](service-fabric-concepts-partitioning.md), l’ensemble étant géré automatiquement par Service Fabric.

### <a name="reliable-actors"></a>Acteurs fiables (Reliable Actors)
Reposant sur des Services fiables, hello [Reliable Actor](service-fabric-reliable-actors-introduction.md) framework est une infrastructure d’application qui implémente le modèle Virtual Actor de hello, selon le modèle de conception d’acteur hello. framework d’acteur fiable Hello utilise des unités indépendantes de calcul et l’état avec une exécution monothread acteurs. Hello Reliable Actor framework fournit intégrée dans la communication pour les acteurs et persistance d’état prédéfinies et des configurations de montée en puissance parallèle.

### <a name="aspnet-core"></a>ASP.NET Core
Service Fabric s’intègre dans [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) en tant que modèle de programmation de premier ordre pour la création d’applications web et API

### <a name="guest-executables"></a>Exécutables invités
Un [exécutable d’invité](service-fabric-deploy-existing-app.md) est un exécutable existant quelconque (écrit dans n’importe quel langage) qui est hébergé sur un cluster Service Fabric avec d’autres services. Les exécutables invités ne s’intègrent pas directement dans les API Service Fabric. Toutefois ils en tirant parti des fonctionnalités hello offres de plateforme, telles que l’intégrité personnalisée et charger la création de rapports et découverte de service en appelant l’API REST. Ils prennent également en charge le cycle de vie complet des applications. 

## <a name="application-lifecycle"></a>Cycle de vie des applications
Comme avec d’autres plateformes, une application de Service Fabric passe généralement par hello suivant phases : conception, développement, test, déploiement, mise à niveau, maintenance et suppression. L’infrastructure de service prend en charge de première classe hello cycle de vie complet des applications de cloud, de développement jusqu’au déploiement, la gestion quotidienne et la désaffectation de tooeventual de maintenance. modèle de service Hello permet plusieurs tooparticipate différents rôles de cycle de vie application hello de façon indépendante. [Cycle de vie application service Fabric](service-fabric-application-lifecycle.md) fournit une vue d’ensemble de l’API de hello et comment ils sont utilisés par les différents rôles de hello tout au long des phases de hello du cycle de vie application hello Service Fabric. 

cycle de vie entier Hello peut être géré à l’aide de [applets de commande PowerShell](/powershell/module/ServiceFabric/), [API C#](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient), [API Java](/java/api/system.fabric._application_management_client), et [API REST](/rest/api/servicefabric/). Vous pouvez également configurer des pipelines d’intégration continue ou de développement continu à l’aide d’outils tels que [Visual Studio Team Services](service-fabric-set-up-continuous-integration.md) ou [Jenkins](service-fabric-cicd-your-linux-java-application-with-jenkins.md).

Hello vidéo Microsoft Virtual Academy suivante décrit comment toomanage le cycle de vie de votre application :<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=My3Ka56yC_6106218965">
<img src="./media/service-fabric-content-roadmap/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="test-applications-and-services"></a>Tester des applications et services
toocreate services de cloud à l’échelle, il est véritablement tooverify critiques que vos applications et services peuvent résister aux défaillances du monde réel. Hello erreur Analysis Services est conçu pour tester les services qui reposent sur l’infrastructure de Service. Avec hello [erreur Analysis Service](service-fabric-testability-overview.md), vous pouvez induire des erreurs significatives et exécuter des scénarios de test complet sur vos applications. Ces erreurs et les scénarios de tester et valider hello de nombreux États et transitions subissent un service tout au long de sa durée de vie, tout de façon contrôlée, sécurisée et cohérente.

Les [actions](service-fabric-testability-actions.md) ciblent un service à tester à l’aide d’erreurs isolées. Un développeur de service peut utiliser en tant que blocs de construction toowrite compliquée scénarios. Exemples d’erreurs simulées :

* Redémarrer un toosimulate de nœud de n’importe quel nombre de situations où un ordinateur ou un ordinateur virtuel est redémarré.
* Déplacer un réplica de l’équilibrage de charge toosimulate service avec état, basculement ou de mise à niveau de l’application.
* Appelez la perte du quorum dans un service avec état de toocreate une situation où les opérations d’écriture ne peut pas continuer, car il n’existe pas suffisamment réplicas « sauvegarde » ou « secondaire » tooaccept de nouvelles données.
* Appelez la perte de données sur un service avec état de toocreate une situation dans laquelle tous les États en mémoire sont complètement supprimé.

Les [scénarios](service-fabric-testability-scenarios.md) sont des opérations complexes composées d’une ou plusieurs actions. Hello erreur Analysis Services fournit deux scénarios intégrés :

* [Scénario de chaos](service-fabric-controlled-chaos.md)-simule les erreurs continus, entrelacés (progressif et anormal) dans l’ensemble de cluster de hello sur de longues périodes.
* [Scénario de basculement](service-fabric-testability-scenarios.md#failover-test)-une version de scénario de test de chaos hello qui cible une partition de service spécifique en laissant d’autres services pas affectées.

## <a name="clusters"></a>Clusters
Un [cluster Service Fabric](service-fabric-deploy-anywhere.md) est un groupe de machines virtuelles ou physiques connectées au réseau, sur lequel vos microservices sont déployés et gérés. Clusters peuvent évoluer toothousands d’ordinateurs. Une machine ou machine virtuelle faisant partie d’un cluster est appelée un nœud de cluster. Un nom (chaîne) est affecté à chaque nœud. Les nœuds présentent des caractéristiques, telles que des propriétés de placement. Chaque machine ou machine virtuelle est dotée d’un service à démarrage automatique, `FabricHost.exe`, qui s’exécute au démarrage, puis lance deux exécutables : Fabric.exe et FabricGateway.exe. Ces deux exécutables constituent de nœud de hello. Pour les scénarios de test, vous pouvez héberger plusieurs nœuds sur une seule et même machine ou sur une seule et même machine virtuelle en exécutant plusieurs instances de `Fabric.exe` et `FabricGateway.exe`.

Les clusters Service Fabric peuvent être créés sur des machines virtuelles ou physiques exécutant Windows Server ou Linux. Sont en mesure de toodeploy et d’exécuter des applications de Service Fabric dans n’importe quel environnement où vous avez un ensemble d’ordinateurs Windows Server ou Linux qui sont interconnectés : localement, sur Microsoft Azure, ou sur n’importe quel fournisseur de cloud.

Hello vidéo Microsoft Virtual Academy suivante décrit les clusters Service Fabric :<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/ClusterOverview.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="clusters-on-azure"></a>Clusters sur Azure
Les clusters de l’infrastructure de Service en cours d’exécution sur Azure fournit l’intégration avec d’autres fonctionnalités d’Azure et les services, ce qui rend les opérations et la gestion du cluster de hello plus facile et plus fiable. Comme un cluster est une ressource Azure Resource Manager, vous pouvez modéliser des clusters comme n’importe quelle autre ressource dans Azure. Le Gestionnaire de ressources fournit également une gestion plus simple de toutes les ressources utilisées par le cluster de hello comme une unité unique. Les clusters dans Azure sont intégrés à Azure Diagnostics et Log Analytics. Les types de nœuds de cluster sont des [groupes de machines virtuelles identiques](/azure/virtual-machine-scale-sets/index) : la fonctionnalité de mise à l’échelle automatique est donc intégrée.

Vous pouvez créer un cluster sur Azure via hello [portail Azure](service-fabric-cluster-creation-via-portal.md), d’un [modèle](service-fabric-cluster-creation-via-arm.md), ou à partir de [Visual Studio](service-fabric-cluster-creation-via-visual-studio.md).

Aperçu de Hello du Service Fabric sur Linux vous permet de toobuild, déployer et gérer des applications hautement disponibles et hautement évolutives sur Linux comme vous le feriez sur Windows. les infrastructures de Service Fabric Hello (Services fiables et Reliable Actors) sont disponibles dans Java sur Linux, en outre tooC # (.NET Core). Vous pouvez également créer des [services exécutables invités](service-fabric-deploy-existing-app.md) via tous les langages ou frameworks. En outre, l’aperçu de hello prend également en charge des conteneurs Docker orchestrant ces opérations. Conteneurs docker peuvent exécuter des exécutables de l’invité ou les services de Service Fabric natives, qui utilisent des infrastructures de Service Fabric hello. Pour plus d’informations, consultez [Service Fabric sur Linux](service-fabric-linux-overview.md).

Étant donné que Service Fabric sur Linux est une version préliminaire, certaines fonctionnalités sont prises en charge sur Windows, mais pas sur Linux. toolearn plus, lisez [les différences entre le Service Fabric sur Linux et Windows](service-fabric-linux-windows-differences.md).

### <a name="standalone-clusters"></a>Clusters autonomes
L’infrastructure de service fournit un package d’installation pour vous toocreate autonome Service Fabric clusters sur site ou sur n’importe quel fournisseur de cloud. Les clusters autonome permettent de vous hello liberté toohost un cluster où vous le souhaitez. Si vos données sont toocompliance de sujet ou des contraintes réglementaires, ou tookeep local de vos données, vous pouvez héberger votre propre cluster et les applications. Les applications de l’infrastructure de service peuvent s’exécuter dans plusieurs environnements d’hébergement sans aucune modification, donc votre connaissance de la création d’applications reprend à partir d’un hébergement tooanother d’environnement. 

[Créer votre premier cluster Service Fabric autonome](service-fabric-get-started-standalone-cluster.md)

Les clusters autonomes Linux ne sont pas encore pris en charge.

### <a name="cluster-security"></a>Sécurité des clusters
Clusters doivent être tooprevent sécurisé non autorisé les utilisateurs de se connecter tooyour cluster, surtout quand les charges de production en cours d’exécution sur ce dernier. Bien qu’il soit possible de toocreate un cluster non sécurisé, cela permet aux utilisateurs anonymes tooconnect tooit si les points de terminaison de gestion sont exposées toohello internet public. Il n’est pas possible toolater activer la sécurité sur un cluster non sécurisée : sécurité du cluster est activée au moment de la création de cluster.

scénarios de sécurité du cluster Hello sont :
* Sécurité nœud à nœud
* Sécurité client à nœud
* Contrôle d’accès en fonction du rôle

Pour plus d’informations, consultez [Sécuriser un cluster](service-fabric-cluster-security.md).

### <a name="scaling"></a>Mise à l'échelle
Si vous ajoutez le nouveau cluster toohello de nœuds, Service Fabric rééquilibrage des réplicas de partitions hello et les instances sur nombre hello augmentée de nœuds. Améliorent les performances de l’application global et réduit les conflits d’accès toomemory. Si les nœuds hello dans un cluster de hello ne sont pas utilisés efficacement, vous pouvez réduire le nombre de hello de nœuds de cluster de hello. Service Fabric rééquilibrage à nouveau les réplicas de partition hello et instances dans le nombre de hello diminué de nœuds toomake améliorer l’utilisation du matériel hello sur chaque nœud. Vous pouvez mettre à l’échelle des clusters dans Azure [manuellement](service-fabric-cluster-scale-up-down.md) ou [par programmation](service-fabric-cluster-programmatic-scaling.md). Les clusters autonomes peuvent être mis à l’échelle [manuellement](service-fabric-cluster-windows-server-add-remove-nodes.md).

### <a name="cluster-upgrades"></a>Mise à niveau des clusters
Nouvelles versions du runtime de Service Fabric hello sont régulièrement publiées. Effectuez des mises à niveau de runtime, ou de structure, sur votre cluster afin de toujours utiliser une [version prise en charge](service-fabric-support.md). En outre toofabric met à niveau, vous pouvez également mettre à jour configuration de cluster telles que des certificats ou des ports de l’application.

Un cluster Service Fabric est une ressource que vous possédez mais qui est en partie gérée par Microsoft. Microsoft est responsable de la mise à jour corrective hello sous-jacente du système d’exploitation et les mises à niveau de l’ensemble fibre optique sur votre cluster. Vous pouvez définir des mises à niveau, votre structure d’automatique tooreceive cluster lorsque Microsoft publie une nouvelle version, ou choisir tooselect une version prise en charge l’infrastructure que vous le souhaitez. Mises à niveau l’infrastructure et de configuration peuvent être définis via hello portail Azure ou via le Gestionnaire de ressources. Pour plus d’informations, consultez [Mettre à niveau un cluster Service Fabric](service-fabric-cluster-upgrade.md). 

Un cluster autonome est une ressource que vous possédez entièrement. Vous êtes responsable de la mise à jour corrective hello sous-jacente du système d’exploitation et de lancer des mises à niveau de l’ensemble fibre optique. Si votre cluster peut se connecter trop[https://www.microsoft.com/download](https://www.microsoft.com/download), vous pouvez définir votre téléchargement tooautomatically de cluster et configurer hello nouveau Service Fabric package runtime. Vous lancer puis mise à niveau hello. Si votre cluster ne peut pas accéder à [https://www.microsoft.com/download](https://www.microsoft.com/download), vous pouvez télécharger manuellement hello nouvelle exécution du package à partir d’un ordinateur connecté internet et puis lancez la mise à niveau hello. Pour plus d’informations, consultez [Mettre à niveau un cluster Service Fabric autonome](service-fabric-cluster-upgrade-windows-server.md).

## <a name="health-monitoring"></a>Surveillance de l’intégrité
Service Fabric introduit un [modèle d’intégrité](service-fabric-health-introduction.md) conçu tooflag les cluster défectueux et les conditions d’application sur des entités spécifiques (par exemple, les nœuds de cluster et les réplicas de service). modèle de contrôle d’intégrité Hello utilise rapporteurs de contrôle d’intégrité (composants système et des agents de surveillance). objectif de Hello est facile et rapide de diagnostic et de réparation. Enregistreurs de service doivent toothink avance sur l’intégrité et comment trop[concevoir des rapports de santé](service-fabric-report-health.md#design-health-reporting). Toutes les conditions qui peuvent avoir un impact sur l’intégrité doivent être signalée, surtout si elle peut aider à des problèmes d’indicateur fermer toohello racine. informations de contrôle d’intégrité Hello pouvant gagner du temps sur le débogage et enquête une fois hello service soit configuré et en cours d’exécution à l’échelle en production.

Moniteur de rapporteurs Hello Service Fabric identifié les conditions d’intérêt. Ils dressent un rapport sur ces conditions en fonction de leur vue locale. Hello [magasin de contrôle d’intégrité](service-fabric-health-introduction.md#health-store) agrège des données de contrôle d’intégrité envoyées par tous les rapporteurs toodetermine si les entités sont globalement intègres. modèle de Hello est toouse riche, flexible et facile de toobe prévue. qualité Hello de rapports d’intégrité de hello détermine la précision hello de vue de contrôle d’intégrité hello du cluster de hello. Des faux positifs qui indiquent erronément des problèmes d’intégrité peuvent avoir une incidence négative sur les mises à niveau ou autres services utilisant des données d’intégrité. Les services de réparation et mécanismes d’alertes sont des exemples de services de ce type. Par conséquent, la réflexion est rapports tooprovide nécessaires qui capturent les conditions d’intérêt dans hello meilleure façon possible.

La création de rapports peut être effectuée à partir des éléments suivants :
* Hello analysés réplica de service Service Fabric ou instance.
* Les agents de surveillance internes déployés en tant que services Service Fabric (par exemple, un service Service Fabric sans état, qui surveille des conditions et émet des rapports). agents de surveillance Hello peuvent être déployés sur tous les nœuds ou peuvent être associés toohello analysé service.
* Agents de surveillance internes qui s’exécutent sur des nœuds de Service Fabric hello mais qui ne sont pas implémentées en tant que services de Fabric de Service.
* Externe watchdogs sonde hello ressource de cluster de Service Fabric hello externe (par exemple, service de surveillance comme Gomez).

En dehors de la zone de hello, composants d’infrastructure de Service rapport d’intégrité sur toutes les entités dans un cluster de hello. Les [rapports d’intégrité du système](service-fabric-understand-and-troubleshoot-with-system-health-reports.md) procurent une visibilité sur les fonctionnalités du cluster et des applications, et signalent les problèmes d’intégrité. Pour les applications et services, les rapports d’intégrité système Vérifiez que les entités sont implémentées et sont comportent correctement à partir de la perspective hello du runtime de Service Fabric hello. rapports de Hello ne pas fournir n’importe quel contrôle d’intégrité de la logique métier de hello du service de hello ou détecter les processus bloqués. la logique du service spécifique tooyour tooadd d’intégrité plus d’informations, [implémenter l’intégrité personnalisée reporting](service-fabric-report-health.md) dans vos services.

L’infrastructure de service fournit plusieurs moyens trop[afficher les rapports d’intégrité](service-fabric-view-entities-aggregated-health.md) agrégé dans le magasin de contrôle d’intégrité hello :
* [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) ou autres outils de visualisation.
* Requêtes d’intégrité (via [PowerShell](/powershell/module/ServiceFabric/), hello [c# FabricClient APIs](/api/system.fabric.fabricclient.healthclient) et [FabricClient APIs Java](/java/api/system.fabric._health_client), ou [API REST](/rest/api/servicefabric)).
* Requêtes générales qui retournent une liste des entités qui ont d’intégrité en tant qu’une des propriétés hello (via PowerShell, les API hello ou REST).

Hello que vidéo Microsoft Virtual Academy suivant décrit le modèle de contrôle d’intégrité de Service Fabric hello et son utilisation :<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-content-roadmap/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment toocreate un [cluster dans Azure](service-fabric-cluster-creation-via-portal.md) ou un [cluster autonome sur Windows](service-fabric-cluster-creation-for-windows-server.md).
* Essayez de créer un service à l’aide de hello [des Services fiables](service-fabric-reliable-services-quick-start.md) ou [Reliable Actors](service-fabric-reliable-actors-get-started.md) modèles de programmation.
* Découvrez comment trop[migrer à partir des Services de cloud computing](service-fabric-cloud-services-migration-differences.md).
* En savoir trop[surveiller et diagnostiquer les services](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). 
* En savoir trop[tester vos applications et services](service-fabric-testability-overview.md).
* En savoir trop[gérer et organiser les ressources de cluster](service-fabric-cluster-resource-manager-introduction.md).
* Examinez hello [exemples de Service Fabric](http://aka.ms/servicefabricsamples).
* Découvrez les [options de support de Service Fabric](service-fabric-support.md).
* Hello de lecture [blog de l’équipe](https://blogs.msdn.microsoft.com/azureservicefabric/) des articles et des annonces.


[cluster-application-instances]: media/service-fabric-content-roadmap/cluster-application-instances.png
[cluster-imagestore-apptypes]: ./media/service-fabric-content-roadmap/cluster-imagestore-apptypes.png
