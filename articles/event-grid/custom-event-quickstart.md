---
title: "Événements personnalisés pour Azure Event Grid | Microsoft Docs"
description: "Utilisez Azure Event Grid pour publier une rubrique et pour vous abonner à cet événement."
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 0290836bebadb20085a3ce84dddc088c3af385da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a><span data-ttu-id="b019b-103">Créer et acheminer des événements personnalisés avec Azure Event Grid</span><span class="sxs-lookup"><span data-stu-id="b019b-103">Create and route custom events with Azure Event Grid</span></span>

<span data-ttu-id="b019b-104">Azure Event Grid est un service de gestion d’événements pour le cloud.</span><span class="sxs-lookup"><span data-stu-id="b019b-104">Azure Event Grid is an eventing service for the cloud.</span></span> <span data-ttu-id="b019b-105">Dans cet article, vous utilisez Azure CLI pour créer une rubrique personnalisée, vous abonner à cette rubrique et déclencher l’événement pour afficher le résultat.</span><span class="sxs-lookup"><span data-stu-id="b019b-105">In this article, you use the Azure CLI to create a custom topic, subscribe to the topic, and trigger the event to view the result.</span></span> <span data-ttu-id="b019b-106">En règle générale, vous envoyez des événements à un point de terminaison qui répond à l’événement, comme un webhook ou une fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="b019b-106">Typically, you send events to an endpoint that responds to the event, such as, a webhook or Azure Function.</span></span> <span data-ttu-id="b019b-107">Toutefois, pour simplifier cet article, vous envoyez les événements à une URL qui collecte seulement les messages.</span><span class="sxs-lookup"><span data-stu-id="b019b-107">However, to simplify this article, you send the events to a URL that merely collects the messages.</span></span> <span data-ttu-id="b019b-108">Vous créez cette URL à l’aide d’un outil tiers en open-source nommé [RequestBin](https://requestb.in/).</span><span class="sxs-lookup"><span data-stu-id="b019b-108">You create this URL by using an open source, third-party tool called [RequestBin](https://requestb.in/).</span></span>

>[!NOTE]
><span data-ttu-id="b019b-109">**RequestBin** est un outil open source qui n’est pas destiné à une utilisation à haut débit.</span><span class="sxs-lookup"><span data-stu-id="b019b-109">**RequestBin** is an open source tool that is not intended for high throughput usage.</span></span> <span data-ttu-id="b019b-110">L’utilisation de l’outil ici est uniquement à but démonstratif.</span><span class="sxs-lookup"><span data-stu-id="b019b-110">The use of the tool here is purely demonstrative.</span></span> <span data-ttu-id="b019b-111">Si vous envoyez plusieurs événements par push en simultané, vous pouvez ne pas voir tous les événements dans l’outil.</span><span class="sxs-lookup"><span data-stu-id="b019b-111">If you push more than one event at a time, you might not see all of your events in the tool.</span></span>

<span data-ttu-id="b019b-112">Une fois terminé, vous voyez que les données d’événement ont été envoyées à un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="b019b-112">When you are finished, you see that the event data has been sent to an endpoint.</span></span>

![Données d’événement](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b019b-114">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, cet article nécessite l’exécution de la version la plus récente d’Azure CLI (2.0.14 ou une version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="b019b-114">If you choose to install and use the CLI locally, this article requires that you are running the latest version of Azure CLI (2.0.14 or later).</span></span> <span data-ttu-id="b019b-115">Pour connaître la version de l’interface, exécutez `az --version`.</span><span class="sxs-lookup"><span data-stu-id="b019b-115">To find the version, run `az --version`.</span></span> <span data-ttu-id="b019b-116">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b019b-116">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="b019b-117">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="b019b-117">Create a resource group</span></span>

<span data-ttu-id="b019b-118">Les rubriques Event Grid sont des ressources Azure et doivent être placées dans un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b019b-118">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="b019b-119">Un groupe de ressources est une collection logique dans laquelle des ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="b019b-119">The resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="b019b-120">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b019b-120">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="b019b-121">L’exemple suivant crée un groupe de ressources nommé *gridResourceGroup* à l’emplacement *westus2*.</span><span class="sxs-lookup"><span data-stu-id="b019b-121">The following example creates a resource group named *gridResourceGroup* in the *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="b019b-122">Créer une rubrique personnalisée</span><span class="sxs-lookup"><span data-stu-id="b019b-122">Create a custom topic</span></span>

<span data-ttu-id="b019b-123">Une rubrique fournit un point de terminaison défini par l’utilisateur vers lequel vous envoyez vos événements.</span><span class="sxs-lookup"><span data-stu-id="b019b-123">A topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="b019b-124">L’exemple suivant permet de créer la rubrique dans votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b019b-124">The following example creates the topic in your resource group.</span></span> <span data-ttu-id="b019b-125">Remplacez `<topic_name>` par un nom unique pour votre rubrique.</span><span class="sxs-lookup"><span data-stu-id="b019b-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="b019b-126">Le nom de la rubrique doit être unique, car elle est représentée par une entrée DNS.</span><span class="sxs-lookup"><span data-stu-id="b019b-126">The topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="b019b-127">Dans sa version préliminaire, Event Grid prend en charge les emplacements **westus2** et **westcentralus**.</span><span class="sxs-lookup"><span data-stu-id="b019b-127">For the preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span>

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="b019b-128">Créer un point de terminaison de message</span><span class="sxs-lookup"><span data-stu-id="b019b-128">Create a message endpoint</span></span>

<span data-ttu-id="b019b-129">Avant de nous abonner à la rubrique, nous allons créer le point de terminaison pour le message de l’événement.</span><span class="sxs-lookup"><span data-stu-id="b019b-129">Before subscribing to the topic, let's create the endpoint for the event message.</span></span> <span data-ttu-id="b019b-130">Au lieu d’écrire du code qui réponde à l’événement, nous allons créer un point de terminaison qui collecte les messages, afin que vous puissiez les consulter.</span><span class="sxs-lookup"><span data-stu-id="b019b-130">Rather than write code to respond to the event, let's create an endpoint that collects the messages so you can view them.</span></span> <span data-ttu-id="b019b-131">RequestBin est un outil tiers en open-source qui vous permet de créer un point de terminaison et d’afficher les requêtes qui lui sont envoyées.</span><span class="sxs-lookup"><span data-stu-id="b019b-131">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="b019b-132">Accédez à [RequestBin](https://requestb.in/), puis cliquez sur **Créer un RequestBin**.</span><span class="sxs-lookup"><span data-stu-id="b019b-132">Go to [RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span>  <span data-ttu-id="b019b-133">Copiez l’URL du fichier bin, dont vous avez besoin pour vous abonner à la rubrique.</span><span class="sxs-lookup"><span data-stu-id="b019b-133">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

## <a name="subscribe-to-a-topic"></a><span data-ttu-id="b019b-134">S’abonner à une rubrique</span><span class="sxs-lookup"><span data-stu-id="b019b-134">Subscribe to a topic</span></span>

<span data-ttu-id="b019b-135">Vous vous abonnez à une rubrique pour communiquer à Event Grid les événements qui vous intéressent. L’exemple suivant s’abonne à la rubrique que vous avez créée et transmet l’URL à partir de RequestBin en tant que point de terminaison de la notification d’événement.</span><span class="sxs-lookup"><span data-stu-id="b019b-135">You subscribe to a topic to tell Event Grid which events you want to track. The following example subscribes to the topic you created, and passes the URL from RequestBin as the endpoint for event notification.</span></span> <span data-ttu-id="b019b-136">Remplacez `<event_subscription_name>` par un nom unique pour votre abonnement, et `<URL_from_RequestBin>` par la valeur de la section précédente.</span><span class="sxs-lookup"><span data-stu-id="b019b-136">Replace `<event_subscription_name>` with a unique name for your subscription, and `<URL_from_RequestBin>` with the value from the preceding section.</span></span> <span data-ttu-id="b019b-137">En spécifiant un point de terminaison lors de l’abonnement, Event Grid gère le routage d’événements vers ce point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="b019b-137">By specifying an endpoint when subscribing, Event Grid handles the routing of events to that endpoint.</span></span> <span data-ttu-id="b019b-138">Pour `<topic_name>`, utilisez la valeur que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="b019b-138">For `<topic_name>`, use the value you created earlier.</span></span> 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-to-your-topic"></a><span data-ttu-id="b019b-139">Envoyer un événement à votre rubrique</span><span class="sxs-lookup"><span data-stu-id="b019b-139">Send an event to your topic</span></span>

<span data-ttu-id="b019b-140">Nous allons maintenant déclencher un événement pour voir comment Event Grid distribue le message à votre point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="b019b-140">Now, let's trigger an event to see how Event Grid distributes the message to your endpoint.</span></span> <span data-ttu-id="b019b-141">Tout d’abord, il nous faut l’URL et la clé de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="b019b-141">First, let's get the URL and key for the topic.</span></span> <span data-ttu-id="b019b-142">Utilisez de nouveau le nom de votre rubrique pour `<topic_name>`.</span><span class="sxs-lookup"><span data-stu-id="b019b-142">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="b019b-143">Pour simplifier cet article, nous avons configuré des exemples de données d’événements à envoyer à la rubrique.</span><span class="sxs-lookup"><span data-stu-id="b019b-143">To simplify this article, we have set up sample event data to send to the topic.</span></span> <span data-ttu-id="b019b-144">En règle générale, une application ou un service Azure envoie les données d’événements.</span><span class="sxs-lookup"><span data-stu-id="b019b-144">Typically, an application or Azure service would send the event data.</span></span> <span data-ttu-id="b019b-145">L’exemple suivant obtient les données d’événements :</span><span class="sxs-lookup"><span data-stu-id="b019b-145">The following example gets the event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="b019b-146">Si vous affichez `echo "$body"`, vous pouvez voir l’événement complet.</span><span class="sxs-lookup"><span data-stu-id="b019b-146">If you `echo "$body"` you can see the full event.</span></span> <span data-ttu-id="b019b-147">L’élément `data` du fichier JSON est la charge utile de l’événement.</span><span class="sxs-lookup"><span data-stu-id="b019b-147">The `data` element of the JSON is the payload of your event.</span></span> <span data-ttu-id="b019b-148">N’importe quel fichier JSON bien construit peut être placé dans ce champ.</span><span class="sxs-lookup"><span data-stu-id="b019b-148">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="b019b-149">Vous pouvez aussi utiliser le champ objet pour un routage et un filtrage avancés.</span><span class="sxs-lookup"><span data-stu-id="b019b-149">You can also use the subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="b019b-150">CURL est un utilitaire qui effectue des requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="b019b-150">CURL is a utility that performs HTTP requests.</span></span> <span data-ttu-id="b019b-151">Dans cet article, nous utilisons CURL pour envoyer l’événement à notre rubrique.</span><span class="sxs-lookup"><span data-stu-id="b019b-151">In this article, we use CURL to send the event to our topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="b019b-152">Vous avez déclenché l’événement, et Event Grid a envoyé le message au point de terminaison configuré lors de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="b019b-152">You have triggered the event, and Event Grid sent the message to the endpoint you configured when subscribing.</span></span> <span data-ttu-id="b019b-153">Accédez à l’URL de RequestBin que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="b019b-153">Browse to the RequestBin URL that you created earlier.</span></span> <span data-ttu-id="b019b-154">Ou cliquez sur Actualiser dans le navigateur RequestBin ouvert.</span><span class="sxs-lookup"><span data-stu-id="b019b-154">Or, click refresh in your open RequestBin browser.</span></span> <span data-ttu-id="b019b-155">L’événement que vous venez d’envoyer apparaît.</span><span class="sxs-lookup"><span data-stu-id="b019b-155">You see the event you just sent.</span></span> 

```json
[{
  "id": "1807",
  "eventType": "recordInserted",
  "subject": "myapp/vehicles/motorcycles",
  "eventTime": "2017-08-10T21:03:07+00:00",
  "data": {
    "make": "Ducati",
    "model": "Monster"
  },
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/topics/{topic}"
}]
```

## <a name="clean-up-resources"></a><span data-ttu-id="b019b-156">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="b019b-156">Clean up resources</span></span>
<span data-ttu-id="b019b-157">Si vous envisagez de continuer à utiliser cet événement, ne supprimez pas les ressources créées dans cet article.</span><span class="sxs-lookup"><span data-stu-id="b019b-157">If you plan to continue working with this event, do not clean up the resources created in this article.</span></span> <span data-ttu-id="b019b-158">Sinon, utilisez la commande suivante pour supprimer les ressources créées avec cet article.</span><span class="sxs-lookup"><span data-stu-id="b019b-158">If you do not plan to continue, use the following command to delete the resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="b019b-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b019b-159">Next steps</span></span>

<span data-ttu-id="b019b-160">Maintenant que vous savez créer des rubriques et des abonnements d’événements, vous pouvez en apprendre davantage sur Event Grid et ce qu’il peut vous offrir :</span><span class="sxs-lookup"><span data-stu-id="b019b-160">Now that you know how to create topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="b019b-161">Event Grid</span><span class="sxs-lookup"><span data-stu-id="b019b-161">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="b019b-162">Surveiller les modifications d’une machine virtuelle avec Azure Event Grid et Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="b019b-162">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
