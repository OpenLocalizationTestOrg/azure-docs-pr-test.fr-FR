---
title: "aaaGetting a démarré avec la sécurité de Microsoft Azure | Documents Microsoft"
description: "Cet article fournit une vue d’ensemble des fonctionnalités de sécurité de Microsoft Azure et les considérations générales pour les organisations qui effectuent une migration leur fournisseur de cloud tooa actifs."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 8d8a0088-c85a-48e7-bd04-2bc7b78b0691
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: c61dd99ffd0143bc7b165367dadadc977ffcf47b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-microsoft-azure-security"></a>Prise en main de la sécurité de Microsoft Azure
Lorsque vous générez ou migrez le fournisseur de cloud de tooa de ressources informatiques, vous recourez tooprotect des capacités de cette organisation vos applications et les données avec les services hello et contrôles hello ils sécurisent hello toomanage vos ressources de cloud.

L’infrastructure Azure est conçu de tooapplications de fonctionnalité hello pour l’hébergement des millions de clients simultanément, et fournit une base fiable sur laquelle entreprises peuvent répondre aux besoins de leur sécurité. En outre, Azure vous offre un large éventail de toocontrol de capacité hello et les options de sécurité configurables leur afin que vous pouvez personnaliser les exigences uniques de hello toomeet sécurité de vos déploiements.

Dans cet article de présentation sur la sécurité Azure, nous allons examiner les points suivants :

* Services Azure et les fonctionnalités que vous pouvez utiliser toohelp sécurisent vos services et les données dans Azure.
* Comment Microsoft protège toohelp d’infrastructure Azure hello protéger vos données et applications.

## <a name="identity-and-access-management"></a>Gestion de l’identité et de l’accès
Il est essentiel de contrôle de l’infrastructure d’accès tooIT, les données et applications. Microsoft Azure fournit ces fonctionnalités par le biais de services tels qu’Azure Active Directory (Azure AD), Stockage Azure et la prise en charge de nombreuses normes et API.

