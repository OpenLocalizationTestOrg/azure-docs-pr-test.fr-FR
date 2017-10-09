---
title: "échecs d’aaaDiagnose - Azure Logic Apps | Documents Microsoft"
description: "Common toounderstand façons échouent où les applications de logique"
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
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="db06f-103">Diagnostiquer des échecs d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="db06f-103">Diagnose logic app failures</span></span>
<span data-ttu-id="db06f-104">Si vous rencontrez des problèmes ou défaillances de vos applications logiques, il existe quelques approches peuvent vous aider à mieux comprendre la provenant des échecs de hello.</span><span class="sxs-lookup"><span data-stu-id="db06f-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where hello failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="db06f-105">Outils du Portail Azure</span><span class="sxs-lookup"><span data-stu-id="db06f-105">Azure portal tools</span></span>
<span data-ttu-id="db06f-106">Hello portail Azure fournit de nombreux outils toodiagnose chaque application logique à chaque étape.</span><span class="sxs-lookup"><span data-stu-id="db06f-106">hello Azure portal provides many tools toodiagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="db06f-107">Historique du déclencheur</span><span class="sxs-lookup"><span data-stu-id="db06f-107">Trigger history</span></span>

<span data-ttu-id="db06f-108">Chaque application logique comporte au moins un déclencheur.</span><span class="sxs-lookup"><span data-stu-id="db06f-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="db06f-109">Si vous remarquez que les applications ne sont pas déclencher, recherchez la première historique de déclencheur hello pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="db06f-109">If you notice that apps aren't firing, look first at hello trigger history for more information.</span></span> <span data-ttu-id="db06f-110">Vous pouvez accéder à l’historique de déclencheur hello sur le panneau de hello logique app'ss principal.</span><span class="sxs-lookup"><span data-stu-id="db06f-110">You can access hello trigger history on hello logic app'ss main blade.</span></span>

![Localisation de l’historique de déclencheur hello][1]

<span data-ttu-id="db06f-112">historique de déclencheur Hello répertorie toutes les tentatives de déclencheur effectuée par votre application logique.</span><span class="sxs-lookup"><span data-stu-id="db06f-112">hello trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="db06f-113">Vous pouvez cliquer sur chaque toodrill de la tentative de déclencheur dans les détails de hello, plus précisément, les entrées ou les sorties qui hello tentative de déclencheur généré.</span><span class="sxs-lookup"><span data-stu-id="db06f-113">You can click each trigger attempt toodrill into hello details, specifically, any inputs or outputs that hello trigger attempt generated.</span></span> <span data-ttu-id="db06f-114">Si vous trouvez des déclencheurs ayant échouées, sélectionnez la tentative de déclencheur hello et choisissez hello **sorties** lien tooreview tout générée message d’erreur, par exemple, pour les informations d’identification FTP qui ne sont pas valides.</span><span class="sxs-lookup"><span data-stu-id="db06f-114">If you find failed triggers, select hello trigger attempt and choose hello **Outputs** link tooreview any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="db06f-115">Vous pouvez voir des états différents de Hello sont :</span><span class="sxs-lookup"><span data-stu-id="db06f-115">hello different statuses you might see are:</span></span>

* <span data-ttu-id="db06f-116">**Ignoré**.</span><span class="sxs-lookup"><span data-stu-id="db06f-116">**Skipped**.</span></span> <span data-ttu-id="db06f-117">point de terminaison Hello a été toocheck interrogée pour les données et a reçu une réponse qu’aucune donnée n’est disponible.</span><span class="sxs-lookup"><span data-stu-id="db06f-117">hello endpoint was polled toocheck for data and received a response that no data was available.</span></span>
* <span data-ttu-id="db06f-118">**Réussi**.</span><span class="sxs-lookup"><span data-stu-id="db06f-118">**Succeeded**.</span></span> <span data-ttu-id="db06f-119">déclencheur de Hello a reçu une réponse que les données étaient disponibles.</span><span class="sxs-lookup"><span data-stu-id="db06f-119">hello trigger received a response that data was available.</span></span> <span data-ttu-id="db06f-120">Cet état peut provenir d’un déclencheur manuel, d’un déclencheur de périodicité ou d’un déclencheur d’interrogation.</span><span class="sxs-lookup"><span data-stu-id="db06f-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="db06f-121">Cet état est généralement accompagné par hello **déclenché** état, mais peut-être ne pas si vous avez une condition ou une commande de SplitOn en mode code qui n’a pas été satisfaite.</span><span class="sxs-lookup"><span data-stu-id="db06f-121">This status is usually accompanied by hello **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="db06f-122">**Échec**.</span><span class="sxs-lookup"><span data-stu-id="db06f-122">**Failed**.</span></span> <span data-ttu-id="db06f-123">Une erreur a été générée.</span><span class="sxs-lookup"><span data-stu-id="db06f-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="db06f-124">Démarrer un déclencheur manuellement</span><span class="sxs-lookup"><span data-stu-id="db06f-124">Start a trigger manually</span></span>

