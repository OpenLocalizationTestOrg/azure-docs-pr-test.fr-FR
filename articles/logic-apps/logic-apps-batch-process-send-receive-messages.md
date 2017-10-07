---
title: traiter les messages aaaBatch comme un groupe ou de la collection - Azure Logic Apps | Documents Microsoft
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
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a><span data-ttu-id="cfb6f-104">Envoyer, recevoir et traiter par lots des messages dans les applications logiques</span><span class="sxs-lookup"><span data-stu-id="cfb6f-104">Send, receive, and batch process messages in logic apps</span></span>

<span data-ttu-id="cfb6f-105">tooprocess les messages dans des groupes, vous pouvez envoyer tooa d’éléments, ou les messages, données *lot*, puis traite ces éléments en tant que lot.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-105">tooprocess messages together in groups, you can send data items, or messages, tooa *batch*, and then process those items as a batch.</span></span> <span data-ttu-id="cfb6f-106">Cette approche est utile lorsque vous souhaitez toomake que l’option des éléments de données sont regroupés de manière spécifique et sont traitées ensemble.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-106">This approach is useful when you want toomake sure data items are grouped in a specific way and are processed together.</span></span> 

<span data-ttu-id="cfb6f-107">Vous pouvez créer des applications de la logique qui reçoivent des éléments en tant que lot à l’aide de hello **lot** déclencheur.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-107">You can create logic apps that receive items as a batch by using hello **Batch** trigger.</span></span> <span data-ttu-id="cfb6f-108">Vous pouvez ensuite créer des applications de la logique qui envoient des éléments tooa lot à l’aide de hello **lot** action.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-108">You can then create logic apps that send items tooa batch by using hello **Batch** action.</span></span>

<span data-ttu-id="cfb6f-109">Cette rubrique montre comment créer une solution de traitement par lot en effectuant les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="cfb6f-109">This topic shows how you can build a batching solution by performing these tasks:</span></span> 

