---
title: "meilleures pratiques de la sécurité de l’infrastructure de Service aaaAzure | Documents Microsoft"
description: "Cet article fournit un ensemble de bonnes pratiques pour la sécurité Azure Service Fabric."
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
ms.openlocfilehash: 483a21240da17d56bb4641653093ddcbad379d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-best-practices"></a>Bonnes pratiques pour la sécurité Azure Service Fabric
Le déploiement d’une application sur Azure est rapide, simple et rentable. Avant de déployer l’application de cloud computing dans toohave utile de production constitue une pratique recommandée tooassist lors de l’évaluation de votre application par rapport à une liste des meilleures pratiques essentielles et recommandées.

Azure Service Fabric est une plateforme de systèmes distribués qui rend facile toopackage, déployer et gérer des microservices fiables et évolutives. Service Fabric résout également des défis de hello dans le développement et la gestion des applications de cloud. Les développeurs et administrateurs sont en mesure d’éviter les problèmes d’infrastructure complexes et peuvent se concentrer sur l’implémentation de charges de travail stratégiques et exigeantes, évolutives, fiables et faciles à gérer. 

Pour chaque bonne pratique, nous détaillons les éléments suivants :

-   Les meilleures pratiques de hello est
-   Raison pour laquelle vous souhaitez tooenable que les meilleures pratiques
-   Ce que peut être le résultat de hello si vous ne parvenez pas la meilleure pratique de tooenable hello
-   Comment vous pouvez apprendre tooenable hello il est recommandé

Nous disposons actuellement hello suivant les meilleures pratiques de sécurité Azure Service Fabric :

-   Utiliser un modèle Azure Resource Manager(ARM) et cluster sécurisée de PowerShell Module de Service Fabric Azure toocreate
-   Utiliser des certificats X.509
-   Configurer des stratégies de sécurité
-   Configurer la sécurité de Reliable Actors
-   Configurer SSL pour Azure Service Fabric
-   Sécurité/isolement réseau avec Azure Service Fabric
-   Configurer un coffre de clés pour la sécurité
-   Affecter des utilisateurs tooroles


## <a name="best-practices-for-securing-your-cluster"></a>Bonnes pratiques pour sécuriser votre cluster

**Grandes lignes**

Utiliser toujours un cluster sécurisé
-   Sécurité du cluster : utiliser des certificats
-   Accès client (admin et en lecture seule) : utiliser AAD

Utiliser des déploiements automatisés
-   Utiliser des scripts toogenerate, déployer et substituer les clés secrètes
-   Conserver les secrets hello dans KV, utiliser Active Directory pour tous les autres accès client
-   Aucun humaines ne doivent avoir toothem accès sans authentification.

En outre, tenez compte des éléments suivants de hello :
-   Créer des zones DMZ à l’aide des groupes de sécurité réseau (NSG)
-   Utiliser saut serveurs tooRDP dans les machines virtuelles du cluster ou toomanage votre cluster

Clusters doivent être tooprevent sécurisé non autorisé les utilisateurs de se connecter tooyour cluster, surtout quand les charges de production en cours d’exécution sur ce dernier. Bien qu’il soit possible de toocreate un cluster non sécurisé, cela permet aux utilisateurs anonymes tooconnect tooit, s’il expose toohello de points de terminaison de gestion Internet public.

Technologies utilisées tooimplement ces scénarios. Hello [les scénarios de sécurité du cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security) sont :

-   Nœud à nœud sécurité-This sécurise les communications entre hello machines virtuelles et les ordinateurs dans un cluster de hello. Cela garantit que seuls les ordinateurs qui sont autorisés toojoin hello clusters peuvent participer hébergeant des applications et services de cluster de hello.
Les clusters qui s’exécutent sur Azure ou les clusters autonomes sur Windows peuvent utiliser la [Sécurité par certificat](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security) ou la [Sécurité Windows](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-windows-security) pour les ordinateurs Windows Server.
-   Nœud-client-la sécurité présente sécurise les communications entre un client de l’infrastructure de Service et les différents nœuds hello cluster.
-   Contrôle d’accès basé sur un rôle (RBAC) - vous spécifiez hello administrateur client rôles d’utilisateur et lors de la création du cluster hello en fournissant des identités séparées (certificats, etc. AAD) pour chacun.
-   Recommandations de sécurité-Azure pour les clusters, il est recommandé d’utiliser AAD sécurité tooauthenticate clients et les certificats pour la sécurité du nœud à l’autre.

