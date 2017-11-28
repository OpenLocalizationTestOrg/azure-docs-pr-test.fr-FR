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
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="9f05e-103">Surveiller et comprendre les exécutions d’une application logique avec Operations Management Suite (OMS) et Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9f05e-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="9f05e-104">Pour la surveillance et l’obtention d’informations de débogage plus détaillées, vous pouvez activer Log Analytics lorsque vous créez une application logique.</span><span class="sxs-lookup"><span data-stu-id="9f05e-104">For monitoring and richer debugging information, you can turn on Log Analytics at the same time when you create a logic app.</span></span> <span data-ttu-id="9f05e-105">Log Analytics fournit des options de journalisation des diagnostics et de surveillance pour les exécutions de votre application logique via le portail Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="9f05e-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through the Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="9f05e-106">Lorsque vous ajoutez la solution Logic Apps Management à OMS, vous obtenez l’état agrégé des exécutions de votre application logique, ainsi que des informations détaillées telles que l’état, la durée d’exécution, l’état de la nouvelle soumission et les ID de corrélation.</span><span class="sxs-lookup"><span data-stu-id="9f05e-106">When you add the Logic Apps Management solution to OMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="9f05e-107">Cette rubrique montre comment activer Log Analytics ou installer la solution Logic Apps Management dans OMS afin de voir les données et les événements du runtime associés aux exécutions de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="9f05e-107">This topic shows how to turn on Log Analytics or install the Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="9f05e-108">Pour surveiller vos applications logiques existantes, effectuez les étapes nécessaires pour [activer la journalisation des diagnostics et envoyer à OMS des données de runtime pour l’application logique](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="9f05e-108">To monitor your existing logic apps, follow these steps to [turn on diagnostic logging and send logic app runtime data to OMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="9f05e-109">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="9f05e-109">Requirements</span></span>