<span data-ttu-id="db06f-125">Si vous souhaitez toocheck d’application hello logique pour un déclencheur disponible immédiatement, sans attendre la prochaine récurrence de hello, cliquez sur **sélectionner le déclencheur** sur hello panneau principal tooforce une vérification.</span><span class="sxs-lookup"><span data-stu-id="db06f-125">If you want hello logic app toocheck for an available trigger immediately without waiting for hello next recurrence, click **Select Trigger** on hello main blade tooforce a check.</span></span> <span data-ttu-id="db06f-126">Par exemple, en cliquant sur ce lien avec un déclencheur d’échange, hello workflow tooimmediately interrogez Dropbox de nouveaux fichiers.</span><span class="sxs-lookup"><span data-stu-id="db06f-126">For example, clicking this link with a Dropbox trigger causes hello workflow tooimmediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="db06f-127">Historique d’exécution</span><span class="sxs-lookup"><span data-stu-id="db06f-127">Run history</span></span>

<span data-ttu-id="db06f-128">Chaque déclenchement entraîne une exécution.</span><span class="sxs-lookup"><span data-stu-id="db06f-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="db06f-129">Vous pouvez accéder à des informations d’exécution à partir du panneau principal hello, qui contient de nombreuses informations qui peuvent vous aider à comprendre le déroulement du flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="db06f-129">You can access run information from hello main blade, which contains many details that can help you understand what happened during hello workflow.</span></span>

![Localisation hello l’historique d’exécution][2]

<span data-ttu-id="db06f-131">Une série de tests affiche l’un des hello suivant des États :</span><span class="sxs-lookup"><span data-stu-id="db06f-131">A run displays one of hello following statuses:</span></span>

