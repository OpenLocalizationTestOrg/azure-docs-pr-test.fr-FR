---
title: connecteur de Outlook Office 365 aaaAdd hello dans vos applications logiques | Documents Microsoft
description: "Créer des applications de logique avec Office 365 connecteur tooenable une interaction avec Office 365. Par exemple : création, modification et mise à jour de contacts et d’éléments de calendrier."
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a><span data-ttu-id="9852d-104">Prise en main hello Office 365 Outlook connector</span><span class="sxs-lookup"><span data-stu-id="9852d-104">Get started with hello Office 365 Outlook connector</span></span>
<span data-ttu-id="9852d-105">connecteur d’Outlook Office 365 Hello permet l’interaction avec Outlook pour Office 365.</span><span class="sxs-lookup"><span data-stu-id="9852d-105">hello Office 365 Outlook connector enables interaction with Outlook in Office 365.</span></span> <span data-ttu-id="9852d-106">Utiliser ce connecteur toocreate, les modifier et les contacts de la mise à jour et les éléments de calendrier et aussi obtenir, envoyer et répondre tooemail.</span><span class="sxs-lookup"><span data-stu-id="9852d-106">Use this connector toocreate, edit, and update contacts and calendar items, and also get, send, and reply tooemail.</span></span>

<span data-ttu-id="9852d-107">Avec Office 365 Outlook, vous pouvez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="9852d-107">With Office 365 Outlook, you:</span></span>

* <span data-ttu-id="9852d-108">Créer votre flux de travail à l’aide des fonctionnalités de messagerie et de calendrier hello dans Office 365.</span><span class="sxs-lookup"><span data-stu-id="9852d-108">Build your workflow using hello email and calendar features within Office 365.</span></span> 
* <span data-ttu-id="9852d-109">Utilisez déclenche toostart votre flux de travail lorsqu’il existe un nouvel e-mail, lorsqu’un élément de calendrier est mis à jour et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="9852d-109">Use triggers toostart your workflow when there is a new email, when a calendar item is updated, and more.</span></span>
* <span data-ttu-id="9852d-110">Utiliser des actions toosend un message électronique, créer un nouvel événement de calendrier et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="9852d-110">Use actions toosend an email, create a new calendar event, and more.</span></span> <span data-ttu-id="9852d-111">Par exemple, lorsqu’il existe un nouvel objet dans Salesforce (un déclencheur), envoyer un courrier électronique tooyour Outlook Office 365 (action).</span><span class="sxs-lookup"><span data-stu-id="9852d-111">For example, when there is a new object in Salesforce (a trigger), send an email tooyour Office 365 Outlook (an action).</span></span> 

<span data-ttu-id="9852d-112">Cette rubrique vous montre comment toouse hello Connecteur Outlook Office 365 dans une application logique, et également les listes hello déclencheurs et actions.</span><span class="sxs-lookup"><span data-stu-id="9852d-112">This topic shows you how toouse hello Office 365 Outlook connector in a logic app, and also lists hello triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="9852d-113">Cette version de l’article de hello s’applique tooLogic applications mise à disposition générale (GA).</span><span class="sxs-lookup"><span data-stu-id="9852d-113">This version of hello article applies tooLogic Apps general availability (GA).</span></span>
> 
> 

<span data-ttu-id="9852d-114">toolearn en savoir plus sur les applications de la logique, consultez [quelles sont les applications logique](../logic-apps/logic-apps-what-are-logic-apps.md) et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9852d-114">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="9852d-115">Se connecter tooOffice 365</span><span class="sxs-lookup"><span data-stu-id="9852d-115">Connect tooOffice 365</span></span>
<span data-ttu-id="9852d-116">Avant que votre application logique peut accéder à n’importe quel service, vous créez tout d’abord un *connexion* toohello service.</span><span class="sxs-lookup"><span data-stu-id="9852d-116">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="9852d-117">Une connexion permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="9852d-117">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="9852d-118">Par exemple, tooconnect tooOffice 365 Outlook, vous devez tout d’abord un Office 365 *connexion*.</span><span class="sxs-lookup"><span data-stu-id="9852d-118">For example, tooconnect tooOffice 365 Outlook, you first need an Office 365 *connection*.</span></span> <span data-ttu-id="9852d-119">toocreate une connexion, entrez des informations d’identification de hello que vous utilisez normalement le service de hello tooaccess tooconnect pour vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="9852d-119">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="9852d-120">Avec Outlook Office 365, entrez tooyour des informations d’identification hello connexion hello toocreate au compte Office 365.</span><span class="sxs-lookup"><span data-stu-id="9852d-120">So with Office 365 Outlook, enter hello credentials tooyour Office 365 account toocreate hello connection.</span></span>