<span data-ttu-id="9f05e-110">Avant de commencer, vous devez disposer d’un espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="9f05e-110">Before you start, you need to have an OMS workspace.</span></span> <span data-ttu-id="9f05e-111">Découvrez comment [créer un espace de travail OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9f05e-111">Learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="9f05e-112">Activer la journalisation des diagnostics lors de la création d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="9f05e-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="9f05e-113">Dans le [portail Azure](https://portal.azure.com), créez une application logique.</span><span class="sxs-lookup"><span data-stu-id="9f05e-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="9f05e-114">Choisissez **Nouveau** > **Intégration d’entreprise** > **Application logique** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="9f05e-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![Créer une application logique](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="9f05e-116">Dans la page **Créer une application logique**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9f05e-116">In the **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="9f05e-117">Nommez votre application logique, puis sélectionnez votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="9f05e-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="9f05e-118">Créez ou sélectionnez un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9f05e-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="9f05e-119">Définissez **Log Analytics** sur **Activé**.</span><span class="sxs-lookup"><span data-stu-id="9f05e-119">Set **Log Analytics** to **On**.</span></span> 
   <span data-ttu-id="9f05e-120">Sélectionnez l’espace de travail OMS vers lequel vous souhaitez envoyer des données concernant les exécutions de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="9f05e-120">Select the OMS workspace where you want to send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="9f05e-121">Lorsque vous êtes prêt, choisissez **Épingler au tableau de bord** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="9f05e-121">When you're ready, choose **Pin to dashboard** > **Create**.</span></span>

      ![Créer une application logique](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="9f05e-123">Une fois cette étape terminée, Azure crée votre application logique, qui est désormais associée à votre espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="9f05e-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="9f05e-124">En outre, cette étape installe automatiquement la solution Logic Apps Management dans votre espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="9f05e-124">Also, this step also automatically installs the Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="9f05e-125">Pour afficher les exécutions de votre application logique dans OMS, [effectuez ces étapes](#view-logic-app-runs-oms).</span><span class="sxs-lookup"><span data-stu-id="9f05e-125">To view your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-the-logic-apps-management-solution-in-oms"></a><span data-ttu-id="9f05e-126">Installer la solution Logic Apps Management dans OMS</span><span class="sxs-lookup"><span data-stu-id="9f05e-126">Install the Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="9f05e-127">Si vous avez déjà activé Log Analytics lors de la création de votre application logique, ignorez cette étape.</span><span class="sxs-lookup"><span data-stu-id="9f05e-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="9f05e-128">En effet, vous disposez déjà de la solution Logic Apps Management dans OMS.</span><span class="sxs-lookup"><span data-stu-id="9f05e-128">You already have the Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="9f05e-129">Dans le [portail Azure](https://portal.azure.com), choisissez **Autres services**.</span><span class="sxs-lookup"><span data-stu-id="9f05e-129">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="9f05e-130">Lancez une recherche sur « log analytics », puis choisissez **Log Analytics** comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="9f05e-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   ![Choisir « Log Analytics »](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="9f05e-132">Sous **Log Analytics**, recherchez et sélectionnez votre espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="9f05e-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Sélectionner votre espace de travail OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="9f05e-134">Sous **Gestion**, choisissez **Portail OMS**.</span><span class="sxs-lookup"><span data-stu-id="9f05e-134">Under **Management**, choose **OMS Portal**.</span></span>

   ![Choisir « Portail OMS »](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="9f05e-136">Sur votre page d’accueil OMS, si la bannière de mise à niveau s’affiche, choisissez la bannière de manière à mettre à niveau d’abord votre espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="9f05e-136">On your OMS homepage, if the upgrade banner appears, choose the banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="9f05e-137">Puis choisissez **Galerie de solutions**.</span><span class="sxs-lookup"><span data-stu-id="9f05e-137">Then choose **Solutions Gallery**.</span></span>

   ![Sélection de « Galerie de solutions »](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="9f05e-139">Sous **Toutes les solutions**, sélectionnez la vignette de votre solution **Logic Apps Management**.</span><span class="sxs-lookup"><span data-stu-id="9f05e-139">Under **All solutions**, find and choose the tile for the **Logic Apps Management** solution.</span></span>

   ![Sélection de « Logic Apps Management »](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="9f05e-141">Pour installer la solution dans votre espace de travail OMS, choisissez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9f05e-141">To install the solution in your OMS workspace, choose **Add**.</span></span>

   ![Sélection de l’option « Ajouter » pour « Logic Apps Management »](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="9f05e-143">Afficher les exécutions de votre application logique dans votre espace de travail OMS</span><span class="sxs-lookup"><span data-stu-id="9f05e-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="9f05e-144">Pour afficher le nombre et l’état des exécutions de votre application logique, accédez à la vue d’ensemble de votre espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="9f05e-144">To view the count and status for your logic app runs, go to the overview page for your OMS workspace.</span></span> <span data-ttu-id="9f05e-145">Passez en revue les détails de la vignette **Logic Apps Management**.</span><span class="sxs-lookup"><span data-stu-id="9f05e-145">Review the details on the **Logic Apps Management** tile.</span></span>

   ![Vignette de présentation affichant l’état et le nombre d’exécutions de l’application logique](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="9f05e-147">Si cette bannière de mise à niveau s’affiche au lieu de la vignette Logic Apps Management, choisissez la bannière de manière à mettre à niveau d’abord votre espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="9f05e-147">If this upgrade banner appears instead of the Logic Apps Management tile, choose the banner so that you upgrade your OMS workspace first.</span></span>
  
   > ![Mettre à niveau « Espace de travail OMS »](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="9f05e-149">Pour afficher un récapitulatif plus détaillé des exécutions de votre application logique, choisissez la vignette **Logic Apps Management**.</span><span class="sxs-lookup"><span data-stu-id="9f05e-149">To view a summary with more details about your logic app runs, choose the **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="9f05e-150">Les exécutions de votre application logique y sont regroupées par nom ou par état d’exécution.</span><span class="sxs-lookup"><span data-stu-id="9f05e-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![Récapitulatif des états pour les exécutions de votre application logique](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="9f05e-152">Pour afficher toutes les exécutions d’une application logique ou un état, sélectionnez la ligne correspondant à cette application logique ou à cet état.</span><span class="sxs-lookup"><span data-stu-id="9f05e-152">To view all the runs for a specific logic app or status, select the row for a logic app or a status.</span></span>

   <span data-ttu-id="9f05e-153">Voici un exemple qui montre toutes les exécutions d’une application logique :</span><span class="sxs-lookup"><span data-stu-id="9f05e-153">Here is an example that shows all the runs for a specific logic app:</span></span>

   ![Affichage des exécutions d’une application logique ou d’un état](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="9f05e-155">La colonne **Nouvelle soumission** indique « Oui » pour les exécutions qui sont en réalité des exécutions soumises une nouvelle fois.</span><span class="sxs-lookup"><span data-stu-id="9f05e-155">The **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="9f05e-156">Pour filtrer ces résultats, vous pouvez effectuer un filtrage côté client et côté serveur.</span><span class="sxs-lookup"><span data-stu-id="9f05e-156">To filter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="9f05e-157">Filtre côté client : pour chaque colonne, choisissez les filtres que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="9f05e-157">Client-side filter: For each column, choose the filters that you want.</span></span> 
   <span data-ttu-id="9f05e-158">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="9f05e-158">Here are some examples:</span></span>

     ![Exemples de filtres de colonne](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="9f05e-160">Filtre côté serveur : pour choisir une fenêtre de temps ou pour limiter le nombre d’exécutions affichées, utilisez la commande d’étendue située en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="9f05e-160">Server-side filter: To choose a specific time window or to limit the number of runs that appear, use the scope control at the top of the page.</span></span> 
   <span data-ttu-id="9f05e-161">Par défaut, vous ne pouvez afficher que 1 000 enregistrements à la fois.</span><span class="sxs-lookup"><span data-stu-id="9f05e-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![Modifier la fenêtre de temps](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="9f05e-163">Pour afficher les actions et les détails relatifs à une exécution, sélectionnez une ligne pour ouvrir la page Recherche dans les journaux.</span><span class="sxs-lookup"><span data-stu-id="9f05e-163">To view all the actions and their details for a specific run, select a row, which opens the Log Search page.</span></span> 

   * <span data-ttu-id="9f05e-164">Pour afficher ces informations dans un tableau, choisissez **Tableau**.</span><span class="sxs-lookup"><span data-stu-id="9f05e-164">To view this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="9f05e-165">Pour modifier la requête, modifiez la chaîne de requête dans la barre de recherche.</span><span class="sxs-lookup"><span data-stu-id="9f05e-165">To change the query, you can edit the query string in the search bar.</span></span> 
   <span data-ttu-id="9f05e-166">Pour une meilleure expérience, choisissez **Analytique avancée**.</span><span class="sxs-lookup"><span data-stu-id="9f05e-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![Affichage des actions et des détails relatifs à une exécution d’application logique](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="9f05e-168">Dans la page Azure Log Analytics, vous pouvez mettre à jour des requêtes et afficher les résultats dans un tableau.</span><span class="sxs-lookup"><span data-stu-id="9f05e-168">Here on the Azure Log Analytics page, you can update queries and view the results from the table.</span></span> 
     <span data-ttu-id="9f05e-169">Cette requête utilise le [langage de requête Kusto](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), que vous pouvez modifier si vous souhaitez afficher des résultats différents.</span><span class="sxs-lookup"><span data-stu-id="9f05e-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want to view different results.</span></span> 

     ![Azure Log Analytics - Vue de la requête](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="9f05e-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9f05e-171">Next steps</span></span>

* [<span data-ttu-id="9f05e-172">Surveiller les messages B2B</span><span class="sxs-lookup"><span data-stu-id="9f05e-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
