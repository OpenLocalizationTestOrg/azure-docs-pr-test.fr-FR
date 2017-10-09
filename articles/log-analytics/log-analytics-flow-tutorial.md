---
title: aaaAutomate Analytique de journal Azure traite avec Microsoft Flow
description: "Découvrez comment vous pouvez utiliser Microsoft Flow tooquickly automatiser des processus reproductibles à l’aide du connecteur d’Analytique des journaux Azure hello."
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="71f9d-103">Automatiser les processus d’Analytique de journal avec le connecteur de hello pour Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="71f9d-103">Automate Log Analytics processes with hello connector for Microsoft Flow</span></span>
<span data-ttu-id="71f9d-104">[Microsoft Flow](https://ms.flow.microsoft.com) vous permet de toocreate automatisée de flux de travail à l’aide des centaines d’actions pour une multitude de services.</span><span class="sxs-lookup"><span data-stu-id="71f9d-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you toocreate automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="71f9d-105">Sortie d’une action peut être utilisée en tant que tooanother d’entrée, ce qui permet une intégration toocreate entre différents services.</span><span class="sxs-lookup"><span data-stu-id="71f9d-105">Output from one action can be used as input tooanother allowing you toocreate integration between different services.</span></span>  <span data-ttu-id="71f9d-106">connecteur d’Analytique des journaux Azure Hello pour Microsoft Flow vous permettent aux workflows toobuild qui incluent des données récupérées par les recherches de journal dans le journal Analytique.</span><span class="sxs-lookup"><span data-stu-id="71f9d-106">hello Azure Log Analytics connector for Microsoft Flow allow you toobuild workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="71f9d-107">Par exemple, vous pouvez utiliser des données de journal Analytique Microsoft Flow toouse dans une notification par courrier électronique à partir d’Office 365, créer un bogue dans Visual Studio Team Services ou publier un message de marge.</span><span class="sxs-lookup"><span data-stu-id="71f9d-107">For example, you can use Microsoft Flow toouse Log Analytics data in an email notification from Office 365, create a bug in Visual Studio Team Services, or post a Slack message.</span></span>  <span data-ttu-id="71f9d-108">Vous pouvez déclencher un flux de travail à l’aide d’un calendrier ou d’une action d’un service connecté, telle que la réception d’un e-mail ou d’un tweet.</span><span class="sxs-lookup"><span data-stu-id="71f9d-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  


> [!NOTE]
> <span data-ttu-id="71f9d-109">connecteur d’Analytique des journaux Azure Hello pour Microsoft Flow nécessite votre espace de travail mis à niveau de toobe toohello nouveau Analytique de journal langage de requête.</span><span class="sxs-lookup"><span data-stu-id="71f9d-109">hello Azure Log Analytics connector for Microsoft Flow requires your workspace toobe upgraded toohello new Log Analytics query language.</span></span> <span data-ttu-id="71f9d-110">Vous pouvez en savoir plus sur le nouveau langage de hello et obtenir hello procédure tooupgrade votre espace de travail à [mise à niveau de votre recherche de journal toonew espace de travail Analytique des journaux Azure](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="71f9d-110">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  

<span data-ttu-id="71f9d-111">didacticiel Hello dans cet article vous montre comment toocreate un flux qui envoie automatiquement hello les résultats d’une recherche de journal Analytique de journal par courrier électronique, qu’un exemple de comment vous pouvez utiliser le journal Analytique dans Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="71f9d-111">hello tutorial in this article shows you how toocreate a flow that automatically sends hello results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="71f9d-112">Étape 1 : Créer un flux</span><span class="sxs-lookup"><span data-stu-id="71f9d-112">Step 1: Create a flow</span></span>
1. <span data-ttu-id="71f9d-113">Connectez-vous trop[Microsoft Flow](http://flow.microsoft.com), puis sélectionnez **flux Mes**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-113">Sign in too[Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="71f9d-114">Cliquez sur **+ Créer entièrement**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-114">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="71f9d-115">Étape 2 : Créer un déclencheur pour votre flux</span><span class="sxs-lookup"><span data-stu-id="71f9d-115">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="71f9d-116">Cliquez sur **Rechercher dans l’ensemble des connecteurs et des déclencheurs**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-116">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="71f9d-117">Type **planification** dans la zone de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="71f9d-117">Type **Schedule** in hello search box.</span></span>
3. <span data-ttu-id="71f9d-118">Sélectionnez **Planifier**, puis **Planification - Récurrence**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-118">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="71f9d-119">Bonjour **fréquence** zone Sélectionnez **jour** et Bonjour **intervalle** , entrez **1**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-119">In hello **Frequency** box select **Day** and in hello **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="71f9d-120">![Boîte de dialogue du déclencheur Microsoft Flow](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="71f9d-120">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="71f9d-121">Étape 3 : Ajouter une action Log Analytics</span><span class="sxs-lookup"><span data-stu-id="71f9d-121">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="71f9d-122">Cliquez sur **+ Nouvelle étape**, puis sur **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-122">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="71f9d-123">Recherchez **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-123">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="71f9d-124">Cliquez sur **Azure Log Analytics – Exécuter la requête et visualiser les résultats**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-124">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="71f9d-125">![Fenêtre d’exécution de la requête Log Analytics](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="71f9d-125">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-hello-log-analytics-action"></a><span data-ttu-id="71f9d-126">Étape 4 : Configurer l’action d’Analytique de journal hello</span><span class="sxs-lookup"><span data-stu-id="71f9d-126">Step 4: Configure hello Log Analytics action</span></span>

1. <span data-ttu-id="71f9d-127">Spécifiez les détails de hello pour votre espace de travail, y compris hello abonnement ID, groupe de ressources et le nom de l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="71f9d-127">Specify hello details for your workspace including hello Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="71f9d-128">Ajouter hello suivant Analytique de journal requête toohello **requête** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="71f9d-128">Add hello following Log Analytics query toohello **Query** window.</span></span>  <span data-ttu-id="71f9d-129">Ceci est un exemple de requête. Vous pouvez donc la remplacer par n’importe quelle autre requête retournant des données.</span><span class="sxs-lookup"><span data-stu-id="71f9d-129">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. <span data-ttu-id="71f9d-130">Sélectionnez **HTML Table** pour hello **Type de graphique**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-130">Select **HTML Table** for hello **Chart Type**.</span></span><br><br><span data-ttu-id="71f9d-131">![Action Log Analytics](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="71f9d-131">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-hello-flow-toosend-email"></a><span data-ttu-id="71f9d-132">Étape 5 : Configurer la messagerie de hello flux toosend</span><span class="sxs-lookup"><span data-stu-id="71f9d-132">Step 5: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="71f9d-133">Cliquez sur **Nouvelle étape**, puis sur **+ Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-133">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="71f9d-134">Recherchez **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-134">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="71f9d-135">Cliquez sur **Office 365 Outlook – Envoyer un message électronique**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-135">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="71f9d-136">![Fenêtre de sélection d’Office 365 Outlook](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="71f9d-136">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="71f9d-137">Spécifiez l’adresse de messagerie hello d’un destinataire Bonjour **à** fenêtre et un objet de messagerie hello dans **sujet**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-137">Specify hello email address of a recipient in hello **To** window and a subject for hello email in **Subject**.</span></span>
5. <span data-ttu-id="71f9d-138">Cliquez n’importe où dans hello **corps** boîte.</span><span class="sxs-lookup"><span data-stu-id="71f9d-138">Click anywhere in hello **Body** box.</span></span>  <span data-ttu-id="71f9d-139">La fenêtre **Contenu dynamique** s’ouvre avec les valeurs des actions précédentes.</span><span class="sxs-lookup"><span data-stu-id="71f9d-139">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="71f9d-140">Sélectionnez **Corps**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-140">Select **Body**.</span></span>  <span data-ttu-id="71f9d-141">Il s’agit de résultats hello de requête hello Bonjour action d’Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="71f9d-141">This is hello results of hello query in hello Log Analytics action.</span></span>
6. <span data-ttu-id="71f9d-142">Cliquez sur **Afficher les options avancées**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-142">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="71f9d-143">Bonjour **HTML** boîte, sélectionnez **Oui**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-143">In hello **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="71f9d-144">![Fenêtre de configuration d’e-mail Office 365](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="71f9d-144">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="71f9d-145">Étape 6 : Enregistrer et tester votre flux</span><span class="sxs-lookup"><span data-stu-id="71f9d-145">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="71f9d-146">Bonjour **nom de flux** zone, ajouter un nom pour votre flux, puis cliquez sur **créer un flux**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-146">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="71f9d-147">![Enregistrer le flux](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="71f9d-147">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="71f9d-148">flux de Hello est maintenant créé et s’exécute après un jour planification hello spécifiée.</span><span class="sxs-lookup"><span data-stu-id="71f9d-148">hello flow is now created and will run after a day which is hello schedule you specified.</span></span> 
3. <span data-ttu-id="71f9d-149">flux de hello tooimmediately test, cliquez sur **exécuter maintenant** , puis **exécuter flux**.</span><span class="sxs-lookup"><span data-stu-id="71f9d-149">tooimmediately test hello flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="71f9d-150">![Exécuter le flux](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="71f9d-150">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="71f9d-151">Lorsque les flux hello est terminée, vérifiez les messages hello du destinataire hello que vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="71f9d-151">When hello flow completes, check hello mail of hello recipient that you specified.</span></span>  <span data-ttu-id="71f9d-152">Vous devez avoir reçu un message électronique avec une similaire toohello suivant du corps :</span><span class="sxs-lookup"><span data-stu-id="71f9d-152">You should have received a mail with a body similar toohello following:</span></span><br><br>![Exemple de message électronique](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="71f9d-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="71f9d-154">Next steps</span></span>

- <span data-ttu-id="71f9d-155">En savoir plus sur les [recherches dans les journaux avec Log Analytics](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="71f9d-155">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="71f9d-156">Découvrez [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="71f9d-156">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



