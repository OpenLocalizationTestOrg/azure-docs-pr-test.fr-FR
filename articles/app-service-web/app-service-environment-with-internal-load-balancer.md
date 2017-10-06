---
title: "aaaCreating et à l’aide d’un équilibreur de charge interne avec un environnement App Service | Documents Microsoft"
description: "Création et utilisation d’un ASE avec un ILB"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: ad9a1e00-d5e5-413e-be47-e21e5b285dbf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 20799f260993d6e81499408e5b547a2e21430174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-an-internal-load-balancer-with-an-app-service-environment"></a>Utilisation d’un équilibreur de charge interne avec un environnement App Service

> [!NOTE] 
> Cet article porte sur hello environnement App Service v1. Il existe une version plus récente de hello environnement App Service toouse plus facile et s’exécute sur une infrastructure plus puissante. toolearn plus d’informations sur la nouvelle version de hello commencent par Bonjour [Introduction toohello environnement App Service](../app-service/app-service-environment/intro.md).
>

fonctionnalité d’environnement de Service d’application (ASE) Hello est une option de service Premium d’Azure App Service qui offre une fonctionnalité d’amélioration de la configuration qui n’est pas disponible dans les tampons d’architecture mutualisée hello. fonctionnalité de ASE Hello déploie essentiellement hello du Service d’applications Azure dans votre Network(VNet) virtuel Azure. toogain une meilleure compréhension des fonctionnalités de hello offertes par les environnements App Service lire hello [qu’est un environnement App Service] [ WhatisASE] documentation. Si vous ne connaissez pas les avantages hello de fonctionner dans un réseau virtuel lire hello [FAQ sur les réseaux virtuels Azure][virtualnetwork]. 

## <a name="overview"></a>Vue d'ensemble
Un environnement App Service peut être déployé avec un point de terminaison accessible via Internet ou avec une adresse IP sur votre réseau virtuel. Commande tooset hello IP adresse tooa adresse de réseau virtuel vous devez toodeploy votre ASE avec un Balancer(ILB) de charge interne. Lorsque votre ASE est configuré avec un équilibrage de charge interne, vous fournissez :

* votre propre domaine ou sous-domaine. toomake facilement, ce document suppose que le sous-domaine, mais vous pouvez le configurer dans les deux cas. 
* certificat Hello utilisé pour HTTPS
* Gestion du service DNS pour votre sous-domaine. 

En retour, vous pouvez effectuer des tâches telles que :

* héberger des applications intranet, comme des applications métier, en toute sécurité dans hello cloud auxquels vous l’accès via un ExpressRoute VPN ou un Site tooSite
* applications d’hôte dans le cloud de hello qui ne figurent pas dans les serveurs DNS publics
* créer des applications de serveur principal internet isolées auxquelles vos applications frontales peuvent s’intégrer en toute sécurité

#### <a name="disabled-functionality"></a>Fonctionnalités désactivées
Lorsque vous utilisez un ASE ILB, certaines opérations ne sont pas autorisées. Ces opérations sont :

* utilisation du protocole IPSSL
* affectation d’adresses IP toospecific applications
* l’achat et à l’aide d’un certificat avec une application via le portail de hello. Vous pouvez bien sûr toujours obtenir des certificats directement avec une autorité de certification et l’utiliser avec vos applications, mais pas par le biais de hello portail Azure.

## <a name="creating-an-ilb-ase"></a>Création d’un environnement App Service d’équilibrage de charge interne (ILB ASE)
La création d’un ILB ASE n’est pas très différente de la création d’un ASE normalement. Pour plus d’informations sur la création d’un environnement app service lire [comment tooCreate un environnement App Service][HowtoCreateASE]. toocreate de processus Hello ASE équilibrage de charge interne est hello identiques entre la création d’un réseau virtuel lors de la création de ASE ou en sélectionnant un réseau virtuel existant. toocreate ASE équilibrage de charge interne : 

