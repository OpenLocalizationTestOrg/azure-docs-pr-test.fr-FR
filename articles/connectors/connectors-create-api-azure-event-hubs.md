---
title: "aaaSet le moniteur d’événement avec des concentrateurs d’événements Azure pour Azure Logic Apps | Documents Microsoft"
description: "Surveiller les événements de tooreceive de flux de données et d’envoyer des événements pour les applications de la logique d’Azure avec Azure Event Hubs"
services: logic-apps
keywords: "flux de données, observateur d’événements, event hubs"
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a><span data-ttu-id="43aa4-104">Surveiller, recevoir et envoyer des événements avec le connecteur de concentrateurs d’événements hello</span><span class="sxs-lookup"><span data-stu-id="43aa4-104">Monitor, receive, and send events with hello Event Hubs connector</span></span>

<span data-ttu-id="43aa4-105">tooset d’un observateur d’événements afin que votre application logique peut détecter les événements de recevoir des événements et envoyer des événements, connecter tooan [concentrateur d’événements Azure](https://azure.microsoft.com/services/event-hubs) à partir de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="43aa4-105">tooset up an event monitor so that your logic app can detect events, receive events, and send events, connect tooan [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="43aa4-106">En savoir plus sur [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="43aa4-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="43aa4-107">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="43aa4-107">Requirements</span></span>

* <span data-ttu-id="43aa4-108">Vous avez toohave un [espace de noms de concentrateurs d’événements et de concentrateur d’événements](../event-hubs/event-hubs-create.md) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="43aa4-108">You have toohave an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="43aa4-109">En savoir plus [comment toocreate un espace de noms de concentrateurs d’événements et d’un concentrateur d’événements](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="43aa4-109">Learn [how toocreate an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="43aa4-110">toouse [n’importe quel connecteur](https://docs.microsoft.com/azure/connectors/apis-list) dans votre logique d’application, vous avez toocreate une logique application tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="43aa4-110">toouse [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have toocreate a logic app first.</span></span> <span data-ttu-id="43aa4-111">En savoir plus [comment une application de la logique de toocreate](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="43aa4-111">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a><span data-ttu-id="43aa4-112">Vérifier les autorisations d’espace de noms de concentrateurs d’événements et recherchez la chaîne de connexion hello</span><span class="sxs-lookup"><span data-stu-id="43aa4-112">Check Event Hubs namespace permissions and find hello connection string</span></span>

<span data-ttu-id="43aa4-113">Pour votre tooaccess d’application logique, un service, vous avez toocreate un [ *connexion* ](./connectors-overview.md) entre votre logique application hello service et, si vous n’avez pas déjà.</span><span class="sxs-lookup"><span data-stu-id="43aa4-113">For your logic app tooaccess any service, you have toocreate a [*connection*](./connectors-overview.md) between your logic app and hello service, if you haven't already.</span></span> <span data-ttu-id="43aa4-114">Cette connexion autorise de vos données tooaccess d’application logique.</span><span class="sxs-lookup"><span data-stu-id="43aa4-114">This connection authorizes your logic app tooaccess data.</span></span>
<span data-ttu-id="43aa4-115">Pour votre tooaccess d’application logique votre concentrateur d’événements, vous avez toohave **gérer** autorisations et la chaîne de connexion de hello pour votre espace de noms de concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="43aa4-115">For your logic app tooaccess your Event Hub, you have toohave **Manage** permissions and hello connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="43aa4-116">toocheck vos autorisations et la chaîne de connexion get hello, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="43aa4-116">toocheck your permissions and get hello connection string, follow these steps.</span></span>

1.  <span data-ttu-id="43aa4-117">Connectez-vous à toohello [portail Azure](https://portal.azure.com "portail Azure").</span><span class="sxs-lookup"><span data-stu-id="43aa4-117">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="43aa4-118">Passez les concentrateurs d’événements tooyour *espace de noms*, pas hello concentrateur d’événements spécifique.</span><span class="sxs-lookup"><span data-stu-id="43aa4-118">Go tooyour Event Hubs *namespace*, not hello specific Event Hub.</span></span> <span data-ttu-id="43aa4-119">Sur le panneau espace de noms de hello, sous **paramètres**, choisissez **les stratégies d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="43aa4-119">On hello namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="43aa4-120">Sous **Revendications**, vérifiez que vous disposez des autorisations **Gérer** pour cet espace de noms.</span><span class="sxs-lookup"><span data-stu-id="43aa4-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![Gérer les autorisations pour votre espace de noms Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="43aa4-122">chaîne de connexion toocopy hello pour l’espace de noms du service Event Hubs hello, choisissez **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="43aa4-122">toocopy hello connection string for hello Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="43aa4-123">Tooyour suivant principal clé de chaîne de connexion, choisissez le bouton de copie hello.</span><span class="sxs-lookup"><span data-stu-id="43aa4-123">Next tooyour primary key connection string, choose hello copy button.</span></span>

    ![Copier la chaîne de connexion d’espace de noms Event Hubs](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="43aa4-125">tooconfirm si votre chaîne de connexion est associé à votre espace de noms de concentrateurs d’événements ou à un concentrateur d’événements spécifiques, vérifiez la chaîne de connexion hello pour hello `EntityPath` paramètre.</span><span class="sxs-lookup"><span data-stu-id="43aa4-125">tooconfirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check hello connection string for hello `EntityPath` parameter.</span></span> <span data-ttu-id="43aa4-126">Si vous trouvez pas ce paramètre, chaîne de connexion hello est pour un concentrateur d’événements « entité » spécifique et n’est pas toouse de bonne chaîne hello avec votre application logique.</span><span class="sxs-lookup"><span data-stu-id="43aa4-126">If you find this parameter, hello connection string is for a specific Event Hub "entity", and is not hello correct string toouse with your logic app.</span></span>

4.  <span data-ttu-id="43aa4-127">Maintenant lorsque vous êtes invité à entrer pour les informations d’identification après l’ajout d’une application de la logique de tooyour déclencheur ou une action concentrateurs d’événements, vous pouvez vous connecter à espace de noms tooyour concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="43aa4-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action tooyour logic app, you can connect tooyour Event Hubs namespace.</span></span> <span data-ttu-id="43aa4-128">Donnez un nom à votre connexion, entrez la chaîne de connexion hello que vous avez copié, choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="43aa4-128">Give your connection a name, enter hello connection string that you copied, and choose **Create**.</span></span>

    ![Entrer la chaîne de connexion pour un espace de noms Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="43aa4-130">Après avoir créé votre connexion, nom de la connexion hello doit apparaître dans hello concentrateurs d’événements déclencheur ou une action.</span><span class="sxs-lookup"><span data-stu-id="43aa4-130">After you create your connection, hello connection name should appear in hello Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="43aa4-131">Vous pouvez ensuite poursuivre hello les autres étapes de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="43aa4-131">You can then continue with hello other steps in your logic app.</span></span>

    ![Connexion d’espace de noms Event Hubs créée](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="43aa4-133">Démarrer le workflow lorsque votre hub Event Hubs reçoit de nouveaux événements</span><span class="sxs-lookup"><span data-stu-id="43aa4-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="43aa4-134">Un [*déclencheur*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) désigne un événement qui démarre un workflow dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="43aa4-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="43aa4-135">Pour démarrer un flux de travail lorsque de nouveaux événements sont envoyés tooyour concentrateur d’événements, procédez comme suit pour ajouter le déclencheur hello qui détecte cet événement.</span><span class="sxs-lookup"><span data-stu-id="43aa4-135">To start a workflow when new events are sent tooyour Event Hub, follow these steps for adding hello trigger that detects this event.</span></span>

1.  <span data-ttu-id="43aa4-136">Bonjour [portail Azure](https://portal.azure.com "portail Azure"), accédez tooyour les application logique existante ou créer une application de logique vide.</span><span class="sxs-lookup"><span data-stu-id="43aa4-136">In hello [Azure portal](https://portal.azure.com "Azure portal"), go tooyour existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="43aa4-137">Dans la zone de recherche hello hello Concepteur d’application logique, entrez `event hubs` pour votre filtre.</span><span class="sxs-lookup"><span data-stu-id="43aa4-137">In hello search box for hello Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="43aa4-138">Sélectionnez ce déclencheur : **When events are available in Event Hub (Lorsque les événements sont disponibles dans un hub Event Hubs)**</span><span class="sxs-lookup"><span data-stu-id="43aa4-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![Sélectionner le déclencheur lorsque votre hub Event Hubs reçoit de nouveaux événements](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="43aa4-140">Si vous ne disposez pas d’un espace de noms de connexion tooyour concentrateurs d’événements, vous êtes invité à entrer toocreate maintenant cette connexion.</span><span class="sxs-lookup"><span data-stu-id="43aa4-140">If you don't already have a connection tooyour Event Hubs namespace, you're prompted toocreate this connection now.</span></span> <span data-ttu-id="43aa4-141">Donnez un nom à votre connexion et entrez la chaîne de connexion hello pour votre espace de noms de concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="43aa4-141">Give your connection a name, and enter hello connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="43aa4-142">Si nécessaire, en savoir plus [comment toofind votre chaîne de connexion](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="43aa4-142">If necessary, learn [how toofind your connection string](#permissions-connection-string).</span></span>

    ![Entrer la chaîne de connexion pour un espace de noms Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="43aa4-144">Après avoir créé la connexion de hello, hello paramètres pour hello **lorsqu’un événement dans disponibles dans un concentrateur d’événements** déclencheur s’affichent.</span><span class="sxs-lookup"><span data-stu-id="43aa4-144">After you create hello connection, hello settings for hello **When an event in available in an Event Hub** trigger appear.</span></span>

    ![Paramètres du déclencheur lorsque votre hub Event Hubs reçoit de nouveaux événements](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="43aa4-146">Entrez ou sélectionnez le nom de hello pour hello concentrateur d’événements que vous souhaitez toomonitor.</span><span class="sxs-lookup"><span data-stu-id="43aa4-146">Enter or select hello name for hello Event Hub that you want toomonitor.</span></span> <span data-ttu-id="43aa4-147">Sélectionnez la fréquence de hello et l’intervalle pour la fréquence à laquelle vous voulez toocheck hello concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="43aa4-147">Select hello frequency and interval for how often you want toocheck hello Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="43aa4-148">toooptionally sélectionner un groupe de consommateurs pour la lecture des événements, choisissez **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="43aa4-148">toooptionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![Spécifier un hub Event Hubs ou un groupe de consommateurs](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="43aa4-150">Vous avez maintenant configuré un toostart déclencheur un flux de travail pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="43aa4-150">You've now set up a trigger toostart a workflow for your logic app.</span></span> 
    <span data-ttu-id="43aa4-151">Votre application logique vérifie hello spécifié concentrateur d’événements selon une planification hello que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="43aa4-151">Your logic app checks hello specified Event Hub based on hello schedule that you set.</span></span> 
    <span data-ttu-id="43aa4-152">Si votre application détecte les nouveaux événements Bonjour concentrateur d’événements, déclencheur de hello exécute les autres actions ou des déclencheurs dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="43aa4-152">If your app finds new events in hello Event Hub, hello trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a><span data-ttu-id="43aa4-153">Envoyer des événements tooyour concentrateur d’événements à partir de votre application logique</span><span class="sxs-lookup"><span data-stu-id="43aa4-153">Send events tooyour Event Hub from your logic app</span></span>

<span data-ttu-id="43aa4-154">Une [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) est une tâche effectuée par le flux de travail de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="43aa4-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="43aa4-155">Après avoir ajouté une application de la logique de déclencheur tooyour, vous pouvez ajouter un opérateur de tooperform action avec les données générées par ce déclencheur.</span><span class="sxs-lookup"><span data-stu-id="43aa4-155">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="43aa4-156">toosend un tooyour événement concentrateur d’événements à partir de votre application logique, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="43aa4-156">toosend an event tooyour Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="43aa4-157">Dans le Concepteur d’application logique, sous le déclencheur de votre application logique, sélectionnez **Nouvelle étape** > **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="43aa4-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    ![Cliquez sur Nouvelle étape, puis sur Ajouter une action](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="43aa4-159">Vous pouvez maintenant rechercher et sélectionner une action tooperform.</span><span class="sxs-lookup"><span data-stu-id="43aa4-159">Now you can find and select an action tooperform.</span></span> 
    <span data-ttu-id="43aa4-160">Bien que vous puissiez sélectionner toute action, pour cet exemple, nous souhaitons les événements toosend action hello concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="43aa4-160">Although you can select any action, for this example, we want hello Event Hubs action toosend events.</span></span>

2.  <span data-ttu-id="43aa4-161">Dans la zone de recherche de hello, entrez `event hubs` pour votre filtre.</span><span class="sxs-lookup"><span data-stu-id="43aa4-161">In hello search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="43aa4-162">Sélectionnez cette action : **Envoyer un événement**</span><span class="sxs-lookup"><span data-stu-id="43aa4-162">Select this action: **Send event**</span></span>

    ![Sélectionnez l’action « Event Hubs - Envoyer un événement »](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="43aa4-164">Entrez les détails de hello requis pour l’événement hello, telles que nom hello pour hello où vous souhaitez les événements de hello toosend concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="43aa4-164">Enter hello required details for hello event, such as hello name for hello Event Hub where you want toosend hello event.</span></span> <span data-ttu-id="43aa4-165">Entrez tous les autres détails sur l’événement hello, tel que le contenu de cet événement facultatif.</span><span class="sxs-lookup"><span data-stu-id="43aa4-165">Enter any other optional details about hello event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="43aa4-166">toooptionally spécifier la partition de concentrateur d’événements hello où toosend hello événement, choisissez **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="43aa4-166">toooptionally specify hello Event Hub partition where toosend hello event, choose **Show advanced options**.</span></span> 

    ![Entrez le nom du hub Event Hubs et les détails facultatifs de l’événement](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="43aa4-168">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="43aa4-168">Save your changes.</span></span>

    ![Enregistrer votre application logique](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="43aa4-170">Vous avez maintenant définir des événements de toosend action à partir de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="43aa4-170">You've now set up an action toosend events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="43aa4-171">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="43aa4-171">Connector-specific details</span></span>

<span data-ttu-id="43aa4-172">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="43aa4-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="43aa4-173">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="43aa4-173">Get help</span></span>

<span data-ttu-id="43aa4-174">tooask questions, répondez aux questions et voir les autres utilisateurs Azure Logic Apps font, visitez hello [forum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="43aa4-174">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="43aa4-175">toohelp améliorer Logic Apps et connecteurs, voter pour ou envoyer vos idées à hello [site de commentaires utilisateur Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="43aa4-175">toohelp improve Logic Apps and connectors, vote on or submit ideas at hello [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="43aa4-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="43aa4-176">Next steps</span></span>

*  [<span data-ttu-id="43aa4-177">Rechercher d’autres connecteurs pour Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="43aa4-177">Find other connectors for Azure Logic apps</span></span>](./apis-list.md)