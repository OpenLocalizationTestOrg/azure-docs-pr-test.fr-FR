---
title: aaaAzure ExpressRoute pour les fournisseurs de solutions de Cloud | Documents Microsoft
description: Cet article fournit des informations pour les fournisseurs de services Cloud qui tooincorporate que vous souhaitez Azure ExpressRoute dans ses offres et des services.
documentationcenter: na
services: expressroute
author: richcar
manager: carmonm
editor: 
ms.assetid: f6c5f8ee-40ba-41a1-ae31-67669ca419a6
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: richcar
ms.openlocfilehash: 062ecbb5e461e4384b01c4ac478cab696b7ed398
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-for-cloud-solution-providers-csp"></a>ExpressRoute pour les fournisseurs de solutions Cloud (CSP)
Microsoft fournit des services de Hyper-mise à l’échelle pour revendeurs traditionnels et de fourniture de toorapidly en mesure de serveurs de distribution (CSP) toobe nouveaux services et solutions pour vos clients sans hello doivent tooinvest dans le développement de ces nouveaux services. tooallow hello fournisseur de solutions de Cloud (CSP) hello capacité toodirectly gérer ces nouveaux services, Microsoft fournit des programmes et des API qui autorisent des ressources Microsoft Azure hello CSP toomanage pour vos clients. L’une de ces ressources est ExpressRoute. ExpressRoute permet de hello CSP tooconnect client ressources tooAzure des services existants. ExpressRoute est un tooservices de lien de communications privées à haut débit dans Azure. 

ExpresRoute se compose d’une paire de circuits pour la haute disponibilité qui sont le seul client tooa attaché un ou plusieurs abonnements et ne peut pas être partagé par plusieurs clients. Chaque circuit doit se terminer dans une autre routeur toomaintain hello haute disponibilité.

> [!NOTE]
> ExpressRoute présente des limites de bande passante et de connexion, ce qui signifie que les implémentations de grande envergure/complexes nécessiteront plusieurs circuits ExpressRoute pour un seul client.
> 
> 

Microsoft Azure fournit un nombre croissant de services que vous pouvez offrir aux clients de tooyour.  toobest tirer parti de ces services requiert l’utilisation hello ExpressRoute connexions tooprovide à haut débit à faible latence accès toohello Microsoft environnement Azure.

