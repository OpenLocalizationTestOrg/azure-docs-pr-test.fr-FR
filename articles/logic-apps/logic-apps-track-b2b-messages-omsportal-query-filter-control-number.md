---
title: aaaQuery pour les messages B2B dans Operations Management Suite - Azure Logic Apps | Documents Microsoft
description: "Créer des requêtes tootrack AS2, X 12 et EDIFACT messages Bonjour Operations Management Suite"
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
ms.openlocfilehash: aee6644ff19add8f074ed5f1725db87b1d3b74b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a><span data-ttu-id="f6fb9-103">Messages de requête pour AS2, X 12 et EDIFACT Bonjour Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="f6fb9-103">Query for AS2, X12, and EDIFACT messages in hello Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="f6fb9-104">toofind hello AS2, X 12 ou EDIFACT les messages dont vous effectuez le suivi avec [Analytique de journal Azure](../log-analytics/log-analytics-overview.md) Bonjour [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), vous pouvez créer des requêtes qui filtrent les actions en fonction des spécifique critères.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-104">toofind hello AS2, X12, or EDIFACT messages that you're tracking with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), you can create queries that filter actions based on specific criteria.</span></span> <span data-ttu-id="f6fb9-105">Par exemple, vous pouvez rechercher des messages sur la base d’un numéro de contrôle d’échange spécifique.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-105">For example, you can find messages based on a specific interchange control number.</span></span>

## <a name="requirements"></a><span data-ttu-id="f6fb9-106">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="f6fb9-106">Requirements</span></span>

