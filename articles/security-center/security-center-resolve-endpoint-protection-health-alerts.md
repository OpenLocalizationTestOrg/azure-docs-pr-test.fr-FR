---
title: "alertes d’intégrité aaaResolve endpoint protection dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandation du centre de sécurité Azure ** alertes ** de résoudre la Protection de point de terminaison d’intégrité."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a>Résoudre les alertes d’intégrité Endpoint Protection dans le Centre de sécurité Azure
Le Centre de sécurité Azure recommande de résoudre les alertes d’intégrité Endpoint Protection.  Centre de sécurité vous permet de toosee les machines virtuelles (VM) ont des échecs de protection de point de terminaison et de combien.

> [!NOTE]
> Ce document présente le service de hello à l’aide d’un exemple de déploiement. Il ne s’agit pas d’un guide pas à pas.
> 
> 

## <a name="implement-hello-recommendation"></a>Implémenter la recommandation de hello
1. Bonjour **Panneau de recommandations**, sélectionnez **alertes d’intégrité de résoudre la Protection de point de terminaison**.
   ![Résoudre les alertes d’intégrité Endpoint Protection][1]
2. Cela ouvre le panneau de hello **Échec de la Protection de point de terminaison** qui répertorie les ordinateurs virtuels avec des échecs et nombre hello d’échecs pour chaque machine virtuelle. Sélectionnez une machine virtuelle à partir de la liste de hello.
   ![Endpoint protection failure][2]
3. A **échecs liste** panneau s’affiche pour hello sélectionné la machine virtuelle, affiche la liste des échecs. Sélectionnez un échec dans toolearn de liste hello plus. Un panneau s’ouvre avec les informations sur les échecs de hello sélectionné.
   ![Liste des échecs][3]
   ![Événement d’échec][4]

## <a name="see-also"></a>Voir aussi
toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md)--Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md): découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md)--Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md)--Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Forum aux questions sur Azure Security Center](security-center-faq.md)--rechercher Forum aux questions sur l’utilisation du service de hello.
* [Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/)--obtenir les dernières informations de sécurité Azure hello et informations.

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
