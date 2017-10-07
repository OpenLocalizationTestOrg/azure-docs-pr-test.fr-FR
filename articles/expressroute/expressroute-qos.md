---
title: "conditions préalables pour ExpressRoute d’aaaQoS | Documents Microsoft"
description: "Cette page fournit des informations détaillées sur la configuration et la gestion de QoS pour des circuits ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a>Configuration requise pour ExpressRoute QoS
Skype Entreprise a différentes charges de travail nécessitant un traitement QoS différencié. Si vous envisagez de services de téléphonie tooconsume via ExpressRoute, vous devez respecter les exigences de toohello décrites ci-dessous.

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> Exigences de qualité de service s’appliquent toohello Microsoft d’homologation uniquement. les valeurs DSCP Hello dans votre trafic réseau reçu sur l’homologation publique Azure et de l’homologation privée Azure sera too0 de réinitialisation. 
> 
> 

Hello tableau suivant fournit une liste des marquages de DSCP utilisé par Skype pour entreprises. Consultez trop[la gestion de la qualité de service pour Skype pour entreprises](https://technet.microsoft.com/library/gg405409.aspx) pour plus d’informations.

| **Classe de trafic** | **Traitement (marquage DSCP)** | **Skype for Business Workloads** |
| --- | --- | --- |
| **Voice** |EF (46) |Skype / Lync voice |
| **Interactive** |AF41 (34) |Vidéo, VBSS |
| AF21 (18) |Partage d’application | |
| **Par défaut** |AF11 (10) |Transfert de fichiers |
| CS0 (0) |Tout autre élément | |

* Vous devez classer les charges de travail hello et marquer les valeurs DSCP hello. Suivez les instructions de hello fournies [ici](https://technet.microsoft.com/library/gg405409.aspx) sur la façon de marquages de DSCP tooset dans votre réseau.
* Vous devez configurer et prendre en charge plusieurs files d’attente QoS au sein de votre réseau. Voix doit être une classe autonome et reçoivent un traitement EF de hello spécifié dans la RFC 3246. 
* Vous pouvez décider hello queuing mécanisme, la stratégie de détection de congestion et allocation de bande passante par la classe de trafic. Toutefois, hello marquage DSCP pour Skype pour les charges de travail métier doit être conservé. Si vous utilisez des marquages de DSCP non répertoriées ci-dessus, par exemple, AF31 (26), vous devez réécrire cette too0 de valeur DSCP avant d’envoyer tooMicrosoft de paquets hello. Microsoft envoie uniquement les paquets marqués avec hello valeur DSCP hello au-dessus de table. 

## <a name="next-steps"></a>Étapes suivantes
* Consultez Configuration requise de toohello pour [routage](expressroute-routing.md) et [NAT](expressroute-nat.md).
* Voir les liens suivants de hello de tooconfigure de votre connexion ExpressRoute.
  
  * [Création d’un circuit ExpressRoute](expressroute-howto-circuit-classic.md)
  * [Configuration du routage](expressroute-howto-routing-classic.md)
  * [Lier un circuit ExpressRoute de tooan réseau virtuel](expressroute-howto-linkvnet-classic.md)