* <span data-ttu-id="db06f-132">**Réussi**.</span><span class="sxs-lookup"><span data-stu-id="db06f-132">**Succeeded**.</span></span> <span data-ttu-id="db06f-133">Toutes les actions ont réussi.</span><span class="sxs-lookup"><span data-stu-id="db06f-133">All actions succeeded.</span></span> <span data-ttu-id="db06f-134">Si une erreur s’est produite, cet échec a été géré par une action qui s’est produite plus loin dans le flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="db06f-134">If a failure happened, that failure was handled by an action that occurred later in hello workflow.</span></span> <span data-ttu-id="db06f-135">Autrement dit, Échec de hello était traitée par une action qui a été définie toorun après une action qui a échoué.</span><span class="sxs-lookup"><span data-stu-id="db06f-135">That is, hello failure was handled by an action that was set toorun after a failed action.</span></span>
* <span data-ttu-id="db06f-136">**Échec**.</span><span class="sxs-lookup"><span data-stu-id="db06f-136">**Failed**.</span></span> <span data-ttu-id="db06f-137">Au moins une action a eu une défaillance qui n’a pas été gérée par une action plus loin dans le flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="db06f-137">At least one action had a failure that was not handled by an action later in hello workflow.</span></span>
* <span data-ttu-id="db06f-138">**Annulé**.</span><span class="sxs-lookup"><span data-stu-id="db06f-138">**Cancelled**.</span></span> <span data-ttu-id="db06f-139">flux de travail Hello était en cours d’exécution, mais a reçu une demande d’annulation.</span><span class="sxs-lookup"><span data-stu-id="db06f-139">hello workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="db06f-140">**Exécution en cours**.</span><span class="sxs-lookup"><span data-stu-id="db06f-140">**Running**.</span></span> <span data-ttu-id="db06f-141">flux de travail Hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="db06f-141">hello workflow is currently running.</span></span> <span data-ttu-id="db06f-142">Cet état peut se produire pour les workflows d’accélérée, ou en raison de hello actuel de plan de tarification.</span><span class="sxs-lookup"><span data-stu-id="db06f-142">This status might occur for throttled workflows, or because of hello current pricing plan.</span></span> <span data-ttu-id="db06f-143">Pour plus d’informations, consultez [limites d’action sur la page de tarification de hello](https://azure.microsoft.com/pricing/details/app-service/plans/).</span><span class="sxs-lookup"><span data-stu-id="db06f-143">For details, see [action limits on hello pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="db06f-144">Configuration des diagnostics (graphiques hello qui apparaissent sous l’historique d’exécution de hello) peut également fournir plus d’informations sur les événements de limitation de bande passante qui se produisent.</span><span class="sxs-lookup"><span data-stu-id="db06f-144">Configuring diagnostics (hello charts that appear under hello run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="db06f-145">Lorsque vous examinez un historique d’exécution, vous pouvez rechercher des détails supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="db06f-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="db06f-146">Sorties du déclencheur</span><span class="sxs-lookup"><span data-stu-id="db06f-146">Trigger outputs</span></span>

<span data-ttu-id="db06f-147">Déclencheur génère des données hello provient d’un déclencheur de hello.</span><span class="sxs-lookup"><span data-stu-id="db06f-147">Trigger outputs show hello data that came from hello trigger.</span></span> <span data-ttu-id="db06f-148">Ces sorties peuvent vous aider à déterminer si toutes les propriétés ont renvoyé les valeurs attendues.</span><span class="sxs-lookup"><span data-stu-id="db06f-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="db06f-149">Si vous rencontrez un contenu que vous ne comprenez pas, découvrez comment Azure Logic Apps [gère les différents types de contenu](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="db06f-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![Exemples de sorties du déclencheur][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="db06f-151">Entrées et sorties d’actions</span><span class="sxs-lookup"><span data-stu-id="db06f-151">Action inputs and outputs</span></span>

<span data-ttu-id="db06f-152">Vous pouvez explorer les entrées hello et sorties reçue d’une action.</span><span class="sxs-lookup"><span data-stu-id="db06f-152">You can drill into hello inputs and outputs that an action received.</span></span> <span data-ttu-id="db06f-153">Ces données sont utiles pour comprendre la taille de hello et la forme de sorties de hello et également pour rechercher des messages d’erreur qui ont été générées.</span><span class="sxs-lookup"><span data-stu-id="db06f-153">This data is useful for understanding hello size and shape of hello outputs, and also for finding any error messages that might have been generated.</span></span>

![Entrées et sorties d’actions][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="db06f-155">Déboguer le runtime du workflow</span><span class="sxs-lookup"><span data-stu-id="db06f-155">Debug workflow runtime</span></span>

<span data-ttu-id="db06f-156">En même temps que l’analyse hello entrées, sorties et les déclencheurs d’une exécution, vous pouvez ajouter certains flux de travail tooa étapes aider au débogage.</span><span class="sxs-lookup"><span data-stu-id="db06f-156">Along with monitoring hello inputs, outputs, and triggers of a run, you could add some steps tooa workflow that help with debugging.</span></span> 
<span data-ttu-id="db06f-157">[RequestBin](http://requestb.in) est un outil puissant que vous pouvez ajouter en tant qu’étape d’un workflow.</span><span class="sxs-lookup"><span data-stu-id="db06f-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="db06f-158">À l’aide de RequestBin, vous pouvez configurer un inspecteur toodetermine hello exacte taille des requêtes HTTP, la forme et le format d’une requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="db06f-158">By using RequestBin, you can set up an HTTP request inspector toodetermine hello exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="db06f-159">Vous pouvez créer un RequestBin et coller des URL de hello dans une action de publication HTTP avec le contenu du corps que vous souhaitez tootest, par exemple, une expression ou une autre sortie de l’étape d’application logique.</span><span class="sxs-lookup"><span data-stu-id="db06f-159">You can create a RequestBin and paste hello URL in a logic app HTTP POST action with body content that you want tootest, for example, an expression or another step output.</span></span> <span data-ttu-id="db06f-160">Après avoir exécuté l’application logique de hello, vous pouvez actualiser votre toosee RequestBin la demande de hello formée lors de la génération à partir du moteur de Logic Apps hello.</span><span class="sxs-lookup"><span data-stu-id="db06f-160">After you run hello logic app, you can refresh your RequestBin toosee how hello request was formed when generated from hello Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
