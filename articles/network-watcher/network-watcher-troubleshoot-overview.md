---
title: "tooresource aaaIntroduction résolution des problèmes dans l’Observateur réseau de Azure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble de capacités de dépannage de ressource hello Observateur réseau"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a>Tooresource présentation résolution des problèmes dans l’Observateur réseau de Azure

Les passerelles de réseau virtuel assurent une connectivité entre les ressources locales et d’autres réseaux virtuels dans Azure. Les passerelles et les connexions d’analyse est critique tooensuring communication n’est pas interrompue. Observateur réseau fournit hello capacité tootroubleshoot les connexions et les passerelles de réseau virtuel. Il peut être appelé via le portail de hello, PowerShell, CLI ou API REST. Lorsqu’elle est appelée, Observateur réseau permet de diagnostiquer la santé de passerelle de réseau virtuel hello ou de connexion et les résultats appropriés hello retour hello. Cette demande est une transaction longue, hello résultats une fois le diagnostic de hello est terminée.

![portail][2]

## <a name="results"></a>Résultats

Hello préliminaire résultats donnent une vue d’ensemble de la santé de ressource de hello hello. Informations plus approfondies peuvent être fournies pour les ressources comme indiqué dans hello suivant la section :

Hello Voici les valeurs hello retournées par hello résoudre les problèmes d’API :

* **startTime** -cette valeur est le temps hello hello résoudre les problèmes d’appel de l’API a démarré.
* **heure de fin** -cette valeur est l’heure de hello hello dépannage fin.
* **code** : la valeur est définie sur UnHealthy en cas d’échec du diagnostic.
* **résultats** -résultats est une collection de résultats retournés sur la passerelle de réseau virtuel de connexion ou hello hello.
    * **ID** -cette valeur est le type d’erreur hello.
    * **Résumé** -cette valeur est un résumé des pannes de hello.
    * **détaillées** -cette valeur fournit une description détaillée de l’erreur de hello.
    * **recommendedActions** -cette propriété est une collection d’actions recommandées tootake.
      * **actionText** -cette valeur contient le texte hello décrivant le tootake action.
      * **actionUri** -cette valeur fournit des hello URI toodocumentation tooact.
      * **actionUriText** -cette valeur est une brève description de texte d’action hello.

Hello suivant tables afficher hello différents types d’erreurs (id de sous les résultats à partir de hello précédant la liste) qui sont disponibles et si les pannes hello créent des journaux.

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
| ConnectionsNotConnected | Aucune connexion n’est établie. Il s’agit simplement d’un avertissement.| Oui|
| GatewayCPUUsageExceeded | utilisation du processeur de passerelle Hello est > 95 %. | Oui |

### <a name="connection"></a>Connexion

| Type d’erreur | Motif | Journal|
|---|---|---|
| NoFault | Quand aucune erreur n’est détectée. |Oui|
| GatewayNotFound | Passerelle introuvable ou non approvisionnée. |Non|
| PlannedMaintenance | Instance de passerelle en maintenance.  |Non|
| UserDrivenUpdate | Quand une mise à jour utilisateur est en cours. Il peut s’agir d’une opération de redimensionnement.  | Non |
| VipUnResponsive | Impossible d’atteindre instance principale hello hello passerelle. Il se produit en cas d’échec de la sonde d’intégrité hello. | Non |
| ConnectionEntityNotFound | La configuration de la connexion est manquante. | Non |
| ConnectionIsMarkedDisconnected | Hello connexion est marquée comme « déconnecté ». |Non|
| ConnectionNotConfiguredOnGateway | service d’Hello sous-jacent n’a pas de hello que connexion configurée. | Oui |
| ConnectionMarkedStandy | Hello service sous-jacent est marqué en état de secours.| Oui|
| Authentification | Non-concordance des clés prépartagées. | Oui|
| PeerReachability | passerelle de homologue Hello n’est pas accessible. | Oui|
| IkePolicyMismatch | passerelle de homologue Hello comporte des stratégies IKE qui ne sont pas pris en charge par Azure. | Oui|
| WfpParse Error | Une erreur s’est produite lors de l’analyse journal de protection de fichiers Windows hello. |Oui|

