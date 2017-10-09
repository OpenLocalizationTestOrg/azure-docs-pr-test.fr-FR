---
title: "aaaAbout les périphériques VPN pour les connexions Azure entre différents locaux | Documents Microsoft"
description: "Cet article traite des périphériques VPN et des paramètres IPsec pour les connexions entre locaux de passerelle VPN S2S. Des liens sont fournis des exemples et des instructions de tooconfiguration."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: ba449333-2716-4b7f-9889-ecc521e4d616
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: yushwang;cherylmc
ms.openlocfilehash: 8b84afbf93d807342ecd56ab369d5909a13343e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-devices-and-ipsecike-parameters-for-site-to-site-vpn-gateway-connections"></a>À propos des périphériques VPN et des paramètres IPsec/IKE pour les connexions de passerelle VPN site à site

Un périphérique VPN est requise tooconfigure un réseau VPN Site à Site (S2S) entre différents locaux à l’aide d’une passerelle VPN. Connexions de site à Site peuvent être utilisé toocreate une solution hybride, ou chaque fois que vous souhaitez sécuriser les connexions entre vos réseaux locaux et de vos réseaux virtuels. Cet article fournit une liste des périphériques VPN validés, ainsi qu’une liste des paramètres IPsec/IKE pour les passerelles VPN.

