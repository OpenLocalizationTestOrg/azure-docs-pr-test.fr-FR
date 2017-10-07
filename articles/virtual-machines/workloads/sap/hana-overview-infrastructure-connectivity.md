---
title: "aaaInfrastructure et connectivité tooSAP HANA sur Azure (Instances de grande taille) | Documents Microsoft"
description: "Configurer la connectivité requis infrastructure toouse SAP HANA sur Azure (Instances de grande taille)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0af34fbd82413bf63981036a76eaa264d8299ec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-infrastructure-and-connectivity-on-azure"></a>Infrastructure et connectivité à SAP HANA (grandes instances) sur Azure 

Quelques définitions avant de lire ce guide. Dans [Vue d’ensemble et architecture de SAP HANA (grandes instances) sur Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture), nous avons présenté deux classes différentes d’unités de grande instance HANA avec :

- S72, S72m, S144, S144m, S192 et S192m, ce qui constitue tooas hello 'I classe de Type' de références (SKU).
- S384, S384m, S384xm, S576, S768 et S960, ce qui constitue tooas hello 'Classe de Type II' des références SKU.

spécificateurs de classe Hello sont toobe continu utilisée tout au long de hello HANA grande Instance documentation tooeventually font référence toodifferent fonctionnalités et les besoins en fonction des références (SKU) Instance volumineux HANA.

Nous utilisons fréquemment les autres définitions suivantes :
- **Cachet d’Instance volumineux :** une pile d’infrastructure matérielle SAP HANA TDI certifié et dédié toorun des instances de SAP HANA dans Azure.
- **SAP HANA sur Azure (Instances de grande taille) :** nom officiel de l’offre de hello dans Azure toorun HANA instances sur l’interface TDI SAP HANA certifié matériel déployé dans les tampons de grande Instance dans différentes régions Azure. Hello liées terme **HANA grande Instance** est l’abréviation de HANA SAP sur Azure (Instances de grande taille) et est largement utilisé ce guide de déploiement technique.
 

Une fois l’achat hello de HANA SAP sur Azure (Instances de grande taille) est finalisé entre vous et hello équipe des comptes Microsoft enterprise, hello informations suivantes sont requis par Microsoft toodeploy HANA grandes unités d’Instance :

- Nom du client
- Coordonnées professionnelles (y compris l’adresse électronique et le numéro de téléphone)
- Coordonnées techniques (y compris l’adresse électronique et le numéro de téléphone)
- Coordonnées de mise en réseau technique (y compris l’adresse électronique et le numéro de téléphone)
- Région de déploiement Azure (Ouest des États-Unis, Est des États-Unis, Est de l’Australie, Sud-Est de l’Australie, Europe de l’ouest et Europe du Nord à partir de juillet 
- 2017)
- Confirmer la référence SKU (configuration) de SAP HANA sur Azure (grandes instances)
- Déjà détaillé dans hello vue d’ensemble et document d’Architecture pour les Instances de grande taille HANA, pour chaque région Azure déployée pour :
    - / 29 plage d’adresses IP pour les connexions P2P-ER qui se connectent à des réseaux virtuels Azure tooHANA grosses Instances
    - Un /24 bloc CIDR utilisé pour hello Pool d’IP HANA grandes Instances de serveur
- valeurs de plage adresses IP Hello utilisés dans l’attribut d’espace d’adressage de réseau virtuel hello de chaque réseau virtuel Azure qui se connecte des Instances de grande taille toohello HANA
- Données pour chaque système de grande instance HANA :
  - Nom d’hôte souhaité : idéalement, avec le nom de domaine complet.
  - Adresse IP souhaitée pour l’unité d’Instance est importante HANA hello hors hello plage d’adresses de Pool IP du serveur - Gardez à l’esprit que hello 30 premières adresses IP dans la plage d’adresses sont réservées pour un usage interne dans les Instances de grande taille HANA Pool IP du serveur de hello
  - Nom de SAP HANA SID d’instance de SAP HANA hello (volumes de disque liés à SAP HANA hello toocreate requis). Hello HANA SID est requis pour la création d’autorisations hello pour <sidadm> sur les volumes NFS hello, qui sont la mise en route unité de HANA grande Instance toohello attaché. Il est également utilisé en tant que composant de nom hello hello des volumes de disque pouvant obtient montés. Si vous souhaitez toorun plusieurs instances HANA sur l’unité de hello, vous devez toolist plusieurs HANA SID. Chacun d’eux obtient un ensemble distinct de volumes assignés.
  - Hello groupid hello hana-sidadm utilisateur a Bonjour du système d’exploitation Linux est requis toocreate volumes de disque liés à SAP HANA hello. Hello installation de SAP HANA crée généralement groupe sapsys de hello avec un id de groupe 1001. utilisateur de hana-sidadm Hello fait partie de ce groupe
  - Hello userid hello hana-sidadm utilisateur a Bonjour du système d’exploitation Linux est requis toocreate volumes de disque liés à SAP HANA hello. Si vous exécutez plusieurs instances HANA sur l’unité de hello, vous devez toolist toutes hello <sid>adm utilisateurs 
