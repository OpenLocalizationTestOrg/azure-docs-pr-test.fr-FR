---
title: aaaLearn comment toouse hello connecteur MQ dans Azure Logic Apps | Documents Microsoft
description: "Se connecter tooan sur site ou serveur Azure à partir de votre toobrowse de flux de travail d’application logique, recevoir et envoyer des messages tooWebSphere MQ"
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a><span data-ttu-id="40ccd-103">Se connecter tooan IBM MQ server à partir d’applications logique à l’aide du connecteur MQ hello</span><span class="sxs-lookup"><span data-stu-id="40ccd-103">Connect tooan IBM MQ server from logic apps using hello MQ connector</span></span> 

<span data-ttu-id="40ccd-104">Microsoft Connector pour MQ envoie et récupère les messages stockés dans un serveur MQ local ou dans Azure.</span><span class="sxs-lookup"><span data-stu-id="40ccd-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="40ccd-105">Ce connecteur inclut un client Microsoft MQ qui communique avec un serveur IBM MQ distant sur un réseau TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="40ccd-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="40ccd-106">Ce document est un connecteur de starter guide toouse hello MQ.</span><span class="sxs-lookup"><span data-stu-id="40ccd-106">This document is a starter guide toouse hello MQ connector.</span></span> <span data-ttu-id="40ccd-107">Nous vous recommandons de commencer en parcourant un seul message dans une file d’attente, et puis que vous essayez de hello autres actions.</span><span class="sxs-lookup"><span data-stu-id="40ccd-107">We recommended you begin by browsing a single message on a queue, and then trying hello other actions.</span></span>    

<span data-ttu-id="40ccd-108">connecteur MQ Hello inclut hello suivant des actions.</span><span class="sxs-lookup"><span data-stu-id="40ccd-108">hello MQ connector includes hello following actions.</span></span> <span data-ttu-id="40ccd-109">Il n’y a aucun déclencheur.</span><span class="sxs-lookup"><span data-stu-id="40ccd-109">There are no triggers.</span></span>

-   <span data-ttu-id="40ccd-110">Parcourir un seul message sans supprimer le message de type hello hello IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="40ccd-110">Browse a single message without deleting hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="40ccd-111">Parcourir un lot de messages sans supprimer les messages hello hello IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="40ccd-111">Browse a batch of messages without deleting hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="40ccd-112">Un seul message de réception et supprimer message de type hello hello IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="40ccd-112">Receive a single message and delete hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="40ccd-113">Réception d’un lot de messages et supprimer des messages de type hello hello IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="40ccd-113">Receive a batch of messages and delete hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="40ccd-114">Envoyer un message unique de toohello IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="40ccd-114">Send a single message toohello IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="40ccd-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="40ccd-115">Prerequisites</span></span>

