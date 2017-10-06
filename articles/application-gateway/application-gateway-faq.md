---
title: "aaaFrequently aux questions pour la passerelle d’Application Azure | Documents Microsoft"
description: "Cette page fournit des réponses aux questions sur la passerelle d’Application Azure d’elles sonttrop"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a>Forum aux questions pour Azure Application Gateway

## <a name="general"></a>Généralités

**Q. Qu’est-ce qu’Application Gateway ?**

Azure Application Gateway est un contrôleur de remise d’application proposé sous la forme d’un service, qui offre diverses fonctionnalités d’équilibrage de charge de couche 7 pour vos applications. Il fournit un service hautement disponible et évolutif, entièrement géré par Azure.

**Q. Quelles sont les fonctionnalités prises en charge par Application Gateway ?**

Passerelle d’application prend en charge SSL tooend fin et de déchargement SSL, pare-feu d’applications Web, d’affinité de session basée sur un cookie, l’url basée sur le chemin d’accès routage, hébergement de plusieurs sites et d’autres. Pour obtenir une liste complète des fonctionnalités prises en charge, visitez [Introduction tooApplication passerelle](application-gateway-introduction.md)

**Q. Qu’est la différence de hello entre la passerelle d’Application et l’équilibrage de charge Azure ?**

Application Gateway est un équilibreur de charge de couche 7, ce qui signifie qu’il fonctionne avec le trafic web uniquement (HTTP/HTTPS/WebSocket). Il prend en charge des fonctionnalités telles que la terminaison SSL, l’affinité de session basée sur les cookies et le tourniquet (round robin) pour le trafic d’équilibrage de charge. Load Balancer équilibre la charge du trafic au niveau de la couche 4 (TCP/UDP).

**Q. Quels sont les protocoles pris en charge par Application Gateway ?**

Application Gateway prend en charge les protocoles HTTP, HTTPS et WebSocket.

**Q. Quelles sont les ressources actuellement prises en charge dans le pool backend ?**

Les pools backend peuvent être composés de cartes d’interface réseau, de groupes de machines virtuelles identiques, d’adresses IP publiques, d’adresses IP internes, de noms de domaine complets et de serveurs principaux multi-locataires comme Azure Web Apps. Passerelle d’application ne sont pas membres du pool principal lié tooan à haute disponibilité. Les membres des pools backend peuvent être sur des clusters, des centres de données ou en dehors d’Azure tant qu’ils disposent d’une connectivité IP.

**Q. Les régions de service n’hello est disponible dans ?**

