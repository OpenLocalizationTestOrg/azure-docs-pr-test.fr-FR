---
title: "aaaStart et stop tootest de nœuds de cluster Azure microservices | Documents Microsoft"
description: "Découvrez comment toouse erreur injection tootest une application de Service Fabric par le démarrage et arrêt des nœuds de cluster."
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: 
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/12/2017
ms.author: lemai
ms.openlocfilehash: 7d3f5147328e6233a67533fbfb2a525aa5fc060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a><span data-ttu-id="8a3eb-103">En remplaçant hello nœud de démarrage et arrêt nœud API avec hello API de Transition de nœud</span><span class="sxs-lookup"><span data-stu-id="8a3eb-103">Replacing hello Start Node and Stop node APIs with hello Node Transition API</span></span>

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a><span data-ttu-id="8a3eb-104">Que hello nœud d’arrêter et démarrer les API de nœud ?</span><span class="sxs-lookup"><span data-stu-id="8a3eb-104">What do hello Stop Node and Start Node APIs do?</span></span>

<span data-ttu-id="8a3eb-105">Hello arrêter les API de nœud (géré : [StopNodeAsync()][stopnode], PowerShell : [Stop-ServiceFabricNode][stopnodeps]) s’arrête à un nœud de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-105">hello Stop Node API (managed: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) stops a Service Fabric node.</span></span>  <span data-ttu-id="8a3eb-106">Un nœud de Service Fabric est le processus, pas un ordinateur virtuel ou un ordinateur : hello machine virtuelle ou ordinateur sera toujours être en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-106">A Service Fabric node is process, not a VM or machine – hello VM or machine will still be running.</span></span>  <span data-ttu-id="8a3eb-107">Pour rest hello du document de hello « nœud » signifie le nœud Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-107">For hello rest of hello document "node" will mean Service Fabric node.</span></span>  <span data-ttu-id="8a3eb-108">L’arrêt d’un nœud les place dans un *arrêté* état où il n’est pas membre du cluster de hello et ne peut pas héberger les services, instaurant ainsi une *vers le bas* nœud.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-108">Stopping a node puts it into a *stopped* state where it is not a member of hello cluster and cannot host services, thus simulating a *down* node.</span></span>  <span data-ttu-id="8a3eb-109">Cela est utile pour l’injection d’erreurs dans hello système tootest votre application.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-109">This is useful for injecting faults into hello system tootest your application.</span></span>  <span data-ttu-id="8a3eb-110">Hello démarrer les API de nœud (géré : [StartNodeAsync()][startnode], PowerShell : [Start-ServiceFabricNode][startnodeps]]) inverse hello arrêter les API de nœud,  ce qui amène hello nœud tooa retour un état normal.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-110">hello Start Node API (managed: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) reverses hello Stop Node API,  which brings hello node back tooa normal state.</span></span>

## <a name="why-are-we-replacing-these"></a><span data-ttu-id="8a3eb-111">Pourquoi remplaçons-nous ces API ?</span><span class="sxs-lookup"><span data-stu-id="8a3eb-111">Why are we replacing these?</span></span>

<span data-ttu-id="8a3eb-112">Comme décrit précédemment, un *arrêté* nœud de Service Fabric est un nœud a été volontairement à l’aide de hello arrêter les API de nœud.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-112">As described earlier, a *stopped* Service Fabric node is a node intentionally targeted using hello Stop Node API.</span></span>  <span data-ttu-id="8a3eb-113">A *vers le bas* nœud est un nœud est arrêté pour une raison quelconque (par exemple hello ordinateur ou la machine virtuelle est désactivée).</span><span class="sxs-lookup"><span data-stu-id="8a3eb-113">A *down* node is a node that is down for any other reason (e.g. hello VM or machine is off).</span></span>  <span data-ttu-id="8a3eb-114">Avec hello arrêter les API de nœud, système de hello n’expose pas toodifferentiate d’informations entre *arrêté* nœuds et *vers le bas* nœuds.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-114">With hello Stop Node API, hello system does not expose information toodifferentiate between *stopped* nodes and *down* nodes.</span></span>

<span data-ttu-id="8a3eb-115">De plus, certaines erreurs renvoyées par ces API ne sont pas aussi descriptives qu’elles pourraient l’être.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-115">In addition, some errors returned by these APIs are not as descriptive as they could be.</span></span>  <span data-ttu-id="8a3eb-116">Par exemple, appeler hello d’arrêter les API de nœud sur un déjà *arrêté* nœud retournera une erreur de hello *InvalidAddress*.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-116">For example, invoking hello Stop Node API on an already *stopped* node will return hello error *InvalidAddress*.</span></span>  <span data-ttu-id="8a3eb-117">Cette expérience pourrait être améliorée.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-117">This experience could be improved.</span></span>