* <span data-ttu-id="40ccd-116">Si vous utilisez un serveur local, [installer la passerelle de données locale hello](../logic-apps/logic-apps-gateway-install.md) sur un serveur au sein de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="40ccd-116">If using an on-premises MQ server, [install hello on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="40ccd-117">Si hello MQ Server est publiquement disponible ou disponible dans Azure, puis la passerelle de données hello est non utilisée ou requises.</span><span class="sxs-lookup"><span data-stu-id="40ccd-117">If hello MQ Server is publicly available, or available within Azure, then hello data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="40ccd-118">serveur Hello où hello passerelle de données locale est installée doit être également installé .net Framework 4.6 est installé pour hello MQ connecteur toofunction.</span><span class="sxs-lookup"><span data-stu-id="40ccd-118">hello server where hello On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for hello MQ Connector toofunction.</span></span>

* <span data-ttu-id="40ccd-119">Créer hello des ressources Azure pour la passerelle de données locale hello - [configurer la connexion de passerelle de données hello](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="40ccd-119">Create hello Azure resource for hello on-premises data gateway - [Set up hello data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="40ccd-120">Versions d’IBM WebSphere MQ Officiellement prises en charge :</span><span class="sxs-lookup"><span data-stu-id="40ccd-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="40ccd-121">MQ 7.5</span><span class="sxs-lookup"><span data-stu-id="40ccd-121">MQ 7.5</span></span>
   * <span data-ttu-id="40ccd-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="40ccd-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="40ccd-123">Créer une application logique</span><span class="sxs-lookup"><span data-stu-id="40ccd-123">Create a logic app</span></span>

1. <span data-ttu-id="40ccd-124">Bonjour **Azure démarrer carte**, sélectionnez  **+**  (signe plus), **Web + Mobile**, puis **application logique**.</span><span class="sxs-lookup"><span data-stu-id="40ccd-124">In hello **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="40ccd-125">Entrez hello **nom**, telles que MQTestApp, **abonnement**, **groupe de ressources**, et **emplacement** (utiliser un emplacement de hello où hello connexion à la passerelle de données locale est configurée).</span><span class="sxs-lookup"><span data-stu-id="40ccd-125">Enter hello **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use hello location where hello on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="40ccd-126">Sélectionnez **code confidentiel toodashboard**, puis sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="40ccd-126">Select **Pin toodashboard**, and select **Create**.</span></span>  
<span data-ttu-id="40ccd-127">![Créer une application logique](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="40ccd-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="40ccd-128">Ajouter un déclencheur</span><span class="sxs-lookup"><span data-stu-id="40ccd-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="40ccd-129">Hello MQ connecteur n’a pas de déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="40ccd-129">hello MQ Connector does not have any triggers.</span></span> <span data-ttu-id="40ccd-130">Par conséquent, utilisez un autre déclencheur toostart votre application logique, par exemple hello **périodicité** déclencheur.</span><span class="sxs-lookup"><span data-stu-id="40ccd-130">So, use another trigger toostart your logic app, such as hello **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="40ccd-131">Hello **Concepteur d’applications logique** s’ouvre, sélectionnez **périodicité** dans la liste hello de déclencheurs courantes.</span><span class="sxs-lookup"><span data-stu-id="40ccd-131">hello **Logic Apps Designer** opens, select **Recurrence** in hello list of common triggers.</span></span>
2. <span data-ttu-id="40ccd-132">Sélectionnez **modifier** dans hello déclencheur de périodicité.</span><span class="sxs-lookup"><span data-stu-id="40ccd-132">Select **Edit** within hello Recurrence Trigger.</span></span> 
3. <span data-ttu-id="40ccd-133">Ensemble hello **fréquence** trop**jour**et ensemble hello **intervalle** trop**7**.</span><span class="sxs-lookup"><span data-stu-id="40ccd-133">Set hello **Frequency** too**Day**, and set hello **Interval** too**7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="40ccd-134">Parcourir un seul message</span><span class="sxs-lookup"><span data-stu-id="40ccd-134">Browse a single message</span></span>
1. <span data-ttu-id="40ccd-135">Sélectionnez **+Nouvelle étape**, puis **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="40ccd-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="40ccd-136">Dans la zone de recherche de hello, tapez `mq`, puis sélectionnez **MQ - Parcourir message**.</span><span class="sxs-lookup"><span data-stu-id="40ccd-136">In hello search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="40ccd-137">![Parcourir un message](media/connectors-create-api-mq/Browse_message.png)</span><span class="sxs-lookup"><span data-stu-id="40ccd-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="40ccd-138">En l’absence d’une connexion MQ existante, puis créez des connexions de hello :</span><span class="sxs-lookup"><span data-stu-id="40ccd-138">If there isn't an existing MQ connection, then create hello connection:</span></span>  

    1. <span data-ttu-id="40ccd-139">Sélectionnez **se connecter via la passerelle de données locale**et entrez les propriétés hello de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="40ccd-139">Select **Connect via on-premises data gateway**, and enter hello properties of your MQ server.</span></span>  
    <span data-ttu-id="40ccd-140">Pour **Server**, vous pouvez entrer le nom du serveur MQ hello ou entrez l’adresse hello suivie d’un signe deux-points et hello le numéro de port.</span><span class="sxs-lookup"><span data-stu-id="40ccd-140">For **Server**, you can enter hello MQ server name, or enter hello IP address followed by a colon and hello port number.</span></span> 
    2. <span data-ttu-id="40ccd-141">Hello **passerelle** liste déroulante répertorie toutes les connexions de passerelle existantes qui ont été configurées.</span><span class="sxs-lookup"><span data-stu-id="40ccd-141">hello **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="40ccd-142">Sélectionnez votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="40ccd-142">Select your gateway.</span></span>
    3. <span data-ttu-id="40ccd-143">Lorsque vous avez terminé, sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="40ccd-143">Select **Create** when finished.</span></span> <span data-ttu-id="40ccd-144">Votre connexion semble similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="40ccd-144">Your connection looks similar toohello following:</span></span>   
    <span data-ttu-id="40ccd-145">![Propriétés de connexion](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="40ccd-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="40ccd-146">Dans les propriétés d’une action hello, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="40ccd-146">In hello action properties, you can:</span></span>  

    * <span data-ttu-id="40ccd-147">Hello d’utilisation **file d’attente** propriété tooaccess un nom de file d’attente différent que celui défini dans la connexion de hello</span><span class="sxs-lookup"><span data-stu-id="40ccd-147">Use hello **Queue** property tooaccess a different queue name than what is defined in hello connection</span></span>
    * <span data-ttu-id="40ccd-148">Hello d’utilisation **MessageId**, **CorrelationId**, **GroupId**et autres toobrowse propriétés d’un message en fonction des propriétés de message hello différents MQ</span><span class="sxs-lookup"><span data-stu-id="40ccd-148">Use hello **MessageId**, **CorrelationId**, **GroupId**, and other properties toobrowse for a message based on hello different MQ message properties</span></span>
    * <span data-ttu-id="40ccd-149">Définissez **IncludeInfo** trop**True** tooinclude informations supplémentaires dans la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="40ccd-149">Set **IncludeInfo** too**True** tooinclude additional message information in hello output.</span></span> <span data-ttu-id="40ccd-150">Ou, définissez-le trop**False** toonot inclure des informations supplémentaires dans une sortie hello.</span><span class="sxs-lookup"><span data-stu-id="40ccd-150">Or, set it too**False** toonot include additional message information in hello output.</span></span>
    * <span data-ttu-id="40ccd-151">Entrez un **délai d’attente** valeur toodetermine toowait combien de temps pour un message tooarrive dans une file d’attente vide.</span><span class="sxs-lookup"><span data-stu-id="40ccd-151">Enter a **Timeout** value toodetermine how long toowait for a message tooarrive in an empty queue.</span></span> <span data-ttu-id="40ccd-152">Si aucune valeur n’est entrée, hello premier message de file d’attente hello est récupérée et il n’existe aucun temps d’attente pour un tooappear de message.</span><span class="sxs-lookup"><span data-stu-id="40ccd-152">If nothing is entered, hello first message in hello queue is retrieved, and there is no time spent waiting for a message tooappear.</span></span>  
    <span data-ttu-id="40ccd-153">![Parcourir les propriétés d’un message](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="40ccd-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="40ccd-154">**Enregistrez** vos modifications, puis **exécutez** votre application logique :</span><span class="sxs-lookup"><span data-stu-id="40ccd-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="40ccd-155">![Enregistrer et exécuter](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="40ccd-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="40ccd-156">Après quelques secondes, étapes hello Hello exécuter sont affichées et vous pouvez examiner la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="40ccd-156">After a few seconds, hello steps of hello run are shown, and you can look at hello output.</span></span> <span data-ttu-id="40ccd-157">Sélectionnez hello coche verte toosee détails de chaque étape.</span><span class="sxs-lookup"><span data-stu-id="40ccd-157">Select hello green checkmark toosee details of each step.</span></span> <span data-ttu-id="40ccd-158">Sélectionnez **consultez sorties brutes** toosee des détails supplémentaires sur hello les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="40ccd-158">Select **See raw outputs** toosee additional details on hello output data.</span></span>  
<span data-ttu-id="40ccd-159">![Parcourir une sortie de message](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="40ccd-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="40ccd-160">Sortie brute :</span><span class="sxs-lookup"><span data-stu-id="40ccd-160">Raw output:</span></span>  
    ![Parcourir une sortie brute de message](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="40ccd-162">Hello lorsque **IncludeInfo** option a la valeur tootrue, hello suivant la sortie s’affiche :</span><span class="sxs-lookup"><span data-stu-id="40ccd-162">When hello **IncludeInfo** option is set tootrue, hello following output is displayed:</span></span>  
<span data-ttu-id="40ccd-163">![Parcourir les informations include d’un message](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="40ccd-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="40ccd-164">Parcourir plusieurs messages</span><span class="sxs-lookup"><span data-stu-id="40ccd-164">Browse multiple messages</span></span>
<span data-ttu-id="40ccd-165">Hello **parcourir les messages** action inclut un **BatchSize** option tooindicate combien de messages doit être retourné à partir de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="40ccd-165">hello **Browse messages** action includes a **BatchSize** option tooindicate how many messages should be returned from hello queue.</span></span>  <span data-ttu-id="40ccd-166">Si l’option **BatchSize** ne comporte aucune entrée, tous les messages sont retournés.</span><span class="sxs-lookup"><span data-stu-id="40ccd-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="40ccd-167">Hello retourné un tableau de messages.</span><span class="sxs-lookup"><span data-stu-id="40ccd-167">hello returned output is an array of messages.</span></span>

1. <span data-ttu-id="40ccd-168">Lors de l’ajout de hello **parcourir les messages** action, hello première connexion qui est configurée est sélectionnée par défaut.</span><span class="sxs-lookup"><span data-stu-id="40ccd-168">When adding hello **Browse messages** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="40ccd-169">Sélectionnez **modifier la connexion** toocreate une nouvelle connexion, ou sélectionnez une autre connexion.</span><span class="sxs-lookup"><span data-stu-id="40ccd-169">Select **Change connection** toocreate a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="40ccd-170">sortie Hello de parcourir les messages montre :</span><span class="sxs-lookup"><span data-stu-id="40ccd-170">hello output of Browse messages shows:</span></span>  
![Parcourir la sortie des messages](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="40ccd-172">Recevoir un seul message</span><span class="sxs-lookup"><span data-stu-id="40ccd-172">Receive a single message</span></span>
<span data-ttu-id="40ccd-173">Hello **recevoir un message** action a hello des mêmes entrées et sorties en tant que hello **Parcourir message** action.</span><span class="sxs-lookup"><span data-stu-id="40ccd-173">hello **Receive message** action has hello same inputs and outputs as hello **Browse message** action.</span></span> <span data-ttu-id="40ccd-174">Lorsque vous utilisez **recevoir un message**, message de type hello est supprimé de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="40ccd-174">When using **Receive message**, hello message is deleted from hello queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="40ccd-175">Recevoir plusieurs messages</span><span class="sxs-lookup"><span data-stu-id="40ccd-175">Receive multiple messages</span></span>
<span data-ttu-id="40ccd-176">Hello **recevoir des messages** action a hello des mêmes entrées et sorties en tant que hello **parcourir les messages** action.</span><span class="sxs-lookup"><span data-stu-id="40ccd-176">hello **Receive messages** action has hello same inputs and outputs as hello **Browse messages** action.</span></span> <span data-ttu-id="40ccd-177">Lorsque vous utilisez **recevoir des messages**, messages hello sont supprimés de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="40ccd-177">When using **Receive messages**, hello messages are deleted from hello queue.</span></span>

<span data-ttu-id="40ccd-178">S’il n’existe aucun message dans la file d’attente hello lorsque vous effectuez une recherche ou une opération de réception, étape de hello échoue avec hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="40ccd-178">If there are no messages in hello queue when doing a browse or a receive, hello step fails with hello following output:</span></span>  
![Erreur MQ Aucun message](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="40ccd-180">Envoyer un message</span><span class="sxs-lookup"><span data-stu-id="40ccd-180">Send a message</span></span>
1. <span data-ttu-id="40ccd-181">Lors de l’ajout de hello **envoyer le message** action, hello première connexion qui est configurée est sélectionnée par défaut.</span><span class="sxs-lookup"><span data-stu-id="40ccd-181">When adding hello **Send message** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="40ccd-182">Sélectionnez **modifier la connexion** toocreate une nouvelle connexion, ou sélectionnez une autre connexion.</span><span class="sxs-lookup"><span data-stu-id="40ccd-182">Select **Change connection** toocreate a new connection, or select a different connection.</span></span> <span data-ttu-id="40ccd-183">Hello valide **Types de messages** sont **datagramme**, **réponse**, ou **demande**.</span><span class="sxs-lookup"><span data-stu-id="40ccd-183">hello valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="40ccd-184">![Propriétés d’envoi des messages](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="40ccd-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="40ccd-185">Hello sortie d’envoyer le message ressemble à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="40ccd-185">hello output of Send message looks like hello following:</span></span>  
![Sortie Envoyer un message](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="40ccd-187">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="40ccd-187">Connector-specific details</span></span>

<span data-ttu-id="40ccd-188">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/mq/).</span><span class="sxs-lookup"><span data-stu-id="40ccd-188">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="40ccd-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="40ccd-189">Next steps</span></span>
<span data-ttu-id="40ccd-190">[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="40ccd-190">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="40ccd-191">Explorer hello tous les autres connecteurs disponibles dans les applications logique à notre [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="40ccd-191">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
