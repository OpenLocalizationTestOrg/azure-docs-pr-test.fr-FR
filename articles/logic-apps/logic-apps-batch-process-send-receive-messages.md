---
title: Traiter des messages par lots (groupe ou collection de messages) - Azure Logic Apps | Microsoft Docs
description: "Envoyer et recevoir des messages à traiter par lots dans les applications logiques"
keywords: lot, traitement par lots
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 480ffce5dbe7c25181bb0ba5639de884e98ff4e6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a><span data-ttu-id="fd476-104">Envoyer, recevoir et traiter par lots des messages dans les applications logiques</span><span class="sxs-lookup"><span data-stu-id="fd476-104">Send, receive, and batch process messages in logic apps</span></span>

<span data-ttu-id="fd476-105">Pour traiter des groupes de messages, vous pouvez envoyer des éléments de données, ou des messages, vers un *lot*, puis traiter ce lot.</span><span class="sxs-lookup"><span data-stu-id="fd476-105">To process messages together in groups, you can send data items, or messages, to a *batch*, and then process those items as a batch.</span></span> <span data-ttu-id="fd476-106">Cette méthode est utile lorsque vous souhaitez regrouper les éléments de données d’une certaine manière et les traiter ensemble.</span><span class="sxs-lookup"><span data-stu-id="fd476-106">This approach is useful when you want to make sure data items are grouped in a specific way and are processed together.</span></span> 

<span data-ttu-id="fd476-107">Vous pouvez créer des applications logiques destinées à recevoir des éléments regroupés dans un lot grâce au déclencheur **Lot**.</span><span class="sxs-lookup"><span data-stu-id="fd476-107">You can create logic apps that receive items as a batch by using the **Batch** trigger.</span></span> <span data-ttu-id="fd476-108">Vous pouvez créer des applications logiques destinées à envoyer des éléments regroupés dans un lot grâce à **l’opération de traitement par lots**.</span><span class="sxs-lookup"><span data-stu-id="fd476-108">You can then create logic apps that send items to a batch by using the **Batch** action.</span></span>

<span data-ttu-id="fd476-109">Cette rubrique montre comment créer une solution de traitement par lot en effectuant les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="fd476-109">This topic shows how you can build a batching solution by performing these tasks:</span></span> 

