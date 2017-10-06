---
title: "Considérations relatives à l’aaaNetworking avec un environnement Azure App Service"
description: "Explique le trafic réseau de hello ASE et comment tooset UDRs avec votre ASE et les groupes de sécurité réseau"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 955a4d84-94ca-418d-aa79-b57a5eb8cb85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ccompy
ms.openlocfilehash: d4d3000f4d4d75814b1e6d47079d967334eb1a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-an-app-service-environment"></a>Considérations relatives à la mise en réseau pour un environnement App Service #

## <a name="overview"></a>Vue d'ensemble ##

 [App Service Environment Azure][Intro] est un déploiement d’Azure App Service dans un sous-réseau d’un réseau virtuel Azure (VNet). Il existe deux types de déploiement pour un environnement App Service (ASE) :

- **ASE externe**: expose hello ASE hébergeant des applications sur une adresse IP accessible via internet. Pour plus d’informations, consultez [Créer un environnement App Service externe][MakeExternalASE].
- **Équilibrage de charge interne ASE**: expose hello ASE hébergeant des applications sur une adresse IP à l’intérieur de votre réseau virtuel. point de terminaison interne Hello est un équilibreur de charge interne (ILB), c’est pourquoi il s’agit d’un environnement app service Équilibrage de charge interne. Pour plus d’informations, consultez [Create and use an ILB ASE][MakeILBASE] (Créer et utiliser un ASE ILB).

Il existe deux versions de l’application App Service : ASEv1 et ASEv2. Pour plus d’informations sur ASEv1, consultez [Introduction tooApp environnement Service v1][ASEv1Intro]. Un ASEv1 peut être déployé dans un réseau virtuel classique ou Resource Manager. Un ASEv2 peut uniquement être déployé dans un réseau virtuel Resource Manager.

Tous les appels à partir d’un environnement app service qui vont toohello internet laisser hello réseau virtuel via une adresse IP virtuelle affectée pour hello ASE. Hello adresse IP publique de cette adresse IP virtuelle est ensuite hello IP source pour tous les appels à partir de hello ASE qui vont toohello internet. Si les applications hello dans votre ASE apportez tooresources d’appels dans votre réseau virtuel ou sur un réseau privé virtuel, hello IP source est un des hello des adresses IP de sous-réseau hello utilisé par votre ASE. Hello ASE étant dans hello réseau virtuel, il peut également accéder aux ressources au sein de hello réseau virtuel sans aucune configuration supplémentaire. Si hello réseau virtuel est connecté tooyour local du réseau, les applications dans votre ASE ont également accès tooresources il. Vous n’avez pas besoin tooconfigure hello ASE ou votre application tous les autres.

![ASE externe][1] 

Si vous avez un environnement app service externe, adresse IP virtuelle publique de hello est également hello point de terminaison que vos applications ASE résoudre toofor :

* HTTP/S. 
* FTP/S. 
* Déploiement Web.
* Débogage à distance.

![ASE ILB][2]

Si vous avez un environnement app service Équilibrage de charge interne, adresse IP hello hello équilibrage de charge interne est hello de point de terminaison pour HTTP/S, FTP/S, le déploiement web et le débogage distant.

ports d’accès application normal Hello sont :

| Utilisation | À partir | trop|
|----------|---------|-------------|
|  HTTP/HTTPS  | Configurable par l’utilisateur |  80, 443 |
|  FTP/FTPS    | Configurable par l’utilisateur |  21, 990, 10001-10020 |
|  Débogage distant de Visual Studio  |  Configurable par l’utilisateur |  4016, 4018, 4020, 4022 |

