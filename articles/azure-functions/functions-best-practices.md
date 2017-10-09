---
title: Pratiques aaaBest pour les fonctions de Azure | Documents Microsoft
description: "Découvrez les bonnes pratiques et les modèles pour Azure Functions."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, modèles, bonne pratique, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur"
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/13/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd3d826b75267a740e355b008943a48f71ebd339
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="92b23-104">Optimiser les performances de hello et la fiabilité des fonctions d’Azure</span><span class="sxs-lookup"><span data-stu-id="92b23-104">Optimize hello performance and reliability of Azure Functions</span></span>

<span data-ttu-id="92b23-105">Cet article fournit des conseils tooimprove hello et fiabilité des applications de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="92b23-105">This article provides guidance tooimprove hello performance and reliability of your function apps.</span></span> 


## <a name="avoid-long-running-functions"></a><span data-ttu-id="92b23-106">Évitez les fonctions dont l’exécution prend beaucoup de longtemps</span><span class="sxs-lookup"><span data-stu-id="92b23-106">Avoid long running functions</span></span>

<span data-ttu-id="92b23-107">Ces fonctions peuvent provoquer des problèmes de délai d’attente inattendus.</span><span class="sxs-lookup"><span data-stu-id="92b23-107">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="92b23-108">Une fonction peut devenir volumineux en raison des dépendances de Node.js réduire.</span><span class="sxs-lookup"><span data-stu-id="92b23-108">A function can become large due toomany Node.js dependencies.</span></span> <span data-ttu-id="92b23-109">L’importation des dépendances peut entraîner une augmentation des temps de chargement aboutissant à des délais d’attente inattendus.</span><span class="sxs-lookup"><span data-stu-id="92b23-109">Importing dependencies can also cause increased load times that result in unexpected timeouts.</span></span> <span data-ttu-id="92b23-110">Les dépendances sont chargées tant explicitement qu’implicitement.</span><span class="sxs-lookup"><span data-stu-id="92b23-110">Dependencies are loaded both explicitly and implicitly.</span></span> <span data-ttu-id="92b23-111">Un module chargé par votre code peut charger ses propres modules supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="92b23-111">A single module loaded by your code may load its own additional modules.</span></span>  

<span data-ttu-id="92b23-112">Autant que possible, subdivisez les fonctions volumineuses en ensembles de fonctions plus petits qui fonctionnent ensemble et retournent des réponses rapides.</span><span class="sxs-lookup"><span data-stu-id="92b23-112">Whenever possible, refactor large functions into smaller function sets that work together and return responses fast.</span></span> <span data-ttu-id="92b23-113">Par exemple, un webhook ou une fonction de déclenchement HTTP peut nécessiter une réponse de l’accusé de réception dans un délai imparti ; Il est courant pour le webhooks toorequire une réponse immédiate.</span><span class="sxs-lookup"><span data-stu-id="92b23-113">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it is common for webhooks toorequire an immediate response.</span></span> <span data-ttu-id="92b23-114">Vous pouvez passer la charge utile de déclencheur hello HTTP dans un toobe de file d’attente traité par une fonction de déclenchement de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="92b23-114">You can pass hello HTTP trigger payload into a queue toobe processed by a queue trigger function.</span></span> <span data-ttu-id="92b23-115">Cette approche vous permet de travail réel de toodefer hello et retourner une réponse immédiate.</span><span class="sxs-lookup"><span data-stu-id="92b23-115">This approach allows you toodefer hello actual work and return an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="92b23-116">Communication entre fonctions</span><span class="sxs-lookup"><span data-stu-id="92b23-116">Cross function communication</span></span>

<span data-ttu-id="92b23-117">Lors de l’intégration de plusieurs fonctions, il est généralement d’une meilleure pratique toouse stockage files d’attente pour entre la communication de la fonction.</span><span class="sxs-lookup"><span data-stu-id="92b23-117">When integrating multiple functions, it is generally a best practice toouse storage queues for cross function communication.</span></span>  <span data-ttu-id="92b23-118">Hello est files d’attente de stockage sont moins chers et quantité tooprovision plus facile.</span><span class="sxs-lookup"><span data-stu-id="92b23-118">hello main reason is storage queues are cheaper and much easier tooprovision.</span></span> 

<span data-ttu-id="92b23-119">Les messages individuels dans une file d’attente de stockage sont limités en taille too64 Ko.</span><span class="sxs-lookup"><span data-stu-id="92b23-119">Individual messages in a storage queue are limited in size too64 KB.</span></span> <span data-ttu-id="92b23-120">Si vous avez besoin de toopass des messages plus volumineux entre les fonctions, une file d’attente Azure Service Bus peut être utilisé toosupport la taille des messages des too256 Ko.</span><span class="sxs-lookup"><span data-stu-id="92b23-120">If you need toopass larger messages between functions, an Azure Service Bus queue could be used toosupport message sizes up too256 KB.</span></span>