> [!IMPORTANT]
> Si vous rencontrez des problèmes de connectivité entre votre des dispositifs VPN locaux et les passerelles VPN, consultez trop[des problèmes de compatibilité des appareils](#known).
>
>

### <a name="items-toonote-when-viewing-hello-tables"></a>Éléments toonote lors de l’affichage des tables de hello :

* Une modification de la terminologie a eu lieu pour les passerelles VPN Azure. Seuls les noms hello ont été modifiés. Aucune modification de fonctionnalité n’est à noter.
  * Routage statique = basé sur des stratégies
  * Routage dynamique = basé sur un itinéraire
* Spécifications de passerelle HighPerformance VPN et passerelle VPN de RouteBased sont hello identiques, sauf indication contraire. Par exemple, les périphériques VPN hello validé qui sont compatibles avec les passerelles VPN de RouteBased sont également compatibles avec hello passerelle HighPerformance VPN.

## <a name="devicetable"></a>Périphériques VPN validés et guides de configuration des périphériques

> [!NOTE]
> Lorsque vous configurez une connexion site à site, une adresse IPv4 publique est requise pour votre périphérique VPN.
>

Nous avons validé un ensemble de périphériques VPN standard en partenariat avec des fournisseurs d’appareils. Toutes les unités hello familles d’appareils hello Bonjour suivant liste doivent fonctionner avec les passerelles VPN. Consultez [sur les paramètres de passerelle VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype) toounderstand hello VPN tapez use (basée sur des stratégies ou RouteBased) pour hello solution de passerelle VPN souhaité tooconfigure.

toohelp configurer votre périphérique VPN, consultez les liens toohello correspondant famille de périphériques tooappropriate. instructions de tooconfiguration Hello des liens sont fournies sur une base du meilleur effort. Pour une prise en charge des appareils VPN, contactez le fabricant de votre appareil.

|**Fournisseur**          |**Famille de périphériques**     |**Version de système d’exploitation minimale** |**Instructions de configuration PolicyBased** |**Instructions de configuration RouteBased** |
| ---                | ---                  | ---                   | ---            | ---           |
| A10 Networks, Inc. |Thunder CFW           |ACOS 4.1.1             |Non compatible  |[Guide de configuration](https://www.a10networks.com/resources/deployment-guides/a10-thunder-cfw-ipsec-vpn-interoperability-azure-vpn-gateways)|
| Allied Telesis     |Routeurs VPN série AR |2.9.2                  |Bientôt disponible     |Non compatible  |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall série F |PolicyBased: 5.4.3<br>RouteBased: 6.2.0 |[Guide de configuration](https://techlib.barracuda.com/NGF/AzurePolicyBasedVPNGW) |[Guide de configuration](https://techlib.barracuda.com/NGF/AzureRouteBasedVPNGW) |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall série X |Pare-feu Barracuda 6.5 |[Guide de configuration](https://techlib.barracuda.com/BFW/ConfigAzureVPNGateway) |Non compatible |
| Brocade            |Routeur virtuel Vyatta 5400   |Routeur virtuel 6.6R3 GA|[Guide de configuration](http://www1.brocade.com/downloads/documents/html_product_manuals/vyatta/vyatta_5400_manual/wwhelp/wwhimpl/js/html/wwhelp.htm#href=VPN_Site-to-Site%20IPsec%20VPN/Preface.1.1.html) |Non compatible |
| Check Point |Passerelle de sécurité |R77.30 |[Guide de configuration](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |[Guide de configuration](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |
| Cisco              |ASA       |8.3 |[Exemples de configuration](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASA) |Non compatible |
| Cisco |ASR |PolicyBased: IOS 15.1<br>RouteBased: IOS 15.2 |[Exemples de configuration](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |[Exemples de configuration](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |
| Cisco |ISR |PolicyBased: IOS 15.0<br>RouteBased*: IOS 15.1 |[Exemples de configuration](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |[Exemples de configuration*](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |
| Citrix |NetScaler MPX, SDX, VPX |10.1 et versions ultérieures |[Guide de configuration](https://docs.citrix.com/en-us/netscaler/11-1/system/cloudbridge-connector-introduction/cloudbridge-connector-azure.html) |Non compatible |
| F5 |Série BIG-IP |12.0 |[Guide de configuration](https://devcentral.f5.com/articles/connecting-to-windows-azure-with-the-big-ip) |[Guide de configuration](https://devcentral.f5.com/articles/big-ip-to-azure-dynamic-ipsec-tunneling) |
| Fortinet |FortiGate |FortiOS 5.4.2 |  |[Guide de configuration](http://cookbook.fortinet.com/ipsec-vpn-microsoft-azure-54) |
| Internet Initiative Japan (IIJ) |Série SEIL |SEIL/X 4.60<br>SEIL/B1 4.60<br>SEIL/x86 3.20 |[Guide de configuration](http://www.iij.ad.jp/biz/seil/ConfigAzureSEILVPN.pdf) |Non compatible |
| Juniper |SRX |PolicyBased: JunOS 10.2<br>Routebased: JunOS 11.4 |[Exemples de configuration](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |[Exemples de configuration](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |
| Juniper |Série J |PolicyBased: JunOS 10.4r9<br>RouteBased: JunOS 11.4 |[Exemples de configuration](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |[Exemples de configuration](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |
| Juniper |ISG |ScreenOS 6.3 |[Exemples de configuration](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |[Exemples de configuration](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |
| Juniper |SSG |ScreenOS 6.2 |[Exemples de configuration](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |[Exemples de configuration](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |
| Microsoft |Service de routage et d’accès à distance |Windows Server 2012 |Non compatible |[Exemples de configuration](http://go.microsoft.com/fwlink/p/?LinkId=717761) |
| Open Systems AG |Passerelle Mission Control Security |N/A |[Guide de configuration](https://www.open.ch/_pdf/Azure/AzureVPNSetup_Installation_Guide.pdf) |Non compatible |
| Openswan |Openswan |2.6.32 |(Bientôt disponible) |Non compatible |
| Palo Alto Networks |Tous les périphériques exécutant PAN-OS |PAN-OS<br>PolicyBased : 6.1.5 ou version ultérieure<br>RouteBased : 7.1.4 |[Guide de configuration](https://live.paloaltonetworks.com/t5/Configuration-Articles/How-to-Configure-VPN-Tunnel-Between-a-Palo-Alto-Networks/ta-p/59065) |[Guide de configuration](https://live.paloaltonetworks.com/t5/Integration-Articles/Configuring-IKEv2-VPN-for-Microsoft-Azure-Environment/ta-p/60340) |
| SonicWall |Série TZ, série NSA<br>Série SuperMassive<br>Série NSA classe E |SonicOS 5.8.x<br>SonicOS 5.9.x<br>SonicOS 6.x |[Guide de configuration pour SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[Guide de configuration pour SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |[Guide de configuration pour SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646)<br>[Guide de configuration pour SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |
| WatchGuard |Tout |Fireware XTM<br> PolicyBased: v11.11.x<br>RouteBased: v11.12.x |[Guide de configuration](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA2F00000000LI7KAM&lang=en_US) |[Guide de configuration](http://watchguardsupport.force.com/publicKB?type=KBArticle&SFDCID=kA22A000000XZogSAG&lang=en_US)|

(*) Les routeurs de la série ISR 7200 prennent uniquement en charge les VPN basés sur des stratégies.

## <a name="additionaldevices"></a>Périphériques VPN non validés

Si vous ne voyez pas votre appareil dans la liste dans la table de périphériques VPN de validé hello, votre périphérique fonctionne toujours avec une connexion Site à Site. Contactez le fabricant de votre périphérique pour obtenir une prise en charge et des instructions de configuration supplémentaires.

## <a name="editing"></a>Modification des exemples de configuration de périphérique

Après le téléchargement d’exemple de configuration de périphérique VPN hello fourni, vous devez tooreplace hello certaines valeurs tooreflect des paramètres de hello pour votre environnement.

### <a name="tooedit-a-sample"></a>tooedit un exemple :

1. Ouvrez l’exemple hello à l’aide du bloc-notes.
2. Rechercher et remplacer tout <*texte*> de chaînes avec les valeurs hello spécifiques tooyour environnement. Être tooinclude que < et >. Lorsqu’un nom est spécifié, le nom hello que vous sélectionnez doit être unique. Si une commande ne fonctionne pas, consultez la documentation du fabricant du périphérique.

| **Texte de l’exemple** | **Valeur de substitution** |
| --- | --- |
| &lt;RP_OnPremisesNetwork&gt; |Nom que vous choisissez pour cet objet. Exemple : MonRéseauLocal |
| &lt;RP_AzureNetwork&gt; |Nom que vous choisissez pour cet objet. Exemple : MonRéseauAzure |
| &lt;RP_AccessList&gt; |Nom que vous choisissez pour cet objet. Exemple : MaListeAccèsAzure |
| &lt;RP_IPSecTransformSet&gt; |Nom que vous choisissez pour cet objet. Exemple : MonJeuTransformationsIPSec |
| &lt;RP_IPSecCryptoMap&gt; |Nom que vous choisissez pour cet objet. Exemple : MaCarteChiffrementIPSec |
| &lt;SP_AzureNetworkIpRange&gt; |Spécifiez une plage. Exemple : 192.168.0.0 |
| &lt;SP_AzureNetworkSubnetMask&gt; |Spécifiez un masque de sous-réseau. Exemple : 255.255.0.0 |
| &lt;SP_OnPremisesNetworkIpRange&gt; |Spécifiez une plage locale. Exemple : 10.2.1.0 |
| &lt;SP_OnPremisesNetworkSubnetMask&gt; |Spécifiez un masque de sous-réseau local. Exemple : 255.255.255.0 |
| &lt;SP_AzureGatewayIpAddress&gt; |Ce réseau virtuel de tooyour spécifique d’informations et se trouve dans le portail de gestion de hello en tant que **adresse IP de passerelle**. |
| &lt;SP_PresharedKey&gt; |Ces informations réseau virtuel est tooyour spécifique et se trouve dans hello portail de gestion en tant que de gérer la clé. |

## <a name="ipsec"></a>Paramètres IPsec/IKE

> [!NOTE]
> Bien que les valeurs hello répertoriées Bonjour tableau suivant sont actuellement pris en charge par la passerelle VPN de hello, il n’existe aucun mécanisme pour vous toospecify ou sélectionnez une combinaison spécifique des algorithmes ou des paramètres à partir de la passerelle VPN de hello. Vous devez spécifier des contraintes à partir de l’appareil VPN local hello. En outre, vous devez définir **MSS** sur **1350**.
> 
>

Bonjour les tableaux suivants :

* AS = association de sécurité
* IKE Phase 1 est également appelé « Mode principal »
* IKE Phase 2 est également appelé « Mode rapide »

### <a name="ike-phase-1-main-mode-parameters"></a>Paramètres IKE Phase 1 (Mode principal)

| **Propriété**          |**PolicyBased**    | **RouteBased**    |
| ---                   | ---               | ---               |
| Version IKE           |IKEv1              |IKEv2              |
| Groupe Diffie-Hellman  |Groupe 2 (1 024 bits) |Groupe 2 (1 024 bits) |
| Méthode d'authentification |Clé prépartagée     |Clé prépartagée     |
| Chiffrement et algorithmes de hachage |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |1. AES256, SHA1<br>2. AES256, SHA256<br>3. AES128, SHA1<br>4. AES128, SHA256<br>5. 3DES, SHA1<br>6. 3DES, SHA256 |
| Durée de vie de l’AS           |28 800 secondes     |28 800 secondes     |

### <a name="ike-phase-2-quick-mode-parameters"></a>Paramètres IKE Phase 2 (Mode rapide)

| **Propriété**                  |**PolicyBased**| **RouteBased**                              |
| ---                           | ---           | ---                                         |
| Version IKE                   |IKEv1          |IKEv2                                        |
| Chiffrement et algorithmes de hachage |1. AES256, SHA256<br>2. AES256, SHA1<br>3. AES128, SHA1<br>4. 3DES, SHA1 |[Offres d’AS RouteBased en mode rapide](#RouteBasedOffers) |
| Durée de vie de l’AS (durée)            |3 600 secondes  |27 000 secondes                                |
| Durée de vie de l’AS (octets)           |102 400 000 Ko | -                                           |
| PFS (Perfect Forward Secrecy) |Non             |[Offres d’AS RouteBased en mode rapide](#RouteBasedOffers) |
| Détection d’homologue mort     |Non pris en charge  |Pris en charge                                    |


### <a name ="RouteBasedOffers"></a>Offres d’association de sécurité VPN IPsec RouteBased (AS IKE en mode rapide)

Hello tableau suivant répertorie les offres d’association de sécurité IPsec (IKE en Mode rapide). Offres sont triés de hello répertoriés de préférence cette offre hello est présentée ou acceptée.

#### <a name="azure-gateway-as-initiator"></a>Passerelle Azure en tant qu’initiateur

|-  |**Chiffrement**|**Authentification**|**Groupe PFS**|
|---| ---          |---               |---          |
| 1 |GCM AES256    |GCM (AES256)      |Aucun         |
| 2 |AES256        |SHA1              |Aucun         |
| 3 |3DES          |SHA1              |Aucun         |
| 4 |AES256        |SHA256            |Aucun         |
| 5 |AES128        |SHA1              |Aucun         |
| 6 |3DES          |SHA256            |Aucun         |

#### <a name="azure-gateway-as-responder"></a>Passerelle Azure en tant que répondeur

|-  |**Chiffrement**|**Authentification**|**Groupe PFS**|
|---| ---          | ---              |---          |
| 1 |GCM AES256    |GCM (AES256)      |Aucun         |
| 2 |AES256        |SHA1              |Aucun         |
| 3 |3DES          |SHA1              |Aucun         |
| 4 |AES256        |SHA256            |Aucun         |
| 5 |AES128        |SHA1              |Aucun         |
| 6 |3DES          |SHA256            |Aucun         |
| 7 |DES           |SHA1              |Aucun         |
| 8 |AES256        |SHA1              |1            |
| 9 |AES256        |SHA1              |2            |
| 10|AES256        |SHA1              |14           |
| 11|AES128        |SHA1              |1            |
| 12|AES128        |SHA1              |2            |
| 13.|AES128        |SHA1              |14           |
| 14|3DES          |SHA1              |1            |
| 15|3DES          |SHA1              |2            |
| 16|3DES          |SHA256            |2            |
| 17|AES256        |SHA256            |1            |
| 18|AES256        |SHA256            |2            |
| 19|AES256        |SHA256            |14           |
| 20|AES256        |SHA1              |24           |
| 21|AES256        |SHA256            |24           |
| 22|AES128        |SHA256            |Aucun         |
| 23|AES128        |SHA256            |1            |
| 24|AES128        |SHA256            |2            |
| 25|AES128        |SHA256            |14           |
| 26|3DES          |SHA1              |14           |

* Vous pouvez spécifier le chiffrement IPsec ESP NULL avec les passerelles VPN RouteBased et HighPerformance. Chiffrement NULL ne fournit pas de toodata protection en transit et doit être utilisé uniquement lorsque le nombre maximal latence sur le débit et la valeur minimale est requise. Les clients peuvent choisir toouse cela dans les scénarios de communication de réseau, ou lorsque le chiffrement est appliqué ailleurs dans la solution de hello.
* Pour la connectivité intersite via Internet de hello, utilisez les paramètres de passerelle VPN Azure hello par défaut avec le chiffrement et les algorithmes de hachage répertoriés dans les tableaux hello au-dessus de sécurité tooensure de vos communications critiques.

## <a name="known"></a>Problèmes de compatibilité connus avec le matériel

> [!IMPORTANT]
> Ceux-ci sont hello des problèmes de compatibilité connus entre les appareils VPN tiers et les passerelles VPN Azure. Hello Azure équipe travaille activement avec les fournisseurs hello tooaddress hello problèmes répertoriés ici. Une fois les problèmes de hello résolus, cette page sera mis à jour avec les informations les plus récentes hello. Revenez la consulter régulièrement.
>
>

### <a name="feb-16-2017"></a>16 février 2017

**Appareils Palo Alto Networks avec too7.1.4 préalable de version** pour Azure VPN basée sur l’itinéraire : Si vous utilisez des périphériques VPN à partir des réseaux de Palo Alto avec too7.1.4 de PAN-OS version antérieure et que vous rencontrez connectivité émet tooAzure passerelles VPN basée sur l’itinéraire, Effectuez hello comme suit :

1. Vérifiez la version du microprogramme hello de votre appareil Palo Alto Networks. Si votre version de système d’exploitation de panoramique est antérieure à 7.1.4, mettre à niveau too7.1.4.
2. Sur l’appareil de Palo Alto Networks hello, modifiez hello too28 de durée de vie Phase 2 SA (ou SA de Mode rapide), 800 secondes (8 heures) lorsque la connexion de passerelle VPN Azure de toohello.
3. Si vous continuez à rencontrer des problèmes de connectivité, ouvrez une demande de support à partir de hello portail Azure.
