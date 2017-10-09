---
title: "pare-feu d’applications aaaIntroduction tooweb (WAF) pour la passerelle d’Application Azure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble du pare-feu d’applications web (WAF) pour la passerelle Application Gateway"
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 04b362bc-6653-4765-86f6-55ee8ec2a0ff
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: amsriva
ms.openlocfilehash: 5a42ce0fb2bd12a391844099e2de8fa2571195e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="web-application-firewall-waf"></a>Pare-feu d’applications web (WAF)

Le pare-feu d’applications Web (WAF) est une fonctionnalité de passerelle d’application qui protège vos applications web de manière centralisée contre les vulnérabilités et exploits courants. 

Pare-feu d’applications Web est basé sur les règles de hello [OWASP avoir des ensembles de règles principales](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) 3.0 ou 2.2.9. Les applications Web sont de plus en plus la cible d’attaques malveillantes qui exploitent des vulnérabilités connues. Communs à ces attaques sont des attaques par injection SQL, l’écriture de scripts entre sites attaques tooname quelques exemples. Prévention de telles attaques dans le code d’application peut être difficile et peut nécessiter rigoureuse maintenance, mise à jour corrective et la surveillance de plusieurs couches de la topologie de l’application hello. Un pare-feu d’applications web centralisé permet de simplifier la gestion de la sécurité et offre une meilleure assurance aux administrateurs de tooapplication contre les menaces ou les intrusions. Une solution WAF peut réagir également de menace pour la sécurité tooa plus rapide par la mise à jour corrective une vulnérabilité connue à un emplacement central par rapport à la sécurisation de chacune des applications web individuelles. Les passerelles d’application existant peuvent être converti tooa web application pare-feu est activé application passerelle facilement.

![imageURLroute](./media/application-gateway-web-application-firewall-overview/WAF1.png)

Passerelle d’application fonctionne comme une remise contrôleur et des offres SSL arrêt de l’application, d’affinité de session basée sur un cookie, distribution de la charge de tourniquet, le routage basé sur le contenu, capacité toohost plusieurs améliorations de sécurité et de sites Web. Améliorations de la sécurité offertes par la passerelle d’Application incluent la gestion de stratégie SSL, tooend fin prennent en charge de SSL. Sécurité de l’application est désormais fournie par WAF (pare-feu d’applications web) offre de hello ADC intégré directement. Cela fournit un toomanage d’emplacement central tooconfigure facile et protéger vos applications web contre les vulnérabilités de web courantes.

## <a name="benefits"></a>Avantages

Hello Voici les principaux avantages hello qui fournissent des pare-feu d’applications web et de la passerelle d’Application :

### <a name="protection"></a>Protection

* Protéger votre application web contre les vulnérabilités de web et sans code toobackend de modification.

* Protéger web plusieurs applications à hello même moment derrière une passerelle d’application. Passerelle d’application prend en charge l’hébergement des sites Web de too20 derrière une passerelle unique qui pourrait être protégée contre les attaques de web avec WAF.

### <a name="monitoring"></a>Surveillance

* Analysez les attaques contre votre application web à l’aide d’un journal WAF en temps réel. Ce journal est intégré à [moniteur Azure](../monitoring-and-diagnostics/monitoring-overview.md) tootrack WAF alertes et se connecte et analyser facilement les tendances.

* WAF sera bientôt intégré à Azure Security Center. Centre de sécurité Azure permet une vue centralisée de l’état de sécurité hello de toutes vos ressources Azure.

### <a name="customization"></a>Personnalisation

* Hello capacité toocustomize WAF règles et règle regroupe les spécifications de votre application toosuit et éliminer les faux positifs.

## <a name="features"></a>Caractéristiques

Pare-feu d’applications Web est préconfiguré avec CRS 3.0 par défaut, ou vous pouvez choisir toouse 2.2.9. CRS 3.0 permet une réduction des faux positifs au-delà de la version 2.2.9. Hello capacité trop[personnaliser les règles toosuit vos besoins](application-gateway-customize-waf-rules-portal.md) est fourni. Parmi le pare-feu d’applications web protège contre les vulnérabilités web courantes hello inclut :

* Protection contre les injections de code SQL
* Protection de l’exécution de script de site à site
* Protection contre les attaques web courante comme l’injection de commande, les dissimulations de requêtes HTTP, la séparation de réponse HTTP et les attaques RFI (Remote File Inclusion)
* Protection contre les violations de protocole HTTP
* Protection contre les anomalies de protocole HTTP comme un agent-utilisateur hôte manquant et les en-têtes Accept
* Protection contre les robots, les crawlers et les scanneurs
* Détection des erreurs de configuration d’application courantes (par exemple, Apache, IIS, etc.)