1. Bonjour Azure sélectionnez portail **Nouveau -> Web + Mobile -> environnement App Service**
2. Sélectionnez votre abonnement
3. Sélectionnez ou créez un groupe de ressources
4. Sélectionnez ou créez un réseau virtuel
5. Créez un sous-réseau si vous sélectionnez un réseau virtuel
6. Sélectionnez **/emplacement de réseau virtuel -> Configuration du réseau virtuel** et ensemble hello tooInternal du Type d’adresse IP virtuelle
7. Fournir le nom de sous-domaine (il s’agit de sous-domaine hello utilisé pour les applications créées dans cette ASE)
8. Sélectionnez Ok puis Créer

![][1]

Dans le panneau de réseau virtuel hello, il existe une option de Configuration du réseau virtuel. Elle vous permet de sélectionner une adresse VIP externe ou interne. valeur par défaut Hello est externe. Si vous l’avez définie tooExternal votre ASE utilisera une adresse IP virtuelle accessible internet. Si vous sélectionnez Interne, votre ASE sera configuré avec un équilibrage de charge sur une adresse IP au sein de votre réseau virtuel interne. 

Après avoir sélectionné interne, hello tooadd capacité plusieurs adresses tooyour QU'ASE est supprimé et au lieu de cela, vous devez sous-domaine de hello tooprovide Hello ASE. Dans un environnement app service avec un hello adresse IP externe nom de hello ASE est utilisé dans le sous-domaine de hello pour les applications créées dans ce ASE. Si votre ASE a été appelé ***contosotest*** et votre application dans ce ASE a été appelée ***MonTest*** , le sous-domaine de hello est de format de hello ***contosotest.p.azurewebsites.net*** et Hello URL pour cette application serait ***mytest.contosotest.p.azurewebsites.net***. Si vous définissez hello tooInternal du Type d’adresse IP virtuelle, votre nom de ASE n’est pas utilisé dans le sous-domaine de hello pour hello ASE. Vous spécifiez explicitement sous-domaine de hello. Si votre sous-domaine a été ***contoso.corp.net*** et effectuée d’une application dans la mesure où ASE nommé ***timereporting*** puis hello URL pour cette application serait ***timereporting.contoso.corp.net***.

## <a name="apps-in-an-ilb-ase"></a>Applications d’un ILB ASE
Création d’une application dans un environnement app service Équilibrage de charge interne est hello identique à la création d’une application dans un environnement app service normalement. 

1. Bonjour Azure sélectionnez portail **Nouveau -> Web + Mobile -> Web** ou **Mobile** ou **application API**
2. Entrez le nom de l’application
3. Sélectionnez un abonnement
4. Sélectionnez ou créez un groupe de ressources
5. Sélectionnez ou créez un plan App Service (ASP). Si la création d’un nouveau ASP puis sélectionnez votre ASE comme emplacement de hello et le pool de travail Sélectionnez hello vous souhaitez que votre toobe ASP créé dans. Lorsque vous créez hello ASP vous sélectionnez votre ASE comme emplacement de hello et le pool de travail hello. Lorsque vous spécifiez le nom hello de l’application hello que vous verrez ce sous-domaine hello sous le nom de votre application est remplacé par sous-domaine de hello pour votre ASE. 
6. Sélectionnez Créer. Vous devez sélectionner hello **toodashboard du code confidentiel** case à cocher si vous souhaitez hello application tooshow sur votre tableau de bord. 

![][2]

Sous l’application hello nom de sous-domaine hello obtient sous-domaine de hello tooreflect mis à jour de votre ASE. 

## <a name="post-ilb-ase-creation-validation"></a>Validation après la création de l’ILB ASE
Un environnement app service Équilibrage de charge interne est légèrement différent que hello non - équilibrage de charge interne ASE. Comme déjà indiqué vous devez toomanage votre propre serveur DNS et que vous avez tooprovide votre propre certificat pour les connexions HTTPS. 

