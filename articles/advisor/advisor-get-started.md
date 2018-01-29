---
title: "Prise en main du conseiller Azure | Microsoft Docs"
description: Prise en main du conseiller Azure.
services: advisor
documentationcenter: NA
author: manbeenkohli
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: makohli
ms.openlocfilehash: dc89cd29e1e8038f0ff317ff6acee332218ebce7
ms.sourcegitcommit: ce934aca02072bdd2ec8d01dcbdca39134436359
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/08/2017
---
# <a name="get-started-with-azure-advisor"></a>Prise en main d’Azure Advisor

Découvrez comment accéder à Advisor à l’aide du portail Azure, obtenir des recommandations et implémenter ces dernières.

## <a name="get-advisor-recommendations"></a>Obtenir des recommandations du conseiller

1. Connectez-vous au [portail Azure](https://portal.azure.com).

2. Dans le volet gauche, cliquez sur **Advisor**.  Si vous ne voyez pas Advisor dans le volet gauche, cliquez sur **Autres services**.  Dans le volet du menu de services, sous **Surveillance et gestion**, cliquez sur **Advisor**.
 Le tableau de bord Advisor s’affiche.

   ![Accéder au conseiller Azure avec le portail Azure](./media/advisor-get-started/advisor-portal-menu.png) 

4. Le tableau de bord Advisor présente un résumé de vos recommandations pour tous les abonnements sélectionnés.  Vous pouvez choisir les abonnements pour lesquels afficher les recommandations à l’aide de la liste déroulante de filtrage des abonnements.

5. Pour obtenir des recommandations pour une catégorie spécifique, cliquez sur l’onglet **Haute disponibilité**, **Sécurité**, **Performances** ou **Coût**.
 
> [!NOTE]
> Pour utiliser Azure Advisor avec un abonnement, un *propriétaire* de cet abonnement doit lancer le tableau de bord Advisor.  Cette action enregistre l’abonnement auprès d’Advisor.  Dès lors, tout *propriétaire*, *contributeur* ou *lecteur* de l’abonnement peut accéder aux recommandations d’Advisor associées.  

  ![Tableau de bord du conseiller Azure](./media/advisor-overview/advisor-dashboard.png)

## <a name="get-advisor-recommendation-details-and-implement-a-solution"></a>Obtenir les détails de recommandation d’Advisor et implémenter une solution

Vous pouvez sélectionner une recommandation dans Advisor pour afficher des détails supplémentaires, tels que les actions de la recommandation et les ressources affectées, et pour implémenter la solution associée à la recommandation.  

1. Connectez-vous au [portail Azure](https://portal.azure.com), puis ouvrez [Advisor](https://aka.ms/azureadvisordashboard).

2. Sélectionnez une catégorie de recommandations pour afficher la liste des recommandations de cette catégorie, ou sélectionnez l’onglet **Tout** pour afficher toutes vos recommandations.

3. Cliquez sur une recommandation que vous souhaitez examiner en détail.

4. Prenez connaissance des informations relatives à la recommandation et aux ressources auxquelles celle-ci s’applique.

5. Cliquez sur **Action recommandée** pour implémenter la recommandation.

## <a name="filter-advisor-recommendations"></a>Filtrer les recommandations d’Advisor

Vous pouvez filtrer les recommandations pour accéder aux informations qui vous intéressent le plus.  Vous pouvez filtrer par abonnement, par type de ressource ou par état de recommandation.  

1. Connectez-vous au [portail Azure](https://portal.azure.com), puis ouvrez [Advisor](https://aka.ms/azureadvisordashboard).

2.  Utilisez les menus déroulants du tableau de bord Advisor pour filtrer par abonnement, par type de ressource ou par état de recommandation.

    ![Critères de filtre de recherche d’Advisor](./media/advisor-get-started/advisor-filters.png)

## <a name="snooze-or-dismiss-advisor-recommendations"></a>Répéter ou ignorer les recommandations d’Advisor

1. Connectez-vous au [portail Azure](https://portal.azure.com), puis ouvrez [Advisor](https://aka.ms/azureadvisordashboard).

2. Accédez à la recommandation que vous souhaitez répéter ou ignorer.

3. Cliquez sur la recommandation.

4. Cliquez sur **Répéter**. 

5. Spécifiez une période de répétition ou sélectionnez **Jamais** pour faire disparaître la recommandation.

## <a name="exclude-subscriptions-or-resource-groups-from-advisor"></a>Exclure des abonnements ou des groupes de ressources d’Advisor

Il se peut que vous possédiez des groupes de ressources ou des abonnements pour lesquels vous ne souhaitez pas recevoir de recommandations d’Advisor, tels que les ressources de « test ».  Vous pouvez configurer Advisor de manière à générer des recommandations uniquement pour des abonnements et des groupes de ressources spécifiques.

> [!NOTE]
> Pour inclure un abonnement ou un groupe de ressources dans Advisor ou l’en exclure, vous devez être propriétaire de cet abonnement ou de ce groupe de ressources.  Si vous ne disposez pas des autorisations requises pour un abonnement ou un groupe de ressources, l’option permettant de l’inclure ou de l’exclure est désactivée dans l’interface utilisateur.

1. Connectez-vous au [portail Azure](https://portal.azure.com), puis ouvrez [Advisor](https://aka.ms/azureadvisordashboard).

2. Dans la barre d’action, cliquez sur **Configurer**.

3. Désactivez les abonnements ou les groupes de ressources pour lesquels vous ne souhaitez pas recevoir de recommandations d’Advisor.

    ![Exemple de configuration de ressources dans Advisor](./media/advisor-get-started/advisor-configure-resources.png)

4. Cliquez sur le bouton **Appliquer**.

## <a name="configure-the-average-cpu-utilization-rule-for-the-low-usage-virtual-machine-recommendation"></a>Configurer la règle d’utilisation moyenne du processeur pour la recommandation en cas de faible utilisation de machines virtuelles

Advisor surveille l’utilisation de votre machine virtuelle pendant 14 jours et identifie les machines virtuelles faiblement utilisées. Les machines virtuelles pour lesquelles l’utilisation moyenne du processeur est inférieure ou égale à 5 % et l’utilisation du réseau est inférieure ou égale à 7 Mo pendant quatre jours ou plus sont considérées comme des machines virtuelles faiblement utilisées.

Si vous souhaitez être plus « agressif » dans l’identification des machines virtuelles faiblement utilisées, vous pouvez ajuster la règle d’utilisation moyenne du processeur par abonnement.  La règle d’utilisation moyenne du processeur peut être définie sur 5 %, 10 %, 15 % ou 20 %.

> [!NOTE]
> Pour ajuster la règle d’utilisation moyenne du processeur aux fins d’identification des machines virtuelles faiblement utilisées, vous devez être *propriétaire* de l’abonnement.  Si vous ne disposez pas des autorisations requises pour un abonnement ou un groupe de ressources, l’option permettant de l’inclure ou de l’exclure est désactivée dans l’interface utilisateur. 

1. Connectez-vous au [portail Azure](https://portal.azure.com), puis ouvrez [Advisor](https://aka.ms/azureadvisordashboard).

2. Dans la barre d’action, cliquez sur **Configurer**.

3. Cliquez sur l’onglet **Règles**.

4. Sélectionnez les abonnements pour lesquels vous voulez ajuster la règle d’utilisation moyenne du processeur, puis cliquez sur **Modifier**.

5. Sélectionnez la valeur d’utilisation moyenne du processeur souhaitée, puis cliquez sur **Appliquer**.

6. Cliquez sur **Actualiser les recommandations** pour mettre à jour vos recommandations existantes avec la nouvelle règle d’utilisation moyenne du processeur. 

   ![Exemple de configuration de règles de recommandation dans Advisor](./media/advisor-get-started/advisor-configure-rules.png)

## <a name="download-your-advisor-recommendations"></a>Télécharger les recommandations d’Advisor

Advisor permet de télécharger un résumé de vos recommandations.  Vous pouvez télécharger vos recommandations sous forme de fichier PDF ou CSV.  En téléchargeant vos recommandations, vous pourrez facilement les partager avec des collègues ou effectuer votre propre analyse sur les données de recommandation.

1. Connectez-vous au [portail Azure](https://portal.azure.com), puis ouvrez [Advisor](https://aka.ms/azureadvisordashboard).

2. Dans la barre d’action, cliquez sur **Télécharger au format CSV** ou **Télécharger au format PDF**.

L’option de téléchargement conserve les filtres que vous avez appliqués au tableau de bord Advisor.  Si vous sélectionnez l’option de téléchargement alors qu’une catégorie de recommandations ou une recommandation spécifique est affichée, le résumé téléchargé inclut uniquement les informations de cette catégorie ou de cette recommandation. 

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur Advisor, consultez les ressources suivantes :
* [Présentation du conseiller Azure](advisor-overview.md)
* [Recommandations du conseiller en matière de haute disponibilité](advisor-high-availability-recommendations.md)
* [Recommandations du conseiller en matière de sécurité](advisor-security-recommendations.md)
-  [Recommandations du conseiller en matière de performances](advisor-performance-recommendations.md)
* [Recommandations du conseiller en matière de coûts](advisor-performance-recommendations.md)
