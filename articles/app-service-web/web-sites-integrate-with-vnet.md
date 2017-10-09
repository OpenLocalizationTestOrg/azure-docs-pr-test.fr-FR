---
title: "aaaIntegrate une application avec un réseau virtuel Azure"
description: "Vous montre comment tooconnect une application dans Azure App Service tooa existant ou nouveau réseau virtuel Azure"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: 90bc6ec6-133d-4d87-a867-fcf77da75f5a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ccompy
ms.openlocfilehash: a93c504481400245b02220b541a008a7c874d10a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-app-with-an-azure-virtual-network"></a>Intégrer une application à un réseau Azure Virtual Network
Ce document décrit la fonctionnalité d’intégration hello Azure App Service réseau virtuel et montre comment tooset, configurez-le avec les applications dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Si vous n’êtes pas familiarisé avec les réseaux virtuels Azure (réseaux virtuels), il s’agit d’une fonctionnalité qui vous permet de tooplace la plupart de vos ressources Azure dans un réseau routables non internet que vous contrôlez l’accès à. Ces réseaux peut ensuite être tooyour connectés sur des réseaux locaux à l’aide de diverses technologies VPN. toolearn plus d’informations sur les réseaux virtuels Azure, démarrer avec les informations de hello ici : [vue d’ensemble du réseau virtuel Azure][VNETOverview]. 

Bonjour Azure App Service a deux formes. 

1. systèmes d’architecture mutualisée Hello qui prennent en charge la gamme complète de hello de plans de tarification
2. fonctionnalité premium d’environnement de Service d’application (ASE) de Hello, qui déploie dans votre réseau virtuel. 

Ce document présente l’intégration au réseau virtuel et non l’environnement App Service. Si vous souhaitez toolearn plus d’informations sur la fonctionnalité de hello ASE, démarrer avec les informations de hello ici : [présentation de l’environnement App Service][ASEintro].

Intégration de réseau virtuel permet de votre tooresources de l’accès d’application web dans votre réseau virtuel, mais n’accorde pas d’un accès privé tooyour web app à partir du réseau virtuel de hello. Accès au site privé fait référence toomaking votre application accessible uniquement à partir d’un réseau privé comme à partir d’un réseau virtuel Azure. L’accès privé aux sites est disponible uniquement via un ASE configuré avec un équilibreur de charge interne (ILB). Pour plus d’informations sur l’utilisation d’un environnement app service Équilibrage de charge interne, commencez par article hello ici : [création et à l’aide d’un environnement app service Équilibrage de charge interne][ILBASE]. 

Un scénario courant où vous pouvez utiliser l’intégration de réseau virtuel est l’activation de l’accès à partir de votre base de données web application tooa ou un service web en cours d’exécution sur une machine virtuelle dans votre réseau virtuel Azure. Avec l’intégration de réseau virtuel, vous n’avez pas besoin tooexpose un point de terminaison public pour les applications sur votre machine virtuelle, mais permet à la place de hello internet non routable des adresses privées. 

fonctionnalité d’intégration de réseau virtuel Hello :

* nécessite un plan de tarification Standard, Premium ou Isolé 
* fonctionne avec le réseau virtuel classique ou Gestionnaire des ressources 
* prend en charge les protocoles TCP et UDP ;
* fonctionne avec les applications web, mobiles et API
* permet à un tooonly de tooconnect application 1 réseau virtuel à la fois
* permet de toofive toobe de réseaux virtuels intégré à un plan App Service 
* permet de hello même toobe de réseau virtuel utilisé par plusieurs applications dans un Plan App Service
* prend en charge d’un contrat SLA de 99,9 % en raison de contrat SLA de toohello sur hello passerelle de réseau virtuel

Certains éléments ne sont pas pris en charge par l’intégration au réseau virtuel, notamment :

* montage d’un lecteur ;
* intégration AD ; 
* NetBios ;
* accès privé aux sites.

### <a name="getting-started"></a>Prise en main
Voici certaines choses tookeep à l’esprit avant de se connecter à votre réseau virtuel du tooa d’application web :

