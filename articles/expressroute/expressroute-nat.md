---
title: exigences aaaNAT pour les circuits ExpressRoute | Documents Microsoft
description: "Cette page détaille les conditions nécessaires à la configuration et à la gestion des NAT pour les circuits ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 867bf936-c851-485f-84c8-d8d6e33fee9f
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 09a0e841235de3f6b85e32172d7f99f20b5baf54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-nat-requirements"></a>Configuration NAT requise pour ExpressRoute
services de cloud computing tooMicrosoft tooconnect à l’aide d’ExpressRoute, vous avez besoin tooset et gérer des périphériques NAT. Certains fournisseurs de connectivité proposent la configuration et la gestion NAT comme un service géré. Vérifiez auprès de votre toosee de fournisseur de connectivité s’ils offrent un tel service. Si ce n’est pas le cas, vous devez respecter les exigences de toohello décrites ci-dessous. 

Hello de révision [ExpressRoute circuits et domaines de routage](expressroute-circuit-peerings.md) page tooget une vue d’ensemble de hello différents domaines de routage. toomeet hello publique matière d’adresses IP pour Azure public et d’homologation Microsoft, nous vous recommandons de configurer NAT entre votre réseau et de Microsoft. Cette section fournit une description détaillée de l’infrastructure NAT hello que vous avez besoin tooset.

## <a name="nat-requirements-for-azure-public-peering"></a>Configuration NAT requise pour l'homologation publique Azure
Hello chemin d’accès d’homologation publique Azure permet de vous tooconnect tooall services hébergés dans Azure sur les adresses IP publiques. Notamment les services répertoriés dans hello [ExpessRoute FAQ](expressroute-faqs.md) et tous les services hébergés par les éditeurs de logiciels indépendants sur Microsoft Azure. 

> [!IMPORTANT]
> Connectivité tooMicrosoft Azure services publics d’homologation est toujours lancée à partir de votre réseau dans le réseau de Microsoft hello. Par conséquent, les sessions ne peuvent pas être lancées à partir du réseau de tooyour de services Microsoft Azure via ExpressRoute. Dans ce cas, toothese de paquets envoyés publiés IPs utilisera hello internet au lieu de ExpressRoute.
> 

Le trafic destiné tooMicrosoft Azure sur l’homologation publique doit être toovalid SNATed qu'avant leur entrée hello Microsoft réseau les adresses IPv4 publiques. figure Hello ci-dessous fournit une image de haut niveau de comment hello NAT peut être configurée hello toomeet au-dessus de spécification.

![](./media/expressroute-nat/expressroute-nat-azure-public.png) 

### <a name="nat-ip-pool-and-route-advertisements"></a>Pool d’adresses IP NAT et publications de routage
Vous devez vous assurer que le trafic est entrant hello Azure chemin d’accès d’homologation publique avec une adresse IPv4 publique valide. Microsoft doit être en mesure de toovalidate la propriété de hello Hello pool d’adresses IPv4 NAT par rapport à un Registre routage Internet régional (RIR) ou d’un routage (tri). Une vérification sera effectuée en fonction de hello comme nombre en cours homologué avec et hello des adresses IP utilisées pour hello NAT. Consultez toohello [conditions de routage ExpressRoute](expressroute-routing.md) page pour plus d’informations sur les registres de routage.

Il n’existe aucune restriction de longueur de hello de préfixe IP NAT de hello publié via cette homologation. Vous devez surveiller un pool NAT hello et vous assurer que vous ne manque pas de sessions NAT.

> [!IMPORTANT]
> Hello pool NAT IP publiés tooMicrosoft ne doit pas être publié toohello Internet. Cette opération rompt les services de connectivité de Microsoft tooother.
> 
> 