<span data-ttu-id="92b23-121">Les rubriques Service Bus sont utiles si vous avez besoin de filtrer les messages avant de les traiter.</span><span class="sxs-lookup"><span data-stu-id="92b23-121">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="92b23-122">Concentrateurs d’événements sont des communications d’un volume élevé de toosupport utile.</span><span class="sxs-lookup"><span data-stu-id="92b23-122">Event hubs are useful toosupport high volume communications.</span></span>


## <a name="write-functions-toobe-stateless"></a><span data-ttu-id="92b23-123">Écrire des fonctions toobe de sans état</span><span class="sxs-lookup"><span data-stu-id="92b23-123">Write functions toobe stateless</span></span> 

<span data-ttu-id="92b23-124">Les fonctions doivent être sans état et idempotentes si possible.</span><span class="sxs-lookup"><span data-stu-id="92b23-124">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="92b23-125">Associez toutes les informations d’état requises à vos données.</span><span class="sxs-lookup"><span data-stu-id="92b23-125">Associate any required state information with your data.</span></span> <span data-ttu-id="92b23-126">Par exemple, une commande en cours de traitement aurait probablement un membre `state` associé.</span><span class="sxs-lookup"><span data-stu-id="92b23-126">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="92b23-127">Une fonction a pu traiter une commande en fonction de cet état tant que fonction hello proprement dite reste sans état.</span><span class="sxs-lookup"><span data-stu-id="92b23-127">A function could process an order based on that state while hello function itself remains stateless.</span></span> 

<span data-ttu-id="92b23-128">Les fonctions idempotentes sont particulièrement recommandées avec les déclencheurs à minuterie.</span><span class="sxs-lookup"><span data-stu-id="92b23-128">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="92b23-129">Par exemple, si vous avez quelque chose que vous devez absolument exécuter une fois par jour, son écriture afin qu’il puisse s’exécuter n’importe quel moment de la journée de hello avec hello mêmes résultats.</span><span class="sxs-lookup"><span data-stu-id="92b23-129">For example, if you have something that absolutely must run once a day, write it so it can run any time during hello day with hello same results.</span></span> <span data-ttu-id="92b23-130">fonction Hello peut se fermer lorsqu’il n’existe aucun travail d’un jour donné.</span><span class="sxs-lookup"><span data-stu-id="92b23-130">hello function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="92b23-131">Également si une exécution précédente a échoué toocomplete, de la prochaine exécution de hello doit choisir où elle s’était arrêtée.</span><span class="sxs-lookup"><span data-stu-id="92b23-131">Also if a previous run failed toocomplete, hello next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="92b23-132">Écrire des fonctions défensives</span><span class="sxs-lookup"><span data-stu-id="92b23-132">Write defensive functions</span></span>

<span data-ttu-id="92b23-133">Supposons que votre fonction peut être confrontée à une exception à tout moment.</span><span class="sxs-lookup"><span data-stu-id="92b23-133">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="92b23-134">Concevez vos fonctions avec toocontinue de capacité hello à partir d’un point d’échec précédent lors de l’exécution suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="92b23-134">Design your functions with hello ability toocontinue from a previous fail point during hello next execution.</span></span> <span data-ttu-id="92b23-135">Considérez un scénario qui nécessite hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="92b23-135">Consider a scenario that requires hello following actions:</span></span>

1. <span data-ttu-id="92b23-136">Récupérer 10 000 lignes d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="92b23-136">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="92b23-137">Créer un message de la file d’attente pour chacun de ces tooprocess lignes davantage les ligne hello vers le bas.</span><span class="sxs-lookup"><span data-stu-id="92b23-137">Create a queue message for each of those rows tooprocess further down hello line.</span></span>
 
<span data-ttu-id="92b23-138">Selon la complexité de votre système, il est possible que des services impliqués en aval se comportent de manière incorrecte, que des pannes réseau se produisent, que des limites de quota soient atteintes, etc. Tous ces facteurs peuvent affecter votre fonction à tout moment.</span><span class="sxs-lookup"><span data-stu-id="92b23-138">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="92b23-139">Vous devez toodesign votre toobe fonctions préparé.</span><span class="sxs-lookup"><span data-stu-id="92b23-139">You need toodesign your functions toobe prepared for it.</span></span>

<span data-ttu-id="92b23-140">Comment votre code réagit-il si une défaillance se produit après l’insertion de 5 000 de ces éléments dans une file d’attente en vue de leur traitement ?</span><span class="sxs-lookup"><span data-stu-id="92b23-140">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="92b23-141">Suivez les éléments dans un jeu que vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="92b23-141">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="92b23-142">Sinon, vous pouvez les réinsérer la prochaine fois.</span><span class="sxs-lookup"><span data-stu-id="92b23-142">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="92b23-143">Cela peut avoir un impact sérieux sur votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="92b23-143">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="92b23-144">Si un élément de la file d’attente a déjà été traité, autoriser votre toobe fonction aucune opération.</span><span class="sxs-lookup"><span data-stu-id="92b23-144">If a queue item was already processed, allow your function toobe a no-op.</span></span>