* L’intégration au réseau virtuel fonctionne uniquement avec des applications faisant partie d’un plan de tarification **Standard**, **Premium** ou **Isolé**. Si vous activez la fonctionnalité de hello et puis faire évoluer votre tooan Plan App Service non pris en charge de vos applications plan de tarification perdent leur toohello de connexions qu’ils utilisent des réseaux virtuels. 
* Si votre réseau virtuel cible existe déjà, il doit avoir des VPN de point-to-site activé avec une passerelle de routage dynamique avant de pouvoir être connectés tooan application. Vous ne pouvez pas activer le réseau privé virtuel (VPN) de point à site si votre passerelle est configurée avec un routage statique.
* réseau virtuel Hello doit être Bonjour même abonnement que votre Plan(ASP) de Service d’application. 
* les applications de Hello qui s’intègrent à un réseau virtuel utilisent hello DNS est spécifié pour ce réseau virtuel.
* Par défaut vos applications intégrées uniquement acheminer le trafic dans votre réseau virtuel selon les itinéraires hello qui sont définis dans votre réseau virtuel. 

## <a name="enabling-vnet-integration"></a>Activation de l’intégration au réseau virtuel
Ce document se concentre essentiellement sur à l’aide de hello portail Azure pour l’intégration de réseau virtuel. tooenable intégration de réseau virtuel avec votre application à l’aide de PowerShell, suivez les instructions de hello ici : [de connecter votre application tooyour réseau virtuel à l’aide de PowerShell][IntPowershell].

Vous avez hello option tooconnect votre application tooa existant ou nouveau réseau virtuel. Si vous créez un nouveau réseau dans le cadre de l’intégration, puis en outre la création de toojust hello réseau virtuel, une passerelle de routage dynamique est préconfigurée pour vous et Point tooSite VPN est activé. 

> [!NOTE]
> La configuration d’une nouvelle intégration au réseau virtuel peut prendre plusieurs minutes. 
> 
> 

tooenable intégration de réseau virtuel, ouvrez votre application de paramètres, puis sélectionnez mise en réseau. Hello l’interface utilisateur qui s’ouvre offre trois options de mise en réseau. Ce guide porte uniquement sur l’intégration au réseau virtuel. Cependant, les connexions hybrides et environnements App Service sont décrits plus loin dans ce document. 

Si votre application n’est pas correct de plan de tarification de hello, hello l’interface utilisateur vous permet de tooscale votre tooa de plan de tarification supérieur plan de votre choix.

![][1]

### <a name="enabling-vnet-integration-with-a-pre-existing-vnet"></a>Activation de l’intégration au réseau virtuel avec un réseau virtuel existant
Hello l’interface utilisateur de l’intégration de réseau virtuel vous permet de tooselect dans une liste de vos réseaux virtuels. Hello classique des réseaux virtuels indiquent qu’ils sont par exemple par le mot hello « Classique » dans le nom de réseau virtuel toohello suivant entre parenthèses. Hello liste triée telles que hello Gestionnaire de ressources VNets sont répertoriés en premier. Bonjour image illustré ci-dessous, vous pouvez voir que qu’un seul réseau virtuel peut être sélectionné. Un réseau virtuel peut être grisé pour plusieurs raisons, notamment :

* Hello réseau virtuel est dans un autre abonnement que votre compte a accès à
* Hello réseau virtuel n’a pas de tooSite Point activé
* Hello réseau virtuel ne dispose pas d’une passerelle de routage dynamique

![][2]

intégration de tooenable cliquez simplement sur hello réseau virtuel que vous souhaitez toointegrate avec. Après avoir sélectionné le réseau virtuel de hello, votre application est redémarrée automatiquement pour effet de tootake modifications hello. 

##### <a name="enable-point-toosite-in-a-classic-vnet"></a>Activer tooSite Point dans un réseau virtuel classique
Si votre réseau virtuel n’a pas d’une passerelle et a tooSite de Point, vous devez tooset d’abord haut. toodo pour un réseau virtuel classique, accédez toohello [portail Azure] [ AzurePortal] et afficher la liste de hello de Networks(classic) virtuel. À ce stade, cliquez sur le réseau hello vous souhaitez toointegrate avec, puis cliquez sur la grande boîte de hello sous Essentials appelé connexions VPN. À ce stade, vous pouvez créer des votre VPN de point toosite et même lui demander de créer une passerelle. Une fois que vous parcourez toosite de point hello avec l’expérience de création de passerelle, il est environ 30 minutes avant qu’il soit prêt. 

![][8]

##### <a name="enabling-point-toosite-in-a-resource-manager-vnet"></a>L’activation de tooSite Point dans un VNet le Gestionnaire de ressources
tooconfigure un gestionnaire de ressources VNet portant une passerelle et le Point de tooSite, vous pouvez utiliser PowerShell comme décrit ici, [configurer un réseau virtuel tooa connexion Point à Site à l’aide de PowerShell] [ V2VNETP2S] ou utilisez hello portail Azure comme décrit ici, [configurer un Point-to-Site connexion tooa réseau virtuel à l’aide de hello le portail Azure][V2VNETPortal]. Hello UI tooperform cette fonctionnalité n’est pas encore disponible. Notez que vous devez toocreate certificats pour la configuration de Point tooSite hello. Lorsque vous vous connectez votre toohello WebApp réseau virtuel est configuré automatiquement. 

