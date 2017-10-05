---
title: "Limites de requête Azure Resource Manager | Microsoft Docs"
description: "Décrit comment utiliser la limitation avec des requêtes Azure Resource Manager lorsque les limites d’abonnement ont été atteintes."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: 6d7eeaf460674c3ab98425a5412ffa465b9ffd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="5cc3e-103">Limitation des requêtes de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5cc3e-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="5cc3e-104">Pour chaque abonnement et locataire, Resource Manager limite les requêtes de lecture à 15 000 par heure et les requêtes d’écriture à 1 200 par heure.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-104">For each subscription and tenant, Resource Manager limits read requests to 15,000 per hour and write requests to 1,200 per hour.</span></span> <span data-ttu-id="5cc3e-105">Ces limites s’appliquent à chaque instance Azure Resource Manager. Chaque région Azure comporte plusieurs instances, et Azure Resource Manager est déployé dans toutes les régions Azure.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-105">These limits apply to each Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed to all Azure regions.</span></span>  <span data-ttu-id="5cc3e-106">Par conséquent, dans la pratique, les limites sont effectivement beaucoup plus importantes que celles répertoriées ci-dessus, car les requêtes utilisateur sont généralement prises en charge par de nombreuses instances différentes.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="5cc3e-107">Si votre application ou script atteint ces limites, vous devez limiter vos requêtes.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-107">If your application or script reaches these limits, you need to throttle your requests.</span></span> <span data-ttu-id="5cc3e-108">Cette rubrique vous montre comment déterminer les requêtes restantes dont vous disposez avant d’atteindre la limite et comment réagir si vous avez atteint la limite.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-108">This topic shows you how to determine the remaining requests you have before reaching the limit, and how to respond when you have reached the limit.</span></span>

<span data-ttu-id="5cc3e-109">Lorsque vous atteignez la limite, vous recevez le code d’état HTTP **429 Trop de requêtes**.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-109">When you reach the limit, you receive the HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="5cc3e-110">L’étendue du nombre de requêtes est votre abonnement ou votre locataire.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-110">The number of requests is scoped to either your subscription or your tenant.</span></span> <span data-ttu-id="5cc3e-111">Si vous disposez de plusieurs applications simultanées envoyant des requêtes dans votre abonnement, les requêtes de ces applications sont combinées pour déterminer le nombre de requêtes restantes.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-111">If you have multiple, concurrent applications making requests in your subscription, the requests from those applications are added together to determine the number of remaining requests.</span></span>

<span data-ttu-id="5cc3e-112">Les requêtes étendues à l’abonnement sont celles qui impliquent la transmission de l’ID d’abonnement, par exemple pour récupérer les groupes de ressources dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-112">Subscription scoped requests are ones the involve passing your subscription id, such as retrieving the resource groups in your subscription.</span></span> <span data-ttu-id="5cc3e-113">Les requêtes étendues au locataire n’incluent pas votre ID d’abonnement, notamment pour la récupération des emplacements Azure valides.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="5cc3e-114">Requêtes restantes</span><span class="sxs-lookup"><span data-stu-id="5cc3e-114">Remaining requests</span></span>
<span data-ttu-id="5cc3e-115">Vous pouvez déterminer le nombre de requêtes restantes en examinant les en-têtes de réponse.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-115">You can determine the number of remaining requests by examining response headers.</span></span> <span data-ttu-id="5cc3e-116">Chaque demande contient des valeurs pour le nombre de requêtes de lecture et d’écriture restantes.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-116">Each request includes values for the number of remaining read and write requests.</span></span> <span data-ttu-id="5cc3e-117">Le tableau suivant décrit les en-têtes de réponse que vous pouvez examiner pour ces valeurs :</span><span class="sxs-lookup"><span data-stu-id="5cc3e-117">The following table describes the response headers you can examine for those values:</span></span>

