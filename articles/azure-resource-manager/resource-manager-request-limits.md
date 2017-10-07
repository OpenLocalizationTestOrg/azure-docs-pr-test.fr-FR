---
title: les limites des demandes Gestionnaire de ressources aaaAzure | Documents Microsoft
description: "Décrit comment les demandes toouse limitation avec Azure Resource Manager lorsque les limites de l’abonnement ont été atteintes."
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
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="d9886-103">Limitation des requêtes de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d9886-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="d9886-104">Pour chaque abonnement et le client, les limites de gestionnaire de ressources too15 de demandes, 000 par heure et écrira les demandes too1, 200 par heure.</span><span class="sxs-lookup"><span data-stu-id="d9886-104">For each subscription and tenant, Resource Manager limits read requests too15,000 per hour and write requests too1,200 per hour.</span></span> <span data-ttu-id="d9886-105">Ces limites s’appliquent d’instance d’Azure Resource Manager tooeach ; Il existe plusieurs instances dans chaque région Azure et Azure Resource Manager est déployé tooall Azure régions.</span><span class="sxs-lookup"><span data-stu-id="d9886-105">These limits apply tooeach Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed tooall Azure regions.</span></span>  <span data-ttu-id="d9886-106">Par conséquent, dans la pratique, les limites sont effectivement beaucoup plus importantes que celles répertoriées ci-dessus, car les requêtes utilisateur sont généralement prises en charge par de nombreuses instances différentes.</span><span class="sxs-lookup"><span data-stu-id="d9886-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="d9886-107">Si votre application ou le script atteint ces limites, vous devez toothrottle vos demandes.</span><span class="sxs-lookup"><span data-stu-id="d9886-107">If your application or script reaches these limits, you need toothrottle your requests.</span></span> <span data-ttu-id="d9886-108">Cette rubrique vous montre comment hello toodetermine restant demande que vous avez avant d’atteindre la limite de hello et toorespond lorsque vous avez atteint la limite de hello.</span><span class="sxs-lookup"><span data-stu-id="d9886-108">This topic shows you how toodetermine hello remaining requests you have before reaching hello limit, and how toorespond when you have reached hello limit.</span></span>

<span data-ttu-id="d9886-109">Lorsque vous atteignez la limite de hello, vous recevez le code d’état HTTP de hello **429 trop grand nombre de demandes**.</span><span class="sxs-lookup"><span data-stu-id="d9886-109">When you reach hello limit, you receive hello HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="d9886-110">nombre de demandes de Hello est étendue tooeither votre abonnement ou votre client.</span><span class="sxs-lookup"><span data-stu-id="d9886-110">hello number of requests is scoped tooeither your subscription or your tenant.</span></span> <span data-ttu-id="d9886-111">Si vous avez plusieurs, applications simultanées qui effectue des demandes dans votre abonnement, hello requêtes à partir de ces applications sont ajoutées ensemble toodetermine hello quantité, pour les requêtes restantes.</span><span class="sxs-lookup"><span data-stu-id="d9886-111">If you have multiple, concurrent applications making requests in your subscription, hello requests from those applications are added together toodetermine hello number of remaining requests.</span></span>

<span data-ttu-id="d9886-112">Demandes d’abonnement d’une étendue sont celles hello impliquent le passage de votre id d’abonnement, telles que la récupération des groupes de ressources hello dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="d9886-112">Subscription scoped requests are ones hello involve passing your subscription id, such as retrieving hello resource groups in your subscription.</span></span> <span data-ttu-id="d9886-113">Les requêtes étendues au locataire n’incluent pas votre ID d’abonnement, notamment pour la récupération des emplacements Azure valides.</span><span class="sxs-lookup"><span data-stu-id="d9886-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="d9886-114">Requêtes restantes</span><span class="sxs-lookup"><span data-stu-id="d9886-114">Remaining requests</span></span>
<span data-ttu-id="d9886-115">Vous pouvez déterminer le nombre de hello d’autres demandes en examinant les en-têtes de réponse.</span><span class="sxs-lookup"><span data-stu-id="d9886-115">You can determine hello number of remaining requests by examining response headers.</span></span> <span data-ttu-id="d9886-116">Chaque demande inclut des valeurs pour le nombre de hello de restant en lecture et les demandes d’écriture.</span><span class="sxs-lookup"><span data-stu-id="d9886-116">Each request includes values for hello number of remaining read and write requests.</span></span> <span data-ttu-id="d9886-117">Hello tableau suivant décrit les en-têtes de réponse hello que vous pouvez examiner ces valeurs :</span><span class="sxs-lookup"><span data-stu-id="d9886-117">hello following table describes hello response headers you can examine for those values:</span></span>