<span data-ttu-id="92b23-145">Tirer parti des mesures de protection déjà fournie pour les composants que vous utilisez dans la plateforme des fonctions de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="92b23-145">Take advantage of defensive measures already provided for components you use in hello Azure Functions platform.</span></span> <span data-ttu-id="92b23-146">Par exemple, consultez **la gestion des messages de la file d’attente de messages incohérents** dans la documentation de hello de [déclenche de la file d’attente de stockage Azure](functions-bindings-storage-queue.md#trigger).</span><span class="sxs-lookup"><span data-stu-id="92b23-146">For example, see **Handling poison queue messages** in hello documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a><span data-ttu-id="92b23-147">Ne combinaison de test et production de code Bonjour même application de la fonction</span><span class="sxs-lookup"><span data-stu-id="92b23-147">Don't mix test and production code in hello same function app</span></span>

<span data-ttu-id="92b23-148">Les fonctions d’une application de fonction partagent des ressources.</span><span class="sxs-lookup"><span data-stu-id="92b23-148">Functions within a function app share resources.</span></span> <span data-ttu-id="92b23-149">Par exemple, la mémoire est partagée.</span><span class="sxs-lookup"><span data-stu-id="92b23-149">For example, memory is shared.</span></span> <span data-ttu-id="92b23-150">Si vous utilisez une application de la fonction en production, n’ajoutez pas aux tests de fonctions et ressources tooit.</span><span class="sxs-lookup"><span data-stu-id="92b23-150">If you're using a function app in production, don't add test-related functions and resources tooit.</span></span> <span data-ttu-id="92b23-151">Cela peut entraîner une surcharge inattendue pendant l’exécution du code de production.</span><span class="sxs-lookup"><span data-stu-id="92b23-151">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="92b23-152">Soyez attentif à ce que vous chargez dans vos applications de fonction en production.</span><span class="sxs-lookup"><span data-stu-id="92b23-152">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="92b23-153">Mémoire moyenne est calculée sur chaque fonction de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="92b23-153">Memory is averaged across each function in hello app.</span></span>

<span data-ttu-id="92b23-154">Si un assembly partagé est référencé dans plusieurs fonctions .Net, placez-le dans un dossier partagé commun.</span><span class="sxs-lookup"><span data-stu-id="92b23-154">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="92b23-155">Assembly hello de référence avec un toohello similaire instruction l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="92b23-155">Reference hello assembly with a statement similar toohello following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="92b23-156">Dans le cas contraire, il est facile tooaccidentally déployer plusieurs versions de test du même binaire qui se comportent différemment entre les fonctions de hello.</span><span class="sxs-lookup"><span data-stu-id="92b23-156">Otherwise, it is easy tooaccidentally deploy multiple test versions of hello same binary that behave differently between functions.</span></span>

<span data-ttu-id="92b23-157">N’utilisez pas de journalisation détaillée dans le code de production.</span><span class="sxs-lookup"><span data-stu-id="92b23-157">Don't use verbose logging in production code.</span></span> <span data-ttu-id="92b23-158">Cela affecte les performances.</span><span class="sxs-lookup"><span data-stu-id="92b23-158">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-blocking-calls"></a><span data-ttu-id="92b23-159">Utiliser du code asynchrone tout en évitant de bloquer les appels</span><span class="sxs-lookup"><span data-stu-id="92b23-159">Use async code but avoid blocking calls</span></span>

<span data-ttu-id="92b23-160">La programmation asynchrone est une pratique recommandée.</span><span class="sxs-lookup"><span data-stu-id="92b23-160">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="92b23-161">Toutefois, toujours éviter de référencer hello `Result` propriété ou l’appel `Wait` méthode sur un `Task` instance.</span><span class="sxs-lookup"><span data-stu-id="92b23-161">However, always avoid referencing hello `Result` property or calling `Wait` method on a `Task` instance.</span></span> <span data-ttu-id="92b23-162">Cette approche peut entraîner l’épuisement de toothread.</span><span class="sxs-lookup"><span data-stu-id="92b23-162">This approach can lead toothread exhaustion.</span></span>


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a><span data-ttu-id="92b23-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="92b23-163">Next steps</span></span>
<span data-ttu-id="92b23-164">Pour plus d’informations, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="92b23-164">For more information, see hello following resources:</span></span>

<span data-ttu-id="92b23-165">Étant donné qu’Azure Functions utilise Azure App Service, vous devez également connaître les directives d’App Service.</span><span class="sxs-lookup"><span data-stu-id="92b23-165">Because Azure Functions uses Azure App Service, you should also be aware of  App Service guidelines.</span></span>
* [<span data-ttu-id="92b23-166">Modèles et pratiques d’optimisations des performances HTTP</span><span class="sxs-lookup"><span data-stu-id="92b23-166">Patterns and Practices HTTP Performance Optimizations</span></span>](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

