---
title: "aaaHow toolog événements tooAzure Hubs d’événements dans la gestion des API Azure | Documents Microsoft"
description: "Découvrez comment toolog événements tooAzure Hubs d’événements dans la gestion des API Azure."
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
ms.openlocfilehash: 09ca65fc48a874467c6662858f7594e9b19fcdb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a><span data-ttu-id="0eec1-103">Comment toolog événements tooAzure Hubs d’événements dans la gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="0eec1-103">How toolog events tooAzure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="0eec1-104">Azure Event Hubs est un service d’entrée de données hautement évolutive qui peut traiter des millions d’événements par seconde afin que vous puissiez traiter et analyser hello des quantités massives de données généré par vos périphériques connectés et les applications.</span><span class="sxs-lookup"><span data-stu-id="0eec1-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="0eec1-105">Concentrateurs d’événements joue le rôle hello « porte d’entrée » pour un pipeline d’événements, et une fois que les données sont collectées dans un concentrateur d’événements, il peut être transformé et stockées à l’aide de n’importe quel fournisseur analytique en temps réel ou des cartes de traitement par lot/stockage.</span><span class="sxs-lookup"><span data-stu-id="0eec1-105">Event Hubs acts as hello "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="0eec1-106">Concentrateurs d’événements dissocie production hello d’un flux d’événements à partir de la consommation de ces événements, hello afin que les consommateurs d’événements peuvent accéder à des événements de hello sur leur propre calendrier.</span><span class="sxs-lookup"><span data-stu-id="0eec1-106">Event Hubs decouples hello production of a stream of events from hello consumption of those events, so that event consumers can access hello events on their own schedule.</span></span>

<span data-ttu-id="0eec1-107">Cet article est un toohello d’accompagnement [intégrer Gestion des API Azure avec des concentrateurs d’événements](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) vidéo et décrit comment les événements de gestion des API toolog à l’aide d’Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="0eec1-107">This article is a companion toohello [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how toolog API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="0eec1-108">Création d'un hub d'événements Azure</span><span class="sxs-lookup"><span data-stu-id="0eec1-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="0eec1-109">toocreate un concentrateur d’événements, connectez-vous toohello [portail Azure classic](https://manage.windowsazure.com) et cliquez sur **nouveau**->**des Services d’application**->**Service Bus**  -> **Concentrateur d’événements**->**création rapide**.</span><span class="sxs-lookup"><span data-stu-id="0eec1-109">toocreate a new Event Hub, sign-in toohello [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="0eec1-110">Entrez un nom d’Event Hub, une région, sélectionnez un abonnement et sélectionnez un espace de noms.</span><span class="sxs-lookup"><span data-stu-id="0eec1-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="0eec1-111">Si vous n’avez pas déjà créé un espace de noms, vous pouvez créer un en tapant un nom Bonjour **Namespace** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="0eec1-111">If you haven't previously created a namespace you can create one by typing a name in hello **Namespace** textbox.</span></span> <span data-ttu-id="0eec1-112">Une fois que toutes les propriétés sont configurées, cliquez sur **créer un concentrateur d’événements** toocreate hello concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="0eec1-112">Once all properties are configured, click **Create a new Event Hub** toocreate hello Event Hub.</span></span>

![Créer un event hub][create-event-hub]

<span data-ttu-id="0eec1-114">Ensuite, accédez toohello **configurer** onglet pour votre nouveau concentrateur d’événements et de créer deux **stratégies d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="0eec1-114">Next, navigate toohello **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="0eec1-115">Nom hello premier **envoi** et lui donner **envoyer** autorisations.</span><span class="sxs-lookup"><span data-stu-id="0eec1-115">Name hello first one **Sending** and give it **Send** permissions.</span></span>

![Stratégie Envoi][sending-policy]

<span data-ttu-id="0eec1-117">Nom hello deuxième **réception**, attribuez-lui **écouter** autorisations, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="0eec1-117">Name hello second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Stratégie Réception][receiving-policy]

<span data-ttu-id="0eec1-119">Chaque stratégie d’accès partagé autorise les applications toosend et recevoir des événements tooand hello concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="0eec1-119">Each shared access policy allows applications toosend and receive events tooand from hello Event Hub.</span></span> <span data-ttu-id="0eec1-120">chaînes de connexion tooaccess hello pour ces stratégies, accédez à toohello **tableau de bord** onglet de hello concentrateur d’événements et cliquez sur **les informations de connexion**.</span><span class="sxs-lookup"><span data-stu-id="0eec1-120">tooaccess hello connection strings for these policies, navigate toohello **Dashboard** tab of hello Event Hub and click **Connection information**.</span></span>