### <a name="creating-a-pre-configured-vnet"></a>Création d’un réseau virtuel préconfiguré
Si vous souhaitez toocreate un nouveau réseau virtuel est configuré avec une passerelle et le Point-to-Site, puis hello mise en réseau de l’interface utilisateur du Service d’applications a hello capacité toodo mais uniquement pour un gestionnaire de ressources réseau virtuel. Si vous le souhaitez toocreate un réseau classique avec une passerelle et Point-to-Site, vous devez toodo cela manuellement via l’interface utilisateur de mise en réseau hello. 

toocreate un VNet le Gestionnaire de ressources via hello l’interface utilisateur de l’intégration de réseau virtuel, il suffit de sélectionner **créer un nouveau réseau virtuel** et fournir le :

* Nom du réseau virtuel
* Bloc d’adresses du réseau virtuel
* Nom du sous-réseau
* Bloc d’adresses du sous-réseau
* Bloc d’adresses de la passerelle
* Bloc d’adresses de point à site

Si vous souhaitez que cette tooany tooconnect de réseau virtuel autres réseaux, vous devez éviter de collecter l’espace d’adressage IP qui se chevauche avec ces réseaux. 

> [!NOTE]
> La création du Gestionnaire de ressources VNet avec une passerelle prend environ 30 minutes et actuellement n’intègre pas hello réseau virtuel avec votre application. Une fois votre réseau virtuel est créé avec la passerelle de hello, vous devez les toocome tooyour arrière application l’interface utilisateur de l’intégration de réseau virtuel, sélectionnez votre nouveau réseau virtuel.
> 
> 

![][3]

En règle générale, les réseaux virtuels Azure sont créés dans des plages d’adresses de réseau privées. Par hello de valeur par défaut intégration de réseau virtuel fonctionnalité achemine tout le trafic destiné à ces plages d’adresses IP dans votre réseau virtuel. plages d’adresses IP privées Hello sont :

* 10.0.0.0/8 - cela est hello même comme 10.0.0.0 - 10.255.255.255
* 172.16.0.0/12 - cela est hello même comme 172.16.0.0 - 172.31.255.255 
* 192.168.0.0/16 - cela est hello même en tant que 192.168.0.0 - 192.168.255.255

Hello espace d’adressage de réseau virtuel doit toobe spécifié dans la notation CIDR. Si vous n’êtes pas familiarisé avec la notation CIDR, il est une méthode permettant de spécifier des blocs d’adresses à l’aide d’une adresse IP et un entier qui représente le masque de réseau hello. À titre de référence rapide, considérez que 10.1.0.0/24 représenterait 256 adresses et 10.1.0.0/25 représenterait 128 adresses. Une adresse IPv4 avec /32 représenterait une seule adresse. 

Si vous définissez ici hello informations du serveur DNS, qui est définie pour votre réseau virtuel. Après la création du réseau virtuel, vous pouvez modifier ces informations à partir d’expériences utilisateur de réseau virtuel hello. Si vous modifiez hello DNS Hello réseau virtuel, vous devez tooperform une opération de synchronisation réseau.

Lorsque vous créez un réseau classique à l’aide de l’interface utilisateur de l’intégration de réseau virtuel de hello, il crée un réseau virtuel dans hello même groupe de ressources que votre application. 

## <a name="how-hello-system-works"></a>Fonctionnement du système hello
Dans les coulisses de hello cette fonctionnalité s’appuie sur le Point-to-Site VPN technologie tooconnect votre tooyour application réseau virtuel. Les applications dans Azure App Service présentent une architecture système mutualisée empêchant qu’une application soit directement approvisionnée dans un réseau virtuel comme dans le cas des machines virtuelles. En s’appuyant sur la technologie point-to-site nous limitons réseau accès toojust hello virtual machine hébergeant l’application hello. Réseau d’accès toohello est encore limité sur ces ordinateurs hôtes d’application afin que vos applications peuvent accéder uniquement aux réseaux hello les configurer tooaccess. 

![][4]

Si vous n’avez pas configuré un serveur DNS à votre réseau virtuel, toouse la ressource tooreach des adresses IP dans hello réseau virtuel est nécessaire à votre application. Lors de l’utilisation des adresses IP, n’oubliez pas que hello principal avantage de cette fonctionnalité est qu’il vous permet de toouse des adresses privées hello au sein de votre réseau privé. Si vous définissez votre application des toouse des adresses IP publiques pour l’une de vos machines virtuelles, vous n’utilisez pas de fonctionnalité d’intégration de réseau virtuel hello et communiquez via hello internet.

