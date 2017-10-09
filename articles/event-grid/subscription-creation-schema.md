---
title: "schéma d’abonnement aaaAzure grille d’événement"
description: "Décrit les propriétés de hello d’abonnement de l’événement tooan avec grille d’événement Azure."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: 6a96d67975a5a733c5ea3c56ea54501f94ea4cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="c4399-103">Schéma d’abonnement à Event Grid</span><span class="sxs-lookup"><span data-stu-id="c4399-103">Event Grid subscription schema</span></span>

<span data-ttu-id="c4399-104">toocreate un abonnement de la grille d’événement, vous envoyez une demande de toohello opération d’abonnement Create Event.</span><span class="sxs-lookup"><span data-stu-id="c4399-104">toocreate an Event Grid subscription, you send a request toohello Create Event subscription operation.</span></span> <span data-ttu-id="c4399-105">Utilisez hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="c4399-105">Use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="c4399-106">Par exemple, toocreate un abonnement aux événements pour un compte de stockage nommé `examplestorage` dans un groupe de ressources nommé `examplegroup`, format utilisez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="c4399-106">For example, toocreate an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="c4399-107">Hello décrit les propriétés hello et schéma de corps hello de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="c4399-107">hello article describes hello properties and schema for hello body of hello request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="c4399-108">Propriétés de l’abonnement aux événements</span><span class="sxs-lookup"><span data-stu-id="c4399-108">Event subscription properties</span></span>

| <span data-ttu-id="c4399-109">Propriété</span><span class="sxs-lookup"><span data-stu-id="c4399-109">Property</span></span> | <span data-ttu-id="c4399-110">Type</span><span class="sxs-lookup"><span data-stu-id="c4399-110">Type</span></span> | <span data-ttu-id="c4399-111">Description</span><span class="sxs-lookup"><span data-stu-id="c4399-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="c4399-112">destination</span><span class="sxs-lookup"><span data-stu-id="c4399-112">destination</span></span> | <span data-ttu-id="c4399-113">objet</span><span class="sxs-lookup"><span data-stu-id="c4399-113">object</span></span> | <span data-ttu-id="c4399-114">objet Hello qui définit le point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="c4399-114">hello object that defines hello endpoint.</span></span> |
| <span data-ttu-id="c4399-115">filter</span><span class="sxs-lookup"><span data-stu-id="c4399-115">filter</span></span> | <span data-ttu-id="c4399-116">objet</span><span class="sxs-lookup"><span data-stu-id="c4399-116">object</span></span> | <span data-ttu-id="c4399-117">Un champ facultatif pour le filtrage de types hello d’événements.</span><span class="sxs-lookup"><span data-stu-id="c4399-117">An optional field for filtering hello types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="c4399-118">objet de destination</span><span class="sxs-lookup"><span data-stu-id="c4399-118">destination object</span></span>

| <span data-ttu-id="c4399-119">Propriété</span><span class="sxs-lookup"><span data-stu-id="c4399-119">Property</span></span> | <span data-ttu-id="c4399-120">Type</span><span class="sxs-lookup"><span data-stu-id="c4399-120">Type</span></span> | <span data-ttu-id="c4399-121">Description</span><span class="sxs-lookup"><span data-stu-id="c4399-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="c4399-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="c4399-122">endpointType</span></span> | <span data-ttu-id="c4399-123">string</span><span class="sxs-lookup"><span data-stu-id="c4399-123">string</span></span> | <span data-ttu-id="c4399-124">type Hello du point de terminaison pour l’abonnement hello (webhook/HTTP, concentrateur d’événements ou file d’attente).</span><span class="sxs-lookup"><span data-stu-id="c4399-124">hello type of endpoint for hello subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="c4399-125">endpointUrl</span><span class="sxs-lookup"><span data-stu-id="c4399-125">endpointUrl</span></span> | <span data-ttu-id="c4399-126">string</span><span class="sxs-lookup"><span data-stu-id="c4399-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="c4399-127">objet de filtre</span><span class="sxs-lookup"><span data-stu-id="c4399-127">filter object</span></span>

| <span data-ttu-id="c4399-128">Propriété</span><span class="sxs-lookup"><span data-stu-id="c4399-128">Property</span></span> | <span data-ttu-id="c4399-129">Type</span><span class="sxs-lookup"><span data-stu-id="c4399-129">Type</span></span> | <span data-ttu-id="c4399-130">Description</span><span class="sxs-lookup"><span data-stu-id="c4399-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="c4399-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="c4399-131">includedEventTypes</span></span> | <span data-ttu-id="c4399-132">array</span><span class="sxs-lookup"><span data-stu-id="c4399-132">array</span></span> | <span data-ttu-id="c4399-133">Mettre en correspondance lorsque le type d’événement hello dans le message d’événement hello est un tooone de correspondance exacte de ces noms de type d’événement.</span><span class="sxs-lookup"><span data-stu-id="c4399-133">Match when hello event type in hello event message is an exact match tooone of these event type names.</span></span> <span data-ttu-id="c4399-134">Génère une erreur lorsque le nom de l’événement ne correspond pas à hello inscrit des noms de type d’événements pour la source d’événement hello.</span><span class="sxs-lookup"><span data-stu-id="c4399-134">Raises an error when event name does not match hello registered event type names for hello event source.</span></span> <span data-ttu-id="c4399-135">Génère une correspondance pour tous les types d’événements.</span><span class="sxs-lookup"><span data-stu-id="c4399-135">Default matches all event types.</span></span> |
| <span data-ttu-id="c4399-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="c4399-136">subjectBeginsWith</span></span> | <span data-ttu-id="c4399-137">string</span><span class="sxs-lookup"><span data-stu-id="c4399-137">string</span></span> | <span data-ttu-id="c4399-138">Un préfixe filtre toohello objet champ de correspondance dans le message d’événement hello.</span><span class="sxs-lookup"><span data-stu-id="c4399-138">A prefix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="c4399-139">valeur par défaut Hello ou chaîne vide correspond à tous.</span><span class="sxs-lookup"><span data-stu-id="c4399-139">hello default or empty string matches all.</span></span> | 
| <span data-ttu-id="c4399-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="c4399-140">subjectEndsWith</span></span> | <span data-ttu-id="c4399-141">string</span><span class="sxs-lookup"><span data-stu-id="c4399-141">string</span></span> | <span data-ttu-id="c4399-142">Un suffixe filtre toohello objet champ de correspondance dans le message d’événement hello.</span><span class="sxs-lookup"><span data-stu-id="c4399-142">A suffix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="c4399-143">valeur par défaut Hello ou chaîne vide correspond à tous.</span><span class="sxs-lookup"><span data-stu-id="c4399-143">hello default or empty string matches all.</span></span> |
| <span data-ttu-id="c4399-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="c4399-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="c4399-145">string</span><span class="sxs-lookup"><span data-stu-id="c4399-145">string</span></span> | <span data-ttu-id="c4399-146">Contrôle la correspondance sensible à la casse pour les filtres.</span><span class="sxs-lookup"><span data-stu-id="c4399-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="c4399-147">Exemple de schéma d’abonnement</span><span class="sxs-lookup"><span data-stu-id="c4399-147">Example subscription schema</span></span>

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "blobCreated", "blobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "subjectIsCaseSensitive": "true"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="c4399-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c4399-148">Next steps</span></span>

* <span data-ttu-id="c4399-149">Pour une introduction tooEvent grille, consultez [quelle est la grille d’événement ?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="c4399-149">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