## <a name="create-hello-connection"></a><span data-ttu-id="9852d-121">Créer la connexion de hello</span><span class="sxs-lookup"><span data-stu-id="9852d-121">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="9852d-122">Utilisation d’un déclencheur</span><span class="sxs-lookup"><span data-stu-id="9852d-122">Use a trigger</span></span>
<span data-ttu-id="9852d-123">Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="9852d-123">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="9852d-124">Déclencheurs « interrogent « service de hello à un intervalle et la fréquence à laquelle vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="9852d-124">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="9852d-125">[En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="9852d-125">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="9852d-126">Dans l’application de la logique de hello, tapez « office 365 » tooget une liste des déclencheurs de hello :</span><span class="sxs-lookup"><span data-stu-id="9852d-126">In hello logic app, type "office 365" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. <span data-ttu-id="9852d-127">Sélectionnez **Office 365 Outlook - When an upcoming event is starting soon** (Office 365 Outlook - Quand un événement à venir est imminent).</span><span class="sxs-lookup"><span data-stu-id="9852d-127">Select **Office 365 Outlook - When an upcoming event is starting soon**.</span></span> <span data-ttu-id="9852d-128">Si une connexion existe déjà, puis sélectionnez un calendrier à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="9852d-128">If a connection already exists, then select a calendar from hello drop-down list.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    <span data-ttu-id="9852d-129">Si vous êtes invité à toosign dans, puis entrez le signe de hello dans Détails toocreate hello de connexion.</span><span class="sxs-lookup"><span data-stu-id="9852d-129">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="9852d-130">[Créer la connexion de hello](connectors-create-api-office365-outlook.md#create-the-connection) dans cette rubrique répertorie les étapes de hello.</span><span class="sxs-lookup"><span data-stu-id="9852d-130">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="9852d-131">Dans cet exemple, application de hello logique s’exécute lorsqu’un événement de calendrier est mis à jour.</span><span class="sxs-lookup"><span data-stu-id="9852d-131">In this example, hello logic app runs when a calendar event is updated.</span></span> <span data-ttu-id="9852d-132">résultats de hello toosee de ce déclencheur, ajouter une autre action qui vous envoie un message texte.</span><span class="sxs-lookup"><span data-stu-id="9852d-132">toosee hello results of this trigger, add another action that sends you a text message.</span></span> <span data-ttu-id="9852d-133">Par exemple, ajouter hello Twilio *envoyer le message* action textes lorsque hello événement de calendrier démarre des 15 dernières minutes.</span><span class="sxs-lookup"><span data-stu-id="9852d-133">For example, add hello Twilio *Send message* action that texts you when hello calendar event is starting in 15 minutes.</span></span> 
   > 
   > 
3. <span data-ttu-id="9852d-134">Sélectionnez hello **modifier** bouton et définissez hello **fréquence** et **intervalle** valeurs.</span><span class="sxs-lookup"><span data-stu-id="9852d-134">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="9852d-135">Par exemple, si vous souhaitez hello déclencheur toopoll toutes les 15 minutes, puis définissez hello **fréquence** trop**Minute**et ensemble hello **intervalle** trop**15**.</span><span class="sxs-lookup"><span data-stu-id="9852d-135">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. <span data-ttu-id="9852d-136">**Enregistrer** vos modifications (situé dans l’angle supérieur gauche de la barre d’outils hello).</span><span class="sxs-lookup"><span data-stu-id="9852d-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="9852d-137">Votre application logique est enregistrée et peut être activée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="9852d-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="9852d-138">Utilisation d’une action</span><span class="sxs-lookup"><span data-stu-id="9852d-138">Use an action</span></span>
<span data-ttu-id="9852d-139">Une action est une opération effectuée par flux de travail hello défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="9852d-139">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="9852d-140">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="9852d-140">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="9852d-141">Sélectionnez le signe plus hello.</span><span class="sxs-lookup"><span data-stu-id="9852d-141">Select hello plus sign.</span></span> <span data-ttu-id="9852d-142">Vous voyez plusieurs choix : **ajouter une action**, **ajouter une condition**, ou l’un des hello **plus** options.</span><span class="sxs-lookup"><span data-stu-id="9852d-142">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. <span data-ttu-id="9852d-143">Choisissez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="9852d-143">Choose **Add an action**.</span></span>
3. <span data-ttu-id="9852d-144">Dans la zone de texte hello, tapez « office 365 » tooget une liste de toutes les actions disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="9852d-144">In hello text box, type “office 365” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. <span data-ttu-id="9852d-145">Dans notre exemple, choisissez **Office 365 Outlook - Créer un contact**.</span><span class="sxs-lookup"><span data-stu-id="9852d-145">In our example, choose **Office 365 Outlook - Create contact**.</span></span> <span data-ttu-id="9852d-146">Si une connexion existe déjà, puis choisissez hello **ID de dossier**, **prénom**et d’autres propriétés :</span><span class="sxs-lookup"><span data-stu-id="9852d-146">If a connection already exists, then choose hello **Folder ID**, **Given Name**, and other properties:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    <span data-ttu-id="9852d-147">Si vous êtes invité hello informations de connexion, puis entrez connexion de hello toocreate hello détails.</span><span class="sxs-lookup"><span data-stu-id="9852d-147">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="9852d-148">[Créer la connexion de hello](connectors-create-api-office365-outlook.md#create-the-connection) dans cette rubrique décrit ces propriétés.</span><span class="sxs-lookup"><span data-stu-id="9852d-148">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="9852d-149">Dans cet exemple, nous créons un contact dans Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="9852d-149">In this example, we create a new contact in Office 365 Outlook.</span></span> <span data-ttu-id="9852d-150">Vous pouvez utiliser la sortie à partir d’un autre contact de hello toocreate déclencheur.</span><span class="sxs-lookup"><span data-stu-id="9852d-150">You can use output from another trigger toocreate hello contact.</span></span> <span data-ttu-id="9852d-151">Par exemple, ajouter hello SalesForce *lorsqu’un objet est créé* déclencheur.</span><span class="sxs-lookup"><span data-stu-id="9852d-151">For example, add hello SalesForce *When an object is created* trigger.</span></span> <span data-ttu-id="9852d-152">Ajoutez ensuite hello Outlook Office 365 *créer contact* action qui utilise hello SalesForce champs toocreate hello nouvelle nouveau contact dans Office 365.</span><span class="sxs-lookup"><span data-stu-id="9852d-152">Then add hello Office 365 Outlook *Create contact* action that uses hello SalesForce fields toocreate hello new new contact in Office 365.</span></span> 
   > 
   > 
5. <span data-ttu-id="9852d-153">**Enregistrer** vos modifications (situé dans l’angle supérieur gauche de la barre d’outils hello).</span><span class="sxs-lookup"><span data-stu-id="9852d-153">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="9852d-154">Votre application logique est enregistrée et peut être activée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="9852d-154">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="9852d-155">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="9852d-155">Connector-specific details</span></span>

<span data-ttu-id="9852d-156">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/office365connector/).</span><span class="sxs-lookup"><span data-stu-id="9852d-156">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/office365connector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9852d-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9852d-157">Next Steps</span></span>
<span data-ttu-id="9852d-158">[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9852d-158">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="9852d-159">Explorer hello tous les autres connecteurs disponibles dans les applications logique à notre [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="9852d-159">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

