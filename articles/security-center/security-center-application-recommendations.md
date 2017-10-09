---
title: "aaaProtecting vos applications dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document traite des recommandations d’Azure Security Center qui peuvent vous aider à protéger vos applications Azure et à rester en conformité avec les stratégies de sécurité."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: b5fc7a9e-24b1-415f-b3b5-62a53f5dd424
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: terrylan
ms.openlocfilehash: da5e02cc2bad55c64e4da14e4e10efd6ddeab39e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-applications-in-azure-security-center"></a>Protection de vos applications dans Azure Security Center
Centre de sécurité Azure analyse l’état de la sécurité de vos ressources Azure hello. Lorsque le centre de sécurité identifie les éventuelles failles de sécurité, il crée des recommandations qui vous guident tout au long des processus de hello de configuration de contrôles de hello nécessité.  Recommandations s’appliquent à des types de ressources tooAzure : machines virtuelles (VM), mise en réseau, SQL et les applications.

Cet article traite des recommandations qui s’appliquent tooapplications.  Les recommandations relatives aux applications se concentrent autour du déploiement d’un pare-feu d’applications web.  Tableau hello ci-dessous comme une référence de toohelp comprendre des recommandations hello disponible et ce que fait chacun d’eux si vous l’appliquez.

## <a name="available-application-recommendations"></a>Recommandations disponibles pour les applications
| Recommandation | Description |
| --- | --- |
| [Ajouter un pare-feu d’applications web](security-center-add-web-application-firewall.md) |Recommande le déploiement d’un pare-feu d’applications web (WAF) pour les points de terminaison web. Une recommandation WAF est indiquée pour n’importe quelle IP publique (adresse IP de niveau d’instance ou adresse IP à équilibrage de charge) ayant un groupe de sécurité réseau associé avec des ports web entrants ouverts (80, 443).</br></br>Centre de sécurité vous recommande de que configurer un toohelp WAF vous défendre contre des attaques ciblant vos applications web sur des ordinateurs virtuels et sur l’environnement App Service. Un environnement App Service (ASE) est une option de plan de service [Premium](https://azure.microsoft.com/pricing/details/app-service/) d'Azure App Service qui fournit un environnement totalement isolé et dédié pour l'exécution sécurisée de vos applications Azure App Service. toolearn en savoir plus sur ASE, consultez hello [Documentation d’environnement App Service](../app-service/app-service-app-service-environments-readme.md).</br></br>Vous pouvez protéger plusieurs applications web dans le centre de sécurité en ajoutant ces applications tooyour WAF les déploiements existants. |
| [Finaliser la protection des applications](security-center-add-web-application-firewall.md#finalize-application-protection) |configuration hello toocomplete un WAF, le trafic doit être toohello reroutage de remise WAF appliance. Respect de cette recommandation termine les modifications de configuration nécessaires hello. |

## <a name="see-also"></a>Voir aussi
toolearn en savoir plus sur les recommandations qui s’appliquent les types de ressources Azure tooother, voir hello :

* [Protection de vos machines virtuelles dans Azure Security Center](security-center-virtual-machine-recommendations.md)
* [Protection de votre réseau dans Azure Security Center](security-center-network-recommendations.md)
* [Protection de votre service SQL Azure dans Azure Security Center](security-center-sql-service-recommendations.md)

toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.