| <span data-ttu-id="d9886-118">En-tête de réponse</span><span class="sxs-lookup"><span data-stu-id="d9886-118">Response header</span></span> | <span data-ttu-id="d9886-119">Description</span><span class="sxs-lookup"><span data-stu-id="d9886-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d9886-120">x-ms-ratelimit-remaining-subscription-reads</span><span class="sxs-lookup"><span data-stu-id="d9886-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="d9886-121">Requêtes de lecture restantes étendues à l’abonnement</span><span class="sxs-lookup"><span data-stu-id="d9886-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="d9886-122">x-ms-ratelimit-remaining-subscription-writes</span><span class="sxs-lookup"><span data-stu-id="d9886-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="d9886-123">Requêtes d’écriture restantes étendues à l’abonnement</span><span class="sxs-lookup"><span data-stu-id="d9886-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="d9886-124">x-ms-ratelimit-remaining-tenant-reads</span><span class="sxs-lookup"><span data-stu-id="d9886-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="d9886-125">Requêtes de lecture restantes étendues au locataire</span><span class="sxs-lookup"><span data-stu-id="d9886-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="d9886-126">x-ms-ratelimit-remaining-tenant-writes</span><span class="sxs-lookup"><span data-stu-id="d9886-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="d9886-127">Requêtes d’écriture restantes étendues au locataire</span><span class="sxs-lookup"><span data-stu-id="d9886-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="d9886-128">x-ms-ratelimit-remaining-subscription-resource-requests</span><span class="sxs-lookup"><span data-stu-id="d9886-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="d9886-129">Requêtes de type de ressource restantes étendues à l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="d9886-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="d9886-130">Cette valeur d’en-tête est uniquement retournée si un service a remplacé la limite par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="d9886-130">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="d9886-131">Le Gestionnaire de ressources ajoute cette valeur au lieu de hello abonnement lectures ou écritures.</span><span class="sxs-lookup"><span data-stu-id="d9886-131">Resource Manager adds this value instead of hello subscription reads or writes.</span></span> |
| <span data-ttu-id="d9886-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="d9886-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="d9886-133">Requêtes de collecte de type de ressource restantes étendues à l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="d9886-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="d9886-134">Cette valeur d’en-tête est uniquement retournée si un service a remplacé la limite par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="d9886-134">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="d9886-135">Cette valeur fournit un nombre de hello d’autres demandes de collecte (ressources de la liste).</span><span class="sxs-lookup"><span data-stu-id="d9886-135">This value provides hello number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="d9886-136">x-ms-ratelimit-remaining-tenant-resource-requests</span><span class="sxs-lookup"><span data-stu-id="d9886-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="d9886-137">Requêtes de type de ressource restantes étendues au locataire.</span><span class="sxs-lookup"><span data-stu-id="d9886-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="d9886-138">Cet en-tête est ajouté uniquement pour les demandes au niveau du client, et uniquement si un service a remplacé la limite par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="d9886-138">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> <span data-ttu-id="d9886-139">Le Gestionnaire de ressources ajoute cette valeur au lieu de hello client lectures ou écritures.</span><span class="sxs-lookup"><span data-stu-id="d9886-139">Resource Manager adds this value instead of hello tenant reads or writes.</span></span> |
| <span data-ttu-id="d9886-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span><span class="sxs-lookup"><span data-stu-id="d9886-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="d9886-141">Requêtes de collecte de type de ressource restantes étendues au locataire.</span><span class="sxs-lookup"><span data-stu-id="d9886-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="d9886-142">Cet en-tête est ajouté uniquement pour les demandes au niveau du client, et uniquement si un service a remplacé la limite par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="d9886-142">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> |

