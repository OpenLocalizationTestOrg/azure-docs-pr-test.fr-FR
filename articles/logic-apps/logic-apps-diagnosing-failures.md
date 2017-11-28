---
title: "Diagnostiquer des échecs - Azure Logic Apps | Microsoft Docs"
description: "Méthodes courantes pour comprendre les points de défaillance des applications logiques"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 814e6f93088cdd96b0a663d2a7494b5a11470d99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="3c78b-103">Diagnostiquer des échecs d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="3c78b-103">Diagnose logic app failures</span></span>
<span data-ttu-id="3c78b-104">Si vous rencontrez des problèmes ou des échecs avec vos applications logiques, certaines approches peuvent vous aider à mieux comprendre l’origine des défaillances.</span><span class="sxs-lookup"><span data-stu-id="3c78b-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where the failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="3c78b-105">Outils du Portail Azure</span><span class="sxs-lookup"><span data-stu-id="3c78b-105">Azure portal tools</span></span>
<span data-ttu-id="3c78b-106">Le Portail Azure fournit plusieurs outils permettant de diagnostiquer chaque application logique à différentes étapes.</span><span class="sxs-lookup"><span data-stu-id="3c78b-106">The Azure portal provides many tools to diagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="3c78b-107">Historique du déclencheur</span><span class="sxs-lookup"><span data-stu-id="3c78b-107">Trigger history</span></span>

<span data-ttu-id="3c78b-108">Chaque application logique comporte au moins un déclencheur.</span><span class="sxs-lookup"><span data-stu-id="3c78b-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="3c78b-109">Si vous constatez que les applications ne se déclenchent pas, commencez par consulter l’historique du déclencheur pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="3c78b-109">If you notice that apps aren't firing, look first at the trigger history for more information.</span></span> <span data-ttu-id="3c78b-110">Vous pouvez accéder à l’historique du déclencheur dans le panneau principal de l’application logique.</span><span class="sxs-lookup"><span data-stu-id="3c78b-110">You can access the trigger history on the logic app'ss main blade.</span></span>

![Emplacement de l’historique du déclencheur][1]

<span data-ttu-id="3c78b-112">L’historique du déclencheur répertorie tous les tentatives effectuées par le déclencheur de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="3c78b-112">The trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="3c78b-113">Vous pouvez cliquer sur chaque tentative du déclencheur pour explorer les détails, en particulier, les entrées ou sorties générées par la tentative du déclencheur.</span><span class="sxs-lookup"><span data-stu-id="3c78b-113">You can click each trigger attempt to drill into the details, specifically, any inputs or outputs that the trigger attempt generated.</span></span> <span data-ttu-id="3c78b-114">Si vous identifiez des déclencheurs ayant échoué, sélectionnez la tentative du déclencheur et choisissez le lien **Sorties** pour passer en revue les messages d’erreur générés, par exemple, indiquant des informations d’identification FTP non valides.</span><span class="sxs-lookup"><span data-stu-id="3c78b-114">If you find failed triggers, select the trigger attempt and choose the **Outputs** link to review any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="3c78b-115">Voici les différents états que vous pouvez voir :</span><span class="sxs-lookup"><span data-stu-id="3c78b-115">The different statuses you might see are:</span></span>

* <span data-ttu-id="3c78b-116">**Ignoré**.</span><span class="sxs-lookup"><span data-stu-id="3c78b-116">**Skipped**.</span></span> <span data-ttu-id="3c78b-117">Le point de terminaison a été interrogé pour vérifier les données et a reçu une réponse indiquant qu’aucune donnée n’était disponible.</span><span class="sxs-lookup"><span data-stu-id="3c78b-117">The endpoint was polled to check for data and received a response that no data was available.</span></span>
* <span data-ttu-id="3c78b-118">**Réussi**.</span><span class="sxs-lookup"><span data-stu-id="3c78b-118">**Succeeded**.</span></span> <span data-ttu-id="3c78b-119">Le déclencheur a reçu une réponse indiquant que les données étaient disponibles.</span><span class="sxs-lookup"><span data-stu-id="3c78b-119">The trigger received a response that data was available.</span></span> <span data-ttu-id="3c78b-120">Cet état peut provenir d’un déclencheur manuel, d’un déclencheur de périodicité ou d’un déclencheur d’interrogation.</span><span class="sxs-lookup"><span data-stu-id="3c78b-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="3c78b-121">Cet état est généralement accompagné d’un état **Déclenché**, sauf si vous avez une condition ou une commande SplitOn en mode Code qui n’a pas été satisfaite.</span><span class="sxs-lookup"><span data-stu-id="3c78b-121">This status is usually accompanied by the **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="3c78b-122">**Échec**.</span><span class="sxs-lookup"><span data-stu-id="3c78b-122">**Failed**.</span></span> <span data-ttu-id="3c78b-123">Une erreur a été générée.</span><span class="sxs-lookup"><span data-stu-id="3c78b-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="3c78b-124">Démarrer un déclencheur manuellement</span><span class="sxs-lookup"><span data-stu-id="3c78b-124">Start a trigger manually</span></span>

