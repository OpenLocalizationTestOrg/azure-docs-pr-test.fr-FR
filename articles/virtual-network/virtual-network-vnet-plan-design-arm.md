---
title: "aaaAzure réseau virtuel (VNet) Guide de conception et de Plan | Documents Microsoft"
description: "Découvrez comment tooplan et la conception des réseaux virtuels dans Azure en fonction de vos besoins d’isolation, la connectivité et emplacement."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 3a4a9aea-7608-4d2e-bb3c-40de2e537200
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/08/2016
ms.author: jdial
ms.openlocfilehash: f3ffadf8cf254f64b1f86b44f90315d2bc679f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-and-design-azure-virtual-networks"></a>Planifier et concevoir des réseaux virtuels Azure
Création d’un tooexperiment de réseau virtuel avec est assez facile, mais sans doute, vous allez déployer plusieurs réseaux virtuels sur les besoins de production temps toosupport hello de votre organisation. Avec une planification et conception, vous être en mesure de toodeploy des réseaux virtuels et connecter des ressources hello que vous avez besoin de manière plus efficace. Si vous n’êtes pas familiarisé avec les réseaux virtuels, il est recommandé que vous [en savoir plus sur les réseaux virtuels](virtual-networks-overview.md) et [comment toodeploy](virtual-networks-create-vnet-arm-pportal.md) un avant de continuer.

## <a name="plan"></a>Planification
Une bonne compréhension des abonnements Azure, des régions et des ressources réseau est essentielle pour réussir. Vous pouvez utiliser la liste hello considérations ci-dessous comme point de départ. Une fois que vous avez compris ces considérations, vous pouvez définir des spécifications de hello pour votre conception de réseau.

### <a name="considerations"></a>Considérations
Avant de répondre aux questions ci-dessous pour la planification de hello, tenez compte des éléments suivants de hello :