<span data-ttu-id="8a3eb-118">En outre, durée hello pour qu'un nœud est arrêté est « infinite » jusqu'à hello que démarrer les API de nœud est appelé.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-118">Also, hello duration a node is stopped for is “infinite” until hello Start Node API is invoked.</span></span>  <span data-ttu-id="8a3eb-119">Nous avons découvert que cela pouvait provoquer des problèmes et des erreurs.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-119">We’ve found this can cause problems and may be error-prone.</span></span>  <span data-ttu-id="8a3eb-120">Par exemple, nous avons vu où un utilisateur appelé hello arrêter les API de nœud sur un nœud, puis souvenez plus de problèmes.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-120">For example, we’ve seen problems where a user invoked hello Stop Node API on a node and then forgot about it.</span></span>  <span data-ttu-id="8a3eb-121">Une version ultérieure, il était difficile de savoir si le nœud de hello était *vers le bas* ou *arrêté*.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-121">Later, it was unclear if hello node was *down* or *stopped*.</span></span>


## <a name="introducing-hello-node-transition-apis"></a><span data-ttu-id="8a3eb-122">Présentation de hello API de Transition de nœud</span><span class="sxs-lookup"><span data-stu-id="8a3eb-122">Introducing hello Node Transition APIs</span></span>

<span data-ttu-id="8a3eb-123">Nous avons résolu les problèmes ci-dessus dans un nouvel ensemble d’API.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-123">We’ve addressed these issues above in a new set of APIs.</span></span>  <span data-ttu-id="8a3eb-124">Hello nouvelle Transition de nœud API (géré : [StartNodeTransitionAsync()][snt]) peut être utilisée tootransition un tooa de nœud de Service Fabric *arrêté* état ou tootransition il à partir d’un *arrêté* tooa état normal d’état.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-124">hello new Node Transition API (managed: [StartNodeTransitionAsync()][snt]) may be used tootransition a Service Fabric node tooa *stopped* state, or tootransition it from a *stopped* state tooa normal up state.</span></span>  <span data-ttu-id="8a3eb-125">Veuillez noter que hello « Start » dans le nom hello Hello API ne fait pas référence à un nœud de toostarting.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-125">Please note that hello “Start” in hello name of hello API does not refer toostarting a node.</span></span>  <span data-ttu-id="8a3eb-126">Il fait référence à une opération asynchrone, que le système de hello exécutera tootransition hello nœud tooeither de toobeginning *arrêté* ou en état démarré.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-126">It refers toobeginning an asynchronous operation that hello system will execute tootransition hello node tooeither *stopped* or started state.</span></span>

<span data-ttu-id="8a3eb-127">**Utilisation**</span><span class="sxs-lookup"><span data-stu-id="8a3eb-127">**Usage**</span></span>

<span data-ttu-id="8a3eb-128">Si hello API de Transition de nœud ne lève pas une exception lorsqu’elle est appelée, puis hello système a accepté l’opération asynchrone de hello et il exécutera.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-128">If hello Node Transition API does not throw an exception when invoked, then hello system has accepted hello asynchronous operation, and will execute it.</span></span>  <span data-ttu-id="8a3eb-129">Un appel réussi n’implique pas l’opération de hello est fini de s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-129">A successful call does not imply hello operation is finished yet.</span></span>  <span data-ttu-id="8a3eb-130">tooget plus d’informations sur l’état actuel de hello d’opération hello, appel hello nœud Transition progression API (géré : [GetNodeTransitionProgressAsync()][gntp]) avec le guid hello utilisé lors de l’appel de nœud API de transition pour cette opération.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-130">tooget information about hello current state of hello operation, call hello Node Transition Progress API (managed: [GetNodeTransitionProgressAsync()][gntp]) with hello guid used when invoking Node Transition API for this operation.</span></span>  <span data-ttu-id="8a3eb-131">Hello nœud Transition progression de l’API retourne un objet NodeTransitionProgress.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-131">hello Node Transition Progress API returns an NodeTransitionProgress object.</span></span>  <span data-ttu-id="8a3eb-132">Propriété d’état de cet objet spécifie l’état actuel de hello d’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-132">This object’s State property specifies hello current state of hello operation.</span></span>  <span data-ttu-id="8a3eb-133">Si l’état hello est « Running » puis hello exécution d’une opération.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-133">If hello state is “Running” then hello operation is executing.</span></span>  <span data-ttu-id="8a3eb-134">Si elle est terminée, l’opération de hello est terminé sans erreur.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-134">If it is Completed, hello operation finished without error.</span></span>  <span data-ttu-id="8a3eb-135">Si elle est défaillante, un problème survenu l’exécution d’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-135">If it is Faulted, there was a problem executing hello operation.</span></span>  <span data-ttu-id="8a3eb-136">Exception de la propriété du résultat de Hello propriété indique quel hello émettre était.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-136">hello Result property’s Exception property will indicate what hello issue was.</span></span>  <span data-ttu-id="8a3eb-137">Consultez https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate pour plus d’informations sur la propriété d’état hello et hello « Utilisation de l’exemple » ci-dessous pour des exemples de code.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-137">See https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate for more information about hello State property, and hello “Sample Usage” section below for code examples.</span></span>


