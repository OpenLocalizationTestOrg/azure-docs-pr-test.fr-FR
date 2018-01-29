---
title: "Protection de votre réseau dans Azure Security Center | Microsoft Docs"
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
ms.openlocfilehash: 00b715507a7c3a4d784b800e7bf0c700f6ea6ff1
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a>Protection de votre réseau dans Azure Security Center
Le Centre de sécurité Azure analyse l’état de sécurité de vos ressources Azure. Lorsque Security Center identifie des failles de sécurité potentielles, il crée des recommandations qui vous guident tout au long du processus de configuration des contrôles nécessaires.  Ces recommandations s’appliquent aux types de ressources Azure : machines virtuelles, mise en réseau, applications et SQL.

Cet article traite des recommandations qui s’appliquent à votre réseau.  Les recommandations relatives au réseau se concentrent autour des pare-feu nouvelle génération, des groupes de sécurité réseau, de la configuration des règles de trafic entrant, et bien plus encore.  Utilisez le tableau ci-dessous pour mieux comprendre les recommandations disponibles pour le réseau et leurs effets.

## <a name="available-network-recommendations"></a>Recommandations disponibles pour le réseau
| Recommandation | Description |
| --- | --- |
| [Ajouter un pare-feu de nouvelle génération](security-center-add-next-generation-firewall.md) |Recommande l’ajout d’un pare-feu de nouvelle génération d’un partenaire Microsoft afin de renforcer vos protections de sécurité. |
| [Acheminer le trafic uniquement via un pare-feu de nouvelle génération](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |Recommande la configuration de règles de groupe de sécurité réseau qui forcent le trafic entrant de votre machine virtuelle via votre pare-feu de nouvelle génération. |
| [Activer des groupes de sécurité réseau sur les sous-réseaux et ou les machines virtuelles](security-center-enable-network-security-groups.md) |Recommande l’activation des groupes de sécurité réseau sur les sous-réseaux ou les machines virtuelles. |
| [Restreindre l’accès via un point de terminaison accessible sur Internet](security-center-restrict-access-through-internet-facing-endpoints.md) |Recommande la configuration de règles de trafic entrant pour les groupes de sécurité réseau. |

## <a name="see-also"></a>Voir aussi
Pour en savoir plus sur les recommandations qui s’appliquent à d’autres types de ressources Azure, consultez les rubriques suivantes :

* [Protection de vos machines virtuelles dans Azure Security Center](security-center-virtual-machine-recommendations.md)
* [Protection de vos applications dans Azure Security Center](security-center-application-recommendations.md)
* [Protection de votre service SQL Azure dans Azure Security Center](security-center-sql-service-recommendations.md)

Pour plus d’informations sur le Centre de sécurité, consultez les rubriques suivantes :

* [Définition des stratégies de sécurité dans Azure Security Center](security-center-policies.md) : découvrez comment configurer des stratégies de sécurité pour vos groupes de ressources et abonnements Azure.
* [Gestion et résolution des alertes de sécurité dans Azure Security Center](security-center-managing-and-responding-alerts.md) : découvrez comment gérer et résoudre les alertes de sécurité.
* [FAQ Azure Security Center](security-center-faq.md) : forum aux questions concernant l’utilisation de ce service.
