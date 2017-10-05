---
title: "Découvrir comment utiliser le connecteur MQ dans Azure Logic Apps | Microsoft Docs"
description: "Connectez-vous à un serveur MQ local ou dans Azure à partir de votre flux de travail d’application logique pour parcourir, recevoir et envoyer des messages dans WebSphere MQ"
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
ms.openlocfilehash: 17c651585b56dae186286f5d8c68c363ae9c524d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-to-an-ibm-mq-server-from-logic-apps-using-the-mq-connector"></a><span data-ttu-id="ea24c-103">Se connecter à un serveur IBM MQ à partir d’applications logiques à l’aide du connecteur MQ</span><span class="sxs-lookup"><span data-stu-id="ea24c-103">Connect to an IBM MQ server from logic apps using the MQ connector</span></span> 

<span data-ttu-id="ea24c-104">Microsoft Connector pour MQ envoie et récupère les messages stockés dans un serveur MQ local ou dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ea24c-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="ea24c-105">Ce connecteur inclut un client Microsoft MQ qui communique avec un serveur IBM MQ distant sur un réseau TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="ea24c-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="ea24c-106">Ce document est un guide de démarrage pour l’utilisation du connecteur MQ.</span><span class="sxs-lookup"><span data-stu-id="ea24c-106">This document is a starter guide to use the MQ connector.</span></span> <span data-ttu-id="ea24c-107">Nous vous recommandons de commencer par parcourir un message dans une file d’attente, puis de tenter les autres actions.</span><span class="sxs-lookup"><span data-stu-id="ea24c-107">We recommended you begin by browsing a single message on a queue, and then trying the other actions.</span></span>    

<span data-ttu-id="ea24c-108">Le connecteur MQ inclut les actions suivantes.</span><span class="sxs-lookup"><span data-stu-id="ea24c-108">The MQ connector includes the following actions.</span></span> <span data-ttu-id="ea24c-109">Il n’y a aucun déclencheur.</span><span class="sxs-lookup"><span data-stu-id="ea24c-109">There are no triggers.</span></span>

-   <span data-ttu-id="ea24c-110">Parcourir un seul message sans le supprimer du serveur IBM MQ</span><span class="sxs-lookup"><span data-stu-id="ea24c-110">Browse a single message without deleting the message from the IBM MQ Server</span></span>
-   <span data-ttu-id="ea24c-111">Parcourir un lot de messages sans supprimer ceux-ci du serveur IBM MQ</span><span class="sxs-lookup"><span data-stu-id="ea24c-111">Browse a batch of messages without deleting the messages from the IBM MQ Server</span></span>
-   <span data-ttu-id="ea24c-112">Recevoir un message unique et supprimer le message à partir du serveur IBM MQ</span><span class="sxs-lookup"><span data-stu-id="ea24c-112">Receive a single message and delete the message from the IBM MQ Server</span></span>
-   <span data-ttu-id="ea24c-113">Recevoir un lot de messages et supprimer les messages du serveur IBM MQ</span><span class="sxs-lookup"><span data-stu-id="ea24c-113">Receive a batch of messages and delete the messages from the IBM MQ Server</span></span>
-   <span data-ttu-id="ea24c-114">Envoyer un message unique au serveur IBM MQ</span><span class="sxs-lookup"><span data-stu-id="ea24c-114">Send a single message to the IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ea24c-115">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="ea24c-115">Prerequisites</span></span>