## <a name="managing-hello-vnet-integrations"></a>Gestion des intégrations de réseau virtuel hello
Hello tooconnect de capacité et s’en déconnecter tooa que réseau virtuel est au niveau de l’application. Les opérations qui peuvent affecter hello intégration de réseau virtuel entre plusieurs applications sont au niveau de ASP. À partir de l’interface utilisateur qui apparaît au niveau d’application hello de hello, vous pouvez obtenir des détails sur votre réseau virtuel. Plupart des mêmes informations sont également affichées à hello ASP au niveau de hello. 

![][5]

À partir de la page d’état de la fonctionnalité réseau hello, vous pouvez voir si votre application est connectée tooyour réseau virtuel. Si votre passerelle de réseau virtuel est en panne pour une raison quelconque, votre application apparaît comme non connectée. 

informations Hello vous avez maintenant tooyou disponible dans l’application hello niveau interface utilisateur de l’intégration de réseau virtuel même hello en tant qu’informations de détail hello vous obtenez à partir de hello ASP. Il s’agit des informations suivantes :

* Nom de réseau virtuel - ce lien ouvre hello réseau virtuel Azure de l’interface utilisateur
* Emplacement - Cela reflète emplacement hello de votre réseau virtuel. Il est possible de toointegrate avec un réseau virtuel dans un autre emplacement.
* État du certificat - il existe des certificats utilisés toosecure hello réseau VPN entre l’application hello et hello réseau virtuel. Cela reflète un tooensure test elles sont synchronisées.
* État de la passerelle - vos passerelles convient vers le bas pour une raison quelconque puis votre application ne peut pas accéder aux ressources hello réseau virtuel. 
* Espace d’adressage de réseau virtuel - il s’agit d’espace d’adressage IP hello pour votre réseau virtuel. 
* Espace d’adressage point tooSite - il s’agit d’espace d’adressage IP hello point toosite pour votre réseau virtuel. Votre application montre la communication comme provenant d’un des hello dans cet espace d’adressage des adresses IP. 
* Espace d’adressage de site toosite - vous pouvez utiliser un Site tooSite VPN tooconnect tooyour de votre réseau virtuel local tooother réseau virtuel ou ressources. Si vous avez configurés puis les plages d’adresses IP hello défini avec que connexion VPN s’affiche ici.
* Serveurs DNS : si des serveurs DNS sont configurés avec votre réseau virtuel, ils sont répertoriés ici.
* Adresses IP routées toohello réseau virtuel : il existe une liste d’adresses IP que votre réseau virtuel est défini pour le routage, et ces adresses affichent ici. 

Hello seule opération que vous pouvez prendre en mode d’application hello d’intégration de votre réseau virtuel est toodisconnect votre application à partir de hello il est actuellement connecté à des réseaux. toodo cet cliquez simplement sur se déconnecter haut hello. Cette action ne modifie pas votre réseau virtuel. Hello réseau virtuel et sa configuration, y compris les passerelles hello reste inchangé. Si vous souhaitez ensuite toodelete votre réseau virtuel, vous devez toofirst delete hello ressources qu’il contient, y compris les passerelles hello. 

Hello vue d’un Plan App Service a un nombre d’opérations supplémentaires. Il est également accessible différemment à partir de l’application hello. tooreach hello l’interface utilisateur de la mise en réseau ASP ouvrez simplement votre interface utilisateur d’ASP et faites défiler. L’interface utilisateur comporte l’élément État de la fonctionnalité réseau. Celui-ci offre quelques détails secondaires sur votre intégration au réseau virtuel. En cliquant sur cette interface utilisateur, hello état interface utilisateur de la fonctionnalité réseau s’ouvre. Si vous cliquez sur « Cliquez ici toomanage », hello l’interface utilisateur qui répertorie les hello intégrations de réseau virtuel dans cette ASP s’ouvre.

![][6]

Hello hello ASP est bonne tooremember en examinant les emplacements hello Hello vous intégrez à des réseaux virtuels. Lorsque hello réseau virtuel est dans un autre emplacement, vous êtes des problèmes de latence toosee beaucoup plus probables. 

Hello intégrées à des réseaux virtuels est un rappel sur le nombre de réseaux virtuels, que vos applications sont intégrées à cette ASP et le nombre que vous pouvez avoir. 