## <a name="retrieving-hello-header-values"></a><span data-ttu-id="d9886-143">La récupération des valeurs d’en-tête hello</span><span class="sxs-lookup"><span data-stu-id="d9886-143">Retrieving hello header values</span></span>
<span data-ttu-id="d9886-144">La récupération de ces valeurs d’en-tête dans votre code ou script est similaire à la récupération de n’importe quelle valeur d’en-tête.</span><span class="sxs-lookup"><span data-stu-id="d9886-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="d9886-145">Par exemple, dans **c#**, vous récupérez la valeur à partir de l’en-tête hello un **HttpWebResponse** objet nommé **réponse** avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="d9886-145">For example, in **C#**, you retrieve hello header value from an **HttpWebResponse** object named **response** with hello following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="d9886-146">Dans **PowerShell**, vous récupériez la valeur d’en-tête hello à partir d’une opération Invoke-WebRequest.</span><span class="sxs-lookup"><span data-stu-id="d9886-146">In **PowerShell**, you retrieve hello header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="d9886-147">Ou, si voulez restant de hello toosee des demandes pour le débogage, vous pouvez fournir hello **-déboguer** paramètre sur votre **PowerShell** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="d9886-147">Or, if want toosee hello remaining requests for debugging, you can provide hello **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="d9886-148">Qui retourne le nombre de valeurs, y compris hello suivant la valeur de la réponse :</span><span class="sxs-lookup"><span data-stu-id="d9886-148">Which returns many values, including hello following response value:</span></span>

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

<span data-ttu-id="d9886-149">Dans **CLI d’Azure**, vous récupérer la valeur d’en-tête hello à l’aide de hello option plus détaillée.</span><span class="sxs-lookup"><span data-stu-id="d9886-149">In **Azure CLI**, you retrieve hello header value by using hello more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="d9886-150">Qui retourne le nombre de valeurs, y compris hello objet :</span><span class="sxs-lookup"><span data-stu-id="d9886-150">Which returns many values, including hello following object:</span></span>

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

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="d9886-151">Attente avant l’envoi de la requête suivante</span><span class="sxs-lookup"><span data-stu-id="d9886-151">Waiting before sending next request</span></span>
<span data-ttu-id="d9886-152">Lorsque vous atteignez la limite de demandes hello, Gestionnaire de ressources renvoie hello **429** code d’état HTTP et un **Retry-After** valeur dans l’en-tête de hello.</span><span class="sxs-lookup"><span data-stu-id="d9886-152">When you reach hello request limit, Resource Manager returns hello **429** HTTP status code and a **Retry-After** value in hello header.</span></span> <span data-ttu-id="d9886-153">Hello **Retry-After** valeur spécifie le nombre de hello de secondes pendant lesquelles votre application doit attendre (ou en veille) avant d’envoyer la demande suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="d9886-153">hello **Retry-After** value specifies hello number of seconds your application should wait (or sleep) before sending hello next request.</span></span> <span data-ttu-id="d9886-154">Si vous envoyez une demande avant de la valeur de nouvelle tentative hello s’est écoulé, votre demande n’est pas traitée et une nouvelle valeur de nouvelle tentative est retournée.</span><span class="sxs-lookup"><span data-stu-id="d9886-154">If you send a request before hello retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9886-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9886-155">Next steps</span></span>

* <span data-ttu-id="d9886-156">Pour plus d’informations sur les limites et les quotas, consultez [Abonnement Azure et limites, quotas et contraintes du service](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="d9886-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="d9886-157">toolearn sur la gestion des demandes asynchrones de REST, consultez [le suivi des opérations asynchrones Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="d9886-157">toolearn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
