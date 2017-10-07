---
title: "guide d’aaaGet démarré pour les développeurs sur Azure | Documents Microsoft"
description: "Cette rubrique fournit des informations essentielles pour les développeurs qui souhaitent tooget démarré à l’aide de la plateforme de Microsoft Azure hello pour les besoins de leur développement."
services: 
cloud: 
documentationcenter: 
author: ggailey777
manager: erikre
ms.assetid: 
ms.service: na
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: glenga
ms.openlocfilehash: 72dc2678db7738923d4bc7783e297fea6fcded83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-guide-for-azure-developers"></a>Guide de prise en main pour les développeurs Azure

## <a name="what-is-azure"></a>Qu’est-ce qu’Azure ?

Azure est une plateforme complète du cloud qui peut héberger vos applications existantes, rationaliser le développement de nouvelles applications hello et même améliorer des applications locales. Azure intègre les services de cloud computing hello que vous avez besoin de toodevelop, tester, déployer et gérer vos applications, tout en tirant parti de l’efficacité de hello de cloud computing.

En hébergeant vos applications dans Azure, vous pouvez commencer à petite échelle et faire évoluer aisément vos applications à mesure que la demande client augmente. Azure propose également la fiabilité hello que nécessaire pour les applications de haute disponibilité, même y compris le basculement entre les différentes régions. Hello [portail Azure](https://portal.azure.com) vous permet de gérer facilement tous vos services Azure. Vous pouvez également gérer vos services par programmation en utilisant des API et des modèles spécifiques aux services.

**Personnes concernées par ce**: ce guide est une plateforme Azure pour les développeurs d’applications de toohello introduction. Il fournit des instructions et la direction que vous avez besoin de toostart création de nouvelles applications dans Azure ou de migration tooAzure d’applications existant.

## <a name="where-do-i-start"></a>Par où commencer ?

Avec tous les services hello Azure offre, il peut être un toofigure tâche fastidieuse savoir quels services vous devez toosupport l’architecture de solution. Cette hello met en évidence de section Azure que les développeurs utilisent généralement des services. Pour obtenir la liste de tous les services Azure, consultez hello [documentation sur Azure](../../index.md).

Tout d’abord, vous devez décider sur la façon de toohost votre application dans Azure. Devez-vous toomanage votre infrastructure en tant qu’un ordinateur virtuel (VM). Vous pouvez utiliser des fonctionnalités de gestion de plateforme de hello Azure fournit ? Peut-être avez-vous besoin d’une infrastructure sans toohost l’exécution de code uniquement ?

Votre application a besoin d’un stockage sur le cloud et Azure propose plusieurs options pour cela. Vous pouvez bénéficier de l’authentification en entreprise d’Azure. Il existe également des outils de développement et de surveillance basés sur le cloud, et la plupart des services d’hébergement offrent une intégration DevOps.

À présent, examinons certains des services spécifiques hello que nous vous recommandons d’examiner pour vos applications.

### <a name="application-hosting"></a>Hébergement d’applications

Azure fournit plusieurs toorun d’offres de calcul basées sur le cloud à votre application afin que vous n’avez pas tooworry sur les détails de l’infrastructure hello. Vous pouvez facilement monter en puissance ou augmenter la taille des instances de vos ressources à mesure que l’utilisation de vos applications augmente.

Azure propose des services qui prennent en charge vos besoins d’hébergement et de développement d’applications. Azure fournit l’infrastructure-as-a-service (IaaS) toogive vous contrôle total sur votre application d’hébergement. Azure platform-as-a-service (PaaS) assurent hello entièrement services nécessaires toopower vos applications gérées. Il existe un hébergement sans même true dans Azure où vous toodo suffit écrire votre code.

![Options d’hébergement d’applications Azure](./media/azure-developer-guide/azure-developer-hosting-options.png)


#### <a name="azure-app-service"></a>Azure App Service 

Lorsque vous souhaitez toopublish de chemin d’accès rapide hello vos projets web, envisagez d’Azure App Service. Service d’applications permet de facilement tooextend votre web apps toosupport vos clients mobiles et de publier des API REST simple. Cette plateforme offre une authentification à l’aide des réseaux sociaux, une mise à l’échelle automatique basée sur le trafic, des tests en production et des déploiements continus et basés sur des conteneurs.

Lorsque vous créez une application de Service d’applications, vous sélectionnez un des types suivants de hello :

- [Web Apps](../../app-service-web/app-service-web-overview.md) : vous permet d’héberger des sites web et des applications web qui sont écrits en langage .NET, Java, PHP, Node.js ou Python.

- [Applications mobiles](../../app-service-mobile/app-service-mobile-value-prop.md): accès de toosupport étend les applications Web à partir d’appareils mobiles. Ce type offre une authentification avec les réseaux sociaux et Azure Active Directory (Azure AD), fournit le stockage principal et s’intègre à [Azure Notification Hubs](../../notification-hubs/notification-hubs-push-notification-overview.md) pour les notifications Push.

- [Applications API](../../app-service-api/app-service-api-apps-why-best-platform.md): vous permet de plus en toute sécurité exposer votre API dans le cloud hello avec des métadonnées Swagger afin que les clients puissent les utiliser facilement.

Étant donné que tous les types de trois applications partagent hello runtime du Service de l’application, vous pouvez héberger un site Web, prendre en charge les clients mobiles et exposer votre API dans Azure, à partir d’hello même projet ou solution. toolearn en savoir plus sur le Service d’application, consultez [mode de fonctionnement du Service application](../../app-service/app-service-how-works-readme.md).

App Service a été conçu en tenant compte de DevOps. Il prend en charge divers outils de déploiement d’intégration continue et de publication, notamment les webhooks GitHub, Jenkins, Visual Studio Team Services, TeamCity, etc.

Vous pouvez migrer vos tooApp applications existantes Service à l’aide de hello [l’outil de migration en ligne](https://www.migratetoazure.net/).

>**Lorsque toouse**: utilisation du Service d’applications lorsque vous effectuez une migration tooAzure d’applications web existantes, et que vous devez une plateforme d’hébergement entièrement gérée pour vos applications web. Vous pouvez également utiliser le Service d’applications lorsque vous avez besoin des clients mobiles toosupport ou exposez des API REST avec votre application.

>**Prise en main**: Service d’applications rend facile toocreate et déployer votre premier [application web](../../app-service-web/web-sites-dotnet-get-started.md), [application mobile](../../app-service-mobile/app-service-mobile-ios-get-started.md), ou [application API](../../app-service-api/app-service-api-dotnet-get-started.md).

>**Essayez dès maintenant**: Service d’applications vous permet de configurer une courte durée de vie tootry hello plateforme d’applications sans avoir toosign pour un compte Azure. Essayez de plateforme de hello et [créer votre application Azure App Service](https://tryappservice.azure.com/).

#### <a name="azure-virtual-machines"></a>Machines virtuelles Azure

Comme fournisseur d’infrastructure-as-a-service (IaaS), Azure vous permet de déployer tooor migrer votre tooeither d’application Windows ou les machines virtuelles Linux. Avec un réseau virtuel Azure, les Machines virtuelles Azure prend en charge le déploiement de hello de tooAzure Windows ou les machines virtuelles Linux. Avec des machines virtuelles, vous avez un contrôle total sur configuration hello de l’ordinateur de hello. Lorsque vous utilisez des machines virtuelles, vous êtes responsable de toutes les tâches d’installation, de configuration et de maintenance du logiciel serveur, ainsi que des correctifs du système d’exploitation.

En raison du niveau de hello de contrôle avec les machines virtuelles, vous pouvez exécuter un large éventail de charges de travail serveur sur Azure qui ne tiennent pas dans un modèle PaaS. Ces charges de travail incluent les serveurs de base de données, Windows Server Active Directory et Microsoft SharePoint. Pour plus d’informations, consultez la documentation de Machines virtuelles de hello pour soit [Linux](/azure/virtual-machines/linux/) ou [Windows](/azure/virtual-machines/windows/).

>**Lorsque toouse**: utilisent des ordinateurs virtuels lorsque vous souhaitez complète de contrôler votre application d’une infrastructure ou toomigrate local application les charges de travail tooAzure sans avoir toomake modifications.

>**Prise en main**: créer un [Linux VM](../../virtual-machines/virtual-machines-linux-quick-create-portal.md) ou [machine virtuelle Windows](../../virtual-machines/virtual-machines-windows-hero-tutorial.md) de hello portail Azure.

#### <a name="azure-functions-serverless"></a>Azure Functions (sans serveur)

Au lieu de se préoccuper création et la gestion d’un ensemble toorun d’infrastructure application ou hello votre code. Que se passe-t-il si vous pouvez simplement écrire votre code et qu’elle s’exécute dans la réponse tooevents ou selon une planification ?  [Les fonctions Azure](../../azure-functions/functions-overview.md) est un « sans serveur »-style de l’offre que vous permet d’écrire simplement hello code dont vous avez besoin. Avec Functions, l’exécution du code est déclenchée par des requêtes HTTP, des webhooks, des événements de service cloud ou selon une planification. Vous pouvez écrire du code dans le langage de développement de votre choix, tel que C\#, F\#, Node.js, Python ou PHP. Avec la facturation basée sur la consommation, vous payez uniquement pour les temps hello que votre code s’exécute, Azure met à l’échelle en fonction des besoins.

>**Lorsque toouse**: utiliser des fonctions Azure lorsque vous avez le code qui est déclenché par d’autres services Azure, en événements basés sur le web, ou selon une planification. Vous pouvez également utiliser les fonctions lorsque vous ne devez hello surcharge d’un projet hébergé ou lorsque vous souhaitez uniquement toopay pour hello exécution de votre code. toolearn, voir [vue d’ensemble des fonctions Azure](../../azure-functions/functions-overview.md).

>**Prise en main**: suivez le didacticiel de démarrage rapide de fonctions hello trop[créer votre première fonction](../../azure-functions/functions-create-first-azure-function.md) à partir du portail de hello.

>**Essayez dès maintenant**: fonctions d’Azure vous permet d’exécuter votre code sans avoir toosign pour un compte Azure. Essayez-le dès à présent et [créez votre première fonction Azure](https://tryappservice.azure.com/).

#### <a name="azure-service-fabric"></a>Azure Service Fabric

Azure Service Fabric est une plateforme de systèmes distribués qui rend facile toobuild, du package, déployer et gérer des microservices fiables et évolutives. Il fournit également des fonctionnalités complètes de gestion d’application pour la configuration, le déploiement, l’analyse, la mise à niveau/mise à jour corrective et la suppression d’applications déployées. Les applications qui s’exécutent sur un pool de machines, peuvent commencer petites et mettre à l’échelle toohundreds, voire des milliers d’ordinateurs en fonction des besoins.

Service Fabric prend en charge WebAPI avec Open Web Interface for .NET (OWIN) et ASP.NET Core. Il fournit des kits SDK pour la création de services sur Linux en langage .NET Core ou Java. toolearn en savoir plus sur l’infrastructure de Service, consultez hello [Service Fabric cursus](https://azure.microsoft.com/documentation/learning-paths/service-fabric/).

>**Lorsque toouse :** Service Fabric est un bon choix lors de la création d’une application ou réécrire un toouse d’application existant une architecture de microservice. Utiliser l’infrastructure de Service lorsque vous avez besoin de contrôler plus ou un accès direct à infrastructure sous-jacente de hello.

>**Démarrer** : [créez votre première application Azure Service Fabric](../../service-fabric/service-fabric-create-your-first-application-in-visual-studio.md).

### <a name="enhance-your-applications-with-azure-services"></a>Améliorer vos applications avec les services Azure

En outre, tooapplication d’hébergement, Azure fournit les offres de service qui peuvent améliorer les fonctionnalités de hello, de développement et de maintenance de vos applications, à la fois dans le cloud de hello et sur site.

#### <a name="hosted-storage-and-data-access"></a>Stockage hébergé et accès aux données

La plupart des applications doit stocker des données, ainsi en fonction de la façon dont vous décidez toohost votre application dans Azure, envisagez une ou plusieurs des hello suivant des services de stockage et de données.

-   **Base de données SQL Azure**: basée sur un Azure la version du moteur de Microsoft SQL Server de hello pour le stockage des données relationnelles sous forme de tableau dans le cloud de hello. SQL Database offre des performances prévisibles et une scalabilité sans interruption de service. Il assure aussi la continuité des activités et la protection des données.

    >**Lorsque toouse**: lorsque votre application nécessite un stockage de données avec intégrité référentielle, prise en charge transactionnelle et prise en charge pour les requêtes TSQL.

    >**Prise en main**: [créer une base de données SQL en quelques minutes à l’aide de hello Azure portal](../../sql-database/sql-database-get-started.md).

-   **Stockage Azure** : offre un stockage durable, hautement disponible pour les objets blob, les files d’attente, les fichiers et d’autres types de données non relationnelles. Stockage des fondements hello stockage pour les machines virtuelles.

    >**Lorsque toouse**: lorsque votre application stocke des données non relationnelles, telles que le paires clé-valeur (tables), les objets BLOB, partages de fichiers ou des messages (files d’attente).

    >**Démarrer** : choisissez parmi les types de stockage suivants : [objets blob](../../storage/blobs/storage-dotnet-how-to-use-blobs.md), [tables](../../cosmos-db/table-storage-how-to-use-dotnet.md), [files d’attente](../../storage/queues/storage-dotnet-how-to-use-queues.md) et [fichiers](../../storage/files/storage-dotnet-how-to-use-files.md).

-   **Azure DocumentDB** : service de base de données NoSQL scalable et entièrement managé, qui permet l’exécution de requêtes SQL sur les données d’objet. Vous pouvez accéder à DocumentDB en utilisant des pilotes MongoDB existants.
    >**Lorsque toouse :** quand votre application a besoin des requêtes SQL toobe en mesure de tooexecute sur des documents JSON, ou si vous utilisez MongoDB.

    >**Démarrer** : [générez une application console C# DocumentDB](../../documentdb/documentdb-get-started.md). Si vous êtes développeur MongoDB, consultez [Prise en charge du protocole DocumentDB pour MongoDB](../../documentdb/documentdb-protocol-mongodb.md).

Vous pouvez utiliser [Azure Data Factory](../../data-factory/data-factory-introduction.md) toomove locales existantes tooAzure de données. Si vous n’êtes pas prêt toomove données toohello dans le cloud, [connexions hybrides](../../biztalk-services/integration-hybrid-connection-overview.md) dans permet de BizTalk Services vous connecter votre application de Service hébergé ressources tooon local d’application. Vous pouvez également connecter des services de données et de stockage tooAzure à partir de vos applications sur site.

#### <a name="docker-support"></a>Prise en charge de Docker

Les conteneurs Docker, forme de virtualisation du système d’exploitation, vous permettent de déployer des applications de manière plus efficace et prévisible. Une application en conteneur fonctionne Bonjour de production même façon que sur vos systèmes de développement et de test. Vous pouvez gérer les conteneurs à l’aide des outils Docker standard. Vous pouvez utiliser vos compétences et les outils open source populaires toodeploy et gérer des applications basées sur le conteneur sur Azure.

Azure offre plusieurs moyens de conteneurs toouse dans vos applications.

-   **L’extension Docker VM Azure**: vous permet de configurer votre machine virtuelle avec tooact d’outils Docker en tant qu’un hôte Docker.

    >**Lorsque toouse**: lorsque vous souhaitez que les déploiements toogenerate conteneur cohérent pour vos applications sur un ordinateur virtuel, ou si vous voulez toouse [Docker Compose](https://docs.docker.com/compose/overview/).

    >**Prise en main**: [créer un environnement de Docker dans Azure à l’aide d’extension de machine virtuelle de Docker hello](../../virtual-machines/virtual-machines-linux-dockerextension.md).

-   **Service de conteneur Azure**: permet de créer, de configurer et de gérer un cluster d’ordinateurs virtuels qui sont préconfigurés toorun en conteneur applications. toolearn en savoir plus sur le Service de conteneur, consultez [introduction du Service de conteneur Azure](../../container-service/container-service-intro.md).

    >**Lorsque toouse**: lorsque vous avez besoin toobuild prêt pour la production d’environnements évolutifs qui fournissent des outils de planification et de gestion supplémentaires, ou lorsque vous déployez un cluster Docker Swarm.

    >**Démarrer** : [déployez un cluster Container Service](../../container-service/dcos-swarm/container-service-deployment.md).

-   **Docker Machine** : vous permet d’installer et de gérer un moteur Docker sur les ordinateurs hôtes virtuels en utilisant les commandes docker-machine.

    >**Lorsque toouse**: lorsque vous devez tooquickly prototype une application en créant un seul hôte Docker.

-   **Image Docker personnalisée pour App Service** : vous permet d’utiliser des conteneurs Docker à partir d’un registre de conteneurs ou d’un conteneur de clients lorsque vous déployez une application web sur Linux.

    >**Lorsque toouse**: lors du déploiement d’une application web sur l’image de Linux tooa Docker.

    >**Démarrer** : [utilisez une image Docker personnalisée pour App Service sur Linux](../../app-service-web/app-service-linux-using-custom-docker-image.md).

### <a name="authentication"></a>Authentification

Son toonot essentiel uniquement de savoir qui utilise vos applications, mais également tooprevent non autorisé d’accéder aux ressources tooyour. Azure fournit plusieurs façons tooauthenticate vos clients de l’application.

-   **Azure Active Directory (Azure AD)**: hello mutualisée, basée sur le cloud, identité et accès service de gestion Microsoft. Vous pouvez ajouter l’authentification unique sur les applications tooyour (SSO) en intégrant avec Azure AD. Vous pouvez accéder à des propriétés de répertoire à l’aide de hello Azure AD Graph API directement ou hello Microsoft Graph API. Vous pouvez intégrer avec prise en charge d’Azure AD pour la structure de d’autorisation OAuth2.0 hello et ouvrez connecter d’ID à l’aide de points de terminaison HTTP/REST natifs et hello bibliothèques d’authentification multi-plateforme Azure AD.

    >**Lorsque toouse**: tooprovide une expérience d’authentification, vous pouvez utiliser des données basées sur le graphique, ou authentifier les utilisateurs de domaine.

    >**Prise en main**: toolearn, voir hello [guide du développeur Azure Active Directory](../../active-directory/active-directory-developers-guide.md).

-   **L’authentification du Service application**: lorsque vous choisissez toohost du Service de l’application de votre application, vous obtenez également prise en charge de l’authentification intégrée pour Azure AD, ainsi que les fournisseurs d’identité sociaux, notamment Facebook, Google, Microsoft et Twitter.

    >**Lorsque toouse**: lorsque vous souhaitez que l’authentification de tooenable dans une application de Service d’applications à l’aide d’Azure AD, fournisseurs d’identité sociaux, ou les deux.

    >**Prise en main**: toolearn en savoir plus sur l’authentification dans le Service d’application, consultez [d’authentification et d’autorisation dans Azure App Service](../../app-service/app-service-authentication-overview.md).

toolearn en savoir plus sur les meilleures pratiques de sécurité dans Azure, consultez [modèles et meilleures pratiques de sécurité Azure](../../security/security-best-practices-and-patterns.md).

### <a name="monitoring"></a>Surveillance

Votre application rapidement et en cours d’exécution dans Azure, vous devez toobe toomonitor en mesure de performances, surveillez les problèmes et voir comment les clients utilisent votre application. Azure fournit plusieurs options de surveillance.

-   **Visual Studio Application Insights**: service hébergé d’un Azure l’analytique extensible qui s’intègre à Visual Studio toomonitor de vos applications web en direct. Elle vous donne les données hello que vous avez besoin de toocontinuously améliorent les performances de hello et de facilité d’utilisation de vos applications, si elles sont hébergés sur Azure ou non.

    >**Prise en main**: suivez hello [didacticiel d’Application Insights](../../application-insights/app-insights-overview.md).

-   **Moniteur de Azure**: un service qui vous permet de toovisualize, requête, route, archive et agir sur les métriques hello et les journaux générés par l’infrastructure Azure et vos ressources. Analyse fournit des vues de données hello que vous consultez Bonjour portail Azure et êtes une source unique pour l’analyse des ressources Azure.
 
    >**Démarrer** : [prenez en main Azure Monitor](../../monitoring-and-diagnostics/monitoring-get-started.md).

### <a name="devops-integration"></a>Intégration DevOps

S’il est mise en service des machines virtuelles ou publier vos applications web avec l’intégration continue, Azure s’intègre à la plupart des outils de DevOps hello populaires. Avec prise en charge des outils comme Jenkins, GitHub, Puppet, Chef, TeamCity, Ansible, VSTS et d’autres personnes, vous pouvez travailler avec les outils que vous avez déjà et optimisez votre expérience de hello.

>**Essayez dès maintenant :** [essayer plusieurs intégrations de DevOps hello](https://azure.microsoft.com/try/devops/).

>**Prise en main**: options de DevOps toosee pour une application de Service d’applications, consultez [tooAzure de déploiement continu du Service d’applications](../../app-service-web/app-service-continuous-deployment.md).


## <a name="azure-regions"></a>Régions Azure

Azure est une plateforme de nuage global qui est généralement disponible dans plusieurs régions monde hello. Lorsque vous configurez un service, une application ou une machine virtuelle dans Azure, vous êtes invité tooselect une région qui représente un centre de données spécifique sur lequel votre application s’exécute ou où sont stockées vos données. Ces régions correspondent à des emplacements de toospecific, qui sont publiés sur hello [régions Azure](https://azure.microsoft.com/regions/) page.

### <a name="choose-hello-best-region-for-your-application-and-data"></a>Choisir la région meilleures hello pour votre application et les données

Un des avantages de hello de l’utilisation d’Azure est que vous pouvez déployer vos centres de données toovarious applications monde hello. région de Hello que vous choisissez peut affecter les performances de hello de votre application. Par exemple, il est mieux toochoose une région toomost proche de votre latence tooreduce de clients dans les demandes réseau. Vous pouvez également vous tooselect votre région toomeet hello juridique configuration requise pour la distribution de votre application dans certains pays. Il est toujours une données d’application toostore meilleure pratique dans hello même centre de données ou dans un centre de données plus près possible toohello le centre de données qui héberge votre application.

### <a name="multi-region-apps"></a>Applications multirégions

Bien qu’improbable, il n’est pas impossible pour un toogo de centre de données entier en mode hors connexion en raison d’un événement tel qu’une catastrophe naturelle ou l’échec de l’Internet. Il s’agit d’une meilleure pratique toohost les applications professionnelles essentielles dans plusieurs centres de données tooprovide assurer une disponibilité maximale. L’utilisation de plusieurs régions peut également réduire la latence pour les utilisateurs internationaux et fournir une flexibilité supplémentaire lors des mises à jour d’applications.

Certains services, tels que les machines virtuelles et Services d’application, utilisent [Azure Traffic Manager](../../traffic-manager/traffic-manager-overview.md) prise en charge de plusieurs régions tooenable avec basculement entre les applications d’entreprise à haute disponibilité régions toosupport. Pour en voir un exemple, consultez [Architecture de référence Azure : application web à haute disponibilité](../../guidance/guidance-web-apps-multi-region.md).

>**Lorsque toouse**: lorsque vous avez des applications enterprise et haute disponibilité qui bénéficient de la réplication et de basculement.

## <a name="how-do-i-manage-my-applications-and-projects"></a>Comment gérer applications et projets ?

Azure fournit un ensemble complet de nouvelles expériences toocreate et gérer vos ressources Azure, les applications et les projets, par programme et Bonjour [portail Azure](https://portal.azure.com/).

### <a name="command-line-interfaces-and-powershell"></a>Interfaces de ligne de commande et PowerShell

Azure fournit deux façons toomanage vos applications et services à partir de la ligne de commande hello à l’aide d’un interpréteur de commandes, Terminal Server, invite de commandes hello ou votre outil de ligne de commande de choix. En règle générale, vous pouvez effectuer hello même tâches à partir de la ligne de commande hello comme hello portail Azure, telles que la création et la configuration des machines virtuelles, les réseaux virtuels, les applications web et les autres services.

-   [Azure Interface de ligne de commande (CLI)](../../xplat-cli-install.md): vous permet de vous connecter tooan abonnement Azure et de programmer des tâches différentes par rapport à des ressources Azure à partir de la ligne de commande hello.

-   [Azure PowerShell](../../powershell-install-configure.md): fournit un ensemble de modules avec les applets de commande qui vous toomanage Azure ressources à l’aide de Windows PowerShell.

### <a name="azure-portal"></a>Portail Azure

Hello portail Azure est une application web que vous pouvez utiliser toocreate, gérer et supprimer des services et des ressources Azure. Hello portail Azure se trouve dans <https://portal.azure.com>. Elle inclut un tableau de bord personnalisable, des outils pour la gestion des ressources Azure et les paramètres d’accès toosubscription et les informations de facturation. Pour plus d’informations, consultez hello [vue d’ensemble du portail Azure](../../azure-portal-overview.md).

### <a name="rest-apis"></a>API REST

Azure repose sur un ensemble d’API REST qui prennent en charge hello interface utilisateur du portail Azure. La plupart de ces API REST sont également pris en charge toolet configurer et gérer vos ressources Azure et les applications à partir de n’importe quel appareil activées pour Internet par programmation. Pour un jeu complet de hello de documentation de l’API REST, consultez hello [référence SDK REST de Azure](https://docs.microsoft.com/rest/api/).

### <a name="apis"></a>API

En outre tooREST API, de nombreux services Azure également vous permettent de gérer par programmation des ressources à partir de vos applications à l’aide spécifique à la plateforme Azure SDK, y compris les kits de développement logiciel pour hello suivant des plateformes de développement :

-   [.NET](https://go.microsoft.com/fwlink/?linkid=834925)
-   [Node.JS](http://azure.github.io/azure-sdk-for-node/)
-   [Java](https://docs.microsoft.com/java/api/)
-   [PHP](https://github.com/Azure/azure-sdk-for-php/blob/master/README.md)
-   [Python](http://azure-sdk-for-python.readthedocs.io/en/latest/)
-   [Ruby](https://github.com/Azure/azure-sdk-for-ruby/blob/master/README.md)

Les services tels que [Mobile Apps](../../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md) et [Azure Media Services](../../media-services/media-services-dotnet-how-to-use.md) fournissent toolet de kits de développement logiciel côté client vous accédez aux services à partir d’applications web et client mobile.

### <a name="azure-resource-manager"></a>Azure Resource Manager 
    
Exécutez votre application sur Azure probablement implique de travailler avec plusieurs services Azure, tous de qui suivent hello vie même cycle et peut être considéré comme une unité logique. Par exemple, une application web peut utiliser Web Apps, SQL Database, Stockage, Cache Redis Azure et les services Azure Content Delivery Network. [Le Gestionnaire de ressources Azure](../../azure-resource-manager/resource-group-overview.md) permet de travailler avec les ressources hello dans votre application en tant que groupe. Vous pouvez déployer, mettre à jour ou supprimer toutes les ressources hello dans une opération unique et coordonnée.

En outre toologically grouper et gérer des ressources associées, Azure Resource Manager inclut les fonctionnalités de déploiement qui vous permettent de personnaliser le déploiement de hello et la configuration de ressources liées. Par exemple, Resource Manager vous permet de déployer et de configurer une application qui se compose de plusieurs machines virtuelles, d’un équilibreur de charge et d’une base de données SQL Azure, comme une unité unique.

Vous développez ces déploiements à l’aide d’un modèle Azure Resource Manager, qui est un document au format JSON. Les modèles vous permettent de définir un déploiement et de gérer vos applications à l’aide de modèles déclaratifs, plutôt que de scripts. Vos modèles peuvent fonctionner pour différents environnements, par exemple des environnements de test, de préproduction et de production. Par exemple, à l’aide de modèles, vous pouvez ajouter un bouton tooa du référentiel GitHub qui déploie le code hello dans jeu de tooa hello référentiel des services Azure avec un seul clic.

>**Lorsque toouse**: utilisez le Gestionnaire de ressources modèles lorsque vous souhaitez un déploiement basé sur un modèle pour votre application que vous pouvez gérer par programme à l’aide de l’API REST, hello CLI d’Azure et d’Azure PowerShell.

>**Prise en main**: tooget démarré à l’aide de modèles, consultez [les modèles de programmation Azure Resource Manager](../../resource-group-authoring-templates.md).

## <a name="understanding-accounts-subscriptions-and-billing"></a>Présentation des comptes, des abonnements et de la facturation

En tant que développeurs, nous comme toodive directement dans le code de hello et essayez tooget démarré aussi rapidement que possible de rendre nos applications de s’exécuter. Nous voulons certainement tooencourage toostart fonctionne dans Azure, aussi facilement que possible. toohelp rendent facile, Azure offre une [version d’évaluation gratuite](https://azure.microsoft.com/free/). Certains services même ont une fonctionnalité « Essayez gratuitement », comme [Azure App Service](https://tryappservice.azure.com/), qui ne nécessite pas trop même créer un compte. Aussi amusant toodive dans le codage et le déploiement de votre application tooAzure, il est également important tootake certains toounderstand temps fonctionne d’Azure à partir d’un point de vue de facturation, les abonnements et les comptes d’utilisateur.

### <a name="what-is-an-azure-account"></a>Qu’est-ce qu’un compte Azure ?

toocreate en mesure de toobe ou de travail avec un abonnement Azure, vous devez disposer d’un compte Azure. Un compte Azure est simplement une identité dans Azure AD ou dans un annuaire, telle qu’une organisation professionnelle ou un établissement scolaire, qui est approuvée par Azure AD. Si vous n’appartenez toosuch une organisation, vous pouvez toujours créer un abonnement à l’aide de votre Account Microsoft, qui est approuvé par Azure AD. toolearn plus sur l’intégration d’Active Directory sur site Windows Server avec Azure AD, consultez [intégrer vos identités locales avec Azure Active Directory](../../active-directory/active-directory-aadconnect.md).

Chaque abonnement Azure dispose d’une relation d’approbation avec une instance Azure AD. Cela signifie qu’il approuve ce tooauthenticate Active les utilisateurs, les services et les périphériques. Plusieurs abonnements peuvent approuver hello même répertoire, mais un abonnement fait confiance à un seul répertoire. toolearn, voir [les abonnements Azure sont associés à Azure Active Directory](../../active-directory/active-directory-how-subscriptions-associated-directory.md).

En plus des identités toodefining compte Azure individuel, également appelé *utilisateurs*, vous pouvez également définir *groupes* dans Azure AD. Création de groupes d’utilisateurs d’est une tooresources d’accès toomanage bon moyen d’un abonnement à l’aide du contrôle d’accès basé sur un rôle (RBAC). toolearn toocreate groupes, voir [créer un groupe dans la version préliminaire d’Azure Active Directory](../../active-directory/active-directory-groups-create-azure-portal.md). Vous pouvez également créer et gérer des groupes en [utilisant PowerShell](../../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md).

### <a name="manage-your-subscriptions"></a>Gérer vos abonnements

Un abonnement est une unité logique de services Azure qui est lié tooan compte Azure. Chaque compte associé a un rôle dans un abonnement. La facturation des services Azure est effectuée par abonnement. Pour obtenir la liste des offres d’abonnement disponibles hello par type, consultez [détails de l’offre Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/).

#### <a name="administrator-roles"></a>Rôles d’administrateur

Un abonnement Azure a plusieurs rôles d’administrateur de compte que vous pouvez assigner à tout moment.

-   **Administrateur de compte**: ce rôle dispose du contrôle total sur les abonnement hello et est hello compte qui est responsable de la facturation.

-   **Administrateur de service**: ce rôle a un contrôle sur tous les services hello dans l’abonnement de hello. Par défaut, il s’agit hello même compte comme hello administrateur de compte.

-   **Coadministrateur**: ce rôle a hello même accéder en tant que hello administrateur de Service, sauf qu’il ne peut pas modifier association hello de hello abonnement tooan annuaire Azure.

toolearn savoir plus sur les rôles d’administrateur, consultez [comment tooadd ou modifier les rôles administrateur Azure](../../billing/billing-add-change-azure-subscription-administrator.md#add-an-admin-for-a-subscription).

#### <a name="resource-groups"></a>Groupes de ressources

Lorsque vous configurez de nouveaux services Azure, vous le faites dans le cadre d’un abonnement donné. Différents services Azure, qui sont également appelées ressources, sont créés dans le contexte de hello d’un groupe de ressources. Groupes de ressources rendent toodeploy plus facile et gérer les ressources de votre application. Un groupe de ressources doit contenir toutes les ressources hello pour votre application souhaité toowork avec en tant qu’unité. Vous pouvez déplacer des ressources entre les groupes de ressources et même toodifferent abonnements. toolearn sur le déplacement de ressources, consultez [déplacer le groupe de ressources toonew ressources ou d’un abonnement](../../resource-group-move-resources.md).

Hello Explorateur de ressources Azure est un excellent outil pour visualiser les ressources hello que vous avez déjà créé dans votre abonnement. toolearn, voir [tooview d’utiliser l’Explorateur de ressources Azure et modifier des ressources](../../resource-manager-resource-explorer.md).

#### <a name="grant-access-tooresources"></a>Accorder l’accès tooresources

Lorsque vous autorisez l’accès tooAzure ressources, il est toujours d’une meilleure pratique de fournir aux utilisateurs avec hello moindre privilège qui tooperform requis une tâche donnée.

-   **Contrôle d’accès basé sur un rôle (RBAC)**: dans Azure, vous pouvez accorder l’accès des comptes toouser (principaux) dans une étendue spécifiée : abonnement, groupe de ressources ou des ressources individuelles. RBAC vous permet de déployer un ensemble de ressources dans un groupe de ressources et d’accorder des autorisations tooa utilisateur ou groupe spécifique. Il vous permettre également de limiter l’accès tooonly hello ressources qui font partie du groupe de ressources cible toohello. Vous pouvez également accorder l’accès tooa seule ressource, tel qu’un ordinateur virtuel ou d’un réseau virtuel. l’accès toogrant, attribuer un rôle toohello utilisateur, groupe ou principal du service. Il existe de nombreux rôles prédéfinis et vous pouvez également définir vos propres rôles personnalisés.

    >**Lorsque toouse**: lorsque vous devez la gestion de l’accès affinée pour les utilisateurs et groupes.

    >**Prise en main**: toolearn, voir [commencer avec la gestion des accès Bonjour Azure portal](../../active-directory/role-based-access-control-what-is.md).

-   **Objets principales de service**: tooproviding en outre accéder à toouser principaux et des groupes, vous pouvez accorder hello même principal du service accès tooa.

    > **Lorsque toouse**: lorsque vous utilisez la gestion des ressources Azure par programme ou accorder l’accès pour les applications. Pour plus d’informations, consultez [Créer une application Active Directory et un principal de service](../../resource-group-create-service-principal-portal.md).

#### <a name="tags"></a>Tags

Le Gestionnaire de ressources Azure vous permet d’affecter des balises personnalisées tooindividual ressources. Balises, qui sont des paires clé-valeur, peuvent être utiles lorsque vous avez besoin des ressources de tooorganize de facturation et d’analyse. Balises vous fournissent un moyen des ressources de tootrack sur plusieurs groupes de ressources. Vous pouvez affecter des balises dans le portail hello, dans le modèle de gestionnaire de ressources Azure hello, ou par programme, à l’aide de hello API REST, hello CLI d’Azure ou PowerShell. Vous pouvez affecter plusieurs balises tooeach ressource. toolearn, voir [à l’aide des balises tooorganize vos ressources Azure](../../resource-group-using-tags.md).

### <a name="billing"></a>Facturation

Dans move hello informatique de services hébergés toocloud sur site, le suivi et l’estimation de l’utilisation du service et les coûts associés sont des préoccupations importantes. Il est important toobe les tooestimate en mesure des nouvelles ressources coûts toorun sur une base mensuelle. Vous devez également tooproject en mesure de toobe aspect de la facturation de hello pour un mois donné, en fonction de dépense actuelle hello.

#### <a name="get-resource-usage-data"></a>Obtenir les données d’utilisation des ressources

Azure fournit un ensemble d’API REST de facturation qui donnent accès tooresource consommation et des informations de métadonnées pour les abonnements Azure. Ces permettent d’API de facturation hello de capacité toobetter prédire et gérer les coûts de Azure. Vous pouvez effectuer le suivi et l’analyse des dépenses par incréments horaires, créer des alertes de dépenses et prévoir la facturation à venir en fonction des tendances d’utilisation actuelles.

>**Prise en main**: toolearn plus sur l’utilisation de hello API de facturation, consultez [vue d’ensemble de l’utilisation de facturation d’Azure et RateCard APIs](../../billing-usage-rate-card-overview.md).

#### <a name="predict-future-costs"></a>Prédire les coûts futurs

Bien qu’il est difficile de coûts tooestimate avance, Azure a un [calculatrice de prix](https://azure.microsoft.com/pricing/calculator/) que vous pouvez utiliser lorsque vous estimez le coût de hello de déployé des ressources. Vous pouvez également utiliser le panneau de facturation hello dans portail de hello et hello de facturation des API REST tooestimate les coûts futurs, en fonction de la consommation actuelle.

>**Démarrer** : consultez [Vue d’ensemble des API de facturation Azure et RateCard](../../billing-usage-rate-card-overview.md).

#### <a name="set-up-billing-alerts"></a>Configurer des alertes de facturation

Une fois que vous avez déployé votre application ou votre solution sur Azure, vous pouvez créer des alertes qui vous envoyer un que courriel lorsque vous approcher hello limites sont définies dans l’alerte de hello de dépense.

>**Prise en main**: toolearn, voir [configurer la facturation des alertes pour vos abonnements Microsoft Azure](../../billing-set-up-alerts.md).