toosee ajouté plus d’informations sur chaque réseau virtuel, cliquez sur hello réseau virtuel qui vous intéressez. En outre toohello plus d’informations qui ont été indiquées précédemment, vous pouvez également voir une liste d’applications hello dans cette ASP qui sont à l’aide de ce réseau virtuel. 

En ce qui concerne tooactions il existe deux actions principales. Hello est tout d’abord les itinéraires tooadd hello capacité qui pilotent le trafic en laissant votre application dans votre réseau virtuel. action de deuxième Hello est certificats de toosync de capacité hello et des informations sur le réseau.

![][7]

**Routage** comme indiqué précédemment itinéraires hello qui sont définis dans votre réseau virtuel sont ce qui est utilisé pour diriger le trafic dans votre réseau virtuel à partir de votre application. Il existe certaines utilisations où les clients souhaitent toosend supplémentaires le trafic sortant à partir d’une application hello réseau virtuel et leur cette fonctionnalité est fournie. Que passe-t-il toohello trafic une fois que les clients de hello toohow configure leur réseau virtuel. 

**Certificats** hello état du certificat reflète une vérification est effectuée par hello toovalidate du Service d’applications que les certificats hello que nous utilisons pour hello connexion VPN sont toujours en bon état. Lors de l’intégration de réseau virtuel est activé, s’il s’agit hello toothat intégration premier réseau virtuel à partir de toutes les applications dans ce ASP, il n’est un échange requis de la sécurité de hello tooensure certificats de connexion de hello. En même temps que les certificats de hello, nous obtenons la configuration DNS hello, les itinéraires et les autres choses similaires qui décrivent le réseau de hello.
Si ces certificats ou des informations sur le réseau sont modifié, vous devez tooclick « Synchronisation réseau ». **REMARQUE** : lorsque vous cliquez sur « Synchronisation réseau », la connectivité entre votre application et votre réseau virtuel est brièvement interrompue. Pendant que votre application n’est pas redémarrée, hello une perte de connectivité pourrait correctement votre fonction toonot de site. 

## <a name="accessing-on-premises-resources"></a>Accès aux ressources sur site
Un des avantages de hello de fonctionnalité d’intégration de réseau virtuel hello est que si votre réseau virtuel est connecté tooyour sur site réseau avec un tooSite Site VPN puis vos applications peuvent avoir accès tooyour des ressources locales à partir de votre application. Pour cette toowork que vous devrez peut-être tooupdate votre passerelle VPN local avec hello route votre plage IP de Point tooSite. Lorsque hello Site tooSite VPN est tout d’abord configurer les scripts hello utilisée tooconfigure il doit définir des itinéraires, y compris votre VPN de Point tooSite. Si vous ajoutez hello VPN de Point tooSite après avoir créé votre tooSite Site VPN, vous devez les itinéraires hello tooupdate manuellement. Détails sur la façon dont toodo qui varient en fonction de passerelle et ne sont pas décrites ici. 

> [!NOTE]
> fonctionnalité d’intégration de réseau virtuel Hello n’intègre pas d’une application avec un réseau virtuel qui a une passerelle ExpressRoute. Même si hello passerelle ExpressRoute est configuré dans [mode de coexistence] [ VPNERCoex] hello intégration de réseau virtuel ne fonctionne pas. Si vous avez besoin de ressources tooaccess via une connexion ExpressRoute, vous pouvez ensuite utiliser un [environnement App Service][ASE], qui s’exécute dans votre réseau virtuel.
> 
> 

## <a name="pricing-details"></a>Détails de la tarification
Il existe quelques tarification nuances que vous devez être conscient lors de l’utilisation de la fonctionnalité d’intégration de réseau virtuel hello. Il existe 3 frais connexes toohello utiliser cette fonctionnalité :

* exigences liées au niveau tarifaire de l’ASP ;
* coût de transfert des données ;
* coûts de la passerelle VPN.

Pour votre toouse en mesure de toobe applications cette fonctionnalité, ils ont besoin toobe dans Standard ou Premium du Plan App Service. Pour plus d’informations sur les coûts, voir : [Tarification App Service][ASPricing]. 

En raison de façon toohello tooSite Point VPN sont gérés, vous devez toujours un coût pour le même si hello réseau virtuel se trouve dans les données sortantes via votre connexion de l’intégration de réseau virtuel hello même centre de données. toosee quelles sont ces frais, d’un coup de œil ici : [détails de tarification de transfert de données][DataPricing]. 

