---
title: Bonnes pratiques pour Azure Functions | Microsoft Docs
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
ms.openlocfilehash: 645a5dd16e72619e7c2470ab8f03098f0fa6c7f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="optimize-the-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="76e4c-104">Optimisation des performances et de la fiabilité d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="76e4c-104">Optimize the performance and reliability of Azure Functions</span></span>

<span data-ttu-id="76e4c-105">Cet article fournit des instructions pour améliorer les performances et la fiabilité de vos applications de fonction.</span><span class="sxs-lookup"><span data-stu-id="76e4c-105">This article provides guidance to improve the performance and reliability of your function apps.</span></span> 


## <a name="avoid-long-running-functions"></a><span data-ttu-id="76e4c-106">Évitez les fonctions dont l’exécution prend beaucoup de longtemps</span><span class="sxs-lookup"><span data-stu-id="76e4c-106">Avoid long running functions</span></span>

<span data-ttu-id="76e4c-107">Ces fonctions peuvent provoquer des problèmes de délai d’attente inattendus.</span><span class="sxs-lookup"><span data-stu-id="76e4c-107">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="76e4c-108">Une fonction peut devenir volumineuse en raison d’un nombre important de dépendances Node.js.</span><span class="sxs-lookup"><span data-stu-id="76e4c-108">A function can become large due to many Node.js dependencies.</span></span> <span data-ttu-id="76e4c-109">L’importation des dépendances peut entraîner une augmentation des temps de chargement aboutissant à des délais d’attente inattendus.</span><span class="sxs-lookup"><span data-stu-id="76e4c-109">Importing dependencies can also cause increased load times that result in unexpected timeouts.</span></span> <span data-ttu-id="76e4c-110">Les dépendances sont chargées tant explicitement qu’implicitement.</span><span class="sxs-lookup"><span data-stu-id="76e4c-110">Dependencies are loaded both explicitly and implicitly.</span></span> <span data-ttu-id="76e4c-111">Un module chargé par votre code peut charger ses propres modules supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="76e4c-111">A single module loaded by your code may load its own additional modules.</span></span>  

<span data-ttu-id="76e4c-112">Autant que possible, subdivisez les fonctions volumineuses en ensembles de fonctions plus petits qui fonctionnent ensemble et retournent des réponses rapides.</span><span class="sxs-lookup"><span data-stu-id="76e4c-112">Whenever possible, refactor large functions into smaller function sets that work together and return responses fast.</span></span> <span data-ttu-id="76e4c-113">Par exemple, un webhook ou une fonction de déclenchement HTTP peut nécessiter une réponse avec accusé de réception dans un délai imparti. Il est courant que des webhooks demandent une réponse immédiate.</span><span class="sxs-lookup"><span data-stu-id="76e4c-113">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it is common for webhooks to require an immediate response.</span></span> <span data-ttu-id="76e4c-114">Vous pouvez passer la charge utile du déclencheur HTTP dans une file d’attente en vue de son traitement par une fonction de déclenchement de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="76e4c-114">You can pass the HTTP trigger payload into a queue to be processed by a queue trigger function.</span></span> <span data-ttu-id="76e4c-115">Cette approche vous permet de différer le travail réel et de retourner une réponse immédiate.</span><span class="sxs-lookup"><span data-stu-id="76e4c-115">This approach allows you to defer the actual work and return an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="76e4c-116">Communication entre fonctions</span><span class="sxs-lookup"><span data-stu-id="76e4c-116">Cross function communication</span></span>

<span data-ttu-id="76e4c-117">Quand vous intégrez plusieurs fonctions, une bonne pratique consiste généralement à utiliser des files d’attente de stockage pour la communication entre les fonctions.</span><span class="sxs-lookup"><span data-stu-id="76e4c-117">When integrating multiple functions, it is generally a best practice to use storage queues for cross function communication.</span></span>  <span data-ttu-id="76e4c-118">La principale raison est que les files d’attente de stockage sont plus économiques et beaucoup plus faciles à configurer.</span><span class="sxs-lookup"><span data-stu-id="76e4c-118">The main reason is storage queues are cheaper and much easier to provision.</span></span> 

<span data-ttu-id="76e4c-119">La taille de chaque message d’une file d’attente de stockage est limitée à 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="76e4c-119">Individual messages in a storage queue are limited in size to 64 KB.</span></span> <span data-ttu-id="76e4c-120">Pour transmettre des messages plus volumineux entre les fonctions, vous pouvez utiliser une file d’attente Azure Service Bus, qui prend en charge les tailles de message allant jusqu’à 256 Ko.</span><span class="sxs-lookup"><span data-stu-id="76e4c-120">If you need to pass larger messages between functions, an Azure Service Bus queue could be used to support message sizes up to 256 KB.</span></span>

