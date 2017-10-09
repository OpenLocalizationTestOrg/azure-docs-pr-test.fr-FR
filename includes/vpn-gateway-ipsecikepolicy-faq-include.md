### <a name="is-custom-ipsecike-policy-supported-on-all-azure-vpn-gateway-skus"></a>La stratégie personnalisée IPsec/IKE est-elle prise en charge sur toutes les références de passerelle VPN Azure ?
La stratégie personnalisée IPsec/IKE est prise en charge sur les passerelles VPN Azure **VpnGw1, VpnGw2, VpnGw3, Standard** et **HighPerformance**. La référence **De base** N’EST PAS prise en charge.

### <a name="how-many-policies-can-i-specify-on-a-connection"></a>Combien de stratégies puis-je spécifier pour une connexion ?
Vous pouvez uniquement spécifier ***une*** combinaison de stratégie pour une connexion donnée.

### <a name="can-i-specify-a-partial-policy-on-a-connection-eg-only-ike-algorithms-but-not-ipsec"></a>Puis-je spécifier une stratégie partielle pour une connexion ? (Par exemple, uniquement les algorithmes IKE mais pas IPsec)
Non, vous devez spécifier tous les algorithmes et paramètres pour IKE (mode principal) et IPsec (mode rapide). Vous n’êtes pas en droit de spécifier de stratégie partielle.

### <a name="what-are-hello-algorithms-and-key-strengths-supported-in-hello-custom-policy"></a>Quelles sont les algorithmes hello et avantages clés pris en charge dans la stratégie personnalisée de hello ?
Hello ci-dessous répertorie les algorithmes de chiffrement pris en charge de hello et atouts configurables par les clients de hello. Vous devez sélectionner une option pour chaque champ.

| **IPsec/IKEv2**  | **Options**                                                                   |
| ---              | ---                                                                           |
| Chiffrement IKEv2 | AES256, AES192, AES128, DES3, DES                                             |
| Intégrité IKEv2  | SHA384, SHA256, SHA1, MD5                                                     |
| Groupe DH         | DHGroup24, ECP384, ECP256, DHGroup14 (DHGroup2048), DHGroup2, DHGroup1, Aucun |
| Chiffrement IPsec | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, Aucun      |
| Intégrité IPsec  | GCMAES256, GCMAES192, GCMAES128, SHA256, SHA1, MD5                            |
| Groupe PFS        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, Aucun                              |
| Durée de vie de l’AS en mode rapide   | Secondes (entier ; **min 300**  /par défaut 27 000 secondes)<br>Kilo-octets (entier ; **min 1 024**  /par défaut 102 400 000 Ko)           |
| Sélecteur de trafic | UsePolicyBasedTrafficSelectors ($True/$False; default $False)                 |
|                  |                                                                               |