![Chaîne de connexion][event-hub-dashboard]

<span data-ttu-id="0eec1-122">Hello **envoi** chaîne de connexion est utilisée lors de la journalisation des événements et hello **réception** chaîne de connexion est utilisée lors du téléchargement des événements à partir de hello concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="0eec1-122">hello **Sending** connection string is used when logging events, and hello **Receiving** connection string is used when downloading events from hello Event Hub.</span></span>

![Chaîne de connexion][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="0eec1-124">Créer un enregistreur d’événements de gestion des API</span><span class="sxs-lookup"><span data-stu-id="0eec1-124">Create an API Management logger</span></span>
<span data-ttu-id="0eec1-125">Maintenant que vous avez un concentrateur d’événements, étape suivante de hello est tooconfigure un [enregistreur d’événements](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) dans votre gestion des API de service afin qu’il puisse consigner les événements toohello concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="0eec1-125">Now that you have an Event Hub, hello next step is tooconfigure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events toohello Event Hub.</span></span>

<span data-ttu-id="0eec1-126">Les journaux de gestion des API sont configurés à l’aide de hello [API REST de gestion des API](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="0eec1-126">API Management loggers are configured using hello [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="0eec1-127">Avant d’utiliser hello API REST pour hello première fois, passez en revue de hello [conditions préalables](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) et assurez-vous d’avoir [activé toohello d’accès aux API REST](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="0eec1-127">Before using hello REST API for hello first time, review hello [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access toohello REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="0eec1-128">toocreate un enregistreur d’événements, vérifiez une demande HTTP PUT à l’aide de hello suivant le modèle d’URL.</span><span class="sxs-lookup"><span data-stu-id="0eec1-128">toocreate a logger, make an HTTP PUT request using hello following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="0eec1-129">Remplacez `{your service}` par nom hello de votre instance de service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="0eec1-129">Replace `{your service}` with hello name of your API Management service instance.</span></span>
* <span data-ttu-id="0eec1-130">Remplacez `{new logger name}` avec le nom souhaité pour votre nouvel enregistreur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="0eec1-130">Replace `{new logger name}` with hello desired name for your new logger.</span></span> <span data-ttu-id="0eec1-131">Vous ferez référence ce nom lorsque vous configurez hello [journal à eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) stratégie</span><span class="sxs-lookup"><span data-stu-id="0eec1-131">You will reference this name when you configure hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="0eec1-132">Ajoutez hello en-têtes toohello demande.</span><span class="sxs-lookup"><span data-stu-id="0eec1-132">Add hello following headers toohello request.</span></span>

* <span data-ttu-id="0eec1-133">Type de contenu : application/json</span><span class="sxs-lookup"><span data-stu-id="0eec1-133">Content-Type : application/json</span></span>
* <span data-ttu-id="0eec1-134">Autorisation : SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="0eec1-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="0eec1-135">Pour obtenir des instructions sur la génération hello `SharedAccessSignature` consultez [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span><span class="sxs-lookup"><span data-stu-id="0eec1-135">For instructions on generating hello `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="0eec1-136">Spécifiez le corps de la demande hello à l’aide de hello suivant le modèle.</span><span class="sxs-lookup"><span data-stu-id="0eec1-136">Specify hello request body using hello following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of hello Event Hub from hello Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="0eec1-137">`type`doit être défini trop`AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="0eec1-137">`type` must be set too`AzureEventHub`.</span></span>
* <span data-ttu-id="0eec1-138">`description`Fournit une description facultative de l’enregistreur d’événements hello et peut être une chaîne de longueur nulle si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="0eec1-138">`description` provides an optional description of hello logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="0eec1-139">`credentials`contient hello `name` et `connectionString` de votre concentrateur d’événements Azure.</span><span class="sxs-lookup"><span data-stu-id="0eec1-139">`credentials` contains hello `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="0eec1-140">Lorsque vous effectuez la demande de hello, si l’enregistreur d’événements hello est créé un code d’état de `201 Created` est retourné.</span><span class="sxs-lookup"><span data-stu-id="0eec1-140">When you make hello request, if hello logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="0eec1-141">Pour connaître les autres codes de retour possibles et leurs raisons, consultez [Créer un enregistreur d’événements](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span><span class="sxs-lookup"><span data-stu-id="0eec1-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="0eec1-142">toosee comment effectuer d’autres opérations telles que la liste, update et delete, consultez hello [journal](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) documentation de l’entité.</span><span class="sxs-lookup"><span data-stu-id="0eec1-142">toosee how perform other operations such as list, update, and delete, see hello [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="0eec1-143">Configurer des stratégies Enregistrer sur event hub</span><span class="sxs-lookup"><span data-stu-id="0eec1-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="0eec1-144">Une fois votre enregistreur d’événements est configuré dans la gestion des API, vous pouvez configurer vos événements de hello souhaité de stratégies de journal à eventhubs toolog.</span><span class="sxs-lookup"><span data-stu-id="0eec1-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies toolog hello desired events.</span></span> <span data-ttu-id="0eec1-145">Hello journal à eventhubs stratégie peut être utilisée dans deux hello stratégie entrante ou section hello stratégie sortante.</span><span class="sxs-lookup"><span data-stu-id="0eec1-145">hello log-to-eventhubs policy can be used in either hello inbound policy section or hello outbound policy section.</span></span>

<span data-ttu-id="0eec1-146">stratégies tooconfigure, connectez-vous toohello [portail Azure](https://portal.azure.com), parcourir le service de gestion des API tooyour et cliquez sur **portail de publication** tooaccess hello portail de publication.</span><span class="sxs-lookup"><span data-stu-id="0eec1-146">tooconfigure policies, sign-in toohello [Azure portal](https://portal.azure.com), navigate tooyour API Management service, and click **Publisher portal** tooaccess hello publisher portal.</span></span>

![Portail des éditeurs][publisher-portal]

<span data-ttu-id="0eec1-148">Cliquez sur **stratégies** dans le menu Gestion des API hello hello gauche, sélectionnez le produit de votre choix hello et API, puis cliquez sur **ajouter une stratégie**.</span><span class="sxs-lookup"><span data-stu-id="0eec1-148">Click **Policies** in hello API Management menu on hello left, select hello desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="0eec1-149">Dans cet exemple, nous ajoutons une stratégie toohello **Echo API** Bonjour **illimité** produit.</span><span class="sxs-lookup"><span data-stu-id="0eec1-149">In this example we're adding a policy toohello **Echo API** in hello **Unlimited** product.</span></span>

![Add policy][add-policy]

<span data-ttu-id="0eec1-151">Placez votre curseur dans hello `inbound` stratégie et cliquez sur hello **journal tooEventHub** hello tooinsert de stratégie `log-to-eventhub` modèle d’instruction de stratégie.</span><span class="sxs-lookup"><span data-stu-id="0eec1-151">Position your cursor in hello `inbound` policy section and click hello **Log tooEventHub** policy tooinsert hello `log-to-eventhub` policy statement template.</span></span>

![Policy editor][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="0eec1-153">Remplacez `logger-id` par nom hello d’enregistreur d’événements de la gestion des API hello configurées à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="0eec1-153">Replace `logger-id` with hello name of hello API Management logger you configured in hello previous step.</span></span>

<span data-ttu-id="0eec1-154">Vous pouvez utiliser n’importe quelle expression qui retourne une chaîne en tant que valeur hello pour hello `log-to-eventhub` élément.</span><span class="sxs-lookup"><span data-stu-id="0eec1-154">You can use any expression that returns a string as hello value for hello `log-to-eventhub` element.</span></span> <span data-ttu-id="0eec1-155">Dans cet exemple, une chaîne contenant la date de hello et heure, nom du service, id de demande, demander l’adresse ip et nom de l’opération est enregistrée.</span><span class="sxs-lookup"><span data-stu-id="0eec1-155">In this example a string containing hello date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="0eec1-156">Cliquez sur **enregistrer** toosave hello mis à jour la configuration de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="0eec1-156">Click **Save** toosave hello updated policy configuration.</span></span> <span data-ttu-id="0eec1-157">Dès qu’elle est enregistrée hello stratégie est active et les événements sont enregistré toohello désigné du concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="0eec1-157">As soon as it is saved hello policy is active and events are logged toohello designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0eec1-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0eec1-158">Next steps</span></span>
* <span data-ttu-id="0eec1-159">En savoir plus sur Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0eec1-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="0eec1-160">Prise en main avec Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0eec1-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="0eec1-161">Réception de messages avec EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="0eec1-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="0eec1-162">Guide de programmation Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0eec1-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="0eec1-163">En savoir plus sur l’intégration de Gestion des API et Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0eec1-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="0eec1-164">Référence d’entité d’enregistreur</span><span class="sxs-lookup"><span data-stu-id="0eec1-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="0eec1-165">Référence de stratégie log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="0eec1-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="0eec1-166">Surveiller vos API avec gestion des API Azure, les hubs d’événements et Runscope</span><span class="sxs-lookup"><span data-stu-id="0eec1-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="0eec1-167">Regarder une procédure pas à pas en vidéo</span><span class="sxs-lookup"><span data-stu-id="0eec1-167">Watch a video walkthrough</span></span>
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
