---
title: "solutions de partenaire aaaManaging dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous guide tout au long de comment Azure Security Center vous permet de vous moniteur dans un état d’intégrité hello aperçu de vos solutions de partenaire intégré à votre abonnement Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a>Surveillance des solutions de partenaire avec le Centre de sécurité Azure
Ce document vous guide tout au long de la toomonitor hello état d’intégrité de vos solutions de partenaire dans le centre de sécurité Azure.

> [!NOTE]
> Ce document présente le service de hello à l’aide d’un exemple de déploiement. Ce document n'est pas un guide pas à pas.
>
>

## <a name="monitoring-partner-solutions"></a>Surveillance des solutions de partenaire
Hello **solutions de partenaire** vignette sur hello **centre de sécurité** panneau vous permet de contrôler dans un état d’intégrité hello aperçu de vos solutions de partenaire sont intégrées à votre abonnement Azure.

![Mosaïque Solutions de partenaire][1]

Hello **solutions de partenaire** vignette affiche le nombre hello de solutions de partenaire intégré à votre abonnement. S’il n’y a aucune solution intégrée, vignette de hello affiche le nombre de hello zéro.

contrôle d’intégrité de tooview hello de vos solutions de partenaire :

1. Sélectionnez hello **solutions de partenaire** vignette. Hello **solutions de partenaire** s’ouvre le panneau affiche la liste de vos solutions de partenaire connecté tooSecurity Center.

   ![Solutions de partenaires][3]

   état Hello d’une solution partenaire peut être :

   * Protégé (vert) : aucun problème d’intégrité.
   * Défectueux (rouge) : problème d’intégrité nécessitant une action immédiate.
   * Arrêté (orange - création de rapports) des solutions de hello se sont arrêté reporting son intégrité.
   * État de protection inconnu (orange) - intégrité hello de solution de hello est inconnu pour l’instant en raison des processus tooa échoué de l’ajout d’une solution existante de nouvelles ressources toohello.
   * Pas signalé (gris) - solution de hello n’a pas signalé quoi que ce soit encore, le statut de la solution est peut-être pas signalée si elle a récemment été connecté et est toujours déploiement.

2. Sélectionnez une solution de partenaire. Dans cet exemple, vous permet de sélectionner hello **Qualys** solution.  Un panneau s’ouvre pour afficher l’état de hello des solutions de partenaire hello et la solution hello associés aux ressources. Sélectionnez **console de la Solution** expérience de gestion des partenaires tooopen hello pour cette solution.

   ![Détail de la solution partenaire][4]
3. Revenir en arrière toohello **Qualys** panneau et sélectionnez **lien VM**. Hello **lien Applications** panneau s’ouvre. Ici, vous pouvez connecter solutions de partenaire de ressources toohello.

   ![Lien ressources toopartner solution][5]

## <a name="next-steps"></a>Étapes suivantes
Dans ce document, vous ont été introduite toohello **Solutions de partenaire** vignette dans le centre de sécurité. toolearn en savoir plus sur le centre de sécurité, consultez hello suivant des articles :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) : Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) — Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) : en savoir comment les alertes toosecurity toomanage et y répondre.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) : Forum aux questions sur l’utilisation hello service de recherche.
* [Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : obtenir les dernières informations de sécurité Azure hello et informations.

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
