---
ms.assetid: 
title: "aaaAzure des conseils de la limitation de coffre de clés | Documents Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="1a5ec-102">Aide sur la limitation de requêtes Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="1a5ec-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="1a5ec-103">La limitation est un processus que vous lancez qui limite le nombre de hello d’appels simultanés toohello service Azure tooprevent utilisation excessive de ressources.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-103">Throttling is a process you initiate that limits hello number of concurrent calls toohello Azure service tooprevent overuse of resources.</span></span> <span data-ttu-id="1a5ec-104">Azure Key Vault (AKV) est conçue toohandle un volume élevé de demandes.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-104">Azure Key Vault (AKV) is designed toohandle a high volume of requests.</span></span> <span data-ttu-id="1a5ec-105">Si un grand nombre de demandes se produit, la limitation de requêtes de votre client vous permet d’assurer des performances optimales et la fiabilité du service AKV de hello.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of hello AKV service.</span></span>

<span data-ttu-id="1a5ec-106">Limites limitation dépend du scénario de hello.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-106">Throttling limits vary based on hello scenario.</span></span> <span data-ttu-id="1a5ec-107">Par exemple, si vous effectuez un volume important d’écritures, possibilité hello pour la limitation est supérieure à si vous effectuez uniquement des lectures.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-107">For example, if you are performing a large volume of writes, hello possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="1a5ec-108">Comment Key Vault gère-t-il ses limites ?</span><span class="sxs-lookup"><span data-stu-id="1a5ec-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="1a5ec-109">Limites de service dans le coffre de clés sont les abus tooprevent des ressources et garantir la qualité de service pour tous les clients du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-109">Service limits in Key Vault are there tooprevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="1a5ec-110">En cas de dépassement d’un seuil de service, Key Vault limite toutes les autres requêtes de ce client sur une période donnée.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="1a5ec-111">Dans ce cas, le coffre de clés retourne le code d’état HTTP 429 (trop grand nombre de demandes), et les requêtes hello échouent.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and hello requests fail.</span></span> <span data-ttu-id="1a5ec-112">En outre, les demandes qui retournent un 429 comptabilisés dans les limites de limitation de bande passante hello suivies par le coffre de clés ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-112">Also, failed requests that return a 429 count towards hello throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="1a5ec-113">Si vous avez un scénario valide justifiant une limitation supérieure, contactez-nous.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a><span data-ttu-id="1a5ec-114">Comment toothrottle votre application dans la réponse tooservice limite</span><span class="sxs-lookup"><span data-stu-id="1a5ec-114">How toothrottle your app in response tooservice limits</span></span>

<span data-ttu-id="1a5ec-115">Hello Voici **meilleures pratiques** pour la limitation de votre application :</span><span class="sxs-lookup"><span data-stu-id="1a5ec-115">hello following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="1a5ec-116">Réduire le nombre hello d’opérations par demande.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-116">Reduce hello number of operations per request.</span></span>
- <span data-ttu-id="1a5ec-117">Réduisez la fréquence hello des requêtes.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-117">Reduce hello frequency of requests.</span></span>
- <span data-ttu-id="1a5ec-118">Évitez les nouvelles tentatives immédiates.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="1a5ec-119">Toutes les requêtes sont comptabilisées dans le cadre de vos limites d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="1a5ec-120">Lorsque vous implémentez la gestion des erreurs de votre application, utilisez hello HTTP Erreur code 429 toodetect hello besoin pour la limitation au niveau du client.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-120">When you implement your app's error handling, use hello HTTP error code 429 toodetect hello need for client-side throttling.</span></span> <span data-ttu-id="1a5ec-121">Si la demande de hello échoue à nouveau avec un code d’erreur HTTP 429, vous rencontrez toujours une limite de service Azure.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-121">If hello request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="1a5ec-122">Continuer toouse hello recommandé de méthode de limitation côté client, une nouvelle tentative de demande de hello jusqu'à ce qu’il réussisse.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-122">Continue toouse hello recommended client-side throttling method, retrying hello request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="1a5ec-123">Méthode de limitation côté client recommandée</span><span class="sxs-lookup"><span data-stu-id="1a5ec-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="1a5ec-124">En cas de code d’erreur HTTP 429, commencez à limiter votre client suivant une approche d’interruption exponentielle :</span><span class="sxs-lookup"><span data-stu-id="1a5ec-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="1a5ec-125">Patientez une seconde, relancez la requête ;</span><span class="sxs-lookup"><span data-stu-id="1a5ec-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="1a5ec-126">Si la limitation persiste, patientez deux secondes, relancez la requête ;</span><span class="sxs-lookup"><span data-stu-id="1a5ec-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="1a5ec-127">Si la limitation persiste, patientez quatre secondes, relancez la requête ;</span><span class="sxs-lookup"><span data-stu-id="1a5ec-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="1a5ec-128">Si la limitation persiste, patientez huit secondes, relancez la requête ;</span><span class="sxs-lookup"><span data-stu-id="1a5ec-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="1a5ec-129">Si la limitation persiste, patientez seize secondes, relancez la requête.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="1a5ec-130">À ce stade, vous ne devriez pas recevoir de code de réponse HTTP 429.</span><span class="sxs-lookup"><span data-stu-id="1a5ec-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="1a5ec-131">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="1a5ec-131">See also</span></span>

<span data-ttu-id="1a5ec-132">Pour une orientation plus approfondie de la limitation sur hello Cloud Microsoft, consultez [de limitation de modèle](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span><span class="sxs-lookup"><span data-stu-id="1a5ec-132">For a deeper orientation of throttling on hello Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