| <span data-ttu-id="5cc3e-118">En-tête de réponse</span><span class="sxs-lookup"><span data-stu-id="5cc3e-118">Response header</span></span> | <span data-ttu-id="5cc3e-119">Description</span><span class="sxs-lookup"><span data-stu-id="5cc3e-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5cc3e-120">x-ms-ratelimit-remaining-subscription-reads</span><span class="sxs-lookup"><span data-stu-id="5cc3e-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="5cc3e-121">Requêtes de lecture restantes étendues à l’abonnement</span><span class="sxs-lookup"><span data-stu-id="5cc3e-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="5cc3e-122">x-ms-ratelimit-remaining-subscription-writes</span><span class="sxs-lookup"><span data-stu-id="5cc3e-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="5cc3e-123">Requêtes d’écriture restantes étendues à l’abonnement</span><span class="sxs-lookup"><span data-stu-id="5cc3e-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="5cc3e-124">x-ms-ratelimit-remaining-tenant-reads</span><span class="sxs-lookup"><span data-stu-id="5cc3e-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="5cc3e-125">Requêtes de lecture restantes étendues au locataire</span><span class="sxs-lookup"><span data-stu-id="5cc3e-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="5cc3e-126">x-ms-ratelimit-remaining-tenant-writes</span><span class="sxs-lookup"><span data-stu-id="5cc3e-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="5cc3e-127">Requêtes d’écriture restantes étendues au locataire</span><span class="sxs-lookup"><span data-stu-id="5cc3e-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="5cc3e-128">x-ms-ratelimit-remaining-subscription-resource-requests</span><span class="sxs-lookup"><span data-stu-id="5cc3e-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="5cc3e-129">Requêtes de type de ressource restantes étendues à l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="5cc3e-130">Cette valeur d’en-tête est retournée uniquement si un service a remplacé la limite par défaut.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-130">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="5cc3e-131">Resource Manager ajoute cette valeur au lieu des requêtes de lecture ou d’écriture de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-131">Resource Manager adds this value instead of the subscription reads or writes.</span></span> |
| <span data-ttu-id="5cc3e-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="5cc3e-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="5cc3e-133">Requêtes de collecte de type de ressource restantes étendues à l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="5cc3e-134">Cette valeur d’en-tête est retournée uniquement si un service a remplacé la limite par défaut.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-134">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="5cc3e-135">Cette valeur fournit le nombre de requêtes de collecte restantes (répertorier les ressources).</span><span class="sxs-lookup"><span data-stu-id="5cc3e-135">This value provides the number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="5cc3e-136">x-ms-ratelimit-remaining-tenant-resource-requests</span><span class="sxs-lookup"><span data-stu-id="5cc3e-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="5cc3e-137">Requêtes de type de ressource restantes étendues au locataire.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="5cc3e-138">Cet en-tête est ajouté uniquement pour les requêtes au niveau du locataire, et uniquement si un service a remplacé la limite par défaut.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-138">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> <span data-ttu-id="5cc3e-139">Resource Manager ajoute cette valeur au lieu des requêtes de lecture ou d’écriture du locataire.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-139">Resource Manager adds this value instead of the tenant reads or writes.</span></span> |
| <span data-ttu-id="5cc3e-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="5cc3e-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="5cc3e-141">Requêtes de collecte de type de ressource restantes étendues au locataire.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="5cc3e-142">Cet en-tête est ajouté uniquement pour les requêtes au niveau du locataire, et uniquement si un service a remplacé la limite par défaut.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-142">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> |

## <a name="retrieving-the-header-values"></a><span data-ttu-id="5cc3e-143">Récupération des valeurs d’en-tête</span><span class="sxs-lookup"><span data-stu-id="5cc3e-143">Retrieving the header values</span></span>
<span data-ttu-id="5cc3e-144">La récupération de ces valeurs d’en-tête dans votre code ou script est similaire à la récupération de n’importe quelle valeur d’en-tête.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="5cc3e-145">Par exemple, en **C#**, vous récupérez la valeur d’en-tête d’un objet **HttpWebResponse** nommé **response** avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="5cc3e-145">For example, in **C#**, you retrieve the header value from an **HttpWebResponse** object named **response** with the following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="5cc3e-146">Dans **PowerShell**, vous récupérez la valeur de l’en-tête d’une opération Invoke-WebRequest.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-146">In **PowerShell**, you retrieve the header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="5cc3e-147">Ou, si voulez voir les requêtes restantes pour le débogage, vous pouvez définir le paramètre **-Debug** sur votre applet de commande **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-147">Or, if want to see the remaining requests for debugging, you can provide the **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="5cc3e-148">Retourne un grand nombre de valeurs, notamment la valeur de réponse suivante :</span><span class="sxs-lookup"><span data-stu-id="5cc3e-148">Which returns many values, including the following response value:</span></span>

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

<span data-ttu-id="5cc3e-149">Dans **l’interface de ligne de commande**, vous récupérez la valeur d’en-tête à l’aide de l’option plus détaillée.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-149">In **Azure CLI**, you retrieve the header value by using the more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="5cc3e-150">Retourne un grand nombre de valeurs, notamment l’objet suivant :</span><span class="sxs-lookup"><span data-stu-id="5cc3e-150">Which returns many values, including the following object:</span></span>

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="5cc3e-151">Attente avant l’envoi de la requête suivante</span><span class="sxs-lookup"><span data-stu-id="5cc3e-151">Waiting before sending next request</span></span>
<span data-ttu-id="5cc3e-152">Lorsque vous atteignez la limite de requêtes, Resource Manager renvoie le code d’état HTTP **429** et une valeur **Retry-After** dans l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-152">When you reach the request limit, Resource Manager returns the **429** HTTP status code and a **Retry-After** value in the header.</span></span> <span data-ttu-id="5cc3e-153">La valeur **Retry-After** spécifie le nombre de secondes pendant lesquelles votre application doit attendre (ou rester en veille) avant d’envoyer la requête suivante.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-153">The **Retry-After** value specifies the number of seconds your application should wait (or sleep) before sending the next request.</span></span> <span data-ttu-id="5cc3e-154">Si vous envoyez une requête avant l’écoulement du temps d’attente, votre requête n’est pas traitée et une nouvelle valeur de nouvelle tentative est retournée.</span><span class="sxs-lookup"><span data-stu-id="5cc3e-154">If you send a request before the retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cc3e-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5cc3e-155">Next steps</span></span>

* <span data-ttu-id="5cc3e-156">Pour plus d’informations sur les limites et les quotas, consultez [Abonnement Azure et limites, quotas et contraintes du service](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="5cc3e-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="5cc3e-157">Pour en savoir plus sur la gestion des demandes REST asynchrones, consultez [Suivi des opérations asynchrones Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="5cc3e-157">To learn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