<span data-ttu-id="76e4c-121">Les rubriques Service Bus sont utiles si vous avez besoin de filtrer les messages avant de les traiter.</span><span class="sxs-lookup"><span data-stu-id="76e4c-121">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="76e4c-122">Les hubs d’événements sont utiles pour prendre en charge les communications de volume élevé.</span><span class="sxs-lookup"><span data-stu-id="76e4c-122">Event hubs are useful to support high volume communications.</span></span>


## <a name="write-functions-to-be-stateless"></a><span data-ttu-id="76e4c-123">Écrire des fonctions sans état</span><span class="sxs-lookup"><span data-stu-id="76e4c-123">Write functions to be stateless</span></span> 

<span data-ttu-id="76e4c-124">Les fonctions doivent être sans état et idempotentes si possible.</span><span class="sxs-lookup"><span data-stu-id="76e4c-124">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="76e4c-125">Associez toutes les informations d’état requises à vos données.</span><span class="sxs-lookup"><span data-stu-id="76e4c-125">Associate any required state information with your data.</span></span> <span data-ttu-id="76e4c-126">Par exemple, une commande en cours de traitement aurait probablement un membre `state` associé.</span><span class="sxs-lookup"><span data-stu-id="76e4c-126">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="76e4c-127">Une fonction peut traiter une commande suivant cet état, tandis que la fonction elle-même reste sans état.</span><span class="sxs-lookup"><span data-stu-id="76e4c-127">A function could process an order based on that state while the function itself remains stateless.</span></span> 

<span data-ttu-id="76e4c-128">Les fonctions idempotentes sont particulièrement recommandées avec les déclencheurs à minuterie.</span><span class="sxs-lookup"><span data-stu-id="76e4c-128">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="76e4c-129">Par exemple, si une tâche doit absolument s’exécuter une fois par jour, écrivez-la de façon à ce qu’elle puisse s’exécuter à n’importe quel moment de la journée avec les mêmes résultats.</span><span class="sxs-lookup"><span data-stu-id="76e4c-129">For example, if you have something that absolutely must run once a day, write it so it can run any time during the day with the same results.</span></span> <span data-ttu-id="76e4c-130">La fonction peut s’arrêter si aucun travail ne doit être effectué au cours d’un jour donné.</span><span class="sxs-lookup"><span data-stu-id="76e4c-130">The function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="76e4c-131">En outre, si une exécution précédente a été interrompue, la prochaine exécution doit reprendre au point d’interruption.</span><span class="sxs-lookup"><span data-stu-id="76e4c-131">Also if a previous run failed to complete, the next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="76e4c-132">Écrire des fonctions défensives</span><span class="sxs-lookup"><span data-stu-id="76e4c-132">Write defensive functions</span></span>

<span data-ttu-id="76e4c-133">Supposons que votre fonction peut être confrontée à une exception à tout moment.</span><span class="sxs-lookup"><span data-stu-id="76e4c-133">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="76e4c-134">Concevez vos fonctions de façon à ce qu’elles puissent reprendre à un point d’échec précédent la prochaine fois qu’elles s’exécutent.</span><span class="sxs-lookup"><span data-stu-id="76e4c-134">Design your functions with the ability to continue from a previous fail point during the next execution.</span></span> <span data-ttu-id="76e4c-135">Imaginez un scénario qui nécessite les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="76e4c-135">Consider a scenario that requires the following actions:</span></span>

1. <span data-ttu-id="76e4c-136">Récupérer 10 000 lignes d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="76e4c-136">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="76e4c-137">Créer un message de file d’attente pour chacune de ces lignes en vue de leur traitement.</span><span class="sxs-lookup"><span data-stu-id="76e4c-137">Create a queue message for each of those rows to process further down the line.</span></span>
 
<span data-ttu-id="76e4c-138">Selon la complexité de votre système, il est possible que des services impliqués en aval se comportent de manière incorrecte, que des pannes réseau se produisent, que des limites de quota soient atteintes, etc. Tous ces facteurs peuvent affecter votre fonction à tout moment.</span><span class="sxs-lookup"><span data-stu-id="76e4c-138">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="76e4c-139">Vous devez concevoir vos fonctions en conséquence.</span><span class="sxs-lookup"><span data-stu-id="76e4c-139">You need to design your functions to be prepared for it.</span></span>

<span data-ttu-id="76e4c-140">Comment votre code réagit-il si une défaillance se produit après l’insertion de 5 000 de ces éléments dans une file d’attente en vue de leur traitement ?</span><span class="sxs-lookup"><span data-stu-id="76e4c-140">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="76e4c-141">Suivez les éléments dans un jeu que vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="76e4c-141">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="76e4c-142">Sinon, vous pouvez les réinsérer la prochaine fois.</span><span class="sxs-lookup"><span data-stu-id="76e4c-142">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="76e4c-143">Cela peut avoir un impact sérieux sur votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="76e4c-143">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="76e4c-144">Si un élément de file d’attente a déjà été traité, permettez à votre fonction d’être une absence d’opération.</span><span class="sxs-lookup"><span data-stu-id="76e4c-144">If a queue item was already processed, allow your function to be a no-op.</span></span>