## <a name="supported-gateway-types"></a>Types de passerelles pris en charge

Hello liste suivante montre la prise en charge de hello les passerelles et les connexions sont pris en charge avec la résolution des problèmes de l’Observateur réseau.
|  |  |
|---------|---------|
|**Types de passerelles**   |         |
|VPN      | Pris en charge        |
|ExpressRoute | Non pris en charge |
|Hypernet | Non pris en charge|
|**Types de VPN** | |
|Route-based | Pris en charge|
|Policy-based | Non pris en charge|
|**Types de connexions**||
|IPsec| Pris en charge|
|Vnet2Vnet| Pris en charge|
|ExpressRoute| Non pris en charge|
|Hypernet| Non pris en charge|
|VPNClient| Non pris en charge|

## <a name="log-files"></a>Fichiers journaux

fichiers de journaux dépannage Hello ressource sont stockés dans un compte de stockage après que la résolution des problèmes de ressource sont terminée. Hello image suivante montre contenu d’exemple hello d’un appel qui a généré une erreur.

![fichier zip][1]

> [!NOTE]
> Dans certains cas, seul un sous-ensemble des fichiers de journaux hello est écrit toostorage.

Pour obtenir des instructions sur le téléchargement de fichiers à partir des comptes de stockage azure, consultez trop[prise en main le stockage Blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). L’explorateur de stockage peut aussi être utilisé. Plus d’informations sur l’Explorateur de stockage trouverez ici hello lien : [Explorateur de stockage](http://storageexplorer.com/)

### <a name="connectionstatstxt"></a>ConnectionStats.txt

Hello **ConnectionStats.txt** fichier contient des statistiques globales de hello connexion, y compris les octets d’entrée et de sortie, l’état de connexion et hello de temps hello connexion a été établie.

> [!NOTE]
> Si toohello d’appel hello dépannage API renvoie sain, seul hello retournée dans le fichier zip de hello est un **ConnectionStats.txt** fichier.

contenu Hello de ce fichier est similaires toohello l’exemple suivant :

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a>CPUStats.txt

Hello **CPUStats.txt** fichier contient l’utilisation du processeur et mémoire disponible au moment de hello du test.  contenu Hello de ce fichier est semblable toohello l’exemple suivant :

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a>IKEErrors.txt

Hello **IKEErrors.txt** fichier contient toutes les erreurs de IKE qui ont été détectées pendant l’analyse.

Hello suivant montre contenu hello d’un fichier IKEErrors.txt. Votre erreurs peuvent être différentes en fonction du problème de hello.

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a>Scrubbed-wfpdiag.txt

Hello **Scrubbed-wfpdiag.txt** fichier journal contient le journal de protection de fichiers Windows hello. Ce journal contient la journalisation des rejets de paquets et des échecs IKE/AuthIP.

Hello suivant montre contenu hello du fichier de Scrubbed-wfpdiag.txt hello. Dans cet exemple, la clé partagée de hello d’une connexion n’était pas correcte comme peuvent être consultés à partir de la ligne en bas de hello 3e hello. Hello l’exemple suivant est simplement un extrait de journal complet de hello, comme le journal de hello peut être longue, en fonction du problème de hello.

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a>wfpdiag.txt.Sum

Hello **wfpdiag.txt.sum** fichier est un journal présentant les mémoires tampons de hello et les événements traités.

Hello exemple suivant est contenu hello d’un fichier wfpdiag.txt.sum.
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment toodiagnose les passerelles VPN et les connexions via hello portail en vous rendant sur [dépannage de la passerelle - portail Azure](network-watcher-troubleshoot-manage-portal.md).
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