Après avoir créé votre ASE vous noterez que ce sous-domaine hello montre sous-domaine de hello, vous avez spécifié et il est un nouvel élément Bonjour **paramètre** menu appelé **certificat de l’équilibrage de charge interne**. Hello ASE est créé avec un certificat auto-signé qui le rend plus facile tootest HTTPS. Hello portail vous indiquera que vous avez besoin de tooprovide votre propre certificat pour le protocole HTTPS, mais il s’agit de toodrive toohave un certificat qui accompagne votre sous-domaine. 

![][3]

Si vous essayez simplement les choses et que vous ne connaissez pas toocreate un certificat, vous pouvez utilisation hello MMC IIS toocreate d’application console a self signé le certificat. Une fois qu’il est créé, vous pouvez l’exporter dans un fichier .pfx et puis le télécharger dans hello l’interface utilisateur du certificat équilibrage de charge interne. Lorsque vous avez accès à un site sécurisé avec un certificat auto-signé, votre navigateur vous donne un avertissement qui hello site que vous accédez à n’est pas sécurisée en raison de certificats de toohello incapacité toovalidate hello. Si vous souhaitez tooavoid cet avertissement, que vous avez besoin d’un certificat signé qui correspond à votre sous-domaine et qui possède une chaîne d’approbation n’est reconnue par votre navigateur.

![][6]

Si vous souhaitez tootry hello flux avec vos propres certificats et tester ASE de tooyour accès HTTP et HTTPS :

1. Accédez tooASE l’interface utilisateur après avoir créé ASE **ASE -> Paramètres -> certificats de l’équilibrage de charge interne**
2. Définissez le certificat ILB en sélectionnant le fichier .pfx du certificat et fournissez un mot de passe. Cette étape prend un peu de lors de la tooprocess et hello message d’une opération de mise à l’échelle en cours est affiché.
3. Obtenir l’adresse d’équilibrage de charge interne hello pour votre ASE (**ASE -> Propriétés -> adresse IP virtuelle**)
4. Création d’une application web dans ASE après sa création 
5. Créer une machine virtuelle si vous n’en avez pas dans ce réseau virtuel (pas dans hello même sous-réseau que hello ASE ou de tâches)
6. Configurez le DNS de votre sous-domaine. Vous pouvez utiliser un caractère générique avec votre sous-domaine dans votre système DNS ou si vous souhaitez toodo des tests simples, modifier le fichier d’hôtes de hello sur votre machine virtuelle tooset web app Nom tooVIP adresse IP. Si votre ASE avait le nom de sous-domaine hello. ilbase.com et que vous effectuées hello web application mytestapp afin que serait traitée au mytestapp.ilbase.com ensuite définir dans votre fichier hosts. (Sur Windows hello hôtes fichier est à C:\Windows\System32\drivers\etc\)
7. Utilisez un navigateur sur cette machine virtuelle et accédez toohttp://mytestapp.ilbase.com (ou tout ce qui est par le nom de votre application web avec votre sous-domaine)
8. Utilisez un navigateur sur cette machine virtuelle et aller toohttps://mytestapp.ilbase.com avoir manque de hello tooaccept de sécurité si vous utilisez un certificat auto-signé. 

adresse IP de Hello pour votre équilibrage de charge interne est répertorié dans les propriétés en tant qu’adresse IP virtuelle de hello

![][4]

## <a name="using-an-ilb-ase"></a>Utilisation d’un ILB ASE
#### <a name="network-security-groups"></a>Network Security Group
Un équilibrage de charge interne ASE Active l’isolement réseau pour vos applications comme hello applications ne sont pas accessibles ou même connues par Bonjour internet. Cette méthode est excellente pour l’hébergement de sites intranet comme les applications métier. Lorsque vous avez besoin toorestrict accès même vous pouvez davantage toujours utiliser l’accès toocontrol Groups(NSGs) de sécurité réseau au niveau du réseau hello. 