<span data-ttu-id="76e4c-145">Tirez parti des mesures défensives déjà fournies pour les composants que vous utilisez dans la plateforme Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="76e4c-145">Take advantage of defensive measures already provided for components you use in the Azure Functions platform.</span></span> <span data-ttu-id="76e4c-146">Par exemple, consultez **Gestion des messages de file d’attente incohérents** dans la documentation sur les [déclencheurs de file d’attente Stockage Azure](functions-bindings-storage-queue.md#trigger).</span><span class="sxs-lookup"><span data-stu-id="76e4c-146">For example, see **Handling poison queue messages** in the documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-the-same-function-app"></a><span data-ttu-id="76e4c-147">Ne pas mélanger code de test et code de production dans la même application de fonction</span><span class="sxs-lookup"><span data-stu-id="76e4c-147">Don't mix test and production code in the same function app</span></span>

<span data-ttu-id="76e4c-148">Les fonctions d’une application de fonction partagent des ressources.</span><span class="sxs-lookup"><span data-stu-id="76e4c-148">Functions within a function app share resources.</span></span> <span data-ttu-id="76e4c-149">Par exemple, la mémoire est partagée.</span><span class="sxs-lookup"><span data-stu-id="76e4c-149">For example, memory is shared.</span></span> <span data-ttu-id="76e4c-150">Si vous utilisez une application de fonction en production, n’y ajoutez pas de ressources et de fonctions de test.</span><span class="sxs-lookup"><span data-stu-id="76e4c-150">If you're using a function app in production, don't add test-related functions and resources to it.</span></span> <span data-ttu-id="76e4c-151">Cela peut entraîner une surcharge inattendue pendant l’exécution du code de production.</span><span class="sxs-lookup"><span data-stu-id="76e4c-151">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="76e4c-152">Soyez attentif à ce que vous chargez dans vos applications de fonction en production.</span><span class="sxs-lookup"><span data-stu-id="76e4c-152">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="76e4c-153">La mémoire moyenne est calculée pour chaque fonction au sein de l’application.</span><span class="sxs-lookup"><span data-stu-id="76e4c-153">Memory is averaged across each function in the app.</span></span>

<span data-ttu-id="76e4c-154">Si un assembly partagé est référencé dans plusieurs fonctions .Net, placez-le dans un dossier partagé commun.</span><span class="sxs-lookup"><span data-stu-id="76e4c-154">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="76e4c-155">Référencez l’assembly avec une instruction similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="76e4c-155">Reference the assembly with a statement similar to the following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="76e4c-156">Sinon, il est facile de déployer accidentellement plusieurs versions de test du même binaire qui se comportent différemment d’une fonction à l’autre.</span><span class="sxs-lookup"><span data-stu-id="76e4c-156">Otherwise, it is easy to accidentally deploy multiple test versions of the same binary that behave differently between functions.</span></span>

<span data-ttu-id="76e4c-157">N’utilisez pas de journalisation détaillée dans le code de production.</span><span class="sxs-lookup"><span data-stu-id="76e4c-157">Don't use verbose logging in production code.</span></span> <span data-ttu-id="76e4c-158">Cela affecte les performances.</span><span class="sxs-lookup"><span data-stu-id="76e4c-158">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-blocking-calls"></a><span data-ttu-id="76e4c-159">Utiliser du code asynchrone tout en évitant de bloquer les appels</span><span class="sxs-lookup"><span data-stu-id="76e4c-159">Use async code but avoid blocking calls</span></span>

<span data-ttu-id="76e4c-160">La programmation asynchrone est une pratique recommandée.</span><span class="sxs-lookup"><span data-stu-id="76e4c-160">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="76e4c-161">Toutefois, évitez toujours de référencer la propriété `Result` ou d’appeler la méthode `Wait` sur une instance `Task`.</span><span class="sxs-lookup"><span data-stu-id="76e4c-161">However, always avoid referencing the `Result` property or calling `Wait` method on a `Task` instance.</span></span> <span data-ttu-id="76e4c-162">Cette approche peut mener à un épuisement des threads.</span><span class="sxs-lookup"><span data-stu-id="76e4c-162">This approach can lead to thread exhaustion.</span></span>


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a><span data-ttu-id="76e4c-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="76e4c-163">Next steps</span></span>
<span data-ttu-id="76e4c-164">Pour plus d’informations, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="76e4c-164">For more information, see the following resources:</span></span>

<span data-ttu-id="76e4c-165">Étant donné qu’Azure Functions utilise Azure App Service, vous devez également connaître les directives d’App Service.</span><span class="sxs-lookup"><span data-stu-id="76e4c-165">Because Azure Functions uses Azure App Service, you should also be aware of  App Service guidelines.</span></span>
* [<span data-ttu-id="76e4c-166">Modèles et pratiques d’optimisations des performances HTTP</span><span class="sxs-lookup"><span data-stu-id="76e4c-166">Patterns and Practices HTTP Performance Optimizations</span></span>](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

