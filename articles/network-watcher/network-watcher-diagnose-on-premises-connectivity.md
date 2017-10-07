---
title: "connectivité locale d’aaaDiagnose via la passerelle VPN avec l’Observateur de réseau Azure | Documents Microsoft"
description: "Cet article décrit comment toodiagnose local connectivité via une passerelle VPN Azure l’Observateur réseau résolution des problèmes de ressource."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: aeffbf3d-fd19-4d61-831d-a7114f7534f9
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9941c5d1b49bec29062210684dae8653cbdb84b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-on-premises-connectivity-via-vpn-gateways"></a>Diagnostiquer la connectivité locale par le biais de passerelles VPN

Passerelle VPN Azure vous permet de solution hybride toocreate permettant de traiter la nécessité de hello pour une connexion sécurisée entre votre réseau local et votre réseau virtuel Azure. Comme vos besoins sont uniques, par conséquent, est hello choix du périphérique VPN sur site. Azure prend actuellement en charge [plusieurs périphériques VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md#devicetable) qui sont validées en permanence en partenariat avec des fournisseurs d’appareils hello. Passez en revue les paramètres de configuration spécifiques à l’appareil hello avant de configurer votre périphérique VPN sur site. De même, la passerelle VPN Azure est configurée avec un ensemble de [paramètres IPsec pris en charge](../vpn-gateway/vpn-gateway-about-vpn-devices.md#ipsec) qui sont utilisés pour établir des connexions. Actuellement il n’existe aucun moyen pour vous toospecify ou sélectionnez une combinaison spécifique de paramètres IPsec à partir de hello passerelle VPN à Azure. Pour établir une connexion entre Azure et locaux, hello localement les paramètres de périphérique VPN doivent être conformément aux paramètres d’IPsec hello par la passerelle VPN à Azure. Si hello paramètres sont corrects, il existe une perte de connectivité et jusqu'à présent résoudre ces problèmes n’a pas été trivial généralement heures tooidentify et résoudre problème de hello.

Avec hello Observateur de réseau Azure résoudre les problèmes de fonctionnalité, sont en mesure de toodiagnose des problèmes avec votre passerelle et les connexions et de quelques minutes ont suffisamment toomake informations un problème de hello toorectify décision informée.

## <a name="scenario"></a>Scénario

Vous voulez tooconfigure un site à site entre Azure et locales à l’aide de FortiGate comme hello passerelle VPN sur site. tooachieve ce scénario, vous nécessiterait hello après l’installation :

1. Passerelle de réseau virtuel - hello la passerelle VPN Azure
1. Passerelle de réseau local - hello [(FortiGate) VPN passerelle locale](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) représentation dans le cloud Azure
1. Connexion de site à site (stratégie basée) - [connexion entre hello passerelle VPN et hello local routeur](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#createconnection)
1. [Configuration de FortiGate](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/Site-to-Site_VPN_using_FortiGate.md)

Vous trouverez des instructions pas à pas détaillées pour la configuration de Site à Site en vous rendant sur : [créer un réseau virtuel avec une connexion de Site à Site à l’aide de hello Azure portal](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

Une des étapes de configuration critiques hello consiste à configurer des paramètres de communication hello IPsec, une mauvaise configuration des prospects tooloss de connectivité entre le réseau local de hello et Azure. Actuellement, les passerelles VPN Azure sont hello toosupport configuré suivant les paramètres IPsec pour la Phase 1. Notez, comme mentionné précédemment, que ces paramètres ne peuvent pas être modifiés.  Comme vous pouvez le voir dans la table hello ci-dessous, les algorithmes de chiffrement hello pris en charge par la passerelle VPN à Azure sont AES256 AES128 et 3DES.

### <a name="ike-phase-1-setup"></a>Configuration IKE phase 1

| **Propriété** | **PolicyBased** | **Basé sur un itinéraire et passerelle VPN standard ou hautes performances** |
| --- | --- | --- |
| Version IKE |IKEv1 |IKEv2 |
| Groupe Diffie-Hellman |Groupe 2 (1 024 bits) |Groupe 2 (1 024 bits) |
| Méthode d'authentification |Clé prépartagée |Clé prépartagée |
| Algorithmes de chiffrement |AES256 AES128 3DES |AES256 3DES |
| Algorithme de hachage |SHA1(SHA128) |SHA1(SHA128), SHA2(SHA256) |
| Durée de vie d’association de sécurité de phase 1 (temps) |28 800 secondes |10 800 secondes |

En tant qu’utilisateur, vous serez requis tooconfigure votre FortiGate, un exemple de configuration se trouvent sur [GitHub](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/fortigate_show%20full-configuration.txt). Sans le savoir, vous avez configuré votre toouse FortiGate SHA-512 comme algorithme de hachage de hello. Comme cet algorithme n’est pas un algorithme pris en charge pour les connexions basées sur une stratégie, votre connexion VPN ne fonctionne pas.

Ces problèmes sont tootroubleshoot dur et causes principales sont souvent non intuitive. Dans ce cas, vous pouvez ouvrir une aide de tooget de ticket de prise en charge sur la résolution de problème de hello. Toutefois, l’API de résolution des problèmes d’Azure Network Watcher vous permet d’identifier ces problèmes vous-même.

## <a name="troubleshooting-using-azure-network-watcher"></a>Résolution des problèmes à l’aide d’Azure Network Watcher

toodiagnose connecter tooAzure PowerShell de votre connexion et lancer hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` applet de commande. Vous trouverez des détails de hello sur l’utilisation de cette applet de commande à [dépanner une passerelle de réseau virtuel et des connexions - PowerShell](network-watcher-troubleshoot-manage-powershell.md). Cette applet de commande peut prendre jusqu'à toofew minutes toocomplete.

Une fois que l’applet de commande hello est terminée, vous pouvez naviguer toohello emplacement de stockage spécifié dans l’applet de commande hello tooget des informations détaillées sur le problème de hello et les journaux. Observateur de réseau Azure crée un dossier zip qui contient les fichiers journaux suivants de hello :

![1][1]

Fichier ouvert hello appelé IKEErrors.txt et il affiche les informations suivantes hello erreur, indiquant un problème avec une configuration incorrecte du paramètre IKE sur site.

```
Error: On-premises device rejected Quick Mode settings. Check values.
     based on log : Peer sent NO_PROPOSAL_CHOSEN notify
```

Vous pouvez obtenir des informations détaillées à partir de hello Scrubbed-wfpdiag.txt sur l’erreur de hello, comme dans ce cas, il mentionne qu’il y a `ERROR_IPSEC_IKE_POLICY_MATCH` que tooconnection prospect ne fonctionne ne pas correctement.

Une autre configuration courante est hello en spécifiant des clés partagées incorrects. En cas de hello précédent exemple que vous aviez spécifié différentes clés partagées, hello IKEErrors.txt montre hello l’erreur suivante : `Error: Authentication failed. Check shared key`.

Observateur de réseau Azure résoudre les problèmes de fonctionnalité vous permet de toodiagnose et résoudre les problèmes de la passerelle VPN et une connexion avec facilité hello d’applet de commande PowerShell simple. Actuellement, nous prennent en charge de diagnostic hello conditions suivantes et travaillez en ajoutant plus de condition.

### <a name="gateway"></a>Passerelle

| Type d’erreur | Motif | Journal|
|---|---|---|
| NoFault | Quand aucune erreur n’est détectée. |Oui|
| GatewayNotFound | Passerelle introuvable ou non approvisionnée. |Non|
| PlannedMaintenance |  Instance de passerelle en maintenance.  |Non|
| UserDrivenUpdate | Quand une mise à jour utilisateur est en cours. Il peut s’agir d’une opération de redimensionnement. | Non |
| VipUnResponsive | Impossible d’atteindre instance principale hello hello passerelle. Cela se produit en cas d’échec de la sonde d’intégrité hello. | Non |
| PlatformInActive | Il existe un problème avec la plateforme de hello. | Non|
| ServiceNotRunning | service sous-jacent de Hello ne fonctionne pas. | Non|
| NoConnectionsFoundForGateway | Aucune connexion n’existe sur la passerelle hello. Il s’agit simplement d’un avertissement.| Non|
| ConnectionsNotConnected | Aucun des connexions de hello sont connectés. Il s’agit simplement d’un avertissement.| Oui|
| GatewayCPUUsageExceeded | utilisation de passerelle actuelle Hello l’utilisation du processeur est > 95 %. | Oui |

### <a name="connection"></a>Connexion

| Type d’erreur | Motif | Journal|
|---|---|---|
| NoFault | Quand aucune erreur n’est détectée. |Oui|
| GatewayNotFound | Passerelle introuvable ou non approvisionnée. |Non|
| PlannedMaintenance | Instance de passerelle en maintenance.  |Non|
| UserDrivenUpdate | Quand une mise à jour utilisateur est en cours. Il peut s’agir d’une opération de redimensionnement.  | Non |
| VipUnResponsive | Impossible d’atteindre instance principale hello hello passerelle. Il se produit en cas d’échec de la sonde d’intégrité hello. | Non |
| ConnectionEntityNotFound | La configuration de la connexion est manquante. | Non |
| ConnectionIsMarkedDisconnected | Hello connexion est marqué comme « déconnecté ». |Non|
| ConnectionNotConfiguredOnGateway | service d’Hello sous-jacent n’a pas de hello que connexion configurée. | Oui |
| ConnectionMarkedStandy | Hello service sous-jacent est marqué en état de secours.| Oui|
| Authentification | Non-concordance des clés prépartagées. | Oui|
| PeerReachability | passerelle de homologue Hello n’est pas accessible. | Oui|
| IkePolicyMismatch | passerelle de homologue Hello comporte des stratégies IKE qui ne sont pas pris en charge par Azure. | Oui|
| WfpParse Error | Une erreur s’est produite lors de l’analyse journal de protection de fichiers Windows hello. |Oui|

## <a name="next-steps"></a>Étapes suivantes

En savoir plus de la connectivité de passerelle VPN toocheck avec PowerShell et Azure Automation en vous rendant sur [passerelles de VPN de moniteur de résolution des problèmes de l’Observateur réseau Azure](network-watcher-monitor-with-azure-automation.md)

[1]: ./media/network-watcher-diagnose-on-premises-connectivity/figure1.png