> [!IMPORTANT]
> 1. DHGroup2048 & PFS2048 sont hello même en tant que groupe Diffie-Hellman **14** dans IKE et IPsec PFS. Consultez [groupes Diffie-Hellman](#DH) pour hello compléter les correspondances.
> 2. Pour les algorithmes GCMAES, vous devez spécifier hello même longueur de clé et l’algorithme GCMAES pour le chiffrement IPsec et l’intégrité.
> 3. Durée de vie de SA de Mode principal IKEv2 est fixée à 28 800 secondes sur les passerelles VPN Azure hello
> 4. Les durées de vie de l’AS en mode rapide sont des paramètres facultatifs. Si rien n’a été spécifié, les valeurs par défaut de 27 000 secondes (7,5 heures) et de 102 400 000 Ko (102 Go) sont utilisées.
> 5. UsePolicyBasedTrafficSelector est un paramètre de l’option de connexion de hello. Consultez hello la question fréquemment posée suivante correspondant à « UsePolicyBasedTrafficSelectors »

### <a name="does-everything-need-toomatch-between-hello-azure-vpn-gateway-policy-and-my-on-premises-vpn-device-configurations"></a>Tous les éléments doit-elle toomatch entre hello stratégie de passerelle VPN Azure et Mes configurations d’appareil VPN local ?
Configuration de votre périphérique VPN local doit correspondre à ou contenir des hello suite d’algorithmes et les paramètres que vous spécifiez sur hello stratégie IPsec/IKE de Azure :

* Algorithme de chiffrement IKE
* Algorithme d’intégrité IKE
* Groupe DH
* Algorithme de chiffrement IPsec
* Algorithme d’intégrité IPsec
* Groupe PFS
* Sélecteur de trafic (*)

durées de vie Hello SA sont des spécifications locales uniquement, n’est pas nécessaire de toomatch.

Si vous activez **UsePolicyBasedTrafficSelectors**, vous devez tooensure votre périphérique VPN a hello mise en correspondance les sélecteurs de trafic définis avec toutes les combinaisons de vos préfixes de (passerelle de réseau local) de réseau local à partir de hello Préfixes de réseau virtuel Azure, au lieu de tout. Par exemple, si les préfixes de votre réseau local sont 10.1.0.0/16 et 10.2.0.0/16, et les préfixes de votre réseau virtuel sont 192.168.0.0/16 et 172.16.0.0/16, vous devez hello toospecify suivant des sélecteurs de trafic :
* 10.1.0.0/16 <====> 192.168.0.0/16
* 10.1.0.0/16 <====> 172.16.0.0/16
* 10.2.0.0/16 <====> 192.168.0.0/16
* 10.2.0.0/16 <====> 172.16.0.0/16

Consultez trop[connecter plusieurs périphériques VPN basée sur des stratégies locales](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) pour plus d’informations sur la façon de toouse cette option.

### <a name ="DH"></a>Quels groupes Diffie-Hellman sont pris en charge ?
tableau de Hello ci-dessous répertorie les groupes de Diffie-Hellman hello pris en charge pour le protocole IKE (DHGroup) et IPsec (PFSGroup) :

| **Groupe Diffie-Hellman**  | **DHGroup**              | **PFSGroup** | **Longueur de clé** |
| ---                       | ---                      | ---          | ---            |
| 1                         | DHGroup1                 | PFS1         | MODP 768 bits   |
| 2                         | DHGroup2                 | PFS2         | MODP 1 024 bits  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | MODP 2 048 bits  |
| 19                        | ECP256                   | ECP256       | ECP 256 bits    |
| 20                        | ECP384                   | ECP284       | ECP 384 bits    |
| 24                        | DHGroup24                | PFS24        | MODP 2 048 bits  |
|                           |                          |              |                |

Consultez trop[RFC3526](https://tools.ietf.org/html/rfc3526) et [RFC5114](https://tools.ietf.org/html/rfc5114) pour plus d’informations.

### <a name="does-hello-custom-policy-replace-hello-default-ipsecike-policy-sets-for-azure-vpn-gateways"></a>Stratégie personnalisée de hello remplace des jeux de stratégie IPsec/IKE hello par défaut pour les passerelles VPN Azure ?
Oui, une fois qu’une stratégie personnalisée est spécifiée sur une connexion, passerelle VPN Azure s’utiliser uniquement une stratégie de hello sur connexion hello, à la fois en tant qu’initiateur IKE et le répondeur IKE.

### <a name="if-i-remove-a-custom-ipsecike-policy-does-hello-connection-become-unprotected"></a>Si je supprime une stratégie IPsec/IKE personnalisée, ne les connexion hello devient non protégée ?
Non, connexion de hello est protégée par IPsec/IKE. Lorsque vous supprimez une connexion de stratégie personnalisée de hello, passerelle VPN Azure de hello reviendra arrière toohello [liste par défaut des propositions de IPsec/IKE](../articles/vpn-gateway/vpn-gateway-about-vpn-devices.md) et redémarrez hello négociation IKE avec votre périphérique VPN sur site.

### <a name="would-adding-or-updating-an-ipsecike-policy-disrupt-my-vpn-connection"></a>L’ajout ou la mise à jour d’une stratégie IPsec/IKE risquent-ils de perturber ma connexion VPN ?
Oui, il pourrait entraîner l’interruption petite (quelques secondes) comme passerelle VPN Azure de hello sera détruire la connexion existante de hello et redémarrez hello IKE négociation toore-établir le tunnel d’IPsec hello avec les nouveaux algorithmes de chiffrement hello et les paramètres. Vérifiez que votre périphérique VPN sur site est également configuré avec une interruption atouts toominimize hello et les algorithmes de correspondance de hello.

### <a name="can-i-use-different-policies-on-different-connections"></a>Puis-je utiliser des stratégies différentes pour des connexions distinctes ?
Oui. Une stratégie personnalisée est appliquée sur une base par connexion. Vous pouvez créer et appliquer des stratégies IPsec/IKE différentes pour des connexions distinctes. Vous pouvez également choisir tooapply stratégies personnalisées sur un sous-ensemble de connexions. Hello restants utilisera les jeux de stratégie IPsec/IKE hello Azure par défaut.

### <a name="can-i-use-hello-custom-policy-on-vnet-to-vnet-connection-as-well"></a>Puis-je utiliser une stratégie personnalisée de hello sur la connexion au réseau ?
Oui, vous pouvez appliquer la stratégie personnalisée pour des connexions IPsec entre différents sites locaux ou des connexions entre des réseaux virtuels.

### <a name="do-i-need-toospecify-hello-same-policy-on-both-vnet-to-vnet-connection-resources"></a>Ai-je besoin toospecify hello même stratégie sur les ressources de connexion au réseau ?
Oui. Un tunnel entre des réseaux virtuels se compose de deux ressources de connexion dans Azure, une pour chaque direction. Vous devez tooensure les ressources de connexion ont hello même stratégie, othereise hello réseau à connexion établira pas.

### <a name="does-custom-ipsecike-policy-work-on-expressroute-connection"></a>La stratégie IPsec/IKE est-elle compatible avec une connexion ExpressRoute ?
Non. Stratégie IPsec/IKE fonctionne uniquement sur les VPN S2S et les connexions au réseau via les passerelles VPN Azure hello.
