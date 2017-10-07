---
title: "la présentation de la sécurité de l’infrastructure du service aaaAzure | Documents Microsoft"
description: "Cet article fournit une vue d’ensemble de hello sécurité de l’infrastructure de service Azure."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: ec5355983c5d59f4e0c3b855965f03ac47f1a4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-overview"></a>Vue d’ensemble de la sécurité Azure Service Fabric
[Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) est une plateforme de systèmes distribués qui rend facile toopackage, déployer et gérer des micro-services fiables et évolutives. L’infrastructure de service traite des défis de hello dans le développement et la gestion des applications de cloud. Les développeurs et administrateurs sont en mesure d’éviter les problèmes d’infrastructure complexes et peuvent se concentrer sur l’implémentation de charges de travail stratégiques et exigeantes, évolutives, fiables et faciles à gérer.

Cet article de la présentation de la sécurité de l’infrastructure du Service Azure se concentre sur hello suivant de zones :

-   Sécurisation de votre cluster
-   Surveillance et diagnostics
-   Sécurisation à l’aide de certificats
-   Contrôle d’accès en fonction du rôle
-   Sécurisation du cluster à l’aide de la sécurité de Windows
-   Configuration de la sécurité de l’application dans Service Fabric
-   Sécurisation des communications pour les services dans la sécurité Azure Service Fabric

## <a name="securing-your-cluster"></a>Sécurisation de votre cluster
Azure Service Fabric est orchestrateur de services sur un cluster d’ordinateurs, les Clusters doivent être tooprevent sécurisé non autorisé les utilisateurs de se connecter tooyour cluster, surtout quand les charges de production en cours d’exécution sur ce dernier. Bien qu’il soit possible de toocreate un cluster non sécurisé, cela permet aux utilisateurs anonymes tooconnect tooit, s’il expose toohello de points de terminaison de gestion Internet public.

Cette section fournit une vue d’ensemble de hello des scénarios de sécurité pour les clusters en cours d’exécution sur Azure ou autonome et hello différentes technologies utilisées tooimplement ces scénarios. scénarios de sécurité du cluster Hello sont :

-   Sécurité nœud à nœud
-   Sécurité client à nœud

### <a name="node-to-node-security"></a>Sécurité nœud à nœud
Sécurise les communications entre les machines virtuelles de hello ou des ordinateurs dans un cluster de hello. Cela garantit que seuls les ordinateurs qui sont autorisés toojoin hello clusters peuvent participer hébergeant des applications et services de cluster de hello.