[Azure AD](../active-directory/active-directory-whatis.md) est un référentiel d’identités et un moteur qui fournit l’authentification, l’autorisation et le contrôle d’accès pour les utilisateurs, groupes et objets d’une organisation. Azure AD offre également aux développeurs une gestion efficace des identités toointegrate dans leurs applications. La prise en charge de protocoles standard comme [SAML 2.0](https://en.wikipedia.org/wiki/SAML_2.0), [WS-Federation](https://msdn.microsoft.com/library/bb498017.aspx) et [OpenID Connect](http://openid.net/connect/) permet l’identification sur différentes plateformes telles que .NET, Java, Node.js et PHP.

Hello basé sur REST l’API Graph permet aux développeurs tooread et écriture toohello le répertoire à partir de n’importe quelle plateforme. Grâce à la prise en charge [d’OAuth 2.0](http://oauth.net/2/), les développeurs peuvent concevoir des applications web et mobiles qui s’intègrent aux API web Microsoft et tierces, et créer leurs propres API web sécurisées. Des bibliothèques clientes open source sont disponibles pour .Net, le Windows Store, iOS et Android, et des bibliothèques supplémentaires sont en cours de développement.

### <a name="how-azure-enables-identity-and-access-management"></a>Comment Azure permet la gestion de l’identité et de l’accès
Azure AD peut servir de répertoire cloud autonome pour votre organisation, ou de solution intégrée avec votre Active Directory local existant. Certaines fonctionnalités d’intégration incluent la synchronisation de répertoire et l’authentification unique (SSO). Étendre la portée hello de vos identités locales existantes dans le cloud de hello et les améliorer hello admin et l’expérience utilisateur.

Parmi les autres fonctionnalités pour la gestion de l’identité et de l’accès :

* Azure AD active [SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) applications tooSaaS, quel que soit l’endroit où elles sont hébergées. Certaines applications sont fédérées avec Azure AD, d’autres utilisent le mot de passe de l’authentification unique. Les applications fédérées peuvent également prendre en charge l’approvisionnement d’utilisateurs et la mise au coffre des mots de passe.
* Toodata d’accès dans [Azure Storage](https://azure.microsoft.com/services/storage/) est contrôlé via l’authentification. Chaque compte de stockage possède une clé primaire ([clé de compte de stockage](https://msdn.microsoft.com/library/azure/ee460785.aspx), ou SAK) et une clé secrète secondaire (signature d’accès partagé hello ou SAS).
* Azure AD fournit l’identité en tant que service par le biais de la fédération en utilisant les [services de fédération Active Directory (AD FS)](../active-directory/fundamentals-identity.md), la synchronisation et la réplication avec les annuaires locaux.
* [L’authentification multifacteur Azure](../multi-factor-authentication/multi-factor-authentication.md) est le service d’authentification multifacteur hello qui requiert des connexions utilisateurs tooverify à l’aide d’une application mobile, un appel téléphonique ou un message texte. Il peut être utilisé avec Azure AD toohelp sécurisée des ressources locales avec le serveur de l’authentification multifacteur Azure hello, ainsi qu’avec des applications personnalisées et les répertoires à l’aide du Kit de développement logiciel de hello.
* [Les Services de domaine Active Directory Azure](https://azure.microsoft.com/services/active-directory-ds/) vous permet de joindre le domaine tooa de machines virtuelles sans déployer des contrôleurs de domaine. Vous pouvez signer dans des machines virtuelles toothese avec vos informations d’identification Active Directory d’entreprise et administrer les ordinateurs virtuels appartenant à un domaine à l’aide des lignes de base de sécurité de stratégie de groupe tooenforce sur toutes vos machines virtuelles Azure.
* [Azure B2C Active Directory](https://azure.microsoft.com/services/active-directory-b2c/) fournit un service de gestion d’identité globale hautement disponible pour les applications consommateur qui s’adapte toohundreds de millions d’identités. Le service peut être intégré sur l’ensemble des plateformes web et mobiles. Vos consommateurs peuvent se connecter tooall vos applications par le biais des expériences personnalisables à l’aide de leurs comptes sociaux existants ou en créant de nouvelles informations d’identification.

## <a name="data-access-control-and-encryption"></a>Contrôle d’accès aux données et chiffrement
Microsoft utilise les principes de hello de séparation des droits et [moindre privilège](https://en.wikipedia.org/wiki/Principle_of_least_privilege) tout au long des opérations de Azure. Toodata d’accès par le personnel de support Azure nécessite l’autorisation explicite et est accordé sur une base « juste-à-temps » qui est enregistrée et auditée, puis révoqué après l’achèvement de l’engagement hello.

En outre, Azure fournit plusieurs fonctionnalités de protection des données en transit et au repos, notamment des fonctions de chiffrement pour les données, fichiers, applications, services, communications et lecteurs. Vous pouvez chiffrer les informations avant de les placer dans Azure, et également stocker des clés dans vos centres de données locaux.

![Microsoft Antimalware dans Azure](./media/azure-security-getting-started/sec-azgsfig1.PNG)

### <a name="azure-encryption-technologies"></a>Technologies de chiffrement Azure
Vous pouvez collecter des détails sur l’environnement d’abonnement tooyour d’un accès administratif à l’aide de [Azure AD Reporting](../active-directory/active-directory-reporting-audit-events.md). Vous pouvez configurer la fonction [Chiffrement de lecteur BitLocker](https://technet.microsoft.com/library/cc732774.aspx) sur les disques durs virtuels contenant des informations sensibles dans Azure.

Autres fonctionnalités dans Azure qui vous aidera tookeep que vos données :

* Les développeurs peuvent créer de chiffrement dans les applications hello ils déploient dans Azure à l’aide de Windows de hello [CryptoAPI](https://msdn.microsoft.com/library/ms867086.aspx) et .NET Framework.
* Contrôler complètement clés hello avec chiffrement côté client pour le stockage d’objets Blob Azure. service de stockage Hello voit les clés hello jamais et ne peut pas déchiffrer les données de salutation.
* [Azure Rights Management (Azure RMS)](https://technet.microsoft.com/library/jj585026.aspx) (avec hello [RMS SDK](https://msdn.microsoft.com/library/dn758244.aspx)) fournit des fichiers et la prévention de chiffrement et les fuites de données au niveau des données via la gestion de l’accès basé sur la stratégie.
* Azure prend en charge le [chiffrement au niveau table et au niveau colonne](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/12/recommendations-for-using-cell-level-encryption-in-azure-sql-database.aspx) dans les machines virtuelles SQL Server, ainsi que les serveurs gestionnaires de clés locaux tiers dans les centres de données.
* Clés de compte de stockage, les Signatures d’accès partagé, les certificats de gestion et les autres clés sont unique tooeach locataire Azure.
* Azure [StorSimple](http://www.microsoft.com/server-cloud/products/storsimple/overview.aspx) stockage hybride chiffre les données via une paire de clés publique/privée 128 bits avant de le télécharger tooAzure stockage.
* Azure prend en charge et utilise de nombreux mécanismes de chiffrement, y compris SSL/TLS, IPsec et AES, en fonction des transports, les conteneurs et les types de données hello.

## <a name="virtualization"></a>Virtualisation
Hello plateforme Azure utilise un environnement virtualisé. Les instances utilisateur fonctionnent comme des machines virtuelles autonomes qui n’ont pas de serveur d’accès tooa hôte physique, et l’isolation est appliquée à l’aide de physique [les niveaux de privilège de processeur (en anneau-0/en anneau-3)](https://en.wikipedia.org/wiki/Protection_ring).

Anneau 0 est hello plus privilégié et 3 hello moins. système d’exploitation invité de Hello exécute 1 moindre privilège en anneau et les applications exécutées hello moins privilégié en anneau 3. Cette virtualisation des ressources physiques conduit tooa distinction claire entre le système d’exploitation invité et l’hyperviseur, ce qui entraîne une séparation de sécurité supplémentaire entre hello deux.

Hello hyperviseur Azure agit comme un micro-noyau et passe toutes les demandes d’accès matériel à partir de l’invité virtual machines toohello hôte pour le traitement à l’aide d’une interface de mémoire partagée appelée VMBus. Cela empêche les utilisateurs d’obtenir un système de toohello l’accès en lecture/écriture/exécution brut et réduit le risque de hello du partage des ressources système.

![Microsoft Antimalware dans Azure](./media/azure-security-getting-started/sec-azgsfig2.PNG)

### <a name="how-azure-implements-virtualization"></a>Comment Azure implémente la virtualisation
Azure utilise un pare-feu hyperviseur (filtre de paquets) qui est implémenté dans hello hyperviseur et configuré par un agent de contrôleur de l’ensemble fibre optique. Cela contribue à protéger les clients contre les accès non autorisés. Par défaut, tout le trafic est bloqué quand un ordinateur virtuel est créé, et l’agent du contrôleur hello fabric configure ensuite tooadd de filtre de paquets hello *règles et les exceptions* tooallow au trafic autorisé.

Il existe deux catégories de règles qui sont programmées ici :

* **Règles de configuration des machines ou d’infrastructure** : par défaut, toutes les communications sont bloquées. Il est des exceptions tooallow un toosend de machine virtuelle et de recevoir du trafic DHCP et DNS. Machines virtuelles peuvent également envoyer le trafic toohello « public » internet et envoyer le trafic tooother machines virtuelles dans un cluster de hello et le serveur d’activation hello du système d’exploitation. liste des ordinateurs virtuels Hello des destinations sortantes autorisées n’inclut pas de sous-réseaux de routeur Azure, Azure management back-end et les autres propriétés de Microsoft.
* **Fichier de configuration de rôle**: définit hello entrants listes de contrôle d’accès (ACL) basées sur le modèle de service du client hello. Par exemple, si un client possède un serveur Web frontal sur le port 80 sur un certain ordinateur virtuel, puis Azure ouvre TCP port 80 tooall des adresses IP si vous configurez un point de terminaison Bonjour [modèle de déploiement classique Azure](../azure-resource-manager/resource-manager-deployment-model.md). Si l’ordinateur virtuel de hello a un rôle fin ou de travail en cours d’exécution, puis il ouvre hello travail rôle toohello machine virtuelle uniquement au sein de hello du même client.

## <a name="isolation"></a>Isolation
Une autre exigence de sécurité importantes cloud est tooprevent de séparation non autorisé et non intentionnelle transfert d’informations entre les déploiements dans une architecture mutualisée partagée.

Azure implémente le [contrôle d’accès réseau](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/) et la répartition par le biais de l’isolation des réseaux locaux virtuels (VLAN), des ACL, des équilibreurs de charge et des filtres IP. Elle restreint le trafic externe entrant tooports et protocoles sur vos ordinateurs virtuels que vous définissez. Azure implémente filtrage tooprevent usurpée trafic réseau et limitent les composants de la plateforme tootrusted le trafic entrant et sortant. Les stratégies de flux de trafic sont implémentées sur des dispositifs de protection des limites refusant le trafic par défaut.

![Microsoft Antimalware dans Azure](./media/azure-security-getting-started/sec-azgsfig3.PNG)

Traduction d’adresses réseau (NAT) est utilisé tooseparate le trafic réseau interne du trafic externe. Le trafic interne n’est pas routable en externe. Les [adresses IP virtuelles](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx) qui sont routables en externe sont traduites en adresses [IP dynamiques internes](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx) qui sont uniquement routables dans Azure.

Machines virtuelles de tooAzure trafic externe est protégée par un pare-feu via des listes ACL sur les routeurs, les équilibreurs de charge et les commutateurs de couche 3. Seuls les protocoles connus spécifiques sont autorisés. Les ACL sont les machines virtuelles invitées provenant des réseaux locaux virtuels tooother utilisés pour la gestion du trafic de toolimit sur place. En outre, le trafic filtré via des filtres IP hello système d’exploitation hôte autres limites hello le trafic sur les deux couches de réseau et de la liaison de données.

### <a name="how-azure-implements-isolation"></a>Comment Azure implémente l’isolation
Hello contrôleur de structure Azure est chargé d’allouer des ressources d’infrastructure tootenant les charges de travail, et qu’elle gère une communication unidirectionnelle à partir d’ordinateurs toovirtual hello. Hello hyperviseur Azure applique la mémoire et séparation du processus entre les machines virtuelles et achemine en toute sécurité aux clients tooguest du système d’exploitation de trafic réseau. Azure implémente également l’isolation pour les clients, le stockage et les réseaux virtuels.

* Chaque client Azure AD est isolé logiquement à l’aide des limites de sécurité.
* Comptes de stockage Azure sont uniques tooeach abonnement, et l’accès doit être authentifié à l’aide d’une clé de compte de stockage.
* Les réseaux virtuels sont isolés logiquement grâce à une combinaison d’adresses IP privées uniques, de pare-feu et d’ACL IP. Équilibreurs de charge acheminer le trafic toohello appropriée aux clients en fonction des définitions de point de terminaison.

## <a name="virtual-networks-and-firewalls"></a>Réseaux virtuels et pare-feu
Hello [des réseaux virtuels et distribuées](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx) dans l’aide d’Azure, assurez-vous que votre trafic réseau privé est logiquement isolé du trafic sur d’autres réseaux virtuels Azure.

![Microsoft Antimalware dans Azure](./media/azure-security-getting-started/sec-azgsfig4.PNG)

Votre abonnement peut contenir plusieurs réseaux privés isolés (et inclure des pare-feu, un équilibrage de charge et une traduction d’adresses réseau).

Azure propose trois niveaux principaux de segmentation de réseau dans chaque Azure toologically du trafic séparé du cluster. [Réseaux locaux virtuels](https://azure.microsoft.com/services/virtual-network/) (virtuels VLAN) est utilisés le trafic de client tooseparate reste hello Hello réseau Azure. Toohello d’accès réseau Azure à partir du cluster en dehors de hello est restreint via les équilibreurs de charge.

Tooand du trafic réseau des machines virtuelles doit passer par le commutateur hyperviseur hello. composant de filtre IP Hello dans le système d’exploitation de la racine hello isole hello racine ordinateur virtuel les machines virtuelles invitées hello et les machines virtuelles invitées hello entre eux. Il effectue le filtrage de la communication de toorestrict le trafic entre les nœuds d’un locataire et les hello Internet public (selon la configuration du service du client hello), les séparer des autres clients.

filtre d’IP Hello empêche les machines virtuelles invitées à partir de :

* Générer un trafic falsifié
* Réception du trafic ne pas adressés toothem.
* Diriger le trafic tooprotected infrastructure points de terminaison.
* Envoyer ou recevoir du trafic de diffusion inapproprié

Vous pouvez placer vos machines virtuelles sur les [réseaux virtuels Azure](https://azure.microsoft.com/documentation/services/virtual-network/). Ces réseaux virtuels est des réseaux toohello similaires, vous configurez dans les environnements locaux, où ils sont généralement associés à un commutateur virtuel. Machines virtuelles connectées toohello même réseau virtuel peut communiquer entre eux sans configuration supplémentaire. Vous pouvez également configurer différents sous-réseaux au sein de votre réseau virtuel.

Vous pouvez utiliser hello suivant des communications sécurisées de réseau virtuel Azure technologies toohelp sur votre réseau virtuel :

* [**Groupes de sécurité réseau (NSG)**](../virtual-network/virtual-networks-nsg.md). Vous pouvez utiliser un tooone de trafic toocontrol groupe de sécurité réseau ou de plusieurs instances de machine virtuelle dans votre réseau virtuel. Un groupe de sécurité réseau contient les règles de contrôle d’accès qui autorisent ou refusent le trafic en fonction de la direction du trafic, du protocole, de l’adresse et du port source ainsi que de l’adresse et du port de destination.
* [**Routage défini par l’utilisateur**](../virtual-network/virtual-networks-udr-overview.md). Vous pouvez contrôler hello routage des paquets via un équipement virtuel en créant des itinéraires définis par l’utilisateur qui spécifient le saut suivant de hello pour les paquets entrants appliances de sécurité de tooa sous-réseau spécifique toogo tooa réseau virtuel.
* [**Transfert IP**](../virtual-network/virtual-networks-udr-overview.md). Un dispositif de sécurité de réseau virtuel doit être tooreceive en mesure de trafic entrant qui n’est pas tooitself dédié. tooallow un tooreceive de machine virtuelle du trafic adressé tooother destinations, vous activez le transfert IP pour l’ordinateur virtuel de hello.
* [**Tunneling forcé**](../vpn-gateway/vpn-gateway-about-forced-tunneling.md). Le tunneling forcé vous permet de rediriger ou de « forcer » tout le trafic Internet généré par vos machines virtuelles dans un emplacement de locale précédent tooyour réseau virtuel via un tunnel VPN de site à site pour l’inspection et d’audit
* [**ACL de point de terminaison**](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Vous pouvez contrôler quels ordinateurs sont autorisées les connexions entrantes à partir de l’ordinateur virtuel de hello Internet tooa sur votre réseau virtuel en définissant l’ACL de point de terminaison.
* [**Solutions de sécurité réseau de partenaires**](https://azure.microsoft.com/marketplace/). Il existe un nombre de solutions de sécurité de réseau partenaire que vous pouvez accéder à partir de hello Azure Marketplace.

### <a name="how-azure-implements-virtual-networks-and-firewalls"></a>Mode d’implémentation par Azure des réseaux virtuels et des pare-feu
Azure implémente des pare-feu de filtrage de paquets sur l’ensemble des machines virtuelles hôtes et invitées par défaut. Les images de système d’exploitation Windows de hello Azure Marketplace ont également des pare-feu Windows est activé par défaut. Équilibreurs de charge au périmètre hello de contrôler les communications des réseaux publics Azure basée sur ACL IP géré par les administrateurs de clients.

Si Azure déplace des données d’un client dans le cadre d’opérations normales ou lors d’une urgence, il le fait sur des canaux de communication privés et chiffrés. Autres fonctionnalités employées par toouse Azure dans le pare-feu et des réseaux virtuels sont :

* **Pare-feu d’hôte natif** : la plateforme Azure Service Fabric et le service Stockage Azure s’exécutent sur un système d’exploitation natif dépourvu d’hyperviseur. Par conséquent, le pare-feu windows hello est configuré avec hello précédente deux ensembles de règles. Stockage exécute les performances toooptimize natif.
* **Pare-feu d’hôte**: pare-feu d’hôte hello est tooprotect hello système hôte d’exploitation qui s’exécute hello hyperviseur. les règles de Hello sont programmées tooallow seul contrôleur de Service Fabric hello et passer le système d’exploitation hôte toohello tootalk de zones sur un port spécifique. Hello d’autres exceptions sont réponse de tooallow DHCP et les réponses DNS. Azure utilise un fichier de configuration d’ordinateur dont le modèle hello de règles de pare-feu pour le système d’exploitation hôte de hello. hôte Hello lui-même est protégé contre les attaques externes par une communication de toopermit configuré le pare-feu Windows uniquement à partir de sources connues et authentifiés.
* **Les pare-feu invité**: réplique les règles hello dans un filtre de paquets de commutateur de machine virtuelle hello mais programmées dans des logiciels différents (par exemple, la partie de pare-feu Windows hello du système d’exploitation invité de hello). pare-feu de machine virtuelle Hello invité peut être tooor de communications toorestrict configuré à partir de l’ordinateur virtuel d’invité hello, même si les communications hello sont autorisée par les configurations au niveau de l’hôte hello filtre IP. Par exemple, vous pouvez choisir de communication toorestrict toouse hello invité virtual machine pare-feu entre deux de vos réseaux virtuels qui ont été configurés tooconnect tooone une autre.
* **Pare-feu de stockage (FW)**: pare-feu hello sur le frontal stockage hello filtre toobe trafic uniquement sur les ports 80/443 et d’autres ports utilitaire nécessaire. pare-feu Hello hello stockage back-end restreint les communications toocome uniquement à partir de serveurs frontaux de stockage.
* **Passerelle de réseau virtuel**: hello [passerelle de réseau virtuel Azure](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) sert de passerelle entre différents locaux de hello connexion vos charges de travail dans le réseau virtuel Azure tooyour sites locaux. Il est requis tooconnect sites tooon local via [tunnels VPN de site à site IPsec](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md), ou via [ExpressRoute](../expressroute/expressroute-introduction.md) circuits. Pour les tunnels IPsec/IKE VPN, les passerelles de hello effectuer les négociations IKE et établissent des tunnels VPN S2S de IPsec de hello entre les réseaux virtuels hello et sites locaux. Les passerelles de réseau virtuel terminent également les [VPN de point à site](../vpn-gateway/vpn-gateway-point-to-site-create.md).

## <a name="secure-remote-access"></a>Accès à distance sécurisé
Les données stockées dans le cloud de hello doivent ont des manipulations de tooprevent activés des dispositifs de protection suffisant et assurer la confidentialité et intégrité pendant le transit. Cela inclut les contrôles réseau associés aux mécanismes de gestion de l’identité et de l’accès, vérifiables et basés sur la stratégie d’une organisation.

Technologie de chiffrement intégrée vous permet de communications tooencrypt dans et entre les déploiements, entre les régions Azure et à partir de centres de données Azure tooon local. Administrateur accès toovirtual machines via [sessions Bureau à distance](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), [à distance Windows PowerShell](http://blogs.technet.com/b/heyscriptingguy/archive/2013/09/07/weekend-scripter-remoting-the-cloud-with-windows-azure-and-powershell.aspx), et hello portail Azure est toujours chiffré.

toosecurely étendre votre site Centre de données toohello cloud, Azure fournit les deux [VPN de site à site](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md) et [point-to-site VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md), ainsi que des liens dédiés avec [ExpressRoute](../expressroute/expressroute-introduction.md)(tooAzure de connexions des réseaux virtuels via le VPN sont chiffrées).

### <a name="how-azure-implements-secure-remote-access"></a>Comment Azure implémente un accès distant sécurisé
Connexions toohello portail Azure doit toujours être authentifiée, et elles nécessitent SSL/TLS. Vous pouvez configurer des certificats tooenable sécurisée de gestion. Les protocoles de sécurité standard tels que [SSTP](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx) et [IPsec](https://en.wikipedia.org/wiki/IPsec) sont entièrement pris en charge.

[Azure ExpressRoute](../expressroute/expressroute-introduction.md) vous permet de créer des connexions privées entre les centres de données Azure et une infrastructure locale ou dans un environnement de colocalisation. Les connexions ExpressRoute ne sont pas établies via hello Internet public. Elles offrent davantage de fiabilité, des vitesses supérieures, des latences inférieures et une sécurité renforcée par rapport aux liaisons Internet classiques. Dans certains cas, le transfert de données entre des emplacements locaux et Azure à l’aide de connexions ExpressRoute peut également générer des économies substantielles.

## <a name="logging-and-monitoring"></a>Enregistrement et surveillance
Azure fournit authentifié la journalisation des événements relatifs à la sécurité qui génèrent une piste d’audit, et il s’agit d’ingénierie tootampering toobe résistant. Cela inclut les informations système, notamment les journaux des événements de sécurité dans les machines virtuelles d’infrastructure Azure et Azure AD. Surveillance des événements de sécurité inclut la collecte des événements tels que les modifications des adresses IP du serveur DHCP ou DNS ; toute tentative d’accès tooports, des protocoles ou des adresses IP qui sont bloquées par la conception ; modifications dans les paramètres du pare-feu ou de la stratégie de sécurité. Création de compte ou groupe ; processus inattendus ou installation du pilote.

![Microsoft Antimalware dans Azure](./media/azure-security-getting-started/sec-azgsfig5.PNG)

Des journaux d’audit enregistrant les accès et activités utilisateur privilégiés, les tentatives d’accès autorisé et non autorisé, les exceptions de système et les événements de sécurité sont conservés pour un laps de temps défini. rétention Hello de vos journaux est à votre convenance, étant donné que vous configurez la collecte de journaux et les conditions de rétention tooyour propre.

### <a name="how-azure-implements-logging-and-monitoring"></a>Comment Azure implémente l’enregistrement et la surveillance
Azure déploie des Agents de gestion (MA) et le moniteur de sécurité Azure (ASM) agents tooeach compute, stockage ou nœud de l’ensemble fibre optique sous gestion qu’ils soient natif ou virtuel. Chaque Agent de gestion est le compte de stockage configuré tooauthenticate tooa service équipe avec un certificat obtenu à partir du magasin de certificats Azure hello et transférer préconfigurée de diagnostic et de compte de stockage d’événements données toohello. Ces agents ne sont pas les ordinateurs virtuels des toocustomers déployé.

Les administrateurs Azure accéder aux journaux via un portail web pour un accès contrôlé et authentifié toohello journaux. Un administrateur peut analyser, filtrer, mettre en corrélation et analyser les journaux. comptes de stockage équipe Hello service Azure pour les journaux sont protégés à partir de l’administrateur direct access toohelp empêchent contre la falsification de journal.

Microsoft collecte des journaux à partir de périphériques réseau à l’aide du protocole de Syslog hello et à partir des serveurs hôtes à l’aide de Microsoft Audit Collection Services (ACS). Ces journaux sont placés dans une base de données de journaux à partir de laquelle des alertes sont générées pour les événements suspects. administrateur de Hello pour accéder et analyser ces journaux.

[Diagnostics Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx) est une fonctionnalité d’Azure qui vous permet de toocollect les données de diagnostic à partir d’une application qui s’exécute dans Azure. Ces données de diagnostic peuvent servir au débogage et à la résolution des problèmes, à la mesure des performances, au suivi de l’utilisation des ressources, à l’analyse de trafic, à la planification de capacité et à l’audit. Collecte des données de diagnostic hello, il peut être transféré tooan compte de stockage Azure pour la persistance. Les transferts peuvent être planifiés ou effectués à la demande.

## <a name="threat-mitigation"></a>Atténuation des menaces
Dans Ajout tooisolation, le chiffrement et le filtrage, Azure utilise plusieurs mécanismes de prévention des menaces et infrastructure tooprotect de processus et services. Celles-ci incluent les contrôles internes et les technologies utilisées toodetect et supprimer les menaces avancées telles que DDoS, une élévation de privilèges et hello [OWASP avoir 10 premières](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project).

contrôles de sécurité Hello et processus de gestion des risques Microsoft a dans toosecure place son infrastructure de cloud réduire hello risque d’incidents de sécurité. Bonjour événement un incident se produit, équipe de gestion d’Incident de sécurité (SIM) hello au sein de l’équipe Microsoft Online Services de sécurité et de conformité (OSSC) hello est toorespond prêt à tout moment.

### <a name="how-azure-implements-threat-mitigation"></a>Comment Azure implémente l’atténuation des menaces
Azure dispose de contrôles de sécurité dans l’atténuation des menaces de tooimplement sur place et également les clients toohelp atténuer les menaces potentielles dans leurs environnements. Hello liste suivante résume les fonctionnalités de prévention de menaces hello proposées par Azure :

* [Azure Antimalware](azure-security-antimalware.md) est activé par défaut sur tous les serveurs d’infrastructure. Vous avez la possibilité de l’activer dans vos propres machines virtuelles.
* Microsoft gère continue l’analyse au-delà des menaces toodetect serveurs, réseaux et les applications et empêcher les attaques. Alertes automatisées avertissent les administrateurs des comportements anormaux, ce qui permet une action corrective tootake contre les menaces internes et externes.
* Vous pouvez déployer des solutions de sécurité tierces au sein de vos abonnements, comme les pare-feu d’applications web de [Barracuda](https://techlib.barracuda.com/ng54/deployonazure).
* Microsoft inclut des tests de toopenetration approche »[rouge-association de cartes](http://download.microsoft.com/download/C/1/9/C1990DBA-502F-4C2A-848D-392B93D9B9C3/Microsoft_Enterprise_Cloud_Red_Teaming.pdf), » qui implique des experts en sécurité Microsoft attaquer les systèmes de production en direct (non client) dans Azure tootest défense réel, avancées , menaces persistantes.
* Systèmes de déploiement intégrés gérer la distribution de hello et l’installation des correctifs de sécurité entre hello plateforme Azure.

## <a name="next-steps"></a>Étapes suivantes
[Centre de gestion de la confidentialité Microsoft Azure](https://azure.microsoft.com/support/trust-center/)

[Blog de l’équipe de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/)

[Centre de réponse aux problèmes de sécurité Microsoft](https://technet.microsoft.com/library/dn440717.aspx)

[Blog Active Directory](http://blogs.technet.com/b/ad/)