Application Gateway est disponible dans toutes les régions de la version globale d’Azure. Il est également disponible dans [Azure en Chine](https://www.azure.cn/) et [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/).

**Q. S’agit-il d’un déploiement dédié à mon abonnement ou est-il partagé entre les clients ?**

Application Gateway est un déploiement dédié dans votre réseau virtuel.

**Q. La redirection HTTP->HTTPS est-elle prise en charge ?**

La redirection est prise en charge. Visitez [vue d’ensemble de la redirection de passerelle d’Application](application-gateway-redirect-overview.md) toolearn plus.

**Q. Dans quel ordre les écouteurs sont-ils traités ?**

Écouteurs sont traités dans l’ordre de hello qu'elles sont affichées. Pour cette raison, si un écouteur de base correspond à une demande entrante, il la traite en premier.  Écouteurs de plusieurs sites doivent être configurés avant un trafic de tooensure base écouteur est routé toohello correct principal.

**Q. Où puis-je trouver le DNS et l’adresse IP d’Application Gateway ?**

Lorsque vous utilisez une adresse IP publique comme point de terminaison, ces informations sont accessibles sur la ressource d’adresse IP publique hello ou sur la page de vue d’ensemble de hello pour hello passerelle d’Application dans le portail de hello. Pour les adresses IP internes, ce sont accessibles sur la page de vue d’ensemble de hello.

**Q. Hello DNS ou IP change sur la durée de vie hello Hello passerelle d’Application ?**

Hello adresse IP virtuelle peut changer si la passerelle de hello est arrêté et démarré par le client de hello. Hello DNS associés avec la passerelle d’Application ne change pas hello du cycle de vie de la passerelle de hello. Pour cette raison, il est recommandé de toouse un alias CNAME et faites-le pointer adresse DNS toohello hello passerelle d’Application.

**Q. Application Gateway prend-il en charge les adresses IP statiques ?**

Non, Application Gateway ne prend pas en charge les adresses IP publiques statiques. Néanmoins, les adresses IP internes statiques sont prises en charge.

**Q. Passerelle d’Application prend-elle en charge plusieurs adresses IP publique sur la passerelle hello ?**

Une seule adresse IP publique est prise en charge sur Application Gateway.

**Q. Application Gateway prend-il en charge les en-têtes x-forwarded-for ?**

Oui, passerelle d’Application insère x transmis pour, proto x transféré et en-têtes x-transféré-port dans la demande de hello transmis toohello principal. format Hello pour x transmis pour l’en-tête est une liste séparée par des virgules d’IP : port. les valeurs valides Hello proto x transmis sont http ou https. X-transféré-port Spécifie le port hello qui demande hello atteint hello passerelle d’Application.

**Q. Combien de temps faut-il toodeploy une passerelle d’Application ? Mon Application Gateway continue-t-elle de fonctionner après une mise à jour  ?**

Les nouveaux déploiements de passerelle d’Application peuvent prendre jusqu'à too20 minutes tooprovision. Taille ou de nombre modifications tooinstance ne sont pas sans interruption, et passerelle de hello reste actif pendant ce temps.

## <a name="configuration"></a>Configuration

**Q. Application Gateway est-il toujours déployé dans un réseau virtuel ?**

Oui, Application Gateway est toujours déployé dans un sous-réseau de réseau virtuel. Ce sous-réseau ne peut contenir que des Application Gateway.

**Q. Passerelle d’Application peut communiquer avec tooinstances en dehors de son réseau virtuel ?**

Passerelle d’application peut communiquer avec tooinstances en dehors du réseau virtuel hello qu’il est aussi de connectivité IP. Si vous prévoyez de toouse le nécessite des adresses IP internes en tant que membres du pool principal, puis il [réseau virtuel d’homologation](../virtual-network/virtual-network-peering-overview.md) ou [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).

**Q. Puis-je déployer rien d’autre dans le sous-réseau de passerelle d’Application hello ?**

Non, mais vous pouvez déployer d’autres passerelles d’application dans un sous-réseau de hello.

**Q. Groupes de sécurité réseau sont pris en charge sur le sous-réseau de passerelle d’Application hello ?**

Groupes de sécurité réseau sont pris en charge sur le sous-réseau de passerelle d’Application hello hello suivant restrictions :

* Exceptions doivent être placées dans pour le trafic entrant sur les ports 65503-65 534 pour le serveur principal d’intégrité toowork correctement.

* La connectivité Internet sortante ne peut pas être bloquée.

* Le trafic à partir de hello AzureLoadBalancer balise doit être autorisé.

**Q. Quelles sont les limites de hello sur la passerelle d’Application ? Puis-je augmenter ces limites ?**

Visitez [limites de passerelle d’Application](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello limites.

**Q. Puis-je utiliser Application Gateway pour le trafic externe et interne simultanément ?**

Oui, Application Gateway peut avoir une adresse IP interne et une adresse IP externe par Application Gateway.

**Q. VNET Peering est-il pris en charge ?**

Oui, VNET Peering est pris en charge et est utile pour équilibrer la charge du trafic des autres réseaux virtuels.

**Q. Puis-je parler tooon des serveurs locaux lorsqu’ils sont connectés par des tunnels ExpressRoute ou VPN ?**

Oui, tant que le trafic est autorisé.

**Q. Puis-je avoir un pool backend servant plusieurs applications sur des ports différents ?**

L’architecture orientée microservices est prise en charge. Il vous faudrait plusieurs tooprobe de paramètres configurés http sur des ports différents.

**Q. Les sondes personnalisées prennent-elles en charge les caractères génériques/les expressions régulières sur les données de réponse ?**

Les sondes personnalisées ne prennent pas en charge les caractères génériques/les expressions régulières sur les données de réponse. 

**Q. Comment les règles sont-elles traitées ?**

Les règles sont traitées dans l’ordre de hello qu’ils sont configurés. Il est recommandé que les règles de plusieurs sites sont configurés avant que les règles de base tooreduce hello risque que le trafic est acheminé principal inappropriée de toohello comme règle de base hello correspondrait à trafic en fonction de la règle de plusieurs sites toohello préalable des ports en cours d’évaluation.

**Q. Comment les règles sont-elles traitées ?**

Les règles sont traitées dans hello leur ordre de création. Nous vous recommandons de configurer les règles multi-sites avant les règles de base. En configurant les écouteurs multisites tout d’abord, cette configuration réduit les risques de hello que le trafic est routé toohello les principaux inappropriés. Ce problème de routage peut se produire comme règle de base hello correspondrait à trafic en fonction de la règle de plusieurs sites toohello préalable des ports en cours d’évaluation.

**Q. Ce que signifier champ de l’hôte hello pour les sondes personnalisés ?**

Champ de l’hôte spécifie hello nom toosend hello de la sonde. S’applique uniquement lorsque plusieurs sites sont configurés sur Application Gateway, sinon utilisez '127.0.0.1'. Cette valeur est différente du nom d’hôte de machine virtuelle et se trouve au format suivant : \<protocole\>://\<hôte\>:\<port\>\<chemin d’accès\>.

**Q. Puis-je tooa d’accès d’autorisation Application Gateway quelques adresses IP de source ?**

Ce scénario peut être réalisé en utilisant des groupes de sécurité réseau sur le sous-réseau d’Application Gateway. Hello suivant restrictions doit être placé sur sous-réseau hello dans l’ordre de hello répertorié de priorité :

* Autoriser le trafic entrant à partir de l’adresse IP ou de la plage d’adresses IP sources.

* Autoriser les demandes entrantes à partir de toutes les sources tooports 65503-65 534 pour [communication de contrôle d’intégrité de serveur principal](application-gateway-diagnostics.md).

* Autoriser les sondes d’équilibrage de charge Azure entrants (balise AzureLoadBalancer) et virtuel le trafic réseau entrant (balise VirtualNetwork) sur hello [NSG](../virtual-network/virtual-networks-nsg.md).

* Bloquer tout autre trafic entrant avec une règle Refuser tout.

* Autoriser le trafic sortant toohello internet pour toutes les destinations.

## <a name="performance"></a>Performances

**Q. Comment Application Gateway prend-il en charge la haute disponibilité et l’évolutivité ?**

Application Gateway prend en charge les scénarios de haute disponibilité lorsque vous avez deux instances déployées ou plus. Azure distribue ces instances sur mise à jour et les pannes tooensure domaines que toutes les instances n’échouent pas à hello même temps. Passerelle d’application prend en charge l’évolutivité en ajoutant plusieurs instances de hello charge hello de tooshare même passerelle.

**Q. Comment puis-je obtenir le scénario de récupération d’urgence dans les centres de données avec Application Gateway ?**

Les clients peuvent utiliser Traffic Manager toodistribute trafic entre plusieurs passerelles d’Application dans différents centres de données.

**Q. La mise à l’échelle automatique est-elle prise en charge ?**

Non, mais la passerelle d’Application a une mesure de débit qui peut être utilisé tooalert lorsqu’un seuil est atteint. Manuellement l’ajout d’instances ou de modification de taille ne redémarre pas de passerelle de hello et n’affecte pas le trafic existant.

**Q. Est-ce que les opérations de montée/descente en puissance effectuées manuellement interrompent le service ?**

Aucune interruption de service n’a lieu, les instances sont réparties entre les domaines de mise à niveau et les domaines d’erreur.

**Q. Puis-je modifier taille de l’instance à partir de la moyenne toolarge sans interruption de service ?**

Oui, Azure distribue les instances sur la mise à jour et les pannes tooensure domaines que toutes les instances n’échouent pas à hello même temps. Application prend en charge de la passerelle mise à l’échelle en ajoutant plusieurs instances de hello même passerelle tooshare hello de charge.

## <a name="ssl-configuration"></a>Configuration SSL

**Q. Quels sont les certificats pris en charge sur Application Gateway ?**

Les certificats auto-signés, les certificats d’autorité de certification et les certificats génériques sont pris en charge. Les certificats de validation étendue ne sont pas pris en charge.

**Q. Quelles sont les hello actuel les suites de chiffrement pris en charge par la passerelle d’Application ?**

Hello Voici hello actuel les suites de chiffrement pris en charge par la passerelle d’application. Visite : [configurer SSL versions de stratégie et des suites de chiffrement sur la passerelle d’Application](application-gateway-configure-ssl-policy-powershell.md) toolearn comment toocustomize options d’authentification SSL.

- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_3DES_EDE_CBC_SHA
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

**Q. Passerelle d’Application prennent également en charge rechiffrement de trafic toohello principal ?**

Oui, déchargement de passerelle d’Application prend en charge SSL et fin tooend SSL, qui chiffre à nouveau hello trafic toohello principal.

**Q. Puis-je configurer des versions de protocole SSL de toocontrol de stratégie SSL ?**

Oui, vous pouvez configurer la passerelle d’Application toodeny TLS1.0, TLS1.1 et TLS 1.2. SSL 2.0 et 3.0 sont déjà désactivés par défaut et ne sont pas configurables.

**Q. Puis-je configurer les suites de chiffrement et l’ordre de la stratégie ?**

Oui, la [configuration des suites de chiffrement](application-gateway-ssl-policy-overview.md) est prise en charge. Lorsque vous définissez une stratégie personnalisée, au moins un des hello suivant des suites de chiffrement doit être activé. Passerelle d’application utilise la gestion de serveur principal toofor SHA256.

* TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 
* TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
* TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_256_CBC_SHA256
* TLS_RSA_WITH_AES_128_CBC_SHA256

**Q. Quel est le nombre de certificats SSL pris en charge ?**

Too20 SSL certificats sont pris en charge.

**Q. Quel est le nombre de certificats d’authentification pour le nouveau chiffrement du backend pris en charge ?**

Jusqu'à too10 les certificats d’authentification sont pris en charge avec la valeur par défaut est 5.

**Q. Application Gateway s’intègre-t-il à Azure Key Vault en mode natif ?**

Non, il n’est pas intégré à Azure Key Vault.

## <a name="web-application-firewall-waf-configuration"></a>Configuration du pare-feu d’application web

**Q. Hello WAF référence (SKU) offre toutes les fonctionnalités de hello disponibles avec hello référence (SKU) Standard ?**

Oui, WAF prend en charge toutes les fonctionnalités de hello hello référence (SKU) Standard.

**Q. Quelle est la version CRS hello que prend en charge de la passerelle d’Application ?**

Application Gateway prend en charge CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) et CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).