* <span data-ttu-id="fd476-110">[Créer une application logique destinée à recevoir et collecter des éléments regroupés dans un lot](#batch-receiver).</span><span class="sxs-lookup"><span data-stu-id="fd476-110">[Create a logic app that receives and collects items as a batch](#batch-receiver).</span></span> <span data-ttu-id="fd476-111">Cette application logique « réceptrice de lots » spécifie les critères relatifs au nom et à la version du lot qui doivent être respectés avant que l’application logique ne publie et traite les éléments.</span><span class="sxs-lookup"><span data-stu-id="fd476-111">This "batch receiver" logic app specifies the batch name and release criteria to meet before the receiver logic app releases and processes items.</span></span> 

* <span data-ttu-id="fd476-112">[Créer une application logique qui envoie les éléments vers un lot](#batch-sender).</span><span class="sxs-lookup"><span data-stu-id="fd476-112">[Create a logic app that sends items to a batch](#batch-sender).</span></span> <span data-ttu-id="fd476-113">Cette application logique « expéditrice de lots » spécifie où envoyer les éléments, qui doivent se trouver dans une application logique réceptrice de lots existante.</span><span class="sxs-lookup"><span data-stu-id="fd476-113">This "batch sender" logic app specifies where to send items, which must be an existing batch receiver logic app.</span></span> <span data-ttu-id="fd476-114">Vous pouvez également spécifier une clé unique (telle qu’un numéro de client) pour que le lot cible soit divisé en sous-ensembles, en fonction de cette clé.</span><span class="sxs-lookup"><span data-stu-id="fd476-114">You can also specify a unique key, like a customer number, to "partition", or divide, the target batch into subsets based on that key.</span></span> <span data-ttu-id="fd476-115">De cette façon, tous les éléments associés à cette clé sont collectés et traités ensemble.</span><span class="sxs-lookup"><span data-stu-id="fd476-115">That way, all items with that key are collected and processed together.</span></span> 

## <a name="requirements"></a><span data-ttu-id="fd476-116">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="fd476-116">Requirements</span></span>

<span data-ttu-id="fd476-117">Pour suivre cet exemple, vous avez besoin de ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="fd476-117">To follow this example, you need these items:</span></span>

* <span data-ttu-id="fd476-118">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="fd476-118">An Azure subscription.</span></span> <span data-ttu-id="fd476-119">Si vous ne disposez d’aucun abonnement, vous pouvez [commencer par créer gratuitement un compte Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="fd476-119">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="fd476-120">Sinon, vous pouvez souscrire à un [abonnement de type paiement à l’utilisation](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="fd476-120">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="fd476-121">Des connaissances de base en [création d’applications logiques](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="fd476-121">Basic knowledge about [how to create logic apps](../logic-apps/logic-apps-create-a-logic-app.md)</span></span> 

* <span data-ttu-id="fd476-122">Un compte de courrier de n’importe quel [fournisseur de messagerie pris en charge par Azure Logic Apps](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="fd476-122">An email account with any [email provider supported by Azure Logic Apps](../connectors/apis-list.md)</span></span>

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a><span data-ttu-id="fd476-123">Créer des applications logiques destinées à recevoir des messages regroupés dans un lot</span><span class="sxs-lookup"><span data-stu-id="fd476-123">Create logic apps that receive messages as a batch</span></span>

<span data-ttu-id="fd476-124">Avant de pouvoir envoyer des messages vers un lot, vous devez d’abord créer une application logique « réceptrice de lots » à l’aide du déclencheur **Lot**.</span><span class="sxs-lookup"><span data-stu-id="fd476-124">Before you can send messages to a batch, you must first create a "batch receiver" logic app with the **Batch** trigger.</span></span> <span data-ttu-id="fd476-125">De cette façon, vous pouvez sélectionner cette application logique réceptrice lorsque vous créez l’application logique expéditrice.</span><span class="sxs-lookup"><span data-stu-id="fd476-125">That way, you can select this receiver logic app when you create the sender logic app.</span></span> <span data-ttu-id="fd476-126">Pour l’application réceptrice, vous devez spécifier le nom du lot, les critères de déclenchement, ainsi que d’autres paramètres.</span><span class="sxs-lookup"><span data-stu-id="fd476-126">For the receiver, you specify the batch name, release criteria, and other settings.</span></span> 

<span data-ttu-id="fd476-127">Les applications logiques expéditrices doivent savoir où envoyer les éléments. Les applications logiques réceptrices, quant à elles, n’ont rien à savoir sur les applications expéditrices.</span><span class="sxs-lookup"><span data-stu-id="fd476-127">Sender logic apps need know where to send items, while receiver logic apps don't need to know anything about the senders.</span></span>

1. <span data-ttu-id="fd476-128">Dans le [portail Azure](https://portal.azure.com), créez une application logique et nommez-la « BatchReceiver ».</span><span class="sxs-lookup"><span data-stu-id="fd476-128">In the [Azure portal](https://portal.azure.com), create a logic app with this name: "BatchReceiver"</span></span> 

2. <span data-ttu-id="fd476-129">Dans le Concepteur d'applications logiques, ajoutez le déclencheur **Lot** qui démarre le flux de travail de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="fd476-129">In Logic Apps Designer, add the **Batch** trigger, which starts your logic app workflow.</span></span> <span data-ttu-id="fd476-130">Dans la zone de recherche, entrez « lot » comme filtre.</span><span class="sxs-lookup"><span data-stu-id="fd476-130">In the search box, enter "batch" as your filter.</span></span> <span data-ttu-id="fd476-131">Sélectionnez le déclencheur **Lot – Traiter les messages par lots**.</span><span class="sxs-lookup"><span data-stu-id="fd476-131">Select this trigger: **Batch – Batch messages**</span></span>

   ![Ajout du déclencheur Lot](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. <span data-ttu-id="fd476-133">Fournissez un nom pour le lot, puis spécifiez des critères pour son déclenchement, par exemple :</span><span class="sxs-lookup"><span data-stu-id="fd476-133">Provide a name for the batch, and specify criteria for releasing the batch, for example:</span></span>

   * <span data-ttu-id="fd476-134">**Nom du lot** : nom utilisé pour identifier le lot (« TestBatch » dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="fd476-134">**Batch Name**: The name used to identify the batch, which is "TestBatch" in this example.</span></span>
   * <span data-ttu-id="fd476-135">**Nombre de messages** : nombre de messages devant être contenus dans un lot avant le déclenchement du traitement (« 5 » dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="fd476-135">**Message Count**: The number of messages to hold as a batch before releasing for processing, which is "5" in this example.</span></span>

   ![Détails à fournir concernant le déclencheur Lot](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. <span data-ttu-id="fd476-137">Ajoutez une autre action qui envoie un e-mail lorsque le lot est déclenché.</span><span class="sxs-lookup"><span data-stu-id="fd476-137">Add another action that sends an email when the batch trigger fires.</span></span> <span data-ttu-id="fd476-138">Chaque fois que le lot atteint cinq éléments, l’application logique envoie un e-mail.</span><span class="sxs-lookup"><span data-stu-id="fd476-138">Each time the batch has five items, the logic app sends an email.</span></span>

   1. <span data-ttu-id="fd476-139">Sous le déclencheur Lot, choisissez **+ Nouvelle étape** > **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="fd476-139">Under the batch trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="fd476-140">Dans la zone de recherche, entrez « e-mail » comme filtre.</span><span class="sxs-lookup"><span data-stu-id="fd476-140">In the search box, enter "email" as your filter.</span></span>
   <span data-ttu-id="fd476-141">Sélectionnez un connecteur de messagerie en fonction de votre fournisseur de messagerie.</span><span class="sxs-lookup"><span data-stu-id="fd476-141">Based on your email provider, select an email connector.</span></span>
   
      <span data-ttu-id="fd476-142">Par exemple, si vous avez un compte professionnel ou scolaire, sélectionnez le connecteur Outlook Office 365.</span><span class="sxs-lookup"><span data-stu-id="fd476-142">For example, if you have a work or school account, select the Office 365 Outlook connector.</span></span> 
      <span data-ttu-id="fd476-143">Si vous avez un compte Gmail, sélectionnez le connecteur Gmail.</span><span class="sxs-lookup"><span data-stu-id="fd476-143">If you have a Gmail account, select the Gmail connector.</span></span>

   3. <span data-ttu-id="fd476-144">Sélectionnez cette action pour votre connecteur : **{*fournisseur de messagerie*} - Envoyer un message électronique**</span><span class="sxs-lookup"><span data-stu-id="fd476-144">Select this action for your connector: **{*email provider*} - Send an email**</span></span>

      <span data-ttu-id="fd476-145">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="fd476-145">For example:</span></span>

      ![Sélection de l’action « Envoyer un message électronique » pour votre fournisseur de messagerie](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. <span data-ttu-id="fd476-147">Si vous n’avez pas déjà créé une connexion pour votre fournisseur de messagerie, entrez votre adresse e-mail et votre mot de passe lorsque vous êtes invité à vous authentifier.</span><span class="sxs-lookup"><span data-stu-id="fd476-147">If you didn't previously create a connection for your email provider, provide your email credentials for authentication when prompted.</span></span> <span data-ttu-id="fd476-148">En savoir plus sur [l’authentification à l’aide d’une adresse e-mail et d’un mot de passe](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="fd476-148">Learn more about [authenticating your email credentials](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

6. <span data-ttu-id="fd476-149">Définissez les propriétés de l’action que vous venez d’ajouter.</span><span class="sxs-lookup"><span data-stu-id="fd476-149">Set the properties for the action you just added.</span></span>

   * <span data-ttu-id="fd476-150">Dans la zone **À**, entrez l’adresse e-mail du destinataire.</span><span class="sxs-lookup"><span data-stu-id="fd476-150">In the **To** box, enter the recipient's email address.</span></span> 
   <span data-ttu-id="fd476-151">À des fins de test, vous pouvez utiliser votre propre adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="fd476-151">For testing purposes, you can use your own email address.</span></span>

   * <span data-ttu-id="fd476-152">Dans la zone **Objet**, lorsque la liste **Contenu dynamique** s’affiche, sélectionnez le champ **Nom de partition**.</span><span class="sxs-lookup"><span data-stu-id="fd476-152">In the **Subject** box, when the **Dynamic content** list appears, select the **Partition Name** field.</span></span>

     ![Dans la liste « Contenu dynamique », sélectionnez « Nom de partition »](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     <span data-ttu-id="fd476-154">Dans une section ultérieure, vous pourrez spécifier une clé de partition unique afin de diviser le lot cible en plusieurs ensembles logiques vers lesquels envoyer des messages.</span><span class="sxs-lookup"><span data-stu-id="fd476-154">In a later section, you can specify a unique partition key that divides the target batch into logical sets to where you can send messages.</span></span> 
     <span data-ttu-id="fd476-155">Chaque ensemble est associé à un numéro unique qui est généré par l’application logique expéditrice.</span><span class="sxs-lookup"><span data-stu-id="fd476-155">Each set has a unique number that's generated by the sender logic app.</span></span> 
     <span data-ttu-id="fd476-156">Cette fonctionnalité permet d’utiliser un lot comprenant plusieurs sous-ensembles et de définir chaque sous-ensemble avec le nom que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="fd476-156">This capability lets you use a single batch with multiple subsets and define each subset with the name that you provide.</span></span>

   * <span data-ttu-id="fd476-157">Dans la zone **Corps**, lorsque la liste **Contenu dynamique** s’affiche, sélectionnez le champ **ID de message**.</span><span class="sxs-lookup"><span data-stu-id="fd476-157">In the **Body** box, when the **Dynamic content** list appears, select the **Message Id** field.</span></span>

     ![Pour « Corps », sélectionnez « ID de message »](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     <span data-ttu-id="fd476-159">Étant donné que l’entrée de l’action Envoyer un message électronique se présente sous la forme d’un tableau, le concepteur ajoute automatiquement une boucle **For each** autour de l’action **Envoyer un message électronique**.</span><span class="sxs-lookup"><span data-stu-id="fd476-159">Because the input for the send email action is an array, the designer automatically adds a **For each** loop around the **Send an email** action.</span></span> 
     <span data-ttu-id="fd476-160">Cette boucle effectue l’action interne sur chaque élément du lot.</span><span class="sxs-lookup"><span data-stu-id="fd476-160">This loop performs the inner action on each item in the batch.</span></span> 
     <span data-ttu-id="fd476-161">Étant donné que le déclencheur de lot est défini sur cinq éléments, vous recevez cinq e-mails chaque fois qu’un lot est déclenché.</span><span class="sxs-lookup"><span data-stu-id="fd476-161">So, with the batch trigger set to five items, you get five emails each time the trigger fires.</span></span>

7.  <span data-ttu-id="fd476-162">Maintenant que vous avez créé l’application logique réceptrice de lots, enregistrez-la.</span><span class="sxs-lookup"><span data-stu-id="fd476-162">Now that you created a batch receiver logic app, save your logic app.</span></span>

    ![Enregistrer votre application logique](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-to-a-batch"></a><span data-ttu-id="fd476-164">Créer des applications logiques qui envoient des messages vers un lot</span><span class="sxs-lookup"><span data-stu-id="fd476-164">Create logic apps that send messages to a batch</span></span>

<span data-ttu-id="fd476-165">À présent, créez une ou plusieurs applications logiques qui envoient des éléments vers le lot défini par l’application logique réceptrice.</span><span class="sxs-lookup"><span data-stu-id="fd476-165">Now create one or more logic apps that send items to the batch defined by the receiver logic app.</span></span> <span data-ttu-id="fd476-166">Pour l’application expéditrice, vous spécifiez l’application logique réceptrice, le nom du lot, le contenu du message et tout autre paramètre nécessaire.</span><span class="sxs-lookup"><span data-stu-id="fd476-166">For the sender, you specify the receiver logic app and batch name, message content, and any other settings.</span></span> <span data-ttu-id="fd476-167">Vous pouvez éventuellement fournir une clé de partition unique pour diviser le lot en sous-ensembles dont le but est de collecter les éléments associés à cette clé.</span><span class="sxs-lookup"><span data-stu-id="fd476-167">You can optionally provide a unique partition key to divide the batch into subsets to collect items with that key.</span></span>

<span data-ttu-id="fd476-168">Les applications logiques expéditrices doivent savoir où envoyer les éléments. Les applications logiques réceptrices, quant à elles, n’ont rien à savoir sur les applications expéditrices.</span><span class="sxs-lookup"><span data-stu-id="fd476-168">Sender logic apps need know where to send items, while receiver logic apps don't need to know anything about the senders.</span></span>

1. <span data-ttu-id="fd476-169">Créez une autre application logique et nommez-la « BatchSender ».</span><span class="sxs-lookup"><span data-stu-id="fd476-169">Create another logic app with this name: "BatchSender"</span></span>

   1. <span data-ttu-id="fd476-170">Dans la zone de recherche, entrez « récurrence » comme filtre.</span><span class="sxs-lookup"><span data-stu-id="fd476-170">In the search box, enter "recurrence" as your filter.</span></span> 
   <span data-ttu-id="fd476-171">Sélectionnez le déclencheur **Planification - Récurrence**</span><span class="sxs-lookup"><span data-stu-id="fd476-171">Select this trigger: **Schedule - Recurrence**</span></span>

      ![Ajout du déclencheur « Planification - Récurrence »](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. <span data-ttu-id="fd476-173">Définissez la fréquence et l’intervalle d’exécution de l’application logique expéditrice sur une minute.</span><span class="sxs-lookup"><span data-stu-id="fd476-173">Set the frequency and interval to run the sender logic app every minute.</span></span>

      ![Définition de la fréquence et de l’intervalle pour le déclencheur Récurrence](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. <span data-ttu-id="fd476-175">Ajoutez une nouvelle étape pour envoyer des messages vers un lot.</span><span class="sxs-lookup"><span data-stu-id="fd476-175">Add a new step for sending messages to a batch.</span></span>

   1. <span data-ttu-id="fd476-176">Sous le déclencheur Récurrence, choisissez **+ Nouvelle étape** > **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="fd476-176">Under the recurrence trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="fd476-177">Dans la zone de recherche, entrez « lot » comme filtre.</span><span class="sxs-lookup"><span data-stu-id="fd476-177">In the search box, enter "batch" as your filter.</span></span> 

   3. <span data-ttu-id="fd476-178">Sélectionnez l’action **Envoyer les messages au lot - Choisir un workflow Logic Apps avec déclencheur de lot**.</span><span class="sxs-lookup"><span data-stu-id="fd476-178">Select this action: **Send messages to batch – Choose a Logic Apps workflow with batch trigger**</span></span>

      ![Sélection de l’option « Envoyer les messages au lot »](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. <span data-ttu-id="fd476-180">Maintenant, sélectionnez l’application logique « BatchReceiver » créée précédemment, qui s’affiche désormais en tant qu’action.</span><span class="sxs-lookup"><span data-stu-id="fd476-180">Now select your "BatchReceiver" logic app that you previously created, which now appears as an action.</span></span>

      ![Sélection de l’application logique « BatchReceiver »](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > <span data-ttu-id="fd476-182">La liste affiche également toutes les autres applications logiques qui sont associées à un déclencheur de lot.</span><span class="sxs-lookup"><span data-stu-id="fd476-182">The list also shows any other logic apps that have batch triggers.</span></span>

3. <span data-ttu-id="fd476-183">Définissez les propriétés du lot.</span><span class="sxs-lookup"><span data-stu-id="fd476-183">Set the batch properties.</span></span>

   * <span data-ttu-id="fd476-184">**Nom du lot** : nom défini par l’application logique réceptrice, (« TestBatch » dans cet exemple) qui est validé lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="fd476-184">**Batch Name**: The batch name defined by the receiver logic app, which is "TestBatch" in this example and is validated at runtime.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="fd476-185">Veillez à ne pas modifier le nom du lot, car il doit correspondre au nom de lot spécifié par l’application logique réceptrice.</span><span class="sxs-lookup"><span data-stu-id="fd476-185">Make sure that you don't change the batch name, which must match the batch name that's specified by the receiver logic app.</span></span>
     > <span data-ttu-id="fd476-186">Si vous modifiez son nom, l’application logique expéditrice échouera.</span><span class="sxs-lookup"><span data-stu-id="fd476-186">Changing the batch name causes the sender logic app to fail.</span></span>

   * <span data-ttu-id="fd476-187">**Contenu du message** : contenu du message que vous souhaitez envoyer.</span><span class="sxs-lookup"><span data-stu-id="fd476-187">**Message Content**: The message content that you want to send.</span></span> 
   <span data-ttu-id="fd476-188">Pour cet exemple, ajoutez cette expression qui insère la date et l’heure actuelles dans le contenu du message que vous envoyez vers le lot :</span><span class="sxs-lookup"><span data-stu-id="fd476-188">For this example, add this expression that inserts the current date and time into the message content that you send to the batch:</span></span>

     1. <span data-ttu-id="fd476-189">Lorsque la liste **Contenu dynamique** s’affiche, choisissez **Expression**.</span><span class="sxs-lookup"><span data-stu-id="fd476-189">When the **Dynamic content** list appears, choose **Expression**.</span></span> 
     2. <span data-ttu-id="fd476-190">Entrez l’expression **utcnow()**, puis choisissez **OK**.</span><span class="sxs-lookup"><span data-stu-id="fd476-190">Enter the expression **utcnow()**, and choose **OK**.</span></span> 

        ![Dans « Contenu du message », choisissez « Expression ».](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. <span data-ttu-id="fd476-193">À présent, définissez une partition pour le lot.</span><span class="sxs-lookup"><span data-stu-id="fd476-193">Now set up a partition for the batch.</span></span> <span data-ttu-id="fd476-194">Dans l’action « BatchReceiver », choisissez **Afficher les options avancées**.</span><span class="sxs-lookup"><span data-stu-id="fd476-194">In the "BatchReceiver" action, choose **Show advanced options**.</span></span>

   * <span data-ttu-id="fd476-195">**Nom de partition** : clé de partition unique facultative à utiliser pour diviser le lot cible.</span><span class="sxs-lookup"><span data-stu-id="fd476-195">**Partition Name**: An optional unique partition key to use for dividing the target batch.</span></span> <span data-ttu-id="fd476-196">Pour cet exemple, ajoutez une expression qui génère un nombre aléatoire compris entre 1 et 5.</span><span class="sxs-lookup"><span data-stu-id="fd476-196">For this example, add an expression that generates a random number between one and five.</span></span>
   
     1. <span data-ttu-id="fd476-197">Lorsque la liste **Contenu dynamique** s’affiche, choisissez **Expression**.</span><span class="sxs-lookup"><span data-stu-id="fd476-197">When the **Dynamic content** list appears, choose **Expression**.</span></span>
     2. <span data-ttu-id="fd476-198">Entrez l’expression **rand(1,6)**.</span><span class="sxs-lookup"><span data-stu-id="fd476-198">Enter this expression: **rand(1,6)**</span></span>

        ![Définition d’une partition pour le lot cible](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        <span data-ttu-id="fd476-200">Cette fonction **rand** génère un nombre compris entre 1 et 5.</span><span class="sxs-lookup"><span data-stu-id="fd476-200">This **rand** function generates a number between one and five.</span></span> 
        <span data-ttu-id="fd476-201">Vous divisez donc ce lot en cinq partitions numérotées, définies dynamiquement par cette expression.</span><span class="sxs-lookup"><span data-stu-id="fd476-201">So you are dividing this batch into five numbered partitions, which this expression dynamically sets.</span></span>

   * <span data-ttu-id="fd476-202">**ID du message** : identificateur de message facultatif. Lorsqu’il est vide, c’est un GUID généré.</span><span class="sxs-lookup"><span data-stu-id="fd476-202">**Message Id**: An optional message identifier and is a generated GUID when empty.</span></span> 
   <span data-ttu-id="fd476-203">Pour cet exemple, laissez cette zone vide.</span><span class="sxs-lookup"><span data-stu-id="fd476-203">For this example, leave this box blank.</span></span>

5. <span data-ttu-id="fd476-204">Enregistrez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="fd476-204">Save your logic app.</span></span> <span data-ttu-id="fd476-205">Votre application logique expéditrice doit désormais ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="fd476-205">Your sender logic app now looks similar to this example:</span></span>

   ![Enregistrement de l’application logique](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a><span data-ttu-id="fd476-207">Tester les applications logiques</span><span class="sxs-lookup"><span data-stu-id="fd476-207">Test your logic apps</span></span>

<span data-ttu-id="fd476-208">Pour tester votre solution de traitement par lots, laissez vos applications logiques s’exécuter pendant quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="fd476-208">To test your batching solution, leave your logic apps running for a few minutes.</span></span> <span data-ttu-id="fd476-209">Vous allez commencer à recevoir des e-mails par groupes de cinq, tous avec la même clé de partition.</span><span class="sxs-lookup"><span data-stu-id="fd476-209">Soon, you start getting emails in groups of five, all with the same partition key.</span></span>

<span data-ttu-id="fd476-210">Votre application logique BatchSender s’exécute chaque minute, génère un nombre aléatoire compris entre 1 et 5 et utilise ce numéro généré comme clé de partition pour le lot cible où sont envoyés les messages.</span><span class="sxs-lookup"><span data-stu-id="fd476-210">Your BatchSender logic app runs every minute, generates a random number between one and five, and uses this generated number as the partition key for the target batch where messages are sent.</span></span> <span data-ttu-id="fd476-211">Chaque fois que le lot atteint cinq éléments ayant une même clé de partition, l’application logique BatchReceiver est déclenchée et envoie un e-mail.</span><span class="sxs-lookup"><span data-stu-id="fd476-211">Each time the batch has five items with the same partition key, your BatchReceiver logic app fires and sends mail for each message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd476-212">Lorsque vous avez terminé vos tests, veillez à désactiver l’application logique BatchSender afin d’arrêter l’envoi de messages et éviter la surcharge de la boîte de réception.</span><span class="sxs-lookup"><span data-stu-id="fd476-212">When you're done testing, make sure that you disable the BatchSender logic app to stop sending messages and avoid overloading your inbox.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd476-213">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fd476-213">Next steps</span></span>

* [<span data-ttu-id="fd476-214">Créer des définitions d’application logique à l’aide de JSON</span><span class="sxs-lookup"><span data-stu-id="fd476-214">Build on logic app definitions by using JSON</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="fd476-215">Créer une application sans serveur dans Visual Studio avec Azure Logic Apps et Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fd476-215">Build a serverless app in Visual Studio with Azure Logic Apps and Functions</span></span>](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [<span data-ttu-id="fd476-216">Gestion des exceptions et journalisation des erreurs pour les applications logiques</span><span class="sxs-lookup"><span data-stu-id="fd476-216">Exception handling and error logging for logic apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