* Tout ce que vous créez dans Azure se compose d’une ou de plusieurs ressources. Un ordinateur virtuel (VM) est une ressource, interface de carte réseau hello (NIC) utilisé par un ordinateur virtuel est une ressource, adresse IP publique hello utilisé par une carte réseau est une ressource, hello de réseau virtuel hello carte réseau est connectée toois une ressource.
* Vous créez des ressources au sein d’une [région Azure](https://azure.microsoft.com/regions/#services) et d’un abonnement. Ressources peuvent uniquement être connecté tooa réseau virtuel qui existe dans hello même ressource de hello région et l’abonnement est en cours.
* Vous pouvez vous connecter à des réseaux virtuels tooeach autres à l’aide de :
    * **[Réseau virtuel d’homologation](virtual-network-peering-overview.md)**: les réseaux virtuels hello doivent exister dans hello même région Azure. La bande passante entre les ressources dans des réseaux virtuels ressources hello est identique comme si les ressources hello ont été connecté toohello même réseau virtuel.
    * **Azure [passerelle VPN](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)**: les réseaux virtuels hello peuvent exister dans hello identiques, ou différentes régions Azure. La bande passante entre les ressources dans des réseaux virtuels connectés via une passerelle VPN est limitée par la bande passante hello Hello passerelle VPN.
* Vous pouvez vous connecter à des réseaux virtuels tooyour sur réseau local à l’aide d’une des hello [les options de connectivité](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) disponibles dans Azure.
* Différentes ressources peuvent être regroupés dans [groupes de ressources](../azure-resource-manager/resource-group-overview.md#resource-groups), rendant la ressource de hello toomanage plus facilement en tant qu’unité. Un groupe de ressources peut contenir des ressources provenant de plusieurs régions, tant que ressources de hello appartiennent toohello même abonnement.

### <a name="define-requirements"></a>Définir les conditions requises
Utilisez les questions hello ci-dessous comme point de départ pour votre conception de réseau Azure.    

1. Les emplacements Azure seront vous utilisez toohost des réseaux virtuels ?
2. Avez-vous besoin de communication tooprovide entre ces emplacements Azure ?
3. Vous devez tooprovide communication entre votre VNet(s) Azure et vos centres locaux ?
4. Combien de machines virtuelles IaaS (Infrastructure as a Service), de rôles de services cloud et d’applications web sont nécessaires pour votre solution ?
5. Avez-vous besoin de trafic tooisolate basé sur des groupes d’ordinateurs virtuels (serveurs web frontaux c'est-à-dire et serveurs de base de données back-end) ?
6. Avez-vous besoin de flux de trafic toocontrol à l’aide des équipements virtuels ?
7. Faire les utilisateurs besoin de différents jeux d’autorisations toodifferent ressources Azure ?

### <a name="understand-vnet-and-subnet-properties"></a>Découvrir les propriétés des réseaux virtuels et sous-réseaux
Les ressources de réseaux virtuels et de sous-réseaux permettent de définir une limite de sécurité pour les charges de travail s’exécutant dans Azure. Un réseau virtuel est caractérisé par une collection d’espaces d’adressage, appelés blocs CIDR.

> [!NOTE]
> Les administrateurs réseau sont familiarisés avec la notation CIDR. Si vous n’êtes pas familiarisé avec CIDR, [obtenez davantage d’informations](http://whatismyipaddress.com/cidr).
>
>

Réseaux virtuels contiennent hello propriétés suivantes.

| Propriété | Description | Contraintes |
| --- | --- | --- |
| **name** |Nom du réseau virtuel |Chaîne de caractères en too80. Peut contenir des lettres, des chiffres, un trait de soulignement, des points ou des traits d’union. Doit commencer par une lettre ou un chiffre. Doit se terminer par une lettre, un chiffre ou un trait de soulignement. Peut contenir des majuscules ou minuscules. |
| **location** |Emplacement Azure (également désignée tooas région). |Doit être de hello emplacements Azure valides. |
| **addressSpace** |Collection de préfixes d’adresses qui composent hello réseau virtuel en notation CIDR. |Doit être un tableau de blocs d’adresses CIDR valides, y compris des plages d’adresses IP publiques. |
| **Sous-réseaux** |Collection des sous-réseaux qui composent hello réseau virtuel |consultez le tableau de propriétés du sous-réseau hello ci-dessous. |
| **dhcpOptions** |Objet qui contient une seule propriété obligatoire nommée **dnsServers**. | |
| **dnsServers** |Tableau des serveurs DNS utilisés par hello réseau virtuel. Si aucun serveur n’est spécifié, la résolution de noms interne Azure est utilisée. |Doit être un tableau de serveurs DNS too10, par adresse IP. |

Un sous-réseau est une ressource enfant d’un réseau virtuel, et permet de définir des segments d’espaces d’adressage dans un bloc CIDR, à l’aide de préfixes d’adresses IP. Cartes réseau peut être ajoutés toosubnets et tooVMs connecté, en offrant une connectivité pour différentes charges de travail.

Sous-réseaux contiennent hello propriétés suivantes.

| Propriété | Description | Contraintes |
| --- | --- | --- |
| **name** |Nom du sous-réseau |Chaîne de caractères en too80. Peut contenir des lettres, des chiffres, un trait de soulignement, des points ou des traits d’union. Doit commencer par une lettre ou un chiffre. Doit se terminer par une lettre, un chiffre ou un trait de soulignement. Peut contenir des majuscules ou minuscules. |
| **location** |Emplacement Azure (également désignée tooas région). |Doit être de hello emplacements Azure valides. |
| **addressPrefix** |Préfixe d’adresse unique qui composent le sous-réseau hello dans la notation CIDR |Doit être un bloc CIDR unique qui fait partie de l’un des espaces d’adressage de réseau virtuel hello. |
| **networkSecurityGroup** |Groupe de sécurité réseau appliqué toohello sous-réseau | |
| **routeTable** |Table d’itinéraires appliqué toohello sous-réseau | |
| **ipConfigurations** |Collection d’objets de configuration IP utilisés par les cartes réseau connectées toohello sous-réseau | |

### <a name="name-resolution"></a>Résolution de noms
Par défaut, votre réseau virtuel utilise [résolution de noms fournie par Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md) tooresolve noms à l’intérieur de hello réseau virtuel et sur hello Internet public. Toutefois, si vous vous connectez vos centres de données des réseaux virtuels tooyour local, vous devez tooprovide [votre propre serveur DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md) tooresolve des noms entre vos réseaux.  

### <a name="limits"></a>limites
Passez en revue les limites de mise en réseau de hello en hello [Azure limite](../azure-subscription-service-limits.md#networking-limits) tooensure article votre conception ne sont en conflit avec les limites de hello. Il est possible d’augmenter certaines limites par le biais d’un ticket d’assistance.

### <a name="role-based-access-control-rbac"></a>Contrôle d’accès en fonction du rôle
Vous pouvez utiliser [Azure RBAC](../active-directory/role-based-access-built-in-roles.md) toocontrol au niveau de hello d’accès des différents utilisateurs peut-être toodifferent ressources dans Azure. De cette façon, que vous pouvez isoler le travail hello effectué par votre équipe en fonction de leurs besoins.

Comme les réseaux virtuels sont concerne, les utilisateurs de hello **réseau collaborateur** rôle ont un contrôle total sur les ressources du réseau virtuel Azure Resource Manager. De même, les utilisateurs de hello **classique réseau collaborateur** rôle ont un contrôle total sur les ressources du réseau virtuel classique.

> [!NOTE]
> Vous pouvez également [créer vos propres rôles](../active-directory/role-based-access-control-configure.md) tooseparate vos besoins d’administration.
>
>

## <a name="design"></a>Conception
Une fois que vous connaissez les réponses hello questions toohello Bonjour [planifier](#Plan) section, consultez hello avant de définir vos réseaux virtuels.

### <a name="number-of-subscriptions-and-vnets"></a>Nombre d’abonnements et de réseaux virtuels
Vous devez envisager de créer plusieurs réseaux virtuels Bonjour les scénarios suivants :

* **Machines virtuelles qui doivent toobe placée dans différents emplacements Azure**. Les réseaux virtuels dans Azure sont régionaux. Ils ne peuvent pas couvrir des emplacements. Par conséquent, vous devez au moins un réseau virtuel pour chaque emplacement Azure que vous souhaitez des machines virtuelles de toohost dans.
* **Charges de travail qui toobe complètement isolé les uns des autres**. Vous pouvez créer des réseaux virtuels distincts, ce hello utilisez même mêmes espaces d’adressage IP, tooisolate différentes charges de travail à partir d’un autre.

Gardez à l’esprit que les limites de hello affichés ci-dessus sont par région, par abonnement. Cela signifie que vous pouvez utiliser plusieurs limite de hello tooincrease abonnements des ressources, que vous pouvez mettre à jour dans Azure. Vous pouvez utiliser un VPN de site à site ou d’un circuit ExpressRoute, tooconnect des réseaux virtuels dans des abonnements différents.

### <a name="subscription-and-vnet-design-patterns"></a>Modèles de conception des abonnements et réseaux virtuels
tableau de Hello ci-dessous présente certains modèles de conception courants pour l’utilisation des abonnements et des réseaux virtuels.

| Scénario | Diagramme | Avantages | Inconvénients |
| --- | --- | --- | --- |
| Abonnement unique, deux réseaux virtuels par application |![Abonnement unique](./media/virtual-network-vnet-plan-design-arm/figure1.png) |Qu’un seul abonnement toomanage. |Nombre maximal de réseaux virtuels par région Azure. Vous avez besoin d’abonnements supplémentaires après cela. Hello de révision [Azure limite](../azure-subscription-service-limits.md#networking-limits) article pour plus d’informations. |
| Un abonnement par application, deux réseaux virtuels par application |![Abonnement unique](./media/virtual-network-vnet-plan-design-arm/figure2.png) |Utilise uniquement deux réseaux virtuels par abonnement. |Toomanage plus difficile lorsqu’il y a trop d’applications. |
| Un abonnement par division, deux réseaux virtuels par application. |![Abonnement unique](./media/virtual-network-vnet-plan-design-arm/figure3.png) |Équilibre entre le nombre d’abonnements et de réseaux virtuels. |Nombre maximal de réseaux virtuel par division (abonnement). Hello de révision [Azure limite](../azure-subscription-service-limits.md#networking-limits) article pour plus d’informations. |
| Un abonnement par division, deux réseaux virtuels par groupe d’applications. |![Abonnement unique](./media/virtual-network-vnet-plan-design-arm/figure4.png) |Équilibre entre le nombre d’abonnements et de réseaux virtuels. |Les applications doivent être isolées à l’aide de sous-réseaux et de groupes de sécurité réseau. |

### <a name="number-of-subnets"></a>Nombre de sous-réseaux
Vous devez envisager plusieurs sous-réseaux dans un réseau virtuel Bonjour les scénarios suivants :

* **Pas suffisamment d’adresses IP privées pour toutes les cartes réseau dans un sous-réseau**. Si votre espace d’adressage de sous-réseau ne contient pas suffisamment d’adresses IP pour nombre hello de cartes réseau dans un sous-réseau de hello, vous devez toocreate plusieurs sous-réseaux. N’oubliez pas que Azure réserve 5 adresses IP privées à partir de chaque sous-réseau qui ne peut pas être utilisé : hello tout d’abord, et la dernière adresses de hello espace d’adressage (adresse de sous-réseau hello et multidiffusion) et toobe 3 adresses utilisées en interne (pour des raisons de DHCP et DNS).
* **Sécurité**. Vous pouvez utiliser des groupes de tooseparate sous-réseaux d’ordinateurs virtuels à partir d’un autre pour les charges de travail qui ont un multicouche de la structure et appliquer différents [réseau (NSG) les groupes de sécurité](virtual-networks-nsg.md#subnets) pour ces sous-réseaux.
* **Connectivité hybride**. Vous pouvez utiliser des passerelles VPN et des circuits ExpressRoute trop[connecter](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) tooone de vos réseaux virtuels un autre, et tooyour centres de données sur site. Passerelles VPN et des circuits ExpressRoute nécessitent un sous-réseau de leur propres toobe créé.
* **Équipements virtuels**. Vous pouvez utiliser un équipement virtuel, comme un pare-feu, un accélérateur WAN ou une passerelle VPN, dans un réseau virtuel Azure. Lorsque vous procédez ainsi, vous devez trop[acheminer le trafic](virtual-networks-udr-overview.md) toothose dispositifs et de les isoler dans leur propre sous-réseau.

### <a name="subnet-and-nsg-design-patterns"></a>Modèles de conception des sous-réseaux et groupes de sécurité réseau
tableau de Hello ci-dessous présente certains modèles de conception courants pour l’utilisation de sous-réseaux.

| Scénario | Diagramme | Avantages | Inconvénients |
| --- | --- | --- | --- |
| Sous-réseau unique, groupes de sécurité réseau par couche d’application, par application |![Sous-réseau unique](./media/virtual-network-vnet-plan-design-arm/figure5.png) |Qu’un seul sous-réseau toomanage. |Plusieurs tooisolate de groupes de sécurité réseau nécessaire chaque application. |
| Un sous-réseau par application, groupes de sécurité réseau par couche d’application |![Sous-réseau par application](./media/virtual-network-vnet-plan-design-arm/figure6.png) |Moins toomanage de groupes de sécurité réseau. |Toomanage de plusieurs sous-réseaux. |
| Un sous-réseau par couche d’application, groupes de sécurité réseau par application |![Sous-réseau par couche](./media/virtual-network-vnet-plan-design-arm/figure7.png) |Équilibre entre le nombre de sous-réseaux et de groupes de sécurité réseau. |Nombre maximal de groupes de sécurité réseau par abonnement. Hello de révision [Azure limite](../azure-subscription-service-limits.md#networking-limits) article pour plus d’informations. |
| Un sous-réseau par couche d’application, par application, groupes de sécurité réseau par sous-réseau |![Sous-réseau par couche et par application](./media/virtual-network-vnet-plan-design-arm/figure8.png) |Nombre éventuellement inférieur de groupes de sécurité réseau. |Toomanage de plusieurs sous-réseaux. |

## <a name="sample-design"></a>Exemple de conception
tooillustrate l’application hello d’informations de hello dans cet article, envisagez de hello scénario.

Vous travaillez pour une société qui possède 2 centres de données en Amérique du Nord et deux centres de données en Europe. Vous avez identifié des 6 différentes client faisant face à des applications gérées par 2 unités commerciales que vous souhaitez tooAzure toomigrate de pilote. architecture de base Hello pour les applications de hello sont les suivantes :

* App1, App2, App3 et App4 sont des applications web hébergées sur des serveurs Linux exécutant Ubuntu. Chaque application connecte tooa serveur d’application distinct qui héberge les services RESTful sur des serveurs Linux. les services RESTful Hello connectent la base de données MySQL tooa back-end.
* App5 et App6 sont des applications web hébergées sur des serveurs Windows exécutant Windows Server 2012 R2. Chaque application connecte à base de données SQL Server tooa back-end.
* Toutes les applications sont actuellement hébergées dans un des centres de données de la société hello en Amérique du Nord.
* centres de données locale Hello utilisent espace d’adressage 10.0.0.0/8 hello.

Vous devez disposer d’une solution de réseau virtuel qui répond aux hello suivant les exigences de toodesign :

* Aucune division ne doit être affectée par la consommation de ressources d’autres divisions.
* Vous devez réduire la quantité de hello de réseaux virtuels et sous-réseaux gestion toomake plus facile.
* Pour chaque division, un seul réseau virtuel de test/développement doit être utilisé pour toutes les applications.
* Chaque application est hébergée dans 2 centres de données Azure différents par continent (Amérique du Nord et Europe).
* Chaque application est totalement isolée des autres.
* Chaque application est accessible par les clients via hello Internet à l’aide de HTTP.
* Chaque application est accessible par les utilisateurs connectés toohello local des centres de données à l’aide d’un tunnel chiffré.
* Connexion des centres de données local tooon doivent utiliser des périphériques VPN existantes.
* Hello groupe de mise en réseau de l’entreprise doit avoir un contrôle total sur la configuration du réseau virtuel hello.
* Les développeurs dans chaque centre de profit doivent uniquement avoir des sous-réseaux tooexisting toodeploy en mesure de machines virtuelles.
* Toutes les applications seront migrées lorsqu’ils sont tooAzure (courbes d’élévation et MAJ).
* bases de données Hello dans chaque emplacement doivent répliquer tooother Azure emplacements une fois par jour.
* Chaque application doit utiliser 5 serveurs web frontaux, 2 serveurs d’applications (si nécessaire) et 2 serveurs de base de données.

### <a name="plan"></a>Planification
Vous devez commencer la conception de votre planification en répondant à la question hello Bonjour [définissent des spécifications](#Define-requirements) section comme indiqué ci-dessous.

1. Les emplacements Azure seront vous utilisez toohost des réseaux virtuels ?

    2 emplacements en Amérique du Nord et 2 emplacements en Europe. Vous devez choisir celles basées sur l’emplacement physique de hello de vos centres de données local existant. De cette façon, votre connexion à partir de votre tooAzure emplacements physiques aura une meilleure latence.
2. Avez-vous besoin de communication tooprovide entre ces emplacements Azure ?

    Oui. Étant donné que les bases de données hello doivent être répliquée tooall emplacements.
3. Vous devez tooprovide communication entre votre VNet(s) Azure et vos centres de données locale ?

    Oui. Étant donné que les utilisateurs connectés toohello des centres de données locale doivent être tooaccess en mesure des applications de hello via un tunnel chiffré.
4. Combien de machines virtuelles IaaS sont nécessaires pour votre solution ?

    200 machines virtuelles IaaS. App1, App2, App3 et App4 nécessitent 5 serveurs web chacun, 2 serveurs d’applications chacun et 2 serveurs de base de données chacun. Ce qui fait un total de 9 machines virtuelles IaaS par application ou 36 machines virtuelles IaaS. App5 et App6 nécessitent 5 serveurs web et 2 serveurs de base de données chacun. Ce qui fait un total de 7 machines virtuelles IaaS par application ou 14 machines virtuelles IaaS. Par conséquent, vous avez besoin de 50 machines virtuelles IaaS pour toutes les applications dans chaque région Azure. Étant donné que nous avons besoin des régions toouse 4, il y aura des machines virtuelles IaaS de 200.

    Vous devez également les serveurs DNS tooprovide dans chaque réseau virtuel, ou dans votre nom de tooresolve de centres de données local entre vos machines virtuelles IaaS de Azure et votre réseau local.
5. Avez-vous besoin de trafic tooisolate basé sur des groupes d’ordinateurs virtuels (serveurs web frontaux c'est-à-dire et serveurs de base de données back-end) ?

    Oui. Chaque application doit être totalement isolée des autres, et chaque couche d’application doit également être isolée.
6. Avez-vous besoin de flux de trafic toocontrol à l’aide des équipements virtuels ?

    Non. Équipements virtuels peuvent être utilisé tooprovide de mieux contrôler le flux de trafic, y compris une journalisation plus détaillée données plan.
7. Faire les utilisateurs besoin de différents jeux d’autorisations toodifferent ressources Azure ?

    Oui. équipe de mise en réseau Hello doit contrôle total sur les paramètres de mise en réseau virtuel hello, tandis que les développeurs ne doivent être en mesure de toodeploy leurs sous-réseaux toopre existant de machines virtuelles.

### <a name="design"></a>Conception
Vous devez suivre la conception de hello en spécifiant des abonnements, des réseaux virtuels, des sous-réseaux et des groupes de sécurité réseau. Nous abordons le sujet ici, mais vous devez en savoir plus sur les [groupes de sécurité réseau](virtual-networks-nsg.md) avant de terminer votre conception.

**Nombre d’abonnements et de réseaux virtuels**

Hello suivant les exigences est toosubscriptions connexes et les réseaux virtuels :

* Aucune division ne doit être affectée par la consommation de ressources d’autres divisions.
* Vous devez réduire la quantité de hello des réseaux virtuels et des sous-réseaux.
* Pour chaque division, un seul réseau virtuel de test/développement doit être utilisé pour toutes les applications.
* Chaque application est hébergée dans 2 centres de données Azure différents par continent (Amérique du Nord et Europe).

En fonction de ces conditions requises, vous avez besoin d’un abonnement pour chaque division. De cette façon, la consommation des ressources d’une division n’est pas prise en compte pour déterminer les limites d’autres divisions. Et dans la mesure où vous souhaitez que le nombre de hello toominimize de réseaux virtuels, vous devez envisager d’utiliser hello **un seul abonnement par unité commerciale, deux réseaux virtuels par groupe d’applications** de modèle comme indiqué ci-dessous.

![Abonnement unique](./media/virtual-network-vnet-plan-design-arm/figure9.png)

Vous devez également l’espace d’adressage toospecify hello pour chaque réseau virtuel. Étant donné que vous avez besoin de connectivité entre hello centres de données sur site hello régions Azure, l’espace d’adressage utilisé pour les réseaux virtuels Azure hello ne peut pas entrer en conflit avec un réseau local hello et espace d’adressage hello utilisé par chaque réseau virtuel ne doit pas entrer en conflit avec d’autres réseaux virtuels existants. Vous pouvez utiliser les espaces d’adressage hello dans la table hello ci-dessous toosatisfy ces exigences.  

| **Abonnement** | **Réseau virtuel** | **Région Azure** | **Espace d’adressage** |
| --- | --- | --- | --- |
| BU1 |ProdBU1US1 |Ouest des États-Unis |172.16.0.0/16 |
| BU1 |ProdBU1US2 |Est des États-Unis |172.17.0.0/16 |
| BU1 |ProdBU1EU1 |Europe du Nord |172.18.0.0/16 |
| BU1 |ProdBU1EU2 |Europe de l'Ouest |172.19.0.0/16 |
| BU1 |TestDevBU1 |Ouest des États-Unis |172.20.0.0/16 |
| BU2 |TestDevBU2 |Ouest des États-Unis |172.21.0.0/16 |
| BU2 |ProdBU2US1 |Ouest des États-Unis |172.22.0.0/16 |
| BU2 |ProdBU2US2 |Est des États-Unis |172.23.0.0/16 |
| BU2 |ProdBU2EU1 |Europe du Nord |172.24.0.0/16 |
| BU2 |ProdBU2EU2 |Europe de l'Ouest |172.25.0.0/16 |

**Nombre de sous-réseaux et de groupes de sécurité réseau**

Hello suivant les exigences est toosubnets connexes et les groupes de sécurité réseau :

* Vous devez réduire la quantité de hello des réseaux virtuels et des sous-réseaux.
* Chaque application est totalement isolée des autres.
* Chaque application est accessible par les clients via hello Internet à l’aide de HTTP.
* Chaque application est accessible par les utilisateurs connectés toohello local des centres de données à l’aide d’un tunnel chiffré.
* Connexion des centres de données local tooon doivent utiliser des périphériques VPN existantes.
* bases de données Hello dans chaque emplacement doivent répliquer tooother Azure emplacements une fois par jour.

En fonction de ces exigences, vous utilisez un sous-réseau par la couche d’application et a utiliser des groupes de sécurité réseau du trafic toofilter par application. De cette façon, vous avez uniquement 3 sous-réseaux dans chaque réseau virtuel (frontal, couche d’application et couche de données) et un groupe de sécurité réseau par application et par sous-réseau. Dans ce cas, vous devez envisager d’utiliser hello **un sous-réseau par la couche d’application, les groupes de sécurité réseau par application** modèle de conception. Hello figure ci-dessous utilisation hello de modèle de conception hello représentant hello **ProdBU1US1** réseau virtuel.

![Un sous-réseau par couche, un groupe de sécurité réseau par application et par couche](./media/virtual-network-vnet-plan-design-arm/figure11.png)

Toutefois, vous devez également toocreate un sous-réseau supplémentaire pour la connectivité VPN de hello entre hello des réseaux virtuels et vos centres de données locale. Et vous avez besoin d’espace d’adressage toospecify hello pour chaque sous-réseau. Hello figure ci-dessous un exemple de solution pour **ProdBU1US1** réseau virtuel. Vous pouvez répliquer ce scénario pour chaque réseau virtuel. Chaque couleur représente une application différente.

![Exemple de réseau virtuel](./media/virtual-network-vnet-plan-design-arm/figure10.png)

**Contrôle d’accès**

tooaccess connexes est Hello en matière de contrôle :

* Hello groupe de mise en réseau de l’entreprise doit avoir un contrôle total sur la configuration du réseau virtuel hello.
* Les développeurs dans chaque centre de profit doivent uniquement avoir des sous-réseaux tooexisting toodeploy en mesure de machines virtuelles.

En fonction de ces exigences, vous pouvez ajouter des utilisateurs à partir de hello toohello équipe intégrée de mise en réseau **réseau collaborateur** rôle dans chaque abonnement ; et créer un rôle personnalisé pour hello les développeurs d’applications pour chaque abonnement accorder à sous-réseaux de tooexisting les droits tooadd machines virtuelles.

## <a name="next-steps"></a>Étapes suivantes
* [Déployer un réseau virtuel](virtual-networks-create-vnet-arm-template-click.md) selon un scénario.
* Comprendre comment trop[équilibrer la charge](../load-balancer/load-balancer-overview.md) machines virtuelles IaaS et [gérer le routage entre plusieurs régions Azure](../traffic-manager/traffic-manager-overview.md).
* En savoir plus sur [groupes de sécurité réseau et la manière dont tooplan et de conception](virtual-networks-nsg.md) une solution de groupe de sécurité réseau.
* En savoir plus sur vos [options de connectivité de réseau virtuel et entre locaux](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti).
