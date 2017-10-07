---
title: "aaaAzure comparaison du Service d’applications, les ordinateurs virtuels, les Service Fabric et les Services de cloud computing | Documents Microsoft"
description: "Découvrez comment toochoose entre le Service d’applications Azure, Machines virtuelles, Service Fabric et les Services de Cloud pour l’hébergement des applications web."
services: app-service\web, virtual-machines, cloud-services
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 7d346a23-532a-42a9-98a8-23b7286d32a8
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 07/07/2016
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 7577332ed049df66178c7b2cd5c440a7f93a7865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-virtual-machines-service-fabric-and-cloud-services-comparison"></a>Comparaison entre Azure App Service, Virtual Machines, Service Fabric et Cloud Services
## <a name="overview"></a>Vue d'ensemble
Azure offre plusieurs moyens de sites web de toohost : [Azure App Service][Azure App Service], [virtuels][Virtual Machines], [Service Fabric ] [ Service Fabric], et [Services de cloud computing][Cloud Services]. Cet article vous aidera à comprendre les options de hello et faire hello bon choix pour votre application web.

Azure App Service est hello meilleur choix pour la plupart des applications web. Déploiement et gestion sont intégrés dans la plateforme de hello, sites peuvent évoluer rapidement les charges de trafic élevé de toohandle et le Gestionnaire de trafic et de l’équilibrage de charge intégrés hello fournit une haute disponibilité. Vous pouvez déplacer existant sites tooAzure du Service d’applications facilement grâce à une [l’outil de migration en ligne](https://www.migratetoazure.net/), utiliser une application open source à partir de la galerie d’applications Web de hello ou créer un nouveau site à l’aide du framework de hello et les outils de votre choix. Hello [WebJobs] [ WebJobs] fonctionnalité, il est facile tooadd arrière-plan travail traitement tooyour application Service web d’application.

Service Fabric est un bon choix si vous créez une nouvelle application ou réécrire une application existante toouse une architecture de microservice. Les applications qui s’exécutent sur un pool de machines, peuvent commencer petites et augmenter l’échelle toomassive avec des centaines, voire des milliers d’ordinateurs en fonction des besoins. Services avec état rendent tooconsistently facile et fiable stocker l’état de l’application, et l’infrastructure de Service gère automatiquement la partition du service, la mise à l’échelle et la disponibilité pour vous.  Service Fabric prend également en charge WebAPI avec Open Web Interface for .NET (OWIN) et ASP.NET Core.  Comparés tooApp Service, Service Fabric fournit également plus contrôler, ou un accès direct à infrastructure sous-jacente de hello. Vous pouvez accéder à distance à vos serveurs ou configurer des tâches de démarrage du serveur. Services de cloud computing similaire tooService infrastructure dans le degré de contrôle par rapport à la facilité d’utilisation, mais il est désormais un service hérité et Service Fabric est recommandée pour tout nouveau développement.

Si vous avez une application existante qui nécessiterait toorun de modifications substantielles dans le Service d’applications ou de l’infrastructure de Service, vous pouvez choisir les Machines virtuelles pour toosimplify commande migration toohello cloud. Toutefois, la configuration correcte, sécurisation et la maintenance des ordinateurs virtuels nécessitent beaucoup plus de temps et expertise informatique comparé tooAzure du Service d’applications et l’infrastructure de Service. Si vous envisagez de Machines virtuelles Azure, veillez à prendre en compte hello maintenance continue effort requis toopatch, mettre à jour et gérer votre environnement de machine virtuelle. Les machines virtuelles Azure sont de type Infrastructure en tant que service (Infrastructure-as-a-Service, (IaaS)), tandis que App Service et Service Fabric sont de type plateforme en tant que service (Platform-as-a-Service (Paas)). 

## <a name="features"></a>Comparaison des fonctionnalités
Hello tableau suivant compare les fonctionnalités de hello du Service d’applications, Services de cloud computing, Machines virtuelles et Service Fabric toohelp vous choisir hello mieux. Pour plus d’informations sur hello SLA pour chaque option, consultez [les contrats de niveau de Service Azure](https://azure.microsoft.com/support/legal/sla/).

| Fonctionnalité | Azure App Service (applications web) | Azure Cloud Services (rôles Web) | Machines virtuelles | Service Fabric | Remarques |
| --- | --- | --- | --- | --- | --- |
| Déploiement presque instantané |X | | |X |Déployer une application ou un tooa de mise à jour d’application Service Cloud ou la création d’une machine virtuelle, prend quelques minutes, au moins ; déploiement d’une application de web application tooa prend quelques secondes. |
| Mettre à l’échelle des ordinateurs toolarger sans redéploiement |X | | |X | |
| Les instances de serveur Web partagent du contenu et configuration, ce qui signifie que vous n’avez tooredeploy ou reconfigurer la mise à l’échelle. |X | | |X | |
| Plusieurs environnements de déploiement (de production et intermédiaire) |X |X | |X |L’infrastructure de service vous permet de toohave plusieurs environnements pour vos applications ou les toodeploy différentes versions de votre application côte à côte. |
| Gestion automatique des mises à jour du système d'exploitation |X |X | | |Des mises à jour automatiques du système d’exploitation sont planifiées dans une version Service Fabric à venir. |
| Migration transparente entre les plateformes (de 32 à 64 bits) |X |X | | | |
| Déploiement de code avec GIT, FTP |X | |X | | |
| Déploiement de code avec Web Deploy |X | |X | |Cloud Services prend en charge hello Web Deploy toodeploy mises à jour tooindividual d’instances de rôle. Toutefois, vous ne pouvez pas l’utiliser pour le déploiement initial d’un rôle, et si vous utilisez Web Deploy pour une mise à jour que toodeploy séparément instance tooeach d’un rôle. Plusieurs instances sont requises dans tooqualify ordre pour hello Cloud Service SLA pour les environnements de production. |
| Prise en charge de WebMatrix |X | |X | | |
| Accès tooservices comme Service Bus, stockage, base de données SQL |X |X |X |X | |
| Hébergement des services Web ou niveaux d'une architecture multiniveau |X |X |X |X | |
| Hébergement du niveau intermédiaire d'une architecture multiniveau |X |X |X |X |Applications de Service d’applications web peuvent facilement héberger un intermédiaire de l’API REST et hello [WebJobs](http://go.microsoft.com/fwlink/?linkid=390226) fonctionnalité peut héberger des travaux de traitement en arrière-plan. Vous pouvez exécuter des tâches Web dans une évolutivité indépendante tooachieve de site Web dédié pour le niveau de hello. Aperçu de Hello [applications API](../app-service-api/app-service-api-apps-why-best-platform.md) fonctionnalité fournit davantage de fonctionnalités pour l’hébergement de services REST. |
| Prise en charge intégrée de MySQL-as-a-service |X |X |X | |Services de cloud computing peuvent intégrer MySQL-as-a-service via les offres de ClearDB, mais pas dans le cadre du flux de travail hello portail Azure. |
| Prise en charge d'ASP.NET, d'ASP, de Node.js, de PHP et de Python |X |X |X |X |L’infrastructure de service prend en charge la création de hello d’un frontal web à l’aide [ASP.NET 5](../service-fabric/service-fabric-add-a-web-frontend.md) ou vous pouvez déployer tout type d’application (Node.js, Java, etc.) comme un [exécutable invité](../service-fabric/service-fabric-deploy-existing-app.md). |
| Montée en puissance parallèle toomultiple instances sans redéploiement |X |X |X |X |Machines virtuelles peuvent monter en charge les instances de toomultiple, mais les services hello en cours d’exécution sur ces derniers doivent être écrites toohandle ce montée en puissance parallèle. Vous avez tooconfigure les demandes de tooroute d’un équilibrage de charge sur plusieurs ordinateurs de hello et créez un groupe d’affinités de tooprevent simultanées redémarrages de toutes les instances en raison de défaillances toomaintenance ou du matériel. |
| Prise en charge de SSL |X |X |X |X |Pour les applications web App Service, le protocole SSL pour les noms de domaine personnalisés est pris en charge uniquement en mode De base et Standard. Pour plus d’informations sur l’utilisation de SSL avec les applications web, consultez la page [Configuration d’un certificat SSL pour un site web Azure](app-service-web-tutorial-custom-ssl.md). |
| Intégration de Visual Studio |X |X |X |X | |
| Débogage à distance |X |X |X | | |
| Déploiement de code avec TFS |X |X |X |X | |
| Isolation du réseau avec [Azure Virtual Network](/azure/virtual-network/) |X |X |X |X |Voir aussi [Intégration au réseau virtuel de Sites Web Azure](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/) |
| Prise en charge d' [Azure Traffic Manager](/azure/traffic-manager/) |X |X |X |X | |
| Surveillance intégrée des points de terminaison |X |X |X | | |
| Accès Bureau à distance tooservers | |X |X |X | |
| Installez n'importe quel MSI personnalisé | |X |X |X |L’infrastructure de service vous permet de toohost fichier de tout fichier exécutable sous un [exécutable invité](../service-fabric/service-fabric-deploy-existing-app.md) ou vous pouvez installer n’importe quelle application sur des machines virtuelles de hello. |
| Tâches de démarrage et d’exécution toodefine capacité | |X |X |X | |
| Peut écouter des événements de tooETW | |X |X |X | |

## <a name="scenarios"></a>Scénarios et recommandations
Voici quelques scénarios d’application courants avec les recommandations comme option d’hébergement toowhich web Azure peut être plus appropriée pour chaque.

* [J’ai besoin d’un serveur web frontal avec traitement en arrière-plan et les applications d’entreprise de base de données principales toorun intégrées à des ressources locales.](#onprem)
* [J’ai besoin d’un toohost de façon fiable atteindre de mon site Web d’entreprise qui s’adapte la barre d’outils et des offres globales.](#corp)
* [J’ai une application IIS6 qui s’exécute sur Windows Server 2003.](#iis6)
* [Je suis un propriétaire de petite entreprise, et je dois un toohost de façon économique de mon site, mais avec une croissance future à l’esprit.](#smallbusiness)
* [Je suis un site ou un concepteur graphique, et souhaitez toodesign et de la génération de sites web pour mes clients.](#designer)
* [Je migre mon application à plusieurs niveaux avec un Cloud de toohello frontal web.](#multitier)
* [Mon application dépend de Windows hautement personnalisé ou environnements Linux et souhaitez toomove il toohello cloud.](#custom)
* [Mon site utilise des logiciels open source et vous voulez toohost dans Azure.](#oss)
* [Je dispose d’une application métier-dont a besoin de réseau d’entreprise de tooconnect toohello.](#lob)
* [Je veux toohost un service web ou les API REST pour les clients mobiles.](#mobile)

### <a id="onprem"></a>J’ai besoin d’un serveur web frontal avec traitement en arrière-plan et les applications d’entreprise de base de données principales toorun intégrées à des ressources locales.
Azure App Service est une excellente solution pour l’hébergement d’applications métier complexes. Il vous permet de développer des applications qui l’échelle automatiquement sur une plateforme à charge équilibrée de charge, sont sécurisées avec Active Directory et connectez tooyour des ressources locales. Il vous permet de gérer ces applications faciles via une API et portail premier ordre et vous permet de toogain idée comment les clients utilisent les avec les outils d’application insight. Hello [Webjobs] [ Webjobs] fonctionnalité vous permet d’exécuter des processus d’arrière-plan et les ressources du précédent tooon local tooconnect facile rendent les tâches dans le cadre de votre couche web, lors de la connectivité hybride et les fonctionnalités de réseau virtuel. Azure App Service offre des contrats SLA pour des applications web à 0,001 % d’erreur et offre les possibilités suivantes :

* Exécution fiable de vos applications sur une plateforme cloud avec corrections et mises à jour automatiques.
* Extension automatique sur un réseau mondial de centres de données.
* Sauvegarde et restauration après sinistre.
* Conformité ISO, SOC2 et PCI.
* Intégration avec Active Directory

### <a id="corp"></a>J’ai besoin d’un toohost de façon fiable atteindre de mon site Web d’entreprise qui s’adapte la barre d’outils et des offres globales.
Azure App Service est une excellente solution pour l’hébergement de sites web d’entreprise. Il tooscale d’applications web rapidement et facilement toomeet la demande sur un réseau mondial de centres de données. Il offre un lien local, une grande tolérance aux pannes et une gestion intelligente du trafic. Sur une plateforme qui fournit des outils de gestion de classe mondiale, ce qui vous toogain approfondie d’intégrité du site et du trafic du site rapidement et facilement. Azure App Service offre des contrats SLA pour des applications web à 0,001 % d’erreur et offre les possibilités suivantes :

* Exécution fiable de vos sites web sur une plateforme cloud avec corrections et mises à jour automatiques.
* Extension automatique sur un réseau mondial de centres de données.
* Sauvegarde et restauration après sinistre.
* Gestion des journaux et du trafic avec des outils intégrés.
* Conformité ISO, SOC2 et PCI.
* Intégration avec Active Directory

### <a id="iis6"></a> J’ai une application IIS6 qui s’exécute sur Windows Server 2003.
Azure App Service rend facile tooavoid hello des coûts d’infrastructure associés à migrer des applications IIS6 plus anciens. Microsoft a créé [toouse facilement les outils de migration et les instructions de migration détaillées](https://www.movemetowebsites.net/) qui vous toocheck compatibilité et d’identifier les modifications qui doivent toobe effectuée. Intégration avec Visual Studio, TFS et les outils courants CMS rend facile toodeploy IIS6 applications directement toohello cloud. Une fois déployé, hello portail Azure fournit des outils de gestion fiable qui vous tooscale les coûts de toomanage et à la demande toomeet selon les besoins. Avec l’outil de migration hello, vous pouvez :

* Rapidement et facilement migrer vos hérité toohello cloud de Windows Server 2003 web application.
* S’abonner tooleave votre toocreate local de base de données attaché SQL une application hybride.
* Déplacer automatiquement votre base de données SQL avec votre application héritée.

### <a id="smallbusiness"></a>Je suis un propriétaire de petite entreprise, et je dois un toohost de façon économique de mon site, mais avec une croissance future à l’esprit.
Azure App Service est une solution idéale dans ce scénario, car vous pouvez démarrer gratuitement, puis ajouter gratuitement des fonctionnalités supplémentaires en fonction de vos besoins. Chaque application web gratuit est fourni avec un domaine fourni par Azure (*votre_société*. azurewebsites.net), et la plateforme de hello inclut des outils de déploiement et de gestion intégrés ainsi que d’une galerie d’applications qui la rendent facile tooget a démarré. Il existe de nombreux autres services et les options de mise à l’échelle qui tooevolve de site hello avec à la demande de l’utilisateur. Avec Azure App Service, vous pouvez effectuer les tâches suivantes :

* Commencer par gratuit hello et ensuite évoluer en fonction des besoins.
* Utilisez tooquickly de galerie d’applications hello configurer des applications web populaires, telles que WordPress.
* Ajouter application supplémentaire de tooyour de fonctionnalités et des services Windows Azure en fonction des besoins.
* Sécurisez votre application web avec le protocole HTTPS.

### <a id="designer"></a>Je suis un site ou un concepteur graphique, et souhaitez toodesign et de la création de sites Web pour mes clients
Pour les développeurs web et les graphistes, Azure App Service s’intègre facilement à de nombreuses infrastructures et à de nombreux outils. Il comprend la prise en charge du déploiement avec Git et FTP et offre une excellente intégration à des outils et services tels que Visual Studio et Base de données SQL. Avec App Service, vous pouvez :

* utiliser les outils en ligne de commande pour les [tâches automatisées][scripting] ;
* utiliser des langages reconnus tels que [.Net][dotnet], [PHP][PHP], [Node.js][nodejs] et [Python][Python] ;
* Sélectionnez les trois niveaux de mise à l’échelle différents pour la mise à l’échelle des capacités de haute toovery.
* Intégration avec d’autres services Azure, tel que [base de données SQL][sqldatabase], [Service Bus] [ servicebus] et [stockage] [ Storage], ou un partenaire d’offres de hello [Azure Store][azurestore], tels que MySQL et MongoDB.
* Intégrer des outils tels que Visual Studio, Git, WebMatrix, WebDeploy, TFS et FTP.

### <a id="multitier"></a>Je migre mon application à plusieurs niveaux avec un toohello de frontal web Cloud
Si vous exécutez une application multicouche, tel qu’un serveur web qui se connecte à base de données tooa, Azure App Service est une bonne option qui offre une intégration étroite avec la base de données SQL Azure. Et vous pouvez utiliser la fonctionnalité de tâches Web hello pour l’exécution des processus principaux.

Choisissez le Service Fabric pour l’une ou plusieurs de vos niveaux si vous avez besoin de plus de contrôlent sur l’environnement de serveur hello, telles que tooremote de capacité hello dans votre serveur ou configurer les tâches de démarrage du serveur.

Choisissez les ordinateurs virtuels pour un ou plusieurs des niveaux de votre si vous souhaitez toouse votre propre image de machine ou exécuter le logiciel serveur ou les services que vous ne pouvez pas configurer sur l’infrastructure de Service.

### <a id="custom"></a>Mon application dépend de Windows hautement personnalisé ou environnements Linux et souhaitez toomove il toohello cloud.
Si votre application nécessite l’installation complexe ou la configuration logicielle et hello système d’exploitation, les ordinateurs virtuels est probablement hello meilleure solution. Virtual Machines vous permet d'effectuer les opérations suivantes :

* Utilisez toostart de la galerie de Machine virtuelle hello avec un système d’exploitation, tels que Windows ou Linux et ensuite les personnaliser en fonction de spécifications de votre application.
* Créez et téléchargez une image personnalisée d’un toorun de serveur local existant sur un ordinateur virtuel dans Azure.

### <a id="oss"></a>Mon site utilise des logiciels open source et vous voulez toohost dans Azure
Si votre infrastructure open source qui est pris en charge sur le Service d’application, les langues hello et infrastructures requises par votre application sont configurées automatiquement pour vous. Avec App Service, vous pouvez :

* utiliser de nombreux langages open source reconnus tels que [.NET][dotnet], [PHP][PHP], [Node.js][nodejs] et [Python][Python] ;
* configurer WordPress, Drupal, Umbraco, DNN et de nombreuses autres applications web tierces.
* Migrer une application existante ou créez-en un à partir de la galerie d’applications de hello.

Si votre infrastructure open source qui n’est pas pris en charge sur le Service d’applications, vous pouvez l’exécuter sur l’un des hello autres options d’hébergement de web Azure. Avec les Machines virtuelles, vous installer et configurer hello logiciel sur l’image de machine hello, qui peut être Windows ou Linux.

### <a id="lob"></a>J’ai une application métier-dont a besoin de réseau d’entreprise de tooconnect toohello
Si vous souhaitez toocreate une application de gestion, votre site Web peut nécessiter un accès direct tooservices ou des données sur le réseau d’entreprise de hello. Cela est possible sur le Service d’applications, Service Fabric et Machines virtuelles à l’aide de hello [service de réseau virtuel Azure](/azure/virtual-network/). Sur le Service d’applications, vous pouvez utiliser hello [fonctionnalité d’intégration de réseau virtuel](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/), qui permet de toorun de vos applications Azure comme s’ils étaient sur votre réseau d’entreprise.

### <a id="mobile"></a>Je veux toohost un service web ou les API REST pour les clients mobiles
Services web basés sur HTTP activer toosupport un large éventail de clients, y compris les clients mobiles. Infrastructures comme l’API Web ASP.NET intégrant avec Visual Studio toomake toocreate plus facile et consomment des services REST.  Ces services sont exposées à partir d’un point de terminaison web, afin qu’il soit possible de toouse un hébergement technique sur Azure toosupport ce scénario web. App Service constitue un choix idéal pour l’hébergement des API REST. Avec App Service, vous pouvez :

* Créez rapidement un [application mobile](../app-service-mobile/app-service-mobile-value-prop.md) ou [application API](../app-service-api/app-service-api-apps-why-best-platform.md) service de web toohost hello HTTP dans un des centres de données distribués internationalement d’Azure.
* migrer des services existants ou en créer de nouveaux.
* Obtenir le contrat SLA de disponibilité avec une instance unique ou monter en charge les ordinateurs toomultiple dédié.
* Hello d’utilisation publié site tooprovide API REST tooany clients HTTP, y compris les clients mobiles.

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte, accédez trop<a href="https://trywebsites.azurewebsites.net/">https://trywebsites.azurewebsites.net</a>, où vous pouvez immédiatement créer une application de démarrage de courte durée de vie dans Azure App Service gratuit. Aucune carte de crédit n’est requise, vous ne prenez aucun engagement.
> 
> 

## <a id="nextsteps"></a> Étapes suivantes
Pour plus d’informations sur le web hello trois options d’hébergement, consultez [Introduction à Azure](../fundamentals-introduction-to-azure.md).

tooget démarré avec les options de hello choisie pour votre application, consultez hello suivant des ressources :

* [Azure App Service](/azure/app-service/)
* [Azure Cloud Services](/azure/cloud-services/)
* [Azure Virtual Machines](/azure/virtual-machines/)
* [Service Fabric](/azure/service-fabric/)

<!-- URL List -->

[Azure App Service]: /azure/app-service/
[Cloud Services]: /azure/cloud-services/
[Virtual Machines]: /azure/virtual-machines/
[Service Fabric]: /azure/service-fabric/
[ClearDB]: http://www.cleardb.com/
[WebJobs]: http://go.microsoft.com/fwlink/?linkid=390226&clcid=0x409
[Configuring an SSL certificate for an Azure Website]: app-service-web-tutorial-custom-ssl.md
[azurestore]: https://azuremarketplace.microsoft.com/en-us/marketplace/apps
[scripting]: https://azure.microsoft.com/documentation/scripts/?services=web-sites
[dotnet]: https://azure.microsoft.com/develop/net/
[nodejs]: https://azure.microsoft.com/develop/nodejs/
[PHP]: https://azure.microsoft.com/develop/php/
[Python]: https://azure.microsoft.com/develop/python/
[servicebus]: /azure/service-bus/
[sqldatabase]: /azure/sql-database/
[Storage]: /azure/storage/

<!-- IMG List -->

[ChoicesDiagram]: ./media/choose-web-site-cloud-service-vm/Websites_CloudServices_VMs_3.png
