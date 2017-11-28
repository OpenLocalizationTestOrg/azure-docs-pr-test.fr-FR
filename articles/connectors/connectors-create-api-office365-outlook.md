---
title: "Ajouter le connecteur Office 365 Outlook dans vos applications logiques | Microsoft Docs"
description: "Créez des applications logiques avec un connecteur Office 365 pour permettre l’interaction avec Office 365. Par exemple : création, modification et mise à jour de contacts et d’éléments de calendrier."
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
ms.openlocfilehash: 5335dae62e61659b68e8befb4ed0d404dffb800c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-outlook-connector"></a><span data-ttu-id="ef62d-104">Prise en main du connecteur Office 365 Outlook</span><span class="sxs-lookup"><span data-stu-id="ef62d-104">Get started with the Office 365 Outlook connector</span></span>
<span data-ttu-id="ef62d-105">Le connecteur Office 365 Outlook permet d’interagir avec Outlook dans Office 365.</span><span class="sxs-lookup"><span data-stu-id="ef62d-105">The Office 365 Outlook connector enables interaction with Outlook in Office 365.</span></span> <span data-ttu-id="ef62d-106">Utilisez ce connecteur pour créer, modifier et mettre à jour des contacts et des éléments de calendrier, ainsi que pour recevoir et envoyer des e-mails et pour y répondre.</span><span class="sxs-lookup"><span data-stu-id="ef62d-106">Use this connector to create, edit, and update contacts and calendar items, and also get, send, and reply to email.</span></span>

<span data-ttu-id="ef62d-107">Avec Office 365 Outlook, vous pouvez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ef62d-107">With Office 365 Outlook, you:</span></span>

* <span data-ttu-id="ef62d-108">Créer votre workflow à l’aide des fonctionnalités de messagerie et de calendrier dans Office 365.</span><span class="sxs-lookup"><span data-stu-id="ef62d-108">Build your workflow using the email and calendar features within Office 365.</span></span> 
* <span data-ttu-id="ef62d-109">Utiliser des déclencheurs pour démarrer votre workflow lorsqu’un nouvel e-mail apparaît, lorsqu’un élément de calendrier est mis à jour, et bien davantage.</span><span class="sxs-lookup"><span data-stu-id="ef62d-109">Use triggers to start your workflow when there is a new email, when a calendar item is updated, and more.</span></span>
* <span data-ttu-id="ef62d-110">Utiliser des actions pour envoyer un e-mail, créer un événement de calendrier, etc.</span><span class="sxs-lookup"><span data-stu-id="ef62d-110">Use actions to send an email, create a new calendar event, and more.</span></span> <span data-ttu-id="ef62d-111">Par exemple, lorsqu’un nouvel objet existe dans Salesforce (déclencheur), un e-mail doit être envoyé à votre application Office 365 Outlook (action).</span><span class="sxs-lookup"><span data-stu-id="ef62d-111">For example, when there is a new object in Salesforce (a trigger), send an email to your Office 365 Outlook (an action).</span></span> 

<span data-ttu-id="ef62d-112">Cette rubrique décrit comment utiliser le connecteur Office 365 Outlook dans une application logique, et répertorie les déclencheurs et les actions.</span><span class="sxs-lookup"><span data-stu-id="ef62d-112">This topic shows you how to use the Office 365 Outlook connector in a logic app, and also lists the triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="ef62d-113">Cette version de l’article s’applique à la disponibilité générale des applications logiques.</span><span class="sxs-lookup"><span data-stu-id="ef62d-113">This version of the article applies to Logic Apps general availability (GA).</span></span>
> 
> 

