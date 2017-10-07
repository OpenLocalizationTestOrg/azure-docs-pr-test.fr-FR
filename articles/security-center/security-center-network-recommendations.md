---
title: "aaaProtecting votre réseau dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document traite des recommandations d’Azure Security Center qui peuvent vous aider à protéger votre réseau Azure et à rester en conformité avec les stratégies de sécurité."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a>Protection de votre réseau dans Azure Security Center
Centre de sécurité Azure analyse l’état de la sécurité de vos ressources Azure hello. Lorsque le centre de sécurité identifie les éventuelles failles de sécurité, il crée des recommandations qui vous guident tout au long des processus de hello de configuration de contrôles de hello nécessité.  Recommandations s’appliquent à des types de ressources tooAzure : machines virtuelles (VM), mise en réseau, SQL et les applications.

Cet article traite des recommandations qui s’appliquent tooyour réseau.  Les recommandations relatives au réseau se concentrent autour des pare-feu nouvelle génération, des groupes de sécurité réseau, de la configuration des règles de trafic entrant, et bien plus encore.  Tableau hello ci-dessous comme un toohelp de référence que vous comprenez les recommandations de réseau disponible hello et ce que fait chacun d’eux si vous l’appliquez.

## <a name="available-network-recommendations"></a>Recommandations disponibles pour le réseau
| Recommandation | Description |
| --- | --- |
| [Ajouter un pare-feu de nouvelle génération](security-center-add-next-generation-firewall.md) |Recommande d’ajouter un pare-feu de la génération suivante (Conviction) à partir d’un tooincrease de partenaire Microsoft votre protections de sécurité. |
| [Acheminer le trafic uniquement via un pare-feu de nouvelle génération](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |Recommande de configurer les règles de groupe (NSG) de sécurité réseau qui force le trafic entrant tooyour machine virtuelle via votre Conviction. |
| [Activer des groupes de sécurité réseau sur les sous-réseaux et ou les machines virtuelles](security-center-enable-network-security-groups.md) |Recommande l’activation des groupes de sécurité réseau sur les sous-réseaux ou les machines virtuelles. |
| [Restreindre l’accès via un point de terminaison accessible sur Internet](security-center-restrict-access-through-internet-facing-endpoints.md) |Recommande la configuration de règles de trafic entrant pour les groupes de sécurité réseau. |

## <a name="see-also"></a>Voir aussi
toolearn en savoir plus sur les recommandations qui s’appliquent les types de ressources Azure tooother, voir hello :

* [Protection de vos machines virtuelles dans Azure Security Center](security-center-virtual-machine-recommendations.md)
* [Protection de vos applications dans Azure Security Center](security-center-application-recommendations.md)
* [Protection de votre service SQL Azure dans Azure Security Center](security-center-sql-service-recommendations.md)

toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.
