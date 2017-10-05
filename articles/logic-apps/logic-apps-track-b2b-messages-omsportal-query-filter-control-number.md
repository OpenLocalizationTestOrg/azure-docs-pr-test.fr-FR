---
title: Interroger des messages B2B dans Operations Management Suite - Azure Logic Apps | Microsoft Docs
description: "Créer des requêtes pour suivre des messages AS2, X 12 et EDIFACT dans Operations Management Suite"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 2748d3d3daf7c13dca05f663a4a088598e1b3605
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-the-microsoft-operations-management-suite-oms"></a><span data-ttu-id="046fe-103">Interroger des messages AS2, X 12 et EDIFACT dans Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="046fe-103">Query for AS2, X12, and EDIFACT messages in the Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="046fe-104">Pour rechercher les messages AS2, X12 ou EDIFACT que vous suivez avec [Azure Log Analytics](../log-analytics/log-analytics-overview.md) dans [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), vous pouvez créer des requêtes qui filtrent les actions en fonction de critères spécifiques.</span><span class="sxs-lookup"><span data-stu-id="046fe-104">To find the AS2, X12, or EDIFACT messages that you're tracking with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), you can create queries that filter actions based on specific criteria.</span></span> <span data-ttu-id="046fe-105">Par exemple, vous pouvez rechercher des messages sur la base d’un numéro de contrôle d’échange spécifique.</span><span class="sxs-lookup"><span data-stu-id="046fe-105">For example, you can find messages based on a specific interchange control number.</span></span>

## <a name="requirements"></a><span data-ttu-id="046fe-106">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="046fe-106">Requirements</span></span>