* <span data-ttu-id="ea24c-116">Si vous utilisez un serveur MQ local, [installez la passerelle de données locale](../logic-apps/logic-apps-gateway-install.md) sur un serveur au sein de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="ea24c-116">If using an on-premises MQ server, [install the on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="ea24c-117">Si le serveur MQ est disponible publiquement ou dans Azure, la passerelle de données n’est pas utilisée ou nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ea24c-117">If the MQ Server is publicly available, or available within Azure, then the data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ea24c-118">Pour que le connecteur MQ fonctionne, .Net Framework 4.6 doit également être installé sur le serveur sur lequel la passerelle de données locale est installée.</span><span class="sxs-lookup"><span data-stu-id="ea24c-118">The server where the On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for the MQ Connector to function.</span></span>

* <span data-ttu-id="ea24c-119">Créez la ressource Azure pour la passerelle de données locale : [configurer la connexion de passerelle de données](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="ea24c-119">Create the Azure resource for the on-premises data gateway - [Set up the data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="ea24c-120">Versions d’IBM WebSphere MQ Officiellement prises en charge :</span><span class="sxs-lookup"><span data-stu-id="ea24c-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="ea24c-121">MQ 7.5</span><span class="sxs-lookup"><span data-stu-id="ea24c-121">MQ 7.5</span></span>
   * <span data-ttu-id="ea24c-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="ea24c-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="ea24c-123">Créer une application logique</span><span class="sxs-lookup"><span data-stu-id="ea24c-123">Create a logic app</span></span>

1. <span data-ttu-id="ea24c-124">Dans le **Panneau de démarrage Azure**, sélectionnez **+** (signe plus), **Web + mobile**, puis **Application logique**.</span><span class="sxs-lookup"><span data-stu-id="ea24c-124">In the **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="ea24c-125">Entrez le **Nom**, par exemple, MQTestApp, l’**Abonnement**, le **Groupe de ressources** et l’**Emplacement** (utilisez l’emplacement où la connexion de passerelle de données locale est configurée).</span><span class="sxs-lookup"><span data-stu-id="ea24c-125">Enter the **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use the location where the on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="ea24c-126">Sélectionnez **Épingler au tableau de bord**, puis sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ea24c-126">Select **Pin to dashboard**, and select **Create**.</span></span>  
<span data-ttu-id="ea24c-127">![Créer une application logique](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="ea24c-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="ea24c-128">Ajouter un déclencheur</span><span class="sxs-lookup"><span data-stu-id="ea24c-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="ea24c-129">Le connecteur MQ ne possède aucun déclencheur.</span><span class="sxs-lookup"><span data-stu-id="ea24c-129">The MQ Connector does not have any triggers.</span></span> <span data-ttu-id="ea24c-130">Par conséquent, utilisez un autre déclencheur pour démarrer votre application logique, tel que le déclencheur de **périodicité**.</span><span class="sxs-lookup"><span data-stu-id="ea24c-130">So, use another trigger to start your logic app, such as the **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="ea24c-131">Le **Concepteur d’applications logique** s’ouvre. Sélectionnez **Périodicité** dans la liste des déclencheurs courants.</span><span class="sxs-lookup"><span data-stu-id="ea24c-131">The **Logic Apps Designer** opens, select **Recurrence** in the list of common triggers.</span></span>
2. <span data-ttu-id="ea24c-132">Sélectionnez **Modifier** dans le déclencheur de périodicité.</span><span class="sxs-lookup"><span data-stu-id="ea24c-132">Select **Edit** within the Recurrence Trigger.</span></span> 
3. <span data-ttu-id="ea24c-133">Définissez la **Fréquence** sur **Jour** et l’**Intervalle** sur **7**.</span><span class="sxs-lookup"><span data-stu-id="ea24c-133">Set the **Frequency** to **Day**, and set the **Interval** to **7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="ea24c-134">Parcourir un seul message</span><span class="sxs-lookup"><span data-stu-id="ea24c-134">Browse a single message</span></span>
1. <span data-ttu-id="ea24c-135">Sélectionnez **+Nouvelle étape**, puis **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="ea24c-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="ea24c-136">Dans la zone de recherche, tapez `mq`, puis sélectionnez **MQ - Parcourir un message**.</span><span class="sxs-lookup"><span data-stu-id="ea24c-136">In the search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="ea24c-137">![Parcourir un message](media/connectors-create-api-mq/Browse_message.png)</span><span class="sxs-lookup"><span data-stu-id="ea24c-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="ea24c-138">À défaut de connexion MQ existante, créez la connexion :</span><span class="sxs-lookup"><span data-stu-id="ea24c-138">If there isn't an existing MQ connection, then create the connection:</span></span>  

    1. <span data-ttu-id="ea24c-139">Sélectionnez **Connect via on-premises data gateway** (Se connecter via la passerelle de données locale), puis entrez les propriétés de votre serveur MQ.</span><span class="sxs-lookup"><span data-stu-id="ea24c-139">Select **Connect via on-premises data gateway**, and enter the properties of your MQ server.</span></span>  
    <span data-ttu-id="ea24c-140">Pour **Serveur**, vous pouvez entrer le nom du serveur MQ, ou l’adresse IP suivie par un signe deux-points et le numéro de port.</span><span class="sxs-lookup"><span data-stu-id="ea24c-140">For **Server**, you can enter the MQ server name, or enter the IP address followed by a colon and the port number.</span></span> 
    2. <span data-ttu-id="ea24c-141">Le menu déroulant **Passerelle** répertorie toutes les connexions de passerelle existantes qui ont été configurées.</span><span class="sxs-lookup"><span data-stu-id="ea24c-141">The **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="ea24c-142">Sélectionnez votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="ea24c-142">Select your gateway.</span></span>
    3. <span data-ttu-id="ea24c-143">Lorsque vous avez terminé, sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ea24c-143">Select **Create** when finished.</span></span> <span data-ttu-id="ea24c-144">Votre connexion ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ea24c-144">Your connection looks similar to the following:</span></span>   
    <span data-ttu-id="ea24c-145">![Propriétés de connexion](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="ea24c-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="ea24c-146">Dans les propriétés de l’action, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="ea24c-146">In the action properties, you can:</span></span>  

    * <span data-ttu-id="ea24c-147">utiliser la propriété **Queue** pour accéder à un nom de file d’attente autre que celui défini dans la connexion ;</span><span class="sxs-lookup"><span data-stu-id="ea24c-147">Use the **Queue** property to access a different queue name than what is defined in the connection</span></span>
    * <span data-ttu-id="ea24c-148">utiliser les propriétés **MessageId**, **CorrelationId**, **GroupId** et autres pour rechercher un message sur la base des différentes propriétés de message MQ ;</span><span class="sxs-lookup"><span data-stu-id="ea24c-148">Use the **MessageId**, **CorrelationId**, **GroupId**, and other properties to browse for a message based on the different MQ message properties</span></span>
    * <span data-ttu-id="ea24c-149">définir la propriété **IncludeInfo** sur **True** pour inclure des informations supplémentaires dans la sortie,</span><span class="sxs-lookup"><span data-stu-id="ea24c-149">Set **IncludeInfo** to **True** to include additional message information in the output.</span></span> <span data-ttu-id="ea24c-150">ou la définir sur **False** pour ne pas inclure des informations de message supplémentaires dans la sortie ;</span><span class="sxs-lookup"><span data-stu-id="ea24c-150">Or, set it to **False** to not include additional message information in the output.</span></span>
    * <span data-ttu-id="ea24c-151">entrer une valeur de **délai d’attente** pour déterminer la durée d’attente de l’arrivée d’un message dans une file d’attente vide.</span><span class="sxs-lookup"><span data-stu-id="ea24c-151">Enter a **Timeout** value to determine how long to wait for a message to arrive in an empty queue.</span></span> <span data-ttu-id="ea24c-152">Si aucune valeur n’est entrée, le premier message dans la file d’attente est récupéré et aucun temps n’est consacré à l’attente de l’affichage d’un message.</span><span class="sxs-lookup"><span data-stu-id="ea24c-152">If nothing is entered, the first message in the queue is retrieved, and there is no time spent waiting for a message to appear.</span></span>  
    <span data-ttu-id="ea24c-153">![Parcourir les propriétés d’un message](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="ea24c-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="ea24c-154">**Enregistrez** vos modifications, puis **exécutez** votre application logique :</span><span class="sxs-lookup"><span data-stu-id="ea24c-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="ea24c-155">![Enregistrer et exécuter](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="ea24c-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="ea24c-156">Après quelques secondes, les étapes de l’exécution sont affichées, et vous pouvez consulter la sortie.</span><span class="sxs-lookup"><span data-stu-id="ea24c-156">After a few seconds, the steps of the run are shown, and you can look at the output.</span></span> <span data-ttu-id="ea24c-157">Sélectionnez la coche verte pour afficher les détails de chaque étape.</span><span class="sxs-lookup"><span data-stu-id="ea24c-157">Select the green checkmark to see details of each step.</span></span> <span data-ttu-id="ea24c-158">Pour consulter des détails supplémentaires sur les données de sortie, sélectionnez **Afficher les sorties brutes**.</span><span class="sxs-lookup"><span data-stu-id="ea24c-158">Select **See raw outputs** to see additional details on the output data.</span></span>  
<span data-ttu-id="ea24c-159">![Parcourir une sortie de message](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="ea24c-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="ea24c-160">Sortie brute :</span><span class="sxs-lookup"><span data-stu-id="ea24c-160">Raw output:</span></span>  
    ![Parcourir une sortie brute de message](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="ea24c-162">Quand l’option **IncludeInfo** est définie sur true, la sortie suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="ea24c-162">When the **IncludeInfo** option is set to true, the following output is displayed:</span></span>  
<span data-ttu-id="ea24c-163">![Parcourir les informations include d’un message](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="ea24c-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="ea24c-164">Parcourir plusieurs messages</span><span class="sxs-lookup"><span data-stu-id="ea24c-164">Browse multiple messages</span></span>
<span data-ttu-id="ea24c-165">L’action **Parcourir des messages** inclut une option **BatchSize** permettant d’indiquer le nombre de messages à retourner à partir de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="ea24c-165">The **Browse messages** action includes a **BatchSize** option to indicate how many messages should be returned from the queue.</span></span>  <span data-ttu-id="ea24c-166">Si l’option **BatchSize** ne comporte aucune entrée, tous les messages sont retournés.</span><span class="sxs-lookup"><span data-stu-id="ea24c-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="ea24c-167">La sortie retournée est un tableau de messages.</span><span class="sxs-lookup"><span data-stu-id="ea24c-167">The returned output is an array of messages.</span></span>

1. <span data-ttu-id="ea24c-168">Lorsque vous ajoutez l’action **Parcourir les messages**, la première connexion configurée est sélectionnée par défaut.</span><span class="sxs-lookup"><span data-stu-id="ea24c-168">When adding the **Browse messages** action, the first connection that is configured is selected by default.</span></span> <span data-ttu-id="ea24c-169">Sélectionnez **Modifier la connexion** pour créer une connexion, ou sélectionnez une autre connexion.</span><span class="sxs-lookup"><span data-stu-id="ea24c-169">Select **Change connection** to create a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="ea24c-170">La sortie de Parcourir les messages affiche ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ea24c-170">The output of Browse messages shows:</span></span>  
![Parcourir la sortie des messages](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="ea24c-172">Recevoir un seul message</span><span class="sxs-lookup"><span data-stu-id="ea24c-172">Receive a single message</span></span>
<span data-ttu-id="ea24c-173">L’action **Recevoir un message** a les mêmes entrées et sorties que l’action **Parcourir un message**.</span><span class="sxs-lookup"><span data-stu-id="ea24c-173">The **Receive message** action has the same inputs and outputs as the **Browse message** action.</span></span> <span data-ttu-id="ea24c-174">Lorsque vous utilisez l’action **Recevoir un message**, le message est supprimé de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="ea24c-174">When using **Receive message**, the message is deleted from the queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="ea24c-175">Recevoir plusieurs messages</span><span class="sxs-lookup"><span data-stu-id="ea24c-175">Receive multiple messages</span></span>
<span data-ttu-id="ea24c-176">L’action **Recevoir des messages** a les mêmes entrées et sorties que l’action **Parcourir des messages**.</span><span class="sxs-lookup"><span data-stu-id="ea24c-176">The **Receive messages** action has the same inputs and outputs as the **Browse messages** action.</span></span> <span data-ttu-id="ea24c-177">Lorsque vous utilisez l’action **Recevoir des messages**, les messages sont supprimés de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="ea24c-177">When using **Receive messages**, the messages are deleted from the queue.</span></span>

<span data-ttu-id="ea24c-178">S’il n’existe aucun message dans la file d’attente lorsque vous effectuez une opération de recherche ou de réception, l’opération échoue en affichant la sortie suivante :</span><span class="sxs-lookup"><span data-stu-id="ea24c-178">If there are no messages in the queue when doing a browse or a receive, the step fails with the following output:</span></span>  
![Erreur MQ Aucun message](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="ea24c-180">Envoyer un message</span><span class="sxs-lookup"><span data-stu-id="ea24c-180">Send a message</span></span>
1. <span data-ttu-id="ea24c-181">Lorsque vous ajoutez l’action **Envoyer un message**, la première connexion configurée est sélectionnée par défaut.</span><span class="sxs-lookup"><span data-stu-id="ea24c-181">When adding the **Send message** action, the first connection that is configured is selected by default.</span></span> <span data-ttu-id="ea24c-182">Sélectionnez **Modifier la connexion** pour créer une connexion, ou sélectionnez une autre connexion.</span><span class="sxs-lookup"><span data-stu-id="ea24c-182">Select **Change connection** to create a new connection, or select a different connection.</span></span> <span data-ttu-id="ea24c-183">Les **Types de messages** valides sont **Datagramme**, **Réponse** ou **Demande**.</span><span class="sxs-lookup"><span data-stu-id="ea24c-183">The valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="ea24c-184">![Propriétés d’envoi des messages](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="ea24c-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="ea24c-185">La sortie de l’opération Envoyer un message ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="ea24c-185">The output of Send message looks like the following:</span></span>  
![Sortie Envoyer un message](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="ea24c-187">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="ea24c-187">Connector-specific details</span></span>

<span data-ttu-id="ea24c-188">Consultez tous les déclencheurs et les actions définies dans le swagger, ainsi que les éventuelles limites dans les [détails des connecteurs](/connectors/mq/).</span><span class="sxs-lookup"><span data-stu-id="ea24c-188">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea24c-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ea24c-189">Next steps</span></span>
<span data-ttu-id="ea24c-190">[Créez une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ea24c-190">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="ea24c-191">Explorez les autres connecteurs disponibles dans les applications logiques en consultant notre [liste d’API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="ea24c-191">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
