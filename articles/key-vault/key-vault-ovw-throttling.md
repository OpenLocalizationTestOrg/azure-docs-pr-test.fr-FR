---
ms.assetid: 
title: "Aide sur la limitation de requêtes Azure Key Vault | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: fe700e22c5323c2a0bdc315e349cd119798bcf40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="133bf-102">Aide sur la limitation de requêtes Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="133bf-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="133bf-103">La limitation de requêtes est le processus permettant de réduire le nombre d’appels simultanés au service Azure afin d’empêcher toute surexploitation des ressources.</span><span class="sxs-lookup"><span data-stu-id="133bf-103">Throttling is a process you initiate that limits the number of concurrent calls to the Azure service to prevent overuse of resources.</span></span> <span data-ttu-id="133bf-104">Azure Key Vault (AKV) est conçu pour gérer un volume élevé de requêtes.</span><span class="sxs-lookup"><span data-stu-id="133bf-104">Azure Key Vault (AKV) is designed to handle a high volume of requests.</span></span> <span data-ttu-id="133bf-105">En cas d’affluence, la limitation des requêtes du client permet de maintenir des performances et une fiabilité optimales pour le service AKV.</span><span class="sxs-lookup"><span data-stu-id="133bf-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of the AKV service.</span></span>

<span data-ttu-id="133bf-106">Les limites varient selon les scénarios.</span><span class="sxs-lookup"><span data-stu-id="133bf-106">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="133bf-107">Par exemple, si vous réalisez un volume important d’écritures, la possibilité de limitation est plus élevée que si vous effectuez uniquement des lectures.</span><span class="sxs-lookup"><span data-stu-id="133bf-107">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="133bf-108">Comment Key Vault gère-t-il ses limites ?</span><span class="sxs-lookup"><span data-stu-id="133bf-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="133bf-109">Les limites de service de Key Vault sont là pour empêcher tout usage abusif des ressources et garantir la qualité du service pour tous les clients de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="133bf-109">Service limits in Key Vault are there to prevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="133bf-110">En cas de dépassement d’un seuil de service, Key Vault limite toutes les autres requêtes de ce client sur une période donnée.</span><span class="sxs-lookup"><span data-stu-id="133bf-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="133bf-111">Dans ce cas, Key Vault retourne le code d’état HTTP 429 (Trop de requêtes), et les requêtes échouent.</span><span class="sxs-lookup"><span data-stu-id="133bf-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and the requests fail.</span></span> <span data-ttu-id="133bf-112">Par ailleurs, les requêtes qui ont échoué et retournent une erreur 429 sont comptabilisées dans les limites suivies par Key Vault.</span><span class="sxs-lookup"><span data-stu-id="133bf-112">Also, failed requests that return a 429 count towards the throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="133bf-113">Si vous avez un scénario valide justifiant une limitation supérieure, contactez-nous.</span><span class="sxs-lookup"><span data-stu-id="133bf-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-to-throttle-your-app-in-response-to-service-limits"></a><span data-ttu-id="133bf-114">Guide pratique pour limiter une application en réponse à des limites de service</span><span class="sxs-lookup"><span data-stu-id="133bf-114">How to throttle your app in response to service limits</span></span>

<span data-ttu-id="133bf-115">Voici les **meilleures pratiques** pour limiter une application :</span><span class="sxs-lookup"><span data-stu-id="133bf-115">The following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="133bf-116">Réduisez le nombre d’opérations par requête.</span><span class="sxs-lookup"><span data-stu-id="133bf-116">Reduce the number of operations per request.</span></span>
- <span data-ttu-id="133bf-117">Réduisez la fréquence des requêtes.</span><span class="sxs-lookup"><span data-stu-id="133bf-117">Reduce the frequency of requests.</span></span>
- <span data-ttu-id="133bf-118">Évitez les nouvelles tentatives immédiates.</span><span class="sxs-lookup"><span data-stu-id="133bf-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="133bf-119">Toutes les requêtes sont comptabilisées dans le cadre de vos limites d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="133bf-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="133bf-120">Lorsque vous implémentez la gestion des erreurs de votre application, utilisez le code d’erreur HTTP 429 pour détecter si une limitation côté client est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="133bf-120">When you implement your app's error handling, use the HTTP error code 429 to detect the need for client-side throttling.</span></span> <span data-ttu-id="133bf-121">Si la requête échoue à nouveau avec un code d’erreur HTTP 429, cela signifie que vous rencontrez toujours une limite de service Azure.</span><span class="sxs-lookup"><span data-stu-id="133bf-121">If the request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="133bf-122">Continuez à utiliser la méthode de limitation côté client recommandée, en réessayant la requête jusqu’à ce qu’elle aboutisse.</span><span class="sxs-lookup"><span data-stu-id="133bf-122">Continue to use the recommended client-side throttling method, retrying the request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="133bf-123">Méthode de limitation côté client recommandée</span><span class="sxs-lookup"><span data-stu-id="133bf-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="133bf-124">En cas de code d’erreur HTTP 429, commencez à limiter votre client suivant une approche d’interruption exponentielle :</span><span class="sxs-lookup"><span data-stu-id="133bf-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="133bf-125">Patientez une seconde, relancez la requête ;</span><span class="sxs-lookup"><span data-stu-id="133bf-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="133bf-126">Si la limitation persiste, patientez deux secondes, relancez la requête ;</span><span class="sxs-lookup"><span data-stu-id="133bf-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="133bf-127">Si la limitation persiste, patientez quatre secondes, relancez la requête ;</span><span class="sxs-lookup"><span data-stu-id="133bf-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="133bf-128">Si la limitation persiste, patientez huit secondes, relancez la requête ;</span><span class="sxs-lookup"><span data-stu-id="133bf-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="133bf-129">Si la limitation persiste, patientez seize secondes, relancez la requête.</span><span class="sxs-lookup"><span data-stu-id="133bf-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="133bf-130">À ce stade, vous ne devriez pas recevoir de code de réponse HTTP 429.</span><span class="sxs-lookup"><span data-stu-id="133bf-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="133bf-131">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="133bf-131">See also</span></span>

<span data-ttu-id="133bf-132">Pour orienter la limitation de façon plus approfondie sur Microsoft Cloud, consultez la page [Modèle de limitation](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span><span class="sxs-lookup"><span data-stu-id="133bf-132">For a deeper orientation of throttling on the Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