- ID d’abonnement Azure pour toowhich d’abonnement Azure hello HANA SAP sur Azure HANA grosses Instances allez toobe directement connecté. Hello abonnement Azure, qui est en train de toobe facturé par hello ou les unités HANA grande Instance fait référence à cet ID d’abonnement.

Une fois que vous fournissez hello plus d’informations, dispositions de Microsoft HANA SAP sur Azure (Instances de grande taille) et retournera toolink nécessaire des informations de hello vos unités des réseaux virtuels Azure tooHANA Instances de grande taille tooaccess hello HANA grande Instance.

## <a name="connecting-azure-vms-toohana-large-instances"></a>Connexion des Instances de grande taille tooHANA machines virtuelles Azure

Comme indiqué précédemment dans [vue d’ensemble de SAP HANA (instances de grande taille) et l’architecture sur Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) hello minimale du déploiement des Instances de grande taille HANA avec la couche d’application hello SAP dans Azure se présente comme :

![Réseau virtuel Azure connecté tooSAP HANA sur Azure (Instances de grande taille) et locales](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

De plus près sur hello côté du réseau virtuel Azure, nous sommes conscients hello nécessaire :

- définition de Hello d’un réseau virtuel Azure qui est à cours toobe utilisé toodeploy VMs hello de couche d’application SAP hello dans.
- Automatiquement cela signifie qu’un sous-réseau par défaut Bonjour que réseau virtuel Azure est défini et qui est hello réellement des toodeploy utilisé un VMs hello dans.
- toohave a besoin de Hello réseau virtuel Azure qui est créé au moins un sous-réseau d’ordinateurs virtuels et un sous-réseau de passerelle ExpressRoute. Plages d’adresses IP hello comme nous l’avons vu dans les sections suivantes de hello et spécifiés doit être assignées à ces sous-réseaux.

Par conséquent, nous allons étudier un peu plus près hello la création du réseau virtuel Azure pour les Instances de grande taille HANA

### <a name="creating-hello-azure-vnet-for-hana-large-instances"></a>Création d’hello réseau virtuel Azure pour les Instances de grande taille HANA

>[!Note]
>Hello réseau virtuel de Azure pour HANA grande Instance doit être créée à l’aide du modèle de déploiement du Gestionnaire de ressources Azure hello. ancien modèle de déploiement Azure Hello, communément appelé modèle de déploiement classique, n’est pas pris en charge par hello solution d’Instance est importante HANA.

Hello réseau virtuel peut être créé à l’aide de hello portail Azure, PowerShell, un modèle Azure ou CLI d’Azure (consultez [créer un réseau virtuel à l’aide de hello portail Azure](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Bonjour l’exemple suivant, nous allons dans un réseau virtuel créé par le biais hello portail Azure.

Si vous examinez dans les définitions de hello d’un réseau virtuel d’Azure via hello portail Azure, examinons quelques-unes des définitions de hello et celles interconnexions toowhat nous la liste des plages d’adresses IP. Comme nous parlons hello **espace d’adressage**, nous entendons l’espace d’adressage hello hello réseau virtuel Azure est autorisée à toouse. Cet espace d’adressage est également de plage d’adresses hello hello utilise de réseau virtuel pour la propagation des itinéraires BGP. Cet **espace d’adressage** est illustré ici :

![Adresse d’espace de réseau virtuel Azure affichés dans hello portail Azure](./media/hana-overview-connectivity/image1-azure-vnet-address-space.png)

Dans les cas de hello précédant avec 10.16.0.0/16, hello réseau virtuel Azure a été spécifié un toouse de plage d’adresse IP plutôt volumineuse et large. Signifie que toutes les plages d’adresses IP hello de sous-réseaux suivantes au sein de ce réseau virtuel peuvent avoir leurs plages au sein de cet espace d’adressage. Généralement, nous ne recommandons pas une plage d’adresses aussi volumineuse pour un seul réseau virtuel dans Azure. Mais l’obtention d’aller plus loin, examinons les sous-réseaux hello définis dans hello réseau virtuel Azure :

![Sous-réseaux de réseaux virtuels Azure et plages d’adresses IP associées](./media/hana-overview-connectivity/image2b-vnet-subnets.png)

Comme vous pouvez le voir, on obtient un réseau virtuel avec un premier sous-réseau de machines virtuelles (appelé « default ») et un sous-réseau appelé « GatewaySubnet ».
Bonjour suivant la section, nous nous référons toohello plage d’adresses IP du sous-réseau hello, qui a été appelée 'default' dans les graphiques de hello en tant que **plage d’adresses IP Azure VM sous-réseau**. Bonjour les sections suivantes, nous nous référons toohello plage d’adresses IP de sous-réseau de passerelle de hello en tant que **plage d’adresses IP de sous-réseau de passerelle de réseau virtuel**. 

Dans les cas de hello illustrées par des graphiques de hello deux ci-dessus, vous voyez que hello **espace d’adressage de réseau virtuel** couvre à la fois, hello **plage d’adresses IP Azure VM sous-réseau** et hello **adresse IP de sous-réseau de passerelle de réseau virtuel plage**. 

Dans d’autres cas où vous devez tooconserve ou être spécifiques avec vos plages d’adresses IP, vous pouvez restreindre hello **espace d’adressage de réseau virtuel** d’un réseau virtuel toohello des plages spécifiques utilisés par chaque sous-réseau. Dans ce cas, vous pouvez définir hello **espace d’adressage de réseau virtuel** d’un réseau virtuel spécifique sous forme de plusieurs plages comme indiqué ici :

![Espace d’adressage de réseau virtuel Azure avec deux espaces](./media/hana-overview-connectivity/image3-azure-vnet-address-space_alternate.png)

Dans ce cas, hello **espace d’adressage de réseau virtuel** a deux espaces définis. Ces deux espaces, plages d’adresses IP toohello identiques sont définis pour **plage d’adresses IP Azure VM sous-réseau** et hello **plage d’adresses IP de sous-réseau de passerelle de réseau virtuel.**

Vous pouvez utiliser n’importe quelle norme d’affectation de noms de votre choix pour ces sous-réseaux locataires (sous-réseaux de machines virtuelles). Toutefois, **doit toujours être un seul et unique, sous-réseau de passerelle pour chaque réseau virtuel** qui connecte toohello SAP HANA sur le circuit ExpressRoute de Azure (Instances de grande taille). Et **ce sous-réseau de passerelle doit toujours être nommé « GatewaySubnet »** tooensure le positionnement correct de passerelle ExpressRoute de hello.

> [!WARNING] 
> Il est essentiel de que ce sous-réseau de passerelle hello est toujours nommé « GatewaySubnet ».

Plusieurs sous-réseaux de machine virtuelle peuvent être utilisés, même s’ils utilisent des plages d’adresses non contiguës. Mais comme mentionné précédemment, ces plages d’adresses doivent être couvert par hello **espace d’adressage de réseau virtuel** Hello réseau virtuel dans un format agrégé ou dans une liste de hello exacte des plages de sous-réseaux d’ordinateurs virtuels hello et hello sous-réseau de passerelle.

Résumé des faits importants de hello sur un réseau virtuel Azure qui se connecte à des Instances de grande taille tooHANA :

- Vous devez toosubmit tooMicrosoft hello **espace d’adressage de réseau virtuel** lorsque vous effectuez un déploiement initial d’Instances de grande taille HANA. 
- Hello **espace d’adressage de réseau virtuel** peut être une plus grande plage qui couvre la plage hello pour l’ou les plages d’adresses IP Azure VM sous-réseau et la plage d’adresses IP de sous-réseau de passerelle de réseau virtuel hello.
- Ou vous pouvez envoyer en tant que **espace d’adressage de réseau virtuel** plusieurs plages qui couvrent hello autre adresse IP ou les plages d’adresse IP virtuelle sous-réseau et la plage d’adresses IP de sous-réseau de passerelle de réseau virtuel hello les plages d’adresses.
- Hello défini **espace d’adressage de réseau virtuel** est utilisée propagation de routage BGP.
- nom de Hello du sous-réseau de passerelle hello doit être : **« GatewaySubnet ».**
- Hello **espace d’adressage de réseau virtuel** est utilisé comme un filtre sur hello HANA grande Instance côté tooallow ou interdire les unités de HANA grande Instance toohello le trafic à partir de Azure. Si hello les informations de routage BGP Hello réseau virtuel Azure et les plages d’adresses IP hello configurés pour le filtrage sur hello côté de l’Instance est importante HANA ne correspondent pas, les problèmes de connectivité peuvent se produire.
- Il existe quelques détails sur le sous-réseau de passerelle hello qui sont décrites plus bas dans la Section « Connexion un tooHANA de réseau virtuel grande Instance ExpressRoute »



### <a name="different-ip-address-ranges-toobe-defined"></a>Plages d’adresse IP différente toobe défini 

Nous avons introduit déjà hello IP adresse plages nécessaire toodeploy HANA les Instances de grande taille dans les sections précédentes. Mais d’autres plages d’adresses IP sont également importantes. Examinons-les plus en détail. Hello des adresses IP suivantes qui n’ont pas besoin toobe soumis tooMicrosoft devez toobe défini, avant d’envoyer une demande pour le déploiement initial :

- **Espace d’adressage de réseau virtuel :** déjà présentées plus haut, est ou sont adresse hello ou les plages que vous avez affectés (ou que vous envisagez de tooassign) tooyour espace paramètre adresse Bonjour ou les réseaux virtuels Azure (VNet) connexion toohello SAP HANA grande Instance environnement. Il est recommandé que ce paramètre de l’espace d’adressage est une valeur multiligne composée de hello ou des plages de sous-réseau d’ordinateurs virtuels Azure et hello plage de sous-réseau de passerelle Azure comme indiqué précédemment dans les graphiques hello. Cette plage NE doit PAS chevaucher les plages d’adresses du pool IP local ou de votre serveur ou encore les plages d’adresses ER-P2P. Comment tooget ce ou ces plages d’adresses IP ? Votre équipe réseau ou votre fournisseur de services doivent vous fournir une ou plusieurs plages d’adresses IP qui ne sont pas utilisées à l’intérieur de votre réseau. Exemple : Si votre sous-réseau d’ordinateurs virtuels Azure (voir plus haut) est 10.0.1.0/24 et votre sous-réseau de passerelle Azure (voir ci-dessous) est 10.0.2.0/28, puis votre espace d’adressage de réseau virtuel Azure est recommandé de toobe deux lignes ; 10.0.1.0/24 et 10.0.2.0/28. Bien que les valeurs de l’espace d’adressage de hello peuvent être agrégées, il est recommandé de leur mise en correspondance plages du sous-réseau toohello tooavoid de réutilisation accidentelle de l’adresse IP inutilisée plages d’adresses dans les espaces d’adressage plus grandes Bonjour futures ailleurs dans votre réseau. **Hello espace d’adressage de réseau virtuel est une plage d’adresses IP, le besoins de toobe soumise tooMicrosoft lors de la demande pour un déploiement initial**

- **Plage d’adresses IP de sous-réseau machine virtuelle Azure :** plage d’adresses IP de ce, comme indiqué précédemment déjà, est hello une vous avez attribué (ou que vous envisagez de tooassign) paramètre de sous-réseau de réseau virtuel Azure toohello dans votre environnement de SAP HANA grande Instance toohello de connexion Azure . Cette plage d’adresses IP est utilisée tooassign IP adresses tooyour machines virtuelles Azure. adresses IP de Hello en dehors de cette plage peuvent tooconnect tooyour SAP HANA grande Instance serveur (s). Si nécessaire, plusieurs sous-réseaux de machines virtuelles Azure peuvent être utilisés. Microsoft recommande d’utiliser un bloc CIDR /24 pour chaque sous-réseau de machines virtuelles Azure. Cette plage d’adresses doit faire partie des valeurs de hello utilisées dans l’espace d’adressage du réseau virtuel Azure de hello. Comment tooget cette plage d’adresses IP ? Votre équipe réseau ou votre fournisseur de services doit vous indiquer une plage d’adresses IP qui n’est pas utilisée actuellement à l’intérieur de votre réseau.

- **Plage d’adresses IP de sous-réseau de passerelle de réseau virtuel :** hello en fonction des fonctionnalités que vous allez toouse, hello recommandé taille serait :
   - Passerelle ExpressRoute ultra-performante : bloc d’adresse /26 - obligatoire pour la classe de Type II des références SKU
   - Coexistence avec VPN et ExpressRoute à l’aide d’une passerelle ExpressRoute hautes performances (ou plus petites) : bloc d’adresses /27
   - Toutes les autres situations : bloc d’adresses /28 Cette plage d’adresses doit faire partie des valeurs de hello utilisées dans les valeurs « Espace d’adressage de réseau virtuel » hello. Cette plage d’adresses doit faire partie des valeurs de hello utilisées dans les valeurs d’espace d’adressage du réseau virtuel Azure hello que vous avez besoin de toosubmit tooMicrosoft. Comment tooget cette plage d’adresses IP ? Votre équipe réseau ou votre fournisseur de services doit vous indiquer une plage d’adresses IP qui n’est pas utilisée actuellement à l’intérieur de votre réseau. 

- **Plage pour la connectivité de P2P-ER d’adresses :** cette plage représente la plage d’IP hello pour votre connexion ExpressRoute Instance volumineux (ER) de SAP HANA P2P. Cette plage d’adresses IP doit correspondre à la plage CIDR /29. Cette plage NE doit PAS chevaucher les plages d’adresses IP locales ou Azure. Cette plage d’adresses IP est utilisée tooset la connectivité hello ER à partir de vos serveurs de SAP HANA grande Instance toohello passerelle ExpressRoute de réseau virtuel Azure. Comment tooget cette plage d’adresses IP ? Votre équipe réseau ou votre fournisseur de services doit vous indiquer une plage d’adresses IP qui n’est pas utilisée actuellement à l’intérieur de votre réseau. **Cette plage est une plage d’adresses IP, le besoins de toobe soumise tooMicrosoft lors de la demande pour un déploiement initial**
  
- **Plage d’adresses IP Pool de serveurs :** cette plage d’adresses IP est utilisée tooassign hello individuels tooHANA grande instance serveurs d’adresses IP. Hello recommandé de taille du sous-réseau est un /24 CIDR bloquer - mais si nécessaire, il peut être plus petite tooa au minimum de fournir de 64 adresses IP. Dans cette plage, hello 30 premières adresses IP sont réservées pour une utilisation par Microsoft. Assurez-vous que cela est pris en compte lors du choix de taille hello de plage de hello. Cette plage NE doit PAS chevaucher les adresses IP locales ou Azure. Comment tooget cette plage d’adresses IP ? Votre équipe réseau ou votre fournisseur de services doit vous indiquer une plage d’adresses IP qui n’est pas utilisée actuellement à l’intérieur de votre réseau. Un /24 (recommandé) unique CIDR bloquer toobe utilisée pour affecter des adresses IP spécifiques hello nécessaires pour SAP HANA sur Azure (Instances de grande taille). **Cette plage est une plage d’adresses IP, le besoins de toobe soumise tooMicrosoft lors de la demande pour un déploiement initial**
 
Si vous devez toodefine et que vous prévoyez de plages d’adresses IP hello ci-dessus, pas toutes les besoin d’être toobe transmis tooMicrosoft. hello toosummarize ci-dessus, vous êtes tooname requis tooMicrosoft les plages d’adresses IP hello sont les suivantes :

- Espace(s) d’adressage du réseau virtuel Azure
- Plage d’adresses pour les connexions ER-P2P
- Plage d’adresses du pool d’adresses IP de serveur

Ajout de réseaux virtuels supplémentaires qui doivent tooconnect tooHANA Instances de grande taille, nécessite que vous toosubmit hello nouvel espace d’adressage du réseau virtuel Azure que vous ajoutez tooMicrosoft. 

Suit est un exemple de plages hello et certaines plages d’exemple que vous devez tooconfigure et éventuellement fournissez tooMicrosoft. Comme vous pouvez le voir, valeur hello pour hello espace d’adressage du réseau virtuel Azure n’est pas agrégée dans le premier exemple de hello, mais il est défini à partir de plages de hello de plage d’adresses hello première machine virtuelle Azure sous-réseau IP et de la plage d’adresses IP de sous-réseau de passerelle de réseau virtuel hello. À l’aide de plusieurs sous-réseaux d’ordinateurs virtuels au sein du réseau virtuel Azure de hello serait travail en conséquence par la configuration et l’envoi de hello IP supplémentaires de plages d’adresses hello supplémentaires trouvées de machine virtuelle dans le cadre de l’espace d’adressage du réseau virtuel Azure de hello.

![Plages d’adresses IP nécessaires pour le déploiement minimal de SAP HANA sur Azure (grandes instances)](./media/hana-overview-connectivity/image4b-ip-addres-ranges-necessary.png)

Vous avez également la possibilité de hello d’agrégation de données hello vous soumettez tooMicrosoft. Dans ce cas, hello espace d’adressage du réseau virtuel Azure de hello uniquement inclut un espace. À l’aide de plages d’adresses IP hello utilisés dans l’exemple de hello antérieures. Cet espace d’adressage de réseau virtuel agrégé pourrait ressembler à ceci :

![Deuxième possibilité de plages d’adresses IP nécessaires pour le déploiement minimal de SAP HANA sur Azure (grandes instances)](./media/hana-overview-connectivity/image5b-ip-addres-ranges-necessary-one-value.png)

Comme vous pouvez le constater ci-dessus, au lieu de deux plages de plus petits qui définie d’espace d’adressage hello Hello réseau virtuel Azure, nous avons une plus grande plage qui couvre les adresses IP 4096. Ce type de définition volumineux de hello espace d’adressage laisse certaines plages plutôt volumineuse inutilisé. Étant donné que hello espace d’adressage de réseau virtuel ou les valeurs sont utilisées pour la propagation des itinéraires BGP, l’utilisation de hello plages inutilisées sur site ou ailleurs dans votre réseau peut provoquer des problèmes de routage. Il est donc hello tookeep recommandée Qu'espace d’adressage être parfaitement en phase avec l’espace d’adressage de sous-réseau réel hello utilisé. Si nécessaire, sans subir des interruptions de service sur hello réseau virtuel, vous pouvez toujours ajouter des nouvelles valeurs de l’espace d’adressage ultérieurement.
 
> [!IMPORTANT] 
> Plage de ER-P2P, Pool IP du serveur, l’espace d’adressage réseau virtuel Azure de chaque adresse IP doit **pas** se chevauchent entre eux ou toute autre plage utilisé quelque part ailleurs dans votre réseau ; chacun doit être discrète et en tant que graphiques de hello deux afficher antérieure, ne peut pas être un sous-réseau de n’importe quel autre. En cas de chevauchement entre les plages, hello réseau virtuel Azure ne peut pas se connecter circuit ExpressRoute de toohello.

### <a name="next-steps-after-address-ranges-have-been-defined"></a>Étapes à suivre après la définition des plages d’adresses
Après ont défini les plages d’adresses IP hello, hello activités suivantes doivent toohappen :

1. Soumettre des plages d’adresses IP hello pour espace d’adressage du réseau virtuel Azure, la connectivité de P2P-ER hello et plage d’adresses IP Pool de serveurs, ainsi que d’autres données qui a été indiquées au début hello du document de hello. À ce stade, vous également pouvez démarrer toocreate hello réseau virtuel et sous-réseaux d’ordinateurs virtuels hello. 
2. Un circuit Express Route est créé par Microsoft entre votre abonnement Azure et l’horodatage d’Instance est importante HANA hello.
3. Un réseau de client est créé sur le marqueur de grande Instance hello par Microsoft.
4. Microsoft configure la mise en réseau dans hello SAP HANA sur tooaccept d’infrastructure Azure (Instances de grande taille) des adresses IP à partir de votre espace d’adressage réseau virtuel Azure communique avec les Instances de grande taille HANA.
5. En fonction de hello que spécifique HANA SAP sur Azure (Instances de grande taille) référence (SKU) achetée, Microsoft affecte une unité de calcul dans un réseau de client, allouer monter le stockage et installer le système d’exploitation hello (SUSE ou Red Hat Linux). Adresses IP pour ces unités sont extraite hello adresses de Pool IP serveur plage que vous avez soumis tooMicrosoft.

Extrémité hello hello du processus de déploiement, Microsoft fournit hello suivant tooyou de données :
- Informations nécessaires tooconnect votre circuit ExpressRoute de toohello VNet(s) d’Azure qui se connecte à des réseaux virtuels Azure tooHANA grosses Instances :
     - Clé(s) d’autorisation
     - PeerID ExpressRoute
- Données tooaccess HANA grosses Instances après avoir établi le circuit ExpressRoute et réseau virtuel Azure.

Vous pouvez également trouver séquence hello de connexion d’Instances de grande taille HANA dans le document de hello [tooEnd le programme d’installation pour des Instances SAP HANA volumineuses de fin](https://azure.microsoft.com/resources/sap-hana-on-azure-large-instances-setup/). Grand nombre de hello comme suit sont affichent dans un exemple de déploiement dans ce document. 


## <a name="connecting-a-vnet-toohana-large-instance-expressroute"></a>La connexion à un réseau virtuel de tooHANA grande Instance ExpressRoute

Quand vous défini toutes les plages d’adresses IP hello et obtenu maintenant les données de salutation auprès de Microsoft, vous pouvez démarrer connexion hello réseau virtuel que vous avez créé avant tooHANA Instances de grande taille. Une fois hello que réseau virtuel Azure est créé, une passerelle ExpressRoute doit être créée sur hello réseau virtuel toolink hello réseau virtuel toohello circuit ExpressRoute qui se connecte locataire toohello sur le marqueur de grande Instance hello.

> [!NOTE] 
> Cette étape peut prendre jusqu'à too30 minutes toocomplete, comme passerelle hello est créé dans hello désigné d’abonnement Azure et puis toohello connecté spécifiée réseau virtuel Azure.

S’il existe déjà une passerelle, vérifiez s’il s’agit d’une passerelle ExpressRoute. Si ce n’est pas le cas, la passerelle de hello doive être supprimée et recréée comme passerelle ExpressRoute. Si une passerelle ExpressRoute est déjà établie, étant donné que hello que réseau virtuel Azure est déjà connecté circuit ExpressRoute de toohello pour la connectivité locale, passez toohello section de liaison des réseaux virtuels ci-dessous.

- Utilisez soit hello (nouvelle) [portail Azure](https://portal.azure.com/), ou PowerShell toocreate une passerelle ExpressRoute VPN connecté tooyour réseau virtuel.
  - Si vous utilisez hello portail Azure, ajoutez un nouvel **passerelle de réseau virtuel** , puis sélectionnez **ExpressRoute** en tant que type de passerelle hello.
  - Si vous avez choisi de PowerShell à la place, tout d’abord télécharger et utiliser hello dernières [Azure PowerShell SDK](https://azure.microsoft.com/downloads/) tooensure une expérience optimale. Hello suivant les commandes de créer une passerelle ExpressRoute. les textes Hello précédé par un  _$_  sont les variables définies par l’utilisateur qui toobe besoin de mise à jour avec les informations spécifiques à votre.

```PowerShell
# These Values should already exist, update toomatch your environment
$myAzureRegion = "eastus"
$myGroupName = "SAP-East-Coast"
$myVNetName = "VNet01"

# These values are used toocreate hello gateway, update for how you wish hello GW components toobe named
$myGWName = "VNet01GW"
$myGWConfig = "VNet01GWConfig"
$myGWPIPName = "VNet01GWPIP"
$myGWSku = "HighPerformance" # Supported values for HANA Large Instances are: HighPerformance or UltraPerformance

# These Commands create hello Public IP and ExpressRoute Gateway
$vnet = Get-AzureRmVirtualNetwork -Name $myVNetName -ResourceGroupName $myGroupName
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
New-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName `
-Location $myAzureRegion -AllocationMethod Dynamic
$gwpip = Get-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $myGWConfig -SubnetId $subnet.Id `
-PublicIpAddressId $gwpip.Id

New-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName -Location $myAzureRegion `
-IpConfigurations $gwipconfig -GatewayType ExpressRoute `
-GatewaySku $myGWSku -VpnType PolicyBased -EnableBgp $true
```

Dans cet exemple, hello hautes performances passerelle référence (SKU) a été utilisé. Les options disponibles sont hautes performances ou UltraPerformance comme hello uniquement les SKU de passerelle sont pris en charge pour SAP HANA sur Azure (Instances de grande taille).

> [!IMPORTANT]
> Pour les Instances de grande taille HANA Hello référence (SKU) types S384, S384m, S384xm, S576, S768 et S960 (Type de classe II SKU), hello utilisation Hello SKU de passerelle UltraPerformance est obligatoire.

### <a name="linking-vnets"></a>Liaison de réseaux virtuels

Maintenant que hello réseau virtuel Azure a une passerelle ExpressRoute, vous utilisez des informations de l’autorisation de hello fournies par Microsoft tooconnect hello ExpressRoute passerelle toohello SAP HANA sur le circuit ExpressRoute de Azure (Instances de grande taille) créé pour cette connexion. Cette étape peut être effectuée à l’aide de hello portail Azure ou PowerShell. portail de Hello est recommandée, toutefois, les instructions PowerShell sont les suivantes. 

- Vous exécutez hello suivant les commandes pour chaque passerelle de réseau virtuel à l’aide d’un AuthGUID différent pour chaque connexion. Hello deux premières entrées suivantes du script hello proviennent des informations de hello fournies par Microsoft. En outre, hello AuthGUID est spécifique à chaque réseau virtuel et sa passerelle. Signifie que, si vous voulez tooadd un autre réseau virtuel de Azure, vous devez tooget un autre ID pour votre circuit ExpressRoute qui connecte des Instances de grande taille HANA dans Azure. 

```PowerShell
# Populate with information provided by Microsoft Onboarding team
$PeerID = "/subscriptions/9cb43037-9195-4420-a798-f87681a0e380/resourceGroups/Customer-USE-Circuits/providers/Microsoft.Network/expressRouteCircuits/Customer-USE01"
$AuthGUID = "76d40466-c458-4d14-adcf-3d1b56d1cd61"

# Your ExpressRoute Gateway Information
$myGroupName = "SAP-East-Coast"
$myGWName = "VNet01GW"
$myGWLocation = "East US"

# Define hello name for your connection
$myConnectionName = "VNet01GWConnection"

# Create a new connection between hello ER Circuit and your Gateway using hello Authorization
$gw = Get-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName
    
New-AzureRmVirtualNetworkGatewayConnection -Name $myConnectionName `
-ResourceGroupName $myGroupName -Location $myGWLocation -VirtualNetworkGateway1 $gw `
-PeerId $PeerID -ConnectionType ExpressRoute -AuthorizationKey $AuthGUID
```

Si vous souhaitez tooconnect hello passerelle toomultiple circuits ExpressRoute qui sont associés à votre abonnement, vous devrez peut-être tooexecute cette étape plusieurs fois. Par exemple, vous allez probablement tooconnect hello même circuit ExpressRoute passerelle de réseau virtuel toohello qui relie hello réseau virtuel tooyour en local.

## <a name="adding-more-ip-addresses-or-subnets"></a>Ajout d’adresses IP ou sous-réseaux supplémentaires

Utilisez soit hello portail Azure, PowerShell ou CLI lors de l’ajout de plusieurs adresses IP ou sous-réseaux.

Dans ce cas, la recommandation de hello est tooadd hello plage d’adresses IP en tant que nouvelle plage toohello espace d’adressage de réseau virtuel au lieu de générer une nouvelle plage agrégée. Dans les deux cas, vous avez besoin toosubmit cette modification tooMicrosoft tooallow connectivité hors que de nouvelles unités de HANA grande Instance de toohello de plage d’adresse IP dans votre client. Vous pouvez ouvrir un prise en charge Azure demande tooget hello nouveau réseau virtuel espace d’adressage ajouté. Après avoir reçu la confirmation, effectuer les étapes suivantes hello.

toocreate un sous-réseau supplémentaire à partir de hello portail Azure, consultez l’article hello [créer un réseau virtuel à l’aide de hello portail Azure](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), et toocreate à partir de PowerShell, consultez [créer un réseau virtuel à l’aide de PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="adding-vnets"></a>Ajout de réseaux virtuels

Après la connexion initiale au moins un des réseaux virtuels Azure, vous pourriez tooadd supplémentaires ceux qui accèdent à SAP HANA sur Azure (Instances de grande taille). Tout d’abord, soumettre une demande de support Azure, dans cette demande notamment à la fois hello des informations spécifiques identification hello particulier déploiement d’Azure et hello IP adresse espace ou les plages de hello espace d’adressage du réseau virtuel Azure. SAP HANA sur la gestion des services Azure fournit des informations sur nécessaires de hello vous devez tooconnect hello ExpressRoute et des réseaux virtuels supplémentaires. Pour chaque réseau virtuel, vous avez besoin d’un toohello de tooconnect unique clé d’autorisation Instances de grande taille tooHANA ExpressRoute Circuit.

Étapes tooadd un réseau virtuel Azure :

1. Terminer la première étape de hello hello processus d’intégration, voir hello _création de réseau virtuel Azure_ section.
2. Hello deuxième étapes hello d’intégration, voir hello _création de sous-réseau de passerelle_ section.
3. tooconnect votre toohello de réseaux virtuels supplémentaire, un circuit ExpressRoute d’Instance volumineux HANA ouvrir une demande de support Azure avec des informations sur hello nouveau réseau virtuel et demander une nouvelle clé d’autorisation.
4. Une fois averti que l’autorisation de hello est terminée, utilisez les informations de l’autorisation fournie par Microsoft hello toocomplete hello troisième étape dans le processus d’intégration de hello, consultez hello _liaison des réseaux virtuels_ section.

## <a name="increasing-expressroute-circuit-bandwidth"></a>Augmentation de la bande passante d’un circuit ExpressRoute

Consultez SAP HANA sur Azure Service Management. Si vous êtes la bande passante de hello tooincrease conseillées Hello SAP HANA sur le circuit ExpressRoute de Azure (Instances de grande taille), créez une demande de support Azure. (Vous pouvez demander une augmentation pour une bande de passante du circuit unique des tooa au maximum 10 Gbits/s.) Vous ensuite recevez une notification une fois l’opération hello est terminée ; Aucune action supplémentaire ne nécessaire tooenable cette vitesse supérieure dans Azure.

## <a name="adding-an-additional-expressroute-circuit"></a>Ajout d’un circuit ExpressRoute supplémentaire

Consultez SAP HANA sur la gestion des services Azure, s’il est recommandé qu’un circuit ExpressRoute supplémentaire est nécessaire, apporter un toocreate de demande de support Azure un nouveau circuit ExpressRoute (et tooget d’autorisation informations tooconnect tooit). espace d’adressage Hello qui va être utilisé sur des réseaux virtuels doivent être définis avant d’effectuer la demande de hello, dans l’ordre pour SAP HANA sur l’autorisation de gestion des services Azure tooprovide de hello.

Une fois que le circuit de nouveau hello est créé et hello SAP HANA sur la configuration de la gestion des services Azure est terminée, vous allez notification tooreceive avec informations hello tooproceed. Suivez les étapes de hello fournies ci-dessus pour la création et connexion hello nouveau réseau virtuel toothis supplémentaire circuit. Vous n’êtes pas en mesure de tooconnect des réseaux virtuels Azure toothis supplémentaire circuit si elles déjà connecté tooanother SAP HANA sur le circuit ExpressRoute de Azure (grande Instance) Bonjour même région Azure.

## <a name="deleting-a-subnet"></a>Suppression d’un sous-réseau

tooremove un sous-réseau de réseau virtuel, soit hello portail Azure, PowerShell ou CLI peut être utilisé. Si votre plage d’adresses IP de réseau virtuel Azure/espace d’adressage de réseau virtuel Azure était une plage agrégée, vous ne recevrez aucun suivi de la part de Microsoft. À l’exception que hello réseau virtuel continue à se propager espace d’adressage de routage BGP qui inclut le sous-réseau de hello supprimé. Si vous avez défini hello plage d’adresse IP de réseau virtuel Azure/Azure espace d’adressage de réseau virtuel en tant que plusieurs plages d’adresses IP de l’application a été attribué tooyour supprimé sous-réseau, vous devez supprimer cet élément en dehors de votre espace d’adressage de réseau virtuel et informe ensuite SAP HANA sur la gestion des services Azure tooremove à partir de hello plages que HANA SAP sur Azure (Instances de grande taille) est autorisée toocommunicate avec.

Alors que n’existe pas encore spécifique, dédié Azure.com obtenir des conseils sur la suppression des sous-réseaux, les processus de hello pour la suppression des sous-réseaux est hello inverse de hello leur processus d’ajout. Consultez l’article hello [créer un réseau virtuel à l’aide de hello portail Azure](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour plus d’informations sur la création de sous-réseaux.

## <a name="deleting-a-vnet"></a>Suppression d’un réseau virtuel

Utilisez soit hello portail Azure, PowerShell ou CLI lors de la suppression d’un réseau virtuel. SAP HANA sur la gestion des services Azure supprime les autorisations existantes de hello sur hello SAP HANA sur le circuit d’Azure ExpressRoute (Instances de grande taille) et supprimer hello plage d’adresse IP de réseau virtuel Azure/Azure espace d’adressage de réseau virtuel pour la communication de hello et Instances de grande taille HANA.

Une fois que hello réseau virtuel a été supprimé, ouvrez un prise en charge Azure demande tooprovide hello espace d’adressage IP ou les plages toobe supprimé.

Alors que n’existe pas encore spécifique, dédié Azure.com obtenir des conseils sur la suppression de réseaux virtuels, les processus de hello pour la suppression de réseaux virtuels est hello inverse de hello leur processus d’ajout, ce qui est décrit ci-dessus. Consultez les articles hello [créer un réseau virtuel à l’aide de hello portail Azure](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) et [créer un réseau virtuel à l’aide de PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour plus d’informations sur la création de réseaux virtuels.

tooensure tous les éléments sont supprimé, supprimez hello éléments suivants :

- Hello connexion ExpressRoute, passerelle de réseau virtuel, adresse IP publique de passerelle de réseau virtuel et de réseau virtuel

## <a name="deleting-an-expressroute-circuit"></a>Suppression d’un circuit ExpressRoute

tooremove un HANA SAP supplémentaires sur le circuit de Azure (Instances de grande taille) ExpressRoute, ouvrir une demande de support Azure avec SAP HANA sur la gestion des services Azure et demandez que le circuit de hello doit être supprimé. Dans hello abonnement Azure, vous pouvez supprimer ou conserver hello réseau virtuel si nécessaire. Toutefois, vous devez supprimer la connexion de hello entre hello circuit ExpressRoute d’Instances volumineux HANA et hello lié passerelle de réseau virtuel.

Si vous voulez également tooremove un réseau virtuel, suivez les instructions de hello sur la suppression d’un réseau virtuel dans la section hello ci-dessus.