Ces ports s’appliquent aussi bien pour un ASE externe que pour un ASE ILB. Si vous êtes dans un environnement app service externe, vous appuyer sur ces ports sur l’adresse IP virtuelle publique de hello. Si vous êtes dans un environnement app service Équilibrage de charge interne, vous appuyer sur ces ports sur hello équilibrage de charge interne. Si vous verrouillez le port 443, il peut y avoir une incidence sur certaines fonctionnalités exposées dans le portail de hello. Pour plus d’informations, consultez la section [Dépendances du portail](#portaldep).

## <a name="ase-dependencies"></a>Dépendances d’un ASE ##

Un ASE présente la dépendance d’accès entrant suivante :

| Utilisation | À partir | trop|
|-----|------|----|
| Gestion | Adresses de gestion App Service | Sous-réseau de l’ASE : 454, 455 |
|  Communications internes de l’ASE | Sous-réseau de l’ASE : tous les ports | Sous-réseau de l’ASE : tous les ports
|  Autoriser le trafic entrant provenant d’Azure Load Balancer | Équilibrage de charge Azure | Sous-réseau de l’ASE : tous les ports
|  Adresses IP affectées par l’application | Adresses affectées par l’application | Sous-réseau de l’ASE : tous les ports

Hello le trafic entrant fournit commande et contrôle de ASE hello dans l’analyse des toosystem d’addition. source de Hello des adresses IP pour ce trafic sont répertoriées dans hello [ASE gestion des adresses] [ ASEManagement] document. configuration de la sécurité réseau Hello doit tooallow l’accès à partir de toutes les adresses IP sur les ports 454 et 455.

Au sein du sous-réseau hello ASE sont grand nombre de ports utilisés pour la communication de composant interne et elles peuvent changer.  Cela nécessite tous les ports hello dans hello ASE sous-réseau toobe accessible à partir du sous-réseau de ASE hello. 

Pour la communication hello entre l’équilibrage de charge Azure hello et hello ASE hello minimale les ports du sous-réseau que toobe besoin ouvert sont 454 et 455 de 16001. port de 16001 Hello est utilisé pour conserver le trafic actif entre l’équilibrage de charge hello et hello ASE. Si vous utilisez un environnement app service Équilibrage de charge interne vous pouvez verrouiller le trafic vers le bas toojust hello 454, 455, 16001 ports.  Si vous utilisez un environnement app service externe vous devez tootake dans les ports d’accès de compte hello application normal.  Si vous utilisez des adresses d’application affectée vous devez tooopen il tooall ports.  Lorsqu’une adresse est assignée application spécifique de tooa, équilibrage de charge hello utilisera les ports qui ne sont pas connus d’avance toosend HTTP et HTTPS traffic toohello ASE.

Si vous utilisez des adresses IP application affectée, vous devez tooallow trafic hello que des adresses IP affectées sous-réseau de ASE toohello tooyour applications.

Pour l’accès sortant, un ASE dépend de plusieurs systèmes externes. Ces dépendances système sont définis avec des noms DNS et ne sont pas tooa ensemble fixé d’adresses IP. Par conséquent, hello ASE requiert un accès sortant à partir de hello ASE sous-réseau tooall des adresses IP externes dans une gamme de ports. Un environnement app service a hello suivant dépendances sortantes :

| Utilisation | À partir | trop|
|-----|------|----|
| Azure Storage | Sous-réseau de l’ASE | table.core.windows.net, blob.core.windows.net, queue.core.windows.net, file.core.windows.net : 80, 443, 445 (le port 445 est requis uniquement pour ASEv1) |
| Azure SQL Database | Sous-réseau de l’ASE | database.windows.net : 1433, 11000-11999, 14000-14999 (pour plus d’informations, consultez [Port utilisé par SQL Database V12](../../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md).)|
| Gestion d’Azure | Sous-réseau de l’ASE | management.core.windows.net, management.azure.com : 443 
| Vérification du certificat SSL |  Sous-réseau de l’ASE            |  ocsp.msocsp.com, mscrl.microsoft.com, crl.microsoft.com : 443
| Azure Active Directory        | Sous-réseau de l’ASE            |  Internet : 443
| Gestion d’App Service        | Sous-réseau de l’ASE            |  Internet : 443
| DNS Azure                     | Sous-réseau de l’ASE            |  Internet : 53
| Communications internes de l’ASE    | Sous-réseau de l’ASE : tous les ports |  Sous-réseau de l’ASE : tous les ports

Si hello ASE perd l’accès des dépendances de toothese, il cesse de fonctionner. Lorsque cela produit long suffisamment, hello ASE est suspendue.

### <a name="customer-dns"></a>DNS client ###

Si hello réseau virtuel est configuré avec un serveur DNS défini par le client, les charges de travail clientes hello l’utiliser. Hello ASE doit toujours toocommunicate avec Azure DNS à des fins de gestion. 

Si hello réseau virtuel est configuré avec un client DNS sur hello autre côté d’un réseau VPN, serveur DNS de hello doit être accessible à partir du sous-réseau hello contenant hello ASE.

<a name="portaldep"></a>

## <a name="portal-dependencies"></a>Dépendances du portail ##

Dans dépendances fonctionnelles toohello ASE de plus, il existe quelques éléments supplémentaires associées toohello portail expérience. Certaines des fonctionnalités hello Bonjour portail Azure dépendent site_ de too_SCM un accès direct. Pour chaque application dans Azure App Service, il existe deux URL. Hello première URL est tooaccess votre application. URL du deuxième Hello est tooaccess hello SCM site, ce qui est également appelé hello _console de Kudu_. Les fonctionnalités qui utilisent le site SCM hello :

-   Tâches web
-   Fonctions
-   Diffusion de journaux
-   Kudu
-   Extensions
-   Process Explorer
-   Console

Lorsque vous utilisez un environnement app service Équilibrage de charge interne, site SCM hello n’est pas accessible depuis l’extérieur hello réseau virtuel d’internet. Lorsque votre application est hébergée sur un environnement app service Équilibrage de charge interne, certaines fonctionnalités ne fonctionneront pas à partir du portail de hello.  

La plupart de ces fonctions qui varient en fonction du site SCM hello sont également disponibles directement dans la console de Kudu hello. Vous pouvez vous connecter tooit directement, plutôt qu’en utilisant le portail de hello. Si votre application est hébergée dans un environnement app service Équilibrage de charge interne, utilisez votre publication toosign d’informations d’identification dans. Hello URL tooaccess hello SCM site d’une application hébergée dans un environnement app service Équilibrage de charge interne a hello suivant le format : 

```
<appname>.scm.<domain name hello ILB ASE was created with> 
```

Si votre ASE d’équilibrage de charge interne est le nom de domaine hello *contoso.net* et le nom de votre application est *testapp*, application hello est atteinte au *testapp.contoso.net*. site SCM Hello qui le suit est atteinte au *testapp.scm.contoso.net*.

### <a name="functions-and-web-jobs"></a>Fonctions et tâches web ###

Les fonctions et Web travaux dépendent de hello SCM site mais sont prises en charge pour une utilisation dans le portail de hello, même si vos applications sont dans un environnement app service Équilibrage de charge interne, tant que votre navigateur peut atteindre le site SCM hello.  Si vous utilisez un certificat auto-signé avec votre ASE d’équilibrage de charge interne, vous devez tooenable votre tootrust de navigateur de certificat.  Pour Internet Explorer ou Edge qui signifie que le certificat de hello a toobe en mode de confiance ordinateur hello stocker.  Si vous utilisez Chrome qui signifie que vous avez accepté certificat hello dans le navigateur de hello précédemment en vraisemblablement appuyant directement sur site de scm hello.  Hello meilleure solution consiste toouse un certificat commercial qui se trouve dans la chaîne du navigateur hello d’approbation.  

## <a name="ase-ip-addresses"></a>Adresses IP d’un ASE ##

Un environnement app service a quelques toobe adresses IP prenant en charge de. Il s'agit de :

- **Adresse IP entrante publique** : utilisée pour le trafic d’applications dans un ASE externe et pour le trafic de gestion aussi bien dans un ASE externe que dans un ASE ILB.
- **Adresse IP publique sortant**: utilisé comme hello IP « de » pour les connexions sortantes à partir de hello ASE que hello laissez réseau virtuel, qui ne sont pas routé vers un réseau privé virtuel.
- **Adresse IP ILB** : si vous utilisez un ASE ILB.
- **Adresse SSL basée sur IP attribuée par l’application** : uniquement possibles avec un ASE externe et lorsque le mode SSL basé sur IP est configuré.

Toutes ces adresses IP sont facilement visibles dans un ASEv2 Bonjour portail Azure à partir de hello ASE UI. Si vous avez un environnement app service Équilibrage de charge interne, IP hello pour hello équilibrage de charge interne est répertorié.

![Adresses IP][3]

### <a name="app-assigned-ip-addresses"></a>Adresses IP attribuées par l’application ###

Avec un environnement app service externe, vous pouvez affecter des adresses IP tooindividual applications. Ce n’est pas possible avec un ASE ILB. Pour plus d’informations sur la façon de tooconfigure toohave de votre application sa propre adresse IP, consultez [lier un existant SSL certificat tooAzure web applications personnalisées](../../app-service-web/app-service-web-tutorial-custom-ssl.md).

Lorsqu’une application possède sa propre adresse SSL basé sur IP, hello ASE réserve adresse IP de deux ports toomap toothat. Un port pour le trafic HTTP, et hello autre port est pour le protocole HTTPS. Ces ports sont répertoriés dans hello UI ASE dans la section d’adresses IP hello. Le trafic doit être en mesure de tooreach ces ports à partir de hello VIP ou les applications de hello sont inaccessibles. Cette exigence est tooremember important lorsque vous configurez des groupes de sécurité réseau (NSG).

## <a name="network-security-groups"></a>Network Security Group ##

[Groupes de sécurité réseau] [ NSGs] hello capacité toocontrol l’accès d’un réseau virtuel. Lorsque vous utilisez le portail de hello, il est implicite deny de règle à hello la plus basse priorité toodeny tous les éléments. Ce que vous créez sont vos règles d’autorisation.

Dans un environnement app service, vous n’avez accès toohello machines virtuelles utilisées toohost hello ASE lui-même. Elles se trouvent dans un abonnement géré par Microsoft. Si vous souhaitez que les applications toohello toorestrict accès sur hello ASE, définir des groupes de sécurité réseau sur le sous-réseau de ASE hello. Ce faisant, soyez très attentif dépendances de ASE toohello. Si vous bloquez toutes les dépendances, hello ASE cesse de fonctionner.

Groupes de sécurité réseau peuvent être configurés via hello portail Azure ou via PowerShell. informations Hello ici montrent hello portail Azure. Vous créez et gérez des groupes de sécurité réseau dans le portail de hello comme une ressource de niveau supérieur sous **réseau**.

Hello exigences entrantes et sortantes sont prises en compte, hello groupes de sécurité réseau doit se présenter comme toohello groupes de sécurité réseau illustrés dans cet exemple. Hello, plage d’adresses réseau virtuel est _192.168.250.0/16_, et le sous-réseau hello hello ASE dans est _192.168.251.128/25_.

Hello tout d’abord deux entrant conditions hello ASE toofunction sont affichées en haut de hello de liste de hello dans cet exemple. Ils activer la gestion de ASE et autoriser toocommunicate ASE de hello avec lui-même. Bonjour autres entrées sont tous les locataires configurable et peuvent contrôler les applications réseau accès toohello ASE hébergé. 

![Règles de sécurité de trafic entrant][4]

Une règle par défaut permet de hello des adresses IP dans le sous-réseau ASE toohello hello réseau virtuel tootalk. Une autre règle par défaut permet l’équilibrage de charge hello, également appelée adresse IP virtuelle publique de hello, toocommunicate avec hello ASE. Sélectionnez des règles par défaut de hello toosee, **règles par défaut** toohello suivant **ajouter** icône. Si vous placez une instruction deny tout le reste de règles une fois hello NSG règles affichées, vous empêchez le trafic entre les adresses IP virtuelles hello et hello ASE. le trafic tooprevent d’à l’intérieur de hello réseau virtuel, ajoutez vos propres tooallow règle entrante. Utiliser un tooAzureLoadBalancer égal source avec une destination **tout** et une plage de ports de  **\*** . Règle de groupe de sécurité réseau hello étant appliqués toohello ASE sous-réseau, vous n’avez pas besoin spécifique de toobe dans la destination de hello.

Si vous avez affecté à une application de tooyour d’adresses IP, assurez-vous que vous conservez hello ports ouverts. sélectionner des ports de hello toosee, **environnement App Service** > **des adresses IP**.  

Tous les éléments hello illustrés hello suivant les règles de trafic sortant sont nécessaires à l’exception du dernier élément de hello. Elles permettent de réseau accès toohello ASE dépendances qui ont été notées précédemment dans cet article. Si vous bloquez un d'entre eux, votre ASE cesse de fonctionner. Hello dernier élément de liste de hello permet à votre toocommunicate ASE avec d’autres ressources dans votre réseau virtuel.

![Règles de sécurité de trafic entrant][5]

Une fois vos groupes de sécurité réseau sont définies, affectez-les sous-réseau toohello votre ASE sur. Si vous ne connaissez pas hello ASE réseaux ou sous-réseaux, vous pouvez le voir à partir du portail de gestion ASE hello. tooassign hello sous-réseau tooyour de groupe de sécurité réseau, le sous-réseau toohello l’interface utilisateur, sélectionnez hello groupe de sécurité réseau.

## <a name="routes"></a>Itinéraires ##

Les itinéraires posent le plus souvent problème lorsque vous configurez votre réseau virtuel avec Azure ExpressRoute. Il existe trois types d’itinéraires dans un réseau virtuel :

-   Itinéraires système
-   Itinéraires BGP
-   Itinéraires définis par l’utilisateur (UDR)

Les itinéraires BGP prennent le pas sur les itinéraires système. Les UDR prennent le pas sur les itinéraires BGP. Pour plus d’informations sur les itinéraires dans les réseaux virtuels Azure, consultez [Présentation des itinéraires définis par l’utilisateur][UDRs].

base de données SQL Azure Hello que hello ASE utilise un système de hello toomanage doté d’un pare-feu. Il requiert toooriginate de communication à partir de hello ASE publique VIP. Connexions toohello base de données SQL hello ASE sera refusé si elles sont envoyées vers le bas hello connexion ExpressRoute et une autre adresse IP.

Si les demandes de gestion des réponses tooincoming sont envoyées vers le bas hello ExpressRoute, adresse de réponse hello est différent de celui de destination d’origine de hello. Cette incompatibilité interrompt les communications TCP hello.

Pour votre toowork ASE pendant la configuration de votre réseau virtuel avec un ExpressRoute, hello plus simple chose toodo est :

-   Configurer ExpressRoute tooadvertise _0.0.0.0/0_. Par défaut, il tunnélise de force tout le trafic sortant local.
-   Créer un UDR. Sous-réseau toohello contenant ASE hello avec un préfixe d’adresse de l’appliquer _0.0.0.0/0_ et en regard de type de tronçon _Internet_.

Si vous modifiez ces deux, destinés à l’internet le trafic en provenance du sous-réseau de ASE hello n’est pas forcé hello ExpressRoute et hello ASE fonctionne. 

> [!IMPORTANT]
> itinéraires Hello définis dans un UDR doivent être suffisamment spécifique tootake priorité sur les itinéraires annoncés par la configuration de ExpressRoute hello. Hello exemple précédent utilise plage d’adresses 0.0.0.0/0 large hello. Il peut potentiellement être remplacé accidentellement par des annonces de routage utilisant des plages d’adresses plus spécifiques.
>
> ASEs ne sont pas pris en charge avec des configurations ExpressRoute entre-publier des routes de hello d’homologation publique toohello d’homologation privée chemin d’accès. Les configurations ExpressRoute ayant une homologation publique configurée reçoivent les publications de routage de Microsoft. les publications Hello contiennent un grand ensemble de plages d’adresses IP de Microsoft Azure. Si les plages d’adresses hello sont publiés entre sur le chemin d’accès de hello d’homologation privée, tous les paquets réseau sortant à partir du sous-réseau de hello de ASE sont infrastructure de réseau local du client force tooa tunnel. Ce flux de réseau n’est actuellement pas pris en charge par les environnements App Service. Un problème de toothis de solution est toostop les itinéraires de publication croisée de hello d’homologation publique toohello d’homologation privée chemin d’accès.

toocreate un UDR, procédez comme suit :

1. Accédez toohello portail Azure. Sélectionnez **Mise en réseau** > **Tables d’itinéraires**.

2. Créer une table de routage Bonjour même région que votre réseau virtuel.

3. À partir de l’interface utilisateur de votre table d’itinéraires, sélectionnez **Itinéraires** > **Ajouter**.

4. Ensemble hello **type de tronçon suivant** trop**Internet** et hello **préfixe d’adresse** trop**0.0.0.0/0**. Sélectionnez **Enregistrer**.

    Vous voyez alors hello suivant :

    ![Itinéraires fonctionnels][6]

5. Après avoir créé une nouvelle table d’itinéraires hello, accédez sous-réseau toohello qui contient votre ASE. Sélectionnez votre table de routage à partir de la liste de hello dans le portail de hello. Après avoir enregistré les modifications de hello, vous devez puis Voir groupes de sécurité réseau hello et itinéraires notées avec votre sous-réseau.

    ![Itinéraires et groupes de sécurité réseau][7]

### <a name="deploy-into-existing-azure-virtual-networks-that-are-integrated-with-expressroute"></a>Déploiement dans des réseaux virtuels Azure existants intégrés à ExpressRoute ###

toodeploy votre ASE dans un réseau virtuel qui est intégré à ExpressRoute, préconfigurer sous-réseau hello où vous souhaitez ASE hello déployé. Utilisez ensuite une toodeploy de modèle de gestionnaire de ressources qu’il. toocreate ASE dans un réseau virtuel qui a déjà ExpressRoute configuré :

- Créer un Bonjour toohost de sous-réseau ASE.

    > [!NOTE]
    > Rien d’autre ne peut être dans le sous-réseau de hello mais hello ASE. Être toochoose qu’un espace d’adressage qui permet une croissance future. Vous ne pouvez pas modifier ce paramètre par la suite. Nous vous recommandons une taille de `/25` avec 128 adresses.

- Créez UDRs (par exemple, les tables d’itinéraires) comme décrit précédemment et le définir sur le sous-réseau de hello.
- Créer hello ASE à l’aide d’un modèle de gestionnaire de ressources comme décrit dans [créer un environnement app service à l’aide d’un modèle de gestionnaire de ressources][MakeASEfromTemplate].

<!--Image references-->
[1]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow.png
[2]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow2.png
[3]: ./media/network_considerations_with_an_app_service_environment/networkase-ipaddresses.png
[4]: ./media/network_considerations_with_an_app_service_environment/networkase-inboundnsg.png
[5]: ./media/network_considerations_with_an_app_service_environment/networkase-outboundnsg.png
[6]: ./media/network_considerations_with_an_app_service_environment/networkase-udr.png
[7]: ./media/network_considerations_with_an_app_service_environment/networkase-subnet.png

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ASEManagement]: ./management-addresses.md