## <a name="nat-requirements-for-microsoft-peering"></a>Configuration NAT requise pour l'homologation Microsoft
chemin d’accès d’homologation de Hello Microsoft vous permet de connecter des services de cloud computing tooMicrosoft qui ne sont pas pris en charge via hello chemin d’accès d’homologation publique Azure. liste Hello des services inclut les services Office 365, telles que Exchange Online, SharePoint Online, Skype entreprise et Dynamics 365. Microsoft attend toosupport une connectivité bidirectionnelle sur l’homologation, Microsoft hello. Services de cloud computing de trafic à destination tooMicrosoft doivent être toovalid SNATed qu'avant leur entrée hello Microsoft réseau les adresses IPv4 publiques. Réseau de tooyour le trafic destiné à partir des services de cloud de Microsoft doit être SNATed à votre tooprevent de bord Internet [routage asymétrique](expressroute-asymmetric-routing.md). figure Hello ci-dessous fournit une image de haut niveau de comment hello NAT doit être le programme d’installation pour l’homologation de Microsoft.

![](./media/expressroute-nat/expressroute-nat-microsoft.png) 

### <a name="traffic-originating-from-your-network-destined-toomicrosoft"></a>Trafic en provenance de votre réseau à destination de tooMicrosoft
* Vous devez vous assurer que le trafic est entrant de chemin d’accès d’homologation hello Microsoft avec une adresse IPv4 publique valide. Microsoft doit être propriétaire de hello toovalidate en mesure de hello pool d’adresses IPv4 NAT sur hello régionaux routage internet du Registre (RIR) ou d’un routage (tri). Une vérification sera effectuée en fonction de hello comme nombre en cours homologué avec et hello des adresses IP utilisées pour hello NAT. Consultez toohello [conditions de routage ExpressRoute](expressroute-routing.md) page pour plus d’informations sur les registres de routage.
* Adresses IP utilisées pour hello Azure public d’homologation le programme d’installation et les autres circuits ExpressRoute ne doivent pas être publié tooMicrosoft via la session BGP de hello. Il n’existe aucune restriction de longueur de hello de préfixe IP NAT de hello publié via cette homologation.
  
  > [!IMPORTANT]
  > Hello pool NAT IP publiés tooMicrosoft ne doit pas être publié toohello Internet. Cette opération rompt les services de connectivité de Microsoft tooother.
  > 
  > 

### <a name="traffic-originating-from-microsoft-destined-tooyour-network"></a>Le trafic en provenance Microsoft destinés à tooyour réseau
* Certains scénarios nécessitent Microsoft tooinitiate connectivité tooservice points de terminaison hébergés au sein de votre réseau. Un exemple typique d’un scénario de hello serait serveurs tooADFS de connectivité hébergés dans votre réseau à partir d’Office 365. Dans ce cas, vous devez entraîner une fuite de préfixes appropriés à partir de votre réseau dans l’homologation de Microsoft hello. 
* Vous devez le trafic de SNAT Microsoft au hello Internet edge pour les points de terminaison de service au sein de votre réseau tooprevent [routage asymétrique](expressroute-asymmetric-routing.md). Les requêtes et **réponses** avec une adresse IP de destination correspondant à un itinéraire reçu via ExpressRoute est toujours envoyé via ExpressRoute. Routage asymétrique existe si la demande de hello est reçu via hello Internet avec hello réponse envoyée via ExpressRoute. SNATing hello Microsoft le trafic entrant à hello Internet edge force toohello arrière de réponse le trafic Internet edge, hello problème résolu.

![Routage asymétrique avec ExpressRoute](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="next-steps"></a>Étapes suivantes
* Consultez Configuration requise de toohello pour [routage](expressroute-routing.md) et [QoS](expressroute-qos.md).
* Pour plus d’informations sur les workflows, consultez [Workflows d’approvisionnement du circuit ExpressRoute et états du circuit](expressroute-workflows.md).
* Configurez votre connexion ExpressRoute.
  
  * [Création d’un circuit ExpressRoute](expressroute-howto-circuit-classic.md)
  * [Configuration du routage](expressroute-howto-routing-classic.md)
  * [Lier un circuit ExpressRoute de tooan réseau virtuel](expressroute-howto-linkvnet-classic.md)