* <span data-ttu-id="046fe-107">Une application logique configurée avec une journalisation des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="046fe-107">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="046fe-108">Découvrez comment [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md) et comment [configurer la journalisation pour cette application logique](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="046fe-108">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) and [how to set up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="046fe-109">Un compte d’intégration configuré avec une surveillance et une journalisation.</span><span class="sxs-lookup"><span data-stu-id="046fe-109">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="046fe-110">Découvrez comment [créer un compte d’intégration](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) et comment [configurer une surveillance et une journalisation pour ce compte](../logic-apps/logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="046fe-110">Learn [how to create an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how to set up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="046fe-111">Si ce n’est déjà fait, [publiez des données de diagnostic sur Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) puis [configurez le suivi des messages dans OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="046fe-111">If you haven't already, [publish diagnostic data to Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) and [set up message tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="046fe-112">Une fois les conditions précédentes réunies, vous devez disposer d’un espace de travail dans [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="046fe-112">After you've met the previous requirements, you should have a workspace in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="046fe-113">Vous devez utiliser l’espace de travail OMS que vous utilisez pour le suivi de votre communication B2B dans OMS.</span><span class="sxs-lookup"><span data-stu-id="046fe-113">You should use the same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="046fe-114">Si vous n’avez pas d’espace de travail OMS, découvrez comment [créer un espace de travail OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="046fe-114">If you don't have an OMS workspace, learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="create-message-queries-with-filters-in-the-operations-management-suite-portal"></a><span data-ttu-id="046fe-115">Créer des requêtes de messages avec des filtres dans le portail Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="046fe-115">Create message queries with filters in the Operations Management Suite portal</span></span>

<span data-ttu-id="046fe-116">Cet exemple montre comment rechercher des messages en fonction de leur numéro de contrôle d’échange.</span><span class="sxs-lookup"><span data-stu-id="046fe-116">This example shows how you can find messages based on their interchange control number.</span></span>

> [!TIP] 
> <span data-ttu-id="046fe-117">Si vous connaissez le nom de votre espace de travail OMS, accédez à la page d’accueil de votre espace de travail (`https://{your-workspace-name}.portal.mms.microsoft.com`), puis passez à l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="046fe-117">If you know your OMS workspace name, go to your workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and start at Step 4.</span></span> <span data-ttu-id="046fe-118">Autrement, commencez à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="046fe-118">Otherwise, start at Step 1.</span></span>

1. <span data-ttu-id="046fe-119">Dans le [portail Azure](https://portal.azure.com), choisissez **Autres services**.</span><span class="sxs-lookup"><span data-stu-id="046fe-119">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="046fe-120">Recherchez « log analytics », puis choisissez **Log Analytics** comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="046fe-120">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![Rechercher Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. <span data-ttu-id="046fe-122">Sous **Log Analytics**, recherchez et sélectionnez votre espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="046fe-122">Under **Log Analytics**, find and select your OMS workspace.</span></span>

   ![Sélectionner votre espace de travail OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. <span data-ttu-id="046fe-124">Sous **Gestion**, choisissez **Portail OMS**.</span><span class="sxs-lookup"><span data-stu-id="046fe-124">Under **Management**, choose **OMS Portal**.</span></span>

   ![Choisir le portail OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. <span data-ttu-id="046fe-126">Dans votre page d’accueil d’OMS, choisissez **Recherche dans les journaux**.</span><span class="sxs-lookup"><span data-stu-id="046fe-126">On your OMS home page, choose **Log Search**.</span></span>

   ![Dans votre page d’accueil d’OMS, choisissez « Recherche dans les journaux »](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="046fe-128">-ou-</span><span class="sxs-lookup"><span data-stu-id="046fe-128">-or-</span></span>

   ![Dans le menu OMS, choisir « Recherche dans les journaux »](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. <span data-ttu-id="046fe-130">Dans la zone de recherche, complétez un champ que vous souhaitez trouver, puis appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="046fe-130">In the search box, enter a field that you want to find, and press **Enter**.</span></span> <span data-ttu-id="046fe-131">Lorsque vous commencez à taper, OMS affiche les correspondances possibles et les opérations que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="046fe-131">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> <span data-ttu-id="046fe-132">Pour en savoir plus, voir [Recherche de données à l’aide de recherches de journal](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="046fe-132">Learn more about [how to find data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   <span data-ttu-id="046fe-133">Cet exemple recherche des événements avec **Type=AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="046fe-133">This example searches for events with **Type=AzureDiagnostics**.</span></span>

   ![Commencer à taper la chaîne de requête](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. <span data-ttu-id="046fe-135">Dans la barre de gauche, choisissez la plage de temps que vous souhaitez afficher.</span><span class="sxs-lookup"><span data-stu-id="046fe-135">In the left bar, choose the timeframe that you want to view.</span></span> <span data-ttu-id="046fe-136">Pour ajouter un filtre à votre requête, choisissez **+Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="046fe-136">To add a filter to your query, choose **+Add**.</span></span>

   ![Ajouter un filtre à une requête](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. <span data-ttu-id="046fe-138">Sous **Ajouter des filtres**, entrez le nom du filtre afin de trouver le filtre souhaité.</span><span class="sxs-lookup"><span data-stu-id="046fe-138">Under **Add Filters**, enter the filter name so you can find the filter you want.</span></span> <span data-ttu-id="046fe-139">Sélectionnez le filtre, puis choisissez **+Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="046fe-139">Select the filter, and choose **+Add**.</span></span>

   <span data-ttu-id="046fe-140">Pour trouver le numéro de contrôle d’échange, cet exemple recherche le mot « interchange » (échange), puis sélectionne **event_record_messageProperties_interchangeControlNumber_s** en tant que filtre.</span><span class="sxs-lookup"><span data-stu-id="046fe-140">To find the interchange control number, this example searches for the word "interchange", and selects **event_record_messageProperties_interchangeControlNumber_s** as the filter.</span></span>

   ![Sélectionner le filtre](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. <span data-ttu-id="046fe-142">Dans la barre de gauche, sélectionnez la valeur de filtre que vous souhaitez utiliser, puis choisissez **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="046fe-142">In the left bar, select the filter value that you want to use, and choose **Apply**.</span></span>

   <span data-ttu-id="046fe-143">Cet exemple sélectionne le numéro de contrôle d’échange pour les messages que nous voulons.</span><span class="sxs-lookup"><span data-stu-id="046fe-143">This example selects the interchange control number for the messages we want.</span></span>

   ![Sélectionner une valeur de filtre](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. <span data-ttu-id="046fe-145">Revenez à présent à la requête que vous créez.</span><span class="sxs-lookup"><span data-stu-id="046fe-145">Now return to the query that you're building.</span></span> <span data-ttu-id="046fe-146">Votre requête a été mise à jour avec l’événement et la valeur de filtre sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="046fe-146">Your query has been updated with your selected filter event and value.</span></span> <span data-ttu-id="046fe-147">Vos résultats précédents sont à présent également filtrés.</span><span class="sxs-lookup"><span data-stu-id="046fe-147">Your previous results are now filtered too.</span></span>

    ![Revenir à votre requête avec les résultats filtrés](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a><span data-ttu-id="046fe-149">Enregistrer votre requête pour un usage ultérieur</span><span class="sxs-lookup"><span data-stu-id="046fe-149">Save your query for future use</span></span>

1. <span data-ttu-id="046fe-150">À partir de votre requête dans la page **Recherche dans les journaux**, choisissez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="046fe-150">From your query on the **Log Search** page, choose **Save**.</span></span> <span data-ttu-id="046fe-151">Donnez un nom à votre requête, sélectionnez une catégorie, puis choisissez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="046fe-151">Give your query a name, select a category, and choose **Save**.</span></span>

   ![Donner un nom et une catégorie à votre requête](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. <span data-ttu-id="046fe-153">Pour afficher votre requête, choisissez **Favoris**.</span><span class="sxs-lookup"><span data-stu-id="046fe-153">To view your query, choose **Favorites**.</span></span>

   ![Choisir « Favoris »](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. <span data-ttu-id="046fe-155">Sous **Recherches enregistrées**, sélectionnez votre requête afin de pouvoir afficher les résultats.</span><span class="sxs-lookup"><span data-stu-id="046fe-155">Under **Saved Searches**, select your query so that you can view the results.</span></span> <span data-ttu-id="046fe-156">Pour mettre à jour la requête afin d’obtenir des résultats différents, modifiez la requête.</span><span class="sxs-lookup"><span data-stu-id="046fe-156">To update the query so you can find different results, edit the query.</span></span>

   ![Sélectionner votre requête](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-the-operations-management-suite-portal"></a><span data-ttu-id="046fe-158">Rechercher et exécuter des requêtes enregistrées dans le portail Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="046fe-158">Find and run saved queries in the Operations Management Suite portal</span></span>

1. <span data-ttu-id="046fe-159">Ouvrez la page d’accueil de votre espace de travail OMS (`https://{your-workspace-name}.portal.mms.microsoft.com`), puis choisissez **Recherche dans les journaux**.</span><span class="sxs-lookup"><span data-stu-id="046fe-159">Open your OMS workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and choose **Log Search**.</span></span>

   ![Dans votre page d’accueil d’OMS, choisissez « Recherche dans les journaux »](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="046fe-161">-ou-</span><span class="sxs-lookup"><span data-stu-id="046fe-161">-or-</span></span>

   ![Dans le menu OMS, choisir « Recherche dans les journaux »](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. <span data-ttu-id="046fe-163">Dans la page d'accueil **Recherche dans les journaux**, choisissez **Favoris**.</span><span class="sxs-lookup"><span data-stu-id="046fe-163">On the **Log Search** home page, choose **Favorites**.</span></span>

   ![Choisir « Favoris »](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. <span data-ttu-id="046fe-165">Sous **Recherches enregistrées**, sélectionnez votre requête afin de pouvoir afficher les résultats.</span><span class="sxs-lookup"><span data-stu-id="046fe-165">Under **Saved Searches**, select your query so that you can view the results.</span></span> <span data-ttu-id="046fe-166">Pour mettre à jour la requête afin d’obtenir des résultats différents, modifiez la requête.</span><span class="sxs-lookup"><span data-stu-id="046fe-166">To update the query so you can find different results, edit the query.</span></span>

   ![Sélectionner votre requête](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a><span data-ttu-id="046fe-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="046fe-168">Next steps</span></span>

* [<span data-ttu-id="046fe-169">Schémas de suivi AS2</span><span class="sxs-lookup"><span data-stu-id="046fe-169">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="046fe-170">Schémas de suivi X12</span><span class="sxs-lookup"><span data-stu-id="046fe-170">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="046fe-171">Schémas de suivi personnalisé</span><span class="sxs-lookup"><span data-stu-id="046fe-171">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)