**Q. Comment puis-je surveiller le pare-feu d’application web ?**

Le pare-feu d’application web est surveillé via la journalisation des diagnostics. Vous trouverez plus d’informations sur la journalisation des diagnostics dans l’article [Intégrité du serveur principal, journalisation des diagnostics et métriques pour la passerelle Application Gateway](application-gateway-diagnostics.md).

**Q. Est-ce que le mode de détection bloque le trafic ?**

Non, le mode de détection journalise uniquement le trafic, ce qui a déclenché une règle de pare-feu d’application web.

**Q. Comment puis-je personnaliser les règles de pare-feu d’application web ?**

Oui, les règles WAF sont personnalisables, pour plus d’informations sur comment toocustomize les visitez [WAF de personnaliser les règles et groupes de règles](application-gateway-customize-waf-rules-portal.md)

**Q. Quelles sont les règles actuellement disponibles ?**

WAF prend actuellement en charge CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) et [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), qui fournissent la sécurité de référence par rapport à la plupart des hello vulnérabilités 10 premiers identifiées par hello ouvrir Web Application sécurité projet (OWASP avoir) est disponible ici [OWASP avoir top 10 vulnérabilités](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)

* Protection contre les injections de code SQL

* Protection de l’exécution de script de site à site

* Protection contre les attaques web courante comme l’injection de commande, les dissimulations de requêtes HTTP, la séparation de réponse HTTP et les attaques RFI (Remote File Inclusion)

