---
title: "événements d’aaaCustom pour la grille d’événement Azure | Documents Microsoft"
description: "Utilisez la grille d’événement Azure toopublish une rubrique et inscription de l’événement de toothat."
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 5055df1c970b043cadf06978a076f7f5c83501cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a><span data-ttu-id="f8914-103">Créer et acheminer des événements personnalisés avec Azure Event Grid</span><span class="sxs-lookup"><span data-stu-id="f8914-103">Create and route custom events with Azure Event Grid</span></span>

<span data-ttu-id="f8914-104">Grille d’événement Azure est un service de gestion des événements pour le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="f8914-104">Azure Event Grid is an eventing service for hello cloud.</span></span> <span data-ttu-id="f8914-105">Dans cet article, vous utilisez hello CLI d’Azure toocreate une rubrique personnalisée s’abonner toohello rubrique et déclencher hello événement tooview hello de résultats.</span><span class="sxs-lookup"><span data-stu-id="f8914-105">In this article, you use hello Azure CLI toocreate a custom topic, subscribe toohello topic, and trigger hello event tooview hello result.</span></span> <span data-ttu-id="f8914-106">En règle générale, vous envoyer des événements tooan point de terminaison qui répond événement toohello, par exemple, un webhook ou d’une fonction d’Azure.</span><span class="sxs-lookup"><span data-stu-id="f8914-106">Typically, you send events tooan endpoint that responds toohello event, such as, a webhook or Azure Function.</span></span> <span data-ttu-id="f8914-107">Toutefois, toosimplify cet article, vous envoyez hello événements tooa URL qui collecte simplement des messages de type hello.</span><span class="sxs-lookup"><span data-stu-id="f8914-107">However, toosimplify this article, you send hello events tooa URL that merely collects hello messages.</span></span> <span data-ttu-id="f8914-108">Vous créez cette URL à l’aide d’un outil tiers en open-source nommé [RequestBin](https://requestb.in/).</span><span class="sxs-lookup"><span data-stu-id="f8914-108">You create this URL by using an open source, third-party tool called [RequestBin](https://requestb.in/).</span></span>

>[!NOTE]
><span data-ttu-id="f8914-109">**RequestBin** est un outil open source qui n’est pas destiné à une utilisation à haut débit.</span><span class="sxs-lookup"><span data-stu-id="f8914-109">**RequestBin** is an open source tool that is not intended for high throughput usage.</span></span> <span data-ttu-id="f8914-110">Hello outil hello ici est purement le tarif.</span><span class="sxs-lookup"><span data-stu-id="f8914-110">hello use of hello tool here is purely demonstrative.</span></span> <span data-ttu-id="f8914-111">Si vous effectuez un push plusieurs événements à la fois, vous verrez ne peut-être pas tous les événements dans l’outil de hello.</span><span class="sxs-lookup"><span data-stu-id="f8914-111">If you push more than one event at a time, you might not see all of your events in hello tool.</span></span>

<span data-ttu-id="f8914-112">Lorsque vous avez terminé, vous voyez que les données d’événement hello a été envoyées tooan le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="f8914-112">When you are finished, you see that hello event data has been sent tooan endpoint.</span></span>

![Données d’événement](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f8914-114">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cet article suppose que vous exécutez la version la plus récente de Azure CLI hello (2.0.14 ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="f8914-114">If you choose tooinstall and use hello CLI locally, this article requires that you are running hello latest version of Azure CLI (2.0.14 or later).</span></span> <span data-ttu-id="f8914-115">version de hello toofind, exécutez `az --version`.</span><span class="sxs-lookup"><span data-stu-id="f8914-115">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="f8914-116">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f8914-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="f8914-117">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="f8914-117">Create a resource group</span></span>

<span data-ttu-id="f8914-118">Les rubriques Event Grid sont des ressources Azure et doivent être placées dans un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="f8914-118">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="f8914-119">groupe de ressources Hello est une collection logique dans le Azure les ressources sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="f8914-119">hello resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="f8914-120">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="f8914-120">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="f8914-121">Hello exemple suivant crée un groupe de ressources nommé *gridResourceGroup* Bonjour *westus2* emplacement.</span><span class="sxs-lookup"><span data-stu-id="f8914-121">hello following example creates a resource group named *gridResourceGroup* in hello *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="f8914-122">Créer une rubrique personnalisée</span><span class="sxs-lookup"><span data-stu-id="f8914-122">Create a custom topic</span></span>

<span data-ttu-id="f8914-123">Une rubrique fournit un point de terminaison défini par l’utilisateur vers lequel vous envoyez vos événements.</span><span class="sxs-lookup"><span data-stu-id="f8914-123">A topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="f8914-124">Hello exemple suivant crée les rubrique hello dans votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f8914-124">hello following example creates hello topic in your resource group.</span></span> <span data-ttu-id="f8914-125">Remplacez `<topic_name>` par un nom unique pour votre rubrique.</span><span class="sxs-lookup"><span data-stu-id="f8914-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="f8914-126">nom de la rubrique Hello doit être unique, car il est représenté par une entrée DNS.</span><span class="sxs-lookup"><span data-stu-id="f8914-126">hello topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="f8914-127">Pour la version préliminaire de hello, prend en charge la grille d’événement **westus2** et **westcentralus** emplacements.</span><span class="sxs-lookup"><span data-stu-id="f8914-127">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span>

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="f8914-128">Créer un point de terminaison de message</span><span class="sxs-lookup"><span data-stu-id="f8914-128">Create a message endpoint</span></span>

<span data-ttu-id="f8914-129">Avant de s’abonner toohello rubrique, nous allons créer le point de terminaison hello pour le message d’événement hello.</span><span class="sxs-lookup"><span data-stu-id="f8914-129">Before subscribing toohello topic, let's create hello endpoint for hello event message.</span></span> <span data-ttu-id="f8914-130">Plutôt que d’écrire un événement de code toorespond toohello, nous allons créer un point de terminaison qui collecte les messages de type hello afin que vous puissiez les afficher.</span><span class="sxs-lookup"><span data-stu-id="f8914-130">Rather than write code toorespond toohello event, let's create an endpoint that collects hello messages so you can view them.</span></span> <span data-ttu-id="f8914-131">RequestBin est une open source, un outil tiers qui vous permet de toocreate un point de terminaison et afficher les demandes qui sont envoyées à tooit.</span><span class="sxs-lookup"><span data-stu-id="f8914-131">RequestBin is an open source, third-party tool that enables you toocreate an endpoint, and view requests that are sent tooit.</span></span> <span data-ttu-id="f8914-132">Accédez trop[RequestBin](https://requestb.in/), puis cliquez sur **créer un RequestBin**.</span><span class="sxs-lookup"><span data-stu-id="f8914-132">Go too[RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span>  <span data-ttu-id="f8914-133">Copier l’URL d’emplacement de hello, car vous en avez besoin lors de l’abonnement toohello rubrique.</span><span class="sxs-lookup"><span data-stu-id="f8914-133">Copy hello bin URL, because you need it when subscribing toohello topic.</span></span>

## <a name="subscribe-tooa-topic"></a><span data-ttu-id="f8914-134">S’abonner tooa rubrique</span><span class="sxs-lookup"><span data-stu-id="f8914-134">Subscribe tooa topic</span></span>

<span data-ttu-id="f8914-135">Vous vous abonnez tooa rubrique tootell grille d’événement quels événements vous souhaitez tootrack.</span><span class="sxs-lookup"><span data-stu-id="f8914-135">You subscribe tooa topic tootell Event Grid which events you want tootrack.</span></span> <span data-ttu-id="f8914-136">Hello exemple suivant s’abonne toohello rubrique que vous avez créé et transmet les URL de hello de RequestBin en tant que point de terminaison hello pour la notification d’événement.</span><span class="sxs-lookup"><span data-stu-id="f8914-136">hello following example subscribes toohello topic you created, and passes hello URL from RequestBin as hello endpoint for event notification.</span></span> <span data-ttu-id="f8914-137">Remplacez `<event_subscription_name>` avec un nom unique pour votre abonnement, et `<URL_from_RequestBin>` avec la valeur hello à partir de la précédente section de hello.</span><span class="sxs-lookup"><span data-stu-id="f8914-137">Replace `<event_subscription_name>` with a unique name for your subscription, and `<URL_from_RequestBin>` with hello value from hello preceding section.</span></span> <span data-ttu-id="f8914-138">En spécifiant un point de terminaison lors de l’abonnement, grille d’événement gère le routage de point de terminaison toothat événements hello.</span><span class="sxs-lookup"><span data-stu-id="f8914-138">By specifying an endpoint when subscribing, Event Grid handles hello routing of events toothat endpoint.</span></span> <span data-ttu-id="f8914-139">Pour `<topic_name>`, utilisez la valeur hello vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="f8914-139">For `<topic_name>`, use hello value you created earlier.</span></span> 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a><span data-ttu-id="f8914-140">Envoyer une rubrique tooyour d’événement</span><span class="sxs-lookup"><span data-stu-id="f8914-140">Send an event tooyour topic</span></span>

<span data-ttu-id="f8914-141">Maintenant, nous allons déclencher un événement toosee comment grille d’événement distribue le point de terminaison tooyour de message hello.</span><span class="sxs-lookup"><span data-stu-id="f8914-141">Now, let's trigger an event toosee how Event Grid distributes hello message tooyour endpoint.</span></span> <span data-ttu-id="f8914-142">Tout d’abord, nous allons obtenir l’URL de hello et la clé pour la rubrique de hello.</span><span class="sxs-lookup"><span data-stu-id="f8914-142">First, let's get hello URL and key for hello topic.</span></span> <span data-ttu-id="f8914-143">Utilisez de nouveau le nom de votre rubrique pour `<topic_name>`.</span><span class="sxs-lookup"><span data-stu-id="f8914-143">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="f8914-144">toosimplify cet article, nous avons configuré exemple événement données toosend toohello de rubrique.</span><span class="sxs-lookup"><span data-stu-id="f8914-144">toosimplify this article, we have set up sample event data toosend toohello topic.</span></span> <span data-ttu-id="f8914-145">En règle générale, une application ou un service Azure envoie les données d’événement hello.</span><span class="sxs-lookup"><span data-stu-id="f8914-145">Typically, an application or Azure service would send hello event data.</span></span> <span data-ttu-id="f8914-146">Hello, l’exemple suivant obtient les données d’événement hello :</span><span class="sxs-lookup"><span data-stu-id="f8914-146">hello following example gets hello event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="f8914-147">Si vous `echo "$body"` vous pouvez voir les événements complète hello.</span><span class="sxs-lookup"><span data-stu-id="f8914-147">If you `echo "$body"` you can see hello full event.</span></span> <span data-ttu-id="f8914-148">Hello `data` élément Hello JSON est la charge utile de hello de votre événement.</span><span class="sxs-lookup"><span data-stu-id="f8914-148">hello `data` element of hello JSON is hello payload of your event.</span></span> <span data-ttu-id="f8914-149">N’importe quel fichier JSON bien construit peut être placé dans ce champ.</span><span class="sxs-lookup"><span data-stu-id="f8914-149">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="f8914-150">Vous pouvez également utiliser le champ de l’objet hello pour le routage et le filtrage avancés.</span><span class="sxs-lookup"><span data-stu-id="f8914-150">You can also use hello subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="f8914-151">CURL est un utilitaire qui effectue des requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="f8914-151">CURL is a utility that performs HTTP requests.</span></span> <span data-ttu-id="f8914-152">Dans cet article, nous utilisons le rubrique tooour événement CURL toosend hello.</span><span class="sxs-lookup"><span data-stu-id="f8914-152">In this article, we use CURL toosend hello event tooour topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="f8914-153">Vous avez avoir déclenché des événements de hello et grille d’événement envoyé le point de terminaison toohello de message hello que vous avez configuré lors de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="f8914-153">You have triggered hello event, and Event Grid sent hello message toohello endpoint you configured when subscribing.</span></span> <span data-ttu-id="f8914-154">Parcourir toohello RequestBin URL que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="f8914-154">Browse toohello RequestBin URL that you created earlier.</span></span> <span data-ttu-id="f8914-155">Ou cliquez sur Actualiser dans le navigateur RequestBin ouvert.</span><span class="sxs-lookup"><span data-stu-id="f8914-155">Or, click refresh in your open RequestBin browser.</span></span> <span data-ttu-id="f8914-156">Vous consultez les événements hello que vous venez d’envoyer.</span><span class="sxs-lookup"><span data-stu-id="f8914-156">You see hello event you just sent.</span></span> 

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

## <a name="clean-up-resources"></a><span data-ttu-id="f8914-157">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="f8914-157">Clean up resources</span></span>
<span data-ttu-id="f8914-158">Si vous prévoyez toocontinue utilisation de cet événement, procédez de nettoyer les ressources hello créées dans cet article.</span><span class="sxs-lookup"><span data-stu-id="f8914-158">If you plan toocontinue working with this event, do not clean up hello resources created in this article.</span></span> <span data-ttu-id="f8914-159">Si vous n’envisagez pas de toocontinue, utilisez hello suivant ressources hello toodelete de la commande que vous avez créé dans cet article.</span><span class="sxs-lookup"><span data-stu-id="f8914-159">If you do not plan toocontinue, use hello following command toodelete hello resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f8914-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f8914-160">Next steps</span></span>

<span data-ttu-id="f8914-161">Maintenant que vous savez comment toocreate rubriques et abonnements aux événements, en savoir plus sur la grille d’événement peut vous aider à effectuer :</span><span class="sxs-lookup"><span data-stu-id="f8914-161">Now that you know how toocreate topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- [<span data-ttu-id="f8914-162">Event Grid</span><span class="sxs-lookup"><span data-stu-id="f8914-162">About Event Grid</span></span>](overview.md)
- [<span data-ttu-id="f8914-163">Surveiller les modifications d’une machine virtuelle avec Azure Event Grid et Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="f8914-163">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)
