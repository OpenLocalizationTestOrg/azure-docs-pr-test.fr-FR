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
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="968d6-103">Surveiller et comprendre les exécutions d’une application logique avec Operations Management Suite (OMS) et Log Analytics</span><span class="sxs-lookup"><span data-stu-id="968d6-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="968d6-104">Pour plus d’informations de débogage plus riches et de surveillance, vous pouvez activer Analytique de journal à hello même temps lorsque vous créez une application logique.</span><span class="sxs-lookup"><span data-stu-id="968d6-104">For monitoring and richer debugging information, you can turn on Log Analytics at hello same time when you create a logic app.</span></span> <span data-ttu-id="968d6-105">Analytique de journal fournit des diagnostics de journalisation et de surveillance pour votre application logique s’exécute via le portail Operations Management Suite (OMS) de hello.</span><span class="sxs-lookup"><span data-stu-id="968d6-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through hello Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="968d6-106">Lorsque vous ajoutez tooOMS de solution hello logique de gestion des applications, vous obtenez l’état agrégé pour votre logique application s’exécute et les détails spécifiques à l’état, durée d’exécution, l’état de la nouvelle soumission et ID de corrélation.</span><span class="sxs-lookup"><span data-stu-id="968d6-106">When you add hello Logic Apps Management solution tooOMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="968d6-107">Cette rubrique montre comment tooturn sur Analytique de journal ou installez hello solution logique de gestion des applications dans OMS afin que vous pouvez afficher les événements d’exécution et exécuter des données pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="968d6-107">This topic shows how tooturn on Log Analytics or install hello Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="968d6-108">toomonitor vos applications logique existant, procédez comme suit [activer la journalisation de diagnostic et d’envoi logique application runtime données tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="968d6-108">toomonitor your existing logic apps, follow these steps too [turn on diagnostic logging and send logic app runtime data tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="968d6-109">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="968d6-109">Requirements</span></span>

<span data-ttu-id="968d6-110">Avant de commencer, vous devez toohave un espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="968d6-110">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="968d6-111">En savoir plus [comment toocreate un espace de travail OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="968d6-111">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="968d6-112">Activer la journalisation des diagnostics lors de la création d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="968d6-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="968d6-113">Dans le [portail Azure](https://portal.azure.com), créez une application logique.</span><span class="sxs-lookup"><span data-stu-id="968d6-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="968d6-114">Choisissez **Nouveau** > **Intégration d’entreprise** > **Application logique** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="968d6-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![Créer une application logique](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="968d6-116">Bonjour **application logique de créer** page, procédez comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="968d6-116">In hello **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="968d6-117">Nommez votre application logique, puis sélectionnez votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="968d6-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="968d6-118">Créez ou sélectionnez un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="968d6-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="968d6-119">Définissez **Analytique de journal** trop**sur**.</span><span class="sxs-lookup"><span data-stu-id="968d6-119">Set **Log Analytics** too**On**.</span></span> 
   <span data-ttu-id="968d6-120">Espace de travail OMS hello sélectionnez où vous souhaitez envoyer des données pour votre application logique trop s’exécute.</span><span class="sxs-lookup"><span data-stu-id="968d6-120">Select hello OMS workspace where you want too send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="968d6-121">Lorsque vous êtes prêt, choisissez **code confidentiel toodashboard** > **créer**.</span><span class="sxs-lookup"><span data-stu-id="968d6-121">When you're ready, choose **Pin toodashboard** > **Create**.</span></span>

      ![Créer une application logique](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="968d6-123">Une fois cette étape terminée, Azure crée votre application logique, qui est désormais associée à votre espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="968d6-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="968d6-124">En outre, cette étape installe aussi automatiquement la solution de logique de gestion des applications de hello dans votre espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="968d6-124">Also, this step also automatically installs hello Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="968d6-125">tooview votre application logique s’exécute dans OMS, [continuer avec ces étapes](#view-logic-app-runs-oms).</span><span class="sxs-lookup"><span data-stu-id="968d6-125">tooview your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-hello-logic-apps-management-solution-in-oms"></a><span data-ttu-id="968d6-126">Installer la solution de gestion des applications logique hello dans OMS</span><span class="sxs-lookup"><span data-stu-id="968d6-126">Install hello Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="968d6-127">Si vous avez déjà activé Log Analytics lors de la création de votre application logique, ignorez cette étape.</span><span class="sxs-lookup"><span data-stu-id="968d6-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="968d6-128">Vous avez déjà installé dans OMS de la solution de la logique de gestion des applications hello.</span><span class="sxs-lookup"><span data-stu-id="968d6-128">You already have hello Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="968d6-129">Bonjour [portail Azure](https://portal.azure.com), choisissez **plus Services**.</span><span class="sxs-lookup"><span data-stu-id="968d6-129">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="968d6-130">Lancez une recherche sur « log analytics », puis choisissez **Log Analytics** comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="968d6-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   ![Choisir « Log Analytics »](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="968d6-132">Sous **Log Analytics**, recherchez et sélectionnez votre espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="968d6-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Sélectionner votre espace de travail OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="968d6-134">Sous **Gestion**, choisissez **Portail OMS**.</span><span class="sxs-lookup"><span data-stu-id="968d6-134">Under **Management**, choose **OMS Portal**.</span></span>

   ![Choisir « Portail OMS »](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="968d6-136">Sur votre page d’accueil OMS, si la bannière de mise à niveau hello s’affiche, choisissez la bannière de hello afin que vous mettez à niveau votre espace de travail OMS tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="968d6-136">On your OMS homepage, if hello upgrade banner appears, choose hello banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="968d6-137">Puis choisissez **Galerie de solutions**.</span><span class="sxs-lookup"><span data-stu-id="968d6-137">Then choose **Solutions Gallery**.</span></span>

   ![Sélection de « Galerie de solutions »](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="968d6-139">Sous **toutes les solutions**, recherchez et sélectionnez mosaïque hello pour hello **logique de gestion des applications** solution.</span><span class="sxs-lookup"><span data-stu-id="968d6-139">Under **All solutions**, find and choose hello tile for hello **Logic Apps Management** solution.</span></span>

   ![Sélection de « Logic Apps Management »](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="968d6-141">solution de hello tooinstall dans votre espace de travail OMS, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="968d6-141">tooinstall hello solution in your OMS workspace, choose **Add**.</span></span>

   ![Sélection de l’option « Ajouter » pour « Logic Apps Management »](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="968d6-143">Afficher les exécutions de votre application logique dans votre espace de travail OMS</span><span class="sxs-lookup"><span data-stu-id="968d6-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="968d6-144">nombre de hello tooview et l’état de votre application logique s’exécute, page Vue d’ensemble de toohello accédez pour votre espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="968d6-144">tooview hello count and status for your logic app runs, go toohello overview page for your OMS workspace.</span></span> <span data-ttu-id="968d6-145">Passez en revue les détails de hello sur hello **logique de gestion des applications** vignette.</span><span class="sxs-lookup"><span data-stu-id="968d6-145">Review hello details on hello **Logic Apps Management** tile.</span></span>

   ![Vignette de présentation affichant l’état et le nombre d’exécutions de l’application logique](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="968d6-147">Si cette mise à niveau bannière s’affiche au lieu de la vignette de la logique de gestion des applications hello, choisissez la bannière de hello afin que vous mettez à niveau votre espace de travail OMS tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="968d6-147">If this upgrade banner appears instead of hello Logic Apps Management tile, choose hello banner so that you upgrade your OMS workspace first.</span></span>
  
   > ![Mettre à niveau « Espace de travail OMS »](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="968d6-149">tooview un résumé avec plus de détails sur votre application logique s’exécute, choisissez hello **logique de gestion des applications** vignette.</span><span class="sxs-lookup"><span data-stu-id="968d6-149">tooview a summary with more details about your logic app runs, choose hello **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="968d6-150">Les exécutions de votre application logique y sont regroupées par nom ou par état d’exécution.</span><span class="sxs-lookup"><span data-stu-id="968d6-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![Récapitulatif des états pour les exécutions de votre application logique](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="968d6-152">tooview que tous hello s’exécute pour une application logique spécifique ou l’état, la ligne hello select pour une application de logique ou un état.</span><span class="sxs-lookup"><span data-stu-id="968d6-152">tooview all hello runs for a specific logic app or status, select hello row for a logic app or a status.</span></span>

   <span data-ttu-id="968d6-153">Voici un exemple qui montre toutes les exécutions de hello pour une application de la logique spécifique :</span><span class="sxs-lookup"><span data-stu-id="968d6-153">Here is an example that shows all hello runs for a specific logic app:</span></span>

   ![Affichage des exécutions d’une application logique ou d’un état](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="968d6-155">Hello **renvoyés** colonne indique « Oui » pour les exécutions qui résultent d’une exécution soumise à nouveau.</span><span class="sxs-lookup"><span data-stu-id="968d6-155">hello **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="968d6-156">toofilter ces résultats, vous pouvez effectuer le filtrage côté client et côté serveur.</span><span class="sxs-lookup"><span data-stu-id="968d6-156">toofilter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="968d6-157">Filtre côté client : pour chaque colonne, choisissez des filtres de hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="968d6-157">Client-side filter: For each column, choose hello filters that you want.</span></span> 
   <span data-ttu-id="968d6-158">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="968d6-158">Here are some examples:</span></span>

     ![Exemples de filtres de colonne](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="968d6-160">Filtre côté serveur : toochoose un nombre spécifique de temps fenêtre ou toolimit hello des exécutions qui s’affichent, utiliser le contrôle d’étendue hello en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="968d6-160">Server-side filter: toochoose a specific time window or toolimit hello number of runs that appear, use hello scope control at hello top of hello page.</span></span> 
   <span data-ttu-id="968d6-161">Par défaut, vous ne pouvez afficher que 1 000 enregistrements à la fois.</span><span class="sxs-lookup"><span data-stu-id="968d6-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![Changement de fenêtre de temps hello](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="968d6-163">tooview tous les hello actions ainsi que leurs informations pour un spécifique, exécution, sélectionnez une ligne, ce qui ouvre la page de recherche de journal hello.</span><span class="sxs-lookup"><span data-stu-id="968d6-163">tooview all hello actions and their details for a specific run, select a row, which opens hello Log Search page.</span></span> 

   * <span data-ttu-id="968d6-164">Choisissez de ces informations dans une table, tooview **Table**.</span><span class="sxs-lookup"><span data-stu-id="968d6-164">tooview this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="968d6-165">requête de hello toochange, vous pouvez modifier le chaîne de requête hello dans la barre de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="968d6-165">toochange hello query, you can edit hello query string in hello search bar.</span></span> 
   <span data-ttu-id="968d6-166">Pour une meilleure expérience, choisissez **Analytique avancée**.</span><span class="sxs-lookup"><span data-stu-id="968d6-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![Affichage des actions et des détails relatifs à une exécution d’application logique](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="968d6-168">Ici sur la page d’Analytique des journaux Azure hello, vous pouvez mettre à jour des requêtes et affichage des résultats à partir de la table de hello hello.</span><span class="sxs-lookup"><span data-stu-id="968d6-168">Here on hello Azure Log Analytics page, you can update queries and view hello results from hello table.</span></span> 
     <span data-ttu-id="968d6-169">Cette requête utilise [Kusto le langage de requête](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), que vous pouvez modifier si vous souhaitez tooview des résultats différents.</span><span class="sxs-lookup"><span data-stu-id="968d6-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want tooview different results.</span></span> 

     ![Azure Log Analytics - Vue de la requête](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="968d6-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="968d6-171">Next steps</span></span>

* [<span data-ttu-id="968d6-172">Surveiller les messages B2B</span><span class="sxs-lookup"><span data-stu-id="968d6-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