<span data-ttu-id="8a3eb-138">**Faisant la distinction entre un nœud arrêté et un nœud en panne** si un nœud est *arrêté* à l’aide de hello nœud Transition API, sortie hello d’une requête de nœud (géré : [GetNodeListAsync()] [ nodequery], PowerShell : [Get-ServiceFabricNode][nodequeryps]) indiquera que ce nœud possède un *IsStopped* valeur de propriété de la valeur true.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-138">**Differentiating between a stopped node and a down node** If a node is *stopped* using hello Node Transition API, hello output of a node query (managed: [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) will show that this node has an *IsStopped* property value of true.</span></span>  <span data-ttu-id="8a3eb-139">Notez cette valeur diffère de la valeur hello hello *NodeStatus* propriété, qui indiquera *vers le bas*.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-139">Note this is different from hello value of hello *NodeStatus* property, which will say *Down*.</span></span>  <span data-ttu-id="8a3eb-140">Si hello *NodeStatus* propriété a la valeur *vers le bas*, mais *IsStopped* est false, le nœud de hello a été pas arrêté à l’aide d’API de Transition de nœud de hello et est  *Vers le bas* en raison d’une autre raison.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-140">If hello *NodeStatus* property has a value of *Down*, but *IsStopped* is false, then hello node was not stopped using hello Node Transition API, and is *Down* due some other reason.</span></span>  <span data-ttu-id="8a3eb-141">Si hello *IsStopped* propriété est true et hello *NodeStatus* propriété *vers le bas*, puis il a été arrêté à l’aide de hello API de Transition de nœud.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-141">If hello *IsStopped* property is true, and hello *NodeStatus* property is *Down*, then it was stopped using hello Node Transition API.</span></span>

<span data-ttu-id="8a3eb-142">Démarrer un *arrêté* nœud à l’aide des API de Transition de nœud de hello retournera il toofunction en tant que membre du cluster de hello normal à nouveau.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-142">Starting a *stopped* node using hello Node Transition API will return it toofunction as a normal member of hello cluster again.</span></span>  <span data-ttu-id="8a3eb-143">Hello sortie de requête de nœud hello API affichera *IsStopped* comme false, et *NodeStatus* en tant que quelque chose qui n’est pas interrompue (par exemple, vers le haut).</span><span class="sxs-lookup"><span data-stu-id="8a3eb-143">hello output of hello node query API will show *IsStopped* as false, and *NodeStatus* as something that is not Down (e.g. Up).</span></span>


<span data-ttu-id="8a3eb-144">**Durée** lors de l’utilisation des API de Transition de nœud de hello toostop un nœud, un des hello paramètres obligatoires *stopNodeDurationInSeconds*, représente hello temps dans le nœud de hello secondes tookeep  *arrêté*.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-144">**Limited Duration** When using hello Node Transition API toostop a node, one of hello required parameters, *stopNodeDurationInSeconds*, represents hello amount of time in seconds tookeep hello node *stopped*.</span></span>  <span data-ttu-id="8a3eb-145">Cette valeur doit être Bonjour plage ayant un minimum de 600 et un maximum de 14400 autorisée.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-145">This value must be in hello allowed range, which has a minimum of 600, and a maximum of 14400.</span></span>  <span data-ttu-id="8a3eb-146">Une fois ce délai expiré, nœud de hello va redémarrer elle-même en état automatiquement.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-146">After this time expires, hello node will restart itself into Up state automatically.</span></span>  <span data-ttu-id="8a3eb-147">Consultez tooSample 1 ci-dessous pour obtenir un exemple d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-147">Refer tooSample 1 below for an example of usage.</span></span>