<span data-ttu-id="ef62d-114">Pour plus d’informations sur Logic Apps, voir [Qu’est-ce qu’une application logique ?](../logic-apps/logic-apps-what-are-logic-apps.md) et [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ef62d-114">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-office-365"></a><span data-ttu-id="ef62d-115">Connexion à Office 365</span><span class="sxs-lookup"><span data-stu-id="ef62d-115">Connect to Office 365</span></span>
<span data-ttu-id="ef62d-116">Pour que votre application logique puisse accéder à un service, vous devez d’abord créer une *connexion* à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="ef62d-116">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="ef62d-117">Une connexion permet d’assurer la connectivité entre une application logique et un autre service.</span><span class="sxs-lookup"><span data-stu-id="ef62d-117">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="ef62d-118">Par exemple, pour vous connecter à Office 365 Outlook, vous devez préalablement disposer d’une *connexion* Office 365.</span><span class="sxs-lookup"><span data-stu-id="ef62d-118">For example, to connect to Office 365 Outlook, you first need an Office 365 *connection*.</span></span> <span data-ttu-id="ef62d-119">Pour créer une connexion, entrez les informations d’identification que vous utilisez généralement pour accéder au service auquel vous souhaitez vous connecter.</span><span class="sxs-lookup"><span data-stu-id="ef62d-119">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="ef62d-120">Ensuite, dans Office 365 Outlook, entrez les informations d’identification de votre compte Office 365 pour créer la connexion.</span><span class="sxs-lookup"><span data-stu-id="ef62d-120">So with Office 365 Outlook, enter the credentials to your Office 365 account to create the connection.</span></span>

## <a name="create-the-connection"></a><span data-ttu-id="ef62d-121">Créer la connexion</span><span class="sxs-lookup"><span data-stu-id="ef62d-121">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to Office 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="ef62d-122">Utilisation d’un déclencheur</span><span class="sxs-lookup"><span data-stu-id="ef62d-122">Use a trigger</span></span>
<span data-ttu-id="ef62d-123">Un déclencheur est un événement qui peut être utilisé pour lancer le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="ef62d-123">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="ef62d-124">Les déclencheurs « interrogent » le service à l’intervalle et à la fréquence de votre choix.</span><span class="sxs-lookup"><span data-stu-id="ef62d-124">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="ef62d-125">[En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="ef62d-125">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="ef62d-126">Dans l’application logique, tapez « office 365 » pour obtenir la liste des déclencheurs :</span><span class="sxs-lookup"><span data-stu-id="ef62d-126">In the logic app, type "office 365" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. <span data-ttu-id="ef62d-127">Sélectionnez **Office 365 Outlook - When an upcoming event is starting soon** (Office 365 Outlook - Quand un événement à venir est imminent).</span><span class="sxs-lookup"><span data-stu-id="ef62d-127">Select **Office 365 Outlook - When an upcoming event is starting soon**.</span></span> <span data-ttu-id="ef62d-128">Si une connexion existe déjà, sélectionnez un calendrier dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="ef62d-128">If a connection already exists, then select a calendar from the drop-down list.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    <span data-ttu-id="ef62d-129">Si vous êtes invité à vous connecter, entrez les informations de connexion pour créer la connexion.</span><span class="sxs-lookup"><span data-stu-id="ef62d-129">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="ef62d-130">La section [Créer la connexion](connectors-create-api-office365-outlook.md#create-the-connection) dans cette rubrique répertorie les étapes.</span><span class="sxs-lookup"><span data-stu-id="ef62d-130">[Create the connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="ef62d-131">Dans cet exemple, l’application logique s’exécute lorsqu’un événement de calendrier est mis à jour.</span><span class="sxs-lookup"><span data-stu-id="ef62d-131">In this example, the logic app runs when a calendar event is updated.</span></span> <span data-ttu-id="ef62d-132">Pour visualiser les résultats de ce déclencheur, ajoutez une autre action qui vous envoie un SMS.</span><span class="sxs-lookup"><span data-stu-id="ef62d-132">To see the results of this trigger, add another action that sends you a text message.</span></span> <span data-ttu-id="ef62d-133">Par exemple, ajoutez l’action Twilio *Send message* (Envoyer un message) qui vous envoie un SMS lorsque l’événement de calendrier doit démarrer dans 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="ef62d-133">For example, add the Twilio *Send message* action that texts you when the calendar event is starting in 15 minutes.</span></span> 
   > 
   > 
3. <span data-ttu-id="ef62d-134">Sélectionnez le bouton **Modifier**, puis renseignez les valeurs **Fréquence** et **Intervalle**.</span><span class="sxs-lookup"><span data-stu-id="ef62d-134">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="ef62d-135">Par exemple, si vous souhaitez que le déclencheur interroge le service toutes les 15 minutes, définissez le champ **Fréquence** sur **Minute**, et le champ **Intervalle** sur **15**.</span><span class="sxs-lookup"><span data-stu-id="ef62d-135">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. <span data-ttu-id="ef62d-136">**Enregistrez** vos modifications (dans le coin supérieur gauche de la barre d’outils).</span><span class="sxs-lookup"><span data-stu-id="ef62d-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="ef62d-137">Votre application logique est enregistrée et peut être activée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ef62d-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="ef62d-138">Utilisation d’une action</span><span class="sxs-lookup"><span data-stu-id="ef62d-138">Use an action</span></span>
<span data-ttu-id="ef62d-139">Une action est une opération effectuée par le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="ef62d-139">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="ef62d-140">[En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="ef62d-140">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="ef62d-141">Sélectionnez le signe plus.</span><span class="sxs-lookup"><span data-stu-id="ef62d-141">Select the plus sign.</span></span> <span data-ttu-id="ef62d-142">Vous disposez de plusieurs options : **Ajouter une action**, **Ajouter une condition** ou l’une des options **Plus**.</span><span class="sxs-lookup"><span data-stu-id="ef62d-142">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. <span data-ttu-id="ef62d-143">Choisissez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="ef62d-143">Choose **Add an action**.</span></span>
3. <span data-ttu-id="ef62d-144">Dans la zone de texte, tapez « office 365 » pour obtenir la liste de toutes les actions disponibles.</span><span class="sxs-lookup"><span data-stu-id="ef62d-144">In the text box, type “office 365” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. <span data-ttu-id="ef62d-145">Dans notre exemple, choisissez **Office 365 Outlook - Créer un contact**.</span><span class="sxs-lookup"><span data-stu-id="ef62d-145">In our example, choose **Office 365 Outlook - Create contact**.</span></span> <span data-ttu-id="ef62d-146">Si une connexion existe déjà, choisissez **ID du dossier**, **Prénom** et d’autres propriétés :</span><span class="sxs-lookup"><span data-stu-id="ef62d-146">If a connection already exists, then choose the **Folder ID**, **Given Name**, and other properties:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    <span data-ttu-id="ef62d-147">Si vous êtes invité à saisir les informations de connexion, entrez les informations requises pour créer la connexion.</span><span class="sxs-lookup"><span data-stu-id="ef62d-147">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="ef62d-148">La section [Créer la connexion](connectors-create-api-office365-outlook.md#create-the-connection) dans cette rubrique décrit ces propriétés.</span><span class="sxs-lookup"><span data-stu-id="ef62d-148">[Create the connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="ef62d-149">Dans cet exemple, nous créons un contact dans Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="ef62d-149">In this example, we create a new contact in Office 365 Outlook.</span></span> <span data-ttu-id="ef62d-150">Vous pouvez utiliser la sortie d’un autre déclencheur pour créer le contact.</span><span class="sxs-lookup"><span data-stu-id="ef62d-150">You can use output from another trigger to create the contact.</span></span> <span data-ttu-id="ef62d-151">Par exemple, ajoutez le déclencheur SalesForce *Quand un objet est créé*.</span><span class="sxs-lookup"><span data-stu-id="ef62d-151">For example, add the SalesForce *When an object is created* trigger.</span></span> <span data-ttu-id="ef62d-152">Ensuite, ajoutez l’action Office 365 Outlook *Créer un contact* qui utilise les champs SalesForce pour créer le contact dans Office 365.</span><span class="sxs-lookup"><span data-stu-id="ef62d-152">Then add the Office 365 Outlook *Create contact* action that uses the SalesForce fields to create the new new contact in Office 365.</span></span> 
   > 
   > 
5. <span data-ttu-id="ef62d-153">**Enregistrez** vos modifications (dans le coin supérieur gauche de la barre d’outils).</span><span class="sxs-lookup"><span data-stu-id="ef62d-153">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="ef62d-154">Votre application logique est enregistrée et peut être activée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ef62d-154">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="ef62d-155">Détails spécifiques aux connecteurs</span><span class="sxs-lookup"><span data-stu-id="ef62d-155">Connector-specific details</span></span>

<span data-ttu-id="ef62d-156">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/office365connector/).</span><span class="sxs-lookup"><span data-stu-id="ef62d-156">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/office365connector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ef62d-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ef62d-157">Next Steps</span></span>
<span data-ttu-id="ef62d-158">[Créez une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ef62d-158">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="ef62d-159">Explorez les autres connecteurs disponibles dans les applications logiques en consultant notre [liste d’API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="ef62d-159">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