dernier élément de Hello est coût hello des passerelles de réseau virtuel hello. Si vous n’avez pas besoin des passerelles de hello pour quelque chose d’autre comme Site tooSite VPN, vous payez pour la fonctionnalité d’intégration de réseau virtuel passerelles toosupport hello. Pour plus d’informations sur ces coûts, voir : [tarification de passerelle VPN][VNETPricing]. 

## <a name="troubleshooting"></a>Résolution des problèmes
Alors que la fonctionnalité de hello est facile tooset, cela ne signifie pas que votre expérience sera problème libre. Si vous rencontrez des problèmes d’accès de votre point de terminaison souhaité il sont des utilitaires que vous pouvez utiliser une connexion de tootest à partir de la console d’application hello. Vous pouvez utiliser deux consoles : Un est à partir de la console de Kudu hello et hello autres console hello que vous pouvez atteindre Bonjour portail Azure. console de Kudu tooget toohello à partir de votre application accédez tooTools -> Kudu. Cela est hello même que si vous passez trop [sitename]. scm.azurewebsites.net. Une fois cet onglet tooget toohello Azure console hébergé portail puis à partir de votre application s’ouvre toohello accédez simplement débogage console accédez tooTools -> Console. 

#### <a name="tools"></a>Outils
un test ping Hello, nslookup et tracert ne fonctionnent pas via la console hello en raison de contraintes de toosecurity. toofill hello void il a été ajoutés deux outils. Dans la fonctionnalité d’ordre de DNS tootest, nous avons ajouté un outil nommé nameresolver.exe. syntaxe de Hello est :

    nameresolver.exe hostname [optional: DNS Server]

Vous pouvez utiliser nameresolver toocheck hello noms d’hôte qui dépend de votre application. De cette manière, vous pouvez tester si vous avez rien mal configurés avec votre serveur DNS ou que vous n’avez peut-être pas serveur d’accès tooyour DNS.

outil suivant de Hello vous permet de tootest pour TCP connectivité tooa hôte combinaison et du port. Cet outil est appelé tcpping.exe et syntaxe de hello est :

    tcpping.exe hostname [optional: port]

utilitaire de tcpping Hello vous indique si vous pouvez atteindre un ordinateur hôte spécifique et un port. Il peut s’afficher uniquement réussite si : il existe une application à l’écoute sur une combinaison d’hôte et le port hello et a accès au réseau de votre ordinateur hôte spécifié de toohello d’application et le port.

#### <a name="debugging-access-toovnet-hosted-resources"></a>Débogage tooVNet d’accès aux ressources hébergées
Plusieurs choses peuvent empêcher votre application d’atteindre un hôte et un port spécifiques. La plupart du temps de hello il est un des trois opérations :

* **Il existe un pare-feu Bonjour moyen** si vous avez un pare-feu de façon de hello, vous atteindrez le délai d’attente de hello TCP. Dans ce cas, il est de 21 secondes. Utiliser une connexion de hello tcpping outil tootest. Délais d’expiration TCP peut être en raison de réduire les choses derrière un pare-feu mais commencer de là. 
* **DNS n’est pas accessible** hello DNS délai est de trois secondes par le serveur DNS. Si vous avez deux serveurs DNS, délai d’attente hello est de 6 secondes. Utilisez nameresolver toosee si le serveur DNS fonctionne. Souvenez-vous que vous ne pouvez pas utiliser nslookup comme qui n’utilise pas hello DNS de votre réseau virtuel est configuré avec.
* **Plage non valide de P2S IP** toobe dans les plages IP privées hello RFC 1918 a besoin de plage d’adresses IP point toosite hello (10.0.0.0-10.255.255.255 / 172.16.0.0-172.31.255.255 / 192.168.0.0-192.168.255.255). Plage de hello utilise des adresses IP en dehors de qui, les éléments ne fonctionnent. 

Si ces éléments ne répondent pas votre problème, recherchez des opérations simples hello comme : 

* Hello passerelle apparaissent comme étant dans le portail de hello ?
* Les certificats s’affichent comme étant synchronisés ?
* A toute personne modifier configuration du réseau hello sans entraîner d’un réseau « Sync » dans hello affectée ASP ? 

Si votre passerelle est en panne, rétablissez-la. Si vos certificats ne sont pas synchronisées, puis accédez vue d’ASP toohello d’intégration de votre réseau virtuel et d’accès « Synchronisation réseau ». Si vous pensez qu’il y a eu une configuration de réseau virtuel tooyour modification apportée et il n’a pas été synchronisation feriez avec votre ASP, accédez vue d’ASP toohello d’intégration de votre réseau virtuel et d’accès juste « Réseau de synchronisation » comme un rappel, cela provoque une brève interruption avec votre connexion de réseau virtuel et de vos applications . 