> [!WARNING]
> <span data-ttu-id="8a3eb-148">Évitez de combiner des API de Transition de nœud et hello nœud d’arrêter et démarrer les API de nœud.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-148">Avoid mixing Node Transition APIs and hello Stop Node and Start Node APIs.</span></span>  <span data-ttu-id="8a3eb-149">recommandation de Hello est trop utiliser hello API de Transition de nœud.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-149">hello recommendation is too use hello Node Transition API only.</span></span>  <span data-ttu-id="8a3eb-150">> Si un nœud a déjà été arrêtée par le biais de hello arrêter les API de nœud, il doit être démarré à l’aide de hello démarrer les API de nœud tout d’abord avant d’utiliser hello > API de Transition de nœud.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-150">> If a node has been already been stopped using hello Stop Node API, it should be started using hello Start Node API first before using hello > Node Transition APIs.</span></span>

> [!WARNING]
> <span data-ttu-id="8a3eb-151">API de Transition nœud plusieurs appels ne peut pas être effectués sur hello même nœud en parallèle.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-151">Multiple Node Transition APIs calls cannot be made on hello same node in parallel.</span></span>  <span data-ttu-id="8a3eb-152">Dans ce cas, hello nœud Transition API sera > lever une FabricException avec une valeur de la propriété ErrorCode de NodeTransitionInProgress.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-152">In such a situation, hello Node Transition API will    > throw a FabricException with an ErrorCode property value of NodeTransitionInProgress.</span></span>  <span data-ttu-id="8a3eb-153">Une fois qu’une transition de nœud sur un nœud spécifique a > été démarré, vous devez patienter jusqu'à ce que l’opération de hello atteigne un état terminal (terminé, Faulted ou ForceCancelled) avant de démarrer un > nouvelle transition sur hello que même nœud.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-153">Once a node transition on a specific node has  > been started, you should wait until hello operation reaches a terminal state (Completed, Faulted, or ForceCancelled) before starting a  > new transition on hello same node.</span></span>  <span data-ttu-id="8a3eb-154">Les appels de transition de nœud parallèles sur des nœuds différents sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-154">Parallel node transition calls on different nodes are allowed.</span></span>


#### <a name="sample-usage"></a><span data-ttu-id="8a3eb-155">Exemple d’utilisation</span><span class="sxs-lookup"><span data-stu-id="8a3eb-155">Sample Usage</span></span>


<span data-ttu-id="8a3eb-156">**Exemple 1** -hello suivant l’exemple hello nœud Transition API toostop un nœud.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-156">**Sample 1** - hello following sample uses hello Node Transition API toostop a node.</span></span>

```csharp
        // Helper function tooget information about a node
        static Node GetNodeInfo(FabricClient fc, string node)
        {
            NodeList n = null;
            while (n == null)
            {
                n = fc.QueryManager.GetNodeListAsync(node).GetAwaiter().GetResult();
                Task.Delay(TimeSpan.FromSeconds(1)).GetAwaiter();
            };

            return n.FirstOrDefault();
        }

        static async Task WaitForStateAsync(FabricClient fc, Guid operationId, TestCommandProgressState targetState)
        {
            NodeTransitionProgress progress = null;

            do
            {
                bool exceptionObserved = false;
                try
                {
                    progress = await fc.TestManager.GetNodeTransitionProgressAsync(operationId, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                    exceptionObserved = true;
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                    exceptionObserved = true;
                }

                if (!exceptionObserved)
                {
                    Console.WriteLine("Current state of operation '{0}': {1}", operationId, progress.State);

                    if (progress.State == TestCommandProgressState.Faulted)
                    {
                        // Inspect hello progress object's Result.Exception.HResult tooget hello error code.
                        Console.WriteLine("'{0}' failed with: {1}, HResult: {2}", operationId, progress.Result.Exception, progress.Result.Exception.HResult);

                        // ...additional logic as required
                    }

                    if (progress.State == targetState)
                    {
                        Console.WriteLine("Target state '{0}' has been reached", targetState);
                        break;
                    }
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (true);
        }

        static async Task StopNodeAsync(FabricClient fc, string nodeName, int durationInSeconds)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            // Create a Guid
            Guid guid = Guid.NewGuid();

            // Create a NodeStopDescription object, which will be used as a parameter into StartNodeTransition
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, durationInSeconds);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStopDescription from above, which will stop hello target node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    // This is retryable
                }
                catch (FabricTransientException fte)
                {
                    // This is retryable
                }

                // Backoff
                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="8a3eb-157">**Exemple 2** - hello suivant l’exemple démarre un *arrêté* nœud.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-157">**Sample 2** - hello following sample starts a *stopped* node.</span></span>  <span data-ttu-id="8a3eb-158">Il utilise des méthodes d’assistance à partir de l’exemple de première hello.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-158">It uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StartNodeAsync(FabricClient fc, string nodeName)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = n.NodeInstanceId;

            // Create a NodeStartDescription object, which will be used as a parameter into StartNodeTransition
            NodeStartDescription description = new NodeStartDescription(guid, n.NodeName, nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="8a3eb-159">**Exemple 3** - hello exemple suivant illustre une utilisation incorrecte.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-159">**Sample 3** - hello following sample shows incorrect usage.</span></span>  <span data-ttu-id="8a3eb-160">Cette utilisation est incorrecte, car hello *stopDurationInSeconds* qu’elle fournit est supérieure à la plage autorisée de hello.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-160">This usage is incorrect because hello *stopDurationInSeconds* it provides is greater than hello allowed range.</span></span>  <span data-ttu-id="8a3eb-161">Depuis StartNodeTransitionAsync() échoue avec une erreur irrécupérable, opération de hello n’a pas été acceptée et API de progression hello ne doit pas être appelée.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-161">Since StartNodeTransitionAsync() will fail with a fatal error, hello operation was not accepted, and hello progress API should not be called.</span></span>  <span data-ttu-id="8a3eb-162">Cet exemple utilise des méthodes d’assistance à partir de l’exemple de première hello.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-162">This sample uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StopNodeWithOutOfRangeDurationAsync(FabricClient fc, string nodeName)
        {
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();

            // Use an out of range value for stopDurationInSeconds toodemonstrate error
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, 99999);

            try
            {
                await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
            }

            catch (FabricException e)
            {
                Console.WriteLine("Caught {0}", e);
                Console.WriteLine("ErrorCode {0}", e.ErrorCode);
                // Output:
                // Caught System.Fabric.FabricException: System.Runtime.InteropServices.COMException (-2147017629)
                // StopDurationInSeconds is out of range ---> System.Runtime.InteropServices.COMException: Exception from HRESULT: 0x80071C63
                // << Parts of exception omitted>>
                //
                // ErrorCode InvalidDuration
            }
        }
```