<span data-ttu-id="3c78b-125">Si vous souhaitez que l’application logique recherche immédiatement un déclencheur disponible (sans attendre la prochaine périodicité), vous pouvez cliquer sur **Sélectionner le déclencheur** dans le panneau principal pour forcer une vérification.</span><span class="sxs-lookup"><span data-stu-id="3c78b-125">If you want the logic app to check for an available trigger immediately without waiting for the next recurrence, click **Select Trigger** on the main blade to force a check.</span></span> <span data-ttu-id="3c78b-126">Par exemple, si vous cliquez sur ce lien avec un déclencheur Dropbox, le workflow interroge immédiatement Dropbox pour rechercher de nouveaux fichiers.</span><span class="sxs-lookup"><span data-stu-id="3c78b-126">For example, clicking this link with a Dropbox trigger causes the workflow to immediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="3c78b-127">Historique d’exécution</span><span class="sxs-lookup"><span data-stu-id="3c78b-127">Run history</span></span>

<span data-ttu-id="3c78b-128">Chaque déclenchement entraîne une exécution.</span><span class="sxs-lookup"><span data-stu-id="3c78b-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="3c78b-129">Vous pouvez accéder aux informations d’exécution dans le panneau principal, qui contient de nombreux détails pouvant vous aider à comprendre le déroulement du workflow.</span><span class="sxs-lookup"><span data-stu-id="3c78b-129">You can access run information from the main blade, which contains many details that can help you understand what happened during the workflow.</span></span>

![Emplacement de l’historique d’exécution][2]

<span data-ttu-id="3c78b-131">Une exécution affiche l’un des états suivants :</span><span class="sxs-lookup"><span data-stu-id="3c78b-131">A run displays one of the following statuses:</span></span>