* Protection contre les violations de protocole HTTP

* Protection contre les anomalies de protocole HTTP comme un agent-utilisateur hôte manquant et les en-têtes Accept

* Protection contre les robots, les crawlers et les scanneurs

* Détection des erreurs de configuration d’application courantes (par exemple, Apache, IIS, etc.)

**Q. Le pare-feu d’application web prend-il également en charge la prévention DDoS ?**

Non, le pare-feu d’application web ne fournit pas de prévention DDoS.

## <a name="diagnostics-and-logging"></a>Diagnostics et journalisation

**Q. Quels sont les types de journaux disponibles avec Application Gateway ?**

Trois journaux sont disponibles pour Application Gateway. Pour plus d’informations sur ces journaux et d’autres fonctionnalités de diagnostic, consultez l’article [Intégrité backend, journaux des diagnostics et métriques pour la passerelle Application Gateway](application-gateway-diagnostics.md).

- **ApplicationGatewayAccessLog** -journal d’accès hello contient chaque demande envoyée toohello passerelle d’Application frontale. les données de salutation incluent IP l’appelant hello, URL demandée, latence de la réponse, code de retour, octets et l’extraction. Le journal d’accès est collecté toutes les 300 secondes. Ce journal contient un enregistrement par instance Application Gateway.
- **ApplicationGatewayPerformanceLog** -journal de performances hello capture des informations de performances sur par instance, y compris le total de demandes traitée, le débit en octets, le nombre total de demandes traitées, nombre de demandes ayant échoué et incorrect nombre d’instances de serveur principal.
- **ApplicationGatewayFirewallLog** -journal du pare-feu hello contient des requêtes qui sont enregistrés via le mode de détection ou de prévention d’une passerelle d’application qui est configuré avec un pare-feu d’applications web.

