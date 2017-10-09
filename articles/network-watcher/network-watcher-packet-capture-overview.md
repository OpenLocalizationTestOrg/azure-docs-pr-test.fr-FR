---
title: "capture de tooPacket aaaIntroduction dans l’Observateur réseau de Azure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble de la fonctionnalité de capture de paquets hello Observateur réseau"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a>Introduction toovariable capture des paquets dans l’Observateur réseau de Azure

Capture de paquet variable de l’Observateur réseau vous permet de toocreate paquet capture sessions tootrack trafic tooand à partir d’un ordinateur virtuel. Capture des paquets permet les anomalies de réseau toodiagnose réactive et proactivity. Autres utilisations incluent la collecte des statistiques de réseau, obtenir des informations sur les intrusions, toodebug client-serveur de communications et bien plus encore.

La capture de paquets est une extension de machine virtuelle qui est démarrée à distance par le biais de Network Watcher. Cette fonctionnalité facilite la charge hello de l’exécution d’une capture de paquets manuellement sur l’ordinateur virtuel hello souhaité, ce qui permet de gagner du temps. Capture de paquets peut être déclenchée via le portail de hello, PowerShell, CLI ou API REST. Les alertes de machine virtuelle constituent un exemple de mode de déclenchement de la capture de paquets. Les filtres sont fournies pour tooensure de session de capture hello vous capturez le trafic que vous souhaitez toomonitor. Ces filtres reposent sur des informations à 5 tuples (protocole, adresse IP locale, adresse IP distante, port local et port distant). les données de Hello capturée sont stockées dans le disque local de hello ou un objet blob de stockage. Il existe une limite de 10 sessions de capture de paquets par région par abonnement. Cette limite s’applique uniquement les sessions toohello et ne s’applique pas toohello enregistré les fichiers de capture de paquet localement sur hello machine virtuelle ou dans un compte de stockage.

> [!IMPORTANT]
> La capture de paquets requiert une extension de machine virtuelle `AzureNetworkWatcherExtension`. Pour installer l’extension de hello sur une machine virtuelle Windows, visitez [extension de machine virtuelle d’Agent de l’Observateur réseau Azure pour Windows](../virtual-machines/windows/extensions-nwa.md) et de, visitez Linux VM [extension de machine virtuelle Azure réseau Observateur Agent pour Linux](../virtual-machines/linux/extensions-nwa.md).

informations de hello tooreduce vous capturez des informations de hello tooonly souhaité, hello options suivantes sont disponibles pour une session de capture de paquet :

**Configuration de la capture**

|Propriété|Description|
|---|---|
|**Nombre maximal d’octets par paquet (octets)** | Hello du nombre d’octets à partir de chaque paquet sont capturées, tous les octets sont capturées, si ce champ est vide. Hello du nombre d’octets à partir de chaque paquet sont capturées, tous les octets sont capturées, si ce champ est vide. Si vous avez besoin d’en-tête IPv4 uniquement hello indiquer 34 ici |
|**Nombre maximal d’octets par session (octets)** | Nombre total d’octets qui est capturée, une fois la valeur de hello atteinte hello session se termine.|
|**Délai imparti (secondes)** | Définit une contrainte de temps sur les paquets hello capturer la session. valeur par défaut de Hello est 18000 secondes ou 5 heures.|

**Filtrage (facultatif)**

|Propriété|Description|
|---|---|
|**Protocole** | toofilter de protocole Hello pour les paquets hello capturer. les valeurs disponibles Hello sont TCP, UDP et toutes.|
|**Adresse IP locale** | Cette valeur filtre toopackets de capture de paquets hello où l’adresse IP locale hello correspond à cette valeur de filtre.|
|**Port local** | Cette valeur filtres hello paquet capture toopackets où port local de hello correspond à cette valeur de filtre.|
|**Adresse IP distante** | Cette valeur filtres hello paquet capture toopackets où adresse IP distante de hello correspond à cette valeur de filtre.|
|**Port distant** | Cette valeur filtres hello paquet capture toopackets où port distant de hello correspond à cette valeur de filtre.|

### <a name="next-steps"></a>Étapes suivantes

Découvrez comment vous pouvez gérer des captures de paquets via le portail de hello en vous rendant sur [gérer la capture des paquets Bonjour Azure portal](network-watcher-packet-capture-manage-portal.md) ou avec PowerShell en vous rendant sur [gérer la Capture de paquet avec PowerShell](network-watcher-packet-capture-manage-powershell.md).

Découvrez comment les captures de paquets de proactive toocreate basés sur des alertes de l’ordinateur virtuel en vous rendant sur [créer une capture de paquets déclenchées alerte](network-watcher-alert-triggered-packet-capture.md)

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