Si tout est correct, vous devez toodig un peu plus approfondie :

* Sont il toutes les autres applications à l’aide des ressources de tooreach d’intégration de réseau virtuel dans hello même réseau virtuel ? 
* Atteindre la console d’application toohello et l’utiliser tcpping tooreach d’autres ressources dans votre réseau virtuel ? 

Si une des hello ci-dessus sont remplie, puis se pose l’intégration de votre réseau virtuel et problème de hello est dans un autre emplacement. Il s’agit où il obtient toobe plus complexe, car il n’existe aucun toosee facilement pourquoi vous ne peut pas atteindre un ordinateur hôte : port. Voici quelques-unes des causes de hello :

* vous avez un pare-feu sur votre hôte empêche les accès toohello application port à partir de votre plage IP de point de toosite. Des sous-réseaux croisés requièrent souvent un accès public.
* Votre hôte cible est hors-service.
* Votre application est arrêtée.
* vous aviez hello les IP incorrect ou le nom d’hôte
* Votre application est à l’écoute sur un port autre que celui que vous envisagiez. Vous pouvez le vérifier en accédant sur cet hôte et à l’aide de « netstat - aon » à partir de l’invite de commandes hello. Cette commande affiche l’ID de processus à l’écoute et le port correspondant. 
* groupes de sécurité de votre réseau sont configurés de manière à ce qu’ils empêchent les hôte d’application tooyour accès et le port à partir de votre plage IP de point de toosite

N’oubliez pas que vous ne connaissez pas le IP dans la plage IP de Point tooSite que votre application utilisera donc vous devez tooallow l’accès à partir de l’intégralité de la plage hello. 

Étapes de débogage supplémentaires :

* Connectez-vous à une autre machine virtuelle dans votre tooreach de réseau virtuel et la tentative de votre ressource : port de l’hôte à partir de là. Vous pouvez utiliser pour cela certains utilitaires ping TCP ou Telnet. Bonjour objectif ici est toodetermine seulement si la connexion est il à partir de cet autre ordinateur virtuel. 
* afficher une application sur un autre ordinateur virtuel et de tester l’hôte de toothat d’accès et le port de console hello à partir de votre application

#### <a name="on-premises-resources"></a>Ressources locales ####
Si votre application ne peut pas atteindre les ressources locales, hello première chose que vous devez vérifier est si vous pouvez atteindre une ressource dans votre réseau virtuel. Si cela fonctionne, essayez d’application de locale hello tooreach à partir d’une machine virtuelle dans hello réseau virtuel. Vous pouvez utiliser Telnet ou un utilitaire ping TCP. Si votre machine virtuelle ne peut pas atteindre votre ressource locale, puis vérifiez que votre connexion VPN de Site tooSite fonctionne. S’il fonctionne, puis vérifiez hello mêmes opérations indiquées précédemment, ainsi que l’état et la configuration de passerelle locale hello. 

Maintenant si votre réseau virtuel hébergé machine virtuelle peut accéder à votre système local, mais votre application ne peut pas de raison de hello est probablement de l’une des manières suivantes de hello :

* votre itinéraires ne sont pas configurés avec des plages IP votre point de toosite dans votre passerelle locale
* groupes de sécurité réseau sont bloque l’accès pour votre plage IP de Point tooSite
* votre pare-feu local bloquent le trafic à partir de votre plage IP de Point tooSite
* vous avez Route(UDR) de définie par un utilisateur dans votre réseau virtuel qui empêche votre trafic tooSite Point en fonction d’atteindre votre réseau local

## <a name="hybrid-connections-and-app-service-environments"></a>Connexions hybrides et environnements App Service
Il existe trois fonctionnalités qui permettent d’accéder aux ressources de tooVNet hébergé. Il s'agit de :

* Intégration au réseau virtuel
* les connexions hybrides
* Environnements App Service

Connexions hybrides requiert que vous tooinstall un agent de relais appelé hello Manager(HCM) de connexion hybride dans votre réseau. Hello HCM doit toobe tooconnect en mesure de tooAzure et également tooyour application. Cette solution est particulièrement efficace à partir d’un réseau distant, tel que votre réseau local ou un autre réseau hébergé dans le cloud, car elle ne nécessite pas de point de terminaison accessible sur Internet. Hello HCM s’exécute uniquement sous Windows, et vous pouvez avoir des instances toofive tooprovide haute disponibilité en cours d’exécution. Connexions hybrides prend uniquement en charge TCP cependant et chaque point de terminaison HC a la combinaison de port d’hôte spécifique : toomatch tooa. 