Pour une liste plus détaillée des règles et les protections Voir hello [ensembles de règles de base](#core-rule-sets).

### <a name="core-rule-sets"></a>Ensembles de règles de base

Application Gateway prend en charge les ensembles de règles CRS 3.0 et CRS 2.2.9. Ces ensembles de règles de base sont des ensembles de règles qui protègent vos applications web des activités malveillantes.

#### <a name="owasp30"></a>OWASP_3.0

ensemble de règles Hello 3.0 core fourni comporte des groupes de règles 13 comme illustré dans hello tableau suivant. Chacun de ces groupes de règles contient plusieurs règles, qui peuvent être désactivées.

|RuleGroup|Description|
|---|---|
|**[REQUEST-910-IP-REPUTATION](application-gateway-crs-rulegroups-rules.md#crs910)**|Contient des tooprotect de règles par rapport aux expéditeurs connus ou des activités malveillantes.|
|**[REQUEST-911-METHOD-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs911)**|Contient des toolock règles méthodes (PUT, PATCH <..)|
|**[REQUEST-912-DOS-PROTECTION](application-gateway-crs-rulegroups-rules.md#crs912)**| Contient les règles des tooprotect contre les attaques par déni de Service (DoS).|
|**[REQUEST-913-SCANNER-DETECTION](application-gateway-crs-rulegroups-rules.md#crs913)**| Contient des tooprotect de règles par rapport à des analyseurs de port et l’environnement.|
|**[REQUEST-920-PROTOCOL-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs920)**|Contient tooprotect règles contre le protocole et les problèmes de codage.|
|**[REQUEST-921-PROTOCOL-ATTACK](application-gateway-crs-rulegroups-rules.md#crs921)**|Contient des tooprotect de règles par rapport à l’injection de l’en-tête, demande de piratage et fractionnement de réponse|
|**[REQUEST-930-APPLICATION-ATTACK-LFI](application-gateway-crs-rulegroups-rules.md#crs930)**|Contient tooprotect règles contre les attaques de fichier et chemin d’accès.|
|**[REQUEST-931-APPLICATION-ATTACK-RFI](application-gateway-crs-rulegroups-rules.md#crs931)**|Contient des règles tooprotect contre d’Inclusion de fichier distant (RFI)|
|**[REQUEST-932-APPLICATION-ATTACK-RCE](application-gateway-crs-rulegroups-rules.md#crs932)**|Contient des règles tooprotect à nouveau l’exécution de Code.|
|**[REQUEST-933-APPLICATION-ATTACK-PHP](application-gateway-crs-rulegroups-rules.md#crs933)**|Contient tooprotect règles contre les attaques par injection de PHP.|
|**[REQUEST-941-APPLICATION-ATTACK-XSS](application-gateway-crs-rulegroups-rules.md#crs941)**|Contient des règles de protection de l’exécution de script de site à site.|
|**[REQUEST-942-APPLICATION-ATTACK-SQLI](application-gateway-crs-rulegroups-rules.md#crs942)**|Contient des règles de protection contre les attaques par injection de code SQL.|
|**[REQUEST-943-APPLICATION-ATTACK-SESSION-FIXATION](application-gateway-crs-rulegroups-rules.md#crs943)**|Contient tooprotect règles contre les attaques de Fixation de Session.|

#### <a name="owasp229"></a>OWASP_2.2.9

ensemble de règles de base Hello 2.2.9 fourni comporte 10 groupes de règles comme illustré dans hello tableau suivant. Chacun de ces groupes de règles contient plusieurs règles, qui peuvent être désactivées.

|RuleGroup|Description|
|---|---|
|**[crs_20_protocol_violations](application-gateway-crs-rulegroups-rules.md#crs20)**|Contient les règles des tooprotect contre les violations de protocole (caractères non valides, GET avec un corps de la demande, un etc..)|
|**[crs_21_protocol_anomalies](application-gateway-crs-rulegroups-rules.md#crs21)**|Contient des tooprotect de règles par rapport aux informations d’en-tête incorrect.|
|**[crs_23_request_limits](application-gateway-crs-rulegroups-rules.md#crs23)**|Contient des tooprotect de règles par rapport à des arguments ou des fichiers qui dépassent les limites.|
|**[crs_30_http_policy](application-gateway-crs-rulegroups-rules.md#crs30)**|Contient des tooprotect de règles par rapport aux méthodes restreintes, les en-têtes et les types de fichiers. |
|**[crs_35_bad_robots](application-gateway-crs-rulegroups-rules.md#crs35)**|Contient des tooprotect de règles par rapport à des robots et des scanneurs.|
|**[crs_40_generic_attacks](application-gateway-crs-rulegroups-rules.md#crs40)**|Contient les règles des tooprotect contre les attaques de génériques (fixation de session, d’inclusion de fichiers distant, injection de PHP, etc.)|
|**[crs_41_sql_injection_attacks](application-gateway-crs-rulegroups-rules.md#crs41sql)**|Contient les règles des tooprotect contre les attaques par injection SQL|
|**[crs_41_xss_attacks](application-gateway-crs-rulegroups-rules.md#crs41xss)**|Contient tooprotect règles contre cross-site scripting.|
|**[crs_42_tight_security](application-gateway-crs-rulegroups-rules.md#crs42)**|Contient un tooprotect règle contre les attaques de parcours d’un chemin d’accès|
|**[crs_45_trojans](application-gateway-crs-rulegroups-rules.md#crs45)**|Contient des tooprotect de règles par rapport aux chevaux de Troie de porte dérobée.|

### <a name="waf-modes"></a>Modes WAF

WAF de passerelle d’application peut être configurée toorun Bonjour suivant deux modes :

* **Mode de détection** : lorsque toorun configuré en mode de détection, Application passerelle WAF surveille et enregistre toutes les alertes de menaces dans le fichier de journal tooa. Journalisation des diagnostics pour la passerelle d’Application ne doit être activées à l’aide de hello **Diagnostics** section. Vous devez également tooensure qui hello WAF journal est sélectionné et activé. Le pare-feu d’applications web exécuté en mode de détection ne bloque pas les requêtes entrantes.
* **Mode de prévention** – lorsque toorun configuré en mode de prévention, Application Gateway bloque activement les intrusions et les attaques détectées par les règles. les intrus Hello reçoit une exception d’accès non autorisé 403 et hello connexion est interrompue. Mode de prévention continue toolog ces attaques dans les journaux hello WAF.

### <a name="application-gateway-waf-reports"></a>Surveillance du pare-feu d’applications web

Il est important de surveiller la santé de votre passerelle d’application hello. Surveillance de l’intégrité de hello de vos applications d’application web du pare-feu et hello qu’il protège sont fournis par la journalisation et l’intégration avec le moniteur de Windows Azure, Azure Security Center (prochainement) et Analytique de journal.

![diagnostics](./media/application-gateway-web-application-firewall-overview/diagnostics.png)

#### <a name="azure-monitor"></a>Azure Monitor

Chaque journal de passerelle d’application est intégré à [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md).  Cela vous permet de tootrack des informations de diagnostic, y compris les journaux et alertes de WAF.  Cette fonctionnalité est fournie dans hello ressource passerelle d’Application de portail hello sous hello **Diagnostics** onglet ou directement via hello Azure moniteur service. toolearn plus d’informations sur l’activation des journaux de diagnostic pour la passerelle d’application visitez [diagnostics de la passerelle d’Application](application-gateway-diagnostics.md)

#### <a name="azure-security-center"></a>Azure Security Center

[Centre de sécurité Azure](../security-center/security-center-intro.md) vous aide à vous empêchez, détectez et répondre toothreats avec une meilleure visibilité et contrôler hello la sécurité de vos ressources Azure. Désormais, Application Gateway [s’intègre à Azure Security Center](application-gateway-integration-security-center.md). Centre de sécurité Azure analyse les applications web votre environnement toodetect non protégé. Il peut maintenant vous recommander application passerelle WAF tooprotect ces ressources vulnérables. Vous pouvez créer directement WAF de passerelle d’application à partir de hello Azure Security Center.  Ces instances WAF sont intégrées à Azure Security Center et seront renvoyer des alertes et les informations de contrôle d’intégrité tooAzure le centre de sécurité pour les rapports.

![figure 1](./media/application-gateway-web-application-firewall-overview/figure1.png)

#### <a name="logging"></a>Journalisation

Application Gateway WAF fournit des rapports détaillés sur chaque menace détectée. La journalisation est intégrée aux journaux Azure Diagnostics et les alertes sont enregistrées au format json. Ces journaux peuvent être intégrés à [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).

![imageURLroute](./media/application-gateway-web-application-firewall-overview/waf2.png)

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupId}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{appGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

## <a name="application-gateway-waf-sku-pricing"></a>Tarification de la référence SKU Application Gateway WAF

Le pare-feu d’applications web est disponible sous une nouvelle référence WAF. Cette référence est disponible uniquement dans le modèle de déploiement Azure Resource Manager et non sous le modèle de déploiement classique hello. Par ailleurs, la référence WAF est proposée uniquement dans les instances de passerelle d’application de moyenne et grande taille. Toutes les limites de hello pour la passerelle d’application s’appliquent également à toohello WAF référence (SKU). La tarification est basée sur les frais d’instance de passerelle par heure et les frais de traitement des données. La tarification par heure de la passerelle pour la référence WAF diffère des frais de référence Standard et est accessible sur [Détails de tarification Application Gateway](https://azure.microsoft.com/pricing/details/application-gateway/). Le traitement des données des frais restent hello identiques. Il n’existe aucun frais par règle ou groupe de règles. Vous pouvez protéger plusieurs applications web derrière hello même web pare-feu d’applications et pas de frais supplémentaires pour prendre en charge de plusieurs applications. 

La facturation pour WAF commence efficacement 5/5/2017, jusqu'à ce que hello puis les passerelles de référence (SKU) WAF continue toobe facturée au tarif standard.

## <a name="next-steps"></a>Étapes suivantes

Après avoir plus d’informations sur les fonctionnalités de WAF hello de formation, visitez [comment tooconfigure web pare-feu d’applications sur la passerelle d’Application](application-gateway-web-application-firewall-portal.md).

