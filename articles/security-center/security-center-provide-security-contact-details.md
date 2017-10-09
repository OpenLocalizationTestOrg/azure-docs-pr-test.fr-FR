---
title: "aaaProvide les détails de contact de sécurité dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooprovide sécurité coordonnées dans le centre de sécurité Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 6c378c9c84c6e4fce70b2541e4cc121018700269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a>Fournir les détails du contact de sécurité dans Azure Security Center
Azure Security Center vous recommande de fournir les détails du contact de sécurité pour votre abonnement Azure, si vous ne l’avez pas déjà fait. Ces informations seront être utilisées par Microsoft toocontact si hello MSRC Microsoft Security Response Center () détecte que votre client a accédé aux données par un tiers illégal ou non autorisé. MSRC réalise une surveillance de hello réseau Azure et l’infrastructure sélectionnez sécurité et reçoit des réclamations intelligence et abus de menace de tiers.

Une notification par courrier électronique est envoyée sur hello première quotidienne d’une alerte et uniquement pour les alertes de gravité élevée. Les préférences de courrier électronique peuvent uniquement être configurées pour les stratégies d’abonnement. Les groupes de ressources d’un abonnement hériteront de ces paramètres.

> [!NOTE]
> Ce document présente le service de hello à l’aide d’un exemple de déploiement.  Il ne s’agit pas d’un guide pas à pas.
>
>

## <a name="implement-hello-recommendation"></a>Implémenter la recommandation de hello
1. Bonjour **recommandations** panneau, sélectionnez **fournissent des détails de contact de sécurité**.
   ![Fournir le contact de sécurité][1]
2. Cela ouvre le panneau de hello **fournissent des détails de contact de sécurité**. Sélectionnez les informations de contact tooprovide abonnement Azure hello sur.
   ![Fournir des informations de contact de sécurité][2]
3. Un second panneau **Fournissez les détails du contact de sécurité** s’ouvre.

   * Entrez l’adresse de messagerie du contact de sécurité hello ou séparés par des virgules des adresses. Il n’est pas un toohello limiter le nombre d’adresses de messagerie que vous pouvez entrer.
   * Entrez le numéro de téléphone international du contact de sécurité.
   * des messages électroniques tooreceive sur les alertes de gravité élevée, activez hello option **m’envoyer des e-mails sur les alertes**.
   * Bonjour futures, vous aurez propriétaires toosubscription des notifications de messagerie hello option toosend. Cette option est actuellement grisée.
   * Sélectionnez **OK** sécurité de hello tooapply contactez tooyour abonnement.

## <a name="see-also"></a>Voir aussi
toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) --Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.
* [Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) --obtenir les dernières informations de sécurité Azure hello et informations.

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