fonctionnalité de l’environnement de Service d’application Hello vous permet de toorun une instance de hello du Service d’applications Azure dans votre réseau virtuel. Ainsi, vos applications peuvent accéder aux ressources de votre réseau virtuel sans étapes supplémentaires. Certaines de hello d’autres avantages d’un environnement App Service sont que vous pouvez utiliser Dv2 en fonction des travailleurs avec des too14 Go de RAM. Un autre avantage est que vous pouvez faire évoluer hello système toomeet vos besoins. Contrairement aux environnements de plusieurs locataires hello où votre ASP est limitée too20 instances, dans un environnement app service vous pouvez faire évoluer des instances d’ASP too100. Une des choses hello que vous obtenez avec ASE pas avec l’intégration de réseau virtuel est qu’un environnement App Service peuvent travailler avec un VPN ExpressRoute. 

S’il existe que certains utilisent le chevauchement des cas, aucune de ces fonctionnalités peut remplacer les hello d’autres. Si vous savez quelles toouse fonctionnalité est liée tooyour besoins. Par exemple :

* Si vous êtes un développeur et simplement toorun un site dans Azure et souhaitez il accéder à base de données hello sur la station de travail hello sous votre bureau, hello plus simple chose toouse est connexions hybrides. 
* Si vous une grande organisation qui souhaite tooput un grand nombre de propriétés web dans un cloud public hello et les gérez dans votre propre réseau, vous souhaitez que toogo avec hello environnement App Service. 
* Si vous avez un nombre de Service d’applications hébergés les applications et simplement vouloir tooaccess des ressources dans votre réseau virtuel, puis intégration de réseau virtuel est toogo de façon hello. 

Au-delà de cas d’usage hello, il existe des raisons de simplicité liées aspects. Si votre réseau virtuel est déjà connecté tooyour local réseau, puis utiliser l’intégration de réseau virtuel ou un environnement App Service est un moyen simple tooconsume ressources locales. Hello autre part, si votre réseau virtuel n’est pas connecté réseau local de tooyour, il est beaucoup que plus tooset généraux d’un toosite site VPN avec votre réseau virtuel par rapport à l’installation hello HCM. 

Ultérieures hello différences fonctionnelles, il sont également prix. fonctionnalité de l’environnement de Service d’application Hello est un Premium offre de service, mais offre hello la plupart des possibilités de configuration de réseau en outre tooother excellentes fonctionnalités. Intégration de réseau virtuel peut être utilisée avec Standard ou Premium ASP et est parfaite pour la consommation des ressources dans votre réseau virtuel à partir de mutualisée hello du Service d’applications en toute sécurité. Connexions hybrides dépend actuellement un compte qui possède des niveaux qui démarrer libre, puis obtiennent progressivement plus coûteux de prix basé sur le montant hello de BizTalk. Lorsqu’il s’agit tooworking entre plusieurs réseaux Cependant, il n’existe aucune autre fonction comme connexions hybrides, ce qui peut vous permettre de ressources tooaccess de plus de 100 réseaux distincts. 

<!--Image references-->
[1]: ./media/web-sites-integrate-with-vnet/vnetint-upgradeplan.png
[2]: ./media/web-sites-integrate-with-vnet/vnetint-existingvnet.png
[3]: ./media/web-sites-integrate-with-vnet/vnetint-createvnet.png
[4]: ./media/web-sites-integrate-with-vnet/vnetint-howitworks.png
[5]: ./media/web-sites-integrate-with-vnet/vnetint-appmanage.png
[6]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanage.png
[7]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanagedetail.png
[8]: ./media/web-sites-integrate-with-vnet/vnetint-vnetp2s.png

<!--Links-->
[VNETOverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-overview/ 
[AzurePortal]: http://portal.azure.com/
[ASPricing]: http://azure.microsoft.com/pricing/details/app-service/
[VNETPricing]: http://azure.microsoft.com/pricing/details/vpn-gateway/
[DataPricing]: http://azure.microsoft.com/pricing/details/data-transfers/
[V2VNETP2S]: http://azure.microsoft.com/documentation/articles/vpn-gateway-howto-point-to-site-rm-ps/
[IntPowershell]: http://azure.microsoft.com/documentation/articles/app-service-vnet-integration-powershell/
[ASEintro]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro
[ILBASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/create-ilb-ase
[V2VNETPortal]: https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal
[VPNERCoex]: http://docs.microsoft.com/en-us/azure/expressroute/expressroute-howto-coexist-resource-manager
[ASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro
