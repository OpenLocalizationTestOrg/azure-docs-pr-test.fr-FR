---
title: "les opérations asynchrones aaaAzure | Documents Microsoft"
description: "Décrit comment tootrack des opérations asynchrones dans Azure."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: b81254196013adf87998eff11a50993efa52d40d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="c5b99-103">Suivre les opérations asynchrones Azure</span><span class="sxs-lookup"><span data-stu-id="c5b99-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="c5b99-104">Certaines opérations REST de Azure exécutent de façon asynchrone car hello opération impossible rapidement.</span><span class="sxs-lookup"><span data-stu-id="c5b99-104">Some Azure REST operations run asynchronously because hello operation cannot be completed quickly.</span></span> <span data-ttu-id="c5b99-105">Cette rubrique décrit comment état de hello tootrack d’opérations asynchrones via les valeurs retournées dans la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="c5b99-105">This topic describes how tootrack hello status of asynchronous operations through values returned in hello response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="c5b99-106">Codes d’état pour les opérations asynchrones</span><span class="sxs-lookup"><span data-stu-id="c5b99-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="c5b99-107">Initialement, une opération asynchrone retourne un code d’état HTTP de type :</span><span class="sxs-lookup"><span data-stu-id="c5b99-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="c5b99-108">201 (créé)</span><span class="sxs-lookup"><span data-stu-id="c5b99-108">201 (Created)</span></span>
* <span data-ttu-id="c5b99-109">202 (accepté)</span><span class="sxs-lookup"><span data-stu-id="c5b99-109">202 (Accepted)</span></span> 

<span data-ttu-id="c5b99-110">Lors de l’opération de hello terminée avec succès, il renvoie :</span><span class="sxs-lookup"><span data-stu-id="c5b99-110">When hello operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="c5b99-111">200 (OK)</span><span class="sxs-lookup"><span data-stu-id="c5b99-111">200 (OK)</span></span>
* <span data-ttu-id="c5b99-112">204 (Pas de contenu)</span><span class="sxs-lookup"><span data-stu-id="c5b99-112">204 (No Content)</span></span> 

<span data-ttu-id="c5b99-113">Consultez toohello [documentation de l’API REST](/rest/api/) toosee les réponses hello pour l’opération hello vous en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="c5b99-113">Refer toohello [REST API documentation](/rest/api/) toosee hello responses for hello operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="c5b99-114">Surveiller l’état de l'opération</span><span class="sxs-lookup"><span data-stu-id="c5b99-114">Monitor status of operation</span></span>
<span data-ttu-id="c5b99-115">Hello asynchrone reste opérations retour valeurs d’en-tête, que vous pouvez utiliser l’état de hello toodetermine de hello l’opération.</span><span class="sxs-lookup"><span data-stu-id="c5b99-115">hello asynchronous REST operations return header values, which you use toodetermine hello status of hello operation.</span></span> <span data-ttu-id="c5b99-116">Il existe potentiellement en-tête trois valeurs tooexamine :</span><span class="sxs-lookup"><span data-stu-id="c5b99-116">There are potentially three header values tooexamine:</span></span>

* <span data-ttu-id="c5b99-117">`Azure-AsyncOperation`-URL de vérification de l’état en cours de hello d’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="c5b99-117">`Azure-AsyncOperation` - URL for checking hello ongoing status of hello operation.</span></span> <span data-ttu-id="c5b99-118">Si votre opération renvoie cette valeur, utilisez toujours le statut de hello tootrack informatique (au lieu d’emplacement) de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="c5b99-118">If your operation returns this value, always use it (instead of Location) tootrack hello status of hello operation.</span></span>
* <span data-ttu-id="c5b99-119">`Location`- URL pour déterminer si une opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="c5b99-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="c5b99-120">Utilisez cette valeur uniquement lorsque la valeur Azure-AsyncOperation n’est pas retournée.</span><span class="sxs-lookup"><span data-stu-id="c5b99-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="c5b99-121">`Retry-After`-hello du nombre de secondes toowait avant de vérifier l’état de hello d’opération asynchrone de hello.</span><span class="sxs-lookup"><span data-stu-id="c5b99-121">`Retry-After` - hello number of seconds toowait before checking hello status of hello asynchronous operation.</span></span>

<span data-ttu-id="c5b99-122">Toutefois, certaines opérations asynchrones ne retournent pas toutes ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="c5b99-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="c5b99-123">Par exemple, vous devrez peut-être valeur d’en-tête tooevaluate hello AsyncOperation de Azure pour une opération et la valeur de l’en-tête emplacement hello pour une autre opération.</span><span class="sxs-lookup"><span data-stu-id="c5b99-123">For example, you may need tooevaluate hello Azure-AsyncOperation header value for one operation, and hello Location header value for another operation.</span></span> 

<span data-ttu-id="c5b99-124">Pour récupérer des valeurs d’en-tête hello comme vous permet de récupérer n’importe quel valeur d’en-tête pour une demande.</span><span class="sxs-lookup"><span data-stu-id="c5b99-124">You retrieve hello header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="c5b99-125">Par exemple, en c#, extraire hello en-tête comprise entre un `HttpWebResponse` objet nommé `response` avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="c5b99-125">For example, in C#, you retrieve hello header value from an `HttpWebResponse` object named `response` with hello following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="c5b99-126">Demande et réponse Azure-AsyncOperation</span><span class="sxs-lookup"><span data-stu-id="c5b99-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="c5b99-127">état de hello tooget d’opération asynchrone de hello, envoyer une URL toohello de demande GET dans la valeur d’en-tête AsyncOperation de Azure.</span><span class="sxs-lookup"><span data-stu-id="c5b99-127">tooget hello status of hello asynchronous operation, send a GET request toohello URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="c5b99-128">corps Hello de réponse hello à partir de cette opération contient des informations sur les opération hello.</span><span class="sxs-lookup"><span data-stu-id="c5b99-128">hello body of hello response from this operation contains information about hello operation.</span></span> <span data-ttu-id="c5b99-129">Hello suivant montre les valeurs possibles de hello retournés à partir de l’opération de hello :</span><span class="sxs-lookup"><span data-stu-id="c5b99-129">hello following example shows hello possible values returned from hello operation:</span></span>

```json
{
    "id": "{resource path from GET operation}",
    "name": "{operation-id}", 
    "status" : "Succeeded | Failed | Canceled | {resource provider values}", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
    "percentComplete": {double between 0 and 100 },
    "properties": {
        /* Specific resource provider values for successful operations */
    },
    "error" : { 
        "code": "{error code}",  
        "message": "{error description}" 
    }
}
```

<span data-ttu-id="c5b99-130">Seule la valeur `status` est renvoyée pour toutes les réponses.</span><span class="sxs-lookup"><span data-stu-id="c5b99-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="c5b99-131">Hello erreur est retourné lorsque l’état de hello est Échec ou annulé.</span><span class="sxs-lookup"><span data-stu-id="c5b99-131">hello error object is returned when hello status is Failed or Canceled.</span></span> <span data-ttu-id="c5b99-132">Toutes les autres valeurs sont facultatives ; Par conséquent, la réponse hello que vous recevez peut ressembler différente de celle hello exemple.</span><span class="sxs-lookup"><span data-stu-id="c5b99-132">All other values are optional; therefore, hello response you receive may look different than hello example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="c5b99-133">Valeurs provisioningState</span><span class="sxs-lookup"><span data-stu-id="c5b99-133">provisioningState values</span></span>

<span data-ttu-id="c5b99-134">Les opérations qui créent, mettent à jour ou suppriment (PUT, PATCH, DELETE) une ressource retournent généralement une valeur `provisioningState`.</span><span class="sxs-lookup"><span data-stu-id="c5b99-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="c5b99-135">Lorsqu’une opération est terminée, une des trois valeurs suivantes est retournée :</span><span class="sxs-lookup"><span data-stu-id="c5b99-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="c5b99-136">Réussi</span><span class="sxs-lookup"><span data-stu-id="c5b99-136">Succeeded</span></span>
* <span data-ttu-id="c5b99-137">Échec</span><span class="sxs-lookup"><span data-stu-id="c5b99-137">Failed</span></span>
* <span data-ttu-id="c5b99-138">Canceled</span><span class="sxs-lookup"><span data-stu-id="c5b99-138">Canceled</span></span>

<span data-ttu-id="c5b99-139">Toutes les autres valeurs indiquent l’opération de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="c5b99-139">All other values indicate hello operation is still running.</span></span> <span data-ttu-id="c5b99-140">fournisseur de ressources Hello peut retourner une valeur personnalisée qui indique son état.</span><span class="sxs-lookup"><span data-stu-id="c5b99-140">hello resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="c5b99-141">Par exemple, vous pouvez recevoir **accepté** lorsque la demande de hello est reçu et en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="c5b99-141">For example, you may receive **Accepted** when hello request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="c5b99-142">Exemples de demandes et de réponses</span><span class="sxs-lookup"><span data-stu-id="c5b99-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="c5b99-143">Démarrez la machine virtuelle (202 avec Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="c5b99-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="c5b99-144">Cet exemple montre comment toodetermine hello état de **Démarrer** opération pour les ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="c5b99-144">This example shows how toodetermine hello status of **start** operation for virtual machines.</span></span> <span data-ttu-id="c5b99-145">demande initiale de Hello est Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="c5b99-145">hello initial request is in hello following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="c5b99-146">Renvoie le code d’état 202.</span><span class="sxs-lookup"><span data-stu-id="c5b99-146">It returns status code 202.</span></span> <span data-ttu-id="c5b99-147">Parmi les valeurs d’en-tête hello, vous voyez :</span><span class="sxs-lookup"><span data-stu-id="c5b99-147">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="c5b99-148">état de hello toocheck d’opération asynchrone hello, envoyer une autre demande toothat URL.</span><span class="sxs-lookup"><span data-stu-id="c5b99-148">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="c5b99-149">corps de réponse Hello contient l’état hello d’opération de hello :</span><span class="sxs-lookup"><span data-stu-id="c5b99-149">hello response body contains hello status of hello operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="c5b99-150">Déployer des ressources (201 avec Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="c5b99-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="c5b99-151">Cet exemple montre comment toodetermine hello état de **déploiements** opération pour le déploiement de ressources tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c5b99-151">This example shows how toodetermine hello status of **deployments** operation for deploying resources tooAzure.</span></span> <span data-ttu-id="c5b99-152">demande initiale de Hello est Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="c5b99-152">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="c5b99-153">Il renvoie le code d’état 201.</span><span class="sxs-lookup"><span data-stu-id="c5b99-153">It returns status code 201.</span></span> <span data-ttu-id="c5b99-154">Hello de corps de réponse de hello inclut :</span><span class="sxs-lookup"><span data-stu-id="c5b99-154">hello body of hello response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="c5b99-155">Parmi les valeurs d’en-tête hello, vous voyez :</span><span class="sxs-lookup"><span data-stu-id="c5b99-155">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="c5b99-156">état de hello toocheck d’opération asynchrone hello, envoyer une autre demande toothat URL.</span><span class="sxs-lookup"><span data-stu-id="c5b99-156">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="c5b99-157">corps de réponse Hello contient l’état hello d’opération de hello :</span><span class="sxs-lookup"><span data-stu-id="c5b99-157">hello response body contains hello status of hello operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="c5b99-158">Lorsque le déploiement de hello est terminé, la réponse de hello contient :</span><span class="sxs-lookup"><span data-stu-id="c5b99-158">When hello deployment is finished, hello response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="c5b99-159">Créer le compte de stockage (202 avec Location et Retry-After)</span><span class="sxs-lookup"><span data-stu-id="c5b99-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="c5b99-160">Cet exemple montre comment toodetermine hello état Hello **créer** opération pour les comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="c5b99-160">This example shows how toodetermine hello status of hello **create** operation for storage accounts.</span></span> <span data-ttu-id="c5b99-161">demande initiale de Hello est Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="c5b99-161">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="c5b99-162">Et le corps de la demande hello contient les propriétés de compte de stockage hello :</span><span class="sxs-lookup"><span data-stu-id="c5b99-162">And hello request body contains properties for hello storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="c5b99-163">Renvoie le code d’état 202.</span><span class="sxs-lookup"><span data-stu-id="c5b99-163">It returns status code 202.</span></span> <span data-ttu-id="c5b99-164">Parmi les valeurs d’en-tête hello, vous voyez hello deux valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="c5b99-164">Among hello header values, you see hello following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="c5b99-165">Après avoir attendu pour le nombre de secondes spécifié dans Retry-After, vérifiez l’état hello d’opération asynchrone de hello en envoyant une autre demande toothat URL.</span><span class="sxs-lookup"><span data-stu-id="c5b99-165">After waiting for number of seconds specified in Retry-After, check hello status of hello asynchronous operation by sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="c5b99-166">Si la demande de hello est en cours d’exécution, vous recevez un code d’état 202.</span><span class="sxs-lookup"><span data-stu-id="c5b99-166">If hello request is still running, you receive a status code 202.</span></span> <span data-ttu-id="c5b99-167">Si la demande de hello est terminée, votre recevoir un code d’état 200 et corps hello de réponse de hello contient des propriétés de hello hello du compte de stockage qui a été créé.</span><span class="sxs-lookup"><span data-stu-id="c5b99-167">If hello request has completed, your receive a status code 200, and hello body of hello response contains hello properties of hello storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5b99-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c5b99-168">Next steps</span></span>

* <span data-ttu-id="c5b99-169">Pour plus d'informations sur chaque opération REST, consultez la [documentation de l'API REST](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="c5b99-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="c5b99-170">Pour plus d’informations sur la gestion des ressources via hello REST API du Gestionnaire de ressources, consultez [Using hello REST API du Gestionnaire de ressources](resource-manager-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="c5b99-170">For information about managing resources through hello Resource Manager REST API, see [Using hello Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="c5b99-171">Pour plus d’informations sur le déploiement de modèles via hello REST API du Gestionnaire de ressources, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et les REST API du Gestionnaire de ressources](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="c5b99-171">for information about deploying templates through hello Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>
