---
title: "aaaMonitor et obtenir des informations sur votre application logique s’exécute à l’aide d’OMS - Azure Logic Apps | Documents Microsoft"
description: "Surveiller votre application logique s’exécute avec les analyses tooget Analytique de journal et Operations Management Suite (OMS) et les détails de débogage plus détaillées pour le dépannage et diagnostics"
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
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a>Surveiller et comprendre les exécutions d’une application logique avec Operations Management Suite (OMS) et Log Analytics

Pour plus d’informations de débogage plus riches et de surveillance, vous pouvez activer Analytique de journal à hello même temps lorsque vous créez une application logique. Analytique de journal fournit des diagnostics de journalisation et de surveillance pour votre application logique s’exécute via le portail Operations Management Suite (OMS) de hello. Lorsque vous ajoutez tooOMS de solution hello logique de gestion des applications, vous obtenez l’état agrégé pour votre logique application s’exécute et les détails spécifiques à l’état, durée d’exécution, l’état de la nouvelle soumission et ID de corrélation.

Cette rubrique montre comment tooturn sur Analytique de journal ou installez hello solution logique de gestion des applications dans OMS afin que vous pouvez afficher les événements d’exécution et exécuter des données pour votre application logique.

 > [!TIP]
 > toomonitor vos applications logique existant, procédez comme suit [activer la journalisation de diagnostic et d’envoi logique application runtime données tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

## <a name="requirements"></a>Configuration requise

Avant de commencer, vous devez toohave un espace de travail OMS. En savoir plus [comment toocreate un espace de travail OMS](../log-analytics/log-analytics-get-started.md). 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a>Activer la journalisation des diagnostics lors de la création d’applications logiques

1. Dans le [portail Azure](https://portal.azure.com), créez une application logique. Choisissez **Nouveau** > **Intégration d’entreprise** > **Application logique** > **Créer**.

   ![Créer une application logique](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. Bonjour **application logique de créer** page, procédez comme indiqué :

   1. Nommez votre application logique, puis sélectionnez votre abonnement Azure. 
   2. Créez ou sélectionnez un groupe de ressources Azure.
   3. Définissez **Analytique de journal** trop**sur**. 
   Espace de travail OMS hello sélectionnez où vous souhaitez envoyer des données pour votre application logique trop s’exécute. 
   4. Lorsque vous êtes prêt, choisissez **code confidentiel toodashboard** > **créer**.

      ![Créer une application logique](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      Une fois cette étape terminée, Azure crée votre application logique, qui est désormais associée à votre espace de travail OMS. 
      En outre, cette étape installe aussi automatiquement la solution de logique de gestion des applications de hello dans votre espace de travail OMS.

3. tooview votre application logique s’exécute dans OMS, [continuer avec ces étapes](#view-logic-app-runs-oms).

## <a name="install-hello-logic-apps-management-solution-in-oms"></a>Installer la solution de gestion des applications logique hello dans OMS

Si vous avez déjà activé Log Analytics lors de la création de votre application logique, ignorez cette étape. Vous avez déjà installé dans OMS de la solution de la logique de gestion des applications hello.

1. Bonjour [portail Azure](https://portal.azure.com), choisissez **plus Services**. Lancez une recherche sur « log analytics », puis choisissez **Log Analytics** comme illustré ici :

   ![Choisir « Log Analytics »](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. Sous **Log Analytics**, recherchez et sélectionnez votre espace de travail OMS. 

   ![Sélectionner votre espace de travail OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. Sous **Gestion**, choisissez **Portail OMS**.

   ![Choisir « Portail OMS »](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. Sur votre page d’accueil OMS, si la bannière de mise à niveau hello s’affiche, choisissez la bannière de hello afin que vous mettez à niveau votre espace de travail OMS tout d’abord. Puis choisissez **Galerie de solutions**.

   ![Sélection de « Galerie de solutions »](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. Sous **toutes les solutions**, recherchez et sélectionnez mosaïque hello pour hello **logique de gestion des applications** solution.

   ![Sélection de « Logic Apps Management »](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. solution de hello tooinstall dans votre espace de travail OMS, cliquez sur **ajouter**.

   ![Sélection de l’option « Ajouter » pour « Logic Apps Management »](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a>Afficher les exécutions de votre application logique dans votre espace de travail OMS

1. nombre de hello tooview et l’état de votre application logique s’exécute, page Vue d’ensemble de toohello accédez pour votre espace de travail OMS. Passez en revue les détails de hello sur hello **logique de gestion des applications** vignette.

   ![Vignette de présentation affichant l’état et le nombre d’exécutions de l’application logique](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > Si cette mise à niveau bannière s’affiche au lieu de la vignette de la logique de gestion des applications hello, choisissez la bannière de hello afin que vous mettez à niveau votre espace de travail OMS tout d’abord.
  
   > ![Mettre à niveau « Espace de travail OMS »](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. tooview un résumé avec plus de détails sur votre application logique s’exécute, choisissez hello **logique de gestion des applications** vignette.

   Les exécutions de votre application logique y sont regroupées par nom ou par état d’exécution.

   ![Récapitulatif des états pour les exécutions de votre application logique](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. tooview que tous hello s’exécute pour une application logique spécifique ou l’état, la ligne hello select pour une application de logique ou un état.

   Voici un exemple qui montre toutes les exécutions de hello pour une application de la logique spécifique :

   ![Affichage des exécutions d’une application logique ou d’un état](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > Hello **renvoyés** colonne indique « Oui » pour les exécutions qui résultent d’une exécution soumise à nouveau.

4. toofilter ces résultats, vous pouvez effectuer le filtrage côté client et côté serveur.

   * Filtre côté client : pour chaque colonne, choisissez des filtres de hello souhaité. 
   Voici quelques exemples :

     ![Exemples de filtres de colonne](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * Filtre côté serveur : toochoose un nombre spécifique de temps fenêtre ou toolimit hello des exécutions qui s’affichent, utiliser le contrôle d’étendue hello en hello haut hello. 
   Par défaut, vous ne pouvez afficher que 1 000 enregistrements à la fois. 
   
     ![Changement de fenêtre de temps hello](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. tooview tous les hello actions ainsi que leurs informations pour un spécifique, exécution, sélectionnez une ligne, ce qui ouvre la page de recherche de journal hello. 

   * Choisissez de ces informations dans une table, tooview **Table**.
   * requête de hello toochange, vous pouvez modifier le chaîne de requête hello dans la barre de recherche hello. 
   Pour une meilleure expérience, choisissez **Analytique avancée**.

     ![Affichage des actions et des détails relatifs à une exécution d’application logique](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     Ici sur la page d’Analytique des journaux Azure hello, vous pouvez mettre à jour des requêtes et affichage des résultats à partir de la table de hello hello. 
     Cette requête utilise [Kusto le langage de requête](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), que vous pouvez modifier si vous souhaitez tooview des résultats différents. 

     ![Azure Log Analytics - Vue de la requête](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a>Étapes suivantes

* [Surveiller les messages B2B](../logic-apps/logic-apps-monitor-b2b-message.md)
