---
title: "Enregistrement des événements sur Azure Event Hubs dans Gestion des API Azure | Microsoft Docs"
description: "Découvrez comment enregistrer des événements sur Azure Event Hubs dans Gestion des API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 88f6507d-7460-4eb2-bffd-76025b73f8c4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: a310236179677046ec49930b07cfdffdadc37974
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-log-events-to-azure-event-hubs-in-azure-api-management"></a><span data-ttu-id="19ae3-103">Comment enregistrer des événements sur Azure Event Hubs dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="19ae3-103">How to log events to Azure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="19ae3-104">Les concentrateurs d'événements Azure sont un service d'entrée de données hautement évolutif qui peut traiter des millions d'événements par seconde afin que vous puissiez traiter et analyser les grandes quantités de données générées par vos périphériques connectés et vos applications.</span><span class="sxs-lookup"><span data-stu-id="19ae3-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="19ae3-105">Les concentrateurs d'événements fonctionnent comme la « porte d'entrée » d’un pipeline d’événements, et une fois que les données sont collectées dans un concentrateur d'événements, elles peuvent être transformées et stockées à l'aide de n'importe quel fournisseur d'analyse en temps réel ou d’adaptateurs de traitement par lot ou de stockage.</span><span class="sxs-lookup"><span data-stu-id="19ae3-105">Event Hubs acts as the "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="19ae3-106">Les concentrateurs d'événements dissocient la production d'un flux d'événements de la consommation de ces événements, de manière à ce que les consommateurs d'événements puissent accéder aux événements selon leur propre planification.</span><span class="sxs-lookup"><span data-stu-id="19ae3-106">Event Hubs decouples the production of a stream of events from the consumption of those events, so that event consumers can access the events on their own schedule.</span></span>

<span data-ttu-id="19ae3-107">Cet article, qui complète la vidéo [Intégrer la gestion des API Azure avec Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) , explique comment consigner les événements Gestion des API à l’aide d’Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="19ae3-107">This article is a companion to the [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how to log API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="19ae3-108">Création d'un hub d'événements Azure</span><span class="sxs-lookup"><span data-stu-id="19ae3-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="19ae3-109">Pour créer un hub d’événements, connectez-vous au [portail Azure Classic](https://manage.windowsazure.com) et cliquez sur **Nouveau**->**App Services**->**Service Bu**->**Hub d’événements**->**Création rapide**.</span><span class="sxs-lookup"><span data-stu-id="19ae3-109">To create a new Event Hub, sign-in to the [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="19ae3-110">Entrez un nom d’Event Hub, une région, sélectionnez un abonnement et sélectionnez un espace de noms.</span><span class="sxs-lookup"><span data-stu-id="19ae3-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="19ae3-111">Si vous n’avez pas créé d’espace de noms précédemment, vous pouvez en créer un en entrant un nom dans la zone de texte **Espace de noms** .</span><span class="sxs-lookup"><span data-stu-id="19ae3-111">If you haven't previously created a namespace you can create one by typing a name in the **Namespace** textbox.</span></span> <span data-ttu-id="19ae3-112">Une fois que toutes les propriétés sont configurées, cliquez sur **Créer un hub d’événements** pour créer le hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="19ae3-112">Once all properties are configured, click **Create a new Event Hub** to create the Event Hub.</span></span>

![Créer un event hub][create-event-hub]

<span data-ttu-id="19ae3-114">Ensuite, accédez à l’onglet **Configurer** de votre nouveau hub d’événements et créez deux **stratégies d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="19ae3-114">Next, navigate to the **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="19ae3-115">Nommez la première stratégie **Envoi** et attribuez-lui des autorisations **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="19ae3-115">Name the first one **Sending** and give it **Send** permissions.</span></span>

![Stratégie Envoi][sending-policy]

<span data-ttu-id="19ae3-117">Nommez la seconde **Réception** et attribuez-lui des autorisations **Écouter**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="19ae3-117">Name the second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Stratégie Réception][receiving-policy]

<span data-ttu-id="19ae3-119">Chaque stratégie d’accès partagé permet aux applications d’envoyer et de recevoir des événements vers et depuis l’Event Hub.</span><span class="sxs-lookup"><span data-stu-id="19ae3-119">Each shared access policy allows applications to send and receive events to and from the Event Hub.</span></span> <span data-ttu-id="19ae3-120">Pour accéder aux chaînes de connexion pour ces stratégies, accédez à l’onglet **Tableau de bord** du hub d’événements et cliquez sur **Informations de connexion**.</span><span class="sxs-lookup"><span data-stu-id="19ae3-120">To access the connection strings for these policies, navigate to the **Dashboard** tab of the Event Hub and click **Connection information**.</span></span>

![Chaîne de connexion][event-hub-dashboard]

<span data-ttu-id="19ae3-122">La chaîne de connexion **Envoi** est utilisée lors de l’enregistrement des événements et la chaîne de connexion **Réception** lors du téléchargement des événements à partir du hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="19ae3-122">The **Sending** connection string is used when logging events, and the **Receiving** connection string is used when downloading events from the Event Hub.</span></span>

