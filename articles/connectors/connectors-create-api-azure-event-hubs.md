---
title: "Configurer l’observateur d’événements avec Azure Event Hubs pour Azure Logic Apps | Microsoft Docs"
description: "Surveiller les flux de données afin de recevoir et envoyer des événements pour Azure Logic Apps avec Azure Event Hubs"
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
ms.openlocfilehash: 2ca27fb8269d1796fb1181fc4d0a8744a592d548
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-receive-and-send-events-with-the-event-hubs-connector"></a><span data-ttu-id="232bc-104">Surveillez, recevez et envoyez des événements avec le connecteur Event Hubs</span><span class="sxs-lookup"><span data-stu-id="232bc-104">Monitor, receive, and send events with the Event Hubs connector</span></span>

<span data-ttu-id="232bc-105">Pour configurer un observateur d’événements afin que votre application logique puisse détecter, recevoir et envoyer des événements, connectez-vous à un hub [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs) à partir de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="232bc-105">To set up an event monitor so that your logic app can detect events, receive events, and send events, connect to an [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="232bc-106">En savoir plus sur [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="232bc-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="232bc-107">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="232bc-107">Requirements</span></span>

* <span data-ttu-id="232bc-108">Vous devez avoir un [espace de noms Event Hubs et un hub Event Hubs](../event-hubs/event-hubs-create.md) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="232bc-108">You have to have an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="232bc-109">Découvrez [comment créer un espace de noms Event Hubs et un hub Event Hubs](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="232bc-109">Learn [how to create an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="232bc-110">Pour utiliser [n’importe quel connecteur](https://docs.microsoft.com/azure/connectors/apis-list) dans votre application logique, vous devez d’abord créer une application logique.</span><span class="sxs-lookup"><span data-stu-id="232bc-110">To use [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have to create a logic app first.</span></span> <span data-ttu-id="232bc-111">Découvrez [comment créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="232bc-111">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-the-connection-string"></a><span data-ttu-id="232bc-112">Vérifier les autorisations d’espace de noms Event Hubs et rechercher la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="232bc-112">Check Event Hubs namespace permissions and find the connection string</span></span>

<span data-ttu-id="232bc-113">Pour que votre application logique accède à n’importe quel service, vous devez créer une [*connexion*](./connectors-overview.md) entre votre application logique et le service, si ce n’est pas déjà fait.</span><span class="sxs-lookup"><span data-stu-id="232bc-113">For your logic app to access any service, you have to create a [*connection*](./connectors-overview.md) between your logic app and the service, if you haven't already.</span></span> <span data-ttu-id="232bc-114">Cette connexion autorise votre application logique à accéder aux données.</span><span class="sxs-lookup"><span data-stu-id="232bc-114">This connection authorizes your logic app to access data.</span></span>
<span data-ttu-id="232bc-115">Pour que votre application logique accède à votre hub Event Hubs, vous devez disposer des autorisations **Gérer** et de la chaîne de connexion pour votre espace de noms Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="232bc-115">For your logic app to access your Event Hub, you have to have **Manage** permissions and the connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="232bc-116">Pour vérifier vos autorisations et obtenir la chaîne de connexion, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="232bc-116">To check your permissions and get the connection string, follow these steps.</span></span>

1.  <span data-ttu-id="232bc-117">Connectez-vous au [portail Azure](https://portal.azure.com "portail Azure").</span><span class="sxs-lookup"><span data-stu-id="232bc-117">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="232bc-118">Accédez à votre *espace de noms* Event Hubs, et non au hub Event Hubs spécifique.</span><span class="sxs-lookup"><span data-stu-id="232bc-118">Go to your Event Hubs *namespace*, not the specific Event Hub.</span></span> <span data-ttu-id="232bc-119">Dans le panneau de l’espace de noms, sous **Paramètres**, choisissez **Stratégies d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="232bc-119">On the namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="232bc-120">Sous **Revendications**, vérifiez que vous disposez des autorisations **Gérer** pour cet espace de noms.</span><span class="sxs-lookup"><span data-stu-id="232bc-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![Gérer les autorisations pour votre espace de noms Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="232bc-122">Pour copier la chaîne de connexion associée à l’espace de noms Event Hubs, choisissez **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="232bc-122">To copy the connection string for the Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="232bc-123">En regard de votre chaîne de connexion de clé primaire, cliquez sur le bouton de copie.</span><span class="sxs-lookup"><span data-stu-id="232bc-123">Next to your primary key connection string, choose the copy button.</span></span>

    ![Copier la chaîne de connexion d’espace de noms Event Hubs](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="232bc-125">Pour vérifier que votre chaîne de connexion est bien associée à votre espace de noms Event Hubs ou à un hub Event Hubs spécifique, vérifiez le paramètre `EntityPath` pour la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="232bc-125">To confirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check the connection string for the `EntityPath` parameter.</span></span> <span data-ttu-id="232bc-126">Si vous trouvez ce paramètre, la chaîne de connexion concerne une « entité » Event Hubs spécifique et elle ne peut pas être utilisée avec votre application logique.</span><span class="sxs-lookup"><span data-stu-id="232bc-126">If you find this parameter, the connection string is for a specific Event Hub "entity", and is not the correct string to use with your logic app.</span></span>

4.  <span data-ttu-id="232bc-127">À présent, lorsque vous êtes invité à indiquer des informations d’identification après avoir ajouté un déclencheur ou une action Event Hubs à votre application logique, vous pouvez vous connecter à votre espace de noms Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="232bc-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action to your logic app, you can connect to your Event Hubs namespace.</span></span> <span data-ttu-id="232bc-128">Nommez votre connexion, entrez la chaîne de connexion que vous avez copiée, puis choisissez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="232bc-128">Give your connection a name, enter the connection string that you copied, and choose **Create**.</span></span>

    ![Entrer la chaîne de connexion pour un espace de noms Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="232bc-130">Une fois votre connexion créée, le nom de connexion doit apparaître dans le déclencheur ou l’action Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="232bc-130">After you create your connection, the connection name should appear in the Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="232bc-131">Vous pouvez désormais passer aux autres étapes dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="232bc-131">You can then continue with the other steps in your logic app.</span></span>

    ![Connexion d’espace de noms Event Hubs créée](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="232bc-133">Démarrer le workflow lorsque votre hub Event Hubs reçoit de nouveaux événements</span><span class="sxs-lookup"><span data-stu-id="232bc-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="232bc-134">Un [*déclencheur*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) désigne un événement qui démarre un workflow dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="232bc-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="232bc-135">Pour démarrer un workflow lorsque de nouveaux événements sont envoyés à votre hub Event Hubs, procédez comme suit afin d’ajouter le déclencheur qui détecte cet événement.</span><span class="sxs-lookup"><span data-stu-id="232bc-135">To start a workflow when new events are sent to your Event Hub, follow these steps for adding the trigger that detects this event.</span></span>

1.  <span data-ttu-id="232bc-136">Dans le [portail Azure](https://portal.azure.com "portail Azure"), accédez à votre application logique existante ou créez une application logique vide.</span><span class="sxs-lookup"><span data-stu-id="232bc-136">In the [Azure portal](https://portal.azure.com "Azure portal"), go to your existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="232bc-137">Dans la zone de recherche du Concepteur d’application logique, entrez `event hubs` pour votre filtre.</span><span class="sxs-lookup"><span data-stu-id="232bc-137">In the search box for the Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="232bc-138">Sélectionnez ce déclencheur : **When events are available in Event Hub (Lorsque les événements sont disponibles dans un hub Event Hubs)**</span><span class="sxs-lookup"><span data-stu-id="232bc-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![Sélectionner le déclencheur lorsque votre hub Event Hubs reçoit de nouveaux événements](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="232bc-140">Si vous ne disposez pas encore d’une connexion à votre espace de noms Event Hubs, vous êtes invité à créer cette connexion dès maintenant.</span><span class="sxs-lookup"><span data-stu-id="232bc-140">If you don't already have a connection to your Event Hubs namespace, you're prompted to create this connection now.</span></span> <span data-ttu-id="232bc-141">Nommez votre connexion, puis entrez la chaîne de connexion pour votre espace de noms Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="232bc-141">Give your connection a name, and enter the connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="232bc-142">Si nécessaire, découvrez [comment rechercher votre chaîne de connexion](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="232bc-142">If necessary, learn [how to find your connection string](#permissions-connection-string).</span></span>

    ![Entrer la chaîne de connexion pour un espace de noms Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="232bc-144">Une fois la connexion créée, les paramètres du déclencheur **When an event in available in Event Hub (Lorsque les événements sont disponibles dans un hub Event Hubs)** s’affichent.</span><span class="sxs-lookup"><span data-stu-id="232bc-144">After you create the connection, the settings for the **When an event in available in an Event Hub** trigger appear.</span></span>

    ![Paramètres du déclencheur lorsque votre hub Event Hubs reçoit de nouveaux événements](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="232bc-146">Entrez ou sélectionnez le nom du hub Event Hubs que vous souhaitez surveiller.</span><span class="sxs-lookup"><span data-stu-id="232bc-146">Enter or select the name for the Event Hub that you want to monitor.</span></span> <span data-ttu-id="232bc-147">Sélectionnez la fréquence et l’intervalle de fréquence auxquels vous souhaitez vérifier le hub Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="232bc-147">Select the frequency and interval for how often you want to check the Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="232bc-148">Si vous souhaitez sélectionner un groupe de consommateurs pour la lecture des événements, choisissez **Afficher les options avancées**.</span><span class="sxs-lookup"><span data-stu-id="232bc-148">To optionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![Spécifier un hub Event Hubs ou un groupe de consommateurs](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="232bc-150">Vous avez à présent défini un déclencheur qui démarre un workflow pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="232bc-150">You've now set up a trigger to start a workflow for your logic app.</span></span> 
    <span data-ttu-id="232bc-151">Votre application logique vérifie le hub Event Hubs spécifié conformément à la planification définie.</span><span class="sxs-lookup"><span data-stu-id="232bc-151">Your logic app checks the specified Event Hub based on the schedule that you set.</span></span> 
    <span data-ttu-id="232bc-152">Si votre application trouve de nouveaux événements dans le hub Event Hubs, le déclencheur exécute d’autres actions ou d’autres déclencheurs dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="232bc-152">If your app finds new events in the Event Hub, the trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-to-your-event-hub-from-your-logic-app"></a><span data-ttu-id="232bc-153">Envoyer des événements à votre hub Event Hubs à partir de votre application logique</span><span class="sxs-lookup"><span data-stu-id="232bc-153">Send events to your Event Hub from your logic app</span></span>

<span data-ttu-id="232bc-154">Une [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) est une tâche effectuée par le flux de travail de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="232bc-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="232bc-155">Après avoir ajouté un déclencheur à votre application logique, vous pouvez ajouter une action permettant d’effectuer des opérations avec les données générées par ce déclencheur.</span><span class="sxs-lookup"><span data-stu-id="232bc-155">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="232bc-156">Pour envoyer un événement à votre hub Event Hubs à partir de votre application logique, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="232bc-156">To send an event to your Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="232bc-157">Dans le Concepteur d’application logique, sous le déclencheur de votre application logique, sélectionnez **Nouvelle étape** > **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="232bc-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    ![Cliquez sur Nouvelle étape, puis sur Ajouter une action](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="232bc-159">Vous pouvez maintenant rechercher et sélectionner une action à effectuer.</span><span class="sxs-lookup"><span data-stu-id="232bc-159">Now you can find and select an action to perform.</span></span> 
    <span data-ttu-id="232bc-160">Bien que vous puissiez sélectionner n’importe quelle action, dans cet exemple, nous souhaitons que l’action Event Hubs envoie les événements.</span><span class="sxs-lookup"><span data-stu-id="232bc-160">Although you can select any action, for this example, we want the Event Hubs action to send events.</span></span>

2.  <span data-ttu-id="232bc-161">Dans la zone de recherche, entrez `event hubs` pour votre filtre.</span><span class="sxs-lookup"><span data-stu-id="232bc-161">In the search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="232bc-162">Sélectionnez cette action : **Envoyer un événement**</span><span class="sxs-lookup"><span data-stu-id="232bc-162">Select this action: **Send event**</span></span>

    ![Sélectionnez l’action « Event Hubs - Envoyer un événement »](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="232bc-164">Entrez les informations requises pour l’événement, comme le nom du hub Event Hubs dans lequel vous souhaitez envoyer l’événement.</span><span class="sxs-lookup"><span data-stu-id="232bc-164">Enter the required details for the event, such as the name for the Event Hub where you want to send the event.</span></span> <span data-ttu-id="232bc-165">Entrez les autres détails facultatifs relatifs à l’événement, comme le contenu de cet événement.</span><span class="sxs-lookup"><span data-stu-id="232bc-165">Enter any other optional details about the event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="232bc-166">Si vous souhaitez spécifier la partition du hub Event Hubs où envoyer l’événement, sélectionnez **Afficher les options avancées**.</span><span class="sxs-lookup"><span data-stu-id="232bc-166">To optionally specify the Event Hub partition where to send the event, choose **Show advanced options**.</span></span> 

    ![Entrez le nom du hub Event Hubs et les détails facultatifs de l’événement](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="232bc-168">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="232bc-168">Save your changes.</span></span>

    ![Enregistrer votre application logique](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="232bc-170">Vous avez à présent défini une action permettant d’envoyer des événements à partir de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="232bc-170">You've now set up an action to send events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="232bc-171">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="232bc-171">Connector-specific details</span></span>

<span data-ttu-id="232bc-172">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="232bc-172">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="232bc-173">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="232bc-173">Get help</span></span>

<span data-ttu-id="232bc-174">Pour poser des questions, répondre aux questions et voir ce que font les autres utilisateurs d’Azure Logic Apps, visitez le [Forum Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="232bc-174">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="232bc-175">Afin d’améliorer Logic Apps ainsi que les connecteurs, votez pour des idées ou soumettez-en sur le [site de commentaires utilisateur Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="232bc-175">To help improve Logic Apps and connectors, vote on or submit ideas at the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="232bc-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="232bc-176">Next steps</span></span>

*  [<span data-ttu-id="232bc-177">Rechercher d’autres connecteurs pour Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="232bc-177">Find other connectors for Azure Logic apps</span></span>](./apis-list.md)