tooconfigure hello autonome cluster Windows, consultez [configurer les paramètres de cluster de windows autonome](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest).

Utiliser les modèles Azure Resource Manager et cluster sécurisée de PowerShell Module de Service Fabric Azure toocreate.
Un guide vous montrant pas à pas comment configurer un cluster Azure Service Fabric sécurisé dans Azure à l’aide d’Azure Resource Manager est disponible [ici](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm).

Utiliser toocustomize de modèle Azure Resource Manager hello votre cluster
-   Stockage des VHD de machine virtuelle géré par le programme d’installation

Utiliser le modèle d’Azure Resource Manager hello modifications toodrive tooyour groupe de ressources
-   Gestion des configurations aisée
-   Audit

Traiter la configuration du cluster comme du code
-   Être complet lors de la vérification des configurations de hello vous choisissez toodeploy
-   Évitez d’utiliser des commandes implicite tootweak vos ressources directement

Plusieurs aspects de hello [cycle de vie application Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-lifecycle) peut être automatisée. Le [module Azure PowerShell Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications#upload-the-application-package) automatise les tâches courantes de déploiement, de mise à niveau, de suppression et de test des applications Service Fabric. Des API gérées et HTTP pour la gestion de l’application sont également disponibles.

## <a name="use-x509-certificates"></a>Utiliser des certificats X.509
Les clusters doivent toujours être sécurisés à l’aide de certificats X.509 ou de la sécurité Windows. La sécurité est configurée uniquement au moment de la création de cluster et n’est pas possible tooenable sécurité après que hello cluster est créé.

Si vous spécifiez un [certificat de cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security), hello valeur ClusterCredentialType tooX509. Si vous spécifiez un certificat de serveur pour les connexions externes, définissez hello ServerCredentialType tooX509.

-   Les certificats utilisés dans les clusters qui exécutent des charges de travail de production doivent être créés en utilisant un service de certificats Windows Server correctement configuré ou obtenus auprès d’une autorité de certification approuvée.
-   En production, n’utilisez jamais de certificats temporaires ou de test créés avec des outils comme MakeCert.exe.
-   Vous pouvez utiliser un certificat auto-signé, mais seulement pour les clusters de test et non en production.

Si le cluster hello est non sécurisé. N’importe qui peut se connecter anonymement et effectuer des opérations de gestion. Les clusters de production doivent donc toujours être sécurisés à l’aide de certificats X.509 ou via la sécurité Windows.

toolearn plus tooenable des certificats dans le cluster service fabric voir, [ajouter ou supprimer des certificats pour un cluster service fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure).

## <a name="configure-security-policies"></a>Configurer des stratégies de sécurité
Service Fabric permet également de certificats, les fichiers, les répertoires et les ressources hello sécurisée qui sont utilisés par les applications au moment de hello du déploiement sous des comptes d’utilisateur hello--par exemple. Ainsi, les applications en cours d’exécution sont plus sécurisées, même dans un environnement hébergé partagé.

-   Utiliser un groupe de domaine Active Directory ou un utilisateur : vous pouvez exécuter le service hello sous les informations d’identification hello pour un compte d’utilisateur ou un groupe Active Directory. Il s’agit d’Active Directory en local au sein de votre domaine et non avec Azure Active Directory (Azure AD). À l’aide un utilisateur de domaine ou un groupe, vous pouvez ensuite accéder autres ressources dans le domaine hello (par exemple, les partages de fichiers) qui dispose d’autorisations.

-   Affecter une stratégie d’accès de sécurité pour les points de terminaison HTTP et HTTPS : Si vous appliquez un service tooa de stratégie d’identification et le manifeste de service hello déclare des ressources de point de terminaison avec le protocole de hello HTTP, vous devez spécifier un tooensure SecurityAccessPolicy que les ports affectés toothese points de terminaison sont correctement avec contrôle d’accès répertoriés pour hello compte d’utilisateur RunAs hello service s’exécute sous. Sinon, http.sys ne possède pas de service d’accès toohello, et vous obtenez des échecs lors des appels à partir du client de hello.
toolearn activer plus des stratégies de sécurité de l’infrastructure de service, consultez [configurer des stratégies de sécurité pour votre application](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-runas-security).

## <a name="reliable-actors-security-configuration"></a>Configurer la sécurité de Reliable Actors
Service Fabric Reliable Actors est une implémentation du modèle de conception d’acteur hello. Comme avec n’importe quel modèle de conception de logiciels, décision hello se toouse un modèle spécifique est effectué en se basant sur ou non un logiciel de conception problème adapté à un modèle de hello.

En règle générale, envisagez hello acteur modèle toomodel votre scénario ou un problème si :
-   Votre espace de problème implique un nombre élevé (plusieurs milliers) de petites unités d’état et de logique indépendantes et isolées.
-   Vous souhaitez toowork avec des objets à thread unique qui ne nécessitent pas d’interaction significative à partir des composants externes, y compris l’interrogation d’état sur un ensemble d’intervenants.
-   Vos instances d’acteurs ne bloquent pas les appelants avec des retards inattendus en exécutant des opérations d’E/S.

Dans l’infrastructure de Service, les acteurs sont implémentées dans le framework Reliable Actors de hello : une infrastructure d’application de modèle-basé sur acteur construite sur [Service des Services de Fabric fiables](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-introduction). Chaque service Reliable Actor que vous écrivez correspond en fait à une instance Reliable Service partitionnée avec état.
Chaque acteur est définie comme une instance d’un type d’acteur, toohello identiques façon un objet .NET est une instance d’un type .NET. Par exemple, il peut y avoir un type d’acteur qui implémente les fonctionnalités de hello d’une calculatrice, et il peut y avoir de nombreux acteurs de ce type qui sont réparties sur différents nœuds sur un cluster. Chaque acteur de ce type est identifié de façon unique par un ID d'acteur.

[Configurations de sécurité Replicator](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-actors-kvsactorstateprovider-configuration) sont le canal de communication utilisé toosecure hello est utilisé lors de la réplication. Cela signifie que les services ne peut pas voir l’autre trafic de réplication, garantissant que les données de salutation hautement disponible sont également sécurisées. Par défaut, une section de configuration de sécurité vide empêche de sécuriser la réplication.
Configurations de réplicateur configurer réplicateur hello qui est responsable de l’état de fournisseur d’état d’acteur hello hautement fiable.

## <a name="configure-ssl-for-azure-service-fabric"></a>Configurer SSL pour Azure Service Fabric

L’authentification du serveur : [authentifie](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) hello client de gestion de tooa de points de terminaison de gestion de cluster, afin que hello gestion client sait qu’il communique avec le véritable toohello cluster. Ce certificat fournit également un [SSL](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) pour hello API de gestion HTTPS et pour le Service Fabric Explorer via le protocole HTTPS.
Vous devez obtenir un nom de domaine personnalisé pour votre cluster. Lorsque vous demandez un certificat à partir d’une autorité de certification, hello nom du sujet du certificat doit correspondre au nom de domaine personnalisé hello que vous utilisez pour votre cluster.

tooconfigure SSL pour une application, vous devez tout d’abord tooget un certificat SSL qui a été signé par un certificat autorité (CA), un tiers de confiance qui émet des certificats à cet effet. Si vous n’en avez pas déjà, vous devez tooobtain une à partir d’une société qui vend des certificats SSL.

certificat de Hello doit respecter hello suivant les exigences pour les certificats SSL dans Azure :
-   certificat de Hello doit contenir une clé privée.
-   certificat de Hello doit être créé pour l’échange de clés, exportable tooa fichier d’échange d’informations personnelles (.pfx).
-   Hello nom du sujet du certificat doit correspondre au service de cloud hello domaine utilisé tooaccess hello. Impossible d’obtenir un certificat SSL à partir d’une autorité de certification (CA) pour le domaine cloudapp.net de hello. Vous devez vous procurer un toouse de nom de domaine personnalisé lorsque accéder à votre service. Lorsque vous demandez un certificat à partir d’une autorité de certification, nom du sujet du certificat hello doit correspondre à hello domaine personnalisé nom utilisé tooaccess votre application. Par exemple, si votre nom de domaine personnalisé est contoso.com, vous demandez un certificat auprès de votre autorité de certification pour **.contoso.com** ou **www.contoso.com**.
-   certificat de Hello doit utiliser un minimum de chiffrement de 2048 bits.

HTTP n’est pas sécurisée et sujet tooeavesdropping attaques parce que les données transférées depuis le serveur web toohello hello web navigateur ou entre les autres points de terminaison hello est transmis en texte brut. Cela signifie que des attaquants peuvent intercepter et afficher des données sensibles, telles que les détails d’une carte de crédit et des informations de connexion de compte. Quand les données sont envoyées ou publiées par le biais d’un navigateur via HTTPS, SSL garantit que ces informations sont chiffrées et protégées contre une interception.

de plus, reportez-vous à toolearn, [configurer de SSL pour une application Windows azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-configure-ssl-certificate).

## <a name="network-isolationsecurity-with-azure-service-fabric"></a>Sécurité/isolement réseau avec Azure Service Fabric
Utilisez [modèle Azure Resource Manager (ARM)](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) sous forme d’exemple pour configurer un nodetype trois cluster sécurisée et toocontrol hello le trafic réseau entrant et sortant à l’aide de groupes de sécurité réseau.

modèle de Hello comporte un groupe de sécurité réseau pour chacun de hello machine virtuelle mise à l’échelle set(VMSS) toocontrol hello le trafic vers et depuis hello mise. Par défaut, les règles de hello sont configurés par hello système hello et services application ports spécifiés dans le modèle de hello tooallow que tous hello le trafic nécessité. Passez en revue ces règles et apporter des modifications toofit vos besoins, y compris ajouter de nouveaux pour vos applications.

Pour plus d’informations, consultez [Azure Service Fabric – scénarios de mise en réseau courants](https://docs.microsoft.com/azure/service-fabric/service-fabric-patterns-networking).

## <a name="set-up-a-key-vault-for-security"></a>Configurer un coffre de clés pour la sécurité
Certificats sont utilisés dans les toosecure Service Fabric tooprovide l’authentification et chiffrement divers aspects d’un cluster et ses applications.

Service Fabric utilise toosecure de certificats X.509 un cluster et fournir des fonctionnalités de sécurité d’application. Vous utilisez le coffre de clés trop[gérer les certificats](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure) pour les clusters Service Fabric dans Azure. Lorsqu’un cluster est déployé dans Azure, fournisseur de ressources Azure hello qui est chargé de créer des clusters Service Fabric extrait les certificats de coffre de clés et les installe sur les machines virtuelles du cluster hello.

Hello relation entre [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault), un cluster service fabric et le fournisseur de ressources Azure hello qui utilise les certificats stockés dans un coffre de clés lorsqu’il crée un cluster.

**Créer un groupe de ressources** hello première étape consiste toocreate un groupe de ressources spécifiquement pour votre coffre de clés. Nous vous recommandons de placer le coffre de clés hello dans son propre groupe de ressources. Cette action permet de supprimer des groupes ressources de calcul et de stockage hello, y compris le groupe de ressources hello qui contient votre cluster Service Fabric, sans perdre vos clés et les clés secrètes. groupe de ressources Hello qui contient votre coffre de clés doit être Bonjour même région que le cluster hello qui l’utilise.

**Créer un coffre de clés dans le nouveau groupe de ressources hello** coffre de clés hello doit être activé pour le déploiement tooallow hello certificats de tooget de fournisseur de ressources de calcul à partir de celui-ci et l’installer sur les instances de machine virtuelle.
toolearn plus tooset de coffre de clés Azure voir, [prise en main d’Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-get-started).

## <a name="assign-users-roles"></a>Assigner des rôles aux utilisateurs
Après avoir créé hello applications toorepresent votre cluster, affecter vos utilisateurs des rôles toohello pris en charge par le Service Fabric : en lecture seule et administrateur. Vous pouvez affecter des rôles de hello à l’aide de hello portail Azure classic.

>[!Note]
> Pour plus d’informations sur les rôles dans Service Fabric, consultez [Contrôle d’accès en fonction du rôle pour les clients de Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles).

Azure Service Fabric prend en charge deux types de contrôle d’accès différents pour les clients qui sont connecté tooa [cluster Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm): administrateur et utilisateur. Contrôle d’accès permet de cluster administrateur toolimit toocertain cluster opérations d’accès pour différents groupes d’utilisateurs, la sécurisation de cluster de hello hello.

## <a name="next-steps"></a>Étapes suivantes
- Configuration de votre [environnement de développement](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started) Service Fabric.
- Découvrez les [options de support de Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-support).