Si vous le souhaitez toouse NSG toofurther restreindre l’accès, puis vous devez toomake que vous n’interrompez pas la communication de hello que ASE hello doit dans l’ordre toooperate. Bien que hello accès HTTP/HTTPS est uniquement par le biais de hello équilibrage de charge interne utilisé par hello hello ASE QU'ASE dépend toujours de ressource en dehors de hello réseau virtuel. toosee quel accès réseau est encore nécessaire examiner les informations de hello dans le document de hello sur [tooan de contrôler le trafic entrant environnement App Service] [ ControlInbound] et document hello sur [réseau Détails de configuration pour les environnements App Service avec ExpressRoute][ExpressRoute]. 

tooconfigure vos groupes de sécurité réseau vous devez tooknow hello IP adresse qui est utilisé par Azure toomanage votre ASE. Cette adresse IP est également hello sortant adresse IP de votre ASE s’il utilise les demandes internet. Hello sortant adresse IP de votre ASE reste statique pour la durée de vie de hello de votre ASE. Si vous supprimez et recréez votre ASE, vous obtenez une nouvelle adresse IP. toofind cette adresse IP accédez trop**Paramètres -> Propriétés** et recherche hello **adresse IP sortante**. 

![][5]

#### <a name="general-ilb-ase-management"></a>Gestion générale de l’ILB ASE
La gestion d’un environnement app service Équilibrage de charge interne est en grande partie hello identique à la gestion d’un environnement app service normalement. Vous avez besoin de tooscale de votre toohost de pools de travail de plusieurs instances d’ASP et monter les volumes de toohandle augmenté de serveurs Front-End du trafic HTTP/HTTPS. Pour obtenir des informations générales sur la gestion de configuration hello de ASE, lire le document de hello sur [configuration d’un environnement App Service][ASEConfig]. 

éléments de gestion supplémentaires Hello sont la gestion des certificats et gestion DNS. Vous devez tooobtain et téléchargez le certificat hello utilisé pour le protocole HTTPS, après la création de l’équilibrage de charge interne ASE et remplacez avant son expiration. Étant donné que Azure possède le domaine de base hello nous pouvons fournir des certificats pour ASEs avec une adresse IP externe. Étant donné que le sous-domaine hello utilisé par un environnement app service Équilibrage de charge interne peut être quoi que ce soit, vous devez tooprovide votre propre certificat pour le protocole HTTPS. 

#### <a name="dns-configuration"></a>Configuration DNS
Lorsque vous utilisez un hello d’adresse IP externe que DNS est géré par Azure. N’importe quelle application créée dans votre ASE est automatiquement ajoutée tooAzure DNS qui est un serveur DNS public. Dans un environnement app service Équilibrage de charge interne ont toomanage votre propre serveur DNS. Pour un sous-domaine spécifique, tel que contoso.corp.net, vous devez toocreate pour qu'a DNS enregistre cette adresse d’équilibrage de charge interne point tooyour :

    * 
    *.scm ftp publish 


## <a name="getting-started"></a>Prise en main
Tous les articles et comment-de pour les environnements App Service sont disponibles dans hello [fichier Lisezmoi pour les environnements de Service d’Application](../app-service/app-service-app-service-environments-readme.md).

tooget démarré avec les environnements de Service d’application, consultez [Introduction tooApp environnements de Service][WhatisASE]

Pour plus d’informations sur la plateforme Azure App Service de hello, consultez [Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createilbase.png
[2]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createapp.png
[3]: ./media/app-service-environment-with-internal-load-balancer/ilbase-newase.png
[4]: ./media/app-service-environment-with-internal-load-balancer/ilbase-vip.png
[5]: ./media/app-service-environment-with-internal-load-balancer/ilbase-externalvip.png
[6]: ./media/app-service-environment-with-internal-load-balancer/ilbase-ilbcertificate.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[vnetnsgs]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