## <a name="microsoft-azure-management"></a>Gestion de Microsoft Azure
Microsoft fournit CSP API toomanage abonnements de client Azure hello en autorisant l’intégration avec vos propres systèmes de gestion de service par programme. Les fonctionnalités de gestion prises en charge sont indiquées [ici](https://msdn.microsoft.com/library/partnercenter/dn974944.aspx).

## <a name="microsoft-azure-resource-management"></a>Gestion des ressources Microsoft Azure
Selon hello contrat avec votre client déterminent comment les abonnement hello seront géré. Hello CSP peut gérer directement de la création de hello et la gestion de ressources ou de client de hello peut gérer le contrôle de hello abonnement Microsoft Azure et créer des ressources Azure hello nécessaire. Si votre client gère la création des ressources dans leur abonnement Microsoft Azure hello qu’ils utiliseront un des deux modèles : « Se connecter via » modèle, ou « Direct-To ». Ces modèles sont décrites en détail dans les sections suivantes de hello.  

### <a name="connect-through-model"></a>Modèle « Connect-through »
![alt text](./media/expressroute-for-cloud-solution-providers/connect-through.png)  

Dans le modèle de se connecter via hello, hello CSP crée une connexion directe entre votre centre de données et d’abonnement Azure de votre client. connexion directe de Hello est effectuée à l’aide d’ExpressRoute, vous connectez votre réseau avec Azure. Votre client connecte ensuite tooyour réseau. Ce scénario nécessite que le client hello traverse hello CSP réseau tooaccess services Azure. 

Si votre client a d’autres abonnements Azure non gérés par vous hello, il convient d’utiliser hello Internet public ou leurs propres services de toothose tooconnect connexion privée configurés sous l’abonnement du fournisseur de services cryptographiques non hello. 

Pour le fournisseur de services cryptographiques la gestion des services Azure, il est supposé que hello CSP a une identité client précédemment établie stocker qui est ensuite répliqué dans Azure Active Directory pour la gestion de leur abonnement CSP via Administrate-On-Behalf-Of (AOBO). Incluent des pilotes clés pour ce scénario où un partenaire donné ou un fournisseur de services a une relation établie avec le client de hello, client de hello consomme actuellement des services de fournisseur ou partenaire de hello possède un tooprovide désir une combinaison de hébergées par un fournisseur les solutions hébergés par Azure tooprovide flexibilité et l’adresse client défis et qui ne peut pas être satisfaites par un seul fournisseur de services cryptographiques. Ce modèle est présenté dans la **Figure**, ci-dessous.

![alt text](./media/expressroute-for-cloud-solution-providers/connect-through-model.png)

### <a name="connect-toomodel"></a>Toomodel se connecter
![alt text](./media/expressroute-for-cloud-solution-providers/connect-to.png)

Bonjour toomodel de se connecter, fournisseur de services hello crée une connexion directe entre le centre de données de leurs clients et abonnement Azure via ExpressRoute hello du client (customer) configuré hello CSP réseau.

> [!NOTE]
> Pour ExpressRoute client de hello aurait besoin toocreate et mettre à jour de circuit ExpressRoute de hello.  
> 
> 

Ce scénario de connectivité requiert que le client hello se connecte directement à l’aide d’un tooaccess de réseau client géré par le fournisseur de services cryptographiques abonnement Azure, à l’aide d’une connexion directe au réseau créée, détenue et gérée entièrement ou en partie par le client de hello. Pour ces clients, il est supposé que fournisseur de hello ne dispose pas actuellement d’un magasin d’identités client établi et fournisseur de hello aiderait client de hello dans la réplication de son magasin d’identité actuelle dans Azure Active Directory pour la gestion de leurs abonnement via AOBO. Les pilotes clés pour ce scénario incluent où un partenaire donné ou un fournisseur de services a une relation établie avec le client de hello, client de hello consomme actuellement des services de fournisseur ou partenaire de hello a un désir tooprovide des services qui sont basées uniquement sur Solutions de hébergés par Azure sans hello avoir besoin d’un centre de données de fournisseur existant ou d’infrastructure.

![alt text](./media/expressroute-for-cloud-solution-providers/connect-to-model.png)

Hello choix entre ces deux options sont basées sur les besoins de vos clients et vos besoin tooprovide Azure services. Hello des détails sur ces modèles et hello associées de contrôle d’accès basé sur le rôle, mise en réseau, et les modèles de conception d’identité sont couverts dans les détails dans hello suivant liens :

* **Contrôle d’accès basé sur les rôles (RBAC)** : RBAC repose sur Azure Active Directory.  Pour plus d’informations concernant Azure RBAC, cliquez [ici](../active-directory/role-based-access-control-configure.md).
* **Mise en réseau** – couvre hello différentes rubriques de mise en réseau dans Microsoft Azure.
* **Azure Active Directory (AAD)** – AAD fournit la gestion des identités hello pour les applications SaaS 3e et Microsoft Azure. Pour plus d’informations sur Azure AD, cliquez [ici](https://azure.microsoft.com/documentation/services/active-directory/).  

## <a name="network-speeds"></a>Vitesses du réseau
ExpressRoute prend en charge les vitesses de réseau à partir de 50 Mo/s too10Gb/s. Cela permet aux clients toopurchase hello quantité de bande passante nécessaire pour leur environnement unique.

> [!NOTE]
> La bande passante réseau peut être augmentée en fonction des besoins sans interrompre les communications, mais la vitesse du réseau tooreduce hello requiert la destruction de circuit de hello et la recréer à vitesse réseau la plus faible hello.  
> 
> 

ExpressRoute prend en charge la connexion hello de plusieurs réseaux virtuels tooa même circuit ExpressRoute pour optimiser l’utilisation des connexions plus rapides de hello. Un même circuit ExpressRoute peut être partagé entre plusieurs abonnements Azure hello appartenant au même client.

## <a name="configuring-expressroute"></a>Configuration d’ExpressRoute
ExpressRoute peut être configuré toosupport trois des types de trafic ([les domaines de routage](#ExpressRoute-routing-domains)) sur un même circuit ExpressRoute. Ce trafic se répartit entre homologation Microsoft, homologation publique Azure et homologation privée. Vous pouvez choisir un ou tous les types de toobe le trafic envoyé sur un même circuit ExpressRoute ou utiliser plusieurs circuits ExpressRoute selon la taille de hello de circuit ExpressRoute de hello et d’isolation de la part de votre client. posture de sécurité Hello du client peut ne pas autorise public du trafic et tootraverse trafic privé sur hello même circuit.

### <a name="connect-through-model"></a>Modèle « Connect-through »
Un Bonjour de se connecter via la configuration, vous serez responsable de toutes les hello réseau tooconnect fondements vos abonnements de toohello de ressources de centre de données clients hébergés dans Azure. Chacun de vos clients de choix toouse fonctionnalités Azure sera peut-être leur propre connexion ExpressRoute, qui est gérée par hello vous. Hello vous utiliserez hello même client hello de méthodes utiliseriez circuit ExpressRoute de hello tooprocure. Hello vous suivrez hello mêmes étapes décrites dans l’article de hello [ExpressRoute workflows](expressroute-workflows.md) pour l’approvisionnement et les États du circuit. Hello que vous configurerez ensuite hello protocole BGP (Border Gateway) itinéraires toocontrol hello tout trafic entre le réseau local de hello et réseau virtuel Azure.

### <a name="connect-toomodel"></a>Toomodel se connecter
Dans une connexion-tooconfiguration, votre client déjà une tooAzure connexion existante ou génèrent un fournisseur de services internet connexion toohello ExpressRoute de liaison à partir de votre centre de données du client tooAzure directement, au lieu de votre centre de données. processus d’approvisionnement hello toobegin, votre client suivez les étapes de hello comme décrit dans le modèle de se connecter via hello, ci-dessus. Une fois que le circuit de hello a été établie, votre client devra tooconfigure hello local routeurs toobe tooaccess en mesure de votre réseau et les réseaux virtuels Azure.

Vous pouvez aider à configurer la connexion de hello et configuration hello achemine les ressources de hello tooallow dans votre toocommunicate centres de ressources du client hello dans votre centre de données ou avec des ressources hello hébergées dans Azure.

## <a name="expressroute-routing-domains"></a>Domaines de routage ExpressRoute
ExpressRoute propose trois domaines de routage : publics, privés et homologation Microsoft. Chacun des domaines de routage hello sont configurés avec les routeurs identiques dans la configuration active-active pour la haute disponibilité. Pour plus d’informations sur les domaines de routage ExpressRoute, cliquez [ici](expressroute-circuit-peerings.md).

Vous pouvez définir des itinéraires personnalisés filtres tooallow uniquement hello ou vous voulez tooallow ou que vous avez besoin. Pour plus d’informations ou toosee toomake ces modifications voir l’article : [créer et modifier le routage pour un circuit ExpressRoute à l’aide de PowerShell](expressroute-howto-routing-classic.md) pour plus d’informations sur les filtres de routage.

> [!NOTE]
> Pour Microsoft et pour l’homologation publique connectivité doit être si une adresse IP publique appartienne hello client ou un fournisseur de services cryptographiques et doit respecter les règles tooall défini. Pour plus d’informations, consultez hello [conditions préalables d’ExpressRoute](expressroute-prerequisites.md) page.  
> 
> 

## <a name="routing"></a>Routage
ExpressRoute connecte toohello Azure réseaux via hello passerelle de réseau virtuel Azure. Les passerelles de réseau assurent le routage pour les réseaux virtuels Azure.

Créer des réseaux virtuels Azure crée également une table de routage par défaut pour le trafic toodirect hello réseau virtuel à partir de sous-réseaux hello de réseau virtuel de hello. Si la table d’itinéraires par défaut hello est insuffisant pour la solution hello personnalisée itinéraires peuvent être créés tooroute appliances de toocustom le trafic sortant ou tooblock achemine toospecific sous-réseaux ou réseaux externes.

### <a name="default-routing"></a>Routage par défaut
table d’itinéraires par défaut Hello inclut hello suivant itinéraires :

* Routage dans un sous-réseau
* Sous-réseau à un réseau virtuel de hello
* toohello Internet
* Réseau virtuel vers réseau virtuel à l’aide de la passerelle VPN
* Réseau virtuel vers réseau local à l’aide d’une passerelle VPN ou ExpressRoute

![alt text](./media/expressroute-for-cloud-solution-providers/default-routing.png)  

### <a name="user-defined-routing-udr"></a>Itinéraire défini par l’utilisateur (UDR)
Itinéraires définis par l’utilisateur autorisent le contrôle hello du trafic sortant à partir de hello affecté sous-réseau sous-réseaux tooother réseau virtuel de hello ou sur un de hello autres passerelles prédéfinies (ExpressRoute ; internet ou VPN). table de routage système par défaut Hello peut être remplacé par une table de routage défini par l’utilisateur qui remplace la table de routage par défaut hello avec des itinéraires personnalisés. Avec le routage de défini par l’utilisateur, les clients créez tooappliances itinéraires spécifiques tels que les pare-feux ou des dispositifs de détection d’intrusion, ou bloquer l’accès des sous-réseaux toospecific à partir du sous-réseau hello itinéraire défini par l’utilisateur de hello d’hébergement. Pour avoir une vue d’ensemble des itinéraires définis par l’utilisateur, cliquez [ici](../virtual-network/virtual-networks-udr-overview.md). 

## <a name="security"></a>Sécurité
Selon le modèle est en cours d’utilisation, Connect-tooor se connecter à, votre client définit les stratégies de sécurité hello dans leur réseau virtuel, ou fournit des exigences de stratégie de sécurité hello toohello CSP toodefine tootheir des réseaux virtuels. Hello suivant des critères de sécurité peut être définie :

1. **Isolation du client** : hello plateforme Windows Azure fournit isolation du client en stockant les informations d’ID de client et le réseau virtuel dans une base de données sécurisée, qui est utilisé tooencapsulate trafic de chaque client dans un tunnel GRE.
2. **Réseau de groupe de sécurité (NSG)** règles permettent de définir le trafic autorisé vers et depuis des sous-réseaux hello dans des réseaux virtuels dans Azure. Par défaut, hello NSG contiennent bloc règles tooblock le trafic de réseau virtuel de hello Internet toohello et règles d’autorisation pour le trafic au sein d’un réseau virtuel. Pour plus d’informations concernant les groupes de sécurité réseau, cliquez [ici](https://azure.microsoft.com/blog/network-security-groups/).
3. **Le tunneling forcé** : il s’agit d’un tooredirect option internet lié le trafic provenant de toobe Azure redirigé sur hello ExpressRoute connexion toohello sur le centre de données local. Pour plus d’informations sur le tunneling forcé, cliquez [ici](expressroute-routing.md#advertising-default-routes).  
4. **Chiffrement** , même si des circuits ExpressRoute hello sont tooa dédié des clients spécifiques, il est possibilité hello qui hello du fournisseur de réseau a enfreint, le trafic de paquet tooexamine permettant à un intrus. tooaddress sur que ce potentiel, un client ou fournisseur de services cryptographiques peut chiffrer le trafic hello connexion en définissant des stratégies de mode de tunnel IPSec pour tout le trafic circulant entre hello sur les ressources de site et des ressources Azure (consultez toohello facultatif en mode de Tunnel IPSec pour le client 1 dans la Figure 5 : ExpressRoute sécurité, ci-dessus). deuxième option de Hello serait toouse un dispositif de pare-feu au niveau de chaque point de terminaison hello Hello circuit ExpressRoute. Vous devrez toobe de machines virtuelles et des équipements installé sur les deux extrémités du trafic de hello tooencrypt via le circuit ExpressRoute de hello de pare-feu tiers 3e supplémentaires.

![alt text](./media/expressroute-for-cloud-solution-providers/expressroute-security.png)  

## <a name="next-steps"></a>Étapes suivantes
Hello service du fournisseur de solutions de Cloud fournit une tooincrease de façon que vos clients de tooyour valeur sans hello ont besoin pour les achats infrastructure et de la fonctionnalité coûteuses, tout en conservant votre position en tant que fournisseur d’externalisation principal hello. Intégration transparente avec Microsoft Azure peut être obtenue via hello CSP API, ce qui permet de gestion toointegrate de Microsoft Azure au sein de vos infrastructures de gestion existant.  

Vous trouverez des informations supplémentaires à hello suivant liens :

[Programme des fournisseurs de solutions Cloud Microsoft](https://partner.microsoft.com/en-US/Solutions/cloud-reseller-overview).  
[Obtenir tootransact prêt en tant qu’un fournisseur de solutions de Cloud](https://partner.microsoft.com/en-us/solutions/cloud-reseller-pre-launch).  
[Ressources des fournisseurs de solutions cloud Microsoft](https://partner.microsoft.com/en-us/solutions/cloud-reseller-resources).