![Chaîne de connexion][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="19ae3-124">Créer un enregistreur d’événements de gestion des API</span><span class="sxs-lookup"><span data-stu-id="19ae3-124">Create an API Management logger</span></span>
<span data-ttu-id="19ae3-125">Maintenant que vous disposez d’un hub d’événements, l’étape suivante consiste à configurer un [enregistreur d’événements](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) dans votre service Gestion des API afin qu’il puisse enregistrer des événements dans le hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="19ae3-125">Now that you have an Event Hub, the next step is to configure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events to the Event Hub.</span></span>

<span data-ttu-id="19ae3-126">Les enregistreurs d’événements de gestion des API peuvent être configurés à l’aide de l’ [API REST Gestion des API](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="19ae3-126">API Management loggers are configured using the [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="19ae3-127">Avant d’utiliser l’API REST pour la première fois, passez en revue les [conditions préalables](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) et assurez-vous que vous avez [activé l’accès à l’API REST](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="19ae3-127">Before using the REST API for the first time, review the [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access to the REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="19ae3-128">Pour créer un enregistreur d’événements, créez une demande HTTP PUT à l’aide du modèle d’URL suivant.</span><span class="sxs-lookup"><span data-stu-id="19ae3-128">To create a logger, make an HTTP PUT request using the following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="19ae3-129">Remplacez `{your service}` par le nom de votre instance de service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="19ae3-129">Replace `{your service}` with the name of your API Management service instance.</span></span>
* <span data-ttu-id="19ae3-130">Remplacez `{new logger name}` par le nom souhaité pour votre nouvel enregistreur d’événements.</span><span class="sxs-lookup"><span data-stu-id="19ae3-130">Replace `{new logger name}` with the desired name for your new logger.</span></span> <span data-ttu-id="19ae3-131">Ce nom servira de référence lors de la configuration de la stratégie [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) .</span><span class="sxs-lookup"><span data-stu-id="19ae3-131">You will reference this name when you configure the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="19ae3-132">Ajoutez les en-têtes suivants à la demande.</span><span class="sxs-lookup"><span data-stu-id="19ae3-132">Add the following headers to the request.</span></span>

* <span data-ttu-id="19ae3-133">Type de contenu : application/json</span><span class="sxs-lookup"><span data-stu-id="19ae3-133">Content-Type : application/json</span></span>
* <span data-ttu-id="19ae3-134">Autorisation : SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="19ae3-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="19ae3-135">Pour obtenir des instructions sur la génération de `SharedAccessSignature` , consultez [Authentification de l’API REST Gestion des API Azure](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span><span class="sxs-lookup"><span data-stu-id="19ae3-135">For instructions on generating the `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="19ae3-136">Spécifiez le corps de la demande en utilisant le modèle suivant.</span><span class="sxs-lookup"><span data-stu-id="19ae3-136">Specify the request body using the following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of the Event Hub from the Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="19ae3-137">`type` doit être défini sur `AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="19ae3-137">`type` must be set to `AzureEventHub`.</span></span>
* <span data-ttu-id="19ae3-138">`description` fournit une description facultative de l’enregistreur d’événements et peut être une chaîne vide si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="19ae3-138">`description` provides an optional description of the logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="19ae3-139">`credentials` contient les valeurs `name` et `connectionString` de votre hub d’événements Azure.</span><span class="sxs-lookup"><span data-stu-id="19ae3-139">`credentials` contains the `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="19ae3-140">Lorsque vous créez la demande, si l’enregistreur d’événements est créé, un code d’état `201 Created` est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="19ae3-140">When you make the request, if the logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="19ae3-141">Pour connaître les autres codes de retour possibles et leurs raisons, consultez [Créer un enregistreur d’événements](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span><span class="sxs-lookup"><span data-stu-id="19ae3-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="19ae3-142">Pour voir comment effectuer d’autres opérations, notamment la création de listes, la mise à jour et la suppression, consultez la documentation de l’entité [Enregistreur d’événements](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) .</span><span class="sxs-lookup"><span data-stu-id="19ae3-142">To see how perform other operations such as list, update, and delete, see the [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="19ae3-143">Configurer des stratégies Enregistrer sur event hub</span><span class="sxs-lookup"><span data-stu-id="19ae3-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="19ae3-144">Une fois que votre journal est configuré dans Gestion des API, vous pouvez configurer vos stratégies Enregistrer sur event hubs pour enregistrer les événements de votre choix.</span><span class="sxs-lookup"><span data-stu-id="19ae3-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies to log the desired events.</span></span> <span data-ttu-id="19ae3-145">La stratégie Enregistrer sur event hubs peut être utilisée dans la section de la stratégie entrante ou dans la section de la stratégie sortante.</span><span class="sxs-lookup"><span data-stu-id="19ae3-145">The log-to-eventhubs policy can be used in either the inbound policy section or the outbound policy section.</span></span>

<span data-ttu-id="19ae3-146">Pour configurer des stratégies, connectez-vous au [portail Azure](https://portal.azure.com), accédez à votre service de gestion des API et cliquez sur **portail de publication** pour accéder au portail de publication.</span><span class="sxs-lookup"><span data-stu-id="19ae3-146">To configure policies, sign-in to the [Azure portal](https://portal.azure.com), navigate to your API Management service, and click **Publisher portal** to access the publisher portal.</span></span>

![Portail des éditeurs][publisher-portal]

<span data-ttu-id="19ae3-148">Cliquez sur **Stratégies** ans le menu Gestion des API situé à gauche, sélectionnez le produit et l’API de votre choix, puis cliquez sur **Ajouter une stratégie**.</span><span class="sxs-lookup"><span data-stu-id="19ae3-148">Click **Policies** in the API Management menu on the left, select the desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="19ae3-149">Dans cet exemple, nous ajoutons une stratégie à l’**API Echo** dans le produit **Illimité**.</span><span class="sxs-lookup"><span data-stu-id="19ae3-149">In this example we're adding a policy to the **Echo API** in the **Unlimited** product.</span></span>

![Add policy][add-policy]

<span data-ttu-id="19ae3-151">Placez votre curseur dans la section de la stratégie `inbound` et cliquez sur la stratégie **Log to EventHub`log-to-eventhub` pour insérer le modèle de déclaration de stratégie** .</span><span class="sxs-lookup"><span data-stu-id="19ae3-151">Position your cursor in the `inbound` policy section and click the **Log to EventHub** policy to insert the `log-to-eventhub` policy statement template.</span></span>

![Policy editor][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="19ae3-153">Remplacez `logger-id` par le nom de l’enregistreur d’événements Gestion des API que vous avez configuré à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="19ae3-153">Replace `logger-id` with the name of the API Management logger you configured in the previous step.</span></span>

<span data-ttu-id="19ae3-154">Vous pouvez utiliser toute expression qui renvoie une chaîne en tant que valeur pour l’élément `log-to-eventhub` .</span><span class="sxs-lookup"><span data-stu-id="19ae3-154">You can use any expression that returns a string as the value for the `log-to-eventhub` element.</span></span> <span data-ttu-id="19ae3-155">Dans cet exemple, une chaîne contenant la date et l’heure, le nom du service, l’ID de la demande, l’adresse IP de la demande et le nom de l’opération est enregistrée.</span><span class="sxs-lookup"><span data-stu-id="19ae3-155">In this example a string containing the date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="19ae3-156">Cliquez sur **Enregistrer** pour enregistrer la configuration de la stratégie mise à jour.</span><span class="sxs-lookup"><span data-stu-id="19ae3-156">Click **Save** to save the updated policy configuration.</span></span> <span data-ttu-id="19ae3-157">Dès qu’elle est enregistrée, la stratégie est active et les événements sont enregistrés dans l’Event Hub désigné.</span><span class="sxs-lookup"><span data-stu-id="19ae3-157">As soon as it is saved the policy is active and events are logged to the designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19ae3-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="19ae3-158">Next steps</span></span>
* <span data-ttu-id="19ae3-159">En savoir plus sur Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="19ae3-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="19ae3-160">Prise en main avec Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="19ae3-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="19ae3-161">Réception de messages avec EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="19ae3-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="19ae3-162">Guide de programmation Event Hubs</span><span class="sxs-lookup"><span data-stu-id="19ae3-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="19ae3-163">En savoir plus sur l’intégration de Gestion des API et Event Hubs</span><span class="sxs-lookup"><span data-stu-id="19ae3-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="19ae3-164">Référence d’entité d’enregistreur</span><span class="sxs-lookup"><span data-stu-id="19ae3-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="19ae3-165">Référence de stratégie log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="19ae3-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="19ae3-166">Surveiller vos API avec gestion des API Azure, les hubs d’événements et Runscope</span><span class="sxs-lookup"><span data-stu-id="19ae3-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="19ae3-167">Regarder une procédure pas à pas en vidéo</span><span class="sxs-lookup"><span data-stu-id="19ae3-167">Watch a video walkthrough</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Integrate-Azure-API-Management-with-Event-Hubs/player]
>
>

[publisher-portal]: ./media/api-management-howto-log-event-hubs/publisher-portal.png
[create-event-hub]: ./media/api-management-howto-log-event-hubs/create-event-hub.png
[event-hub-connection-string]: ./media/api-management-howto-log-event-hubs/event-hub-connection-string.png
[event-hub-dashboard]: ./media/api-management-howto-log-event-hubs/event-hub-dashboard.png
[receiving-policy]: ./media/api-management-howto-log-event-hubs/receiving-policy.png
[sending-policy]: ./media/api-management-howto-log-event-hubs/sending-policy.png
[event-hub-policy]: ./media/api-management-howto-log-event-hubs/event-hub-policy.png
[add-policy]: ./media/api-management-howto-log-event-hubs/add-policy.png