**Q. Comment savoir si les membres de mon pool backend sont intègres ?**

Vous pouvez utiliser les applets de commande PowerShell hello `Get-AzureRmApplicationGatewayBackendHealth` ou vérifier l’intégrité via le portail de hello en vous rendant sur [Diagnostics de passerelle d’Application](application-gateway-diagnostics.md)

**Q. Quelle est la stratégie de rétention hello sur les journaux de diagnostic hello ?**

Compte de stockage de toohello clients des journaux de diagnostic et les clients peuvent définir la stratégie de rétention de hello en fonction de leurs préférences. Journaux de diagnostic peuvent également être envoyés à tooan concentrateur d’événements ou Analytique de journal. Consultez l’article [Intégrité du serveur principal, journalisation des diagnostics et métriques pour la passerelle Application Gateway](application-gateway-diagnostics.md) pour plus de détails.

**Q. Comment puis-je obtenir des journaux d’audit pour Application Gateway ?**

Les journaux d’audit sont disponibles pour Application Gateway. Dans le portail de hello, cliquez sur **le journal d’activité** dans le panneau de menu hello d’un journal d’audit de passerelle d’Application tooaccess hello. 

**Q. Puis-je définir des alertes avec Application Gateway ?**

Oui, Application Gateway prend en charge les alertes ; les alertes sont configurées à partir des mesures.  Passerelle d’application n’a actuellement une métrique de « débit », qui peut être tooalert configuré. toolearn en savoir plus sur les alertes, visitez [recevoir des notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

**Q. L’intégrité du serveur principal renvoie un état inconnu, à quoi est dû cet état ?**

raison la plus courante Hello est accès toohello principal est bloqué par un groupe de sécurité réseau ou le DNS personnalisé. Visitez [principal d’intégrité, de journalisation des diagnostics et de mesures pour la passerelle d’Application](application-gateway-diagnostics.md) toolearn plus.

## <a name="next-steps"></a>Étapes suivantes

toolearn plus sur la passerelle d’Application, visitez [Introduction tooApplication passerelle](application-gateway-introduction.md).