Les clusters qui s’exécutent sur Azure ou les clusters autonomes sur Windows peuvent utiliser la [Sécurité par certificat](https://msdn.microsoft.com/library/ff649801.aspx) ou la [Sécurité Windows](https://msdn.microsoft.com/library/ff649396.aspx) pour les ordinateurs Windows Server.

**Sécurité de certificat de nœud à nœud**

L’infrastructure de service utilise les certificats de serveur X.509 que vous spécifiez dans le cadre des configurations de nœud de type hello lorsque vous créez un cluster. Un rapide aperçu de ce que sont ces certificats et de la [façon dont vous pouvez les acquérir ou les créer est proposé dans cet article](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/working-with-certificates).

Sécurité de certificat est configurée lors de la création de cluster de hello via hello portail Azure, des modèles Azure Resource Manager ou un modèle JSON autonome. Vous pouvez spécifier un certificat primaire et un certificat secondaire facultatif utilisé pour les renouvellements de certificats. Hello certificats principaux et secondaires, vous spécifiez doivent être différents de celui de client d’administration hello et les certificats de client en lecture seule vous spécifiez pour [sécurité du Client au nœud](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security).

### <a name="client-to-node-security"></a>Sécurité client à nœud
Sécurité de toonode client est configurée à l’aide d’identification du Client. tooestablish d’approbation entre un client et hello du cluster, vous devez configurer hello cluster tooknow les identités de client qu’il peut faire confiance. Cette opération peut être réalisée de deux manières :

-   Spécifiez les utilisateurs du groupe domaine hello qui peuvent se connecter ou
-   Spécifiez les utilisateurs de nœud de domaine de hello qui peuvent se connecter.

L’infrastructure de service prend en charge deux types de contrôle d’accès différents pour les clients qui sont connectés tooa Service Fabric clusters :

-   Administrateur
-   Utilisateur

Contrôle d’accès permet hello hello cluster administrateur toolimit accès toocertain types d’opérations de cluster pour différents groupes d’utilisateurs, la sécurisation de cluster de hello. Les administrateurs disposent de fonctionnalités de toomanagement d’un accès complet (y compris les fonctionnalités en lecture/écriture). Les utilisateurs, par défaut, ont uniquement un accès en lecture toomanagement fonctionnalités (par exemple, les fonctions de requête), hello capacité tooresolve applications et services.

**Sécurité par certificat de client à nœud**

Sécurité du certificat du client à ce nœud est configurée lors de la création de cluster de hello via hello portail Azure, les modèles de gestionnaire de ressources ou d’un modèle JSON autonome en spécifiant un certificat de client d’administration et/ou d’un certificat client utilisateur. Hello administrateur client et l’utilisateur les certificats clients que vous spécifiez doivent être différentes de celle des certificats primaires et secondaires hello, que vous spécifiez pour la sécurité du nœud à l’autre.

Les clients se connectant cluster toohello à l’aide du certificat d’administration hello ont des fonctionnalités de toomanagement d’un accès complet. Les clients se connectant cluster toohello à l’aide du certificat de client utilisateur en lecture seule hello ont uniquement des fonctionnalités de toomanagement de l’accès en lecture. Dans un autre mot que ces certificats sont utilisés pour hello rôle de base de contrôle d’accès (RBAC).

Pour lire les Azure [configurer un cluster à l’aide d’un modèle Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) toolearn comment tooconfigure certificat de sécurité dans un cluster.

**Sécurité Azure Active Directory (AAD) de client-à-nœud sur Azure**

Les clusters en cours d’exécution sur Azure peuvent également sécuriser l’accès aux points de terminaison de gestion toohello à l’aide d’Azure Active Directory (AAD). Consultez [configurer un cluster à l’aide d’un modèle Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) pour plus d’informations sur la façon dont toocreate hello artefacts AAD nécessaires, comment toopopulate au cours de cluster la création, et comment tooconnect toothose clusters par la suite.

AAD permet aux organisations (appelées locataires) toomanage utilisateur accès tooapplications, qui sont réparties entre les applications avec une interface utilisateur de connexion basée sur le web et une expérience client natif.

Un cluster Service Fabric offre plusieurs tooits de points d’entrée des fonctionnalités de gestion, y compris hello basée sur le web Service Fabric Explorer et Visual Studio. Par conséquent, vous créez le cluster de deux accès AAD applications toocontrol toohello, une application web et une application native.
Pour les clusters Azure, il est recommandé d’utiliser AAD sécurité tooauthenticate clients et les certificats pour la sécurité du nœud à l’autre.

Pour les clusters Windows Server, nous vous recommandons d’utiliser la sécurité Windows avec des comptes gérés par des groupes (GMA) si vous avez Windows Server 2012 R2 et Active Directory. Sinon, continuez à utiliser la sécurité Windows avec les comptes Windows.

## <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>Surveillance et diagnostics pour Azure Service Fabric
[Analyse et diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-overview) sont critiques toodeveloping, tester et déployer des applications et des services dans n’importe quel environnement. Les solutions Service Fabric conviennent mieux pour planifier et implémenter une surveillance et des diagnostics afin de s’assurer que les applications et services fonctionnent comme prévu dans un environnement de développement local ou de production.

Du point de vue de la sécurité, hello principaux objectifs de l’analyse et diagnostics sont :

-   Détecter et diagnostiquer les problèmes de matériel et l’infrastructure qui peuvent être dû à des événements de sécurité tooa.
-   Détecter les problèmes de logiciel et d’applications pouvant indiquer une compromission.
-   Ressource de comprendre la consommation toohelp empêcher accidentelle de déni de service.

Hello workflow global de l’analyse et de diagnostics se compose de trois étapes :

-   **Génération d’événements :** inclut des événements (journaux, des traces, les événements personnalisés) à l’infrastructure hello (cluster) et de niveau application / service. En savoir plus sur [les événements de niveau infrastructure](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-infra) et [les événements de niveau application](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-app) toounderstand, ce qui est indiqué, et comment tooadd plus d’instrumentation.
-   **L’agrégation d’événements :** les événements générés doivent toobe collectées et agrégées avant d’être affichées. En général, nous recommandons d’utiliser [Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-wad) (collection de journal tooagent plus similaire) ou [EventFlow](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow) (en-processus de collecte de journaux).
-   **Analyse :** les événements doivent toobe visualisé et accessible dans le format ou certains tooallow pour l’analyse et l’affichage en fonction des besoins. Il existe plusieurs plateformes excellentes qui existent dans le marché de hello lorsqu’il s’agit d’analyse de toohello et la visualisation des données de surveillance et de diagnostic. Hello deux que nous recommandons sont [OMS](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-oms) et [Application Insights](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-appinsights) en raison de tootheir une meilleure intégration à l’infrastructure de Service.

Vous pouvez également utiliser [moniteur Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) toomonitor nombreux hello ressources Azure sur lequel un cluster Service Fabric est construit.

Une surveillance est un service séparé qui peut surveiller l’intégrité et la charge entre les services et le signalement d’intégrité pour n’importe où dans la hiérarchie du modèle d’intégrité hello. Cela peut aider à éviter les erreurs qui ne sont pas détectées en fonction de la vue hello d’un service unique. Agents de surveillance sont également un bon endroit toohost code qui effectue des actions correctives sans intervention de l’utilisateur (par exemple, le nettoyage des fichiers journaux dans le stockage à intervalles réguliers). Vous trouverez un exemple d’implémentation de service d’agent de surveillance [ici](https://azure.microsoft.com/resources/samples/service-fabric-watchdog-service/).

## <a name="secure-using-certificates"></a>Sécurisation à l’aide de certificats
L’utilisation de certificats, il indique comment les communications de hello toosecure entre hello différents nœuds du cluster Windows autonome, tooauthenticate les clients se connectant toothis cluster, à l’aide de certificats X.509 ainsi que comment. Cela garantit que seuls les utilisateurs autorisés peuvent accéder à cluster de hello, hello des applications déployées et effectuer des tâches de gestion. Sécurité de certificat doit être activée sur le cluster de hello lorsque hello cluster est créé.

### <a name="x509-certificates-and-service-fabric"></a>Certificats X.509 et Service Fabric
Les certificats numériques X.509 sont couramment utilisés tooauthenticate clients et les serveurs et tooencrypt et signer numériquement les messages.

Hello tableau ci-dessous répertorie les certificats hello dont vous aurez besoin de votre configuration de cluster :

|Définition des informations sur le certificat |Description|
|-------------------------------|-----------|
|ClusterCertificate|    Ce certificat est la communication de hello toosecure requis entre les nœuds de hello sur un cluster. Vous pouvez utiliser deux certificats différents : un certificat principal et un certificat secondaire pour la mise à niveau.|
|ServerCertificate| Ce certificat est présenté toohello client quand il tente de tooconnect toothis cluster. Vous pouvez utiliser deux certificats de serveur différents : un certificat principal et un certificat secondaire pour la mise à niveau.|
|ClientCertificateThumbprints|  Il s’agit d’un jeu de certificats que vous souhaitez tooinstall sur les clients de hello authentifié.|
|ClientCertificateCommonNames|  Hello de nom commun du certificat de client premier hello pour hello CertificateCommonName du jeu. Hello CertificateIssuerThumbprint est l’empreinte numérique hello pour émetteur hello de ce certificat.|
|ReverseProxyCertificate|   Il s’agit d’un certificat facultatif qui peut être spécifié si vous souhaitez toosecure votre [Proxy inverse](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).|

Pour plus d’informations sur la sécurisation à l’aide de certificats, [cliquez ici](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security).

## <a name="role-based-access-control-rbac"></a>Contrôle d’accès en fonction du rôle
Contrôle d’accès permet de cluster administrateur toolimit toocertain cluster opérations d’accès pour différents groupes d’utilisateurs, la sécurisation de cluster de hello hello. Deux types de contrôle d’accès différents sont pris en charge pour les clients se connectant tooa cluster : rôle d’administrateur et le rôle d’utilisateur.

Les administrateurs disposent de fonctionnalités de toomanagement d’un accès complet (y compris les fonctionnalités en lecture/écriture). Les utilisateurs, par défaut, ont uniquement un accès en lecture toomanagement fonctionnalités (par exemple, les fonctions de requête), hello capacité tooresolve applications et services.

Vous spécifiez hello administrateur client rôles d’utilisateur et lors de la création du cluster hello en fournissant des identités séparées (certificats, etc. AAD) pour chacun. Pour plus d’informations sur les paramètres de contrôle de l’accès par défaut hello et comment toochange hello les paramètres par défaut, consultez [le contrôle d’accès basée sur les rôles pour les clients du Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles).

## <a name="secure-standalone-cluster-using-windows-security"></a>Sécuriser un cluster autonome à l’aide de la sécurité de Windows
tooprevent non autorisé cluster Service Fabric de tooa accès, vous devez sécuriser le cluster de hello. Sécurité est particulièrement importante lorsque le cluster de hello exécutant des charges de travail de production. Il décrit comment la sécurité de nœud à nœud et client à nœud tooconfigure à l’aide de la sécurité dans Windows hello ClusterConfig.JSON fichier.

**Configuration de la sécurité Windows à l’aide de gMSA**

Sécurité toonode du nœud est configurée en définissant [ClustergMSAIdentity](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-windows-security) quand service fabric doit toorun sous service administré de groupe. Dans l’ordre toobuild relations d’approbation entre nœuds, ils doivent être informés de l’autre.

Sécurité de toonode client est configurée à l’aide de ClientIdentities. Commande tooestablish une confiance entre le client et hello cluster, vous devez configurer hello cluster tooknow les identités de client qu’il peut faire confiance.

**Configuration de la sécurité Windows à l’aide d’un groupe de machines**

Sécurité du nœud toonode est configurée par le paramètre à l’aide de ClusterIdentity si vous voulez toouse un groupe d’ordinateurs dans un domaine Active Directory. Pour en savoir plus, consultez la rubrique traitant de la [création d’un groupe de machines dans Active Directory](https://msdn.microsoft.com/library/aa545347).

La sécurité de client à nœud est configurée avec ClientIdentities. tooestablish d’approbation entre un client et hello du cluster, vous devez configurer hello cluster tooknow hello client peuvent faire confiance à des identités hello cluster. Vous pouvez établir cette approbation de deux manières différentes :

-   Spécifiez les utilisateurs de groupe de domaine hello qui peuvent se connecter.
-   Spécifiez les utilisateurs de nœud de domaine de hello qui peuvent se connecter.

## <a name="configure-application-security-in-service-fabric"></a>Configuration de la sécurité de l’application dans Service Fabric
### <a name="managing-secrets-in-service-fabric-applications"></a>Gestion des secrets dans des applications Service Fabric
Cette méthode permet de gérer les secrets dans une application Service Fabric. Les secrets peuvent être des informations sensibles quelconques, notamment des chaînes de connexion de stockage, des mots de passe ou d’autres valeurs qui ne doivent pas être traitées en texte brut.

Cette approche utilise [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis) toomanage clés et les secrets. Toutefois, à l’aide des clés secrètes dans une application est cluster tooa cloud indépendant de la plateforme tooallow applications toobe déployé hébergé n’importe où. Ce flux comprend quatre étapes principales :

-   Obtenez un certificat de chiffrement de données.
-   Installer le certificat de hello dans votre cluster.
-   Chiffrer les valeurs des secrets lors du déploiement d’une application avec un certificat de hello et les injecter dans le fichier de configuration d’un service Settings.xml.
-   Valeurs en lecture chiffré hors Settings.xml en déchiffrant avec hello même certificat de chiffrement.

>[!Note]
>Découvrez-en plus sur la [gestion des secrets dans des applications Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).

### <a name="configure-security-policies-for-your-application"></a>Configurer les stratégies de sécurité de votre application
En utilisant la sécurité de l’infrastructure de Service Azure, vous pouvez aider à sécuriser les applications qui sont exécutent dans le cluster hello sous différents comptes d’utilisateurs. Sécurité de l’infrastructure de service permet également de certificats, les fichiers, les répertoires et les ressources hello sécurisée qui sont utilisés par les applications au moment de hello du déploiement sous des comptes d’utilisateur hello--par exemple. Ainsi, les applications en cours d’exécution sont plus sécurisées, même dans un environnement hébergé partagé.
Hello étapes :

-   Configurer la stratégie hello pour un point d’entrée de service le programme d’installation.
-   Lancer des commandes PowerShell à partir d’un point d’entrée de configuration.
-   Utiliser la console de redirection pour le débogage local.
-   Configurer une stratégie pour les packages de code de service.
-   Assigner une stratégie d’accès de sécurité pour des points de terminaison HTTP et HTTPS.

## <a name="secure-communication-for-services-in-azure-service-fabric-security"></a>Sécuriser les communications pour les services dans la sécurité Azure Service Fabric
La sécurité est un des aspects les plus importants hello de communication. infrastructure d’application des Services fiables Hello fournit quelques piles de communication prédéfinies et des outils qui peuvent être utilisés tooimprove sécurité.

-   [Sécuriser un service quand vous utilisez la communication à distance des services](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication).
-   [Sécuriser un service quand vous utilisez une pile de communication basée sur WCF](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication#help-secure-a-service-when-youre-using-a-wcf-based-communication-stack).

## <a name="next-steps"></a>Étapes suivantes
- Pour obtenir des informations conceptuelles sur la sécurité des clusters, consultez [Créer un cluster dans Azure à l’aide d’un modèle Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) et [Portail Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal).
- Pour en savoir plus, consultez [Sécurité du cluster Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security).
