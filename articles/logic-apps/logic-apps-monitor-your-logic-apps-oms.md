---
title: "Surveiller et comprendre les exécutions de votre application logique à l’aide d’OMS - Azure Logic Apps | Microsoft Docs"
description: "Surveillez les exécutions de votre application logique avec Log Analytics et Operations Management Suite (OMS) pour mieux les comprendre et obtenir des informations détaillées pouvant servir au débogage et au diagnostic."
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: 0e9f0ef3c87b5c0da1cc4ad16d37178c8f5c9625
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a>Surveiller et comprendre les exécutions d’une application logique avec Operations Management Suite (OMS) et Log Analytics

Pour la surveillance et l’obtention d’informations de débogage plus détaillées, vous pouvez activer Log Analytics lorsque vous créez une application logique. Log Analytics fournit des options de journalisation des diagnostics et de surveillance pour les exécutions de votre application logique via le portail Operations Management Suite (OMS). Lorsque vous ajoutez la solution Logic Apps Management à OMS, vous obtenez l’état agrégé des exécutions de votre application logique, ainsi que des informations détaillées telles que l’état, la durée d’exécution, l’état de la nouvelle soumission et les ID de corrélation.

Cette rubrique montre comment activer Log Analytics ou installer la solution Logic Apps Management dans OMS afin de voir les données et les événements du runtime associés aux exécutions de votre application logique.

 > [!TIP]
 > Pour surveiller vos applications logiques existantes, effectuez les étapes nécessaires pour [activer la journalisation des diagnostics et envoyer à OMS des données de runtime pour l’application logique](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

## <a name="requirements"></a>Configuration requise

Avant de commencer, vous devez disposer d’un espace de travail OMS. Découvrez comment [créer un espace de travail OMS](../log-analytics/log-analytics-get-started.md). 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a>Activer la journalisation des diagnostics lors de la création d’applications logiques

1. Dans le [portail Azure](https://portal.azure.com), créez une application logique. Choisissez **Nouveau** > **Intégration d’entreprise** > **Application logique** > **Créer**.

   ![Créer une application logique](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. Dans la page **Créer une application logique**, effectuez les étapes suivantes :

   1. Nommez votre application logique, puis sélectionnez votre abonnement Azure. 
   2. Créez ou sélectionnez un groupe de ressources Azure.
   3. Définissez **Log Analytics** sur **Activé**. 
   Sélectionnez l’espace de travail OMS vers lequel vous souhaitez envoyer des données concernant les exécutions de votre application logique. 
   4. Lorsque vous êtes prêt, choisissez **Épingler au tableau de bord** > **Créer**.

      ![Créer une application logique](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      Une fois cette étape terminée, Azure crée votre application logique, qui est désormais associée à votre espace de travail OMS. 
      En outre, cette étape installe automatiquement la solution Logic Apps Management dans votre espace de travail OMS.

3. Pour afficher les exécutions de votre application logique dans OMS, [effectuez ces étapes](#view-logic-app-runs-oms).

## <a name="install-the-logic-apps-management-solution-in-oms"></a>Installer la solution Logic Apps Management dans OMS

Si vous avez déjà activé Log Analytics lors de la création de votre application logique, ignorez cette étape. En effet, vous disposez déjà de la solution Logic Apps Management dans OMS.

1. Dans le [portail Azure](https://portal.azure.com), choisissez **Autres services**. Lancez une recherche sur « log analytics », puis choisissez **Log Analytics** comme illustré ici :

   ![Choisir « Log Analytics »](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. Sous **Log Analytics**, recherchez et sélectionnez votre espace de travail OMS. 

   ![Sélectionner votre espace de travail OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. Sous **Gestion**, choisissez **Portail OMS**.

   ![Choisir « Portail OMS »](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. Sur votre page d’accueil OMS, si la bannière de mise à niveau s’affiche, choisissez la bannière de manière à mettre à niveau d’abord votre espace de travail OMS. Puis choisissez **Galerie de solutions**.

   ![Sélection de « Galerie de solutions »](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. Sous **Toutes les solutions**, sélectionnez la vignette de votre solution **Logic Apps Management**.

   ![Sélection de « Logic Apps Management »](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. Pour installer la solution dans votre espace de travail OMS, choisissez **Ajouter**.

   ![Sélection de l’option « Ajouter » pour « Logic Apps Management »](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a>Afficher les exécutions de votre application logique dans votre espace de travail OMS

1. Pour afficher le nombre et l’état des exécutions de votre application logique, accédez à la vue d’ensemble de votre espace de travail OMS. Passez en revue les détails de la vignette **Logic Apps Management**.

   ![Vignette de présentation affichant l’état et le nombre d’exécutions de l’application logique](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > Si cette bannière de mise à niveau s’affiche au lieu de la vignette Logic Apps Management, choisissez la bannière de manière à mettre à niveau d’abord votre espace de travail OMS.
  
   > ![Mettre à niveau « Espace de travail OMS »](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. Pour afficher un récapitulatif plus détaillé des exécutions de votre application logique, choisissez la vignette **Logic Apps Management**.

   Les exécutions de votre application logique y sont regroupées par nom ou par état d’exécution.

   ![Récapitulatif des états pour les exécutions de votre application logique](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. Pour afficher toutes les exécutions d’une application logique ou un état, sélectionnez la ligne correspondant à cette application logique ou à cet état.

   Voici un exemple qui montre toutes les exécutions d’une application logique :

   ![Affichage des exécutions d’une application logique ou d’un état](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > La colonne **Nouvelle soumission** indique « Oui » pour les exécutions qui sont en réalité des exécutions soumises une nouvelle fois.

4. Pour filtrer ces résultats, vous pouvez effectuer un filtrage côté client et côté serveur.

   * Filtre côté client : pour chaque colonne, choisissez les filtres que vous souhaitez. 
   Voici quelques exemples :

     ![Exemples de filtres de colonne](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * Filtre côté serveur : pour choisir une fenêtre de temps ou pour limiter le nombre d’exécutions affichées, utilisez la commande d’étendue située en haut de la page. 
   Par défaut, vous ne pouvez afficher que 1 000 enregistrements à la fois. 
   
     ![Modifier la fenêtre de temps](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. Pour afficher les actions et les détails relatifs à une exécution, sélectionnez une ligne pour ouvrir la page Recherche dans les journaux. 

   * Pour afficher ces informations dans un tableau, choisissez **Tableau**.
   * Pour modifier la requête, modifiez la chaîne de requête dans la barre de recherche. 
   Pour une meilleure expérience, choisissez **Analytique avancée**.

     ![Affichage des actions et des détails relatifs à une exécution d’application logique](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     Dans la page Azure Log Analytics, vous pouvez mettre à jour des requêtes et afficher les résultats dans un tableau. 
     Cette requête utilise le [langage de requête Kusto](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), que vous pouvez modifier si vous souhaitez afficher des résultats différents. 

     ![Azure Log Analytics - Vue de la requête](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a>Étapes suivantes

* [Surveiller les messages B2B](../logic-apps/logic-apps-monitor-b2b-message.md)
