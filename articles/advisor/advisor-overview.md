---
title: aaaIntroduction tooAzure Advisor | Documents Microsoft
description: "Utilisez l’Assistant Azure toooptimize vos déploiements Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 5d796fc06366221efdb6f1bda39ab3fb676abfd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-advisor"></a>Introduction tooAzure Advisor

En savoir plus sur le Conseiller d’Azure et de ses fonctionnalités clées et obtenir elles sonttrop des réponses aux questions.

## <a name="what-is-advisor"></a>Qu’est-ce qu’Advisor ?
Advisor est un consultant personnalisé de cloud qui vous permet de suivre les meilleures pratiques toooptimize vos déploiements Azure. Il analyse votre configuration de la ressource et la télémétrie d’utilisation et puis recommande des solutions qui peuvent vous aider à améliorent la rentabilité hello, performances, haute disponibilité et la sécurité de vos ressources Azure.

Avec Advisor, vous pouvez :
* Bénéficier de recommandations en termes de meilleures pratiques proactives, interactives et personnalisées. 
* Améliorer hello, sécurité et une haute disponibilité de vos ressources, que vous identifiez tooreduce opportunités votre Azure global passent à.
* Obtenir des recommandations avec des propositions d’actions intégrées.

Vous pouvez accéder Advisor via hello [portail Azure](https://aka.ms/azureadvisordashboard). Connectez-vous à toohello [portal](https://portal.azure.com), sélectionnez **Parcourir**, puis faites défiler trop**Azure Advisor**. tableau de bord de conseiller Hello affiche des recommandations personnalisées pour un abonnement sélectionné. 

recommandations de Hello sont divisées en quatre catégories : 

* **Haute disponibilité**: tooensure et améliorer la continuité de hello de vos applications critiques. Pour plus d’informations, consultez [Recommandations du conseiller en matière de haute disponibilité](advisor-high-availability-recommendations.md).

* **Sécurité**: toodetect menaces et vulnérabilités pouvant entraîner des failles de toosecurity. Pour plus d’informations, consultez [Recommandations du conseiller en matière de sécurité](advisor-security-recommendations.md).

* **Performances**: vitesse de hello tooimprove de vos applications. Pour plus d’informations, consultez [Recommandations du conseiller en matière de performances](advisor-performance-recommendations.md).

* **Coût**: toooptimize et réduire votre Azure globale dépenses. Pour plus d’informations, consultez [Recommandations du conseiller en matière de coût](advisor-cost-recommendations.md).

  ![Types de recommandation du conseiller](./media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> tooaccess recommandations de l’Assistant, vous devez d’abord *enregistrer votre abonnement* avec l’Assistant. Un abonnement est enregistré quand un *abonnement propriétaire* lance hello hello de tableau de bord et clique sur Advisor **obtenir des recommandations** bouton. Cette opération ne doit être *exécutée qu’une seule fois*. Une fois l’abonnement de hello est enregistré, vous pouvez accéder à des recommandations de l’Assistant en tant que *propriétaire*, *collaborateur*, ou *lecteur* pour un abonnement, un groupe de ressources, ou un ressource spécifique.

Vous pouvez cliquer sur une recommandation toolearn plus d’informations. Vous pouvez également en savoir plus sur les actions que vous pouvez effectuer parti tootake de l’opportunité ou résoudre un problème. 

Le conseiller fournit des recommandations accompagnées d’actions intégrées ou de liens vers de la documentation. En cliquant sur une action inline vous guide tout au long une tooimplement « voyage utilisateur interactive » il. En cliquant sur un lien vers la documentation vous oriente toodocumentation qui explique comment implémenter l’action de hello toomanually. 

Advisor met à jour les recommandations toutes les heures. Si vous n’envisagez pas une action immédiate tootake sur une recommandation, vous pouvez le répéter pour une période de temps ou la faire disparaître. 

## <a name="frequently-asked-questions"></a>Forum Aux Questions

### <a name="how-do-i-access-advisor"></a>Accès au conseiller
Vous pouvez accéder Advisor via hello [portail Azure](https://aka.ms/azureadvisordashboard). Connectez-vous à toohello [portal](https://portal.azure.com), sélectionnez **Parcourir**, puis faites défiler trop**Azure Advisor**. tableau de bord de conseiller Hello affiche des recommandations personnalisées pour un abonnement sélectionné. 

Vous pouvez également afficher les recommandations de l’Assistant via le panneau des ressources hello machine virtuelle. Choisissez un ordinateur virtuel, puis faites défiler les recommandations tooAdvisor dans le menu de hello. 

### <a name="what-permissions-do-i-need-tooaccess-advisor"></a>Que faire autorisations ai-je besoin tooaccess Advisor ?

tooaccess recommandations de l’Assistant, vous devez d’abord *enregistrer votre abonnement* avec l’Assistant. Un abonnement est enregistré quand un *abonnement propriétaire* lance hello hello de tableau de bord et clique sur Advisor **obtenir des recommandations** bouton. Cette opération ne doit être *exécutée qu’une seule fois*. Une fois l’abonnement de hello est enregistré, vous pouvez accéder à des recommandations de l’Assistant en tant que *propriétaire*, *collaborateur*, ou *lecteur* pour un abonnement, un groupe de ressources, ou un ressource spécifique.

### <a name="how-often-are-advisor-recommendations-updated"></a>A quelle fréquence les recommandations du conseiller sont-elles mises à jour ?

Les recommandations d’Advisor sont mises à jour toutes les heures.

### <a name="what-resources-does-advisor-provide-recommendations-for"></a>Pour quelles ressources le conseiller fournit-il des recommandations ?

Advisor fournit des recommandations pour les machines virtuelles, les groupes à haute disponibilité, les passerelles d’application, App Services, les serveurs SQL, les bases de données SQL et le Cache Redis.

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a>Puis-je répéter ou ignorer une recommandation ?

toosnooze ou ignorer une recommandation, cliquez sur hello **répéter** bouton ou lien. Vous pouvez spécifier une heure de période ou sélectionnez **jamais** toodismiss hello recommandation.

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur les recommandations de l’Assistant, consultez :

* [Prise en main du conseiller](advisor-get-started.md)
* [Recommandations du conseiller en matière de haute disponibilité](advisor-high-availability-recommendations.md)
* [Recommandations du conseiller en matière de sécurité](advisor-security-recommendations.md)
* [Recommandations du conseiller en matière de performances](advisor-performance-recommendations.md)
* [Recommandations du conseiller en matière de coûts](advisor-cost-recommendations.md)
