---
title: "aaaPrerequisites pour l’adoption d’Azure ExpressRoute | Documents Microsoft"
description: "Cette page fournit une liste de toobe conditions remplie avant que vous pouvez commander un circuit ExpressRoute d’Azure."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: f872d25e-acfd-405d-9d1b-dcb9f323a2ff
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/30/2017
ms.author: cherylmc
ms.openlocfilehash: 524c86f6570dc6e6505fe55323b8508e8eeff791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-prerequisites--checklist"></a>Configuration requise pour ExpressRoute et liste de contrôle
cloud de tooMicrosoft tooconnect services à l’aide d’ExpressRoute, vous devez tooverify que hello suivant les exigences répertoriées dans les sections suivantes de hello ont été remplies.

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

## <a name="azure-account"></a>Compte Azure
* Un compte Microsoft Azure actif et valide. Ce compte est requis tooset des hello circuit ExpressRoute. Les circuits ExpressRoute sont des ressources au sein des abonnements Azure. Un abonnement Azure est une exigence, même si la connexion est limitée toonon-Azure Microsoft cloud services, tels que les services Office 365 et Dynamics 365.
* Un abonnement Office 365 actif (si vous utilisez les services Office 365). Pour plus d’informations, consultez hello [conditions spécifiques d’Office 365](#office-365-specific-requirements) section de cet article.

## <a name="connectivity-provider"></a>Fournisseur de connectivité

* Vous pouvez travailler avec un [partenaire de connectivité ExpressRoute](expressroute-locations.md#partners) tooconnect toohello cloud de Microsoft. Vous pouvez établir une connexion entre votre réseau local et Microsoft de [trois façons différentes](expressroute-introduction.md).
* Si votre fournisseur n’est pas un partenaire de connectivité ExpressRoute, vous pouvez toujours vous connecter toohello Microsoft cloud via une [fournisseur de cloud exchange](expressroute-locations.md#connectivity-through-exchange-providers).

## <a name="network-requirements"></a>Configuration requise pour le réseau
* **Connectivité redondante**: il n’est pas nécessaire d’assurer la redondance de la connectivité physique entre vous et votre fournisseur. Microsoft n’exige pas redondant toobe de sessions BGP configurée entre des routeurs de Microsoft et les routeurs d’homologation de hello, même lorsque vous avez simplement [une connexion physique tooa cloud exchange](expressroute-faqs.md#onep2plink).
* **Routage**: selon la façon dont vous vous connectez toohello Cloud Microsoft, vous ou votre fournisseur doit tooset des et gère les sessions BGP hello pour [les domaines de routage](expressroute-circuit-peerings.md). Certains fournisseurs de connectivité Ethernet ou fournisseurs d’échange de Cloud peuvent proposer la gestion BGP en tant que service à valeur ajoutée.
* **Traduction d’adresses réseau (NAT)**: Microsoft accepte uniquement les adresses IP publiques par le biais de l’homologation Microsoft. Si vous utilisez des adresses IP privées dans votre réseau local, vous ou votre fournisseur besoin tootranslate hello privée des adresses IP des adresses IP publiques toohello [à l’aide de hello NAT](expressroute-nat.md).
* **Qualité de service (QoS)** : Skype Entreprise comprend différents services (par exemple, voix, vidéo, texte) nécessitant un traitement QoS différencié. Vous et votre fournisseur doivent suivre hello [les exigences de qualité de service](expressroute-qos.md).
* **Sécurité réseau**: envisagez [sécurité réseau](../best-practices-network-security.md) lors de la connexion toohello Microsoft Cloud via ExpressRoute.

## <a name="office-365"></a>Office 365
Si vous prévoyez ExpressRoute tooenable Office 365, passez en revue hello suivant des documents pour plus d’informations sur la configuration requise d’Office 365.

* [Vue d’ensemble d’ExpressRoute pour Office 365](https://support.office.com/en-us/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)
* [Routage avec ExpressRoute pour Office 365](https://support.office.com/en-us/article/Routing-with-ExpressRoute-for-Office-365-e1da26c6-2d39-4379-af6f-4da213218408)
* [URL et plages d’adresses IP Office 365](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
* [Planification réseau et optimisation des performances pour Office 365](https://support.office.com/en-us/article/Network-planning-and-performance-tuning-for-Office-365-e5f1228c-da3c-4654-bf16-d163daee8848)
* [Outils et calculatrices de bande passante réseau](https://support.office.com/en-us/article/Network-and-migration-planning-for-Office-365-f5ee6c33-bcd7-4b0b-b0f8-dc1d9fb8d132)
* [Intégration d’Office 365 aux environnements locaux](https://support.office.com/en-us/article/Office-365-integration-with-on-premises-environments-263faf8d-aa21-428b-aed3-2021837a4b65)
* [Vidéos de formation avancée à ExpressRoute sur Office 365](https://channel9.msdn.com/series/aer/)

## <a name="dynamics-365"></a>Dynamics 365
Si vous prévoyez tooenable Dynamics 365 sur ExpressRoute, consultez hello suivant des documents pour plus d’informations sur Dynamics 365

* [Livre blanc Dynamics 365 et ExpressRoute](http://download.microsoft.com/download/B/2/8/B2896B38-9832-417B-9836-9EF240C0A212/Microsoft%20Dynamics%20365%20and%20ExpressRoute.pdf)
* [URL](https://support.microsoft.com/kb/2655102) et [plages d’adresses IP Dynamics 365](https://support.microsoft.com/kb/2728473)

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).
* Recherchez un fournisseur de connectivité ExpressRoute. Consultez la page [Partenaires ExpressRoute et emplacements d’homologation](expressroute-locations.md).
* Consultez toorequirements pour [routage](expressroute-routing.md), [NAT](expressroute-nat.md), et [QoS](expressroute-qos.md).
* Configurez votre connexion ExpressRoute.
  * [Création d’un circuit ExpressRoute](expressroute-howto-circuit-classic.md)
  * [Configuration du routage](expressroute-howto-routing-classic.md)
  * [Lier un circuit ExpressRoute de tooan réseau virtuel](expressroute-howto-linkvnet-classic.md)