* <span data-ttu-id="cfb6f-110">[Créer une application logique destinée à recevoir et collecter des éléments regroupés dans un lot](#batch-receiver).</span><span class="sxs-lookup"><span data-stu-id="cfb6f-110">[Create a logic app that receives and collects items as a batch](#batch-receiver).</span></span> <span data-ttu-id="cfb6f-111">Cette application de la logique « récepteur lot » spécifie toomeet critères hello lot nom et la version avant application logique de récepteur hello libère et traite les éléments.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-111">This "batch receiver" logic app specifies hello batch name and release criteria toomeet before hello receiver logic app releases and processes items.</span></span> 

* <span data-ttu-id="cfb6f-112">[Créer une application de la logique qui envoie des éléments tooa lot](#batch-sender).</span><span class="sxs-lookup"><span data-stu-id="cfb6f-112">[Create a logic app that sends items tooa batch](#batch-sender).</span></span> <span data-ttu-id="cfb6f-113">Cette application de la logique « expéditeur lot » Spécifie l’emplacement des éléments toosend, qui doivent être une application de la logique de récepteur lot existante.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-113">This "batch sender" logic app specifies where toosend items, which must be an existing batch receiver logic app.</span></span> <span data-ttu-id="cfb6f-114">Vous pouvez également spécifier une clé unique, par exemple, un numéro de client, trop de « partition » ou divisez, lot cible de hello en sous-ensembles, en fonction de cette clé.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-114">You can also specify a unique key, like a customer number, too"partition", or divide, hello target batch into subsets based on that key.</span></span> <span data-ttu-id="cfb6f-115">De cette façon, tous les éléments associés à cette clé sont collectés et traités ensemble.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-115">That way, all items with that key are collected and processed together.</span></span> 

## <a name="requirements"></a><span data-ttu-id="cfb6f-116">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="cfb6f-116">Requirements</span></span>

<span data-ttu-id="cfb6f-117">toofollow cet exemple, vous avez besoin de ces éléments :</span><span class="sxs-lookup"><span data-stu-id="cfb6f-117">toofollow this example, you need these items:</span></span>

* <span data-ttu-id="cfb6f-118">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-118">An Azure subscription.</span></span> <span data-ttu-id="cfb6f-119">Si vous ne disposez d’aucun abonnement, vous pouvez [commencer par créer gratuitement un compte Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="cfb6f-119">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="cfb6f-120">Sinon, vous pouvez souscrire à un [abonnement de type paiement à l’utilisation](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="cfb6f-120">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="cfb6f-121">Connaissance de base [comment toocreate logique applications](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="cfb6f-121">Basic knowledge about [how toocreate logic apps](../logic-apps/logic-apps-create-a-logic-app.md)</span></span> 

* <span data-ttu-id="cfb6f-122">Un compte de courrier de n’importe quel [fournisseur de messagerie pris en charge par Azure Logic Apps](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="cfb6f-122">An email account with any [email provider supported by Azure Logic Apps](../connectors/apis-list.md)</span></span>

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a><span data-ttu-id="cfb6f-123">Créer des applications logiques destinées à recevoir des messages regroupés dans un lot</span><span class="sxs-lookup"><span data-stu-id="cfb6f-123">Create logic apps that receive messages as a batch</span></span>

<span data-ttu-id="cfb6f-124">Avant d’envoyer le traitement par lots de messages tooa, vous devez d’abord créer une application de logique « récepteur lot » avec hello **lot** déclencheur.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-124">Before you can send messages tooa batch, you must first create a "batch receiver" logic app with hello **Batch** trigger.</span></span> <span data-ttu-id="cfb6f-125">De cette façon, vous pouvez sélectionner cette application logique de récepteur quand vous créez une application de logique hello expéditeur.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-125">That way, you can select this receiver logic app when you create hello sender logic app.</span></span> <span data-ttu-id="cfb6f-126">Pour le récepteur hello, vous spécifiez le nom du lot hello, les critères de déclenchement et les autres paramètres.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-126">For hello receiver, you specify hello batch name, release criteria, and other settings.</span></span> 

<span data-ttu-id="cfb6f-127">Applications de la logique de l’expéditeur doivent connaître où toosend éléments, tandis que les applications de la logique de récepteur n’avez pas besoin tooknow n’est pas défini sur les expéditeurs hello.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-127">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="cfb6f-128">Bonjour [portail Azure](https://portal.azure.com), créez une application de logique avec ce nom : « BatchReceiver »</span><span class="sxs-lookup"><span data-stu-id="cfb6f-128">In hello [Azure portal](https://portal.azure.com), create a logic app with this name: "BatchReceiver"</span></span> 

2. <span data-ttu-id="cfb6f-129">Dans le Concepteur d’applications logique, ajouter hello **lot** déclencheur qui démarre le workflow d’application logique.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-129">In Logic Apps Designer, add hello **Batch** trigger, which starts your logic app workflow.</span></span> <span data-ttu-id="cfb6f-130">Dans la zone de recherche de hello, entrez « batch » comme filtre.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-130">In hello search box, enter "batch" as your filter.</span></span> <span data-ttu-id="cfb6f-131">Sélectionnez le déclencheur **Lot – Traiter les messages par lots**.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-131">Select this trigger: **Batch – Batch messages**</span></span>

   ![Ajout du déclencheur Lot](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. <span data-ttu-id="cfb6f-133">Fournissez un nom pour le traitement par lots hello et spécifiez les critères pour libérer le lot de hello, par exemple :</span><span class="sxs-lookup"><span data-stu-id="cfb6f-133">Provide a name for hello batch, and specify criteria for releasing hello batch, for example:</span></span>

   * <span data-ttu-id="cfb6f-134">**Nom du lot**: hello nom utilisé tooidentify hello lot, c'est-à-dire « TestBatch » dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-134">**Batch Name**: hello name used tooidentify hello batch, which is "TestBatch" in this example.</span></span>
   * <span data-ttu-id="cfb6f-135">**Nombre de messages**: hello du nombre de messages toohold en tant que lot avant de libérer pour le traitement, qui est « 5 » dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-135">**Message Count**: hello number of messages toohold as a batch before releasing for processing, which is "5" in this example.</span></span>

   ![Détails à fournir concernant le déclencheur Lot](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. <span data-ttu-id="cfb6f-137">Ajouter une autre action qui envoie un message électronique au déclenchement de déclenchement du lot hello.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-137">Add another action that sends an email when hello batch trigger fires.</span></span> <span data-ttu-id="cfb6f-138">Chaque lot de hello temps comporte cinq éléments, hello logique application envoie un message électronique.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-138">Each time hello batch has five items, hello logic app sends an email.</span></span>

   1. <span data-ttu-id="cfb6f-139">Sous le déclenchement du lot hello, choisissez **+ nouvelle étape** > **ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-139">Under hello batch trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="cfb6f-140">Dans la zone de recherche de hello, entrez « email » comme filtre.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-140">In hello search box, enter "email" as your filter.</span></span>
   <span data-ttu-id="cfb6f-141">Sélectionnez un connecteur de messagerie en fonction de votre fournisseur de messagerie.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-141">Based on your email provider, select an email connector.</span></span>
   
      <span data-ttu-id="cfb6f-142">Par exemple, si vous avez un compte professionnel ou scolaire, sélectionnez Connecteur Outlook Office 365 de hello.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-142">For example, if you have a work or school account, select hello Office 365 Outlook connector.</span></span> 
      <span data-ttu-id="cfb6f-143">Si vous avez un compte Gmail, sélectionnez le connecteur de Gmail hello.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-143">If you have a Gmail account, select hello Gmail connector.</span></span>

   3. <span data-ttu-id="cfb6f-144">Sélectionnez cette action pour votre connecteur : **{*fournisseur de messagerie*} - Envoyer un message électronique**</span><span class="sxs-lookup"><span data-stu-id="cfb6f-144">Select this action for your connector: **{*email provider*} - Send an email**</span></span>

      <span data-ttu-id="cfb6f-145">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="cfb6f-145">For example:</span></span>

      ![Sélection de l’action « Envoyer un message électronique » pour votre fournisseur de messagerie](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. <span data-ttu-id="cfb6f-147">Si vous n’avez pas déjà créé une connexion pour votre fournisseur de messagerie, entrez votre adresse e-mail et votre mot de passe lorsque vous êtes invité à vous authentifier.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-147">If you didn't previously create a connection for your email provider, provide your email credentials for authentication when prompted.</span></span> <span data-ttu-id="cfb6f-148">En savoir plus sur [l’authentification à l’aide d’une adresse e-mail et d’un mot de passe](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="cfb6f-148">Learn more about [authenticating your email credentials](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

6. <span data-ttu-id="cfb6f-149">Définir les propriétés de hello pour action hello que vous venez d’ajouter.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-149">Set hello properties for hello action you just added.</span></span>

   * <span data-ttu-id="cfb6f-150">Bonjour **à** , entrez l’adresse de messagerie du destinataire hello.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-150">In hello **To** box, enter hello recipient's email address.</span></span> 
   <span data-ttu-id="cfb6f-151">À des fins de test, vous pouvez utiliser votre propre adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-151">For testing purposes, you can use your own email address.</span></span>

   * <span data-ttu-id="cfb6f-152">Bonjour **sujet** boîte lorsque hello **contenu dynamique** liste apparaît, sélectionnez hello **nom de la Partition** champ.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-152">In hello **Subject** box, when hello **Dynamic content** list appears, select hello **Partition Name** field.</span></span>

     ![Dans la liste « Contenu dynamique » hello, sélectionnez « Nom de Partition »](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     <span data-ttu-id="cfb6f-154">Dans une section ultérieure, vous pouvez spécifier une clé de partition unique que le divise hello lot cible dans la logique définit toowhere, vous pouvez envoyer des messages.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-154">In a later section, you can specify a unique partition key that divides hello target batch into logical sets toowhere you can send messages.</span></span> 
     <span data-ttu-id="cfb6f-155">Chaque jeu possède un numéro unique qui est généré par l’application de la logique d’expéditeur hello.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-155">Each set has a unique number that's generated by hello sender logic app.</span></span> 
     <span data-ttu-id="cfb6f-156">Cette fonctionnalité vous permet d’utiliser un lot unique avec plusieurs sous-ensembles et définir chaque sous-ensemble avec nom hello que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-156">This capability lets you use a single batch with multiple subsets and define each subset with hello name that you provide.</span></span>

   * <span data-ttu-id="cfb6f-157">Bonjour **corps** boîte lorsque hello **contenu dynamique** liste apparaît, sélectionnez hello **Id de Message** champ.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-157">In hello **Body** box, when hello **Dynamic content** list appears, select hello **Message Id** field.</span></span>

     ![Pour « Corps », sélectionnez « ID de message »](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     <span data-ttu-id="cfb6f-159">Étant donné que l’entrée hello pour l’action d’envoi de message hello est un tableau, hello concepteur ajoute automatiquement une **pour chaque** boucle autour hello **envoyer un courrier électronique** action.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-159">Because hello input for hello send email action is an array, hello designer automatically adds a **For each** loop around hello **Send an email** action.</span></span> 
     <span data-ttu-id="cfb6f-160">Cette boucle effectue une action interne de hello sur chaque élément dans un lot de hello.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-160">This loop performs hello inner action on each item in hello batch.</span></span> 
     <span data-ttu-id="cfb6f-161">Par conséquent, avec hello lot déclencheur ensemble toofive éléments, vous obtenez des cinq messages électroniques que chaque déclencheur hello de temps est activé.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-161">So, with hello batch trigger set toofive items, you get five emails each time hello trigger fires.</span></span>

7.  <span data-ttu-id="cfb6f-162">Maintenant que vous avez créé l’application logique réceptrice de lots, enregistrez-la.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-162">Now that you created a batch receiver logic app, save your logic app.</span></span>

    ![Enregistrer votre application logique](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a><span data-ttu-id="cfb6f-164">Créer des applications de la logique qui envoient le traitement par lots de messages tooa</span><span class="sxs-lookup"><span data-stu-id="cfb6f-164">Create logic apps that send messages tooa batch</span></span>

<span data-ttu-id="cfb6f-165">À présent créer une ou plusieurs applications de logique qui envoient des éléments toohello lot est définie par l’application de la logique de récepteur hello.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-165">Now create one or more logic apps that send items toohello batch defined by hello receiver logic app.</span></span> <span data-ttu-id="cfb6f-166">Pour un expéditeur hello, vous spécifiez application logique de récepteur hello et nom du lot, contenu du message et tous les autres paramètres.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-166">For hello sender, you specify hello receiver logic app and batch name, message content, and any other settings.</span></span> <span data-ttu-id="cfb6f-167">Vous pouvez éventuellement fournir un lot de hello de toodivide clé de partition unique dans éléments toocollect de sous-ensembles avec cette clé.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-167">You can optionally provide a unique partition key toodivide hello batch into subsets toocollect items with that key.</span></span>

<span data-ttu-id="cfb6f-168">Applications de la logique de l’expéditeur doivent connaître où toosend éléments, tandis que les applications de la logique de récepteur n’avez pas besoin tooknow n’est pas défini sur les expéditeurs hello.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-168">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="cfb6f-169">Créez une autre application logique et nommez-la « BatchSender ».</span><span class="sxs-lookup"><span data-stu-id="cfb6f-169">Create another logic app with this name: "BatchSender"</span></span>

   1. <span data-ttu-id="cfb6f-170">Dans la zone de recherche de hello, entrez « recurrence » comme filtre.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-170">In hello search box, enter "recurrence" as your filter.</span></span> 
   <span data-ttu-id="cfb6f-171">Sélectionnez le déclencheur **Planification - Récurrence**</span><span class="sxs-lookup"><span data-stu-id="cfb6f-171">Select this trigger: **Schedule - Recurrence**</span></span>

      ![Ajouter le déclencheur de hello « Planification Recurrence »](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. <span data-ttu-id="cfb6f-173">Définir la fréquence de hello et intervalle toorun hello expéditeur logique application toutes les minutes.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-173">Set hello frequency and interval toorun hello sender logic app every minute.</span></span>

      ![Définition de la fréquence et de l’intervalle pour le déclencheur Récurrence](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. <span data-ttu-id="cfb6f-175">Ajouter une nouvelle étape pour l’envoi de lot tooa de messages.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-175">Add a new step for sending messages tooa batch.</span></span>

   1. <span data-ttu-id="cfb6f-176">Sous le déclencheur de périodicité hello, choisissez **+ nouvelle étape** > **ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-176">Under hello recurrence trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="cfb6f-177">Dans la zone de recherche de hello, entrez « batch » comme filtre.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-177">In hello search box, enter "batch" as your filter.</span></span> 

   3. <span data-ttu-id="cfb6f-178">Sélectionnez cette action : **envoyer des messages toobatch : choisissez un flux de travail Logic Apps avec déclenchement du lot**</span><span class="sxs-lookup"><span data-stu-id="cfb6f-178">Select this action: **Send messages toobatch – Choose a Logic Apps workflow with batch trigger**</span></span>

      ![Sélectionnez « Envoyer des messages toobatch »](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. <span data-ttu-id="cfb6f-180">Maintenant, sélectionnez l’application logique « BatchReceiver » créée précédemment, qui s’affiche désormais en tant qu’action.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-180">Now select your "BatchReceiver" logic app that you previously created, which now appears as an action.</span></span>

      ![Sélection de l’application logique « BatchReceiver »](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > <span data-ttu-id="cfb6f-182">liste de Hello montre également toutes les autres applications de la logique qui ont des déclencheurs de lot.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-182">hello list also shows any other logic apps that have batch triggers.</span></span>

3. <span data-ttu-id="cfb6f-183">Définir les propriétés de lot hello.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-183">Set hello batch properties.</span></span>

   * <span data-ttu-id="cfb6f-184">**Nom du lot**: nom du lot hello défini par l’application hello récepteur logique, qui est « TestBatch » dans cet exemple est validée lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-184">**Batch Name**: hello batch name defined by hello receiver logic app, which is "TestBatch" in this example and is validated at runtime.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="cfb6f-185">Assurez-vous que vous ne pas modifier le nom du lot hello, qui doit correspondre au nom de lot hello spécifié par l’application de la logique de récepteur hello.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-185">Make sure that you don't change hello batch name, which must match hello batch name that's specified by hello receiver logic app.</span></span>
     > <span data-ttu-id="cfb6f-186">Modification du nom de lot hello provoque l’expéditeur de hello toofail d’application logique.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-186">Changing hello batch name causes hello sender logic app toofail.</span></span>

   * <span data-ttu-id="cfb6f-187">**Contenu du message**: hello du contenu du message que vous souhaitez toosend.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-187">**Message Content**: hello message content that you want toosend.</span></span> 
   <span data-ttu-id="cfb6f-188">Pour cet exemple, ajoutez cette expression que les insertions hello date et heure actuelles dans le message de type hello contenu que vous envoyez un lot de toohello :</span><span class="sxs-lookup"><span data-stu-id="cfb6f-188">For this example, add this expression that inserts hello current date and time into hello message content that you send toohello batch:</span></span>

     1. <span data-ttu-id="cfb6f-189">Hello lorsque **contenu dynamique** liste apparaît, choisissez **Expression**.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-189">When hello **Dynamic content** list appears, choose **Expression**.</span></span> 
     2. <span data-ttu-id="cfb6f-190">Entrez l’expression de hello **utcnow()**, puis choisissez **OK**.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-190">Enter hello expression **utcnow()**, and choose **OK**.</span></span> 

        ![Dans « Contenu du message », choisissez « Expression ».](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. <span data-ttu-id="cfb6f-193">Définir une partition pour le traitement par lots hello.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-193">Now set up a partition for hello batch.</span></span> <span data-ttu-id="cfb6f-194">Bonjour « BatchReceiver » action, choisissez **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-194">In hello "BatchReceiver" action, choose **Show advanced options**.</span></span>

   * <span data-ttu-id="cfb6f-195">**Nom de partition**: un toouse clé de partition unique facultatif permettant de diviser le traitement par lots de hello cible.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-195">**Partition Name**: An optional unique partition key toouse for dividing hello target batch.</span></span> <span data-ttu-id="cfb6f-196">Pour cet exemple, ajoutez une expression qui génère un nombre aléatoire compris entre 1 et 5.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-196">For this example, add an expression that generates a random number between one and five.</span></span>
   
     1. <span data-ttu-id="cfb6f-197">Hello lorsque **contenu dynamique** liste apparaît, choisissez **Expression**.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-197">When hello **Dynamic content** list appears, choose **Expression**.</span></span>
     2. <span data-ttu-id="cfb6f-198">Entrez l’expression **rand(1,6)**.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-198">Enter this expression: **rand(1,6)**</span></span>

        ![Définition d’une partition pour le lot cible](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        <span data-ttu-id="cfb6f-200">Cette fonction **rand** génère un nombre compris entre 1 et 5.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-200">This **rand** function generates a number between one and five.</span></span> 
        <span data-ttu-id="cfb6f-201">Vous divisez donc ce lot en cinq partitions numérotées, définies dynamiquement par cette expression.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-201">So you are dividing this batch into five numbered partitions, which this expression dynamically sets.</span></span>

   * <span data-ttu-id="cfb6f-202">**ID du message** : identificateur de message facultatif. Lorsqu’il est vide, c’est un GUID généré.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-202">**Message Id**: An optional message identifier and is a generated GUID when empty.</span></span> 
   <span data-ttu-id="cfb6f-203">Pour cet exemple, laissez cette zone vide.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-203">For this example, leave this box blank.</span></span>

5. <span data-ttu-id="cfb6f-204">Enregistrez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-204">Save your logic app.</span></span> <span data-ttu-id="cfb6f-205">Votre application de la logique d’expéditeur ressemble exemple toothis similaire :</span><span class="sxs-lookup"><span data-stu-id="cfb6f-205">Your sender logic app now looks similar toothis example:</span></span>

   ![Enregistrement de l’application logique](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a><span data-ttu-id="cfb6f-207">Tester les applications logiques</span><span class="sxs-lookup"><span data-stu-id="cfb6f-207">Test your logic apps</span></span>

<span data-ttu-id="cfb6f-208">tootest votre solution, de traitement par lot laisser vos applications logiques en cours d’exécution pendant quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-208">tootest your batching solution, leave your logic apps running for a few minutes.</span></span> <span data-ttu-id="cfb6f-209">Bientôt, vous commencez à recevoir des messages électroniques dans les groupes de cinq, toutes les données avec hello même clé de partition.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-209">Soon, you start getting emails in groups of five, all with hello same partition key.</span></span>

<span data-ttu-id="cfb6f-210">Votre application de la logique BatchSender s’exécute chaque minute, génère un nombre aléatoire compris entre 1 et 5 et utilise ce numéro généré en tant que clé de partition hello pour le traitement par lots de hello cible où les messages sont envoyés.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-210">Your BatchSender logic app runs every minute, generates a random number between one and five, and uses this generated number as hello partition key for hello target batch where messages are sent.</span></span> <span data-ttu-id="cfb6f-211">Chaque fois que les commandes hello a cinq éléments par hello même clé de partition, votre application de la logique BatchReceiver se déclenche et envoie un message pour chaque message.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-211">Each time hello batch has five items with hello same partition key, your BatchReceiver logic app fires and sends mail for each message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cfb6f-212">Lorsque vous avez terminé de test, assurez-vous que vous désactivez hello BatchSender logique application toostop envoi de messages et évitez de surcharger votre boîte de réception.</span><span class="sxs-lookup"><span data-stu-id="cfb6f-212">When you're done testing, make sure that you disable hello BatchSender logic app toostop sending messages and avoid overloading your inbox.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfb6f-213">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cfb6f-213">Next steps</span></span>

* [<span data-ttu-id="cfb6f-214">Créer des définitions d’application logique à l’aide de JSON</span><span class="sxs-lookup"><span data-stu-id="cfb6f-214">Build on logic app definitions by using JSON</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="cfb6f-215">Créer une application sans serveur dans Visual Studio avec Azure Logic Apps et Azure Functions</span><span class="sxs-lookup"><span data-stu-id="cfb6f-215">Build a serverless app in Visual Studio with Azure Logic Apps and Functions</span></span>](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [<span data-ttu-id="cfb6f-216">Gestion des exceptions et journalisation des erreurs pour les applications logiques</span><span class="sxs-lookup"><span data-stu-id="cfb6f-216">Exception handling and error logging for logic apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