* <span data-ttu-id="3c78b-132">**Réussi**.</span><span class="sxs-lookup"><span data-stu-id="3c78b-132">**Succeeded**.</span></span> <span data-ttu-id="3c78b-133">Toutes les actions ont réussi.</span><span class="sxs-lookup"><span data-stu-id="3c78b-133">All actions succeeded.</span></span> <span data-ttu-id="3c78b-134">Les éventuelles défaillances ont été corrigées par une action exécutée ultérieurement dans le workflow.</span><span class="sxs-lookup"><span data-stu-id="3c78b-134">If a failure happened, that failure was handled by an action that occurred later in the workflow.</span></span> <span data-ttu-id="3c78b-135">Autrement dit, la défaillance a été corrigée par une action configurée pour s’exécuter après l’échec d’une autre action.</span><span class="sxs-lookup"><span data-stu-id="3c78b-135">That is, the failure was handled by an action that was set to run after a failed action.</span></span>
* <span data-ttu-id="3c78b-136">**Échec**.</span><span class="sxs-lookup"><span data-stu-id="3c78b-136">**Failed**.</span></span> <span data-ttu-id="3c78b-137">Au moins une action a rencontré un échec qui n’a pas été traité par une action ultérieure dans le workflow.</span><span class="sxs-lookup"><span data-stu-id="3c78b-137">At least one action had a failure that was not handled by an action later in the workflow.</span></span>
* <span data-ttu-id="3c78b-138">**Annulé**.</span><span class="sxs-lookup"><span data-stu-id="3c78b-138">**Cancelled**.</span></span> <span data-ttu-id="3c78b-139">Le workflow était en cours d’exécution mais a reçu une demande d’annulation.</span><span class="sxs-lookup"><span data-stu-id="3c78b-139">The workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="3c78b-140">**Exécution en cours**.</span><span class="sxs-lookup"><span data-stu-id="3c78b-140">**Running**.</span></span> <span data-ttu-id="3c78b-141">Si un workflow est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="3c78b-141">The workflow is currently running.</span></span> <span data-ttu-id="3c78b-142">Cet état peut se produire pour les workflows limités ou en raison du plan de tarification actuel.</span><span class="sxs-lookup"><span data-stu-id="3c78b-142">This status might occur for throttled workflows, or because of the current pricing plan.</span></span> <span data-ttu-id="3c78b-143">Pour en savoir plus, consultez les [limites d’action sur la page de tarification](https://azure.microsoft.com/pricing/details/app-service/plans/).</span><span class="sxs-lookup"><span data-stu-id="3c78b-143">For details, see [action limits on the pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="3c78b-144">La configuration des diagnostics (les graphiques apparaissant en dessous de l’historique des exécutions) peut également fournir des informations sur les événements de limitation qui se produisent.</span><span class="sxs-lookup"><span data-stu-id="3c78b-144">Configuring diagnostics (the charts that appear under the run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="3c78b-145">Lorsque vous examinez un historique d’exécution, vous pouvez rechercher des détails supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="3c78b-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="3c78b-146">Sorties du déclencheur</span><span class="sxs-lookup"><span data-stu-id="3c78b-146">Trigger outputs</span></span>

<span data-ttu-id="3c78b-147">Les sorties du déclencheur affichent les données reçues du déclencheur.</span><span class="sxs-lookup"><span data-stu-id="3c78b-147">Trigger outputs show the data that came from the trigger.</span></span> <span data-ttu-id="3c78b-148">Ces sorties peuvent vous aider à déterminer si toutes les propriétés ont renvoyé les valeurs attendues.</span><span class="sxs-lookup"><span data-stu-id="3c78b-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="3c78b-149">Si vous rencontrez un contenu que vous ne comprenez pas, découvrez comment Azure Logic Apps [gère les différents types de contenu](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="3c78b-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![Exemples de sorties du déclencheur][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="3c78b-151">Entrées et sorties d’actions</span><span class="sxs-lookup"><span data-stu-id="3c78b-151">Action inputs and outputs</span></span>

<span data-ttu-id="3c78b-152">Vous pouvez explorer les entrées et sorties associées à une action.</span><span class="sxs-lookup"><span data-stu-id="3c78b-152">You can drill into the inputs and outputs that an action received.</span></span> <span data-ttu-id="3c78b-153">Ces données sont utiles pour comprendre la taille et la forme des sorties, mais aussi pour identifier les messages d’erreur susceptibles d’avoir été générés.</span><span class="sxs-lookup"><span data-stu-id="3c78b-153">This data is useful for understanding the size and shape of the outputs, and also for finding any error messages that might have been generated.</span></span>

![Entrées et sorties d’actions][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="3c78b-155">Déboguer le runtime du workflow</span><span class="sxs-lookup"><span data-stu-id="3c78b-155">Debug workflow runtime</span></span>

<span data-ttu-id="3c78b-156">En plus du contrôle des entrées, des sorties et des déclencheurs d’une exécution, vous pouvez ajouter des étapes à un workflow pour faciliter le débogage.</span><span class="sxs-lookup"><span data-stu-id="3c78b-156">Along with monitoring the inputs, outputs, and triggers of a run, you could add some steps to a workflow that help with debugging.</span></span> 
<span data-ttu-id="3c78b-157">[RequestBin](http://requestb.in) est un outil puissant que vous pouvez ajouter en tant qu’étape d’un workflow.</span><span class="sxs-lookup"><span data-stu-id="3c78b-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="3c78b-158">À l’aide de RequestBin, vous configurez un inspecteur de requête HTTP qui détermine précisément la taille, la forme et le format d’une requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="3c78b-158">By using RequestBin, you can set up an HTTP request inspector to determine the exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="3c78b-159">Vous pouvez créer un élément RequestBin et coller l’URL dans une action HTTP POST de l’application logique avec le contenu du corps que vous voulez tester (par exemple, une expression ou une autre sortie de l’étape).</span><span class="sxs-lookup"><span data-stu-id="3c78b-159">You can create a RequestBin and paste the URL in a logic app HTTP POST action with body content that you want to test, for example, an expression or another step output.</span></span> <span data-ttu-id="3c78b-160">Après avoir exécuté l’application logique, vous actualisez votre élément RequestBin pour voir comment la requête a été formée lors de sa génération à partir du moteur Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="3c78b-160">After you run the logic app, you can refresh your RequestBin to see how the request was formed when generated from the Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