<span data-ttu-id="8a3eb-163">**Exemple 4** - hello exemple suivant montre les informations d’erreur hello qui seront retournées par hello nœud Transition progression API lors de l’opération hello initiée par hello API de Transition de nœud est acceptée, mais échoue ultérieurement lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-163">**Sample 4** - hello following sample shows hello error information that will be returned from hello Node Transition Progress API when hello operation initiated by hello Node Transition API is accepted, but fails later while executing.</span></span>  <span data-ttu-id="8a3eb-164">Dans les cas de hello, elle échoue car hello nœud Transition API tente toostart un nœud qui n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-164">In hello case, it fails because hello Node Transition API attempts toostart a node that does not exist.</span></span>  <span data-ttu-id="8a3eb-165">Cet exemple utilise des méthodes d’assistance à partir de l’exemple de première hello.</span><span class="sxs-lookup"><span data-stu-id="8a3eb-165">This sample uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StartNodeWithNonexistentNodeAsync(FabricClient fc)
        {
            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = 12345;

            // Intentionally use a nonexistent node
            NodeStartDescription description = new NodeStartDescription(guid, "NonexistentNode", nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hello desired state is reached.  In this case, it will end up in hello Faulted state since hello node does not exist.
            // When StartNodeTransitionProgressAsync()'s returned progress object has a State if Faulted, inspect hello progress object's Result.Exception.HResult tooget hello error code.
            // In this case, it will be NodeNotFound.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Faulted).ConfigureAwait(false);
        }
```

[stopnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StopNodeAsync_System_String_System_Numerics_BigInteger_System_Fabric_CompletionMode_
[stopnodeps]: https://msdn.microsoft.com/library/mt125982.aspx
[startnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StartNodeAsync_System_String_System_Numerics_BigInteger_System_String_System_Int32_System_Fabric_CompletionMode_System_Threading_CancellationToken_
[startnodeps]: https://msdn.microsoft.com/library/mt163520.aspx
[nodequery]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient#System_Fabric_FabricClient_QueryClient_GetNodeListAsync_System_String_
[nodequeryps]: https://docs.microsoft.com/powershell/servicefabric/vlatest/Get-ServiceFabricNode?redirectedfrom=msdn
[snt]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_StartNodeTransitionAsync_System_Fabric_Description_NodeTransitionDescription_System_TimeSpan_System_Threading_CancellationToken_
[gntp]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_GetNodeTransitionProgressAsync_System_Guid_System_TimeSpan_System_Threading_CancellationToken_