* <span data-ttu-id="f6fb9-107">Une application logique configurée avec une journalisation des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-107">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="f6fb9-108">En savoir plus [comment toocreate une application logique](../logic-apps/logic-apps-create-a-logic-app.md) et [comment tooset configure une journalisation pour cette application logique](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="f6fb9-108">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md) and [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="f6fb9-109">Un compte d’intégration configuré avec une surveillance et une journalisation.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-109">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="f6fb9-110">En savoir plus [comment toocreate un compte d’intégration](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) et [comment tooset de surveillance et la journalisation pour ce compte](../logic-apps/logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="f6fb9-110">Learn [how toocreate an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how tooset up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="f6fb9-111">Si vous n’avez pas déjà fait, [publier des données de diagnostic tooLog Analytique](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) et [configurer le suivi des messages dans OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="f6fb9-111">If you haven't already, [publish diagnostic data tooLog Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) and [set up message tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f6fb9-112">Une fois que vous avez requise hello précédente, vous devez disposer d’un espace de travail Bonjour [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f6fb9-112">After you've met hello previous requirements, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="f6fb9-113">Vous devez utiliser hello même espace de travail OMS pour le suivi de vos communications B2B dans OMS.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-113">You should use hello same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="f6fb9-114">Si vous n’avez pas un espace de travail OMS, Découvrez [comment toocreate un espace de travail OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f6fb9-114">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a><span data-ttu-id="f6fb9-115">Créer des requêtes de messages avec des filtres dans le portail Operations Management Suite de hello</span><span class="sxs-lookup"><span data-stu-id="f6fb9-115">Create message queries with filters in hello Operations Management Suite portal</span></span>

<span data-ttu-id="f6fb9-116">Cet exemple montre comment rechercher des messages en fonction de leur numéro de contrôle d’échange.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-116">This example shows how you can find messages based on their interchange control number.</span></span>

> [!TIP] 
> <span data-ttu-id="f6fb9-117">Si vous connaissez le nom de votre espace de travail OMS, consultez la page d’accueil espace de travail tooyour (`https://{your-workspace-name}.portal.mms.microsoft.com`) et commencez à l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-117">If you know your OMS workspace name, go tooyour workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and start at Step 4.</span></span> <span data-ttu-id="f6fb9-118">Autrement, commencez à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-118">Otherwise, start at Step 1.</span></span>

1. <span data-ttu-id="f6fb9-119">Bonjour [portail Azure](https://portal.azure.com), choisissez **plus Services**.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-119">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="f6fb9-120">Recherchez « log analytics », puis choisissez **Log Analytics** comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="f6fb9-120">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![Rechercher Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. <span data-ttu-id="f6fb9-122">Sous **Log Analytics**, recherchez et sélectionnez votre espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-122">Under **Log Analytics**, find and select your OMS workspace.</span></span>

   ![Sélectionner votre espace de travail OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. <span data-ttu-id="f6fb9-124">Sous **Gestion**, choisissez **Portail OMS**.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-124">Under **Management**, choose **OMS Portal**.</span></span>

   ![Choisir le portail OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. <span data-ttu-id="f6fb9-126">Dans votre page d’accueil d’OMS, choisissez **Recherche dans les journaux**.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-126">On your OMS home page, choose **Log Search**.</span></span>

   ![Dans votre page d’accueil d’OMS, choisissez « Recherche dans les journaux »](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="f6fb9-128">-ou-</span><span class="sxs-lookup"><span data-stu-id="f6fb9-128">-or-</span></span>

   ![Menu hello OMS, choisissez « Recherche de journal »](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. <span data-ttu-id="f6fb9-130">Dans la zone de recherche de hello, entrez un champ que vous souhaitez toofind, puis appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-130">In hello search box, enter a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="f6fb9-131">Lorsque vous commencez à taper, OMS affiche les correspondances possibles et les opérations que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-131">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> <span data-ttu-id="f6fb9-132">En savoir plus sur [comment toofind les données dans le journal Analytique](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="f6fb9-132">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   <span data-ttu-id="f6fb9-133">Cet exemple recherche des événements avec **Type=AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-133">This example searches for events with **Type=AzureDiagnostics**.</span></span>

   ![Commencer à taper la chaîne de requête](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. <span data-ttu-id="f6fb9-135">Dans la barre de gauche hello, choisissez hello laps de temps que vous souhaitez tooview.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-135">In hello left bar, choose hello timeframe that you want tooview.</span></span> <span data-ttu-id="f6fb9-136">tooadd une requête tooyour de filtre, choisissez **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-136">tooadd a filter tooyour query, choose **+Add**.</span></span>

   ![Ajouter le filtre tooquery](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. <span data-ttu-id="f6fb9-138">Sous **ajouter des filtres**, entrez le nom du filtre hello afin que vous puissiez rechercher hello du filtre.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-138">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="f6fb9-139">Sélectionnez le filtre de hello, puis choisissez **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-139">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="f6fb9-140">numéro de contrôle d’échange toofind hello cet exemple recherche le mot hello « échange » et sélectionne **event_record_messageProperties_interchangeControlNumber_s** comme filtre de hello.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-140">toofind hello interchange control number, this example searches for hello word "interchange", and selects **event_record_messageProperties_interchangeControlNumber_s** as hello filter.</span></span>

   ![Sélectionner le filtre](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. <span data-ttu-id="f6fb9-142">Dans la barre de gauche hello, sélectionnez valeur hello du filtre que vous souhaitez toouse, choisissez **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-142">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   <span data-ttu-id="f6fb9-143">Cet exemple sélectionne le numéro de contrôle d’échange hello pour les messages hello que nous voulons.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-143">This example selects hello interchange control number for hello messages we want.</span></span>

   ![Sélectionner une valeur de filtre](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. <span data-ttu-id="f6fb9-145">Requête toohello retournent désormais que vous générez.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-145">Now return toohello query that you're building.</span></span> <span data-ttu-id="f6fb9-146">Votre requête a été mise à jour avec l’événement et la valeur de filtre sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-146">Your query has been updated with your selected filter event and value.</span></span> <span data-ttu-id="f6fb9-147">Vos résultats précédents sont à présent également filtrés.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-147">Your previous results are now filtered too.</span></span>

    ![Retourne la requête tooyour résultats filtrés](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a><span data-ttu-id="f6fb9-149">Enregistrer votre requête pour un usage ultérieur</span><span class="sxs-lookup"><span data-stu-id="f6fb9-149">Save your query for future use</span></span>

1. <span data-ttu-id="f6fb9-150">À partir de votre requête sur hello **recherche de journal** choisissez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-150">From your query on hello **Log Search** page, choose **Save**.</span></span> <span data-ttu-id="f6fb9-151">Donnez un nom à votre requête, sélectionnez une catégorie, puis choisissez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-151">Give your query a name, select a category, and choose **Save**.</span></span>

   ![Donner un nom et une catégorie à votre requête](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. <span data-ttu-id="f6fb9-153">tooview votre requête, choisissez **favoris**.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-153">tooview your query, choose **Favorites**.</span></span>

   ![Choisir « Favoris »](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. <span data-ttu-id="f6fb9-155">Sous **recherches enregistrées**, sélectionnez votre requête afin que vous pouvez afficher les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-155">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="f6fb9-156">requête de hello tooupdate afin de trouver des résultats différents, modifier la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-156">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![Sélectionner votre requête](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a><span data-ttu-id="f6fb9-158">Rechercher et exécuter des requêtes enregistrées dans le portail Operations Management Suite de hello</span><span class="sxs-lookup"><span data-stu-id="f6fb9-158">Find and run saved queries in hello Operations Management Suite portal</span></span>

1. <span data-ttu-id="f6fb9-159">Ouvrez la page d’accueil de votre espace de travail OMS (`https://{your-workspace-name}.portal.mms.microsoft.com`), puis choisissez **Recherche dans les journaux**.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-159">Open your OMS workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and choose **Log Search**.</span></span>

   ![Dans votre page d’accueil d’OMS, choisissez « Recherche dans les journaux »](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="f6fb9-161">-ou-</span><span class="sxs-lookup"><span data-stu-id="f6fb9-161">-or-</span></span>

   ![Menu hello OMS, choisissez « Recherche de journal »](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. <span data-ttu-id="f6fb9-163">Sur hello **recherche de journal** page d’accueil, choisissez **favoris**.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-163">On hello **Log Search** home page, choose **Favorites**.</span></span>

   ![Choisir « Favoris »](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. <span data-ttu-id="f6fb9-165">Sous **recherches enregistrées**, sélectionnez votre requête afin que vous pouvez afficher les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-165">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="f6fb9-166">requête de hello tooupdate afin de trouver des résultats différents, modifier la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="f6fb9-166">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![Sélectionner votre requête](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a><span data-ttu-id="f6fb9-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f6fb9-168">Next steps</span></span>

* [<span data-ttu-id="f6fb9-169">Schémas de suivi AS2</span><span class="sxs-lookup"><span data-stu-id="f6fb9-169">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="f6fb9-170">Schémas de suivi X12</span><span class="sxs-lookup"><span data-stu-id="f6fb9-170">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="f6fb9-171">Schémas de suivi personnalisé</span><span class="sxs-lookup"><span data-stu-id="f6fb9-171">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)